# 🧠 Machine Learning Integration

The core capability of Civic Resolve is automated ticket triage and categorization. By processing text descriptions, the system accurately routes issues to specific department wings while filtering out spam or noise.

---

## 🔬 ML Pipeline Overview

The system processes complaint texts using a two-stage scikit-learn pipeline:

1.  **TF-IDF Vectorization (`vectorizer.pkl`)**:
    - Converts raw complaint descriptions into sparse feature matrices.
    - Utilizes a unigram and bigram representation (`ngram_range=(1, 2)`) to capture both single key terms (e.g., *"leak"*, *"fuse"*) and structural context (e.g., *"not working"*, *"water pipe"*).
2.  **Multinomial Naive Bayes Classifier (`model.pkl`)**:
    - A probabilistic classifier suited for discrete features (like word counts and TF-IDF frequencies).
    - It computes the probability distribution over all department categories (wings) and assigns the class with the highest probability.

---

## 🛡️ Routing Decisions & Thresholds

To handle low-quality, incomplete, or ambiguous complaints, the routing logic in `app.py` enforces three distinct decision boundaries based on text length and classification confidence:

### 1. Spam Filtering (Heuristic)
If a description has less than 10 characters:
*   **Result**: Instantly flagged as `Spam`.
*   **Routing**: The internal routing key (`true_wing`) is set to `General`.

### 2. High-Uncertainty / Noise Filter
If the maximum prediction probability is lower than **10%** ($P < 0.10$):
*   **Result**: Flagged as `Spam` due to extremely low confidence.
*   **Routing**: The internal routing key (`true_wing`) is set to `General`.

### 3. Ambiguity / Medium-Uncertainty Filter
If the maximum prediction probability falls between **10% and 25%** ($0.10 \le P < 0.25$):
*   **Result**: Flagged as `Uncertain`.
*   **Routing**: The internal routing key (`true_wing`) is set to `General`, alerting all available staff to review and categorize it manually.

### 4. High-Confidence Route
If the maximum prediction probability is **25% or higher** ($P \ge 0.25$):
*   **Result**: High confidence route.
*   **Routing**: The internal routing key (`true_wing`) and public category (`wing`) are set to the model's predicted department (e.g., `Electrical`, `Plumbing`).

---

## 💻 Python Prediction Implementation

Below is the routing logic implemented in `project/app.py`:

```python
def predict_wing(description):
    if not model or not vectorizer:
        return "Unassigned", False, True
    try:
        # Vectorize input text
        vec = vectorizer.transform([description])
        
        # Heuristic Spam Check: Too short
        if len(description.strip()) < 10:
            return "Spam", True, False
            
        # Get probability distributions
        probs = model.predict_proba(vec)[0]
        max_prob = np.max(probs)
        prediction = model.classes_[np.argmax(probs)]
        
        # Uncertainty thresholds
        is_uncertain = max_prob < 0.25
        is_spam = max_prob < 0.1
        
        return prediction, is_spam, is_uncertain
    except Exception as e:
        print(f"Prediction error: {e}")
        return "Unassigned", False, True
```

---

## 🔄 Retraining & Calibration

When new training patterns emerge or routing performance needs adjustment:

1.  **Update Dataset**: Append correctly labeled complaint records to `project/data/complaints.csv`.
2.  **Run Training**: Open `project/model.ipynb` and run the training pipeline cells. This will fit a new `TfidfVectorizer` and `MultinomialNB` model.
3.  **Deploy**: The notebook outputs new `model.pkl` and `vectorizer.pkl` binaries directly in the project root. Restart the Flask app to load the new weights.

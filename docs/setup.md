# 🛠️ Setup & Installation Guide

Follow this guide to configure and run the **Civic Resolve** platform on your local development environment.

---

## 📋 Prerequisites

Before proceeding, ensure you have the following software installed:

*   **Python**: Version `3.9` or higher is required.
*   **Database**: MySQL Server (v8.0+ recommended) running locally.
*   **Package Manager**: `pip` (Python Package Installer).

---

## 🚀 Step-by-Step Installation

### 1. Clone the Repository
Clone the codebase and navigate to the project directory:
```bash
git clone https://github.com/MukundXplore/Civic-Resolve-Intelligent-Complaint-Routing.git
cd Civic-Resolve-Intelligent-Complaint-Routing/project
```

### 2. Install Dependencies
Install all required libraries (Flask, NumPy, Pandas, Scikit-learn, and the MySQL database connector):
```bash
pip install -r requirements.txt
```

> [!NOTE]
> If a `requirements.txt` is not present, you can install the core packages manually:
> ```bash
> pip install flask pandas scikit-learn mysql-connector-python numpy
> ```

---

## 🗄️ Database Configuration

### 1. Enable Local Infile Loading
The setup scripts import seed CSV data directly into MySQL. This requires the local data loading feature to be enabled.

1. Open your MySQL client/terminal and run:
   ```sql
   SET GLOBAL local_infile = 1;
   ```

2. When connecting to MySQL, ensure the client enables local infile loading.

### 2. Run Database Initializations
Execute the SQL initialization scripts located in `project/data/sql/` in the following sequence:

1.  **`users.sql`**: Creates the `Users` table and loads the default student/staff profiles.
2.  **`complaints.sql`**: Creates the `Complaints` table structure.
3.  **`syslogs.sql`**: Prepares the system action log table.

> [!IMPORTANT]
> In `users.sql` and `complaints.sql`, replace the placeholder `[COMPLETE-PATH]` with the absolute system paths to `project/data/users.csv` and `project/data/complaints.csv` respectively.

### 3. Update Application Credentials

Update the `dbconfig` credentials in `project/app.py` on line 8 to match your MySQL database settings.

Alternatively (recommended for security), copy `project/.env.example` to `project/.env` and update the database credentials and secret key:
```env
DB_USER=root
DB_PASSWORD=your_password
DB_HOST=127.0.0.1
DB_NAME=civic_resolve
SECRET_KEY=your-secret-key
```
Flask will automatically load configurations from the `.env` file.

---

## 💻 Running the Application

### 1. Start the Flask Server
Run the application script:
```bash
python app.py
```

### 2. Access the Application
- Open your browser and navigate to: **`http://localhost:5000`**
- To log in, choose the appropriate role and enter credentials from `project/data/users.csv` (e.g., sample Student ID and Password).

---

## 🔍 Troubleshooting

> [!WARNING]
> **Database Connection Error**:
> Double-check that your MySQL service is running (`net start mysql` on Windows) and that your password/username in `app.py` matches exactly.

> [!TIP]
> **Model Loading Issues**:
> If you see a warning about ML models not loading, or if the auto-assignment defaults to General, make sure `model.pkl` and `vectorizer.pkl` exist in the `project/` root. If they are missing, open `project/model.ipynb` and run all cells to retrain the model and save the pickle files.

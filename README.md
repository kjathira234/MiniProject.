# FinWise – Personal Finance Management System

## Introduction

FinWise is a Django web application for recording personal income, expenses, and loan information. It provides a dashboard and monthly financial analysis, including a machine-learning prediction of financial health.

## Project Objectives

- Provide a single place to maintain personal income, expense, and loan records.
- Help users review spending, savings, and monthly EMI commitments.
- Use financial and profile information to estimate a user's financial health.
- Present recommendations and retain a history of previous predictions.

## Main Features

- **Registration and login:** Create an account and sign in using Django authentication. Registration also collects profile information used for analysis.
- **Income tracking:** Add, edit, and delete income records, including source, amount, and date.
- **Expense tracking:** Add, edit, and delete categorized expense records, including amount and date.
- **Loan and EMI management:** Record loan type, amount, monthly EMI, and date; update or remove loan records.
- **Dashboard:** Review totals for income, expenses, savings, loans, and EMIs, along with financial ratios.
- **Financial analysis:** Analyze a selected month of a user's financial records and show a health prediction, recommendations, and risk-management suggestions.
- **Prediction history:** View previously generated financial health predictions.

## Technologies Used

- Python
- Django
- HTML, CSS, and JavaScript (used in the Django templates)
- SQLite
- Machine-learning model loaded from a saved scikit-learn-compatible model file
- pandas and joblib for preparing prediction input and loading the model

## Machine-Learning Prediction

The application sends profile and monthly financial data to the saved model in `models/best_financial_status_model.pkl`. Inputs include age, gender, education level, employment status, income, expenses, savings, loan and EMI amounts, and financial ratios. The model's result is displayed as **Good**, **Average**, or **Poor** when it returns one of those classes. FinWise also generates recommendations and stores each result in the prediction history.

The model file is required for predictions. The application handles a missing or unloadable model, but financial analysis will not be available until the model can be loaded.

## Project Structure

```text
personal finance/
├── manage.py
├── db.sqlite3
├── models/
│   ├── best_financial_status_model.pkl
│   └── financial_status_features.pkl
├── selected_features.pkl
├── financeapp/
│   ├── admin.py
│   ├── apps.py
│   ├── forms.py
│   ├── models.py
│   ├── risk_utils.py
│   ├── tests.py
│   ├── views.py
│   ├── migrations/
│   └── templates/
├── personalfinance/
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
├── templates/
│   ├── home.html
│   ├── login.html
│   ├── registration.html
│   ├── dashboard.html
│   ├── financial_details.html
│   ├── financial_analysis.html
│   ├── prediction_history.html
│   ├── edit_income.html
│   ├── edit_expense.html
│   └── edit_loan.html
├── graphs/  (currently empty)
└── *.png    (saved analysis and model visualizations)
```

The application templates are stored in the root `templates/` directory. Django settings point SQLite at `db.sqlite3` in the project root. There is no dependency manifest in the project, so the installation instructions below list the Python packages imported by the application and its model-loading code.

## Installation on Windows

Use Python 3.13 or another Python version compatible with the installed Django and scikit-learn packages.

1. Open PowerShell in the project root.
2. Create and activate a virtual environment:

   ```powershell
   py -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

   If PowerShell activation is not available, use Command Prompt instead:

   ```bat
   .venv\Scripts\activate.bat
   ```

3. Install the required packages:

   ```powershell
   python -m pip install Django pandas joblib scikit-learn
   ```

## Run the Django Application

With the virtual environment activated and the current directory set to the project root, run database migrations and start Django's development server:

```powershell
python manage.py migrate
python manage.py runserver
```

Open `http://127.0.0.1:8000/` in a browser. Register an account, sign in, and add financial records before requesting an analysis. The analysis uses profile information collected during registration. The development server is intended for local development, not production deployment.

## Future Enhancements

- Add a dependency file with tested package versions.
- Add automated tests for authentication, financial record management, and prediction behavior.
- Improve data visualizations and provide longer-term income and expense trends.
- Support exporting financial records and analysis reports.
- Add model evaluation and retraining workflows with documented training data and metrics.
- Prepare production deployment settings, including secure secret management and debug settings.

## Author

**Author:** [Your Name]

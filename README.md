An enterprise-grade Clinical Decision Support System (CDSS) engineered to predict 30-day patient readmission risks in real time. Rather than relying on a static analysis notebook, this repository implements a complete full-stack machine learning architecture: a high-performance FastAPI microservice backend serving a fine-tuned XGBoost engine paired with a stateful Streamlit web application tailored for healthcare environments. The Real-World ProblemUnplanned 30-day hospital readmissions strain clinical capacity, impact patient recovery runways, and incur massive financial penalties for hospital networks from healthcare regulators. In fast-paced clinical settings, manual data aggregation across fragmented electronic health records (EHR) makes it exceptionally difficult to identify subtle patient vulnerability trends before discharge signature.This system acts as an automated, intelligent second pair of eyes at the point of care. It ingests active metrics along with historical patient utilization data, instantly extracts engineered interaction parameters, and triggers proactive clinical guidance if a patient profile crosses an operational risk ceiling threshold of 38%.⚙️ Key Technical FeaturesHigh-Performance FastAPI Layer: Implements a lean, asynchronous API utilizing a structural validation pipeline powered by Pydantic. Includes built-in engine health check interfaces (/health).Robust 75-Feature Schema Alignment: Automatically cleanses input parameters and maps them onto the exact structural dimensions expected by the underlying machine learning model, handling flag values, categorical midpoints, and schema edge cases flawlessly.On-the-Fly Feature Engineering: The microservice backend dynamically computes complex interaction parameters during the live inference lifecycle, including total visits Aggregation of past year outpatient, emergency, and inpatient encounters.med_to_procedure_ratio: Balancing medication intensity against direct clinical interventions.high_utilizer_sick: A binary operational flag identifying multi-admission historical patterns.Stateful Domain-Specific UI: Built utilizing Streamlit forms control to manage runtime execution loops effectively, keeping the input state predictable before running network operations. Includes interactive pre-configured EHR templates for instant simulation.🛠️ System Architecture[Clinical Staff Interface] (Streamlit Frontend :8501)
            │
            ▼ (JSON Payload via HTTP POST)
[Enterprise Inference Gateway] (FastAPI Backend :8000)
            │
            ├─► Feature Engineering & 75-Schema Realignment
            ├─► XGBoost Binary Classifier Evaluation
            │
            ▼ (Structured Risk Analytics Response)
[Real-Time Visualization & Automated Alert Matrix]
Installation & Local Deployment GuidePrerequisitesPython 3.10 or higher installed on your local operating system.1. Clone & Set Up the RepositoryBashgit clone https://github.com/your-username/hospital-readmission-ai.git
cd hospital-readmission-ai
2. Configure Virtual Environment & DependenciesCreate your local isolated environment, activate it, and install all required production and infrastructure libraries:Bash# Create Virtual Environment
python -m venv venv

# Activate Environment (Windows CMD)
venv\Scripts\activate

# Install Required Dependencies
pip install fastapi uvicorn streamlit xgboost pandas numpy joblib requests
3. Initialize the Backend Inference MicroserviceOpen a dedicated terminal window, ensure your virtual environment is active, and launch the Uvicorn application server:Bash# Navigate to the project source root directory
cd src

# Launch FastAPI microservice with automated reload tracking
python -m uvicorn api.main:app --reload --port 8000
Verify the server initialization logs indicate:  Success: XGBoost Model Binary loaded securely into API memory layer.4. Boot Up the Clinical Dashboard FrontendOpen a new, separate terminal window, reactivate the local environment, and execute the Streamlit runtime command:Bashpython -m streamlit run hospital-readmission-ai/src/app.py
Your default browser context will automatically pop open to http://localhost:8501.🧪 Simulation & Validation ScenariosTo test the system's runtime validation pipelines, toggle the dashboard variables to match these target profiles:Clinical AttributeScenario A: Low-Risk RecoveryScenario B: High-Risk Multi-MorbidityEncounter Duration (Days)29Lab Procedures Executed1676Specialized Procedures02Formulary Medications838Prior Inpatient Admissions04Total Diagnoses Entered29Patient Age Bracket30-4070-80🎯 System Output Status🟢 LOW RISK (~2.50%)🚨 HIGH RISK (~97.50%)📂 Project Directory LayoutPlaintexthospital-readmission-ai/
├── models/
│   └── xgboost_elite_80.pkl       # Serialized fine-tuned XGBoost model artifact
├── src/
│   ├── api/
│   │   └── main.py                # FastAPI microservice logic & feature engineering pipeline
│   └── app.py                     # Stateful Streamlit user interface dashboard logic
├── README.md                      # Production system documentation
└── requirements.txt               # Main runtime framework dependencies list
🤝 Contact & FeedbackIf you have questions about the real-time feature engineering pipeline, integration configurations, or deployment practices, feel free to open an issue or connect directly on LinkedIn.

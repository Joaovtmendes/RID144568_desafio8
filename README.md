#  Data Processing Pipeline with Apache Airflow

This repository contains a data pipeline orchestrated by Apache Airflow, developed to transform raw data into valuable insights. The pipeline follows a layered architecture with Bronze, Silver, and Gold stages, performing data cleaning, transformation, and aggregation.

##  Technologies Used
- **Apache Airflow:** Task orchestration and workflow management.
- **Docker:** Airflow containerization for a controlled and portable environment.
- **Pandas:** Data manipulation and transformation.

##  Project Structure
The project consists of the following main folders and files:

```console
├── dags/
│   └── data_pipeline_dag.py   # DAG definition orchestrating the data pipeline
│── data/
│   ├── raw_data.csv           # Raw data file
│   ├── bronze/                # Loaded data stored without modifications
│   ├── silver/                # Cleaned and prepared data for analysis
│   └── gold/                  # Transformed data ready for strategic decisions
├── logs/                      # Folder to store Airflow logs
├── plugins/                   # Folder for Airflow plugins
├── docker-compose.yml         # File to initialize Airflow via Docker
└── README.md                  # This file
```

##  How to Run the Project
### 1. Environment Setup
To run the pipeline locally, you need Docker installed. If not installed, download and set up Docker Desktop.

### 2. Start Apache Airflow with Docker
After cloning this repository, navigate to the project folder and execute the following commands in the terminal to start Apache Airflow via Docker:

```console
docker-compose up -d
```

This will start the necessary services for Apache Airflow. You can access the Airflow Webserver at: [http://localhost:8080](http://localhost:8080).

### 3. Access the Airflow Web Interface
- Open your browser and go to [http://localhost:8080](http://localhost:8080).
- The default login credentials are:
  - Username: `admin`
  - Password: `admin`

### 4. Run the DAG
After accessing the Airflow interface, locate the DAG `data_pipeline_dag` in the list of DAGs and click to run it.

### 5. Check the Results
The processing results can be found in the `bronze`, `silver`, and `gold` folders within the `data` directory. Each pipeline stage saves the transformed data in the corresponding folder.

##  Transformations Performed
### 1. Data Loading (Bronze Layer)
Raw data from the `data/raw_data.csv` file is loaded into the Bronze layer without transformations. The original file contains user data with some inconsistencies that are addressed in subsequent steps.

### 2. Data Cleaning (Silver Layer)
In the Silver layer, the following cleaning and validation processes are performed:
- **Removal of Invalid Records:** Records with null mandatory fields, such as name, email, and date of birth, are removed.
- **Email Correction:** If a user's email does not contain the `@` character, it is corrected by replacing the `example` part with `@example` to ensure validity.
- **Age Calculation:** Users' ages are calculated based on their date of birth and the current day.

### 3. Data Transformation (Gold Layer)
In the Gold layer, transformations include:
- **Aggregation by Age Group and Status:** Data is aggregated by age group (0-10, 11-20, 21-30 years, etc.) and status (active or inactive), enabling a more detailed analysis of user profiles.
- **Result:** The result is stored in the `gold/` folder, ready for deeper analyses and strategic decisions.

📚 References
- [Apache Airflow Documentation](https://airflow.apache.org/docs/)
- [Docker Documentation](https://docs.docker.com/)
- [Pandas Documentation](https://pandas.pydata.org/docs/)


```python

# Imports

# Functions

# default_args

# Dataset objects

with DAG(...) as dag:

    # Operators

    # TaskGroup

    # Dependencies
```


```python
# Standard library
import csv                                                    # Read CSV files
from datetime import datetime, timedelta                      # Standard Python imports


# Third-party libraries
from airflow import DAG                                       # Airflow DAG class
from airflow.models import Variable                           # Read Airflow Variables
from airflow.datasets import Dataset                          # Dataset scheduling
from airflow.hooks.base import BaseHook                       # Read Airflow Connections
from airflow.operators.bash import BashOperator               # Execute Bash commands
from airflow.operators.python import PythonOperator           # Execute Python functions
from airflow.operators.branch import BranchPythonOperator          # Branch execution
from airflow.operators.empty import EmptyOperator                  # Empty/Dummy task
from airflow.operators.python import ShortCircuitOperator          # Skip downstream tasks
from airflow.operators.trigger_dagrun import TriggerDagRunOperator # Trigger another DAG
from airflow.sensors.external_task import ExternalTaskSensor       # Wait for another DAG
from airflow.utils.trigger_rule import TriggerRule                # Trigger rules
from airflow.utils.task_group import TaskGroup                # Group related tasks

# Local application imports
from my_project.utils import helper


customer_dataset = Dataset("gs://company-data/customer/customer.csv") # IP: Shared dataset between DAGs
    

default_args = {
    "owner": "airflow",                                 # IP: Owner of the DAG/tasks
    "depends_on_past": False,                           # IP: Current task run doesn't depend on the previous run
    "email": ["airflow@example.com"],                   # Email recipients for task notifications
    "email_on_failure": True,                           # IP: Send email if a task fails
    "email_on_retry": False,                            # Don't send email when a task is retried
    "retries": 3,                                       # IP: Retry a failed task up to 3 times
    "retry_delay": timedelta(minutes=5),                # IP: Wait 5 minutes before each retry
}



    
    

def start_task(**context):
    """Print execution details and push file path to XCom."""

    execution_date = context["execution_date"]                # IP: Logical execution time
    ds = context["ds"]                                        # IP: Execution date (YYYY-MM-DD)

    print(f"Execution Date : {execution_date}")
    print(f"DS             : {ds}")

    environment = Variable.get(                               # IP: Read Airflow Variable
        "environment",
        default_var="dev",
    )

    print(f"Environment    : {environment}")

    context["ti"].xcom_push(                                  # IP: Push value to XCom
        key="file_path",
        value="/opt/airflow/data/employees.csv",
    )


def process_csv_task(**context):
    """Read CSV using file path received from XCom."""

    task_instance = context["ti"]

    csv_file = task_instance.xcom_pull(                       # IP: Read value from XCom
        task_ids="start_task",
        key="file_path",
    )

    print(f"CSV File : {csv_file}")

    connection = BaseHook.get_connection(                     # IP: Read Airflow Connection
        "postgres_default"
    )

    print(f"Host     : {connection.host}")
    print(f"Schema   : {connection.schema}")
    print(f"Username : {connection.login}")

    row_count = 0

    with open(csv_file, mode="r", encoding="utf-8") as file:
        reader = csv.DictReader(file)

        for row in reader:
            print(row)
            row_count += 1

    print(f"Total Rows : {row_count}")

    task_instance.xcom_push(                                  # IP: Push processed result
        key="row_count",
        value=row_count,
    )


def end_task(**context):
    """Read processed data from XCom."""

    task_instance = context["ti"]

    total_rows = task_instance.xcom_pull(                     # IP: Pull value from previous task
        task_ids="process_csv",
        key="row_count",
    )

    print("CSV processed successfully.")
    print(f"Rows Processed : {total_rows}")





def choose_processing_type(**context):
    """Choose processing path based on CSV row count."""

    total_rows = context["ti"].xcom_pull(                         # IP: Read value from XCom
        task_ids="process_csv",
        key="row_count",
    )

    if total_rows >= 100:
        return "large_file_processing"

    return "small_file_processing"


def validate_csv(**context):
    """Allow downstream tasks only when rows are available."""

    total_rows = context["ti"].xcom_pull(
        task_ids="process_csv",
        key="row_count",
    )

    return total_rows > 0                                        # IP: False skips downstream tasks


def print_runtime_config(**context):
    """Print runtime configuration."""

    dag_conf = context["dag_run"].conf or {}              # IP: Handle empty dag_run.conf
    
    country = dag_conf.get(
        "country",
        "INDIA",
    )

    print(f"Country : {country}")
    

def on_success(context):
    """Executed when a task succeeds."""

    print(f"Task '{context['task_instance'].task_id}' completed successfully.")


def on_failure(context):
    """Executed when a task fails."""

    print(f"Task '{context['task_instance'].task_id}' failed.")
    


with DAG(
    dag_id="daily_csv_processing",                      # IP: Unique identifier of the DAG
    description="Sample Airflow interview DAG",         # IP: Description shown in Airflow UI
    default_args=default_args,                          # IP: Common task-level arguments
    start_date=datetime(2025, 1, 1),                    # IP: Date from which scheduling starts
    schedule="0 6 * * *",                               # IP: Runs every day at 6 AM (Cron expression)
    catchup=False,                                      # IP: Skip historical DAG runs
    max_active_runs=1,                                  # IP: Allow only one active DAG run at a time
    max_active_tasks=5,                                 # IP: Maximum concurrent tasks in this DAG
    render_template_as_native_obj=True,                 # IP: Render Jinja templates as native Python objects
    default_view="graph",                               # IP: Default view in Airflow UI
    tags=["interview", "python", "xcom"],               # IP: Categorize DAGs in the Airflow UI
    is_paused_upon_creation=True,                       # DAG remains paused after creation
    dagrun_timeout=timedelta(hours=2),                  # Maximum allowed time for a DAG run
    template_searchpath=["/opt/airflow/sql"],           # Directory for SQL/Jinja templates
    concurrency=10,                                     # (Airflow 1.x / deprecated in newer versions)
    params={"env": "dev"},                              # IP: Default parameters accessible in templates
) as dag:
    
    
    start = PythonOperator(
        task_id="start_task",
        python_callable=start_task,
    )
    
    process_csv = PythonOperator(
        task_id="process_csv",
        python_callable=process_csv_task,
    )
    
    end = PythonOperator(
        task_id="end_task",
        python_callable=end_task,
    )
    
    branch = BranchPythonOperator(
        task_id="branch_task",
        python_callable=choose_processing_type,
    )
    
    
    large_file_processing = PythonOperator(
        task_id="large_file_processing",
        python_callable=lambda: print("Processing large CSV file."),
        retries=5,                                                   # IP: Override DAG retry count
        execution_timeout=timedelta(minutes=10),                     # IP: Maximum task runtime
        sla=timedelta(minutes=5),                                    # IP: SLA monitoring
    )
    
    
    small_file_processing = PythonOperator(
        task_id="small_file_processing",
        python_callable=lambda: print("Processing small CSV file."),
    )
    
    
    validation = ShortCircuitOperator(
        task_id="validate_csv",
        python_callable=validate_csv,
    )
    
    
    trigger_reporting_dag = TriggerDagRunOperator(
        task_id="trigger_reporting_dag",
        trigger_dag_id="daily_reporting_pipeline",
        conf={
            "source": "employee_pipeline",
            "run_date": "{{ ds }}",                                  # IP: Jinja template
            "execution_time": "{{ ts }}",
        },
        wait_for_completion=False,                                   # IP: Trigger asynchronously
    )
    
    
    wait_for_customer_pipeline = ExternalTaskSensor(
        task_id="wait_for_customer_pipeline",
        external_dag_id="customer_pipeline",
        external_task_id="load_customer_table",
        allowed_states=["success"],
        failed_states=["failed"],
        mode="reschedule",                                           # IP: Release worker slot while waiting
        poke_interval=60,                                            # IP: Check every 60 seconds
        timeout=1800,                                                # IP: Stop waiting after 30 minutes
    )
    
    print_configuration = PythonOperator(
        task_id="print_configuration",
        python_callable=print_runtime_config,
    )
    
    
    pipeline_completed = EmptyOperator(
        task_id="pipeline_completed",
        trigger_rule=TriggerRule.NONE_FAILED_MIN_ONE_SUCCESS,        # IP: Continue if one branch succeeds
    )
    
    
    
    with TaskGroup(                                               # IP: Organize tasks in Graph View
        group_id="data_validation"
    ) as validation_group:
    
        validate_schema = BashOperator(
            task_id="validate_schema",
            bash_command="echo 'Schema validation completed.'",
        )
    
        validate_duplicates = BashOperator(
            task_id="validate_duplicates",
            bash_command="echo 'Duplicate validation completed.'",
        )
    
        validate_nulls = BashOperator(
            task_id="validate_nulls",
            bash_command="echo 'Null validation completed.'",
        )
    
        validate_schema >> validate_duplicates >> validate_nulls
    
    
    load_to_database = BashOperator(
        task_id="load_to_database",
        bash_command="echo 'Loading data into database.'",
        pool="database_pool",                                     # IP: Limit concurrent database tasks
        pool_slots=1,                                             # IP: Consume one pool slot
        on_success_callback=on_success,                           # IP: Success callback
        on_failure_callback=on_failure,                           # IP: Failure callback
    )
    
    
    generate_report = BashOperator(
        task_id="generate_report",
        bash_command="echo 'Generating report.'",
        queue="reporting_queue",                                  # IP: Execute on specific worker queue
    )
    
    
    send_notification = BashOperator(
        task_id="send_notification",
        bash_command="echo 'Notification sent.'",
        priority_weight=10,                                       # IP: Higher priority during scheduling
    )
    
    
    publish_customer_dataset = BashOperator(
        task_id="publish_customer_dataset",
        bash_command="echo 'Customer dataset published.'",
        outlets=[customer_dataset],                               # IP: Mark dataset as updated
    )
    
    
    publish_customer_dataset.doc_md = """
    ### Publish Customer Dataset
    
    Publishes the latest customer dataset.
    
    This dataset can trigger downstream Dataset scheduled DAGs.
    """
    
    start >> process_csv                                      # IP: Task dependency using >>
    process_csv >> end                                        # IP: Equivalent to end << process_csv
    
    
    end >> validation
    
    validation >> branch
    
    branch >> large_file_processing
    branch >> small_file_processing
    
    [large_file_processing, small_file_processing] >> pipeline_completed
    
    pipeline_completed >> trigger_reporting_dag
    
    trigger_reporting_dag >> wait_for_customer_pipeline
    
    wait_for_customer_pipeline >> print_configuration
    
    print_configuration >> validation_group
    
    validation_group >> load_to_database
    
    load_to_database >> generate_report
    
    generate_report >> send_notification
    
    send_notification >> publish_customer_dataset
    ```

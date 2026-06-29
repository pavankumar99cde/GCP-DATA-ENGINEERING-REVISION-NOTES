|	--	| Interview Question                                                | One-Line Answer                                                                                                    |
|	--| ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
|	1	| What is Airflow?                                                  | Apache Airflow is an open-source workflow orchestration tool used to schedule, monitor, and manage data pipelines. |
|	2	| What is a DAG?                                                    | A DAG (Directed Acyclic Graph) defines the workflow and task dependencies in Airflow.                              |
|	3	| What is a Task?                                                   | A task is a single unit of work inside a DAG.                                                                      |
|	4	| What is a PythonOperator?                                         | PythonOperator executes a Python function as an Airflow task.                                                      |
|	5	| What are `default_args`?                                          | `default_args` define common task parameters shared across all tasks in a DAG.                                     |
|	6	| What is `schedule`?                                               | `schedule` defines when the DAG should run using a cron expression or preset.                                      |
|	7	| What is `catchup=False`?                                          | It prevents Airflow from running historical DAG executions that were missed.                                       |
|	8	| What is `start_date`?                                             | `start_date` specifies when Airflow begins scheduling the DAG.                                                     |
|	9	| What is `owner`?                                                  | `owner` identifies the person or team responsible for the DAG.                                                     |
|	10	| What are `retries`?                                               | `retries` specifies how many times Airflow retries a failed task.                                                  |
|	11	| What is `retry_delay`?                                            | `retry_delay` is the waiting time before retrying a failed task.                                                   |
|	12	| What is XCom?                                                     | XCom is Airflow's mechanism for passing small amounts of data between tasks.                                       |
|	13	| Difference between `xcom_push` and `xcom_pull`?                   | `xcom_push()` stores data, while `xcom_pull()` retrieves data from another task.                                   |
|	14	| What is an Airflow Variable?                                      | Variables store global key-value configuration accessible by any DAG.                                              |
|	15	| What is an Airflow Connection?                                    | Connections securely store credentials for external systems like databases and cloud services.                     |
|	16	| Why use BaseHook?                                                 | BaseHook retrieves Airflow Connections programmatically inside tasks.                                              |
|	17	| What is `execution_date`?                                         | `execution_date` is the logical date representing the scheduled DAG run.                                           |
|	18	| What is `ds`?                                                     | `ds` is the execution date formatted as `YYYY-MM-DD`.                                                              |
|	19	| Why use `BranchPythonOperator`?                                   | It chooses one execution path among multiple downstream tasks.                                                     |
|	20	| What should `BranchPythonOperator` return?                        | It must return the `task_id` of the task to execute next.                                                          |
|	21	| What is `ShortCircuitOperator`?                                   | It skips downstream tasks when the callable returns `False`.                                                       |
|	22	| Difference between BranchPythonOperator and ShortCircuitOperator? | Branch selects one path, while ShortCircuit either continues or skips all downstream tasks.                        |
|	23	| What is `TriggerDagRunOperator`?                                  | It starts another DAG from the current DAG.                                                                        |
|	24	| What is `dag_run.conf`?                                           | `dag_run.conf` contains runtime parameters passed when triggering a DAG.                                           |
|	25	| What are Jinja Templates?                                         | Jinja templates dynamically render values like `{{ ds }}` at runtime.                                              |
|	26	| What is `ExternalTaskSensor`?                                     | It waits for a task in another DAG to complete before continuing.                                                  |
|	27	| Why use `mode="reschedule"`?                                      | It releases the worker slot while waiting, improving resource utilization.                                         |
|	28	| What is `poke_interval`?                                          | It defines how frequently a sensor checks for completion.                                                          |
|	29	| What is `timeout`?                                                | It specifies the maximum time a sensor waits before failing.                                                       |
|	30	| What is `execution_timeout`?                                      | It limits how long a task is allowed to run before failing.                                                        |
|	31	| What is SLA?                                                      | SLA monitors whether a task finishes within the expected time but does not stop execution.                         |
|	32	| Difference between SLA and `execution_timeout`?                   | SLA only reports delays, whereas `execution_timeout` terminates long-running tasks.                                |
|	33	| What is `TriggerRule`?                                            | TriggerRule controls when a task executes based on upstream task states.                                           |
|	34	| What does `NONE_FAILED_MIN_ONE_SUCCESS` mean?                     | The task runs if at least one upstream task succeeds and none fail.                                                |
|	35	| What is `EmptyOperator`?                                          | EmptyOperator is a placeholder task used for organizing workflows.                                                 |
|	36	| What is a TaskGroup?                                              | TaskGroup logically groups related tasks for better DAG visualization.                                             |
|	37	| What is a Pool?                                                   | A Pool limits the number of concurrent tasks sharing a resource.                                                   |
|	38	| What is `pool_slots`?                                             | It defines how many slots a task consumes from a pool.                                                             |
|	39	| What is a Queue?                                                  | A Queue routes tasks to specific workers in distributed executors.                                                 |
|	40	| What is `priority_weight`?                                        | It determines the scheduling priority when multiple tasks compete for resources.                                   |
|	41	| What is `on_success_callback`?                                    | It executes custom logic after a task completes successfully.                                                      |
|	42	| What is `on_failure_callback`?                                    | It executes custom logic when a task fails.                                                                        |
|	43	| What is a Dataset?                                                | A Dataset represents shared data that can trigger dependent DAGs when updated.                                     |
|	44	| What are `outlets`?                                               | `outlets` mark datasets as updated after a task finishes.                                                          |
|	45	| What is `doc_md`?                                                 | `doc_md` adds Markdown documentation visible in the Airflow UI.                                                    |
|	46	| Why use `>>` and `<<`?                                            | They define task execution dependencies in a readable way.                                                         |
|	47	| Difference between `>>` and `set_downstream()`?                   | Both create downstream dependencies, but `>>` is shorter and more readable.                                        |
|	48	| What is an Executor?                                      | An Executor determines how and where Airflow tasks are executed.                                    |
|	49	| What are the types of Executors?                          | SequentialExecutor, LocalExecutor, CeleryExecutor, KubernetesExecutor, and LocalKubernetesExecutor. |
|	50	| Which Executor is used in production?                     | CeleryExecutor and KubernetesExecutor are commonly used in production.                              |
|	51	| What is the Scheduler?                                    | The Scheduler continuously checks DAGs and schedules runnable tasks.                                |
|	52	| What is a Worker?                                         | A Worker executes the tasks assigned by the Executor.                                               |
|	53	| Difference between Scheduler and Executor?                | Scheduler decides what to run, Executor decides how to run it.                                      |
|	54	| Difference between Executor and Worker?                   | Executor manages task execution; Worker actually runs the task.                                     |
|	55	| What is the Metadata Database?                            | It stores DAG runs, task instances, logs, XComs, Variables, and Connections.                        |
|	56	| What is the Webserver?                                    | The Webserver provides the Airflow UI for monitoring and managing workflows.                        |
|	57	| What is a Sensor?                                         | A Sensor waits for an external event before allowing downstream tasks to run.                       |
|	58	| Types of Sensors?                                         | FileSensor, ExternalTaskSensor, HttpSensor, SqlSensor, S3KeySensor, GCSObjectExistenceSensor, etc.  |
|	59	| Difference between poke mode and reschedule mode?         | Poke mode occupies a worker; reschedule mode releases the worker while waiting.                     |
|	60	| What is a DAG Run?                                        | A DAG Run is a single execution instance of a DAG.                                                  |
|	61	| What is a Task Instance?                                  | A Task Instance is the execution of a task for a specific DAG Run.                                  |
|	62	| What is a Backfill?                                       | Backfill executes DAG runs for past dates that were missed.                                         |
|	63	| What is Manual Trigger?                                   | It starts a DAG immediately through the UI, CLI, or API.                                            |
|	64	| What is a Cron Expression?                                | A cron expression defines a recurring schedule for DAG execution.                                   |
|	65	| What is `depends_on_past`?                                | It allows a task to run only if the previous execution succeeded.                                   |
|	66	| What is `max_active_runs`?                                | It limits how many DAG runs can execute simultaneously.                                             |
|	67	| What is `max_active_tasks`?                               | It limits the number of running tasks across a DAG.                                                 |
|	68	| What is `concurrency`?                                    | It limits the number of concurrently running task instances in a DAG.                               |
|	69	| Difference between `concurrency` and `max_active_runs`?   | Concurrency limits tasks; `max_active_runs` limits DAG runs.                                        |
|	70	| What is `dagrun_timeout`?                                 | It sets the maximum duration for an entire DAG run.                                                 |
|	71	| What is `depends_on_past=True` used for?                  | It ensures sequential processing of dependent data.                                                 |
|	72	| What is `wait_for_downstream`?                            | It delays the next run until downstream tasks from the previous run finish.                         |
|	73	| What is a DAG Tag?                                        | Tags organize and filter DAGs in the Airflow UI.                                                    |
|	74	| What is `params`?                                         | `params` passes custom parameters to tasks at runtime.                                              |
|	75	| Difference between Variables and Params?                  | Variables are global; Params are DAG-run specific.                                                  |
|	76	| Difference between Variables and XCom?                    | Variables are global configuration; XCom is task-to-task communication.                             |
|	77	| What is a Secret Backend?                                 | It stores sensitive information externally instead of in Airflow metadata DB.                       |
|	78	| Which Secret Backends does Airflow support?               | HashiCorp Vault, AWS Secrets Manager, GCP Secret Manager, Azure Key Vault, etc.                     |
|	79	| Why use Secret Backend?                                   | To securely manage credentials without storing them in Airflow.                                     |
|	80	| What is Logging in Airflow?                               | Airflow stores task execution logs for monitoring and debugging.                                    |
|	81	| Where are Airflow logs stored?                            | Locally or remotely in GCS, S3, Azure Blob Storage, etc.                                            |
|	82	| How do you retry only failed tasks?                       | Clear the failed task from the UI or CLI and rerun it.                                              |
|	83	| What is DAG Serialization?                                | DAG Serialization stores DAGs in the metadata database for efficient webserver performance.         |
|	84	| What are Airflow Plugins?                                 | Plugins extend Airflow with custom operators, hooks, sensors, and views.                            |
|	85	| What is a Custom Operator?                                | A user-defined operator implementing custom business logic.                                         |
|	86	| What is a Hook?                                           | A Hook manages reusable connections to external systems.                                            |
|	87	| Difference between Hook and Operator?                     | Hook connects to systems; Operator performs workflow tasks.                                         |
|	88	| What is a Deferrable Operator?                            | A Deferrable Operator releases worker resources while waiting for external events.                  |
|	89	| Why use Deferrable Operators?                             | They improve scalability by reducing worker utilization.                                            |
|	90	| What is Dynamic DAG Generation?                           | Creating multiple DAGs programmatically from configuration or metadata.                             |
|	91	| What is Dynamic Task Mapping?                             | Creating tasks dynamically at runtime based on input data.                                          |
|	92	| Difference between Dynamic DAGs and Dynamic Task Mapping? | Dynamic DAGs create DAGs at parse time; Task Mapping creates tasks at runtime.                      |
|	93	| What is Airflow CLI?                                      | A command-line interface to manage DAGs, tasks, users, and scheduler operations.                    |
|	94	| How do you pause a DAG?                                   | From the UI or using the `airflow dags pause` CLI command.                                          |
|	95	| How do you trigger a DAG from CLI?                        | `airflow dags trigger <dag_id>`.                                                                    |
|	96	| How do you test a task locally?                           | `airflow tasks test <dag_id> <task_id> <execution_date>`.                                           |
|	97	| How do you clear failed tasks?                            | Use the UI or `airflow tasks clear`.                                                                |
|	98	| How do you monitor failed DAGs?                           | Through the Airflow UI, logs, alerts, or email notifications.                                       |
|	99	| How do you debug a failed DAG?                            | Check task logs, scheduler logs, dependencies, and configuration.                                   |
|	100	| How do you deploy DAGs?                                   | Copy DAG files into the configured DAGs folder or CI/CD pipeline.                                   |
|	101	| How do you version control DAGs?                          | Store DAGs in Git and deploy through CI/CD pipelines.                                               |
|	102	| How do you make DAGs reusable?                            | By using common utilities, custom operators, reusable functions, and configuration files.           |
|	103	| Why does the Airflow Scheduler become slow with thousands of DAGs? | Because DAG parsing is CPU-intensive, metadata DB queries increase, and scheduling decisions become more expensive.   |
|	104	| How do you optimize Scheduler performance?                         | Use DAG Serialization, multiple schedulers, minimize DAG parsing, and tune the metadata database.                     |
|	105	| Why should you avoid heavy code at DAG parse time?                 | DAG files are parsed repeatedly by the Scheduler, so expensive operations slow scheduling.                            |
|	106	| What operations should never be done at DAG parse time?            | Database queries, API calls, file reads, Spark sessions, or large computations.                                       |
|	107	| What is DAG parsing?                                               | The Scheduler imports DAG Python files to discover DAG definitions and tasks.                                         |
|	108	| How often does Airflow parse DAGs?                                 | The Scheduler continuously reparses DAG files based on configuration.                                                 |
|	109	| Why should imports be lightweight in DAG files?                    | Heavy imports increase DAG parsing time and Scheduler load.                                                           |
|	110	| Why should business logic not be written inside DAG files?         | DAG files should define workflows only; business logic belongs in reusable modules.                                   |
|	111	| Why is XCom not suitable for large data?                           | XCom stores data in the metadata database, which can become slow and oversized.                                       |
|	112	| What is the XCom size limitation?                                  | There is no strict Airflow limit, but only small metadata should be stored; large data should go to external storage. |
|	113	| How do you share large data between tasks?                         | Store it in GCS, S3, HDFS, or a database, and pass only the path through XCom.                                        |
|	114	| Why shouldn't Pandas DataFrames be pushed to XCom?                 | They increase metadata database size and degrade Scheduler performance.                                               |
|	115	| How do you prevent duplicate DAG runs?                             | Use idempotent processing, unique run identifiers, and proper concurrency settings.                                   |
|	116	| What is an idempotent DAG?                                         | A DAG that produces the same result even if executed multiple times.                                                  |
|	117	| How do you make a DAG idempotent?                                  | Avoid duplicate inserts, use MERGE/UPSERT, checkpoints, and deterministic processing.                                 |
|	118	| How do you recover from partial pipeline failures?                 | Restart from checkpoints or rerun only failed tasks while ensuring idempotency.                                       |
|	119	| How do you handle long-running tasks?                              | Split them into smaller tasks or use Deferrable Operators for waiting.                                                |
|	120	| Why are Deferrable Operators preferred over Sensors?               | They free worker resources while waiting, improving scalability.                                                      |
|	121	| When would you use KubernetesExecutor?                             | For isolated, auto-scaling task execution in Kubernetes.                                                              |
|	122	| When would you use CeleryExecutor?                                 | For distributed execution across multiple worker nodes.                                                               |
|	123	| How do you horizontally scale Airflow?                             | Add Scheduler instances, Workers, and optimize the metadata database.                                                 |
|	124	| Why is the metadata database considered the bottleneck?            | Every Scheduler, Worker, XCom, and task state update depends on it.                                                   |
|	125	| Which database is recommended for production?                      | PostgreSQL or MySQL; SQLite is only for development.                                                                  |
|	126	| Why is SQLite not recommended?                                     | It doesn't support concurrent production workloads.                                                                   |
|	127	| How do you secure Airflow Connections?                             | Store credentials in Secret Backends instead of the metadata database.                                                |
|	128	| What happens if the Scheduler goes down?                           | Running tasks continue, but no new tasks are scheduled until it recovers.                                             |
|	129	| What happens if a Worker crashes?                                  | The task fails or retries based on configuration.                                                                     |
|	130	| How do you avoid zombie tasks?                                     | Configure heartbeats correctly and monitor Scheduler/Worker health.                                                   |
|	131	| What are Zombie Tasks?                                             | Tasks that are still running but have lost communication with the Scheduler.                                          |
|	132	| What are Orphaned Tasks?                                           | Tasks existing without an active Scheduler managing them.                                                             |
|	133	| How does Airflow detect failed workers?                            | Through heartbeat monitoring stored in the metadata database.                                                         |
|	134	| How do you make DAG deployments zero downtime?                     | Use CI/CD, version control, and atomic DAG deployments.                                                               |
|	135	| Why should DAG IDs never change?                                   | Changing the DAG ID creates a new DAG history in the metadata database.                                               |
|	136	| What happens if you rename a task_id?                              | Airflow treats it as a new task, losing previous execution history.                                                   |
|	137	| Why shouldn't task_id change frequently?                           | It breaks historical tracking and task state continuity.                                                              |
|	138	| How do you version DAGs?                                           | Keep the DAG ID constant and version the code repository instead.                                                     |
|	139	| How do you deploy DAGs in production?                              | Use Git-based CI/CD pipelines with automated testing.                                                                 |
|	140	| How do you monitor Airflow?                                        | Monitor Scheduler, Workers, DAG success rate, task duration, and metadata database health.                            |
|	141	| Which metrics do you monitor?                                      | DAG success rate, task duration, Scheduler latency, queue length, worker utilization, and DB latency.                 |
|	142	| How do you reduce Airflow startup time?                            | Reduce heavy imports, avoid parse-time logic, and enable DAG Serialization.                                           |
|	143	| Why use Local Imports?                                             | Import heavy libraries inside task functions to reduce DAG parsing overhead.                                          |
|	144	| Difference between parse time and runtime?                         | Parse time loads DAG definitions; runtime executes task logic.                                                        |
|	145	| What is Airflow's biggest bottleneck?                              | Scheduler performance and metadata database scalability.                                                              |
|	146	| How do you optimize thousands of DAGs?                             | Split DAG folders, enable serialization, reduce parsing, and use multiple schedulers.                                 |
|	147	| What causes Scheduler lag?                                         | Heavy DAG parsing, slow metadata DB, excessive Sensors, or overloaded Workers.                                        |
|	148	| Why avoid dynamic DAG generation from databases?                   | Frequent database calls during parsing slow the Scheduler.                                                            |
|	149	| What is the best practice for dynamic DAGs?                        | Read static configuration files instead of querying databases at parse time.                                          |
|	150	| How do you debug a Scheduler issue?                                | Check Scheduler logs, parse times, heartbeat status, and metadata DB performance.                                     |
|	151	| How do you debug a stuck DAG?                                      | Verify dependencies, Scheduler status, task states, pools, queues, and logs.                                          |
|	152	| How do you prevent task starvation?                                | Configure pools, queues, and priority weights appropriately.                                                          |
|	153	| What happens if a Pool has no slots?                               | Tasks remain queued until slots become available.                                                                     |
|	154	| How do you prevent deadlocks?                                      | Design dependencies carefully and avoid circular waits.                                                               |
|	155	| Why is Airflow not suitable for stream processing?                 | Airflow is designed for orchestration, not continuous low-latency processing.                                         |
|	156	| Difference between orchestration and execution?                    | Airflow orchestrates workflows; tools like Spark execute computations.                                                |
|	157	| Should Spark logic be inside Airflow?                              | No, Airflow should trigger Spark jobs, not execute Spark transformations itself.                                      |
|	158	| Why use Airflow with Dataflow or Dataproc?                         | Airflow manages workflow dependencies while Dataflow/Dataproc handle distributed processing.                          |

## GCP Cloud Storage Classes – Complete Difference Table

| Feature                               | Standard                 | Nearline                          | Coldline                               | Archive                            |
| ------------------------------------- | ------------------------ | --------------------------------- | -------------------------------------- | ---------------------------------- |
| **Purpose**                           | Frequently accessed data | Data accessed about once a month  | Data accessed about once every 90 days | Long-term archival data            |
| **Typical Access Frequency**          | Multiple times/day       | Once every 30 days                | Once every 90 days                     | Less than once every 365 days      |
| **Minimum Storage Duration**          | None                     | 30 days                           | 90 days                                | 365 days                           |
| **Retrieval Time**                    | Immediate (milliseconds) | Immediate (milliseconds)          | Immediate (milliseconds)               | Immediate (milliseconds)           |
| **Storage Cost**                      | Highest                  | Lower than Standard               | Lower than Nearline                    | Lowest                             |
| **Data Retrieval Cost**               | No retrieval charge      | Yes                               | Yes                                    | Highest retrieval charge           |
| **Early Deletion Charge**             | No                       | Charged if deleted before 30 days | Charged if deleted before 90 days      | Charged if deleted before 365 days |
| **Availability (Regional)**           | 99.99%                   | 99.99%                            | 99.99%                                 | 99.99%                             |
| **Availability (Multi/ Dual Region)** | 99.95%                   | 99.95%                            | 99.95%                                 | 99.95%                             |
| **Latency**                           | Milliseconds             | Milliseconds                      | Milliseconds                           | Milliseconds                       |
| **Throughput**                        | High                     | High                              | High                                   | High                               |
| **Best For**                          | Active applications      | Monthly backups                   | Quarterly backups                      | Compliance and long-term archives  |
| **Streaming Reads**                   | Yes                      | Yes                               | Yes                                    | Yes                                |
| **Streaming Writes**                  | Yes                      | Yes                               | Yes                                    | Yes                                |
| **Object Updates**                    | Frequent                 | Occasional                        | Rare                                   | Very Rare                          |
| **Supports Versioning**               | Yes                      | Yes                               | Yes                                    | Yes                                |
| **Supports Lifecycle Rules**          | Yes                      | Yes                               | Yes                                    | Yes                                |
| **Supports Object Lock**              | Yes                      | Yes                               | Yes                                    | Yes                                |
| **Supports CMEK**                     | Yes                      | Yes                               | Yes                                    | Yes                                |
| **Supports CSEK**                     | Yes                      | Yes                               | Yes                                    | Yes                                |

---

## Cost Trend

| Storage Class | Storage Cost | Retrieval Cost |
| ------------- | ------------ | -------------- |
| Standard      | Highest      | Lowest (None)  |
| Nearline      | ↓ Lower      | Medium         |
| Coldline      | ↓↓ Lower     | Higher         |
| Archive       | Lowest       | Highest        |

---

## Minimum Storage Duration

| Storage Class | Minimum Duration |
| ------------- | ---------------- |
| Standard      | None             |
| Nearline      | 30 Days          |
| Coldline      | 90 Days          |
| Archive       | 365 Days         |

---

## Which One Should You Use?

| Scenario                             | Recommended Storage Class |
| ------------------------------------ | ------------------------- |
| Website images                       | Standard                  |
| Frequently accessed datasets         | Standard                  |
| Daily ETL files                      | Standard                  |
| Monthly backups                      | Nearline                  |
| Disaster recovery backups            | Coldline                  |
| Quarterly reports                    | Coldline                  |
| Compliance documents                 | Archive                   |
| Financial records retained for years | Archive                   |
| Legal records                        | Archive                   |
| Medical archives                     | Archive                   |

---

## Memory Trick

| Storage Class | Remember As         |
| ------------- | ------------------- |
| **Standard**  | Use every day       |
| **Nearline**  | Use every month     |
| **Coldline**  | Use every 3 months  |
| **Archive**   | Almost never access |

---

## Most Asked Interview Questions

| Question                                                                    | One-Line Answer                                                                   |
| --------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| Which storage class has the lowest storage cost?                            | Archive                                                                           |
| Which storage class has no minimum storage duration?                        | Standard                                                                          |
| Which storage class is best for active workloads?                           | Standard                                                                          |
| Which storage class is best for monthly backups?                            | Nearline                                                                          |
| Which storage class is best for disaster recovery?                          | Coldline                                                                          |
| Which storage class is best for long-term archival?                         | Archive                                                                           |
| Does Archive take hours to retrieve data?                                   | No, retrieval is immediate (milliseconds); it is expensive to retrieve, not slow. |
| Which storage class has the highest retrieval cost?                         | Archive                                                                           |
| Can lifecycle rules automatically change storage classes?                   | Yes.                                                                              |
| Can an object move automatically from Standard to Archive?                  | Yes, by configuring lifecycle rules.                                              |
| Which storage class is most commonly used for production applications?      | Standard                                                                          |
| Which storage class incurs early deletion charges after 365 days?           | Archive                                                                           |
| Which storage class incurs early deletion charges after 90 days?            | Coldline                                                                          |
| Which storage class incurs early deletion charges after 30 days?            | Nearline                                                                          |
| Which storage class should you choose if you don't know the access pattern? | Standard (or use Autoclass to optimize automatically).                            |

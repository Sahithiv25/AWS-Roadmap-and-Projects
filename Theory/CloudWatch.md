## CloudWatch
Amazon CloudWatch is AWS’s monitoring and observability service.
It helps you understand what your AWS resources are doing by collecting:
- Metrics (numbers that change over time)
- Logs (text output from applications)
- Alarms (notifications when something goes wrong)
- Dashboards (visualizations)

Interview answer
CloudWatch is AWS’s monitoring service that collects metrics, logs, and events from AWS resources and applications. It lets teams visualize performance, troubleshoot issues, and set alarms to react to problems in real time.

#### CloudWatch metrics
Metrics are time-series data that CloudWatch automatically collects from AWS services.
| AWS Service  | CloudWatch Metric Example              |
| ------------ | -------------------------------------- |
| **EC2**      | CPUUtilization, NetworkIn, DiskReadOps |
| **S3**       | NumberOfObjects, BucketSizeBytes       |
| **Lambda**   | Invocations, Errors, Duration          |
| **DynamoDB** | Read/WriteCapacity, ThrottledRequests  |
| **ECS**      | CPUReservation, MemoryUtilization      |

CloudWatch Metrics help you understand resource usage trends and identify abnormal behavior.

#### CloudWatch logs
Logs are raw text data coming from:
- EC2 servers (/var/log/syslog)
- Lambda function logs
- ECS task logs
- Application logs you send manually

CloudWatch Logs let you:
- Search logs
- Filter errors
- Create metrics from logs
- Retain logs for months/years

Ex:
INFO Server started
ERROR Database connection timeout
WARNING High latency detected

#### CloudWatch Alarms
Alarms watch a metric and alert you if it crosses a threshold.
Examples: CPU > 80% for 5 minutes, Lambda errors > 10, FreeStorageSpace < 1GB, 

Alarms can:
- Notify you via SNS email/SMS
- Automatically stop/start EC2 instances
- Trigger Auto Scaling actions

#### CloudWatch Events / EventBridge
This part is important for system design interviews.
EventBridge (formerly CloudWatch Events) can respond to system actions like:
- EC2 instance state changes
- S3 object uploads
- Scheduled cron jobs
- Lambda function failures

Example: “When a file is uploaded to S3, trigger a Lambda function.”

#### CloudWatch Dashboards
Dashboards allow you to visualize key metrics:
CPU graphs, Memory usage, API latency, Custom business KPIs
Teams use dashboards for: Monitoring during releases, Incident response, Daily health checks

#### Questions
Q1: What is CloudWatch?

“CloudWatch is AWS’s monitoring service that collects metrics, logs, and events to help detect issues, understand performance, and automate responses via alarms or event triggers.”

Q2: Difference between CloudWatch Metrics and Logs?

“Metrics are numerical time-series data like CPU or memory usage. Logs are raw text output produced by applications or system processes.”

Q3: How do CloudWatch Alarms work?

“Alarms watch a metric and trigger actions when a threshold is crossed — such as sending notifications or performing auto-scaling actions.”

Q4: How is CloudWatch used for EC2 monitoring?

“CloudWatch collects CPU, disk, and network metrics automatically for EC2, and you can send OS-level metrics (like memory) or logs using the CloudWatch agent.”

Q5: How is CloudWatch used with Lambda?

“Every Lambda invocation automatically sends metrics (invocations, duration, errors) and logs (console logs) to CloudWatch.”

Q6: How does CloudWatch help in debugging?

“You can trace errors in CloudWatch Logs and correlate them with spikes in metrics or alarms to quickly pinpoint root causes.”
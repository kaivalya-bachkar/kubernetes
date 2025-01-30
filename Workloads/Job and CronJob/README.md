# Job and CronJob
In Kubernetes, Job and CronJob are used to run one-off or scheduled tasks, respectively. They provide a way to manage batch or periodic processes within a Kubernetes cluster.

### 1. Job:
A Job in Kubernetes is responsible for running one or more Pods to perform a specific task until completion. Once the Job is done (success or failure), the associated Pods are terminated. Jobs are typically used for tasks that need to run only once or require retrying upon failure.

#### Key Features of a Job:
- Creates one or more Pods to execute a task.
- Automatically retries the task if the Pod fails (configurable).
- Ensures the task runs to completion (i.e., the Pod succeeds).
- You can configure parallelism to run multiple Pods simultaneously.

#### Use Cases:
- Data processing tasks.
- Batch jobs (e.g., data migrations, backups).
- Jobs that are idempotent or need retries.

### Steps to deploy daemonset:

- You will see 1 manifest in the same directory (Job and CronJob) with name job.yml.
- Copy the content of the manifest and run the following command to deploy it.
```bash
kubectl apply -f job.yaml
```

### 2. CronJob:
A CronJob is a type of Job in Kubernetes that is scheduled to run at a specific time or interval, much like a cron job on Unix/Linux systems. It is used to automate repetitive tasks, and you can define the schedule using cron syntax.

#### Key Features of a CronJob:
- Runs Jobs at scheduled times using cron-like syntax.
- Can create Jobs on a repeating schedule.
- Useful for recurring tasks like backups, cleaning up resources, or periodic reporting.
- Handles missed schedules (when the cluster is down) based on configurable settings.

#### Cron Syntax:
- "*/5 * * * *" – Run every 5 minutes.
- "0 12 * * *" – Run at noon every day.

#### Use Cases:
- Scheduled backups or data processing.
- Regularly scheduled health checks.
- Sending periodic reports.

### Steps to deploy daemonset:

- You will see 1 manifest in the same directory (Job and CronJob) with name job.yml.
- Copy the content of the manifest and run the following command to deploy it.
```bash
kubectl apply -f job.yaml
```

### Differences Between Job and CronJob:
- **Job**: Runs immediately when created, used for one-off tasks.
- **CronJob**: Runs on a schedule and can repeat the task periodically.


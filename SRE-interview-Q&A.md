# Interview Preparation - Observability Experience

## Q1: What is your experience in Observability?

### ✅ Improved Answer

👉 (Say this confidently)

I have around **2 years of hands-on experience in observability** as part of my DevOps role, where I worked closely with monitoring and reliability practices in **Kubernetes environments**.

---

### 🔹 My Observability Approach

I follow the **three pillars of observability**:

- **Metrics** → using **Prometheus**
- **Logs** → using **Fluent Bit** and **Loki**
- **Traces** → using **OpenTelemetry** with **Jaeger/Tempo**

---

### 🔹 Beyond Tools: My Focus

- Detecting issues proactively using **alerts**
- Performing **root cause analysis** by correlating logs and metrics
- Reducing downtime and improving **MTTR (Mean Time to Recovery)**

---

### 🔹 Example: EKS-based System

- Used **Prometheus exporters** like `node-exporter` and `kube-state-metrics`
- Created **Grafana dashboards** for infrastructure health
- Set **alerts** for CPU spikes, pod crashes, and node issues

---

### 🔹 Incident Workflow

During incidents, I correlate:

- 👉 **Metrics** → identify anomaly  
- 👉 **Logs** → find exact error  
- 👉 **Traces** → understand request flow  

This helps in identifying **why the issue happened, not just what happened**.

## Q2: What is Grafana used for?

### ✅ Improved Answer

Grafana is primarily used as a **visualization and observability platform**.  
It does not collect data itself — instead, it connects to data sources like **Prometheus, Loki, etc.**

---

### 🔹 My Usage of Grafana

- Build dashboards for:
  - Node-level metrics (CPU, memory)
  - Kubernetes metrics (pods, deployments)
  - Application-level metrics

- Configure **alerting rules** in Grafana/Prometheus  
- Create **SLO-based dashboards**  
- Use Grafana during incidents to quickly identify anomalies  

---

### 🔹 Grafana’s Key Role

👉 Monitoring  
👉 Alerting  
👉 Incident debugging  

---

## Q3: Explain Prometheus + Exporters

### ✅ Improved Answer

Prometheus follows a **pull-based model** where it scrapes metrics from **exporters**.

---

### 🔹 Exporters I Worked With

- **node-exporter** → system-level metrics (CPU, memory, disk)  
- **kube-state-metrics** → Kubernetes object states (pods, deployments)  
- **blackbox exporter** → endpoint monitoring  

These exporters expose metrics via **HTTP endpoints**, and Prometheus scrapes them at intervals.

---

### 🔹 Workflow

1. Prometheus stores **time-series data**  
2. Grafana is used to **visualize** it  
3. Define **alert rules** in Prometheus using **PromQL**  
4. Alerts are routed via **Alertmanager**  

---

### 🔹 Summary

Prometheus + Exporters provide the **data collection and storage**,  
Grafana provides the **visualization and incident response layer**.

## Q4: Explain your project (MOST IMPORTANT)

### ✅ Strong Answer

In my recent project, I worked on an **AWS EKS-based microservices platform** where my role involved both **DevOps and SRE responsibilities**.

---

### 🔹 Responsibilities

**Infrastructure Monitoring**
- Set up Prometheus and Grafana for cluster monitoring
- Used exporters like `node-exporter` and `kube-state-metrics`

**Alerting**
- Configured alerts for:
  - High CPU/memory usage
  - Pod crashes (CrashLoopBackOff)
  - Node failures

**Incident Handling**
- Checked Grafana dashboards for anomalies
- Used `kubectl logs` to analyze failures
- Identified root causes (resource limits, misconfigurations, dependency failures)

---

### 🔹 Example Incident

- Frequent pod restarts in one service  
- Metrics showed **memory spikes**  
- Logs revealed **OOMKilled issue**  

**Solution:**
- Adjusted resource requests/limits  
- Optimized JVM memory configuration  

**Outcome:**
- Reduced pod failures  
- Improved service stability  
- Faster debugging (reduced MTTR)  

Although my exposure was more infrastructure-focused, I actively collaborated with developers during debugging.

---

## Q5: Tell me about a P1 / Incident you handled

### ✅ Improved Answer

I was involved in a **high-priority incident** related to our monitoring system where **Prometheus storage was getting exhausted frequently**.

---

### 🔹 Problem

- Prometheus storing high-volume metrics on EBS  
- Disk usage kept increasing (200GB → 250GB → 300GB)  
- Prometheus started crashing due to storage exhaustion  

**Impact:**  
- Loss of monitoring visibility  
- Risk of missing alerts → high reliability risk  

---

### 🔹 Root Cause

- Prometheus is not designed for long-term storage  
- High cardinality + retention caused storage pressure  

---

### 🔹 Solution (Thanos Implementation)

- Introduced **Thanos** for long-term, scalable storage  
- Implemented Thanos sidecar with Prometheus  
- Configured **S3 bucket** for object storage  
- Reduced Prometheus retention from 7 days → 1 day  
- Validated data availability via Grafana queries  

**Outcome:**  
- Eliminated storage issues  
- Improved system stability  
- Enabled long-term historical analysis  

---

## Q6: What is Thanos and how does it work?

### ✅ Strong Answer

Thanos is an **extension of Prometheus** that provides:

- Long-term storage  
- High availability  
- Global querying across multiple Prometheus instances  

---

### 🔹 How It Works

- **Thanos Sidecar** → runs alongside Prometheus, uploads TSDB blocks to object storage (S3), exposes data to Thanos Query  
- **Object Storage (S3)** → stores historical metrics in compressed format  
- **Thanos Store Gateway** → fetches historical data from S3  
- **Thanos Query** → unified query layer combining recent (Prometheus) + historical (S3) data  

**In our case:**  
- Recent 1-day data → Prometheus (EBS)  
- Older data → S3 via Thanos  

**Key Benefit:**  
- Infinite scalable storage  
- No dependency on EBS size  
- Centralized observability  

---

## Q7: Is Thanos a storage client?

### ✅ Correct Answer

Thanos is **not just a storage client**.  
It is a **distributed monitoring system** built on top of Prometheus.

It includes:  
- Sidecar (for uploading data)  
- Store Gateway (for reading data)  
- Query (for unified access)  

It uses object storage like S3, but it is much more than just a storage layer.

---

## Q8: What storage does Thanos support?

### ✅ Improved Answer

Thanos supports multiple object storage backends such as:

- AWS S3  
- Google Cloud Storage (GCS)  
- Azure Blob Storage  
- MinIO (S3-compatible)  

**In our setup:**  
We used **AWS S3** because of its durability and scalability.

---

## Q9: Why moving from DevOps to SRE?

### ✅ Strong Answer

I see **SRE as an evolution of DevOps**, focusing more on **reliability, observability, and system stability**.

---

### 🔹 My Current Role

- Kubernetes operations  
- Infrastructure automation using Terraform  
- Monitoring setup using Prometheus and Grafana  

Additionally:  
- Incident debugging  
- Alert-based monitoring  
- Improving system stability  

---

### 🔹 Transition

I am not transitioning into SRE from scratch — I am already working in that direction.  
Now I want to:  
- Go deeper into **SRE practices** like SLOs, SLIs  
- Improve **incident response strategies**  
- Work on **reliability engineering at scale**


## Q10: Did you create dashboards/alerts or just consume them?

### ✅ Strong Answer

Initially, the dashboards were already available, and I used them for monitoring cluster health.  
However, based on specific use cases, I contributed by:

- Enhancing existing dashboards with additional panels  
- Identifying gaps in monitoring coverage  
- Suggesting improvements for better visibility  

**Example:**  
- Added panels for pod restart trends and resource saturation  
- Worked with Prometheus queries (PromQL) to refine metrics  

Over time, I moved from just consuming dashboards to **improving observability** based on real incidents and gaps.

---

## Q11: Did you take proactive steps or just monitor dashboards?

### ✅ Strong Answer

Yes, I focused on reducing manual monitoring effort by introducing **proactive alerting and automation**.  

Instead of continuously watching dashboards, I:  
- Configured alerting based on thresholds (CPU, memory, pod failures)  
- Automated repetitive checks using **GitHub Actions and Python**  

**Goal:**  
👉 Reduce toil  
👉 Improve response time  
👉 Move towards proactive monitoring  

---

## Q12: Give an example of automation you built

### ✅ Strong STAR Answer

**Problem:**  
- EBS volumes in MSK clusters were auto-scaling (500GB → 600GB → 700GB)  
- Terraform configs still had old values (500GB) → configuration drift  

**Solution:**  
- Built a **GitHub Actions workflow** using Python  
- Fetches actual EBS size from AWS  
- Compares with configuration values  
- Detects mismatches across multiple regions (20–25 regions)  

**Trigger:**  
- Runs on a scheduled basis (cron)  
- Supports manual trigger (`workflow_dispatch`)  

**Outcome:**  
- Early detection of configuration drift  
- Reduced manual validation effort  
- Improved infrastructure consistency  
- Moved towards **automated governance** instead of manual checks  

---

## Q13: What trigger are you using?

### ✅ Correct + Strong Answer

The primary trigger I used was **schedule** for periodic execution (cron-based).  

**Example:**
```yaml
on:
  schedule:
    - cron: '0 */6 * * *'


## Q14: What are different triggers in GitHub Actions?

### ✅ Strong Answer

GitHub Actions supports multiple triggers depending on the use case:

- 🔹 **push**  
  Triggered when code is pushed to a branch  

- 🔹 **pull_request**  
  Runs during PR creation/update (used for validation)  

- 🔹 **schedule**  
  Cron-based trigger for periodic jobs  

- 🔹 **workflow_dispatch**  
  Manual trigger with input parameters  

- 🔹 **repository_dispatch**  
  External event/API-based trigger  

- 🔹 **workflow_run**  
  Trigger based on completion of another workflow  

**In my use case:**  
👉 Mainly used **schedule + workflow_dispatch**

---

## Q15: What else (beyond schedule)?

### ✅ Strong Answer

Apart from **schedule**, other important triggers include:

- **push** → for CI/CD pipelines  
- **pull_request** → for validation before merge  
- **workflow_dispatch** → for manual execution  
- **repository_dispatch** → for external integrations  

These triggers provide flexibility in automating different workflows.

## Q16: What are Leading and Lagging Indicators?

### ✅ Strong Answer

In SRE, **leading and lagging indicators** help us understand system health at different stages.

---

### 🔹 Leading Indicators
- Early warning signals  
- Indicate a potential issue **before it impacts users**  

**Examples:**
- CPU gradually increasing  
- Memory nearing threshold  
- Queue length increasing  

---

### 🔹 Lagging Indicators
- Indicate that an issue has **already impacted the system**  

**Examples:**
- Pod crash  
- Service downtime  
- Increased error rate (5xx)  

---

### 🔹 Summary
👉 **Leading = Preventive signals**  
👉 **Lagging = Failure confirmation**

---

## Q17: Which one would you prefer in SRE?

### ✅ Strong Answer

In SRE, **both are important**, but the focus is more on **leading indicators** because they help prevent incidents before they impact users.  

However, we should not rely only on leading indicators, because:  
- They can generate noise  
- Not all warnings lead to real issues  

**Balanced Approach:**  
- Leading indicators → for **prevention**  
- Lagging indicators → for **incident detection and SLA tracking**

---

## Q18: Will you wake people at night for leading alerts?

### ✅ Strong Answer

No, we should **not wake up on-call engineers** for leading indicators.  

**Reasoning:**  
- Leading alerts are predictive, not confirmed failures  
- Waking engineers unnecessarily leads to **alert fatigue**  

**Best Practice:**  
- Only **lagging indicators (critical alerts)** should page on-call engineers  
- Leading indicators should be handled via **automation or low-priority alerts**


## Q19: Then what is the use of leading indicators?

### ✅ Strong Answer

Leading indicators are mainly used for **proactive automation and prevention**, not manual intervention.  

Instead of waking engineers, we:

- 🔹 **Trigger automation**
  - Auto-scale resources (CPU, memory, pods)  
  - Expand storage (EBS)  
  - Restart unhealthy services  

- 🔹 **Self-healing systems**
  - Kubernetes auto-healing (pod restart)  
  - HPA for scaling  

- 🔹 **Alert categorization**
  - Info / Warning → no paging  
  - Critical → paging  

**Summary:**  
Leading indicators help us move towards a **proactive SRE model** instead of reactive firefighting.

---

## Q20: Who handles warning alerts?

### ✅ Strong Answer

Warning alerts are usually **not handled manually in real-time**.  

Instead, they are either:  
- Logged for **trend analysis**  
- Used to **trigger automation**  

In mature SRE systems:  
- Only **actionable alerts** reach humans  
- Non-actionable alerts are automated or suppressed  

This reduces **alert fatigue** and improves efficiency.

---

## Q21: How do you use leading indicators practically?

### ✅ Strong Answer

Leading indicators are integrated with **automation workflows**.

**Examples:**

- 🔹 **Scenario: CPU > 70% (warning level)**  
  - Trigger HPA → scale pods  
  - Or trigger automation → increase resources  

- 🔹 **Scenario: Disk usage > 75%**  
  - Automatically expand EBS volume  

- 🔹 **Scenario: Memory pressure**  
  - Restart pods or rebalance workloads  

**Outcome:**  
- Issues resolved before becoming incidents  
- No human intervention required  
- Proactive SRE approach in action  

---

## Q22: Proactive vs Reactive approach

### ✅ Strong Answer

- 🔹 **Reactive Approach**  
  - Act **after issue happens**  
  - Based on **lagging indicators**  
  - Example: Pod crash → then fix  

- 🔹 **Proactive Approach**  
  - Act **before issue happens**  
  - Based on **leading indicators**  
  - Example: CPU spike → auto-scale before crash  

**In SRE:**  
👉 Goal is to move from **reactive → proactive systems**

## Q23: What is the difference between SLI, SLO, and SLA?

### ✅ Strong Answer

These are core reliability concepts in SRE:

- 🔹 **SLI (Service Level Indicator)**  
  - It is a **measurement metric**  
  - Example: Request success rate, latency  
  - Example formula: 👉 Successful requests / Total requests  

- 🔹 **SLO (Service Level Objective)**  
  - It is the **target value for SLI**  
  - Defined internally by the team  
  - Example: 👉 “99% of requests should be successful”  

- 🔹 **SLA (Service Level Agreement)**  
  - It is a **business agreement with customers**  
  - Includes penalties if not met  
  - Example: 👉 “We guarantee 95% uptime, else compensation applies”  

---

### 🔹 Relationship
- **SLI → measures**  
- **SLO → target**  
- **SLA → commitment**  

🔥 **Senior-level insight:**  
Typically: 👉 **SLO is stricter than SLA** (e.g., SLO = 99%, SLA = 95%)  
This buffer helps avoid SLA violations.

---

## Q24: Explain Error Budget

### ✅ Strong Answer

Error budget is the **allowed level of unreliability** in a system.  

**Formula:**  
👉 Error Budget = 100% - SLO  

**Example:**  
- If SLO = 99%  
- Error Budget = 1% downtime allowed  

---

### 🔹 Why It Is Important
- Balances **Reliability vs Release velocity**  

**Usage:**  
- If error budget is **not consumed** → release new features faster  
- If error budget is **exhausted** → stop releases, focus on stability  

**Example:**  
- In a 30-day month (~43,200 minutes)  
- 1% error budget ≈ **432 minutes allowed downtime**  

This helps teams make **data-driven decisions**.

---

## Q25: What is MTTR, MTTA, MTTD?

### ✅ Strong Answer

These are key **incident management metrics**:

- 🔹 **MTTA (Mean Time To Acknowledge)**  
  - Time taken to acknowledge an alert  

- 🔹 **MTTD (Mean Time To Detect)**  
  - Time taken to detect an issue  

- 🔹 **MTTR (Mean Time To Resolve/Recover)**  
  - Time taken to fix the issue and restore service  

---

### 🔹 Example

- Issue occurred at **10:00**  
- Detected at **10:10** → MTTD = 10 min  
- Acknowledged at **10:12** → MTTA = 2 min  
- Resolved at **10:30** → MTTR = 30 min  

---

### 🔹 Goal in SRE
- Reduce **MTTR**  
- Improve **detection speed**  
- Automate recovery where possible

## Q26: Why are these metrics important?

### ✅ Strong Answer

These metrics are critical because they help us:

- **Measure system reliability**  
  - Provide quantifiable insights into uptime, performance, and stability  

- **Improve incident response**  
  - Track how quickly issues are detected, acknowledged, and resolved  

- **Identify bottlenecks in detection and recovery**  
  - Highlight weak points in monitoring, alerting, or resolution processes  

---

### 🔹 Example

- **High MTTD** → indicates poor monitoring or delayed detection  
- **High MTTR** → indicates slow resolution or lack of automation  

---

### 🔹 Continuous Optimization

By analyzing these metrics, SRE teams can:  
- Strengthen monitoring systems  
- Automate recovery processes  
- Reduce downtime and improve user experience  

**Summary:**  
Reliability metrics are not just numbers — they are feedback loops that drive **continuous improvement in system health and incident management**.

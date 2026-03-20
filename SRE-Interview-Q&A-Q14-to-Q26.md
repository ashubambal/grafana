# Interview Preparation - Observability Experience

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

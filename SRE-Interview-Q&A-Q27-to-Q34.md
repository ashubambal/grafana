# 🚀 SRE / DevOps Interview Preparation Notes

## 🟢 Q27. How do you handle alert noise / alert fatigue?

### ❌ Weak Answer
- Slack colors (green/yellow/red)
- Ignore warnings  

👉 This is not sufficient for SRE practices.

---

### ✅ Strong Answer

**Alert fatigue happens when too many non-actionable alerts overwhelm engineers.**

To handle this, follow a structured approach:

#### 🔹 1. Alert Classification
- **Critical** → Pager (on-call)
- **Warning** → Slack / dashboards
- **Info** → Logs only

#### 🔹 2. Remove Noise
- Identify duplicate alerts  
- Remove non-actionable alerts  
- Tune thresholds properly  

#### 🔹 3. Alert Deduplication & Grouping
- Use Alertmanager to group similar alerts  
- Avoid multiple alerts for same issue  

#### 🔹 4. Add Cooldown / Suppression
- Prevent repeated alerts within short time  

#### 🔹 5. Automation for Known Issues
- Convert frequent alerts → auto-remediation  

#### 🔹 6. SLO-based Alerting
- Alert only when user impact is likely  

👉 **Goal:**  
Only actionable alerts should reach humans  

---

## 🟢 Q28. If Slack also becomes noisy, what will you do?

### ❌ Weak Answer
- Reduce frequency  
- Ignore messages  

---

### ✅ Strong Answer

If Slack becomes noisy, alerts are not properly tuned.

#### 🔹 1. Audit Alerts
Identify:
- Noisy alerts  
- Duplicate alerts  
- Low-value alerts  

#### 🔹 2. Define Actionability
Ask:  
👉 *Can someone take action on this alert?*  

- If NO → remove or downgrade  

#### 🔹 3. Threshold Tuning
- Avoid static thresholds (e.g., CPU 60%)  
- Use dynamic or SLO-based thresholds  

#### 🔹 4. Routing Strategy
- Critical → PagerDuty  
- Warning → Slack  
- Info → Dashboard only  

#### 🔹 5. Automation
Examples:
- CPU warning → trigger autoscaling  
- Disk warning → auto-expand  

#### 🔹 6. Alert Aggregation
- Combine multiple alerts into one summary  

👉 **Goal:**  
Reduce noise → improve signal quality  

---

## 🟢 Q29. What are Kubernetes probes?

### ❌ Weak Answer
- Mixed definitions  
- Confusion between readiness & liveness  

---

### ✅ Strong Answer

Kubernetes probes check container health and lifecycle status.

#### 🔹 1. Liveness Probe
- Checks if container is alive  
- If fails → container is restarted  

#### 🔹 2. Readiness Probe
- Checks if pod is ready to serve traffic  
- If fails → removed from service endpoints  

#### 🔹 3. Startup Probe
- Used for slow-start applications  
- Delays liveness/readiness until app is initialized  

---

### 🔹 Flow

Startup → Readiness → Liveness


👉 **Key Concepts:**
- Readiness = traffic control  
- Liveness = restart control  

---

## 🟢 Q30. Capacity Planning in Kubernetes

### ❌ Weak Answer
- Mentioned Goldilocks only  
- No depth  

---

### ✅ Strong Answer

Capacity planning ensures sufficient resources without over-provisioning.

#### 🔹 1. Resource Monitoring
- CPU / Memory usage trends  

#### 🔹 2. Right-Sizing
- Use tools like Goldilocks / VPA  

#### 🔹 3. Historical Analysis
- Analyze past usage patterns  

#### 🔹 4. Scaling Strategy
- HPA → scale pods  
- Cluster Autoscaler / Karpenter → scale nodes  

#### 🔹 5. Buffer Planning
- Maintain headroom for traffic spikes  

#### 🔹 6. Cost Optimization
- Avoid over-provisioning  

👉 **Goal:**  
Balance performance + cost + reliability  

---

## 🟢 Q31. Types of Scaling in Kubernetes

### ❌ Weak Answer
- Unstructured explanation  

---

### ✅ Strong Answer

#### 🔹 1. Horizontal Pod Autoscaler (HPA)
- Scales number of pods  
- Based on CPU/memory/custom metrics  

#### 🔹 2. Vertical Pod Autoscaler (VPA)
- Adjusts CPU/memory of pods  

#### 🔹 3. Cluster Autoscaler
- Adds/removes nodes based on demand  

#### 🔹 4. Karpenter
- Advanced node provisioning  
- Faster + cost-optimized  

👉 Each solves different scaling problems  

---

## 🟢 Q32. Explain Karpenter

### ❌ Weak Answer
- Unclear explanation  

---

### ✅ Strong Answer

Karpenter is a Kubernetes node provisioning tool that dynamically launches nodes based on workload.

#### 🔹 Key Features
- Faster scaling than Cluster Autoscaler  
- Flexible instance type selection  
- Cost optimization (spot + right-sizing)  

#### 🔹 Example
- Pods pending → Karpenter launches nodes immediately  
- Removes underutilized nodes to reduce cost  

---

## 🟢 Q33. HPA Manifest Example

### ✅ Example YAML

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: my-app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-app
  minReplicas: 2
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 60
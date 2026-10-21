# Camunda 8 Leave Request Process

A basic workflow implementation for managing employee leave requests built on Camunda 8 and the Zeebe engine[cite: 2, 4]. This repository contains the process definition and examples of how to deploy, trigger, and monitor the workflow.

## 📌 Process Overview
[ Apply Leave ] ──▶ [ Approve Leave (User Task) ] ──▶ [ Leave Processed ]

* **Process Name:** Leave Request Process[cite: 1, 2]
* **Process ID:** `leave-request`[cite: 1, 2]
* **Executable:** `true`[cite: 1, 2]

### Workflow Elements

| Element | Type | Details |
| :--- | :--- | :--- |
| **Apply Leave** | Start Event | Initiates the workflow when a leave request is submitted. |
| **Approve Leave** | User Task | Assigned to the user `demo` for manual review. |
| **Leave Processed**| End Event | Marks the completion of the process[cite: 2]. |

---

## 📁 Repository Files

This repository references the following core files:

* `leave-request.bpmn`: The BPMN 2.0 XML definition of the workflow[cite: 2].
* 
<img width="1387" height="997" alt="image" src="https://github.com/user-attachments/assets/2efe7040-b944-4097-b6a4-ec3e57fcc156" />
* A visual screenshot of the workflow in the Camunda Modeler[cite: 1].

<img width="1918" height="133" alt="image" src="https://github.com/user-attachments/assets/4ef13f88-6f46-4cf3-b18a-1af24e34042a" />
A screenshot demonstrating the REST API execution via curl[cite: 3].


<img width="1875" height="988" alt="image" src="https://github.com/user-attachments/assets/fe68d4a1-21be-43ef-bae2-f72fa567e9af" />
 A screenshot of the active process instance tracked inside Camunda Operate.

---
## 🚀 How to Run

### 1. Prerequisites
* A running Camunda 8 instance (Self-Managed or Camunda Cloud).
* Access to the Zeebe Gateway REST API, default `http://localhost:8080`[cite: 3].

### 2. Deploy the Workflow
Deploy the `leave-request.bpmn` file to your Camunda 8 cluster using Camunda Modeler, Web Modeler, or the `zbctl` CLI[cite: 1, 2].

### 3. Start a Process Instance
Trigger the workflow via the Zeebe REST API (`v2`) by passing the required variables[cite: 3]. 

**Command (Windows CMD/PowerShell):**
```powershell
curl.exe -X POST "http://localhost:8080/v2/process-instances" `
  -H "Content-Type: application/json" `
  -d "{\"processDefinitionId\":\"leave-request\",\"variables\":{\"employeeName\":\"Ravi\",\"days\":3}}"

Command (Bash/Linux/macOS):
curl -X POST "http://localhost:8080/v2/process-instances" \
  -H "Content-Type: application/json" \
  -d '{
    "processDefinitionId": "leave-request",
    "variables": {
      "employeeName": "Ravi",
      "days": 3
    }
  }'

Example API Response:
{
  "processDefinitionId": "leave-request",
  "processDefinitionVersion": 1,
  "tenantId": "<default>",
  "variables": {},
  "processDefinitionKey": "2251799813797561",
  "processInstanceKey": "2251799813797634",
  "tags": [],
  "businessId": null
}


# Lab 7 (CST8915) <br> pate1595

### Youtube Video link: <br>
https://youtu.be/X7T4OnEIy4M

---



## RabbitMQ Configuration Analysis

### 1. Whether RabbitMQ is a stateless or stateful application
RabbitMQ is a stateful application. It stores messages, queues, and exchange data that must persist even after pod restarts.

---

### 2. The implications of running RabbitMQ without persistent storage
In this YAML file, RabbitMQ is deployed as a Deployment without any PersistentVolumeClaim (PVC).  
That means its data is ephemeral and will be lost when the pod restarts or the node is rescheduled.

---

### 3. What happens when the RabbitMQ pod is deleted or restarted
- All message queues and routing data are deleted when the pod terminates.  
- Order Service and Product Service lose communication until RabbitMQ restarts.  
- The application becomes unreliable in real production environments.

---

### 4. Potential solutions to this problem (research-based)

| Solution | Description | Benefit |
|-----------|--------------|----------|
| **Add PersistentVolumeClaim (PVC)** | Mount Azure Disk or File share at `/var/lib/rabbitmq`. | Keeps RabbitMQ data after restart. |
| **Use StatefulSet** | Replace Deployment with StatefulSet for stable network IDs. | Ensures reliable re-scheduling of pods. |
| **Use Helm Chart** | Official RabbitMQ Helm chart includes persistence and probes. | Easier to manage and monitor. |
| **Switch to Azure Service Bus** | Managed messaging service provided by Azure. | Eliminates data-loss issues entirely. |

---

### 5. Does using Azure Service Bus solve the issues identified with RabbitMQ Configuration in this Lab?
Yes. Azure Service Bus is stateful, durable, and fully managed, handling replication, storage, and scaling automatically no manual PVCs or RabbitMQ configuration required.

---


# CST8915 – Lab 8 Submission – Algonquin Pet Store on Steroids



---

##  YouTube Demo Video Link
https://youtu.be/Vzgzn0PUWHk



---

# Task 2 – MongoDB and RabbitMQ Persistence 

---

## MongoDB Persistence

MongoDB was deployed as a **StatefulSet with 3 replicas** and **Persistent Volume Claims (10Gi each)** to ensure data is not lost when pods restart.

### Verification

- Check MongoDB pods:
  - `kubectl get pods`
- Check MongoDB PVCs:
  - `kubectl get pvc`

This confirmed that:
- `mongodb-0`, `mongodb-1`, and `mongodb-2` were running
- All MongoDB PVCs were in `Bound` state

### Persistence Test

- Connect to MongoDB:
  - `kubectl exec -it mongodb-0 -- mongo`
- Insert data:
  - `use orderdb`
  - `db.demo.insertOne({ name: "lab8", value: 1 })`
  - `db.demo.find()`
- Exit:
  - `exit`
- Delete MongoDB pod:
  - `kubectl delete pod mongodb-0`
  - `kubectl get pods`
- Reconnect and verify data:
  - `kubectl exec -it mongodb-0 -- mongo`
  - `use orderdb`
  - `db.demo.find()`

 Data was still present after pod recreation, proving MongoDB persistence.

---

## RabbitMQ Persistence

RabbitMQ was deployed as a **StatefulSet with a Persistent Volume Claim** mounted at `/var/lib/rabbitmq` to ensure queue data survives pod restarts.

### Verification

- Start management UI:
  - `kubectl port-forward service/rabbitmq 15672:15672`
- Open in browser:
  - `http://localhost:15672`
- Login:
  - Username: `username`
  - Password: `password`

### Persistence Test

- Create durable queue:
  - `lab8_queue`
- Publish test messages using UI
- Delete RabbitMQ pod:
  - `kubectl delete pod rabbitmq-0`
  - `kubectl get pods`
- Reconnect to UI and verify:
  - `kubectl port-forward service/rabbitmq 15672:15672`
  - Confirm `lab8_queue` still exists

The queue remained after pod restart, proving RabbitMQ persistence.

---

## Issue Faced

- When Task 1 was applied after Task 2, MongoDB data sometimes appeared missing.
- After re-applying Task 2:
  - `kubectl apply -f aps-all-in-one-Task2.yaml`
- The data became visible again.

I think this happened because Task 1 does not manage PVCs, while Task 2 re-attaches them correctly.

---

## Final Deployment Order Used

- Apply Task 1:
  - `kubectl apply -f aps-all-in-one-Task1.yaml`
- Apply Task 2:
  - `kubectl apply -f aps-all-in-one-Task2.yaml`
- Perform MongoDB and RabbitMQ persistence tests



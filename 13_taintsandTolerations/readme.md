Taints ARE SET ON NODE
Tolerations are set on pod

kubectl taint nodes <node name> <key>=<value>:<taint-effect>


to remove taint

kubectl taint nodes <nodename> <key>-   # the hifen atlast tells to remove tains

taint-effect is three types

1) NoSchedule
2) PreferNoSchedukle
3) NoExecute (if the pod was already running it will evict pod in addition to NoSchedule)

# Why Kubernetes Tolerations Need `effect`

In Kubernetes, **tolerations** are used to allow pods to be scheduled on nodes with specific **taints**. Taints and tolerations work together to control which pods can be scheduled on which nodes. The `effect` field in a toleration specifies the type of behavior the toleration is addressing for a taint. Here's why the `effect` field is important:

---

## **What is a Taint?**
A **taint** is applied to a node to mark it as having a special condition that affects scheduling. For example, a node might be tainted to indicate it is reserved for specific workloads or is undergoing maintenance. A taint has three components:
1. **Key**: A label-like identifier for the taint.
2. **Value**: An optional value associated with the key.
3. **Effect**: Specifies the scheduling behavior for pods that do not tolerate the taint.

The `effect` can be one of the following:
- **NoSchedule**: Pods that do not tolerate the taint will not be scheduled on the node.
- **PreferNoSchedule**: Kubernetes will try to avoid scheduling pods that do not tolerate the taint, but it is not guaranteed.
- **NoExecute**: Pods that do not tolerate the taint will be evicted from the node if they are already running, and new pods will not be scheduled.

---

## **What is a Toleration?**
A **toleration** is applied to a pod to allow it to be scheduled on nodes with specific taints. A toleration has the following components:
1. **Key**: Matches the key of the taint.
2. **Value**: Matches the value of the taint (optional).
3. **Effect**: Matches the effect of the taint.
4. **Operator**: Specifies how the toleration matches the taint (e.g., `Equal` or `Exists`).

---

## **Why Does a Toleration Need an Effect?**
The `effect` in a toleration is necessary because it defines **which type of taint behavior the pod is tolerating**. Without specifying the effect, Kubernetes would not know how to interpret the toleration in relation to the taint. Here's why the `effect` is important:

### 1. **Precise Matching**
- A node can have multiple taints with different effects (e.g., `NoSchedule`, `NoExecute`).
- The toleration's `effect` ensures the pod tolerates the correct type of taint behavior.

### 2. **Control Over Scheduling and Eviction**
- If a node has a `NoSchedule` taint, the toleration must explicitly specify `NoSchedule` to allow the pod to be scheduled on that node.
- If a node has a `NoExecute` taint, the toleration must explicitly specify `NoExecute` to prevent the pod from being evicted.

### 3. **Avoid Ambiguity**
- Without the `effect`, Kubernetes cannot determine whether the toleration applies to scheduling (`NoSchedule`), eviction (`NoExecute`), or preference (`PreferNoSchedule`).

### 4. **Granular Behavior**
- By specifying the `effect`, you can fine-tune pod behavior. For example:
  - Allow a pod to tolerate `NoSchedule` taints but not `NoExecute` taints.
  - Allow a pod to tolerate `PreferNoSchedule` taints for soft constraints.

---

## **Example: Taint and Toleration with Effect**

### **Taint on Node**
```bash
kubectl taint nodes node1 key=value:NoSchedule
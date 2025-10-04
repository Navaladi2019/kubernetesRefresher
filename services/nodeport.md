it maps port on a node to port on a pod

port range in node 30000 - 32767

if the pods are deployed in multiple nodes kubernetes creates service 
that spans across all nodes in such case i can use any node ip address and same port a


node port uses random algorithm to balance load to pod and session affinity as yes if multiple pod of same type is running inside a node.

kubectl get svc <service-name> -o jsonpath='{.spec.ports[0].nodePort}'


external application can access pod only via node port and only the application in the same cluster can access via cluster ip so external ingress is not handled by clusterip service.

kubectl describe svc <service name>


External Client
    |
    v
Node's IP + NodePort (e.g., http://<Node-IP>:31001)
    |
    v
Service Port (e.g., 8081)
    |
    v
Pod TargetPort (e.g., 80)

**When to Use NodePort**
- NodePort is useful for exposing a Service to the outside world without using an Ingress or LoadBalancer.
    However, it has limitations:
- The client must know the Node's IP address and the NodePort.
- It exposes the Service on every node, which might not be ideal for security or scalability.



 It is responsible for load balancing traffic across multiple Pods, even if those Pods are running on the same node or across different nodes.



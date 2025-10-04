- kubectl replace -f <filename> to apply chanes to replica set from file
- kubectl edit replicaset <name> to edit in vim 
- kubectl scale replicaset <name> --replicas = 5(number you want to scale to)
- kubectl get rs
- kubectl create rs -f <filename>
- kubectl delete replicaset <name>
- kubectl describe replicaset <name>

- Replication controller is older technology replaced by replica set

- If there are already Pods in the cluster with labels that match the selector, the ReplicationController will "adopt" those Pods and include them in its management.

Replication controller:

    - Replication controller always tries to keep the configured instance of pod always running.
    - Load balancing and scaling
    - Replication controller and replica set both have same purpose. replica set(older) is replaced            by                  replication controller

    
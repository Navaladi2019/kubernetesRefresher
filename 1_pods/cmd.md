kubectl run <name> --image=<imagename>

kubectl get pods (list all pods)

kubectl get pods -o wide (gets ip address of pods as well  with node name)

kubectl describe pods <podname>

kubectl delete pods <pod name>

kubectl edit pods <pod name>


kubectl create deployment nginx --image=nginx


 **kubectl apply command is used to create or update resources in Kubernetes.**
kubectl apply -f <yml file name>

kubectl create -f <yml file name>
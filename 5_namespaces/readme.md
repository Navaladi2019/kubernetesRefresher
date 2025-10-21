

three default namespaces

1) kube-system (netwok, dns)
2) default
3) kube-public


to access the resource in another namespace we have to append namespace + resouce name



service.namespace.svc.cluster.local is the fully qualified domain name of the service


cluster.local -> defaukt domain name
svc -> service


kubectl get pods  --namespace=<name space name>


kubectl create -f <filename> --namespace=<namespace name> to create resources in namespace


we can also move name space in the pod definition file under metadata

kubectl create namespace <namespace name>





kubectl config set-context $(kubectl config current-context) --namespace=<name> to set default namespace for the current context terminal


kubectl get pods --all-namespaces
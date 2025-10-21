- comfig maps are defined as key value pairs and these can be referred in pod definition file


kubectl create configmap <config map name> \ --from-literal=APP_COLOR=blue \ --from-literal=APP_MOD=prod


kubectl creae configmap <name> --from-file <filepath>


encrypting secret data at rest



secret type by default is opaque

kubectl create secret <secretname> --from-literal=<key>=<value>

by default secrets are store without encryption so to mitigate it we are going to us eencryption at rest



ps-aux | grep kube-api | grep "encryption-provider-config" to see if encryption is already enabled or not


also we can verify using
ls etc/etc/kubernetes/manifests/  and cat kube-apiserver

by default secrets are not encrypted and store to mitigate it we need to us eencryption at  rest.


after creating encryption config yaml file store it in master node location and link it to kube-apiserver
follow using the link https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/


sometimes instead of kubernetes secret we can use azure keyvalut with appropriate driver to store secrets 
 we just need to create secret provider class 

# if we do secret key ref then if the value od secret changes 
# then we need to restart the pod to have the secrets refreshed in env so to avoid it we can use volumne mount to have the key linked as mount in that way even if secret is changed mount is refreshed
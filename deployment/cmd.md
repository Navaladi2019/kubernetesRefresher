kubectl get all (to get all)

//deployments enclose replicasets

- kubectl rollout status deployment/<deployment name>
- kubectl rollout history deployment.apps/<mame> 
- kubectl rollout undo deployment/<name>
- kubectl delete deployment <name>


deployment strategy
    -Recreate (destroy all and create new instance) 
    - ROLLING UPDATE    (DEFAULT DEPLOYMENT STRATEGY)


WHEN WE UPDATE THE DEPLOYMENT IT CREATES NEW REPLICA SETS AND DEPLOY PODS THERE


kubectl create -f deployment.yml --record (command that caused the deployment command)


kubectl set image deployemnt <deploymentname> <containername>=<newimage> 
Above is to set new image of deployment
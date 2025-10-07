- scheduler identifies the nodes where the pod requires resources and allocated the pod to that node


Resource Requests means the guaranted or minimum or allocated esource for that container


cpu 1 or 0.1 -> 10m


1 count of cpu is

1 aws vcpu
1 gcp core
1 azure core
1 hyperthread

MEM -> 268Mi or 1Gi or 1 Mi or 1 G or 1M or iK  

A container cannot consume more cpu it will just throttle

A container can consume more memory that mentioned in the limits in those cases pod will be terminated with  OOM error

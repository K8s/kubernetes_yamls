Service is way to communicate the backend PODs using Loadbalancer which is
inbuild functionality of kubernetes, insteed of using external loadbalancer

Different values supported for type in service spec:

ClusterIP(default), NodePort, LoadBalancer, EnternalName

Supported Protocols:

TCP, UCP, HTTP, SCTP


Service can also be created in two ways:
Headless and Normal(clusterIP)

Default Kubernetes service type is clusterIP, When you create a headless
service by setting clusterIP None, no load-balancing is done and no cluster IP
is allocated for this service. Only DNS is automatically configured. When you
run a DNS query for headless service, you will get the list of the Pods IPs
and usually client dns chooses the first DNS record.

Example:
1)kubectl create deployment nginx --image=nginx
2)kubectl scale --replicas=3 deployment nginx
3)kubectl expose deployment nginx --name nginxheadless --cluster-ip=None
or for clusterIP
kubectl expose deployment nginx --name nginxclusterip --port=80  --target-port=80
4)kubectl run --generator=run-pod/v1 --rm utils -it --image arunvelsriram/utils bash
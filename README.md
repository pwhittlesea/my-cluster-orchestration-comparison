# My Cluster Orchestration Tool Comparison
A comparison of Cluster Orchestration Solutions.

| Requirement | [Kubernetes](http://kubernetes.io) | [Tutum](https://www.tutum.co) | [Rancher](http://rancher.com) | [Mesosphere](https://mesosphere.com) |
| --------------- | --- | --- | --- | --- |
| Production Ready (not beta/alpha) | Y | N | N | |
| Service Discovery by DNS | Y | Y | Y | |
| Service Discovery of External services (E.g. RDS) | [?](#k8s-service-discovery-of-external-services) | | | |
| Rolling Updates | Y | | | |
| Local Deployments | Y | [Y](#tutum-local-deployments) | | |
| Autoscaling of Services | [?](#k8s-autoscaling) | | | |
| Private Docker registry support | [Y](#k8s-private-registry-support) | | | |
| Deploy multiple Clusters at the same time | [Y](#k8s-multiple-clusters) | | | |
| Secure container communication | | Y | | |
| Manage public load balancers | [Y](#k8s-public-load-balancers) | | | |
| Service Health Checks | Y | | Y | |
| UI | [?](#k8s-ui) | Y | Y | Y |
| Container failure recovery (start another) | Y | Y | Y | Y |
| Tagging | Y | | Y | |
| Service Graph | N | | Y | |

## Notes
## Kubernetes
#### K8S Service Discovery of External Services
You can create 'services' which map to static IPs but you cannot currently create a 'CNAME' for a service. This is unsuiltable for something that may change IP, like RDS.
#### K8S Autoscaling
This is currently in Beta
#### K8S Private Registry Support
Done using *secrets* on each service you define. Kinda clumsy.
#### K8S Multiple Clusters
Using Namespaces.
#### K8S Public Load Balancers
Kubernetes can create ELBs for specific services.
#### K8S UI
It shows minimal state but does not provide any control.

## Tutum
#### Tutum Local Deployments
As far as I can tell, Tutum is a BYOH (bring your own hardware) so local deployments are possible because Tutum is a hosted API and your hardware 'dials in'.

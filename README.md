# My Cluster Orchestration Tool Comparison
A comparison of Cluster Orchestration Solutions.

Comparing:
- [ECS](https://aws.amazon.com/ecs/details/)
- [Kubernetes](http://kubernetes.io)
- [Tutum](https://www.tutum.co)
- [Rancher](http://rancher.com)
- [Mesosphere](https://mesosphere.com) (implicitly including Marathon)
- [Shipyard](http://shipyard-project.com)
- [vamp](http://vamp.io)
- [lattice](http://lattice.cf)
- [helios](https://github.com/spotify/helios)
- [deis](http://deis.io)

Key:
- **blank** = not looked into it
- Y = supported
- N = not supported
- ? = Possibly (see notes)

| Project Status | ECS | Kubernetes | Tutum | Rancher | Mesosphere | Shipyard | vamp | lattice | helios | deis |
| --------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Production Ready (not beta/alpha) | Y | Y | N | N | Y | ? | N | ? | Y | Y |

|  Must Have Requirement | ECS | Kubernetes | Tutum | Rancher | Mesosphere | Shipyard | vamp | lattice | helios | deis |
| --------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Service Discovery by DNS        | [?](#ecs-service-discovery-by-dns) | Y                                  | Y                             | Y | Y | | | | | |
| Local Deployments (testing)     | N                                  | Y                                  | [Y](#tutum-local-deployments) | Y | Y | | | | | |
| Private Docker registry support | [?](#ecs-private-registry-support) | [Y](#k8s-private-registry-support) | Y                             | Y | Y | | | | | |
| Service Health Checks           | [?](#ecs-health-checks)            | Y                                  | ?                             | Y | Y | | | | | |
| Container failure recovery      | Y                                  | Y                                  | Y                             | Y | Y | | | | | |
| API/CLI                         | Y                                  | Y                                  | Y                             | Y | Y | | | | | |

| Should Have Requirement | ECS | Kubernetes | Tutum | Rancher | Mesosphere | Shipyard | vamp | lattice | helios | deis |
| --------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Service Discovery of External services (E.g. RDS) | [?](#ecs-service-discovery-of-external-services) | [?](#k8s-service-discovery-of-external-services) |   | Y | N | | | | | |
| Multi-tenancy                                     | N                                                | [Y](#k8s-multi-tenancy)                          |   | Y | Y | | | | | |
| Tagging                                           | N                                                | Y                                                |   | Y | Y | | | | | |
| Random port for services (no host/port conflicts) | N                                                |                                                  | Y | Y | Y | | | | | |

| Nice To Have Requirement | ECS | Kubernetes | Tutum | Rancher | Mesosphere | Shipyard | vamp | lattice | helios | deis |
| --------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Rolling Updates                | Y                     | Y                               |   | Y |   |   |   |   |   |   |
| Autoscaling of Services        | [?](#ecs-autoscaling) | [?](#k8s-autoscaling)           |   |   |   |   |   |   |   |   |
| Secure container communication |                       |                                 | Y |   |   |   |   |   |   |   |
| Manage public load balancers   | N                     | [Y](#k8s-public-load-balancers) | N | N | N | N | N | N | N | N |
| UI                             | Y                     | [?](#k8s-ui)                    | Y | Y | Y |   |   |   |   |   |
| Service Graph                  | N                     | N                               |   | Y |   |   |   |   |   |   |

| API support | ECS | Kubernetes | Tutum | Rancher | Mesosphere | Shipyard | vamp | lattice | helios | deis |
| --------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [Docker Machine](https://docs.docker.com/machine/) | N | N | N | Y | N | N | N                        | N | N | N |
| [Docker Swarm](https://docs.docker.com/swarm/)     | N | N | N | N | N | Y | [?](#vamp-swarm-support) | N | N | N |

## Notes
## EC2 Container Service (ECS)
#### ECS Service Discovery by DNS
I really want to mark this as no but it does support it. You have to create an internal ELB and a Route 53 entry for your service.
It is by no means easy and in my opinion forces Developers to delve into the hardware which takes away isolation of architecture layers.
#### ECS Service Discovery of External Services
Can be done by creating a Route 53 entity.
#### ECS Autoscaling
I think this can be done if you set up Cloudwatch.
#### ECS Private Registry Support
Have to add credentials to all hardware hosts before system start. Really clumsy (changing whilst running would suck).
#### ECS Health Checks
It will check if the container has stopped. Pretty sure thats it. Unless its behind a ELB.

## Kubernetes
#### K8S Service Discovery of External Services
You can create 'services' which map to static IPs but you cannot currently create a 'CNAME' for a service. This is unsuiltable for something that may change IP, like RDS.
#### K8S Autoscaling
This is currently in Beta
#### K8S Private Registry Support
Done using *secrets* on each service you define. Kinda clumsy.
#### K8S Multi-tenancy
Using Namespaces.
#### K8S Public Load Balancers
Kubernetes can create ELBs for specific services.
#### K8S UI
It shows minimal state but does not provide any control.

## Tutum
#### Tutum Local Deployments
As far as I can tell, Tutum is a BYOH (bring your own hardware) so local deployments are possible because Tutum is a hosted API and your hardware 'dials in'.

## vamp
#### vamp Swarm Support
Planned.

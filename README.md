# Jenkins Helm Chart

Jenkins master and slave cluster utilizing the Jenkins Kubernetes plugin

* https://wiki.jenkins-ci.org/display/JENKINS/Kubernetes+Plugin

Inspired by the awesome work of Carlos Sanchez <mailto:carlos@apache.org>

## Chart Details

This chart will do the following:

* 1 x Jenkins Master with port 8080 exposed on an external LoadBalancer
* All using Kubernetes Deployments

### Modify Ingress Controller to use [LoadBalancerPublicIp].nip.io
```bash
$ LB_HOST=$(kubectl -n ingress-nginx get svc ingress-nginx -o jsonpath="{.status.loadBalancer.ingress[0].hostname}")
$ LB_IP="$(dig +short $LB_HOST | tail -n 1)"
$ echo $LB_HOST;HOST="jenkins.$LB_IP.nip.io"
$ echo $HOST
```

## Installing the Chart

To install the chart with the release name `jenkins`:

```bash
$ helm install stable/jenkins \
    --name jenkins \
    --namespace default \
    --values jenkins-values.yaml \
    --set Master.HostName=$HOSTs
```

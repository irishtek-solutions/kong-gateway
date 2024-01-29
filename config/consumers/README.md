# Working with your first Consumer

**Consumer:** typically refers to an entity that consumes or uses the APIs managed by Kong. Consumers can be applications, services, or users who interact with your APIs. Kong allows you to define and manage consumers, apply access control policies, and monitor their usage of APIs.

Consumers in Kong are often associated with key authentication, OAuth, or other authentication and authorization mechanisms. They are essential for controlling access to your APIs, tracking usage, and ensuring security.

**Pre-requisite:** Kongs Gateway up and running.

## How to create a Consumer in the UI - Video

[Youtube video on creating a Consumer](https://youtu.be/pS2iqOjRK9o)

## Video on how to create a Consumer using Deck

[Youtube video on creating a Consumer using Deck](https://youtu.be/9s33A6h6N5g)

To install this using deck:

1. Navigate to this directory
2. Make sure you have deck [installed](https://docs.konghq.com/deck/latest/installation/)
3. Make sure you can connect: `deck gateway ping --headers Kong-Admin-Token:<token> --kong-addr http://<kong-admin-endpoint>` should return a successful response `Successfully connected to Kong! Kong version:  3.5.0.0`
4. Run deck sync: `deck gateway sync --headers Kong-Admin-Token:<token> --kong-addr http://<kong-admin-endpoint> kong.yaml`

## Deploy your first Consumer using the Admin API

[Youtube video on creating a Consumer using the Admin API](https://youtu.be/FByjJNS1bsA)


## Deploy your first Consumer using KIC

[Youtube video on creating a Consumer using the KIC](https://youtu.be/1cqYRYilvoE)


**Pre-requisite**

Make sure you have Kong Ingress Controller installed and it's working. When running  `kubectl get svc,po -n kong` it should look something like below:

```
$  kubectl get po,svc -n kong
NAME                                          READY   STATUS      RESTARTS      AGE
pod/kong-kong-5b9f85dcf7-gtqvt                2/2     Running     6 (21h ago)   2d12h
pod/kong-kong-post-upgrade-migrations-5x6pj   0/1     Completed   0             2d12h
pod/kong-kong-pre-upgrade-migrations-rktkx    0/1     Completed   0             2d12h
pod/kong-postgresql-0                         1/1     Running     0             2d12h

NAME                                   TYPE           CLUSTER-IP     EXTERNAL-IP    PORT(S)                      AGE
service/kong-kong-admin                NodePort       10.80.15.21    <none>         8001:32488/TCP               2d12h
service/kong-kong-cluster              ClusterIP      10.80.7.37     <none>         8005/TCP                     2d12h
service/kong-kong-clustertelemetry     ClusterIP      10.80.10.87    <none>         8006/TCP                     2d12h
service/kong-kong-manager              NodePort       10.80.13.231   <none>         8002:30924/TCP               2d12h
service/kong-kong-proxy                LoadBalancer   10.80.10.58    <IP>   80:32035/TCP,443:32689/TCP   2d12h
service/kong-kong-validation-webhook   ClusterIP      10.80.3.0      <none>         443/TCP                      2d12h
service/kong-postgresql                ClusterIP      10.80.11.229   <none>         5432/TCP                     2d12h
service/kong-postgresql-hl             ClusterIP      None           <none>         5432/TCP                     2d12h
```

1. **Install Echo deployment:** `kubectl apply -f 1-consumer.yaml`
2. **Check to see if consumer is installed:** `kubectl get KongConsumer -n testing`
# Working with your first Upstream and Target

In Kong, "Upstreams" and "Targets" are concepts related to load balancing, which is a mechanism for distributing incoming requests across multiple instances of a backend service to improve performance, scalability, and fault tolerance.

**Upstream:**

- An Upstream in Kong represents a group or collection of one or more instances of a backend service. It is essentially a logical entity that defines a set of targets (individual instances of a service) and contains configuration settings related to load balancing.
- Upstreams enable you to group multiple instances of a service under a single umbrella, allowing Kong to distribute incoming requests among them based on a chosen load-balancing algorithm.
- Configuration for an Upstream includes settings such as the load balancing algorithm, health checks, and other parameters.

**Target:**

- A Target is an individual instance of a backend service associated with an Upstream. It represents a specific server or node that can handle requests for a particular service.
- Targets are the actual endpoints where Kong forwards incoming requests for load balancing. Each target is associated with an Upstream, and Kong dynamically distributes traffic among the available targets based on the configured load-balancing algorithm.
- When a request arrives at Kong, it selects a target within the associated Upstream and forwards the request to that target.

![Upstream Targets](../images/upstreams-targets-new-no-trans.png)

**Pre-requisite:** Kong Gateway up and running.

## How to create an Upstream and Target the UI

[Youtube video on creating A Upstream and Target]()

## Video on how to create an Upstream and Target using Deck

[Youtube video on creating A Upstream and Target using Deck]()

To install this using deck:

1. Navigate to this directory
2. Make sure you have deck [installed](https://docs.konghq.com/deck/latest/installation/)
3. Make sure you can connect: `deck gateway ping --headers Kong-Admin-Token:<token> --kong-addr http://<kong-admin-endpoint>` should return a successful response `Successfully connected to Kong! Kong version:  3.5.0.0`
4. Run deck sync: `deck gateway sync --headers Kong-Admin-Token:<token> --kong-addr http://<kong-admin-endpoint> kong.yaml`
5. 
```
creating service Upstream-Example
creating upstream upstream-example
creating route Upstream-example
creating target google.com:80 for upstream deebcedd-7be5-4fce-83fb-c954c81603e4
creating target httpbin.org:80 for upstream deebcedd-7be5-4fce-83fb-c954c81603e4
Summary:
  Created: 5
  Updated: 0
  Deleted: 0
```

1. You should now see it toggle between `google.com` and `httpbin.org` when calling the `/api` endpoint for the proxy for 50% of the time.

![target 1](../images/target-1.png)


![target 2](../images/target-2.png)

## Deploy your firstUpstream and Target using the Admin API

[Youtube video on creating A Upstream and Target using the Kongs Admin API]()

## Deploy your firstUpstream and Target using KIC

[Youtube video on creating A Upstream and Target using KIC]()

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

1. **Install Echo deployment:** `kubectl apply -f 1-create-echo.yaml`
2. **Add Ingress Resource:** `kubectl apply -f 2-echo-ingress.yaml` 
3. **Upstreams and targets get automatically set**
4. **Scale the echo deployment. You'll notice additional targetsb get added automatically:**  `kubectl scale deployment echo --replicas=1 -n testing`
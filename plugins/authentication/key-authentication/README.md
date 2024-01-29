# How to use the Key Authentication Plugin

- [How to use the Key Authentication Plugin](#how-to-use-the-key-authentication-plugin)
  - [What is the Key Authentication?](#what-is-the-key-authentication)
  - [Watch the video on how to use the key-authentication plugin](#watch-the-video-on-how-to-use-the-key-authentication-plugin)
  - [Installation using Deck](#installation-using-deck)
  - [Installation using KIC](#installation-using-kic)

## What is the Key Authentication?

**Key authentication:** also known as API key authentication or token-based authentication, involves using a unique API key or token to authenticate and authorize access to an API. When a client sends a request to an API, they include their API key in the request (typically via a header or query param). When it comes to Key Authentication and using it at the Gateway, the API gateway then validates the key and grants access if it's valid.

**How to do it with Kong**

1. Create a Service and Route
2. Test to see if we can proxy request with a key or no key
3. Enable Kong’s Key Authentication Plugin
4. Try to access the API now. We will not be able to access the API.
5. Create a consumer in Kong
6. Provision the Consumer a Key
7. Test the API with the newly created key credential

![Key Auth](../../images/key-auth.png)

## Watch the video on how to use the key-authentication plugin

[Using Key Authentication](https://www.youtube.com/watch?v=AamUp3JBB6o)
[Using Key Authentication with KIC](https://www.youtube.com/watch?v=TOUhx9eF4nQ)


## Installation using Deck

To install this using deck:

1. Navigate to this directory
2. Make sure you have deck [installed](https://docs.konghq.com/deck/latest/installation/)
3. Make sure you can connect: `deck gateway ping --headers Kong-Admin-Token:<token> --kong-addr http://<kong-admin-endpoint>` should return a successful response `Successfully connected to Kong! Kong version:  3.5.0.0`
4. Run deck sync: `deck gateway sync --headers Kong-Admin-Token:<token> --kong-addr http://<kong-admin-endpoint> --select-tag key-auth-example kong.yaml`

## Installation using KIC

**Pre-requisite**

Make sure you have Kong Ingress Controller installed and it's working. When running  `kubectl get svc,po -n kong` it should look something similar like below:

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
service/kong-kong-proxy                LoadBalancer   10.80.10.58    34.41.87.189   80:32035/TCP,443:32689/TCP   2d12h
service/kong-kong-validation-webhook   ClusterIP      10.80.3.0      <none>         443/TCP                      2d12h
service/kong-postgresql                ClusterIP      10.80.11.229   <none>         5432/TCP                     2d12h
service/kong-postgresql-hl             ClusterIP      None           <none>         5432/TCP                     2d12h
```

1. **Install Echo deployment:** `kubectl apply -f 1-create-echo.yaml`
2. **Add Ingress Resource:** `kubectl apply -f 2-echo-ingress.yaml` 
3. **Note: `konghq.com/plugins: key-auth-plugin` ingress annotation is already present for the plugin**
4. **Proxy to the endpoint:** Using insomnia or `curl http://<kong-proxy-endpoint>:<port>/key-auth`
5. **Add the plugin resource:** `kubectl apply -f 3-key-auth-plugin.yaml`
6. **Proxy to the endpoint, plugin is now enabled:** Using insomnia or `curl http://<kong-proxy-endpoint>:<port>/key-auth`
7. **Create a credential secret for consumer "John", with key "john-key" :** `kubectl apply -f 4-create-credentials.yaml`
8. **Create a consumer called "john" who has the credential created in the previous step:** `kubectl apply -f 5-create-consumer.yaml `
9. **Test to see if you can now get access to the API by using credentials:** Using insomnia or curl:

```
curl --request GET \
  --url http://<kong-proxy>/key-auth \
  --header 'apikey: john-key'
```
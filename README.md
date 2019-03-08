# Trending Topics Campaigns (TTC) - Helm Charts

For documentation, please refer to [TTC Docs](https://github.com/Activiti/ttc-docs)

Note: This is not a GitHub Pages repo. Please clone the repo to use the chart.

Currently only the backend of the example as the UI is not yet fully parameterised. To be used for running ttc-acceptance-tests

## Notes for using Docker for Desktop (with local k8s cluster)

Here are some notes that may help you to run the example locally using Docker for Desktop with a local k8s cluster. 
Note: other options include using minikube or installing onto a remote k8s cluster running in your favourite cloud provider, eg. AWS, Azure or GCP.

1. Change to ttc-example directory

```
cd /charts/ttc-example
```

2. Find your host ip address. On Mac, use System Preferences -> Network pane or you may be able to use:

```
ipconfig getifaddr en0
```

In my case, the ip address was 10.15.240.126

3. As sudo, add following to your /etc/hosts file

```
10.15.240.126       activiti-cloud-gateway
10.15.240.126       activiti-keycloak
```
 
replacing 10.15.240.126 with your ip address above. Note: due to KeyCloak auth, you will not be able to use localhost, 10.0.0.1 or 127.0.0.1.

4. Edit your local copy of values.yaml

You will need to remove "jx-staging.35.197.207.143.nip.io" in three places. 

For reference, here are the the example diffs:

```
 global:
   keycloak:
-    url: "http://activiti-keycloak.jx-staging.35.197.207.143.nip.io/auth"
+    url: "http://activiti-keycloak/auth"
```

```
           hosts:
-            - "activiti-keycloak.jx-staging.35.197.207.143.nip.io"
+            - "activiti-keycloak"
```

```
   activiti-cloud-gateway:
     ingress:
       enabled: true
-      hostName: "activiti-cloud-gateway.jx-staging.35.197.207.143.nip.io"
+      hostName: "activiti-cloud-gateway"

```

Note: do not try to push these changes back.

5. use helm install

eg. using default namespace with auto-generated release name
```
helm install -f values.yaml .
```
eg. using a previous created namespace and specific release name
```
kubectl create namespace my-namespace
helm install -f values.yaml --namespace=my-namespace --name my-name .
```

6. Use kubectl (or k8s dashboard) to check that all pods are running and ready

```
kubectl get pods --namespace=my-namespace
```

Depending on your k8s cluster, you may need to wait 5 to 10 minutes for all pods to be fully up and ready

7. Use the Postman Collection to sanity check your deployed example

Please refer to [TTC Docs](https://github.com/Activiti/ttc-docs)

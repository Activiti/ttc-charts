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

2. Find your host ip

```
kubectl describe node docker-for-desktop  | grep InternalIP | awk '{print $2}'
```

3. copy values.yaml to my-values.yaml

You will need to edit and replace "jx-staging.35.197.207.143" with your host ip in three places. Alternatively,
you can create your own my-values.yaml and use that as a parameter to the helm install command.

4. use helm install

eg. using default namespace with auto-generated release name
```
helm install -f my-values.yaml .
```
eg. using a previous created namespace and specific release name
```
kubectl create namespace my-namespace
helm install -f my-values.yaml --namespace=my-namespace --name my-name .
```

5. Use kubectl (or k8s dashboard) to check that all pods are running and ready

```
kubectl get pods --namespace=my-namespace
```

Depending on your k8s cluster, you may need to wait 5 to 10 minutes for all pods to be fully up and ready

6. Use the Postman Collection to sanity check your deployed example

Please refer to [TTC Docs](https://github.com/Activiti/ttc-docs)

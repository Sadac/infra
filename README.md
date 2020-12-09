# k8s

## Deployment
posts-depl.yaml
1. Make sure the Deployment config file is using the `latest` tag in the pod spec
2. Make any update on the code
3. Build the image
```bash
docker build -t roccosada/posts .
```
4. Push the image to the docker registry
```bash
docker push roccosada/posts
```
5. Restart the Deployment
```bash
kubectl rollout restart deployment [deployment_name]
```

## Service
posts-srv.yaml
1. To apply a Service: 
```bash
kubectl apply -f posts-srv.yaml
```
2. To get the port and communicate with the microservice from outisde the cluster you can execute
```bash
kubectl describe service posts-srv
```
and then, take the `NodePort: posts  31306/TCP` and just hit the endpoint, for example:
`http://localhost:31306/posts`

## Setup the ingress-nginx
1. In order to create a Load Balancer + Ingress we can use the
https://kubernetes.github.io/ingress-nginx/deploy/#provider-specific-steps project, and apply the manifest depending on our OS.
For Mac:
```sh
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.41.2/deploy/static/provider/cloud/deploy.yaml
```
2. Create an ingress-srv.yaml to teach the Ingress Controller how to route the incoming requests to the different pods.
The Ingress Controller is just a manifest that indicates the router rules
Then apply it
```sh
kubectl apply -f ingress-srv.yaml
```
3. Add in etc/hosts a redirection to the host defined in the manifest `- host: posts.com`
```127.0.0.1 posts.com``` so every time we try to go posts.com, a redirection its being made
```http://posts.com/posts``` is like we're trying ```http://localhost:31306/posts```
take the port from `kubectl describe service posts-srv`

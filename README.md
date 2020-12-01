# k8s

## Deployment
posts-depl.yaml
1. Make sure the Deployment config file is using the `latest` tag in the pod spec
2. Make any update on the code
3. Build the image
```docker build -t roccosada/posts .```
4. Push the image to the docker registry
```docker push roccosada/posts```
5. Restart the Deployment
```kubectl rollout restart deployment [deployment_name]```

## Service
posts-srv.yaml
1. To apply a Service: ```kubectl apply -f posts-srv.yaml```
2. To get the port and communicate with the microservice from outisde the cluster you can execute
```kubectl describe service posts-srv```
and then, take the `NodePort: posts  31306/TCP` and just hit the endpoint, for example:
`http://localhost:31306/posts`

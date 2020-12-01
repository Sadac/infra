# k8s

## Deployment
1. Make sure the Deployment config file is using the `latest` tag in the pod spec
2. Make any update on the code
3. Build the image
`docker build -t roccosada/posts .`
4. Push the image to the docker registry
`docker push roccosada/posts`
5. Restart the Deployment
`kubectl rollout restart deployment [deployment_name]`

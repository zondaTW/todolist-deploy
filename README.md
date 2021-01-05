# todolist deploy

## Run

### Docker compose

```shell
$ docker-compose up -d
```

### Kubernetes

Modify secret files in k8s directory:  
* api-secret.yaml  
    example:  
    ```yaml
    apiVersion: v1
    kind: Secret
    metadata:
    name: api-secret
    data:
    auth-key: c2VjcmV0a2V5 # secretkey that encoded by base64
    ```
* postgres-secret.yaml  
    example:  
    ```yaml
    apiVersion: v1
    kind: Secret
    metadata:
    name: postgres-secret
    data:
    password: cGFzc3dvcmQ= # password that encoded by base64
    ```

When you use minkube, need to:  
`$ minikube addons enable ingress`  
`$ minikube addons enable metrics-server`  

Apply:  
`$ kubectl apply -f k8s`  
Get ip address:  
`$ kubectl get ingress.extensions/ingress-service`  
Get Weave Scope external port:  
`kubectl get svc -n weave`  

## Reference

[The Kubernetes Handbook](https://www.freecodecamp.org/news/the-kubernetes-handbook/)  
[Installing Weave Scope](https://www.weave.works/docs/scope/latest/installing/#orchestrators)  

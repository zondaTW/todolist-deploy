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

Apply:  
`$ kubectl apply -f k8s`  
and get ip address:  
`$ kubectl get ingress.extensions/ingress-service`  

# Kubernetes RBAC

```
1. Download openssl
2. KIND
    - docker cp NAMA_CONTAINER:/etc/kubernetes/pki/ca.crt ca.crt
    - docker cp NAMA_CONTAINER:/etc/kubernetes/pki/ca.key ca.key

3. openssl genrsa -out developer.key 2048
4. openssl req -new -key developer.key -out developer.csr -subj "/CN=Developer/O=Developer"
5. openssl x509 -req -in developer.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out developer.crt -days 7

6. export KUBECONFIG=~/.kube/kind-developer

7. kubectl config set-cluster kind-studi-devops --server=https://192.168.49.2 --certificate-authority=ca.crt --embed-certs=true
8. kubectl config set-credentials Developer --client-certificate=developer.crt --client-key=developer.key --embed-certs=true
9. kubectl config set-context developer --cluster=kind-studi-devops --user=Developer
10. kubectl config use-context developer
```
Minikube:
```
minikube start --driver=docker --extra-config="apiserver.authorization-mode=Node,RBAC"
```

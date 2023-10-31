# Service Account
```
apiVersion: v1
kind: ServiceAccount
metadata:
  name: developer-app
  namespace: default
```

# Secret
```
apiVersion: v1
kind: Secret
metadata:
  name: token-developer-app
  namespace: default
  annotations:
    kubernetes.io/service-account.name: developer-app
type: kubernetes.io/service-account-token
```

# Test List of Pods
```
# Replace the placeholders with your actual values
KUBE_API_SERVER="https://192.168.76.2:8443"
KUBE_API_VERSION="api/v1"
NAMESPACE="development"
TOKEN="YOUR TOKEN"

# Curl command to list pods in the specific namespace
curl -X GET "$KUBE_API_SERVER/$KUBE_API_VERSION/namespaces/$NAMESPACE/pods" -H "Authorization: Bearer $TOKEN" -k
```
don't forget add service account to kubernetes `role binding`
```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: development
subjects:
- kind: ServiceAccount
  name: developer-app
  namespace: development
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

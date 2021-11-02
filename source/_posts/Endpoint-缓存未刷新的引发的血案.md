---
title: Endpoint 缓存未刷新的引发的血案
categories:
- kubernetes
tags: 
- kubernetes
date: 2019-11-02 23:57:59
---



rancher中偶遇配置不生效，可以直接用执行kubetcl命令

<!--more-->




# 查看指定endpoint

```
kubectl get ep rhea-service --namespace=app
```

# 导出endpoint yaml配置

```
> kubectl get ep rhea-service --namespace=app -o yaml
apiVersion: v1
kind: Endpoints
metadata:
  creationTimestamp: "2019-11-27T03:19:52Z"
  labels:
    cattle.io/creator: norman
  name: rhea-service
  namespace: app
  resourceVersion: "27649995"
  selfLink: /api/v1/namespaces/app/endpoints/rhea-service
  uid: a725c92b-d125-4c5b-bcd0-57a16cf56ad3
subsets:
- addresses:
  - ip: 10.42.0.247
    nodeName: dev-master
    targetRef:
      kind: Pod
      name: cw-hotpot-backend-6b6869df6c-dxmc5
      namespace: app
      resourceVersion: "27649990"
      uid: 24ac3c44-61a7-4466-baa0-1a793ebb2cea
  - ip: 10.42.0.66
    nodeName: dev-master
    targetRef:
      kind: Pod
      name: cw-rhea-d9657c9db-tlkdm
      namespace: app
      resourceVersion: "27649992"
      uid: 6f6208eb-a1f3-4d28-9b6d-24a907e7d354
  - ip: 10.42.2.157
    nodeName: dev-gpu-worker2
    targetRef:
      kind: Pod
      name: cw-hotpot-backend-6b6869df6c-2vxmd
      namespace: app
      resourceVersion: "27649991"
      uid: 4e8d44c3-7582-4050-8d0c-595d0f760fdc
  ports:
  - name: default
    port: 42
    protocol: TCP
```



# 删除指定的endpoint

```
kubectl delete ep rhea-service --namespace=app
```


# 修改 endpoint yaml配置 并重新创建

```
apiVersion: v1
kind: Endpoints
metadata:
  creationTimestamp: "2019-11-27T03:19:52Z"
  labels:
    cattle.io/creator: norman
  name: rhea-service
  namespace: app
  resourceVersion: "27649995"
  selfLink: /api/v1/namespaces/app/endpoints/rhea-service
  uid: a725c92b-d125-4c5b-bcd0-57a16cf56ad3
subsets:
- addresses:
  - ip: 10.42.2.62
    nodeName: dev-master
    targetRef:
      kind: Pod
      name: cw-rhea-d9657c9db-tlkdm
      namespace: app
      resourceVersion: "27649992"
      uid: 6f6208eb-a1f3-4d28-9b6d-24a907e7d354
  ports:
  - name: default
    port: 42
    protocol: TCP
```






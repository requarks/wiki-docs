---
title: Kubernetes
description: Getting started with a Kubernetes installation using Helm Charts
published: true
date: 2020-04-19T22:49:08.309Z
tags: setup, docker
---

# Prerequisites

- A Kubernetes cluster
- [Helm](https://helm.sh/docs/using_helm/#installing-helm)
- PostgreSQL Database

# Important

- **You must deploy a single instance in order to setup the application.** Once setup is completed, you can increase the number of replicas to any amount.
- Even though Wiki.js supports other database engines, using **PostgreSQL is a requirement** for multiple replicas.

# Install the Helm Chart

*Coming soon*

# Install the yaml file

## Create the settings to pod 

1. Create a yaml file with name requarks-settings.yaml and copy and paste this code

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: requarks-settings
  labels:
    app: requarks
# Replace with your infos
data:
  DB_TYPE: mssql
  DB_HOST: mydatabase
  DB_PORT: "1433"
  DB_USER: ""
  DB_NAME: requarks
  DB_SSL: "false"
  
---
apiVersion: v1
kind: Secret
metadata:
  name:  requarks-secrets
  labels:
   app: requarks
data:
   DB_PASS:  QkFTRTY0X0VOQ09ERURfVkFMVUU= #replace with the pass encoded with base64
type: Opaque

```
2. Create the setting on cluster

```yaml

kubectl apply -f ./requarks-settings.yaml -n <your-namespace>

```
3. Create a yaml file with name requarks-service.yaml and copy and paste this code

> this sample is based on environment with edge router, so service no has external ip and ssl

```yaml
kind: Service
apiVersion: v1
metadata:
  name: requarks-service
  labels:
    app: requarks
spec:
  selector:
    app: requarks
  type: ClusterIP
  ports:
  - name:  http
    port:  80
    targetPort:  3000

```

```yaml
kubectl apply -f ./requarks-service.yaml  -n <your-namespace>
```


4. Create kubernetes deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: requarks
spec:
  selector:
    matchLabels:
      app: requarks
  template:
    metadata:
      labels:
        app: requarks
    spec:
      containers:
      - name: requarks
        image: requarks/wiki:2
        env:
        - name: DB_PASS
          valueFrom:
            secretKeyRef:
              name: requarks-secrets
              key: DB_PASS
        envFrom:
          - configMapRef:
            name: requarks-settings          
        resources:
          limits:
            memory: "128Mi"
            cpu: "500m"
        ports:
        - containerPort: 3000

```

 

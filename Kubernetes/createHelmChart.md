# Helm Chart

## 创建chart

默认创建chart,这里会创建默认web-ui的chart

> helm create web-ui

## chart中设置secret

拉image的仓库可能是私有仓库，于是这里会需要校验，这个secret一般存放目录为values.yaml

```yaml
containers:
  image:
    # If pulling from a private repository then need to reference full path
    repository: "web-ui"
    tag: latest
    pullPolicy: Always
    pullSecretName: use-secret-such-as-this

```

## 部署后访问url的位置设置

在values.yaml文件中设置

```yaml
global:
  environmentTag: "PROD"
  ingress:
    host: web-ui

```

以上会被ingress.yaml调用到

ref: <https://kubernetes.io/docs/concepts/services-networking/ingress/>

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: {{ .Values.service.name | default .Chart.Name }}
  namespace: {{ .Release.Namespace }}
  {{- template "ace.labels" . }}
  annotations:
    ingress.kubernetes.io/tls-minimum-version: "1.2"
    ingress.kubernetes.io/ssl-redirect: "true"
    ingress.kubernetes.io/secure-backends: "true"
    ingress.kubernetes.io/backend-protocol: HTTP
    kubernetes.io/ingress.class: nginx
    ingress.kubernetes.io/rewrite-target: /{{ .Values.service.path }}
spec:
  rules:
  - host: {{ .Values.global.ingress.host }}
    http:
      paths:
      - path: /
        backend:
          serviceName: {{ .Values.service.name | default .Chart.Name }}
          servicePort: {{ .Values.service.securePort }}

```

## 创建pv

```yaml
kind: PersistentVolume
apiVersion: v1
metadata:
  name: pv0001
  labels:
    type: local
spec:
  capacity:
    storage: 20Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /disk/

```

## 创建pvc

```yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 20Gi

```

## 使用pvc

需要在deployment.yaml中，volumes生命这个pvc的名字，以下仅列出pvc被引用部分

```yaml
spec:
  template:
    spec:
      containers:
          volumeMounts:
            # This name must match the volumes.name below.
            - name: data-disk
              mountPath: /disk
      volumes:
        - name: data-disk
          persistentVolumeClaim:
            claimName: web-ui

```

## helm install

> helm install --name this-name-is-deploy-name --namespace this-is-name-space this-is-chart-name-or-folder-name

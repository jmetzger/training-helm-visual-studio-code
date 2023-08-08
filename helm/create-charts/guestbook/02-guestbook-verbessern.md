# Guestbook verbessern (Hooks)

## Step 1: 

```
cd
mkdir guestbook/templates/backup
touch guestbook/templates/backup/persistentVolume-claim.yaml
touch guestbook/templates/backup/job.yaml
```

## Step 2: persistentvolumeclaim.yaml und job bevölkern 

```
# nano guestbook/templates/backup/persistentVolume-claim.yaml

{{- if .Values.redis.master.persistence.enabled }}
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: redis-data-{{ .Values.redis.fullnameOverride }}-master-0-backup-{{ sub .Release.Revision 1 }}
  labels:
    {{- include "guestbook.labels" . | nindent 4 }}
  annotations:
    "helm.sh/hook": pre-upgrade
    "helm.sh/hook-weight": "0"
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: {{ .Values.redis.master.persistence.size }}
{{- end }}
```

```
# nano guestbook/templates/backup/job.yaml
{{- if .Values.redis.master.persistence.enabled }}
apiVersion: batch/v1
kind: Job
metadata:
  name: {{ include "guestbook.fullname" . }}-backup
  labels:
    {{- include "guestbook.labels" . | nindent 4 }}
  annotations:
    "helm.sh/hook": pre-upgrade
    "helm.sh/hook-delete-policy": before-hook-creation,hook-succeeded
    "helm.sh/hook-weight": "1"
spec:
  template:
    spec:
      containers:
        - name: backup
          image: redis:alpine3.11
          command: ["/bin/sh", "-c"]
          args: ["redis-cli -h {{ .Values.redis.fullnameOverride }}-master save && cp /data/dump.rdb /backup/dump.rdb"]
          volumeMounts:
            - name: redis-data
              mountPath: /data
            - name: backup
              mountPath: /backup
      restartPolicy: Never
      volumes:
        - name: redis-data
          persistentVolumeClaim:
            claimName: redis-data-{{ .Values.redis.fullnameOverride }}-master-0
        - name: backup
          persistentVolumeClaim:
            claimName: redis-data-{{ .Values.redis.fullnameOverride }}-master-0-backup-{{ sub .Release.Revision 1 }}
{{- end }}
```

## Step 3: pre-rollback hook erstellen 

```
mkdir guestbook/templates/restore
touch guestbook/templates/restore/job.yaml
```

```
# nano guestbook/templates/restore/job.yaml
{{- if .Values.redis.master.persistence.enabled }}
apiVersion: batch/v1
kind: Job
metadata:
  name: {{ include "guestbook.fullname" . }}-restore
  labels:
    {{- include "guestbook.labels" . | nindent 4 }}
  annotations:
    "helm.sh/hook": pre-rollback
    "helm.sh/hook-delete-policy": before-hook-creation,hook-succeeded
spec:
  template:
    spec:
      containers:
        - name: restore
          image: redis:alpine3.11
          command: ["/bin/sh", "-c"]
          args: ["cp /backup/dump.rdb /data/dump.rdb &&
            redis-cli -h {{ .Values.redis.fullnameOverride }}-master debug restart || true"]
          volumeMounts:
            - name: redis-data
              mountPath: /data
            - name: backup
              mountPath: /backup
      restartPolicy: Never
      volumes:
        - name: redis-data
          persistentVolumeClaim:
            claimName: redis-data-{{ .Values.redis.fullnameOverride }}-master-0
        - name: backup
          persistentVolumeClaim:
            claimName: redis-data-{{ .Values.redis.fullnameOverride }}-master-0-backup-{{ .Release.Revision }}
{{- end }}
```

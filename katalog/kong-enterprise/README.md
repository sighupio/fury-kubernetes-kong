# Kong Enterprise

In this architecture, we have two components, the Data Plane and the Control Plane. All the images we are using for
Kong are the Enterprise Images.

The Kong Ingress controller is deployed in the Control Plane statefulset as a Sidecar.

The Kong Data Plane is deployed as a Deployment, all the Kong Data Plane reads the configurations from the DB.

![Kong Enterprise DB Architecture](../../docs/images/deployment-classic-distributed.png)



## Upgrades

When upgrading Kong to a new minor version, you need to run two jobs.
Delete the existing job using:

```bash
kubectl delete job kong-migrations
```

Then **patch** the migration with the `migrations up` command:

```yaml
---
apiVersion: batch/v1
kind: Job
metadata:
  name: kong-migrations
  namespace: kong
spec:
  template:
    spec:
      containers:
        - name: kong-migrations
          command: [ "/bin/sh", "-c", "kong migrations up" ]
      restartPolicy: OnFailure
```

Wait for the job to finish and delete it:

```bash
kubectl delete job kong-migrations
```

Now **patch** the migration with the `migrations finish` command:

```yaml
---
apiVersion: batch/v1
kind: Job
metadata:
  name: kong-migrations
  namespace: kong
spec:
  template:
    spec:
      containers:
        - name: kong-migrations
          command: [ "/bin/sh", "-c", "kong migrations finish" ]
      restartPolicy: OnFailure
```

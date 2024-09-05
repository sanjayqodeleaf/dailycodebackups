**Configuration of StatefulSet**

#### tried to debug the statefulset / exploring more 

#### statefulsetsql.yaml

``` 
   apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mysql1
spec:
  serviceName: mysql
  replicas: 1
  selector:
    matchLabels:
      app: mysql1
  template:
    metadata:
      labels:
        app: mysql1
    spec:
      terminationGracePeriodSeconds: 10
      containers:
      - name: mysql1
        image: mysql:5.7
        ports:
        - containerPort: 3306
        volumeMounts:
        - name: mysql-store
          mountPath: /var/lib/mysql
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-password
              key: MYSQL_ROOT_PASSWORD
  volumeClaimTemplates:
  - metadata:
      name: mysql-store
    spec:
      accessModes: ["ReadWriteOnce"]
      storageClassName: "pd-standard"
      resources:
        requests:
          storage: 5Gi

```

#### sqlsecret.yaml

```
   apiVersion: v1
kind: Secret
metadata:
  name: mysql-password
type: opaque
stringData:
  MYSQL_ROOT_PASSWORD: password

```

#### storageclass.yaml

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: standard
provisioner: kubernetes.io/gce-pd
reclaimPolicy: Retain
parameters:
  type: pd-standard
  fstype: ext4

```

#### pvc-mysql.yaml

```
   apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-store1
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 6Gi
  storageClassName: storageclass

```
#### headlesssvc.yaml

```
apiVersion: v1
kind: Service
metadata:
  name: mysql1
  labels:
    app: mysql1
spec:
  ports:
  - port: 3306
  clusterIP: None
  selector:
    app: mysql1

```

#### The error i am getting while depoloyig the sts

```
  0/2 nodes are available: pod has unbound immediate PersistentVolumeClaims. preemption: 0/2 nodes are available:
  2 Preemption is not helpful for scheduling.
```

#### Went through multiple websites to debug the issue links below:

```
   https://stackoverflow.com/questions/66351213/0-2-nodes-are-available-2-pod-has-unbound-immediate-persistentvolumeclaims

```
```
   https://github.com/hashicorp/consul-helm/issues/237
```
```
   https://discuss.hashicorp.com/t/0-3-nodes-are-available-pod-has-unbound-immediate-persistentvolumeclaims/51642
```
```
   https://www.datree.io/resources/kubernetes-troubleshooting-fixing-persistentvolumeclaims-error
```
```
   https://discuss.kubernetes.io/t/pod-has-unbound-immediate-persistentvolumeclaims-
   preemption-0-1-nodes-are-available-1-no-preemption-victims-found-for-incoming-pod/22198
```

#### Important points captured from the whole process
   - Check Node Availability: Ensure that you have enough available nodes in your cluster. If not, consider adding more nodes.
   - Resource Limits: Verify that nodes have sufficient resources (CPU, memory) to meet the PVC requirements. Adjust resource limits if needed.
   - Storage Classes: Confirm that the StorageClasses in your PVCs are available and compatible with your cluster’s storage backend.
   - Pod Priority and Preemption: If using Pod priority and preemption, ensure correct priority levels and preemption policies.
   - Node Affinity and Anti-affinity: Check for node affinity or anti-affinity rules that may prevent pod scheduling.
   - Pod Disruption Budgets: If PodDisruptionBudgets are set, ensure they allow for the eviction of pods necessary for preemption.
   - Check Logs: Examine scheduler, controller-manager, and kubelet logs for error messages. Review events associated with PVCs and Pods for more details.

#### went through the module and completed 80% of the task given today

#### got an overview of operators 

```
   https://kubernetes.io/docs/concepts/extend-kubernetes/operator/

```

#### The project  planning is going on 60% done 


     




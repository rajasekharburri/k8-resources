# Kubernetes Storage & Workloads -- Notes

## 💾 Storage in Kubernetes
🧠 Key Concept
- Pod = Ephemeral
- Node = Also Ephemeral (can be replaced)

👉 By default:

-   When a Pod is created, it gets storage from the node
-   When the Pod is deleted, the data is also deleted
##  Types of Storage

## 1. Ephemeral Storage (Temporary)
-   Data lives only as long as the Pod lives

### ✅ emptyDir
- Default temporary storage
- Created when Pod starts, deleted when Pod dies
- Shared between containers in same Pod

##### Use case:
- Sidecar pattern (log sharing)

## hostPath
- ephemeral storage used by pod to access the underlying host storage, this is not secure but in few situations like shipping the logs to external storage we are using hostpath with readonly access.

⚠️ Not secure (access to host machine)

### Use cases:

- Running Log collection
- Node-level monitoring

🔁Sidecar Pattern
- Main container → writes logs
- Sidecar container → reads logs & sends to tools like ELK

## Workloads

### 1.ReplicaSet

-   Maintains pod count

### 2.Deployment

-   Rolling updates & rollback

### 3.DaemonSet
- it will make sure one replica of pod runs in each and every node. we can ship the logs using daemonset by access host logs through hostPath. hostPath persist the data until the pod runs on the node.


### 4.StatefulSet

-   Stable identity
-   Persistent storage

## permanent volumes
1. networking
2. storage
3. programming
4. os


## Persistent Storage(permanent)

### HD (EBS) -Elastic Block Storage

- should be as near as possible to computer
- data trasfer is very fast
- can connect to only computer at a time
- databases and OS should be in EBS


### Drive(NFS) EFS(Elastic file storage)
- should be anywhere in the network
- data transfer is slow compared to EBS
- can be used in multiple systems at a time
- databases and os can't be used in EFS
- you can keep files in EFS

## Provisioning

-   Static: manually creating disks
-   Dynamic: pods can create disks dynamically whenever required


## Kubernetes Objects

### PV

-   Actual storage

### PVC

-   Storage request

### StorageClass

-   Defines storage type

## Analogy

Pod → PVC → PV → Disk Son → Mother → Father → Wallet

Dynamic: Pod → PVC → StorageClass → Disk Son → Mother → PhonePe

## Admin Tasks

-   Create storage
-   Attach/detach
-   Resize
-   Backup/restore
-   Replication

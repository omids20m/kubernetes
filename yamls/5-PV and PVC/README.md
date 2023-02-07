# Persistent Volumes and Persistent Volume Claims

1. Create a pv
2. Create a pvc (request a pv)
3. Create a Pod that uses pvc to get the pv

## Static provisioning

Send a request to Cluster administrator to create a pv and we use it

## Dynamic provisioning

Cluster administrator creates a Storage Class
When u request a pv using pvc the storage class creates a pv automatically

## Types of Persistent Volumes

https://kubernetes.io/docs/concepts/storage/persistent-volumes/#types-of-persistent-volumes

PersistentVolume types are implemented as plugins. Kubernetes currently supports the following plugins:

* [`cephfs`](https://kubernetes.io/docs/concepts/storage/volumes/#cephfs) - CephFS volume
* [`csi`](https://kubernetes.io/docs/concepts/storage/volumes/#csi) - Container Storage Interface (CSI)
* [`fc`](https://kubernetes.io/docs/concepts/storage/volumes/#fc) - Fibre Channel (FC) storage
* [`hostPath`](https://kubernetes.io/docs/concepts/storage/volumes/#hostpath) - HostPath volume (for single node testing only; WILL NOT WORK in a multi-node cluster; consider using `local` volume instead)
* [`iscsi`](https://kubernetes.io/docs/concepts/storage/volumes/#iscsi) - iSCSI (SCSI over IP) storage
* [`local`](https://kubernetes.io/docs/concepts/storage/volumes/#local) - local storage devices mounted on nodes.
* [`nfs`](https://kubernetes.io/docs/concepts/storage/volumes/#nfs) - Network File System (NFS) storage
* [`rbd`](https://kubernetes.io/docs/concepts/storage/volumes/#rbd) - Rados Block Device (RBD) volume

AWS EBS: Amazon Elastic Block Storage
GCE PD: Google Compute Disk
Microsoft Azure Disk

On Prem:
longhorn
cephfs

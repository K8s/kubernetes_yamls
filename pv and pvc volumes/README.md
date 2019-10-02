A PV will be provisioned by administrator to store the data Persistence,
which means data will be available even after POD deletion.
We can also provision the PV dynamically using Storage Classes.

A PersistentVolumeClaim (PVC) is a request for storage by a user.
It is similar to a pod. Pods consume node resources and PVCs consume
PV resources. Pods can request specific levels of resources (CPU and Memory).
Claims can request specific size and access modes (e.g., can be mounted once
read/write or many times read-only).

As updated earlier, PVs can be provisioned in two ways:

Static and Dynamic

Static PV are provisioned by cluster administrator, which can be managed by
kubernetes apiserver

Dynamic PV are created when none of the PV exists created by administrator,
it will provision the dynamic PV in the background.

We have three types of reclaim policies:

Retain, Delete and Recycle

The Retain reclaim policy allows for manual reclamation of the resource.
When the PersistentVolumeClaim is deleted, the PersistentVolume still exists
and the volume is considered “released”. But it is not yet available for
another claim because the previous claimant’s data remains on the volume.
An administrator can manually reclaim the volume with the following steps.

Delete the PersistentVolume. The associated storage asset in external
infrastructure (such as an AWS EBS, GCE PD, Azure Disk, or Cinder volume)
still exists after the PV is deleted. Manually clean up the data on the
associated storage asset accordingly. Manually delete the associated storage
asset, or if you want to reuse the same storage asset, create a new
PersistentVolume with the storage asset definition.

For Delete policy, For volume plugins that support the Delete reclaim policy,
deletion removes both the PersistentVolume object from Kubernetes, as well as
the associated storage asset in the external infrastructure, such as an AWS
EBS, GCE PD, Azure Disk, or Cinder volume.

For recycle, If supported by the underlying volume plugin, the Recycle reclaim
policy
performs a basic scrub (rm -rf /thevolume/*) on the volume and makes it
available again for a new claim.


Ceph Storage Provision:
kubectl get pvc
NAME        STATUS  VOLUME                                   CAPACITY ACCESSMODES  AGE
ceph-claim  Bound   pvc-f548d663-3cac-11e7-9937-0024e8650c7a 2Gi      RWO          1m
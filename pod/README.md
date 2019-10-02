CPU
CPU resources are measured in millicore. If a node has 2 cores, the
node’s CPU capacity would be represented as 2000m. The unit suffix
m stands for “thousandth of a core.” 1000m or 1000 millicore is equal
to 1 core. 4000m would represent 4 cores. 250 millicore per pod means
4 pods with a similar value of 250m can run on a single core. On a 4
core node, 16 pods each having 250m can run on that node.

Memory is measured in bytes. However, you can express memory with
various suffixes (E,P,T,G,M,K and Ei, Pi, Ti, Gi, Mi, Ki) to express
mebibytes (Mi) to petabytes (Pi). Most simply use Mi.

Static POD kubelet service entries:
root@workernodeone:/etc/systemd/system/kubelet.service.d# cat 10-kubeadm.conf
# Note: This dropin only works with kubeadm and kubelet v1.11+
[Service]
Environment="KUBELET_KUBECONFIG_ARGS=--bootstrap-kubeconfig=/etc/kubernetes/bootstrap-kubelet.conf --kubeconfig=/etc/kubernetes/kubelet.conf"
Environment="KUBELET_CONFIG_ARGS=--config=/var/lib/kubelet/config.yaml"
# This is a file that "kubeadm init" and "kubeadm join" generates at runtime, populating the KUBELET_KUBEADM_ARGS variable dynamically
EnvironmentFile=-/var/lib/kubelet/kubeadm-flags.env
# This is a file that the user can use for overrides of the kubelet args as a last resort. Preferably, the user should use
# the .NodeRegistration.KubeletExtraArgs object in the configuration files instead. KUBELET_EXTRA_ARGS should be sourced from this file.
EnvironmentFile=-/etc/default/kubelet
ExecStart=
ExecStart=/usr/bin/kubelet $KUBELET_KUBECONFIG_ARGS $KUBELET_CONFIG_ARGS $KUBELET_KUBEADM_ARGS $KUBELET_EXTRA_ARGS --pod-manifest-path=/etc/kubelet.d/
root@workernodeone:/etc/systemd/system/kubelet.service.d#

Now reload the systemd daemon with "systemctl daemon-reload" and then restart kubelet service


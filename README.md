# Talos Install

```
mise install
mise run fetch-talos-secrets
```

```
talosctl gen config pid1labs https://192.168.168.15:6443  --install-image=d4ed705ed680e200144df495701db951b85ec0361e2868456643ee721a497344 --install-disk /dev/nvme0n1 --config-patch @cni.yaml
```


```
talosctl patch mc --nodes 192.168.168.15 --talosconfig=./talosconfig -e 192.168.168.15 --patch @nvidia-patch.yaml
```


## For a single node
```

  helm install cilium cilium/cilium \
      --version 1.19.2 \
      --namespace kube-system \
      --set operator.replicas=1 \
      --set ipam.mode=kubernetes \
      --set kubeProxyReplacement=true \
      --set k8sServiceHost=<YOUR_NODE_IP> \
      --set k8sServicePort=6443 \
      --set tunnel=disabled \
      --set routingMode=native \
      --set autoDirectNodeRoutes=true \
      --set ipv4NativeRoutingCIDR=10.244.0.0/24 \
      --set hostServices.enabled=true \
      --set nodeport.enabled=true \
      --set hubble.enabled=true \
      --set hubble.relay.enabled=true \
      --set hubble.ui.enabled=true \
      --set socketLB.hostNamespaceOnly=true \
      --set bpf.masquerade=true \
      --set "devices={ens18,enp3s0np0}" \
      --set installNoConntrackIptablesRules=true \
      --set endpointRoutes.enabled=true \
      --set "securityContext.capabilities.ciliumAgent={CHOWN,KILL,NET_ADMIN,NET_RAW,IPC_LOCK,SYS_ADMIN,SYS_RESOURCE,DAC
  _OVERRIDE,FOWNER,SETGID,SETUID}" \
      --set "securityContext.capabilities.cleanCiliumState={NET_ADMIN,SYS_ADMIN,SYS_RESOURCE}" \
      --set cgroup.autoMount.enabled=false \
      --set cgroup.hostRoot=/sys/fs/cgroup
```

```
talosctl patch mc --nodes 192.168.168.15 --talosconfig=./talosconfig -e 192.168.168.15 --patch @flux-extra-manifests.yaml
```

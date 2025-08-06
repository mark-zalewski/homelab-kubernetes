# Talos Configuration Generation and Application  
```talosctl gen config zalewski-dev-cluster https://10.0.30.131:6443 \
  --with-secrets secrets.yaml \
  --config-patch @patches/allow-controlplane-workloads.yaml \
  --config-patch @patches/cni.yaml \
  --config-patch @patches/dhcp.yaml \
  --config-patch @patches/install-disk.yaml \
  --config-patch @patches/interface-names.yaml \
  --config-patch-control-plane @patches/vip.yaml \
  --output rendered/
  ```


## Set the TALOSCONFIG environment variable to point to the generated configuration
### This is where talosctl will look for the configuration files
### Adjust the path as necessary based on your directory structure
```
export TALOSCONFIG=./rendered/talosconfig
```


# Apply the control plane configuration
  ### This assumes you have a control plane node at 10.0.30.131
```
talosctl apply -f rendered/controlplane.yaml -n 10.0.30.131 --insecure
```

# Apply the worker node configuration
  ### This assumes you have a worker node at 10.0.30.132
```
talosctl apply -f rendered/worker.yaml -n 10.0.30.132 --insecure
```

# Set the Talos endpoint to the control plane node
### $CONTROL_PLANE_IP is the IP address of your control plane node, e.g., 10.0.30.131
```
export TALOSCONFIG="_out/talosconfig"
talosctl config endpoint $CONTROL_PLANE_IP
talosctl config node $CONTROL_PLANE_IP
```

# Bootstrap the cluster
```
talosctl bootstrap
```
# Retrieve the kubeconfig file to interact with the Kubernetes cluster
```
talosctl kubeconfig .
``` 

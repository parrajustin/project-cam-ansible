# project-cam-ansible

First update inventory with passwords and ip address of workers.

run update with

```bash
ansible-playbook -i inventory.yaml update.yaml --ask-vault-pass
```

```bash
ansible-playbook -i inventory.yaml hostname.yaml --ask-vault-pass
```

Run install snap with

<!--
```bash
ansible-playbook -i inventory.yaml install_snap.yaml
``` -->

```bash
ansible-playbook -i inventory.yaml install_k8s.yaml --ask-vault-pass
```

Now create the cluster

```bash
ansible-playbook -i inventory.yaml create_cluster.yml --ask-vault-pass
```

Now install helm

```bash
ansible-playbook -i inventory.yaml install_helm.yml --ask-vault-pass
```

Now create the dashboard

```bash
microk8s enable dashboard
# Get token
microk8s kubectl describe secret -n kube-system microk8s-dashboard-token
# Port forward
kubectl port-forward -n kube-system service/kubernetes-dashboard 10443:443
```

Now enable istio

```bash
microk8s enable community
microk8s enable istio
```

lets you see all pods/services

```bash
watch microk8s.kubectl get all --all-namespaces
```

Enable istio sidcar injection

```bash
microk8s.kubectl label namespace default istio-injection=enabled
```

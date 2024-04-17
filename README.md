# k8s-argo-aoa

Argo AoA pattern to stand up apps on k8s.lan

## Local Argo Dashboard

- Start port forwarding

```bash
$ ssh -L 6443:k8s.lan:6443 k8s.lan
```

- Export the k8s config

```bash
$ export KUBECONFIG=~/.kube/k8s-config
```

- Start the local Argo Dashboard

```bash
argocd admin dashboard -n argocd
```

## Manual Configurations

- Updated the configuration to use second ssd for topolvm:

Once the vg has been created:

```bash
$ oc -n openshift-storage edit cm lvmd
```

- Create cert-manager issuers:

```yaml
apiVersion: cert-manager.io/v1
kind: ClusterIssuer
metadata:
  name: letsencrypt
spec:
  acme:
    email: <email address>
    server: https://acme-v02.api.letsencrypt.org/directory
    privateKeySecretRef:
      name: lets-encrypt-secret-prod
    solvers:
    - http01:
       ingress:
         serviceType: ClusterIP
```

- Create the velro AWS backup creds




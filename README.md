# kubeadm-certs

Only modify kubeadm`s expiry for certificate(ca,etcd,kube-apiserver,kube-*) to 200 years.


## Certificate

CA certificate


- https://github.com/kubernetes/kubernetes/blob/v1.21.0/staging/src/k8s.io/client-go/util/cert/cert.go#L38
- https://github.com/kubernetes/kubernetes/blob/v1.21.0/staging/src/k8s.io/client-go/util/cert/cert.go#L66

Component certificate

- https://github.com/kubernetes/kubernetes/blob/v1.21.0/cmd/kubeadm/app/constants/constants.go#L49
- https://github.com/kubernetes/kubernetes/blob/v1.21.0/cmd/kubeadm/app/util/pkiutil/pki_helpers.go#L659

## Usage

The release version of the project is the same as that of kubernetes, which can be downloaded from [releases](https://github.com/dyrnq/kubeadm-certs/releases)

```bash
[ -f /usr/bin/kubeadm ] && mv /usr/bin/kubeadm{,_src}
wget https://github.com/dyrnq/kubeadm-certs/releases/download/v1.24.0/kubeadm-linux-amd64 -O /usr/bin/kubeadm
chmod +x /usr/bin/kubeadm
```

for existing kubernetes cluster

```bash
kubeadm certs renew all -v5
kubeadm init phase upload-certs --upload-certs -v5
```

for upgrade first control plane

```bash
kubeadm upgrade plan

kubeadm upgrade apply --force --certificate-renewal=false v1.23.1
```

for upgrade other control plane and nodes

```bash
kubeadm upgrade node --certificate-renewal=false v1.23.1
```

## LICENSE

MIT


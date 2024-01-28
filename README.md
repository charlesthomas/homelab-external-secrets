# homelab-external-secrets

This is a mirco-services repo for deploying
[external-secrets](https://external-secrets.io/)
into [my homelab](https://github.com/charlesthomas/homelab).

manages secrets by syncing them from [vault-warden](https://githb.com/charlesthomas/homelab-vault-warden)

bitwarden doesn't provide a docker image, and i couldn't find a trustworthy enough looking one.

[external-secrets documentation](https://external-secrets.io/v0.9.9/examples/bitwarden/) provides everything you need in order to build an image yourself,

so i did that here: [charlesthomas/bitwarden-cli](https://github.com/charlesthomas/bitwarden-cli)

it publishes a public image as (at the time of this writing):

```bash
ghcr.io/charlesthomas/bitwarden-cli:2024.1.0
```

which is the image referenced in `deployments.yaml`

## update secret

```bash
kubectl -n external-secrets edit secret bitwarden-cli
```

```yaml
data:
    BW_HOST: <base64 host>
    BW_USERNAME: <base64 username>
    BW_PASSWORD: <base64 password>
```

# install manually

```bash
kubectl kustomize --enable-helm external-secrets/ | kubectl apply -f -
```

---
This repo is templated via
[homelab-template](https://github.com/charlesthomas/homelab-template)
and automatically updated via
[🤖 Templatron](https://github.com/charlesthomas/templatron).

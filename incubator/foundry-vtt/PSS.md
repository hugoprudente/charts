# Pod Security Standards (PSS) and cluster administrators

Clusters enforce workload security with [Pod Security Admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/) and the three [Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/) profiles: `privileged`, `baseline`, and `restricted`.

Admins set policy on the **namespace** (labels). The chart sets the **pod** side via `security.hardened`, `container.uid` / `container.gid`, and optional `podSecurityContext` / `securityContext`.

## What cluster admins typically do

### 1. Choose a PSS level for the Foundry namespace

| Level | Typical use |
| ----- | ----------- |
| **privileged** | No PSA restrictions (lab / exceptions only). |
| **baseline** | Common default; blocks many risky settings while allowing typical app pods. |
| **restricted** | Stricter; may require `security.hardened: true` and tuned volumes. |

Start with **baseline** unless your platform mandates **restricted**.

The profiles are defined in the Kubernetes docs: [overview](https://kubernetes.io/docs/concepts/security/pod-security-standards/#profile-details), [baseline](https://kubernetes.io/docs/concepts/security/pod-security-standards/#baseline), and [restricted](https://kubernetes.io/docs/concepts/security/pod-security-standards/#restricted).

### 2. Label the namespace (Pod Security Admission)

Create or label the namespace where Foundry runs:

```bash
export NAMESPACE=foundry

kubectl create namespace "${NAMESPACE}" --dry-run=client -o yaml | kubectl apply -f -

kubectl label namespace "${NAMESPACE}" \
  pod-security.kubernetes.io/enforce=baseline \
  pod-security.kubernetes.io/enforce-version=latest \
  pod-security.kubernetes.io/audit=baseline \
  pod-security.kubernetes.io/audit-version=latest \
  pod-security.kubernetes.io/warn=baseline \
  pod-security.kubernetes.io/warn-version=latest \
  --overwrite
```

Label keys and the `enforce` / `audit` / `warn` modes match [Kubernetes: enforce standards with namespace labels](https://kubernetes.io/docs/tasks/configure-pod-container/enforce-standards-namespace-labels/).

For **restricted** enforcement (stricter):

```bash
kubectl label namespace "${NAMESPACE}" \
  pod-security.kubernetes.io/enforce=restricted \
  pod-security.kubernetes.io/enforce-version=latest \
  pod-security.kubernetes.io/audit=restricted \
  pod-security.kubernetes.io/audit-version=latest \
  pod-security.kubernetes.io/warn=restricted \
  pod-security.kubernetes.io/warn-version=latest \
  --overwrite
```

Same labelling guide; profile name `restricted` is from the [restricted profile](https://kubernetes.io/docs/concepts/security/pod-security-standards/#restricted) docs.

Check labels:

```bash
kubectl get namespace "${NAMESPACE}" --show-labels
```

### 3. Namespace manifest (GitOps / platform repo)

Example Namespace for a platform or umbrella repo (this chart does not create namespaces):

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: foundry
  labels:
    pod-security.kubernetes.io/enforce: baseline
    pod-security.kubernetes.io/enforce-version: latest
    pod-security.kubernetes.io/audit: baseline
    pod-security.kubernetes.io/audit-version: latest
    pod-security.kubernetes.io/warn: baseline
    pod-security.kubernetes.io/warn-version: latest
```

Same labels as in step 2 — see [enforce standards with namespace labels](https://kubernetes.io/docs/tasks/configure-pod-container/enforce-standards-namespace-labels/).

### 4. Cluster-wide PSA configuration (optional)

Some clusters set a default level in the API server so unlabeled namespaces inherit a policy. That is distribution-specific (EKS, GKE, AKS, Rancher, etc.); see [how Pod Security Admission works](https://kubernetes.io/docs/concepts/security/pod-security-admission/) and your vendor’s install guide.

On **OpenShift**, use [Security Context Constraints](https://docs.openshift.com/container-platform/latest/security/containers_and_linux/security-context-constraints-understanding.html) instead of PSA namespace labels.

### 5. What application values to use with PSA

After the namespace is labeled, install with settings that match the policy. For **baseline** or **restricted**, hardened defaults help:

```yaml
security:
  hardened: true

container:
  uid: 1000
  gid: 1000
```

`security.hardened` is defined in [`values.yaml`](values.yaml) and implemented in [`templates/deployment.yaml`](templates/deployment.yaml) (non-root, `RuntimeDefault` seccomp, read-only root where applicable). Defaults for uid/gid are in the same values file. The layout follows Felddy’s [kubernetes manifests](https://github.com/felddy/foundryvtt-docker/tree/main/kubernetes).

Example install:

```bash
helm upgrade --install my-foundry ./incubator/foundry-vtt \
  --namespace foundry \
  --create-namespace \
  --set security.hardened=true
```

Install flow matches [`README.md`](README.md). `--create-namespace` does not add PSA labels — do step 2 first or ship a Namespace manifest from step 3.

## Troubleshooting admission failures

If pods stay `Pending` or events mention `violates PodSecurity`:

1. Confirm namespace labels: `kubectl get ns <name> --show-labels`
2. Read events: `kubectl describe pod -n <namespace> <pod>`
3. Try **baseline** before **restricted**, or set `security.hardened: true`
4. Inspect what the chart renders: `helm template my-release . --set security.hardened=true | rg -A20 securityContext`

For what the admission controller is checking, see [Pod Security Admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/).

## Further reading

- [Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/)
- [Pod Security Admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/)
- [Enforce standards with namespace labels](https://kubernetes.io/docs/tasks/configure-pod-container/enforce-standards-namespace-labels/)
- Felddy: [foundryvtt-docker/kubernetes](https://github.com/felddy/foundryvtt-docker/tree/main/kubernetes)
- Chart: [`values.yaml`](values.yaml), [`templates/deployment.yaml`](templates/deployment.yaml), [`README.md`](README.md)

Discussion: [charts#28](https://github.com/hugoprudente/charts/issues/28).

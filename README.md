# Production GitOps Platform on EKS



## 🎥 Project Demo

See the **Production GitOps Platform on Amazon EKS** in action.

The demo covers:

- Terraform-based AWS infrastructure
- Amazon EKS cluster
- ArgoCD GitOps workflow
- Kubernetes application deployment
- Git-based continuous delivery

<video src="./assets/gitops-platform-demo.mp4" controls width="100%"></video>

> **GitOps Flow:**  
> GitHub → GitHub Actions → Terraform → Amazon EKS → ArgoCD → Kubernetes

### ▶️ Demo Video

[Watch / Download the GitOps Platform Demo](./assets/gitops-platform-demo.mp4)

Minimal reference implementation of a production-style GitOps platform on Amazon EKS.

- **Infra**: Terraform provisions the EKS cluster, VPC, and node groups.
- **GitOps**: ArgoCD watches this repo and syncs Kubernetes manifests to the cluster.
- **Apps**: Kustomize-based manifests with base + prod overlay.
- **CI**: GitHub Actions lints/validates Terraform and manifests on PRs.

## Structure
```
terraform/        # EKS cluster + VPC IaC
argocd/apps/       # ArgoCD Application CRDs
manifests/base/    # Base k8s manifests
manifests/overlays/prod/  # Prod-specific kustomize overlay
.github/workflows/ # CI pipelines
```

## Flow
1. Terraform provisions EKS.
2. ArgoCD is installed on the cluster, pointed at `argocd/apps`.
3. ArgoCD syncs `manifests/overlays/prod` into the cluster automatically on every git push.

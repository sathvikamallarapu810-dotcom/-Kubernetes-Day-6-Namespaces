🐙 Kubernetes-Day-6-Namespaces

📌 Overview

Today I learned how Kubernetes Namespaces organize and isolate groups of resources within a single Kubernetes cluster.

Namespaces are useful for separating environments such as:

development
testing
production

They provide a scope for names and resources within a cluster.

🧠 1. Understanding Namespaces

A Kubernetes cluster can contain multiple namespaces:

Kubernetes Cluster
│
├── default
│
├── development
│
├── testing
│
└── production

Each namespace can contain resources such as:

Pods
Deployments
Services
ConfigMaps
Secrets
🛠️ 2. Create a Namespace

I created a namespace called development:

kubectl create namespace development

Verified it with:

kubectl get namespaces

Result:

development   Active
📦 3. Create a Pod Inside the Namespace

I created an Nginx Pod specifically inside development:

kubectl run nginx-dev --image=nginx -n development

Then verified:

kubectl get pods -n development

Result:

NAME        READY   STATUS
nginx-dev   1/1     Running
🔍 4. Understanding -n

The -n option specifies the namespace.

Default namespace
kubectl get pods
Development namespace
kubectl get pods -n development

This helped me understand why my nginx-dev Pod didn't appear when I simply ran:

kubectl get pods

The command was looking at the default namespace.

🗂️ 5. Namespace-Specific ConfigMap

I also created a ConfigMap inside development:

kubectl create configmap dev-config \
  --from-literal=APP_ENV=development \
  -n development

Verified using:

kubectl get configmap -n development

Result:

NAME               DATA
dev-config         1
kube-root-ca.crt   1

This demonstrated that namespace-scoped resources can be organized separately.

🧠 Simple Architecture
                    Kubernetes Cluster
                           │
             ┌─────────────┴─────────────┐
             ▼                           ▼
         default                    development
             │                           │
     ┌───────┼───────┐             ┌─────┴─────┐
     ▼       ▼       ▼             ▼           ▼
   Pods   Services  ConfigMap     nginx-dev   dev-config
⭐ Key Takeaways
Namespace organizes resources inside a cluster.
-n specifies the namespace.
Different namespaces can contain resources with the same name.
Namespaces are useful for environments such as development, testing, and production.
Not every Kubernetes resource is namespace-scoped; for example, Nodes are cluster-wide resources.
📈 Kubernetes Progress
Day 1 — Kubernetes Basics & Pods       ✅
Day 2 — Deployments & ReplicaSets      ✅
Day 3 — Services & Networking          ✅
Day 4 — Labels & Selectors             ✅
Day 5 — ConfigMaps & Secrets           ✅
Day 6 — Namespaces                     ✅
🚀 Learning approach

Learn → Practice → Troubleshoot → Verify → Document

Continuing my journey into Kubernetes, Cloud & DevOps. 🚀

#Kubernetes #DevOps #CloudComputing #Docker #AWS #Minikube #KubernetesJourney #CloudEngineer #LearningInPublic

<img width="959" height="562" alt="Screenshot 2026-08-18 214348" src="https://github.com/user-attachments/assets/c5fd73b1-0a0b-42f4-8360-7d7eb9e3e7fb" />

<img width="959" height="552" alt="Screenshot 2026-08-18 214358" src="https://github.com/user-attachments/assets/c7a431bd-22cd-4e3f-92d4-07f5f5a2398a" />



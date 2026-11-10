# helloworld (dev)

Application Hello World Golden Path déployée sur EKS Spoke avec S3 et RDS PostgreSQL via Crossplane

Dépôt généré automatiquement en Self-Service depuis le Software Template **Backstage Golden Path**.

## Architecture GitOps (ArgoCD + Crossplane)

Ce dépôt est synchronisé par l'ArgoCD du cluster Hub (`global`) via deux `Applications` complémentaires :

1. **`infra/` (Crossplane sur le cluster Hub `global` avec `ProviderConfig: aws-dev`)** :
   - **Bucket S3** : `helloworld-dev-assets-948025766648` (`infra/s3-bucket.yaml`) créé dans le compte AWS `dev` (`948025766648`)
   - **Instance RDS PostgreSQL 16** : `helloworld-dev-db` (`db.t4g.micro`, `infra/rds-postgres.yaml`) créée dans le DB Subnet Group `idp-platform-dev-db-subnet-group` du compte AWS `dev`
2. **`k8s/` (Workloads Kubernetes sur le cluster EKS Spoke `idp-platform-dev-eks`)** :
   - `Deployment`, `ConfigMap`, `Service` et `Ingress` Traefik exposés en HTTPS sur :
     **https://helloworld.dev.dsery.me**

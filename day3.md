How Argo CD works – end-to-end flow

Consider a developer making changes to an application.

1. Developer pushes code to Git

Developer updates Kubernetes deployment YAML or Helm values and creates a pull request.

2. Pull request is merged

Updated manifests are stored in the Git repository.

3. Argo CD detects changes

Argo CD periodically checks Git or receives a webhook notification.

4. Repo Server fetches manifests

It retrieves the latest repository revision and renders Helm, Kustomize or YAML configurations.

5. Application Controller compares states

It compares the desired configuration with the actual Kubernetes resources.

6. Argo CD performs synchronization

If automated sync is enabled, it applies the required changes. Otherwise, an authorized user can trigger manual sync.

7. Kubernetes deploys the application

Kubernetes creates or updates the required resources.

8. Argo CD monitors application health

The application status is updated to reflect synchronization and health.


===========================================================================================================================

Argo CD Application states

Two important concepts to understand:

Status                      Meaning

Synced                      Live configuration matches Git

OutOfSync                   Live configuration differs from Git

Healthy                     Application resources are healthy

Progressing                 Resources are still progressing

Degraded                    One or more resources are unhealthy

Missing                     Expected resources are absent

Note that Sync status and Health status are different. An application can be Synced but Degraded.


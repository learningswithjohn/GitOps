1. API Server (argocd-server)

It is the component through which users and external tools interact with Argo CD (through UI/CLI)

Responsibilities:

Accepts requests from users through the Argo CD UI or CLI.

Authenticates users and checks their permissions (SSO auth, RBAC permissions)

Provides information about applications and their deployment status.

Accepts requests to deploy, sync, refresh or delete applications.

Manages application operations such as sync and rollback.

Receives Git webhook notifications.

Example: When you click the Sync button in the Argo CD UI, the API Server handles the request and initiates the operation.

===========================================================================================================================

2. Repository Server (argocd-repo-server)

The Repo Server communicates with Git repositories and generates Kubernetes manifests.

Responsibilities:

Clones or fetches Git repositories.

Reads Kubernetes YAML files.

Renders Helm charts.

Processes Kustomize configurations.

Converts deployment configurations into Kubernetes manifests.

Provides the generated manifests to the Application Controller.

In simple words: It reads the deployment instructions from Git and prepares them in a format that Kubernetes can understand.

===========================================================================================================================

3. Application Controller (argocd-application-controller)

This component is responsible for continuously checking whether the application running in Kubernetes matches the configuration stored in Git.

It continuously monitors applications and compares:

Desired state: Configuration stored in Git.

Live state: Resources currently running in Kubernetes.


Responsibilities:

Monitors Kubernetes resources.

Detects configuration drift.

Identifies OutOfSync applications.

Performs automatic or manual synchronization.

Executes PreSync, Sync and PostSync hooks.

Monitors application health.

===========================================================================================================================

4. Dex Server

Dex provides authentication integration with external identity providers.

Examples:

Google

GitHub

LDAP

Microsoft Entra ID

Other OIDC providers

Dex is optional if another supported authentication configuration is used.

===========================================================================================================================

5. Redis

Redis provides caching functionality.

Responsibilities:

Caches application state.

Reduces unnecessary API requests.

Improves UI responsiveness.

Helps with internal state and performance management.

===========================================================================================================================

6. ApplicationSet Controller

Automatically creates and manages multiple Argo CD Applications.

Example:

You have 10 Kubernetes clusters and want to deploy the same application into all 10 clusters.

ApplicationSet can generate the Application resources automatically.

===========================================================================================================================

7. Notifications Controller

Sends notifications about application events.

Examples:

Application deployed successfully.

Application sync failed.

Application became OutOfSync.

Application health degraded.

Notifications can be integrated with Slack, email and other supported services.

===========================================================================================================================

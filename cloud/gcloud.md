# gcloud Cheat-Sheet

## Setup & Authentication

| Command                                                        | Description                                         |
| -------------------------------------------------------------- | --------------------------------------------------- |
| `gcloud init`                                                  | Initialize gcloud (login, project, default region)  |
| `gcloud version`                                               | Show installed gcloud and component versions        |
| `gcloud auth login`                                            | Authenticate with a Google account                  |
| `gcloud auth list`                                             | List authenticated accounts                         |
| `gcloud auth revoke <account>`                                 | Revoke credentials of an account                    |
| `gcloud auth application-default login`                        | Set Application Default Credentials (ADC) for code  |
| `gcloud auth activate-service-account --key-file=<key.json>`   | Authenticate as a service account                   |
| `gcloud auth print-access-token`                               | Print an OAuth 2.0 access token                     |
| `gcloud auth configure-docker <region>-docker.pkg.dev`         | Configure Docker to push/pull Artifact Registry     |

### Components

| Command                                | Description                     |
| -------------------------------------- | ------------------------------- |
| `gcloud components list`               | List available components       |
| `gcloud components install <id>`       | Install a component (e.g. kubectl) |
| `gcloud components update`             | Update all installed components |
| `gcloud components remove <id>`        | Remove a component              |

## Configuration

| Command                                          | Description                              |
| ------------------------------------------------ | ---------------------------------------- |
| `gcloud config list`                             | Show the active configuration            |
| `gcloud config set project <project-id>`         | Set the default project                  |
| `gcloud config set compute/region <region>`      | Set the default region                   |
| `gcloud config set compute/zone <zone>`          | Set the default zone                     |
| `gcloud config get-value project`                | Print the current project ID             |
| `gcloud config unset <property>`                 | Unset a property                         |
| `gcloud info`                                    | Show environment and config details      |

### Named Configurations

| Command                                          | Description                              |
| ------------------------------------------------ | ---------------------------------------- |
| `gcloud config configurations list`              | List all configurations                  |
| `gcloud config configurations create <name>`     | Create a new configuration               |
| `gcloud config configurations activate <name>`   | Switch to a configuration                |
| `gcloud config configurations delete <name>`     | Delete a configuration                   |

## Projects & APIs

| Command                                   | Description                          |
| ----------------------------------------- | ------------------------------------ |
| `gcloud projects list`                    | List all accessible projects         |
| `gcloud projects create <project-id>`     | Create a project                     |
| `gcloud projects describe <project-id>`   | Show project details                 |
| `gcloud projects delete <project-id>`     | Delete a project                     |
| `gcloud services list --enabled`          | List enabled APIs                    |
| `gcloud services list --available`        | List APIs available to enable        |
| `gcloud services enable <api>`            | Enable an API (e.g. `run.googleapis.com`) |
| `gcloud services disable <api>`           | Disable an API                       |

## IAM

| Command                                                                                              | Description                         |
| ---------------------------------------------------------------------------------------------------- | ----------------------------------- |
| `gcloud projects get-iam-policy <project-id>`                                                        | Show the project IAM policy         |
| `gcloud projects add-iam-policy-binding <project-id> --member=<member> --role=<role>`                | Grant a role to a member            |
| `gcloud projects remove-iam-policy-binding <project-id> --member=<member> --role=<role>`             | Revoke a role from a member         |
| `gcloud iam roles list`                                                                              | List predefined roles               |
| `gcloud iam roles describe <role>`                                                                   | Show permissions in a role          |
| `gcloud iam roles create <role-id> --project=<project-id> --file=<role.yaml>`                        | Create a custom role                |

> Member format examples: `user:name@example.com`, `serviceAccount:sa@<project-id>.iam.gserviceaccount.com`, `group:team@example.com`

### Service Accounts

| Command                                                                        | Description                              |
| ------------------------------------------------------------------------------ | ---------------------------------------- |
| `gcloud iam service-accounts list`                                             | List service accounts                    |
| `gcloud iam service-accounts create <name> --display-name=<text>`              | Create a service account                 |
| `gcloud iam service-accounts describe <sa-email>`                              | Show service account details             |
| `gcloud iam service-accounts delete <sa-email>`                                | Delete a service account                 |
| `gcloud iam service-accounts keys create <key.json> --iam-account=<sa-email>`  | Create a key file (prefer keyless where possible) |
| `gcloud iam service-accounts keys list --iam-account=<sa-email>`               | List keys of a service account           |
| `gcloud iam service-accounts keys delete <key-id> --iam-account=<sa-email>`    | Delete a key                             |

## Compute Engine

### Instances

| Command                                                                                  | Description                         |
| ---------------------------------------------------------------------------------------- | ----------------------------------- |
| `gcloud compute instances list`                                                          | List VM instances                   |
| `gcloud compute instances describe <vm>`                                                 | Show VM details                     |
| `gcloud compute instances create <vm> --machine-type=e2-medium --image-family=debian-12 --image-project=debian-cloud` | Create a VM |
| `gcloud compute instances start <vm>`                                                    | Start a VM                          |
| `gcloud compute instances stop <vm>`                                                     | Stop a VM                           |
| `gcloud compute instances suspend <vm>`                                                  | Suspend a VM                        |
| `gcloud compute instances resume <vm>`                                                   | Resume a suspended VM               |
| `gcloud compute instances reset <vm>`                                                    | Hard reset a VM                     |
| `gcloud compute instances delete <vm>`                                                   | Delete a VM                         |
| `gcloud compute instances set-machine-type <vm> --machine-type=<type>`                   | Change machine type (VM must be stopped) |
| `gcloud compute instances add-tags <vm> --tags=<tag>`                                    | Add network tags                    |
| `gcloud compute ssh <vm>`                                                                | SSH into a VM                       |
| `gcloud compute ssh <vm> --tunnel-through-iap`                                           | SSH through Identity-Aware Proxy    |
| `gcloud compute scp <local-file> <vm>:<remote-path>`                                     | Copy a file to a VM                 |
| `gcloud compute scp <vm>:<remote-path> <local-path>`                                     | Copy a file from a VM               |
| `gcloud compute instances get-serial-port-output <vm>`                                   | Show serial console output          |

### Disks, Snapshots & Images

| Command                                                                   | Description                         |
| ------------------------------------------------------------------------- | ----------------------------------- |
| `gcloud compute disks list`                                               | List disks                          |
| `gcloud compute disks create <disk> --size=<GB> --type=pd-ssd`            | Create a disk                       |
| `gcloud compute disks resize <disk> --size=<GB>`                          | Increase disk size                  |
| `gcloud compute instances attach-disk <vm> --disk=<disk>`                 | Attach a disk to a VM               |
| `gcloud compute instances detach-disk <vm> --disk=<disk>`                 | Detach a disk from a VM             |
| `gcloud compute disks snapshot <disk> --snapshot-names=<snapshot>`        | Create a snapshot                   |
| `gcloud compute snapshots list`                                           | List snapshots                      |
| `gcloud compute snapshots delete <snapshot>`                              | Delete a snapshot                   |
| `gcloud compute images list`                                              | List available images               |
| `gcloud compute images create <image> --source-disk=<disk>`               | Create an image from a disk         |

### Networking

| Command                                                                                                    | Description                    |
| ---------------------------------------------------------------------------------------------------------- | ------------------------------ |
| `gcloud compute networks list`                                                                             | List VPC networks              |
| `gcloud compute networks create <network> --subnet-mode=custom`                                            | Create a VPC network           |
| `gcloud compute networks subnets list`                                                                     | List subnets                   |
| `gcloud compute networks subnets create <subnet> --network=<network> --range=<cidr> --region=<region>`     | Create a subnet                |
| `gcloud compute firewall-rules list`                                                                       | List firewall rules            |
| `gcloud compute firewall-rules create <rule> --allow=tcp:443 --source-ranges=<cidr>`                       | Create a firewall rule         |
| `gcloud compute firewall-rules delete <rule>`                                                              | Delete a firewall rule         |
| `gcloud compute addresses create <name> --region=<region>`                                                 | Reserve a static external IP   |
| `gcloud compute addresses list`                                                                            | List reserved IP addresses     |

### Discovery

| Command                                            | Description                  |
| -------------------------------------------------- | ---------------------------- |
| `gcloud compute regions list`                      | List regions                 |
| `gcloud compute zones list`                        | List zones                   |
| `gcloud compute machine-types list --zones=<zone>` | List machine types in a zone |

## Google Kubernetes Engine (GKE)

| Command                                                                          | Description                           |
| -------------------------------------------------------------------------------- | ------------------------------------- |
| `gcloud container clusters list`                                                 | List clusters                         |
| `gcloud container clusters create <cluster> --region=<region>`                   | Create a standard cluster             |
| `gcloud container clusters create-auto <cluster> --region=<region>`              | Create an Autopilot cluster           |
| `gcloud container clusters describe <cluster> --region=<region>`                 | Show cluster details                  |
| `gcloud container clusters get-credentials <cluster> --region=<region>`          | Configure kubectl for a cluster       |
| `gcloud container clusters resize <cluster> --num-nodes=<n>`                     | Resize a node pool                    |
| `gcloud container clusters upgrade <cluster>`                                    | Upgrade cluster nodes/control plane   |
| `gcloud container clusters delete <cluster>`                                     | Delete a cluster                      |
| `gcloud container node-pools list --cluster=<cluster>`                           | List node pools                       |
| `gcloud container node-pools create <pool> --cluster=<cluster>`                  | Create a node pool                    |

## Cloud Run

| Command                                                                                          | Description                             |
| ------------------------------------------------------------------------------------------------ | --------------------------------------- |
| `gcloud run deploy <service> --image=<image> --region=<region>`                                  | Deploy a container image                |
| `gcloud run deploy <service> --source=.`                                                         | Build and deploy from source            |
| `gcloud run services list`                                                                       | List services                           |
| `gcloud run services describe <service> --region=<region>`                                       | Show service details                    |
| `gcloud run services update <service> --set-env-vars=KEY=VALUE`                                  | Update environment variables            |
| `gcloud run services update-traffic <service> --to-latest`                                       | Send all traffic to the latest revision |
| `gcloud run revisions list --service=<service>`                                                  | List revisions                          |
| `gcloud run services add-iam-policy-binding <service> --member=allUsers --role=roles/run.invoker` | Make a service public                  |
| `gcloud run services delete <service> --region=<region>`                                         | Delete a service                        |
| `gcloud run jobs list`                                                                           | List Cloud Run jobs                     |

## Cloud Functions

| Command                                                                                     | Description                  |
| ------------------------------------------------------------------------------------------- | ---------------------------- |
| `gcloud functions deploy <name> --gen2 --runtime=<runtime> --trigger-http --region=<region>` | Deploy an HTTP function     |
| `gcloud functions list`                                                                     | List functions               |
| `gcloud functions describe <name> --region=<region>`                                        | Show function details        |
| `gcloud functions call <name> --region=<region>`                                            | Invoke a function            |
| `gcloud functions logs read <name> --region=<region>`                                       | Read function logs           |
| `gcloud functions delete <name> --region=<region>`                                          | Delete a function            |

## Cloud Storage

| Command                                                   | Description                                |
| --------------------------------------------------------- | ------------------------------------------ |
| `gcloud storage buckets list`                             | List buckets                               |
| `gcloud storage buckets create gs://<bucket> --location=<region>` | Create a bucket                    |
| `gcloud storage buckets delete gs://<bucket>`             | Delete an empty bucket                     |
| `gcloud storage ls gs://<bucket>`                         | List objects in a bucket                   |
| `gcloud storage cp <local-file> gs://<bucket>/`           | Upload a file                              |
| `gcloud storage cp gs://<bucket>/<object> <local-path>`   | Download an object                         |
| `gcloud storage cp -r <dir> gs://<bucket>/`               | Upload a directory recursively             |
| `gcloud storage mv gs://<bucket>/<src> gs://<bucket>/<dst>` | Move or rename an object                 |
| `gcloud storage rsync -r <dir> gs://<bucket>/<path>`      | Sync a local directory to a bucket         |
| `gcloud storage rm gs://<bucket>/<object>`                | Delete an object                           |
| `gcloud storage rm -r gs://<bucket>`                      | Delete a bucket and all its contents       |

## Secret Manager

| Command                                                           | Description                       |
| ----------------------------------------------------------------- | --------------------------------- |
| `gcloud secrets list`                                             | List secrets                      |
| `gcloud secrets create <secret> --replication-policy=automatic`   | Create a secret                   |
| `gcloud secrets versions add <secret> --data-file=<file>`         | Add a new secret version          |
| `gcloud secrets versions access latest --secret=<secret>`         | Read the latest secret value      |
| `gcloud secrets versions list <secret>`                           | List secret versions              |
| `gcloud secrets delete <secret>`                                  | Delete a secret                   |

## Cloud SQL

| Command                                                                              | Description                  |
| ------------------------------------------------------------------------------------ | ---------------------------- |
| `gcloud sql instances list`                                                          | List instances               |
| `gcloud sql instances create <instance> --database-version=POSTGRES_16 --region=<region>` | Create an instance      |
| `gcloud sql instances describe <instance>`                                           | Show instance details        |
| `gcloud sql instances restart <instance>`                                            | Restart an instance          |
| `gcloud sql connect <instance> --user=<user>`                                        | Connect with a SQL client    |
| `gcloud sql backups create --instance=<instance>`                                    | Create an on-demand backup   |
| `gcloud sql databases list --instance=<instance>`                                    | List databases               |
| `gcloud sql instances delete <instance>`                                             | Delete an instance           |

## Artifact Registry

| Command                                                                                          | Description                    |
| ------------------------------------------------------------------------------------------------ | ------------------------------ |
| `gcloud artifacts repositories list`                                                             | List repositories              |
| `gcloud artifacts repositories create <repo> --repository-format=docker --location=<region>`     | Create a Docker repository     |
| `gcloud artifacts docker images list <region>-docker.pkg.dev/<project-id>/<repo>`                | List images in a repository    |
| `gcloud artifacts repositories delete <repo> --location=<region>`                                | Delete a repository            |

## Logging

| Command                                                              | Description                         |
| -------------------------------------------------------------------- | ----------------------------------- |
| `gcloud logging read "<filter>" --limit=20`                          | Read log entries                    |
| `gcloud logging read "severity>=ERROR" --freshness=1h`               | Show errors from the last hour      |
| `gcloud logging logs list`                                           | List available logs                 |
| `gcloud logging sinks list`                                          | List log sinks                      |

## Output, Filters & Global Flags

| Command / Flag                                          | Description                                  |
| ------------------------------------------------------- | -------------------------------------------- |
| `--format=json`                                         | Output as JSON                               |
| `--format=yaml`                                         | Output as YAML                               |
| `--format="value(name)"`                                | Print only specific field values             |
| `--format="table(name,zone,status)"`                    | Custom table columns                         |
| `--filter="status=RUNNING"`                             | Filter results server/client side            |
| `--filter="name~^web-"`                                 | Filter with a regular expression             |
| `--sort-by=~creationTimestamp`                          | Sort results (`~` for descending)            |
| `--limit=<n>`                                           | Limit the number of results                  |
| `--project=<project-id>`                                | Override the default project for one command |
| `--impersonate-service-account=<sa-email>`              | Run a command as a service account           |
| `--quiet` / `-q`                                        | Disable prompts (use defaults)               |
| `--verbosity=debug`                                     | Show debug output                            |
| `gcloud <group> <command> --help`                       | Show help for any command                    |
| `gcloud help -- <search-term>`                          | Search the help text                         |

---
id: kubernetes
title: Kubernetes
---

# Deploying ToolJet on Kubernetes

:::info
You should setup a PostgreSQL database manually to be used by ToolJet.
:::

Follow the steps below to deploy ToolJet on a Kubernetes cluster.

1. **Setup a PostgreSQL database** <br/>
   ToolJet uses a postgres database as the persistent storage for storing data related to users and apps. We do not have plans to support other databases such as MySQL.
2. **Create a Kubernetes secret with name `server`.** <br/>
   For the setup, ToolJet requires:

   - **TOOLJET_DB**
   - **TOOLJET_DB_HOST**
   - **TOOLJET_DB_USER**
   - **TOOLJET_DB_PASS**
   - **PG_HOST**
   - **PG_DB**
   - **PG_USER**
   - **PG_PASS**
   - **SECRET_KEY_BASE**
   - **LOCKBOX_KEY**

   Read **[environment variables reference](/docs/setup/env-vars)**

3. Create a Kubernetes deployment

   ```bash
   kubectl apply -f https://tooljet-deployments.s3.us-west-1.amazonaws.com/kubernetes/deployment.yaml
   ```

:::info
The file given above is just a template and might not suit production environments. You should download the file and configure parameters such as the replica count and environment variables according to your needs.
:::

:::info
If there are self signed HTTPS endpoints that ToolJet needs to connect to, please make sure that `NODE_EXTRA_CA_CERTS` environment variable is set to the absolute path containing the certificates. You can make use of kubernetes secrets to mount the certificate file onto the containers.
:::

4. Verify if ToolJet is running

   ```bash
    kubectl get pods
   ```

5. Create a Kubernetes services to publish the Kubernetes deployment that you've created. This step varies with cloud providers. We have a [template](https://tooljet-deployments.s3.us-west-1.amazonaws.com/kubernetes/service.yaml) for exposing the ToolJet server as a service using an AWS loadbalancer.

   **Examples:**

   - [Application load balancing on Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/alb-ingress.html)
   - [GKE Ingress for HTTP(S) Load Balancing](https://cloud.google.com/kubernetes-engine/docs/concepts/ingress)

:::tip
If you want to serve ToolJet client from services such as Firebase or Netlify, please read the client Setup documentation **[here](/docs/setup/client)**.
:::

## ToolJet Database

To use the ToolJet Database, you need to set up and deploy a PostgREST server, which facilitates querying the database. Detailed setup instructions are available [here](/docs/tooljet-db/tooljet-database).

Starting with ToolJet 3.0, deploying the ToolJet Database is mandatory to avoid migration issues. Refer to the documentation below for details on the new major version, including breaking changes and required adjustments for your applications.

- [ToolJet 3.0 Migration Guide for Self-Hosted Versions](./upgrade-to-v3.md)

1. Setup PostgREST server

   ```bash
   kubectl apply -f https://tooljet-deployments.s3.us-west-1.amazonaws.com/kubernetes/GKE/postgrest.yaml
   ```

2. Update ToolJet deployment with the appropriate env variables [here](https://tooljet-deployments.s3.us-west-1.amazonaws.com/kubernetes/GKE/deployment.yaml) and apply the changes.

## Upgrading to the Latest LTS Version

New LTS versions are released every 3-5 months with an end-of-life of atleast 18 months. To check the latest LTS version, visit the [ToolJet Docker Hub](https://hub.docker.com/r/tooljet/tooljet/tags) page. The LTS tags follow a naming convention with the prefix `LTS-` followed by the version number, for example `tooljet/tooljet:ee-lts-latest`.

If this is a new installation of the application, you may start directly with the latest version. This guide is not required for new installations.

#### Prerequisites for Upgrading to the Latest LTS Version:

- It is crucial to perform a **comprehensive backup of your database** before starting the upgrade process to prevent data loss.

- Users on versions earlier than **v2.23.0-ee2.10.2** must first upgrade to this version before proceeding to the LTS version.

_If you have any questions feel free to join our [Slack Community](https://join.slack.com/t/tooljet/shared_invite/zt-2rk4w42t0-ZV_KJcWU9VL1BBEjnSHLCA) or send us an email at hello@tooljet.com._

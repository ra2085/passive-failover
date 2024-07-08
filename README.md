# Apigee sample for Passive Failover

This sample demonstrates Passive Failover configuration options.

## Prerequisites
1. [Provision Apigee X](https://cloud.google.com/apigee/docs/api-platform/get-started/provisioning-intro)
2. Access to deploy proxies to Apigee, deploy Cloud Run and trigger Cloud Build
3. Configure [external access](https://cloud.google.com/apigee/docs/api-platform/get-started/configure-routing#external-access) for API traffic to your Apigee X instance
4. Make sure the following tools are available in your terminal's $PATH (Cloud Shell has these pre-configured)
    * [gcloud SDK](https://cloud.google.com/sdk/docs/install)
    * unzip
    * curl
    * jq
    * npm

## Setup instructions

1. Clone the passive-failover repo, and switch the spike-arrest directory

```bash
git clone https://github.com/ra2085/passive-failover.git
cd passive-failover
```

2. Edit the `env.sh` and configure the ENV vars

* `PROJECT` the project where your Apigee organization is located
* `APIGEE_HOST` the externally reachable hostname of the Apigee environment group that contains APIGEE_ENV
* `APIGEE_ENV` the Apigee environment where the demo resources should be created
* `PRIMARY_TARGET` the primary target to route traffic to
* `SECONDARY_TARGET` the secondary target / failover

Now source the `env.sh` file

```bash
source ./env.sh
```

## Deploy Apigee components

Next, let's create and deploy the Apigee resources.

```sh
./deploy-active-retry.sh
```

## Test the APIs

You can test the API call to make sure the deployment was successful

```sh
curl --location --request GET "https://$APIGEE_HOST/active-retry" -H "x-apikey: $API_KEY" -vvv
```

## Cleanup

If you want to clean up the artifacts from this example in your Apigee Organization, first source your `env.sh` script, and then run

```bash
./clean-up-active-retry.sh
```

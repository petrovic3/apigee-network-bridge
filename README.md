# apigee-network-bridge

This repo creates a network bridge between [Google Cloud Load Balancer](https://cloud.google.com/load-balancing/docs/https) and [Apigee public cloud](https://cloud.google.com/apigee/docs) running on GCP.

## Architecture

The Apigee service when provisioned in GCP, it is available as a private service (behind an internal load balancer). 

<img src="./ngsaas-networking.png" align="center">

This repo contains scripts that provisions a managed instance group with NAT rules to forward API requests from an external load balancer to Apigee's internal load balancer. 

## Prerequisites

* An Apigee org is provisioned. See [here](https://cloud.google.com/apigee/docs/api-platform/get-started/overview) for instructions. 
* gcloud CLI is installed

To know which runtime instances you have, run the command:

```bash
token="$(gcloud auth print-access-token)"
curl -H "Authorization: Bearer $token" https://apigee.googleapis.com/v1/organizations/{org}/instances
```

### VPC Peering

If you haven't done so already, use this script to configure Service Networking to peer with Apigee. NOTE: You can skip this step if you have already run the eval wizard https://apigee.google.com/setup/eval

```bash
./setup-peering.sh $PROJECTID
```

## Installation

* [Install via scripts](./scripts)
* [Install via Terraform](./tform)

___

## Support

This is not an officially supported Google product

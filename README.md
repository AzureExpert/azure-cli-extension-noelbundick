# Noel's grab bag of Azure CLI goodies

This repo contains things that I like or find useful, offered up with absolutely zero guarantee that it will work for anyone else

## Azure Active Directory

* `az ad app list-mine`: List only the applications you own
* `az ad sp create-for-ralph`: Create a service principal and store the password in Key Vault ([thread](https://twitter.com/acanthamoeba/status/988185653199360002))
* `az ad sp list-mine`: List only the service principals you own. Optionally filter by expiration

## Log Analytics

* `az loganalytics workspace create`
* `az loganalytics workspace delete`
* `az loganalytics workspace show`
* `az loganalytics workspace update`
* `az loganalytics workspace keys list`

## Self-Destruct Mode

Set an expiration time when creating a resource or resource group, and a Logic App will automatically delete it when the time's up.

* `az * create --self-destruct`: Global argument that enables automatic deletion. You can specify self-destruct dates like 1d, 6h, 2h30m, 30m, etc
* `az self-destruct arm`: Enable automatic deletion on a resource that already exists
* `az self-destruct configure`: One-time configuration
* `az self-destruct disarm`: Disable automatic deletion for a resource
* `az self-destruct list`: List items that are scheduled for deletion

> Works on management-plane resources only (resource groups, storage accounts, VMs). Guaranteed to be broken for data-plane operations like blobs

### Usage

```bash
az self-destruct configure
az group create -n myRG -l eastus --self-destruct 1h
```

## Virtual Machines

* `az vm auto-shutdown enable`
* `az vm auto-shutdown disable`
* `az vm auto-shutdown show`

## Development

Use the `scripts/hack.sh` script

```bash
source scripts/hack.sh
```

or, do it the long way with your directories

```bash
export AZURE_EXTENSION_DIR=~/.azure/devcliextensions
pip install --upgrade --target ~/.azure/devcliextensions/noelbundick ~/code/noelbundick/azure-cli-extension-noelbundick/src/noelbundick
```
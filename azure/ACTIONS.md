# GitHub Actions

## Create Azure Service Principal and GitHub Actions Secret

1. Open <https://shell.azure.com/> and run the following snippet:
```bash
SUBSCRIPTION_ID=$(az account show | jq -r .id)
RESOURCE_GROUP='200200-actions'
LOCATION='eastus'

az group create -n $RESOURCE_GROUP -l $LOCATION

SP=$(az ad sp create-for-rbac -n $RESOURCE_GROUP --role contributor \
    --scopes "/subscriptions/${SUBSCRIPTION_ID}/resourceGroups/${RESOURCE_GROUP}")
echo $SP
```

2. Copy the JSON above and create a secret `AZURE_CREDENTIALS` under `Settings > Secrets` in your GitHub repository (e.g. <https://github.com/asw101/python-actions-flask-aci/settings/secrets>).

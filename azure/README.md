# Deploy to Azure with GitHub Actions

## 1. Create Azure Service Principal 

Open <https://shell.azure.com/> and run the following snippet:
```bash
RESOURCE_GROUP='200200-actions'
LOCATION='eastus'
SUBSCRIPTION_ID=$(az account show | jq -r .id)

az group create -n $RESOURCE_GROUP -l $LOCATION

SP=$(az ad sp create-for-rbac -n $RESOURCE_GROUP --role contributor \
    --scopes "/subscriptions/${SUBSCRIPTION_ID}/resourceGroups/${RESOURCE_GROUP}")
echo $SP
```

## 2. Create GitHub Actions Secret

Copy the JSON above and create a secret `AZURE_CREDENTIALS` under `Settings > Secrets` in your GitHub repository (e.g. <https://github.com/asw101/python-actions-flask-aci/settings/secrets>).

## 3. Modify [DEPLOY.sh](DEPLOY.sh) and trigger a build

1. Set the correct variables for `RESOURCE_GROUP`, etc, under `# variables` in [DEPLOY.sh](DEPLOY.sh).
1. Modify [DEPLOY.txt](DEPLOY.txt) to trigger a build.

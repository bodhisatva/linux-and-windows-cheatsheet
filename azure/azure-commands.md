# Azure

Azure CLI setup on macOS and basic commands with example use cases.

## Azure CLI installation and setup

Install Azure CLI with Homebrew:

```sh
brew update && brew install azure-cli
```

Open Azure CLI:

```sh
az
```

You need to sign in to your Azure account:

```sh
az login
```

The command will open a web browser window where you can sign in with your Azure credentials.

After signing in, return to the terminal.

## CLI Basic Commands

| Command                                                        | Description                                                                                       |
| -------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `az version`                                                   | Displays the version of the Azure CLI installed on your system.                                   |
| `az account show`                                              | Shows details of the currently active Azure subscription.                                         |
| `az account list --output table`                               | Lists all subscriptions associated with your account in a table format.                           |
| `az account list-locations --output table \| grep -i <region>` | List all available regions                                                                        |
| `az config set core.output=jsonc`                              | Sets the default output format to JSON with colorization (jsonc).                                 |
| `az interactive`                                               | Launches the Azure CLI in interactive mode, providing auto-completion and context-sensitive help. |

### Creating and deleting a resource group

List all resource groups:

```bash
az group list
```

If you don't already have a resource group, create one using command:

```bash
az group create --name <resource_name> --location <resource_location>

# az group create --name testing-cli-group --location swedencentral
```

Show detail of a resource group:

```bash
az group show --name <resource_name>

# az group show --name testing-cli-group
```

Delete a resource group:

```bash
az group delete --name <resource_name>

# az group delete --name testing-cli-group
```

### Creating a storage resource

List all resources in the current subscription:

```bash
az resource list
```

To list only storage accounts and select their names, locations and resource groups:

```bash
az storage account list --query "[].{Name:name, Location:primaryLocation, ResourceGroup:resourceGroup}" --output table
```

Create a storage account with a unique name:

```bash
az storage account create --resource-group <resource_group_name> --name <store_name> --location <azure_region> --sku <replication_strategy> --kind <storage_account_type>

# az storage account create --resource-group testing-cli-group --name testingclistorage --location swedencentral --sku Standard_LRS --kind StorageV2
```

Creating a Blob container requires authentication. To retrieve the storage account key:

```bash
STORAGE_KEY=$(az storage account keys list --resource-group <resource_group_name> --account-name <storage_account_name> --query '[0].value' --output tsv)

# STORAGE_KEY=$(az storage account keys list --resource-group testing-cli-group --account-name testingclistorage --query '[0].value' --output tsv)
```

Create a Blob container:

```bash
az storage container create --name <storage_container_name> --account-name <storage_account_name> --account-key $STORAGE_KEY

# az storage container create --name clicontainername --account-name testingclistorage --account-key $STORAGE_KEY
```

### Creating a virtual network

Virtual network must be created in the same region where the VM is created and should have an IP range different from, for example, used in a home network. Virtual network contains an IP address range for outgoing resources.

```bash
az network create --resource-group <resource-group-name> --address-prefix 10.0.0.0/16 --subnet-name <subnet-name> --subnet-prefix 10.0.1.0/24

```

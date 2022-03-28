# dp-420

This repository makes use of .NET Interactive Workbooks, as part of Visual Studio Code. For more information, visit [https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.dotnet-interactive-vscode](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.dotnet-interactive-vscode)

## Getting started

- Install the latest [Visual Studio Code](https://code.visualstudio.com/).

- Install the latest [.NET 6 SDK](https://dotnet.microsoft.com/download/dotnet/6.0)
- Install [.NET 3.1 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/3.1) (used by cosmicworks command-line tool)

- Install the .NET Interactive Notebooks extension from the [marketplace](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.dotnet-interactive-vscode).

- Azure CLI and Azure PowerShell

```bash
sudo apt-get update
sudo apt-get install azure-cli
sudo apt-get install powershell
pwsh
Install-Module -Name Az -AllowClobber -Scope CurrentUser
```

- Install the cosmicworks command-line tool for global use on your machine.

```bash
dotnet tool install --global cosmicworks
```

## Lab materials

Lab materials are available [here](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/)

## DP-420 Learn Collection

[Self-paced modules on Microsoft Learn](https://docs.microsoft.com/en-us/users/msftofficialcurriculum-4292/collections/1k8wcz8zooj2nx)

## Setup for demo's

```bash
az login
az account set --subscription "<subscriptionid>"
az group create --name rg-dp-420 --location westeurope

az cosmosdb create --name cosmos-dp-420-sql-provisioned --resource-group rg-dp-420
az cosmosdb create --name cosmos-dp-420-sql-serverless --resource-group rg-dp-420

COSMOS_DB_PROVISIONED_CONNECTION_STRING=$(az cosmosdb keys list --name cosmos-dp-420-sql-provisioned --resource-group rg-dp-420 --type connection-strings --query "connectionStrings[?description=='Primary SQL Connection String'].connectionString" --output tsv)

COSMOS_DB_SERVERLESS_CONNECTION_STRING=$(az cosmosdb keys list --name cosmos-dp-420-sql-serverless --resource-group rg-dp-420 --type connection-strings --query "connectionStrings[?description=='Primary SQL Connection String'].connectionString" --output tsv)
```

(in the notebooks we can get this through a powershell cell and share the result in a C# cell)

```pwsh
Connect-AzAccount
Set-AzContext -Subscription "b895a719-7034-411a-9944-ff196d1f450f"

$cosmosDBConnectionString = (Get-AzCosmosDBAccountKey -ResourceGroupName rg-dp-420 -Name cosmos-dp-420-sql-provisioned -Type "ConnectionStrings")["Primary SQL Connection String"]
````

```csharp
#!share --from pwsh cosmosDBConnectionString
Console.WriteLine(cosmosDBConnectionString)
```

## Modules

- Module 01: Get started with Azure Cosmos DB SQL API
  - [[notebook]](notebooks/module-01.ipynb)
  - [[Learning path]](https://docs.microsoft.com/en-us/learn/paths/get-started-azure-cosmos-db-sql-api/?ns-enrollment-type=Collection&ns-enrollment-id=1k8wcz8zooj2nx)
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/01-create-account.html): Create an Azure Cosmos DB SQL API account
- Module 02: Plan and implement Azure Cosmos DB SQL API
  - [[notebook]](notebooks/module-02.ipynb)
  - [[Learning path]](https://docs.microsoft.com/en-us/learn/paths/plan-implement-azure-cosmos-db-sql-api/?ns-enrollment-type=Collection&ns-enrollment-id=1k8wcz8zooj2nx)
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/02-configure-throughput.html): Configure throughput for Azure Cosmos DB SQL API with the Azure portal
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/03-migrate-data.html): Migrate existing data using Azure Data Factory
- Module 03: Connect to Azure Cosmos DB SQL API with the SDK
  - [[notebook]](notebooks/module-03.ipynb)
  - [[Learning path]](https://docs.microsoft.com/en-us/learn/paths/connect-to-azure-cosmos-db-sql-api-sdk/?ns-enrollment-type=Collection&ns-enrollment-id=1k8wcz8zooj2nx)
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/04-sdk-connect.html): Connect to Azure Cosmos DB SQL API with the SDK
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/05-sdk-offline.html): Configure the Azure Cosmos DB SQL API SDK for offline development
- Module 04: Access and manage data with the Azure Cosmos DB SQL API SDKs
  - [[notebook]](notebooks/module-04.ipynb)
  - [[Learning path]](https://docs.microsoft.com/en-us/learn/paths/access-manage-data-azure-cosmos-db-sql-api-sdks/?ns-enrollment-type=Collection&ns-enrollment-id=1k8wcz8zooj2nx)
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/06-sdk-crud.html): Create and update documents with the Azure Cosmos DB SQL API SDK
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/07-sdk-batch.html): Batch multiple point operations together with the Azure Cosmos DB SQL API SDK
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/08-sdk-bulk.html): Move multiple documents in bulk with the Azure Cosmos DB SQL API SDK
- Module 05: Execute queries in Azure Cosmos DB SQL API
  - [[notebook]](notebooks/module-05.ipynb)
  - [[Learning path]](https://docs.microsoft.com/en-us/learn/paths/execute-queries-azure-cosmos-db-sql-api/?ns-enrollment-type=Collection&ns-enrollment-id=1k8wcz8zooj2nx)
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/09-sdk-queries.html): Execute a query with the Azure Cosmos DB SQL API SDK
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/10-sdk-pagination.html): Paginate cross-product query results with the Azure Cosmos DB SQL API SDK
- Module 06: Define and implement an indexing strategy for Azure Cosmos DB SQL API
  - [[notebook]](notebooks/module-06.ipynb)
  - [[Learning path]](https://docs.microsoft.com/en-us/learn/paths/define-implement-indexing-strategy-cosmos-db-sql-api/?ns-enrollment-type=Collection&ns-enrollment-id=1k8wcz8zooj2nx)
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/11-default-indexing-policy.html): Review the default index policy for an Azure Cosmos DB SQL API container with the portal
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/12-sdk-indexing-policy-custom.html): Configure an Azure Cosmos DB SQL API container’s index policy with the portal
- Module 07: Integrate Azure Cosmos DB SQL API with Azure services
  - [[notebook]](notebooks/module-07.ipynb)
  - [[Learning path]](https://docs.microsoft.com/en-us/learn/paths/integrate-azure-cosmos-db-sql-api-azure-services/?ns-enrollment-type=Collection&ns-enrollment-id=1k8wcz8zooj2nx)
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/13-change-feed.html): Process change feed events using the Azure Cosmos DB SQL API SDK
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/14-functions.html): Process Azure Cosmos DB SQL API data using Azure Functions
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/15-cognitive-search.html): Search data using Azure Cognitive Search and Azure Cosmos DB SQL API
- Module 08: Implement a data modeling and partitioning strategy for Azure Cosmos DB SQL API
  - [[notebook]](notebooks/module-08.ipynb)
  - [[Learning path]](https://docs.microsoft.com/en-us/learn/paths/implement-modeling-partitioning-azure-cosmos-db-sql-api/?ns-enrollment-type=Collection&ns-enrollment-id=1k8wcz8zooj2nx)
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/16-measure-performance.html): Measure performance of entities in separate and embeded containers
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/17-denormalize.html): Cost of denormalizing data and aggregates and using the change feed for referential integrity
- Module 09: Design and implement a replication strategy for Azure Cosmos DB SQL API
  - [[notebook]](notebooks/module-09.ipynb)
  - [[Learning path]](https://docs.microsoft.com/en-us/learn/paths/design-implement-replication-strategy-cosmos-db-sql-api/?ns-enrollment-type=Collection&ns-enrollment-id=1k8wcz8zooj2nx)
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/20-sdk-regions.html): Connect to different regions with the Azure Cosmos DB SQL API SDK
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/21-sdk-consistency-model.html): Configure consistency models in the portal and the Azure Cosmos DB SQL API SDK
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/22-sdk-multi-region.html): Connect to a multi-region write account with the Azure Cosmos DB SQL API SDK
- Module 10: Optimize query and operation performance in Azure Cosmos DB SQL API
  - [[notebook]](notebooks/module-10.ipynb)
  - [[Learning path]](https://docs.microsoft.com/en-us/learn/paths/optimize-query-performance-azure-cosmos-db-sql-api/?ns-enrollment-type=Collection&ns-enrollment-id=1k8wcz8zooj2nx)
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/23-index-optimization.html): Optimize an Azure Cosmos DB SQL API container indexing policy for write operations
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/24-query-optimization.html): Optimize an Azure Cosmos DB SQL API container indexing policy for a query
- Module 11: Monitor and troubleshoot an Azure Cosmos DB SQL API solution
  - [[notebook]](notebooks/module-11.ipynb)
  - [[Learning path]](https://docs.microsoft.com/en-us/learn/paths/monitor-troubleshoot-azure-cosmos-db-sql-api-solution/?ns-enrollment-type=Collection&ns-enrollment-id=1k8wcz8zooj2nx)
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/25-monitor.html): Use Azure Monitor to analyze an Azure Cosmos DB SQL API account
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/26-sdk-troubleshoot.html): Troubleshoot an application using the Azure Cosmos DB SQL API SDK
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/28-key-vault.html): Store Azure Cosmos DB SQL API account keys in Azure Key Vault
- Module 12: Manage an Azure Cosmos DB SQL API solution using DevOps practices
  - [[notebook]](notebooks/module-12.ipynb)
  - [[Learning path]](https://docs.microsoft.com/en-us/learn/paths/manage-cosmos-db-sql-api-solution-using-devops-practices/?ns-enrollment-type=Collection&ns-enrollment-id=1k8wcz8zooj2nx)
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/30-adjust-throughput-cli-script.html): Adjust provisioned throughput using an Azure CLI script
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/31-create-container-arm-template.html): Create an Azure Cosmos DB SQL API container using Azure Resource Manager templates
- Module 13: Create server-side programming constructs in Azure Cosmos DB SQL API
  - [[notebook]](notebooks/module-13.ipynb)
  - [[Learning path]](https://docs.microsoft.com/en-us/learn/paths/create-server-side-programming-azure-cosmos-db-sql-api/?ns-enrollment-type=Collection&ns-enrollment-id=1k8wcz8zooj2nx)
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/32-create-sproc-portal.html): Create a stored procedure with the Azure portal
  - [[Lab]](https://microsoftlearning.github.io/dp-420-cosmos-db-dev/instructions/33-create-use-udf-sdk.html): Implement and then use a UDF using the SDK

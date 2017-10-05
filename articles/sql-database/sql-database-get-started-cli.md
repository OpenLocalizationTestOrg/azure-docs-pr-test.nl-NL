---
title: 'Azure CLI: een SQL-database maken | Microsoft Docs'
description: Meer informatie over hoe u met behulp van de Azure CLI een logische SQL Database-server, een firewallregel op serverniveau en databases maakt.
keywords: zelfstudie over sql-database, een sql-database maken
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: a735f7e6aa65ac36dc4e5a49c5a9a834be43d71a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-single-azure-sql-database-using-the-azure-cli"></a><span data-ttu-id="31524-104">Een individuele Azure SQL-database maken met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="31524-104">Create a single Azure SQL database using the Azure CLI</span></span>

<span data-ttu-id="31524-105">De Azure CLI wordt gebruikt voor het maken en beheren van Azure-resources vanaf de opdrachtregel of in scripts.</span><span class="sxs-lookup"><span data-stu-id="31524-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="31524-106">Deze handleiding geeft meer informatie over het gebruik van de Azure CLI voor het implementeren van een Azure SQL-database in een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) in een [logische Azure SQL Database-server](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="31524-106">This guide details using the Azure CLI to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="31524-107">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="31524-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="31524-108">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="31524-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="31524-109">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="31524-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="31524-110">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="31524-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="define-variables"></a><span data-ttu-id="31524-111">Variabelen definiëren</span><span class="sxs-lookup"><span data-stu-id="31524-111">Define variables</span></span>

<span data-ttu-id="31524-112">Definieer variabelen voor gebruik in de scripts in deze Quick Start.</span><span class="sxs-lookup"><span data-stu-id="31524-112">Define variables for use in the scripts in this quick start.</span></span>

```azurecli-interactive
# The data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# The logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# The ip address range that you want to allow to access your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# The database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a><span data-ttu-id="31524-113">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="31524-113">Create a resource group</span></span>

<span data-ttu-id="31524-114">Maak een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) met de opdracht [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="31524-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="31524-115">Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en groepsgewijs worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="31524-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="31524-116">In het volgende voorbeeld wordt een resourcegroep met de naam `myResourceGroup` gemaakt op de locatie `westeurope`.</span><span class="sxs-lookup"><span data-stu-id="31524-116">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="31524-117">Een logische server maken</span><span class="sxs-lookup"><span data-stu-id="31524-117">Create a logical server</span></span>

<span data-ttu-id="31524-118">Als u een [logische Azure SQL Database-server](sql-database-features.md) wilt maken, gebruikt u de opdracht [az sql server create](/cli/azure/sql/server#create).</span><span class="sxs-lookup"><span data-stu-id="31524-118">Create an [Azure SQL Database logical server](sql-database-features.md) using the [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="31524-119">Een logische server bevat een groep met databases die worden beheerd als groep.</span><span class="sxs-lookup"><span data-stu-id="31524-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="31524-120">In het volgende voorbeeld wordt een server met een willekeurige naam gemaakt in de resourcegroep met een beheerdersaccount met de gebruikersnaam `ServerAdmin` en het wachtwoord `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="31524-120">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="31524-121">U kunt deze vooraf gedefinieerde waarden vervangen.</span><span class="sxs-lookup"><span data-stu-id="31524-121">Replace these pre-defined values as desired.</span></span>

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="31524-122">Een serverfirewallregel configureren</span><span class="sxs-lookup"><span data-stu-id="31524-122">Configure a server firewall rule</span></span>

<span data-ttu-id="31524-123">Maak een [Azure SQL Database-firewallregel op serverniveau](sql-database-firewall-configure.md) met de opdracht [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="31524-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="31524-124">Een firewallregel op serverniveau kan een externe toepassing, zoals SQL Server Management Studio of het hulpprogramma SQLCMD verbinding laten maken met een SQL-database via de firewall van de SQL Database-service.</span><span class="sxs-lookup"><span data-stu-id="31524-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span></span> <span data-ttu-id="31524-125">In het volgende voorbeeld wordt de firewall alleen geopend voor andere Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="31524-125">In the following example, the firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="31524-126">Voor externe connectiviteit wijzigt u het IP-adres in een correct adres voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="31524-126">To enable external connectivity, change the IP address to an appropriate address for your environment.</span></span> <span data-ttu-id="31524-127">Als u alle IP-adressen wilt openen, gebruikt u 0.0.0.0 als beginadres en 255.255.255.255 als eindadres.</span><span class="sxs-lookup"><span data-stu-id="31524-127">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="31524-128">SQL Database communiceert via poort 1433.</span><span class="sxs-lookup"><span data-stu-id="31524-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="31524-129">Als u verbinding probeert te maken vanuit een bedrijfsnetwerk, wordt uitgaand verkeer via poort 1433 mogelijk niet toegestaan door de firewall van uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="31524-129">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="31524-130">In dat geval kunt u alleen verbinding maken met uw Azure SQL Database-server als uw IT-afdeling poort 1433 openstelt.</span><span class="sxs-lookup"><span data-stu-id="31524-130">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-the-server-with-sample-data"></a><span data-ttu-id="31524-131">Een database op de server maken met voorbeeldgegevens</span><span class="sxs-lookup"><span data-stu-id="31524-131">Create a database in the server with sample data</span></span>

<span data-ttu-id="31524-132">Maak een database met een [prestatieniveau van S0](sql-database-service-tiers.md) op de server met de opdracht [az sql db create](/cli/azure/sql/db#create).</span><span class="sxs-lookup"><span data-stu-id="31524-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="31524-133">In het volgende voorbeeld wordt een database met de naam `mySampleDatabase` gemaakt en worden de gegevens uit het AdventureWorksLT-voorbeeld in deze database geladen.</span><span class="sxs-lookup"><span data-stu-id="31524-133">The following example creates a database called `mySampleDatabase` and loads the AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="31524-134">U kunt deze vooraf gedefinieerde waarden desgewenst vervangen. (Andere Quick Starts in deze verzameling zijn echter op de waarden in deze Quick Start gebaseerd.)</span><span class="sxs-lookup"><span data-stu-id="31524-134">Replace these predefined values as desired (other quick starts in this collection build upon the values in this quick start).</span></span>

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="31524-135">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="31524-135">Clean up resources</span></span>

<span data-ttu-id="31524-136">Andere Quick Starts in deze verzameling zijn op deze Quick Start gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="31524-136">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="31524-137">Als u van plan bent om door te gaan met andere Quick Starts, verwijdert u de resources die u in deze Quick Start hebt gemaakt niet.</span><span class="sxs-lookup"><span data-stu-id="31524-137">If you plan to continue on to work with subsequent quick starts, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="31524-138">Als u niet wilt doorgaan, gebruikt u de volgende stappen om alle resources te verwijderen die door deze Quick Start in Azure Portal zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="31524-138">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="31524-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="31524-139">Next steps</span></span>

<span data-ttu-id="31524-140">Nu u een database hebt, kunt u verbinding maken met een hulpprogramma naar keuze en hiermee query's uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="31524-140">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="31524-141">Klik op de onderstaande hulpprogramma's voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="31524-141">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="31524-142">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="31524-142">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="31524-143">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="31524-143">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="31524-144">.NET</span><span class="sxs-lookup"><span data-stu-id="31524-144">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="31524-145">PHP</span><span class="sxs-lookup"><span data-stu-id="31524-145">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="31524-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="31524-146">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="31524-147">Java</span><span class="sxs-lookup"><span data-stu-id="31524-147">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="31524-148">Python</span><span class="sxs-lookup"><span data-stu-id="31524-148">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="31524-149">Ruby</span><span class="sxs-lookup"><span data-stu-id="31524-149">Ruby</span></span>](sql-database-connect-query-ruby.md)


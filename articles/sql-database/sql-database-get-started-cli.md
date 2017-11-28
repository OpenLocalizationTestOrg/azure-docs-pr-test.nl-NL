---
title: 'Azure CLI: een SQL-database maken | Microsoft Docs'
description: Meer informatie over hoe Hallo toocreate een logische SQL Database-server, firewallregel op serverniveau en databases die gebruikmaken van Azure CLI.
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
ms.openlocfilehash: 9b1ffb17eabeb70a000ff0c997128832b07aa4fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a><span data-ttu-id="4a7e1-104">Maken van één Azure SQL database met behulp van hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4a7e1-104">Create a single Azure SQL database using hello Azure CLI</span></span>

<span data-ttu-id="4a7e1-105">Hello Azure CLI is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="4a7e1-106">Deze handleiding hello Azure CLI toodeploy wilt weergeven voor een Azure SQL database in een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) in een [logische Azure SQL Database-server](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="4a7e1-106">This guide details using hello Azure CLI toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="4a7e1-107">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4a7e1-108">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, in dit onderwerp is vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="4a7e1-109">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4a7e1-110">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4a7e1-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="define-variables"></a><span data-ttu-id="4a7e1-111">Variabelen definiëren</span><span class="sxs-lookup"><span data-stu-id="4a7e1-111">Define variables</span></span>

<span data-ttu-id="4a7e1-112">Definieer de variabelen voor gebruik in Hallo-scripts in deze snel starten.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-112">Define variables for use in hello scripts in this quick start.</span></span>

```azurecli-interactive
# hello data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# hello ip address range that you want tooallow tooaccess your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# hello database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a><span data-ttu-id="4a7e1-113">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="4a7e1-113">Create a resource group</span></span>

<span data-ttu-id="4a7e1-114">Maak een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) met Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="4a7e1-115">Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en groepsgewijs worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="4a7e1-116">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westeurope` locatie.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-116">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="4a7e1-117">Een logische server maken</span><span class="sxs-lookup"><span data-stu-id="4a7e1-117">Create a logical server</span></span>

<span data-ttu-id="4a7e1-118">Maak een [logische Azure SQL Database-server](sql-database-features.md) met Hallo [az sql server maken](/cli/azure/sql/server#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-118">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="4a7e1-119">Een logische server bevat een groep met databases die worden beheerd als groep.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="4a7e1-120">Hallo volgende voorbeeld wordt een willekeurige naam server in de resourcegroep met de beheerderaanmelding van een met de naam `ServerAdmin` en het wachtwoord `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-120">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="4a7e1-121">U kunt deze vooraf gedefinieerde waarden vervangen.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-121">Replace these pre-defined values as desired.</span></span>

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="4a7e1-122">Een serverfirewallregel configureren</span><span class="sxs-lookup"><span data-stu-id="4a7e1-122">Configure a server firewall rule</span></span>

<span data-ttu-id="4a7e1-123">Maak een [Azure SQL Database firewallregel op serverniveau](sql-database-firewall-configure.md) met Hallo [az sql server-firewall maken](/cli/azure/sql/server/firewall-rule#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="4a7e1-124">Een firewallregel op serverniveau kunt een externe toepassing, zoals SQL Server Management Studio of Hallo SQLCMD-hulpprogramma tooconnect tooa SQL-database via Hallo SQL Database-service firewall.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="4a7e1-125">In Hallo voorbeeld te volgen, wordt alleen Hallo firewall geopend voor andere Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-125">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="4a7e1-126">tooenable externe connectiviteit wijziging Hallo IP-adres tooan juiste adres voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-126">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="4a7e1-127">tooopen alle IP-adressen 0.0.0.0 gebruiken als Hallo IP-adres en 255.255.255.255 starten als Hallo eindadres.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-127">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="4a7e1-128">SQL Database communiceert via poort 1433.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="4a7e1-129">Als u tooconnect van binnen een bedrijfsnetwerk probeert, kan uitgaand verkeer via poort 1433 niet worden toegestaan door de firewall van uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-129">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="4a7e1-130">Zo ja, zich u niet kunnen tooconnect tooyour Azure SQL Database-server tenzij uw IT-afdeling poort 1433 wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-130">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="4a7e1-131">Een database in het Hallo-server met voorbeeldgegevens maken</span><span class="sxs-lookup"><span data-stu-id="4a7e1-131">Create a database in hello server with sample data</span></span>

<span data-ttu-id="4a7e1-132">Maken van een database met een [prestatieniveau S0](sql-database-service-tiers.md) in Hallo-server op Hallo met [az sql-database maken](/cli/azure/sql/db#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="4a7e1-133">Hallo volgende voorbeeld maakt u een database met de naam `mySampleDatabase` en belastingen Hallo AdventureWorksLT voorbeeldgegevens in deze database.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-133">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="4a7e1-134">Vervang deze vooraf gedefinieerde waarden naar wens (andere snel aan de slag in deze verzameling gebouwd op Hallo-waarden in deze snel starten).</span><span class="sxs-lookup"><span data-stu-id="4a7e1-134">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="4a7e1-135">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="4a7e1-135">Clean up resources</span></span>

<span data-ttu-id="4a7e1-136">Andere Quick Starts in deze verzameling zijn op deze Quick Start gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-136">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="4a7e1-137">Als u van plan toocontinue toowork met latere snel aan de slag bent, Hallo-resources die zijn gemaakt in deze snelle opruimen start niet.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-137">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="4a7e1-138">Als u niet van plan toocontinue bent, gebruikt u Hallo na stappen toodelete alle resources gemaakt door deze snel starten in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-138">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="4a7e1-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4a7e1-139">Next steps</span></span>

<span data-ttu-id="4a7e1-140">Nu u een database hebt, kunt u verbinding maken met een hulpprogramma naar keuze en hiermee query's uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4a7e1-140">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="4a7e1-141">Klik op de onderstaande hulpprogramma's voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="4a7e1-141">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="4a7e1-142">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="4a7e1-142">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="4a7e1-143">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="4a7e1-143">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="4a7e1-144">.NET</span><span class="sxs-lookup"><span data-stu-id="4a7e1-144">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="4a7e1-145">PHP</span><span class="sxs-lookup"><span data-stu-id="4a7e1-145">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="4a7e1-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="4a7e1-146">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="4a7e1-147">Java</span><span class="sxs-lookup"><span data-stu-id="4a7e1-147">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="4a7e1-148">Python</span><span class="sxs-lookup"><span data-stu-id="4a7e1-148">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="4a7e1-149">Ruby</span><span class="sxs-lookup"><span data-stu-id="4a7e1-149">Ruby</span></span>](sql-database-connect-query-ruby.md)


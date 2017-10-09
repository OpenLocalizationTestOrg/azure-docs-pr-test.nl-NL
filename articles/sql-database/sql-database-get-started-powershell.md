---
title: 'Azure PowerShell: een SQL-database maken | Microsoft Docs'
description: Meer informatie over hoe Hallo toocreate een logische SQL Database-server, firewallregel op serverniveau en databases die in Azure-portal.
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
ms.devlang: PowerShell
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: e89f68b44083a3b64e61f95117dbbedfa6647ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="21ba6-104">Een individuele Azure SQL Database maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="21ba6-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="21ba6-105">PowerShell is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts.</span><span class="sxs-lookup"><span data-stu-id="21ba6-105">PowerShell is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="21ba6-106">Deze handleiding PowerShell toodeploy wilt weergeven voor een Azure SQL database in een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) in een [logische Azure SQL Database-server](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="21ba6-106">This guide details using PowerShell toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="21ba6-107">Als u nog geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="21ba6-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="21ba6-108">Deze zelfstudie vereist hello Azure PowerShell-moduleversie 4.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="21ba6-108">This tutorial requires hello Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="21ba6-109">Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="21ba6-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="21ba6-110">Als u tooinstall of upgrade nodig hebt, raadpleegt u [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="21ba6-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="21ba6-111">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="21ba6-111">Log in tooAzure</span></span>

<span data-ttu-id="21ba6-112">Tooyour aanmelden met Azure-abonnement met Hallo [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) opdracht in en volg Hallo op het scherm instructies.</span><span class="sxs-lookup"><span data-stu-id="21ba6-112">Log in tooyour Azure subscription using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command and follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="21ba6-113">Variabelen maken</span><span class="sxs-lookup"><span data-stu-id="21ba6-113">Create variables</span></span>

<span data-ttu-id="21ba6-114">Definieer de variabelen voor gebruik in Hallo-scripts in deze snel starten.</span><span class="sxs-lookup"><span data-stu-id="21ba6-114">Define variables for use in hello scripts in this quick start.</span></span>

```powershell
# hello data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# hello login information for hello server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# hello ip address range that you want tooallow tooaccess your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# hello database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="21ba6-115">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="21ba6-115">Create a resource group</span></span>

<span data-ttu-id="21ba6-116">Maak een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) met Hallo [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) opdracht.</span><span class="sxs-lookup"><span data-stu-id="21ba6-116">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="21ba6-117">Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en groepsgewijs worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="21ba6-117">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="21ba6-118">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westeurope` locatie.</span><span class="sxs-lookup"><span data-stu-id="21ba6-118">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="21ba6-119">Een logische server maken</span><span class="sxs-lookup"><span data-stu-id="21ba6-119">Create a logical server</span></span>

<span data-ttu-id="21ba6-120">Maak een [logische Azure SQL Database-server](sql-database-features.md) met Hallo [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) opdracht.</span><span class="sxs-lookup"><span data-stu-id="21ba6-120">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) command.</span></span> <span data-ttu-id="21ba6-121">Een logische server bevat een groep met databases die worden beheerd als groep.</span><span class="sxs-lookup"><span data-stu-id="21ba6-121">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="21ba6-122">Hallo volgende voorbeeld wordt een willekeurige naam server in de resourcegroep met de beheerderaanmelding van een met de naam `ServerAdmin` en het wachtwoord `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="21ba6-122">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="21ba6-123">U kunt deze vooraf gedefinieerde waarden vervangen.</span><span class="sxs-lookup"><span data-stu-id="21ba6-123">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="21ba6-124">Een serverfirewallregel configureren</span><span class="sxs-lookup"><span data-stu-id="21ba6-124">Configure a server firewall rule</span></span>

<span data-ttu-id="21ba6-125">Maak een [Azure SQL Database firewallregel op serverniveau](sql-database-firewall-configure.md) met Hallo [nieuw AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) opdracht.</span><span class="sxs-lookup"><span data-stu-id="21ba6-125">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="21ba6-126">Een firewallregel op serverniveau kunt een externe toepassing, zoals SQL Server Management Studio of Hallo SQLCMD-hulpprogramma tooconnect tooa SQL-database via Hallo SQL Database-service firewall.</span><span class="sxs-lookup"><span data-stu-id="21ba6-126">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="21ba6-127">In Hallo voorbeeld te volgen, wordt alleen Hallo firewall geopend voor andere Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="21ba6-127">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="21ba6-128">tooenable externe connectiviteit wijziging Hallo IP-adres tooan juiste adres voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="21ba6-128">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="21ba6-129">tooopen alle IP-adressen 0.0.0.0 gebruiken als Hallo IP-adres en 255.255.255.255 starten als Hallo eindadres.</span><span class="sxs-lookup"><span data-stu-id="21ba6-129">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="21ba6-130">SQL Database communiceert via poort 1433.</span><span class="sxs-lookup"><span data-stu-id="21ba6-130">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="21ba6-131">Als u tooconnect van binnen een bedrijfsnetwerk probeert, kan uitgaand verkeer via poort 1433 niet worden toegestaan door de firewall van uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="21ba6-131">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="21ba6-132">Zo ja, zich u niet kunnen tooconnect tooyour Azure SQL Database-server tenzij uw IT-afdeling poort 1433 wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="21ba6-132">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="21ba6-133">Een database in het Hallo-server met voorbeeldgegevens maken</span><span class="sxs-lookup"><span data-stu-id="21ba6-133">Create a database in hello server with sample data</span></span>

<span data-ttu-id="21ba6-134">Maken van een database met een [prestatieniveau S0](sql-database-service-tiers.md) in Hallo-server op Hallo met [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) opdracht.</span><span class="sxs-lookup"><span data-stu-id="21ba6-134">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="21ba6-135">Hallo volgende voorbeeld maakt u een database met de naam `mySampleDatabase` en belastingen Hallo AdventureWorksLT voorbeeldgegevens in deze database.</span><span class="sxs-lookup"><span data-stu-id="21ba6-135">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="21ba6-136">Vervang deze vooraf gedefinieerde waarden naar wens (andere snel aan de slag in deze verzameling gebouwd op Hallo-waarden in deze snel starten).</span><span class="sxs-lookup"><span data-stu-id="21ba6-136">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="21ba6-137">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="21ba6-137">Clean up resources</span></span>

<span data-ttu-id="21ba6-138">Andere Quick Starts in deze verzameling zijn op deze Quick Start gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="21ba6-138">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="21ba6-139">Als u van plan toocontinue toowork met latere snel aan de slag bent, Hallo-resources die zijn gemaakt in deze snelle opruimen start niet.</span><span class="sxs-lookup"><span data-stu-id="21ba6-139">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="21ba6-140">Als u niet van plan toocontinue bent, gebruikt u Hallo na stappen toodelete alle resources gemaakt door deze snel starten in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="21ba6-140">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="21ba6-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="21ba6-141">Next steps</span></span>

<span data-ttu-id="21ba6-142">Nu u een database hebt, kunt u verbinding maken met een hulpprogramma naar keuze en hiermee query's uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="21ba6-142">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="21ba6-143">Klik op de onderstaande hulpprogramma's voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="21ba6-143">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="21ba6-144">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="21ba6-144">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="21ba6-145">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="21ba6-145">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="21ba6-146">.NET</span><span class="sxs-lookup"><span data-stu-id="21ba6-146">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="21ba6-147">PHP</span><span class="sxs-lookup"><span data-stu-id="21ba6-147">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="21ba6-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="21ba6-148">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="21ba6-149">Java</span><span class="sxs-lookup"><span data-stu-id="21ba6-149">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="21ba6-150">Python</span><span class="sxs-lookup"><span data-stu-id="21ba6-150">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="21ba6-151">Ruby</span><span class="sxs-lookup"><span data-stu-id="21ba6-151">Ruby</span></span>](sql-database-connect-query-ruby.md)


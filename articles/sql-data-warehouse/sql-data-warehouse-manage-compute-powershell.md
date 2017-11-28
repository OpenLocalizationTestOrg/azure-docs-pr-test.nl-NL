---
title: aaaManage rekencapaciteit in Azure SQL Data Warehouse (PowerShell) | Microsoft Docs
description: PowerShell taken toomanage rekenkracht. Het aantal rekenresources door dwu's aan te passen. Of onderbreken en hervatten compute-bronnen toosave kosten.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 8354a3c1-4e04-4809-933f-db414a8c74dc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 8b379d4cf89570649767f6896d2c630d4f1111d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="045ad-105">De rekencapaciteit in Azure SQL Data Warehouse (PowerShell) beheren</span><span class="sxs-lookup"><span data-stu-id="045ad-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="045ad-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="045ad-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="045ad-107">Portal</span><span class="sxs-lookup"><span data-stu-id="045ad-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="045ad-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="045ad-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="045ad-109">REST</span><span class="sxs-lookup"><span data-stu-id="045ad-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="045ad-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="045ad-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="045ad-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="045ad-111">Before you begin</span></span>
### <a name="install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="045ad-112">Hallo meest recente versie van Azure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="045ad-112">Install hello latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="045ad-113">Azure PowerShell gebruiken met SQL Data Warehouse toouse, moet u Azure PowerShell-versie 1.0.3 of hoger.</span><span class="sxs-lookup"><span data-stu-id="045ad-113">toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="045ad-114">Hallo-opdracht uitvoeren voor tooverify uw huidige versie **Get-Module - ListAvailable-Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="045ad-114">tooverify your current version run hello command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="045ad-115">U kunt de nieuwste versie van de Hallo van installeren [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="045ad-115">You can install hello latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="045ad-116">Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="045ad-116">For more information, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="045ad-117">Aan de slag met Azure PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="045ad-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="045ad-118">tooget gestart:</span><span class="sxs-lookup"><span data-stu-id="045ad-118">tooget started:</span></span>

1. <span data-ttu-id="045ad-119">Open Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="045ad-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="045ad-120">Deze toosign opdrachten uitvoeren in Azure Resource Manager toohello bij Hallo PowerShell-prompt en uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="045ad-120">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="045ad-121">De rekencapaciteit schaal</span><span class="sxs-lookup"><span data-stu-id="045ad-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="045ad-122">toochange hello dwu's, gebruiken Hallo [Set-AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="045ad-122">toochange hello DWUs, use hello [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="045ad-123">Hallo volgende voorbeeld wordt Hallo service level objective tooDW1000 voor Hallo database MySQLDW die wordt gehost op de server MijnServer.</span><span class="sxs-lookup"><span data-stu-id="045ad-123">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="045ad-124">De rekencapaciteit onderbreken</span><span class="sxs-lookup"><span data-stu-id="045ad-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="045ad-125">een database toopause gebruiken Hallo [Suspend-AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="045ad-125">toopause a database, use hello [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="045ad-126">Hallo onderbroken volgende voorbeeld een database met naam Database02 gehost op een server met de naam Server01.</span><span class="sxs-lookup"><span data-stu-id="045ad-126">hello following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="045ad-127">Hallo-server in een Azure-resourcegroep genaamd ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="045ad-127">hello server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="045ad-128">Let op: als uw server foo.database.windows.net, "foo" gebruiken zoals Hallo - servernaam in Hallo PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="045ad-128">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="045ad-129">Een Variant dit volgende voorbeeld haalt Hallo-database naar het Hallo $database-object.</span><span class="sxs-lookup"><span data-stu-id="045ad-129">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="045ad-130">Deze geeft vervolgens Hallo-object te[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="045ad-130">It then pipes hello object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="045ad-131">Hallo resultaten worden opgeslagen in Hallo object resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="045ad-131">hello results are stored in hello object resultDatabase.</span></span> <span data-ttu-id="045ad-132">de laatste opdracht Hallo toont Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="045ad-132">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="045ad-133">Compute hervatten</span><span class="sxs-lookup"><span data-stu-id="045ad-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="045ad-134">een database toostart gebruiken Hallo [Resume-AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="045ad-134">toostart a database, use hello [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="045ad-135">Hallo wordt volgende voorbeeld een database met naam Database02 gehost op een server met de naam Server01.</span><span class="sxs-lookup"><span data-stu-id="045ad-135">hello following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="045ad-136">Hallo-server in een Azure-resourcegroep genaamd ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="045ad-136">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="045ad-137">Een Variant dit volgende voorbeeld haalt Hallo-database naar het Hallo $database-object.</span><span class="sxs-lookup"><span data-stu-id="045ad-137">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="045ad-138">Deze geeft vervolgens Hallo-object te[Resume-AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] en slaat Hallo resultaten in $resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="045ad-138">It then pipes hello object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores hello results in $resultDatabase.</span></span> <span data-ttu-id="045ad-139">de laatste opdracht Hallo toont Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="045ad-139">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="045ad-140">Controleer de databasestatus van de</span><span class="sxs-lookup"><span data-stu-id="045ad-140">Check database state</span></span>

<span data-ttu-id="045ad-141">Zoals u in Hallo bovenstaande voorbeelden, gebruiken een [Get-AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] cmdlet tooget informatie voor een database, waardoor controleren Hallo status, maar ook toouse als argument.</span><span class="sxs-lookup"><span data-stu-id="045ad-141">As shown in hello above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet tooget information on a database, thereby checking hello status, but also toouse as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="045ad-142">Die zal leiden tot iets dat</span><span class="sxs-lookup"><span data-stu-id="045ad-142">Which will result in something like</span></span> 

```powershell   
ResourceGroupName             : nytrg
ServerName                    : nytsvr
DatabaseName                  : nytdb
Location                      : West US
DatabaseId                    : 86461aae-8e3d-4ded-9389-ac9d4bc69bbb
Edition                       : DataWarehouse
CollationName                 : SQL_Latin1General_CP1CI_AS
CatalogCollation              :
MaxSizeBytes                  : 32212254720
Status                        : Online
CreationDate                  : 10/26/2016 4:33:14 PM
CurrentServiceObjectiveId     : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
CurrentServiceObjectiveName   : System2
RequestedServiceObjectiveId   : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
RequestedServiceObjectiveName :
ElasticPoolName               :
EarliestRestoreDate           : 1/1/0001 12:00:00 AM
```

<span data-ttu-id="045ad-143">Waarin u kunt vervolgens controleren toosee hello *Status* van Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="045ad-143">Where you can then check toosee hello *Status* of hello database.</span></span> <span data-ttu-id="045ad-144">In dit geval kunt u zien dat deze database online is.</span><span class="sxs-lookup"><span data-stu-id="045ad-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="045ad-145">Wanneer u deze opdracht uitvoert, ontvangt u een waarde voor de Status van een Online, onderbreken, hervat, schaal en onderbroken.</span><span class="sxs-lookup"><span data-stu-id="045ad-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="045ad-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="045ad-146">Next steps</span></span>
<span data-ttu-id="045ad-147">Zie voor andere beheertaken [Beheeroverzicht][Management overview].</span><span class="sxs-lookup"><span data-stu-id="045ad-147">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/

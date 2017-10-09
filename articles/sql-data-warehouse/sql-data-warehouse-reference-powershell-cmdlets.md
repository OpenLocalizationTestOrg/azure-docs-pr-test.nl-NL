---
title: aaaPowerShell-cmdlets voor Azure SQL Data Warehouse
description: Hallo bovenste PowerShell-cmdlets voor Azure SQL Data Warehouse vinden met inbegrip van hoe toopause en hervatten van een database.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 6f0d5772-f05f-4cc8-9749-4adb153dfd50
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 84353b56131cf856e0724d338d7ed186fd2ceeaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a><span data-ttu-id="ad181-103">PowerShell-cmdlets en REST-API's voor SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ad181-103">PowerShell cmdlets and REST APIs for SQL Data Warehouse</span></span>
<span data-ttu-id="ad181-104">Veel SQL Data Warehouse-beheertaken kunnen worden beheerd met behulp van Azure PowerShell-cmdlets of REST-API's.</span><span class="sxs-lookup"><span data-stu-id="ad181-104">Many SQL Data Warehouse administration tasks can be managed using either Azure PowerShell cmdlets or REST APIs.</span></span>  <span data-ttu-id="ad181-105">Hieronder volgen enkele voorbeelden van hoe toouse PowerShell-tooautomate algemene taken in uw SQL Data Warehouse opdrachten.</span><span class="sxs-lookup"><span data-stu-id="ad181-105">Below are some examples of how toouse PowerShell commands tooautomate common tasks in your SQL Data Warehouse.</span></span>  <span data-ttu-id="ad181-106">Zie voor een goede voorbeelden van de REST Hallo artikel [beheren schaalbaarheid met REST][Manage scalability with REST].</span><span class="sxs-lookup"><span data-stu-id="ad181-106">For some good REST examples, see hello article [Manage scalability with REST][Manage scalability with REST].</span></span>

> [!NOTE]
> <span data-ttu-id="ad181-107">In de volgorde toouse Azure PowerShell gebruiken met SQL Data Warehouse, moet u Azure PowerShell-versie 1.0.3 of hoger.</span><span class="sxs-lookup"><span data-stu-id="ad181-107">In order toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="ad181-108">U kunt uw versie controleren door te voeren **Get-Module - ListAvailable-Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="ad181-108">You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="ad181-109">de meest recente versie Hallo kan worden geïnstalleerd vanaf [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="ad181-109">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="ad181-110">Zie voor meer informatie over het installeren van de meest recente versie Hallo [hoe tooinstall en configureren van Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="ad181-110">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="ad181-111">Aan de slag met Azure PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="ad181-111">Get started with Azure PowerShell cmdlets</span></span>
1. <span data-ttu-id="ad181-112">Open Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad181-112">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="ad181-113">Deze toosign opdrachten uitvoeren in Azure Resource Manager toohello bij Hallo PowerShell-prompt en uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="ad181-113">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a><span data-ttu-id="ad181-114">Voorbeeld van onderbreken SQL datawarehouse</span><span class="sxs-lookup"><span data-stu-id="ad181-114">Pause SQL Data Warehouse Example</span></span>
<span data-ttu-id="ad181-115">Onderbreken van een database met naam 'Database02' gehost op een server met de naam "Server01."</span><span class="sxs-lookup"><span data-stu-id="ad181-115">Pause a database named "Database02" hosted on a server named "Server01."</span></span>  <span data-ttu-id="ad181-116">Hallo-server zich in een Azure-resourcegroep met de naam 'ResourceGroup1'.</span><span class="sxs-lookup"><span data-stu-id="ad181-116">hello server is in an Azure resource group named "ResourceGroup1."</span></span>

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="ad181-117">Een variatie in dit voorbeeld doorgesluisd Hallo opgehaald object te[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="ad181-117">A variation, this example pipes hello retrieved object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span>  <span data-ttu-id="ad181-118">Als gevolg hiervan is Hallo-database onderbroken.</span><span class="sxs-lookup"><span data-stu-id="ad181-118">As a result, hello database is paused.</span></span> <span data-ttu-id="ad181-119">de laatste opdracht Hallo toont Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="ad181-119">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a><span data-ttu-id="ad181-120">Start SQL datawarehouse voorbeeld</span><span class="sxs-lookup"><span data-stu-id="ad181-120">Start SQL Data Warehouse Example</span></span>
<span data-ttu-id="ad181-121">Hervatten van een database met naam 'Database02' gehost op een server met de naam "Server01."</span><span class="sxs-lookup"><span data-stu-id="ad181-121">Resume operation of a database named "Database02" hosted on a server named "Server01."</span></span> <span data-ttu-id="ad181-122">Hallo server deel uitmaakt van een resourcegroep met de naam 'ResourceGroup1'.</span><span class="sxs-lookup"><span data-stu-id="ad181-122">hello server is contained in a resource group named "ResourceGroup1."</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="ad181-123">Een variatie in dit voorbeeld haalt een database met naam 'Database02' van een server met de naam 'Server01' die is opgenomen in een resourcegroep met de naam 'ResourceGroup1'.</span><span class="sxs-lookup"><span data-stu-id="ad181-123">A variation, this example retrieves a database named "Database02" from a server named "Server01" that is contained in a resource group named "ResourceGroup1."</span></span> <span data-ttu-id="ad181-124">Het object Hallo opgehaald te doorgesluisd[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="ad181-124">It pipes hello retrieved object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> <span data-ttu-id="ad181-125">Let op: als uw server foo.database.windows.net, "foo" gebruiken zoals Hallo - servernaam in Hallo PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="ad181-125">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
> 
> 

## <a name="other-supported-powershell-cmdlets"></a><span data-ttu-id="ad181-126">Overige ondersteunde PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="ad181-126">Other supported PowerShell cmdlets</span></span>
<span data-ttu-id="ad181-127">Deze PowerShell-cmdlets worden ondersteund met Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ad181-127">These PowerShell cmdlets are supported with Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="ad181-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="ad181-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="ad181-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span><span class="sxs-lookup"><span data-stu-id="ad181-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span></span>
* <span data-ttu-id="ad181-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span><span class="sxs-lookup"><span data-stu-id="ad181-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span></span>
* <span data-ttu-id="ad181-131">[Nieuwe AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="ad181-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="ad181-132">[Verwijder AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="ad181-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="ad181-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="ad181-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="ad181-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="ad181-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="ad181-135">[SELECT-AzureRmSubscription][Select-AzureRmSubscription]</span><span class="sxs-lookup"><span data-stu-id="ad181-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span></span>
* <span data-ttu-id="ad181-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="ad181-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="ad181-137">[Onderbreken AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="ad181-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad181-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ad181-138">Next steps</span></span>
<span data-ttu-id="ad181-139">Zie voor meer voorbeelden van PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ad181-139">For more PowerShell examples, see:</span></span>

* <span data-ttu-id="ad181-140">[Maken van een SQL Data Warehouse met behulp van PowerShell][Create a SQL Data Warehouse using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="ad181-140">[Create a SQL Data Warehouse using PowerShell][Create a SQL Data Warehouse using PowerShell]</span></span>
* <span data-ttu-id="ad181-141">[Database terugzetten][Database restore]</span><span class="sxs-lookup"><span data-stu-id="ad181-141">[Database restore][Database restore]</span></span>

<span data-ttu-id="ad181-142">Zie voor andere taken die kunnen worden geautomatiseerd met PowerShell [Azure SQL Database-Cmdlets][Azure SQL Database Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="ad181-142">For other tasks which can be automated with PowerShell, see [Azure SQL Database Cmdlets][Azure SQL Database Cmdlets].</span></span> <span data-ttu-id="ad181-143">Houd er rekening mee dat niet alle Azure SQL Database-cmdlets voor Azure SQL Data Warehouse worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ad181-143">Note that not all Azure SQL Database cmdlets are supported for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="ad181-144">Zie voor een lijst van taken die kan worden geautomatiseerd met REST [bewerkingen voor Azure SQL-Databases][Operations for Azure SQL Databases].</span><span class="sxs-lookup"><span data-stu-id="ad181-144">For a list of tasks which can be automated with REST, see [Operations for Azure SQL Databases][Operations for Azure SQL Databases].</span></span>

<!--Image references-->

<!--Article references-->
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Create a SQL Data Warehouse using PowerShell]: ./sql-data-warehouse-get-started-provision-powershell.md
[Database restore]: ./sql-data-warehouse-restore-database-powershell.md
[Manage scalability with REST]: ./sql-data-warehouse-manage-compute-rest-api.md

<!--MSDN references-->
[Azure SQL Database Cmdlets]: https://msdn.microsoft.com/library/mt574084.aspx
[Operations for Azure SQL Databases]: https://msdn.microsoft.com/library/azure/dn505719.aspx
[Get-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt603648.aspx
[Get-AzureRmSqlDeletedDatabaseBackup]: https://msdn.microsoft.com/library/mt693387.aspx
[Get-AzureRmSqlDatabaseRestorePoints]: https://msdn.microsoft.com/library/mt603642.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Remove-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619368.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
<!-- It appears that Select-AzureRmSubscription isn't documented, so this points tooSelect-AzureSubscription -->
[Select-AzureRmSubscription]: https://msdn.microsoft.com/library/dn722499.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps

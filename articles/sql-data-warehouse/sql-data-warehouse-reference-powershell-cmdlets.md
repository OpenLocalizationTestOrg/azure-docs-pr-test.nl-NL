---
title: PowerShell-cmdlets voor Azure SQL Data Warehouse
description: De bovenste PowerShell-cmdlets voor Azure SQL Data Warehouse, inclusief het onderbreken en hervatten van een database niet vinden.
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
ms.openlocfilehash: ce3e11587c2e0cb92923868a4f26d7f59c7ef4ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a><span data-ttu-id="1e29b-103">PowerShell-cmdlets en REST-API's voor SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1e29b-103">PowerShell cmdlets and REST APIs for SQL Data Warehouse</span></span>
<span data-ttu-id="1e29b-104">Veel SQL Data Warehouse-beheertaken kunnen worden beheerd met behulp van Azure PowerShell-cmdlets of REST-API's.</span><span class="sxs-lookup"><span data-stu-id="1e29b-104">Many SQL Data Warehouse administration tasks can be managed using either Azure PowerShell cmdlets or REST APIs.</span></span>  <span data-ttu-id="1e29b-105">Hieronder volgen enkele voorbeelden van het PowerShell-opdrachten gebruiken voor het automatiseren van algemene taken in uw SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1e29b-105">Below are some examples of how to use PowerShell commands to automate common tasks in your SQL Data Warehouse.</span></span>  <span data-ttu-id="1e29b-106">Zie het artikel voor een goede voorbeelden van de REST [beheren schaalbaarheid met REST][Manage scalability with REST].</span><span class="sxs-lookup"><span data-stu-id="1e29b-106">For some good REST examples, see the article [Manage scalability with REST][Manage scalability with REST].</span></span>

> [!NOTE]
> <span data-ttu-id="1e29b-107">Om Azure PowerShell gebruiken met SQL Data Warehouse, moet u Azure PowerShell-versie 1.0.3 of hoger.</span><span class="sxs-lookup"><span data-stu-id="1e29b-107">In order to use Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="1e29b-108">U kunt uw versie controleren door te voeren **Get-Module - ListAvailable-Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="1e29b-108">You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="1e29b-109">De meest recente versie kan worden geïnstalleerd vanaf [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="1e29b-109">The latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="1e29b-110">Zie [Azure PowerShell installeren en configureren][How to install and configure Azure PowerShell] voor meer informatie over het installeren van de meest recente versie.</span><span class="sxs-lookup"><span data-stu-id="1e29b-110">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="1e29b-111">Aan de slag met Azure PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="1e29b-111">Get started with Azure PowerShell cmdlets</span></span>
1. <span data-ttu-id="1e29b-112">Open Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e29b-112">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="1e29b-113">Voer deze opdrachten aanmelden in de Azure Resource Manager en selecteer uw abonnement op de PowerShell-prompt.</span><span class="sxs-lookup"><span data-stu-id="1e29b-113">At the PowerShell prompt, run these commands to sign in to the Azure Resource Manager and select your subscription.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a><span data-ttu-id="1e29b-114">Voorbeeld van onderbreken SQL datawarehouse</span><span class="sxs-lookup"><span data-stu-id="1e29b-114">Pause SQL Data Warehouse Example</span></span>
<span data-ttu-id="1e29b-115">Onderbreken van een database met naam 'Database02' gehost op een server met de naam "Server01."</span><span class="sxs-lookup"><span data-stu-id="1e29b-115">Pause a database named "Database02" hosted on a server named "Server01."</span></span>  <span data-ttu-id="1e29b-116">De server zich in een Azure-resourcegroep met de naam 'ResourceGroup1'.</span><span class="sxs-lookup"><span data-stu-id="1e29b-116">The server is in an Azure resource group named "ResourceGroup1."</span></span>

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="1e29b-117">Een variatie in dit voorbeeld doorgesluisd het opgehaalde object [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="1e29b-117">A variation, this example pipes the retrieved object to [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span>  <span data-ttu-id="1e29b-118">Als gevolg hiervan is de database is onderbroken.</span><span class="sxs-lookup"><span data-stu-id="1e29b-118">As a result, the database is paused.</span></span> <span data-ttu-id="1e29b-119">De laatste opdracht toont de resultaten.</span><span class="sxs-lookup"><span data-stu-id="1e29b-119">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a><span data-ttu-id="1e29b-120">Start SQL datawarehouse voorbeeld</span><span class="sxs-lookup"><span data-stu-id="1e29b-120">Start SQL Data Warehouse Example</span></span>
<span data-ttu-id="1e29b-121">Hervatten van een database met naam 'Database02' gehost op een server met de naam "Server01."</span><span class="sxs-lookup"><span data-stu-id="1e29b-121">Resume operation of a database named "Database02" hosted on a server named "Server01."</span></span> <span data-ttu-id="1e29b-122">De server deel uitmaakt van een resourcegroep met de naam 'ResourceGroup1'.</span><span class="sxs-lookup"><span data-stu-id="1e29b-122">The server is contained in a resource group named "ResourceGroup1."</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="1e29b-123">Een variatie in dit voorbeeld haalt een database met naam 'Database02' van een server met de naam 'Server01' die is opgenomen in een resourcegroep met de naam 'ResourceGroup1'.</span><span class="sxs-lookup"><span data-stu-id="1e29b-123">A variation, this example retrieves a database named "Database02" from a server named "Server01" that is contained in a resource group named "ResourceGroup1."</span></span> <span data-ttu-id="1e29b-124">Deze het opgehaalde object doorgesluisd [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="1e29b-124">It pipes the retrieved object to [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> <span data-ttu-id="1e29b-125">Let op: als uw server foo.database.windows.net, is "foo" als - servernaam in de PowerShell-cmdlets gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1e29b-125">Note that if your server is foo.database.windows.net, use "foo" as the -ServerName in the PowerShell cmdlets.</span></span>
> 
> 

## <a name="other-supported-powershell-cmdlets"></a><span data-ttu-id="1e29b-126">Overige ondersteunde PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="1e29b-126">Other supported PowerShell cmdlets</span></span>
<span data-ttu-id="1e29b-127">Deze PowerShell-cmdlets worden ondersteund met Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1e29b-127">These PowerShell cmdlets are supported with Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="1e29b-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1e29b-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1e29b-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span><span class="sxs-lookup"><span data-stu-id="1e29b-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span></span>
* <span data-ttu-id="1e29b-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span><span class="sxs-lookup"><span data-stu-id="1e29b-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span></span>
* <span data-ttu-id="1e29b-131">[Nieuwe AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1e29b-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1e29b-132">[Verwijder AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1e29b-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1e29b-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1e29b-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1e29b-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1e29b-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1e29b-135">[SELECT-AzureRmSubscription][Select-AzureRmSubscription]</span><span class="sxs-lookup"><span data-stu-id="1e29b-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span></span>
* <span data-ttu-id="1e29b-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1e29b-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1e29b-137">[Onderbreken AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1e29b-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e29b-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1e29b-138">Next steps</span></span>
<span data-ttu-id="1e29b-139">Zie voor meer voorbeelden van PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1e29b-139">For more PowerShell examples, see:</span></span>

* <span data-ttu-id="1e29b-140">[Maken van een SQL Data Warehouse met behulp van PowerShell][Create a SQL Data Warehouse using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="1e29b-140">[Create a SQL Data Warehouse using PowerShell][Create a SQL Data Warehouse using PowerShell]</span></span>
* <span data-ttu-id="1e29b-141">[Database terugzetten][Database restore]</span><span class="sxs-lookup"><span data-stu-id="1e29b-141">[Database restore][Database restore]</span></span>

<span data-ttu-id="1e29b-142">Zie voor andere taken die kunnen worden geautomatiseerd met PowerShell [Azure SQL Database-Cmdlets][Azure SQL Database Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="1e29b-142">For other tasks which can be automated with PowerShell, see [Azure SQL Database Cmdlets][Azure SQL Database Cmdlets].</span></span> <span data-ttu-id="1e29b-143">Houd er rekening mee dat niet alle Azure SQL Database-cmdlets voor Azure SQL Data Warehouse worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="1e29b-143">Note that not all Azure SQL Database cmdlets are supported for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="1e29b-144">Zie voor een lijst van taken die kan worden geautomatiseerd met REST [bewerkingen voor Azure SQL-Databases][Operations for Azure SQL Databases].</span><span class="sxs-lookup"><span data-stu-id="1e29b-144">For a list of tasks which can be automated with REST, see [Operations for Azure SQL Databases][Operations for Azure SQL Databases].</span></span>

<!--Image references-->

<!--Article references-->
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
<!-- It appears that Select-AzureRmSubscription isn't documented, so this points to Select-AzureSubscription -->
[Select-AzureRmSubscription]: https://msdn.microsoft.com/library/dn722499.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps

---
title: aaaHow toouninstall elastische database taken hulpprogramma
description: Hoe toouninstall Hallo taken hulpprogramma voor de elastische database
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 3bc1e889d5042bc3eaa9fd9da89816737e0b8df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="ddbde-103">Elastische Database taken onderdelen verwijderen</span><span class="sxs-lookup"><span data-stu-id="ddbde-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="ddbde-104">**Elastische Database taken** onderdelen kunnen worden verwijderd met behulp van Hallo Portal of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ddbde-104">**Elastic Database jobs** components can be uninstalled using either hello Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a><span data-ttu-id="ddbde-105">Elastische taken databaseonderdelen met hello Azure-portal verwijderen</span><span class="sxs-lookup"><span data-stu-id="ddbde-105">Uninstall Elastic Database jobs components using hello Azure portal</span></span>
1. <span data-ttu-id="ddbde-106">Open Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ddbde-106">Open hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ddbde-107">Navigeer toohello-abonnement met **elastische Database taken** onderdelen, namelijk Hallo abonnement in welke elastische Database taken onderdelen zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ddbde-107">Navigate toohello subscription that contains **Elastic Database jobs** components, namely hello subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="ddbde-108">Klik op **Bladeren** en klik op **resourcegroepen**.</span><span class="sxs-lookup"><span data-stu-id="ddbde-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="ddbde-109">Selecteer Hallo-resourcegroep met de naam '__ElasticDatabaseJob'.</span><span class="sxs-lookup"><span data-stu-id="ddbde-109">Select hello resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="ddbde-110">Hallo-resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ddbde-110">Delete hello resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="ddbde-111">Elastische taken databaseonderdelen met behulp van PowerShell verwijderen</span><span class="sxs-lookup"><span data-stu-id="ddbde-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="ddbde-112">Start een Microsoft Azure PowerShell-opdrachtvenster en navigeer toohello extra submap onder de map Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x Hallo: Type **cd extra**.</span><span class="sxs-lookup"><span data-stu-id="ddbde-112">Launch a Microsoft Azure PowerShell command window and navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="ddbde-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x* > cd-hulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="ddbde-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="ddbde-114">Hallo.\UninstallElasticDatabaseJobs.ps1 PowerShell-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ddbde-114">Execute hello .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="ddbde-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools > deblokkeren bestand.\UninstallElasticDatabaseJobs.ps1 PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools >.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="ddbde-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="ddbde-116">Of gewoon uitvoeren Hallo script volgen, ervan uitgaande dat standaard waarden waar gebruikt op de installatie van Hallo-onderdelen:</span><span class="sxs-lookup"><span data-stu-id="ddbde-116">Or simply, execute hello following script, assuming default values where used on installation of hello components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "hello Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing hello Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing hello Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="ddbde-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ddbde-117">Next steps</span></span>
<span data-ttu-id="ddbde-118">taken van de elastische Database toore installeren, Zie [Hallo elastische Database taak service installeren](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="ddbde-118">toore-install Elastic Database jobs, see [Installing hello Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="ddbde-119">Zie voor een overzicht van de elastische Database taken [elastische Database taken overzicht](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ddbde-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->



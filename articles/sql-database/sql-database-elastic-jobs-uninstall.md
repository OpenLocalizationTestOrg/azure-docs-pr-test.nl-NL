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
# <a name="uninstall-elastic-database-jobs-components"></a>Elastische Database taken onderdelen verwijderen
**Elastische Database taken** onderdelen kunnen worden verwijderd met behulp van Hallo Portal of PowerShell.

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a>Elastische taken databaseonderdelen met hello Azure-portal verwijderen
1. Open Hallo [Azure-portal](https://portal.azure.com/).
2. Navigeer toohello-abonnement met **elastische Database taken** onderdelen, namelijk Hallo abonnement in welke elastische Database taken onderdelen zijn geïnstalleerd.
3. Klik op **Bladeren** en klik op **resourcegroepen**.
4. Selecteer Hallo-resourcegroep met de naam '__ElasticDatabaseJob'.
5. Hallo-resourcegroep verwijderen.

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a>Elastische taken databaseonderdelen met behulp van PowerShell verwijderen
1. Start een Microsoft Azure PowerShell-opdrachtvenster en navigeer toohello extra submap onder de map Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x Hallo: Type **cd extra**.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x* > cd-hulpprogramma's
2. Hallo.\UninstallElasticDatabaseJobs.ps1 PowerShell-script uitvoeren.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools > deblokkeren bestand.\UninstallElasticDatabaseJobs.ps1 PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools >.\UninstallElasticDatabaseJobs.ps1

Of gewoon uitvoeren Hallo script volgen, ervan uitgaande dat standaard waarden waar gebruikt op de installatie van Hallo-onderdelen:

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

## <a name="next-steps"></a>Volgende stappen
taken van de elastische Database toore installeren, Zie [Hallo elastische Database taak service installeren](sql-database-elastic-jobs-service-installation.md)

Zie voor een overzicht van de elastische Database taken [elastische Database taken overzicht](sql-database-elastic-jobs-overview.md).

<!--Image references-->



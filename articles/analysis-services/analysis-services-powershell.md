---
title: aaaManage Azure Analysis Services met PowerShell | Microsoft Docs
description: Azure Analysis Services-beheer met PowerShell.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: owend
ms.openlocfilehash: bc4250bf77b5a0d86c1049ee57493bcf2a1f0c1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-analysis-services-with-powershell"></a>Azure analyseservices met PowerShell beheren

In dit artikel beschrijft de PowerShell-cmdlets gebruikt tooperform Azure Analysis Services-server en database beheertaken. 

Server-beheertaken zoals maken of verwijderen van een server, onderbreken of hervatten van serverbewerkingen of Hallo serviceniveau (laag) wijzigt cmdlets van Azure Resource Manager (AzureRM) gebruiken. Andere taken voor het beheren van databases, zoals het toevoegen of verwijderen van leden van een rol, verwerking of partitioneren gebruiken-cmdlets die zijn opgenomen in Hallo dezelfde SQL Server-module als SQL Server Analysis Services.

## <a name="permissions"></a>Machtigingen
De meeste PowerShell taken moet dat u beheerdersbevoegdheden hebben op Hallo Analysis Services server die u beheert. Geplande taken van PowerShell zijn zonder toezicht bewerkingen. Hallo-account met Hallo scheduler moet beheerdersbevoegdheden hebben op Hallo Analysis Services-server. 

Serverbewerkingen met behulp van cmdlets AzureRm, uw account of met scheduler Hallo-account moet ook deel uitmaken van rol van eigenaar toohello voor Hallo resource in [gebaseerd toegangsbeheer (RBAC)](../active-directory/role-based-access-control-what-is.md). 

## <a name="server-operations"></a>Bewerkingen van server 
Azure Analysis Services-cmdlets zijn opgenomen in Hallo [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) onderdeel module. Zie tooinstall AzureRM cmdlet-modules [Azure Resource Manager-cmdlets](/powershell/azure/overview) in PowerShell Gallery Hallo.

|Cmdlet|Beschrijving| 
|------------|-----------------| 
|[Export AzureAnalysisServicesInstance](/powershell/module/azurerm.analysisservices/export-azureanalysisservicesinstancelog)|Uitvoer Meld toofile.| 
|[Get-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/get-azurermanalysisservicesserver)|Details van een server-exemplaar wordt opgehaald.|  
|[Nieuwe AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)|Hiermee maakt u een server-exemplaar.|
|[Verwijder AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/remove-azurermanalysisservicesserver)|Hiermee verwijdert u een server-exemplaar.|  
|[Onderbreken AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/suspend-azurermanalysisservicesserver)|Een server-exemplaar onderbreekt.| 
|[Resume-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/resume-azurermanalysisservicesserver)|Hervatten van een server-exemplaar.|  
|[Set-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/set-azurermanalysisservicesserver)|Hiermee wijzigt u een server-exemplaar.|   
|[Test AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/test-azurermanalysisservicesserver)|Tests Hallo bestaan van een server-exemplaar.| 

## <a name="database-operations"></a>Databasebewerkingen

Azure Analysis Services databasebewerkingen gebruiken dezelfde Hallo [SqlServer](https://www.powershellgallery.com/packages/SqlServer) module als SQL Server Analysis Services. Niet alle cmdlets worden echter ondersteund voor Azure Analysis Services. 

Hallo SqlServer module biedt taakspecifieke database management-cmdlets als alsmede Hallo algemeen Invoke ASCmd cmdlet die een Tabellair Model Scripting Language (TMSL) accepteert een query of script. Hallo worden volgende Hallo SqlServer module-cmdlets ondersteund voor Azure Analysis Services.

  
|Cmdlet|Beschrijving|
|------------|-----------------| 
|[Voeg RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Toevoegen van een lid tooa-databaserol.| 
|[Back-up ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet)|Back-up van een Analysis Services-database.|  
|[Verwijder RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|Een lid verwijderen uit een databaserol.|   
|[Aanroepen ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|Een script TMSL uitvoeren.|
|[Aanroepen ProcessASDatabase](https://msdn.microsoft.com/library/mt651773.aspx)|Verwerken van een database.|  
|[Aanroepen ProcessPartition](https://msdn.microsoft.com/library/hh510164.aspx)|Verwerken van een partitie.| 
|[Aanroepen ProcessTable](https://msdn.microsoft.com/library/mt651774.aspx)|Verwerken van een tabel.|  
|[Samenvoegen partitie](https://msdn.microsoft.com/library/hh479576.aspx)|Samenvoegen van een partitie.|  
|[Restore ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet)|Een Analysis Services-database herstellen.| 
  

## <a name="related-information"></a>Gerelateerde informatie

* [SQL Server PowerShell-Module downloaden](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [Downloaden van SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   
* [SQL Server-module in PowerShell Gallery](https://www.powershellgallery.com/packages/SqlServer)    
* [Tabellaire Model wilt programmeren voor compatibiliteit niveau 1200 of hoger](https://msdn.microsoft.com/library/mt712541.aspx)

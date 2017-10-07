---
title: een Azure Analysis Services-server met behulp van PowerShell aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een Azure Analysis Services-server met behulp van PowerShell
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a>Een Azure Analysis Services-server maken met behulp van PowerShell

Deze snelstartgids wordt beschreven met behulp van PowerShell van Hallo opdrachtregel toocreate een Azure Analysis Services-server in een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) in uw Azure-abonnement.

Voor deze taak is Azure PowerShell-moduleversie 4.0 of hoger vereist. toofind hello versie, voer ` Get-Module -ListAvailable AzureRM`. tooinstall upgraden, raadpleegt u [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps). 

> [!NOTE]
> Het maken van een server kan zorgen voor een nieuwe factureerbare service. toolearn meer, Zie [Analysis Services-prijzen](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="prerequisites"></a>Vereisten
toocomplete deze snelstartgids die u nodig:

* **Azure-abonnement**: Ga naar [gratis proefversie van Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate een account.
* **Azure Active Directory**: uw abonnement moet worden gekoppeld aan een Azure Active Directory-tenant en u moet een account hebben in de betreffende map. toolearn meer, Zie [verificatie en gebruikersmachtigingen](analysis-services-manage-users.md).

## <a name="import-azurermanalysisservices-module"></a>AzureRm.AnalysisServices-module importeren
een server in uw abonnement toocreate, gebruikt u Hallo [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) onderdeel module. Hallo AzureRm.AnalysisServices module in uw PowerShell-sessie laden.

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a>Meld u aan tooAzure

Azure-abonnement tooyour aanmelden via Hallo [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) opdracht. Volg Hallo op het scherm-instructies.

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Een resourcegroep maken
 
Een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) is een logische container waarin Azure-resources worden geïmplementeerd en als groep beheerd. Wanneer u de server maakt, moet u een resourcegroep opgeven in uw abonnement. Als u nog geen een resourcegroep, kunt u een nieuwe met behulp van Hallo [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) opdracht. Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in de regio VS-West Hallo.

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a>Een server maken

Maak een nieuwe server met behulp van Hallo [nieuw AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) opdracht. Hallo volgende voorbeeld maakt u een server met de naam MijnServer in myResourceGroup in Hallo VS-West regio op Hallo D1 laag, en geeft philipc@adventureworks.com als serverbeheerder.

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a>Resources opschonen

U kunt Hallo server verwijderen uit uw abonnement via Hallo [verwijderen AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) opdracht. Verwijder de server niet als u met andere snelstartgidsen en zelfstudies in deze verzameling doorgaat. Hallo verwijdert volgende voorbeeld Hallo-server in de vorige stap Hallo gemaakt.


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a>Volgende stappen
[Azure Analysis Services beheren met PowerShell](analysis-services-powershell.md)   
[Een model implementeren vanuit SSDT](analysis-services-deploy.md)   
[Een model maken in Azure Portal](analysis-services-create-model-portal.md)
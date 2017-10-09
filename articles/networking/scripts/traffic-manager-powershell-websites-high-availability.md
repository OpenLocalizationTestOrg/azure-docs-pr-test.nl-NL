---
title: aaaAzure PowerShell-voorbeeldscript - routeverkeer voor hoge beschikbaarheid van toepassingen | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - routeverkeer voor hoge beschikbaarheid van toepassingen
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: georgewallace
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 11d15780403b4ed79e85d7b3495bc5d674bfdaee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a>Verkeer leiden voor hoge beschikbaarheid van toepassingen

Dit script maakt een resourcegroep, twee app-serviceabonnementen, twee web-apps, een traffic manager-profiel en twee traffic manager-eindpunten. Traffic Manager stuurt verkeer toohello toepassing in één regio bevinden als de primaire regio Hallo en de secundaire regio toohello wanneer Hallo-toepassing in Hallo primaire regio niet beschikbaar is. Voordat u Hallo script wordt uitgevoerd, moet u Hallo MyWebApp, MyWebAppL1 en MyWebAppL2 waarden toounique waarden in Azure. Na het uitvoeren van script hello, kunt u in de primaire regio Hallo met Hallo URL mywebapp.trafficmanager.net Hallo app openen.

Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]


Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt Hallo opdrachten toocreate een resourcegroep, web-app, traffic manager-profiel te volgen en alle bijbehorende resources. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [Nieuwe AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [Nieuwe AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Hiermee maakt u een App Service-abonnement. Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app. |
| [Nieuwe AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Hiermee maakt u een Azure-web-app in het Hallo-App Service-abonnement. |
| [Set-AzureRmResource](/powershell/module/azurerm.resources/new-azurermresource) | Hiermee maakt u een Azure-web-app in het Hallo-App Service-abonnement. |
| [Nieuwe AzureRmTrafficManagerProfile](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | Een Azure Traffic Manager-profiel maakt. |
| [Nieuwe AzureRmTrafficManagerEndpoint](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | Voegt een eindpunt tooan Azure Traffic Manager-profiel. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Aanvullende voorbeelden voor netwerken PowerShell-script kunnen worden gevonden in Hallo [overzicht van Azure-netwerken documentatie](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).

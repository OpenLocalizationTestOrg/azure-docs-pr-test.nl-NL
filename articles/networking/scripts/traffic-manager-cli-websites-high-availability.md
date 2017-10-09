---
title: aaaAzure voorbeeldscript CLI - routeverkeer voor hoge beschikbaarheid van toepassingen | Microsoft Docs
description: Azure CLI-voorbeeldscript - routeverkeer voor hoge beschikbaarheid van toepassingen
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a>Verkeer leiden voor hoge beschikbaarheid van toepassingen

Dit script maakt een resourcegroep, twee app-serviceabonnementen, twee web-apps, een traffic manager-profiel en twee traffic manager-eindpunten. Traffic Manager stuurt verkeer toohello toepassing in één regio bevinden als de primaire regio Hallo en de secundaire regio toohello wanneer Hallo-toepassing in Hallo primaire regio niet beschikbaar is. Voordat u Hallo script wordt uitgevoerd, moet u Hallo MyWebApp, MyWebAppL1 en MyWebAppL2 waarden toounique waarden in Azure. Na het uitvoeren van script hello, kunt u in de primaire regio Hallo met Hallo URL mywebapp.trafficmanager.net Hallo app openen.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Na het uitvoeren van het voorbeeldscript Hallo is Hallo Volg opdracht gebruikte tooremove Hallo-resourcegroep, App Service-app en alle gerelateerde resources.

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt Hallo opdrachten toocreate een resourcegroep, web-app, traffic manager-profiel te volgen en alle bijbehorende resources. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ appservice-abonnement maken](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Hiermee maakt u een App Service-abonnement. Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app. |
| [AZ appservice web maken](https://docs.microsoft.com/cli/azure/appservice/web#create) | Hiermee maakt u een Azure-web-app in het Hallo-App Service-abonnement. |
| [AZ netwerk traffic manager-profiel maken](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | Een Azure Traffic Manager-profiel maakt. |
| [netwerkeindpunt voor het traffic manager AZ maken](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | Voegt een eindpunt tooan Azure Traffic Manager-profiel. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [documentatie Azure Networking](../cli-samples.md).

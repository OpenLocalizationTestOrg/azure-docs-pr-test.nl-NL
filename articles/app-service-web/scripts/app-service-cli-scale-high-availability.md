---
title: aaaAzure voorbeeldscript CLI - schalen een web-app wereldwijd een hoge availabilty-architectuur | Microsoft Docs
description: Azure CLI-voorbeeldscript - schaal een web-app wereldwijd een hoge availabilty-architectuur
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4033a50-0e05-4505-8ce8-c876204b2acc
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b72fbccd7f2aaab58e4b4721e14dca14146c7c72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a>Schalen van een web-app wereldwijd een hoge beschikbaarheid-architectuur

In dit scenario maakt u een resourcegroep, twee app-serviceabonnementen, twee web-apps, een traffic manager-profiel en twee traffic manager-eindpunten. Zodra de Hallo oefening is voltooid hebt u een hoog beschikbare architectuur waarmee biedt globale beschikbaarheid van uw web-app op basis van de laagste netwerklatentie Hallo.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 


## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt Hallo opdrachten toocreate een resourcegroep, web-app, traffic manager-profiel te volgen en alle bijbehorende resources. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ appservice-abonnement maken](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Hiermee maakt u een App Service-abonnement. Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app. |
| [AZ webapp maken](https://docs.microsoft.com/cli/azure/webapp#create) | Hiermee maakt u een Azure-web-app. |
| [AZ netwerk traffic manager-profiel maken](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | Een Azure Traffic Manager-profiel maakt. |
| [netwerkeindpunt voor het traffic manager AZ maken](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | Voegt een eindpunt tooan Azure Traffic Manager-profiel. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie](../app-service-cli-samples.md).

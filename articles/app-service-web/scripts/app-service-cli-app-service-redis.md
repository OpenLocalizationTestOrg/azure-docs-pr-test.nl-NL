---
title: aaaAzure voorbeeldscript CLI - verbinding maken met een web-app tooa redis-cache | Microsoft Docs
description: Azure CLI-Script steekproef - verbinding maken met een web-app tooa redis-cache
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b911e6643591b8f07aeb64d4d62876c0fa156a8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-redis-cache"></a>Verbinding maken met een web-app tooa redis-cache

In dit scenario leert u hoe toocreate een Azure redis-cache en een Azure-web-app. Vervolgens koppelt u Hallo redis-cache toohello web-app met app-instellingen.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep of web-app redis-cache en alle bijbehorende resources te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ appservice-abonnement maken](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Hiermee maakt u een App Service-abonnement. Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app. |
| [AZ webapp maken](https://docs.microsoft.com/cli/azure/webapp#create) | Hiermee maakt u een Azure-web-app. |
| [AZ redis maken](https://docs.microsoft.com/en-us/cli/azure/redis#create) | Nieuwe Redis-Cache-exemplaar maken. Dit is het Hallo-gegevens worden opgeslagen. |
| [AZ redis lijst-sleutels](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | Hallo toegangstoetsen voor redis-cache-exemplaar Hallo bevat. |
| [AZ webapp config appsettings instellen](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | Maken of bijwerken van een app-instelling voor een Azure-web-app. App-instellingen worden weergegeven als omgevingsvariabelen voor uw app. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie](../app-service-cli-samples.md).

---
title: 'Azure CLI-Script voorbeeld: een web-app maken met de implementatie van GitHub | Microsoft Docs'
description: 'Azure CLI-Script voorbeeld: een web-app maken met de implementatie van GitHub'
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0205c991-0989-4ca3-bb41-237dcc964460
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: sample
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 61e9d65319cecf3ea4e9152ebdf1035566aad74c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a>Een web-app maken met de implementatie van GitHub

Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en implementeert vervolgens uw web-app-code uit een openbare GitHub-opslagplaats (zonder continue implementatie). Zie voor een implementatie met continue implementatie van GitHub [een WebApp maken met continue implementatie van GitHub](app-service-cli-continuous-deployment-github.md).

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger. Voer `az --version` uit om de versie te bekijken. Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "een web-app maken met de implementatie van GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Script uitleg 

Dit script maakt gebruik van de volgende opdrachten. Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ appservice-abonnement maken](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Hiermee maakt u een App Service-abonnement. |
| [AZ webapp maken](https://docs.microsoft.com/cli/azure/webapp#create) | Hiermee maakt u een Azure-web-app. |
| [AZ webapp implementatieconfiguratie bron](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | Een Azure-web-app koppelt aan een opslagplaats Git of volgt. |
| [AZ webapp bladeren](https://docs.microsoft.com/cli/azure/webapp#browse) | Een Azure-web-app in een browser openen. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).

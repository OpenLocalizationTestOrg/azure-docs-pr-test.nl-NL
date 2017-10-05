---
title: Azure CLI-voorbeeldscript - web-app maken en implementeren van code in een testomgeving | Microsoft Docs
description: Azure CLI-voorbeeldscript - web-app maken en implementeren van code in een testomgeving
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 2b995dcd-e471-4355-9fda-00babcdb156e
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d586b50258c32e44f55859aad0a89475e9e4d2eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a>Een web-app maken en implementeren van code in een testomgeving

Dit voorbeeldscript maakt u een web-app in App Service met een extra implementatiesleuf naam 'staging', en implementeert u een voorbeeld-app in de sleuf 'staging'.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger. Voer `az --version` uit om de versie te bekijken. Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "een web-app maken en implementeren van code in een testomgeving")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van de volgende opdrachten. Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ appservice-abonnement maken](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Hiermee maakt u een App Service-abonnement. |
| [AZ webapp maken](https://docs.microsoft.com/cli/azure/webapp#create) | Hiermee maakt u een Azure-web-app. |
| [AZ webapp implementatiesleuf maken](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | Een implementatiesleuf te maken. |
| [AZ webapp implementatieconfiguratie bron](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | Een Azure-web-app koppelt aan een opslagplaats Git of volgt. |
| [AZ webapp bladeren](https://docs.microsoft.com/cli/azure/webapp#browse) | Een Azure-web-app in een browser openen. |
| [AZ webapp implementatiesleuf wisselen](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | Een opgegeven implementatiesleuf wisselen naar de productie. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).

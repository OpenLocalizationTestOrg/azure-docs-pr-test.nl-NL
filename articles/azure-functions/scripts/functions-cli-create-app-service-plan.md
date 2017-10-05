---
title: 'Azure CLI-Script voorbeeld: een functie-App maken in App Service-abonnement | Microsoft Docs'
description: 'Azure CLI-Script voorbeeld: een functie-App maken in App Service-abonnement'
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 40c3fa6fa6c07d59e4bf55531e116ba50aa92b91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a>Een functie-App maken in App Service-abonnement

Dit voorbeeldscript wordt gemaakt van een functie-App van Azure, dat een container voor uw functies is. De functie-App is gemaakt met behulp van een specifieke App Service-abonnement, wat betekent dat uw serverbronnen steeds zijn dat ingeschakeld.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger. Voer `az --version` uit om de versie te bekijken. Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Voorbeeld van een script

Dit script maakt een Azure-functie-app met een speciaal [App Service-abonnement](../functions-scale.md#app-service-plan).

[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "een Azure-functie op een App Service-abonnement maken")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Script uitleg

Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht. Dit script maakt gebruik van de volgende opdrachten:

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ storage-account maken](https://docs.microsoft.com/cli/azure/storage/account#create) | Een Azure Storage-account maakt. |
| [AZ appservice-abonnement maken](https://docs.microsoft.com/cli/azure/appserviceplan#create) | Hiermee maakt u een App Service-abonnement. |
| [AZ functionapp maken](https://docs.microsoft.com/cli/azure/functionapp#delete) | Hiermee maakt u een Azure-functie-app. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende voorbeelden van Azure Functions CLI-script kunnen worden gevonden in de [documentatie van Azure Functions](../functions-cli-samples.md).

---
title: aaaCreate een functie-App en functiecode van Visual Studio Team Services implementeren | Microsoft Docs
description: Een functie-App maken en implementeren van de functiecode van Visual Studio Team Services
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/28/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 774bee73025cc9ac46f8b2a6c10edbfa3c2d353b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a>Maak een App Service

In dit scenario wordt beschreven hoe een functie-app met toocreate Hallo [verbruik plan](../functions-scale.md#consumption-plan) met de bijbehorende resources en continu implementeert uw functiecode uit de opslagplaats van een Visual Studio Team Services (VSTS). In dit voorbeeld hebt u het volgende nodig:

* Een opslagplaats VSTS met functies code, die u hebt beheerdersbevoegdheden nodig voor.
* Een [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) voor uw GitHub-account.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Voorbeeld van een script

Dit voorbeeld maakt u een Azure-functie-app en functiecode van Visual Studio Team Services implementeert.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, web-app, documentdb en alle gerelateerde resources te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ storage-account maken](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Hiermee maakt u een App Service-abonnement. |
| [AZ functionapp maken](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [AZ appservice webconfiguratie bronbeheer](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | Een functie-app koppelt aan een Git of volgt opslagplaats. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende voorbeelden van Azure Functions CLI script kunnen u vinden in Hallo [documentatie van Azure Functions](../functions-cli-samples.md).

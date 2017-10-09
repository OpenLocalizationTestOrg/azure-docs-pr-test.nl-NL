---
title: aaaCreate een functie-App en functiecode vanuit GitHub implementeren | Microsoft Docs
description: Azure CLI-voorbeeldscript - een functie-App maken en implementeren van functiecode vanuit GitHub
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 026886f11909149db695d9a52d0aa37f109f64e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a>Een functie-app maken en implementeren van functiecode vanuit GitHub

Dit voorbeeldscript wordt gemaakt van een functie-app met behulp van Hallo [verbruik plan](../functions-scale.md#consumption-plan) met de bijbehorende resources en de functiecode uit een openbare GitHub-opslagplaats (zonder continue implementatie) implementeert. Lees voor continue levering van functiecode vanuit GitHub, [maken van een functie-app en continu implementeren vanuit GitHub](functions-cli-create-function-app-github-continuous.md)

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Voorbeeld van een script

Dit voorbeeld maakt u een Azure-functie-app en implementeert functiecode vanuit GitHub.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Script uitleg

Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie. Dit script maakt gebruik van Hallo volgende opdrachten:

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ storage-account maken](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Hiermee maakt u een App Service-abonnement. |
| [AZ functionapp maken](https://docs.microsoft.com/cli/azure/appservice/web#delete) | Hiermee maakt u een Azure-functie-app. |
| [AZ appservice webconfiguratie bronbeheer](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | Een functie-app koppelt aan een Git of volgt opslagplaats. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende voorbeelden van Azure Functions CLI script kunnen u vinden in Hallo [documentatie van Azure Functions](../functions-cli-samples.md).

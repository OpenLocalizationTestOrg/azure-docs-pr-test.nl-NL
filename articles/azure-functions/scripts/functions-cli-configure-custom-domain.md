---
title: aaaAzure voorbeeldscript CLI - toewijzen een aangepast domein tooa functie-app | Microsoft Docs
description: 'Azure CLI - voorbeeldscript: de toewijzing van een aangepast domein tooa functie-app in Azure.'
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d127e347-7581-47d7-b289-e0f51f2fbfbc
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c7cb0a3e132b491250623b945aecf6aea4f57c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-function-app"></a>Toewijzen van een aangepast domein tooa functie-app

Dit voorbeeldscript wordt gemaakt van een functie-app met verwante resources en wijst vervolgens `www.<yourdomain>` tooit. toomap tooa aangepast domein, de functie-app moet worden gemaakt in een App Service-plan en niet in een plan verbruik. Azure Functions biedt alleen ondersteuning voor het toewijzen van een aangepast domein met een A-record.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 


## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa function app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ storage-account maken](https://docs.microsoft.com/cli/azure/storage/account#create) | Maakt een opslagaccount dat is vereist voor Hallo functie-app. |
| [AZ appservice-abonnement maken](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Maakt een App Service-abonnement vereist toomap een aangepast domein. |
| [AZ functionapp maken]() | Hiermee maakt u een functie-app. |
| [AZ appservice web config hostnaam toevoegen](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | Een aangepast domein tooa functie-app wordt toegewezen. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende functies CLI scriptvoorbeelden kunnen u vinden in Hallo [documentatie van Azure Functions]().

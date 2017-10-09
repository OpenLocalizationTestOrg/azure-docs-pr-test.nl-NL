---
title: aaaAzure voorbeeldscript CLI - Bind een aangepaste SSL-certificaat tooa functie-app | Microsoft Docs
description: Azure CLI-voorbeeldscript - Bind een aangepaste SSL-certificaat tooa functie-app in Azure
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a>Binden van een aangepaste SSL-certificaat tooa functie-app

Dit voorbeeldscript wordt gemaakt van een functie-app in App Service met de bijbehorende resources en vervolgens Hallo SSL-certificaat van een aangepast domein naam tooit wordt gebonden. Voor dit voorbeeld hebt u het volgende nodig:

* Toegang tot pagina tooyour-domeinregistrar van DNS-configuratie.
* Een geldig. PFX-bestand en het bijbehorende wachtwoord voor Hallo SSL-certificaat u wilt dat tooupload en een binding.

toobind een SSL-certificaat, de functie-app moet worden gemaakt in een App Service-plan en niet in een plan verbruik.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ appservice-abonnement maken](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Hiermee maakt u een App Service-abonnement vereist toobind SSL-certificaten. |
| [AZ functionapp maken]() | Hiermee maakt u een functie-app. |
| [AZ appservice web config hostnaam toevoegen](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | Een aangepast domein toohello functie-app wordt toegewezen. |
| [AZ appservice web config ssl uploaden](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | Een SSL-certificaat tooa functie-app geüpload. |
| [AZ appservice web config ssl-binding](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | Een geüploade SSL-certificaat tooa functie-app, wordt gebonden. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie]().

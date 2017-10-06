---
title: een Azure-functie die verbinding tooan Azure Storage maakt aaaCreate | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: Maak een Azure-functie die verbinding tooan Azure Storage maakt'
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: a51a2c17149478eb2d3d0d4034400ed00cd8416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a>Functie-App integreren met Azure Storage-Account

Dit voorbeeldscript wordt gemaakt voor een functie-App en Storage-Account.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Voorbeeld van een script

Dit voorbeeld maakt u een Azure-functie-app en voegt Hallo storage connection string tooan app-instelling.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]


## <a name="clean-up-deployment"></a>Opschonen van implementatie

Na het uitvoeren van het voorbeeldscript Hallo kan na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, App Service-app en alle gerelateerde resources zijn:

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ aanmelding](https://docs.microsoft.com/cli/azure/#login) | Aanmelding tooAzure. |
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Een resourcegroep maken met de locatie |
| [AZ storage-account maken](https://docs.microsoft.com/cli/azure/storage/account) | Een opslagaccount maken |
| [AZ functionapp maken](https://docs.microsoft.com/cli/azure/functionapp#create) | Een nieuwe functie-app maken |
| [AZ groep verwijderen](https://docs.microsoft.com/cli/azure/group#delete) | Opruimen |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende voorbeelden van Azure Functions CLI script kunnen u vinden in Hallo [documentatie van Azure Functions](../functions-cli-samples.md).

---
title: aaaAzure voorbeeldscript CLI - maakt een functie-App voor uitvoering zonder server | Microsoft Docs
description: Azure CLI-Script steekproef - maken van een functie-App voor uitvoering zonder server
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
ms.openlocfilehash: 7ec872b642e50827896a73a9e43bcc87233e15c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a>Maken van een functie-App voor uitvoering zonder server

Dit voorbeeldscript wordt gemaakt van een functie-App van Azure, dat een container voor uw functies is. Hallo functie-App wordt gemaakt met Hallo [verbruik plan](../functions-scale.md#consumption-plan), dit is ideaal voor workloads van gebeurtenisafhankelijke zonder server.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Voorbeeld van een script

Dit script maakt een Azure-functie-app met behulp van Hallo [verbruik plan](../functions-scale.md#consumption-plan).

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Script uitleg

Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie. Dit script maakt gebruik van Hallo volgende opdrachten:

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ storage-account maken](/cli/azure/storage/account#create) | Een Azure Storage-account maakt. |
| [AZ functionapp maken](https://docs.microsoft.com/cli/azure/functionapp#create) | Hiermee maakt u een Azure-functie. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende voorbeelden van Azure Functions CLI script kunnen u vinden in Hallo [documentatie van Azure Functions](../functions-cli-samples.md).

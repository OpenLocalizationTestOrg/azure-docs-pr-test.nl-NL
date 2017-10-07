---
title: aaaAzure CLI-voorbeeldscript - Get-Hallo hostnaam, poorten en sleutels voor Azure Redis-Cache | Microsoft Docs
description: Azure CLI voorbeeldscript - Get Hallo hostnaam, poorten en sleutels voor een Azure Redis-Cache-exemplaar
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a>Hallo-hostnaam, poorten en sleutels voor Azure Redis-Cache ophalen

In dit scenario leert u hoe tooretrieve Hallo hostnaam, poorten en sleutels tooconnect tooan Azure Redis-Cache-exemplaar gebruikt.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten tooretrieve Hallo hostnaam, sleutels en poorten van een Azure Redis-Cache-exemplaar te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ redis weergeven](https://docs.microsoft.com/cli/azure/redis#show) | Ophalen van gegevens van een Azure Redis-Cache-exemplaar. |
| [AZ redis lijst-sleutels](https://docs.microsoft.com/cli/azure/redis#list-keys) | Sneltoetsen voor een Azure Redis-Cache-exemplaar worden opgehaald. |


## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende voorbeelden van Azure Redis-Cache CLI script kunnen u vinden in Hallo [documentatie van Azure Redis-Cache](../cli-samples.md).

---
title: Azure CLI-voorbeeldscript - Get de hostnaam, poorten en sleutels voor Azure Redis-Cache | Microsoft Docs
description: Azure CLI-voorbeeldscript - Get de hostnaam, poorten en sleutels voor een Azure Redis-Cache-exemplaar
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
ms.openlocfilehash: cd9adc784bceb0fff5e7c2bbee2be0950c51c8f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-hostname-ports-and-keys-for-azure-redis-cache"></a>Ophalen van de hostnaam, poorten en sleutels voor Azure Redis-Cache

In dit scenario u informatie over het ophalen van de hostnaam, poorten en sleutels die verbinding maken met een Azure Redis-Cache-exemplaar worden gebruikt.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli[belangrijkste](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis-Cache")]


## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van de volgende opdrachten voor het ophalen van de hostnaam, sleutels en poorten van een Azure Redis-Cache-exemplaar. Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.

| Opdracht | Opmerkingen |
|---|---|
| [AZ redis weergeven](https://docs.microsoft.com/cli/azure/redis#show) | Ophalen van gegevens van een Azure Redis-Cache-exemplaar. |
| [AZ redis lijst-sleutels](https://docs.microsoft.com/cli/azure/redis#list-keys) | Sneltoetsen voor een Azure Redis-Cache-exemplaar worden opgehaald. |


## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende voorbeelden van Azure Redis-Cache CLI-script kunnen worden gevonden in de [documentatie van Azure Redis-Cache](../cli-samples.md).
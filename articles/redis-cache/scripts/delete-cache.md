---
title: Het voorbeeldscript Azure CLI - verwijderen van een Azure Redis-Cache | Microsoft Docs
description: Het voorbeeldscript Azure CLI - verwijderen van een Azure Redis-Cache
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 7beded7a-d2c9-43a6-b3b4-b8079c11de4a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: f959823b3a7c5b0262f693ecad1e6efc4eec4f35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="delete-an-azure-redis-cache"></a>Verwijderen van een Azure Redis-Cache

In dit scenario wordt informatie over het verwijderen van een Azure Redis-Cache.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli[belangrijkste](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis-Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a>Script uitleg

Dit script wordt de volgende opdrachten om te verwijderen van een Azure Redis-Cache-exemplaar. Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.

| Opdracht | Opmerkingen |
|---|---|
| [AZ redis verwijderen](https://docs.microsoft.com/cli/azure/redis#delete) | Verwijderen van Redis-Cache-exemplaar. |


## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende voorbeelden van Azure Redis-Cache CLI-script kunnen worden gevonden in de [documentatie van Azure Redis-Cache](../cli-samples.md).
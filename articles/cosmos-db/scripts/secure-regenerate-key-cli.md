---
title: Azure CLI Script-opnieuw genereren Azure Cosmos DB accountsleutel | Microsoft Docs
description: Azure CLI-voorbeeldscript - opnieuw genereren accountcode Azure Cosmos-DB
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: 1a0ff3f8b8fb3eaf398d9fa925ef027b2481d47a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="regenerate-an-azure-cosmos-db-account-key-using-the-azure-cli"></a>Opnieuw genereren met de Azure CLI accountcode Azure Cosmos-DB

Dit voorbeeld wordt opnieuw gegenereerd elk soort sleutel voor Azure DB die Cosmos-account met de Azure CLI. 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger. Voer `az --version` uit om de versie te bekijken. Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/cosmosdb/secure-cosmosdb-regenerate-keys/secure-cosmosdb-regenerate-keys.sh?highlight=27-31 "Azure Cosmos-DB opnieuw genereren van sleutels")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie

Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van de volgende opdrachten. Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ cosmosdb maken](https://docs.microsoft.com/cli/azure/cosmosdb#create) | Een account voor Azure DB die Cosmos-updates. |
| [AZ cosmosdb opnieuw genereren-sleutel](/cli/azure/cosmosdb/regenerate-key) | Toegangscodes Regeneratates Azure Cosmos DB. |
| [AZ groep verwijderen](https://docs.microsoft.com/cli/azure/group#delete) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra Azure Cosmos DB CLI scriptvoorbeelden vindt u in de [Azure Cosmos DB CLI documentatie](../cli-samples.md).

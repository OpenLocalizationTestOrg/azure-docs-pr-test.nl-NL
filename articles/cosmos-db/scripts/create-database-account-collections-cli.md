---
title: aaaAzure CLI Script maakt een API van Azure Cosmos DB DocumentDB-account, database en verzameling | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: een API van Azure Cosmos DB DocumentDB-account, database en verzameling maken'
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
ms.date: 06/06/2017
ms.author: mimig
ms.openlocfilehash: 53919a849e04fa69680219e51c0289b9f2affe07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-an-documentdb-api-account-using-cli"></a>Azure Cosmos DB: Een DocumentDB-API-account maken met CLI

Dit voorbeeldscript CLI maakt een API van Azure Cosmos DB DocumentDB-account, database en verzameling.  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/create-cosmosdb-account-database/create-cosmosdb-account-database.sh?highlight=15-35 "Create an Azure Cosmos DB DocumentDB API account, database, and collection")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie

Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ cosmosdb maken](/cli/azure/cosmosdb#create) | Maakt een Cosmos-DB Azure-account. |
| [AZ groep verwijderen](/cli/azure/resource#delete) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra Azure Cosmos DB CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Cosmos DB CLI documentatie](../cli-samples.md).

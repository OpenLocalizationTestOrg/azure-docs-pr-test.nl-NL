---
title: CLI-voorbeelden voor Azure Cosmos DB aaaAzure | Microsoft Docs
description: Voorbeelden van Azure CLI - maken en beheren van Azure DB die Cosmos-accounts, databases, containers, regio's en firewalls.
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 06/07/2017
ms.author: mimig
ms.openlocfilehash: d6eefc3274e0b66eec4e69166bb7d4ddd58a522e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a>Azure CLI-voorbeelden voor Azure Cosmos-DB

Hallo bevat volgende tabel koppelingen toosample Azure CLI-scripts voor Azure Cosmos DB. Pagina's met naslaginformatie voor alle Azure Cosmos DB CLI-opdrachten zijn beschikbaar in Hallo [naslaginformatie over Azure CLI 2.0](https://docs.microsoft.com/cli/azure/cosmosdb).

| |  |
|---|---|
|**Azure DB die Cosmos-account, database en containers maken**||
|[Een DocumentDB-API, grafiek of tabel API-account maken](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Maakt een enkele Cosmos DB-API van Azure-account, database en container voor gebruik met Hallo DocumentDB, grafiek of tabel API's. |
| [Een API MongoDB-account maken](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Maakt een enkel account, database en verzameling in Azure Cosmos DB MongoDB-API. |
|**Azure Cosmos DB schalen**||
| [Schaal container doorvoer](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Wijzigingen Hallo ingericht througput in een container.|
|[Azure DB die Cosmos-databaseaccount in meerdere regio's worden gerepliceerd en het configureren van failover prioriteiten](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Globaal repliceert accountgegevens naar meerdere regio's met een opgegeven failover-prioriteit.|
|**Azure Cosmos DB beveiligen**||
| [Sleutels van account ophalen](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Hiermee haalt u Hallo primaire en secundaire master schrijven en primaire en secundaire alleen-lezen sleutels voor Hallo-account.|
| [MongoDB-verbindingsreeks ophalen](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Hiermee haalt u Hallo connection string tooconnect uw MongoDB app tooyour Azure DB die Cosmos-account.|
|[Opnieuw genereren van sleutels](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Genereert Hallo master of alleen-lezen-sleutel voor Hallo-account.|
|[Maken van een firewall](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Maakt een inkomende IP-access control beleid toolimit toohello toegangsaccount van een goedgekeurde reeks machines en/of cloud-services.|
|**Hoge beschikbaarheid, herstel na noodgevallen, back-up en herstel**||
|[Failover-beleid configureren](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Sets Hallo failover prioriteit van elke regio waarin het Hallo-account wordt gerepliceerd.|
|**Azure Cosmos DB verbinding te maken met bronnen**||
|[Verbinding maken met een web-app tooAzure Cosmos-DB](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|Maken en koppelen van een Azure DB die Cosmos-database en een Azure-web-app.|
|||

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
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="d048b-103">Azure CLI-voorbeelden voor Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="d048b-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="d048b-104">Hallo bevat volgende tabel koppelingen toosample Azure CLI-scripts voor Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d048b-104">hello following table includes links toosample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="d048b-105">Pagina's met naslaginformatie voor alle Azure Cosmos DB CLI-opdrachten zijn beschikbaar in Hallo [naslaginformatie over Azure CLI 2.0](https://docs.microsoft.com/cli/azure/cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="d048b-105">Reference pages for all Azure Cosmos DB CLI commands are available in hello [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="d048b-106">**Azure DB die Cosmos-account, database en containers maken**</span><span class="sxs-lookup"><span data-stu-id="d048b-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="d048b-107">Een DocumentDB-API, grafiek of tabel API-account maken</span><span class="sxs-lookup"><span data-stu-id="d048b-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="d048b-108">Maakt een enkele Cosmos DB-API van Azure-account, database en container voor gebruik met Hallo DocumentDB, grafiek of tabel API's.</span><span class="sxs-lookup"><span data-stu-id="d048b-108">Creates a single Azure Cosmos DB API account, database, and container for use with hello DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="d048b-109">Een API MongoDB-account maken</span><span class="sxs-lookup"><span data-stu-id="d048b-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="d048b-110">Maakt een enkel account, database en verzameling in Azure Cosmos DB MongoDB-API.</span><span class="sxs-lookup"><span data-stu-id="d048b-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="d048b-111">**Azure Cosmos DB schalen**</span><span class="sxs-lookup"><span data-stu-id="d048b-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="d048b-112">Schaal container doorvoer</span><span class="sxs-lookup"><span data-stu-id="d048b-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="d048b-113">Wijzigingen Hallo ingericht througput in een container.</span><span class="sxs-lookup"><span data-stu-id="d048b-113">Changes hello provisioned througput on a container.</span></span>|
|[<span data-ttu-id="d048b-114">Azure DB die Cosmos-databaseaccount in meerdere regio's worden gerepliceerd en het configureren van failover prioriteiten</span><span class="sxs-lookup"><span data-stu-id="d048b-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="d048b-115">Globaal repliceert accountgegevens naar meerdere regio's met een opgegeven failover-prioriteit.</span><span class="sxs-lookup"><span data-stu-id="d048b-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="d048b-116">**Azure Cosmos DB beveiligen**</span><span class="sxs-lookup"><span data-stu-id="d048b-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="d048b-117">Sleutels van account ophalen</span><span class="sxs-lookup"><span data-stu-id="d048b-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="d048b-118">Hiermee haalt u Hallo primaire en secundaire master schrijven en primaire en secundaire alleen-lezen sleutels voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="d048b-118">Gets hello primary and secondary master write keys and primary and secondary read-only keys for hello account.</span></span>|
| [<span data-ttu-id="d048b-119">MongoDB-verbindingsreeks ophalen</span><span class="sxs-lookup"><span data-stu-id="d048b-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="d048b-120">Hiermee haalt u Hallo connection string tooconnect uw MongoDB app tooyour Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="d048b-120">Gets hello connection string tooconnect your MongoDB app tooyour Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="d048b-121">Opnieuw genereren van sleutels</span><span class="sxs-lookup"><span data-stu-id="d048b-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="d048b-122">Genereert Hallo master of alleen-lezen-sleutel voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="d048b-122">Regenerates hello master or read-only key for hello account.</span></span>|
|[<span data-ttu-id="d048b-123">Maken van een firewall</span><span class="sxs-lookup"><span data-stu-id="d048b-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="d048b-124">Maakt een inkomende IP-access control beleid toolimit toohello toegangsaccount van een goedgekeurde reeks machines en/of cloud-services.</span><span class="sxs-lookup"><span data-stu-id="d048b-124">Creates an inbound IP access control policy toolimit access toohello account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="d048b-125">**Hoge beschikbaarheid, herstel na noodgevallen, back-up en herstel**</span><span class="sxs-lookup"><span data-stu-id="d048b-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="d048b-126">Failover-beleid configureren</span><span class="sxs-lookup"><span data-stu-id="d048b-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="d048b-127">Sets Hallo failover prioriteit van elke regio waarin het Hallo-account wordt gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="d048b-127">Sets hello failover priority of each region in which hello account is replicated.</span></span>|
|<span data-ttu-id="d048b-128">**Azure Cosmos DB verbinding te maken met bronnen**</span><span class="sxs-lookup"><span data-stu-id="d048b-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="d048b-129">Verbinding maken met een web-app tooAzure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="d048b-129">Connect a web app tooAzure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="d048b-130">Maken en koppelen van een Azure DB die Cosmos-database en een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="d048b-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||

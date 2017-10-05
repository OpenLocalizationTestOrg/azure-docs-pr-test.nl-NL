---
title: Voorbeelden van Azure CLI voor Azure Cosmos DB | Microsoft Docs
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
ms.openlocfilehash: 709d2ccce0f4b9827a8076f683c7e0f74cbdd4ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="fba07-103">Azure CLI-voorbeelden voor Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="fba07-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="fba07-104">De volgende tabel bevat koppelingen naar de Azure CLI-voorbeeldscripts voor Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fba07-104">The following table includes links to sample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="fba07-105">Pagina's met naslaginformatie voor alle Azure Cosmos DB CLI-opdrachten zijn beschikbaar in de [naslaginformatie over Azure CLI 2.0](https://docs.microsoft.com/cli/azure/cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="fba07-105">Reference pages for all Azure Cosmos DB CLI commands are available in the [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="fba07-106">**Azure DB die Cosmos-account, database en containers maken**</span><span class="sxs-lookup"><span data-stu-id="fba07-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="fba07-107">Een DocumentDB-API, grafiek of tabel API-account maken</span><span class="sxs-lookup"><span data-stu-id="fba07-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="fba07-108">Maakt een enkele Cosmos DB-API van Azure-account, database en container voor gebruik met de DocumentDB, de grafiek of de tabel-API's.</span><span class="sxs-lookup"><span data-stu-id="fba07-108">Creates a single Azure Cosmos DB API account, database, and container for use with the DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="fba07-109">Een API MongoDB-account maken</span><span class="sxs-lookup"><span data-stu-id="fba07-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="fba07-110">Maakt een enkel account, database en verzameling in Azure Cosmos DB MongoDB-API.</span><span class="sxs-lookup"><span data-stu-id="fba07-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="fba07-111">**Azure Cosmos DB schalen**</span><span class="sxs-lookup"><span data-stu-id="fba07-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="fba07-112">Schaal container doorvoer</span><span class="sxs-lookup"><span data-stu-id="fba07-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="fba07-113">Hiermee wijzigt u de ingerichte througput in een container.</span><span class="sxs-lookup"><span data-stu-id="fba07-113">Changes the provisioned througput on a container.</span></span>|
|[<span data-ttu-id="fba07-114">Azure DB die Cosmos-databaseaccount in meerdere regio's worden gerepliceerd en het configureren van failover prioriteiten</span><span class="sxs-lookup"><span data-stu-id="fba07-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="fba07-115">Globaal repliceert accountgegevens naar meerdere regio's met een opgegeven failover-prioriteit.</span><span class="sxs-lookup"><span data-stu-id="fba07-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="fba07-116">**Azure Cosmos DB beveiligen**</span><span class="sxs-lookup"><span data-stu-id="fba07-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="fba07-117">Sleutels van account ophalen</span><span class="sxs-lookup"><span data-stu-id="fba07-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="fba07-118">Hiermee haalt u de primaire en secundaire master schrijven en primaire en secundaire alleen-lezen sleutels voor het account.</span><span class="sxs-lookup"><span data-stu-id="fba07-118">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="fba07-119">MongoDB-verbindingsreeks ophalen</span><span class="sxs-lookup"><span data-stu-id="fba07-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="fba07-120">Hiermee haalt u de verbindingsreeks naar uw MongoDB-app verbinden met uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="fba07-120">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="fba07-121">Opnieuw genereren van sleutels</span><span class="sxs-lookup"><span data-stu-id="fba07-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="fba07-122">De sleutel van het model of de alleen-lezen voor het account genereert.</span><span class="sxs-lookup"><span data-stu-id="fba07-122">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="fba07-123">Maken van een firewall</span><span class="sxs-lookup"><span data-stu-id="fba07-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="fba07-124">Hiermee maakt u een binnenkomende IP-beleid voor toegangsbeheer om aan het account de toegang beperken tot een goedgekeurde aantal machines en/of cloudservices.</span><span class="sxs-lookup"><span data-stu-id="fba07-124">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="fba07-125">**Hoge beschikbaarheid, herstel na noodgevallen, back-up en herstel**</span><span class="sxs-lookup"><span data-stu-id="fba07-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="fba07-126">Failover-beleid configureren</span><span class="sxs-lookup"><span data-stu-id="fba07-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="fba07-127">Hiermee stelt u de prioriteit van de failover van elke regio waarin het account wordt gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="fba07-127">Sets the failover priority of each region in which the account is replicated.</span></span>|
|<span data-ttu-id="fba07-128">**Azure Cosmos DB verbinding te maken met bronnen**</span><span class="sxs-lookup"><span data-stu-id="fba07-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="fba07-129">Een WebApp verbinden met Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="fba07-129">Connect a web app to Azure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="fba07-130">Maken en koppelen van een Azure DB die Cosmos-database en een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="fba07-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||

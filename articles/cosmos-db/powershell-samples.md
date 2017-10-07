---
title: Voorbeelden van PowerShell voor Azure Cosmos DB aaaAzure | Microsoft Docs
description: Azure PowerShell-voorbeelden - Scripts toohelp maken en beheren van Azure DB die Cosmos-accounts.
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 8815e775f720226e98cc8dcf7743e481c213272b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-azure-cosmos-db"></a><span data-ttu-id="9d5e6-103">Voorbeelden van Azure PowerShell voor Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="9d5e6-103">Azure PowerShell samples for Azure Cosmos DB</span></span>

<span data-ttu-id="9d5e6-104">Hallo bevat volgende tabel koppelingen toosample Azure PowerShell-scripts voor Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9d5e6-104">hello following table includes links toosample Azure PowerShell scripts for Azure Cosmos DB.</span></span>

| |  |
|---|---|
|<span data-ttu-id="9d5e6-105">**Een Azure DB die Cosmos-account maken**</span><span class="sxs-lookup"><span data-stu-id="9d5e6-105">**Create an Azure Cosmos DB account**</span></span>||
|[<span data-ttu-id="9d5e6-106">Een DocumentDB-API-account maken</span><span class="sxs-lookup"><span data-stu-id="9d5e6-106">Create a DocumentDB API account</span></span>](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="9d5e6-107">Maakt een enkele Azure Cosmos DB account toouse Hello DocumentDB-API.</span><span class="sxs-lookup"><span data-stu-id="9d5e6-107">Creates a single Azure Cosmos DB account toouse with hello DocumentDB API.</span></span> |
|<span data-ttu-id="9d5e6-108">**Azure Cosmos DB schalen**</span><span class="sxs-lookup"><span data-stu-id="9d5e6-108">**Scale Azure Cosmos DB**</span></span>||
|[<span data-ttu-id="9d5e6-109">Azure DB die Cosmos-account in meerdere regio's worden gerepliceerd en configureren van failover-prioriteiten</span><span class="sxs-lookup"><span data-stu-id="9d5e6-109">Replicate Azure Cosmos DB account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="9d5e6-110">Globaal repliceert accountgegevens naar meerdere regio's met een opgegeven failover-prioriteit.</span><span class="sxs-lookup"><span data-stu-id="9d5e6-110">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="9d5e6-111">**Azure Cosmos DB beveiligen**</span><span class="sxs-lookup"><span data-stu-id="9d5e6-111">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="9d5e6-112">Sleutels van account ophalen</span><span class="sxs-lookup"><span data-stu-id="9d5e6-112">Get account keys</span></span>](scripts/secure-get-account-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="9d5e6-113">Hiermee haalt u Hallo primaire en secundaire master schrijven en primaire en secundaire alleen-lezen sleutels voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="9d5e6-113">Gets hello primary and secondary master write keys and primary and secondary read-only keys for hello account.</span></span>|
| [<span data-ttu-id="9d5e6-114">MongoDB-verbindingsreeks ophalen</span><span class="sxs-lookup"><span data-stu-id="9d5e6-114">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="9d5e6-115">Hiermee haalt u Hallo connection string tooconnect uw MongoDB app tooyour Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="9d5e6-115">Gets hello connection string tooconnect your MongoDB app tooyour Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="9d5e6-116">Opnieuw genereren van sleutels</span><span class="sxs-lookup"><span data-stu-id="9d5e6-116">Regenerate account keys</span></span>](scripts/secure-regenerate-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="9d5e6-117">Genereert Hallo master of alleen-lezen-sleutel voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="9d5e6-117">Regenerates hello master or read-only key for hello account.</span></span>|
|[<span data-ttu-id="9d5e6-118">Maken van een firewall</span><span class="sxs-lookup"><span data-stu-id="9d5e6-118">Create a firewall</span></span>](scripts/create-firewall-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="9d5e6-119">Maakt een inkomende IP-access control beleid toolimit toohello toegangsaccount van een goedgekeurde reeks machines en/of cloud-services.</span><span class="sxs-lookup"><span data-stu-id="9d5e6-119">Creates an inbound IP access control policy toolimit access toohello account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="9d5e6-120">**Hoge beschikbaarheid, herstel na noodgevallen, back-up en herstel**</span><span class="sxs-lookup"><span data-stu-id="9d5e6-120">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="9d5e6-121">Failover-beleid configureren</span><span class="sxs-lookup"><span data-stu-id="9d5e6-121">Configure failover policy</span></span>](scripts/ha-failover-policy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="9d5e6-122">Sets Hallo failover prioriteit van elke regio waarin het Hallo-account wordt gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="9d5e6-122">Sets hello failover priority of each region in which hello account is replicated.</span></span>|
|||
---
title: MongoDB-verbindingsreeks voor een account voor Azure Cosmos DB | Microsoft Docs
description: Ontdek hoe u uw MongoDB-app verbinden met een Azure DB die Cosmos-account met behulp van een verbindingsreeks voor MongoDB.
keywords: mongodb-verbindingsreeks
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: 5a47001705531d971d3181df9c0aa8f957168845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-mongodb-application-to-azure-cosmos-db"></a><span data-ttu-id="63137-104">Verbinding maken met een toepassing MongoDB bij Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="63137-104">Connect a MongoDB application to Azure Cosmos DB</span></span>
<span data-ttu-id="63137-105">Ontdek hoe u uw MongoDB-app verbinden met een Azure DB die Cosmos-account met behulp van een verbindingsreeks voor MongoDB.</span><span class="sxs-lookup"><span data-stu-id="63137-105">Learn how to connect your MongoDB app to an Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="63137-106">U kunt vervolgens een Azure DB die Cosmos-database als het archief voor uw app MongoDB.</span><span class="sxs-lookup"><span data-stu-id="63137-106">You can then use an Azure Cosmos DB database as the data store for your MongoDB app.</span></span> 

<span data-ttu-id="63137-107">Deze zelfstudie biedt twee manieren verbindingsreeksgegevens ophalen:</span><span class="sxs-lookup"><span data-stu-id="63137-107">This tutorial provides two ways to retrieve connection string information:</span></span>

- <span data-ttu-id="63137-108">[De snel starten methode](#QuickstartConnection), voor gebruik met .NET, Node.js, MongoDB-Shell, Java en Python-stuurprogramma's</span><span class="sxs-lookup"><span data-stu-id="63137-108">[The quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="63137-109">[De aangepaste tekenreeks verbindingsmethode](#GetCustomConnection), voor gebruik met andere stuurprogramma's</span><span class="sxs-lookup"><span data-stu-id="63137-109">[The custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63137-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="63137-110">Prerequisites</span></span>

- <span data-ttu-id="63137-111">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="63137-111">An Azure account.</span></span> <span data-ttu-id="63137-112">Als u geen Azure-account hebt, maakt u een [gratis Azure-account](https://azure.microsoft.com/free/) nu.</span><span class="sxs-lookup"><span data-stu-id="63137-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="63137-113">Een Azure Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="63137-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="63137-114">Zie voor instructies [bouwen van een web-app van de MongoDB-API met .NET- en de Azure-portal](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="63137-114">For instructions, see [Build a MongoDB API web app with .NET and the Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="63137-115"><a id="QuickstartConnection"></a>De MongoDB-verbindingsreeks ophalen met behulp van de snel starten</span><span class="sxs-lookup"><span data-stu-id="63137-115"><a id="QuickstartConnection"></a>Get the MongoDB connection string by using the quick start</span></span>
1. <span data-ttu-id="63137-116">In een internetbrowser, moet u zich aanmelden bij de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="63137-116">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="63137-117">In de **Azure Cosmos DB** blade, selecteert u de API voor MongoDB-account.</span><span class="sxs-lookup"><span data-stu-id="63137-117">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="63137-118">Klik in het linkerdeelvenster van de accountblade **snel starten**.</span><span class="sxs-lookup"><span data-stu-id="63137-118">In the left pane of the account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="63137-119">Kies uw platform (**.NET**, **Node.js**, **MongoDB-Shell**, **Java**, **Python**).</span><span class="sxs-lookup"><span data-stu-id="63137-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="63137-120">Als er geen het hulpprogramma wordt weergegeven, of je--Documenteer we continu meer verbinding codefragmenten.</span><span class="sxs-lookup"><span data-stu-id="63137-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="63137-121">Stuur een reactie hieronder op wat u zou willen zien.</span><span class="sxs-lookup"><span data-stu-id="63137-121">Please comment below on what you'd like to see.</span></span> <span data-ttu-id="63137-122">Lees voor meer informatie over hoe u uw eigen verbinding opgesteld, [ophalen van het account verbindingsinformatie](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="63137-122">To learn how to craft your own connection, read [Get the account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="63137-123">Kopieer en plak het volgende codefragment in uw app MongoDB.</span><span class="sxs-lookup"><span data-stu-id="63137-123">Copy and paste the code snippet into your MongoDB app.</span></span>

    ![De blade snel starten](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="63137-125"><a id="GetCustomConnection"></a>De verbindingsreeks MongoDB om aan te passen ophalen</span><span class="sxs-lookup"><span data-stu-id="63137-125"><a id="GetCustomConnection"></a> Get the MongoDB connection string to customize</span></span>
1. <span data-ttu-id="63137-126">In een internetbrowser, moet u zich aanmelden bij de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="63137-126">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="63137-127">In de **Azure Cosmos DB** blade, selecteert u de API voor MongoDB-account.</span><span class="sxs-lookup"><span data-stu-id="63137-127">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="63137-128">Klik in het linkerdeelvenster van de accountblade **verbindingsreeks**.</span><span class="sxs-lookup"><span data-stu-id="63137-128">In the left pane of the account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="63137-129">De **verbindingsreeks** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="63137-129">The **Connection String** blade opens.</span></span> <span data-ttu-id="63137-130">Alle informatie die nodig zijn voor verbinding met het account met behulp van een stuurprogramma voor MongoDB, met inbegrip van een vooraf gedefinieerde verbindingsreeks heeft.</span><span class="sxs-lookup"><span data-stu-id="63137-130">It has all the information necessary to connect to the account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Connection String-blade](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="63137-132">Vereisten voor verbinding tekenreeks</span><span class="sxs-lookup"><span data-stu-id="63137-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="63137-133">Azure Cosmos DB heeft strenge beveiligingsvereisten en standaarden.</span><span class="sxs-lookup"><span data-stu-id="63137-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="63137-134">Azure DB Cosmos-accounts vereist verificatie en veilige communicatie via *SSL*.</span><span class="sxs-lookup"><span data-stu-id="63137-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="63137-135">Azure Cosmos DB ondersteunt standaard MongoDB URI indeling van de verbindingsreeks, met een aantal specifieke vereisten: Azure Cosmos DB accounts verificatie en veilige communicatie via SSL vereisen.</span><span class="sxs-lookup"><span data-stu-id="63137-135">Azure Cosmos DB supports the standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="63137-136">Indeling van de verbindingsreeks is dus:</span><span class="sxs-lookup"><span data-stu-id="63137-136">So, the connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="63137-137">De waarden van deze tekenreeks zijn beschikbaar in de **verbindingsreeks** blade eerder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="63137-137">The values of this string are available in the **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="63137-138">Gebruikersnaam (vereist): Azure DB die Cosmos-accountnaam.</span><span class="sxs-lookup"><span data-stu-id="63137-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="63137-139">Wachtwoord (vereist): Azure Cosmos DB accountwachtwoord.</span><span class="sxs-lookup"><span data-stu-id="63137-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="63137-140">Host (vereist): FQDN-naam van de Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="63137-140">Host (required): FQDN of the Azure Cosmos DB account.</span></span>
* <span data-ttu-id="63137-141">Poort (vereist): 10255.</span><span class="sxs-lookup"><span data-stu-id="63137-141">Port (required): 10255.</span></span>
* <span data-ttu-id="63137-142">Database (optioneel): de database die de verbinding wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="63137-142">Database (optional): The database that the connection uses.</span></span> <span data-ttu-id="63137-143">Als er geen database wordt opgegeven, wordt de standaarddatabase is 'test'.</span><span class="sxs-lookup"><span data-stu-id="63137-143">If no database is provided, the default database is "test."</span></span>
* <span data-ttu-id="63137-144">SSL = true (vereist)</span><span class="sxs-lookup"><span data-stu-id="63137-144">ssl=true (required)</span></span>

<span data-ttu-id="63137-145">Neem bijvoorbeeld het account dat wordt weergegeven in de **verbindingsreeks** blade.</span><span class="sxs-lookup"><span data-stu-id="63137-145">For example, consider the account shown in the **Connection String** blade.</span></span> <span data-ttu-id="63137-146">Er is een geldige verbindingsreeks:</span><span class="sxs-lookup"><span data-stu-id="63137-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="63137-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="63137-147">Next steps</span></span>
* <span data-ttu-id="63137-148">Meer informatie over hoe [MongoChef gebruiken](mongodb-mongochef.md) met een Azure Cosmos DB-API voor MongoDB-account.</span><span class="sxs-lookup"><span data-stu-id="63137-148">Learn how to [use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="63137-149">De API van Azure Cosmos DB verkennen voor MongoDB hand [voorbeelden](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="63137-149">Explore the Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>

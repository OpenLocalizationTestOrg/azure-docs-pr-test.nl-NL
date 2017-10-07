---
title: de verbindingsreeks aaaMongoDB voor een Azure DB die Cosmos-account | Microsoft Docs
description: Meer informatie over hoe tooconnect uw MongoDB app tooan Azure DB die Cosmos-account met behulp van een verbindingsreeks voor MongoDB.
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
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a><span data-ttu-id="a81ce-104">Verbinding maken met een MongoDB toepassing tooAzure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="a81ce-104">Connect a MongoDB application tooAzure Cosmos DB</span></span>
<span data-ttu-id="a81ce-105">Meer informatie over hoe tooconnect uw MongoDB app tooan Azure DB die Cosmos-account met behulp van een verbindingsreeks voor MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a81ce-105">Learn how tooconnect your MongoDB app tooan Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="a81ce-106">U kunt vervolgens een Azure DB die Cosmos-database als Hallo gegevens opslaan voor uw app MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a81ce-106">You can then use an Azure Cosmos DB database as hello data store for your MongoDB app.</span></span> 

<span data-ttu-id="a81ce-107">Deze zelfstudie biedt twee manieren verbindingsreeksgegevens tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="a81ce-107">This tutorial provides two ways tooretrieve connection string information:</span></span>

- <span data-ttu-id="a81ce-108">[Hallo snel starten methode](#QuickstartConnection), voor gebruik met .NET, Node.js, MongoDB-Shell, Java en Python-stuurprogramma's</span><span class="sxs-lookup"><span data-stu-id="a81ce-108">[hello quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="a81ce-109">[tekenreeks van aangepaste verbindingsmethode Hallo](#GetCustomConnection), voor gebruik met andere stuurprogramma's</span><span class="sxs-lookup"><span data-stu-id="a81ce-109">[hello custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a81ce-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a81ce-110">Prerequisites</span></span>

- <span data-ttu-id="a81ce-111">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="a81ce-111">An Azure account.</span></span> <span data-ttu-id="a81ce-112">Als u geen Azure-account hebt, maakt u een [gratis Azure-account](https://azure.microsoft.com/free/) nu.</span><span class="sxs-lookup"><span data-stu-id="a81ce-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="a81ce-113">Een Azure Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="a81ce-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="a81ce-114">Zie voor instructies [bouwen van een web-app van de MongoDB-API met .NET en Azure-portal Hallo](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="a81ce-114">For instructions, see [Build a MongoDB API web app with .NET and hello Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="a81ce-115"><a id="QuickstartConnection"></a>Hallo MongoDB-verbindingsreeks ophalen met behulp van Hallo snel starten</span><span class="sxs-lookup"><span data-stu-id="a81ce-115"><a id="QuickstartConnection"></a>Get hello MongoDB connection string by using hello quick start</span></span>
1. <span data-ttu-id="a81ce-116">Aanmelden in een internetbrowser toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a81ce-116">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a81ce-117">In Hallo **Azure Cosmos DB** blade Selecteer Hallo-API voor MongoDB-account.</span><span class="sxs-lookup"><span data-stu-id="a81ce-117">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="a81ce-118">Klik in het linkerdeelvenster Hallo van Hallo accountblade op **snel starten**.</span><span class="sxs-lookup"><span data-stu-id="a81ce-118">In hello left pane of hello account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="a81ce-119">Kies uw platform (**.NET**, **Node.js**, **MongoDB-Shell**, **Java**, **Python**).</span><span class="sxs-lookup"><span data-stu-id="a81ce-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="a81ce-120">Als er geen het hulpprogramma wordt weergegeven, of je--Documenteer we continu meer verbinding codefragmenten.</span><span class="sxs-lookup"><span data-stu-id="a81ce-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="a81ce-121">Stuur een reactie hieronder op wat u wilt dat toosee.</span><span class="sxs-lookup"><span data-stu-id="a81ce-121">Please comment below on what you'd like toosee.</span></span> <span data-ttu-id="a81ce-122">toolearn hoe toocraft uw eigen verbinding Lees [Hallo-account verbindingsreeksgegevens ophalen](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="a81ce-122">toolearn how toocraft your own connection, read [Get hello account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="a81ce-123">Kopieer en plak Hallo codefragment in uw app MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a81ce-123">Copy and paste hello code snippet into your MongoDB app.</span></span>

    ![De blade snel starten](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="a81ce-125"><a id="GetCustomConnection"></a>Hallo MongoDB connection string toocustomize ophalen</span><span class="sxs-lookup"><span data-stu-id="a81ce-125"><a id="GetCustomConnection"></a> Get hello MongoDB connection string toocustomize</span></span>
1. <span data-ttu-id="a81ce-126">Aanmelden in een internetbrowser toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a81ce-126">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a81ce-127">In Hallo **Azure Cosmos DB** blade Selecteer Hallo-API voor MongoDB-account.</span><span class="sxs-lookup"><span data-stu-id="a81ce-127">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="a81ce-128">Klik in het linkerdeelvenster Hallo van Hallo accountblade op **verbindingsreeks**.</span><span class="sxs-lookup"><span data-stu-id="a81ce-128">In hello left pane of hello account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="a81ce-129">Hallo **verbindingsreeks** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="a81ce-129">hello **Connection String** blade opens.</span></span> <span data-ttu-id="a81ce-130">Alle Hallo informatie nodig tooconnect toohello account heeft met behulp van een stuurprogramma voor MongoDB, met inbegrip van een vooraf gedefinieerde verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="a81ce-130">It has all hello information necessary tooconnect toohello account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Connection String-blade](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="a81ce-132">Vereisten voor verbinding tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a81ce-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="a81ce-133">Azure Cosmos DB heeft strenge beveiligingsvereisten en standaarden.</span><span class="sxs-lookup"><span data-stu-id="a81ce-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="a81ce-134">Azure DB Cosmos-accounts vereist verificatie en veilige communicatie via *SSL*.</span><span class="sxs-lookup"><span data-stu-id="a81ce-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="a81ce-135">Azure Cosmos DB ondersteunt Hallo standaard MongoDB URI indeling verbindingsreeks, met een aantal specifieke vereisten: Azure Cosmos DB accounts verificatie en veilige communicatie via SSL vereisen.</span><span class="sxs-lookup"><span data-stu-id="a81ce-135">Azure Cosmos DB supports hello standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="a81ce-136">Dus is indeling verbindingsreeks Hallo:</span><span class="sxs-lookup"><span data-stu-id="a81ce-136">So, hello connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="a81ce-137">Hallo-waarden van deze tekenreeks zijn beschikbaar in Hallo **verbindingsreeks** blade eerder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="a81ce-137">hello values of this string are available in hello **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="a81ce-138">Gebruikersnaam (vereist): Azure DB die Cosmos-accountnaam.</span><span class="sxs-lookup"><span data-stu-id="a81ce-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="a81ce-139">Wachtwoord (vereist): Azure Cosmos DB accountwachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a81ce-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="a81ce-140">Host (vereist): FQDN-naam van hello Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="a81ce-140">Host (required): FQDN of hello Azure Cosmos DB account.</span></span>
* <span data-ttu-id="a81ce-141">Poort (vereist): 10255.</span><span class="sxs-lookup"><span data-stu-id="a81ce-141">Port (required): 10255.</span></span>
* <span data-ttu-id="a81ce-142">Database (optioneel): Hallo-database die Hallo verbinding wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a81ce-142">Database (optional): hello database that hello connection uses.</span></span> <span data-ttu-id="a81ce-143">Als er geen database wordt opgegeven, is de standaarddatabase Hallo 'test'.</span><span class="sxs-lookup"><span data-stu-id="a81ce-143">If no database is provided, hello default database is "test."</span></span>
* <span data-ttu-id="a81ce-144">SSL = true (vereist)</span><span class="sxs-lookup"><span data-stu-id="a81ce-144">ssl=true (required)</span></span>

<span data-ttu-id="a81ce-145">Denk bijvoorbeeld Hallo-account wordt weergegeven in Hallo **verbindingsreeks** blade.</span><span class="sxs-lookup"><span data-stu-id="a81ce-145">For example, consider hello account shown in hello **Connection String** blade.</span></span> <span data-ttu-id="a81ce-146">Er is een geldige verbindingsreeks:</span><span class="sxs-lookup"><span data-stu-id="a81ce-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="a81ce-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a81ce-147">Next steps</span></span>
* <span data-ttu-id="a81ce-148">Meer informatie over hoe te[MongoChef gebruiken](mongodb-mongochef.md) met een Azure Cosmos DB-API voor MongoDB-account.</span><span class="sxs-lookup"><span data-stu-id="a81ce-148">Learn how too[use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="a81ce-149">Hello Azure Cosmos DB-API voor MongoDB verkennen hand [voorbeelden](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a81ce-149">Explore hello Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>

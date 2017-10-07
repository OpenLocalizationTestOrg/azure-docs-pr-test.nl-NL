---
title: aaaUse MongoChef voor Azure Cosmos DB | Microsoft Docs
description: 'Meer informatie over hoe toouse MongoChef met een Cosmos Azure DB: API voor MongoDB-account'
keywords: mongochef
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 4b047797b231c34ccc6f2ed02416525c6228d596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="3aae0-104">MongoChef gebruiken met een Cosmos Azure DB: API voor MongoDB-account</span><span class="sxs-lookup"><span data-stu-id="3aae0-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="3aae0-105">tooconnect tooan Azure Cosmos DB: de API voor MongoDB-account, moet u:</span><span class="sxs-lookup"><span data-stu-id="3aae0-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="3aae0-106">Download en installeer [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="3aae0-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="3aae0-107">Uw Azure-Cosmos-DB hebben:-API voor MongoDB account [verbindingsreeks](connect-mongodb-account.md) informatie</span><span class="sxs-lookup"><span data-stu-id="3aae0-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-hello-connection-in-mongochef"></a><span data-ttu-id="3aae0-108">Hallo verbinding maken in MongoChef</span><span class="sxs-lookup"><span data-stu-id="3aae0-108">Create hello connection in MongoChef</span></span>
<span data-ttu-id="3aae0-109">tooadd uw Cosmos Azure DB: API voor MongoDB account toohello MongoChef Verbindingsbeheer uitvoeren Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="3aae0-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello MongoChef connection manager, perform hello following steps.</span></span>

1. <span data-ttu-id="3aae0-110">Ophalen van de Cosmos Azure DB:-API voor MongoDB-verbindingsgegevens Hallo instructies [hier](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="3aae0-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Schermopname van Hallo connection string-blade](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="3aae0-112">Klik op **Connect** tooopen Hallo Connection Manager en klik vervolgens op **nieuwe verbinding**</span><span class="sxs-lookup"><span data-stu-id="3aae0-112">Click **Connect** tooopen hello Connection Manager, then click **New Connection**</span></span>

    ![Schermopname van Hallo MongoChef Verbindingsbeheer](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="3aae0-114">In Hallo **nieuwe verbinding** venster op Hallo **Server** tabblad, voert u Hallo HOST (FQDN) van hello Azure Cosmos DB:-API voor MongoDB-account en het Hallo-poort.</span><span class="sxs-lookup"><span data-stu-id="3aae0-114">In hello **New Connection** window, on hello **Server** tab, enter hello HOST (FQDN) of hello Azure Cosmos DB: API for MongoDB account and hello PORT.</span></span>

    ![Schermopname van tabblad voor Hallo MongoChef connection manager-server](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="3aae0-116">In Hallo **nieuwe verbinding** venster op Hallo **verificatie** Kies verificatiemodus **standaard (MONGODB CR of SCARM-SHA-1)** en Hallo gebruikersnaam invoeren en HET WACHTWOORD.</span><span class="sxs-lookup"><span data-stu-id="3aae0-116">In hello **New Connection** window, on hello **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter hello USERNAME and PASSWORD.</span></span>  <span data-ttu-id="3aae0-117">Accepteer Hallo standaard verificatie db (admin) of geef uw eigen waarde.</span><span class="sxs-lookup"><span data-stu-id="3aae0-117">Accept hello default authentication db (admin) or provide your own value.</span></span>

    ![Schermopname van tabblad voor verificatie van Hallo MongoChef connection manager](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="3aae0-119">In Hallo **nieuwe verbinding** venster op Hallo **SSL** tabblad, controleert u Hallo **Gebruik SSL-protocol tooconnect** selectievakje en Hallo **accepteren server zelfondertekend SSL certificaten** keuzerondje.</span><span class="sxs-lookup"><span data-stu-id="3aae0-119">In hello **New Connection** window, on hello **SSL** tab, check hello **Use SSL protocol tooconnect** check box and hello **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Schermopname van tabblad voor Hallo MongoChef connection manager SSL](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="3aae0-121">Klik op Hallo **testverbinding** toovalidate Hallo verbindingsgegevens klikken, klik op **OK** tooreturn toohello nieuwe verbinding venster en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3aae0-121">Click hello **Test Connection** button toovalidate hello connection information, click **OK** tooreturn toohello New Connection window, and then click **Save**.</span></span>

    ![Schermopname van het venster Hallo MongoChef test-verbinding](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a><span data-ttu-id="3aae0-123">Gebruik MongoChef toocreate een database, de verzameling en de documenten</span><span class="sxs-lookup"><span data-stu-id="3aae0-123">Use MongoChef toocreate a database, collection, and documents</span></span>
<span data-ttu-id="3aae0-124">toocreate een database, verzameling en -documenten met MongoChef, uitvoeren Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="3aae0-124">toocreate a database, collection, and documents using MongoChef, perform hello following steps.</span></span>

1. <span data-ttu-id="3aae0-125">In **Verbindingsbeheer**, markeer Hallo verbinding en klikt u op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="3aae0-125">In **Connection Manager**, highlight hello connection and click **Connect**.</span></span>

    ![Schermopname van Hallo MongoChef Verbindingsbeheer](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="3aae0-127">Klik met de rechtermuisknop op Hallo host en kies **Database toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3aae0-127">Right click hello host and choose **Add Database**.</span></span>  <span data-ttu-id="3aae0-128">Geef de naam van een database en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3aae0-128">Provide a database name and click **OK**.</span></span>

    ![Schermopname van het Hallo databaseoptie van MongoChef toevoegen](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="3aae0-130">Klik met de rechtermuisknop op Hallo-database en kies **verzameling toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3aae0-130">Right click hello database and choose **Add Collection**.</span></span>  <span data-ttu-id="3aae0-131">Geef de naam van een verzameling en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="3aae0-131">Provide a collection name and click **Create**.</span></span>

    ![Schermopname van het Hallo MongoChef-verzameling toevoegen-optie](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="3aae0-133">Klik op Hallo **verzameling** menu item, klikt u vervolgens op **toevoegen Document**.</span><span class="sxs-lookup"><span data-stu-id="3aae0-133">Click hello **Collection** menu item, then click **Add Document**.</span></span>

    ![Schermopname van Hallo MongoChef toevoegen Document menu-item](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="3aae0-135">Plak in het dialoogvenster toevoegen Document Hallo Hallo volgende en klik op **toevoegen Document**.</span><span class="sxs-lookup"><span data-stu-id="3aae0-135">In hello Add Document dialog, paste hello following and then click **Add Document**.</span></span>

        {
        "_id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
               { "firstName": "Thomas" },
               { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "isRegistered": true
        }
6. <span data-ttu-id="3aae0-136">Deze tijd Hello na inhoud toevoegen aan een ander document.</span><span class="sxs-lookup"><span data-stu-id="3aae0-136">Add another document, this time with hello following content.</span></span>

        {
        "_id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam",
                 "givenName": "Jesse",
                "gender": "female", "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            {
                "familyName": "Miller",
                 "givenName": "Lisa",
                 "gender": "female",
                 "grade": 8 }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
        }
7. <span data-ttu-id="3aae0-137">Een voorbeeldquery uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3aae0-137">Execute a sample query.</span></span> <span data-ttu-id="3aae0-138">Bijvoorbeeld zoeken naar families met de achternaam 'Andersen' hello en return Hallo ouders en velden voor status.</span><span class="sxs-lookup"><span data-stu-id="3aae0-138">For example, search for families with hello last name 'Andersen' and return hello parents and state fields.</span></span>

    ![Schermopname van het Mongo Chef queryresultaten](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="3aae0-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3aae0-140">Next steps</span></span>
* <span data-ttu-id="3aae0-141">Verkennen Azure Cosmos DB: API voor MongoDB [voorbeelden](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3aae0-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>

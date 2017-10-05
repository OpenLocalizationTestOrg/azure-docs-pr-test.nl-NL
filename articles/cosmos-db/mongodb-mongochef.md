---
title: MongoChef gebruiken voor Azure Cosmos DB | Microsoft Docs
description: 'Informatie over het gebruik van MongoChef met een Cosmos Azure DB: API voor MongoDB-account'
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
ms.openlocfilehash: 54c9799bd646b827f602e2ea2f9a15a4fc853f00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="f07c5-104">MongoChef gebruiken met een Cosmos Azure DB: API voor MongoDB-account</span><span class="sxs-lookup"><span data-stu-id="f07c5-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="f07c5-105">Verbinding maken met een Cosmos Azure DB: de API voor MongoDB-account, moet u:</span><span class="sxs-lookup"><span data-stu-id="f07c5-105">To connect to an Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="f07c5-106">Download en installeer [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="f07c5-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="f07c5-107">Uw Azure-Cosmos-DB hebben:-API voor MongoDB account [verbindingsreeks](connect-mongodb-account.md) informatie</span><span class="sxs-lookup"><span data-stu-id="f07c5-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-the-connection-in-mongochef"></a><span data-ttu-id="f07c5-108">De verbinding in MongoChef maken</span><span class="sxs-lookup"><span data-stu-id="f07c5-108">Create the connection in MongoChef</span></span>
<span data-ttu-id="f07c5-109">Toevoegen van uw Azure-Cosmos-DB: API voor MongoDB-account zodanig in het Verbindingsbeheer MongoChef de volgende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f07c5-109">To add your Azure Cosmos DB: API for MongoDB account to the MongoChef connection manager, perform the following steps.</span></span>

1. <span data-ttu-id="f07c5-110">Ophalen van de Cosmos Azure DB:-API voor MongoDB-verbindingsgegevens van de instructies [hier](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="f07c5-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![Schermopname van de connection string-blade](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="f07c5-112">Klik op **Connect** om te openen in het Verbindingsbeheer, klikt u vervolgens op **nieuwe verbinding**</span><span class="sxs-lookup"><span data-stu-id="f07c5-112">Click **Connect** to open the Connection Manager, then click **New Connection**</span></span>

    ![Schermopname van het MongoChef Verbindingsbeheer](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="f07c5-114">In de **nieuwe verbinding** venster op de **Server** tabblad, voert u de HOST (FQDN) van de Cosmos Azure DB: API voor MongoDB-account en de poort.</span><span class="sxs-lookup"><span data-stu-id="f07c5-114">In the **New Connection** window, on the **Server** tab, enter the HOST (FQDN) of the Azure Cosmos DB: API for MongoDB account and the PORT.</span></span>

    ![Schermopname van het tabblad MongoChef connection manager-server](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="f07c5-116">In de **nieuwe verbinding** venster op de **verificatie** Kies verificatiemodus **standaard (MONGODB CR of SCARM-SHA-1)** en voer de gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="f07c5-116">In the **New Connection** window, on the **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter the USERNAME and PASSWORD.</span></span>  <span data-ttu-id="f07c5-117">Accepteer de standaard verificatie-db (admin) of geef uw eigen waarde.</span><span class="sxs-lookup"><span data-stu-id="f07c5-117">Accept the default authentication db (admin) or provide your own value.</span></span>

    ![Schermopname van het tabblad MongoChef connection manager verificatie](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="f07c5-119">In de **nieuwe verbinding** venster op de **SSL** tabblad, Controleer de **Gebruik SSL-protocol om verbinding te** selectievakje en de **accepteren van zelfondertekende SSL-certificaten van server**  keuzerondje.</span><span class="sxs-lookup"><span data-stu-id="f07c5-119">In the **New Connection** window, on the **SSL** tab, check the **Use SSL protocol to connect** check box and the **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Schermopname van het tabblad MongoChef verbinding manager SSL](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="f07c5-121">Klik op de **testverbinding** knop valideren van de verbindingsinformatie, klikt u op **OK** terug te keren naar de nieuwe verbinding en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f07c5-121">Click the **Test Connection** button to validate the connection information, click **OK** to return to the New Connection window, and then click **Save**.</span></span>

    ![Schermopname van het venster MongoChef test verbinding](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-to-create-a-database-collection-and-documents"></a><span data-ttu-id="f07c5-123">MongoChef gebruiken voor het maken van een database, de verzameling en de documenten</span><span class="sxs-lookup"><span data-stu-id="f07c5-123">Use MongoChef to create a database, collection, and documents</span></span>
<span data-ttu-id="f07c5-124">Voor het maken van een database, verzameling en -documenten met MongoChef, moet u de volgende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f07c5-124">To create a database, collection, and documents using MongoChef, perform the following steps.</span></span>

1. <span data-ttu-id="f07c5-125">In **Verbindingsbeheer**, markeer de verbinding en klikt u op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="f07c5-125">In **Connection Manager**, highlight the connection and click **Connect**.</span></span>

    ![Schermopname van het MongoChef Verbindingsbeheer](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="f07c5-127">Klik met de rechtermuisknop op de host en kies **Database toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f07c5-127">Right click the host and choose **Add Database**.</span></span>  <span data-ttu-id="f07c5-128">Geef de naam van een database en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f07c5-128">Provide a database name and click **OK**.</span></span>

    ![Schermopname van de databaseoptie MongoChef toevoegen](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="f07c5-130">Klik met de rechtermuisknop op de database en kies **verzameling toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f07c5-130">Right click the database and choose **Add Collection**.</span></span>  <span data-ttu-id="f07c5-131">Geef de naam van een verzameling en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="f07c5-131">Provide a collection name and click **Create**.</span></span>

    ![Schermopname van de optie verzameling MongoChef toevoegen](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="f07c5-133">Klik op de **verzameling** menu item, klikt u vervolgens op **toevoegen Document**.</span><span class="sxs-lookup"><span data-stu-id="f07c5-133">Click the **Collection** menu item, then click **Add Document**.</span></span>

    ![Schermopname van de menuopdracht Document MongoChef toevoegen](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="f07c5-135">Plak het volgende in het dialoogvenster Document toevoegen en klik vervolgens op **toevoegen Document**.</span><span class="sxs-lookup"><span data-stu-id="f07c5-135">In the Add Document dialog, paste the following and then click **Add Document**.</span></span>

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
6. <span data-ttu-id="f07c5-136">Deze tijd de volgende inhoud toevoegen aan een ander document.</span><span class="sxs-lookup"><span data-stu-id="f07c5-136">Add another document, this time with the following content.</span></span>

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
7. <span data-ttu-id="f07c5-137">Een voorbeeldquery uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f07c5-137">Execute a sample query.</span></span> <span data-ttu-id="f07c5-138">Bijvoorbeeld zoeken families met de naam van de laatste 'Andersen' en de bovenliggende groepen en velden voor status geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="f07c5-138">For example, search for families with the last name 'Andersen' and return the parents and state fields.</span></span>

    ![Schermopname van het Mongo Chef queryresultaten](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="f07c5-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f07c5-140">Next steps</span></span>
* <span data-ttu-id="f07c5-141">Verkennen Azure Cosmos DB: API voor MongoDB [voorbeelden](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f07c5-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>

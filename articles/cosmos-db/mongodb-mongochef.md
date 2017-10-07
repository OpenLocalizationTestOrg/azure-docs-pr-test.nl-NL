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
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a>MongoChef gebruiken met een Cosmos Azure DB: API voor MongoDB-account

tooconnect tooan Azure Cosmos DB: de API voor MongoDB-account, moet u:

* Download en installeer [MongoChef](http://3t.io/mongochef)
* Uw Azure-Cosmos-DB hebben:-API voor MongoDB account [verbindingsreeks](connect-mongodb-account.md) informatie

## <a name="create-hello-connection-in-mongochef"></a>Hallo verbinding maken in MongoChef
tooadd uw Cosmos Azure DB: API voor MongoDB account toohello MongoChef Verbindingsbeheer uitvoeren Hallo stappen te volgen.

1. Ophalen van de Cosmos Azure DB:-API voor MongoDB-verbindingsgegevens Hallo instructies [hier](connect-mongodb-account.md).

    ![Schermopname van Hallo connection string-blade](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. Klik op **Connect** tooopen Hallo Connection Manager en klik vervolgens op **nieuwe verbinding**

    ![Schermopname van Hallo MongoChef Verbindingsbeheer](./media/mongodb-mongochef/ConnectionManager.png)
3. In Hallo **nieuwe verbinding** venster op Hallo **Server** tabblad, voert u Hallo HOST (FQDN) van hello Azure Cosmos DB:-API voor MongoDB-account en het Hallo-poort.

    ![Schermopname van tabblad voor Hallo MongoChef connection manager-server](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. In Hallo **nieuwe verbinding** venster op Hallo **verificatie** Kies verificatiemodus **standaard (MONGODB CR of SCARM-SHA-1)** en Hallo gebruikersnaam invoeren en HET WACHTWOORD.  Accepteer Hallo standaard verificatie db (admin) of geef uw eigen waarde.

    ![Schermopname van tabblad voor verificatie van Hallo MongoChef connection manager](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. In Hallo **nieuwe verbinding** venster op Hallo **SSL** tabblad, controleert u Hallo **Gebruik SSL-protocol tooconnect** selectievakje en Hallo **accepteren server zelfondertekend SSL certificaten** keuzerondje.

    ![Schermopname van tabblad voor Hallo MongoChef connection manager SSL](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. Klik op Hallo **testverbinding** toovalidate Hallo verbindingsgegevens klikken, klik op **OK** tooreturn toohello nieuwe verbinding venster en klik vervolgens op **opslaan**.

    ![Schermopname van het venster Hallo MongoChef test-verbinding](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a>Gebruik MongoChef toocreate een database, de verzameling en de documenten
toocreate een database, verzameling en -documenten met MongoChef, uitvoeren Hallo stappen te volgen.

1. In **Verbindingsbeheer**, markeer Hallo verbinding en klikt u op **Connect**.

    ![Schermopname van Hallo MongoChef Verbindingsbeheer](./media/mongodb-mongochef/ConnectToAccount.png)
2. Klik met de rechtermuisknop op Hallo host en kies **Database toevoegen**.  Geef de naam van een database en klik op **OK**.

    ![Schermopname van het Hallo databaseoptie van MongoChef toevoegen](./media/mongodb-mongochef/AddDatabase1.png)
3. Klik met de rechtermuisknop op Hallo-database en kies **verzameling toevoegen**.  Geef de naam van een verzameling en klik op **maken**.

    ![Schermopname van het Hallo MongoChef-verzameling toevoegen-optie](./media/mongodb-mongochef/AddCollection.png)
4. Klik op Hallo **verzameling** menu item, klikt u vervolgens op **toevoegen Document**.

    ![Schermopname van Hallo MongoChef toevoegen Document menu-item](./media/mongodb-mongochef/AddDocument1.png)
5. Plak in het dialoogvenster toevoegen Document Hallo Hallo volgende en klik op **toevoegen Document**.

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
6. Deze tijd Hello na inhoud toevoegen aan een ander document.

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
7. Een voorbeeldquery uitvoeren. Bijvoorbeeld zoeken naar families met de achternaam 'Andersen' hello en return Hallo ouders en velden voor status.

    ![Schermopname van het Mongo Chef queryresultaten](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a>Volgende stappen
* Verkennen Azure Cosmos DB: API voor MongoDB [voorbeelden](mongodb-samples.md).

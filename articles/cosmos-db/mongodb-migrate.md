---
title: aaaUse mongoimport en mongorestore met hello Azure Cosmos DB-API voor MongoDB | Microsoft Docs
description: Meer informatie over hoe toouse mongoimport en mongorestore tooimport gegevens tooan API voor MongoDB-account
keywords: mongoimport, mongorestore
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
ms.date: 06/12/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 921354bc7b09a076a73e0cbf5e4aabcc9e83d5a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a>Azure Cosmos DB: Import MongoDB-gegevens 

toomigrate gegevens van MongoDB tooan Azure DB die Cosmos-account voor gebruik met de Hallo API voor MongoDB, moet u:

* Download een *mongoimport.exe* of *mongorestore.exe* van Hallo [MongoDB-Downloadcentrum](https://www.mongodb.com/download-center).
* Ophalen van uw [-API voor MongoDB-verbindingsreeks](connect-mongodb-account.md).

Als u gegevens importeert uit MongoDB en plan toouse met Azure Cosmos DB hello, moet u Hallo [hulpprogramma voor gegevensmigratie](import-data.md) tooimport gegevens.

Deze zelfstudie behandelt Hallo taken te volgen:

> [!div class="checklist"]
> * Bij het ophalen van de verbindingsreeks
> * MongoDB-gegevens importeren met behulp van mongoimport
> * MongoDB-gegevens importeren met behulp van mongorestore

## <a name="prerequisites"></a>Vereisten

* Verhoogt de doorvoer: Hallo duur van de migratie, is afhankelijk van Hallo hoeveelheid doorvoer die u voor uw verzamelingen instellen. Ervoor tooincrease Hallo doorvoer voor grotere gegevens migraties worden. Nadat u Hallo migratie hebt voltooid, kunt u Hallo doorvoer toosave kosten verlagen. Voor meer informatie over de toenemende doorvoer in Hallo [Azure-portal](https://portal.azure.com), Zie [prestatieniveaus en prijscategorieën in Azure Cosmos DB](performance-levels.md).

* Schakel SSL: Azure Cosmos DB heeft strenge beveiligingsvereisten en standaarden. Ervoor tooenable SSL zijn wanneer u met uw account communiceert. Hallo procedures in de rest van het artikel Hallo Hallo omvatten hoe tooenable SSL voor mongoimport en mongorestore.

## <a name="find-your-connection-string-information-host-port-username-and-password"></a>Verbindingsreeksgegevens (host, poort, gebruikersnaam en wachtwoord) vinden

1. In Hallo [Azure-portal](https://portal.azure.com), in linkerdeelvenster hello, klik op Hallo **Azure Cosmos DB** vermelding.
2. In Hallo **abonnementen** deelvenster, selecteer de accountnaam van uw.
3. In Hallo **verbindingsreeks** blade, klikt u op **verbindingsreeks**.  
Hallo rechter deelvenster bevat alle Hallo-gegevens die u nodig hebt toosuccessfully tooyour-account koppelen.

    ![Connection String-blade](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a>Gegevens toohello API voor MongoDB importeren met behulp van mongoimport

tooimport gegevens tooyour Azure DB die Cosmos-account gebruiken Hallo sjabloon te volgen. Vul *host*, *gebruikersnaam*, en *wachtwoord* met Hallo-waarden die specifieke tooyour account zijn.  

Sjabloon:

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

Voorbeeld:  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a>Gegevens toohello API voor MongoDB importeren met behulp van mongorestore

toorestore gegevens tooyour API voor MongoDB-account gebruiken Hallo Hallo importeren van een servicesjabloon tooexecute te volgen. Vul *host*, *gebruikersnaam*, en *wachtwoord* met Hallo-waarden die specifieke tooyour account zijn.

Sjabloon:

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

Voorbeeld:

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a>Handleiding voor een succesvolle migratie

1. Vooraf maken en schalen van uw verzamelingen:
        
    * Standaard levert Azure Cosmos DB een nieuwe verzameling MongoDB met 1000 aanvraageenheden (RUs). Voordat u Hallo migratie begint met behulp van mongoimport, mongorestore of mongomirror, vooraf maken van alle verzamelingen van Hallo [Azure-portal](https://portal.azure.com) of van MongoDB-stuurprogramma's en hulpprogramma's. Als uw verzameling groter dan 10 GB is, zorg ervoor dat toocreate een [shard/gepartitioneerd verzameling](partition-data.md) met een juiste shard-sleutel.

    * Van Hallo [Azure-portal](https://portal.azure.com), uw verzamelingen doorvoer van 1000 RUs voor een verzameling van één partitie en 2500 RUs voor een verzameling shard voor migratie van Hallo verhogen. Met hogere doorvoer hello, kunt u voorkomen bandbreedtebeperking en migreer in minder tijd. Met elk uur facturering in Azure Cosmos DB, kunt u Hallo doorvoer onmiddellijk na Hallo migratie toosave kosten verminderen.

2. Hallo geschatte RU kosten voor een schrijfbewerking voor één document berekenen:

    a. Sluit tooyour Azure Cosmos DB MongoDB-database van Hallo MongoDB-Shell. U vindt instructies in [verbinding maken met een MongoDB toepassing tooAzure Cosmos DB](connect-mongodb-account.md).
    
    b. Een voorbeeld van een opdracht insert uitvoeren via een van uw voorbeelddocumenten van Hallo MongoDB-Shell:
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    c. Voer ```db.runCommand({getLastRequestStatistics: 1})``` en ontvangt u een antwoord zoals deze:
     
        ```
        globaldb:PRIMARY> db.runCommand({getLastRequestStatistics: 1})
        {
            "_t": "GetRequestStatisticsResponse",
            "ok": 1,
            "CommandName": "insert",
            "RequestCharge": 10,
            "RequestDurationInMilliSeconds": NumberLong(50)
        }
        ```
        
    d. Let op Hallo aanvraag kosten.
    
3. Hallo latentie van uw machine toohello Cosmos-DB Azure cloudservice bepalen:
    
    a. Uitgebreide logboekregistratie van Hallo MongoDB-Shell inschakelen met behulp van deze opdracht:```setVerboseShell(true)```
    
    b. Een eenvoudige query uitvoeren op database Hallo: ```db.coll.find().limit(1)```. U ontvangt een antwoord zoals deze:

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. Hallo ingevoegd document voordat Hallo migratie tooensure dat er geen dubbele documenten zijn verwijderen. Met deze opdracht kunt u documenten:```db.coll.remove({})```

5. Hallo geschatte berekenen *batchSize* en *numInsertionWorkers* waarden:

    * Voor *batchSize*, delen Hallo totaal ingericht RUs door Hallo RUs verbruikt van uw schrijven voor één document in stap 3.
    
    * Als Hallo berekend *batchSize* < = 24, gebruikt u dat nummer als uw *batchSize* waarde.
    
    * Als Hallo berekend *batchSize* > 24, set Hallo *batchSize* too24 waarde.
    
    * Voor *numInsertionWorkers*, gebruiken deze vergelijking: *numInsertionWorkers = (ingerichte doorvoer * latentie in seconden) / (batchgrootte * RUs verbruikt voor een enkele schrijven)*.
        
    |Eigenschap|Waarde|
    |--------|-----|
    |batchSize| 24 |
    |RUs ingericht | 10.000 |
    |Latentie | 0.100 s |
    |RU in rekening gebracht voor 1 doc schrijven | 10 RUs |
    |numInsertionWorkers | ? |
    
    *numInsertionWorkers = (10000 RUs x 0,1 s) / (24 x 10 RUs) 4.1666 =*

6. Hallo uiteindelijke migratie opdracht uitvoeren:

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a>Volgende stappen

U kunt de volgende zelfstudie toohello gaan en meer informatie hoe tooquery MongoDB-gegevens met behulp van Azure Cosmos DB. 

> [!div class="nextstepaction"]
>[Hoe tooquery MongoDB gegevens?](../cosmos-db/tutorial-query-mongodb.md)

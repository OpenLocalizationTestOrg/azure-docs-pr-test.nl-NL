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
# <a name="azure-cosmos-db-import-mongodb-data"></a><span data-ttu-id="8938d-104">Azure Cosmos DB: Import MongoDB-gegevens</span><span class="sxs-lookup"><span data-stu-id="8938d-104">Azure Cosmos DB: Import MongoDB data</span></span> 

<span data-ttu-id="8938d-105">toomigrate gegevens van MongoDB tooan Azure DB die Cosmos-account voor gebruik met de Hallo API voor MongoDB, moet u:</span><span class="sxs-lookup"><span data-stu-id="8938d-105">toomigrate data from MongoDB tooan Azure Cosmos DB account for use with hello API for MongoDB, you must:</span></span>

* <span data-ttu-id="8938d-106">Download een *mongoimport.exe* of *mongorestore.exe* van Hallo [MongoDB-Downloadcentrum](https://www.mongodb.com/download-center).</span><span class="sxs-lookup"><span data-stu-id="8938d-106">Download either *mongoimport.exe* or *mongorestore.exe* from hello [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="8938d-107">Ophalen van uw [-API voor MongoDB-verbindingsreeks](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="8938d-107">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="8938d-108">Als u gegevens importeert uit MongoDB en plan toouse met Azure Cosmos DB hello, moet u Hallo [hulpprogramma voor gegevensmigratie](import-data.md) tooimport gegevens.</span><span class="sxs-lookup"><span data-stu-id="8938d-108">If you are importing data from MongoDB and plan toouse it with hello Azure Cosmos DB, you should use hello [Data Migration tool](import-data.md) tooimport data.</span></span>

<span data-ttu-id="8938d-109">Deze zelfstudie behandelt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="8938d-109">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8938d-110">Bij het ophalen van de verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="8938d-110">Retrieving your connection string</span></span>
> * <span data-ttu-id="8938d-111">MongoDB-gegevens importeren met behulp van mongoimport</span><span class="sxs-lookup"><span data-stu-id="8938d-111">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="8938d-112">MongoDB-gegevens importeren met behulp van mongorestore</span><span class="sxs-lookup"><span data-stu-id="8938d-112">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8938d-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8938d-113">Prerequisites</span></span>

* <span data-ttu-id="8938d-114">Verhoogt de doorvoer: Hallo duur van de migratie, is afhankelijk van Hallo hoeveelheid doorvoer die u voor uw verzamelingen instellen.</span><span class="sxs-lookup"><span data-stu-id="8938d-114">Increase throughput: hello duration of your data migration depends on hello amount of throughput you set up for your collections.</span></span> <span data-ttu-id="8938d-115">Ervoor tooincrease Hallo doorvoer voor grotere gegevens migraties worden.</span><span class="sxs-lookup"><span data-stu-id="8938d-115">Be sure tooincrease hello throughput for larger data migrations.</span></span> <span data-ttu-id="8938d-116">Nadat u Hallo migratie hebt voltooid, kunt u Hallo doorvoer toosave kosten verlagen.</span><span class="sxs-lookup"><span data-stu-id="8938d-116">After you've completed hello migration, decrease hello throughput toosave costs.</span></span> <span data-ttu-id="8938d-117">Voor meer informatie over de toenemende doorvoer in Hallo [Azure-portal](https://portal.azure.com), Zie [prestatieniveaus en prijscategorieën in Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="8938d-117">For more information about increasing throughput in hello [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="8938d-118">Schakel SSL: Azure Cosmos DB heeft strenge beveiligingsvereisten en standaarden.</span><span class="sxs-lookup"><span data-stu-id="8938d-118">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="8938d-119">Ervoor tooenable SSL zijn wanneer u met uw account communiceert.</span><span class="sxs-lookup"><span data-stu-id="8938d-119">Be sure tooenable SSL when you interact with your account.</span></span> <span data-ttu-id="8938d-120">Hallo procedures in de rest van het artikel Hallo Hallo omvatten hoe tooenable SSL voor mongoimport en mongorestore.</span><span class="sxs-lookup"><span data-stu-id="8938d-120">hello procedures in hello rest of hello article include how tooenable SSL for mongoimport and mongorestore.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="8938d-121">Verbindingsreeksgegevens (host, poort, gebruikersnaam en wachtwoord) vinden</span><span class="sxs-lookup"><span data-stu-id="8938d-121">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="8938d-122">In Hallo [Azure-portal](https://portal.azure.com), in linkerdeelvenster hello, klik op Hallo **Azure Cosmos DB** vermelding.</span><span class="sxs-lookup"><span data-stu-id="8938d-122">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Cosmos DB** entry.</span></span>
2. <span data-ttu-id="8938d-123">In Hallo **abonnementen** deelvenster, selecteer de accountnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="8938d-123">In hello **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="8938d-124">In Hallo **verbindingsreeks** blade, klikt u op **verbindingsreeks**.</span><span class="sxs-lookup"><span data-stu-id="8938d-124">In hello **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="8938d-125">Hallo rechter deelvenster bevat alle Hallo-gegevens die u nodig hebt toosuccessfully tooyour-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="8938d-125">hello right pane contains all hello information that you need toosuccessfully connect tooyour account.</span></span>

    ![Connection String-blade](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a><span data-ttu-id="8938d-127">Gegevens toohello API voor MongoDB importeren met behulp van mongoimport</span><span class="sxs-lookup"><span data-stu-id="8938d-127">Import data toohello API for MongoDB by using mongoimport</span></span>

<span data-ttu-id="8938d-128">tooimport gegevens tooyour Azure DB die Cosmos-account gebruiken Hallo sjabloon te volgen.</span><span class="sxs-lookup"><span data-stu-id="8938d-128">tooimport data tooyour Azure Cosmos DB account, use hello following template.</span></span> <span data-ttu-id="8938d-129">Vul *host*, *gebruikersnaam*, en *wachtwoord* met Hallo-waarden die specifieke tooyour account zijn.</span><span class="sxs-lookup"><span data-stu-id="8938d-129">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>  

<span data-ttu-id="8938d-130">Sjabloon:</span><span class="sxs-lookup"><span data-stu-id="8938d-130">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="8938d-131">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8938d-131">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a><span data-ttu-id="8938d-132">Gegevens toohello API voor MongoDB importeren met behulp van mongorestore</span><span class="sxs-lookup"><span data-stu-id="8938d-132">Import data toohello API for MongoDB by using mongorestore</span></span>

<span data-ttu-id="8938d-133">toorestore gegevens tooyour API voor MongoDB-account gebruiken Hallo Hallo importeren van een servicesjabloon tooexecute te volgen.</span><span class="sxs-lookup"><span data-stu-id="8938d-133">toorestore data tooyour API for MongoDB account, use hello following template tooexecute hello import.</span></span> <span data-ttu-id="8938d-134">Vul *host*, *gebruikersnaam*, en *wachtwoord* met Hallo-waarden die specifieke tooyour account zijn.</span><span class="sxs-lookup"><span data-stu-id="8938d-134">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>

<span data-ttu-id="8938d-135">Sjabloon:</span><span class="sxs-lookup"><span data-stu-id="8938d-135">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="8938d-136">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8938d-136">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a><span data-ttu-id="8938d-137">Handleiding voor een succesvolle migratie</span><span class="sxs-lookup"><span data-stu-id="8938d-137">Guide for a successful migration</span></span>

1. <span data-ttu-id="8938d-138">Vooraf maken en schalen van uw verzamelingen:</span><span class="sxs-lookup"><span data-stu-id="8938d-138">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="8938d-139">Standaard levert Azure Cosmos DB een nieuwe verzameling MongoDB met 1000 aanvraageenheden (RUs).</span><span class="sxs-lookup"><span data-stu-id="8938d-139">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units (RUs).</span></span> <span data-ttu-id="8938d-140">Voordat u Hallo migratie begint met behulp van mongoimport, mongorestore of mongomirror, vooraf maken van alle verzamelingen van Hallo [Azure-portal](https://portal.azure.com) of van MongoDB-stuurprogramma's en hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="8938d-140">Before you start hello migration by using mongoimport, mongorestore, or mongomirror, pre-create all your collections from hello [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="8938d-141">Als uw verzameling groter dan 10 GB is, zorg ervoor dat toocreate een [shard/gepartitioneerd verzameling](partition-data.md) met een juiste shard-sleutel.</span><span class="sxs-lookup"><span data-stu-id="8938d-141">If your collection is greater than 10 GB, make sure toocreate a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="8938d-142">Van Hallo [Azure-portal](https://portal.azure.com), uw verzamelingen doorvoer van 1000 RUs voor een verzameling van één partitie en 2500 RUs voor een verzameling shard voor migratie van Hallo verhogen.</span><span class="sxs-lookup"><span data-stu-id="8938d-142">From hello [Azure portal](https://portal.azure.com), increase your collections' throughput from 1,000 RUs for a single partition collection and 2,500 RUs for a sharded collection just for hello migration.</span></span> <span data-ttu-id="8938d-143">Met hogere doorvoer hello, kunt u voorkomen bandbreedtebeperking en migreer in minder tijd.</span><span class="sxs-lookup"><span data-stu-id="8938d-143">With hello higher throughput, you can avoid throttling and migrate in less time.</span></span> <span data-ttu-id="8938d-144">Met elk uur facturering in Azure Cosmos DB, kunt u Hallo doorvoer onmiddellijk na Hallo migratie toosave kosten verminderen.</span><span class="sxs-lookup"><span data-stu-id="8938d-144">With hourly billing in Azure Cosmos DB, you can reduce hello throughput immediately after hello migration toosave costs.</span></span>

2. <span data-ttu-id="8938d-145">Hallo geschatte RU kosten voor een schrijfbewerking voor één document berekenen:</span><span class="sxs-lookup"><span data-stu-id="8938d-145">Calculate hello approximate RU charge for a single document write:</span></span>

    <span data-ttu-id="8938d-146">a.</span><span class="sxs-lookup"><span data-stu-id="8938d-146">a.</span></span> <span data-ttu-id="8938d-147">Sluit tooyour Azure Cosmos DB MongoDB-database van Hallo MongoDB-Shell.</span><span class="sxs-lookup"><span data-stu-id="8938d-147">Connect tooyour Azure Cosmos DB MongoDB database from hello MongoDB Shell.</span></span> <span data-ttu-id="8938d-148">U vindt instructies in [verbinding maken met een MongoDB toepassing tooAzure Cosmos DB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="8938d-148">You can find instructions in [Connect a MongoDB application tooAzure Cosmos DB](connect-mongodb-account.md).</span></span>
    
    <span data-ttu-id="8938d-149">b.</span><span class="sxs-lookup"><span data-stu-id="8938d-149">b.</span></span> <span data-ttu-id="8938d-150">Een voorbeeld van een opdracht insert uitvoeren via een van uw voorbeelddocumenten van Hallo MongoDB-Shell:</span><span class="sxs-lookup"><span data-stu-id="8938d-150">Run a sample insert command by using one of your sample documents from hello MongoDB Shell:</span></span>
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    <span data-ttu-id="8938d-151">c.</span><span class="sxs-lookup"><span data-stu-id="8938d-151">c.</span></span> <span data-ttu-id="8938d-152">Voer ```db.runCommand({getLastRequestStatistics: 1})``` en ontvangt u een antwoord zoals deze:</span><span class="sxs-lookup"><span data-stu-id="8938d-152">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you will receive a response like this one:</span></span>
     
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
        
    <span data-ttu-id="8938d-153">d.</span><span class="sxs-lookup"><span data-stu-id="8938d-153">d.</span></span> <span data-ttu-id="8938d-154">Let op Hallo aanvraag kosten.</span><span class="sxs-lookup"><span data-stu-id="8938d-154">Take note of hello request charge.</span></span>
    
3. <span data-ttu-id="8938d-155">Hallo latentie van uw machine toohello Cosmos-DB Azure cloudservice bepalen:</span><span class="sxs-lookup"><span data-stu-id="8938d-155">Determine hello latency from your machine toohello Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="8938d-156">a.</span><span class="sxs-lookup"><span data-stu-id="8938d-156">a.</span></span> <span data-ttu-id="8938d-157">Uitgebreide logboekregistratie van Hallo MongoDB-Shell inschakelen met behulp van deze opdracht:```setVerboseShell(true)```</span><span class="sxs-lookup"><span data-stu-id="8938d-157">Enable verbose logging from hello MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="8938d-158">b.</span><span class="sxs-lookup"><span data-stu-id="8938d-158">b.</span></span> <span data-ttu-id="8938d-159">Een eenvoudige query uitvoeren op database Hallo: ```db.coll.find().limit(1)```.</span><span class="sxs-lookup"><span data-stu-id="8938d-159">Run a simple query against hello database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="8938d-160">U ontvangt een antwoord zoals deze:</span><span class="sxs-lookup"><span data-stu-id="8938d-160">You will receive a response like this one:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. <span data-ttu-id="8938d-161">Hallo ingevoegd document voordat Hallo migratie tooensure dat er geen dubbele documenten zijn verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8938d-161">Remove hello inserted document before hello migration tooensure that there are no duplicate documents.</span></span> <span data-ttu-id="8938d-162">Met deze opdracht kunt u documenten:```db.coll.remove({})```</span><span class="sxs-lookup"><span data-stu-id="8938d-162">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

5. <span data-ttu-id="8938d-163">Hallo geschatte berekenen *batchSize* en *numInsertionWorkers* waarden:</span><span class="sxs-lookup"><span data-stu-id="8938d-163">Calculate hello approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="8938d-164">Voor *batchSize*, delen Hallo totaal ingericht RUs door Hallo RUs verbruikt van uw schrijven voor één document in stap 3.</span><span class="sxs-lookup"><span data-stu-id="8938d-164">For *batchSize*, divide hello total provisioned RUs by hello RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="8938d-165">Als Hallo berekend *batchSize* < = 24, gebruikt u dat nummer als uw *batchSize* waarde.</span><span class="sxs-lookup"><span data-stu-id="8938d-165">If hello calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="8938d-166">Als Hallo berekend *batchSize* > 24, set Hallo *batchSize* too24 waarde.</span><span class="sxs-lookup"><span data-stu-id="8938d-166">If hello calculated *batchSize* > 24, set hello *batchSize* value too24.</span></span>
    
    * <span data-ttu-id="8938d-167">Voor *numInsertionWorkers*, gebruiken deze vergelijking: *numInsertionWorkers = (ingerichte doorvoer * latentie in seconden) / (batchgrootte * RUs verbruikt voor een enkele schrijven)*.</span><span class="sxs-lookup"><span data-stu-id="8938d-167">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput * latency in seconds) / (batch size * consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="8938d-168">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="8938d-168">Property</span></span>|<span data-ttu-id="8938d-169">Waarde</span><span class="sxs-lookup"><span data-stu-id="8938d-169">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="8938d-170">batchSize</span><span class="sxs-lookup"><span data-stu-id="8938d-170">batchSize</span></span>| <span data-ttu-id="8938d-171">24</span><span class="sxs-lookup"><span data-stu-id="8938d-171">24</span></span> |
    |<span data-ttu-id="8938d-172">RUs ingericht</span><span class="sxs-lookup"><span data-stu-id="8938d-172">RUs provisioned</span></span> | <span data-ttu-id="8938d-173">10.000</span><span class="sxs-lookup"><span data-stu-id="8938d-173">10000</span></span> |
    |<span data-ttu-id="8938d-174">Latentie</span><span class="sxs-lookup"><span data-stu-id="8938d-174">Latency</span></span> | <span data-ttu-id="8938d-175">0.100 s</span><span class="sxs-lookup"><span data-stu-id="8938d-175">0.100 s</span></span> |
    |<span data-ttu-id="8938d-176">RU in rekening gebracht voor 1 doc schrijven</span><span class="sxs-lookup"><span data-stu-id="8938d-176">RU charged for 1 doc write</span></span> | <span data-ttu-id="8938d-177">10 RUs</span><span class="sxs-lookup"><span data-stu-id="8938d-177">10 RUs</span></span> |
    |<span data-ttu-id="8938d-178">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="8938d-178">numInsertionWorkers</span></span> | <span data-ttu-id="8938d-179">?</span><span class="sxs-lookup"><span data-stu-id="8938d-179">?</span></span> |
    
    <span data-ttu-id="8938d-180">*numInsertionWorkers = (10000 RUs x 0,1 s) / (24 x 10 RUs) 4.1666 =*</span><span class="sxs-lookup"><span data-stu-id="8938d-180">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

6. <span data-ttu-id="8938d-181">Hallo uiteindelijke migratie opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8938d-181">Run hello final migration command:</span></span>

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="8938d-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8938d-182">Next steps</span></span>

<span data-ttu-id="8938d-183">U kunt de volgende zelfstudie toohello gaan en meer informatie hoe tooquery MongoDB-gegevens met behulp van Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8938d-183">You can proceed toohello next tutorial and learn how tooquery MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="8938d-184">Hoe tooquery MongoDB gegevens?</span><span class="sxs-lookup"><span data-stu-id="8938d-184">How tooquery MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)

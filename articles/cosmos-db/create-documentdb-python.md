---
title: 'Azure Cosmos DB: Bouwen van een app met behulp van Python en DocumentDB API Hallo | Microsoft Docs'
description: Geeft een Python-codevoorbeeld kunt u tooconnect tooand query hello Azure Cosmos DB DocumentDB-API
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 51c11be2-af6d-425f-a86a-39cbfe61da29
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 05/13/2017
ms.author: mimig
ms.openlocfilehash: e66965ab493c6ef693e88a3767a401d39e1bde2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-hello-azure-portal"></a><span data-ttu-id="aa6f6-103">Azure Cosmos DB: Een DocumentDB-API-App met behulp van Python en hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="aa6f6-103">Azure Cosmos DB: Build a DocumentDB API app with Python and hello Azure portal</span></span>

<span data-ttu-id="aa6f6-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="aa6f6-105">U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="aa6f6-106">Deze snel starten laat zien hoe Hallo toocreate een Cosmos-DB Azure-account, documentdatabase en verzameling met behulp van Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="aa6f6-107">U vervolgens bouwen en uitvoeren van een console-app die is gebouwd op Hallo [DocumentDB Python API](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="aa6f6-107">You then build and run a console app built on hello [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa6f6-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="aa6f6-108">Prerequisites</span></span>

* <span data-ttu-id="aa6f6-109">Voordat u dit voorbeeld uitvoeren kunt, hebt u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="aa6f6-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="aa6f6-110">[Visual Studio 2015](http://www.visualstudio.com/) of hoger.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="aa6f6-111">Python Tools for Visual Studio van [GitHub](http://microsoft.github.io/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="aa6f6-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="aa6f6-112">In deze zelfstudie wordt gebruikgemaakt van Python Tools for VS 2015.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="aa6f6-113">Python 2.7 van [python.org](https://www.python.org/downloads/release/python-2712/)</span><span class="sxs-lookup"><span data-stu-id="aa6f6-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="aa6f6-114">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="aa6f6-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="aa6f6-115">Een verzameling toevoegen</span><span class="sxs-lookup"><span data-stu-id="aa6f6-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="aa6f6-116">Hallo-voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="aa6f6-116">Clone hello sample application</span></span>

<span data-ttu-id="aa6f6-117">Nu we de kloon een DocumentDB-API-app vanuit github Hallo verbindingsreeks instellen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-117">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="aa6f6-118">U ziet hoe eenvoudig het is toowork met gegevens via een programma.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-118">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="aa6f6-119">Open een git-terminalvenster zoals git bash en en `cd` tooa werkmap.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="aa6f6-120">Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-120">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-hello-code"></a><span data-ttu-id="aa6f6-121">Hallo code bekijken</span><span class="sxs-lookup"><span data-stu-id="aa6f6-121">Review hello code</span></span>

<span data-ttu-id="aa6f6-122">We maken een kort overzicht van wat in Hallo-app gebeurt er.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="aa6f6-123">Open Hallo DocumentDBGetStarted.py bestands- en u vindt dat deze regels code hello Azure Cosmos DB resources maken.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-123">Open hello DocumentDBGetStarted.py file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="aa6f6-124">Hallo DocumentClient is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-124">hello DocumentClient is initialized.</span></span>

    ```python
    # Initialize hello Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="aa6f6-125">Er wordt een nieuwe database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="aa6f6-126">Er wordt een nieuwe verzameling gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-126">A new collection is created.</span></span>

    ```python
    # Create collection options
    options = {
        'offerEnableRUPerMinuteThroughput': True,
        'offerVersion': "V2",
        'offerThroughput': 400
    }

    # Create a collection
    collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)
    ```

* <span data-ttu-id="aa6f6-127">Er wordt een aantal documenten gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-127">Some documents are created.</span></span>

    ```python
    # Create some documents
    document1 = client.CreateDocument(collection['_self'],
        { 
            'id': 'server1',
            'Web Site': 0,
            'Cloud Service': 0,
            'Virtual Machine': 0,
            'name': 'some' 
        })
    ```

* <span data-ttu-id="aa6f6-128">Een query wordt uitgevoerd met behulp van SQL.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-128">A query is performed using SQL</span></span>

    ```python
    # Query them in SQL
    query = { 'query': 'SELECT * FROM server s' }    
            
    options = {} 
    options['enableCrossPartitionQuery'] = True
    options['maxItemCount'] = 2

    result_iterable = client.QueryDocuments(collection['_self'], query, options)
    results = list(result_iterable);

    print(results)
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="aa6f6-129">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="aa6f6-129">Update your connection string</span></span>

<span data-ttu-id="aa6f6-130">Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-130">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="aa6f6-131">In Hallo [Azure-portal](http://portal.azure.com/), in uw Azure DB-Cosmos-account, klik op in de linkernavigatiebalk Hallo **sleutels**, en klik vervolgens op **lezen-schrijven sleutels**.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-131">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="aa6f6-132">U Hallo kopie knoppen op de rechterkant Hallo Hallo scherm toocopy Hallo URI en primaire sleutel in Hallo `DocumentDBGetStarted.py` bestand in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-132">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `DocumentDBGetStarted.py` file in hello next step.</span></span>

    ![Bekijken en kopiëren van een toegangssleutel in hello Azure-portal, de blade sleutels](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="aa6f6-134">In Open Hallo `DocumentDBGetStarted.py` bestand.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-134">In Open hello `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="aa6f6-135">Kopieer de waarde van de URI van Hallo-portal (met behulp van de knop kopiëren Hallo), waardoor het Hallo Hallo eindpunt sleutelwaarde in `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-135">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="aa6f6-136">Vervolgens kopieert u de waarde van de primaire sleutel van Hallo-portal en deze waarde Hallo Hallo `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-136">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="aa6f6-137">U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-137">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="aa6f6-138">Hallo-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="aa6f6-138">Run hello app</span></span>
1. <span data-ttu-id="aa6f6-139">In Visual Studio met de rechtermuisknop op Hallo-project in **Solution Explorer**, selecteer Hallo huidige Python-omgeving en klik met de rechtermuisknop.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-139">In Visual Studio, right-click on hello project in **Solution Explorer**, select hello current Python environment, then right click.</span></span>

2. <span data-ttu-id="aa6f6-140">Selecteer Python-pakket installeren en typ vervolgens **pydocumentdb**</span><span class="sxs-lookup"><span data-stu-id="aa6f6-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="aa6f6-141">F5 toorun Hallo toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-141">Run F5 toorun hello application.</span></span> <span data-ttu-id="aa6f6-142">Uw app wordt in uw browser weergegeven.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="aa6f6-143">U kunt nu gaat u terug tooData Explorer en Zie query, wijzigen en werken met deze nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-143">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="aa6f6-144">Sla's bekijken in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="aa6f6-144">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="aa6f6-145">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="aa6f6-145">Clean up resources</span></span>

<span data-ttu-id="aa6f6-146">Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="aa6f6-146">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="aa6f6-147">Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-147">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="aa6f6-148">Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-148">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa6f6-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aa6f6-149">Next steps</span></span>

<span data-ttu-id="aa6f6-150">In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account, een verzameling met Hallo Data Explorer maken en uitvoeren van een app.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-150">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="aa6f6-151">U kunt nu aanvullende gegevens tooyour Cosmos DB account importeren.</span><span class="sxs-lookup"><span data-stu-id="aa6f6-151">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa6f6-152">Gegevens importeren in Azure Cosmos DB voor Hallo DocumentDB-API</span><span class="sxs-lookup"><span data-stu-id="aa6f6-152">Import data into Azure Cosmos DB for hello DocumentDB API</span></span>](import-data.md)



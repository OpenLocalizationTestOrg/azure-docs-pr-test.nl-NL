---
title: 'Azure Cosmos DB: een toepassing bouwen met Python en de DocumentDB API | Microsoft Docs'
description: "Biedt een voorbeeld van Python-code dat u kunt gebruiken om verbinding te maken met de DocumentDB API van Azure Cosmos DB en er query’s op uit te voeren"
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
ms.openlocfilehash: 08d467ea27484e7d1d07d6c21b2e04b6525fbcd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-the-azure-portal"></a><span data-ttu-id="e4360-103">Azure Cosmos DB: een DocumentDB API-app bouwen met Python en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e4360-103">Azure Cosmos DB: Build a DocumentDB API app with Python and the Azure portal</span></span>

<span data-ttu-id="e4360-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e4360-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="e4360-105">U kunt snel databases maken van documenten, sleutel/waarde-paren en grafieken en hier query’s op uitvoeren. Deze databases genieten allemaal het voordeel van de globale distributie en horizontale schaalmogelijkheden die ten grondslag liggen aan Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e4360-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="e4360-106">Deze Quick Start laat zien hoe u een Azure Cosmos DB-account, een documentdatabase en een verzameling kunt maken met behulp van Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e4360-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="e4360-107">Vervolgens ontwikkelt u een console-app die is gebouwd op de [DocumentDB Python-API](documentdb-sdk-python.md) en voert u deze uit.</span><span class="sxs-lookup"><span data-stu-id="e4360-107">You then build and run a console app built on the [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4360-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e4360-108">Prerequisites</span></span>

* <span data-ttu-id="e4360-109">Voordat u met dit voorbeeld aan de slag gaat, moet u aan de volgende vereisten voldoen:</span><span class="sxs-lookup"><span data-stu-id="e4360-109">Before you can run this sample, you must have the following prerequisites:</span></span>
    * <span data-ttu-id="e4360-110">[Visual Studio 2015](http://www.visualstudio.com/) of hoger.</span><span class="sxs-lookup"><span data-stu-id="e4360-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="e4360-111">Python Tools for Visual Studio van [GitHub](http://microsoft.github.io/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="e4360-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="e4360-112">In deze zelfstudie wordt gebruikgemaakt van Python Tools for VS 2015.</span><span class="sxs-lookup"><span data-stu-id="e4360-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="e4360-113">Python 2.7 van [python.org](https://www.python.org/downloads/release/python-2712/)</span><span class="sxs-lookup"><span data-stu-id="e4360-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="e4360-114">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="e4360-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="e4360-115">Een verzameling toevoegen</span><span class="sxs-lookup"><span data-stu-id="e4360-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="e4360-116">De voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="e4360-116">Clone the sample application</span></span>

<span data-ttu-id="e4360-117">We gaan nu een DocumentDB API-app klonen vanuit GitHub, de verbindingsreeks instellen en de app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e4360-117">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="e4360-118">U zult zien hoe gemakkelijk het is om op een programmatische manier met gegevens te werken.</span><span class="sxs-lookup"><span data-stu-id="e4360-118">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="e4360-119">Open een git-terminalvenster zoals git bash en `cd` naar een werkmap.</span><span class="sxs-lookup"><span data-stu-id="e4360-119">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="e4360-120">Voer de volgende opdracht uit om de voorbeeldopslagplaats te klonen.</span><span class="sxs-lookup"><span data-stu-id="e4360-120">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-the-code"></a><span data-ttu-id="e4360-121">De code bekijken</span><span class="sxs-lookup"><span data-stu-id="e4360-121">Review the code</span></span>

<span data-ttu-id="e4360-122">Laten we eens kijken wat er precies gebeurt in de app.</span><span class="sxs-lookup"><span data-stu-id="e4360-122">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="e4360-123">Open het bestand DocumentDBGetStarted.py en u zult zien dat deze regels code de Azure Cosmos DB-resources maken.</span><span class="sxs-lookup"><span data-stu-id="e4360-123">Open the DocumentDBGetStarted.py file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="e4360-124">De DocumentClient wordt geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="e4360-124">The DocumentClient is initialized.</span></span>

    ```python
    # Initialize the Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="e4360-125">Er wordt een nieuwe database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e4360-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="e4360-126">Er wordt een nieuwe verzameling gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e4360-126">A new collection is created.</span></span>

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

* <span data-ttu-id="e4360-127">Er wordt een aantal documenten gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e4360-127">Some documents are created.</span></span>

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

* <span data-ttu-id="e4360-128">Een query wordt uitgevoerd met behulp van SQL.</span><span class="sxs-lookup"><span data-stu-id="e4360-128">A query is performed using SQL</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="e4360-129">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="e4360-129">Update your connection string</span></span>

<span data-ttu-id="e4360-130">Ga nu terug naar Azure Portal om de verbindingsreeksinformatie op te halen en kopieer deze in de app.</span><span class="sxs-lookup"><span data-stu-id="e4360-130">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="e4360-131">Klik in [Azure Portal](http://portal.azure.com/), in uw Azure Cosmos DB-account, in het linker navigatiegedeelte op **Sleutels** en klik vervolgens op **Sleutels voor lezen/schrijven**.</span><span class="sxs-lookup"><span data-stu-id="e4360-131">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="e4360-132">In de volgende stap gebruikt u de kopieerknoppen aan de rechterkant van het scherm om de URI en primaire sleutel in het bestand `DocumentDBGetStarted.py` te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="e4360-132">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the `DocumentDBGetStarted.py` file in the next step.</span></span>

    ![Een toegangssleutel bekijken en kopiëren in Azure Portal, blade Sleutels](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="e4360-134">Open het bestand `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="e4360-134">In Open the `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="e4360-135">Kopieer uw URI-waarde vanaf de portal (met de kopieerknop) en geef deze als waarde aan de eindpuntsleutel in `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="e4360-135">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="e4360-136">Kopieer vervolgens de waarde van uw PRIMAIRE SLEUTEL vanaf de portal en geef deze als waarde aan de `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="e4360-136">Then copy your PRIMARY KEY value from the portal and make it the value of the `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="e4360-137">U hebt uw app nu bijgewerkt met alle informatie die nodig is voor de communicatie met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e4360-137">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-the-app"></a><span data-ttu-id="e4360-138">De app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e4360-138">Run the app</span></span>
1. <span data-ttu-id="e4360-139">Klik in Visual Studio met de rechtermuisknop op het project in **Solution Explorer**, selecteer de huidige Python-omgeving en klik er met de rechtermuisknop op.</span><span class="sxs-lookup"><span data-stu-id="e4360-139">In Visual Studio, right-click on the project in **Solution Explorer**, select the current Python environment, then right click.</span></span>

2. <span data-ttu-id="e4360-140">Selecteer Python-pakket installeren en typ vervolgens **pydocumentdb**</span><span class="sxs-lookup"><span data-stu-id="e4360-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="e4360-141">Druk op F5 om de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="e4360-141">Run F5 to run the application.</span></span> <span data-ttu-id="e4360-142">Uw app wordt in uw browser weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e4360-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="e4360-143">U kunt nu teruggaan naar Data Explorer en deze nieuwe gegevens bekijken, wijzigen, een query erop uitvoeren of er iets anders mee doen.</span><span class="sxs-lookup"><span data-stu-id="e4360-143">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="e4360-144">SLA’s bekijken in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e4360-144">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="e4360-145">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="e4360-145">Clean up resources</span></span>

<span data-ttu-id="e4360-146">Als u deze app niet verder gaat gebruiken, kunt u alle resources verwijderen die door deze Quick Start zijn aangemaakt door onderstaande stappen te volgen in Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="e4360-146">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="e4360-147">Klik in het menu aan de linkerkant in Azure Portal op **Resourcegroepen** en klik vervolgens op de resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e4360-147">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="e4360-148">Klik op de pagina van uw resourcegroep op **Verwijderen**, typ de naam van de resource die u wilt verwijderen in het tekstvak en klik vervolgens op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="e4360-148">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4360-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e4360-149">Next steps</span></span>

<span data-ttu-id="e4360-150">In deze Quick Start hebt u geleerd hoe u een Azure Cosmos DB-account kunt maken, hoe u een verzameling kunt maken met Data Explorer en hebt u een app uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e4360-150">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run an app.</span></span> <span data-ttu-id="e4360-151">Nu kunt u aanvullende gegevens in uw Cosmos DB-account importeren.</span><span class="sxs-lookup"><span data-stu-id="e4360-151">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e4360-152">Gegevens importeren in Azure Cosmos DB voor de DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="e4360-152">Import data into Azure Cosmos DB for the DocumentDB API</span></span>](import-data.md)



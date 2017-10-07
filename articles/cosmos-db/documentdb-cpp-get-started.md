---
title: aaaC ++ zelfstudie voor Azure Cosmos DB | Microsoft Docs
description: Dit is een C++ zelfstudie waarmee u een C++ database en -consoletoepassing maakt met Azure Cosmos DB-SDK voor C++. Azure Cosmos DB is een databaseservice op wereldwijde schaal.
services: cosmos-db
documentationcenter: cpp
author: asthana86
manager: jhubbard
editor: 
ms.assetid: b8756b60-8d41-4231-ba4f-6cfcfe3b4bab
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 12/25/2016
ms.author: aasthan
ms.openlocfilehash: 2d5eeff349b7753e39936b7eb77557ad30c5830a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a><span data-ttu-id="5d1e9-104">Azure Cosmos DB: C++ console toepassing zelfstudie voor DocumentDB API Hallo</span><span class="sxs-lookup"><span data-stu-id="5d1e9-104">Azure Cosmos DB: C++ console application tutorial for hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5d1e9-105">.NET</span><span class="sxs-lookup"><span data-stu-id="5d1e9-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="5d1e9-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="5d1e9-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="5d1e9-107">Node.js voor MongoDB</span><span class="sxs-lookup"><span data-stu-id="5d1e9-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="5d1e9-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="5d1e9-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="5d1e9-109">Java</span><span class="sxs-lookup"><span data-stu-id="5d1e9-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="5d1e9-110">C++</span><span class="sxs-lookup"><span data-stu-id="5d1e9-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="5d1e9-111">Welkom toohello C++-zelfstudie voor DocumentDB-API van Azure Cosmos DB Hallo goedgekeurde SDK voor C++!</span><span class="sxs-lookup"><span data-stu-id="5d1e9-111">Welcome toohello C++ tutorial for hello Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="5d1e9-112">Wanneer u deze zelfstudie hebt voltooid, beschikt u over een consoletoepassing waarmee u Azure Cosmos DB-resources kunt maken en er query's op kunt uitvoeren. Een van deze resources is een C++ database.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="5d1e9-113">De volgende onderwerpen komen aan bod:</span><span class="sxs-lookup"><span data-stu-id="5d1e9-113">We'll cover:</span></span>

* <span data-ttu-id="5d1e9-114">Maken en te verbinden tooan Azure DB die Cosmos-account</span><span class="sxs-lookup"><span data-stu-id="5d1e9-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="5d1e9-115">Uw toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="5d1e9-115">Setting up your application</span></span>
* <span data-ttu-id="5d1e9-116">Een C++ Azure Cosmos DB-database maken</span><span class="sxs-lookup"><span data-stu-id="5d1e9-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="5d1e9-117">Een verzameling maken</span><span class="sxs-lookup"><span data-stu-id="5d1e9-117">Creating a collection</span></span>
* <span data-ttu-id="5d1e9-118">JSON-documenten maken</span><span class="sxs-lookup"><span data-stu-id="5d1e9-118">Creating JSON documents</span></span>
* <span data-ttu-id="5d1e9-119">Hallo verzameling opvragen</span><span class="sxs-lookup"><span data-stu-id="5d1e9-119">Querying hello collection</span></span>
* <span data-ttu-id="5d1e9-120">Een document vervangen</span><span class="sxs-lookup"><span data-stu-id="5d1e9-120">Replacing a document</span></span>
* <span data-ttu-id="5d1e9-121">Een document verwijderen</span><span class="sxs-lookup"><span data-stu-id="5d1e9-121">Deleting a document</span></span>
* <span data-ttu-id="5d1e9-122">Hallo C++ Azure DB die Cosmos-database verwijderen</span><span class="sxs-lookup"><span data-stu-id="5d1e9-122">Deleting hello C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="5d1e9-123">Hebt u geen tijd?</span><span class="sxs-lookup"><span data-stu-id="5d1e9-123">Don't have time?</span></span> <span data-ttu-id="5d1e9-124">Geen probleem.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-124">Don't worry!</span></span> <span data-ttu-id="5d1e9-125">Hallo volledige oplossing is beschikbaar op [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span><span class="sxs-lookup"><span data-stu-id="5d1e9-125">hello complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="5d1e9-126">Zie [ophalen van de volledige oplossing Hallo](#GetSolution) voor beknopte instructies.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="5d1e9-127">Nadat u Hallo C++-zelfstudie hebt voltooid, stemknoppen Controleer gebruik Hallo Hallo onder deze pagina toogive aan ons feedback.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-127">After you've completed hello C++ tutorial, please use hello voting buttons at hello bottom of this page toogive us feedback.</span></span> 

<span data-ttu-id="5d1e9-128">Als u graag toocontact u rechtstreeks kunt u gratis tooinclude je e-mailadres in uw opmerkingen of [bereiken toous hier](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="5d1e9-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments or [reach out toous here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="5d1e9-129">Tijd om aan de slag te gaan.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-c-tutorial"></a><span data-ttu-id="5d1e9-130">Vereisten voor Hallo C++-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="5d1e9-130">Prerequisites for hello C++ tutorial</span></span>
<span data-ttu-id="5d1e9-131">Controleer of dat u de volgende Hallo hebt:</span><span class="sxs-lookup"><span data-stu-id="5d1e9-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="5d1e9-132">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-132">An active Azure account.</span></span> <span data-ttu-id="5d1e9-133">Als u nog geen abonnement hebt, kunt u zich registreren voor een [gratis Azure-proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5d1e9-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5d1e9-134">[Visual Studio](https://www.visualstudio.com/downloads/), waarbij Hallo C++ taalonderdelen zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-134">[Visual Studio](https://www.visualstudio.com/downloads/), with hello C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="5d1e9-135">Stap 1: een Azure Cosmos DB-account maken</span><span class="sxs-lookup"><span data-stu-id="5d1e9-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="5d1e9-136">Begin met het maken van een Azure Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="5d1e9-137">Als u al een account dat u wilt dat toouse hebt, kunt u verder gaan te[uw C++-toepassing instellen](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="5d1e9-137">If you already have an account you want toouse, you can skip ahead too[Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="5d1e9-138"><a id="SetupC++"></a>Stap 2: uw C++-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="5d1e9-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="5d1e9-139">Open Visual Studio en klik vervolgens op Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-139">Open Visual Studio, and then on hello **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="5d1e9-140">In Hallo **nieuw Project** in Hallo venster **geïnstalleerde** deelvenster Vouw **Visual C++**, klikt u op **Win32**, en klik vervolgens op  **Win32-consoletoepassing**.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-140">In hello **New Project** window, in hello **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="5d1e9-141">Hallo project hellodocumentdb naam en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-141">Name hello project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Schermafbeelding van de wizard voor nieuw project Hallo](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="5d1e9-143">Wanneer het Hallo-Wizard van Win32-toepassing wordt gestart, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-143">When hello Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="5d1e9-144">Zodra het Hallo-project is gemaakt, opent u NuGet-Pakketbeheer Hallo met de rechtermuisknop op Hallo **hellodocumentdb** project in **Solution Explorer** en te klikken op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-144">Once hello project has been created, open hello NuGet package manager by right-clicking hello **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![Schermopname van de NuGet-pakket beheren op Hallo project menu](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="5d1e9-146">In Hallo **NuGet: hellodocumentdb** tabblad **Bladeren**, en zoek vervolgens naar *documentdbcpp*.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-146">In hello **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="5d1e9-147">Selecteer in Hallo resultaten DocumentDbCPP, zoals wordt weergegeven in de volgende schermafbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-147">In hello results, select DocumentDbCPP, as shown in hello following screenshot.</span></span> <span data-ttu-id="5d1e9-148">Dit pakket installeert verwijzingen tooC ++ REST SDK, die een afhankelijkheid voor Hallo DocumentDbCPP is.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-148">This package installs references tooC++ REST SDK, which is a dependency for hello DocumentDbCPP.</span></span>  
   
    ![Schermopname van Hallo DocumentDbCpp pakket gemarkeerd](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="5d1e9-150">Zodra hello-pakketten tooyour project zijn toegevoegd, zijn we alle set toostart schrijven van code.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-150">Once hello packages have been added tooyour project, we are all set toostart writing some code.</span></span>   

## <span data-ttu-id="5d1e9-151"><a id="Config"></a>Stap 3: verbindingsgegevens kopiëren vanuit Azure Portal voor uw Azure Cosmos DB-database</span><span class="sxs-lookup"><span data-stu-id="5d1e9-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="5d1e9-152">Online zetten van [Azure-portal](https://portal.azure.com) en kunt doorlopen toohello Azure DB die Cosmos-databaseaccount u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-152">Bring up [Azure portal](https://portal.azure.com) and traverse toohello Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="5d1e9-153">We nodig Hallo URI en primaire sleutel van de Hallo van Azure-portal op Hallo volgende stap tooestablish een verbinding van onze codefragment C++.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-153">We will need hello URI and hello primary key from Azure portal in hello next step tooestablish a connection from our C++ code snippet.</span></span> 

![Azure Cosmos DB URI en sleutels in hello Azure-portal](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="5d1e9-155"><a id="Connect"></a>Stap 4: Tooan Azure DB die Cosmos-account koppelen</span><span class="sxs-lookup"><span data-stu-id="5d1e9-155"><a id="Connect"></a>Step 4: Connect tooan Azure Cosmos DB account</span></span>
1. <span data-ttu-id="5d1e9-156">Hallo na headers en naamruimten tooyour broncode na toevoegen `#include "stdafx.h"`.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-156">Add hello following headers and namespaces tooyour source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="5d1e9-157">Naast toevoegen Hallo volgende code van de belangrijkste functie tooyour en vervang de accountconfiguratie Hallo en primaire sleutel toomatch uw Azure DB die Cosmos-instellingen van stap 3.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-157">Next add hello following code tooyour main function and replace hello account configuration and primary key toomatch your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="5d1e9-158">Nu dat u Hallo code tooinitialize hello documentdb-client hebt, gaan we kijken werken met Azure DB die Cosmos-resources te nemen.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-158">Now that you have hello code tooinitialize hello documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="5d1e9-159"><a id="CreateDBColl"></a>Stap 5: een C++-database en -verzameling maken</span><span class="sxs-lookup"><span data-stu-id="5d1e9-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="5d1e9-160">Voordat we deze stap uitvoert, nu via een database, de verzameling en de documenten wisselwerking voor mensen die nieuwe tooAzure Cosmos DB zijn.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new tooAzure Cosmos DB.</span></span> <span data-ttu-id="5d1e9-161">Een [database](documentdb-resources.md#databases) is een logische container voor documentopslag, gepartitioneerd in verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="5d1e9-162">Een [verzameling](documentdb-resources.md#collections) is een container van JSON-documenten en Hallo bijbehorende JavaScript-toepassingslogica.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and hello associated JavaScript application logic.</span></span> <span data-ttu-id="5d1e9-163">U kunt meer informatie over hello Azure Cosmos DB hiërarchische resourcemodel en -concepten in [hiërarchische Azure DB die Cosmos-resourcemodel en -concepten](documentdb-resources.md).</span><span class="sxs-lookup"><span data-stu-id="5d1e9-163">You can learn more about hello Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="5d1e9-164">toocreate een database en een bijbehorende verzameling toevoegen Hallo na code toohello einde van uw belangrijkste functie.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-164">toocreate a database and a corresponding collection add hello following code toohello end of your main function.</span></span> <span data-ttu-id="5d1e9-165">Hiermee maakt u een database met de naam 'FamilyRegistry' en een verzameling FamilyCollection Hallo-clientconfiguratie die u in de vorige stap Hallo gedeclareerd met genoemd.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using hello client configuration you declared in hello previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="5d1e9-166"><a id="CreateDoc"></a>Stap 6: een document maken</span><span class="sxs-lookup"><span data-stu-id="5d1e9-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="5d1e9-167">[Documenten](documentdb-resources.md#documents) bestaan uit door gebruikers gedefinieerde (willekeurige) JSON-inhoud.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="5d1e9-168">U kunt nu een document invoegen in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="5d1e9-169">U kunt een document maken door te kopiëren van de volgende code in Hallo einde van de belangrijkste functie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-169">You can create a document by copying hello following code into hello end of hello main function.</span></span> 

    try {
      value document_family;
      document_family[L"id"] = value::string(L"AndersenFamily");
      document_family[L"FirstName"] = value::string(L"Thomas");
      document_family[L"LastName"] = value::string(L"Andersen");
      shared_ptr<Document> doc = coll->CreateDocumentAsync(document_family).get();

      document_family[L"id"] = value::string(L"WakefieldFamily");
      document_family[L"FirstName"] = value::string(L"Lucy");
      document_family[L"LastName"] = value::string(L"Wakefield");
      doc = coll->CreateDocumentAsync(document_family).get();
    } catch (ResourceAlreadyExistsException ex) {
      wcout << ex.message();
    }

<span data-ttu-id="5d1e9-170">toosummarize, deze code maakt een Azure DB die Cosmos-database, de verzameling en de documenten die u kunt een query in documentverkenner in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-170">toosummarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![Zelfstudie voor C++ - Diagram ter illustratie van Hallo hiërarchische relatie tussen Hallo-account, Hallo database Hallo verzameling en Hallo-documenten](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="5d1e9-172"><a id="QueryDB"></a>Stap 7: query's uitvoeren op Azure Cosmos DB-resources</span><span class="sxs-lookup"><span data-stu-id="5d1e9-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="5d1e9-173">Azure Cosmos DB biedt ondersteuning voor [uitgebreide query's](documentdb-sql-query.md) op de JSON-documenten die zijn opgeslagen in elke verzameling.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="5d1e9-174">Hallo ziet volgende voorbeeldcode u een query gemaakt met behulp van SQL-syntaxis die u kunt uitvoeren op Hallo documenten dat in de vorige stap Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-174">hello following sample code shows a query made using SQL syntax that you can run against hello documents we created in hello previous step.</span></span>

<span data-ttu-id="5d1e9-175">Hallo-functie wordt in als argumenten Hallo unique identifier of resource-id voor Hallo-database en verzameling Hallo samen met de Hallo document client.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-175">hello function takes in as arguments hello unique identifier or resource id for hello database and hello collection along with hello document client.</span></span> <span data-ttu-id="5d1e9-176">Voeg deze code toe voor de main-functie.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-176">Add this code before main function.</span></span>

    void executesimplequery(const DocumentClient &client,
                            const wstring dbresourceid,
                            const wstring collresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        wstring coll_name = coll->id();
        shared_ptr<DocumentIterator> iter =
            coll->QueryDocumentsAsync(wstring(L"SELECT * FROM " + coll_name)).get();
        wcout << "\n\nQuerying collection:";
        while (iter->HasMore()) {
          shared_ptr<Document> doc = iter->Next();
          wstring doc_name = doc->id();
          wcout << "\n\t" << doc_name << "\n";
          wcout << "\t"
                << "[{\"FirstName\":"
                << doc->payload().at(U("FirstName")).as_string()
                << ",\"LastName\":" << doc->payload().at(U("LastName")).as_string()
                << "}]";
        }
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="5d1e9-177"><a id="Replace"></a>Stap 8: een document vervangen</span><span class="sxs-lookup"><span data-stu-id="5d1e9-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="5d1e9-178">Azure Cosmos DB ondersteunt Vervang JSON-documenten, zoals wordt beschreven in de volgende code Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in hello following code.</span></span> <span data-ttu-id="5d1e9-179">Voeg deze code achter Hallo executesimplequery functie.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-179">Add this code after hello executesimplequery function.</span></span>

    void replacedocument(const DocumentClient &client, const wstring dbresourceid,
                         const wstring collresourceid,
                         const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        value newdoc;
        newdoc[L"id"] = value::string(L"WakefieldFamily");
        newdoc[L"FirstName"] = value::string(L"Lucy");
        newdoc[L"LastName"] = value::string(L"Smith Wakefield");
        coll->ReplaceDocument(docresourceid, newdoc);
      } catch (DocumentDBRuntimeException ex) {
        throw;
      }
    }

## <span data-ttu-id="5d1e9-180"><a id="Delete"></a>Stap 9: een document verwijderen</span><span class="sxs-lookup"><span data-stu-id="5d1e9-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="5d1e9-181">Azure DB Cosmos ondersteunt verwijderen van JSON-documenten, kunt u doen door kopiëren en plakken Hallo code achter Hallo replacedocument functie te volgen.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting hello following code after hello replacedocument function.</span></span> 

    void deletedocument(const DocumentClient &client, const wstring dbresourceid,
                        const wstring collresourceid, const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        coll->DeleteDocumentAsync(docresourceid).get();
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="5d1e9-182"><a id="DeleteDB"></a>Stap 10: een database verwijderen</span><span class="sxs-lookup"><span data-stu-id="5d1e9-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="5d1e9-183">Verwijderen Hallo gemaakt database verwijdert Hallo-database en alle onderliggende resources (verzamelingen, documenten, enz.).</span><span class="sxs-lookup"><span data-stu-id="5d1e9-183">Deleting hello created database removes hello database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="5d1e9-184">Kopieer en plak Hallo codefragment (functie opschonen) na Hallo deletedocument functie tooremove Hallo database en alle Hallo onderliggende resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-184">Copy and paste hello following code snippet (function cleanup) after hello deletedocument function tooremove hello database and all hello child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="5d1e9-185"><a id="Run"></a>Stap 11: uw C++-consoletoepassing volledig uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5d1e9-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="5d1e9-186">Code toocreate nu hebt toegevoegd we een query, wijzigen en verwijderen van verschillende Azure DB die Cosmos-bronnen.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-186">We have now added code toocreate, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="5d1e9-187">Laat het ons nu wire dit door toe te voegen aanroepen toothese verschillende functies van onze belangrijkste functie in hellodocumentdb.cpp samen met enkele diagnostische berichten.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-187">Let us now wire this up by adding calls toothese different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="5d1e9-188">U kunt dit doen door de belangrijkste functie van uw toepassing hello vervangen door een Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-188">You can do so by replacing hello main function of your application with hello following code.</span></span> <span data-ttu-id="5d1e9-189">Deze schrijfbewerkingen via Hallo account_configuration_uri en primary_key die u hebt gekopieerd in Hallo-code in stap 3, dus die regel of een kopie van Hallo waarden opslaan in opnieuw vanuit de portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-189">This writes over hello account_configuration_uri and primary_key you copied into hello code in Step 3, so save that line or copy hello values in again from hello portal.</span></span> 

    int main() {
        try {
            // Start by defining your account's configuration
            DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
            // Create your client
            DocumentClient client(conf);
            // Create a new database
            try {
                shared_ptr<Database> db = client.CreateDatabase(L"FamilyDB");
                wcout << "\nCreating database:\n" << db->id();
                // Create a collection inside database
                shared_ptr<Collection> coll = db->CreateCollection(L"FamilyColl");
                wcout << "\n\nCreating collection:\n" << coll->id();
                value document_family;
                document_family[L"id"] = value::string(L"AndersenFamily");
                document_family[L"FirstName"] = value::string(L"Thomas");
                document_family[L"LastName"] = value::string(L"Andersen");
                shared_ptr<Document> doc =
                    coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                document_family[L"id"] = value::string(L"WakefieldFamily");
                document_family[L"FirstName"] = value::string(L"Lucy");
                document_family[L"LastName"] = value::string(L"Wakefield");
                doc = coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                replacedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nReplaced document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                deletedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nDeleted document:\n" << doc->id();
                deletedb(client, db->resource_id());
                wcout << "\n\nDeleted db:\n" << db->id();
                cin.get();
            }
            catch (ResourceAlreadyExistsException ex) {
                wcout << ex.message();
            }
        }
        catch (DocumentDBRuntimeException ex) {
            wcout << ex.message();
        }
        cin.get();
    }

<span data-ttu-id="5d1e9-190">U moet nu kunnen toobuild worden en uw code uitvoeren in Visual Studio door op F5 te drukken of u kunt ook in terminalvenster door te zoeken naar de toepassing hello en Hallo Hallo uitvoerbare.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-190">You should now be able toobuild and run your code in Visual Studio by pressing F5 or alternatively in hello terminal window by locating hello application and running hello executable.</span></span> 

<span data-ttu-id="5d1e9-191">U ziet de uitvoer Hallo van uw getstarted-app.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-191">You should see hello output of your get started app.</span></span> <span data-ttu-id="5d1e9-192">Hallo-uitvoer moet overeenkomen met de Hallo volgende schermopname.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-192">hello output should match hello following screenshot.</span></span>

![Uitvoer Azure Cosmos DB C++ toepassing](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="5d1e9-194">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-194">Congratulations!</span></span> <span data-ttu-id="5d1e9-195">U Hallo C++-zelfstudie hebt voltooid en u hebt uw eerste Azure DB die Cosmos-consoletoepassing!</span><span class="sxs-lookup"><span data-stu-id="5d1e9-195">You've completed hello C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="5d1e9-196"><a id="GetSolution"></a>Hallo voltooid C++-zelfstudieoplossing ophalen</span><span class="sxs-lookup"><span data-stu-id="5d1e9-196"><a id="GetSolution"></a>Get hello complete C++ tutorial solution</span></span>
<span data-ttu-id="5d1e9-197">toobuild hello GetStarted-oplossing die alle Hallo voorbeelden in dit artikel bevat, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="5d1e9-197">toobuild hello GetStarted solution that contains all hello samples in this article, you need hello following:</span></span>

* <span data-ttu-id="5d1e9-198">[Azure Cosmos DB-account][create-account].</span><span class="sxs-lookup"><span data-stu-id="5d1e9-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="5d1e9-199">Hallo [GetStarted](https://github.com/stalker314314/DocumentDBCpp) oplossing is beschikbaar op GitHub.</span><span class="sxs-lookup"><span data-stu-id="5d1e9-199">hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d1e9-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5d1e9-200">Next steps</span></span>
* <span data-ttu-id="5d1e9-201">Meer informatie over hoe te[bewaken van een account voor Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="5d1e9-201">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="5d1e9-202">Query's uitvoeren op onze voorbeeldgegevensset in Hallo [Queryspeelplaats](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="5d1e9-202">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="5d1e9-203">Meer informatie over Hallo programmeermodel vindt u in de sectie ontwikkelen van Hallo Hallo [documentatiepagina voor Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="5d1e9-203">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account



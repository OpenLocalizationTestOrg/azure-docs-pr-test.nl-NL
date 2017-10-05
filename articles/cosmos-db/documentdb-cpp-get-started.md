---
title: C++ zelfstudie voor Azure Cosmos DB | Microsoft Docs
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
ms.openlocfilehash: 7d8de973765830ccd7983182bc1bb19b1e01e505
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-the-documentdb-api"></a><span data-ttu-id="2563a-104">Azure Cosmos DB: C++ consoletoepassingszelfstudie voor de DocumentDB-API</span><span class="sxs-lookup"><span data-stu-id="2563a-104">Azure Cosmos DB: C++ console application tutorial for the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2563a-105">.NET</span><span class="sxs-lookup"><span data-stu-id="2563a-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="2563a-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="2563a-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="2563a-107">Node.js voor MongoDB</span><span class="sxs-lookup"><span data-stu-id="2563a-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="2563a-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="2563a-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="2563a-109">Java</span><span class="sxs-lookup"><span data-stu-id="2563a-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="2563a-110">C++</span><span class="sxs-lookup"><span data-stu-id="2563a-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="2563a-111">Welkom bij de C++ zelfstudie over de Azure Cosmos DocumentDB-API-SDK voor C++.</span><span class="sxs-lookup"><span data-stu-id="2563a-111">Welcome to the C++ tutorial for the Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="2563a-112">Wanneer u deze zelfstudie hebt voltooid, beschikt u over een consoletoepassing waarmee u Azure Cosmos DB-resources kunt maken en er query's op kunt uitvoeren. Een van deze resources is een C++ database.</span><span class="sxs-lookup"><span data-stu-id="2563a-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="2563a-113">De volgende onderwerpen komen aan bod:</span><span class="sxs-lookup"><span data-stu-id="2563a-113">We'll cover:</span></span>

* <span data-ttu-id="2563a-114">Een Azure Cosmos DB-account maken en er verbinding mee maken</span><span class="sxs-lookup"><span data-stu-id="2563a-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="2563a-115">Uw toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="2563a-115">Setting up your application</span></span>
* <span data-ttu-id="2563a-116">Een C++ Azure Cosmos DB-database maken</span><span class="sxs-lookup"><span data-stu-id="2563a-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="2563a-117">Een verzameling maken</span><span class="sxs-lookup"><span data-stu-id="2563a-117">Creating a collection</span></span>
* <span data-ttu-id="2563a-118">JSON-documenten maken</span><span class="sxs-lookup"><span data-stu-id="2563a-118">Creating JSON documents</span></span>
* <span data-ttu-id="2563a-119">Query's uitvoeren op de verzameling</span><span class="sxs-lookup"><span data-stu-id="2563a-119">Querying the collection</span></span>
* <span data-ttu-id="2563a-120">Een document vervangen</span><span class="sxs-lookup"><span data-stu-id="2563a-120">Replacing a document</span></span>
* <span data-ttu-id="2563a-121">Een document verwijderen</span><span class="sxs-lookup"><span data-stu-id="2563a-121">Deleting a document</span></span>
* <span data-ttu-id="2563a-122">De C++ Azure Cosmos DB-database verwijderen</span><span class="sxs-lookup"><span data-stu-id="2563a-122">Deleting the C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="2563a-123">Hebt u geen tijd?</span><span class="sxs-lookup"><span data-stu-id="2563a-123">Don't have time?</span></span> <span data-ttu-id="2563a-124">Geen probleem.</span><span class="sxs-lookup"><span data-stu-id="2563a-124">Don't worry!</span></span> <span data-ttu-id="2563a-125">De volledige oplossing is beschikbaar via [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span><span class="sxs-lookup"><span data-stu-id="2563a-125">The complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="2563a-126">Zie [De volledige oplossing gebruiken](#GetSolution) voor beknopte instructies.</span><span class="sxs-lookup"><span data-stu-id="2563a-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="2563a-127">Wanneer u de C++-zelfstudie hebt voltooid, gebruikt u de stemknoppen onder aan deze pagina om feedback te verzenden.</span><span class="sxs-lookup"><span data-stu-id="2563a-127">After you've completed the C++ tutorial, please use the voting buttons at the bottom of this page to give us feedback.</span></span> 

<span data-ttu-id="2563a-128">Als u graag rechtstreeks contact wilt opnemen, kunt u uw e-mailadres aan uw reactie toevoegen of [hier contact met ons opnemen](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="2563a-128">If you'd like us to contact you directly, feel free to include your email address in your comments or [reach out to us here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="2563a-129">Tijd om aan de slag te gaan.</span><span class="sxs-lookup"><span data-stu-id="2563a-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-c-tutorial"></a><span data-ttu-id="2563a-130">Vereisten voor de C++-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="2563a-130">Prerequisites for the C++ tutorial</span></span>
<span data-ttu-id="2563a-131">Zorg ervoor dat u over de volgende zaken beschikt:</span><span class="sxs-lookup"><span data-stu-id="2563a-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="2563a-132">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="2563a-132">An active Azure account.</span></span> <span data-ttu-id="2563a-133">Als u nog geen abonnement hebt, kunt u zich registreren voor een [gratis Azure-proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2563a-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2563a-134">[Visual Studio](https://www.visualstudio.com/downloads/) met de C++-taalonderdelen geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="2563a-134">[Visual Studio](https://www.visualstudio.com/downloads/), with the C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="2563a-135">Stap 1: een Azure Cosmos DB-account maken</span><span class="sxs-lookup"><span data-stu-id="2563a-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="2563a-136">Begin met het maken van een Azure Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="2563a-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="2563a-137">Als u al een account hebt dat u wilt gebruiken, kunt u verder naar de stap [Uw C++-toepassing instellen](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="2563a-137">If you already have an account you want to use, you can skip ahead to [Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="2563a-138"><a id="SetupC++"></a>Stap 2: uw C++-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="2563a-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="2563a-139">Open Visual Studio en klik in het menu **Bestand** op **Nieuw** en vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="2563a-139">Open Visual Studio, and then on the **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="2563a-140">Vouw in het venster **Nieuw project**, in het deelvenster **Geïnstalleerd**, **Visual C++** uit, klik op **Win32** en klik vervolgens op **Win32-consoletoepassing**.</span><span class="sxs-lookup"><span data-stu-id="2563a-140">In the **New Project** window, in the **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="2563a-141">Noem het project hellodocumentdb en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2563a-141">Name the project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Schermafbeelding van de wizard Nieuw project](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="2563a-143">Klik zodra de Win32-toepassingswizard is gestart op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="2563a-143">When the Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="2563a-144">Open nadat het project is gemaakt het NuGet-pakketbeheer door met de rechtermuisknop op het project **hellodocumentdb** te klikken in **Solution Explorer** en vervolgens op **NuGet-pakketten beheren** te klikken.</span><span class="sxs-lookup"><span data-stu-id="2563a-144">Once the project has been created, open the NuGet package manager by right-clicking the **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![Schermafbeelding van NuGet-pakketten beheren in het projectmenu](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="2563a-146">Klik in het tabblad **NuGet: hellodocumentdb** op **Bladeren** en zoek naar *documentdbcpp*.</span><span class="sxs-lookup"><span data-stu-id="2563a-146">In the **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="2563a-147">Selecteer DocumentDbCPP in de resultaten, zoals weergegeven in de volgende schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="2563a-147">In the results, select DocumentDbCPP, as shown in the following screenshot.</span></span> <span data-ttu-id="2563a-148">Met dit pakket worden referenties naar C++ REST SDK geïnstalleerd, een afhankelijkheid voor de DocumentDbCPP.</span><span class="sxs-lookup"><span data-stu-id="2563a-148">This package installs references to C++ REST SDK, which is a dependency for the DocumentDbCPP.</span></span>  
   
    ![Schermafbeelding waarin het DocumentDbCpp-pakket is gemarkeerd](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="2563a-150">Zodra de pakketten aan uw project zijn toegevoegd, kunt u code gaan schrijven.</span><span class="sxs-lookup"><span data-stu-id="2563a-150">Once the packages have been added to your project, we are all set to start writing some code.</span></span>   

## <span data-ttu-id="2563a-151"><a id="Config"></a>Stap 3: verbindingsgegevens kopiëren vanuit Azure Portal voor uw Azure Cosmos DB-database</span><span class="sxs-lookup"><span data-stu-id="2563a-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="2563a-152">Open [Azure Portal](https://portal.azure.com) en ga naar het Azure Cosmos DB-databaseaccount dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2563a-152">Bring up [Azure portal](https://portal.azure.com) and traverse to the Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="2563a-153">U hebt de URI en de primaire sleutel uit Azure Portal nodig in de volgende stap om verbinding te maken vanaf uw C++-codefragment.</span><span class="sxs-lookup"><span data-stu-id="2563a-153">We will need the URI and the primary key from Azure portal in the next step to establish a connection from our C++ code snippet.</span></span> 

![Azure Cosmos DB-URI en sleutels in Azure Portal](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="2563a-155"><a id="Connect"></a>Stap 4: verbinding maken met een Azure Cosmos DB-account</span><span class="sxs-lookup"><span data-stu-id="2563a-155"><a id="Connect"></a>Step 4: Connect to an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="2563a-156">Voeg de volgende kopteksten en naamruimtes toe aan uw broncode, na `#include "stdafx.h"`.</span><span class="sxs-lookup"><span data-stu-id="2563a-156">Add the following headers and namespaces to your source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="2563a-157">Voeg daarna de volgende code toe aan de functie Main en vervang de accountconfiguratie en primaire sleutel, zodat ze overeenkomen met uw Azure Cosmos DB-instellingen uit stap 3.</span><span class="sxs-lookup"><span data-stu-id="2563a-157">Next add the following code to your main function and replace the account configuration and primary key to match your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="2563a-158">Nu u beschikt over de code om de DocumentDB-client opnieuw te initialiseren, kunt u zich verder verdiepen in het werken met Azure Cosmos DB-resources.</span><span class="sxs-lookup"><span data-stu-id="2563a-158">Now that you have the code to initialize the documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="2563a-159"><a id="CreateDBColl"></a>Stap 5: een C++-database en -verzameling maken</span><span class="sxs-lookup"><span data-stu-id="2563a-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="2563a-160">Voordat u deze stap uitvoert, behandelen we eerst hoe een database, verzameling en documenten met elkaar communiceren, voor het geval Azure Cosmos DB nieuw voor u is.</span><span class="sxs-lookup"><span data-stu-id="2563a-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new to Azure Cosmos DB.</span></span> <span data-ttu-id="2563a-161">Een [database](documentdb-resources.md#databases) is een logische container voor documentopslag, gepartitioneerd in verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="2563a-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="2563a-162">Een [verzameling](documentdb-resources.md#collections) is een container van JSON-documenten en de bijbehorende JavaScript-toepassingslogica.</span><span class="sxs-lookup"><span data-stu-id="2563a-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and the associated JavaScript application logic.</span></span> <span data-ttu-id="2563a-163">Meer informatie over het hiërarchische resourcemodel en concepten voor Azure Cosmos DB vindt u in [Hiërarchisch Azure Cosmos DB-resourcemodel en -concepten](documentdb-resources.md).</span><span class="sxs-lookup"><span data-stu-id="2563a-163">You can learn more about the Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="2563a-164">Voeg de volgende code toe aan het eind van de main-functie om een database en bijbehorende verzameling te maken.</span><span class="sxs-lookup"><span data-stu-id="2563a-164">To create a database and a corresponding collection add the following code to the end of your main function.</span></span> <span data-ttu-id="2563a-165">Hiermee maakt u een database genaamd 'FamilyRegistry' en een verzameling genaamd 'FamilyCollection' met behulp van de klantconfiguratie die u in de vorige stap hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="2563a-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using the client configuration you declared in the previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="2563a-166"><a id="CreateDoc"></a>Stap 6: een document maken</span><span class="sxs-lookup"><span data-stu-id="2563a-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="2563a-167">[Documenten](documentdb-resources.md#documents) bestaan uit door gebruikers gedefinieerde (willekeurige) JSON-inhoud.</span><span class="sxs-lookup"><span data-stu-id="2563a-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="2563a-168">U kunt nu een document invoegen in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2563a-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="2563a-169">U kunt een document maken door de volgende code aan het einde van de main-functie te plakken.</span><span class="sxs-lookup"><span data-stu-id="2563a-169">You can create a document by copying the following code into the end of the main function.</span></span> 

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

<span data-ttu-id="2563a-170">Kort samengevat maakt u met deze code een Azure Cosmos DB-database, -verzameling en -documenten, waarop u query's kunt toepassen in Documentverkenner in Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2563a-170">To summarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![C++-zelfstudie: diagram waarin u de hiërarchische relatie ziet tussen het account, de database, de verzameling en de documenten](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="2563a-172"><a id="QueryDB"></a>Stap 7: query's uitvoeren op Azure Cosmos DB-resources</span><span class="sxs-lookup"><span data-stu-id="2563a-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="2563a-173">Azure Cosmos DB biedt ondersteuning voor [uitgebreide query's](documentdb-sql-query.md) op de JSON-documenten die zijn opgeslagen in elke verzameling.</span><span class="sxs-lookup"><span data-stu-id="2563a-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="2563a-174">De volgende voorbeeldcode bevat een query die is gemaakt met de SQL-syntaxis. Deze query kan worden uitgevoerd voor de documenten die in de vorige stap zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2563a-174">The following sample code shows a query made using SQL syntax that you can run against the documents we created in the previous step.</span></span>

<span data-ttu-id="2563a-175">De functie omvat als argumenten de unieke id of resource-id voor de database en de verzameling, samen met het clientdocument.</span><span class="sxs-lookup"><span data-stu-id="2563a-175">The function takes in as arguments the unique identifier or resource id for the database and the collection along with the document client.</span></span> <span data-ttu-id="2563a-176">Voeg deze code toe voor de main-functie.</span><span class="sxs-lookup"><span data-stu-id="2563a-176">Add this code before main function.</span></span>

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

## <span data-ttu-id="2563a-177"><a id="Replace"></a>Stap 8: een document vervangen</span><span class="sxs-lookup"><span data-stu-id="2563a-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="2563a-178">Azure Cosmos DB ondersteunt het vervangen van JSON-documenten, zoals in de volgende code wordt gedemonstreerd.</span><span class="sxs-lookup"><span data-stu-id="2563a-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in the following code.</span></span> <span data-ttu-id="2563a-179">Voeg deze code toe na de functie executesimplequery.</span><span class="sxs-lookup"><span data-stu-id="2563a-179">Add this code after the executesimplequery function.</span></span>

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

## <span data-ttu-id="2563a-180"><a id="Delete"></a>Stap 9: een document verwijderen</span><span class="sxs-lookup"><span data-stu-id="2563a-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="2563a-181">Azure Cosmos DB ondersteunt het verwijderen van JSON-documenten. U kunt deze documenten verwijderen door de volgende code te kopiëren en achter de instructie replacedocument te plakken.</span><span class="sxs-lookup"><span data-stu-id="2563a-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting the following code after the replacedocument function.</span></span> 

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

## <span data-ttu-id="2563a-182"><a id="DeleteDB"></a>Stap 10: een database verwijderen</span><span class="sxs-lookup"><span data-stu-id="2563a-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="2563a-183">Als u de gemaakte database verwijdert, worden de database en alle onderliggende resources (verzamelingen, documenten enz.) verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2563a-183">Deleting the created database removes the database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="2563a-184">Kopieer en plak het volgende codefragment (functie cleanup) na de functie deletedocument om de database en alle onderliggende resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2563a-184">Copy and paste the following code snippet (function cleanup) after the deletedocument function to remove the database and all the child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="2563a-185"><a id="Run"></a>Stap 11: uw C++-consoletoepassing volledig uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2563a-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="2563a-186">U hebt nu code toegevoegd om verschillende Azure Cosmos DB-resources te maken, aan te passen, te verwijderen en er query's op toe te passen.</span><span class="sxs-lookup"><span data-stu-id="2563a-186">We have now added code to create, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="2563a-187">Nu is het tijd om alles te verbinden door calls toe te voegen aan de verschillende functies vanuit de main-functie in hellodocumentdb.cpp, samen met een aantal diagnostische berichten.</span><span class="sxs-lookup"><span data-stu-id="2563a-187">Let us now wire this up by adding calls to these different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="2563a-188">U doet dit door de main-functie van uw toepassing te vervangen door de volgende code.</span><span class="sxs-lookup"><span data-stu-id="2563a-188">You can do so by replacing the main function of your application with the following code.</span></span> <span data-ttu-id="2563a-189">Deze overschrijft de account_configuration_uri en primary_key die u in de code hebt geplakt in stap 3, dus bewaar deze regel of kopieer en plak de waarden opnieuw vanuit de portal.</span><span class="sxs-lookup"><span data-stu-id="2563a-189">This writes over the account_configuration_uri and primary_key you copied into the code in Step 3, so save that line or copy the values in again from the portal.</span></span> 

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

<span data-ttu-id="2563a-190">U zou nu uw code moeten kunnen bouwen en uitvoeren in Visual Studio door op F5 te drukken of naar het terminalvenster te gaan, de toepassing te zoeken en het uitvoerbare bestand uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="2563a-190">You should now be able to build and run your code in Visual Studio by pressing F5 or alternatively in the terminal window by locating the application and running the executable.</span></span> 

<span data-ttu-id="2563a-191">U ziet de uitvoer van uw GetStarted-app.</span><span class="sxs-lookup"><span data-stu-id="2563a-191">You should see the output of your get started app.</span></span> <span data-ttu-id="2563a-192">De uitvoer moet overeenkomen met de volgende schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="2563a-192">The output should match the following screenshot.</span></span>

![Uitvoer Azure Cosmos DB C++ toepassing](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="2563a-194">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="2563a-194">Congratulations!</span></span> <span data-ttu-id="2563a-195">U hebt de C++ zelfstudie voltooid en beschikt nu over uw eerste Azure Cosmos DB-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="2563a-195">You've completed the C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="2563a-196"><a id="GetSolution"></a>De volledige C++-zelfstudieoplossing ophalen</span><span class="sxs-lookup"><span data-stu-id="2563a-196"><a id="GetSolution"></a>Get the complete C++ tutorial solution</span></span>
<span data-ttu-id="2563a-197">Als u een GetStarted-oplossing wilt bouwen die alle voorbeelden uit dit artikel bevat, hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="2563a-197">To build the GetStarted solution that contains all the samples in this article, you need the following:</span></span>

* <span data-ttu-id="2563a-198">[Azure Cosmos DB-account][create-account].</span><span class="sxs-lookup"><span data-stu-id="2563a-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="2563a-199">De [GetStarted](https://github.com/stalker314314/DocumentDBCpp)-oplossing die beschikbaar is via GitHub.</span><span class="sxs-lookup"><span data-stu-id="2563a-199">The [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2563a-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2563a-200">Next steps</span></span>
* <span data-ttu-id="2563a-201">Leer hoe het [bewaken van een Azure Cosmos DB-account](monitor-accounts.md) werkt.</span><span class="sxs-lookup"><span data-stu-id="2563a-201">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="2563a-202">Voer query's uit op onze voorbeeldgegevensset in de [Queryspeelplaats](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="2563a-202">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="2563a-203">Meer informatie over het programmeermodel vindt u in de sectie Ontwikkelen van de [pagina met Azure Cosmos DB-documentatie](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="2563a-203">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account



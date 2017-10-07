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
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a>Azure Cosmos DB: C++ console toepassing zelfstudie voor DocumentDB API Hallo
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js voor MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 
 

Welkom toohello C++-zelfstudie voor DocumentDB-API van Azure Cosmos DB Hallo goedgekeurde SDK voor C++! Wanneer u deze zelfstudie hebt voltooid, beschikt u over een consoletoepassing waarmee u Azure Cosmos DB-resources kunt maken en er query's op kunt uitvoeren. Een van deze resources is een C++ database.

De volgende onderwerpen komen aan bod:

* Maken en te verbinden tooan Azure DB die Cosmos-account
* Uw toepassing instellen
* Een C++ Azure Cosmos DB-database maken
* Een verzameling maken
* JSON-documenten maken
* Hallo verzameling opvragen
* Een document vervangen
* Een document verwijderen
* Hallo C++ Azure DB die Cosmos-database verwijderen

Hebt u geen tijd? Geen probleem. Hallo volledige oplossing is beschikbaar op [GitHub](https://github.com/stalker314314/DocumentDBCpp). Zie [ophalen van de volledige oplossing Hallo](#GetSolution) voor beknopte instructies.

Nadat u Hallo C++-zelfstudie hebt voltooid, stemknoppen Controleer gebruik Hallo Hallo onder deze pagina toogive aan ons feedback. 

Als u graag toocontact u rechtstreeks kunt u gratis tooinclude je e-mailadres in uw opmerkingen of [bereiken toous hier](https://www.research.net/r/8BKRJ3Z). 

Tijd om aan de slag te gaan.

## <a name="prerequisites-for-hello-c-tutorial"></a>Vereisten voor Hallo C++-zelfstudie
Controleer of dat u de volgende Hallo hebt:

* Een actief Azure-account. Als u nog geen abonnement hebt, kunt u zich registreren voor een [gratis Azure-proefversie](https://azure.microsoft.com/pricing/free-trial/).
* [Visual Studio](https://www.visualstudio.com/downloads/), waarbij Hallo C++ taalonderdelen zijn geïnstalleerd.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Stap 1: een Azure Cosmos DB-account maken
Begin met het maken van een Azure Cosmos DB-account. Als u al een account dat u wilt dat toouse hebt, kunt u verder gaan te[uw C++-toepassing instellen](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupC++"></a>Stap 2: uw C++-toepassing instellen
1. Open Visual Studio en klik vervolgens op Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**. 
2. In Hallo **nieuw Project** in Hallo venster **geïnstalleerde** deelvenster Vouw **Visual C++**, klikt u op **Win32**, en klik vervolgens op  **Win32-consoletoepassing**. Hallo project hellodocumentdb naam en klik op **OK**. 
   
    ![Schermafbeelding van de wizard voor nieuw project Hallo](media/documentdb-cpp-get-started/hello.png)
3. Wanneer het Hallo-Wizard van Win32-toepassing wordt gestart, klikt u op **voltooien**.
4. Zodra het Hallo-project is gemaakt, opent u NuGet-Pakketbeheer Hallo met de rechtermuisknop op Hallo **hellodocumentdb** project in **Solution Explorer** en te klikken op **NuGet-pakketten beheren**. 
   
    ![Schermopname van de NuGet-pakket beheren op Hallo project menu](media/documentdb-cpp-get-started/nuget.png)
5. In Hallo **NuGet: hellodocumentdb** tabblad **Bladeren**, en zoek vervolgens naar *documentdbcpp*. Selecteer in Hallo resultaten DocumentDbCPP, zoals wordt weergegeven in de volgende schermafbeelding Hallo. Dit pakket installeert verwijzingen tooC ++ REST SDK, die een afhankelijkheid voor Hallo DocumentDbCPP is.  
   
    ![Schermopname van Hallo DocumentDbCpp pakket gemarkeerd](media/documentdb-cpp-get-started/cpp.png)
   
    Zodra hello-pakketten tooyour project zijn toegevoegd, zijn we alle set toostart schrijven van code.   

## <a id="Config"></a>Stap 3: verbindingsgegevens kopiëren vanuit Azure Portal voor uw Azure Cosmos DB-database
Online zetten van [Azure-portal](https://portal.azure.com) en kunt doorlopen toohello Azure DB die Cosmos-databaseaccount u hebt gemaakt. We nodig Hallo URI en primaire sleutel van de Hallo van Azure-portal op Hallo volgende stap tooestablish een verbinding van onze codefragment C++. 

![Azure Cosmos DB URI en sleutels in hello Azure-portal](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <a id="Connect"></a>Stap 4: Tooan Azure DB die Cosmos-account koppelen
1. Hallo na headers en naamruimten tooyour broncode na toevoegen `#include "stdafx.h"`.
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. Naast toevoegen Hallo volgende code van de belangrijkste functie tooyour en vervang de accountconfiguratie Hallo en primaire sleutel toomatch uw Azure DB die Cosmos-instellingen van stap 3. 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    Nu dat u Hallo code tooinitialize hello documentdb-client hebt, gaan we kijken werken met Azure DB die Cosmos-resources te nemen.

## <a id="CreateDBColl"></a>Stap 5: een C++-database en -verzameling maken
Voordat we deze stap uitvoert, nu via een database, de verzameling en de documenten wisselwerking voor mensen die nieuwe tooAzure Cosmos DB zijn. Een [database](documentdb-resources.md#databases) is een logische container voor documentopslag, gepartitioneerd in verzamelingen. Een [verzameling](documentdb-resources.md#collections) is een container van JSON-documenten en Hallo bijbehorende JavaScript-toepassingslogica. U kunt meer informatie over hello Azure Cosmos DB hiërarchische resourcemodel en -concepten in [hiërarchische Azure DB die Cosmos-resourcemodel en -concepten](documentdb-resources.md).

toocreate een database en een bijbehorende verzameling toevoegen Hallo na code toohello einde van uw belangrijkste functie. Hiermee maakt u een database met de naam 'FamilyRegistry' en een verzameling FamilyCollection Hallo-clientconfiguratie die u in de vorige stap Hallo gedeclareerd met genoemd.

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <a id="CreateDoc"></a>Stap 6: een document maken
[Documenten](documentdb-resources.md#documents) bestaan uit door gebruikers gedefinieerde (willekeurige) JSON-inhoud. U kunt nu een document invoegen in Azure Cosmos DB. U kunt een document maken door te kopiëren van de volgende code in Hallo einde van de belangrijkste functie Hallo Hallo. 

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

toosummarize, deze code maakt een Azure DB die Cosmos-database, de verzameling en de documenten die u kunt een query in documentverkenner in Azure-portal. 

![Zelfstudie voor C++ - Diagram ter illustratie van Hallo hiërarchische relatie tussen Hallo-account, Hallo database Hallo verzameling en Hallo-documenten](media/documentdb-cpp-get-started/docs.png)

## <a id="QueryDB"></a>Stap 7: query's uitvoeren op Azure Cosmos DB-resources
Azure Cosmos DB biedt ondersteuning voor [uitgebreide query's](documentdb-sql-query.md) op de JSON-documenten die zijn opgeslagen in elke verzameling. Hallo ziet volgende voorbeeldcode u een query gemaakt met behulp van SQL-syntaxis die u kunt uitvoeren op Hallo documenten dat in de vorige stap Hallo is gemaakt.

Hallo-functie wordt in als argumenten Hallo unique identifier of resource-id voor Hallo-database en verzameling Hallo samen met de Hallo document client. Voeg deze code toe voor de main-functie.

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

## <a id="Replace"></a>Stap 8: een document vervangen
Azure Cosmos DB ondersteunt Vervang JSON-documenten, zoals wordt beschreven in de volgende code Hallo. Voeg deze code achter Hallo executesimplequery functie.

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

## <a id="Delete"></a>Stap 9: een document verwijderen
Azure DB Cosmos ondersteunt verwijderen van JSON-documenten, kunt u doen door kopiëren en plakken Hallo code achter Hallo replacedocument functie te volgen. 

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

## <a id="DeleteDB"></a>Stap 10: een database verwijderen
Verwijderen Hallo gemaakt database verwijdert Hallo-database en alle onderliggende resources (verzamelingen, documenten, enz.).

Kopieer en plak Hallo codefragment (functie opschonen) na Hallo deletedocument functie tooremove Hallo database en alle Hallo onderliggende resources te volgen.

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="Run"></a>Stap 11: uw C++-consoletoepassing volledig uitvoeren
Code toocreate nu hebt toegevoegd we een query, wijzigen en verwijderen van verschillende Azure DB die Cosmos-bronnen.  Laat het ons nu wire dit door toe te voegen aanroepen toothese verschillende functies van onze belangrijkste functie in hellodocumentdb.cpp samen met enkele diagnostische berichten.

U kunt dit doen door de belangrijkste functie van uw toepassing hello vervangen door een Hallo code te volgen. Deze schrijfbewerkingen via Hallo account_configuration_uri en primary_key die u hebt gekopieerd in Hallo-code in stap 3, dus die regel of een kopie van Hallo waarden opslaan in opnieuw vanuit de portal Hallo. 

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

U moet nu kunnen toobuild worden en uw code uitvoeren in Visual Studio door op F5 te drukken of u kunt ook in terminalvenster door te zoeken naar de toepassing hello en Hallo Hallo uitvoerbare. 

U ziet de uitvoer Hallo van uw getstarted-app. Hallo-uitvoer moet overeenkomen met de Hallo volgende schermopname.

![Uitvoer Azure Cosmos DB C++ toepassing](media/documentdb-cpp-get-started/console.png)

Gefeliciteerd. U Hallo C++-zelfstudie hebt voltooid en u hebt uw eerste Azure DB die Cosmos-consoletoepassing!

## <a id="GetSolution"></a>Hallo voltooid C++-zelfstudieoplossing ophalen
toobuild hello GetStarted-oplossing die alle Hallo voorbeelden in dit artikel bevat, moet u de volgende Hallo:

* [Azure Cosmos DB-account][create-account].
* Hallo [GetStarted](https://github.com/stalker314314/DocumentDBCpp) oplossing is beschikbaar op GitHub.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[bewaken van een account voor Azure Cosmos DB](monitor-accounts.md).
* Query's uitvoeren op onze voorbeeldgegevensset in Hallo [Queryspeelplaats](https://www.documentdb.com/sql/demo).
* Meer informatie over Hallo programmeermodel vindt u in de sectie ontwikkelen van Hallo Hallo [documentatiepagina voor Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account



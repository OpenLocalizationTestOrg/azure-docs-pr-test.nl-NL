---
title: 'Azure Cosmos DB: aan de slag met de DocumentDB-API | Microsoft Docs'
description: Een zelfstudie waarmee u maakt een online database en C#-consoletoepassing Hallo DocumentDB API gebruiken.
keywords: nosql zelfstudie, onlinedatabase, c#-consoletoepassing
services: cosmos-db
documentationcenter: .net
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2017
ms.author: anhoh
ms.openlocfilehash: 65a181f715a670987492ad7815ef2ec94498e84d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a>Azure Cosmos DB: aan de slag met de DocumentDB-API
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js voor MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Zelfstudie Welkom toohello API van Azure Cosmos DB DocumentDB aan de slag! Wanneer u deze zelfstudie hebt voltooid, beschikt u over een consoletoepassing waarmee u Azure Cosmos DB-resources kunt maken en er query's op kunt uitvoeren.

De volgende onderwerpen komen aan bod:

* Maken en te verbinden tooan Azure DB die Cosmos-account
* Uw Visual Studio-oplossing configureren
* Een online-database maken
* Een verzameling maken
* JSON-documenten maken
* Hallo verzameling opvragen
* Een document vervangen
* Een document verwijderen
* Hallo-database verwijderen

Hebt u geen tijd? Geen probleem. Hallo volledige oplossing is beschikbaar op [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started). Springen toohello [Hallo volledige NoSQL-zelfstudieoplossing sectie ophalen](#GetSolution) voor beknopte instructies.

Daarna stemknoppen Neem gebruik Hallo Hallo boven of onder aan deze pagina toogive ons feedback. Als u graag toocontact u rechtstreeks kunt u gratis tooinclude je e-mailadres in uw opmerkingen.

Tijd om aan de slag te gaan.

## <a name="prerequisites"></a>Vereisten
Controleer of dat u de volgende Hallo hebt:

* Een actief Azure-account. Als u nog geen account hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/). 
    * U kunt ook hello gebruiken [Azure Cosmos DB Emulator](local-emulator.md) voor deze zelfstudie.
* [Visual Studio Community 2017](http://www.visualstudio.com/).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Stap 1: een Azure Cosmos DB-account maken
Begin met het maken van een Azure Cosmos DB-account. Als u al een account dat u wilt dat toouse hebt, kunt u verder gaan te[uw Visual Studio-oplossing instellen](#SetupVS). Als u hello Azure Cosmos DB Emulator, volgt u stappen op Hallo [Azure Cosmos DB Emulator](local-emulator.md) toosetup Hallo emulator en gaat u verder te[uw Visual Studio-oplossing instellen](#SetupVS).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Stap 2: uw Visual Studio-oplossing instellen
1. Open **Visual Studio 2017** op uw computer.
2. Op Hallo **bestand** selecteert u **nieuw**, en kies vervolgens **Project**.
3. In Hallo **nieuw Project** dialoogvenster Selecteer **sjablonen** / **Visual C#** / **consoletoepassing**en de naam uw project en klik vervolgens op **OK**.
   ![Schermopname van het venster Hallo-nieuw Project](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)
4. In Hallo **Solution Explorer**, klik met de rechtermuisknop op uw nieuwe consoletoepassing die zich onder uw Visual Studio-oplossing, en klik vervolgens op **NuGet-pakketten beheren...**
    
    ![Schermopname van Hallo rechts op wordt geklikt Menu voor Hallo Project](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. In Hallo **Nuget** tabblad **Bladeren**, en het type **azure documentdb** in het zoekvak Hallo.
6. Binnen Hallo resultaten vinden **Microsoft.Azure.DocumentDB** en klik op **installeren**.
   Hallo pakket-id voor hello Azure Cosmos DB DocumentDB-API-clientbibliotheek [Microsoft Azure DocumentDB-clientbibliotheek](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).
   ![Schermopname van het Hallo Nuget-Menu voor het vinden van Client-SDK van Azure Cosmos DB](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)

    Als u een berichten krijgt over het controleren van wijzigingen toohello oplossing, klikt u op **OK**. Als u een bericht ontvangt over het accepteren van de licentie, klikt u op **Accepteren**.

Goed gedaan. Nu dat Hallo setup is voltooid, begint schrijven van code. Op [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs) vindt u een voltooid codeproject voor deze zelfstudie.

## <a id="Connect"></a>Stap 3: Verbinding maken met tooan Azure DB die Cosmos-account
Voeg eerst deze verwijzingen toohello begin van de C#-toepassing, in het bestand Program.cs Hallo:

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> Controleer of dat u Hallo bovenstaande afhankelijkheden toevoegen in de volgorde toocomplete Hallo zelfstudie.
> 
> 

Voeg nu deze twee constanten en de variabele *client* toe onder de openbare klasse *Program*.

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

Vervolgens head back-toohello [Azure Portal](https://portal.azure.com) tooretrieve uw eindpunt-URL en de primaire sleutel. Hallo eindpunt-URL en de primaire sleutel nodig zijn om uw toepassing toounderstand waar tooconnect en voor Azure Cosmos DB tootrust van uw toepassing verbinding.

In Azure Portal Hallo, navigeer tooyour Azure DB die Cosmos-account en klik op **sleutels**.

Hallo URI van de portal Hallo Kopieer en plak deze in `<your endpoint URL>` in het bestand program.cs Hallo. Vervolgens kopiëren primaire sleutel van de portal Hallo Hallo en plak deze in `<your primary key>`.

![Schermopname van hello Azure Portal gebruikt door Hallo NoSQL-zelfstudie toocreate een C#-consoletoepassing. Ziet u een Cosmos Azure DB-account met de actieve hub Hallo gemarkeerd, Hallo knop sleutels gemarkeerd op de blade hello Azure DB die Cosmos-account en de waarden URI, primaire sleutel en secundaire sleutel Hallo gemarkeerd op Hallo blade sleutels][keys]

Vervolgens we toepassing hello beginnen met het maken van een nieuw exemplaar van Hallo **DocumentClient**.

Hieronder Hallo **Main** methode toevoegen van nieuwe asynchrone taak aangeroepen **GetStartedDemo**, die wordt een exemplaar van onze nieuwe **DocumentClient**.

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

Voeg Hallo volgende code toorun uw asynchrone taak van uw **Main** methode. Hallo **Main** methode wordt onderschept uitzonderingen en toohello console geschreven.

    static void Main(string[] args)
    {
            // ADD THIS PART tooYOUR CODE
            try
            {
                    Program p = new Program();
                    p.GetStartedDemo().Wait();
            }
            catch (DocumentClientException de)
            {
                    Exception baseException = de.GetBaseException();
                    Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
            }
            catch (Exception e)
            {
                    Exception baseException = e.GetBaseException();
                    Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
            }
            finally
            {
                    Console.WriteLine("End of demo, press any key tooexit.");
                    Console.ReadKey();
            }

Druk op **F5** toorun uw toepassing. Hallo-console-venster uitvoer geeft het Hallo-bericht `End of demo, press any key tooexit.` bevestigen dat Hallo verbinding is gemaakt.  U kunt vervolgens Hallo-consolevenster sluiten. 

Gefeliciteerd. U hebt verbinding gemaakt tooan Azure DB die Cosmos-account, laten we nu eens kijken werken met Azure DB die Cosmos-resources.  

## <a name="step-4-create-a-database"></a>Stap 4: een database maken
Voordat u Hallo-code voor het maken van een database toevoegt, Voeg een Help-methode voor het schrijven van toohello-console.

Kopieer en plak Hallo **WriteToConsoleAndPromptToContinue** methode na Hallo **GetStartedDemo** methode.

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

Uw Azure-Cosmos-DB [database](documentdb-resources.md#databases) kunnen worden gemaakt met behulp van Hallo [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) methode Hallo **DocumentClient** klasse. Een database is een logische container voor documentopslag, gepartitioneerd in verzamelingen JSON Hallo.

Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode na het Hallo-client maken. Hiermee maakt u een database met de naam *FamilyDB*.

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

Druk op **F5** toorun uw toepassing.

Gefeliciteerd. U hebt een Azure Cosmos DB-database gemaakt.  

## <a id="CreateColl"></a>Stap 5: een verzameling maken
> [!WARNING]
> Met **CreateDocumentCollectionIfNotExistsAsync** maakt u een nieuwe verzameling met gereserveerde doorvoer, wat gevolgen heeft voor de kosten. Zie onze [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/) voor meer informatie.
> 
> 

Een [verzameling](documentdb-resources.md#collections) kunnen worden gemaakt met behulp van Hallo [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) methode Hallo **DocumentClient** klasse. Een verzameling is een container van JSON-documenten en de bijbehorende JavaScript-toepassingslogica.

Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode na het Hallo-database maken. Hiermee maakt u een documentverzameling met de naam *FamilyCollection*.

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

Druk op **F5** toorun uw toepassing.

Gefeliciteerd. U hebt een Azure Cosmos DB-documentverzameling gemaakt.  

## <a id="CreateDoc"></a>Stap 6: JSON-documenten maken
Een [document](documentdb-resources.md#documents) kunnen worden gemaakt met behulp van Hallo [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) methode Hallo **DocumentClient** klasse. Documenten bestaan uit door gebruikers gedefinieerde (willekeurige) JSON-inhoud. U kunt nu een of meer documenten invoegen. Als u gegevens die u wilt toostore in de database al hebt, kunt u hello Azure Cosmos DB [hulpprogramma voor gegevensmigratie](import-data.md) tooimport Hallo gegevens in een database.

We moeten eerst toocreate een **familie** klasse die objecten die zijn opgeslagen in Azure Cosmos DB in dit voorbeeld wordt aangegeven. Daarnaast moeten de subklassen **Parent**, **Child**, **Pet** en **Address** worden gemaakt die in de klasse **Family** worden gebruikt. Houd er rekening mee dat de documenten een **id**-eigenschap moeten bevatten die in JSON is geserialiseerd als **id**. Maak deze klassen door toe te voegen na interne onderliggende klassen na Hallo Hallo **GetStartedDemo** methode.

Kopieer en plak Hallo **familie**, **bovenliggende**, **onderliggende**, **huisdier**, en **adres** klassen na Hallo **WriteToConsoleAndPromptToContinue** methode.

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
    }

    // ADD THIS PART tooYOUR CODE
    public class Family
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        public string LastName { get; set; }
        public Parent[] Parents { get; set; }
        public Child[] Children { get; set; }
        public Address Address { get; set; }
        public bool IsRegistered { get; set; }
        public override string ToString()
        {
            return JsonConvert.SerializeObject(this);
        }
    }

    public class Parent
    {
        public string FamilyName { get; set; }
        public string FirstName { get; set; }
    }

    public class Child
    {
        public string FamilyName { get; set; }
        public string FirstName { get; set; }
        public string Gender { get; set; }
        public int Grade { get; set; }
        public Pet[] Pets { get; set; }
    }

    public class Pet
    {
        public string GivenName { get; set; }
    }

    public class Address
    {
        public string State { get; set; }
        public string County { get; set; }
        public string City { get; set; }
    }

Kopieer en plak Hallo **CreateFamilyDocumentIfNotExists** methode onder uw **adres** klasse.

    // ADD THIS PART tooYOUR CODE
    private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
            this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
                this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
            }
            else
            {
                throw;
            }
        }
    }

En Voeg twee documenten, één voor Hallo Andersen Family en Hallo Wakefield Family.

Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode na het maken van een verzameling Hallo document.

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


    // ADD THIS PART tooYOUR CODE
    Family andersenFamily = new Family
    {
            Id = "Andersen.1",
            LastName = "Andersen",
            Parents = new Parent[]
            {
                    new Parent { FirstName = "Thomas" },
                    new Parent { FirstName = "Mary Kay" }
            },
            Children = new Child[]
            {
                    new Child
                    {
                            FirstName = "Henriette Thaulow",
                            Gender = "female",
                            Grade = 5,
                            Pets = new Pet[]
                            {
                                    new Pet { GivenName = "Fluffy" }
                            }
                    }
            },
            Address = new Address { State = "WA", County = "King", City = "Seattle" },
            IsRegistered = true
    };

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", andersenFamily);

    Family wakefieldFamily = new Family
    {
            Id = "Wakefield.7",
            LastName = "Wakefield",
            Parents = new Parent[]
            {
                    new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                    new Parent { FamilyName = "Miller", FirstName = "Ben" }
            },
            Children = new Child[]
            {
                    new Child
                    {
                            FamilyName = "Merriam",
                            FirstName = "Jesse",
                            Gender = "female",
                            Grade = 8,
                            Pets = new Pet[]
                            {
                                    new Pet { GivenName = "Goofy" },
                                    new Pet { GivenName = "Shadow" }
                            }
                    },
                    new Child
                    {
                            FamilyName = "Miller",
                            FirstName = "Lisa",
                            Gender = "female",
                            Grade = 1
                    }
            },
            Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
            IsRegistered = false
    };

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

Druk op **F5** toorun uw toepassing.

Gefeliciteerd. U hebt twee Azure Cosmos DB-documenten gemaakt.  

![Diagram ter illustratie Hallo hiërarchische relatie tussen Hallo-account, onlinedatabase Hallo Hallo verzameling en Hallo documenten die worden gebruikt door Hallo NoSQL-zelfstudie toocreate een C#-consoletoepassing](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Stap 7: query's uitvoeren op Azure Cosmos DB-resources
Azure Cosmos DB biedt ondersteuning voor uitgebreide [query's](documentdb-sql-query.md) op de JSON-documenten die zijn opgeslagen in elke verzameling.  Hallo volgende voorbeeldcode bevat verschillende query's: met behulp van zowel SQL Azure Cosmos DB syntaxis als LINQ, die kunnen worden uitgevoerd op basis van documenten die wordt ingevoegd in de vorige stap Hallo Hallo.

Kopieer en plak Hallo **ExecuteSimpleQuery** methode na uw **CreateFamilyDocumentIfNotExists** methode.

    // ADD THIS PART tooYOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find hello Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // hello query is executed synchronously here, but can also be executed asynchronously via hello IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute hello same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode na het Hallo tweede document maken.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

Druk op **F5** toorun uw toepassing.

Gefeliciteerd. U hebt een query uitgevoerd op een Azure Cosmos DB-verzameling.

Hallo volgende diagram illustreert hoe hello Azure Cosmos DB SQL-query syntaxis wordt aangeroepen voor Hallo verzameling die u hebt gemaakt en hello dezelfde logica toegepast toohello LINQ-query.

![Diagram ter illustratie van Hallo bereik en de betekenis van Hallo query die wordt gebruikt door Hallo NoSQL-zelfstudie toocreate een C#-consoletoepassing](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

Hallo [FROM](documentdb-sql-query.md#FromClause) sleutelwoord is optioneel in Hallo query omdat Azure Cosmos DB-query's al één verzameling tooa binnen het bereik zijn. Daarom kan FROM Families f worden ingewisseld door FROM root r, of een andere gewenste variabelenaam. Azure Cosmos DB wordt afgeleid dat Families, root of Hallo variabelenaam u hebt gekozen, verwijzing Hallo huidige verzameling standaard.

## <a id="ReplaceDocument"></a>Stap 8: JSON-document vervangen
Azure Cosmos DB biedt ondersteuning voor het vervangen van JSON-documenten.  

Kopieer en plak Hallo **ReplaceFamilyDocument** methode na uw **ExecuteSimpleQuery** methode.

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode na de queryuitvoering Hallo achter Hallo Hallo-methode. Na het Hallo-document vervangen, Hallo wordt uitgevoerd dezelfde query opnieuw tooview Hallo gewijzigd document.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

Druk op **F5** toorun uw toepassing.

Gefeliciteerd. U hebt een Azure Cosmos DB-document vervangen.

## <a id="DeleteDocument"></a>Stap 9: JSON-document verwijderen
Azure Cosmos DB biedt ondersteuning voor het verwijderen van JSON-documenten.  

Kopieer en plak Hallo **DeleteFamilyDocument** methode na uw **ReplaceFamilyDocument** methode.

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode na Hallo tweede queryuitvoering, achter Hallo Hallo-methode.

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

Druk op **F5** toorun uw toepassing.

Gefeliciteerd. U hebt een Azure Cosmos DB-document verwijderd.

## <a id="DeleteDatabase"></a>Stap 10: Hallo-database verwijderen
Verwijderen Hallo gemaakt van de database wordt verwijderd Hallo-database en alle onderliggende resources (verzamelingen, documenten, enz.).

Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode na Hallo document toodelete Hallo gehele database en alle onderliggende resources verwijderen.

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

Druk op **F5** toorun uw toepassing.

Gefeliciteerd. U hebt een Azure Cosmos DB-database verwijderd.

## <a id="Run"></a>Stap 11: uw C#-consoletoepassing volledig uitvoeren
Druk op F5 in Visual Studio toobuild Hallo toepassing in de foutopsporingsmodus.

U ziet Hallo-uitvoer van uw getstarted-app in een consolevenster. Hallo-uitvoer ziet Hallo resultaten van Hallo query's die zijn toegevoegd en moet overeenkomen met de onderstaande Hallo voorbeeldtekst.

    Created FamilyDB
    Press any key toocontinue ...
    Created FamilyCollection
    Press any key toocontinue ...
    Created Family Andersen.1
    Press any key toocontinue ...
    Created Family Wakefield.7
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key tooexit.

Gefeliciteerd. U hebt Hallo-zelfstudie voltooid en beschikt nu over een werkende C#-consoletoepassing!

## <a id="GetSolution"></a>Volledige Hallo-zelfstudieoplossing ophalen
Als u geen tijd toocomplete Hallo in deze zelfstudie of alleen wilt toodownload Hallo codevoorbeelden stappen, kunt u het krijgen van [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started). 

toobuild hello GetStarted-oplossing, moet u de volgende Hallo:

* Een actief Azure-account. Als u nog geen account hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/).
* Een [Azure Cosmos DB account][cosmos-db-create-account].
* Hallo [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) oplossing is beschikbaar op GitHub.

toorestore hello verwijzingen toohello Azure Cosmos DB .NET SDK in Visual Studio met de rechtermuisknop op Hallo **GetStarted** oplossing in Solution Explorer en klik vervolgens op **NuGet-pakket herstellen inschakelen**. In het bestand App.config Hallo werk vervolgens de waarden bij voor EndpointUrl en AuthorizationKey Hallo zoals beschreven in [tooan Azure DB die Cosmos-account koppelen](#Connect).

Dat is alles, bouw nu de oplossing. Succes!


## <a name="next-steps"></a>Volgende stappen
* Wilt u een complexere ASP.NET MVC-zelfstudie? Zie [ASP.NET MVC-zelfstudie: Web ontwikkelen van toepassingen met Azure Cosmos DB](documentdb-dotnet-application.md).
* Wilt u tooperform schaal en prestaties testen met Azure Cosmos DB? Zie [prestaties en schaal testen met Azure Cosmos-DB](performance-testing.md)
* Meer informatie over hoe te[bewaken aanvragen, gebruik en opslag van Azure DB die Cosmos](monitor-accounts.md).
* Query's uitvoeren op onze voorbeeldgegevensset in Hallo [Queryspeelplaats](https://www.documentdb.com/sql/demo).
* Zie toolearn meer informatie over Azure Cosmos DB [tooAzure Cosmos DB Welkom](https://docs.microsoft.com/azure/cosmos-db/introduction).

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account

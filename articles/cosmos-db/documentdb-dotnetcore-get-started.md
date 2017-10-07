---
title: 'Azure Cosmos DB: aan de slag met de DocumentDB-API met .NET Core | Microsoft Docs'
description: Een zelfstudie waarmee u maakt een online database en C#-consoletoepassing hello Azure Cosmos DB DocumentDB API .NET Core SDK gebruiken.
services: cosmos-db
documentationcenter: .net
author: arramac
manager: jhubbard
editor: 
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 5e7efb327252e9e73e9b2a340820eeecc6937fa5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a>Azure Cosmos DB: Aan de slag met Hallo DocumentDB API en .NET Core
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js voor MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Welkom toohello DocumentDB-API voor Azure Cosmos DB aan de slag met .NET Core zelfstudie. Wanneer u deze zelfstudie hebt voltooid, beschikt u over een consoletoepassing waarmee u Azure Cosmos DB-resources kunt maken en er query's op kunt uitvoeren.

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

Hebt u geen tijd? Geen probleem. Hallo volledige oplossing is beschikbaar op [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started). Springen toohello [Hallo volledige oplossing sectie ophalen](#GetSolution) voor beknopte instructies.

Wilt u toobuild een Xamarin iOS, Android of formulieren met behulp van toepassing hello DocumentDB API en .NET Core SDK? Zie [ontwikkelen van mobiele toepassingen met Xamarin en Azure Cosmos DB](mobile-apps-with-xamarin.md).

> [!NOTE]
> Hello Azure Cosmos DB .NET Core SDK gebruikt in deze zelfstudie is nog niet compatibel met Universal Windows Platform (UWP)-apps. Voor een preview-versie van Hallo .NET Core SDK die ondersteuning biedt voor UWP-apps te e-mailbericht verzenden[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

Tijd om aan de slag te gaan.

## <a name="prerequisites"></a>Vereisten
Controleer of dat u de volgende Hallo hebt:

* Een actief Azure-account. Als u nog geen account hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/). 
    * U kunt ook hello gebruiken [Azure Cosmos DB Emulator](local-emulator.md) voor deze zelfstudie.
* [Visual Studio 2017](https://www.visualstudio.com/vs/) 
    * Als u op Mac OS- of Linux werkt, kunt u Hallo opdrachtregelprogramma .NET Core-apps ontwikkelen Hallo installeren [.NET Core SDK](https://www.microsoft.com/net/core#macos) voor Hallo platform van uw keuze. 
    * Als u in Windows werkt, kunt u .NET Core apps Hallo opdrachtregelprogramma ontwikkelen door het installeren van Hallo [.NET Core SDK](https://www.microsoft.com/net/core#windows). 
    * U kunt uw eigen editor gebruiken of [Visual Studio-code](https://code.visualstudio.com/) downloaden. Deze code is gratis en werkt onder Windows, Linux en Mac OS. 

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Stap 1: een Azure Cosmos DB-account maken
Begin met het maken van een Azure Cosmos DB-account. Als u al een account dat u wilt dat toouse hebt, kunt u verder gaan te[uw Visual Studio-oplossing instellen](#SetupVS). Als u hello Azure Cosmos DB Emulator, volgt u stappen op Hallo [Azure Cosmos DB Emulator](local-emulator.md) toosetup Hallo emulator en gaat u verder te[uw Visual Studio-oplossing instellen](#SetupVS).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Stap 2: uw Visual Studio-oplossing instellen
1. Open **Visual Studio 2017** op uw computer.
2. Op Hallo **bestand** selecteert u **nieuw**, en kies vervolgens **Project**.
3. In Hallo **nieuw Project** dialoogvenster Selecteer **sjablonen** / **Visual C#** / **.NET Core** / **Consoletoepassing (.NET Core)**, uw project een naam **DocumentDBGettingStarted**, en klik vervolgens op **OK**.

   ![Schermopname van het venster Hallo-nieuw Project](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. In Hallo **Solution Explorer**, klik met de rechtermuisknop op **DocumentDBGettingStarted**.
5. Klikt u op zonder Hallo menu **NuGet-pakketten beheren...** .

   ![Schermopname van Hallo rechts op wordt geklikt Menu voor Hallo Project](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. In Hallo **NuGet** tabblad **Bladeren** Hallo boven aan het Hallo-venster en typ **azure documentdb** in het zoekvak Hallo.
7. Binnen Hallo resultaten vinden **Microsoft.Azure.DocumentDB.Core** en klik op **installeren**.
   Hallo pakket-id voor DocumentDB-clientbibliotheek voor .NET Core Hallo [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core). Als u zich richt op een .NET Framework-versie (zoals net461) die niet wordt ondersteund door dit .NET Core NuGet-pakket, gebruikt u [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) die alle versies van .NET Framework vanaf .NET Framework 4.5 ondersteunt.
8. Op Hallo prompts Hallo NuGet-pakket installaties en Hallo licentieovereenkomst te accepteren.

Goed gedaan. Nu dat Hallo setup is voltooid, begint schrijven van code. Op [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) vindt u een voltooid codeproject voor deze zelfstudie.

## <a id="Connect"></a>Stap 3: Verbinding maken met tooan Azure DB die Cosmos-account
Voeg eerst deze verwijzingen toohello begin van de C#-toepassing, in het bestand Program.cs Hallo:

```csharp
using System;

// ADD THIS PART tooYOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> In deze zelfstudie voor toocomplete order, zorg ervoor dat u Hallo bovenstaande afhankelijkheden toevoegen.

Voeg nu deze twee constanten en de variabele *client* toe onder de openbare klasse *Program*.

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

Vervolgens head toohello [Azure Portal](https://portal.azure.com) tooretrieve uw URI en primaire sleutel. Hello Azure Cosmos DB URI en primaire sleutel nodig zijn voor uw toepassing toounderstand waar tooconnect en voor Azure Cosmos DB tootrust van uw toepassing verbinding.

In Azure Portal Hallo, navigeer tooyour Azure DB die Cosmos-account en klik op **sleutels**.

Hallo URI van de portal Hallo Kopieer en plak deze in `<your endpoint URI>` in het bestand program.cs Hallo. Vervolgens kopiëren primaire sleutel van de portal Hallo Hallo en plak deze in `<your key>`. Als u hello Azure Cosmos DB Emulator, gebruikt u `https://localhost:8081` als Hallo eindpunt en Hallo goed gedefinieerde autorisatiesleutel van [hoe met behulp van toodevelop hello Azure Cosmos DB Emulator](local-emulator.md). Zorg ervoor dat tooremove Hallo < en >, maar laat Hallo dubbele aanhalingstekens rond uw eindpunt en -sleutel.

![Schermopname van hello Azure Portal gebruikt door Hallo NoSQL-zelfstudie toocreate een C#-consoletoepassing. Ziet u een Cosmos Azure DB-account met de actieve hub Hallo gemarkeerd, Hallo knop sleutels gemarkeerd op de blade hello Azure DB die Cosmos-account en de waarden URI, primaire sleutel en secundaire sleutel Hallo gemarkeerd op Hallo blade sleutels][keys]

We ophalen gestarte toepassing hello beginnen met het maken van een nieuw exemplaar van Hallo **DocumentClient**.

Hieronder Hallo **Main** methode toevoegen van nieuwe asynchrone taak aangeroepen **GetStartedDemo**, die wordt een exemplaar van onze nieuwe **DocumentClient**.

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART tooYOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

Voeg Hallo volgende code toorun uw asynchrone taak van uw **Main** methode. Hallo **Main** methode wordt onderschept uitzonderingen en toohello console geschreven.

```csharp
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
```

Druk op Hallo **DocumentDBGettingStarted** toobuild knop en het Hallo-toepassing worden uitgevoerd.

Gefeliciteerd. U hebt verbinding gemaakt tooan Azure DB die Cosmos-account, laten we nu eens kijken werken met Azure DB die Cosmos-resources.  

## <a name="step-4-create-a-database"></a>Stap 4: een database maken
Voordat u Hallo-code voor het maken van een database toevoegt, Voeg een Help-methode voor het schrijven van toohello-console.

Kopieer en plak Hallo **WriteToConsoleAndPromptToContinue** methode onder Hallo **GetStartedDemo** methode.

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

Uw Azure-Cosmos-DB [database](documentdb-resources.md#databases) kunnen worden gemaakt met behulp van Hallo [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) methode Hallo **DocumentClient** klasse. Een database is een logische container voor documentopslag, gepartitioneerd in verzamelingen JSON Hallo.

Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode onder Hallo client maken. Hiermee maakt u een database met de naam *FamilyDB*.

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

Druk op Hallo **DocumentDBGettingStarted** knop toorun uw toepassing.

Gefeliciteerd. U hebt een Azure Cosmos DB-database gemaakt.  

## <a id="CreateColl"></a>Stap 5: een verzameling maken
> [!WARNING]
> Met **CreateDocumentCollectionAsync** maakt u een nieuwe verzameling met gereserveerde doorvoer, wat gevolgen heeft voor de kosten. Zie onze [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/) voor meer informatie.

Een [verzameling](documentdb-resources.md#collections) kunnen worden gemaakt met behulp van Hallo [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) methode Hallo **DocumentClient** klasse. Een verzameling is een container van JSON-documenten en de bijbehorende JavaScript-toepassingslogica.

Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode onder Hallo database wordt gemaakt. Hiermee maakt u een documentverzameling met de naam *FamilyCollection_oa*.

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

Druk op Hallo **DocumentDBGettingStarted** knop toorun uw toepassing.

Gefeliciteerd. U hebt een Azure Cosmos DB-documentverzameling gemaakt.  

## <a id="CreateDoc"></a>Stap 6: JSON-documenten maken
Een [document](documentdb-resources.md#documents) kunnen worden gemaakt met behulp van Hallo [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) methode Hallo **DocumentClient** klasse. Documenten bestaan uit door gebruikers gedefinieerde (willekeurige) JSON-inhoud. U kunt nu een of meer documenten invoegen. Als u gegevens die u wilt toostore in de database al hebt, kunt u Azure Cosmos DB [hulpprogramma voor gegevensmigratie](import-data.md).

We moeten eerst toocreate een **familie** klasse die objecten die zijn opgeslagen in Azure Cosmos DB in dit voorbeeld wordt aangegeven. Daarnaast moeten de subklassen **Parent**, **Child**, **Pet** en **Address** worden gemaakt die in de klasse **Family** worden gebruikt. Houd er rekening mee dat de documenten een **id**-eigenschap moeten bevatten die in JSON is geserialiseerd als **id**. Maak deze klassen door toe te voegen na interne onderliggende klassen na Hallo Hallo **GetStartedDemo** methode.

Kopieer en plak Hallo **familie**, **bovenliggende**, **onderliggende**, **huisdier**, en **adres** klassen onder Hallo **WriteToConsoleAndPromptToContinue** methode.

```csharp
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
```

Kopieer en plak Hallo **CreateFamilyDocumentIfNotExists** methode onder uw **CreateDocumentCollectionIfNotExists** methode.

```csharp
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
```

En Voeg twee documenten, één voor Hallo Andersen Family en Hallo Wakefield Family.

Kopieer en plak Hallo-code die volgt `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** methode onder Hallo verzamelen van documenten.

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

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

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

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

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

Druk op Hallo **DocumentDBGettingStarted** knop toorun uw toepassing.

Gefeliciteerd. U hebt twee Azure Cosmos DB-documenten gemaakt.  

![Diagram ter illustratie Hallo hiërarchische relatie tussen Hallo-account, onlinedatabase Hallo Hallo verzameling en Hallo documenten die worden gebruikt door Hallo NoSQL-zelfstudie toocreate een C#-consoletoepassing](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Stap 7: query's uitvoeren op Azure Cosmos DB-resources
Azure Cosmos DB biedt ondersteuning voor uitgebreide [query's](documentdb-sql-query.md) op de JSON-documenten die zijn opgeslagen in elke verzameling.  Hallo volgende voorbeeldcode bevat verschillende query's: met behulp van zowel SQL Azure Cosmos DB syntaxis als LINQ, die kunnen worden uitgevoerd op basis van documenten die wordt ingevoegd in de vorige stap Hallo Hallo.

Kopieer en plak Hallo **ExecuteSimpleQuery** methode onder uw **CreateFamilyDocumentIfNotExists** methode.

```csharp
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
```

Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode onder Hallo tweede document maken.

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

Druk op Hallo **DocumentDBGettingStarted** knop toorun uw toepassing.

Gefeliciteerd. U hebt een query uitgevoerd op een Azure Cosmos DB-verzameling.

Hallo volgende diagram illustreert hoe hello Azure Cosmos DB SQL-query syntaxis wordt aangeroepen voor Hallo verzameling die u hebt gemaakt en hello dezelfde logica toegepast toohello LINQ-query.

![Diagram ter illustratie van Hallo bereik en de betekenis van Hallo query die wordt gebruikt door Hallo NoSQL-zelfstudie toocreate een C#-consoletoepassing](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

Hallo [FROM](documentdb-sql-query.md#FromClause) sleutelwoord is optioneel in Hallo query omdat Azure Cosmos DB-query's al één verzameling tooa binnen het bereik zijn. Daarom kan FROM Families f worden ingewisseld door FROM root r, of een andere gewenste variabelenaam. DocumentDB wordt afgeleid dat Families, root of Hallo variabelenaam u hebt gekozen, verwijzing Hallo huidige verzameling standaard.

## <a id="ReplaceDocument"></a>Stap 8: JSON-document vervangen
Azure Cosmos DB biedt ondersteuning voor het vervangen van JSON-documenten.  

Kopieer en plak Hallo **ReplaceFamilyDocument** methode onder uw **ExecuteSimpleQuery** methode.

```csharp
// ADD THIS PART tooYOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode onder Hallo queryuitvoering. Na het Hallo-document vervangen, Hallo wordt uitgevoerd dezelfde query opnieuw tooview Hallo gewijzigd document.

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

Druk op Hallo **DocumentDBGettingStarted** knop toorun uw toepassing.

Gefeliciteerd. U hebt een Azure Cosmos DB-document vervangen.

## <a id="DeleteDocument"></a>Stap 9: JSON-document verwijderen
Azure Cosmos DB biedt ondersteuning voor het verwijderen van JSON-documenten.  

Kopieer en plak Hallo **DeleteFamilyDocument** methode onder uw **ReplaceFamilyDocument** methode.

```csharp
// ADD THIS PART tooYOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode onder Hallo tweede queryuitvoering.

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

Druk op Hallo **DocumentDBGettingStarted** knop toorun uw toepassing.

Gefeliciteerd. U hebt een Azure Cosmos DB-document verwijderd.

## <a id="DeleteDatabase"></a>Stap 10: Hallo-database verwijderen
Verwijderen Hallo gemaakt van de database wordt verwijderd Hallo-database en alle onderliggende resources (verzamelingen, documenten, enz.).

Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode onder Hallo document toodelete Hallo gehele database en alle onderliggende resources verwijderen.

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

Druk op Hallo **DocumentDBGettingStarted** knop toorun uw toepassing.

Gefeliciteerd. U hebt een Azure Cosmos DB-database verwijderd.

## <a id="Run"></a>Stap 11: uw C#-consoletoepassing volledig uitvoeren
Druk op Hallo **DocumentDBGettingStarted** knop in Visual Studio toobuild Hallo toepassing in de foutopsporingsmodus.

U ziet de uitvoer van uw getstarted-app in het consolevenster Hallo Hallo. Hallo-uitvoer ziet Hallo resultaten van Hallo query's die zijn toegevoegd en moet overeenkomen met de onderstaande Hallo voorbeeldtekst.

```
Created FamilyDB_oa
Press any key toocontinue ...
Created FamilyCollection_oa
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
```

Gefeliciteerd. U hebt Hallo-zelfstudie voltooid en beschikt nu over een werkende C#-consoletoepassing!

## <a id="GetSolution"></a>Volledige Hallo-zelfstudieoplossing ophalen
toobuild hello GetStarted-oplossing die alle Hallo voorbeelden in dit artikel bevat, moet u de volgende Hallo:

* Een actief Azure-account. Als u nog geen account hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/).
* Een [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].
* Hallo [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) oplossing is beschikbaar op GitHub.

toorestore hello verwijzingen toohello DocumentDB-API voor Azure Cosmos DB .NET Core SDK in Visual Studio met de rechtermuisknop op Hallo **GetStarted** oplossing in Solution Explorer en klik vervolgens op **inschakelen NuGet-pakket herstellen**. In het bestand Program.cs Hallo werk vervolgens de waarden bij voor EndpointUrl en AuthorizationKey Hallo zoals beschreven in [tooan Azure DB die Cosmos-account koppelen](#Connect).

## <a name="next-steps"></a>Volgende stappen
* Wilt u een complexere ASP.NET MVC-zelfstudie? Zie [ASP.NET MVC-zelfstudie: Web ontwikkelen van toepassingen met Azure Cosmos DB](documentdb-dotnet-application.md).
* Wilt u toodevelop een Xamarin iOS, Android of formulieren DocumentDB-API voor Azure Cosmos DB .NET Core SDK gebruikt toepassing hello? Zie [ontwikkelen van mobiele toepassingen met Xamarin en Azure Cosmos DB](mobile-apps-with-xamarin.md).
* Wilt u tooperform schaal en prestaties testen met Azure Cosmos DB? Zie [prestaties en schaal testen met Azure Cosmos-DB](performance-testing.md)
* Meer informatie over hoe te[Monitor Azure Cosmos DB aanvragen, het gebruik en de opslag](monitor-accounts.md).
* Query's uitvoeren op onze voorbeeldgegevensset in Hallo [Queryspeelplaats](https://www.documentdb.com/sql/demo).
* toolearn meer informatie over het programmeermodel hello, Zie [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png

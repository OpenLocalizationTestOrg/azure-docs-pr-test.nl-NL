---
title: 'Azure Cosmos DB: Ontwikkelen met Hallo tabel API in .NET | Microsoft Docs'
description: Meer informatie over hoe toodevelop met tabel-API van Azure Cosmos DB met .NET
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a>Azure Cosmos DB: Ontwikkelen met Hallo tabel API in .NET

Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft. U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren.

Deze zelfstudie behandelt Hallo taken te volgen: 

> [!div class="checklist"] 
> * Maak een Azure Cosmos DB-account 
> * Schakel de functionaliteit in Hallo app.config-bestand 
> * Een tabel maken met de Hallo [tabel API](table-introduction.md) (preview)
> * Een entiteit tooa tabel toevoegen 
> * Een batch entiteiten invoegen 
> * Eén entiteit ophalen 
> * Query-entiteiten met behulp van automatische secundaire indexen 
> * Een entiteit vervangen 
> * Een entiteit verwijderen 
> * Een tabel verwijderen
 
## <a name="tables-in-azure-cosmos-db"></a>Tabellen in Azure Cosmos DB 

Azure Cosmos DB biedt Hallo [tabel API](table-introduction.md) (preview) voor toepassingen die een sleutel-waardearchief met een schema-less-ontwerp moeten. [Azure Table storage](../storage/common/storage-introduction.md) SDK's en REST-API's kunnen worden gebruikt toowork met Azure Cosmos DB. U kunt Azure Cosmos DB toocreate tabellen met hoge doorvoer vereisten. Azure Cosmos DB ondersteunt tabellen die zijn geoptimaliseerd voor doorvoer (ook wel eens premium-tabellen genoemd), en is momenteel beschikbaar in de openbare preview-versie. 

Toouse Azure Table storage voor tabellen met hoge opslag en lagere doorvoer vereisten kan worden voortgezet. Ondersteuning voor tabellen geoptimaliseerd voor opslag in een toekomstige update leidt tot Azure Cosmos DB en bestaande en nieuwe Azure Table storage-accounts naadloos worden bijgewerkt tooAzure Cosmos DB.

Als u momenteel Azure Table storage, krijgt u de volgende voordelen met preview-Hallo 'tabel premium' hello:

- Directe [globale distributie](distribute-data-globally.md) met multihoming en [automatische en handmatige failover](regional-failover.md)
- Ondersteuning voor automatische schema-networkdirect indexeren tegen alle eigenschappen ('secundaire indexen') en snelle query 's 
- Ondersteuning voor [onafhankelijke schalen van opslag en doorvoer](partition-data.md), via verschillende regio's
- Ondersteuning voor [toegewezen doorvoer per tabel](request-units.md) die kunnen worden geschaald van honderden toomillions van aanvragen per seconde
- Ondersteuning voor [vijf instelbare consistentieniveaus](consistency-levels.md) tootrade beschikbaarheid, latentie en consistentiecontroles uit op basis van de behoeften van uw toepassing
- 99,99% beschikbaarheid binnen één regio en de mogelijkheid tooadd meer regio's voor hogere beschikbaarheid en [toonaangevende uitgebreide serviceovereenkomsten](https://azure.microsoft.com/support/legal/sla/cosmos-db/) op algemene beschikbaarheid
- Werken met Hallo bestaande Azure-opslag .NET SDK en er geen code wijzigingen tooyour toepassing

Tijdens het Hallo-preview hello Azure Cosmos DB ondersteunt tabel-API met behulp van Hallo .NET SDK. U kunt downloaden Hallo [Preview-SDK van Azure Storage](https://aka.ms/premiumtablenuget) vanuit NuGet, die Hallo is dezelfde klassen- en handtekeningen als Hallo [Azure-opslag-SDK](https://www.nuget.org/packages/WindowsAzure.Storage), ook verbinding kan maken met tooAzure Cosmos DB accounts met Hallo Tabel-API.

toolearn meer informatie over complexe taken voor Azure Table-opslag, Zie:

* [Inleiding tooAzure Cosmos DB: tabel-API](table-introduction.md)
* Tabel-naslagdocumentatie voor meer informatie over beschikbare API's Hallo [Storage-clientbibliotheek voor .NET-verwijzing](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)

### <a name="about-this-tutorial"></a>Over deze zelfstudie
Voor ontwikkelaars die bekend bent met hello Azure Table storage SDK en wilt toouse Hallo Premiumfuncties die beschikbaar is in deze zelfstudie met behulp van Azure Cosmos DB. Deze is gebaseerd op [aan de slag met Azure Table storage met .NET](table-storage-how-to-use-dotnet.md) en ziet u hoe tootake profiteren van extra mogelijkheden, zoals secundaire indexen, ingerichte doorvoer en multihoming. We hebben betrekking op hoe toouse hello Azure portal toocreate een Cosmos-DB Azure-account, en vervolgens bouwen en implementeren van de toepassing van een tabel. We helpt ook bij .NET-voorbeelden voor het maken en verwijderen van een tabel en invoegen, bijwerken, verwijderen en opvragen van tabelgegevens. 

Als u Visual Studio 2017 geïnstalleerd nog geen hebt, kunt u downloaden en gebruiken van Hallo **gratis** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Zorg ervoor dat u inschakelt **ontwikkelen van Azure** tijdens de installatie van Visual Studio Hallo.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Een databaseaccount maken

Begint met het maken van een Azure DB die Cosmos-account in hello Azure-portal.  

> [!TIP]
> * Hebt u al een Azure DB die Cosmos-account? Als dit het geval is, gaat u verder te[instellen van uw Visual Studio-oplossing](#SetupVS).
> * Hebt u een Azure-DocumentDB-account? Als u dus uw account is nu een Cosmos-DB Azure-account en kunt u verder gaan te[instellen van uw Visual Studio-oplossing](#SetupVS).  
> * Als u hello Azure Cosmos DB Emulator, volgt u stappen op Hallo [Azure Cosmos DB Emulator](local-emulator.md) toosetup Hallo emulator en gaat u verder te[instellen van uw Visual Studio-oplossing](#SetupVS).
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a>Hallo-voorbeeldtoepassing klonen

Nu gaan we een tabel-app vanuit github Hallo verbindingsreeks instellen en voer dit klonen.

1. Open een git-terminalvenster zoals git bash en en `cd` tooa werkmap.  

2. Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. Open het oplossingsbestand Hallo in Visual Studio.

## <a name="update-your-connection-string"></a>Uw verbindingsreeks bijwerken

Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app.

1. In Hallo [Azure-portal](http://portal.azure.com/), in uw Azure DB-Cosmos-account, klik op in de linkernavigatiebalk Hallo **sleutels**, en klik vervolgens op **lezen-schrijven sleutels**. Gebruikt u de knoppen kopiëren Hallo aan de rechterkant Hallo van Hallo scherm toocopy Hallo-verbindingsreeks in Hallo app.config-bestand in de volgende stap Hallo.

2. Open in Visual Studio Hallo app.config-bestand. 

3. Kopieer de waarde van de URI van Hallo-portal (met behulp van de knop kopiëren Hallo), waardoor het Hallo Hallo account-sleutelwaarde in app.config. Hallo-accountnaam eerder hebt gemaakt voor account-name in app.config gebruiken.
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> toouse deze app met standaard Azure Table Storage, moet u toochange Hallo-verbindingsreeks in `app.config file`. Hallo-accountnaam gebruiken als tabel accountnaam en de sleutel als Azure Storage primaire sleutel. <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a>Hallo-app bouwen en implementeren
1. In Visual Studio met de rechtermuisknop op Hallo-project in **Solution Explorer** en klik vervolgens op **NuGet-pakketten beheren**. 

2. In Hallo NuGet **Bladeren** in het vak ***WindowsAzure.Storage PremiumTable***. Controleer **omvatten prerelease-versie**.

3. Installeren in Hallo resultaten Hallo **WindowsAzure.Storage PremiumTable** en kies Hallo preview-build `0.0.1-preview`. Deze actie installeert hello Azure Table storage pakket en alle afhankelijkheden.

4. Klik op CTRL + F5 toorun Hallo-toepassing. 

U kunt nu gaat u terug tooData Explorer en Zie query, wijzigen en werken met de gegevens van deze tabel. 

> [!NOTE]
> toouse deze app met een Azure Cosmos DB Emulator, u zojuist hebt moet toochange Hallo-verbindingsreeks in `app.config file`. Hallo onder waarde voor de emulator gebruiken. <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a>Mogelijkheden van Azure DB Cosmos
Azure Cosmos DB ondersteunt een aantal mogelijkheden die niet beschikbaar in hello Azure Table storage-API. Hallo nieuwe functionaliteit kan worden ingeschakeld via de volgende Hallo `appSettings` configuratiewaarden. Wij kon niet alle nieuwe handtekeningen overloads toohello voorbeeld of Azure-opslag-SDK introduceren. Hiermee kunt u tooconnect tooboth standard en premium-tabellen en werken met andere Azure Storage-services zoals Blobs en wachtrijen. 


| Sleutel | Beschrijving |
| --- | --- |
| TableConnectionMode  | Azure Cosmos DB ondersteunt twee modi voor connectiviteit. In `Gateway` modus aanvragen worden altijd gedaan toohello Azure DB die Cosmos-gateway het toohello bijbehorende gegevenspartities stuurt. In `Direct` connectiviteitsmodus, Hallo client haalt Hallo toewijzing van tabellen toopartitions en aanvragen worden gedaan, rechtstreeks op basis van de gegevenspartities. Het is raadzaam `Direct`, Hallo standaard.  |
| TableConnectionProtocol | Azure Cosmos DB ondersteunt twee verbindingsprotocollen - `Https` en `Tcp`. `Tcp`is de standaardinstelling Hallo en aanbevolen omdat het meer lightweight. |
| TablePreferredLocations | Door komma's gescheiden lijst met aanbevolen (multihoming) locaties voor leesbewerkingen. Elke Azure DB die Cosmos-account kan worden gekoppeld met 1-30 + regio's. Elk clientexemplaar kunt u een subset van deze gebieden in volgorde van voorkeur Hallo voor lage latentie leesbewerkingen opgeven. Hallo-regio's moeten de namen van hun [weergavenamen](https://msdn.microsoft.com/library/azure/gg441293.aspx), bijvoorbeeld `West US`. Zie ook [multihoming API's](tutorial-global-distribution-table.md).
| TableConsistencyLevel | U kunt uitschakelen handel tussen latentie, consistentie en beschikbaarheid door te kiezen tussen vijf goed gedefinieerde consistentieniveaus: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, en `Eventual`. Standaard is `Session`. Hallo keuze van de consistentieniveau maakt een belangrijke prestatieverbetering verschil in meerdere landen/regio-instellingen. Zie [consistentieniveaus](consistency-levels.md) voor meer informatie. |
| TableThroughput | Gereserveerde doorvoer voor Hallo tabel uitgedrukt in aanvraageenheden (RU) per seconde. Biedt ondersteuning voor één tabellen 100s-miljoenen RU/s. Zie [Aanvraageenheden](request-units.md). Standaard is`400` |
| TableIndexingPolicy | Consistente en automatische secundaire indexeren van alle kolommen in tabellen | JSON-tekenreeks die voldoen toohello beleidsspecificatie van het te indexeren. Zie [indexeren beleid](indexing-policies.md) toosee hoe u indexering beleid tooinclude en uitsluiten specifieke kolommen kunt wijzigen. | Automatische indexering van alle eigenschappen (hash voor tekenreeksen) en bereik voor getallen |
| TableQueryMaxItemCount | Maximum aantal items geretourneerd per tabelquery in een enkel retour Hallo configureren. Standaard is `-1`, waarmee Azure Cosmos DB dynamisch bepalen Hallo waarde tijdens runtime. |
| TableQueryEnableScan | Als Hallo query niet kan Hallo index voor elk filter, voer het toch via een scan. Standaard is `false`.|
| TableQueryMaxDegreeOfParallelism | Hallo mate van parallelle uitvoering voor uitvoering van een query cross-partitie. `0`seriële met geen vooraf ophalen, is `1` serieel met vooraf ophalen en hogere waarden toename Hallo frequentie van parallelle uitvoering. Standaard is `-1`, waarmee Azure Cosmos DB dynamisch bepalen Hallo waarde tijdens runtime. |

toochange Hallo-standaardwaarde, open Hallo `app.config` bestand vanuit Solution Explorer in Visual Studio. Hallo-inhoud van Hallo toevoegen `<appSettings>` element hieronder weergegeven. Vervang `account-name` met Hallo-naam van uw opslagaccount en `account-key` door de toegangssleutel voor uw account. 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

We maken een kort overzicht van wat in Hallo-app gebeurt er. Open Hallo `Program.cs` bestands- en u vindt dat deze regels code Hallo tabel resources maken. 

## <a name="create-hello-table-client"></a>Hallo tabel client maken
U initialiseren een `CloudTableClient` tooconnect toohello tabel account.

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
Deze client is geïnitialiseerd met behulp van Hallo `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, en `TablePreferredLocations` configuratiewaarden als opgegeven in de instellingen van de Hallo-app.
    
## <a name="create-a-table"></a>Een tabel maken
Maakt u een tabel met `CloudTable`. Tabellen in Azure Cosmos DB onafhankelijk kunnen schalen in termen van opslag en de doorvoer en automatisch partitioneren is verwerkt door Hallo-service. Azure Cosmos DB ondersteunt zowel vaste grootte als onbeperkt aantal tabellen. Zie [partitioneren in Azure Cosmos DB](partition-data.md) voor meer informatie. 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

Er is een belangrijk verschil in hoe tabellen worden gemaakt. Azure Cosmos DB reserveert doorvoer, in tegenstelling tot Azure storage op basis van verbruik model voor transacties. Hallo-reservering model biedt twee belangrijke voordelen:

* De doorvoer is toegewezen/gereserveerd, zodat u nooit kunnen beperkt ophalen als uw aanvraagsnelheid op of onder uw ingerichte doorvoer is
* Hallo-reservering model is meer [rendabel voor doorvoer zware workloads](key-value-store-cost.md)

U kunt Hallo standaard doorvoer configureren door het Hallo-instelling voor `TableThroughput` in termen van RU (aanvraageenheden) per seconde. 

Het lezen van een entiteit 1 KB is genormaliseerd als 1 RU en andere bewerkingen zijn genormaliseerde tooa vaste RU-waarde op basis van hun verbruik CPU, geheugen en IOPS. Meer informatie over [Aanvraageenheden in Azure Cosmos DB](request-units.md).

> [!NOTE]
> Terwijl de SDK-tabelopslag biedt momenteel geen ondersteuning voor doorvoer wijzigen, kunt u Hallo doorvoer onmiddellijk op elk gewenst moment hello Azure-portal of Azure CLI.

Vervolgens we doorlopen Hallo eenvoudige lezen en schrijven (CRUD)-bewerkingen met hello Azure Table storage SDK. Deze zelfstudie wordt gedemonstreerd voorspelbare lage één cijfer milliseconde latenties en snelle query's die worden geleverd door Azure Cosmos DB.

## <a name="add-an-entity-tooa-table"></a>Een entiteit tooa tabel toevoegen
Entiteiten in de Azure-tabelopslag van Hallo uitbreiden `TableEntity` klasse en moet `PartitionKey` en `RowKey` eigenschappen. Hier volgt een voorbeeld-definitie voor een klantentiteit.

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

Hallo volgende fragment toont hoe tooinsert een entiteit met Azure storage SDK Hallo. Azure Cosmos DB is ontworpen voor lage latentie op elke schaal gegarandeerd via Hallo wereld.

Schrijfbewerkingen voltooien < 15 ms op p99 en ~ 6 ms op p50 voor toepassingen die worden uitgevoerd dezelfde regio bevinden als hello Azure Cosmos DB account Hallo. En deze duur accounts voor Hallo fact die schrijft back toohello client zijn bevestigd nadat ze zijn synchroon gerepliceerd, blijvend doorgevoerd, en alle inhoud wordt geïndexeerd.

Hallo tabel-API voor Azure DB die Cosmos is een Preview-versie. Algemene beschikbaarheid worden Hallo p99 latentie garanties ondersteund door serviceovereenkomsten net als andere Azure Cosmos DB-API's. 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a>Een batch entiteiten invoegen
Azure Table storage ondersteunt een bewerking API van batch, waarmee u updates, verwijderingen, combineren en voegt in dezelfde batchbewerking Hallo. Azure Cosmos DB heeft geen enkele van Hallo beperkingen op Hallo batch-API als Azure Table storage. Bijvoorbeeld, kunt u meerdere leesbewerkingen binnen een batch uitvoeren, kunt u meerdere schrijfbewerkingen toohello uitvoeren dezelfde entiteit binnen een batch en er is geen limiet van 100 bewerkingen per batch. 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a>Eén entiteit ophalen
(Opgehaald) opgehaald in Azure Cosmos DB voltooid < 10 ms op p99 en ~ 1 ms op p50 in Hallo dezelfde Azure-regio. Zo veel gebieden tooyour account toevoegen voor leesbewerkingen lage latentie en implementeren van toepassingen tooread van hun lokale regio ('multihomed') door in te stellen `TablePreferredLocations`. 

U kunt met behulp van de volgende codefragment Hallo één entiteit ophalen:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> Meer informatie over multihoming API's op [ontwikkelen met meerdere regio's](tutorial-global-distribution-table.md)
>

## <a name="query-entities-using-automatic-secondary-indexes"></a>Query-entiteiten met behulp van automatische secundaire indexen
Tabellen kunnen worden opgevraagd met Hallo `TableQuery` klasse. Azure Cosmos-database heeft een schrijven geoptimaliseerd database-engine die automatisch alle kolommen in de tabel indexeert. Indexeren in Azure DB die Cosmos is agnostisch tooschema. Dus wordt zelfs als uw schema afwijkt van rijen, of als Hallo schema gedurende een bepaalde periode zich verder ontwikkelen, deze automatisch geïndexeerd. Omdat Azure Cosmos DB automatische secundaire indexen ondersteunt, wordt een query uitgevoerd naar een eigenschap Hallo index kunnen gebruiken en efficiënt worden geleverd.

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

In voorbeeld van Azure DB die Cosmos Hallo ondersteunt dezelfde functionaliteit als Azure Table-opslag voor Hallo API van de tabel zoeken. Azure Cosmos DB biedt ook ondersteuning voor sorteren, statistische functies, georuimtelijke query hiërarchie en een groot aantal ingebouwde functies. Hallo aanvullende functionaliteit worden vermeld in de tabel API Hallo in een toekomstige service-update. Zie [Azure Cosmos DB-query](documentdb-sql-query.md) voor een overzicht van deze mogelijkheden. 

## <a name="replace-an-entity"></a>Een entiteit vervangen
tooupdate een entiteit ophalen uit de tabelservice hello, Hallo entiteitsobject wijzigen en vervolgens weer toohello tabelservice Hallo wijzigingen opslaan. Hallo wijzigt volgende code het telefoonnummer van een bestaande klant. 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
Op deze manier kunt u uitvoeren `InsertOrMerge` of `Merge` bewerkingen.  

## <a name="delete-an-entity"></a>Een entiteit verwijderen
U kunt een entiteit gemakkelijk verwijderen nadat u deze hebt opgehaald met behulp van Hallo hetzelfde patroon weergegeven voor het bijwerken van een entiteit. Hallo na de code opgehaald en wordt een klantentiteit verwijderd.

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a>Een tabel verwijderen
Ten slotte verwijdert Hallo volgende codevoorbeeld een tabel uit een opslagaccount. U kunt verwijderen en opnieuw maken van een tabel met Azure Cosmos DB onmiddellijk.

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a>Resources opschonen 

Als u deze app niet toocontinue toouse gaat, gebruikt u Hallo stappen toodelete alle resources die zijn gemaakt met deze zelfstudie in hello Azure-portal te volgen.   

1. Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt.  
2. Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**. 

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie wordt besproken hoe tooget gestart met behulp van Azure DB die Cosmos Hello tabel API en u Hallo volgende hebt gedaan: 

> [!div class="checklist"] 
> * Een Azure DB die Cosmos-account gemaakt 
> * Ingeschakelde functionaliteit in Hallo app.config-bestand 
> * Een tabel gemaakt 
> * Een entiteit tooa tabel toegevoegd 
> * Een batch entiteiten invoegen 
> * Één entiteit opgehaald 
> * De query entiteiten met behulp van automatische secundaire indexen 
> * Een entiteit vervangen 
> * Een entiteit wordt verwijderd 
> * Een tabel verwijderd  

U kunt nu de volgende zelfstudie toohello gaan en meer informatie over het opvragen van tabelgegevens. 

> [!div class="nextstepaction"]
> [Query's uitvoeren met Hallo tabel-API](tutorial-query-table.md)

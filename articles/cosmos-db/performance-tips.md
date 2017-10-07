---
title: aaaPerformance tips - Azure Cosmos DB NoSQL | Microsoft Docs
description: Meer informatie over client configuration opties tooimprove Azure Cosmos DB prestaties van de database
keywords: hoe tooimprove prestaties database
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 94ff155e-f9bc-488f-8c7a-5e7037091bb9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: mimig
ms.openlocfilehash: 4f3e82ae5048e3dbc20b0fd891a2d3aa22adf3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tips-for-azure-cosmos-db"></a>Tips voor betere prestaties voor Azure Cosmos-DB
Azure Cosmos-database is een snelle en flexibele gedistribueerde database waarin naadloos met gegarandeerde latentie en doorvoer schaalt. U geen toomake architectuur van belangrijke wijzigingen hebben of complexe code tooscale uw database met Cosmos DB schrijven. Omhoog en omlaag schalen is net zo eenvoudig als het maken van één API-aanroep of [SDK-aanroep van methode](set-throughput.md#set-throughput-sdk). Omdat Cosmos DB wordt benaderd zijn er netwerk aanroepen clientzijde optimalisaties kunt u tooachieve optimale prestaties.

Dus als u vraagt "hoe kan ik mijn de databaseprestaties verbeteren?" Houd rekening met Hallo volgende opties:

## <a name="networking"></a>Netwerken
<a id="direct-connection"></a>

1. **Verbindingsbeleid: de modus rechtstreekse verbinding gebruiken**

    Hoe een client verbinding maakt met tooCosmos DB heeft belangrijke gevolgen voor de prestaties, met name in termen van waargenomen-clientzijde latentie. Er zijn twee belangrijke configuratie-instellingen beschikbaar zijn voor het configureren van client verbindingsbeleid – Hallo verbinding *modus* en Hallo [verbinding *protocol*](#connection-protocol).  Hallo-modi voor twee beschikbaar zijn:

   1. Gateway-modus (standaard)
   2. Directe modus

      Gateway-modus wordt ondersteund op alle SDK-platforms en is de standaardinstelling Hallo geconfigureerd.  Als uw toepassing wordt uitgevoerd binnen een bedrijfsnetwerk met strikte firewallbeperkingen, is Gateway modus Hallo beste keuze omdat maakt gebruik van Hallo HTTPS-poort en één eindpunt. Hallo prestaties afweging, is echter dat Gateway modus betrekking heeft op een extra netwerk-hop telkens wanneer gegevens worden gelezen of geschreven tooCosmos DB. Daarom biedt directe modus betere prestaties vanwege toofewer netwerkhops.
<a id="use-tcp"></a>
2. **Verbindingsbeleid: Hallo TCP-protocol gebruiken**

    Wanneer u directe modus gebruikt, zijn er twee protocolopties beschikbaar:

   * TCP
   * HTTPS

     Cosmos DB biedt een eenvoudige en RESTful-programmeermodel openen via HTTPS. Daarnaast biedt het een efficiënte TCP-protocol, dat is ook RESTful in het communicatiemodel en is beschikbaar via Hallo .NET SDK voor clients. Directe TCP- en HTTPS worden SSL gebruiken voor eerste authenticatie en versleuteling verkeer. Gebruik voor de beste prestaties Hallo TCP-protocol indien mogelijk.

     Bij gebruik van TCP in de modus van de Gateway, TCP-poort 443 Hallo Cosmos-DB-poort is en 10255 hello MongoDB-API-poort is. Bij gebruik van TCP in modus voor Direct in toevoeging toohello Gateway poorten, moet u tooensure Hallo poort bereik tussen 10000 en 20000 is geopend, omdat de Cosmos-database maakt gebruik van dynamische TCP-poorten. Als deze poorten niet geopend zijn en u toouse TCP probeert, ontvangt u een 503 Service niet beschikbaar-fout.

     Hallo Connectiviteitsmodus wordt geconfigureerd tijdens de constructiefase Hallo van Hallo DocumentClient exemplaar met de Hallo ConnectionPolicy parameter. Als de modus Direct wordt gebruikt, kan Hallo Protocol ook worden ingesteld binnen Hallo ConnectionPolicy parameter.

    ```C#
    var serviceEndpoint = new Uri("https://contoso.documents.net");
    var authKey = new "your authKey from hello Azure portal";
    DocumentClient client = new DocumentClient(serviceEndpoint, authKey,
    new ConnectionPolicy
    {
        ConnectionMode = ConnectionMode.Direct,
        ConnectionProtocol = Protocol.Tcp
    });
    ```

    Omdat TCP wordt alleen ondersteund in de directe modus als Gateway-modus wordt gebruikt, vervolgens Hallo HTTPS-protocol altijd is gebruikt toocommunicate Hello Gateway en Hallo protocolwaarde in Hallo die connectionpolicy wordt genegeerd.

    ![Afbeelding van Hallo verbindingsbeleid Azure Cosmos-DB](./media/performance-tips/connection-policy.png)

3. **OpenAsync tooavoid opstarten latentie voor de eerste aanvraag aanroepen**

    De eerste aanvraag Hallo heeft standaard een hogere latentie omdat hieraan toofetch Hallo adres routeringstabel. tooavoid deze latentie opstarten op Hallo eerst aanvragen, moet u OpenAsync() als volgt één keer tijdens de initialisatie aanroepen.

        await client.OpenAsync();
   <a id="same-region"></a>
4. **Clients in hetzelfde Azure-regio voor prestaties plaatsen**

    Mogelijk is, plaats alle toepassingen Cosmos DB aanroepen in dezelfde regio bevinden als Hallo Hallo wanneer Cosmos DB-database. Voor een vergelijking bij benadering, roept tooCosmos DB binnen dezelfde regio voltooid binnen 1-2-ms, maar de latentie tussen Hallo West en oostkust Hallo VS is Hallo Hallo > 50 ms. Deze latentie variëren van aanvraag toorequest afhankelijk van het Hallo-route Hallo-aanvraag die het doorgeven van Hallo client toohello Azure-datacenter grens waarschijnlijk. Hallo laagst mogelijke latentie wordt gerealiseerd door ervoor te zorgen Hallo aanroepen toepassing bevindt zich in Hallo dezelfde Azure-regio als Hallo ingericht Cosmos-DB-eindpunt. Zie voor een lijst met beschikbare regio's, [Azure-gebieden](https://azure.microsoft.com/regions/#services).

    ![Afbeelding van Hallo verbindingsbeleid Azure Cosmos-DB](./media/performance-tips/same-region.png)
   <a id="increase-threads"></a>
5. **Verhoog het aantal threads/taken**

    Omdat aanroepen tooAzure Cosmos DB worden aangebracht via Hallo netwerk, moet u mogelijk toovary Hallo mate van parallelle uitvoering van uw verzoeken, zodat de client-toepassing hello nodig heeft voor het zeer weinig tijd wachten tussen aanvragen. Bijvoorbeeld als u. De NET [taak parallelle bibliotheek](https://msdn.microsoft.com//library/dd460717.aspx), in volgorde van 100s van taken lezen of schrijven tooCosmos DB Hallo maken.

## <a name="sdk-usage"></a>Gebruik van de SDK
1. **Installeer Hallo meest recente SDK**

    Hallo Cosmos DB SDK's voortdurend worden verbeterd tooprovide Hallo optimale prestaties. Zie Hallo [Cosmos DB SDK](documentdb-sdk-dotnet.md) pagina's toodetermine Hallo meest recente SDK en verbeteringen controleren.
2. **Een singleton Cosmos-DB-client voor de levensduur van uw toepassing hello gebruiken**

    Houd er rekening mee dat elk exemplaar DocumentClient thread-veilige en efficiënte Verbindingsbeheer en adrescaching in directe modus wordt uitgevoerd. efficiënt beheer van tooallow en betere prestaties door DocumentClient, is het aanbevolen toouse één exemplaar van de DocumentClient per AppDomain voor Hallo levensduur van de toepassing hello.

   <a id="max-connection"></a>
3. **System.Net MaxConnections per host verhogen als u de Gateway-modus**

    DB cosmos-aanvragen worden gedaan via HTTPS/REST bij gebruik van Gateway-modus en ondergaan toohello standaardlimiet verbinding per hostnaam of IP-adres zijn. U moet mogelijk tooset Hallo MaxConnections tooa hogere waarde (100-1000) zodat hello clientbibliotheek van meerdere gelijktijdige verbindingen tooCosmos DB gebruikmaken kan. In de .NET SDK 1.8.0 Hallo en Hallo hierboven, de standaardwaarde voor [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx) is 50 en toochange Hallo waarde, kunt u instellen dat Hallo [Documents.Client.ConnectionPolicy.MaxConnectionLimit ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.connectionpolicy.maxconnectionlimit.aspx) tooa hogere waarde.   
4. **Parallelle query's voor gepartitioneerde verzamelingen afstemmen**

     DocumentDB .NET SDK versie 1.9.0 en hoger ondersteuning parallelle query's waarmee u een gepartitioneerde verzameling worden parallel tooquery (Zie [werken met Hallo SDK's](documentdb-partition-data.md#working-with-the-azure-cosmos-db-sdks) en gerelateerde Hallo [codevoorbeelden](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Queries/Program.cs) voor meer informatie). Parallelle query's zijn ontworpen tooimprove Querylatentie en doorvoer via hun seriële equivalent. Parallelle query's bieden twee parameters dat gebruikers toocustom aanpassen de vereisten (a) MaxDegreeOfParallelism afstemmen kunnen: toocontrol Hallo maximum aantal partities vervolgens kan worden opgevraagd in parallel en (b) MaxBufferedItemCount: toocontrol Hallo aantal vooraf opgehaalde resultaten.

    (a) ***afstemmen MaxDegreeOfParallelism\: *** parallelle query werkt door meerdere partities parallel uitvoeren van query's. Echter worden gegevens uit een afzonderlijke gepartitioneerde verzamelen opeenvolgend opgehaald met opzicht toohello query. Instelling Hallo MaxDegreeOfParallelism toohello aantal partities heeft dus Hallo maximale kans op Hallo van de meeste zodat query, opgegeven blijven voor alle andere voorwaarden system Hallo dezelfde. Als u niet dat het aantal partities Hallo weet, kunt u Hallo MaxDegreeOfParallelism tooa groot aantal instellen en Hallo systeem kiest Hallo minimum (aantal partities, invoer van de gebruiker opgegeven) zoals MaxDegreeOfParallelism Hallo.

    Het is belangrijk toonote die parallelle query's produceren Hallo best voordelen als Hallo gegevens evenredig verdeeld over alle partities met opzicht toohello query. Als Hallo gepartitioneerd verzameling is gepartitioneerd zodanig dat alle of een meerderheid van Hallo-gegevens geretourneerd door een query voornamelijk in een paar partities (één partitie in ergste geval) en prestaties van query Hallo Hallo als knelpunt zou worden verwerkt door deze partities.

    (b) ***afstemmen MaxBufferedItemCount\: *** parallelle query wordt ontworpen toopre-ophalen resultaten terwijl de huidige batch Hallo van resultaten wordt verwerkt door het Hallo-client. Hallo vooraf ophalen helpt u bij algemene verbetering van de latentie van een query. MaxBufferedItemCount is Hallo parameter toolimit Hallo aantal vooraf opgehaalde resultaten. Instelling MaxBufferedItemCount verwacht toohello aantal resultaten geretourneerd (of een hogere waarde) kunt Hallo query tooreceive maximaal profiteren van het vooraf ophalen.

    Houd er rekening mee dat vooraf ophalen works Hallo dezelfde manier uitgevoerd ongeacht Hallo MaxDegreeOfParallelism, en er één buffer voor Hallo gegevens van alle partities.  
5. **Schakel op de GC-serverzijde**

    In sommige gevallen kan verminderen Hallo frequentie van garbagecollection helpen. Stel in .NET, [gcServer](https://msdn.microsoft.com/library/ms229357.aspx) tootrue.
6. **Backoff RetryAfter intervallen implementeren**

    Tijdens het testen van prestaties, moet u load verhogen tot een klein aantal aanvragen ophalen beperkt. Als beperkt, Hallo clienttoepassing moet backoff op versnelling voor Hallo server opgegeven interval voor opnieuw proberen. Hallo backoff te respecteren, zorgt u ervoor dat u besteden aan de minimale hoeveelheid tijd wachten tussen nieuwe pogingen. Ondersteuning voor nieuwe pogingen Groepsbeleid is opgenomen in versie 1.8.0 en hoger Hallo DocumentDB [.NET](documentdb-sdk-dotnet.md) en [Java](documentdb-sdk-java.md), versie 1.9.0 en hoger Hallo [Node.js](documentdb-sdk-node.md) en [ Python](documentdb-sdk-python.md), en alle ondersteunde versies van Hallo [.NET Core](documentdb-sdk-dotnet-core.md) SDK's. Zie voor meer informatie [Exceeding gereserveerd doorvoerlimieten](request-units.md#RequestRateTooLarge) en [RetryAfter](https://msdn.microsoft.com/library/microsoft.azure.documents.documentclientexception.retryafter.aspx).
7. **Uitbreiden van de werkbelasting van uw client**

    Als u op niveaus met hoge doorvoer testen wilt (> 50.000 RU/s), Hallo clienttoepassing mogelijk Hallo knelpunt vanwege toohello machine beperking af op CPU- of -gebruik. Als u deze punt bereikt, kunt u toopush hello Cosmos DB account verder gaan door uw clienttoepassingen schalen op meerdere servers.
8. **Cache document URI's voor lagere latentie mogelijk lezen**

    URI's waar mogelijk voor de beste lezen prestaties Hallo document in de cache.
   <a id="tune-page-size"></a>
9. **Hallo paginagrootte voor query's leestijd feeds voor betere prestaties afstemmen**

    Bij het uitvoeren van een bulksgewijs documenten met behulp van de feed functionaliteit (bijvoorbeeld ReadDocumentFeedAsync) lezen of lezen bij de uitgifte van een DocumentDB SQL-query, zijn Hallo resultaten op een gesegmenteerde wijze als Hallo resultatenset te groot is. Standaard resultaten worden geretourneerd in segmenten van 100 items of 1 MB, eerst de limiet is bereikt.

    tooreduce hello aantal netwerk retouren vereist tooretrieve alle toepasselijke resultaten, kunt u de paginagrootte Hallo met behulp van de x-ms-max-item-count-aanvraag-header tooup too1000 verhogen. In gevallen waarin u toodisplay alleen enkele resultaten moet bijvoorbeeld, als uw gebruikers-interface of toepassing API retourneert alleen 10 een tijd resulteert, u kunt ook verlagen Hallo pagina grootte too10 tooreduce Hallo doorvoer verbruikt voor leesbewerkingen en query's.

    Hallo paginaformaat kunnen ook worden ingesteld met behulp van Hallo beschikbaar Cosmos DB-SDK's.  Bijvoorbeeld:

        IQueryable<dynamic> authorResults = client.CreateDocumentQuery(documentCollection.SelfLink, "SELECT p.Author FROM Pages p WHERE p.Title = 'About Seattle'", new FeedOptions { MaxItemCount = 1000 });
10. **Verhoog het aantal threads/taken**

    Zie [Verhoog het aantal threads/taken](#increase-threads) in Hallo sectie over netwerken.

11. **Gebruik 64-bits host verwerken**

    Hallo DocumentDB SDK werkt in een 32-bits hostproces wanneer u de DocumentDB .NET SDK versie 1.11.4 gebruikt en hoger. Als u over verschillende partitie query's gebruikt, wordt 64-bits host verwerken echter aanbevolen voor verbeterde prestaties. Hallo volgende soorten toepassingen hebben 32-bits host als Hallo standaard verwerken, dus in volgorde toochange dat too64-bits, als volgt op basis van uw toepassing hello type:

    - Voor uitvoerbare toepassingen, kan dit worden gedaan door unchecking hello **liever 32-bits** optie in Hallo **Projecteigenschappen** venster op Hallo **bouwen** tabblad.

    - Voor VSTest op basis van de Testprojecten, kunt u dit doen door te selecteren **testen**->**instellingen testen**->**processorarchitectuur standaard als X64**, van Hallo **Visual Studio Test** menuoptie.

    - Voor lokaal geïmplementeerde ASP.NET-webtoepassingen, kunt dit doen door te controleren Hallo **gebruik Hallo 64-bits versie van IIS Express voor websites en projecten**onder **extra** ->  **Opties**->**projecten en oplossingen**->**Web-projecten**.

    - Voor ASP.NET-webtoepassingen wordt geïmplementeerd in Azure, kunt dit doen door te kiezen Hallo **Platform als 64-bits** in Hallo **toepassingsinstellingen** op Hallo Azure-portal.

## <a name="indexing-policy"></a>Indexeringsbeleid
1. **Gebruik vertraagde indexering voor snellere piek tijd opname tarieven**

    Cosmos DB kunt u toospecify – op niveau Hallo verzameling – indexeringsbeleid, waarmee u toochoose als u wilt dat Hallo documenten in een verzameling toobe automatisch geïndexeerd of niet.  U kunt bovendien ook tussen synchrone (consistente) en updates van de index asynchrone (Lazy). Hallo-index wordt standaard synchroon bijgewerkt op elke invoegen, vervangen of verwijderen van een document toohello-verzameling. Synchroon modus schakelt Hallo query's toohonor Hallo dezelfde [consistentieniveau](consistency-levels.md) als die van Hallo document leest zonder enige vertraging voor Hallo-index te 'lopen'.

    Vertraagde indexeren kan worden overwogen om scenario's waarin gegevens worden geschreven in bursts en u wilt dat tooamortize Hallo werk dat nodig is tooindex inhoud gedurende een langere periode. Vertraagde indexeren kunt u ook toouse uw doorvoer effectief ingericht en dienst schrijfaanvragen piekuren met een minimale latentie. Het is belangrijk toonote, echter dat wanneer vertraagde indexeren is ingeschakeld, queryresultaten uiteindelijk consistent ongeacht Hallo consistentieniveau geconfigureerd voor Hallo Cosmos-DB-account zijn.

    Daarom Hallo hoogste aanvraag eenheid kosten per schrijfbewerking tijdens het indexeren modus (IndexingPolicy.IndexingMode wordt ingesteld tooLazy) en geen indexering Lazy leidt ertoe dat Consistent indexing-modus (IndexingPolicy.IndexingMode wordt ingesteld tooConsistent) (IndexingPolicy.Automatic is ingesteld tooFalse) hebben van nul indexering kosten op Hallo moment van schrijven.
2. **Ongebruikte paden uitsluiten van indexering voor snellere schrijfbewerkingen**

    Indexeringsbeleid cosmos van de database kunt u ook toospecify die paden tooinclude document of uitsluiten door gebruik te indexeren paden (IndexingPolicy.IncludedPaths en IndexingPolicy.ExcludedPaths) te indexeren. Hallo-gebruik van het indexeren paden kunt aanbieden verbeterde schrijfprestaties en lagere opslagkosten voor index voor scenario's in welke Hallo querypatronen zijn wel tevoren indexering kosten zijn rechtstreeks gecorreleerde toohello aantal unieke paden die zijn geïndexeerd.  Bijvoorbeeld toont Hallo volgende code hoe tooexclude een hele sectie Hallo documenten (ook een substructuur) niet kan indexeren met behulp van Hallo ' * ' jokerteken.

    ```C#
    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*");
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);
    ```

    Zie voor meer informatie [Azure Cosmos DB indexeren beleid](indexing-policies.md).

## <a name="throughput"></a>Doorvoer
<a id="measure-rus"></a>

1. **Meten en stemmen voor lagere aanvraag eenheden/seconde gebruik**

    Cosmos DB biedt een uitgebreide reeks databasebewerkingen, met inbegrip van relationele en hiërarchische query's met UDF's, opgeslagen procedures en triggers – alle operationele op Hallo documenten binnen een verzameling van de database. Hallo kosten die zijn gekoppeld aan elk van deze bewerkingen varieert op basis van Hallo CPU, IO en geheugen vereist toocomplete Hallo-bewerking. In plaats van het denken over en beheer van hardwareresources, kunt u zien van een aanvraag-eenheid (RU) als één maatregel voor Hallo resources vereist tooperform diverse databasebewerkingen en service een toepassingsaanvraag.

    [Aanvraageenheden](request-units.md) zijn ingericht voor het account van elke database op basis van het aantal eenheden voor capaciteit die u aanschaft Hallo. Aanvraag eenheidsverbruik wordt geëvalueerd als een percentage per seconde. Toepassingen die groter zijn dan Hallo ingerichte aanvraag eenheid beoordelen voor het account beperkt is pas Hallo snelheid Hallo gereserveerde serviceniveau voor Hallo-account. Als uw toepassing een hogere mate van doorvoer vereist, kunt u extra capaciteitseenheden aanschaffen.

    Hallo complexiteit van een query heeft gevolgen voor het aantal eenheden van de aanvraag voor een bewerking worden verbruikt. aantal predicaten Hello, aard van Hallo predicaten, UDF's aantal en grootte van alle Hallo kosten van invloed zijn op bron-gegevensset voor Hallo Hallo query bewerkingen.

    toomeasure hello overhead van elke bewerking (maken, bijwerken of verwijderen) inspecteren Hallo x-ms-aanvraag-kosten header (of gelijkwaardige RequestCharge-eigenschap in ResourceResponse Hallo<T> of FeedResponse<T> in .NET SDK Hallo) toomeasure Hallo aantal aanvraageenheden verbruikt door deze bewerkingen.

    ```C#
    // Measure hello performance (request units) of writes
    ResourceResponse<Document> response = await client.CreateDocumentAsync(collectionSelfLink, myDocument);
    Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);
    // Measure hello performance (request units) of queries
    IDocumentQuery<dynamic> queryable = client.CreateDocumentQuery(collectionSelfLink, queryString).AsDocumentQuery();
    while (queryable.HasMoreResults)
         {
              FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>();
              Console.WriteLine("Query batch consumed {0} request units", queryResponse.RequestCharge);
         }
    ```             

    Hallo aanvraag kosten geretourneerd in deze header is een fractie van de ingerichte doorvoer (dat wil zeggen, 2000 RUs / seconde). Bijvoorbeeld, als hello voorgaande query 1000 1KB-documenten retourneert, is Hallo kosten van het Hallo-bewerking 1000. Als zodanig binnen één seconde Hallo server respecteert slechts twee dergelijke aanvragen voordat de beperking van de volgende aanvragen. Zie voor meer informatie [Aanvraageenheden](request-units.md) en Hallo [aanvraag eenheid Rekenmachine](https://www.documentdb.com/capacityplanner).
<a id="429"></a>
2. **Verwerken frequentie beperken/aanvraagsnelheid te groot**

    Wanneer een client tooexceed Hallo gereserveerde doorvoer voor een account probeert, is er geen verslechtering van prestaties optreedt op Hallo-server en er geen gebruik van doorvoercapaciteit buiten Hallo gereserveerd niveau. Hallo server beëindigd optie preventief Hallo-aanvraag met RequestRateTooLarge (HTTP-statuscode 429) en wordt geretourneerd Hallo header x-ms-opnieuw-na-ms aangegeven hoeveelheid tijd in milliseconden die gebruiker Hallo Hallo moet wachten voordat het opnieuw proberen van Hallo aanvraag.

        HTTP Status 429,
        Status Line: RequestRateTooLarge
        x-ms-retry-after-ms :100

    Hallo-SDK's alle impliciet dit antwoord catch, te respecteren Hallo server opgegeven opnieuw proberen na header en Hallo aanvraag opnieuw proberen. Tenzij uw account wordt door meerdere clients tegelijkertijd geopend, wordt een nieuwe poging gedaan Hallo slaagt.

    Als er meer dan één client cumulatief werken consistent boven aanvraagsnelheid hello, Hallo standaardaantal nieuwe pogingen momenteel set too9 intern door Hallo-client niet toereikend zijn; in dit geval Hallo client genereert een DocumentClientException met status code 429 toohello toepassing. aantal nieuwe pogingen van Hallo standaard kan worden gewijzigd door de instelling Hallo RetryOptions op Hallo ConnectionPolicy exemplaar. Standaard Hallo DocumentClientException met statuscode 429 na een cumulatieve wachttijd van 30 seconden geretourneerd als Hallo aanvraag toooperate hierboven Hallo aanvraagsnelheid blijft. Dit gebeurt zelfs wanneer de huidige pogingen Hallo kleiner is dan Hallo max. aantal, het Hallo-standaardwaarde van 9 of een door de gebruiker gedefinieerde waarde.

    Hoewel Hallo geautomatiseerde gedrag voor het opnieuw kunt tooimprove tolerantie en gebruiksgemak voor Hallo de meeste toepassingen, deze mogelijk geleverd op odds bij het uitvoeren van prestatiebenchmarks, vooral wanneer meten latentie.  Hallo client waargenomen-latentie wordt pieken als Hallo experiment Hallo server versnelling treffers en zorgt ervoor Hallo client SDK toosilently probeer het opnieuw dat. tooavoid latentie bereikt tijdens prestaties experimenten, meting Hallo kosten geretourneerd door elke bewerking en zorg ervoor dat aanvragen hieronder Hallo gereserveerde aanvraagsnelheid werkt. Zie voor meer informatie [Aanvraageenheden](request-units.md).
3. **Ontwerp voor kleinere documenten voor een hogere doorvoer**

    Hallo aanvraag kosten (dat wil zeggen aanvraagverwerking kosten) van een bepaalde bewerking is rechtstreeks gecorreleerde toohello grootte van het Hallo-document. Bewerkingen op grote documenten duurder dan bewerkingen voor kleine documenten.

## <a name="next-steps"></a>Volgende stappen
Zie voor een voorbeeld toepassing gebruikt tooevaluate Cosmos DB voor scenario's met hoge prestaties op enkele clientcomputers, [prestaties en schaal testen met Cosmos DB](performance-testing.md).

Toolearn meer informatie over het ontwerpen van uw aanvraag voor schaal en hoge prestaties, Zie ook [partitionering en schalen in Azure Cosmos DB](partition-data.md).

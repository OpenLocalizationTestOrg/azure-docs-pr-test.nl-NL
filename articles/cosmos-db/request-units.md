---
title: aaaRequest eenheden & schatten van doorvoer - Azure Cosmos DB | Microsoft Docs
description: Meer informatie over hoe toounderstand, geef en vereisten voor aanvraag-eenheid in Azure Cosmos DB schatten.
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a>Aanvraageenheden in Azure Cosmos DB
Nu beschikbaar: Azure Cosmos DB [aanvraag eenheid Rekenmachine](https://www.documentdb.com/capacityplanner). Meer informatie [schatting van de doorvoer moet](request-units.md#estimating-throughput-needs).

![Doorvoer Rekenmachine][5]

## <a name="introduction"></a>Inleiding
[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) van Microsoft wereldwijd gedistribueerde database voor meerdere model is. Met Azure Cosmos DB niet u toorent virtuele machines hebt, software implementeren of databases bewaken. Azure Cosmos DB wordt beheerd en continu bewaakt door Microsoft bovenste engineers toodeliver world klasse beschikbaarheid, prestaties en beveiliging. U toegang hebt tot uw gegevens met behulp van API's van uw keuze als [DocumentDB SQL](documentdb-sql-query.md) (document) MongoDB (document) [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (sleutel-waarde), en [Gremlin](https://tinkerpop.apache.org/gremlin.html) (grafiek) worden ondersteund. Hallo valuta van Azure DB die Cosmos is Hallo aanvragen Unit (RU). Met RUs hoeft u niet tooreserve lezen/schrijven capaciteiten of het inrichten CPU, geheugen en IOPS.

Azure Cosmos DB ondersteunt een aantal API's met verschillende bewerkingen, variërend van eenvoudige leest en schrijft toocomplex grafiek query's. Omdat niet alle aanvragen gelijk zijn, zijn ze een genormaliseerde hoeveelheid toegewezen **aanvraageenheden** op basis van Hallo hoeveelheid berekening vereist tooserve Hallo aanvraag. Hallo aantal aanvraageenheden voor een bewerking is deterministisch en kunt u het aantal aanvraageenheden verbruikt door elke bewerking in Azure Cosmos DB via een antwoordheader Hallo bijhouden. 

tooprovide voorspelbare prestaties, moet u tooreserve doorvoer in eenheden van 100 RU/seconde. 

Na het lezen van dit artikel, moet u kunnen tooanswer Hallo vragen te volgen:  

* Wat zijn aanvraageenheden en kosten aanvragen?
* Hoe geef ik aanvraag eenheid capaciteit voor een verzameling?
* Hoe u schat dat mijn toepassing aanvraag heeft?
* Wat gebeurt er als ik aanvraag eenheid capaciteit voor een verzameling overschrijdt?

Zoals Azure Cosmos DB een database met meerdere modellen is, is het belangrijk toonote dat tooa verzameling/document voor een API-document, een grafiek/knooppunt voor de API van een grafiek en een Tabelentiteit voor tabel-API wordt verwezen. Doorvoer in dit document wordt we toohello concepten van container item/generalize.

## <a name="request-units-and-request-charges"></a>Aanvraageenheden en kosten van de aanvraag
Azure Cosmos DB biedt snelle en voorspelbare prestaties door *reserveren* resources toosatisfy doorvoer van uw toepassing nodig heeft.  Omdat de toepassing laden en toegang tot patronen wijzigen na verloop van tijd, wordt Azure Cosmos DB kunt u tooeasily toename of minder Hallo gereserveerde doorvoer beschikbaar tooyour toepassing.

Met Azure Cosmos DB is gereserveerde doorvoer opgegeven in termen van aanvraageenheden per seconde verwerkt. U kunt zien aanvraageenheden als valuta doorvoer, waarbij u *reserveren* een hoeveelheid gegarandeerd aanvraageenheden beschikbaar tooyour toepassing op basis van per seconde.  Elke bewerking in Azure Cosmos DB - schrijven, uitvoeren van een query, het bijwerken van een document - verbruikt CPU, geheugen en IOPS.  Dat wil zeggen, elke bewerking leidt ertoe dat een *aanvragen kosten*, die wordt uitgedrukt in *aanvraageenheden*.  Inzicht in Hallo factoren die van invloed zijn op aanvraag eenheid kosten, samen met de vereisten van de doorvoer van uw toepassing, kunt u toorun uw toepassing als de kosten-effectief mogelijk. Hallo queryverkenner is ook een fantastische hulpprogramma tootest Hallo kern van een query.

Het is raadzaam om aan de slag door bekijkt hello video te volgen waarbij Aravind Ramachandran wordt uitgelegd aanvraageenheden en voorspelbare prestaties met Azure Cosmos DB.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a>Capaciteit van de aanvraag-eenheid opgeven in Azure Cosmos-DB
Bij het starten van een nieuwe verzameling, de tabel of de grafiek, u Hallo-nummer opgeven aantal aanvraageenheden per seconde (ru/s per seconde) u wilt dat gereserveerd. Op basis van de ingerichte doorvoer hello, Azure Cosmos DB toegewezen fysieke partities toohost uw verzameling en splitsingen/rebalances gegevens meerdere partities wanneer deze groeit.

Azure Cosmos DB moet dat een partitie sleutel toobe worden opgegeven wanneer een verzameling is ingericht met 2500 aanvraageenheden of hoger. Een partitiesleutel is ook vereist tooscale doorvoer afgezien van 2500 aanvraageenheden in toekomstige Hallo van uw verzameling. Daarom is het raadzaam tooconfigure een [partitiesleutel](partition-data.md) bij het maken van een container ongeacht uw eerste doorvoer. Omdat de gegevens toobe verdelen over meerdere partities wellicht, is het nodig toopick een partitiesleutel met een hoge kardinaliteit (100 toomillions van afzonderlijke waarden) zodat uw tabel-verzameling/grafiek en aanvragen kunnen worden vergroot of verkleind gelijkmatig door Azure Cosmos DB. 

> [!NOTE]
> Een partitiesleutel is een grens van een logische en niet een fysieke. U moet daarom niet toolimit Hallo aantal afzonderlijke partitie sleutelwaarden. Het is in feite betere toohave duidelijker sleutelwaarden dan kleiner, partitie-als Azure Cosmos DB heeft meer opties voor taakverdeling.

Hier volgt een codefragment voor het maken van een verzameling met 3000 aanvraag eenheden per met behulp van tweede Hallo .NET SDK:

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

Azure Cosmos-database is van invloed op een model reservering op doorvoer. Dat wil zeggen, u wordt gefactureerd voor Hallo hoeveelheid doorvoer *gereserveerde*, ongeacht hoeveel waarop doorvoer is actief *gebruikt*. Als uw toepassing werklast, gegevens en informatie over het gebruik patronen wijzigen kunt u eenvoudig de schaal omhoog en omlaag Hallo hoeveelheid gereserveerde RUs via SDK's of met behulp van Hallo [Azure Portal](https://portal.azure.com).

Elke verzameling, de tabel/het grafiek zijn toegewezen tooan `Offer` resource in Azure Cosmos DB met metagegevens over Hallo ingerichte doorvoer. U kunt Hallo toegewezen doorvoer wijzigen door op Hallo bijbehorende aanbieding resource voor een container te zoeken en vervolgens bijgewerkt met nieuwe doorvoercapaciteit Hallo. Hier volgt een codefragment voor het wijzigen van Hallo doorvoer van een verzameling too5, 000 aanvraageenheden per met behulp van tweede Hallo .NET SDK:

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

Er is geen impact toohello beschikbaarheid van de container wanneer u Hallo doorvoer wijzigt. Hallo nieuwe gereserveerde doorvoer is doorgaans effectieve binnen enkele seconden op de toepassing van nieuwe Hallo-doorvoer.

## <a name="request-unit-considerations"></a>Overwegingen voor aanvraag-eenheid
Bij schatten Hallo aantal aanvraag eenheden tooreserve voor uw Azure DB die Cosmos-container, is het belangrijk tootake Hallo variabelen in aanmerking te volgen:

* **De grootte van item**. Als grootte toeneemt Hallo eenheden tooread verbruikt of Hallo-gegevens schrijven wordt ook vergroot.
* **Aantal eigenschappen item**. Ervan uitgaande dat standaard indexeren van alle eigenschappen, Hallo eenheden verbruikt toowrite een document, de knooppunt/het ntity wordt verhoogd als Hallo eigenschap count toeneemt.
* **Gegevensconsistentie**. Wanneer u gegevens consistentieniveaus van sterke of gebonden veroudering, worden aanvullende eenheden verbruikte tooread items.
* **Geïndexeerde eigenschappen**. Een index-beleid op elke container bepaalt welke eigenschappen standaard worden geïndexeerd. Door het aantal geïndexeerde eigenschappen hello te beperken of doordat de vertraagde indexeren, kunt u uw aanvraag eenheidsverbruik verminderen.
* **Document indexeren**. Standaard die elk item wordt automatisch geïndexeerd, wordt u minder aanvraageenheden gebruiken als u ervoor geen tooindex aantal objecten kiest.
* **Query uitvoeren op patronen**. Hallo complexiteit van een query heeft gevolgen voor het aantal eenheden van de aanvraag voor een bewerking worden verbruikt. aantal predicaten Hello, aard van Hallo predikaten, projecties, aantal UDF's en grootte van alle Hallo kosten van invloed zijn op bron-gegevensset voor Hallo Hallo query bewerkingen.
* **Gebruik een script**.  Net als bij query's, opgeslagen procedures en triggers in beslag nemen aanvraageenheden op basis van Hallo complexiteit van het Hallo-bewerkingen die worden uitgevoerd. Tijdens het ontwikkelen van uw toepassing hello aanvraag kosten inspecteren header toobetter begrijpen hoe elke bewerking aanvraag eenheid capaciteit is verbruikt.

## <a name="estimating-throughput-needs"></a>Schatten van doorvoerbehoeften
Een aanvraag-eenheid is een genormaliseerde meting van de kosten voor aanvraagverwerking. Een eenheid één aanvraag vertegenwoordigt Hallo verwerking vereiste capaciteit tooread (via self link- of -id) voor een enkele 1KB item dat bestaat uit 10 unieke eigenschapswaarden (met uitzondering van Systeemeigenschappen). Een aanvraag toocreate (invoegen), vervangen of verwijderen van hetzelfde item verbruikt meer verwerken van de service Hallo Hallo en waardoor meer aanvraageenheden.   

> [!NOTE]
> Hallo basislijn van de aanvraag 1 eenheid voor een 1KB item overeenkomt met eenvoudige tooa ophalen door self link- of -id van Hallo-item.
> 
> 

Hier is bijvoorbeeld een tabel waarin het aantal aanvragen eenheden tooprovision op drie verschillende item grootten (1KB, 4KB en 64KB) en op twee verschillende prestatieniveaus (500 leesbewerkingen per seconde + 100 schrijfbewerkingen per seconde en 500 leesbewerkingen per seconde + 500 schrijfbewerkingen per seconde). Hallo gegevensconsistentie op sessie is geconfigureerd en Hallo indexeren beleid tooNone is ingesteld.

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>De grootte van artikel</strong></p></td>
            <td valign="top"><p><strong>Leesbewerkingen per seconde</strong></p></td>
            <td valign="top"><p><strong>Schrijfbewerkingen per seconde</strong></p></td>
            <td valign="top"><p><strong>Aanvraageenheden</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1) + (100 * 5) = 1000 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1) + (500 * 5) = 3.000 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1.3) + (100 * 7) = 1,350 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1.3) + (500 * 7) = 4,150 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 kB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 10) + (100 * 48) = 9,800 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 kB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 10) + (500 * 48) = 29.000 RU/s</p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a>Hallo aanvraag eenheid Rekenmachine gebruiken
toohelp klanten fijn stemmen hun schattingen doorvoer, wordt er een op het web gebaseerd [aanvraag eenheid Rekenmachine](https://www.documentdb.com/capacityplanner) toohelp schatting Hallo aanvraag eenheid vereisten voor normale bewerkingen, inclusief:

* Item maakt (schrijft)
* Item leest
* Item wordt verwijderd
* Item updates

Hallo hulpprogramma biedt tevens ondersteuning voor het schatten van opslagbehoeften op basis van Hallo voorbeelditems die u opgeeft.

Het hulpprogramma voor Hallo is eenvoudig:

1. Upload een of meer representatieve items.
   
    ![Items toohello aanvraag eenheid Rekenmachine uploaden][2]
2. vereisten voor gegevensopslag tooestimate, typ Hallo totaal aantal items u toostore verwacht.
3. Voer Hallo aantal items maken, lezen, bijwerken en verwijderen van bewerkingen die u nodig (op basis van het per seconde hebt). tooestimate hello aanvraag eenheid kosten van item update-bewerkingen, upload een kopie van Hallo voorbeeld item uit stap 1 bovenstaande typische veld updates bevat.  Als updates objecten doorgaans twee eigenschappen met de naam lastLogin en userVisits wijzigen en vervolgens Hallo voorbeeld item te kopiëren, Hallo waarden voor deze twee eigenschappen bijwerken en Hallo gekopieerd item uploaden.
   
    ![Doorvoer vereisten invoeren in de Hallo aanvraag eenheid Rekenmachine][3]
4. Klik op berekenen en bekijkt hello resultaten.
   
    ![Eenheid Rekenmachine resultaten aanvragen][4]

> [!NOTE]
> Als u itemtypen die aanzienlijk verschillen in termen van de grootte en Hallo aantal geïndexeerde eigenschappen hebt wordt, uploadt u een voorbeeld van elke *type* van typische item toohello hulpprogramma en Hallo resultaten vervolgens te berekenen.
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a>Hello Azure Cosmos DB kosten antwoord aanvraagheader gebruiken
Elke reactie van hello Azure DB die Cosmos-service bestaat uit een aangepaste header (`x-ms-request-charge`) die Hallo aanvraageenheden verbruikt voor Hallo-aanvraag bevat. Deze header is ook toegankelijk via hello Azure Cosmos DB SDK's. Hallo .NET SDK is RequestCharge een eigenschap van Hallo ResourceResponse object.  Hello Azure Cosmos DB Queryverkenner in hello Azure-portal biedt voor query's, kosten aanvraaggegevens voor uitgevoerde query's.

![RU kosten in Hallo Queryverkenner onderzoeken][1]

Met dat gegeven in gedachte, is een methode voor het schatten van de hoeveelheid gereserveerde doorvoer vereist door uw toepassing hello toorecord Hallo aanvraag eenheid kosten die zijn gekoppeld aan met het normale bewerkingen uitvoeren in een representatieve item gebruikt door de toepassing en vervolgens schatten Hallo aantal bewerkingen wilt u uitvoeren per seconde.  Ervoor toomeasure en typische query's en ook gebruik van Azure DB die Cosmos script bevatten.

> [!NOTE]
> Als er itemtypen die aanzienlijk in termen van de grootte en Hallo aantal geïndexeerde eigenschappen verschillen wordt, en noteer vervolgens Hallo toepasselijke bewerking aanvraag eenheid kosten die zijn gekoppeld aan elk *type* van typische item.
> 
> 

Bijvoorbeeld:

1. Hallo aanvraag eenheid kosten voor het maken van (invoegen) opnemen een typische item. 
2. Record Hallo aanvraag eenheid kosten voor het lezen van een typische item.
3. Record Hallo aanvraag eenheid kosten van het bijwerken van een typische item.
4. Record Hallo aanvraag eenheid kosten van item gebruikelijke, algemene query's.
5. Record Hallo aanvraag eenheid kosten van alle aangepaste scripts (opgeslagen procedures, triggers, gebruiker gedefinieerde functies) door de toepassing hello worden gebruikt
6. Berekenen Hallo vereiste aanvraag dat eenheden Hallo geschatte aantal bewerkingen verwacht toorun per seconde.

### <a id="GetLastRequestStatistics"></a>API voor van MongoDB GetLastRequestStatistics opdracht gebruiken
API voor MongoDB biedt ondersteuning voor een aangepaste opdracht *getLastRequestStatistics*, voor het ophalen van Hallo aanvraag kosten voor opgegeven bewerkingen.

Bijvoorbeeld in Hallo Mongo-Shell, gewenste tooverify Hallo aanvraag kosten voor Hallo-bewerking uitvoeren.
```
> db.sample.find()
```

Vervolgens Hallo-opdracht uitvoeren *getLastRequestStatistics*.
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

Met dat gegeven in gedachte, is een methode voor het schatten van de hoeveelheid gereserveerde doorvoer vereist door uw toepassing hello toorecord Hallo aanvraag eenheid kosten die zijn gekoppeld aan met het normale bewerkingen uitvoeren in een representatieve item gebruikt door de toepassing en vervolgens schatten Hallo aantal bewerkingen wilt u uitvoeren per seconde.

> [!NOTE]
> Als er itemtypen die aanzienlijk in termen van de grootte en Hallo aantal geïndexeerde eigenschappen verschillen wordt, en noteer vervolgens Hallo toepasselijke bewerking aanvraag eenheid kosten die zijn gekoppeld aan elk *type* van typische item.
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a>API gebruiken voor de portal metrieken van MongoDB
Hallo de eenvoudigste manier tooget een goede schatting van de aanvraag eenheid voor uw API berekent voor MongoDB-database toouse hello is [Azure-portal](https://portal.azure.com) metrische gegevens. Hello *aantal aanvragen* en *aanvraag kosten* grafieken, kunt u een schatting van het aantal aanvraageenheden elke bewerking is verbruikt en krijgen hoeveel aanvraageenheden ze relatieve tooone verbruiken een andere.

![API voor MongoDB portal metrische gegevens][6]

## <a name="a-request-unit-estimation-example"></a>Een voorbeeld van een aanvraag eenheid schatting
Houd rekening met Hallo ~ 1KB document te volgen:

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> Documenten zijn in Azure Cosmos DB minified zodat Hallo systeem berekend grootte van de bovenstaande Hallo-document is iets minder dan 1KB.
> 
> 

Hallo volgende tabel ziet u een benadering aanvraag eenheid kosten voor normale bewerkingen op dit object (Hallo geschatte aanvraag eenheid kosten wordt ervan uitgegaan dat Hallo consistentieniveau-account te is ingesteld dat alle items automatisch worden geïndexeerd en 'Sessie'):

| Bewerking | Aanvraag eenheid kosten |
| --- | --- |
| -Item maken |~ 15 RU |
| Item lezen |~ 1 RU |
| Query-item met id |~2.5 RU |

In deze tabel ziet een benadering aanvraag bovendien eenheid kosten voor typische query's in de toepassing hello gebruikt:

| Query’s uitvoeren | Aanvraag eenheid kosten | het aantal geretourneerde artikelen |
| --- | --- | --- |
| Selecteer voeding door-id |~2.5 RU |1 |
| Selecteer levensmiddelen op fabrikant |~ 7 RU |7 |
| Selecteer door Voedingsgroep en de volgorde op basis van gewicht |~ 70 RU |100 |
| Bovenste 10 levensmiddelen in een Voedingsgroep selecteren |~ 10 RU |10 |

> [!NOTE]
> RU kosten variëren op basis van het aantal items geretourneerd Hallo.
> 
> 

Met deze informatie kunnen we verwachten Hallo RU vereisten voor deze toepassing opgegeven Hallo aantal bewerkingen en query's die we verwachten dat per seconde:

| Bewerking/Query | Het geschatte aantal per seconde | Vereiste RUs |
| --- | --- | --- |
| -Item maken |10 |150 |
| Item lezen |100 |100 |
| Selecteer levensmiddelen op fabrikant |25 |175 |
| Selecteer door de Voedingsgroep |10 |700 |
| Selecteer top 10 |15 |150 totaal |

In dit geval we verwachten dat de vereiste van een gemiddelde doorvoersnelheid van 1,275 RU/s.  Afronden up toohello dichtstbijzijnde 100, zouden we 1.300 RU/s voor de verzameling van deze toepassing inrichten.

## <a id="RequestRateTooLarge"></a>Overschrijding van gereserveerde doorvoer grenzen in Azure Cosmos-DB
Intrekken dat verzoek eenheidsverbruik wordt beoordeeld als een percentage per seconde als Hallo budget leeg is. Voor toepassingen die groter zijn dan Hallo aanvragen ingerichte aanvraagsnelheid eenheid voor een container toothat verzameling wordt beperkt pas Hallo snelheid Hallo gereserveerd niveau. Wanneer er een vertraging optreedt, eindigen Hallo server optie preventief Hallo-aanvraag met RequestRateTooLargeException (HTTP-statuscode 429) en wordt geretourneerd Hallo-header x-ms-opnieuw-na-ms aangegeven hoeveelheid tijd in milliseconden die gebruiker Hallo Hallo moet wachten voordat Hallo-aanvraag nogmaals te proberen.

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

Als u gebruikmaakt van Client-SDK voor .NET en LINQ Hallo-query's en vervolgens Hallo tijd die u nooit toodeal met deze uitzondering als de huidige versie van de Hallo van Client-SDK voor .NET Hallo impliciet dit antwoord dat de meeste, respecteert server opgegeven opnieuw proberen na header Hallo en Hallo-aanvraag voor nieuwe pogingen. Tenzij uw account wordt door meerdere clients tegelijkertijd geopend, wordt een nieuwe poging gedaan Hallo slaagt.

Als er meer dan één client cumulatief werken boven aanvraagsnelheid hello, hello standaardgedrag voor opnieuw proberen niet toereikend zijn en Hallo client genereert een DocumentClientException met status code 429 toohello toepassing. In dergelijke gevallen overweegt u verwerken gedrag voor het opnieuw en logica in uw toepassing fout routines voor het afhandelen of een uitbreiding van Hallo gereserveerde doorvoer voor Hallo-container.

## <a id="RequestRateTooLargeAPIforMongoDB"></a>Gereserveerde doorvoerlimieten in API overschrijden voor MongoDB
Toepassingen die groter is dan de aanvraageenheden Hallo ingericht voor een verzameling wordt pas Hallo snelheid Hallo gereserveerd niveau worden beperkt. Wanneer er een vertraging optreedt, Hallo back-end optie preventief eindigt Hallo-aanvraag met een *16500* foutcode - *te veel aanvragen*. API voor MongoDB wordt standaard automatisch opnieuw van too10 tijden voordat er een *te veel aanvragen* foutcode. Als er veel *te veel aanvragen* foutcodes, kunt u ook beide toe te voegen gedrag voor het opnieuw in routines voor foutafhandeling van uw toepassing of [Hallo gereserveerde doorvoer voor Hallo verzamelingverhogen](set-throughput.md).

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over gereserveerde doorvoer met Azure DB die Cosmos-databases, bekijk deze resources:

* [Prijzen van Azure DB Cosmos](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [Gegevens in Azure Cosmos DB te partitioneren](partition-data.md)

toolearn meer informatie over Azure Cosmos DB Zie hello Azure Cosmos DB [documentatie](https://azure.microsoft.com/documentation/services/cosmos-db/). 

Zie tooget gestart met de schaal en prestaties testen met Azure Cosmos DB [prestaties en schaal testen met Azure Cosmos DB](performance-testing.md).

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png

---
title: ondersteuning voor Cosmos DB Gremlin aaaAzure | Microsoft Docs
description: Meer informatie over Hallo van Apache TinkerPop, waarmee u functies en stappen Gremlin taal en beschikbaar in Azure Cosmos-DB
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 6016ccba-0fb9-4218-892e-8f32a1bcc590
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/10/2017
ms.author: denlee
ms.openlocfilehash: f8c2ce50c6946e971f56fe1f3838b0899cb2ad8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-gremlin-graph-support"></a>Ondersteuning van Azure DB-Gremlin Cosmos-grafiek
Biedt ondersteuning voor Azure Cosmos DB [van Apache Tinkerpop](http://tinkerpop.apache.org) graph traversal taal, [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps), namelijk een Graph-API voor het maken van de grafiek entiteiten en grafiek querybewerkingen uitvoert. U kunt Hallo Gremlin taal toocreate grafiek entiteiten (hoekpunten en randen) gebruiken, eigenschappen binnen deze entiteiten wijzigen, uitvoeren van query's en traversals en entiteiten te verwijderen. 

Azure Cosmos DB brengt ondernemingsniveau functies toograph databases. Dit omvat de algemene distributie, onafhankelijke schalen van opslag en doorvoer, voorspelbare één cijfer milliseconde latenties, automatisch te indexeren en sla van 99,99%. Omdat Azure Cosmos DB TinkerPop/Gremlin ondersteunt, kunt u eenvoudig toepassingen die zijn geschreven met behulp van een andere grafiek database zonder codewijzigingen toomake migreren. Bovendien grond Gremlin ondersteuning, Azure Cosmos DB naadloos kan worden geïntegreerd met TinkerPop ingeschakeld analytics frameworks zoals [Apache Spark GraphX](http://spark.apache.org/graphx/). 

In dit artikel wij bieden een snel overzicht van Gremlin en opsommen Hallo Gremlin functies en de stappen die worden ondersteund in preview Hallo van Graph API-ondersteuning.

## <a name="gremlin-by-example"></a>Gremlin door voorbeeld
We gaan een voorbeeld grafiek toounderstand hoe query's kunnen worden uitgedrukt in Gremlin gebruiken. Hallo volgende afbeelding ziet u een zakelijke toepassing die gegevens over gebruikers, interesses en apparaten in de vorm van een grafiek Hallo beheert.  

![Voorbeelddatabase met personen, apparaten en interesses](./media/gremlin-support/sample-graph.png) 

Deze grafiek bevat Hallo hoekpunt typen (de "label" op in Gremlin genoemd) te volgen:

- Personen: Hallo grafiek bevat drie personen, Robin, Thomas en Ben
- Interesses: hun interesses, in dit voorbeeld Hallo game van Football
- : Hallo apparaten die mensen gebruiken
- Besturingssystemen: Hallo-besturingssystemen die op Hallo apparaten worden uitgevoerd

Er gelden voor Hallo relaties tussen deze entiteiten via Hallo rand typen/labels te volgen:

- Kent: bijvoorbeeld 'Thomas kent Robin"
- Geïnteresseerd: toorepresent Hallo interesses van Hallo mensen in onze grafiek, bijvoorbeeld 'Ben is geïnteresseerd in Football'
- RunsOS: Laptop uitvoert Hallo Windows-besturingssysteem
- Vormen van gebruik: toorepresent welk apparaat een persoon wordt gebruikt. Robin gebruikt bijvoorbeeld een telefoon Motorola met serienummer 77

Laten we enkele bewerkingen uitvoeren op deze grafiek met Hallo [Gremlin Console](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console). U kunt ook deze bewerkingen met Gremlin stuurprogramma's in Hallo platform van uw keuze (Java, Node.js, Python of .NET) uitvoeren.  Voordat we wat wordt ondersteund in Azure Cosmos DB kijken, bekijken we enkele voorbeelden tooget bekend met de Hallo-syntaxis.

Eerste bekijken we CRUD. Hallo volgende Gremlin-instructie wordt ingevoegd Hallo 'Thomas' vertex in Hallo grafiek:

```
:> g.addV('person').property('id', 'thomas.1').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44)
```

Vervolgens voegt Hallo Gremlin-instructie een edge 'kent' tussen Thomas en Robin.

```
:> g.V('thomas.1').addE('knows').to(g.V('robin.1'))
```

Hallo retourneert volgende query Hallo 'persoon' hoekpunten in aflopende volgorde van de namen van de eerste:
```
:> g.V().hasLabel('person').order().by('firstName', decr)
```

Indien grafieken harte is wanneer u wordt tooanswer vragen zoals 'welke besturingssystemen vrienden of van Thomas gebruik?'. U kunt deze eenvoudige Gremlin traversal tooget die informatie uitvoeren vanaf Hallo grafiek:

```
:> g.V('thomas.1').out('knows').out('uses').out('runsos').group().by('name').by(count())
```
Nu gaan we kijken wat Azure Cosmos DB voor ontwikkelaars Gremlin biedt.

## <a name="gremlin-features"></a>Gremlin functies
TinkerPop is een standaard die betrekking heeft op een breed scala aan graph-technologieën. Daarom heeft standaard terminologie toodescribe welke functies worden geleverd door een provider van de grafiek. Azure Cosmos DB voorziet in een permanente, hoge gelijktijdigheid, beschrijfbare graph-database die op meerdere servers of clusters kan worden gepartitioneerd. 

Hallo bevat volgende tabel Hallo TinkerPop functies die worden geïmplementeerd door Azure Cosmos DB: 

| Category | Azure DB Cosmos-implementatie |  Opmerkingen | 
| --- | --- | --- |
| Grafiek-functies | Biedt de persistentie en ConcurrentAccess in preview. Ontworpen toosupport transacties | Computer-methoden kunnen worden geïmplementeerd via Hallo Spark-connector. |
| Variabele functies | Ondersteunt Booleaans, Integer, Byte, dubbelklik, Float, Integer, Long, tekenreeks | Biedt ondersteuning voor primitieve typen, is compatibel met complexe typen via gegevensmodel |
| Hoekpunt functies | Ondersteunt RemoveVertices, MetaProperties, AddVertices, MultiProperties, StringIds, UserSuppliedIds, AddProperty, RemoveProperty  | Ondersteunt het maken, wijzigen en verwijderen van hoekpunten |
| Hoekpunt eigenschap functies | StringIds, UserSuppliedIds, AddProperty, RemoveProperty, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues | Ondersteunt het maken, wijzigen en verwijderen van hoekpunt eigenschappen |
| Edge-functies | AddEges, RemoveEdges, StringIds, UserSuppliedIds, AddProperty, RemoveProperty | Ondersteunt het maken, wijzigen en verwijderen van randen |
| Rand eigenschap functies | Eigenschappen van BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues | Ondersteunt het maken, wijzigen en verwijderen van eigenschappen van rand |

## <a name="gremlin-wire-format-graphson"></a>Gremlin draadindeling: GraphSON

Gebruikt Azure Cosmos-DB Hallo [GraphSON indeling](https://github.com/thinkaurelius/faunus/wiki/GraphSON-Format) bij het retourneren van resultaten van Gremlin bewerkingen. GraphSON is Hallo Gremlin standaardindeling voor het voorstellen hoekpunten randen en met een JSON-eigenschappen (eigenschappen van één of meerdere waarden). 

Bijvoorbeeld: hello volgende fragment toont een GraphSON weergave van een hoekpunt *toohello client geretourneerd* uit Azure Cosmos-database. 

```json
  {
    "id": "a7111ba7-0ea1-43c9-b6b2-efc5e3aea4c0",
    "label": "person",
    "type": "vertex",
    "outE": {
      "knows": [
        {
          "id": "3ee53a60-c561-4c5e-9a9f-9c7924bc9aef",
          "inV": "04779300-1c8e-489d-9493-50fd1325a658"
        },
        {
          "id": "21984248-ee9e-43a8-a7f6-30642bc14609",
          "inV": "a8e3e741-2ef7-4c01-b7c8-199f8e43e3bc"
        }
      ]
    },
    "properties": {
      "firstName": [
        {
          "value": "Thomas"
        }
      ],
      "lastName": [
        {
          "value": "Andersen"
        }
      ],
      "age": [
        {
          "value": 45
        }
      ]
    }
  }
```

Hallo-eigenschappen die zijn gebruikt door GraphSON voor hoekpunten zijn Hallo volgende:

| Eigenschap | Beschrijving |
| --- | --- |
| id | Hallo-ID voor Hallo hoekpunt. Moet uniek zijn (in combinatie met de Hallo-waarde van _partition indien van toepassing) |
| Label | Hallo-label van Hallo hoekpunt. Dit is optioneel en gebruikte toodescribe Hallo entiteitstype. |
| type | Gebruikte toodistinguish hoekpunten van documenten voor niet-grafiek |
| properties | De eigenschappenverzameling van de gebruiker gedefinieerde eigenschappen Hallo hoekpunt gekoppeld. Elke eigenschap kan meerdere waarden hebben. |
| _partition (configureren) | Hallo partitiesleutel van Hallo hoekpunt. Gebruikte tooscale uit grafieken kan toomultiple servers worden |
| outE | Dit document bevat een lijst met uit randen van een hoekpunt. Opslaan van Hallo Aangrenzing informatie met hoekpunt kunt u snel de uitvoering van traversals. Randen zijn gegroepeerd op basis van hun labels. |

En Hallo rand bevat Hallo informatie toohelp met navigatie tooother onderdelen van Hallo grafiek te volgen.

| Eigenschap | Beschrijving |
| --- | --- |
| id | Hallo-ID voor Hallo rand. Moet uniek zijn (in combinatie met de Hallo-waarde van _partition indien van toepassing) |
| Label | Hallo-label van Hallo rand. Deze eigenschap is optioneel en gebruikte toodescribe Hallo relatietype. |
| Geïnventariseerde | Dit document bevat een lijst met in hoekpunten voor een edge. Hallo Aangrenzing informatie op te slaan met Hallo rand kunt u snel de uitvoering van traversals. Hoekpunten worden gegroepeerd op basis van hun labels. |
| properties | De eigenschappenverzameling van de gebruiker gedefinieerde eigenschappen die zijn gekoppeld aan de rand Hallo. Elke eigenschap kan meerdere waarden hebben. |

Elke eigenschap kunnen meerdere waarden binnen een matrix worden opgeslagen. 

| Eigenschap | Beschrijving |
| --- | --- |
| waarde | Hallo-waarde van eigenschap Hallo

## <a name="gremlin-partitioning"></a>Gremlin partitioneren

In Azure Cosmos DB grafieken worden opgeslagen in de containers die kunnen worden geschaald onafhankelijk in termen van opslag en doorvoer (uitgedrukt in genormaliseerde aanvragen per seconde). Elke container moet Definieer een optioneel, maar aanbevolen partitie-sleuteleigenschap die de grens van een logische partitie voor de bijbehorende gegevens bepaalt. Elke hoekpunt/rand moet een hebben een `id` eigenschap die uniek is voor entiteiten in die waarde voor de partitiesleutel. Hallo details vindt u in [partitioneren in Azure Cosmos DB](partition-data.md).

Gremlin bewerkingen werken naadloos tussen grafiekgegevens die meerdere partities in Azure Cosmos DB omvatten. Het is echter aanbevolen toochoose voor uw grafieken die meestal wordt gebruikt als een filter in query's veel afzonderlijke waarden heeft, en vergelijkbare frequentie van toegang tot deze waarden een partitiesleutel. 

## <a name="gremlin-steps"></a>Gremlin stappen
Nu gaan we kijken Hallo Gremlin stappen ondersteund door Azure Cosmos DB. Zie voor een volledig overzicht van Gremlin, [TinkerPop verwijzing](http://tinkerpop.apache.org/docs/current/reference).

| Stap | Beschrijving | TinkerPop 3.2-documentatie | Opmerkingen |
| --- | --- | --- | --- |
| `addE` | Voegt een rand tussen twee hoekpunten | [addE stap](http://tinkerpop.apache.org/docs/current/reference/#addedge-step) | |
| `addV` | Voegt een hoekpunt toohello-grafiek | [addV stap](http://tinkerpop.apache.org/docs/current/reference/#addvertex-step) | |
| `and` | Ensurest dat alle Hallo traversals een waarde retourneren | [en stap](http://tinkerpop.apache.org/docs/current/reference/#and-step) | |
| `as` | Een stap modulator tooassign een variabele toohello uitvoer van een stap | [Als stap](http://tinkerpop.apache.org/docs/current/reference/#as-step) | |
| `by` | Een stap modulator gebruikt met `group` en`order` | [door stap](http://tinkerpop.apache.org/docs/current/reference/#by-step) | |
| `coalesce` | Hallo eerste traversal die een resultaat retourneert geretourneerd | [coalesce-stap](http://tinkerpop.apache.org/docs/current/reference/#coalesce-step) | |
| `constant` | Retourneert een constante waarde. Gebruikt met`coalesce`| [constante stap](http://tinkerpop.apache.org/docs/current/reference/#constant-step) | |
| `count` | Retourneert Hallo telling van het Hallo-transport | [aantal stap](http://tinkerpop.apache.org/docs/current/reference/#count-step) | |
| `dedup` | Retourneert Hallo waarden met Hallo dubbele waarden zijn verwijderd | [Ontdubbeling stap](http://tinkerpop.apache.org/docs/current/reference/#dedup-step) | |
| `drop` | Verwijdert Hallo waarden (hoekpunt/zijde) | [stap verwijderen](http://tinkerpop.apache.org/docs/current/reference/#drop-step) | |
| `fold` | Fungeert als een barrière die wordt berekend Hallo aggregatie van resultaten| [Vouw stap](http://tinkerpop.apache.org/docs/current/reference/#fold-step) | |
| `group` | Groepen Hallo waarden op basis van het Hallo-labels die zijn opgegeven| [groep-stap](http://tinkerpop.apache.org/docs/current/reference/#group-step) | |
| `has` | Toofilter eigenschappen, hoekpunten en randen gebruikt. Ondersteunt `hasLabel`, `hasId`, `hasNot`, en `has` varianten. | [stap heeft](http://tinkerpop.apache.org/docs/current/reference/#has-step) | |
| `inject` | Het invoeren van waarden in een stream| [stap invoeren](http://tinkerpop.apache.org/docs/current/reference/#inject-step) | |
| `is` | Tooperform gebruikt een filter met behulp van een Boole-expressie | [stap](http://tinkerpop.apache.org/docs/current/reference/#is-step) | |
| `limit` | Het aantal items toolimit in Hallo traversal gebruikt| [limiet voor-stap](http://tinkerpop.apache.org/docs/current/reference/#limit-step) | |
| `local` | Lokale teruglopen een gedeelte van een verandering, vergelijkbaar tooa subquery | [lokale stap](http://tinkerpop.apache.org/docs/current/reference/#local-step) | |
| `not` | Tooproduce hello ontkenning van een filter gebruikt | [niet-stap](http://tinkerpop.apache.org/docs/current/reference/#not-step) | |
| `optional` | Retourneert het resultaat van Hallo opgegeven Hallo traversal als het een resultaat anders het resultaat oplevert Hallo aanroepen element | [optionele stap](http://tinkerpop.apache.org/docs/current/reference/#optional-step) | |
| `or` | Zorgt ervoor dat ten minste één Hallo traversals retourneert een waarde | [of -stap](http://tinkerpop.apache.org/docs/current/reference/#or-step) | |
| `order` | Retourneert resultaten in Hallo sorteervolgorde opgegeven | [volgorde-stap](http://tinkerpop.apache.org/docs/current/reference/#order-step) | |
| `path` | Retourneert Hallo volledige pad van Hallo traversal | [pad-stap](http://tinkerpop.apache.org/docs/current/reference/#path-step) | |
| `project` | Eigenschappen van de projecten Hallo als een kaart | [Project-stap](http://tinkerpop.apache.org/docs/current/reference/#project-step) | |
| `properties` | Retourneert Hallo eigenschappen voor Hallo opgegeven labels | [stap eigenschappen](http://tinkerpop.apache.org/docs/current/reference/#properties-step) | |
| `range` | Filters toohello opgegeven waardenbereik| [bereik stap](http://tinkerpop.apache.org/docs/current/reference/#range-step) | |
| `repeat` | Hallo-stap wordt herhaald voor Hallo opgegeven aantal keren. Gebruikt voor het herhalen | [Herhaal stap](http://tinkerpop.apache.org/docs/current/reference/#repeat-step) | |
| `sample` | Toosample resultaten van Hallo traversal gebruikt | [voorbeeld-stap](http://tinkerpop.apache.org/docs/current/reference/#sample-step) | |
| `select` | Tooproject resultaten van Hallo traversal gebruikt |  [Selecteer de stap](http://tinkerpop.apache.org/docs/current/reference/#select-step) | |
| `store` | Gebruikt voor niet-blokkerende statistische functies van Hallo traversal | [stap opslaan](http://tinkerpop.apache.org/docs/current/reference/#store-step) | |
| `tree` | Cumulatieve paden van een hoekpunt in een boomstructuur | [structuur stap](http://tinkerpop.apache.org/docs/current/reference/#tree-step) | |
| `unfold` | Een iterator u als een stap| [stap uitgevouwen](http://tinkerpop.apache.org/docs/current/reference/#unfold-step) | |
| `union` | Resultaten van meerdere traversals samenvoegen| [Union stap](http://tinkerpop.apache.org/docs/current/reference/#union-step) | |
| `V` | Bevat de stappen nodig zijn voor traversals Hallo tussen hoekpunten en randen `V`, `E`, `out`, `in`, `both`, `outE`, `inE`, `bothE`, `outV`, `inV`, `bothV`, en `otherV` voor | [hoekpunt stappen](http://tinkerpop.apache.org/docs/current/reference/#vertex-steps) | |
| `where` | Toofilter resultaten van Hallo traversal gebruikt. Ondersteunt `eq`, `neq`, `lt`, `lte`, `gt`, `gte`, en `between` operators  | [waar stap](http://tinkerpop.apache.org/docs/current/reference/#where-step) | |

Geoptimaliseerd voor schrijven Azure Cosmos-DB-engine biedt ondersteuning voor automatisch indexeren van alle eigenschappen in hoekpunten en randen standaard. Daarom vraagt met filters, query's sorteren, het bereik of aggregaties aan een eigenschap zijn van de index Hallo verwerkt en efficiënt geleverd. Zie voor meer informatie over hoe indexering werkt in Azure Cosmos DB onze paper op [schema networkdirect indexeren](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf).

## <a name="next-steps"></a>Volgende stappen
* Aan de slag bouwen van een toepassing grafiek [met onze SDK's](create-graph-dotnet.md) 
* Meer informatie over [Azure Cosmos DB graph-ondersteuning](graph-introduction.md)

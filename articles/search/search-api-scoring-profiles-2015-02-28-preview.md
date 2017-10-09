---
title: aaaScoring profielen (Azure Search REST API-versie 2015-02-28-Preview) | Microsoft Docs
description: Azure Search is een gehoste cloud-zoekservice die ondersteuning biedt voor afstemming van gerangschikte resultaten op basis van de gebruiker gedefinieerde scoreprofiel profielen.
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: bfd62649-13d7-40b3-a8fa-85521a15084d
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.author: heidist
ms.date: 10/27/2016
ms.openlocfilehash: 17f83fdf6818dc6ffcc3e04f5d0185c6f646b63d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scoring-profiles-azure-search-rest-api-version-2015-02-28-preview"></a>Score berekenen voor profielen (Azure Search REST API-versie 2015-02-28-Preview)
> [!NOTE]
> Dit artikel wordt beschreven scoreprofiel profielen in Hallo [2015-02-28-Preview](search-api-2015-02-28-preview.md). Er is momenteel geen verschil tussen Hallo `2016-09-01` versie beschreven op [MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx) en Hallo `2015-02-28-Preview` versie Hier wordt beschreven, maar wij bieden van dit document toch in de volgorde tooprovide documentdekking tussen Hallo volledige API.
>
>

## <a name="overview"></a>Overzicht
Score berekenen voor verwijst berekening van de score van een zoekopdracht toohello voor elk item in de zoekresultaten worden geretourneerd. Hallo score is een indicator van belang zijn van een item in de context van de huidige zoekopdracht Hallo Hallo. Hallo hogere Hallo score, Hallo meer relevante Hallo-item. In de zoekresultaten zijn items gerangschikt van hoge toolow, op basis van Hallo zoeken score berekend voor elk item positie.

Azure Search gebruikt standaard een initiële score score berekenen voor toocompute, maar u Hallo berekening via een scoreprofiel kunt aanpassen. Scoreprofiel profielen bieden u meer controle over het Hallo-volgorde van items in de zoekresultaten. U kan bijvoorbeeld tooboost items op basis van hun potentiële omzet wilt, nieuwere objecten promoten of mogelijk verhogen items die zijn aangebracht in de inventarisatie is te lang.

Een scoreprofiel maakt deel uit van de indexdefinitie hello, bestaat uit velden, functies en parameters.

toogive u een idee van wat een scoreprofiel lijkt erop dat hello volgende voorbeeld ziet u een eenvoudige profiel met de naam 'geo'. Dit verhoogt de items waarvoor Hallo zoekterm in Hallo `hotelName` veld. Gebruikt ook Hallo `distance` toofavor items die zich binnen tien kilometer van de huidige locatie Hallo werken. Als iemand op Hallo term 'inn zoekt' en 'inn' toobe deel van Hallo hotel naam gebeurt, wordt documenten met hotels met 'inn' hoger in de zoekresultaten Hallo weergegeven.

    "scoringProfiles": [
      {
        "name": "geo",
        "text": {
          "weights": { "hotelName": 5 }
        },
        "functions": [
          {
            "type": "distance",
            "boost": 5,
            "fieldName": "location",
            "interpolation": "logarithmic",
            "distance": {
              "referencePointParameter": "currentLocation",
              "boostingDistance": 10
            }
          }
        ]
      }
    ]

Deze scoreprofiel, uw query is toouse geformuleerd toospecify Hallo profiel op Hallo queryreeks. In onderstaande Hallo query, ziet u Hallo queryparameter `scoringProfile=geo` in Hallo-aanvraag.

    GET /indexes/hotels/docs?search=inn&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&api-version=2015-02-28-Preview

Deze query zoekt op Hallo term 'inn' en wordt doorgegeven in de huidige locatie Hallo. Opmerking dat deze query bevat een of andere parameters, zoals `scoringParameter`. Query-parameters worden beschreven in [documenten zoeken (Azure Search API)](search-api-2015-02-28-preview.md#SearchDocs).

Klik op [voorbeeld](#example) tooreview een meer gedetailleerd voorbeeld van een scoreprofiel.

## <a name="what-is-default-scoring"></a>Wat is standaard score berekenen?
Score berekenen voor berekent een zoekopdracht score voor elk item in een resultaatset waarden van positie geordende. Elk item in de resultatenset van een zoekopdracht is toegewezen een score zoeken en vervolgens hoogste toolowest gerangschikt. Items met hogere scores Hallo worden toohello toepassing geretourneerd. Standaard hello bovenste 50 zijn geretourneerd, maar u kunt Hallo `$top` parameter tooreturn een kleiner of groter aantal items (omhoog too1000 in een enkel antwoord).

Een zoekopdracht-score wordt berekend op basis van statistische eigenschappen van het Hallo-gegevens en Hallo query standaard. Azure Search vindt documenten die Hallo zoektermen in de queryreeks hello opnemen (enkele of alle, afhankelijk van `searchMode`), documenten met veel exemplaren van de zoekterm Hallo voorkeur. Hallo zoeken score toeneemt zelfs hoger als Hallo term zeldzame tussen Hallo gegevens corpus maar algemene binnen Hallo-document. Hallo basis voor deze benadering toocomputing relevantie staat bekend als TF-IDF of (frequentie term frequentie inverse document).

Ervan uitgaande dat er geen aangepaste sorteren,-resultaten, worden vervolgens op Zoeken score gerangschikt voordat ze de aanroepende toepassing toohello worden geretourneerd. Als `$top` niet is opgegeven, 50 items met de hoogste zoeken Hallo score worden geretourneerd.

Zoeken score waarden kunnen worden herhaald in een resultatenset. Bijvoorbeeld, u wellicht 10 items met een score van 1.2 20 items met een score van 1.0 en 20 items met een score van 0,5. Wanneer meerdere treffers hebben dezelfde zoeken score hello, Hallo ordening van dezelfde scored items is niet gedefinieerd en is niet stabiel. Hallo query opnieuw uitvoert en u ziet mogelijk verschuift de positie van items. Twee items met een identieke score gegeven, wordt er geen garantie van welke eerst verschijnt is.

## <a name="when-toouse-custom-scoring"></a>Wanneer toouse aangepaste score berekenen
Wanneer Hallo standaard rangschikken gedrag niet gaat ver genoeg in voldoen aan uw zakelijke doelstellingen, moet u een of meer scoreprofiel profielen maken. U kunt bijvoorbeeld besluiten dat zoekrelevantie voorrang toegevoegde items moet geven. Ook moet u wellicht een veld dat winstmarge bevat, of een ander veld potentiële omzet waarmee wordt aangegeven. Versterking van treffers die voordelen tooyour business meenemen, kan een belangrijke factor in score berekenen voor profielen toouse beslist zijn.

Op basis van relevantie ordening wordt ook geïmplementeerd via score berekenen voor profielen. Houd rekening met pagina's die u hebt gebruikt in de afgelopen Hallo waarmee u kunnen op prijs, datum, classificatie of relevantie sorteren zoekresultaten. In Azure Search station scoreprofiel profielen Hallo 'relevantie' optie. Hallo-definitie van belang is door u worden beheerd, echter afhankelijk van de zakelijke doelstellingen en Hallo type zoekervaring gewenste toodeliver.

<a name="example"></a>

## <a name="example"></a>Voorbeeld
Zoals vermeld, wordt aangepaste score berekenen geïmplementeerd via score berekenen voor profielen die zijn gedefinieerd in het indexschema van een.

In dit voorbeeld toont Hallo schema van een index met twee scoreprofiel profielen (`boostGenre`, `newAndHighlyRated`). Een query op deze index die beide profiel bevat, zoals een queryparameter Hallo profiel tooscore Hallo-resultatenset wordt gebruikt.

    {
      "name": "musicstoreindex",
      "fields": [
        { "name": "key", "type": "Edm.String", "key": true },
        { "name": "albumTitle", "type": "Edm.String" },
        { "name": "albumUrl", "type": "Edm.String", "filterable": false },
        { "name": "genre", "type": "Edm.String" },
        { "name": "genreDescription", "type": "Edm.String", "filterable": false },
        { "name": "artistName", "type": "Edm.String" },
        { "name": "orderableOnline", "type": "Edm.Boolean" },
        { "name": "rating", "type": "Edm.Int32" },
        { "name": "tags", "type": "Collection(Edm.String)" },
        { "name": "price", "type": "Edm.Double", "filterable": false },
        { "name": "margin", "type": "Edm.Int32", "retrievable": false },
        { "name": "inventory", "type": "Edm.Int32" },
        { "name": "lastUpdated", "type": "Edm.DateTimeOffset" }
      ],
      "scoringProfiles": [
        {
          "name": "boostGenre",
          "text": {
            "weights": {
              "albumTitle": 1.5,
              "genre": 5,
              "artistName": 2
            }
          }
        },
        {
          "name": "newAndHighlyRated",
          "functions": [
            {
              "type": "freshness",
              "fieldName": "lastUpdated",
              "boost": 10,
              "interpolation": "quadratic",
              "freshness": {
                "boostingDuration": "P365D"
              }
            },
            {
              "type": "magnitude",
              "fieldName": "rating",
              "boost": 10,
              "interpolation": "linear",
              "magnitude": {
                "boostingRangeStart": 1,
                "boostingRangeEnd": 5,
                "constantBoostBeyondRange": false
              }
            }
          ]
        }
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["albumTitle", "artistName"]
        }
      ]
    }


## <a name="workflow"></a>Werkstroom
aangepaste tooimplement score berekenen gedrag, een score profiel toohello schema toevoegt waarin Hallo index definieert. U kunt hebben van too16 scoreprofiel profielen in een index (Zie [Servicelimieten](search-limits-quotas-capacity.md)), maar u kunt slechts één profiel tegelijk in een bepaalde query opgeven.

Beginnen met Hallo [sjabloon](#bkmk_template) vindt u in dit onderwerp.

Geef een naam. Scoreprofiel profielen zijn optioneel, maar als u een toevoegen, Hallo-naam is vereist. Worden ervoor toofollow Hallo naamgevingsregels voor velden (begint met een letter, voorkomt speciale tekens en gereserveerde woorden). Zie [naamgevingsregels](http://msdn.microsoft.com/library/azure/dn857353.aspx) voor meer informatie.

Hallo-hoofdtekst van Hallo score berekenen profiel is samengesteld uit gewogen velden en functies.

### <a name="weights"></a>Gewicht
Hallo `weights` eigenschap van een scoreprofiel geeft u naam-waardeparen die een relatieve gewicht tooa veld toewijzen. In Hallo [voorbeeld](#example), Hallo albumTitle genre en artistName velden zijn gestimuleerd 1.5, 5 en 2, respectievelijk. Waarom wordt genre versterkt zoveel hoger dan Hallo anderen? Als de zoekopdracht wordt uitgevoerd via de gegevens die zijn enigszins homogene (zoals Hallo geval met 'genre' in hello `musicstoreindex`), moet u mogelijk een groter verschil in Hallo relatieve gewicht. Bijvoorbeeld in Hallo `musicstoreindex`, 'uit' wordt weergegeven als beide genre en in dezelfde geformuleerd genre beschrijvingen. Als u genre toooutweigh genre beschrijving wilt, moet Hallo genre veld een veel hoger relatieve gewicht.

### <a name="functions"></a>Functies
Functies worden gebruikt wanneer extra berekeningen nodig om specifieke contexten zijn. Geldige functietypen zijn `freshness`, `magnitude`, `distance` en `tag`. Elke functie heeft parameters die uniek tooit zijn.

* `freshness`moet worden gebruikt als u wilt dat tooboost door hoe nieuwe of oude een item is. Deze functie kan alleen worden gebruikt met datetime-velden (`Edm.DataTimeOffset`). Opmerking Hallo `boostingDuration` kenmerk wordt alleen gebruikt met Hallo nieuwheid functie.
* `magnitude`moet worden gebruikt als u wilt dat tooboost op basis van hoe hoog of laag van een numerieke waarde is. Scenario's die voor deze functie aanroepen zijn waarbij de winstmarge, hoogste prijs, laagste prijs of het aantal downloads. Als u wilt dat Hallo inverse patroon (bijvoorbeeld tooboost lagere prijs items meer dan hogere geprijsde items), kunt u Hallo bereik, hoge toolow omkeren. Gegeven een bereik van de prijzen van $100 te$ 1, stelt u `boostingRangeStart` op 100 en `boostingRangeEnd` 1 tooboost Hallo lagere prijs items. Deze functie kan alleen worden gebruikt met velden double en geheel getal.
* `distance`moet worden gebruikt als u wilt dat tooboost door nabijheid of geografische locatie. Deze functie kan alleen worden gebruikt met `Edm.GeographyPoint` velden.
* `tag`moet worden gebruikt als u wilt dat tooboost door codes gemeenschappelijk tussen documenten en zoekquery's. Deze functie kan alleen worden gebruikt met `Edm.String` en `Collection(Edm.String)` velden.

#### <a name="rules-for-using-functions"></a>Regels voor het gebruik van functies
* Functietype (versheid, grootte, afstand, tag) moet in kleine letters.
* Functies kunnen niet null of lege waarden bevatten. Als u fieldname opneemt, u hebt tooset het toosomething.
* Functies kunnen alleen worden toegepast toofilterable velden. Zie [Create Index](search-api-2015-02-28-preview.md#CreateIndex) voor meer informatie over Filterbaar velden.
* Functies kunnen alleen worden toegepast toofields die zijn gedefinieerd in de verzameling van velden Hallo van een index.

Na het Hallo index is gedefinieerd, Hallo index bouwen door Hallo Indexeer schema, gevolgd door documenten te uploaden. Zie [Create Index](search-api-2015-02-28-preview.md#CreateIndex) en [toevoegen of Update documenten](search-api-2015-02-28-preview.md#AddOrUpdateDocuments) voor instructies voor deze bewerkingen. Zodra het Hallo-index is samengesteld, moet u een functionele scoreprofiel die geschikt is voor uw zoekopdracht gegevens hebben.

<a name="bkmk_template"></a>

## <a name="template"></a>Template
Deze sectie toont Hallo syntaxis en sjabloon voor score berekenen voor profielen. Raadpleeg te[Index kenmerkverwijzing](#bkmk_indexref) in de volgende sectie Hallo voor beschrijvingen van Hallo kenmerken.

    ...
    "scoringProfiles": [
      {
        "name": "name of scoring profile",
        "text": (optional, only applies toosearchable fields) {
          "weights": {
            "searchable_field_name": relative_weight_value (positive #'s),
            ...
          }
        },
        "functions": (optional) [
          {
            "type": "magnitude | freshness | distance | tag",
            "boost": # (positive number used as multiplier for raw score != 1),
            "fieldName": "...",
            "interpolation": "constant | linear (default) | quadratic | logarithmic",

            "magnitude": {
              "boostingRangeStart": #,
              "boostingRangeEnd": #,
              "constantBoostBeyondRange": true | false (default)
            }

            // (- or -)

            "freshness": {
              "boostingDuration": "..." (value representing timespan over which boosting occurs)
            }

            // (- or -)

            "distance": {
              "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location)
              "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
            }

            // (- or -)

            "tag": {
              "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field)
            }
          }
        ],
        "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
      }
    ],
    "defaultScoringProfile": (optional) "...",
    ...

<a name="bkmk_indexref"></a>

## <a name="scoring-profile-property-reference"></a>Score berekenen profiel eigenschapverwijzing
> [!NOTE]
> Een score functie kan alleen worden toegepast toofields die Filterbaar zijn.
>
>

| Eigenschap | Beschrijving |
| --- | --- |
| `name` |Vereist. Dit is de naam Hallo Hallo score berekenen profiel. Er volgt Hallo aliasnaam gelden dezelfde regels van een veld. Het moet beginnen met een letter, mogen geen punten, dubbele punten bevatten of @ symbolen, en mag niet beginnen met Hallo zinsnede 'azuresearch ' omdat' (hoofdlettergevoelig). |
| `text` |Hallo gewichten eigenschap bevat. |
| `weights` |Optioneel. Een naam / waarde-paar waarmee een veldnaam en het relatieve gewicht. Relatieve gewicht moet een positief geheel getal of een getal met drijvende komma. U kunt de veldnaam Hallo zonder een bijbehorende gewicht opgeven. Gewicht zijn gebruikte tooindicate Hallo belang van relatieve tooanother één veld. |
| `functions` |Optioneel. Houd er rekening mee een score functie kan alleen worden toegepast toofields die Filterbaar zijn. |
| `type` |Vereist voor scorefuncties functies. Geeft de functie toouse Hallo type. Geldige waarden zijn `magnitude`, `freshness`, `distance` en `tag`. U kunt meer dan één functie in elke scoreprofiel opnemen. de naam van de functie Hallo moet kleine letters. |
| `boost` |Vereist voor scorefuncties functies. Een positief getal dat wordt gebruikt als vermenigvuldiger voor onbewerkte scores. Kan niet gelijk too1. |
| `fieldName` |Vereist voor scorefuncties functies. Een score functie kan alleen worden toegepast toofields die deel uitmaken van de verzameling van veld Hallo van Hallo-index en die Filterbaar zijn. Elk functietype introduceert bovendien aanvullende beperkingen (nieuwheid wordt gebruikt met datetime-velden magnitude met geheel getal zijn of dubbel velden, afstand met locatievelden en label met een tekenreeks of een verzameling tekenreeksvelden). U kunt slechts één veld per functiedefinitie opgeven. Voor bijvoorbeeld toouse magnitude tweemaal in Hallo hetzelfde profiel, moet u twee tooinclude definities magnitude, één voor elk veld. |
| `interpolation` |Vereist voor scorefuncties functies. Definieert de helling Hallo voor welke Hallo scoreversterking toeneemt van Hallo Hallo bereik toohello einde van het Hallo-bereik is gestart. Geldige waarden zijn `linear` (standaard), `constant`, `quadratic`, en `logarithmic`. Zie [interpolations ingesteld](#bkmk_interpolation) voor meer informatie. |
| `magnitude` |Hallo magnitude score berekenen voor de functie is gebruikte tooalter classificaties op basis van Hallo bereik van waarden voor een numeriek veld. Enkele van Hallo meest voorkomende gebruiksvoorbeelden hiervan zijn:<ul><li>Sterclassificaties: Alter Hallo score berekenen op basis van Hallo-waarde in 'Ster classificatie' Hallo-veld. Wanneer twee items zijn die relevant, wordt eerst Hallo-item met de Hallo hogere classificatie weergegeven.</li><li>Marge: Wanneer twee documenten zijn die relevant, de detailhandel kunt desgewenst tooboost documenten waarvoor hogere marges eerst.</li><li>Klik op de aantallen: voor toepassingen die volgen, klikt u op door acties tooproducts of pagina's, kunt u magnitude tooboost items die doorgaans tooget Hallo de meeste verkeer.</li><li>Telt het aantal downloaden: voor toepassingen die downloads bijhouden Hallo magnitude functie kunt u items waarvoor Hallo meeste downloads verbeteren.</li></ul> |
| `magnitude:boostingRangeStart` |Sets Hallo start waarde van Hallo bereik gedurende welke de magnitude wordt berekend. Hallo-waarde moet een geheel getal of een getal met drijvende komma zijn. Voor sterwaarderingen van 1 tot en met 4, zou dit 1. Voor de marges van meer dan 50% zou dit 50. |
| `magnitude:boostingRangeEnd` |Hiermee stelt u Hallo eindwaarde van Hallo bereik gedurende welke de magnitude wordt berekend. Hallo-waarde moet een geheel getal of een getal met drijvende komma zijn. Voor sterwaarderingen van 1 tot en met 4, zou dit 4. |
| `magnitude:constantBoostBeyondRange` |Geldige waarden zijn true of false (standaard). Bij het instellen van tootrue, Hallo volledige versterking tooapply toodocuments die een waarde hebben voor Hallo doelveld hoger is dan de bovengrens Hallo van Hallo bereik. Als het ONWAAR is, niet Hallo versterking van deze functie toegepaste toodocuments een waarde Hallo doelveld die buiten Hallo bereik valt. |
| `freshness` |Hallo nieuwheid score berekenen voor de functie is gebruikte tooalter rangschikking scores voor items op basis van waarden in de DateTimeOffset-velden. Een item met een meer recente datum kan bijvoorbeeld hoger dan de oudere items worden gerangschikt. (Opmerking Het is ook mogelijk toorank items zoals agenda-items met toekomstige datums zodat items dichter toohello aanwezig op de hoger dan items verder in toekomstige hello wordt gerangschikt.) Het huidige servicerelease hello, wordt één end van Hallo bereik verholpen toohello huidige tijd. Hallo andere einde is een tijd in de afgelopen op basis van Hallo Hallo `boostingDuration`. een aantal keer Hallo toekomstige tooboost gebruiken een negatieve `boostingDuration`. Hallo tarief op welke Hallo versterking van wijzigingen uit een maximale en minimale bereik wordt bepaald door Hallo interpolatie toegepast toohello score berekenen profiel (Zie onderstaande afbeelding ziet Hallo). tooreverse Hallo prestatieverbetering factor die wordt toegepast, kiest u een factor versterking van minder dan 1. |
| `freshness:boostingDuration` |Hiermee stelt u een vervalperiode in waarna versterking van een bepaald document wordt stopgezet. Zie [boostingDuration ingesteld](#bkmk_boostdur) in Hallo volgende sectie voor de syntaxis en voorbeelden. |
| `distance` |Hallo afstand score berekenen voor de functie is gebruikte tooaffect Hallo score van documenten op basis van hoe sluiten of ver ze zich relatieve tooa opgegeven geografische locatie. Hallo referentielocatie krijgt als onderdeel van Hallo-query in een parameter (met behulp van Hallo `scoringParameter` queryparameter) als een ion, lat argument. |
| `distance:referencePointParameter` |Een parameter toobe doorgegeven als verwijzing locatie toouse query's. scoringParameter is een queryparameter. Zie [documenten zoeken](search-api-2015-02-28-preview.md#SearchDocs) voor beschrijvingen van de queryparameters. |
| `distance:boostingDistance` |Een getal dat aangeeft Hallo afstand in kilometer tot Hallo verwijzing locatie waar Hallo versterking bereik eindigt. |
| `tag` |Hallo score berekenen voor de functie wordt gebruikt tooaffect Hallo score van documenten op basis van de labels in documenten en zoekquery's. Kan documenten met labels net als bij Hallo-zoekopdracht wordt verhoogd. Hallo labels voor zoekquery Hallo is opgegeven als parameter voor elke zoekaanvraag scoreprofiel (met behulp van Hallo `scoringParameter` queryparameter). |
| `tag:tagsParameter` |Een parameter toobe doorgegeven in query's toospecify labels voor een bepaald verzoek. `scoringParameter`is een queryparameter. Zie [documenten zoeken](search-api-2015-02-28-preview.md#SearchDocs) voor beschrijvingen van de queryparameters. |
| `functionAggregation` |Optioneel. Geldt alleen als functies worden opgegeven. Geldige waarden zijn: `sum` (standaard), `average`, `minimum`, `maximum`, en `firstMatching`. Een score search is een waarde die wordt berekend op basis van meerdere variabelen, met inbegrip van meerdere functies. Deze kenmerken geeft aan hoe Hallo verhoogt van alle Hallo-functies worden gecombineerd tot een enkel cumulatieve versterking die zich bevindt, wordt de toegepaste toohello baseren document score. Hallo base score is gebaseerd op Hallo tf-idf waarde berekend op basis van Hallo document en Hallo zoekopdracht. |
| `defaultScoringProfile` |Wanneer u een zoekopdracht uitvoert als er geen scoreprofiel is opgegeven, wordt standaard score berekenen gebruikt (tf-idf alleen). Score berekenen profielnaam standaard kan hier worden ingesteld waardoor Azure Search toouse wanneer er geen specifieke profiel wordt gegeven in de zoekaanvraag Hallo dit profiel. |

<a name="bkmk_interpolation"></a>

## <a name="set-interpolations"></a>Set interpolations
Interpolations kunt u toodefine Hallo helling voor welke Hallo scoreversterking toeneemt van Hallo Hallo bereik toohello einde van het Hallo-bereik is gestart. Hallo na interpolations kan worden gebruikt:

* `Linear`: Voor de items die zich binnen het Hallo max en min bereik, worden Hallo versterking toegepast toohello item uitgevoerd in een voortdurend afneemt. Lineaire is Hallo standaard interpolatie voor een scoreprofiel.
* `Constant`: Voor de items die zich binnen het Hallo-begin- en bereik beëindigen, worden een versterking van constante toegepaste toohello positie resultaten.
* `Quadratic`: ABC wordt in eerste instantie afnemen in kleinere tempo in vergelijking tooa lineaire interpolatie die een voortdurend afnemende versterking heeft, en als het Hallo-eindbereik nadert, deze neemt af op basis van een veel hoger interval. Deze optie interpolatie is niet toegestaan in label score berekenen voor functies.
* `Logarithmic`: Logaritmisch wordt in eerste instantie verkleinen hoger tempo in vergelijking tooa lineaire interpolatie die een voortdurend afnemende versterking heeft, en als het Hallo-eindbereik nadert, deze neemt af op basis van een veel kleinere interval. Deze optie interpolatie is niet toegestaan in label score berekenen voor functies.

<a name="Figure1"></a> ![][1]

<a name="bkmk_boostdur"></a>

## <a name="set-boostingduration"></a>Set boostingDuration
`boostingDuration`is een kenmerk van Hallo nieuwheid functie. U tooset een vervalperiode in waarna versterking stopt van een bepaald document. Tooboost producten of merken gedurende een periode 10 dagen, geeft u bijvoorbeeld Hallo 10 dagen als 'P10D' voor deze documenten. Of tooboost toekomstige gebeurtenissen in Hallo volgende week opgeven '-P7D '.

`boostingDuration`moet worden opgemaakt als een XSD-waarde van het 'dayTimeDuration' (een beperkte subset van een ISO 8601-duurwaarde). Hallo-patroon hiervoor is: `[-]P[nD][T[nH][nM][nS]]`.

Hallo volgende tabel bevat enkele voorbeelden.

| Duur | boostingDuration |
| --- | --- |
| 1 dag |'P1D' |
| 2 dagen en 12 uur |'P2DT12H' |
| 15 minuten |'PT15M' |
| 30 dagen, 5 uur, 10 minuten en 6.334 seconden |'P30DT5H10M6.334S' |

Zie voor meer voorbeelden [XML-Schema: gegevenstypen (website W3.org)](http://www.w3.org/TR/xmlschema11-2/).

**Zie ook**
[Azure Search Service REST-API](http://msdn.microsoft.com/library/azure/dn798935.aspx) op MSDN <br/>
[Index (Azure Search API) maken](http://msdn.microsoft.com/library/azure/dn798941.aspx) op MSDN<br/>
[Toevoegen van een score profiel tooa search-index](http://msdn.microsoft.com/library/azure/dn798928.aspx) op MSDN<br/>

<!--Image references-->
[1]: ./media/search-api-scoring-profiles-2015-02-28-Preview/scoring_interpolations.png

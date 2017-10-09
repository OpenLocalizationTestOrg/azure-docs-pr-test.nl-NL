---
title: architectuur van aaaFull tekst zoeken engine (Lucene) in Azure Search | Microsoft Docs
description: Uitleg van de Lucene query verwerking en document ophalen concepten voor zoeken in volledige tekst, als verwante tooAzure zoeken.
services: search
manager: jhubbard
author: yahnoosh
documentationcenter: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/06/2017
ms.author: jlembicz
ms.openlocfilehash: c6d1bea8d40154fd9237b9e44584cdfcd193cbd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-full-text-search-works-in-azure-search"></a>Hoe vol tekst zoeken werkt in Azure Search

Dit artikel is voor ontwikkelaars die u een beter begrip moeten van de werking van Lucene zoeken in volledige tekst in Azure Search. Voor tekst-query's, Azure Search naadloos verwachte resultaten in de meeste gevallen levert, maar soms mogelijk krijgt u een resultaat enigszins lijkt "off". In deze situaties met een achtergrond in vier fasen van de queryuitvoering Lucene Hallo (query parseren, lexicale analyse, document-koppeling, score berekenen) kunt u specifieke wijzigingen tooquery parameters te identificeren of index van de configuratie die Hallo levert het gewenste resultaat. 

> [!Note] 
> Azure Search Lucene gebruikt voor zoekopdrachten in volledige tekst, maar Lucene-integratie is niet volledig. We selectief weergeven en Lucene functionaliteit tooenable Hallo scenario's belangrijke tooAzure zoekopdracht uit te breiden. 

## <a name="architecture-overview-and-diagram"></a>Overzicht van de architectuur en diagram

Verwerking van een zoekopdracht voor volledige tekst begint met het parseren van tooextract zoektermen op Hallo query tekst. Hallo zoekmachine maakt gebruik van een index tooretrieve documenten met overeenkomende voorwaarden. Afzonderlijke querytermen soms worden opgedeeld en geregenereerd in nieuwe formulieren toocast breder net over wat kan worden beschouwd als een mogelijke overeenkomst. Geen resultatenset is vervolgens gesorteerd op een relevantie score toegewezen tooeach afzonderlijke overeenkomende document. Die boven Hallo Hallo gerangschikte lijst worden de aanroepende toepassing toohello geretourneerd.

Aangepast, bestaat uitvoering van de query uit vier fasen: 

1. Query bij het parseren van 
2. Lexicale analyse 
3. Document ophalen 
4. Score berekenen 

Hallo diagram hieronder ziet u Hallo onderdelen die worden gebruikt tooprocess een zoekaanvraag. 

 ![Architectuurdiagram van de Lucene-query in Azure Search][1]


| Belangrijkste onderdelen | Functionele beschrijving | 
|----------------|------------------------|
|**Query parsers** | Afzonderlijke querytermen van query's en Hallo query structuur (een querystructuur) toobe verzonden toohello zoekmachine maken. |
|**Analyzers** | Lexicale analyse uitvoeren op querytermen. Dit proces kan betrekking hebben op transformeren, te verwijderen of uitbreiden van de voorwaarden van de query. |
|**Index** | Een efficiënte gegevensstructuur toostore gebruikt en organiseren doorzoekbare voorwaarden opgehaald uit de geïndexeerde documenten. |
|**Zoekmachine** | Haalt en scores die overeenkomt met de documenten op basis van de inhoud Hallo Hallo omgekeerd index. |

## <a name="anatomy-of-a-search-request"></a>Anatomie van een zoekaanvraag

Een zoekaanvraag is een complete specificatie van wat moet worden geretourneerd in een resultatenset. In de meest eenvoudige vorm is een lege query zonder criteria alle soorten. Een voorbeeld van een meer realistische parameters bevat, verschillende query termen, mogelijk bereik toocertain velden, met mogelijk een filterexpressie en ordening van regels.  

Hallo volgende voorbeeld wordt een zoekaanvraag u mogelijk tooAzure Search verzendt met behulp van Hallo [REST-API](https://docs.microsoft.com/rest/api/searchservice/search-documents).  

~~~~
POST /indexes/hotels/docs/search?api-version=2016-09-01 
{  
    "search": "Spacious, air-condition* +\"Ocean view\"",  
    "searchFields": "description, title",  
    "searchMode": "any",
    "filter": "price ge 60 and price lt 300",  
    "orderby": "geo.distance(location, geography'POINT(-159.476235 22.227659)')", 
    "queryType": "full" 
 } 
~~~~

Voor deze aanvraag zoekmachine Hallo Hallo te volgen:

1. Documenten gefilterd waar Hallo prijs is ten minste $60 en minder dan 300 $.
2. Hallo query worden uitgevoerd. In dit voorbeeld Hallo zoekquery bestaat uit zinnen en voorwaarden: `"Spacious, air-condition* +\"Ocean view\""` (gebruikers doorgaans niet leestekens in te voeren, maar op te nemen in Hallo voorbeeld, kunnen wij tooexplain hoe analyzers verwerkt; het). Voor deze query zoekmachine Hallo Hallo beschrijving gescand en titelvelden opgegeven in `searchFields` voor documenten die 'Oceaan weergave' bevatten en ook op Hallo term 'groot' of op voorwaarden die met het voorvoegsel Hallo beginnen 'air-condition'. Hallo `searchMode` parameter gebruikte toomatch zich op een term (standaard) of al deze gevallen waarbij een term niet expliciet hoeft (`+`).
3. Resulterende reeks hotels Hallo orders door nabijheid tooa opgegeven geografische locatie en vervolgens de aanroepende toepassing toohello wordt geretourneerd. 

Hallo meerderheid van dit artikel is over het verwerken van Hallo *zoekquery*: `"Spacious, air-condition* +\"Ocean view\""`. Filteren en ordening vallen buiten het bereik. Zie voor meer informatie, Hallo [zoeken-API-naslagdocumentatie](https://docs.microsoft.com/rest/api/searchservice/search-documents).

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a>Stap 1: Een Query bij het parseren van 

Zoals vermeld, is queryreeks Hallo Hallo eerste regel van Hallo-aanvraag: 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

Hallo query parser scheidt operators (zoals `*` en `+` in Hallo voorbeeld) in een zoekvak, en het Hallo-zoekopdracht in deconstructs *subquery's* met een ondersteund type: 

+ *term query* voor zelfstandige voorwaarden (zoals groot)
+ *woordgroep query* voor tussen aanhalingstekens voorwaarden (zoals Oceaan weergave)
+ *voorvoegsel query* voor voorwaarden gevolgd door een operator voorvoegsel `*` (zoals air-condition)

Zie voor een volledige lijst met ondersteunde querytypen [Lucene query sytnax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

Operators die zijn gekoppeld aan een subquery bepalen of Hallo query 'moet' of 'moet' om een document tevreden toobe beschouwd als een overeenkomst. Bijvoorbeeld: `+"Ocean view"` 'moet' is vanwege toohello `+` operator. 

Hallo queryparser worden opnieuw gestructureerd Hallo subquery's in een *querystructuur* (een interne structuur die Hallo query) dit wordt doorgegeven op toohello zoekmachine. In de eerste fase van de query bij het parseren van Hallo uitziet Hallo querystructuur.  

 ![Booleaanse waarde searchmode ieder query][2]

### <a name="supported-parsers-simple-and-full-lucene"></a>Ondersteund parsers: eenvoudig en volledige Lucene 

 Azure Search beschrijft de twee andere querytalen `simple` (standaard) en `full`. Door de instelling Hallo `queryType` parameter bij uw zoekaanvraag, geeft u aan Hallo queryparser welke querytaal gewenst zodat deze weet hoe toointerpret Hallo operators en syntaxis. Hallo [eenvoudige query taal](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) intuïtief en robuuste, vaak geschikte toointerpret gebruikersinvoer als-is zonder dat de verwerking van de clientzijde. Biedt ondersteuning voor query's van webzoekmachines bekend. Hallo [volledige Lucene-querytaal](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), die wordt geleverd door in te stellen `queryType=full`, wordt de standaardtaal eenvoudige query Hallo uitgebreid met ondersteuning voor meer operators en querytypen zoals jokerteken, bij benadering, regex en veldgerelateerde query's. Bijvoorbeeld, wordt een reguliere expressie in vereenvoudigde querysyntaxis verzonden geïnterpreteerd als een queryreeks bevat en niet een expressie. aanvraag voor het voorbeeld in dit artikel Hallo Hallo volledige Lucene querytaal gebruikt.

### <a name="impact-of-searchmode-on-hello-parser"></a>Gevolgen van het searchMode op Hallo parser 

Een andere aanvraag zoekparameter die gevolgen heeft voor het parseren is Hallo `searchMode` parameter. Hiermee kunt u de standaardoperator Hallo voor Boole-query's: een (standaard) of alle.  

Wanneer `searchMode=any`, dat standaard Hallo Hallo spatie als scheidingsteken tussen groot is en air-condition is of (`||`), waardoor Hallo query voorbeeldtekst gelijk aan: 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

Expliciete operators zoals `+` in `+"Ocean view"`, zijn niet-ambigue Booleaanse query constructie (Hallo term *moet* overeen). Minder duidelijk is hoe toointerpret Hallo resterende termen: groot en air-condition. Moet Hallo zoekmachine overeenkomsten vinden voor de weergave Oceaan *en* groot *en* air-condition? Of moet Oceaan weergave vinden plus *een* Hallo resterende voorwaarden? 

Standaard (`searchMode=any`), Hallo zoekmachine wordt ervan uitgegaan dat Hallo breder interpretatie. Een veld *moet* overeenkomen, opgetreden bij het weergeven 'of' semantiek. structuur van de eerste query Hallo geïllustreerd voorheen Hello twee 'moet' bewerkingen, toont Hallo standaard.  

Stel dat we nu `searchMode=all`. In dit geval wordt Hallo ruimte geïnterpreteerd als een 'en'-bewerking. Elk van de overige voorwaarden Hallo zijn beide aanwezig in Hallo document tooqualify als een overeenkomst. de resulterende voorbeeldquery Hello wordt geïnterpreteerd als volgt: 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

Een boomstructuur gewijzigde query voor deze query zou zijn als volgt, waarbij een overeenkomende document Hallo snijpunt van alle drie subquery's is: 

 ![Booleaanse query searchmode alle][3]

> [!Note] 
> Kiezen `searchMode=any` via `searchMode=all` is een beste beslissing ontvangen op door het uitvoeren van representatieve query's. Gebruikers die waarschijnlijk tooinclude operators (algemeen zijn wanneer zoeken document opslaat) wellicht resultaten intuïtievere als `searchMode=all` informeert Booleaanse query constructies. Voor meer informatie over de wisselwerking tussen Hallo `searchMode` en operators, Zie [vereenvoudigde querysyntaxis](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a>Stap 2: Lexicale analyse 

Lexicale analyzers proces *benaming query's* en *woorden van query's* nadat Hallo querystructuur is opgebouwd. Een analyzer accepteert tekst invoer opgegeven tooit Hallo door Hallo parser, processen tekst hello en vervolgens verzendt terug tokenized voorwaarden toobe opgenomen in de querystructuur van de Hallo. 

meest voorkomende vorm van lexicale analyse Hallo is *taalkundige analysis* welke transformaties querytermen op basis van regels voor specifieke tooa opgegeven taal: 

* Een query term toohello hoofdmap vorm van een woord verminderen 
* Verwijderen van niet-essentiële woorden (stopwoorden, zoals 'het' of 'en' in het Engels) 
* Een samengestelde woord in onderdelen op te splitsen 
* Kleine hoofdlettergebruik van een woord hoofdletters 

Al deze bewerkingen vaak tooerase verschillen tussen Hallo tekstinvoer geleverd door het Hallo-gebruiker en Hallo voorwaarden opgeslagen in het Hallo-index. Dergelijke bewerkingen voorbij de verwerking van tekst en vereisen diepgaande kennis van Hallo taal zelf. tooadd deze laag van de taalkundige awareness, Azure Search ondersteunt een lange lijst met [taalanalyse](https://docs.microsoft.com/rest/api/searchservice/language-support) van Lucene en van Microsoft.

> [!Note]
> Vereisten voor analyse kunnen variëren van minimale tooelaborate afhankelijk van uw scenario. U kunt de complexiteit van lexicale analyse beheren door Hallo een vooraf gedefinieerde Hallo analyzers te selecteren of door het maken van uw eigen [aangepaste analyzer](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search). Analyzers bereik toosearchable velden zijn en worden opgegeven als onderdeel van de velddefinitie van een. Hiermee kunt u toovary lexicale analyse op basis van de per-veld. Hallo niet is opgegeven, *standaard* Lucene analyzer wordt gebruikt.

In ons voorbeeld voorafgaande tooanalysis Hallo eerste querystructuur heeft Hallo term 'Spacious' met een hoofdletter "S" en een komma die queryparser Hallo wordt geïnterpreteerd als een deel van de zoekterm hello (een door komma's wordt niet beschouwd als een query language-operator).  

Wanneer Hallo standaard analyzer Hallo term verwerkt, wordt deze kleine letters 'Oceaan weergeven' en 'groot' en Hallo kommateken verwijderen. Hallo gewijzigde querystructuur ziet er als volgt uit: 

 ![Booleaanse query geanalyseerde voorwaarden][4]

### <a name="testing-analyzer-behaviors"></a>Analyzer gedrag testen 

Hallo-gedrag van een analyzer kan worden getest met Hallo [analyseren API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer). Geef Hallo tekst tooanalyze toosee welke vermeldingen analyzer wordt gegenereerd. Bijvoorbeeld, hoe Hallo standaard analyzer zou verwerken toosee Hallo tekst 'air-condition', kunt u de volgende aanvraag Hallo uitgeven:

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

de ingevoerde tekst hello Hallo standaard analyzer opgesplitst in Hallo na twee tokens, aantekeningen te maken met kenmerken zoals begin en einde offsets (gebruikt voor het markeren van treffers), evenals hun positie (gebruikt voor de zinsnede overeenkomende):

~~~~
{  
  "tokens": [
    {
      "token": "air",
      "startOffset": 0,
      "endOffset": 3,
      "position": 0
    },
    {
      "token": "condition",
      "startOffset": 4,
      "endOffset": 13,
      "position": 1
    }
  ]
}
~~~~

### <a name="exceptions-toolexical-analysis"></a>Uitzonderingen toolexical analyse 

Lexicale analysis geldt alleen tooquery typen waarvoor volledige voorwaarden – een term query of een woordgroep-query. Het tooquery typen met onvolledige voorwaarden – voorvoegsel query, jokertekens query, regex query – of tooa fuzzy query niet van toepassing. De querytypen, inclusief Hallo voorvoegsel query met term *air-condition\**  in ons voorbeeld toegevoegd rechtstreeks toohello querystructuur Hallo analysis fase overslaan. Hallo is alleen transformatie uitgevoerd op de voorwaarden van deze typen query lowercasing.

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a>Stap 3: Document ophalen 

Ophalen van het document verwijst toofinding documenten met overeenkomende voorwaarden in Hallo index. Deze fase is beste begrepen door een voorbeeld. Laten we beginnen met een index hotels met Hallo eenvoudige schema te volgen: 

~~~~
{   
    "name": "hotels",     
    "fields": [     
        { "name": "id", "type": "Edm.String", "key": true, "searchable": false },     
        { "name": "title", "type": "Edm.String", "searchable": true },     
        { "name": "description", "type": "Edm.String", "searchable": true }
    ] 
} 
~~~~

Verder wordt ervan uitgegaan dat deze index bevat Hallo vier documenten te volgen: 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance toohello beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on hello north shore of hello island of Kauaʻi. Ocean view."     
        },       
        {         
            "id": "3",         
            "title": "Playa Hotel",         
            "description": "Comfortable, air-conditioned rooms with ocean view."
        },       
        {         
            "id": "4",         
            "title": "Ocean Retreat",         
            "description": "Quiet and secluded"
        }    
    ]
}
~~~~

**Hoe voorwaarden worden geïndexeerd**

ophalen van toounderstand helpt tooknow enkele basisbeginselen van het indexeren. Hallo-eenheid voor opslag is een omgekeerde index, één voor elk doorzoekbaar veld. Is een gesorteerde lijst van alle voorwaarden van alle documenten in een omgekeerde index. Elke term maps toohello lijst van documenten waarin zich, zo duidelijk in Hallo in het volgende voorbeeld voordoet.

tooproduce hello voorwaarden in een omgekeerde index Hallo zoekmachine voert lexicale analyse over de inhoud van documenten, Hallo vergelijkbare toowhat er gebeurt tijdens het verwerken van query's. Tekst invoer worden doorgegeven tooan analyzer, geïntegreerd in een kleine, enz., afhankelijk van Hallo analyzer configuratie en leestekens verwijderd. Het algemene, maar niet vereist is, toouse Hallo dezelfde analyzers voor zoeken en indexeren operations zodat querytermen zoals voorwaarden binnen Hallo index meer uitzien.

> [!Note]
> Azure Search kunt u verschillende analyzers voor indexeren opgeven en zoek via aanvullende `indexAnalyzer` en `searchAnalyzer` veld parameters. Als u niets opgeeft, Hallo analyzer ingesteld met Hallo `analyzer` eigenschap wordt gebruikt voor het indexeren en het zoeken.  

**Omgekeerde index voor voorbeelddocumenten**

Retourneren van tooour zo kan voor Hallo **titel** veld Hallo omgekeerde index ziet er als volgt:

| Termijn | Lijst met standaarddocumenten |
|------|---------------|
| atman | 1 |
| strand | 2 |
| hotel | 1, 3 |
| Oceaan | 4  |
| playa | 3 |
| toevlucht | 3 |
| Terugtrekken | 4 |

In Hallo titelveld alleen *hotel* wordt weergegeven in twee documenten: 1, 3.

Voor Hallo **beschrijving** veld Hallo index is als volgt:

| Termijn | Lijst met standaarddocumenten |
|------|---------------|
| lucht | 3
| en | 4
| strand | 1
| voorwaarde | 3
| vertrouwd | 3
| afstand | 1
| eiland | 2
| kauaʻi | 2
| zich bevindt | 2
| Noord | 2
| Oceaan | 1, 2, 3
| van | 2
| op |2
| Stille | 4
| ruimten  | 1, 3
| secluded | 4
| wal | 2
| groot | 1
| Hallo | 1, 2
| te| 1
| weergeven | 1, 2, 3
| roulatie van | 1
| met | 3


**Overeenkomende querytermen tegen geïndexeerde voorwaarden**

Hallo omgekeerd indexen bovenstaande gegeven, gaan we terug toohello voorbeeldquery en Zie hoe overeenkomende documenten zijn gevonden voor de voorbeeldquery. Intrekken dat Hallo laatste querybewerking structuur ziet er als volgt: 

 ![Booleaanse query geanalyseerde voorwaarden][4]

Tijdens het uitvoeren van query worden afzonderlijke query's uitgevoerd met de doorzoekbare velden Hallo onafhankelijk. 

+ Hallo TermQuery 'groot' komt overeen met document 1 (Hotel Atman). 

+ Hallo PrefixQuery, ' air-condition * ', komt niet overeen met alle documenten. 

  Dit is een probleem dat soms confuses ontwikkelaars. Hoewel Hallo term air-conditioned Hallo document bevat, is deze opgesplitst in twee termen door Hallo standaard analyzer. Intrekken voorvoegsel query's die voor gedeeltelijke termen bevatten, worden niet geanalyseerd. Daarom voorwaarden met het voorvoegsel 'air-condition' worden opgezocht in Hallo omgekeerde index en niet gevonden.

+ Hallo PhraseQuery 'Oceaan weergave' Hallo voorwaarden "Oceaan" en "view" worden opgezocht en Hallo nabijheid van termen in het originele document Hallo controleert. Documenten 1, 2 en 3 overeen met deze query in Hallo beschrijvingsveld. Kennisgeving document 4 Hallo term Oceaan in Hallo titel heeft, maar wordt niet beschouwd als een overeenkomst als we op zoek bent naar Hallo "view Oceaan" woordgroep in plaats van afzonderlijke woorden. 

> [!Note]
> Een zoekopdracht wordt onafhankelijk uitgevoerd tegen de doorzoekbare velden in Azure Search-index tenzij u beperken Hallo velden ingesteld met Hallo Hallo `searchFields` parameter, zoals geïllustreerd in de zoekaanvraag Hallo-voorbeeld. Documenten die overeenkomen met een Hallo geselecteerd velden worden geretourneerd. 

Hallo-documenten die overeenkomen met zijn op Hallo hele voor Hallo query betrokken, 1, 2, 3. 

## <a name="stage-4-scoring"></a>Stap 4: score berekenen  

Elk document dat in een resultatenset search is een score relevantie toegewezen. Hallo-functie van Hallo relevantie score is toorank hoger die documenten best een gebruiker te beantwoorden vraag Hallo zoekquery uitgedrukt. Hallo-score wordt berekend op basis van statistische eigenschappen van de voorwaarden die overeenkomen met. Hallo core Hallo score berekenen voor de formule is [TF/IDF (frequentie term frequentie inverse document)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf). In de query's met zeldzame en algemene voorwaarden, bevordert TF/IDF Hallo zeldzame term met resultaten. Bijvoorbeeld in een hypothetische index met alle artikelen voor Wikipedia (Engelstalig) van de documenten die query overeenkomende hello *Hallo directeur*, documenten die overeenkomen met op *directeur* worden beschouwd als meer dan relevante documenten die overeenkomen met op *de*.


### <a name="scoring-example"></a>Score berekenen voor voorbeeld

Hallo drie documenten die overeenkomen met onze voorbeeldquery intrekken:
~~~~
search=Spacious, air-condition* +"Ocean view"  
~~~~
~~~~
{  
  "value": [
    {
      "@search.score": 0.25610128,
      "id": "1",
      "title": "Hotel Atman",
      "description": "Spacious rooms, ocean view, walking distance toohello beach."
    },
    {
      "@search.score": 0.08951007,
      "id": "3",
      "title": "Playa Hotel",
      "description": "Comfortable, air-conditioned rooms with ocean view."
    },
    {
      "@search.score": 0.05967338,
      "id": "2",
      "title": "Ocean Resort",
      "description": "Located on a cliff on hello north shore of hello island of Kauai. Ocean view."
    }
  ]
}
~~~~

1 overeenkomende Hallo query beste document omdat beide Hallo term *groot* Hallo vereist wachtwoordzin *Oceaan weergave* in Hallo beschrijvingsveld optreden. de volgende twee documenten Hallo overeen met alleen Hallo woordgroep *Oceaan weergave*. Het kan worden verrast die Hallo relevantie score voor document 2 en 3 verschilt ondanks dat ze overeenkomen met Hallo-query in Hallo dezelfde manier. Het is omdat Hallo score berekenen voor de formule meer onderdelen dan alleen TF/IDF bevat. In dit geval document 3 die een enigszins hogere score is toegewezen, omdat de beschrijving korter is. Meer informatie over [Lucene van praktische score berekenen voor de formule](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) toounderstand hoe veldlengte en andere factoren kunnen invloed hebben op Hallo relevantie score.

Sommige querytypen (jokerteken, voorvoegsel, regex) bijdragen altijd een constante score toohello totale score-document. Hierdoor komt overeen met via query uitbreiding toobe opgenomen in het Hallo-resultaten, maar zonder Hallo ranking gevonden. 

Een voorbeeld illustreert waarom dit is van belang. Zoekopdrachten met jokertekens, met inbegrip van zoekopdrachten voor voorvoegsel, zijn niet-eenduidige per definitie omdat Hallo-invoer gedeeltelijke tekenreeks met mogelijke overeenkomsten op een zeer groot aantal verschillende voorwaarden is (Houd rekening met een invoer van het "rondleiding *" met overeenkomsten gevonden op 'rondleidingen', 'tourettes', en " tourmaline'). Opgegeven Hallo aard van deze resultaten, is er geen enkele manier tooreasonably afleiden welke voorwaarden vindt u meer dan andere waardevolle. Om deze reden negeren we term frequenties wanneer resultaten scoren van typen jokerteken, voorvoegsel en regex-query's. In een meerdelig zoekaanvraag met gedeeltelijke en volledige voorwaarden, resultaten van Hallo gedeeltelijke invoer met een constante zijn ingebouwd score tooavoid afwijking naar mogelijk onverwachte resultaten.

### <a name="score-tuning"></a>Score afstemmen

Er zijn twee manieren tootune relevantie scores in Azure Search:

1. **Score berekenen voor profielen** promoveren van documenten in Hallo gerangschikte lijst met resultaten op basis van een reeks regels. In ons voorbeeld, kunnen we documenten die overeenkomen met in Hallo titelveld relevanter dan documenten die overeenkomen met in beschrijvingsveld Hallo overwegen. Bovendien kan er als onze index had een prijsveld voor elke hotel, documenten met lagere prijs promoveren. Meer informatie hoe te[score berekenen voor profielen tooa search-index toevoegen.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)
2. **Versterking** (alleen beschikbaar in de volledige Lucene-querysyntaxis Hallo) biedt een prestatieverbetering operator `^` die kunnen worden toegepast tooany deel uit van Hallo querystructuur. In ons voorbeeld, in plaats van het zoeken op voorvoegsel Hallo *air-condition*\*, een kan zoeken naar een van beide Hallo exacte termen *air-condition* Hallo voorvoegsel maar documenten die overeenkomen met op Hallo exacte term hoger door toe te passen versterking toohello term query zijn gerangschikt: *lucht voorwaarde ^ 2 || AIR-condition**. Meer informatie over [versterking](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).


### <a name="scoring-in-a-distributed-index"></a>Score berekenen voor in een gedistribueerde index

Alle indexen in Azure Search worden automatisch splitsen in meerdere shards, zodat ons tooquickly distribueren Hallo index over meerdere knooppunten tijdens service schaal omhoog of omlaag schalen. Wanneer een zoekaanvraag is uitgegeven, wordt deze onafhankelijk tegen elke shard verstrekt. Hallo worden resultaten van elke shard vervolgens samengevoegd en geordend op score (als er geen andere volgorde gedefinieerd). Het is belangrijk tooknow die Hallo scoreprofiel functie gewichten query term frequentie tegen de inverse document frequentie in alle documenten in de shard hello, niet over de breedte van alle shards.

Dit betekent dat een score relevantie *kan* zijn verschillend voor identieke documenten als ze zich op andere shards bevinden. Deze verschillen vaak gelukkig toodisappear wanneer het aantal documenten in index Hallo Hallo vanwege toomore zelfs term distributie groeit. Het is niet mogelijk tooassume op welke shard een document wordt geplaatst. Echter, ervan uitgaande dat de documentsleutel van een niet wijzigen, deze wordt altijd toegewezen toohello dezelfde shard.

Document score is in het algemeen niet aanbevolen Hallo-kenmerk voor het ordenen van documenten als stabiliteit van de volgorde belangrijk is. Bijvoorbeeld, gezien twee document met een identieke score, er is geen garantie waarvoor een eerste wordt weergegeven in latere runs Hallo dezelfde query. Document score alleen geeft een algemeen beeld van het document relevantie relatieve tooother documenten in de resultatenset Hallo.

## <a name="conclusion"></a>Conclusie

Hallo succes van zoekmachines internet heeft verwachtingen voor zoeken in volledige tekst gegenereerd via persoonlijke gegevens. Voor vrijwel elke soort zoekervaring nu naar verwachting krijgt Hallo-engine toounderstand onze bedoeling, zelfs wanneer de voorwaarden zijn getypt of zijn onvolledig. We verwachten mogelijk zelfs op basis van in de buurt vergelijkbare termen of synoniemen die we hebben nooit echt opgegeven.

Zoekopdracht in volledige tekst is van een technisch oogpunt zeer complex is of waarvoor geavanceerde analyses van de taalkundige en een tooprocessing systematisch op een manier die distill, vouw en transformeren query voorwaarden toodeliver een relevante resultaat. Opgegeven Hallo inherente complexiteit, zijn er veel factoren die van invloed kunnen zijn op Hallo uitkomst van een query. Om deze reden biedt investeren Hallo tijd toounderstand Hallo mechanisme van zoeken in volledige tekst concrete voordelen bij het toowork via onverwachte resultaten.  

In dit artikel verkend zoeken in volledige tekst in de context Hallo van Azure Search. We hopen dat dit biedt u voldoende achtergrond toorecognize mogelijke oorzaken en oplossingen voor het adresseren van veelvoorkomende problemen van de query. 

## <a name="next-steps"></a>Volgende stappen

+ Hallo voorbeeld index bouwen, uitproberen verschillende query's en resultaten bekijken. Zie voor instructies [bouwen en query uitvoeren op een index in de portal Hallo](search-get-started-portal.md#query-index).

+ Probeer extra querysyntaxis van Hallo [documenten zoeken](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) voorbeeld in deze sectie of van [vereenvoudigde querysyntaxis](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) in Search explorer in Hallo-portal.

+ Bekijk [score berekenen voor profielen](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) als u wilt dat tootune classificeren in uw zoektoepassing.

+ Meer informatie over hoe tooapply [taalspecifieke lexicale analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support).

+ [Configureren van aangepaste analyzers](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) voor minimale verwerking of speciale verwerking voor specifieke velden.

+ [Standard- en Engelse analyzers vergelijken](http://alice.unearth.ai/)) naast elkaar op deze demo-website. 

## <a name="see-also"></a>Zie ook

[REST-API documenten zoeken](https://docs.microsoft.com/rest/api/searchservice/search-documents)

[Vereenvoudigde querysyntaxis](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[Volledige Lucene-querysyntaxis](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

[Zoekresultaten verwerken](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png

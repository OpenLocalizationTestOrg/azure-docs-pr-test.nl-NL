---
title: aaaHow tooimplement meervoudige navigatie in Azure Search | Microsoft Docs
description: "Voeg facetnavigatie tooapplications die kunnen worden geïntegreerd met Azure Search, een zoekservice in de cloud gehoste op Microsoft Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: cdf98fd4-63fd-4b50-b0b0-835cb08ad4d3
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 3/10/2017
ms.author: heidist
ms.openlocfilehash: c1e6bf9dc55d0044525db79e37d35a50ded5a736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-faceted-navigation-in-azure-search"></a>Hoe tooimplement meervoudige navigatie in Azure Search
Meervoudige navigatie is een filtermechanisme waarmee zelf gerichte analyse navigatie in toepassingen. Hallo term 'facetnavigatie' niet bekend zijn, maar u hebt waarschijnlijk het eerder gebruikt. Als de Hallo volgende voorbeeld wordt getoond, is meervoudige navigatie niets meer dan Hallo categorieën gebruikt toofilter resultaten.

 ![Azure Search taak Portal-Demo][1]

Meervoudige navigatie is een alternatieve vermelding punt toosearch. Biedt een handige alternatieve tootyping complexe zoekopdracht expressies handmatig. Facetten kunt u vinden wat u zoekt, terwijl u ervoor zorgt dat er geen nul resultaten. Als een ontwikkelaar kunnen facetten u blootstellen Hallo nuttigst zoekcriteria voor uw zoekopdracht corpus navigeren. In online retail-toepassingen is vaak facetnavigatie gebouwd via merken, afdelingen (kinderen om), grootte, prijs, populariteit en classificaties. 

Implementatie van meervoudige navigatie verschilt voor elk voor zoekopdracht technologieën. In Azure Search is meervoudige navigatie op moment van de query wordt gebouwd met velden die u eerder in uw schema toegeschreven.

-   Hallo-query's die uw toepassing wordt gemaakt, een query moet verzenden *facet queryparameters* resultaatset tooget Hallo beschikbaar facet filterwaarden voor het document.

-   tooactually trim Hallo document resultatenset, Hallo toepassing moet worden toegepast een `$filter` expressie.

In uw toepassingsontwikkeling vormt schrijven van code die wordt gemaakt van query's Hallo bulksgewijs Hallo werk. Veel van het gedrag van de Hallo-toepassingen die u van meervoudige navigatie verwacht worden geleverd door het Hallo-service, inclusief ingebouwde ondersteuning voor het definiëren van de bereiken en ophalen van tellingen voor facet resultaten. Hallo-service omvat ook de praktische standaardwaarden die u helpen te voorkomen dat onhandig navigatiestructuur. 

## <a name="sample-code-and-demo"></a>Voorbeeldcode en demo
In dit artikel wordt een taak zoeken portal als voorbeeld. Hallo-voorbeeld wordt geïmplementeerd als een ASP.NET MVC-toepassing.

-   Zie en testen Hallo werkende demo online op [Azure Search taak Portal-Demo](http://azjobsdemo.azurewebsites.net/).

-   Hallo code downloaden van Hallo [Azure-Samples-opslagplaats op GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).

## <a name="get-started"></a>Aan de slag
Als u nieuwe toosearch ontwikkeling, is het beste manier toothink Hallo van meervoudige navigatie Hallo mogelijkheden voor gericht zoeken dat wordt. Het is een soort inzoomen zoekervaring, op basis van vooraf gedefinieerde filters, die worden gebruikt voor het verfijnen van snel omlaag zoekresultaten via point-and-click acties. 

### <a name="interaction-model"></a>Interactie model

Hallo zoekervaring voor meervoudige navigatie is herhaald, dus laten we eerst het als een reeks van query's die in toouser reacties uitgevouwen begrijpen.

Hallo beginpunt is een toepassingspagina waarmee facetnavigatie doorgaans op Hallo omtrek geplaatst. Meervoudige navigatie is vaak een boomstructuur met selectievakjes uit voor elke waarde of overeen. 

1. Een query verzonden tooAzure zoeken geeft Hallo facetnavigatie structuur via een of meer facet queryparameters. Bijvoorbeeld Hallo query mogelijk ook `facet=Rating`, mogelijk met een `:values` of `:sort` optie toofurther Hallo presentatie verfijnen.
2. Hallo presentatie laag geeft een zoekpagina waarmee facetnavigatie met Hallo facetten die zijn opgegeven op het Hallo-aanvraag.
3. Uitgaande van een meervoudige navigatie-structuur met de classificatie, klikt u op "4" tooindicate die alleen producten met een classificatie van 4 of hoger moeten worden weergegeven. 
4. Als antwoord verzendt toepassing hello een query met`$filter=Rating ge 4` 
5. Hallo presentatie laag updates Hallo pagina, met een verminderde resultatenset met alleen de items die voldoen aan de nieuwe criteria Hallo (in dit geval producten beoordeeld 4 en hoger).

Een facet is een queryparameter, maar niet verwarren met invoer voor de query. Dit wordt nooit gebruikt als selectiecriteria in een query. In plaats daarvan zien facet queryparameters als invoer toohello navigatiestructuur die weer in het Hallo-antwoord. Voor elke facet queryparameter die u opgeeft, evalueert Azure Search hoeveel documenten zijn in Hallo gedeeltelijke resultaten voor elke facetwaarde.

Kennisgeving Hallo `$filter` in stap 4. Hallo-filter is een belangrijk aspect van meervoudige navigatie. Hoewel de facetten en filters onafhankelijk van elkaar in Hallo API zijn, moet u beide toodeliver Hallo-ervaring die u van plan bent. 

### <a name="app-design-pattern"></a>Het ontwerppatroon App

Hallo patroon is in de toepassingscode, toouse facet query parameters tooreturn hello facetnavigatiestructuur samen met facet resultaten, plus een $filter-expressie.  Hallo filter expressie ingangen Hallo-gebeurtenis op Hallo facetwaarde geklikt. Bedenk Hallo `$filter` expressie als Hallo code achter de werkelijke bijsnijden Hallo zoekresultaten toohello presentatie laag geretourneerd. Gezien een facet kleuren, te klikken op Hallo kleur rood wordt geïmplementeerd via een `$filter` expressie die u selecteert alleen de items die een kleur van rood hebben. 

### <a name="query-basics"></a>Query-basisbeginselen

In Azure Search een aanvraag via een of meer queryparameters is opgegeven (Zie [documenten zoeken](http://msdn.microsoft.com/library/azure/dn798927.aspx) voor een beschrijving van elk criterium). Geen van de queryparameters Hallo zijn vereist, maar u moet ten minste één om een geldige query-toobe hebben.

Precisie, begrepen zoals hello mogelijkheid toofilter uit irrelevante treffers verkregen is via een van deze expressies of beide:

-   **zoeken =**  
    Hallo-waarde van deze parameter wordt verstaan onder Hallo zoekexpressie. Een los stukje van tekst of een complexe zoekopdracht-expressie met meerdere voorwaarden en operators mogelijk. Op Hallo van server, wordt een zoekexpressie gebruikt voor zoeken in volledige tekst, doorzoekbare velden in Hallo index voor die overeenkomt met de voorwaarden, retourneren resultaten in de volgorde van de waarden van positie opvragen. Als u instelt `search` toonull, queryuitvoering ligt boven de gehele index hello (dat wil zeggen, `search=*`). In this case, andere elementen van Hallo query uitvoert, zoals een `$filter` of Hallo primaire factoren die invloed hebben op welke documenten worden geretourneerd scoren van profiel zijn `($filter`) en in welke volgorde (`scoringProfile` of `$orderby`).

-   **$filter =**  
    Een filter is een krachtig mechanisme voor het beperken van de grootte van de zoekresultaten op basis van waarden van specifieke documentkenmerken Hallo Hallo. Een `$filter` wordt eerst geëvalueerd, gevolgd door de facetten logica die Hallo beschikbare waarden en bijbehorende tellingen voor elke waarde genereert

Complexe zoekopdracht expressies verminderen Hallo prestaties van query Hallo. Waar mogelijk, goed opgebouwde filter expressies tooincrease precisie gebruiken en queryprestaties verbeteren.

toobetter begrijpen hoe nauwkeuriger in een filter wordt toegevoegd, een complexe zoekopdracht expressie tooone met een filterexpressie vergelijken:

-   `GET /indexes/hotel/docs?search=lodging budget +Seattle –motel +parking`
-   `GET /indexes/hotel/docs?search=lodging&$filter=City eq ‘Seattle’ and Parking and Type ne ‘motel’`

Beide query's zijn geldig, maar Hallo tweede beter als u niet motels met parkeerplaatsen in Haarlem zoekt is.
-   de eerste query Hallo afhankelijk van deze specifieke woorden wordt vermeld of niet wordt vermeld in tekenreeksvelden zoals naam, beschrijving en andere velden die doorzoekbare gegevens.
-   Hallo tweede query zoekt nauwkeurige overeenkomsten op gestructureerde gegevens en is waarschijnlijk toobe nauwkeuriger.

In toepassingen die facetnavigatie omvatten, maar zorg ervoor dat wordt elke actie van de gebruiker over de structuur van een meervoudige navigatie vergezeld van een beperking van de zoekresultaten. toonarrow resultaten, een filterexpressie gebruiken.

<a name="howtobuildit"></a>

## <a name="build-a-faceted-navigation-app"></a>Een meervoudige navigatie-app bouwen
U implementeren meervoudige navigatie met Azure Search in uw toepassingscode die Hallo zoekaanvraag voortbouwt. Hallo facetnavigatie afhankelijk van de elementen in het schema dat u eerder hebt gedefinieerd.

Hallo vooraf gedefinieerd in uw search-index is `Facetable [true|false]` kenmerk indexeren, ingesteld op de geselecteerde velden tooenable of uitschakelen van het gebruik ervan in een meervoudige navigatie-structuur. Zonder `"Facetable" = true`, een veld in de navigatiebalk facet kan niet worden gebruikt.

Hallo presentatie laag in uw code biedt Hallo gebruikerservaring. Het beste Hallo samenstellende delen van meervoudige navigatie hello, zoals Hallo label, waarden, selectievakjes en Hallo aantal aanbieden. Hello Azure Search REST API is platform networkdirect, dus elke taal en het platform dat u wilt gebruiken. Hallo belangrijkste is dat tooinclude UI-elementen die ondersteuning bieden voor incrementele met bijgewerkte gebruikersinterfacestatus vernieuwen omdat elke extra facet is geselecteerd. 

Op het moment dat de query, maakt de toepassingscode een aanvraag met `facet=[string]`, een aanvraagparameter waarmee Hallo veld toofacet door. Een query kunt beschikt over meerdere facetten zoals `&facet=color&facet=category&facet=rating`, elkaar gescheiden door een ampersand (&)-teken.

Ook moet opgeven, toepassingscode een `$filter` expressie toohandle Hallo klikt u op de gebeurtenissen in meervoudige navigatie. Een `$filter` Hallo zoekresultaten wilt weergeven, met behulp van de facetwaarde van Hallo als filtercriteria vermindert.

Azure Search retourneert Hallo zoekresultaten, op basis van een of meer voorwaarden die u, samen met updates toohello facetnavigatie structuur invoert. In Azure Search meervoudige navigatie is één niveau gebouwd facet waarden, statistieken en hoeveel resultaten gevonden voor elk criterium.

In de Hallo uit te voeren, nemen we nader bekeken hoe toobuild elk onderdeel.

<a name="buildindex"></a>

## <a name="build-hello-index"></a>Hallo-index maken
Facetten is ingeschakeld op basis van door veld in de index Hallo via deze indexkenmerk: `"Facetable": true`.  
Alle veldtypen die mogelijk kunnen worden gebruikt in facetnavigatie `Facetable` standaard. Dergelijke veldtypen omvatten `Edm.String`, `Edm.DateTimeOffset`, en alle numerieke veldtypen Hallo (in wezen alle veldtypen zijn geschikt voor facetten behalve `Edm.GeographyPoint`, die niet worden gebruikt in facetnavigatie). 

Als u een index maakt, is een aanbevolen procedure voor meervoudige navigatie tooexplicitly Schakel facetten voor velden die nooit mogen worden gebruikt als een facet uitgeschakeld.  In het bijzonder tekenreeksvelden voor singleton-waarden, zoals een naam-ID of het product te moeten worden ingesteld`"Facetable": false` tooprevent hun onbedoeld (en ongeschikt) in meervoudige navigatie gebruiken. Schakelen facetten uitschakelen wanneer u deze niet nodig bijdraagt aan de grootte van Hallo index Hallo klein en meestal verbetert de prestaties.

Volgende maakt deel uit van het Hallo-schema voor Hallo taak Portal-Demo voorbeeld-app afgekapte van enkele kenmerken tooreduce Hallo grootte:

```json
{
  ...
  "name": "nycjobs",
  "fields": [
    { “name”: "id",                 "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "job_id",             "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "agency",              "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "posting_type",        "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "num_of_positions",    "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "business_title",      "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "civil_service_title", "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "title_code_no",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "level",               "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_from",   "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_to",     "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_frequency",    "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "work_location",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
…
    { “name”: "geo_location",        "type": "Edm.GeographyPoint",     "searchable": false, "filterable": true, ...  "facetable": false, ... },
    { “name”: "tags",                "type": "Collection(Edm.String)", "searchable": true,  "filterable": true, ...  "facetable": true, ...  }
  ],
…
}
```

Zoals u in de voorbeeld-schema Hallo ziet `Facetable` is uitgeschakeld voor tekenreeksvelden als facetten, zoals id-waarden mag niet worden gebruikt. Schakelen facetten uitschakelen wanneer u deze niet nodig bijdraagt aan de grootte van Hallo index Hallo klein en meestal verbetert de prestaties.

> [!TIP]
> Als een best practice bevatten Hallo volledige set indexkenmerken voor elk veld. Hoewel `Facetable` is standaard ingeschakeld voor bijna alle velden, opzettelijk instelling elk kenmerk kunt u denkt dat via Hallo implicaties van elke beslissing schema. 

<a name="checkdata"></a>

## <a name="check-hello-data"></a>Hallo gegevens controleren
Hallo kwaliteit van uw gegevens heeft een directe invloed op of Hallo facetnavigatie structuur gebeurtenis zich voordoet dan u verwacht. Het is ook van invloed op Hallo gebruiksgemak filters tooreduce Hallo resultatenset construeren.

Als u toofacet door merk of prijs wilt, elk document moet waarden bevatten voor *BrandName* en *ProductPrice* die geldig, consistente en productief zijn als een filteroptie zijn.

Hier volgen enkele herinneringen van welke tooscrub voor:

* Voor elk veld dat u wilt dat toofacet door, afvragen of deze bevat waarden die geschikt is als filters in zelf gerichte zoeken. Hallo-waarden moet korte, beschrijvende en voldoende onderscheidende toooffer een duidelijke keuze tussen concurrerende opties.
* De spelling of bijna overeenkomende waarden. Als u facet op kleur en veldwaarden oranje en Ornage (onjuist gespeld) omvatten, maar een facet op basis van Hallo kleurveld zou kunnen worden opgepikt beide.
* Gemengde case tekst kan ook aanrichten functies in facetnavigatie met oranje en oranje verschijnen als twee verschillende waarden. 
* Enkelvoudige en meervoudige versies van dezelfde waarde in een afzonderlijke facet voor elk resulteren kan Hallo.

Als u zich kunt voorstellen is zorgvuldigheid Hallo gegevens voorbereiden een essentieel aspect van effectieve meervoudige navigatie.

<a name="presentationlayer"></a>

## <a name="build-hello-ui"></a>Hallo gebruikersinterface bouwen
Werkt terug uit Hallo presentatie laag kunt u vereisten die mogelijk anders worden overgeslagen en begrijpen welke mogelijkheden zijn essentieel toohello onthullen help zoeken ervaring.

Invoer van de gebruiker op de pagina Hallo detecteert en Hallo gewijzigd elementen invoegt in termen van meervoudige navigatie uw web- of -pagina geeft Hallo facetnavigatie structuur. 

Voor webtoepassingen, wordt AJAX meestal gebruikt in Hallo presentatie laag omdat hiermee toorefresh incrementele wijzigingen. U kunt ook ASP.NET MVC- of een andere visualisatie-platform die tooan Azure Search-service via HTTP verbinden kan. Hallo-voorbeeldtoepassing waarnaar wordt verwezen in dit artikel--hello **Azure Search taak Portal-Demo** – gebeurt toobe een ASP.NET MVC-toepassing.

In voorbeeld Hallo is meervoudige navigatie ingebouwd in Hallo zoekresultatenpagina. Hallo volgende voorbeeld, die afkomstig zijn uit Hallo `index.cshtml` resultatenpagina-bestand van de voorbeeldtoepassing hello, toont Hallo statische HTML-structuur voor het weergeven van meervoudige navigatie op Hallo zoeken. Hallo-lijst met facetten is gebouwd of dynamisch opnieuw opbouwen wanneer u een zoekterm of schakelt u uit een beperkingsfacet.

```html
<div class="widget sidebar-widget jobs-filter-widget">
  <h5 class="widget-title">Filter Results</h5>
    <p id="filterReset"></p>
    <div class="widget-content">

      <h6 id="businessTitleFacetTitle">Business Title</h6>
      <ul class="filter-list" id="business_title_facets">
      </ul>

      <h6>Location</h6>
      <ul class="filter-list" id="posting_type_facets">
      </ul>

      <h6>Posting Type</h6>
      <ul class="filter-list" id="posting_type_facets"></ul>

      <h6>Minimum Salary</h6>
      <ul class="filter-list" id="salary_range_facets">
      </ul>

  </div>
</div>
```

Hallo volgende codefragment uit Hallo `index.cshtml` pagina dynamisch Hallo HTML toodisplay Hallo eerste facet, zakelijke titel. Hallo HTML voor Hallo samenstellen soortgelijke functies dynamisch andere facetten. Elke facet heeft een label en een telling waarin het aantal items gevonden voor die resulteren facet Hallo.

```js
function UpdateBusinessTitleFacets(data) {
  var facetResultsHTML = '';
  for (var i = 0; i < data.length; i++) {
    facetResultsHTML += '<li><a href="javascript:void(0)" onclick="ChooseBusinessTitleFacet(\'' + data[i].Value + '\');">' + data[i].Value + ' (' + data[i].Count + ')</span></a></li>';
  }

  $("#business_title_facets").html(facetResultsHTML);
}
```

> [!TIP]
> Bij het ontwerpen van de zoekresultatenpagina Hallo onthouden tooadd een mechanisme voor het wissen van facetten. Als u selectievakjes toevoegt, kunt u eenvoudig zien hoe tooclear Hallo filtert. Voor andere indelingen moet u mogelijk een patroon breadcrumb of een andere creative benadering. Bijvoorbeeld in Hallo voorbeeldtoepassing taak zoeken Portal, kunt u Hallo `[X]` na een geselecteerde facet tooclear Hallo-beperkingsfacet.

<a name="buildquery"></a>

## <a name="build-hello-query"></a>Hallo query opbouwen
Hallo-code die u voor het bouwen van query's schrijven moet opgeven, alle onderdelen van een geldige query, zoals zoeken expressies, facetten, filters, score berekenen profielen – iets tooformulate een aanvraag gebruikt. In deze sectie besproken waar facetten past in een query en hoe filters worden gebruikt met facetten toodeliver een verminderde resultaatset.

U ziet dat facetten integraal in deze voorbeeldtoepassing. Hallo zoekfunctie in Hallo taak Portal-Demo is ontworpen om meervoudige navigatie en filters. Hallo opvallende plaatsing van meervoudige navigatie op Hallo pagina ziet u het belang. 

Een voorbeeld is vaak een goede plaats toobegin. Hallo volgende voorbeeld, die afkomstig zijn uit Hallo `JobsSearch.cs` builds die een aanvraag die facet navigatie worden gemaakt op basis van functie, locatie, soort boeken en minimale salaris-bestand. 

```cs
SearchParameters sp = new SearchParameters()
{
  ...
  // Add facets
  Facets = new List<String>() { "business_title", "posting_type", "level", "salary_range_from,interval:50000" },
};
```

Een queryparameter facet tooa veld is ingesteld en afhankelijk van het Hallo-gegevenstype, kunnen worden verder als parameters gebruikt door komma's gescheiden lijst met `count:<integer>`, `sort:<>`, `interval:<integer>`, en `values:<list>`. Een lijst met waarden wordt ondersteund voor numerieke gegevens bij het instellen van bereiken. Zie [documenten zoeken (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) voor informatie over het gebruik.

Hallo-aanvraag geformuleerd door uw toepassing samen met de facetten, moet ook filters toonarrow omlaag Hallo set candidate documenten op basis van een waarde facet selectie maken. Voor een winkel fiets facetnavigatie biedt aanwijzingen tooquestions zoals *welke kleuren, fabrikanten en typen bikes beschikbaar zijn?*. Filteren van antwoorden op vragen zoals *mountainbikes, welke exacte bikes rood zijn, in dit bereik te prijs?*. Wanneer u "Red" tooindicate die alleen rode producten moeten worden weergegeven, klikt u op volgende query Hallo-toepassing hello verzendt bevat `$filter=Color eq ‘Red’`.

Hallo volgende codefragment uit Hallo `JobsSearch.cs` pagina wordt geselecteerd Hallo Business titel toohello filter toegevoegd als u een waarde van Hallo Business titel facet selecteren.

```cs
if (businessTitleFacet != "")
  filter = "business_title eq '" + businessTitleFacet + "'";
```

<a name="tips"></a> 

## <a name="tips-and-best-practices"></a>Tips en best practices

### <a name="indexing-tips"></a>Tips indexeren
**Index-efficiëntie te verbeteren, als u een zoekvak niet gebruikt**

Als uw toepassing gebruikmaakt van meervoudige navigatie uitsluitend (dat wil zeggen, geen zoekvak), kunt u Hallo veld als markeren `searchable=false`, `facetable=true` tooproduce een compacter index. Bovendien indexeren doet zich alleen op de hele facet waarden, met geen woordafbreking of indexeren van Hallo-onderdelen van een waarde met meerdere woord.

**Opgeven welke velden kunnen worden gebruikt als facetten**

Intrekken van die Hallo schema van Hallo index bepaalt welke velden beschikbaar toouse als een beperkingsfacet. Uitgaande van dat een veld is geschikt voor facetten geeft Hallo query aan welke velden toofacet door. Hallo-veld waarop u facetten zijn biedt Hallo-waarden die worden weergegeven onder Hallo label. 

Hallo-waarden die worden vermeld onder elk label worden opgehaald uit het Hallo-index. Bijvoorbeeld, als hello facet veld is *kleur*, Hallo waarden beschikbaar voor het filteren van aanvullende zijn Hallo waarden voor dat veld - rood en zwart.

Voor numerieke en datum-/ alleen waarden, kunt u waarden expliciet instellen op Hallo facet veld (bijvoorbeeld `facet=Rating,values:1|2|3|4|5`). Een lijst met waarden is toegestaan voor deze veld typen toosimplify Hallo scheiding van facet resultaten in aaneengesloten bereiken (ofwel bereiken op basis van numerieke waarden of perioden). 

**Standaard kunt u slechts één niveau van meervoudige navigatie hebt** 

Zoals is aangegeven, is er geen rechtstreekse ondersteuning voor het nesten van facetten in een hiërarchie. Standaard ondersteunt meervoudige navigatie in Azure Search slechts één niveau van filters. Tijdelijke oplossingen echter bestaan. U kunt coderen een facet hiërarchische structuur in een `Collection(Edm.String)` verwijzen met één vermelding per hiërarchie. Deze oplossing implementeren valt buiten bereik Hallo van dit artikel. 

### <a name="querying-tips"></a>Tips opvragen
**Velden valideren**

Als u Hallo lijst met facetten dynamisch op basis van niet-vertrouwde gebruikersinvoer bouwt, controleert u het Hallo-namen van Hallo meervoudige velden zijn geldig. Of escape Hallo namen tijdens het bouwen van URL's met behulp van `Uri.EscapeDataString()` in .NET of Hallo equivalent in uw favoriete platform.

### <a name="filtering-tips"></a>Tips voor het filteren
**De precisie van de zoekopdracht verhogen met filters**

Filters gebruiken. Als u zich baseert op net zoeken expressies alleen gegevens als gevolg kan leiden tot een document toobe heeft geretourneerd dat geen nauwkeurige facetwaarde van Hallo in een van de velden.

**Het verhogen van de prestaties van de zoekopdracht met filters**

Filters beperken Hallo set candidate documenten voor zoeken en ranking uitsluiten. Als er een groot aantal documenten, kunt met behulp van een selectief beperkingsfacet inzoomen vaak u betere prestaties.
  
**Alleen Hallo meervoudige velden filteren**

In meervoudige inzoomen, wilt u doorgaans tooonly documenten met Hallo facetwaarde in een specifieke (beperkt) veld niet overal in de doorzoekbare velden opnemen. Een filter toe te voegen versterkt Hallo doelveld door Hallo service toosearch Hallo meervoudige veld naar een overeenkomende waarde.

**Trim facet resultaten met meer filters**

Facet resultaten worden gevonden in de zoekresultaten Hallo die overeenkomen met een term facet documenten. In het volgende voorbeeld wordt in de zoekresultaten voor Hallo *cloudcomputing*, 254 items hebben ook *interne specificatie* als een inhoudstype. Items zijn niet noodzakelijkerwijs sluiten elkaar wederzijds uit. Als een item voldoet aan de criteria Hallo van beide filters, wordt het beschouwd in elk criterium. Deze duplicaten is mogelijk wanneer facetten op `Collection(Edm.String)` velden, welke vaak gebruikt tooimplement document labels.

        Search term: "cloud computing"
        Content type
           Internal specification (254)
           Video (10) 

In het algemeen als u vindt dat facet resultaten consistent is te groot, is het raadzaam dat u toevoegt, meer filters toogive gebruikers meer opties voor het Hallo-zoekopdracht te verfijnen.

### <a name="tips-about-result-count"></a>Tips voor het aantal resultaten

**Hallo aantal items in de Hallo facet navigatie beperken**

Er is een standaardlimiet van 10 waarden voor elk meervoudige veld in de navigatiestructuur Hallo. Deze standaardinstelling zinvolle voor navigatiestructuur omdat Hallo waarden beheerbare lijstgrootte tooa blijven. U kunt Hallo standaardinstelling negeren door een waarde toocount toewijzen.

* `&facet=city,count:5`Hiermee geeft u op dat alleen Hallo eerste vijf steden gevonden in Hallo boven gerangschikt resultaten worden geretourneerd als gevolg hiervan facet. U kunt een voorbeeldquery met een zoekterm van 'luchthaven' en 32 overeenkomsten. Als het Hallo-query is `&facet=city,count:5`, alleen de eerste vijf unieke steden Hallo Hello meeste documenten in de zoekresultaten Hallo zijn opgenomen in Hallo facet resultaten.

Kennisgeving Hallo onderscheid tussen facet resultaten en zoekresultaten. Zoekresultaten zijn alle Hallo-documenten die overeenkomen met Hallo-query. Facet resultaten zijn Hallo overeenkomt met voor elke facetwaarde. In voorbeeld hello bevatten de zoekresultaten stad namen die zich niet in Hallo facet classificatie lijst (5 in ons voorbeeld). De resultaten worden gefilterd via facetnavigatie zichtbaar wanneer u facetten wissen, of kies andere facetten naast plaats. 

> [!NOTE]
> Bespreken `count` wanneer er meer dan één type kan verwarrend zijn. Hallo biedt volgende tabel een kort overzicht van hoe Hallo term wordt gebruikt in Azure Search API, voorbeeldcode en documentatie. 

* `@colorFacet.count`<br/>
  In de presentatiecode ziet u een parameter van het aantal op Hallo facet, gebruikte toodisplay Hallo aantal facet resultaten. Aantal wijst facet resultaten Hallo aantal documenten die overeenkomen met op Hallo facet term of -bereik.
* `&facet=City,count:12`<br/>
  U kunt in een query facet tooa waarde instellen.  Hallo standaardwaarde is 10, maar u kunt deze hogere of lagere instellen. Instelling `count:12` opgehaald Hallo bovenste 12-overeenkomsten in facet resultaten door het aantal documenten.
* "`@odata.count`"<br/>
  Hallo query-antwoord wordt geeft deze waarde het aantal overeenkomende items in de zoekresultaten Hallo Hallo. Gemiddeld het groter is dan Hallo som van alle facet resultaten gecombineerd vanwege toohello aanwezigheid van items die overeenkomen met de zoekterm hello, maar hebben geen waarde facet overeenkomsten.

**Telt het aantal in facet resultaten ophalen**

Wanneer u een filter tooa meervoudige query toevoegt, kunt u tooretain Hallo facet instructie (bijvoorbeeld `facet=Rating&$filter=Rating ge 4`). Technisch gezien facet = waardering is niet nodig, maar deze te houden Hallo tellingen van facet waarden voor de classificaties retourneert 4 en hoger. Als u op "4" en Hallo query bevat bijvoorbeeld een filter voor groter of gelijk te '4', aantallen worden geretourneerd voor elke classificatie is 4 en hoger.  

**Zorg ervoor dat u nauwkeurige facet aantallen ophalen**

Onder bepaalde omstandigheden, ziet u wellicht facet aantallen komen niet overeen met de resultatensets hello (Zie [facetnavigatie in Azure Search (forum post)](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch)).

Facet tellingen kunnen onnauwkeurig zijn vanwege toohello sharding-architectuur. Elke search-index heeft meerdere shards en elke shard rapporteert Hallo bovenste N facetten door het aantal documenten, die vervolgens worden gecombineerd tot een enkelvoudig resultaat wordt verkregen. Als sommige shards veel overeenkomende waarden, hebt terwijl anderen minder hebben, merkt u dat sommige waarden facet ontbreken of onder-telling in Hallo resultaten.

Hoewel dit gedrag op elk gewenst moment wijzigen kan als u vandaag de dag dit probleem ondervindt, kunt u omzeilen deze door kunstmatig verversen Hallo-aantal:<number> tooa groot aantal tooenforce volledige rapportages van elke shard. Als waarde van het aantal Hallo: is groter dan of gelijk toohello getal met unieke waarden in het veld Hallo u nauwkeurige resultaten gegarandeerd. Echter, wanneer het aantal documenten, wat hoog zijn, er is een prestatiestraf, dus zorgvuldig gebruik deze optie.

### <a name="user-interface-tips"></a>Tips voor gebruiker-interface
**Labels voor elk veld in de navigatiebalk facet toevoegen**

Labels worden gewoonlijk gedefinieerd in Hallo HTML of formulier (`index.cshtml` in de voorbeeldtoepassing Hallo). Er is geen API in Azure Search voor facet navigatielabels of andere metagegevens.

<a name="rangefacets"></a>

## <a name="filter-based-on-a-range"></a>Filteren op basis van een bereik
Facetten via bereiken met waarden is een algemene zoekopdracht toepassing vereiste. Bereiken worden ondersteund voor numerieke gegevens en DateTime-waarden. Meer informatie over elke methode in [documenten zoeken (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx).

Azure Search vereenvoudigt bereik constructie dankzij de twee methoden voor het berekenen van een bereik. Voor beide benaderingen maakt Azure Search Hallo juiste bereiken opgegeven Hallo invoerwaarden die u hebt opgegeven. Bijvoorbeeld, als u de waarden van 10 opgeeft | 20 | 30, wordt kan bereiken van 0-10, 10-20, 20-30 automatisch gemaakt. Uw toepassing kunt desgewenst verwijderen voor de tijdstippen die leeg zijn. 

**Methode 1: Hallo interval parameter gebruiken**  
tooset prijs facetten in $10 stappen, geeft u op:`&facet=price,interval:10`

**Methode 2: Een lijst met waarden gebruiken**  
U kunt een lijst met waarden gebruiken voor numerieke gegevens.  Houd rekening met Hallo facet bereik voor een `listPrice` veld als volgt weergegeven:

  ![Lijst met waarden van voorbeeld][5]

toospecify een facet bereik, zoals Hallo in Hallo voorgaande schermopname, gebruikt u een lijst met waarden:

    facet=listPrice,values:10|25|100|500|1000|2500

Elk bereik is 0 als uitgangspunt, een waarde uit de lijst Hallo als een eindpunt gebruikt en vervolgens afgekapte Hallo vorige bereik toocreate discrete intervallen gebouwd. Azure Search biedt deze dingen als onderdeel van meervoudige navigatie. U hoeft geen toowrite code voor het structureren van elk interval.

### <a name="build-a-filter-for-a-range"></a>Een filter voor een bereik bouwen
toofilter documenten op basis van een bereik dat u selecteert, kunt u Hallo `"ge"` en `"lt"` operators in een tweedelige-expressie die Hallo eindpunten van Hallo bereik definieert filteren. Bijvoorbeeld, als u ervoor kiest Hallo bereik 10-25 voor een `listPrice` veld Hallo-filter is `$filter=listPrice ge 10 and listPrice lt 25`. In de voorbeeldcode Hallo Hallo filterexpressie gebruikt **priceFrom** en **priceTo** parameters tooset Hallo eindpunten. 

  ![Query voor een bereik van waarden][6]

<a name="geofacets"></a> 

## <a name="filter-based-on-distance"></a>Filter gebaseerd op afstand
De algemene toosee filters waarmee u een winkel, een restaurant of een bestemming op basis van de huidige locatie van nabijheid tooyour kiezen. Hoewel dit type filter als facetnavigatie eruitzien kan, is alleen een filter. We vermeld hier voor mensen die specifiek implementatie advies voor het probleem bepaald ontwerp zoekt.

Er zijn twee georuimtelijke functies in Azure Search **geo.distance** en **geo.intersects**.

* Hallo **geo.distance** functie retourneert Hallo afstand in kilometer tussen twee punten. Één punt is een veld en andere een constante doorgegeven als onderdeel van het Hallo-filter. 
* Hallo **geo.intersects** functie retourneert true als er een opgegeven punt zich binnen een bepaalde veelhoek. Hallo-punt is een veld en Hallo veelhoek is opgegeven als een constante lijst coördinaten doorgegeven als onderdeel van het Hallo-filter.

Vindt u voorbeelden van filter in [OData-expressiesyntaxis (Azure Search)](http://msdn.microsoft.com/library/azure/dn798921.aspx).

<a name="tryitout"></a>

## <a name="try-hello-demo"></a>Probeer het Hallo-demo
Hello Azure Search taak Portal-Demo bevat Hallo voorbeelden waarnaar wordt verwezen in dit artikel.

-   Zie en testen Hallo werkende demo online op [Azure Search taak Portal-Demo](http://azjobsdemo.azurewebsites.net/).

-   Hallo code downloaden van Hallo [Azure-Samples-opslagplaats op GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).

Als u met zoekresultaten werkt, bekijk Hallo-URL voor wijzigingen in het samenstellen van query. Deze toepassing gebeurt tooappend facetten toohello URI terwijl u elk item selecteert.

1. toouse hello toewijzing functionaliteit van Hallo demo-app, u een Bing Maps-sleutel van Hallo [Bing Maps Dev Center](https://www.bingmapsportal.com/). Plak deze via de bestaande sleutel Hallo in Hallo `index.cshtml` pagina. Hallo `BingApiKey` instellen in Hallo `Web.config` -bestand wordt niet gebruikt. 

2. Hallo-toepassing uitvoeren. Hallo-optioneel rondleiding of Hallo dialoogvenster sluiten.
   
3. Geef een zoekterm, zoals 'analist', en klik op het zoekpictogram Hallo. Hallo-query snel wordt uitgevoerd.
   
   De structuur van een meervoudige navigatie wordt ook geretourneerd met Hallo zoekresultaten. In de pagina met zoekresultaten Hallo omvat Hallo facetnavigatie structuur tellingen voor elk resultaat facet. Er is geen facetten zijn geselecteerd, zodat alle overeenkomende resultaten worden geretourneerd.
   
   ![Zoekresultaten voordat u selecteert facetten][11]

4. Klik op een functie, de locatie of de minimale salaris. Facetten zijn null op Hallo zoekt, maar als deze waarden ondernemen, Hallo zoekresultaten zijn afgekapt tot van items die niet langer overeenkomen met.
   
   ![Zoekresultaten na het selecteren van facetten][12]

5. tooclear hello meervoudige query zodat u kunt andere query gedrag, klikt u op Hallo `[X]` nadat Hallo facetten tooclear Hallo facetten geselecteerd.
   
<a name="nextstep"></a>

## <a name="learn-more"></a>Meer informatie
Bekijk [Azure Search diepgaand](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410). 45:25, er is een demo voor het tooimplement facetten.

Voor meer informatie over ontwerp beginselen voor meervoudige navigatie wordt aangeraden Hallo koppelingen te volgen:

* [Ontwerpen voor meervoudige zoeken](http://www.uie.com/articles/faceted_search/)
* [Ontwerppatronen: Meervoudige navigatie](http://alistapart.com/article/design-patterns-faceted-navigation)


<!--Anchors-->
[How toobuild it]: #howtobuildit
[Build hello presentation layer]: #presentationlayer
[Build hello index]: #buildindex
[Check for data quality]: #checkdata
[Build hello query]: #buildquery
[Tips on how toocontrol faceted navigation]: #tips
[Faceted navigation based on range values]: #rangefacets
[Faceted navigation based on GeoPoints]: #geofacets
[Try it out]: #tryitout

<!--Image references-->
[1]: ./media/search-faceted-navigation/azure-search-faceting-example.PNG
[2]: ./media/search-faceted-navigation/Facet-2-CSHTML.PNG
[3]: ./media/search-faceted-navigation/Facet-3-schema.PNG
[4]: ./media/search-faceted-navigation/Facet-4-SearchMethod.PNG
[5]: ./media/search-faceted-navigation/Facet-5-Prices.PNG
[6]: ./media/search-faceted-navigation/Facet-6-buildfilter.PNG
[7]: ./media/search-faceted-navigation/Facet-7-appstart.png
[8]: ./media/search-faceted-navigation/Facet-8-appbike.png
[9]: ./media/search-faceted-navigation/Facet-9-appbikefaceted.png
[10]: ./media/search-faceted-navigation/Facet-10-appTitle.png
[11]: ./media/search-faceted-navigation/faceted-search-before-facets.png
[12]: ./media/search-faceted-navigation/faceted-search-after-facets.png

<!--Link references-->
[Designing for Faceted Search]: http://www.uie.com/articles/faceted_search/
[Design Patterns: Faceted Navigation]: http://alistapart.com/article/design-patterns-faceted-navigation
[Create your first application]: search-create-first-solution.md
[OData expression syntax (Azure Search)]: http://msdn.microsoft.com/library/azure/dn798921.aspx
[Azure Search Adventure Works Demo]: https://azuresearchadventureworksdemo.codeplex.com/
[http://www.odata.org/documentation/odata-version-2-0/overview/]: http://www.odata.org/documentation/odata-version-2-0/overview/ 
[Faceting on Azure Search forum post]: ../faceting-on-azure-search.md?forum=azuresearch
[Search Documents (Azure Search API)]: http://msdn.microsoft.com/library/azure/dn798927.aspx


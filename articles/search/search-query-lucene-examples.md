---
title: Voorbeelden van query aaaLucene voor Azure Search | Microsoft Docs
description: Lucene-querysyntaxis voor fuzzy zoeken, zoeken bij benadering, term versterking, zoeken op reguliere expressies en zoeken met jokertekens.
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: Lucene query analyzer syntax
ms.assetid: 147f360d-a5ce-4d7b-a909-c8b65bfb748c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: liamca
ms.openlocfilehash: d859cf697ef9485a49e9e0591b68e812ffa55f1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="lucene-query-syntax-examples-for-building-queries-in-azure-search"></a>Lucene query syntaxisvoorbeelden voor het bouwen van query's in Azure Search
Bij het maken van query's voor Azure Search, kunt u de standaard Hallo [vereenvoudigde querysyntaxis](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) of Hallo alternatieve [Lucene Queryparser in Azure Search](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search). Hallo Lucene Queryparser ondersteunt een complexere query-constructs, zoals veldgerelateerde query's, fuzzy zoeken, zoeken bij benadering, term versterking en zoeken op reguliere expressies.

In dit artikel kunt u stapsgewijs door voorbeelden demonstreren querybewerkingen beschikbaar wanneer u de volledige syntaxis Hallo.

## <a name="viewing-hello-examples-in-jsfiddle"></a>U bekijkt hello voorbeelden in JSFiddle

Alle voorbeelden in dit artikel Hallo uitvoerbare query's uitvoeren op een vooraf geladen Search-index in zijn [JSFiddle](https://jsfiddle.net), een online code-editor voor het testen van scripts en HTML. 

toorun, met de rechtermuisknop op Hallo query voorbeeld-URL's tooopen JSFiddle in een apart browservenster.

> [!NOTE]
> Hallo volgende voorbeelden gebruikmaken van een zoekindex die bestaat uit functies die beschikbaar zijn op basis van een gegevensset die is geleverd door Hallo [stad New York OpenData](https://nycopendata.socrata.com/) initiatief. Deze gegevens moet niet worden beschouwd als huidige of voltooid. Hallo-index is op een sandbox-service van Microsoft. U hoeft niet een Azure-abonnement of een Azure Search tootry deze query's.
>


## <a name="how-tooinvoke-full-lucene-parsing"></a>Hoe tooinvoke volledige Lucene parseren

Alle voorbeelden in dit artikel Hallo Hallo opgeven **queryType = full** parameter, die aangeeft dat de volledige syntaxis van die hello, verwerkt door Hallo Lucene Queryparser zoeken. 

**Voorbeeld 1** --met de rechtermuisknop op Hallo na query codefragment tooopen in de browser van een nieuwe pagina die wordt geladen JSFiddle en wordt uitgevoerd Hallo query:

* [& queryType volledige = & zoeken = *](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*)

In een nieuw browservenster hello, wordt Hallo JavaScript-bron- en HTML-uitvoer weergegeven naast elkaar. Hallo script verwijst naar een volledige query (niet alleen Hallo codefragment, zoals wordt weergegeven in het Hallo-koppeling). Hallo volledige query wordt weergegeven in het Hallo-URL's voor elk voorbeeld. 

Deze query retourneert documenten uit onze index New York City-taken (nycjobs, op een sandboxservice geladen). Hallo query geeft alleen zakelijke titels worden geretourneerd voor beknopt alternatief bevat. Hallo volledige onderliggende query is als volgt:

    http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*

Hallo **searchFields** parameter Hallo toojust Hallo business titel zoekveld beperkt. Hallo **queryType** te is ingesteld,**volledige**, die Hiermee geeft u Azure Search toouse hello Lucene Queryparser voor deze query.

> [!NOTE]
> Zie voor achtergrondinformatie over de verwerking van query's, [hoe volledige tekst zoeken werkt in Azure Search](search-lucene-query-architecture.md). Zie voor meer informatie over zoekparameters [documenten zoeken (Azure Search Service REST-API)](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).
>

### <a name="fielded-query-operation"></a>Fielded querybewerking
U kunt Hallo voorbeelden in dit artikel wijzigen door op te geven een **fieldname:searchterm** bouw toodefine fielded querybewerking, waarbij Hallo-veld is één woord en Hallo zoekterm is ook een woord of woordgroep, eventueel met Booleaanse operators. Enkele voorbeelden zijn Hallo volgende:

* business_title:(senior NOT junior)
* status: ("Den Haag ' en"Nieuwe Jersey")

Niet zeker tooput meerdere tekenreeksen binnen de aanhalingstekens zijn als u wilt dat beide tekenreeksen toobe geëvalueerd als één entiteit, zoals in dit geval zoekt naar twee verschillende plaatsen in het veld locatie Hallo. Zorg er ook voor Hallo operator een hoofdletter is als u niet ziet en AND.

Hallo-veld opgegeven in de **fieldname:searchterm** moet een doorzoekbaar veld. Zie [Create Index (Azure Search Service REST-API)](https://docs.microsoft.com/rest/api/searchservice/create-index) voor meer informatie over hoe indexkenmerken in velddefinities worden gebruikt.

**Voorbeeld 2** --met de rechtermuisknop op Hallo volgende query codefragment deze query zoekt naar zakelijke titels Hello benaming senior bevat, maar niet beginnend:

* [& queryType volledige = & zoeken = business_title:senior niet beginnend](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:senior+NOT+junior)

## <a name="fuzzy-search-example"></a>Voorbeeld van fuzzy zoeken
Een fuzzy zoeken overeenkomsten worden gevonden in de termen die vergelijkbaar gebouwd zijn. Per [Lucene documentatie](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html), fuzzy zoekopdrachten zijn gebaseerd op [Damerau Levenshtein afstand](https://en.wikipedia.org/wiki/Damerau%e2%80%93Levenshtein_distance).

toodo een fuzzy zoeken toevoegen Hallo tilde ' ~ ' symbool aan Hallo einde van één woord met een optionele parameter, een waarde tussen 0 en 2, waarmee Hallo bewerken afstand. Bijvoorbeeld ' blue ~ ' of ' blue ~ 1" zou retourneren blauw, blauwe en lijm.

**Voorbeeld 3** --met de rechtermuisknop op Hallo volgende query codefragment. Deze query zoekt naar taken met Hallo term koppelen (waar het is verkeerd gespeld):

* [& queryType volledige = & zoeken = business_title:asosiate ~](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:asosiate~)

> [!Note]
> Fuzzy query's zijn niet [geanalyseerd](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis), wat verrassend als u verwacht als gevolg of Lemmata dat kan zijn. Lexicale analyse wordt alleen uitgevoerd op de volledige (een term query of woordgroep query). Querytypen met onvolledige voorwaarden (voorvoegsel query, jokertekens query, regex query, fuzzy query) worden toegevoegd rechtstreeks toohello querystructuur Hallo analysis fase overslaan. Hallo is alleen transformatie uitgevoerd op onvolledige querytermen lowercasing.
>

## <a name="proximity-search-example"></a>Voorbeeld van nabijheid zoeken
Nabijheid zoekopdrachten zijn gebruikte toofind voorwaarden die zich dicht bij elkaar in een document. Invoegen van een tilde ' ~ ' symbool aan Hallo einde van een wachtwoordzin gevolgd door Hallo aantal woorden die Hallo nabijheid grens maken. Bijvoorbeeld 'hotel luchthaven' ~ 5 zoeken Hallo voorwaarden hotel en luchthaven binnen 5 woorden van elkaar in een document.

**Voorbeeld 4** --met de rechtermuisknop op Hallo query. Zoeken naar taken met Hallo term 'senior analist' waarin deze worden gescheiden door niet meer dan één woord:

* [& queryType volledige = & zoeken = business_title: 'senior analist' ~ 1](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~1)

**Voorbeeld 5** --probeer het opnieuw Hallo woorden tussen Hallo term "senior analist" verwijderen.

* [& queryType volledige = & zoeken = business_title: 'senior analist' ~ 0](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~0)

## <a name="term-boosting-examples"></a>Term versterking van voorbeelden
Term versterking verwijst tooranking een document hoger als het Hallo bevat boosted termijn, relatieve toodocuments die geen Hallo term bevatten. Dit verschilt van de score berekenen voor profielen in de betreffende scoreprofiel profielen bepaalde velden in plaats van door specifieke termen verbeteren. Hallo volgende voorbeeld helpt illustreren Hallo verschillen.

U kunt een scoreprofiel die verhoogt, zoals in een bepaalde veld overeenkomt met **genre** in Hallo musicstoreindex voorbeeld. Term versterking mogelijk gebruikte toofurther versterking bepaalde zoeken hoger dan de andere voorwaarden. Bijvoorbeeld ' steen ^ 2 elektronische ' documenten met Hallo zoektermen in hello wordt verhogen **genre** veld hoger is dan andere doorzoekbare velden in Hallo index. Bovendien wordt documenten met zoekterm Hallo 'uit' gerangschikt hoger dan Hallo andere zoekterm 'elektronische' als gevolg van Hallo term versterking waarde (2).

tooboost een termijn, gebruik Hallo caret, "^", symbool met een factor versterking (een getal) achter Hallo Hallo term die u zoekt. Hallo hoger Hallo versterking factor, hello meer relevante Hallo term relatieve tooother zoektermen worden. Hallo versterking factor is 1. Hoewel Hallo versterking factor moet positief zijn, kan kleiner dan 1 zijn (bijvoorbeeld 0,2) zijn.

**Voorbeeld 6** --met de rechtermuisknop op Hallo query. Zoeken naar taken met Hallo term 'computer analist"waar we zien er zijn geen resultaten met woorden computer en analist nog analist taken zijn Hallo boven aan het Hallo-resultaten.

* [& queryType volledige = & zoeken = business_title:computer analist](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

**Voorbeeld 7** --opnieuw probeert, versterking van deze tijd resulteert met Hallo term computer via Hallo term analist als beide woorden bestaat niet.

* [& queryType volledige = & zoeken = business_title:computer ^ 2 analist](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

## <a name="regular-expression-example"></a>Voorbeeld van een reguliere expressie
Een zoekopdracht reguliere expressie gevonden op basis van Hallo inhoud tussen voorwaartse slashes '/', als de gedocumenteerde in Hallo [klasse RegExp](http://lucene.apache.org/core/4_10_2/core/org/apache/lucene/util/automaton/RegExp.html).

**Voorbeeld 8** --met de rechtermuisknop op Hallo query. Taken met Hallo term Senior of Junior zoekt.

* `&queryType=full&$select=business_title&search=business_title:/(Sen|Jun)ior/`

Hallo-URL voor dit voorbeeld wordt niet correct weergegeven in het Hallo-pagina. Hallo de onderstaande URL kopiëren en plak deze in Hallo browser-URL-adres als tijdelijke oplossing:`http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:/(Sen|Jun)ior/)`

## <a name="wildcard-search-example"></a>Voorbeeld van jokertekens zoeken
U kunt een algemeen erkende syntaxis gebruiken voor meerdere (\*) of van afzonderlijke zoekopdrachten met jokertekens teken (?). Houd er rekening mee Hallo Lucene query parser ondersteunt Hallo gebruik van deze symbolen met één begrip en niet een wachtwoordzin.

**Voorbeeld 9** --met de rechtermuisknop op Hallo query. Zoeken naar taken die Hallo voorvoegsel 'prog, waaronder zakelijke titels met Hallo voorwaarden programmeren en programmeurs erin zou bevatten.

* [& queryType = volledige & $select = business_title & search business_title:prog* =](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:prog*)

U kunt geen gebruiken een * of? symbool als eerste teken van een zoekopdracht Hallo.

## <a name="next-steps"></a>Volgende stappen
Geef Hallo Lucene Queryparser in uw code. Hallo koppelingen volgen wordt uitgelegd hoe tooset u zoeken naar .NET- en Hallo REST-API zoekt. Hallo koppelingen eenvoudige standaardsyntaxis hello gebruiken zodat u tooapply moet wat u in dit artikel toospecify Hallo geleerd **queryType**.

* [Query uitvoeren op uw Azure Search-Index met behulp van Hallo .NET SDK](search-query-dotnet.md)
* [Query uitvoeren op uw Azure Search-Index met behulp van Hallo REST-API](search-query-rest-api.md)

## <a name="see-also"></a>Zie ook

 [Hoe vol tekst zoeken werkt in Azure Search](search-lucene-query-architecture.md)
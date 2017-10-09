---
title: Veelgestelde vragen (FAQ) over Azure Search aaaFrequently | Microsoft Docs
description: Vind antwoorden toocommon vragen over Microsoft Azure Search-Service
services: search
author: HeidiSteen
manager: jhubbard
ms.service: search
ms.technology: search
ms.topic: article
ms.date: 08/03/2017
ms.author: heidist
ms.openlocfilehash: 2c573750600d80585b746bfce20d6c0f8df5a262
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search---frequently-asked-questions-faq"></a>Azure Search - Veelgestelde vragen (FAQ)
 
 Vinden toocommonly antwoorden op veelgestelde vragen over concepten, code en scenario's gerelateerde tooAzure zoeken.

## <a name="platform"></a>Platform

### <a name="how-is-azure-search-different-from-full-text-search-in-my-dbms"></a>Hoe wordt Azure Search van zoeken in volledige tekst in mijn DBMS?

Azure Search biedt ondersteuning voor meerdere gegevensbronnen [taalkundige analyse voor vele talen](https://docs.microsoft.com/rest/api/searchservice/language-support), [aangepaste analyse voor interessante en ongebruikelijke gegevens invoer](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search), positie besturingselementen via zoeken [score berekenen profielen](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index), en gebruikerservaring functies zoals typeahead treffers markeren en meervoudige navigatie. Dit omvat ook andere onderdelen, zoals synoniemen en uitgebreide querysyntaxis, maar deze functies zijn niet in het algemeen verschillen.

### <a name="what-is-hello-difference-between-azure-search-and-elasticsearch"></a>Wat is Hallo verschil tussen Azure Search en Elasticsearch?

Bij het vergelijken van de zoekopdracht technologieën vragen klanten vaak voor specifieke informatie over op hoe Azure Search worden vergeleken met Elasticsearch. Klanten die Azure Search via Elasticsearch voor hun zoekacties toepassing projecten meestal kiezen doen omdat we een belangrijke taak eenvoudiger aangebracht hebben of ze nodig hebben Hallo ingebouwde integratie met andere Microsoft-technologieën:

+ Azure Search is een volledig beheerde cloudservice met 99,9% serviceovereenkomsten (SLA) wanneer ingericht met voldoende redundantie (2 replica's voor leestoegang, 3 replica's voor lezen-schrijven).
+ Microsoft [natuurlijke taal processors](https://docs.microsoft.com/rest/api/searchservice/language-support) toonaangevende inguistic analysis bieden.  
+ [Azure Search indexeerfuncties](search-indexer-overview.md) tal van Azure-gegevensbronnen voor initiële en incrementele indexeren kunt verkennen.
+ Als u snelle respons toofluctuations in query of volumes indexeren nodig hebt, kunt u [schuifregelaars](search-manage.md#scale-up-or-down) in hello Azure portal of voer een [PowerShell-script](search-manage-powershell.md), shard management rechtstreeks te omzeilen.  
+ [Score berekenen en afstemmen van functies](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) bieden Hallo betekent dat voor het zoeken positie scores afgezien van wat zoekmachine Hallo alleen kunt bieden beïnvloeden. 

### <a name="can-i-pause-azure-search-service-and-stop-billing"></a>Kan ik onderbreken Azure Search-service en facturering stoppen?

U kunt Hallo-service kan niet onderbreken. Rekenkracht en opslagbronnen worden toegewezen voor uw exclusief gebruik wanneer het Hallo-service wordt gemaakt. Het is niet mogelijk toorelease en het vrijmaken van deze bronnen op aanvraag. 

## <a name="indexing-operations"></a>Indexbewerkingen

### <a name="backup-and-restore-or-download-and-move-indexes-or-index-snapshots"></a>Back-up en herstellen (of downloaden en verplaatsen) indexen of index momentopnamen?

Weliswaar u kunt [ophalen van een indexdefinitie](https://docs.microsoft.com/rest/api/searchservice/get-index) op elk gewenst moment er is geen index extractie, momentopname of terugzetten van back-up-functie voor het downloaden van een *ingevuld* index uitgevoerd in de Hallo cloud tooa lokaal systeem, of het verplaatsen van deze tooanother Azure Search-service. 

Indexen zijn gebouwd en op basis van de code die u schrijft en alleen uitvoeren op Azure Search in de cloud Hallo gevuld. Normaal gesproken klanten die toomove een index tooanother service willen doen door hun code toouse een nieuw eindpunt te bewerken en voer het indexeren. Als u wilt dat Hallo mogelijkheid tootake een momentopname of back-up van een index, een stem geconverteerd op [User Voice](https://feedback.azure.com/forums/263029-azure-search/suggestions/8021610-backup-snapshot-of-index).

### <a name="can-i-index-from-sql-database-replicas-applies-tooazure-sql-database-indexershttpsdocsmicrosoftcomazuresearchsearch-howto-connecting-azure-sql-database-to-azure-search-using-indexers"></a>Kan ik index in SQL database-replica's (van de toepassing te[indexeerfuncties in Azure SQL Database](https://docs.microsoft.com/azure/search/search-howto-connecting-azure-sql-database-to-azure-search-using-indexers))

 Er zijn geen beperkingen op Hallo gebruik van primaire of secundaire replica's als een gegevensbron bij het bouwen van een index maken. Vernieuwen van een index met incrementele updates (op basis van gewijzigde records) vereist echter Hallo primaire replica. Deze vereiste zijn afkomstig van de SQL-Database, welke gegarandeerd op primaire replica's bijhouden. Als u met behulp van de secundaire replica's voor de werkbelasting van een index vernieuwen probeert, is er geen garantie dat u alle Hallo-gegevens ophalen.

## <a name="search-operations"></a>Zoekopdrachten

### <a name="can-i-search-across-multiple-indexes"></a>Kan ik meerdere indexen doorzoeken?

Nee, deze bewerking wordt niet ondersteund. Zoeken is altijd binnen het bereik tooa enkele index.

### <a name="can-i-restrict-search-corpus-access-by-user-identity"></a>Kan ik zoeken corpus toegang beperken door de gebruikersidentiteit van de?

Azure Search beschikt niet over een beveiligingsmodel op basis van rollen voor gegevenstoegang per gebruiker. Verificatie is de volledige rechten of alleen-lezen op Hallo serviceniveau. Sommige klanten hebben geïmplementeerd oplossingen op basis van [ `$filter` zoekparameter](https://docs.microsoft.com/rest/api/searchservice/search-documents), maar met de beste is een tijdelijke oplossing. Als u deze functie wilt, een stem geconverteerd op [User Voice](https://feedback.azure.com/forums/263029-azure-search/category/86074-security).

### <a name="why-are-there-zero-matches-on-terms-i-know-toobe-valid"></a>Waarom zijn er nul overeenkomt met op voorwaarden die ik toobe geldig weet?

meest voorkomende Hallo-aanvraag is niet te weten dat elk querytype verschillende zoekgedrag en niveaus van de taalkundige analyses ondersteunt. Zoekopdracht in volledige tekst, dit de belangrijkste werkbelasting hello is, bevat de analysefase van een taal die wordt verbroken voorwaarden omlaag tooroot formulieren. Dit aspect van het parseren van de query cast breder net over mogelijke overeenkomsten omdat hello tokens term overeenkomt met een groter aantal varianten.

Als u aanroept [andere querytypen](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) (jokertekens zoeken, fuzzy zoeken, zoeken bij benadering, suggesties, onder andere), is er geen taalkundige analyse. Voorwaarden zijn toegevoegd toohello querystructuur-is. 

### <a name="why-is-hello-search-rank-a-constant-or-equal-score-of-10-for-every-hit"></a>Waarom is een constante of gelijk zijn score van 1.0 voor elke treffer positie in zoekresultaten Hallo?

Standaard zoekresultaten worden berekend op basis van Hallo [statistische eigenschappen van die overeenkomt met de voorwaarden](search-lucene-query-architecture.md#stage-4-scoring), en hoge toolow in de resultatenset Hallo gerangschikt. Evenwel sommige querytypen (jokerteken, voorvoegsel, regex) bijdragen altijd een constante score toohello totale score-document. Dit gedrag is standaard. Azure Search gelden een constante tooallow gevonden via query uitbreiding toobe opgenomen in het Hallo-resultaten, zonder Hallo ranking beoordelen. 

Stel bijvoorbeeld dat een invoer van het 'rondleiding *' in een zoeken met jokertekens produceert komt overeen met 'rondleidingen', 'tourettes' en 'tourmaline'. Opgegeven Hallo aard van deze resultaten, is er geen enkele manier tooreasonably afleiden welke voorwaarden vindt u meer dan andere waardevolle. Om deze reden negeren we term frequenties wanneer resultaten scoren van typen jokerteken, voorvoegsel en regex-query's. Zoekresultaten op basis van een gedeeltelijke invoer een constante zijn opgegeven score tooavoid afwijking naar mogelijk onverwachte resultaten.

## <a name="design-patterns"></a>Ontwerppatronen

### <a name="what-is-hello-best-approach-for-implementing-localized-search"></a>Wat is de aanbevolen aanpak voor het implementeren van gelokaliseerde zoeken Hallo?

De meeste klanten specifieke velden over een verzameling kiezen wanneer deze wordt gezet toosupporting verschillende landinstellingen (talen) in de Hallo dezelfde index. Landspecifieke velden maken het mogelijk tooassign een juiste analyzer. Bijvoorbeeld, toewijzen aan Hallo Microsoft Frans Analyzer tooa veld met Franse tekenreeksen. Het vereenvoudigt ook filteren. Als u dat een query wordt gestart op een pagina fr-fr, kunt u zoekveld resultaten toothis kan beperken. Of maak een [score berekenen profiel](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) toogive Hallo veld meer relatieve gewicht.

## <a name="next-steps"></a>Volgende stappen

Uw vraag over een ontbrekende functie of functionaliteit is? Hallo-functie op Hallo aanvragen [User Voice-website](https://feedback.azure.com/forums/263029-azure-search).

## <a name="see-also"></a>Zie ook

 [StackOverflow: Azure Search](https://stackoverflow.com/questions/tagged/azure-search)   
 [Hoe vol tekst zoeken werkt in Azure Search](search-lucene-query-architecture.md)  
 [Wat is Azure Search?](search-what-is-azure-search.md)

 
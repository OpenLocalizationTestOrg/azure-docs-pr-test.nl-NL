---
title: 'Azure DB Cosmos-ontwerppatroon: sociale media-apps | Microsoft Docs'
description: Meer informatie over een ontwerppatroon voor sociale netwerken dankzij het gebruik van Hallo opslag flexibiliteit van Azure DB die Cosmos en andere Azure-services.
keywords: Sociale media-apps
services: cosmos-db
author: ealsur
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 2dbf83a7-512a-4993-bf1b-ea7d72e095d9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: mimig
ms.openlocfilehash: 47a22f2c5762d62b176921c8052e7bd75d8cf6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="going-social-with-azure-cosmos-db"></a>Met Azure Cosmos DB sociale gaan
Die in een samenleving massively onderling verbonden betekent dat op een bepaald moment in leven u deel van uitmaken een **sociale netwerken**. We gebruiken onze passie tookeep sociale netwerken op de hoogte blijft vrienden, collega's, familie of soms tooshare met mensen met een gemeenschappelijke interesses.

Als engineers of ontwikkelaars kunnen we mogelijk hebben zich wel eens afgevraagd hoe deze netwerken opslaan en onze gegevens onderling verbinding maken of mogelijk hebt zelfs is toocreate te beheren of systeemarchitect een nieuw sociale netwerk voor een specifieke gespecialiseerde markt uzelf. Als de grote vraag Hallo zich voordoet: hoe worden al deze gegevens opgeslagen?

Stel dat we een nieuwe en glanzend sociale netwerken, waar onze gebruikers artikelen met gerelateerde medium, zoals foto's, video's of zelfs muziek kunnen boeken maakt. Gebruikers kunnen opmerkingen over berichten en punten geven voor de classificaties. Er wordt een feed van berichten die worden weergegeven voor gebruikers en kunnen toointeract met op Hallo belangrijkste website-startpagina. Dit erg complex niet begrijpt (aanvankelijk), maar voor Hallo mogelijk te houden van eenvoud, gaan we er (we kan aangepaste gebruiker feeds van invloed op een relaties dieper, maar is langer dan Hallo doel van dit artikel).

Ja, hoe kan we dit opslaan en waar?

Veel van u mogelijk ervaring op SQL-databases of hebt u ten minste begrip [relationele gegevens modelleren](https://en.wikipedia.org/wiki/Relational_model) en u geneigd toostart tekenen van ongeveer het volgende mogelijk:

![Diagram ter illustratie van een relatieve relationele model](./media/social-media-apps/social-media-apps-sql.png) 

Een perfect genormaliseerde en gegevensstructuur... die niet wordt geschaald. 

Geen krijgt mij verkeerde, ik heb gewerkt om alle mijn leven met SQL-databases, ze zijn ideaal, maar zoals elke patroon, practice en software-platform, is het niet ideaal voor elk scenario.

Waarom is SQL Hallo beste keuze in dit scenario niet? Bekijk Hallo-structuur van een enkele post, als ik wilde tooshow die in een website of toepassing boekt, zou er toodo een query met... tabel 8 joins (!) alleen tooshow één enkele post, nu afbeelding is een stream van berichten die dynamisch wordt geladen en worden weergegeven op het welkomstscherm en u kunt tegenkomen wanneer ik ga.

We kunnen natuurlijk gebruiken een internationale SQL-exemplaar met voldoende power toosolve duizendtallen van query's met deze veel joins tooserve onze content maar echt, waarom zouden we wanneer een eenvoudigere oplossing bestaat?

## <a name="hello-nosql-road"></a>Hallo NoSQL weg
In dit artikel begeleidt u bij uw sociale platform-gegevens met Azure NoSQL-database te modelleren [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) op een rendabele manier tijdens het gebruik van andere Azure DB die Cosmos-functies zoals Hallo [Gremlin Graph API ](../cosmos-db/graph-introduction.md). Met behulp van een [NoSQL](https://en.wikipedia.org/wiki/NoSQL) benadering voor het opslaan van gegevens in JSON-indeling en toepassen van [denormalization](https://en.wikipedia.org/wiki/Denormalization), onze eerder ingewikkeld post kan worden omgezet in één [Document](https://en.wikipedia.org/wiki/Document-oriented_database):


    {
        "id":"ew12-res2-234e-544f",
        "title":"post title",
        "date":"2016-01-01",
        "body":"this is an awesome post stored on NoSQL",
        "createdBy":User,
        "images":["http://myfirstimage.png","http://mysecondimage.png"],
        "videos":[
            {"url":"http://myfirstvideo.mp4", "title":"hello first video"},
            {"url":"http://mysecondvideo.mp4", "title":"hello second video"}
        ],
        "audios":[
            {"url":"http://myfirstaudio.mp3", "title":"hello first audio"},
            {"url":"http://mysecondaudio.mp3", "title":"hello second audio"}
        ]
    }

En kan worden verkregen met één query op, en er is geen joins. Dit is nog veel meer eenvoudig en snel en budget-wise, vereist minder resources tooachieve een beter resultaat.

Azure Cosmos DB zorgt ervoor dat alle Hallo-eigenschappen worden geïndexeerd met de automatische indexeren, wat kan zelfs zijn [aangepaste](indexing-policies.md). Hallo schemavrije benadering kan we documenten opslaan met andere en dynamische structuren, mogelijk morgen willen we posts toohave wordt afgehandeld tijdens een lijst met categorieën of -hashtags die zijn gekoppeld, Cosmos DB Hallo nieuwe documenten Hello kenmerken met zonder extra toegevoegd werk dat nodig is door ons.

Opmerkingen over een post kunnen worden behandeld als alleen andere advertenties met een bovenliggende eigenschap (vereenvoudigt de objecttoewijzing van onze). 

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":User2,
        "parent":"ew12-res2-234e-544f"
    }

    {
        "id":"asd2-fee4-23gc-jh67",
        "title":"Ditto!",
        "date":"2016-01-03",
        "createdBy":User3,
        "parent":"ew12-res2-234e-544f"
    }

En alle sociale interacties kunnen worden opgeslagen op een afzonderlijke object als items:

    {
        "id":"dfe3-thf5-232s-dse4",
        "post":"ew12-res2-234e-544f",
        "comments":2,
        "likes":10,
        "points":200
    }

Maken van feeds is zojuist een kwestie van het maken van documenten die een lijst met post-id's met een bepaalde relevantie volgorde kunnen bevatten:

    [
        {"relevance":9, "post":"ew12-res2-234e-544f"},
        {"relevance":8, "post":"fer7-mnb6-fgh9-2344"},
        {"relevance":7, "post":"w34r-qeg6-ref6-8565"}
    ]

We een 'laatste' stream met berichten die zijn geordend op aanmaakdatum kan hebben, die 'gegevensbeheer' stream geboekt met meer positieve in Hallo afgelopen 24 uur kan zelfs implementeren van een aangepaste stroom voor elke gebruiker op basis van logica zoals pc-gebruikers en interesses en is nog steeds een lijst met  advertenties. Het is een kwestie van hoe toobuild die deze lijsten, maar Hallo lezen prestaties concurrerende blijft. Zodra er een van deze lijsten aanschaft, geven we een enkele query tooCosmos DB met Hallo [IN de operator](documentdb-sql-query.md#WhereClause) tooobtain pagina's van berichten op een tijdstip.

Hallo streams feed kan worden gebouwd met behulp van [Azure App Services](https://azure.microsoft.com/services/app-service/) processen op de achtergrond: [Webjobs](../app-service-web/web-sites-create-web-jobs.md). Nadat een advertentie is gemaakt, achtergrondverwerking kan worden geactiveerd met behulp van [Azure Storage](https://azure.microsoft.com/services/storage/) [wachtrijen](../storage/queues/storage-dotnet-how-to-use-queues.md) en geactiveerd met behulp van Hallo Webjobs [Azure Webjobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md), uitvoering Hallo boeken doorgeven in streams op basis van ons eigen aangepaste regels. 

Punten en positieve via een post kunnen worden verwerkt in een uitgestelde manier met behulp van deze dezelfde techniek toocreate een omgeving uiteindelijk consistent is.

Pc-gebruikers zijn lastiger. Cosmos DB heeft een maximale grootte van maximaal document en grote documenten lezen/schrijven kunnen invloed hebben op Hallo schaalbaarheid van uw toepassing. Zo kunt u denkt dat over het opslaan van pc-gebruikers als een document met deze structuur:

    {
        "id":"234d-sd23-rrf2-552d",
        "followersOf": "dse4-qwe2-ert4-aad2",
        "followers":[
            "ewr5-232d-tyrg-iuo2",
            "qejh-2345-sdf1-ytg5",
            //...
            "uie0-4tyg-3456-rwjh"
        ]
    }

Dit werkt mogelijk voor een gebruiker met enkele duizenden pc-gebruikers, maar als onze posities lid wordt van sommige beroemdheden, deze benadering tooa groot documentgrootte leidt en grootte van het document uiteindelijk treffers Hallo cap mogelijk.

toosolve, gebruiken we een gemengde benadering. Als onderdeel van Hallo gebruikersstatistieken document bewaren wij Hallo aantal pc-gebruikers:

    {
        "id":"234d-sd23-rrf2-552d",
        "user": "dse4-qwe2-ert4-aad2",
        "followers":55230,
        "totalPosts":452,
        "totalPoints":11342
    }

En de werkelijke grafiek Hallo van pc-gebruikers kan worden opgeslagen met behulp van Azure DB die Cosmos [Gremlin Graph API](../cosmos-db/graph-introduction.md), toocreate [hoekpunten](http://mathworld.wolfram.com/GraphVertex.html) voor elke gebruiker en [randen](http://mathworld.wolfram.com/GraphEdge.html) handhaven Hallo ' A-volgt-B'-relaties. Hallo Graph API we u niet alleen verkrijgen Hallo pc-gebruikers van een bepaalde gebruiker maar complexe query's tooeven voorstellen mensen gemeenschappelijk maken. Als we toohello grafiek Hallo toevoegen inhoud categorieën die mensen, zoals of profiteer van, gaat u weven ervaringen met slim inhoud content voorstellen die we volgen zoals of zoeken naar personen met wie er mogelijk veel gemeen hebben.

Hallo gebruikersstatistieken document kan nog steeds gebruikte toocreate kaarten in Hallo UI of snelle profiel previews.

## <a name="hello-ladder-pattern-and-data-duplication"></a>Hallo 'Ladder'-patroon en gegevens worden gedupliceerd
Als u in Hallo JSON-document dat verwijst naar een post opgevallen mogelijk, zijn er meerdere exemplaren van een gebruiker. En u zou hebben geraden rechts, betekent dit dat het Hallo-informatie die een gebruiker, krijgt deze denormalization vertegenwoordigt aanwezig is in meer dan één plaats zijn mogelijk.

In volgorde tooallow voor snellere query's worden er gegevens worden gedupliceerd. Hallo probleem met dit neveneffect is dat als door een bepaalde actie, wijzigingen van de gegevens van een gebruiker, moeten we toofind alle Hallo activiteiten hij ooit hebt en deze relaties bijwerken alle. Geen geluid zeer praktische, rechts?

We zijn gaan toosolve deze door te identificeren Hallo sleutelkenmerken van een gebruiker die we in onze toepassing voor elke activiteit zien. Als we visueel een bericht met onze toepassing weergeven en net Hallo maker van naam en afbeelding wilt weergeven, waarom u alle Hallo gebruikersgegevens opgeslagen in het kenmerk Hallo 'controleactiviteit gemaakt door'? Voor elke opmerking we zojuist Hallo gebruikersafbeelding weergeven, hoeft er niet echt Hallo overige zijn gegevens. Dat is waar iets dat ik aanroepen Hallo 'Ladder patroon' in het spel worden opgehaald.

We gaan gebruikersgegevens als een voorbeeld:

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "address":"742 Evergreen Terrace",
        "birthday":"1983-05-07",
        "email":"john@doe.com",
        "twitterHandle":"@john",
        "username":"johndoe",
        "password":"some_encrypted_phrase",
        "totalPoints":100,
        "totalPosts":24
    }

Door deze informatie bekijkt, kunnen we snel die belangrijke informatie en die niet is, waardoor een 'Ladder' detecteren:

![Diagram van een patroon ladder](./media/social-media-apps/social-media-apps-ladder.png)

Hallo kleinste stap heet een UserChunk, Hallo minimale stukje informatie waarmee een gebruiker en het wordt gebruikt voor gegevens worden gedupliceerd. Hallo-grootte van Hallo gedupliceerd tooonly Hallo gegevens we 'tonen' verlaagt, beperken we Hallo dat grote updates.

middelste stap Hallo Hallo gebruiker wordt genoemd, is het Hallo volledige gegevens die worden gebruikt op de meeste prestaties-afhankelijke query's op Cosmos-DB Hallo meest gebruikte en kritieke. Het bevat Hallo-informatie dat wordt vertegenwoordigd door een UserChunk.

grootste Hallo is Hallo Extended gebruiker. Dit omvat alle kritieke Hallo gebruikersgegevens plus andere gegevens die niet echt nodig toobe lezen snel hebt of gebruik de uiteindelijke (zoals Hallo aanmelding) is. Deze gegevens kan worden opgeslagen buiten Cosmos-database in Azure SQL Database- of Azure Storage-tabellen.

Waarom zouden we Hallo gebruiker splitsen en zelfs deze informatie op te slaan op verschillende plaatsen? Omdat vanuit het oogpunt van prestaties hello groter Hallo documenten, Hallo costlier Hallo-query's. Documenten bewaren dunne Hello rechts informatie toodo alle uw prestaties afhankelijk zijn van een query voor het sociaal netwerk en store Hallo andere extra informatie voor de uiteindelijke scenario's zoals, volledig profiel bewerkt, aanmeldingen, zelfs gegevensanalyse voor gebruiksanalyse en Big Gegevens initiatieven. We zeker niet van belang als Hallo verzamelen van gegevens voor gegevensanalyse is langzamer, omdat deze wordt uitgevoerd op Azure SQL Database, we hebben betrekking op echter dat onze gebruikers met een snelle en dunne ervaring hebben. Een gebruiker wordt opgeslagen op een Cosmos-DB eruit als volgt:

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "username":"johndoe"
        "email":"john@doe.com",
        "twitterHandle":"@john"
    }

En een Post eruit als:

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":{
            "id":"dse4-qwe2-ert4-aad2",
            "username":"johndoe"
        }
    }

En wanneer een bewerking waarbij een van de kenmerken Hallo van Hallo segment wordt beïnvloed ontstaat, is het eenvoudig toofind Hallo van invloed op documenten met behulp van query's die verwijzen toohello geïndexeerde kenmerken (Selecteer * FROM boekt p waar p.createdBy.id == 'edited_user_id') en vervolgens bij te werken Hallo-segmenten.

## <a name="hello-search-box"></a>Hallo zoekvak
Gebruikers zullen gelukkig veel inhoud genereren. En we moet kunnen tooprovide Hallo mogelijkheid toosearch en inhoud die mogelijk niet direct in hun inhoud gegevensstromen, mogelijk omdat we volgen Hallo auteurs niet vinden, of misschien we zojuist proberen toofind dat oude bericht die we 6 maanden geleden is.

Gelukkig en omdat we Azure Cosmos DB gebruiken, kunnen we eenvoudig implementeren een zoekactie engine met [Azure Search](https://azure.microsoft.com/services/search/) binnen een paar minuten en zonder te hoeven typen één regel code (anders dan natuurlijk Hallo Zoek proces en de gebruikersinterface).

Waarom is dit dus eenvoudig?

Azure Search implementeert wat ze aanroepen [indexeerfuncties](https://msdn.microsoft.com/library/azure/dn946891.aspx), achtergrondprocessen die haakje in de opslagplaatsen van uw gegevens en automagically toevoegen, bijwerken of verwijderen van uw objecten in Hallo indexen. Deze ondersteuning bieden voor een [indexeerfuncties in Azure SQL Database](https://blogs.msdn.microsoft.com/kaevans/2015/03/06/indexing-azure-sql-database-with-azure-search/), [Azure Blobs indexeerfuncties](../search/search-howto-indexing-azure-blob-storage.md) en gelukkig [Azure Cosmos DB indexeerfuncties](../search/search-howto-index-documentdb.md). Hallo overgang van de gegevens van de Cosmos-DB tooAzure zoeken is eenvoudig, als beide archiefgegevens in JSON-indeling, we hoeft te[onze Index maken](../search/search-create-index-portal.md) en welke kenmerken van onze documenten we geïndexeerde willen en dit is Alles toewijzen binnen een paar minuten (afhankelijk van de grootte Hallo van onze gegevens), worden alle onze inhoud beschikbaar toobe doorzocht, door Hallo beste Search-as-a-Service-oplossing in cloudinfrastructuur. 

Voor meer informatie over Azure Search vindt u Hallo [Hitchhiker van handleiding tooSearch](https://blogs.msdn.microsoft.com/mvpawardprogram/2016/02/02/a-hitchhikers-guide-to-search/).

## <a name="hello-underlying-knowledge"></a>Hallo onderliggende kennis
Na deze inhoud die moet worden uitgebreid en wordt elke dag op te slaan, kunnen we vinden onszelf gegevensclassificatie: wat kan ik doen met deze stroom van gegevens van mijn gebruikers?

Hallo-antwoord is eenvoudig: toowork plaatsen en te leren van het.

Maar wat we meer? Een paar eenvoudige voorbeelden zijn [gevoel analysis](https://en.wikipedia.org/wiki/Sentiment_analysis), inhoud aanbevelingen op basis van gebruikersvoorkeuren of zelfs een geautomatiseerde inhoud beheerder dat ervoor zorgt dat alle inhoud die wordt gepubliceerd door onze sociale netwerken Hallo voor Hallo veilig is familie.

Nu dat ik heb u aangesloten, zult u waarschijnlijk moet u enkele PhD in math wetenschappelijke tooextract deze patronen en de informatie uit de eenvoudige databases en -bestanden, maar u zou verkeerde zien.

[Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/), deel uit van Hallo [Cortana Intelligence Suite](https://www.microsoft.com/en/server-cloud/cortana-analytics-suite/overview.aspx), Hallo is een volledig beheerde cloudservice waarmee u het maken van werkstromen met algoritmen in een eenvoudige interface voor slepen en neerzetten, code van uw eigen algoritmen in [R](https://en.wikipedia.org/wiki/R_\(programming_language\)) of gebruik een aantal Hallo al zijn gemaakt en gereed toouse API's, zoals: [Tekstanalyse](https://gallery.cortanaanalytics.com/MachineLearningAPI/Text-Analytics-2), [inhoud beheerder](https://www.microsoft.com/moderator) of [aanbevelingen](https://gallery.cortanaanalytics.com/MachineLearningAPI/Recommendations-2).

tooachieve elk van deze Machine Learning-scenario's kunnen we gebruiken [Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) tooingest Hallo gegevens uit verschillende bronnen en gebruik [U-SQL](https://azure.microsoft.com/documentation/videos/data-lake-u-sql-query-execution/) tooprocess Hallo informatie en uitvoer genereren die kunnen worden verwerkt door Azure Machine Learning.

Is een andere beschikbare optie toouse [Microsoft cognitieve Services](https://www.microsoft.com/cognitive-services) tooanalyze onze gebruikers inhoud; niet alleen kunnen we ze begrijpen betere (via het analyseren van schrijven met [Text Analytics API](https://www.microsoft.com/cognitive-services/en-us/text-analytics-api)), maar We kan ook ongewenste of volwassen inhoud detecteren en dienovereenkomstig reageren met [Computer Vision-API](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api). Cognitieve Services bevatten een groot aantal out-of-the-box-oplossingen die geen enkele vorm van Machine Learning knowledge toouse is vereist.

## <a name="a-planet-scale-social-experience"></a>Een sociaal wereld scale-ervaring
Er is een laatste, maar niet in het minst belangrijk onderwerp die ik moet houden: **schaalbaarheid**. Bij het ontwerpen van een architectuur cruciaal is dat elk onderdeel kan worden geschaald op een eigen, ofwel omdat we tooprocess meer gegevens nodig is of omdat we willen toohave een grotere geografische dekking (of beide!). Gelukkig bereiken van een complexe taak is een **klare ervaring** met Cosmos-DB.

Biedt ondersteuning voor cosmos DB [dynamische partitionering](https://azure.microsoft.com/blog/10-things-to-know-about-documentdb-partitioned-collections/) out-of-the-box door het automatisch maken van partities op basis van een bepaalde **partitiesleutel** (gedefinieerd als een van de kenmerken Hallo in uw documenten). Hallo juist partitiesleutel moet worden uitgevoerd tijdens de ontwerpfase definiëren en behouden in gedachten Hallo [aanbevolen procedures](../cosmos-db/partition-data.md#designing-for-partitioning) beschikbaar; in geval van een sociale ervaring Hallo moet uw strategie voor partitionering worden afgestemd op Hallo manier waarop u een query (leesbewerkingen dezelfde partitie zijn binnen Hallo wenselijk) en schrijven ("hotspots" voorkomen door te spreiden schrijfbewerkingen op meerdere partities). Sommige opties zijn: partities op basis van een tijdelijke sleutel (dag/maand/week) door inhoud categorie, per geografische regio, door gebruiker. Alles echt afhankelijk van hoe u Hallo gegevens opvragen en weergeven in uw sociale ervaring. 

Een interessant punt opgemerkt Cosmos-database wordt uitgevoerd is met uw query's (inclusief [statistische functies](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)) voor alle partities in uw transparant, hoeft u niet tooadd alle logica wanneer uw gegevens groeit.

Met de tijd, wordt uiteindelijk groeien in verkeer en het verbruik van uw (gemeten in [RUs](request-units.md), of Aanvraageenheden) wordt verhoogd. U leest en schrijft vaker als uw userbase groeit en ze gaat maken en lezen meer inhoud; de mogelijkheid van Hallo **schalen van uw doorvoer** is het essentieel. Onze RUs verhoging is heel eenvoudig, we kunt dit doen met een paar klikken op Hallo Azure Portal of door [uitgeven van opdrachten via Hallo API](https://docs.microsoft.com/rest/api/documentdb/replace-an-offer).

![Omhoog schalen en het definiëren van een partitiesleutel](./media/social-media-apps/social-media-apps-scaling.png)

Wat gebeurt er als dingen wordt steeds betere en gebruikers van een andere regio, land of continent, ziet uw platform en gaan gebruiken, wat een geweldige verrassing!

Maar geduld … ontdekt u snel hun ervaring met uw platform is niet optimaal; ze zijn tot nu toe weg van uw operationele regio dat Hallo latentie verschrikkelijke is en u natuurlijk niet dat ze tooquit wilt. Als er slechts er een eenvoudige manier van is **uitbreiden van uw globale bereik**..., maar er is!

Cosmos DB kunt u [globaal uw gegevens repliceren](../cosmos-db/tutorial-global-distribution-documentdb.md) en transparant met een paar muisklikken en automatisch kiezen uit Hallo beschikbare regio's van uw [clientcode](../cosmos-db/tutorial-global-distribution-documentdb.md). Dit betekent ook dat u hebt [meerdere regio's voor failover-](regional-failover.md). 

Wanneer u uw gegevens globaal repliceert, moet u ervoor dat uw clients kunnen profiteren van deze toomake. Als u een web-front- of toegang tot API's vanaf mobiele clients gebruikt, kunt u implementeren [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) en klonen van uw Azure App Service op alle gewenste Hallo-regio's met behulp van een [prestaties configuratie](../app-service-web/web-sites-traffic-manager.md)toosupport de uitgebreide dekking van uw globale. Wanneer uw clients toegang krijgen uw frontend of API's tot, worden ze gerouteerde toohello dichtstbijzijnde App Service, waarmee op zijn beurt verbinding toohello lokale Cosmos DB replica wordt gemaakt.

![Globale dekking tooyour sociale platform toevoegen](./media/social-media-apps/social-media-apps-global-replicate.png)

## <a name="conclusion"></a>Conclusie
In dit artikel wordt geprobeerd tooshed sommige in Hallo alternatieven sociale netwerken volledig op Azure maken met services voor lage kosten en goede resultaten door bevorderen Hallo gebruik van een oplossing en gegevens verdeling van opslag met meerdere lagen licht 'Ladder' genoemd.

![Diagram van interactie tussen Azure-services voor sociale netwerken](./media/social-media-apps/social-media-apps-azure-solution.png)

Hallo waarheid is dat er geen zilver opsommingsteken voor dit soort scenario's, is hieraan Hallo synergie gemaakt door Hallo combinatie van goede services die we toobuild geweldige ervaringen kunnen: Hallo snelheid en vrijheid van Azure DB die Cosmos tooprovide een goede sociale toepassing Hallo intelligence achter een zoekoplossing klas, zoals Azure Search, Hallo flexibiliteit van Azure App Services toohost niet zelfs taal networkdirect toepassingen maar krachtige achtergrondprocessen en Hallo uitbreidbare Azure Storage en Azure SQL Database voor opslaan van grote hoeveelheden gegevens en Hallo analytische kracht van Azure Machine Learning toocreate kennis en intelligentie die u kunt uw feedback tooour processen en Help ons te leveren Hallo rechts inhoud toohello juiste gebruikers.

## <a name="next-steps"></a>Volgende stappen
Zie toolearn meer informatie over gebruiksvoorbeelden voor Cosmos-DB [algemene Cosmos DB gebruiksvoorbeelden](use-cases.md).

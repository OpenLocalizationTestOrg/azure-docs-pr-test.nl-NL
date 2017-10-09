---
title: aaaCommon gebruiken voor aanvragen en scenario's voor Azure Cosmos DB | Microsoft Docs
description: 'Meer informatie over Hallo top vijf gebruiksvoorbeelden voor Azure Cosmos DB: gebruiker gegenereerde inhoud, logboekregistratie van gebeurtenissen, gegevens in de catalogus, gebruikersgegevens voorkeuren en Internet der dingen (IoT).'
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: eca68a58-1a8c-4851-8cf8-6e4d2b889905
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: mimig
ms.openlocfilehash: 115a418e7b18d5033c4d7e64591bf302aea0190b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="common-azure-cosmos-db-use-cases"></a>Algemene gebruiksvoorbeelden voor Azure Cosmos-DB
In dit artikel biedt een overzicht van enkele algemene gebruiksvoorbeelden voor Azure Cosmos DB.  Hallo aanbevelingen in dit artikel fungeren als een beginpunt tijdens het ontwikkelen van uw toepassing met Cosmos-DB.   

Na het lezen van dit artikel, moet u kunnen tooanswer Hallo vragen te volgen: 

* Wat zijn algemene gebruiksvoorbeelden voor Azure Cosmos DB Hallo?
* Wat zijn Hallo voordelen van het gebruik van Azure DB die Cosmos voor retail toepassingen?
* Wat zijn Hallo voordelen van het gebruik van Azure DB die Cosmos als gegevensopslag voor Internet der dingen (IoT) systemen?
* Wat zijn Hallo voordelen van het gebruik van Azure DB die Cosmos voor webtoepassingen en mobiele toepassingen?

## <a name="introduction"></a>Inleiding
[Azure Cosmos DB](../cosmos-db/introduction.md) globaal gedistribueerde database-service van Microsoft is. Hallo-service is ontworpen tooallow klanten tooelastically (en onafhankelijk) schaal doorvoer en opslag voor een willekeurig aantal geografische regio's. Azure Cosmos DB Hallo eerste globaal gedistribueerde database-service is in Hallo markt vandaag toooffer uitgebreide [serviceovereenkomsten](https://azure.microsoft.com/support/legal/sla/cosmos-db/) die omvat doorvoer, latentie, beschikbaarheid en consistentie. 

Hello Azure Cosmos DB project gestart in 2011 als 'Project Florence' tooaddress developer-knelpunten worden managementoverhead voor grote Internet-toepassingen binnen Microsoft. Observeren dat deze problemen zijn niet uniek tooMicrosoft toepassingen, we besloten toomake Azure Cosmos DB algemeen beschikbaar tooexternal ontwikkelaars in 2015 is in de vorm van Hallo [Azure DocumentDB](https://azure.microsoft.com/blog/documentdb-moving-to-general-availability/). Hallo-service wordt ubiquitously intern gebruikt binnen Microsoft en is een van Hallo snelst groeiende services die door Azure ontwikkelaars extern gebruikt. 

Azure Cosmos-database is een globale gedistribueerde, meerdere model-database die wordt gebruikt in een breed scala aan toepassingen en gebruiksvoorbeelden. Er is een goede keuze voor een [zonder server](http://azure.com/serverless) toepassing die moet beschikken over lage reactietijden van de volgorde van milliseconde en tooscale moet snel en internationaal niveau opereren. Deze ondersteuning biedt voor meerdere gegevensmodellen (sleutel / waarde-, documenten, grafieken en kolommen) en veel API's voor toegang tot inclusief [MongoDB](mongodb-introduction.md), [DocumentDB SQL](documentdb-introduction.md), [Gremlin](graph-introduction.md), en [Azure-tabellen](table-introduction.md) systeemeigen en in een uitbreidbare manier. 

Hallo hieronder vindt u enkele kenmerken die geschikt zijn voor krachtige toepassingen met globale streven van Azure Cosmos-database.

* Azure Cosmos DB partities systeemeigen van uw gegevens voor hoge beschikbaarheid en schaalbaarheid. Azure Cosmos DB biedt 99,99% garanties met betrekking tot beschikbaarheid, doorvoer, lage latentie en consistentie.
* Azure Cosmos DB heeft back SSD-opslag met lage latentie reactietijden van de volgorde van milliseconde.
* Azure DB van Cosmos-ondersteuning voor consistentieniveaus zoals uiteindelijke, consistente voorvoegsel, sessie en gebonden-verouderd kan volledige flexibiliteit en lage kosten voor prestaties verhouding. Er is geen databaseservice biedt zoveel flexibiliteit als Azure Cosmos DB in niveaus consistentie. 
* Azure Cosmos-database heeft een flexibele data-vriendelijk-prijsmodel die meters opslag en doorvoer onafhankelijk.
* Azure Cosmos-DB gereserveerde doorvoer model kunt u toothink in termen van het aantal leest/schrijft in plaats van de CPU/geheugen/IOPs van Hallo onderliggende hardware.
* Azure Cosmos-DB ontwerp kunt die u de schaal van toomassive aanvraag volumes in Hallo volgorde Biljoenen aanvragen per dag.

Deze kenmerken zijn nuttig in webtoepassingen, mobiele games en IoT-toepassingen die moeten lage responstijden en moeten toohandle enorme hoeveelheden lees- en schrijfbewerkingen.

## <a name="iot-and-telematics"></a>IoT en telematica
Gebruiksvoorbeelden IoT vaak sommige patronen in hoe ze, verwerken opnemen, delen en opslaan van gegevens.  Deze systemen moeten eerst tooingest bursts van gegevens van het apparaat sensoren van verschillende landinstellingen. Vervolgens deze systemen verwerken en analyseren van streaming gegevens tooderive realtime-inzichten verkrijgen. Hallo-gegevens zijn vervolgens toocold opslag voor batch analytics gearchiveerd. Microsoft Azure biedt uitgebreide services die kunnen worden toegepast voor IoT gebruiksvoorbeelden, waaronder Azure Cosmos DB, Azure Event Hubs, Azure Stream Analytics, Azure Notification Hub, Azure Machine Learning, Azure HDInsight en Power BI. 

![Azure IoT voor Cosmos-DB-referentiearchitectuur](./media/use-cases/iot.png)

Bursts van gegevens kunnen door Azure Event Hubs worden ingenomen zoals gegevensopname hoge doorvoersnelheden met een lage latentie biedt. Ingenomen gegevens die moeten worden verwerkt toobe voor realtime inzicht mag softwareproducten tooAzure Stream Analytics voor realtime analyses. Gegevens kunnen worden geladen naar Cosmos-DB Azure ad-hoc query's. Zodra het Hallo-gegevens in Azure DB die Cosmos is geladen, is Hallo gegevens gereed toobe opgevraagd. Bovendien kunnen nieuwe gegevens van en wijzigingen tooexisting worden gelezen op wijziging feed. Wijziging feed is een permanente, alleen logboek waarin wijzigingen tooCosmos DB verzamelingen in opeenvolgende volgorde toevoegen. Hallo die alle gegevens of alleen wijzigingen toodata in Azure Cosmos DB kan worden gebruikt als referentiegegevens als onderdeel van realtime-analyses. Bovendien worden gegevens verder verfijnd en verwerkt door de verbindende Azure Cosmos DB gegevens tooHDInsight voor Pig, Hive of kaart/verminderen taken.  Verfijnd gegevens worden vervolgens back tooAzure Cosmos DB geladen voor rapportage.   

Zie voor een voorbeeld IoT-oplossing met Azure Cosmos DB, EventHubs en Storm, Hallo [hdinsight-storm-voorbeelden opslagplaats op GitHub](https://github.com/hdinsight/hdinsight-storm-examples/).

Zie voor meer informatie over Azure IoT-producten [maken Hallo Internet uw dingen](http://www.microsoft.com/server-cloud/internet-of-things.aspx). 

## <a name="retail-and-marketing"></a>Detailhandel en marketing
Azure Cosmos DB wordt uitgebreid in van het Microsoft commerciële platforms met Hallo Windows Store en XBox Live gebruikt. Het wordt ook gebruikt in de detailhandel Hallo voor het opslaan van gegevens in de catalogus en voor gebeurtenis bron in volgorde pijplijnen verwerken.

Gebruiksscenario's voor data Catalog hebben betrekking op opslaat en gegevensquery's van een set kenmerken voor entiteiten zoals mensen, plaatsen en producten. Enkele voorbeelden van gegevens in de catalogus zijn gebruikersaccounts, catalogi, IoT-apparaat registers en factuur van materialen systemen. Kenmerken voor deze gegevens kunnen variëren en via tijd toofit toepassingsvereisten kunnen wijzigen.

Bekijk een voorbeeld van een productcatalogus voor de leverancier van een auto-onderdelen. Elk onderdeel hebben een eigen kenmerken in toevoeging toohello gangbare kenmerken die delen van alle onderdelen. Kenmerken voor een bepaald deel kunnen bovendien Hallo volgende jaar wanneer een nieuw model wordt vrijgegeven wijzigen. Azure Cosmos DB ondersteunt flexibele schema's en hiërarchische gegevens en het is dus geschikt voor het opslaan van gegevens in de productcatalogus.

![Azure DB Cosmos catalogus retail referentiearchitectuur](./media/use-cases/product-catalog.png)

Azure Cosmos DB wordt vaak gebruikt voor gebeurtenis bron toopower gebeurtenissen architecturen met behulp van de [wijzigen van de feed](change-feed.md) functionaliteit. Hallo wijziging feed biedt downstream microservices Hallo mogelijkheid tooreliably en incrementeel lezen wordt ingevoegd en updates (bijvoorbeeld volgorde gebeurtenissen) tooan Azure Cosmos DB gemaakt. Deze functie kan worden overgenomen tooprovide een persistente gebeurtenis opslaan als broker bericht voor wijzigen van de status van gebeurtenissen en station verwerking werkstroom tussen veel microservices (die kunnen worden geïmplementeerd als [zonder server Azure Functions](http://azure.com/serverless)).

![Azure Cosmos DB ordening referentiearchitectuur pijplijn](./media/use-cases/event-sourcing.png)

Bovendien kunnen gegevens die zijn opgeslagen in Azure Cosmos DB worden geïntegreerd met HDInsight voor big data-analyses via Apache Spark-taken. Zie voor meer informatie op Hallo Spark-Connector voor Azure Cosmos DB [een Spark-taak uitvoert met Cosmos DB en HDInsight](spark-connector.md).

## <a name="gaming"></a>Gaming
Hallo databaselaag is een belangrijk onderdeel van games. Moderne games grafische verwerking op clients mobile-console uitvoeren, maar afhankelijk zijn van Hallo cloud toodeliver aangepast en gepersonaliseerde inhoud, zoals in het spel statistieken, sociale media-integratie en hoge-score scoreborden. Games vaak vereisen één milliseconde latenties voor leest en schrijft tooprovide een aantrekkelijke in game-ervaring. Een game database moet toobe snel en kunnen toohandle grote pieken in tarieven voor aanvraag tijdens nieuwe spel wordt gestart en functie-updates.

Azure Cosmos-database wordt gebruikt door games zoals [Hallo roulatie van inactieve: Nee Man van Land](https://azure.microsoft.com/blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/) door [volgende Games](http://www.nextgames.com/), en [Halo 5: voogden](https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/). Azure Cosmos DB biedt Hallo volgende voordelen biedt voor ontwikkelaars toogame:

* Azure Cosmos DB kunt prestaties toobe geschaald omhoog of omlaag elastisch. Hierdoor games toohandle bijwerken profiel en statistieken van tientallen toomillions van gelijktijdige gamers doordat één API-aanroep.
* Azure DB Cosmos ondersteunt milliseconde leest en schrijft toohelp te voorkomen dat een lag tijdens het spel.
* Azure Cosmos-DB automatisch indexeren kunt u filteren op meerdere verschillende eigenschappen in realtime, bijvoorbeeld vinden spelers door hun interne player-id's of hun GameCenter, Facebook, Google-id's of query op basis van lidmaatschap in een vereniging player. Dit is mogelijk zonder het bouwen van complexe te indexeren of sharding-infrastructuur.
* Sociale functies zoals in het spel chatberichten, player vereniging lidmaatschappen uitdagingen voltooid, hoge-score scoreborden en sociale grafieken zijn eenvoudiger tooimplement met een flexibele schema.
* Azure Cosmos-database als een beheerde platform-as-a-service (PaaS) vereist minimale installatie en beheer werk tooallow voor snelle herhaling en tijd toomarket beperken.

![Azure DB Cosmos gaming-referentiearchitectuur](./media/use-cases/gaming.png)

## <a name="web-and-mobile-applications"></a>Web- en mobiele toepassingen
Azure Cosmos DB wordt meestal gebruikt in de web- en mobiele toepassingen en is geschikt voor het modelleren van sociale interacties integreren met de services van derden en voor het bouwen van uitgebreide persoonlijke ervaring. Hallo Cosmos DB SDK's kan worden gebruikte build uitgebreide iOS en Android-toepassingen met behulp van populaire Hallo [Xamarin framework](mobile-apps-with-xamarin.md).  

### <a name="social-applications"></a>Sociale toepassingen
Een algemene gebruiksvoorbeeld voor Azure DB die Cosmos is toostore en query gebruiker gegenereerde inhoud (UGC) voor webtoepassingen, mobiele en sociale media-toepassingen. Enkele voorbeelden van UGC zijn chat-sessies, tweets blogberichten, classificaties en opmerkingen. Hallo UGC in toepassingen met sociale media is vaak een combinatie van vrije tekst, eigenschappen, labels en relaties die niet beperkt rigid structuur tot zijn. Inhoud zoals Chat, opmerkingen en berichten kunnen worden opgeslagen in Cosmos DB zonder transformaties of complexe object toorelational toewijzing lagen.  Data-eigenschappen kunnen worden toegevoegd of gewijzigd eenvoudig toomatch vereisten zoals ontwikkelaars toepassingscode hello doorlopen, dus promoveren snelle ontwikkeling.  

Toepassingen die zijn geïntegreerd met sociale netwerken van derden moeten toochanging schema's van deze netwerken reageren. Als de gegevens wordt in Cosmos DB standaard automatisch geïndexeerd, zijn gegevens gereed toobe opgevraagd op elk gewenst moment. Deze toepassingen hebben daarom Hallo flexibiliteit tooretrieve projecties volgens hun respectieve behoeften.

Veel van sociale Hallo-toepassingen uitvoeren op globale schaal en onvoorspelbare gebruikspatronen kunnen vertonen. Flexibiliteit toe voor het schalen van Hallo-gegevensarchief is essentieel tijdens Hallo toepassingslaag toomatch gebruiksvereisten schalen.  U kunt uitbreiden door aanvullende gegevenspartities onder een Cosmos-DB-account toe te voegen.  Bovendien kunt u ook aanvullende Cosmos-DB-accounts maken in meerdere regio's. Zie voor de beschikbaarheid van een Cosmos-DB service regio [Azure-gebieden](https://azure.microsoft.com/regions/#services).

![Azure DB Cosmos web-app-referentiearchitectuur](./media/use-cases/apps-with-global-reach.png)

### <a name="personalization"></a>Personalisatie
Tegenwoordig moderne toepassingen worden geleverd met complexe weergaven en ervaringen. Dit zijn doorgaans dynamisch is, catering toouser voorkeuren of stemming en huisstijl behoeften. Daarom toepassingen toobe kunnen tooretrieve van persoonlijke instellingen moeten effectief toorender UI-elementen en ervaringen snel. 

JSON, een indeling die wordt ondersteund door Cosmos DB, is een effectieve indeling toorepresent UI lay-outgegevens, zoals het is niet alleen lichtgewicht, maar ook kan worden eenvoudig geïnterpreteerd door JavaScript. Cosmos DB biedt instelbare consistentieniveaus waarmee snelle Lees met lage latentie voor schrijfbewerkingen. Daarom opslaan UI lay-outgegevens met inbegrip van persoonlijke instellingen JSON-documenten in Cosmos-database is een effectieve manier tooget deze gegevens via de kabel Hallo.

![Azure DB Cosmos web-app-referentiearchitectuur](./media/use-cases/personalization.png)

## <a name="next-steps"></a>Volgende stappen
de slag met Azure Cosmos DB tooget Volg ons [snel aan de slag](create-documentdb-dotnet.md), die helpt u bij het maken van een account en aan de slag met Cosmos-DB. 

Of als u meer informatie over de klanten die gebruikmaken van de Cosmos-DB tooread, hello volgende ervaringen van klanten zijn beschikbaar:

* [Jet.com](https://jet.com). E-commerce uitdager ogen Hallo bovenste positie, wordt uitgevoerd op Hallo Microsoft cloud, maakt gebruik van de Cosmos-database op een wereldwijde schaal.
* [Asos.com](http://www.asos.com/). Asos.com is een Brits wijze en voordeel onlinewinkel. Asos is voornamelijk bedoeld voor jonge volwassenen, verkoopt meer dan 850 merken, evenals een eigen reeks kleding en accessoires.
* [Toyota](https://www.toyota.com/). Toyota Motor Corporation is een Japanse auto fabrikant. Cosmos DB Toyota gebruikt voor een algemene IoT-app.
* [Citrix](https://customers.microsoft.com/story/citrix). Citrix ontwikkelt eenmalige aanmelding oplossing met behulp van Azure Service Fabric en Azure Cosmos-DB
* [TEXA](https://customers.microsoft.com/story/texaspa) van TEXA revolutionaire IoT-oplossing voor eigenaren van vehicle bespaart u tijd, geld, gas, en mogelijk.
* [De Domino Pizza](https://www.dominos.com). De Domino Pizza Inc. is een restaurant American pizza keten.
* [Hiermee bepaalt u Johnson](http://www.johnsoncontrols.com). Johnson Controls is een globale gediversifieerde technologie en meerdere industriële opvulteken voor een breed scala aan klanten in meer dan 150 landen.
* [Microsoft Windows, Universal Store Azure IoT Hub, Xbox Live en andere services Internet scale](https://azure.microsoft.com/blog/how-azure-documentdb-planet-scale-nosql-helps-run-microsoft-s-own-businesses/). Hoe Microsoft sterk schaalbare services met behulp van Azure DB die Cosmos maakt.
* [Microsoft Data en analyses team](https://customers.microsoft.com/story/microsoftdataandanalytics). Microsoft team van gegevens en Analytics realiseert wereld scale big data-verzameling met Azure Cosmos-DB
* [Sulekha.com](https://customers.microsoft.com/story/sulekha-uses-azure-documentdb-to-connect-customers-and-businesses-across-india). Sulekha gebruikt Azure Cosmos DB tooconnect klanten en bedrijven op India.
* [NewOrbit](https://customers.microsoft.com/story/neworbit-takes-flight-with-azure-documentdb). NewOrbit duurt vlucht met Azure Cosmos DB.
* [Affinio](https://customers.microsoft.com/doclink/affinio-switches-from-aws-to-azure-documentdb-to-harness-social-data-at-scale). Affinio verandert van AWS tooAzure Cosmos DB tooharness sociale gegevens op grote schaal.
* [Naast Games](https://azure.microsoft.com//blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/). Hallo wandel onbestelbare: Man van Land game soars te #1 wordt ondersteund door Azure Cosmos DB.
* [Halo](https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/). Hoe Halo 5 sociale spelen met behulp van Azure DB die Cosmos geïmplementeerd.
* [Cortana-Analytics galerie](https://azure.microsoft.com/blog/cortana-analytics-gallery-a-scalable-community-site-built-on-azure-documentdb/). Cortana Analytics Gallery - een communitysite schaalbare is gebouwd op Azure Cosmos DB.
* [Eenvoudig](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18602). Voorloopspaties Integrator geeft meertalige ondernemingen globale inzicht in minuten met flexibele Cloudtechnologieën.
* [Nieuws Republiek](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18639). Toohello nieuws tooprovide bedrijfsinformatie met als doel voor de betrokken burgers toevoegen. 
* [BG's International](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18653). Belangrijke merken inschakelen voor consistente kleur over Hallo wereld tooSGS. En schakelt u tooAzure BG's.
* [Telenor](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18608). Globale opvulteken Telenor gebruikt Hallo cloud toomove met Hallo snelheid van een opstarten. 
* [XOMNI](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18667). Hallo-archief met Hallo toekomstige wordt uitgevoerd op een snelle, zoeken en Hallo eenvoudig stroom van gegevens.
* [Nucleo](https://customers.microsoft.com/story/azure-based-software-platform-breaks-down-barriers-bet). Op basis van een Azure-softwareplatform uitvalt barrières tussen bedrijven en klanten
* [Weka](https://customers.microsoft.com/story/weka-smart-fridge-improves-vaccine-management-so-more-people-can-be-protected-against-diseases). Smart koelkast weka verbetert vaccin beheer zodat meer gebruikers kunnen worden beveiligd tegen ziekten
* [Oranje Tribes](https://customers.microsoft.com/story/theres-more-to-that-food-app-than-meets-the-eye-or-the-mouth). Er is meer toothat voeding app dan voldoet aan of Hallo mond Hallo ogen.
* [Echte Madrid](https://customers.microsoft.com/story/real-madrid-brings-the-stadium-closer-to-450-million-f). Echte Madrid brengt Hallo stadium dichter too450 miljoen ventilatoren hele Hallo wereld, hello Microsoft Cloud.
* [Tuku](https://customers.microsoft.com/story/tuku-makes-car-buying-fun-with-help-from-azure-services). TUKU maakt auto kopen plezier met behulp van Azure-services

---
title: aaaCortana Intelligence oplossing sjabloon Playbook voor het voorspellen van de vraag van energie | Microsoft Docs
description: Een oplossingssjabloon met Microsoft Cortana Intelligence waarmee forecast aanvraag voor een bedrijf, energie-hulpprogramma.
services: cortana-analytics
documentationcenter: 
author: ilanr9
manager: ilanr9
editor: yijichen
ms.assetid: 8855dbb9-8543-45b9-b4c6-aa743a04d547
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2016
ms.author: ilanr9;yijichen;garye
ms.openlocfilehash: 32fc6ece7e24ced34282baf107548039694a38b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-template-playbook-for-demand-forecasting-of-energy"></a>Cortana Intelligence oplossing sjabloon Playbook voor het voorspellen van de vraag van energie
## <a name="executive-summary"></a>Managementsamenvatting
In Hallo voorbij jaren Internet der dingen (IoT) hebben alternatieve energie- en big data samengevoegde toocreate enorme mogelijkheden in Hallo hulpprogramma en de energie-domein. Op Hallo hebben hetzelfde moment, Hallo hulpprogramma en Hallo volledige energiesector verbruik plat uit met betere manieren toocontrol veeleisende consumenten hun gebruik van energie gezien. Daarom Hallo hulpprogramma en slimme raster bedrijven tooinnovate nodig zijn en zelf te vernieuwen. Bovendien veel hulpprogramma's en energiebeheer rasters worden steeds verouderde en kostbare toomaintain en beheren. Tijdens het afgelopen jaar hello werkt Hallo team op een aantal betrokkenheid binnen Hallo energie-domein. Er is veel gevallen utilities of ISV's (Independent Software Vendors) in welke Hallo in voorspellen voor toekomstige energie vraag is opzoeken tijdens deze betrokkenheid. Deze prognoses speelt een belangrijke rol in hun bedrijf huidige en toekomstige en Hallo fundering voor verschillende gebruiksvoorbeelden zijn geworden. Het gaat hierbij om korte en lange termijn power load prognose, handel, taakverdeling, raster optimalisatie, enzovoort. BIG data en geavanceerde analyses AA-methoden zoals Machine Learning (ML) zijn onderdelen mogelijk maken van Hallo voor het produceren van nauwkeurige en betrouwbare prognoses.  

In deze playbook we samenstellen Hallo bedrijfs- en analytische richtlijnen die nodig zijn voor een geslaagde ontwikkeling en implementatie van de vraag energie forecast oplossing. Deze voorgestelde richtlijnen kunnen u hulpprogramma's, gegevenswetenschappers en gegevens engineers volledig geoperationaliseerd, cloud-gebaseerde, voorspellen van de vraag oplossingen tot stand wordt gebracht. Voor de bedrijven die hun big data en geavanceerde analyses vervoer net beginnen, kan een dergelijke oplossing Hallo basiswaarde in hun langetermijnstrategie smart raster vertegenwoordigen.

> [!TIP]
> een diagram waarin u een overzicht van de architectuur van deze sjabloon bevat toodownload Zie [Cortana Intelligence oplossingssjabloon architectuur voor het voorspellen van de vraag van energie](cortana-analytics-architecture-demand-forecasting-energy.md).  
> 
> 

## <a name="overview"></a>Overzicht
Dit document bevat informatie over zakelijke hello, gegevens en technische aspecten van het gebruik van Cortana Intelligence en in bepaalde Azure Machine Learning (AML) voor de implementatie van energie prognose oplossingen en Hallo-implementatie. Hallo document bestaat uit drie hoofdonderdelen:  

1. Inzicht in het bedrijf  
2. Understanding Data  
3. Technische implementatie

Hallo **bedrijven inzicht** onderdeel overzichten Hallo business aspect één behoeften toounderstand en eerdere toomaking Overweeg een beslissing investering. Hierin wordt uitgelegd hoe tooqualify Hallo zakelijke probleem aan de hand tooensure predictive analytics en machine learning inderdaad effectieve en van toepassing zijn. verder Hallo document wordt uitgelegd Hallo basisprincipes van machine learning en hoe deze gebruikt tooaddress energie prognose problemen. Het bevat een overzicht Hallo vereisten en Hallo kwalificatiecriteria van een gebruiksvoorbeeld. Aantal voorbeelden gebruiken aanvragen en het bedrijfsscenario scenario's worden ook gegeven.

Gegevens zijn Hallo hoofdbestanddeel voor een machine learning-oplossing. Hallo **gegevens Understanding** deel van dit document bevat enkele belangrijke aspecten van Hallo-gegevens. Hierin wordt beschreven Hallo soort gegevens die nodig is voor de prognose energie, data quality vereisten en welke gegevensbronnen bestaan doorgaans. Ook wordt uitgelegd hoe Hallo onbewerkte gegevens gebruikte tooprepare gegevensfuncties die daadwerkelijk station Hallo modelleren onderdeel is.

Hallo derde onderdeel van Hallo document bevat informatie over Hallo **technische implementatie** aspect van een oplossing. Functie-engineering modellering Hallo kern van Hallo gegevens wetenschap proces en zijn daarom in sommige detail worden besproken. Het Hallo-concept van webservices een belangrijk medium voor cloudimplementatie van predictive analytics-oplossingen zijn worden behandeld. We een typische architectuur van een operationalized end-to-end-oplossing ook een overzicht.

Daarnaast bevat Hallo document referentiemateriaal dat u toogain meer inzicht in de Hallo domein en de technologie kunt gebruiken.

Het is belangrijk toonote dat er niet van plan toocover in dit document Hallo meer gedetailleerde gegevens wetenschap proces, de wiskundige en technische aspecten bent. Deze gegevens vindt u in [documentatie voor Azure ML](http://azure.microsoft.com/services/machine-learning/) en [blogs](http://blogs.microsoft.com/blog/tag/azure-machine-learning/).

### <a name="target-audience"></a>Doelgroep
Hallo doelgroep voor dit document is zowel zakelijke en technisch personeel die graag toogain kennis en inzicht in Machine Learning op basis van oplossingen en hoe deze worden gebruikt specifiek binnen Hallo energie prognose domein.

Gegevenswetenschappers kunnen ook profiteren van dit document toogain beter inzicht te krijgen van hoog niveau proces Hallo dat stations implementatie van een oplossing prognose energie Hallo lezen. Het kan ook gebruikte tooestablish een goede basis en startpunt voor meer gedetailleerde en materiaal geavanceerde zijn in deze context.

### <a name="industry-trends"></a>Trends van
In Hallo voorbij jaren hebben IoT, alternatieve energie en big data samengevoegde toocreate enorme mogelijkheden in Hallo hulpprogramma en de energie-ruimte. Op Hallo hebben hetzelfde moment, Hallo hulpprogramma en Hallo volledige energiesectoren verbruik plat uit met betere manieren toocontrol veeleisende consumenten hun gebruik van energie gezien.

Hallo is pioneering aan veel hulpprogramma en slimme energiebedrijven hebben [smart raster](https://en.wikipedia.org/wiki/Smart_grid) door het implementeren van een aantal gebruik gevallen die gebruik van Hallo gegevens die worden gegenereerd door Hallo raster. Veel gebruiksvoorbeelden gebaseerd op Hallo inherente kenmerken van elektriciteitsproductie: kan niet worden verzameld of gereserveerd als inventarisatie worden opgeslagen. Ja, wat wordt geproduceerd moet worden gebruikt. Hulpprogramma's die u wilt dat toobecome efficiënter moeten tooforecast energieverbruik gewoon omdat die deze meer mogelijkheden te krijgt**en aanbod in evenwicht**, waardoor wordt voorkomen dat energie verliezen, **handel verminderen uitstoot gas**, en beheerkosten.

Bij het bespreken van de kosten, is er een ander belangrijk aspect, de prijs is. Nieuwe mogelijkheden tootrade power tussen hulpprogramma's te hebben gebracht een nodig**voorspellen van toekomstige vraag en toekomstige prijs elektriciteit**. Hierdoor kunnen bedrijven hun omvang van de productie te bepalen.

Wanneer we Hallo word 'smart' gebruiken, verwijzen we daadwerkelijk tooa raster die u kunt meer informatie over de en voorspellingen. Kan het seizoen wijzigingen in het verbruik van verwacht, evenals **voorzien van tijdelijke overbelasting situaties en automatisch aanpassen voor**. Door op afstand reguleren verbruik (aan de hand van de Hallo van deze smartcard meters), kunnen gelokaliseerde overbelasting situaties worden verwerkt. **Door eerst voorspellen en vervolgens fungeert**, Hallo raster maakt zelf slimmer gedurende een bepaalde periode.

Voor de rest van dit document gaan we in op een specifieke reeks gebruiksvoorbeelden die betrekking hebben op voorspellen van toekomstige, Hallo korte termijn en op lange termijn energie-aanvraag. We werken al op deze gebieden een paar maanden en sommige kennis en vaardigheden dat wij tooproduce bedrijfstak hoogwaardige resultaten hebt verkregen. Andere toepassingen worden ook behandeld in Hallo-document in Hallo nabije toekomst.

## <a name="business-understanding"></a>Inzicht in het bedrijf
### <a name="business-goals"></a>Zakelijke doelstellingen
Hallo **energie Demo** streeft toodemonstrate een typische predictive analytics en machine learning-oplossing die kan worden geïmplementeerd in een korte periode. In het bijzonder is onze huidige focus over het inschakelen van energie vraag prognose oplossingen zodat de bedrijfswaarde kan snel worden gerealiseerd en worden gebruikt bij. Hallo-informatie in deze playbook kunt Hallo klant Hallo volgende doelstellingen te bereiken:

* Korte tijd toovalue van machine learning gebaseerde oplossing
* Mogelijkheid tooexpand een test gebruik case tooother gebruik gevallen of tooa breder bereik op basis van hun zakelijke behoeften
* Snel krijgen van Cortana Intelligence Suite productkennis

Met deze doelstellingen in gedachten beoogd deze playbook Hallo bedrijven en technische kennis die u helpt bij het bereiken van deze doelstellingen te bezorgen.

### <a name="power-load-and-demand-forecasting"></a>Power laden en het voorspellen van de vraag
Binnen Hallo energie-sector, kan er veel manieren besproken waarop vraag prognose kan helpen bedrijfsproblemen oplost. In feite kan voorspellen van de vraag worden overwogen Hallo fundering voor veel core gebruiksvoorbeelden in Hallo industrie. In het algemeen we twee soorten energie vraagprognoses beschouwen: korte en lange termijn. Elk criterium mag hebben een ander doel en gebruikmaken van een andere benadering. Hallo belangrijkste verschil tussen Hallo twee is Hallo horizon, wat betekent dat Hallo tijdsbereik in toekomstige Hallo waarvoor we zou forecast prognose.

#### <a name="short-term-load-forecasting"></a>Voor de korte termijn Load prognose
Korte termijn laden prognose (STLF) wordt in de context van de Hallo van energie-aanvraag gedefinieerd als Hallo geaggregeerde belasting die wordt een prognose in Hallo nabije toekomst op verschillende onderdelen van Hallo raster (of Hallo raster als geheel). In deze context is korte termijn gedefinieerde toobe periode binnen het bereik van 1 uur too24 uur Hallo. In sommige gevallen is er ook een periode van 48 uur mogelijk. Daarom is STLF heel gebruikelijk in een operationele gebruiksvoorbeeld van Hallo raster. Hier volgen enkele voorbeelden van STLF aangestuurd gebruiksvoorbeelden:

* Vraag en aanbod Netwerktaakverdeling
* Handelspartners ondersteuning voor energiebeheer
* Markt maken (instelling power prijs)
* Raster operationele optimalisatie
* [Vraag antwoord](https://en.wikipedia.org/wiki/Demand_response)
* Pieksnelheden voorspellen van de vraag
* Vraag aan clientzijde management
* Taakverdeling en preventie van de overbelasting
* Lange termijn Load prognose
* Detectie van fouttolerantie en afwijkingsdetectie
* Piek inperking/herverdeling 

STLF model zijn voornamelijk gebaseerd op Hallo in de buurt van het verleden (laatste dag of week) gegevens over het verbruik en gebruik prognose temperatuur als een belangrijke manier. Het verkrijgen van nauwkeurige temperatuur forecast voor Hallo uur en too24 uur wordt steeds minder van een challenge nu dagen. Deze modellen zijn minder gevoelig tooseasonal patronen of trends voor lange termijn verbruik.

Er zijn ook SLTF oplossingen waarschijnlijk toogenerate groot aantal voorspelling aanroepen (serviceaanvragen) omdat ze zijn wordt aangeroepen op uurbasis en in sommige gevallen zelfs met een hogere frequentie. Het is ook heel gebruikelijk toosee stadium van de innesteling waar elke afzonderlijke onderstation of transformator wordt weergegeven als een model met zelfstandige en zijn daarom Hallo volume van de voorspelling aanvragen nog groter.

#### <a name="long-term-load-forecasting"></a>Lange termijn Load prognose
Hallo-doel van de lange termijn Load prognose (LTLF) is tooforecast power aanvraag met een periode die variëren van 1 week toomultiple maanden (en in sommige gevallen een aantal jaar). Dit bereik van de horizon is vooral van toepassing voor het plannen van investering gebruiksscenario's.

Voor de lange termijn scenario's is het belangrijk toohave van hoge kwaliteitsgegevens die betrekking heeft op een reeks van meerdere jaren (minimaal 3 jaar). Deze modellen wordt doorgaans periodieke patronen van historische gegevens Hallo uitpakken en gebruikmaken van externe predicators zoals als weer en klimaat patronen.

Het is belangrijk tooclarify die langer Hallo prognose horizon Hallo, Hallo minder nauwkeurig Hallo prognose mogelijk. Het is daarom belangrijk tooproduce die sommige intervallen vertrouwen samen met de werkelijke Hallo forecast waarmee mensen toofactor Hallo mogelijke variatie in hun planningsproces.

Aangezien Hallo verbruik scenario voor LTLF is voornamelijk planning, verwachten we veel lagere voorspelling volumes (als vergeleken tooSTLF). We deze voorspellingen in visualisatie's zoals Excel of Power BI embedded standaard wordt weergegeven en handmatig door de gebruiker Hallo worden aangeroepen.

### <a name="short-term-vs-long-term-prediction"></a>Korte termijn vs. Voorspelling van de lange termijn
Hallo volgende tabel vergelijkt STLF en LTLF in verband toohello meest belangrijke kenmerken:

| Kenmerk | Korte termijn Load Forecast | Lange termijn Load prognose |
| --- | --- | --- |
| Prognose Horizon |1 uur too48 uur |Vanaf 1 too6 maanden of meer |
| Samenvattingen van gegevens |Elk uur |Elk uur of dagelijks |
| Typische gebruiksvoorbeelden |<ul><li>Vraag/aanbod Netwerktaakverdeling</li><li>Kies uur prognose</li><li>Vraag antwoord</li></ul> |<ul><li>Lange termijn planning</li><li>Raster activa plannen</li><li>Resourceplanning</li></ul> |
| Typische variabelen |<ul><li>Dag of week</li><li>Uur van dag</li><li>Temperatuur per uur</li></ul> |<ul><li>Maand van het jaar</li><li>Dag van de maand</li><li>Lange termijn temperatuur- en klimaat</li></ul> |
| Historische gegevensbereik |Twee toothree jaar aan gegevens |Vijf too10 jaar aan gegevens |
| Gemiddelde nauwkeurigheid |MAPE * van 5% of minder |MAPE * van 25% of minder |
| Prognose frequentie |Elk uur of elke 24 uur geproduceerd |Geproduceerd zodra per maand, kwartaal of jaar |

\*[MAPE](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error) – gemiddeld percentage fout betekent

Zoals blijkt uit deze tabel, is erg belangrijk toodistinguish tussen Hallo korte en lange termijn van Hallo prognose scenario's, omdat dit andere bedrijfsbehoeften vertegenwoordigen en verbruik patronen met een andere implementatie en wellicht.

### <a name="example-use-case-1-esmart-systems--overload-optimization"></a>Gebruiksvoorbeeld voorbeeld 1: eSmart systemen – overbelasting optimalisatie
Een belangrijke rol van een [smart raster](https://en.wikipedia.org/wiki/Smart_grid) toodynamically is en voortdurend te optimaliseren en voor verbruik patronen wijzigen Hallo aanpassen. Energieverbruik kan worden beïnvloed door op korte termijn wijzigingen die hoofdzakelijk worden veroorzaakt door temperatuur schommelingen (*bijvoorbeeld*, meer stroom wordt gebruikt voor lucht voorwaarde of verwarming). AT Hallo dezelfde tijd, energiebeheer verbruik wordt ook beïnvloed door de trends op lange termijn. Deze kunnen seizoensgebonden effecten, feestdagen op lange termijn groei van de consumptie en zelfs economische factoren zoals consumer index olie en bbp bevatten.

In dit geval gebruik [eSmart](http://www.esmartsystems.com/) toodeploy cloud-gebaseerde oplossing waarmee Hallo investeringsneiging voorspellen van de overbelasting van Hallo raster op een gegeven onderstation wilden. In het bijzonder wilde eSmart tooidentify onderstations die waarschijnlijk toooverload binnen Hallo uur, zodat een onmiddellijke actie tooavoid kan worden uitgevoerd of die situatie oplossen.

Een nauwkeurige en snel uitvoeren voorspelling vereist de implementatie van de drie voorspellende modellen:

* Lange termijn model dat Hiermee prognose van het energieverbruik op elke onderstation tijdens Hallo volgende enkele weken of maanden
* Korte termijn model waarmee voorspelling van overbelasting op een gegeven onderstation tijdens Hallo uur
* Temperatuur model waarmee voorspellen van toekomstige temperatuur via meerdere scenario 's

Hallo-doel van Hallo op lange termijn model is toorank Hallo onderstations door hun investeringsneiging toooverload (toegekend hun verzending energiecapaciteit) tijdens het Hallo volgende week of maand. Hierdoor Hallo maken van een korte lijst met onderstations die als invoer voor de korte termijn voorspelling Hallo bedienen. Zoals temperatuur een belangrijke manier voor de lange termijn model hello is, er is een noodzaak tooconstantly produceren meerdere scenario temperatuur prognoses en ze als invoer in de lange termijn model toohello feed. de korte termijn Hallo prognose wordt vervolgens aangeroepen toopredict welke onderstation waarschijnlijk toooverload via Hallo volgende uur is.

Hallo korte en lange termijn modellen worden afzonderlijk per elke onderstation geïmplementeerd. Daarom vereist Hallo praktische uitvoering van deze modellen uitgebreide orchestration. voor elk uur van de dag Hallo toogain hogere nauwkeurigheid op Hallo korte termijn, een meer gedetailleerd model is gereserveerd. Alle deze modellen worden elk uur uitgevoerd en worden uitgevoerd binnen een paar minuten tooallow voldoende tijd toorespond voltooien en preventieve maatregelen indien nodig. Deze verzameling van modellen wordt bijgewerkt door periodieke retraining met behulp van de meest recente gegevens Hallo.

Meer informatie over deze gebruiksvoorbeeld vindt [hier](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18945).

#### <a name="use-case-qualification-criteria--prerequisites"></a>Gebruik Case kwalificatiecriteria: vereisten
Hallo belangrijkste sterkte van Cortana Intelligence is in de krachtige mogelijkheid toodeploy en schaal machine learning gericht oplossingen. Het is ontworpen toosupport duizendtallen van voorspellingen die gelijktijdig worden uitgevoerd. Deze kan toomeet een veranderende verbruik patroon automatisch schalen. Een oplossing focus is daarom op de nauwkeurigheid en de computerprestaties. Bijvoorbeeld, is een bedrijf hulpprogramma geïnteresseerd in het opstellen van nauwkeurige energie-vraag prognose voor Hallo uur en voor elk uur van de dag Hallo. Op Hallo daarentegen, we minder geïnteresseerd bent in het beantwoorden van vraag waarin wordt uitgelegd waarom Hallo vraag voorspelde toobe omdat deze hello (Hallo model zelf zorgt voor die).

Het is daarom belangrijk toorealize dat niet alle gebruiksvoorbeelden en zakelijke problemen effectief kunnen worden opgelost met behulp van machine learning.

Cortana Intelligence en machine learning mogelijk zeer effectieve bij het oplossen van een bepaalde zakelijke probleem wanneer Hallo volgende criteria wordt voldaan:

* Hallo zakelijke probleem in de hand is **voorspellende** aard. Een voorbeeld van een Voorspellend gebruik case is een hulpprogramma bedrijf die graag toopredict power belasting van een bepaalde onderstation tijdens Hallo uur. Op Hallo daarentegen, analyseren en classificeren van stuurprogramma's van de historische vraag zou worden **beschrijvende** van aard en bijgevolg minder van toepassing.
* Er is een duidelijke **pad van de actie** toobe genomen eenmaal Hallo voorspelling beschikbaar is. Bijvoorbeeld, het voorspellen van een overbelasting op een onderstation tijdens Hallo uur een proactieve actie van de belasting die is gekoppeld aan die onderstation verminderen en zo mogelijk te voorkomen dat een overbelasting activeren.
* Hallo gebruiksvoorbeeld vertegenwoordigt een **typische type probleem** zo dat als opgelost het Hallo manier toosolving andere vergelijkbare gebruiksvoorbeelden kunt vrijmaken.
* Hallo klant kunt instellen **kwalitatieve en kwantitatieve doelstellingen** toodemonstrate een oplossing voor geslaagde implementatie. Een goede kwantitatief doel voor energie vraagprognose zou bijvoorbeeld Hallo vereiste nauwkeurigheid drempelwaarde (*bijvoorbeeld*, up too5% is een fout is toegestaan) of wanneer het voorspellen van onderstation overbelasting vervolgens Hallo precision (percentage van de waarde true positieven) en intrekken (mate van true positieven) moet hoger dan een opgegeven drempelwaarde. Deze doelstellingen moeten zijn afgeleid van van de klant Hallo zakelijke doelstellingen.
* Er is een duidelijke **integratiescenario** met van het bedrijf Hallo zakelijke werkstroom. Hallo onderstation load prognose kan bijvoorbeeld worden geïntegreerd in Hallo raster center tooallow overbelasting preventie controleactiviteiten.
* Hallo klant heeft gereed toouse **gegevens met voldoende kwaliteit** toosupport Hallo gebruiksvoorbeeld (Zie voor meer informatie in de volgende sectie hello, **gegevenskwaliteit**, van deze playbook).
* Hallo klant hebben gericht gegevens cloudarchitectuur of **cloud-gebaseerde machine learning**, met inbegrip van Azure ML en andere onderdelen Cortana Intelligence Suite.
* Hallo klant is bereid tooestablish **de gegevensstroom van een end-tooend** opslagruimten Hallo levering van gegevens in de cloud Hallo voortdurend en bereid is te**operationeel** Hallo oplossing.
* Hallo klant is gereed te**toe te wijzen aan resources** toohello klant bij geslaagd die zal worden actief ingeschakeld tijdens de eerste test implementatie Hallo zodat kennis en eigendom van Hallo oplossing kunnen worden overgedragen voltooiing.
* Hallo klant bron moet een **ervaren gegevens professional**, bij voorkeur een wetenschappelijk gegevens.

Eis van een gebruiksvoorbeeld op basis van Hallo bovenstaande criteria kan aanzienlijk verbeteren Hallo succespercentages van een gebruiksvoorbeeld en tot stand brengen van een goede beachhead voor toekomstig gebruik gevallen Hallo-implementatie.

### <a name="cloud-based-solutions"></a>Cloud-gebaseerde oplossingen
Cortana Intelligence Suite in Azure is een geïntegreerde omgeving die zich in de cloud Hallo bevindt. Hallo-implementatie van een oplossing voor geavanceerde analyses in een cloudomgeving bevat aanzienlijke voordelen voor bedrijven en op Hallo hetzelfde moment kan betekenen dat big wijziging voor bedrijven die nog steeds on-premises gebruiken IT-oplossingen. Er is een duidelijke trend van geleidelijke migratie van bewerkingen in de cloud Hallo binnen Hallo energie-sector. Deze trend gaat gepaard samen met de Hallo ontwikkeling van Hallo smart raster zoals beschreven in bovenstaande **Trends van**. Zoals deze playbook is gericht op een cloud-gebaseerde oplossing in Hallo energie-domein, is het belangrijk tooexplain Hallo voordelen en andere overwegingen voor het implementeren van een cloud-gebaseerde oplossing.

Misschien hello grootste voordeel van een cloud-gebaseerde oplossing is Hallo kosten. Als een oplossing maakt gebruik van cloud geïmplementeerd onderdelen, er is geen opstartkosten of onderdeelkosten omzet (kosten van de omzet) gekoppeld. Dat betekent dat er geen noodzaak tooinvest in hardware, software en het onderhoud van IT, en dus er een aanzienlijke vermindering van bedrijfsrisico is.

Een ander belangrijk voordeel is Hallo betalen naar gebruik kostenstructuur van de cloud gebaseerde oplossingen. Cloud-gebaseerde servers voor computing of de opslag kunnen worden geïmplementeerd en worden geschaald op basis van just-nodig. Hiermee wordt Hallo kosten efficiëntie profiteren van een cloud-gebaseerde oplossing.

Er is ten slotte niet nodig voor het investeren in de IT-onderhoud of toekomstige infrastructuurontwikkeling, omdat deze deel uitmaakt van Hallo cloudaanbieding. toothat mate, Cortana Intelligence Suite bevat Hallo beste in klasse services en de routekaart houdt in ontwikkeling. Nieuwe functies, onderdelen en -mogelijkheden zijn voortdurend geïntroduceerd en ontwikkelen.

Voor een bedrijf dat de overgang naar Hallo cloud nog wordt gestart, bevelen maximaal we tootake een geleidelijke aanpak door het implementeren van een routekaart voor cloud-migratie. We zijn ervan overtuigd dat de Hallo gebruiksvoorbeelden die worden beschreven in deze playbook voor hulpprogramma's en bedrijven in Hallo energie-domein, een uitstekende gelegenheid voor het testen van predictive analytics-oplossingen in de cloud Hallo vertegenwoordigen.

#### <a name="business-case-justification-considerations"></a>Overwegingen voor zakelijke rechtvaardiging voor de aanvraag
In veel gevallen Hallo klant mogelijk geïnteresseerd zijn bij het maken van een zakelijke rechtvaardiging voor een bepaalde gebruiksvoorbeeld waarin een cloud-gebaseerde oplossing en Machine Learning belangrijke onderdelen zijn. In tegenstelling tot een on-premises-oplossing, in geval van een oplossing cloud-gebaseerde Hallo Hallo vooraf kosten onderdeel minimale is en de meeste Hallo kostenelementen zijn gekoppeld aan het werkelijke gebruik. Wanneer deze een oplossing op Cortana Intelligence Suite prognose energie toodeploying wordt, kunnen meerdere services kunnen worden geïntegreerd met een enkele algemene kostenstructuur. Bijvoorbeeld: databases (*bijvoorbeeld*, SQL Azure) kan gebruikte toostore Hallo onbewerkte gegevens en vervolgens voor Hallo werkelijke prognoses Azure ML is gebruikte toohost Hallo prognose services. In dit voorbeeld kan Hallo structuur kosten opslag en transactionele onderdelen bevatten.

Op Hallo daarentegen moet één een goed begrip van Hallo zakelijke voordelen van het besturingssysteem van een energie-vraag prognose (korte of lange termijn) hebben. Het is in feite belangrijk toorealize Hallo bedrijfswaarde van elke bewerking van de prognose. Bijvoorbeeld nauwkeurige prognose power belasting voor Hallo binnen 24 uur kunt voorkomen dat overproduction of overloads op Hallo raster kan voorkomen en dit kan worden bepaalde in termen van financiële besparingen dagelijks.

Een eenvoudige formule voor het berekenen van financiële voordeel van de vraag Hallo forecast oplossing: ![Basic formule voor het berekenen van financiële voordeel van de vraag Hallo forecast oplossing](media/cortana-analytics-playbook-demand-forecasting-energy/financial-benefit-formula.png)

Aangezien Cortana Intelligence Suite een betalen naar gebruik prijsmodel biedt, hoeft niet voor een vaste kosten onderdeel toothis formule aangaan. Deze formule kan worden berekend op basis van dagelijks, maandelijks of jaarlijks.

Huidige Cortana Intelligence Suite en Azure ML prijsstelling vindt [hier](http://azure.microsoft.com/pricing/details/machine-learning/).

### <a name="solution-development-process"></a>Ontwikkelingsproces oplossing
Hallo ontwikkelingscyclus van een energie-vraag prognose oplossing omvat doorgaans 4 fasen, die allemaal we maken gebruik van cloud-gebaseerde technologieën en services binnen Hallo Cortana Intelligence Suite.

Dit wordt geïllustreerd in het volgende diagram Hallo:

![Smart raster cyclus](media/cortana-analytics-playbook-demand-forecasting-energy/smart-grid-cycle.png)

Hallo na alinea beschrijft het proces van deze stap 4:

1. **Gegevensverzameling** – een geavanceerde gebaseerd analytics-oplossing is afhankelijk van de gegevens (Zie **gegevens Understanding**). In het bijzonder wanneer deze wordt toopredictive analytics en prognoses, wij zijn afhankelijk van continue, dynamische stroom van gegevens. In geval van het voorspellen van de vraag energie Hallo deze gegevens kan afkomstig zijn direct vanaf smart meters of al op een on-premises-database worden geaggregeerd. Er is ook afhankelijk van andere externe gegevensbronnen zoals weer en temperatuur. Deze continue stroom van gegevens moet worden beheerd, gepland en opgeslagen. [Azure Data Factory](http://azure.microsoft.com/services/data-factory/) (ADF) is onze belangrijkste werkpaard voor het uitvoeren van deze taak.
2. **Modeling** : voor nauwkeurige en betrouwbare energie prognoses, moet een ontwikkelen (train) en een geweldige model waarmee het gebruik van historische gegevens Hallo en uitgepakt Hallo zinvolle onderhouden en voorspellende patronen in Hallo gegevens. Hallo-gebied van Machine Learning (ML) heeft groeien snel met meer geavanceerde algoritmen die regelmatig worden ontwikkeld. Azure ML Studio biedt een goede gebruikerservaring die gebruikmaken van de meest geavanceerde algoritmen ML binnen een werkstroom voltooid Hallo helpt. Werkstroom wordt weergegeven in een intuïtieve stroomdiagram en Hallo gegevens voorbereiden, het ophalen van functies, modellering en evaluatie van het model bevat. Hallo-gebruiker kunt ophalen in honderden verschillende modellen die zijn opgenomen in deze omgeving. Hallo-einde van deze fase hebben een wetenschappelijk gegevens een werkmodel die volledig geëvalueerd en klaar voor implementatie.
   
   Hallo volgende diagram wordt een afbeelding van een gangbare werkstroom:
   
   ![Modellering van een werkstroom](media/cortana-analytics-playbook-demand-forecasting-energy/modeling-workflow.png)
3. **Implementatie** – met een werkmodel in kant Hallo volgende stap is voor implementatie. Hier wordt Hallo model geconverteerd naar een webservice die een RESTful-API die gelijktijdig kunnen worden aangeroepen via Internet Hallo van verschillende verbruik clients beschrijft. Azure ML biedt een eenvoudige manier voor het implementeren van een model rechtstreeks vanuit hello Azure ML Studio met één klik een knop. de volledige implementatieproces Hallo gebeurt achter de schermen Hallo. Deze oplossing kunt toomeet Hallo vereist verbruik automatisch schalen.
4. **Verbruik** : In deze fase, maken we daadwerkelijk Hallo prognose model tooproduce voorspellingen gebruiken. Hallo-verbruik van de toepassing van een gebruiker kan worden bepaald (*bijvoorbeeld*, dashboard) of rechtstreeks van een operationeel systeem zoals vraag/aanbod balancing systeem of een raster optimalisatie-oplossing. Meerdere gebruiksmogelijkheden kunnen uit één model worden aangestuurd.

## <a name="data-understanding"></a>Understanding Data
Na die betrekking hebben op Hallo business overwegingen (Zie **bedrijven inzicht**) van een energie-vraag prognose oplossing, we zijn nu gereed toodiscuss Hallo gegevensonderdeel. Een predictive analytics-oplossing is afhankelijk van betrouwbare gegevens. Voor het voorspellen van energie de vraag, afhankelijk wij zijn van historische verbruiksgegevens met verschillende detailniveaus. Historische gegevens wordt gebruikt als Hallo grondstoffen. Deze worden onderworpen aan een zorgvuldige analyse in welke Hallo identificeert gegevens wetenschappelijk variabelen (ook waarnaar wordt verwezen tooas functies) die in een model die uiteindelijk Hallo vereist prognoses genereert kunnen worden geplaatst.

In de rest van de Hallo van deze sectie, maar wij beschrijven Hallo verschillende stappen en overwegingen voor Hallo gegevens inzicht en hoe toobring het tooa bruikbare vorm.

### <a name="hello-model-development-cycle"></a>Hallo ontwikkelingscyclus Model
Het opstellen van goede prognose modellen vereist zorgvuldige voorbereiding en planning. Splitsen Hallo proces modelleren in meerdere stappen en gericht op één stap tegelijk kan aanzienlijk te verbeteren Hallo resultaat van het hele proces Hallo.

Hallo volgende diagram illustreert hoe Hallo modelleren proces kan worden onderverdeeld in meerdere stappen:

![Model ontwikkelingscyclus](media/cortana-analytics-playbook-demand-forecasting-energy/model-development-cycle.png)

Zoals te zien Hallo cyclus bestaat uit zes stappen uitvoeren:

* Probleem formulering
* Gegevensopname en verkennen
* Voorbereiden van gegevens en functie-engineering
* Modelleren
* Model-evaluatie
* Ontwikkeling

In de rest van deze sectie Hallo wordt Hallo afzonderlijke stappen en items tooconsider bij elke stap beschreven.

### <a name="problem-formulation"></a>Probleem formulering
We kunnen de Hallo probleem formulering rekening te houden bij het Hallo meest kritieke stap één moet eerdere tooimplementing tootake een predictive analytics-oplossing. We zouden hier transformeren Hallo zakelijke probleem en het toospecific-elementen die kunnen worden opgelost door middel van gegevens technieken afbreken. Het is raadzaam om tooformulate Hallo probleem als een reeks vragen willen we graag tooanswer. Hier volgen enkele mogelijke vragen die mogelijk van toepassing binnen Hallo bereik van het voorspellen van de vraag energie:

* Wat is de belasting van de Hallo verwacht op een afzonderlijke onderstation in Hallo volgende uur of dag?
* Op welk tijdstip Hallo mijn raster merken pieken?
* Hoe waarschijnlijk is mijn piekbelasting raster toosustain Hallo verwacht?
* Hoeveel energie moet Hallo power station genereren tijdens elk uur van de dag Hallo?

Het opstellen van deze vragen kan wij toofocus op de juiste gegevens Hallo ophalen en implementeren van een oplossing die volledig is afgestemd op Hallo zakelijke probleem bij de hand. Bovendien kunnen we enkele belangrijke metrische gegevens die kunnen we de prestaties van de tooevaluate Hallo van Hallo model wordt ingesteld. Bijvoorbeeld hoe nauwkeurig moet Hallo prognose worden en wat is Hallo bereik van de fout die nog steeds door Hallo bedrijf aanvaardbaar zijn?

### <a name="data-sources"></a>Gegevensbronnen
Hallo moderne smart raster verzamelt gegevens uit verschillende onderdelen en -onderdelen van Hallo raster. Deze gegevens vertegenwoordigt verschillende aspecten van Hallo bewerking en gebruik van Hallo power raster Hallo. Binnen het bereik van de Hallo van Hallo energie vraag prognose, zijn we Hallo bespreking van de gegevensbronnen die overeenkomen met Hallo werkelijke vraag verbruik te beperken. Een belangrijke bron van het energieverbruik zijn smart meters. Hulpprogramma's voor hele Hallo wereld implementeert snel smart meters voor hun consumenten. Smart meters Hallo werkelijke energieverbruik vastleggen en dit bedrijf gegevens back toohello hulpprogramma voortdurend relay. Gegevens worden verzameld en verzonden terug op een vast interval, variërend van elke 5 minuten too1 uur. Meer geavanceerde smart meters extern kunnen worden geprogrammeerd toocontrol en saldo Hallo werkelijke verbruik binnen een huishouden. Smart meter gegevens is relatief betrouwbare en een tijdstempel bevat. Dat is het belangrijk ingrediënt voor vraag prognose. Gegevens van de meter kan worden geaggregeerd (getotaliseerde) op verschillende niveaus binnen Hallo raster-topologie: transformator, onderstation, regio, *enzovoort*. We kunnen vervolgens Hallo vereist aggregatie niveau toobuild een prognosemodel kiezen voor. Bijvoorbeeld als Hallo hulpprogramma bedrijf zoals tooforecast toekomstige op elk van de rasterlijnen onderstations laden zou kunnen vervolgens alle meters gegevens worden samengevoegd voor elke afzonderlijke onderstation en gebruikt als invoer voor Hallo prognose model. We verwijzen toosmart meters als een interne gegevensbron.

Een aanvraag betrouwbare energie prognose vertrouwt ook op andere externe gegevensbronnen. Een belangrijke factor die invloed heeft op energieverbruik is Hallo weer of preciezer Hallo temperatuur. Historische gegevens vindt u nauwe correlatie tussen externe temperatuur- en energieverbruik. Hot zomer dagen, de consument maken gebruik van hun airconditioning en tijdens het Hallo winter inschakelen verwarming. Een betrouwbare bron van historische temperaturen op Hallo rasterlocatie is daarom sleutel. Bovendien afhankelijk we ook van nauwkeurige voorspelling van temperatuur energieverbruik te voorspellen.

Andere externe gegevensbronnen kunnen ook helpen bij het bouwen van prognosemodellen energie-aanvraag. Deze kunnen wijzigingen in de lange termijn klimaat, voordelige indexen bevatten (*bijvoorbeeld*, bbp), en andere. In dit document nemen niet we deze andere gegevensbronnen.

### <a name="data-structure"></a>De structuur van gegevens
Nadat gegevensbronnen te identificeren Hallo worden vereist, zou we zoals tooensure dat onbewerkte gegevens die zijn verzameld Hallo bevat corrigeren gegevensfuncties. prognosemodel toobuild een betrouwbare vraag, moeten we tooensure die verzamelde gegevens Hallo gegevenselementen die kunnen helpen bij het voorspellen van toekomstige vraag Hallo bevat. Hier volgen enkele basisvereisten betreffende Hallo gegevensstructuur (schema) van de onbewerkte gegevens Hallo.

Hallo onbewerkte gegevens bestaat uit rijen en kolommen. Elke meting wordt weergegeven als één rij met gegevens. Elke rij gegevens bevat meerdere kolommen (ook waarnaar wordt verwezen tooas functies of velden).

1. **Tijdstempel** – Hallo tijdstempelveld vertegenwoordigt Hallo werkelijke tijd waarop Hallo meting is geregistreerd. Het moet voldoen aan een van de algemene datum/tijd-indelingen Hallo. Zowel de datum en tijd onderdelen moeten worden opgenomen. In de meeste gevallen is niet nodig voor Hallo tijd toobe vastgelegd tot Hallo tweede niveau van granulatie. Het is belangrijk toospecify Hallo-tijdzone waarin Hallo gegevens worden geregistreerd.
2. **ID meten** -Hallo meter of Hallo meting apparaat in dit veld aangegeven. Dit kan is een categorische variabele en een combinatie van cijfers en tekens.
3. **Waarde van de consumptie** – dit is de werkelijke verbruik Hallo op een gegeven datum/tijd. Hallo-verbruik kan worden gemeten in kWh (kilowatt-hour) of een andere gewenste eenheden. Het is belangrijk toonote die maateenheid Hallo moet over alle metingen in Hallo gegevens consistent blijven. In sommige gevallen kan verbruik meer dan 3 power fasen worden opgegeven. In dat geval zou moeten we toocollect alle Hallo onafhankelijke verbruik fasen.
4. **Temperatuur** – Hallo temperatuur doorgaans worden verzameld van een onafhankelijke bron. Er moet echter compatibel is met gegevens over het verbruik Hallo. Hierbij is een tijdstempel zoals hierboven beschreven waarmee het toobe gesynchroniseerd met de werkelijke verbruiksgegevens Hallo. Hallo temperatuur waarde kan worden opgegeven in graden c of Fahrenheit, maar moet blijven consistent op alle metingen.
5. **Locatie –** Hallo locatieveld is meestal gekoppeld aan Hallo plaats waar Hallo temperatuur gegevens zijn verzameld. Worden kan weergegeven als een zip-code number of breedtegraad/lengtegraad (lat/lang)-indeling.

Hallo volgende tabellen ziet u voorbeelden van een goede gebruiks- en temperatuur gegevensindeling:

| **Datum** | **Tijd** | **ID van de meter** | **Fase 1** | **Fase 2** | **Fase 3** |
| --- | --- | --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |ABC1234 |7.0 |2.1 |5.3 |
| 7/1/2015 |10:00:01 |ABC1234 |7.1 |2.2 |4.3 |
| 7/1/2015 |10:00:02 |ABC1234 |6.0 |2.1 |4.0 |

| **Datum** | **Tijd** | **Locatie** | **Temperatuur** |
| --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |11242 |24.4 |
| 7/1/2015 |10:00:01 |11242 |24.4 |
| 7/1/2015 |10:00:02 |11242 |24.5 |

Zoals hierboven kan worden afgeleid, worden in dit voorbeeld 3 verschillende waarden voor verbruik die zijn gekoppeld aan 3 power fasen bevat. Houd er ook rekening mee dat Hallo datum en tijd velden worden gescheiden, maar ze kunnen ook worden gecombineerd in één kolom. In dit geval wordt Hallo locatie kolom weergegeven in een 5-cijferige postcode indeling en Hallo temperatuur in een zekere mate c-indeling.

### <a name="data-format"></a>Indeling van gegevens
Meest voorkomende gegevensopmaak Hallo zoals CSV, TSV JSON, kan worden ondersteund door Cortana Intelligence Suite *enzovoort*. Het is belangrijk dat gegevensindeling Hallo voor de volledige levenscyclus van project Hallo Hallo consistent blijft.

### <a name="data-ingestion"></a>Gegevensopname
Aangezien energie vraagprognose wordt voortdurend en vaak voorspeld, moet we ervoor zorgen dat de onbewerkte gegevens Hallo door middel van een solide en betrouwbare opname-proces stroomt. Hallo opname proces moet garanderen dat de onbewerkte gegevens Hallo beschikbaar is voor Hallo prognose proces tegelijk Hallo vereist. Dat betekent Hallo gegevens opname frequentie moet groter zijn dan Hallo prognose frequentie.

Bijvoorbeeld: als onze vraag prognose oplossing genereert een nieuwe prognose om 8:00 uur per dag moeten we tooensure die alle Hallo-gegevens die zijn verzameld tijdens de laatste Hallo opnieuw 24 uur volledig tot dat moment ingenomen is en tooeven Hallo opnemen afgelopen uur van gegevens.

In volgorde tooaccomplish, Cortana Intelligence Suite biedt verschillende manieren toosupport een betrouwbare gegevens opname-proces. Hiermee wordt meer gedetailleerd besproken Hallo **implementatie** gedeelte van dit document.

### <a name="data-quality"></a>Gegevenskwaliteit
Hallo onbewerkte gegevensbron die is vereist voor het uitvoeren van de aanvraag voor betrouwbare en nauwkeurige prognose moet voldoen aan de criteria van een aantal basisgegevens kwaliteit. Hoewel geavanceerde statistische methoden gebruikte toocompensate voor een aantal mogelijke gegevens kwaliteit probleem, moeten we nog steeds tooensure we zijn een aantal basisgegevens kwaliteit drempelwaarde overschrijden bij het ophalen van nieuwe gegevens. Hier volgen enkele overwegingen betreffende de kwaliteit van de onbewerkte gegevens:

* **Ontbrekende waarde** – verwijst deze situatie toohello wanneer bepaalde meting is niet verzameld. Hallo hier een eerste vereiste is dat Hallo ontbrekende waarde frequentie mag niet langer dan 10% voor een bepaalde periode. In geval een enkele waarde is het ontbrekende moet worden aangegeven met een vooraf gedefinieerde waarde (bijvoorbeeld: '9999') en niet '0', die een geldige meting kan worden.
* **Nauwkeurigheid van de meting** – Hallo werkelijke waarde van verbruik of temperatuur nauwkeurig moet worden geregistreerd. Onjuiste metingen levert onnauwkeurige prognoses. Hallo meting fout moet worden doorgaans lager is dan de waarde van 1% relatieve toohello ' True '.
* **Tijdstip van de meting** – dit is vereist tijdstempel Hallo werkelijke Hallo gegevens verzameld wordt niet door meer dan 10 seconden relatieve toohello true tijd van de werkelijke meting Hallo afwijken.
* **Synchronisatie** – wanneer meerdere gegevensbronnen worden gebruikt (*bijvoorbeeld*, gebruiks- en temperatuur) we moet ervoor zorgen dat er geen tijdsynchronisatie problemen ertussen. Dit betekent dat Hallo tijdstip verschil tussen de tijdstempel van twee onafhankelijke gegevensbronnen Hallo verzameld mag niet langer zijn dan meer dan 10 seconden.
* **Latentie** - zoals beschreven in bovenstaande **gegevensopname**, wij zijn afhankelijk van een betrouwbare gegevens stroom en opnamesnelheid proces. toocontrol dat we ervoor zorgen moet dat wij Hallo gegevens latentie bepalen. Dit is opgegeven als Hallo tijdverschil Hallo tijd waarop de werkelijke meting Hallo heeft plaatsgevonden, en Hallo tijdstip waarop deze is geladen in het Hallo Cortana Intelligence Suite opslag en is klaar voor gebruik. Voor de korte termijn load mag prognoses Hallo totale latentie niet langer dan 30 minuten. Voor de lange termijn load moet prognoses Hallo totale latentie niet groter dan 1 dag.

### <a name="data-preparation-and-feature-engineering"></a>Voorbereiden van gegevens en functie-Engineering
Zodra de onbewerkte gegevens Hallo zijn geconsumeerd (Zie **gegevensopname**) en is veilig opgeslagen, is deze gereed toobe verwerkt. Hallo gegevens voorbereidingsfase is in feite Hallo onbewerkte gegevens en converteren (transformeert, opnieuw) in een formulier voor Hallo modelleren fase. Eventueel die eenvoudige handelingen zoals het gebruik van Hallo onbewerkte gegevenskolom is met de werkelijke waarde van de gemeten, gestandaardiseerde waarden, meer complexe bewerkingen zoals [tijd achtergebleven](https://en.wikipedia.org/wiki/Lag_operator), en andere. gegevenskolommen Hallo nieuw gemaakt zijn waarnaar wordt verwezen tooas gegevensfuncties en Hallo-proces voor het genereren van deze functie-engineering tooas waarnaar wordt verwezen. Hallo-einde van dit proces zouden we een nieuwe gegevensset die is is afgeleid van Hallo onbewerkte gegevens en kan worden gebruikt voor het modelleren hebben. Bovendien Hallo gegevens voorbereidingsfase tootake antwoord ontbrekende waarden moet (Zie **gegevenskwaliteit**) en compenseren voor hen. In sommige gevallen moet er tevens toonormalize Hallo gegevens tooensure die alle waarden worden weergegeven in dezelfde schaal Hallo.

In deze sectie die wordt een overzicht van Hallo algemene gegevensfuncties vermeld die zijn opgenomen in Hallo energie prognosemodellen vraag.

**Tijd gebaseerde functies:** deze functies zijn afgeleid van Hallo datum/tijdstempel gegevens. Deze zijn geëxtraheerd en geconverteerd naar categorische functies, zoals:

* Tijd van de dag – dit Hallo uur van Hallo-dag waarmee de waarden van 0 too23 is
* Dag van week – dit vertegenwoordigt Hallo dag van week Hallo en waarden van 1 (zondag) too7 (zaterdag)
* Dag van de maand – dit Hallo werkelijke datum voorstelt en kan waarden vanaf 1 too31
* Maand van het jaar – dit vertegenwoordigt Hallo maand en waarden vanaf 1 (januari) too12 (December)
* Weekend – dit is een binaire waarde-functie waarmee Hallo waarden van 0 voor weekdagen of 1 voor het weekend
* Vakantiedag - dit is een binaire waarde-functie waarmee Hallo waarden van 0 voor een normale dag of 1 voor een feestdag
* Voorwaarden Fourier – Fourier voorwaarden zijn gewichten die zijn afgeleid van tijdstempel Hallo Hallo en gebruikte toocapture Hallo seizoensgebonden (cycli) in Hallo gegevens zijn. Aangezien we meerdere seizoen in onze gegevens hebben mogelijk moeten we meerdere Fourier voorwaarden. Waarden van de aanvraag kunnen bijvoorbeeld jaarlijkse wekelijks en dagelijks seizoen/cycli dat in 3 Fourier voorwaarden resulteert.

**Onafhankelijke meting functies:** Hallo onafhankelijke functies omvatten alle Hallo gegevenselementen dat willen we graag toouse als variabelen in het model. Hier we Hallo afhankelijke functie waardoor we moeten uitsluiten toopredict.

* De functie lag – dit tijd verschoven zijn waarden van de werkelijke vraag Hallo. Bijvoorbeeld, bevatten functies lag 1 Hallo vraag waarde in Hallo vorige uur (ervan uitgaande dat per uur) relatieve toohello Huidig timestamp. Op deze manier we toevoegen lag 2, 3, lag *enzovoort*. Hallo werkelijke combinatie van lag-functies die worden gebruikt tijdens de fase modelleren Hallo worden bepaald door de evaluatie van Hallo model resultaten.
* Lange termijn trends – deze functie Hallo lineaire groei van de vraag tussen jaar vertegenwoordigt.

**Afhankelijke functie:** Hallo afhankelijk onderdeel is Hallo gegevenskolom die willen we onze toopredict model. Met [onder supervisie machine learning](https://en.wikipedia.org/wiki/Supervised_learning), moeten we eerst met behulp van de afhankelijke onderdelen Hallo Hallo-model (dit is ook bedoeld tooas labels) te trainen. Hierdoor kunnen Hallo model toolearn Hallo patronen in Hallo-gegevens die zijn gekoppeld met afhankelijke Hallo-functie. We willen dat doorgaans toopredict Hallo werkelijke vraag in energie vraag prognose en daarom we deze als afhankelijke Hallo-functie wilt gebruiken.

**Verwerking van de ontbrekende waarden:** tijdens voorbereidingsfase Hallo gegevens, moeten we toodetermine Hallo aanbevolen strategie toohandle ontbrekende waarden. Dit is vooral met behulp van Hallo diverse statistiek [begrip Gegevensmethoden](https://en.wikipedia.org/wiki/Imputation_\(statistics\)). In geval van energie-vraag prognose Hallo rekenen we ontbrekende waarden meestal met behulp van zwevend gemiddelde van de vorige beschikbare gegevenspunten.

**Gegevensnormalisatie:** gegevensnormalisatie is een ander type transformatie die gebruikte toobring alle numerieke gegevens zoals vraag in een vergelijkbare schaal Forecast. Dit meestal verbetert Hallo model nauwkeurigheid en precisie. We gewoonlijk doet dit door de werkelijke waarde Hallo delen door Hallo gegevensbereik Hallo.
Hiermee wordt de oorspronkelijke waarde Hallo omlaag schalen in een kleiner bereik, doorgaans tussen 1 en 1.

## <a name="modeling"></a>Modelleren
Hallo modelleren fase is waar Hallo conversie van Hallo-gegevens in een model plaatsvindt. In Hallo zijn core van dit proces er geavanceerde algoritmen die scannen Hallo historische gegevens (trainingsgegevens), patronen ophalen en een model bouwen. Dit model kan worden later gebruikte toopredict op nieuwe gegevens die niet gebruikte toobuild Hallo model is.

Wanneer we beschikken over een werkende betrouwbare vereist model we kan vervolgens worden gebruikt tooscore nieuwe gegevens die gestructureerde tooinclude Hallo onderdelen (X). Hallo score berekenen voor proces maakt gebruik van Hallo persistente model (object uit Hallo training fase) en Hallo doelvariabele die wordt aangeduid met Ŷ voorspellen.

### <a name="demand-forecasting-modeling-techniques"></a>Prognosemodel Modelleringstechnieken vraag
In geval van Hallo van vraag prognose maken we gebruik van historische gegevens op die is besteld op tijd. In het algemeen is toodata met Hallo tijddimensie als [time series](https://en.wikipedia.org/wiki/Time_series). Hallo-doel in tijd reeks modellering toofind tijd gerelateerd trends, seizoensgebonden, auto-correlatie (correlatie na verloop van tijd) en die in een model te formuleren.

In de afgelopen jaren zijn geavanceerde algoritmen ontwikkelde tooaccommodate time series prognose en tooimprove nauwkeurigheid prognose. We beschreven enkele van deze hier kort.

> [!NOTE]
> Deze sectie is niet bedoeld toobe gebruikt als een machine learning en overzicht prognoses, maar in plaats daarvan als een kort overzicht van modelleren technieken die vaak worden gebruikt voor het voorspellen van de vraag. Voor meer informatie en educatieve materiaal over tijd reeks prognose wordt ten zeerste aanbevolen Hallo online boekverkoper [prognose: beginselen en praktijken](https://www.otexts.org/book/fpp).
> 
> 

#### <a name="ma-moving-averagehttpswwwotextsorgfpp62"></a>[**MA (zwevend gemiddelde)**](https://www.otexts.org/fpp/6/2)
Zwevend gemiddelde is een van de Hallo eerste analytische technieken die is gebruikt voor het voorspellen van de reeks tijd en het is nog steeds een van de meest gebruikte Hallo technieken vanaf vandaag. Het is ook Hallo basis voor meer geavanceerde prognose technieken. Met zwevend gemiddelde zijn we de volgende gegevenspunt Hallo gemiddelde via de meest recente punten Hallo K, waarbij K wordt bepaald door de volgorde Hallo Hallo zwevend gemiddelde van de prognose.

zwevend gemiddelde techniek Hallo Hallo effect van het vloeiend Hallo forecast heeft en daarom mogelijk niet verwerken en grote volatiliteit in Hallo-gegevens.

#### <a name="ets-exponential-smoothinghttpswwwotextsorgfpp75"></a>[**ETS (exponentiële demping)**](https://www.otexts.org/fpp/7/5)
Exponentiële vloeiend maken (ETS) is een serie van verschillende methoden die gewogen gemiddelde van recente gegevenspunten in volgorde toopredict Hallo volgende gegevenspunt gebruiken. Hallo idee tooassign hogere gewichten toomore recente waarden is en dit gewicht voor oudere meetwaarden geleidelijk te verlagen. Er zijn een aantal verschillende manieren met deze familie, zijn enkele van deze verwerking van de seizoensgebonden in Hallo gegevens zoals [Holt Winters seizoensgebonden methode](https://www.otexts.org/fpp/7/5).

Sommige van deze methoden factor ook in de seizoensgebonden Hallo Hallo-gegevens.

#### <a name="arima-auto-regression-integrated-moving-averagehttpswwwotextsorgfpp8"></a>[**ARIMA (automatische regressie geïntegreerd zwevend gemiddelde)**](https://www.otexts.org/fpp/8)
Automatische regressie geïntegreerde zwevend gemiddelde (ARIMA) is een ander gezin van methoden die wordt meestal gebruikt voor de prognose tijdreeks. Het combineert automatisch regressie methoden vrijwel met zwevend gemiddelde. Regressie-modellen automatisch regressie methoden gebruiken door vorige tijd reekswaarden in volgorde toocompute Hallo volgende datum punt. ARIMA methoden differentiërende methodes waaronder Hallo verschil tussen de gegevenspunten te berekenen en het gebruik van die in plaats van de oorspronkelijke gemeten waarde Hallo ook van toepassing. Ten slotte ARIMA ook maakt gebruik van Hallo zwevend gemiddelde van de technieken die hierboven worden beschreven. Hallo combinatie van al deze methoden op verschillende manieren is welke constructies Hallo-familie van ARIMA-methoden.

ETS en ARIMA worden zijn veel vandaag gebruikt voor het voorspellen van de energie-vraag en veel andere prognoses problemen. In veel gevallen zijn deze gecombineerd toodeliver zeer nauwkeurige resultaten.

**Algemene meerdere regressies** regressie modellen Hallo belangrijkste modellering benadering binnen Hallo domein van de machine learning en statistieken kunnen worden. In de context van tijdreeks hello gebruiken we regressie toopredict Hallo toekomstige waarden (*bijvoorbeeld*, van de vraag). In regressie we nemen van een lineaire combinatie van Hallo variabelen en meer Hallo gewichten (ook waarnaar wordt verwezen tooas coëfficiënten) van deze variabelen tijdens Hallo training. Hallo-doel is tooproduce een lijn die onze voorspelde waarde wordt verwacht. Regressie methoden zijn geschikt wanneer Hallo doelvariabele numerieke en daarom ook time series prognose past. Er is een breed scala aan regressie methoden inclusief zeer eenvoudig regressie modellen zoals [lineaire regressie](https://en.wikipedia.org/wiki/Linear_regression) en meer geavanceerde toepassingsgroepen zoals beslissingsstructuren [willekeurige Forests](https://en.wikipedia.org/wiki/Random_forest), [Neural Networks](https://en.wikipedia.org/wiki/Artificial_neural_network), en Boosted Decision Trees.

Energie-aanvraag prognose als een probleem regressie construeren ons een grote flexibiliteit bij het selecteren van de gegevensfuncties van onze die kunnen worden gecombineerd van Hallo werkelijke vraag tijd reeksgegevens en externe factoren zoals temperatuur biedt. Meer informatie over functies Hallo geselecteerd worden besproken in functie-Engineering hello (Zie **voorbereiden van gegevens en functie-Engineering**) sectie van dit playbook.

Uit onze ervaring met implementatie- en implementatie van energie vraag prognoses test, er is vastgesteld dat hello geavanceerde regressie modellen die beschikbaar in Azure ML zijn vaak tooproduce Hallo krijgt de beste resultaten en we maken gebruik ervan.

## <a name="model-evaluation"></a>Model-evaluatie
Evaluatie van het model is een belangrijke rol binnen Hallo **Model ontwikkelingscyclus**. Bij deze stap kijken we naar het Hallo-model en de prestaties met echte leven gegevens valideren. Tijdens Hallo modelleren stap gebruiken we een gedeelte van de beschikbare gegevens Hallo Hallo-model te trainen. Tijdens de evaluatiefase Hallo nemen we Hallo overige tootest Hallo-Hallo gegevensmodel. Vrijwel betekent dit dat we Hallo nieuwe modelgegevens dat Hallo dezelfde functies als Hallo training gegevensset bevat en dat heeft is geherstructureerd zijn voeding. Echter tijdens het validatieproces hello, we Hallo model toopredict Hallo target-variabele gebruiken in plaats Hallo beschikbaar doelvariabele bieden. Vaak is toothis proces als het score model. We zouden gebruiken Hallo true doelwaarden en ze Hello voorspelde waarden vergelijken. Hallo doel hier is toomeasure en Hallo voorspelling fout, wat betekent dat Hallo verschil tussen Hallo voorspellingen en de waarde true Hallo minimaliseren. Hallo fout meting kwantificeren is sleutel omdat we wilt toofine afstemmen Hallo model en valideren of Hallo fout daadwerkelijk afneemt. Verder aanpassen Hallo-model is mogelijk doordat Modelparameters waarmee Hallo leerproces of door het toevoegen of verwijderen van functies (waarnaar wordt verwezen tooas [parameters vegen](https://channel9.msdn.com/Blogs/Azure/Data-Science-Series-Building-an-Optimal-Model-With-Parameter-Sweep)). Vrijwel dit betekent dat er mogelijk tooiterate tussen Hallo functie-engineering, modelleren, moet evaluatie fasen model meerdere keren totdat we kunnen tooreduce Hallo foutniveau toohello vereist zijn.

Het is belangrijk tooemphasis Hallo voorspelling fout kan nooit worden nul omdat er is nooit een model dat elke uitkomst perfect kan voorspellen. Er is echter een bepaalde grootte van de fout die wordt geaccepteerd door Hallo bedrijf. Tijdens het validatieproces hello graag willen we tooensure dat onze model prediction-fout is op Hallo of beter dan Hallo business tolerantie niveau. Het is daarom belangrijk tooset Hallo niveau van de toegestane fout Hallo aan begin Hallo Hallo cyclus tijdens Hallo **probleem formulering** fase.

### <a name="typical-evaluation-techniques"></a>Typische evaluatietechnieken
Er zijn verschillende manieren in welke voorspelling fout kan worden gemeten en bepaalde. In deze sectie gaan we Hallo discussie op evaluatie technieken relevante tootime reeks en in specifieke voor energie vraag prognose.

#### <a name="mapehttpsenwikipediaorgwikimeanabsolutepercentageerror"></a>[**MAPE**](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
MAPE staat voor de gemiddelde Absolute Percentage fout. We zijn Hallo verschil tussen elke voorspelde punt en een werkelijke waarde van dat punt Hallo computing met MAPE. We vervolgens kwantificeren Hallo fout per punt door te berekenen Hallo deel van de werkelijke waarde van Hallo verschil relatieve toohello. Op de laatste stap gemiddelde we deze waarden. Hallo wiskundige formule gebruikt voor MAPE is Hallo volgende:

![MAPE formule](media/cortana-analytics-playbook-demand-forecasting-energy/mape-formula.png)
*waar een<sub>t</sub> Hallo werkelijke waarde F<sub>t</sub> Hallo voorspelde waarde en n Hallo forecast horizon.*

## <a name="deployment"></a>Implementatie
We zijn gereed toogo in Hallo implementatiefase nadat we hebben, kunt u Hallo fase modelleren en gevalideerd Hallo model prestaties. In deze context implementatie betekent het inschakelen van Hallo klant tooconsume Hallo model door uitgevoerd werkelijke voorspellingen op grote schaal. Hallo-concept van implementatie is de sleutel in Azure ML omdat onze belangrijkste doel tooconstantly is voorspellingen aanroepen als tegengestelde toojust Hallo inzicht verkrijgen uit Hallo-gegevens. Hallo-implementatiefase is Hallo onderdeel waar we Hallo model toobe verbruikt op grote schaal kunnen inschakelen.

In de context van de Hallo van energie-vraag prognose, is onze doel tooinvoke continue en periodieke prognoses zonder dat nieuwe gegevens is beschikbaar voor Hallo model dat Hallo prognose gegevens back toohello consumerende client worden verzonden terwijl.

### <a name="web-services-deployment"></a>Implementatie van Web-Services
Hallo belangrijkste implementeerbare bouwsteen in Azure ML is Hallo-webservice. Dit is Hallo meest effectieve manier tooenable verbruik van een Voorspellend model in de cloud Hallo. Hallo webservice Hallo model ingekapseld en wordt afgerond met een [RESTful](http://www.restapitutorial.com/) API (Application Programming Interface). Hallo API kan worden gebruikt als onderdeel van een clientcode zoals geïllustreerd in het onderstaande diagram kunt Hallo.

![We Service-implementatie en het verbruik](media/cortana-analytics-playbook-demand-forecasting-energy/web-service-deployment-and-consumption.png)

Zoals u kunt zien, wordt Hallo-webservice wordt geïmplementeerd in Hallo Cortana Intelligence Suite cloud en kan worden aangeroepen met het blootgestelde REST-API-eindpunt. Ander type van clients in verschillende domeinen kunt tegelijkertijd Hallo-service via Hallo Web-API aanroepen. Hallo-webservice kan ook schalen ter ondersteuning van duizenden gelijktijdige aanroepen.

### <a name="a-typical-solution-architecture"></a>Een typische oplossingsarchitectuur
Bij het implementeren van een oplossing prognose energie-vraag bent we geïnteresseerd in een end tooend oplossing die zich verder uitstrekt dan Hallo voorspelling-webservice en de hele gegevensstroom Hallo vereenvoudigt implementeren. Tijdens het Hallo die we een nieuwe prognose aanroepen, moeten we toomake ervoor dat Hallo-model met de functies van de meest recente gegevens worden ingevoerd. Dat houdt in dat Hallo zojuist verzamelde onbewerkte gegevens voortdurend ingenomen, verwerkt en omgezet in Hallo vereiste functieset op welk model Hallo is opgebouwd. AT Hallo dezelfde tijd, we wilt toomake Hallo prognose gegevens beschikbaar voor Hallo consumerende clients beëindigen. Een voorbeeld van de gegevens stroom cyclus (of gegevens pijplijn) wordt weergegeven in Hallo diagram hieronder:

![Prognose End tooEnd gegevensstroom van de energie-vraag](media/cortana-analytics-playbook-demand-forecasting-energy/energy-demand-forecase-end-data-flow.png)

Dit zijn Hallo stappen die uitgevoerd als onderdeel van Hallo vraag prognose energiecyclus worden:

1. Miljoenen meters geïmplementeerde gegevens genereren voortdurend energieverbruiksgegevens in realtime.
2. Deze gegevens worden verzameld en geüpload naar een cloud-opslagplaats (*bijvoorbeeld*, Azure Blob).
3. Voordat het wordt verwerkt, is Hallo onbewerkte gegevens geaggregeerde tooa onderstation of regionaal niveau zoals gedefinieerd door Hallo bedrijven.
4. Hallo functie verwerking (Zie **voorbereiden van gegevens en verwerken van de functie**) vervolgens vindt plaats en produceert Hallo gegevens die vereist is voor model trainen of score berekenen – Hallo functie setgegevens worden opgeslagen in een database (*bijvoorbeeld*, SQL Azure).
5. Hallo opnieuw trainen van de service wordt opgeroepen Hallo van toore train model – dat versie van Hallo model bijgewerkte prognose worden bewaard, zodat deze kan worden gebruikt door Hallo score berekenen voor web-service.
6. Hallo score berekenen voor webservice wordt aangeroepen op een planning die geschikt is voor prognose frequentie Hallo vereist.
7. Hallo prognose gegevens worden opgeslagen in een database die toegankelijk zijn voor Hallo end verbruik client.
8. Hallo verbruik client haalt Hallo prognoses, past deze weer in het raster hello en in overeenstemming met gebruiksvoorbeeld Hallo vereist worden verbruikt.

Het is belangrijk toonote die deze volledige cyclus is volledig geautomatiseerd en volgens een planning wordt uitgevoerd. Hallo gehele orchestration van deze gegevenscyclus kunt doen met behulp van hulpprogramma's zoals [Azure Data Factory](http://azure.microsoft.com/services/data-factory/).

### <a name="end-tooend-deployment-architecture"></a>End tooEnd architectuur voor implementatie
In de volgorde toopractically implementeert een prognose energie demand-oplossing op Cortana Intelligence, moeten we tooensure Hallo vereiste onderdelen worden vastgesteld en is juist geconfigureerd.

Hallo wordt volgende diagram een typische Cortana Intelligence gebaseerd architectuur die wordt geïmplementeerd en stuurt Hallo stroom gegevenscyclus die hierboven wordt beschreven:

![End tooEnd architectuur voor implementatie](media/cortana-analytics-playbook-demand-forecasting-energy/architecture.png)

Raadpleeg voor meer informatie over elk van de Hallo-onderdelen en volledige architectuur Hallo toohello energie oplossingssjabloon.


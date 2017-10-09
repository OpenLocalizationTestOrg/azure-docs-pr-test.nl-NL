---
title: aaaIntroduction toomicroservices in Azure | Microsoft Docs
description: Een overzicht van waarom cloudtoepassingen maken met een benadering microservices is belangrijk voor toepassingsontwikkeling moderne en hoe Azure Service Fabric een tooachieve platform biedt dit.
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: fae2be85-0ab4-4cd3-9d1f-e0d95fe1959b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell
ms.openlocfilehash: b11920b9105e7575390e8fcf0d1ef6ab3c632978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="why-a-microservices-approach-toobuilding-applications"></a>Waarom een microservices benadering toobuilding toepassingen?
Software-ontwikkelaars zijn er geen nieuwe functies in onze verwachting over waarbij een toepassing in onderdelen. Het is centrale paradigma Hallo stand object software abstracties en componentization. Vandaag de dag doorgaans dit factoriseren tootake Hallo vorm van klassen en interfaces tussen gedeelde bibliotheken en lagen van de technologie. Normaal gesproken wordt een gelaagde benadering gemaakt met een back-end-winkel, bedrijfslogica middelste laag en een front-gebruikersinterface (UI). Wat *heeft* gewijzigd via Hallo laatste jaren is dat we, ontwikkelaars, bouwt gedistribueerde toepassingen die voor de cloud Hallo en aangedreven door Hallo bedrijven.

Hallo veranderende bedrijfsbehoeften zijn:

* Een service die gebaseerd en werkt op schaal tooreach klanten in nieuwe geografische regio's (bijvoorbeeld).
* Snellere levering van functies en mogelijkheden toobe kunnen toorespond toocustomer aanvragen in een flexibele manier.
* Verbeterde gebruik tooreduce resourcekosten.

Deze bedrijfsbehoeften van invloed zijn op *hoe* we bij het ontwikkelen van toepassingen.

Lees voor meer informatie over Hallo benadering van Azure toomicroservices [Microservices: een toepassing revolution aangedreven door Hallo cloud](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/).

## <a name="monolithic-vs-microservice-design-approach"></a>Monolithische versus microservice ontwerpbenadering
Alle toepassingen ontwikkelen gedurende een bepaalde periode. Succesvolle toepassingen ontwikkelen door nuttig toopeople. Mislukte toepassingen niet doen evolueren en uiteindelijk zijn afgeschaft. volgende vraag Hallo: hoeveel u weet over de vereisten van uw vandaag, en wat ze zich in toekomstige Hallo? Stel dat dat u een reporting-toepassing voor een afdeling wilt maken. U bent ervoor dat de toepassing hello binnen Hallo bereik van uw bedrijf blijft en dat Hallo rapporten tijdelijke. Uw keuze van benadering wijkt af van, spreken, video-inhoud tootens miljoenen klanten bouwen van een service die biedt. 

Soms iets uit Hallo deur ophalen als bewijs van het concept is aangedreven factor hello, terwijl u weet dat toepassing hello later kan worden aangepast. Er is weinig punt in iets te veel engineering die nooit wordt gebruikt. De Hallo gebruikelijke engineering nadeel. Hallo op daarentegen wanneer bedrijven over gebouw praten voor hello cloud, Hallo verwachting groei en informatie over het gebruik is. Hallo-probleem is dat groei en schaal onvoorspelbaar zijn. We willen er ook toobe kunnen tooprototype snel achterhoofd ook dat er zich op een pad toodeal met succes in de toekomst bevinden. Dit is Hallo lean opstarten benadering: bouwen, te meten, informatie over en herhalen.

Tijdens het Hallo-client / server-era doorgaans we toofocus over het bouwen van gelaagde toepassingen met behulp van specifieke technologieën in elke laag. Hallo term *monolithische* toepassing geworden dat voor deze methoden. Hallo-interfaces doorgaans toobe tussen Hallo lagen en het ontwerp van een meer nauw gekoppeld tussen onderdelen binnen elke laag is gebruikt. Ontwikkelaars ontworpen en meeberekend klassen die zijn gecompileerd in bibliotheken en aan elkaar gekoppeld in een paar uitvoerbare programma's en dll-bestanden. 

Er zijn een monolithisch ontwerpbenadering toosuch voordelen. Het is vaak eenvoudiger toodesign en biedt sneller aanroepen tussen onderdelen, omdat deze aanroepen vaak via IPC (interprocess communication zijn). Bovendien iedereen één product, doorgaans toobe meer mensen-resource-efficiënt wordt getest. Hallo nadeel is dat er een nauwe koppeling tussen gelaagde lagen, en u kunt geen afzonderlijke onderdelen schalen. Als u tooperform oplossingen of -upgrades nodig hebt, hebt u toowait voor anderen toofinish hun testen. Is het moeilijker toobe flexibele.

Microservices adres deze nadelen en meer nauw zijn afgestemd op Hallo voorafgaand aan de zakelijke vereisten, maar ze hebben ook zowel voordelen en verplichtingen. Hallo voordelen van microservices zijn dat elk criterium doorgaans eenvoudiger business functionaliteit, zodat u omhoog of omlaag test schalen, implementeren en beheren onafhankelijk ingekapseld. Een belangrijk voordeel van een microservice-benadering is dat teams meer bedrijfsscenario's dan wordt aangestuurd door technologie, die een gelaagde benadering Hallo moedigt. In de praktijk kleinere teams een microservice op basis van een klant-scenario ontwikkelen en eventuele technologieën die ze gebruiken. 

Hallo organisatie nodig niet met andere woorden, toostandardize tech toomaintain microservice toepassingen. Afzonderlijke teams dat eigen services doen kunnen wat zinvol voor toe op basis van het team expertise of wat het meest geschikte toosolve Hallo probleem is. In de praktijk kan een reeks aanbevolen technologieën, zoals een bepaald NoSQL opslaan of web-toepassingsframework, verdient de voorkeur.

Hallo nadeel van microservices wordt geleverd bij het beheren van Hallo verhoogd aantal afzonderlijke entiteiten en omgaan met complexere implementaties en versiebeheer. Netwerkverkeer tussen Hallo microservices verhoogd en de bijbehorende netwerkvertragingen Hallo. Veel chatty, gedetailleerde services zijn een recept voor een nachtmerrie prestaties. De afhankelijkheden bekijken zonder extra toohelp, is het moeilijk te 'Zie' hello gehele systeem. 

Standaarden maken Hallo microservice benadering werkt door afspreken hoe toocommunicate en wordt alleen Hallo dingen fouttolerante u bij een service in plaats van rigid contracten moet. Het is belangrijk toodefine deze contracten vooraf in Hallo ontwerpt, omdat services onafhankelijk van elkaar bijwerken. Een andere beschrijving lang geleden bedacht voor het ontwerpen van een benadering microservices is ' fijnmazig service oriented architecture (SOA).'

***De eenvoudigste is hello microservices ontwerpbenadering over een ontkoppelde federation Services met onafhankelijke wijzigingen tooeach en overeengekomen standaarden voor communicatie.***

Als u meer cloud-apps worden geproduceerd, mensen heeft ontdekt dat dit afbreken Hallo algehele app in onafhankelijke, scenario gerichte services is een beter op lange termijn benadering.

## <a name="comparison-between-application-development-approaches"></a>Vergelijking tussen toepassingsontwikkeling nadert
![Toepassingsontwikkeling service Fabric-platform][Image1]

1) Een monolithisch app domeinspecifieke functionaliteit bevat en normaal wordt gedeeld door functionele lagen, zoals web en business gegevens.

2) U een monolithisch app schalen door het klonen op meerdere servers/virtuele machines/containers.

3) Een toepassing microservice scheidt functionaliteit in afzonderlijke kleinere services.

4) Hallo microservices benadering kan worden geschaald uit door het implementeren van elke service afzonderlijk, exemplaren van deze services te maken tussen servers/virtuele machines/containers.

Met een microservice ontwerpen aanpak is niet een wondermiddel voor alle projecten, maar deze zijn afgestemd beter Hallo zakelijke doelstellingen die eerder zijn beschreven. Beginnen met een monolithisch benadering wellicht acceptabel als u weet dat u Hallo kans toorework Hallo code later in het ontwerp van een microservices hebt. Vaker voorkomt, begint met een monolithisch toepassing en langzaam splits deze in fasen verlopen, beginnen met het Hallo-modules die toobe schaalbaar of meer flexibele moeten.

toosummarize, Hallo microservice aanpak is toocompose uw toepassing van veel kleine services. Hallo-services worden uitgevoerd in de containers die zijn geïmplementeerd op een cluster van machines. Kleinere teams ontwikkelen van een service die is gericht op een scenario onafhankelijk, versie testen, implementeren en schalen van elke service, zodat de gehele toepassing hello kunt ontwikkelen.

## <a name="what-is-a-microservice"></a>Wat is een microservice?
Er zijn verschillende definities van microservices. Als u Hallo Internet zoekt, vindt u veel nuttige informatiebronnen die hun eigen standpunten en definities bieden. Echter, de meeste van de volgende kenmerken van microservices Hallo zijn algemeen overeengekomen:

* Een klant of zakelijke scenario inkapselen. Wat is Hallo probleem, u het oplossen van?
* Ontwikkeld door een klein engineering team.
* Geschreven in elke programmeertaal en elk framework gebruiken.
* Bestaan uit de code en (optioneel) state, die beide zijn onafhankelijk samengestelde geïmplementeerd en geschaald.
* Communiceren met andere microservices via goed gedefinieerde interfaces en protocollen.
* Unieke namen (URL's) gebruikt tooresolve hun locatie zijn.
* Blijven consistent en beschikbaar zijn in Hallo aanwezigheid van fouten.

U kunt deze kenmerken in samenvatten:

***Microservice-toepassingen bestaan uit kleine, onafhankelijk van elkaar samengestelde en schaalbare klantgerichte services die via standaardprotocollen met goed gedefinieerde interfaces met elkaar communiceren.***

We eerst twee punten in de voorgaande sectie Hallo Hallo behandeld en nu uitvouwt op en verduidelijken Hallo anderen.

### <a name="written-in-any-programming-language-and-use-any-framework"></a>Geschreven in elke programmeertaal en elk framework gebruiken
Ontwikkelaars moeten we gratis toochoose een taal of elk framework die we, afhankelijk van onze vaardigheden of Hallo eisen van Hallo-service willen. In sommige services mogelijk u Hallo prestatievoordelen van C++ boven alle andere waarde. In andere services zijn Hallo gebruiksgemak beheerde-ontwikkeling in C# of Java zeer belangrijk. In sommige gevallen toouse een bibliotheek specifieke partner technologie voor gegevensopslag, moet u mogelijk of manier van het blootstellen van Hallo service tooclients.

Nadat u een technologie hebt gekozen, wordt u later toohello operationele of levenscyclusbeheer en schalen van Hallo-service.

### <a name="allows-code-and-state-toobe-independently-versioned-deployed-and-scaled"></a>Kan code en status toobe onafhankelijk samengestelde geïmplementeerd en geschaald
Maar u toowrite kiezen uw microservices, Hallo code en eventueel Hallo status moeten onafhankelijk implementeren, bijwerken en schalen. Dit is daadwerkelijk een Hallo moeilijker problemen toosolve, omdat tooyour keuze van technologieën bepaalde. Schalen is het lastig begrijpen hoe toopartition (of shard) beide Hallo code en status. Wanneer Hallo code en de status van afzonderlijke technologieën die algemene vandaag, moeten Hallo implementatiescripts voor uw microservice toobe kunnen toocope met beide schalen. Dit is ook over wendbaarheid en flexibiliteit, zodat u enkele Hallo microservices bijwerken kunt zonder tooupgrade allemaal in één keer.

Retourneert toohello monolithische versus microservice benadering even hello volgende diagram toont Hallo verschillen Hallo benadering toostoring status.

#### <a name="state-storage-between-application-styles"></a>Status opslag tussen toepassing stijlen
![Service Fabric-platform status opslag][Image2]

***Hallo monolithische benadering aan de linkerkant Hallo heeft een individuele database en lagen van specifieke technologieën.***

***Hallo microservices benadering op Hallo rechts heeft een grafiek van onderling verbonden microservices waarbij staat doorgaans binnen het bereik toohello microservice en verschillende technologieën worden gebruikt.***

In een monolithisch benadering, doorgaans Hallo toepassing gebruikt een individuele database. Hallo voordeel is dat het één locatie, waardoor het eenvoudig toodeploy is. Elk onderdeel kan een toostore één tabel hebben de status. Teams moeten toostrictly afzonderlijke staat, die een uitdaging. Onvermijdelijk er zijn temptations tooadd een nieuwe kolom tooan bestaande klantentabel, een koppeling tussen tabellen doen en afhankelijkheden op Hallo opslaglaag maken. Nadat dit gebeurt, kunt u afzonderlijke onderdelen kan niet schalen. 

Hallo microservices benadering, elke service beheert en slaat de eigen staat. Elke service is verantwoordelijk voor het schalen van zowel de code en de status samen toomeet Hallo-eisen van Hallo-service. Een nadeel is dat wanneer er een nodig toocreate weergaven of query's van de gegevens van uw toepassing, moet u tooquery in uiteenlopende status winkels. Dit is meestal opgelost door een afzonderlijke microservice die een weergave in een verzameling microservices voortbouwt. Als u tooperform meerdere ad hoc query's op Hallo gegevens moet, moet elke microservice rekening houden met schrijven van de gegevens tooa magazijnbeheer gegevensservice voor offline analyses.

Versiebeheer is specifiek toohello geïmplementeerd versie van een microservice zodanig dat meerdere verschillende versies implementeren en naast elkaar uitvoeren. Versiebeheer adressen Hallo scenario's waarbij een nieuwere versie van een microservice mislukt tijdens de upgrade en tooroll back tooan moet eerdere versie. Hallo is andere scenario voor versiebeheer Bezig met A/B-stijl testen, waarbij verschillende gebruikers verschillende versies van Hallo service ondervindt. Het is bijvoorbeeld algemene tooupgrade een microservice voor een specifieke set met nieuwe functies voor klanten tootest voordat dit veel meer rollen. Na het levenscyclusbeheer van microservices brengt deze nu ons toocommunication ertussen.

### <a name="interacts-with-other-microservices-over-well-defined-interfaces-and-protocols"></a>Interactie met andere microservices via goed gedefinieerde interfaces en protocollen
In dit onderwerp aandacht weinig hier, omdat uitgebreide documentatie over service oriented architecture die is gepubliceerd via Hallo afgelopen 10 jaar communicatiepatronen beschrijft. Servicecommunicatie gebruikt in het algemeen een REST-benadering met HTTP- en TCP-protocollen en XML- of JSON als Hallo serialisatie-indeling. Vanuit het perspectief van een interface is het over Hallo web ontwerpbenadering gaan hanteren. Maar niets u voorkomt met binaire protocollen of uw eigen gegevensindelingen. Worden voorbereid voor personen toohave moeilijker tegelijk met behulp van uw microservices als deze openbaar beschikbaar.

### <a name="has-a-unique-name-url-used-tooresolve-its-location"></a>Een unieke naam (URL) heeft gebruikt tooresolve de locatie
Houd er rekening mee hoe we houden waarin wordt aangegeven dat Hallo microservice aanpak zoals Hallo web is? Zoals Hallo web moet uw microservice toobe adresseerbare waar deze wordt uitgevoerd. Als u denkt u over virtuele machines en welke een bepaalde microservice wordt uitgevoerd, gaan dingen onjuiste snel. 

In Hallo dezelfde manier of DNS oplossing voor een bepaalde URL tooa bepaalde machine, uw microservice moet een unieke naam toohave zodat de huidige locatie kan worden gedetecteerd. Microservices moet adresseerbare namen zodat ze onafhankelijk van het Hallo-infrastructuur die ze worden uitgevoerd. Dit betekent dat er een interactie tussen hoe uw service wordt geïmplementeerd en hoe deze wordt gedetecteerd, is omdat er moet een register service toobe. Evenredig, wanneer een machine is mislukt, Hallo registry-service moet laat u weten waar Hallo-service wordt nu uitgevoerd. 

Hiermee beschikt u over ons toohello Volgend onderwerp: herstelmogelijkheden en consistentie.

### <a name="remains-consistent-and-available-in-hello-presence-of-failures"></a>Consistente en beschikbaar zijn in de aanwezigheid van fouten Hallo blijft
Omgaan met onverwachte fouten is een van de Hallo moeilijkst problemen toosolve, met name in een gedistribueerde systemen. Veel van Hallo-code die we als ontwikkelaars schrijven is afhandeling van uitzonderingen en dit is ook waar hello meeste tijd is besteed tests. Hallo-probleem is meer dan het schrijven van code toohandle fouten die zijn betrokken. Wat gebeurt er wanneer het Hallo-machine waarop Hallo microservice wordt uitgevoerd uitvalt? Niet alleen u toodetect deze microservice-fout (een vaste probleem zelf), maar u moet ook iets toorestart uw microservice. 

Een microservice moet toobe robuuste toofailures en vaak opnieuw op een andere computer omwille van de beschikbaarheid. Dit wordt ook geleverd toohello-status die is opgeslagen namens Hallo microservice, waarbij Hallo microservice kunt herstellen deze status van, en of de Hallo microservice kunnen toorestart is voltooid. Met andere woorden, moet toobe herstelmogelijkheden in compute hello (Hallo proces opnieuw wordt opgestart), evenals herstelmogelijkheden in Hallo of gegevens (er worden geen gegevens verloren gaan en Hallo gegevens consistent blijven).

Hallo problemen tolerantieniveau zijn samengesteld tijdens andere scenario's, zoals wanneer fouten tijdens een upgrade van de toepassing optreden. Hallo hoeft microservice, werken met implementatiesysteem hello, niet toorecover. Moet ook toothen bepalen of het kan gaan toomove forward toohello nieuwere versie of in plaats daarvan tooa vorige versie toomaintain een consistente status terugdraaien. Vragen zoals of voldoende machines zijn beschikbaar tookeep vooruitgang en hoe toorecover eerdere versies van Hallo microservice toobe beschouwd als nodig. Hiervoor moet deze beslissingen Hallo microservice tooemit health informatie toobe kunnen toomake.

### <a name="reports-health-and-diagnostics"></a>Rapporten status en diagnose
Het lijkt misschien duidelijk, en wordt vaak wordt overgeslagen, maar een microservice de status en diagnose moet rapporteren. Anders is er weinig inzicht vanuit het perspectief van een bewerkingen. Diagnostische gebeurtenissen correleren in een reeks onafhankelijke services en omgaan met machine klok laat toomake beeld krijgt van Hallo gebeurtenis volgorde is het lastig om. In Hallo dezelfde manier om te communiceren met een microservice via overeengekomen protocollen en gegevens indelingen, ontstaat er naar standaardisering in hoe toolog health en diagnostische gebeurtenissen die uiteindelijk op een gebeurtenis terechtkomen opslaan voor het uitvoeren van query's en weergeven. In een benadering microservices is deze sleutel verschillende teams overeenstemming worden bereikt over een één-indeling. Er moet een consistente werkwijze tooviewing van diagnostische gebeurtenissen in Hallo toepassing als geheel toobe.

Health wijkt af van diagnostische gegevens. De status is over Hallo microservice rapportage van de huidige status tootake nodige acties. Een goed voorbeeld werkt met de upgrade en implementatie mechanismen toomaintain beschikbaarheid. Hoewel een service is mogelijk momenteel beschadigd vanwege tooa proces crash of opnieuw opstarten van de computer, Hallo-service nog steeds mogelijk operationeel. Hallo laatste wat u moet deze erger van toomake is door het uitvoeren van een upgrade. Hallo beste aanpak is toodo onderzoek eerst of er voldoende tijd uittrekken om Hallo microservice toorecover. Gebeurtenissen van de status van een microservice helpt ons gefundeerde beslissingen te nemen en van kracht te zelfherstellende services maken.

## <a name="service-fabric-as-a-microservices-platform"></a>Service Fabric als microservices platform
Azure Service Fabric ontstaan uit een overgang door Microsoft in het vak-producten, doorgaans monolithische in stijl, toodelivering services zijn leveren. Hallo-ervaring voor bouwen en operationele grote services, zoals Azure SQL Database en Azure Cosmos DB in de vorm van Service Fabric. Hallo platform ontwikkeld na verloop van tijd meer services wordt aangenomen. Service Fabric had toorun belangrijker nog, niet alleen in Azure, maar ook in implementaties met zelfstandige Windows Server.

***Hallo-doel van de Service Fabric is toosolve Hallo harde problemen van het bouwen en uitvoeren van een service en infrastructuur bronnen efficiënt gebruiken zodat teams met behulp van een benadering microservices bedrijfsproblemen kunnen oplossen.***

Service Fabric biedt drie gebieden brede toohelp ontwikkelen van toepassingen die gebruikmaken van een benadering microservices:

* Een platform waarmee system services toodeploy, upgraden, detecteren, en mislukte services opnieuw starten, services detecteren, routeren van berichten, status beheren en controleren van status. Deze systeemservices kunnen van kracht veel Hallo kenmerken van microservices die eerder is beschreven.
* Mogelijkheid toodeploy toepassingen processen voor beide in containers of als die wordt uitgevoerd. Service Fabric is een container en een proces orchestrator.
* Productief programming API's, toohelp ontwikkelen van toepassingen als microservices: [ASP.NET Core, Reliable Actors en Reliable Services](service-fabric-choose-framework.md). U kunt uw microservice eventuele toobuild code. Maar deze API's Hallo taak eenvoudiger maken en ze integreren met een dieper niveau Hallo-platform. Op deze manier bijvoorbeeld, status en diagnose informatie kunt u vinden, of kunt u profiteren van de ingebouwde hoge beschikbaarheid.

***Service Fabric is agnostisch op hoe het bouwen van uw service en kunt u elke technologie. Dit biedt echter ingebouwde programming API's waarmee u gemakkelijker toobuild microservices.***

### <a name="migrating-existing-applications-tooservice-fabric"></a>Migreren van bestaande toepassingen tooService Fabric
Een sleutel benadering tooService Fabric is tooreuse bestaande code, die vervolgens kan worden modernized met nieuwe microservices. Er zijn vijf fasen tooapplication modernisering en u kunt starten en stoppen op een van de Hallo fasen. Dit zijn;

1) Een traditionele monolithische toepassing
2) Lift- en Shift - containers of Gast uitvoerbare bestanden toohost bestaande code gebruiken in Service Fabric.
3) Modernisering - nieuwe microservices toegevoegd naast de bestaande beperkte code. 
4) Innoveren - opsplitsen Hallo monolithische microservices alleen is gebaseerd op nodig.
5) Omgezet in microservices - Hallo transformatie van bestaande monolithische toepassingen of het ontwikkelen van nieuwe greenfield toepassingen.

![Migratie tooMicroservices][Image3]

Het is belangrijk tooemphasis opnieuw, u kunt **starten en stoppen op een van deze fasen**, u bent niet verplicht toomoved toohello volgende fase. We gaan nu kijken voorbeelden voor elk van deze fasen.

**Lift- en verschuiven** - grote aantallen van bedrijven zijn op te heffen en bestaande monolithische toepassingen verschuiving in containers toofor twee redenen;

- Kosten vermindering ofwel vanwege tooconsolidation en verwijderen van bestaande hardware of met toepassingen met hogere dichtheid. 
- Consistente implementatie contract tussen ontwikkel- en bewerkingen.

Kosten kortingen begrijpelijk zijn en worden binnen Microsoft grote aantallen van bestaande toepassingen beperkte gewoon toomillions van bedragen. Consistente implementatie is moeilijker tooevaluate, maar als net zo belangrijk. Wordt aangegeven dat ontwikkelaars kunnen nog worden gratis toochoose Hallo technologie die suites ze maar Hallo operations alleen een eenduidige manier toodeploy accepteert en deze toepassingen te beheren. Dit vermindert Hallo operations opheft toodeal met Hallo complexiteit van veel verschillende technologieën of bepaalde objecten waardoor ontwikkelaars tooonly kiezen. In wezen elke toepassing is beperkte in zelfstandige implementatie-installatiekopieën.

Veel organisaties stoppen hier. Ze al Hallo voordelen van containers en Service Fabric biedt volledige beheerervaring Hallo van implementatie, upgrades, versiebeheer, Rollback, health monitoring enzovoort.

**Modernisering** -is Hallo toevoeging van nieuwe services samen met de bestaande beperkte code. Als u nieuwe code toowrite gaat, is het beste toodecide tootake kleine stappen omlaag Hallo microservices pad. Dit kan een nieuw REST-API-eindpunt, of een nieuwe bedrijfsregels worden toevoegt. Op deze manier die u start op reis Hallo van nieuwe microservices gebouw en praktijken ontwikkelen en implementeren.

**Innoveren** -die oorspronkelijke veranderende zakelijke behoeften aan Hallo begin van dit artikel, die genereren Hallo microservices benadering toeneemt onthouden? Op deze fase Hallo besluit is, zijn dit gebeurt toomy huidige toepassing en zo ja, ik toostart hello monoliet splitsen of innoveren nodig. Hier een voorbeeld is wanneer een database een knelpunt verwerken wordt omdat deze wordt gebruikt als een werkstroom wachtrij. Als het aantal werkstroom aanvragen verhogen Hallo Hallo werken behoeften toobe voor schaal gedistribueerd. Dus voor dat bepaalde deel van het Hallo-toepassing die niet wordt geschaald, of u hebt tooupdate meer vaak dit uit te splitsen in een microservice en innoveren. 

**Omgezet in microservices** -waar uw toepassing is het volledig samengesteld uit (of ontleed in) microservices. Hier tooreach hello microservices reis zijn aangebracht. U kunt starten, maar toodo dit zonder een platform microservices toohelp is van een aanzienlijke investering. 

### <a name="are-microservices-right-for-my-application"></a>Microservices zijn geschikt voor mijn toepassing?
Misschien. We heeft ondergaan is veel van deze Hallo voordelen van een benadering microservice-achtige duurt mogelijk als er steeds meer teams in Microsoft begon toobuild voor Hallo cloud voor zakelijke redenen, gerealiseerde. Bing, bijvoorbeeld heeft is de ontwikkeling van microservices in zoeken naar jaar. Hallo microservices aanpak is voor andere teams nieuwe. Teams gevonden dat er vaste problemen toosolve buiten hun belangrijkste gebieden van kracht zijn. Dit is de reden waarom de Service Fabric opgedaan tractie Hallo-technologie van keuze voor het bouwen van services.

Hallo-doel van de Service Fabric is tooreduce Hallo complexiteit van het bouwen van toepassingen met een benadering microservice, zodat er geen toogo via als veel dure redesigns. Begin klein, indien nodig worden geschaald, afschaffen services, nieuwe toevoegen en ontwikkelen met klant gebruik Hallo aanpak is. We ook weten dat er veel andere problemen zijn nog toobe toomake microservices meer gebruiksvriendelijke voor de meeste ontwikkelaars opgelost. Containers en Hallo actor-programmeermodel vindt u voorbeelden van kleine stappen in deze richting, en we zeker weet dat dat meer innovaties ontstaan toomake dit eenvoudiger.
 
<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Volgende stappen
* [Overzicht van service Fabric-terminologie](service-fabric-technical-overview.md)
* [Microservices: Een toepassing revolution aangedreven door Hallo cloud](https://azure.microsoft.com/en-us/blog/microservices-an-application-revolution-powered-by-the-cloud/)

[Image1]: media/service-fabric-overview-microservices/monolithic-vs-micro.png
[Image2]: media/service-fabric-overview-microservices/statemonolithic-vs-micro.png
[Image3]: media/service-fabric-overview-microservices/microservices-migration.png

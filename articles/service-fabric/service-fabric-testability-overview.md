---
title: overzicht van de Analysis Service aaaFault | Microsoft Docs
description: In dit artikel beschrijft Hallo Analysis Services-fout in Service Fabric voor fouten veroorzaken en Testscenario's uitvoeren op basis van uw services.
services: service-fabric
documentationcenter: .net
author: anmolah
manager: timlt
editor: vturecek
ms.assetid: 1f064276-293a-4989-a513-e0d0b9fdf703
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: anmola
ms.openlocfilehash: deac16ec830aa10d4e488e60691faa9ef2b6cd33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-fault-analysis-service"></a>Inleiding toohello Analysis Services-fout
Hallo-fout Analysis Services is ontworpen voor het testen van de services die zijn gebouwd op Microsoft Azure Service Fabric. U kunt met Hallo veroorzaakt Analysis Service zinvolle fouten veroorzaken en volledige Testscenario's uitvoeren op uw toepassingen. Deze fouten en scenario's uitoefenen en valideren Hallo talrijke statussen en overgangen die een service in een gecontroleerde, veilige en consistente manier tijdens de levensduur krijgen.

Acties zijn de afzonderlijke fouten Hallo als een service voor het testen van het doel. Een ontwikkelaar van de service kunt deze als bouwstenen toowrite ingewikkeld scenario's gebruiken. Bijvoorbeeld:

* Start opnieuw op een knooppunt toosimulate een willekeurig aantal situaties waarbij een computer of virtuele machine opnieuw is opgestart.
* Verplaatsen van een replica van de stateful service toosimulate load balancing, failover of upgrade van de toepassing.
* Quorumverlies op een stateful service toocreate een situatie waarin schrijfbewerkingen kunnen niet doorgaan omdat er niet voldoende 'back-up' of 'secundair' replica's tooaccept nieuwe gegevens worden aangeroepen.
* Verlies van gegevens op een stateful service toocreate een situatie waarin alle geheugenstatus volledig wordt gewist uit worden aangeroepen.

Scenario's zijn complexe bewerkingen bestaat uit een of meer acties. Hallo-fout Analysis Service biedt twee ingebouwde voltooien van scenario's:

* Chaos Scenario
* Failover-Scenario

## <a name="testing-as-a-service"></a>Als een service testen
Hallo-fout Analysis Services is een Service Fabric-systeemservice die automatisch wordt gestart met een Service Fabric-cluster. Deze service fungeert als host voor fouttolerantie injectie scenario testuitvoering en statusanalyse Hallo. 

![Fout met betrekking tot Analysis Services][0]

Wanneer een fout met betrekking tot actie of een test-scenario is gestart, wordt een opdracht toohello Analysis Services-fout toorun Hallo veroorzaakt actie of test scenario verzonden. Hallo-fout Analysis Services is stateful zodat betrouwbaar kunnen fouten en scenario's worden uitgevoerd en valideer de resultaten. Een Testscenario langlopende kan bijvoorbeeld betrouwbaar uitgevoerd door Hallo veroorzaakt Analysis Services. En omdat tests worden in Hallo cluster wordt uitgevoerd, Hallo service kunt bekijkt hello status van Hallo-cluster en uw tooprovide services meer gedetailleerde informatie over mislukte.

## <a name="testing-distributed-systems"></a>Gedistribueerde systemen testen
Service Fabric maakt Hallo taak schrijven en het beheren van gedistribueerde schaalbare toepassingen aanzienlijk eenvoudiger. Hallo-fout Analysis Service vereenvoudigt het testen van een gedistribueerde toepassing die op dezelfde manier eenvoudiger. Er zijn drie belangrijkste problemen die toobe opgelost moeten bij het testen:

1. Simuleren/genereren van fouten die in real-world scenario's optreden: een van de Hallo belangrijke aspecten van een Service Fabric is dat het mogelijk toorecover gedistribueerde toepassingen van diverse fouten maakt. Echter tootest die toepassing hello kunnen toorecover deze fouten is, moeten we een mechanisme toosimulate/genereren deze echte storingen in een gecontroleerde testomgeving.
2. Hallo mogelijkheid toogenerate gecorreleerde fouten: Basic storingen in Hallo-systeem, zoals netwerkstoringen en machine, zijn eenvoudig tooproduce afzonderlijk. Genereren van een groot aantal scenario's die kunnen ontstaan in de praktijk Hallo als gevolg van Hallo interacties van deze fouten voor afzonderlijke is essentieel.
3. Uniforme wijze van werken over verschillende niveaus van ontwikkeling en implementatie: Er zijn veel fout injectiesystemen die verschillende typen fouten kunnen doen. Hallo-ervaring in al deze waarden is slecht wanneer het verplaatsen van een vak developer-scenario's, toorunning Hallo dezelfde tests in grote testomgevingen, toousing ze voor in productie wordt getest.

Hoewel er veel mechanismen toosolve deze problemen, een systeem dat dezelfde vereiste garanties--alle Hallo manier vanuit een developer 1-box-omgeving Hallo ontbreekt tootest in productieclusters. Hallo-fout Analysis Service helpt Hallo ontwikkelaars zich concentreren op hun zakelijke logica te testen. Hallo-fout Analysis Service biedt dat alle mogelijkheden van Hallo tootest Hallo interactie van Hallo service met onderliggende gedistribueerde systeem Hallo nodig.

### <a name="simulatinggenerating-real-world-failure-scenarios"></a>Scenario's voor echte fouten simuleren/genereren
tootest hello robuustheid van een gedistribueerde systeem tegen storingen, moeten we een mechanisme toogenerate fouten. Terwijl in theorie genereren een fout als een knooppunt omlaag gemakkelijk lijkt, wordt het Hallo roept dezelfde set consistentieproblemen dat Service Fabric toosolve probeert. Een voorbeeld: als we tooshut omlaag een knooppunt wilt Hallo vereist werkstroom Hallo volgende is:

1. Uitgeven van Hallo-client een aanvraag tot afsluiten knooppunt.
2. Hallo aanvraag toohello juiste knooppunt verzenden.
   
    a. Als het Hallo-knooppunt is niet gevonden, moet het mislukken.
   
    b. Als het Hallo-knooppunt wordt gevonden, deze moet worden geretourneerd alleen als Hallo-knooppunt is afgesloten.

tooverify hello fout van een perspectief test, Hallo test moet tooknow dat wanneer deze fout is veroorzaakt, Hallo fout daadwerkelijk gebeurt. Hallo-garantie van Service Fabric bevat is dat een van de knooppunten Hallo zal of al was niet actief wanneer de opdracht Hallo Hallo knooppunt bereikt. In beide case Hallo moet test worden kunnen toocorrectly reden over Hallo status en slagen of mislukken correct in de validatie. Een systeem buiten de Service Fabric toodo Hallo die dezelfde set fouten kunnen hit die veel netwerk, hardware en softwareproblemen die u ervoor zorgen deze dat wilt Hallo voorgaande garanties geïmplementeerd. In de aanwezigheid van Hallo problemen vermeld voordat Service Fabric zal Hallo cluster status toowork rond Hallo problemen opnieuw configureren, en daarom Hallo veroorzaakt Analysis Service Hallo wordt nog steeds worden kunnen toogive Hallo rechts ingesteld van garanties.

### <a name="generating-required-events-and-scenarios"></a>Scenario's en vereiste gebeurtenissen genereren
Een werkelijke storing consistent simuleren is robuust toostart met, Hallo mogelijkheid toogenerate gecorreleerde fouten is zelfs verscherping. Bijvoorbeeld, een verlies van gegevens in een stateful service persistente wanneer gebeurt Hallo dingen volgende gebeuren:

1. Alleen een quorum van schrijven van Hallo replica's zijn bijgewerkt voor de replicatie. Alle Hallo secundaire replica's lag achter Hallo primaire.
2. Hallo schrijven quorum wordt uitgeschakeld vanwege Hallo replica's tijdelijk niet beschikbaar (vervaldatum tooa codepakket of knooppunt tijdelijk niet beschikbaar).
3. Hallo schrijven quorum kan niet terugkeren van omdat Hallo-gegevens voor Hallo replica's verloren gaat (vervaldatum toodisk beschadiging of machine teruggezet).

Deze gecorreleerde storingen in de praktijk hello, maar niet zo vaak als afzonderlijke fouten optreden. Hallo mogelijkheid tootest voor deze scenario's voordat ze in productie optreden is essentieel. Zelfs belangrijker wordt Hallo mogelijkheid toosimulate deze scenario's met de productie-workloads in gecontroleerde omstandigheden (Hallo midden van de dag Hallo met alle engineers op dek). Dat is beter dan dat het programma worden uitgevoerd voor Hallo eerst in de productieomgeving om 2:00 uur

### <a name="unified-experience-across-different-environments"></a>Geïntegreerde ervaring in verschillende omgevingen
Hallo-procedure is normaal gesproken toocreate drie verschillende sets van ervaringen, één voor de ontwikkelomgeving hello, één voor de tests en één voor productie. Hallo-model is:

1. In Hallo-ontwikkelomgeving produceren statusovergangen waarmee controles van afzonderlijke methoden.
2. In de testomgeving Hallo fouten tooallow end-to-end tests dat oefening verschillende scenario's voor de fout te produceren.
3. Houd Hallo productie-omgeving nieuw tooprevent eventuele niet natuurlijke fouten en er is zeer snelle menselijke antwoord toofailure tooensure.

In Service Fabric via Hallo veroorzaakt Analysis Service, wordt een tooturn dit rond en gebruik Hallo dezelfde methodologie van ontwikkelaars omgeving tooproduction. Er zijn twee manieren tooachieve dit:

1. tooinduce beheerd fouten, Hallo veroorzaakt Analysis Service-API's vanuit een 1-box-omgeving gebruiken alle Hallo manier tooproduction clusters.
2. Hallo toogive cluster een KVP dat ervoor zorgt dat automatische doen ontstaan van fouten, gebruik Hallo Analysis Services-fout toogenerate automatische fouten. Beheren Hallo percentage mislukte via configuratie kunt Hallo dezelfde service toobe anders in verschillende omgevingen getest.

Met Service Fabric, hoewel Hallo schaal van fouten in verschillende omgevingen hello, anders zou Hallo werkelijke mechanismen niet identiek zijn. Hierdoor kan een veel sneller code-implementatie-pijplijn en Hallo mogelijkheid tootest Hallo services onder echte laadt.

## <a name="using-hello-fault-analysis-service"></a>Hallo-fout Analysis Service gebruiken
**C#**

Fout met betrekking tot Analysis Services-functies zijn in Hallo System.Fabric naamruimte in Hallo Microsoft.ServiceFabric NuGet-pakket. Hallo nuget-pakket bevatten toouse Hallo veroorzaakt Analysis Service-functies als een verwijzing in uw project.

**PowerShell**

toouse PowerShell, moet u Hallo Service Fabric SDK installeren. Na de SDK is geïnstalleerd, Hallo Hallo ServiceFabric PowerShell-module is automatisch voor u toouse geladen.

## <a name="next-steps"></a>Volgende stappen
toocreate echt cloud scale-services is kritieke tooensure vóór en na de implementatie van dat services werkelijkheid fouten kunnen tolereren. In vandaag Hallo services wereld, Hallo mogelijkheid tooinnovate snel en verplaats code tooproduction snel is erg belangrijk. Hallo-fout Analysis Service helpt service ontwikkelaars toodo nauwkeurig dat.

Beginnen met het testen van uw toepassingen en services met behulp van de ingebouwde Hallo ['s testen](service-fabric-testability-scenarios.md), of maak uw eigen Testscenario's met behulp van Hallo [acties fault](service-fabric-testability-actions.md) geleverd door Hallo veroorzaakt Analysis Services.

<!--Image references-->
[0]: ./media/service-fabric-testability-overview/faultanalysisservice.png

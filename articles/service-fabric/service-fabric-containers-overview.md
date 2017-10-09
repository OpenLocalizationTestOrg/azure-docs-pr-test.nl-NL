---
title: aaaOverview van Service Fabric en containers | Microsoft Docs
description: Een overzicht van Service Fabric en Hallo gebruik van containers toodeploy microservice-toepassingen. Dit artikel bevat een overzicht van hoe containers kunnen worden gebruikt en Hallo beschikbaar mogelijkheden in Service Fabric.
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: c98b3fcb-c992-4dd9-b67d-2598a9bf8aab
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: fce94c4b476351c90f23f706aab8bc17319cce22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-and-containers"></a>Service Fabric en containers
> [!NOTE]
> Deze functie is Preview-versie voor Linux.  Implementatie van containers tooa Service Fabric-cluster in Windows 10 wordt niet ondersteund nog (binnenkort). 
>   

## <a name="introduction"></a>Inleiding
Azure Service Fabric is een [orchestrator](service-fabric-cluster-resource-manager-introduction.md) van services in een cluster van machines met jaar gebruiks- en optimalisatie in grootschalige services bij Microsoft. Services kunnen worden ontwikkeld op tal van manieren via Hallo [Service Fabric modellen programming](service-fabric-choose-framework.md) toodeploying [Gast uitvoerbare bestanden](service-fabric-deploy-existing-app.md). Standaard wordt Service Fabric implementeert en deze services als processen wordt geactiveerd. Processen bieden de snelste activation Hallo en hoogste dichtheid gebruik van Hallo bronnen in een cluster. Service Fabric kunnen ook services implementeren in container-installatiekopieën. Belangrijker nog, kunt u services in processen en services in containers in Hallo elkaar dezelfde toepassing. 

## <a name="containers-and-service-fabric-roadmap"></a>Containers en Service Fabric-roadmap
Veel verbeteringen zijn in toekomstige releases gepland voor de container orchestration met Service Fabric. Verbeteringen bestaan onder andere functies voor verbeterde netwerken met ondersteuning voor virtuele netwerken in een toepassing, beveiligingsfuncties, verbeterde diagnostische gegevens en het hulpprogramma-ondersteuning. Service Fabric kunt u de combinatie van containers die zijn verpakt met bestaande code (bijvoorbeeld IIS MVC-apps) met services die zijn ontwikkeld met Hallo Service Fabric-programmeermodellen toocreate-toepassingen.  U kunt verschillende dergelijke toepassingen uitvoeren op één cluster. 

## <a name="what-are-containers"></a>Wat zijn containers?
Containers worden ingekapseld, afzonderlijk implementeerbare onderdelen die worden uitgevoerd als geïsoleerde gevallen op Hallo dezelfde kernel tootake profiteren van virtualisatie die een besturingssysteem biedt. Dus elke toepassing en de runtime, afhankelijkheden en system-bibliotheken worden uitgevoerd binnen een container met volledige, persoonlijke toegang toohello container eigen geïsoleerde weergave van besturingssysteem constructies. Samen met draagbaarheid is deze mate van beveiliging en resource isolatie Hallo belangrijkste voordeel voor het gebruik van containers met Service Fabric, die anders services in processen worden uitgevoerd.

Containers zijn een virtualisatietechnologie die Hallo onderliggende besturingssysteem van toepassingen virtualiseert. Containers bieden een niet-wijzigbaar omgeving voor toorun toepassingen met verschillende mate van isolatie. Containers rechtstreeks boven op Hallo kernel uitvoeren en hebben een geïsoleerd beeld van het bestandssysteem Hallo en andere bronnen. Vergeleken toovirtual machines containers hebben Hallo volgende voordelen:

* **Kleine**: Containers gebruiken een enkel ruimte en laag versies en updates tooincrease opslagruimte.
* **Snel**: Containers geen tooboot een volledige besturingssysteem, zodat deze veel sneller, doorgaans in seconden opstarten kunnen.
* **Draagbaarheid**: de installatiekopie van een beperkte toepassing overbrengen toorun in de cloud hello, on-premises, binnen de virtuele machines of rechtstreeks op fysieke computers kan worden.
* **Resource governance**: een container Hallo fysieke resources die deze kan worden gebruikt op de host kunt beperken.

## <a name="container-types"></a>Containertypen
Service Fabric ondersteunt containers op Linux- en Windows, en biedt ook ondersteuning voor Hyper-V-isolatiemodus op Hallo laatste. 

### <a name="docker-containers-on-linux"></a>Docker-containers op Linux
Docker biedt op hoog niveau API's toocreate en beheer containers boven op Linux kernel containers. Docker-Hub is een centrale opslagplaats toostore en ophalen van installatiekopieën van de container.
Zie voor een zelfstudie [implementeert een Docker-container tooService Fabric](service-fabric-get-started-containers-linux.md).

### <a name="windows-server-containers"></a>Windows Server-containers
Windows Server 2016 biedt twee verschillende soorten containers die Hallo niveau van de opgegeven isolatie van elkaar verschillen. Windows Server-containers en Docker-containers zijn vergelijkbaar, omdat zowel de naamruimte en de bestandsnaam system isolatie maar share Hallo kernel met Hallo host die ze worden uitgevoerd. Op Linux, deze isolatie oudsher is geleverd door `cgroups` en `namespaces`, en Windows Server-containers hetzelfde gedrag vertonen.

Windows Hyper-V-containers bieden meer isolatie en beveiligingsvereisten omdat elke container Hallo besturingssysteemkernel niet met andere containers of Hallo host delen. Met deze hoger niveau van beveiliging, isolatie, worden de Hyper-V-containers gericht op onveilige, multitenant-scenario's.
Zie voor een zelfstudie [implementeren van een Windows-container tooService Fabric](service-fabric-get-started-containers.md).

Hallo volgende afbeelding toont Hallo verschillende typen van netwerkvirtualisatie en -isolatie zijn beschikbaar in besturingssysteem Hallo.
![Service Fabric-platform][Image1]

## <a name="scenarios-for-using-containers"></a>Scenario's voor het gebruik van containers
Hier volgen typische voorbeelden waar een container een goede keuze is:

* **IIS lift- en verschuiven**: als u bestaande hebt [ASP.NET MVC](https://www.asp.net/mvc) apps die u wilt dat toocontinue toouse, plaatst u deze in een container in plaats van ze tooASP.NET Core migreren. Deze apps ASP.NET MVC afhankelijk zijn van op Internet Information Services (IIS). U kunt deze toepassingen in container afbeeldingen van Hallo precreated IIS installatiekopie van het pakket en implementeren met Service Fabric. Zie [Container afbeeldingen op Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/quick_start/quick_start_images) voor informatie over het toocreate IIS installatiekopieën.
* **Meng containers en Service Fabric microservices**: een installatiekopie van een bestaande container gebruiken voor een deel van uw toepassing. Bijvoorbeeld, kunt u Hallo [NGINX-container](https://hub.docker.com/_/nginx/) voor Hallo webfront-end van uw toepassing en stateful services voor Hallo intensievere berekening van de back-end.
* **De gevolgen van de 'ruis neighbors' services**: U kunt Hallo resource governance mogelijkheid van containers toorestrict Hallo resources die gebruikmaakt van een service op een host. Als services kunnen veel resources in beslag nemen en invloed hebben op prestaties Hallo van anderen (zoals een langlopende, query-achtige-bewerking), kunt u deze services in de containers die resource governance stellen.

## <a name="service-fabric-support-for-containers"></a>Service Fabric-ondersteuning voor containers
Service Fabric ondersteunt momenteel de implementatie van Docker-containers voor Linux en Windows Server-containers op Windows Server 2016, evenals ondersteuning voor Hyper-V-isolatiemodus. 

In Service Fabric Hallo [toepassingsmodel](service-fabric-application-model.md), een container vertegenwoordigt een toepassingshost welke service meerdere replica's worden geplaatst. Service Fabric geen containers kunt uitvoeren en Hallo scenario is vergelijkbaar toohello [Gast uitvoerbare scenario](service-fabric-deploy-existing-app.md), waar u een bestaande toepassing binnen een container van het pakket. Dit scenario is Hallo algemene use case voor containers en uitvoeren van een toepassing die is geschreven met behulp van elke taal of frameworks, maar niet met behulp van Hallo ingebouwde Service Fabric programmeermodellen enkele voorbeelden.

Bovendien kunt u een Service Fabric-services in containers ook uitvoeren. Ondersteuning voor actieve Service Fabric-services in containers is beperkt op dit moment maar toobe verbeterd in toekomstige releases.

* **Betrouwbare Stateless services in containers**: betrouwbare Stateless services met behulp van Hallo Reliable Services programmeermodellen worden alleen ondersteund op Linux. Ondersteuning voor betrouwbare Stateless services in Windows-containers is gepland voor een toekomstige release.
* **Stateful services in containers**: deze services Hallo Reliable Actors of Reliable Services programmeermodel gebruiken. Ondersteuning voor stateful services worden uitgevoerd in containers wordt toegevoegd in de toekomst vrijgeven.

Service Fabric heeft diverse container mogelijkheden waarmee u toepassingen maken die bestaan uit een van microservices die beperkte zijn. Service Fabric biedt Hallo mogelijkheden voor beperkte services te volgen:

* Implementatie van de container en activering.
* Resource governance.
* Verificatie van de opslagplaats.
* Container toohost poort poorttoewijzing.
* Detectie van de container-naar-container en communicatie.
* Mogelijkheid tooconfigure en omgevingsvariabelen worden ingesteld.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd over containers dat Service Fabric is een container orchestrator en dat het Service Fabric bevat functies die ondersteuning bieden voor containers. Een volgende stap we gaan over voorbeelden van elke Hallo functies tooshow u hoe toouse ze.

[Een Windows-container tooService Fabric op Windows Server 2016 implementeren](service-fabric-get-started-containers.md)

[Implementeert een Docker-container tooService Fabric op Linux](service-fabric-get-started-containers-linux.md)

[Image1]: media/service-fabric-containers/Service-Fabric-Types-of-Isolation.png

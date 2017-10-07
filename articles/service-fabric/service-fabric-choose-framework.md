---
title: aaaService Fabric programming model overzicht | Microsoft Docs
description: 'Service Fabric biedt twee frameworks voor het bouwen van services: Hallo actor framework en Hallo serviceframework. Ze bieden verschillende verschillen in eenvoud en controle.'
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: vturecek
ms.assetid: 974b2614-014e-4587-a947-28fcef28b382
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: vturecek
ms.openlocfilehash: b48af2a7b41935bdf0e4594c765f363e520c254e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-programming-model-overview"></a>Overzicht van service Fabric programming model
Service Fabric biedt meerdere manieren toowrite en beheren van uw services. Services kunt toouse Hallo Service Fabric-API's tootake volledig gebruikmaken van de functies en toepassingsframeworks Hallo-platform. Services kunnen ook worden alle gecompileerde uitvoerbaar programma geschreven in elke taal of de code die wordt uitgevoerd in een container gewoon worden gehost op een Service Fabric-cluster.

## <a name="guest-executables"></a>Gast uitvoerbare bestanden
Een [Gast uitvoerbaar bestand](service-fabric-deploy-existing-app.md) is een bestaande willekeurige uitvoerbaar bestand (geschreven in een andere taal) en dat kan worden uitgevoerd als een service in uw toepassing. Uitvoerbare bestanden Gast Hallo Service Fabric SDK-API's niet rechtstreeks aangeroepen. Maar ze nog steeds profiteren van functies Hallo platform biedt, zoals zichtbaarheid van de service, aangepaste gezondheid en load reporting door het aanroepen van REST-API's die worden weergegeven door de Service Fabric. Ze hebben ook de volledige toepassing lifecycle ondersteuning.

Aan de slag met gast uitvoerbare bestanden door het implementeren van uw eerste [Gast uitvoerbare toepassing](service-fabric-deploy-existing-app.md).

## <a name="containers"></a>Containers
Standaard wordt Service Fabric implementeert en services als processen wordt geactiveerd. Service Fabric kunnen ook services implementeren in [containers](service-fabric-containers-overview.md). Service Fabric ondersteunt de implementatie van containers voor Linux en Windows-containers op Windows Server 2016. Container installatiekopieën kunnen worden opgehaald uit de opslagplaats voor elke container en toohello machine geïmplementeerd. Kunt u bestaande toepassingen implementeren als gast exectuables, Service Fabric stateless of stateful Reliable services of Reliable Actors in containers, en u kunnen combineren services in processen en -services in containers in dezelfde toepassing hello.

[Meer informatie over uw services in Windows of Linux containerizing](service-fabric-deploy-container.md)

## <a name="reliable-services"></a>Reliable Services
Reliable Services is een lichtgewicht framework voor het schrijven van services die integreren met Hallo Service Fabric-platform en profiteren van de volledige set Hallo van platformfuncties. Betrouwbare Services bieden een minimale set API's waarmee Hallo Service Fabric-runtime toomanage Hallo levenscyclus van uw services en waarmee uw toointeract services met Hallo-runtime. Hallo-toepassingsframework is minimaal, zodat u volledige controle over het ontwerp en de implementatie-opties en gebruikte toohost andere toepassingsframework, zoals ASP.NET Core kan worden.

Reliable Services kunnen worden staatloze, vergelijkbaar toomost service platforms, zoals webservers, waarbij elk exemplaar van de service Hallo gelijk wordt gemaakt en status is opgeslagen in een externe oplossing, zoals Azure DB of Azure Table Storage.

Reliable Services kunnen ook stateful, exclusieve tooService Fabric worden waar status rechtstreeks in het Hallo-service zelf betrouwbare verzamelingen is opgeslagen. Staat het maken van maximaal beschikbare door middel van replicatie en gedistribueerd via partitioneren, alle beheerde automatisch door de Service Fabric.

[Meer informatie over Reliable Services](service-fabric-reliable-services-introduction.md) of aan de slag door [schrijven van uw eerste betrouwbare Service](service-fabric-reliable-services-quick-start.md).

## <a name="reliable-actors"></a>Reliable Actors
Gebouwd op Reliable Services, is Hallo betrouwbare Actor-framework een toepassingsframework dat Hallo virtuele Actor patroon, op basis van Hallo actor ontwerppatroon implementeert. onafhankelijke eenheden van de berekenings- en status Hallo betrouwbare Actor-framework gebruikt met één thread uitvoering actoren aangeroepen. Hallo betrouwbare Actor-framework biedt ingebouwde communicatie voor actors en vooraf ingestelde status persistentie en scale-out-configuraties.

Als Reliable Actors zelf een toepassingsframework dat is gebaseerd op Reliable Services is, is het volledig geïntegreerd met Hallo Service Fabric-platform en voordelen van Hallo volledige set met functies die worden aangeboden door het Hallo-platform.

[Meer informatie over Reliable Actors](service-fabric-reliable-actors-introduction.md) of aan de slag door [schrijven van uw eerste betrouwbare Actor-service](service-fabric-reliable-actors-get-started.md)

## <a name="aspnet-core"></a>ASP.NET Core
Service Fabric kan worden geïntegreerd met [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) voor het ontwikkelen van Web- en API-services die kan worden opgenomen als onderdeel van uw toepassing. 

[Een front-end-service met behulp van ASP.NET Core bouwen](service-fabric-add-a-web-frontend.md)

## <a name="next-steps"></a>Volgende stappen
[Overzicht van service Fabric en containers](service-fabric-containers-overview.md)

[Overzicht van betrouwbare Services](service-fabric-reliable-services-introduction.md)

[Overzicht van betrouwbare Services](service-fabric-reliable-actors-introduction.md)

[Service Fabric- en ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)





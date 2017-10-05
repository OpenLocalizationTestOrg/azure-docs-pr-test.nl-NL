---
title: Beschikbaarheid van Service Fabric-services | Microsoft Docs
description: Hierin wordt beschreven foutenopsporing, failovers en herstel voor services
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 279ba4a4-f2ef-4e4e-b164-daefd10582e4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 41ff2c3129facb0eea9d896ce75d7343ae2a018e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="availability-of-service-fabric-services"></a>Beschikbaarheid van Service Fabric-services
In dit artikel biedt een overzicht van hoe de beschikbaarheid van een service voor het onderhouden van Service Fabric.

## <a name="availability-of-service-fabric-stateless-services"></a>Beschikbaarheid van Service Fabric stateless services
Azure Service Fabric-services kunnen stateful of stateless zijn. Een stateless service is een toepassingsservice die geen [lokale status](service-fabric-concepts-state.md) dat moet worden maximaal beschikbaar of betrouwbaar.

Het maken van een stateless service moet definiëren van een `InstanceCount`. Het aantal exemplaren definieert het aantal exemplaren van de staatloze service toepassingslogica die moet worden uitgevoerd in het cluster. Het aantal exemplaren is de aanbevolen manier van een staatloze service uitbreiden.

Wanneer een exemplaar van staatloze service met de naam is mislukt, wordt een nieuw exemplaar gemaakt op een bepaald in aanmerking komende knooppunt in het cluster. Bijvoorbeeld, een stateless service-exemplaar op knooppunt1 mislukken en opnieuw worden gemaakt op Knooppunt5.

## <a name="availability-of-service-fabric-stateful-services"></a>Beschikbaarheid van Service Fabric stateful services
Een stateful service heeft een status die is gekoppeld aan deze. Een stateful service is in Service Fabric gemodelleerd als een set van replica's. Elke replica is een actief exemplaar van de code van de service die ook een kopie van de status voor de service heeft. Lezen en schrijven bewerkingen worden uitgevoerd op één replica (de primaire genoemd). Schrijven van wijzigingen in de status van bewerkingen zijn *gerepliceerd* aan de andere replica's in de replicaset (aangeroepen actieve secundaire replica's) en toegepast. 

Er mag slechts één primaire replica kunnen, maar er meerdere actieve secundaire replica's zijn. Het aantal actieve secundaire replica's kan worden geconfigureerd en een hoger aantal replica's tolereert een groter aantal gelijktijdige software en hardwarefouten.

Als de primaire replica uitgeschakeld wordt, Service Fabric kunt u een van de actieve secundaire replica's de nieuwe primaire replica. Deze actieve secundaire replica is al de bijgewerkte versie van de status (via *replicatie*), en deze kunt doorgaan met het verwerken van verdere lees- en schrijfbewerkingen.

Dit concept, van een replica wordt een primaire of secundaire Active staat bekend als de Replica-rol.

### <a name="replica-roles"></a>Replica-functies
De rol van een replica wordt gebruikt voor het beheren van de levenscyclus van de status wordt beheerd door die replica. Een replica wie de rol primaire services is schijfleesaanvragen. De primaire worden ook alle schrijfaanvragen verwerkt door het bijwerken van de status en het repliceren van de wijzigingen. Deze wijzigingen worden toegepast op de actieve secundaire replica's in de replicaset. De taak van een actieve secundaire is ontvangen statuswijzigingen die de primaire replica is gerepliceerd en het bijwerken van de weergave van de status.

> [!NOTE]
> Een hoger niveau programmering modellen zoals [Reliable Actors](service-fabric-reliable-actors-introduction.md) en [Reliable Services](service-fabric-reliable-services-introduction.md) verbergen van het concept van de replicarol van de ontwikkelaar. In actoren is het begrip van de rol overbodig, terwijl in Services het grotendeels voor de meeste scenario wordt vereenvoudigd.
>

## <a name="next-steps"></a>Volgende stappen
Zie de volgende artikelen voor meer informatie over Service Fabric-concepten:

- [Schalen van Service Fabric-services](service-fabric-concepts-scalability.md)
- [Partitionering Service Fabric-services](service-fabric-concepts-partitioning.md)
- [Definiëren en beheren van status](service-fabric-concepts-state.md)
- [Reliable Services](service-fabric-reliable-services-introduction.md)

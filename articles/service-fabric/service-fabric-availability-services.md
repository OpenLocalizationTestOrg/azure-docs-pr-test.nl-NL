---
title: aaaAvailability van Service Fabric-services | Microsoft Docs
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
ms.openlocfilehash: c443aadfe31a1413359b08d34c4b7dd5db4edd16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="availability-of-service-fabric-services"></a>Beschikbaarheid van Service Fabric-services
In dit artikel biedt een overzicht van hoe de beschikbaarheid van een service voor het onderhouden van Service Fabric.

## <a name="availability-of-service-fabric-stateless-services"></a>Beschikbaarheid van Service Fabric stateless services
Azure Service Fabric-services kunnen stateful of stateless zijn. Een stateless service is een toepassingsservice die geen [lokale status](service-fabric-concepts-state.md) dat toobe moet maximaal beschikbaar of betrouwbaar.

Het maken van een stateless service moet definiëren van een `InstanceCount`. aantal exemplaren op Hallo definieert Hallo aantal exemplaren van toepassingslogica Hallo staatloze service die moet worden uitgevoerd in de cluster Hallo. Aantal exemplaren Hallo verhogen is Hallo aanbevolen manier om een stateless service uitbreiden.

Wanneer een exemplaar van staatloze service met de naam is mislukt, wordt een nieuw exemplaar op sommige in aanmerking komende knooppunt in het Hallo-cluster gemaakt. Bijvoorbeeld, een stateless service-exemplaar op knooppunt1 mislukken en opnieuw worden gemaakt op Knooppunt5.

## <a name="availability-of-service-fabric-stateful-services"></a>Beschikbaarheid van Service Fabric stateful services
Een stateful service heeft een status die is gekoppeld aan deze. Een stateful service is in Service Fabric gemodelleerd als een set van replica's. Elke replica is een actief exemplaar van het Hallo-code van Hallo-service ook een kopie van Hallo staat voor de service heeft. Lezen en schrijven bewerkingen worden uitgevoerd op één replica (Hallo primaire genoemd). Wijzigingen toostate van schrijfbewerkingen zijn *gerepliceerd* toohello andere replica's in Hallo replicaset (actieve secundaire replica's genoemd) en toegepast. 

Er mag slechts één primaire replica kunnen, maar er meerdere actieve secundaire replica's zijn. Hallo aantal actieve secundaire replica's kan worden geconfigureerd en een hoger aantal replica's tolereert een groter aantal gelijktijdige software en hardwarefouten.

Als de primaire replica Hallo uitvalt, kunt u Service Fabric een Hallo actieve secundaire replica's Hallo nieuwe primaire replica. Deze actieve secundaire replica al Hallo bijgewerkt versie van Hallo-status (via *replicatie*), en deze kunt doorgaan met het verwerken van verdere lees- en schrijfbewerkingen.

Dit concept, van een replica wordt een primaire of secundaire Active staat bekend als Hallo Replicarol.

### <a name="replica-roles"></a>Replica-functies
Hallo-rol van een replica is gebruikte toomanage Hallo levenscyclus van Hallo status wordt beheerd door die replica. Een replica wie de rol primaire services is schijfleesaanvragen. alle schrijfaanvragen verwerkt Hallo primaire tevens door de status bijwerken en het Hallo-wijzigingen te repliceren. Deze wijzigingen zijn toegepast toohello actieve secundaire replica's in Hallo replicaset. Hallo-taak van een actieve secundaire is tooreceive statuswijzigingen die Hallo primaire replica is gerepliceerd en de weergave van Hallo status bijwerken.

> [!NOTE]
> Een hoger niveau programmering modellen zoals [Reliable Actors](service-fabric-reliable-actors-introduction.md) en [Reliable Services](service-fabric-reliable-services-introduction.md) Hallo begrip van de replicarol van de ontwikkelaar Hallo verbergen. In actoren is Hallo begrip van de rol overbodig, terwijl in Services het grotendeels voor de meeste scenario wordt vereenvoudigd.
>

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over Service Fabric-concepten Hallo artikelen te volgen:

- [Schalen van Service Fabric-services](service-fabric-concepts-scalability.md)
- [Partitionering Service Fabric-services](service-fabric-concepts-partitioning.md)
- [Definiëren en beheren van status](service-fabric-concepts-state.md)
- [Reliable Services](service-fabric-reliable-services-introduction.md)

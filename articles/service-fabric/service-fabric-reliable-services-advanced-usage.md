---
title: aaaAdvanced gebruik van Reliable Services | Microsoft Docs
description: Meer informatie over de geavanceerde informatie over het gebruik van de Service Fabric Reliable Services voor extra flexibiliteit in uw services.
services: Service-Fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: masnider
ms.assetid: f2942871-863d-47c3-b14a-7cdad9a742c7
ms.service: Service-Fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: e6d6310a4deae9edcfcd76551e1337f0e39e9e5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-usage-of-hello-reliable-services-programming-model"></a>Informatie over het gebruik van Hallo Reliable Services programmeermodel geavanceerde
Azure Service Fabric vereenvoudigt schrijven en betrouwbare staatloze en stateful services beheren. Deze handleiding wordt gesproken over geavanceerde gebruik van Reliable Services toogain meer controle en flexibiliteit via uw services. Eerdere tooreading deze handleiding, raken met [Hallo Reliable Services programmeermodel](service-fabric-reliable-services-introduction.md).

Stateful en staatloze services hebben twee primaire ingangspunten voor gebruikerscode:

* `RunAsync(C#) / runAsync(Java)`is een algemene toegangspunt voor uw servicecode.
* `CreateServiceReplicaListeners(C#)`en `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` is voor het openen van communicatielisteners voor clientaanvragen.

Voor de meeste services zijn deze twee ingangspunten voldoende. In zeldzame gevallen wanneer meer controle over de levenscyclus van een service vereist is, de levenscyclus van aanvullende gebeurtenissen zijn beschikbaar.

## <a name="stateless-service-instance-lifecycle"></a>Levenscyclus van staatloze service-exemplaar
Er is een staatloze service lifecycle zeer eenvoudig. Een stateless service kan alleen worden geopend, gesloten of afgebroken. `RunAsync`in een stateless service wordt uitgevoerd wanneer een service-exemplaar wordt geopend en wanneer een service-exemplaar is gesloten of afgebroken geannuleerd.

Hoewel `RunAsync` moet voldoende in bijna alle gevallen Hallo geopend, sluit en gebeurtenissen in een stateless service afbreken zijn ook beschikbaar:

* `Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java`OnOpenAsync wordt aangeroepen wanneer Hallo staatloze service-exemplaar over toobe gebruikt is. Initialisatie van uitgebreide servicetaken kunnen op dit moment worden gestart.
* `Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java`OnCloseAsync wordt aangeroepen wanneer Hallo staatloze service-exemplaar toobe gaat probleemloos afsluiten. Dit kan gebeuren wanneer Hallo servicecode wordt bijgewerkt, Hallo service-exemplaar is verplaatst vanwege tooload netwerktaakverdeling of een tijdelijke fout wordt gedetecteerd. OnCloseAsync kunt sluiten gebruikte toosafely worden alle resources, eventuele achtergrondverwerking stoppen, hebt opgeslagen status van externe of bestaande verbindingen afgesloten.
* `void OnAbort() - C# / void onAbort() - Java`OnAbort wordt aangeroepen wanneer Hallo staatloze service-exemplaar geforceerd wordt afgesloten. Dit wordt doorgaans als een permanente storing wordt gedetecteerd op Hallo-knooppunt, of wanneer het Service Fabric niet betrouwbaar Hallo service-exemplaar van de levenscyclus van vanwege fouten toointernal beheren genoemd.

## <a name="stateful-service-replica-lifecycle"></a>Levenscyclus van de replica stateful service

> [!NOTE]
> Stateful betrouwbare services worden nog niet ondersteund in Java.
>
>

De levenscyclus van een stateful service-replica is veel complexer dan staatloze service-exemplaar. Bovendien tooopen, sluiten en afbreken van gebeurtenissen, een stateful service replica rol ondergaat tijdens de levensduur. Wanneer een replica stateful service rol wordt gewijzigd, Hallo `OnChangeRoleAsync` gebeurtenis wordt geactiveerd:

* `Task OnChangeRoleAsync(ReplicaRole, CancellationToken)`OnChangeRoleAsync wordt aangeroepen wanneer Hallo stateful service replica-rol, bijvoorbeeld tooprimary of secundaire site wordt gewijzigd. Primaire replica's worden vermeld write-status (toocreate zijn toegestaan en tooReliable verzamelingen schrijven). Secundaire replica's zijn opgegeven leesstatus (kan alleen worden gelezen van bestaande betrouwbare verzamelingen). De meeste werk in een stateful service wordt uitgevoerd op de primaire replica Hallo. Secundaire replica's kunnen uitvoeren voor validatie van alleen-lezen, rapport genereren, gegevensanalyse of andere taken alleen-lezen.

In een stateful service alleen Hallo primaire replica heeft schrijftoegang toostate en dus wordt doorgaans wanneer Hallo service echte werk wordt uitgevoerd. Hallo `RunAsync` methode in een stateful service wordt alleen uitgevoerd wanneer de Hallo stateful service replica primaire is. Hallo `RunAsync` methode wordt geannuleerd als een primaire replica rol wijzigingen weg van primaire, evenals tijdens Hallo sluit en gebeurtenissen afbreken.

Met behulp van Hallo `OnChangeRoleAsync` gebeurtenis kunt u tooperform werk, afhankelijk van de replicarol ook zoals in het antwoord toorole wijzigen.

Een stateful service biedt ook Hallo dezelfde vier lifecycle gebeurtenissen als een stateless service gebruiksscenario's Hallo dezelfde heeft:

```csharp
* Task OnOpenAsync(IStatefulServicePartition, CancellationToken)
* Task OnCloseAsync(CancellationToken)
* void OnAbort()
```

## <a name="next-steps"></a>Volgende stappen
Zie voor meer geavanceerde onderwerpen gerelateerde tooService Fabric, Hallo artikelen te volgen:

* [Configureren van stateful Reliable Services](service-fabric-reliable-services-configuration.md)
* [Service Fabric health Inleiding](service-fabric-health-introduction.md)
* [Systeemstatusrapporten gebruiken voor het oplossen van problemen](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Services configureren met Hallo Service Fabric-Cluster Resource Manager](service-fabric-cluster-resource-manager-configure-services.md)

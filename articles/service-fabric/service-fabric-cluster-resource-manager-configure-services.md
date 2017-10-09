---
title: aaaSpecify metrische gegevens en plaatsing van de instellingen in Azure microservices | Microsoft Docs
description: Met een beschrijving van een Service Fabric-service door metrische gegevens, plaatsingsbeperkingen en andere plaatsingsbeleid te geven.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 16e135c1-a00a-4c6f-9302-6651a090571a
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c633518b5dbf0c7b84e0d46c06bf1f92365d184d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-cluster-resource-manager-settings-for-service-fabric-services"></a>Cluster resource manager-instellingen voor Service Fabric-services configureren
Hallo Service Fabric-Cluster Resource Manager kunt fijnmazig besturen Hallo-regels die bepalen van elke afzonderlijke service met de naam. Elke benoemde service kunt regels voor hoe moet worden toegewezen in Hallo cluster opgeven. Elke benoemde service kunt Hallo set van metrische gegevens dat deze wil tooreport, met inbegrip van hoe belangrijk ze zijn toothat service ook definiëren. Configureren van services uitvalt in drie verschillende taken:

1. Plaatsingsbeperkingen configureren
2. Metrische gegevens configureren
3. Configureren van geavanceerde plaatsingsbeleid en andere regels (minder algemeen)

## <a name="placement-constraints"></a>Plaatsingsbeperkingen
Plaatsingsbeperkingen zijn gebruikte toocontrol welke knooppunten in cluster Hallo een service kunt daadwerkelijk uitvoeren op. Doorgaans een bepaalde service-exemplaar of alle services van een bepaald type beperkte toorun op een bepaald type knooppunt genoemd. Plaatsingsbeperkingen worden uitgebreid. U kunt een set eigenschappen per knooppunttype definiëren en vervolgens selecteren ze met beperkingen bij het maken van services. U kunt ook een service plaatsingsbeperkingen wijzigen terwijl deze wordt uitgevoerd. Hiermee kunt u toorespond toochanges in Hallo cluster of Hallo vereisten van Hallo-service. Hallo-eigenschappen van een bepaald knooppunt kunnen ook dynamisch worden bijgewerkt in Hallo-cluster. Meer informatie over plaatsingsbeperkingen en hoe tooconfigure ze kunnen worden gevonden [in dit artikel](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)

## <a name="metrics"></a>Metrische gegevens
Meetgegevens voor Hallo set resources die een bepaalde benoemde service moet zijn. Configuratie van de service omvat hoeveel van de bron elke stateful replica of stateless exemplaar van die service standaard verbruikt. Metrische gegevens behoren ook een gewicht dat hoe belangrijk dat metriek balancing toothat-service aangeeft als voor-en nadelen nodig zijn.

## <a name="advanced-placement-rules"></a>Van geavanceerde plaatsingsregels
Er zijn andere typen regels die handig in een minder algemene scenario's zijn voor de plaatsing. Een aantal voorbeelden:
- Beperkingen die u bij geografisch verspreide clusters helpen
- Bepaalde toepassingsarchitecturen

Andere plaatsingsregels zijn via correlaties of beleidsregels geconfigureerd.

## <a name="next-steps"></a>Volgende stappen
- Metrische gegevens zijn hoe Hallo Service Fabric-Cluster Resource Manager beheert gebruiks- en capaciteit in Hallo-cluster. meer informatie over metrische gegevens toolearn en hoe tooconfigure, Bekijk [in dit artikel](service-fabric-cluster-resource-manager-metrics.md)
- Affiniteit is één modus die u voor uw services configureren kunt. Wordt meestal niet, maar als u deze nodig hebt u meer over deze [hier](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
- Er zijn veel verschillende plaatsingsregels die op uw service toohandle aanvullende scenario's kunnen worden geconfigureerd. U vindt informatie over deze beleidsregels voor verschillende plaatsing [hier](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)
- Vanaf Hallo begin starten en [ophalen van een inleiding toohello Service Fabric-Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)
- toofind uit over hoe Hallo Cluster Resource Manager beheert en een compromis tussen de werklast van de cluster Hallo, bekijk Hallo artikel op [load balancing](service-fabric-cluster-resource-manager-balancing.md)
- Hallo Cluster Resource Manager heeft veel opties voor het beschrijven van Hallo-cluster. toofind voor meer informatie over deze Raadpleeg dit artikel op [met een beschrijving van een Service Fabric-cluster](service-fabric-cluster-resource-manager-cluster-description.md)

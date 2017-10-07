---
title: aaaThrottling in Hallo Service Fabric-cluster resourcemanager | Microsoft Docs
description: Meer informatie over tooconfigure Hallo vertragingen geleverd door Hallo Service Fabric-Cluster Resource Manager.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4a44678b-a5aa-4d30-958f-dc4332ebfb63
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f418536911d3e3814e78a4d9f057dfb867ca7c63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-hello-service-fabric-cluster-resource-manager"></a>Beperking van Hallo Service Fabric-Cluster Resource Manager
Zelfs als u Hallo Cluster Resource Manager correct hebt geconfigureerd, kan Hallo cluster ophalen verstoord. Bijvoorbeeld, kan er gelijktijdige knooppunt en fouttolerantie domein fouten - wat er zou gebeuren als die is opgetreden tijdens een upgrade? Hallo Cluster Resource Manager probeert altijd toofix alles van het cluster Hallo bronnen probeert tooreorganize en fix Hallo-cluster. Vertragingen zorgt voor een backstop zodat Hallo cluster resources toostabilize kunt-Hallo knooppunten terugkeren, Hallo netwerkpartities retoucheren, gecorrigeerde bits geïmplementeerd.

toohelp met dit soort situaties Hallo Service Fabric-Cluster Resource Manager bevat verschillende vertragingen. Deze vertragingen zijn alle behoorlijk groot hamers. Ze mag niet in het algemeen worden gewijzigd zonder een zorgvuldige planning en testen.

Als u Hallo Cluster Resource Manager van vertragingen wijzigt, moet u ze tooyour verwachte daadwerkelijke laadbewerking afstemmen. U bepaald moet u toohave sommige bandbreedte aanwezig is, zelfs als het Hallo-cluster duurt langer toostabilize in sommige gevallen betekent. Testen van is vereiste toodetermine Hallo juiste waarden voor vertragingen. Vertragingen moeten toobe hoog genoeg tooallow Hallo cluster toorespond toochanges binnen redelijke tijd en laag voldoende tooactually te voorkomen dat te veel resourceverbruik. 

Meestal Hallo die we klanten hebt gezien vertragingen die is nu omdat ze al aanwezig in een omgeving met beperkte resource waren gebruiken. Enkele voorbeelden voor afzonderlijke knooppunten of schijven die niet kunnen toobuild veel stateful replica's in een beperkte netwerkbandbreedte zou worden parallelle vanwege toothroughput beperkingen. Zonder vertragingen, kunnen operations deze resources, waardoor operations toofail overbelast of traag zijn. In deze situaties klanten vertragingen gebruikt en op de hoogte dat zijn ze Hallo hoeveelheid tijd die nodig zou Hallo cluster tooreach geen stabiele status uitbreiden. Klanten ook begrepen dat ze kunnen terechtkomen op lagere algehele betrouwbaarheid actief, terwijl ze zijn beperkt.


## <a name="configuring-hello-throttles"></a>Configureren Hallo bandbreedte

Service Fabric heeft twee mechanismen voor het aantal verplaatsingen van het type replica Hallo beperking. Hallo-standaardmechanisme die bestonden voordat de Service Fabric 5.7 vertegenwoordigt beperking als een absoluut aantal verplaatst toegestaan. Dit werkt niet voor clusters van elke grootte. Met name voor grote clusters Hallo standaard is waarde te klein, aanzienlijk vertragen balancing zelfs wanneer deze nodig is, terwijl hiervoor geen effect in kleinere clusters. Dit mechanisme voorafgaande is vervangen door beperking percentage is gebaseerd, die beter bij dynamische clusters geschaald in welke Hallo aantal services en knooppunten regelmatig wijzigen.

Hallo vertragingen zijn gebaseerd op een percentage van het aantal replica's in clusters Hallo Hallo. Op basis van Percetage vertragingen uitdrukken Hallo regel inschakelen: 'niet verplaatsen meer dan 10% van de replica's in een interval van 10 minuten', bijvoorbeeld.

Hallo-configuratie-instellingen voor bandbreedtebeperking op basis van een percentage zijn:

  - GlobalMovementThrottleThresholdPercentage - verplaatsingen toegestaan in het cluster op elk gewenst moment het maximale aantal uitgedrukt als percentage van totaal aantal replica's in het Hallo-cluster. 0 geeft geen limiet. Hallo-standaardwaarde is 0. Als deze instelling en de GlobalMovementThrottleThreshold worden opgegeven, wordt klikt u vervolgens hello meer conservatief limiet gebruikt.
  - GlobalMovementThrottleThresholdPercentageForPlacement - maximumaantal verplaatsingen van het type toegestaan tijdens Hallo plaatsing fase, uitgedrukt als percentage van totaal aantal replica's in het Hallo-cluster. 0 geeft geen limiet. Hallo-standaardwaarde is 0. Als deze instelling en de GlobalMovementThrottleThresholdForPlacement worden opgegeven, wordt klikt u vervolgens hello meer conservatief limiet gebruikt.
  - GlobalMovementThrottleThresholdPercentageForBalancing - maximumaantal verplaatsingen van het type toegestaan tijdens het Hallo balancing fase, uitgedrukt als percentage van totaal aantal replica's in het Hallo-cluster. 0 geeft geen limiet. Hallo-standaardwaarde is 0. Als deze instelling en de GlobalMovementThrottleThresholdForBalancing worden opgegeven, wordt klikt u vervolgens hello meer conservatief limiet gebruikt.

Wanneer u Hallo versnellingspercentage opgeeft, geeft u 5% als 0,05. Hallo-interval waarop deze vertragingen worden geregeld is Hallo GlobalMovementThrottleCountingInterval die is opgegeven in seconden.


``` xml
<Section Name="PlacementAndLoadBalancing">
     <Parameter Name="GlobalMovementThrottleThresholdPercentage" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForPlacement" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForBalancing" Value="0" />
     <Parameter Name="GlobalMovementThrottleCountingInterval" Value="600" />
</Section>
```

gehoste clusters via ClusterConfig.json voor zelfstandige implementaties of Template.json voor Azure:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "GlobalMovementThrottleThresholdPercentage",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForPlacement",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForBalancing",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleCountingInterval",
          "value": "600"
      }
    ]
  }
]
```

### <a name="default-count-based-throttles"></a>Standaard op basis van aantal vertragingen
Deze informatie wordt geboden voor het geval u oudere clusters hebt, of behoud van deze configuraties in clusters die sindsdien zijn bijgewerkt. In het algemeen wordt aangeraden dat deze worden vervangen door Hallo percentage gebaseerde vertragingen hierboven. Aangezien bandbreedtebeperking op basis van het percentage is standaard uitgeschakeld, blijven deze vertragingen Hallo standaard vertragingen voor een cluster totdat deze zijn uitgeschakeld en door Hallo percentage gebaseerde vertragingen vervangen. 

  - GlobalMovementThrottleThreshold – deze instelling bepaalt Hallo kunt u het totale aantal verplaatsingen van het type in Hallo cluster gedurende een bepaalde periode. Hallo hoeveelheid tijd is in seconden als Hallo GlobalMovementThrottleCountingInterval opgegeven. de standaardwaarde Hallo voor Hallo GlobalMovementThrottleThreshold is 1000 en de standaardwaarde Hallo voor Hallo GlobalMovementThrottleCountingInterval 600 is.
  - MovementPerPartitionThrottleThreshold – deze instelling bepaalt Hallo kunt u het totale aantal verplaatsingen van het type voor elke partitie service gedurende een bepaalde periode. Hallo hoeveelheid tijd is in seconden als Hallo MovementPerPartitionThrottleCountingInterval opgegeven. de standaardwaarde Hallo voor Hallo MovementPerPartitionThrottleThreshold is 50 en Hallo standaardwaarde voor Hallo MovementPerPartitionThrottleCountingInterval is 600.

Hallo-configuratie voor deze vertragingen volgt Hallo hetzelfde patroon als Hallo bandbreedtebeperking op basis van een percentage.

## <a name="next-steps"></a>Volgende stappen
- toofind uit over hoe Hallo Cluster Resource Manager beheert en een compromis tussen de werklast van de cluster Hallo, bekijk Hallo artikel op [load balancing](service-fabric-cluster-resource-manager-balancing.md)
- Hallo Cluster Resource Manager heeft veel opties voor het beschrijven van Hallo-cluster. toofind voor meer informatie over deze Raadpleeg dit artikel op [met een beschrijving van een Service Fabric-cluster](service-fabric-cluster-resource-manager-cluster-description.md)

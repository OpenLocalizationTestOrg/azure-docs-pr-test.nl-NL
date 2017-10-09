---
title: aaaDefragmentation van metrische gegevens in Azure Service Fabric | Microsoft Docs
description: Een overzicht van defragmentatie gebruiken of als een strategie voor metrische gegevens in Service Fabric verpakken
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: e5ebfae5-c8f7-4d6c-9173-3e22a9730552
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: d09045a6cf196d2771f1a0794637f4579d3eb96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a>Defragmentatie van metrische gegevens en de belasting in Service Fabric
Hallo Service Fabric Cluster Resource Manager standaard strategie voor het beheren van metrische gegevens laden in het Hallo-cluster is de toodistribute Hallo belasting. Ervoor te zorgen dat de knooppunten gelijkmatig worden gebruikt, voorkomt warme en koude plaatsen die tooboth conflicten en verspilde bronnen leiden. Distributie van werkbelastingen in Hallo-cluster is ook Hallo veiligste in termen van functionerende fouten omdat Hiermee zorgt u ervoor dat een fout wordt pas uit een groot percentage van een bepaalde werkbelasting. 

Hallo Service Fabric-Cluster Resource Manager biedt ondersteuning voor een andere strategie voor het beheren van belasting, namelijk defragmentatie. Defragmentatie betekent dat in plaats van toodistribute Hallo gebruik van een metriek probeert over Hallo-cluster, het geconsolideerd. Consolidatie is slechts een omkering van Hallo standaard strategie – in plaats van voor het minimaliseren van gemiddelde standaardafwijking Hallo van metrische load balancing, Hallo Cluster Resource Manager probeert tooincrease deze.

## <a name="when-toouse-defragmentation"></a>Wanneer de defragmentatie toouse
Laden in het cluster Hallo distribueren verbruikt aantal Hallo bronnen op elk knooppunt. Sommige werkbelastingen maken van services die uitzonderlijk groot en gebruiken van de meeste of alle van een knooppunt. In deze gevallen is het mogelijk dat wanneer er grote werkbelastingen ophalen gemaakt die er niet genoeg ruimte vrij op elk knooppunt toorun ze. Grote werkbelastingen zijn niet van een probleem in Service Fabric; in deze gevallen Hallo bepaalt Cluster Resource Manager dat het moet tooreorganize Hallo cluster toomake ruimte voor deze grote werkbelasting. In Hallo tussentijd heeft werkbelasting echter toowait toobe gepland in Hallo-cluster.

Als er veel services en status toomove rond, kan klikt u vervolgens het lang duren voor Hallo grote werkbelasting toobe in Hallo cluster geplaatst. Dit is het waarschijnlijker als andere werkbelastingen in Hallo cluster ook grote zijn en dus tooreorganize langer duren. Hallo Service Fabric-team gemeten maken keer simulaties van dit scenario. We vinden dat grote services maken veel langer duurde zodra clustergebruik kreeg hierboven tussen 30 en 50%. toohandle dit scenario wordt er defragmentatie als een strategie voor taakverdeling zijn geïntroduceerd. We vinden dat voor grote werkbelastingen, met name zijn waarop Aanmaaktijd belangrijk is, defragmentatie echt geholpen bij deze nieuwe werkbelastingen ophalen gepland in Hallo-cluster.

U kunt Defragmentatie metrische gegevens toohave Hallo Cluster Resource Manager tooproactively probeer toocondense Hallo belasting van Hallo services configureren in minder knooppunten. Dit zorgt ervoor dat er is bijna altijd ruimte voor grote services zonder te ordenen Hallo cluster. Niet met tooreorganize Hallo cluster, kunt snel grote werkbelastingen maken.

De meeste mensen hoeft niet defragmentatie. Services zijn meestal worden klein, dus niet harde toofind ruimte voor hen in Hallo-cluster. Wanneer de reorganisatie mogelijk is, gaat snel, omdat de meeste services klein zijn en snel en parallel kunnen worden verplaatst. Als u grote services hebt en ze snel gemaakt moet en Hallo is defragmentatie strategie voor u. We bespreken Hallo-en nadelen van het gebruik van defragmentatie vervolgens. 

## <a name="defragmentation-tradeoffs"></a>Defragmentatie-en nadelen
Defragmentatie kunt impactfulness van fouten, verhogen omdat meer services die worden uitgevoerd op knooppunten die niet voldoen aan. Defragmentatie kan ook kosten, verhogen omdat bronnen in Hallo cluster deel van reserve uitmaken moeten, wachten op Hallo maken van een grote werkbelastingen.

Hallo biedt volgende diagram een visuele representatie van twee clusters, één dat wordt gedefragmenteerd en één die niet. 

<center>
![Vergelijken met gelijke taakverdeling en gedefragmenteerd Clusters][Image1]
</center>

Overweeg het aantal verplaatsingen van het type die nodig zijn tooplace een van de grootste serviceobjecten Hallo Hallo in geval van Hallo met gelijke taakverdeling. In Hallo gedefragmenteerde cluster kan Hallo grote werkbelasting worden geplaatst op knooppunten vier of vijf zonder toowait voor alle andere services toomove.

## <a name="defragmentation-pros-and-cons"></a>Defragmentatie voor- en nadelen
Wat zijn zodat deze conceptuele optimalisatie? Dit is een snelle tabel met dingen toothink over:

| Defragmentatie-professionals | Defragmentatie nadelen |
| --- | --- |
| Hiermee kunt sneller maken van grote services |Concentraten op minder knooppunten, verhogen conflicten laden |
| Hiermee verlagen verplaatsing van gegevens tijdens het maken van |Fouten kunnen invloed meer services en meer verloop veroorzaken |
| Hiermee maakt u uitgebreide beschrijving van de vereisten en het vrijmaken van ruimte |Complexere algehele Resource Management-configuratie |

U kunt combineren gedefragmenteerde en normale metrische gegevens in hetzelfde cluster Hallo. Hallo Cluster Resource Manager probeert tooconsolidate Hallo defragmentatie metrische gegevens zo veel mogelijk bij het uitleggen Hallo anderen. Hallo resultaten van de combinatie van defragmentatie en netwerktaakverdeling strategieën, is afhankelijk van verschillende factoren, waaronder:
  - Hallo aantal balancing metrische gegevens versus Hallo aantal defragmentatie metrische gegevens
  - Hiermee wordt aangegeven of alle services maakt gebruik van beide typen metrische gegevens 
  - Hallo metrische gewichten
  - huidige metrische gegevens worden geladen
  
Experimenteren is vereist toodetermine Hallo exacte configuratie nodig. Het is raadzaam grondige meting van de werkbelasting van uw voordat u Defragmentatie metrische gegevens in de productieomgeving inschakelen. Dit geldt met name wanneer de combinatie van defragmentatie en taakverdeling metrische gegevens binnen Hallo dezelfde service. 

## <a name="configuring-defragmentation-metrics"></a>Defragmentatie metrische gegevens configureren
Een globale beslissing in Hallo cluster configureren defragmentatie metrische gegevens is en afzonderlijke metrische gegevens voor defragmentatie kan worden geselecteerd. Hallo na config codefragmenten laten zien hoe tooconfigure metrische gegevens voor defragmentatie. In dit geval 'Metric1' geconfigureerd als een metriek defragmentatie 'Metric2' wordt verder toobe normaal gesproken met gelijke taakverdeling. 

ClusterManifest.xml:

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

gehoste clusters via ClusterConfig.json voor zelfstandige implementaties of Template.json voor Azure:

```json
"fabricSettings": [
  {
    "name": "DefragmentationMetrics",
    "parameters": [
      {
          "name": "Metric1",
          "value": "true"
      },
      {
          "name": "Metric2",
          "value": "false"
      }
    ]
  }
]
```


## <a name="next-steps"></a>Volgende stappen
- Hallo Cluster Resource Manager heeft man-opties voor het beschrijven van Hallo-cluster. toofind voor meer informatie over deze Raadpleeg dit artikel op [met een beschrijving van een Service Fabric-cluster](service-fabric-cluster-resource-manager-cluster-description.md)
- Metrische gegevens zijn hoe Hallo Service Fabric-Cluster Resource Manager beheert gebruiks- en capaciteit in Hallo-cluster. meer informatie over metrische gegevens toolearn en hoe tooconfigure, Bekijk [in dit artikel](service-fabric-cluster-resource-manager-metrics.md)

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png

---
title: aaaBalance uw Azure Service Fabric-cluster | Microsoft Docs
description: Een inleiding toobalancing uw cluster Hello Service Fabric-Cluster Resource Manager.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 030b1465-6616-4c0b-8bc7-24ed47d054c0
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5f7ad2f5cf4cfb3751a860f5293b03d2d5266d99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="balancing-your-service-fabric-cluster"></a>Taakverdeling van uw service fabric-cluster
Hallo Service Fabric-Cluster Resource Manager biedt ondersteuning voor dynamische belasting bij wijzigingen, kruisreagerende tooadditions of verwijderingen van knooppunten of services. Deze functie ook automatisch gecorrigeerd schendingen van plaatsingsbeperkingen en proactief rebalances Hallo-cluster. Maar hoe vaak deze acties worden uitgevoerd en wat ze activeert?

Er zijn drie verschillende categorieën van het werk dat Hallo Cluster Resource Manager wordt uitgevoerd. Ze zijn:

1. Plaatsing: deze fase omgaat met de plaatsing van een stateful replica's of stateless exemplaren die ontbreken. Plaatsing bevat nieuwe services en de afhandeling van stateful replica's of stateless exemplaren die zijn mislukt. Verwijderen en het verwijderen van replica's of exemplaren worden hier afgehandeld.
2. Beperking controleert: deze fase controleert en corrigeert schendingen van Hallo verschillende plaatsingsbeperkingen (regels) binnen het Hallo-systeem. Voorbeelden van regels zijn bijvoorbeeld ervoor te zorgen dat knooppunten niet overbelast zijn en dat de plaatsingsbeperkingen voor een service is voldaan.
3. Netwerktaakverdeling: deze fase controleert toosee als herverdeling nodig op basis van Hallo geconfigureerd is gewenst niveau van verdelen voor een andere metrische gegevens. Als dit het geval probeert toofind een rangschikking in Hallo cluster is verdeeld.

## <a name="configuring-cluster-resource-manager-timers"></a>Cluster Resource Manager Timers configureren
Hallo eerste set besturingselementen rond balancing zijn een set van timers. Deze timers bepalen hoe vaak hello Cluster Resource Manager Hallo cluster worden gecontroleerd en neemt corrigerende maatregelen.

Elk van deze verschillende soorten correcties Hallo Cluster Resource Manager kunt aanbrengen wordt beheerd door een andere timer die de frequentie bepaalt. Wanneer elke timer wordt gestart, Hallo taak. Standaard Hallo Resource Manager:

* de status wordt gescand en past updates (zoals opname die een knooppunt niet actief is) elke 1/10 van een seconde
* Hallo plaatsing selectievakje markering wordt ingesteld 
* stelt Hallo beperking selectievakje vlag per seconde
* Hiermee stelt u Hallo balancing vlag elke vijf seconden.

Voorbeelden van Hallo-configuratie voor deze timers zijn hieronder:

ClusterManifest.xml:

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

gehoste clusters via ClusterConfig.json voor zelfstandige implementaties of Template.json voor Azure:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PLBRefreshGap",
          "value": "0.10"
      },
      {
          "name": "MinPlacementInterval",
          "value": "1.0"
      },
      {
          "name": "MinConstraintCheckInterval",
          "value": "1.0"
      },
      {
          "name": "MinLoadBalancingInterval",
          "value": "5.0"
      }
    ]
  }
]
```

Vandaag de dag voert Hallo Cluster Resource Manager alleen een van deze acties op een tijdstip sequentieel worden verwerkt. Dit is de reden waarom we toothese timers als "minimale intervallen verwijzen" en acties die ophalen uitgevoerd wanneer Hallo timers uitschakelen als 'instelling vlaggen gaat' Hallo. Hallo Cluster Resource Manager voor in behandeling zijnde zorgt aanvragen bijvoorbeeld toocreate services voordat balancing-cluster Hallo. Zoals u door Hallo standaard-tijdsintervallen is opgegeven zien kunt, zoekt Hallo Cluster Resource Manager naar iets deze behoeften toodo vaak. Dit betekent gewoonlijk Hallo set wijzigingen die zijn aangebracht tijdens elke stap is klein. Kleine wijzigingen vaak waardoor staat Hallo Cluster Resource Manager toobe responsief wanneer dingen in Hallo-cluster gebeuren. Hallo standaard timers bieden sommige batchverwerking sinds veel Hallo dezelfde typen gebeurtenissen meestal toooccur tegelijk. 

Bijvoorbeeld, wanneer knooppunten uitvallen ze dus hele domeinen met fouten per keer kunnen doen. Alle deze fouten worden vastgelegd tijdens de volgende status Hallo bijgewerkt na Hallo *PLBRefreshGap*. Hallo correcties worden vastgelegd tijdens Hallo plaatsing check-beperking, volgen en Netwerktaakverdeling wordt uitgevoerd. Cluster Resource Manager is niet door standaard Hallo scannen via uren van wijzigingen in het Hallo-cluster en probeert tooaddress alle wijzigingen in één keer. In dat geval leiden toobursts van verloop.

Hallo Cluster Resource Manager moet ook een aantal aanvullende informatie toodetermine als Hallo cluster imbalanced. Voor die we hebben twee andere delen van configuratie: *BalancingThresholds* en *ActivityThresholds*.

## <a name="balancing-thresholds"></a>Drempelwaarden voor netwerktaakverdeling
Een drempelwaarde Balancing is de belangrijkste besturingselement Hallo voor activering van herverdeling. Hallo Balancing drempelwaarde voor een metriek is een _verhouding_. Als Hallo load voor een metriek op Hallo meest knooppunt gedeeld door Hallo hoeveelheid load op Hallo minste geladen geladen knooppunt is groter dan deze metriek *BalancingThreshold*, dan is imbalanced Hallo-cluster. Als gevolg hiervan balancing is triggered Hallo volgende tijd Hallo Cluster Resource Manager controleert. Hallo *MinLoadBalancingInterval* timer definieert hoe vaak hello Cluster Resource Manager moet controleren als herverdeling nodig is. Controleren betekent niet dat iets gebeurt. 

Drempelwaarden voor taakverdeling worden gedefinieerd op basis van per metriek als onderdeel van de definitie van Hallo-cluster. Bekijk voor meer informatie over metrische gegevens [in dit artikel](service-fabric-cluster-resource-manager-metrics.md).

ClusterManifest.xml

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

gehoste clusters via ClusterConfig.json voor zelfstandige implementaties of Template.json voor Azure:

```json
"fabricSettings": [
  {
    "name": "MetricBalancingThresholds",
    "parameters": [
      {
          "name": "MetricName1",
          "value": "2"
      },
      {
          "name": "MetricName2",
          "value": "3.5"
      }
    ]
  }
]
```

<center>
![Voorbeeld van taakverdeling drempelwaarde][Image1]
</center>

In dit voorbeeld wordt elke service één eenheid van sommige metriek verbruikt. In de bovenste voorbeeld Hallo Hallo maximale belasting van een knooppunt is vijf en Hallo minimum is twee. Stel dat Hallo balancing drempelwaarde voor deze metrische gegevens is drie. Aangezien Hallo verhouding in Hallo cluster 5/2 = 2,5 en dat is kleiner dan Hallo opgegeven drempelwaarde van drie, Hallo-cluster is taakverdeling. Er is geen balancing wordt geactiveerd wanneer Hallo Cluster Resource Manager controleert.

Hallo maximale belasting van een knooppunt is in Hallo onder bijvoorbeeld 10, terwijl Hallo minimaal twee, wat resulteert in een ratio van vijf. Vijf is groter dan Hallo aangewezen taakverdeling drempelwaarde van drie voor deze metrische gegevens. Als gevolg hiervan worden rebalancing run geplande volgende tijd Hallo balancing timer deze gebeurtenis wordt gestart. Sommige werklast is in een dergelijke situatie meestal gedistribueerde tooNode3. Omdat Hallo Service Fabric-Cluster Resource Manager biedt geen een greedy benadering gebruiken, kan een aantal load ook gedistribueerde tooNode2 worden. 

<center>
![Taakverdeling drempelwaarde voorbeeld acties][Image2]
</center>

> [!NOTE]
> Twee verschillende strategieën voor het beheren van laden in het cluster 'Balancing' worden verwerkt. Hallo standaard strategie die Hallo Cluster Resource Manager gebruikt is toodistribute load over Hallo knooppunten in het Hallo-cluster. Hallo andere strategie is [defragmentatie](service-fabric-cluster-resource-manager-defragmentation-metrics.md). Defragmentatie wordt uitgevoerd tijdens de Hallo dezelfde Netwerktaakverdeling uitvoeren. Hallo taakverdeling en defragmentatie strategieën kunnen worden gebruikt voor andere metrische gegevens binnen Hallo hetzelfde cluster. Een service kunt taakverdeling en defragmentatie metrische gegevens hebben. Voor defragmentatie metrische gegevens en Hallo ratio van Hallo in Hallo cluster triggers herverdeling wanneer deze wordt geladen _hieronder_ Hallo balancing drempelwaarde. 
>

Onder drempelwaarde balancing Hallo ophalen is niet een expliciete doel. Taakverdeling drempelwaarden zijn slechts een *trigger*. De taakverdeling wordt uitgevoerd, bepaalt Hallo Cluster Resource Manager welke verbeteringen in deze maken kan, indien van toepassing. Omdat een taakverdeling zoekopdracht is gestarte betekent niet dat alles wordt verplaatst. Soms Hallo-cluster is imbalanced maar te beperkte toocorrect. U kunt ook Hallo verbeteringen verplaatsingen die te zijn vereisen [kostbare](service-fabric-cluster-resource-manager-movement-cost.md)).

## <a name="activity-thresholds"></a>Drempelwaarden voor de activiteit
Soms knooppunten wel relatief imbalanced, Hallo *totale* hoeveelheid laden in het Hallo-cluster is laag. Hallo gebrek aan load kan een tijdelijke dip, of omdat Hallo cluster nieuwe en net ophalen bootstrap uitvoert. In beide gevallen kunt u geen toospend tijd balancing-cluster Hallo omdat er weinig toobe heeft gekregen. Als Hallo cluster twee balancing, zou u besteden netwerk en resources toomove dingen rond berekenen zonder dat een grote *absolute* verschil. onnodige tooavoid wordt verplaatst, wordt er een ander besturingselement wel drempelwaarden voor de activiteit is. Drempelwaarden voor de activiteit kunt u toospecify sommige absolute ondergrens voor de activiteit. Als er geen knooppunt boven deze drempelwaarde, is niet balancing geactiveerd, zelfs als hello Balancing drempelwaarde wordt voldaan.

Stel dat we onze drempelwaarde Balancing van drie voor deze metrische gegevens behouden. Stel ook dat we hebben een drempel voor de activiteit van 1536. In het eerste geval hello, terwijl Hallo cluster imbalanced per Hallo drempelwaarde Balancing er is geen knooppunt voldoet aan deze drempelwaarde voor de activiteit, dus niets gebeurt. In voorbeeld Hallo onder is knooppunt1 via Hallo activiteit drempelwaarde. Aangezien beide Balancing drempelwaarde Hallo en Hallo activiteit drempelwaarde voor Hallo metriek is overschreden, is balancing gepland. Een voorbeeld: Bekijk Hallo-diagram te volgen: 

<center>
![Voorbeeld van de activiteit drempelwaarde][Image3]
</center>

Net als de drempelwaarden voor netwerktaakverdeling zijn activiteit drempelwaarden gedefinieerde per-meetwaarde via Hallo cluster definitie:

ClusterManifest.xml

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

gehoste clusters via ClusterConfig.json voor zelfstandige implementaties of Template.json voor Azure:

```json
"fabricSettings": [
  {
    "name": "MetricActivityThresholds",
    "parameters": [
      {
          "name": "Memory",
          "value": "1536"
      }
    ]
  }
]
```

Taakverdeling en activiteit drempelwaarden zijn beide gebonden tooa specifieke metrische gegevens - taakverdeling wordt geactiveerd als beide Balancing drempelwaarde Hallo en activiteit drempelwaarde is overschreden voor Hallo dezelfde metrische gegevens.

## <a name="balancing-services-together"></a>Services Netwerktaakverdeling samen
Of Hallo cluster imbalanced of niet is een hele cluster beslissing is. Hallo manier we gaat over het oplossen van het is echter afzonderlijke service replica's en -exemplaren rond verplaatsen. Dit klinkt logisch, toch? Als het geheugen is up gestapelde op één knooppunt, meerdere replica's of exemplaren kunnen een bijdrage leveren tooit. Corrigeren Hallo onbalans nodig Hallo stateful replica's of stateless exemplaren die gebruikmaken van Hallo imbalanced metrische gegevens te verplaatsen.

Tijd tot tijd al een service die is niet van zichzelf imbalanced opgehaald verplaatst (onthouden Hallo bespreking van de lokale en globale gewicht eerder). Waarom zou een service verplaatst wanneer alle metrische gegevens van de service zijn verdeeld? We bekijken een voorbeeld:

- Stel dat er zijn vier services, Service1, Service2 Service3 en Service4. 
- Service1 rapporten metrische gegevens Metric1 en Metric2. 
- Service2 rapporten metrische gegevens Metric2 en Metric3. 
- Service3 rapporteert metrische gegevens Metric3 en Metric4.
- Service4 metrische Metric99 rapporteert. 

U kunt nietwaar zien waar gaan we hier: Er is een keten! Er zijn momenteel geen echt vier onafhankelijke services, hebben we drie services die zijn gerelateerd en één die is uitgeschakeld op zichzelf.

<center>
![Services Netwerktaakverdeling samen][Image4]
</center>

Vanwege deze keten is het mogelijk een onbalans in metrics 1-4 dat replica's of exemplaren die horen tooservices 1-3 toomove rond. We ook weten dat een onbalans in Metrics 1, 2 of 3 verplaatsingen van het type kan niet in Service4 veroorzaken. Er zou er is geen sinds het Hallo-replica's te verplaatsen of exemplaren die horen tooService4 rond kan absoluut niets doen tooimpact Hallo saldo maatstaven voor 1-3.

Hallo Cluster Resource Manager automatisch weten welke services zijn gerelateerd te achterhalen. Toevoegen, verwijderen of wijzigen Hallo metrische gegevens voor services kunnen invloed hebben op hun relaties. Bijvoorbeeld, tussen twee uitvoert balancing Service2 mogelijk is de bijgewerkte tooremove Metric2. Dit Hallo keten tussen Service1 en Service2 wordt verbroken. In plaats van twee groepen van gerelateerde services zijn er nu drie:

<center>
![Services Netwerktaakverdeling samen][Image5]
</center>

## <a name="next-steps"></a>Volgende stappen
* Metrische gegevens zijn hoe Hallo Service Fabric-Cluster Resource Manager beheert gebruiks- en capaciteit in Hallo-cluster. meer informatie over metrische gegevens toolearn en hoe tooconfigure, Bekijk [in dit artikel](service-fabric-cluster-resource-manager-metrics.md)
* Verplaatsingkosten is één manier toohello Cluster Resource Manager-signalering dat bepaalde services zijn duurder toomove dan andere. Voor meer informatie over verplaatsingskosten, Raadpleeg te[in dit artikel](service-fabric-cluster-resource-manager-movement-cost.md)
* Hallo Cluster Resource Manager bevat verschillende vertragingen die u kunt tooslow omlaag verloop in Hallo cluster configureren. Ze dat niet normaal gesproken nodig zijn, maar als u deze nodig hebt vindt u meer informatie hierover [hier](service-fabric-cluster-resource-manager-advanced-throttling.md)

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png

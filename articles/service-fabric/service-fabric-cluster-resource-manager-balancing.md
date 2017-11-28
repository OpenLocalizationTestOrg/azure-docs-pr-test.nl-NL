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
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="f3b5d-103">Taakverdeling van uw service fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="f3b5d-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="f3b5d-104">Hallo Service Fabric-Cluster Resource Manager biedt ondersteuning voor dynamische belasting bij wijzigingen, kruisreagerende tooadditions of verwijderingen van knooppunten of services.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-104">hello Service Fabric Cluster Resource Manager supports dynamic load changes, reacting tooadditions or removals of nodes or services.</span></span> <span data-ttu-id="f3b5d-105">Deze functie ook automatisch gecorrigeerd schendingen van plaatsingsbeperkingen en proactief rebalances Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-105">It also automatically corrects constraint violations, and proactively rebalances hello cluster.</span></span> <span data-ttu-id="f3b5d-106">Maar hoe vaak deze acties worden uitgevoerd en wat ze activeert?</span><span class="sxs-lookup"><span data-stu-id="f3b5d-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="f3b5d-107">Er zijn drie verschillende categorieën van het werk dat Hallo Cluster Resource Manager wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-107">There are three different categories of work that hello Cluster Resource Manager performs.</span></span> <span data-ttu-id="f3b5d-108">Ze zijn:</span><span class="sxs-lookup"><span data-stu-id="f3b5d-108">They are:</span></span>

1. <span data-ttu-id="f3b5d-109">Plaatsing: deze fase omgaat met de plaatsing van een stateful replica's of stateless exemplaren die ontbreken.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="f3b5d-110">Plaatsing bevat nieuwe services en de afhandeling van stateful replica's of stateless exemplaren die zijn mislukt.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="f3b5d-111">Verwijderen en het verwijderen van replica's of exemplaren worden hier afgehandeld.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="f3b5d-112">Beperking controleert: deze fase controleert en corrigeert schendingen van Hallo verschillende plaatsingsbeperkingen (regels) binnen het Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-112">Constraint Checks – this stage checks for and corrects violations of hello different placement constraints (rules) within hello system.</span></span> <span data-ttu-id="f3b5d-113">Voorbeelden van regels zijn bijvoorbeeld ervoor te zorgen dat knooppunten niet overbelast zijn en dat de plaatsingsbeperkingen voor een service is voldaan.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="f3b5d-114">Netwerktaakverdeling: deze fase controleert toosee als herverdeling nodig op basis van Hallo geconfigureerd is gewenst niveau van verdelen voor een andere metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-114">Balancing – this stage checks toosee if rebalancing is necessary based on hello configured desired level of balance for different metrics.</span></span> <span data-ttu-id="f3b5d-115">Als dit het geval probeert toofind een rangschikking in Hallo cluster is verdeeld.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-115">If so it attempts toofind an arrangement in hello cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="f3b5d-116">Cluster Resource Manager Timers configureren</span><span class="sxs-lookup"><span data-stu-id="f3b5d-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="f3b5d-117">Hallo eerste set besturingselementen rond balancing zijn een set van timers.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-117">hello first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="f3b5d-118">Deze timers bepalen hoe vaak hello Cluster Resource Manager Hallo cluster worden gecontroleerd en neemt corrigerende maatregelen.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-118">These timers govern how often hello Cluster Resource Manager examines hello cluster and takes corrective actions.</span></span>

<span data-ttu-id="f3b5d-119">Elk van deze verschillende soorten correcties Hallo Cluster Resource Manager kunt aanbrengen wordt beheerd door een andere timer die de frequentie bepaalt.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-119">Each of these different types of corrections hello Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="f3b5d-120">Wanneer elke timer wordt gestart, Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-120">When each timer fires, hello task is scheduled.</span></span> <span data-ttu-id="f3b5d-121">Standaard Hallo Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="f3b5d-121">By default hello Resource Manager:</span></span>

* <span data-ttu-id="f3b5d-122">de status wordt gescand en past updates (zoals opname die een knooppunt niet actief is) elke 1/10 van een seconde</span><span class="sxs-lookup"><span data-stu-id="f3b5d-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="f3b5d-123">Hallo plaatsing selectievakje markering wordt ingesteld</span><span class="sxs-lookup"><span data-stu-id="f3b5d-123">sets hello placement check flag</span></span> 
* <span data-ttu-id="f3b5d-124">stelt Hallo beperking selectievakje vlag per seconde</span><span class="sxs-lookup"><span data-stu-id="f3b5d-124">sets hello constraint check flag every second</span></span>
* <span data-ttu-id="f3b5d-125">Hiermee stelt u Hallo balancing vlag elke vijf seconden.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-125">sets hello balancing flag every five seconds.</span></span>

<span data-ttu-id="f3b5d-126">Voorbeelden van Hallo-configuratie voor deze timers zijn hieronder:</span><span class="sxs-lookup"><span data-stu-id="f3b5d-126">Examples of hello configuration governing these timers are below:</span></span>

<span data-ttu-id="f3b5d-127">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="f3b5d-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="f3b5d-128">gehoste clusters via ClusterConfig.json voor zelfstandige implementaties of Template.json voor Azure:</span><span class="sxs-lookup"><span data-stu-id="f3b5d-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="f3b5d-129">Vandaag de dag voert Hallo Cluster Resource Manager alleen een van deze acties op een tijdstip sequentieel worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-129">Today hello Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="f3b5d-130">Dit is de reden waarom we toothese timers als "minimale intervallen verwijzen" en acties die ophalen uitgevoerd wanneer Hallo timers uitschakelen als 'instelling vlaggen gaat' Hallo.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-130">This is why we refer toothese timers as “minimum intervals” and hello actions that get taken when hello timers go off as "setting flags".</span></span> <span data-ttu-id="f3b5d-131">Hallo Cluster Resource Manager voor in behandeling zijnde zorgt aanvragen bijvoorbeeld toocreate services voordat balancing-cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-131">For example, hello Cluster Resource Manager takes care of pending requests toocreate services before balancing hello cluster.</span></span> <span data-ttu-id="f3b5d-132">Zoals u door Hallo standaard-tijdsintervallen is opgegeven zien kunt, zoekt Hallo Cluster Resource Manager naar iets deze behoeften toodo vaak.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-132">As you can see by hello default time intervals specified, hello Cluster Resource Manager scans for anything it needs toodo frequently.</span></span> <span data-ttu-id="f3b5d-133">Dit betekent gewoonlijk Hallo set wijzigingen die zijn aangebracht tijdens elke stap is klein.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-133">Normally this means that hello set of changes made during each step is small.</span></span> <span data-ttu-id="f3b5d-134">Kleine wijzigingen vaak waardoor staat Hallo Cluster Resource Manager toobe responsief wanneer dingen in Hallo-cluster gebeuren.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-134">Making small changes frequently allows hello Cluster Resource Manager toobe responsive when things happen in hello cluster.</span></span> <span data-ttu-id="f3b5d-135">Hallo standaard timers bieden sommige batchverwerking sinds veel Hallo dezelfde typen gebeurtenissen meestal toooccur tegelijk.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-135">hello default timers provide some batching since many of hello same types of events tend toooccur simultaneously.</span></span> 

<span data-ttu-id="f3b5d-136">Bijvoorbeeld, wanneer knooppunten uitvallen ze dus hele domeinen met fouten per keer kunnen doen.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="f3b5d-137">Alle deze fouten worden vastgelegd tijdens de volgende status Hallo bijgewerkt na Hallo *PLBRefreshGap*.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-137">All these failures are captured during hello next state update after hello *PLBRefreshGap*.</span></span> <span data-ttu-id="f3b5d-138">Hallo correcties worden vastgelegd tijdens Hallo plaatsing check-beperking, volgen en Netwerktaakverdeling wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-138">hello corrections are determined during hello following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="f3b5d-139">Cluster Resource Manager is niet door standaard Hallo scannen via uren van wijzigingen in het Hallo-cluster en probeert tooaddress alle wijzigingen in één keer.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-139">By default hello Cluster Resource Manager is not scanning through hours of changes in hello cluster and trying tooaddress all changes at once.</span></span> <span data-ttu-id="f3b5d-140">In dat geval leiden toobursts van verloop.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-140">Doing so would lead toobursts of churn.</span></span>

<span data-ttu-id="f3b5d-141">Hallo Cluster Resource Manager moet ook een aantal aanvullende informatie toodetermine als Hallo cluster imbalanced.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-141">hello Cluster Resource Manager also needs some additional information toodetermine if hello cluster imbalanced.</span></span> <span data-ttu-id="f3b5d-142">Voor die we hebben twee andere delen van configuratie: *BalancingThresholds* en *ActivityThresholds*.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="f3b5d-143">Drempelwaarden voor netwerktaakverdeling</span><span class="sxs-lookup"><span data-stu-id="f3b5d-143">Balancing thresholds</span></span>
<span data-ttu-id="f3b5d-144">Een drempelwaarde Balancing is de belangrijkste besturingselement Hallo voor activering van herverdeling.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-144">A Balancing Threshold is hello main control for triggering rebalancing.</span></span> <span data-ttu-id="f3b5d-145">Hallo Balancing drempelwaarde voor een metriek is een _verhouding_.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-145">hello Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="f3b5d-146">Als Hallo load voor een metriek op Hallo meest knooppunt gedeeld door Hallo hoeveelheid load op Hallo minste geladen geladen knooppunt is groter dan deze metriek *BalancingThreshold*, dan is imbalanced Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-146">If hello load for a metric on hello most loaded node divided by hello amount of load on hello least loaded node exceeds that metric's *BalancingThreshold*, then hello cluster is imbalanced.</span></span> <span data-ttu-id="f3b5d-147">Als gevolg hiervan balancing is triggered Hallo volgende tijd Hallo Cluster Resource Manager controleert.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-147">As a result balancing is triggered hello next time hello Cluster Resource Manager checks.</span></span> <span data-ttu-id="f3b5d-148">Hallo *MinLoadBalancingInterval* timer definieert hoe vaak hello Cluster Resource Manager moet controleren als herverdeling nodig is.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-148">hello *MinLoadBalancingInterval* timer defines how often hello Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="f3b5d-149">Controleren betekent niet dat iets gebeurt.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="f3b5d-150">Drempelwaarden voor taakverdeling worden gedefinieerd op basis van per metriek als onderdeel van de definitie van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-150">Balancing Thresholds are defined on a per-metric basis as a part of hello cluster definition.</span></span> <span data-ttu-id="f3b5d-151">Bekijk voor meer informatie over metrische gegevens [in dit artikel](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="f3b5d-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="f3b5d-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="f3b5d-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="f3b5d-153">gehoste clusters via ClusterConfig.json voor zelfstandige implementaties of Template.json voor Azure:</span><span class="sxs-lookup"><span data-stu-id="f3b5d-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="f3b5d-154"><center>
![Voorbeeld van taakverdeling drempelwaarde][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="f3b5d-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="f3b5d-155">In dit voorbeeld wordt elke service één eenheid van sommige metriek verbruikt.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="f3b5d-156">In de bovenste voorbeeld Hallo Hallo maximale belasting van een knooppunt is vijf en Hallo minimum is twee.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-156">In hello top example, hello maximum load on a node is five and hello minimum is two.</span></span> <span data-ttu-id="f3b5d-157">Stel dat Hallo balancing drempelwaarde voor deze metrische gegevens is drie.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-157">Let’s say that hello balancing threshold for this metric is three.</span></span> <span data-ttu-id="f3b5d-158">Aangezien Hallo verhouding in Hallo cluster 5/2 = 2,5 en dat is kleiner dan Hallo opgegeven drempelwaarde van drie, Hallo-cluster is taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-158">Since hello ratio in hello cluster is 5/2 = 2.5 and that is less than hello specified balancing threshold of three, hello cluster is balanced.</span></span> <span data-ttu-id="f3b5d-159">Er is geen balancing wordt geactiveerd wanneer Hallo Cluster Resource Manager controleert.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-159">No balancing is triggered when hello Cluster Resource Manager checks.</span></span>

<span data-ttu-id="f3b5d-160">Hallo maximale belasting van een knooppunt is in Hallo onder bijvoorbeeld 10, terwijl Hallo minimaal twee, wat resulteert in een ratio van vijf.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-160">In hello bottom example, hello maximum load on a node is 10, while hello minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="f3b5d-161">Vijf is groter dan Hallo aangewezen taakverdeling drempelwaarde van drie voor deze metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-161">Five is greater than hello designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="f3b5d-162">Als gevolg hiervan worden rebalancing run geplande volgende tijd Hallo balancing timer deze gebeurtenis wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-162">As a result, a rebalancing run will be scheduled next time hello balancing timer fires.</span></span> <span data-ttu-id="f3b5d-163">Sommige werklast is in een dergelijke situatie meestal gedistribueerde tooNode3.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-163">In a situation like this some load is usually distributed tooNode3.</span></span> <span data-ttu-id="f3b5d-164">Omdat Hallo Service Fabric-Cluster Resource Manager biedt geen een greedy benadering gebruiken, kan een aantal load ook gedistribueerde tooNode2 worden.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-164">Because hello Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed tooNode2.</span></span> 

<span data-ttu-id="f3b5d-165"><center>
![Taakverdeling drempelwaarde voorbeeld acties][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="f3b5d-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="f3b5d-166">Twee verschillende strategieën voor het beheren van laden in het cluster 'Balancing' worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="f3b5d-167">Hallo standaard strategie die Hallo Cluster Resource Manager gebruikt is toodistribute load over Hallo knooppunten in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-167">hello default strategy that hello Cluster Resource Manager uses is toodistribute load across hello nodes in hello cluster.</span></span> <span data-ttu-id="f3b5d-168">Hallo andere strategie is [defragmentatie](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="f3b5d-168">hello other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="f3b5d-169">Defragmentatie wordt uitgevoerd tijdens de Hallo dezelfde Netwerktaakverdeling uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-169">Defragmentation is performed during hello same balancing run.</span></span> <span data-ttu-id="f3b5d-170">Hallo taakverdeling en defragmentatie strategieën kunnen worden gebruikt voor andere metrische gegevens binnen Hallo hetzelfde cluster.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-170">hello balancing and defragmentation strategies can be used for different metrics within hello same cluster.</span></span> <span data-ttu-id="f3b5d-171">Een service kunt taakverdeling en defragmentatie metrische gegevens hebben.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="f3b5d-172">Voor defragmentatie metrische gegevens en Hallo ratio van Hallo in Hallo cluster triggers herverdeling wanneer deze wordt geladen _hieronder_ Hallo balancing drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-172">For defragmentation metrics, hello ratio of hello loads in hello cluster triggers rebalancing when it is _below_ hello balancing threshold.</span></span> 
>

<span data-ttu-id="f3b5d-173">Onder drempelwaarde balancing Hallo ophalen is niet een expliciete doel.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-173">Getting below hello balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="f3b5d-174">Taakverdeling drempelwaarden zijn slechts een *trigger*.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="f3b5d-175">De taakverdeling wordt uitgevoerd, bepaalt Hallo Cluster Resource Manager welke verbeteringen in deze maken kan, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-175">When balancing runs, hello Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="f3b5d-176">Omdat een taakverdeling zoekopdracht is gestarte betekent niet dat alles wordt verplaatst.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="f3b5d-177">Soms Hallo-cluster is imbalanced maar te beperkte toocorrect.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-177">Sometimes hello cluster is imbalanced but too constrained toocorrect.</span></span> <span data-ttu-id="f3b5d-178">U kunt ook Hallo verbeteringen verplaatsingen die te zijn vereisen [kostbare](service-fabric-cluster-resource-manager-movement-cost.md)).</span><span class="sxs-lookup"><span data-stu-id="f3b5d-178">Alternatively, hello improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="f3b5d-179">Drempelwaarden voor de activiteit</span><span class="sxs-lookup"><span data-stu-id="f3b5d-179">Activity thresholds</span></span>
<span data-ttu-id="f3b5d-180">Soms knooppunten wel relatief imbalanced, Hallo *totale* hoeveelheid laden in het Hallo-cluster is laag.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-180">Sometimes, although nodes are relatively imbalanced, hello *total* amount of load in hello cluster is low.</span></span> <span data-ttu-id="f3b5d-181">Hallo gebrek aan load kan een tijdelijke dip, of omdat Hallo cluster nieuwe en net ophalen bootstrap uitvoert.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-181">hello lack of load could be a transient dip, or because hello cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="f3b5d-182">In beide gevallen kunt u geen toospend tijd balancing-cluster Hallo omdat er weinig toobe heeft gekregen.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-182">In either case, you may not want toospend time balancing hello cluster because there’s little toobe gained.</span></span> <span data-ttu-id="f3b5d-183">Als Hallo cluster twee balancing, zou u besteden netwerk en resources toomove dingen rond berekenen zonder dat een grote *absolute* verschil.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-183">If hello cluster underwent balancing, you’d spend network and compute resources toomove things around without making any large *absolute* difference.</span></span> <span data-ttu-id="f3b5d-184">onnodige tooavoid wordt verplaatst, wordt er een ander besturingselement wel drempelwaarden voor de activiteit is.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-184">tooavoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="f3b5d-185">Drempelwaarden voor de activiteit kunt u toospecify sommige absolute ondergrens voor de activiteit.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-185">Activity Thresholds allows you toospecify some absolute lower bound for activity.</span></span> <span data-ttu-id="f3b5d-186">Als er geen knooppunt boven deze drempelwaarde, is niet balancing geactiveerd, zelfs als hello Balancing drempelwaarde wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-186">If no node is over this threshold, balancing isn't triggered even if hello Balancing Threshold is met.</span></span>

<span data-ttu-id="f3b5d-187">Stel dat we onze drempelwaarde Balancing van drie voor deze metrische gegevens behouden.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="f3b5d-188">Stel ook dat we hebben een drempel voor de activiteit van 1536.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="f3b5d-189">In het eerste geval hello, terwijl Hallo cluster imbalanced per Hallo drempelwaarde Balancing er is geen knooppunt voldoet aan deze drempelwaarde voor de activiteit, dus niets gebeurt.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-189">In hello first case, while hello cluster is imbalanced per hello Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="f3b5d-190">In voorbeeld Hallo onder is knooppunt1 via Hallo activiteit drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-190">In hello bottom example, Node1 is over hello Activity Threshold.</span></span> <span data-ttu-id="f3b5d-191">Aangezien beide Balancing drempelwaarde Hallo en Hallo activiteit drempelwaarde voor Hallo metriek is overschreden, is balancing gepland.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-191">Since both hello Balancing Threshold and hello Activity Threshold for hello metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="f3b5d-192">Een voorbeeld: Bekijk Hallo-diagram te volgen:</span><span class="sxs-lookup"><span data-stu-id="f3b5d-192">As an example, let's look at hello following diagram:</span></span> 

<span data-ttu-id="f3b5d-193"><center>
![Voorbeeld van de activiteit drempelwaarde][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="f3b5d-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="f3b5d-194">Net als de drempelwaarden voor netwerktaakverdeling zijn activiteit drempelwaarden gedefinieerde per-meetwaarde via Hallo cluster definitie:</span><span class="sxs-lookup"><span data-stu-id="f3b5d-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via hello cluster definition:</span></span>

<span data-ttu-id="f3b5d-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="f3b5d-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="f3b5d-196">gehoste clusters via ClusterConfig.json voor zelfstandige implementaties of Template.json voor Azure:</span><span class="sxs-lookup"><span data-stu-id="f3b5d-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="f3b5d-197">Taakverdeling en activiteit drempelwaarden zijn beide gebonden tooa specifieke metrische gegevens - taakverdeling wordt geactiveerd als beide Balancing drempelwaarde Hallo en activiteit drempelwaarde is overschreden voor Hallo dezelfde metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-197">Balancing and activity thresholds are both tied tooa specific metric - balancing is triggered only if both hello Balancing Threshold and Activity Threshold is exceeded for hello same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="f3b5d-198">Services Netwerktaakverdeling samen</span><span class="sxs-lookup"><span data-stu-id="f3b5d-198">Balancing services together</span></span>
<span data-ttu-id="f3b5d-199">Of Hallo cluster imbalanced of niet is een hele cluster beslissing is.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-199">Whether hello cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="f3b5d-200">Hallo manier we gaat over het oplossen van het is echter afzonderlijke service replica's en -exemplaren rond verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-200">However, hello way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="f3b5d-201">Dit klinkt logisch, toch?</span><span class="sxs-lookup"><span data-stu-id="f3b5d-201">This makes sense, right?</span></span> <span data-ttu-id="f3b5d-202">Als het geheugen is up gestapelde op één knooppunt, meerdere replica's of exemplaren kunnen een bijdrage leveren tooit.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-202">If memory is stacked up on one node, multiple replicas or instances could be contributing tooit.</span></span> <span data-ttu-id="f3b5d-203">Corrigeren Hallo onbalans nodig Hallo stateful replica's of stateless exemplaren die gebruikmaken van Hallo imbalanced metrische gegevens te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-203">Fixing hello imbalance could require moving any of hello stateful replicas or stateless instances that use hello imbalanced metric.</span></span>

<span data-ttu-id="f3b5d-204">Tijd tot tijd al een service die is niet van zichzelf imbalanced opgehaald verplaatst (onthouden Hallo bespreking van de lokale en globale gewicht eerder).</span><span class="sxs-lookup"><span data-stu-id="f3b5d-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember hello discussion of local and global weights earlier).</span></span> <span data-ttu-id="f3b5d-205">Waarom zou een service verplaatst wanneer alle metrische gegevens van de service zijn verdeeld?</span><span class="sxs-lookup"><span data-stu-id="f3b5d-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="f3b5d-206">We bekijken een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f3b5d-206">Let’s see an example:</span></span>

- <span data-ttu-id="f3b5d-207">Stel dat er zijn vier services, Service1, Service2 Service3 en Service4.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="f3b5d-208">Service1 rapporten metrische gegevens Metric1 en Metric2.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="f3b5d-209">Service2 rapporten metrische gegevens Metric2 en Metric3.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="f3b5d-210">Service3 rapporteert metrische gegevens Metric3 en Metric4.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="f3b5d-211">Service4 metrische Metric99 rapporteert.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="f3b5d-212">U kunt nietwaar zien waar gaan we hier: Er is een keten!</span><span class="sxs-lookup"><span data-stu-id="f3b5d-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="f3b5d-213">Er zijn momenteel geen echt vier onafhankelijke services, hebben we drie services die zijn gerelateerd en één die is uitgeschakeld op zichzelf.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="f3b5d-214"><center>
![Services Netwerktaakverdeling samen][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="f3b5d-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="f3b5d-215">Vanwege deze keten is het mogelijk een onbalans in metrics 1-4 dat replica's of exemplaren die horen tooservices 1-3 toomove rond.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging tooservices 1-3 toomove around.</span></span> <span data-ttu-id="f3b5d-216">We ook weten dat een onbalans in Metrics 1, 2 of 3 verplaatsingen van het type kan niet in Service4 veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="f3b5d-217">Er zou er is geen sinds het Hallo-replica's te verplaatsen of exemplaren die horen tooService4 rond kan absoluut niets doen tooimpact Hallo saldo maatstaven voor 1-3.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-217">There would be no point since moving hello replicas or instances belonging tooService4 around can do absolutely nothing tooimpact hello balance of Metrics 1-3.</span></span>

<span data-ttu-id="f3b5d-218">Hallo Cluster Resource Manager automatisch weten welke services zijn gerelateerd te achterhalen.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-218">hello Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="f3b5d-219">Toevoegen, verwijderen of wijzigen Hallo metrische gegevens voor services kunnen invloed hebben op hun relaties.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-219">Adding, removing, or changing hello metrics for services can impact their relationships.</span></span> <span data-ttu-id="f3b5d-220">Bijvoorbeeld, tussen twee uitvoert balancing Service2 mogelijk is de bijgewerkte tooremove Metric2.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-220">For example, between two runs of balancing Service2 may have been updated tooremove Metric2.</span></span> <span data-ttu-id="f3b5d-221">Dit Hallo keten tussen Service1 en Service2 wordt verbroken.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-221">This breaks hello chain between Service1 and Service2.</span></span> <span data-ttu-id="f3b5d-222">In plaats van twee groepen van gerelateerde services zijn er nu drie:</span><span class="sxs-lookup"><span data-stu-id="f3b5d-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="f3b5d-223"><center>
![Services Netwerktaakverdeling samen][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="f3b5d-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="f3b5d-224">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f3b5d-224">Next steps</span></span>
* <span data-ttu-id="f3b5d-225">Metrische gegevens zijn hoe Hallo Service Fabric-Cluster Resource Manager beheert gebruiks- en capaciteit in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-225">Metrics are how hello Service Fabric Cluster Resource Manger manages consumption and capacity in hello cluster.</span></span> <span data-ttu-id="f3b5d-226">meer informatie over metrische gegevens toolearn en hoe tooconfigure, Bekijk [in dit artikel](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="f3b5d-226">toolearn more about metrics and how tooconfigure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="f3b5d-227">Verplaatsingkosten is één manier toohello Cluster Resource Manager-signalering dat bepaalde services zijn duurder toomove dan andere.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-227">Movement Cost is one way of signaling toohello Cluster Resource Manager that certain services are more expensive toomove than others.</span></span> <span data-ttu-id="f3b5d-228">Voor meer informatie over verplaatsingskosten, Raadpleeg te[in dit artikel](service-fabric-cluster-resource-manager-movement-cost.md)</span><span class="sxs-lookup"><span data-stu-id="f3b5d-228">For more about movement cost, refer too[this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="f3b5d-229">Hallo Cluster Resource Manager bevat verschillende vertragingen die u kunt tooslow omlaag verloop in Hallo cluster configureren.</span><span class="sxs-lookup"><span data-stu-id="f3b5d-229">hello Cluster Resource Manager has several throttles that you can configure tooslow down churn in hello cluster.</span></span> <span data-ttu-id="f3b5d-230">Ze dat niet normaal gesproken nodig zijn, maar als u deze nodig hebt vindt u meer informatie hierover [hier](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="f3b5d-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png

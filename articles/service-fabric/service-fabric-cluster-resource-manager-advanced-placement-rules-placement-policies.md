---
title: aaaService Fabric Cluster Resource Manager - Plaatsingsbeleid | Microsoft Docs
description: Overzicht van de van extra plaatsingsbeleid en de regels voor Service Fabric-Services
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 5c2d19c6-dd40-4c4b-abd3-5c5ec0abed38
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: bb58642520085ab3000f3929cf9aea7a8f6e3070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="placement-policies-for-service-fabric-services"></a><span data-ttu-id="5de8e-103">Plaatsingsbeleid voor service fabric-services</span><span class="sxs-lookup"><span data-stu-id="5de8e-103">Placement policies for service fabric services</span></span>
<span data-ttu-id="5de8e-104">Plaatsing beleidsregels zijn extra regels die plaatsing van de service gebruikte toogovern in enkele specifieke, minder algemene scenario's kunnen worden.</span><span class="sxs-lookup"><span data-stu-id="5de8e-104">Placement policies are additional rules that can be used toogovern service placement in some specific, less-common scenarios.</span></span> <span data-ttu-id="5de8e-105">Er zijn enkele voorbeelden van de scenario's:</span><span class="sxs-lookup"><span data-stu-id="5de8e-105">Some examples of those scenarios are:</span></span>

- <span data-ttu-id="5de8e-106">Service Fabric-cluster omvat geografische afstanden, zoals meerdere lokale datacenters of tussen Azure-regio 's</span><span class="sxs-lookup"><span data-stu-id="5de8e-106">Your Service Fabric cluster spans geographic distances, such as multiple on-premises datacenters or across Azure regions</span></span>
- <span data-ttu-id="5de8e-107">Uw omgeving omvat meerdere gebieden van geopolitieke of een juridische of enige andere geval waar u de grenzen van het beleid hebt u nodig hebt tooenforce</span><span class="sxs-lookup"><span data-stu-id="5de8e-107">Your environment spans multiple areas of geopolitical or legal control, or some other case where you have policy boundaries you need tooenforce</span></span>
- <span data-ttu-id="5de8e-108">Er zijn communicatie prestaties of de latentie-overwegingen vanwege toolarge afstanden of het gebruik van een tragere of minder betrouwbaar netwerkkoppelingen</span><span class="sxs-lookup"><span data-stu-id="5de8e-108">There are communication performance or latency considerations due toolarge distances or use of slower or less reliable network links</span></span>
- <span data-ttu-id="5de8e-109">U moet tookeep bepaalde werkbelastingen geplaatste als een zo goed mogelijke poging met andere werkbelastingen of in de buurt toocustomers</span><span class="sxs-lookup"><span data-stu-id="5de8e-109">You need tookeep certain workloads collocated as a best effort, either with other workloads or in proximity toocustomers</span></span>

<span data-ttu-id="5de8e-110">De meeste van deze vereisten zijn afgestemd op Hallo fysieke indeling van Hallo-cluster, zoals Hallo domeinen met fouten van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="5de8e-110">Most of these requirements align with hello physical layout of hello cluster, represented as hello fault domains of hello cluster.</span></span> 

<span data-ttu-id="5de8e-111">Hallo geavanceerde plaatsing beleidsregels die helpen bij die de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="5de8e-111">hello advanced placement policies that help address these scenarios are:</span></span>

1. <span data-ttu-id="5de8e-112">Ongeldige domeinen</span><span class="sxs-lookup"><span data-stu-id="5de8e-112">Invalid domains</span></span>
2. <span data-ttu-id="5de8e-113">Vereiste domeinen</span><span class="sxs-lookup"><span data-stu-id="5de8e-113">Required domains</span></span>
3. <span data-ttu-id="5de8e-114">Voorkeursdomeinen</span><span class="sxs-lookup"><span data-stu-id="5de8e-114">Preferred domains</span></span>
4. <span data-ttu-id="5de8e-115">Replica verpakking verbieden</span><span class="sxs-lookup"><span data-stu-id="5de8e-115">Disallowing replica packing</span></span>

<span data-ttu-id="5de8e-116">De meeste Hallo volgende besturingselementen kan worden geconfigureerd via de eigenschappen van het knooppunt en plaatsingsbeperkingen, maar sommige ingewikkelder zijn.</span><span class="sxs-lookup"><span data-stu-id="5de8e-116">Most of hello following controls could be configured via node properties and placement constraints, but some are more complicated.</span></span> <span data-ttu-id="5de8e-117">toomake zaken eenvoudiger, Hallo Service Fabric-Cluster Resource Manager biedt deze extra plaatsingsbeleid.</span><span class="sxs-lookup"><span data-stu-id="5de8e-117">toomake things simpler, hello Service Fabric Cluster Resource Manager provides these additional placement policies.</span></span> <span data-ttu-id="5de8e-118">Plaatsing beleidsregels zijn geconfigureerd op basis van service per benoemde exemplaar.</span><span class="sxs-lookup"><span data-stu-id="5de8e-118">Placement policies are configured on a per-named service instance basis.</span></span> <span data-ttu-id="5de8e-119">Ze kunnen ook dynamisch worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="5de8e-119">They can also be updated dynamically.</span></span>

## <a name="specifying-invalid-domains"></a><span data-ttu-id="5de8e-120">Ongeldige domeinen opgeven</span><span class="sxs-lookup"><span data-stu-id="5de8e-120">Specifying invalid domains</span></span>
<span data-ttu-id="5de8e-121">Hallo **InvalidDomain** plaatsing beleid kunt u toospecify dat een bepaalde Foutdomein ongeldig voor een specifieke service is.</span><span class="sxs-lookup"><span data-stu-id="5de8e-121">hello **InvalidDomain** placement policy allows you toospecify that a particular Fault Domain is invalid for a specific service.</span></span> <span data-ttu-id="5de8e-122">Dit beleid zorgt ervoor dat een bepaalde service nooit wordt uitgevoerd op een bepaald gebied, bijvoorbeeld voor geopolitieke of zakelijke beleidsredenen.</span><span class="sxs-lookup"><span data-stu-id="5de8e-122">This policy ensures that a particular service never runs in a particular area, for example for geopolitical or corporate policy reasons.</span></span> <span data-ttu-id="5de8e-123">Meerdere ongeldige domeinen kunnen worden opgegeven via afzonderlijke beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="5de8e-123">Multiple invalid domains may be specified via separate policies.</span></span>

<span data-ttu-id="5de8e-124"><center>
![Voorbeeld van een domein is ongeldig][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="5de8e-124"><center>
![Invalid Domain Example][Image1]
</center></span></span>

<span data-ttu-id="5de8e-125">Code:</span><span class="sxs-lookup"><span data-stu-id="5de8e-125">Code:</span></span>

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="5de8e-126">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5de8e-126">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a><span data-ttu-id="5de8e-127">Vereiste domeinen opgeven</span><span class="sxs-lookup"><span data-stu-id="5de8e-127">Specifying required domains</span></span>
<span data-ttu-id="5de8e-128">Hallo vereist domein plaatsing beleid vereist dat Hallo-service alleen toegestaan in Hallo opgegeven domein is.</span><span class="sxs-lookup"><span data-stu-id="5de8e-128">hello required domain placement policy requires that hello service is present only in hello specified domain.</span></span> <span data-ttu-id="5de8e-129">Meerdere vereist domeinen kunnen worden opgegeven via afzonderlijke beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="5de8e-129">Multiple required domains can be specified via separate policies.</span></span>

<span data-ttu-id="5de8e-130"><center>
![Voorbeeld van een domein te verstrekken][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="5de8e-130"><center>
![Required Domain Example][Image2]
</center></span></span>

<span data-ttu-id="5de8e-131">Code:</span><span class="sxs-lookup"><span data-stu-id="5de8e-131">Code:</span></span>

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

<span data-ttu-id="5de8e-132">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5de8e-132">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a><span data-ttu-id="5de8e-133">Een voorkeur domein voor Hallo primaire replica's van een stateful service opgeven</span><span class="sxs-lookup"><span data-stu-id="5de8e-133">Specifying a preferred domain for hello primary replicas of a stateful service</span></span>
<span data-ttu-id="5de8e-134">Hallo primair domein voorkeur geeft Hallo veroorzaakt domein tooplace Hallo primaire in.</span><span class="sxs-lookup"><span data-stu-id="5de8e-134">hello Preferred Primary Domain specifies hello fault domain tooplace hello Primary in.</span></span> <span data-ttu-id="5de8e-135">Hallo primaire belandt in dit domein als alles goed.</span><span class="sxs-lookup"><span data-stu-id="5de8e-135">hello Primary ends up in this domain when everything is healthy.</span></span> <span data-ttu-id="5de8e-136">Als Hallo domein of de primaire replica Hallo mislukt of is afgesloten, Hallo primaire verplaatst toosome andere locatie, bij voorkeur in Hallo hetzelfde domein.</span><span class="sxs-lookup"><span data-stu-id="5de8e-136">If hello domain or hello Primary replica fails or shuts down, hello Primary moves toosome other location, ideally in hello same domain.</span></span> <span data-ttu-id="5de8e-137">Als deze nieuwe locatie niet in de gewenste domein hello, Hallo Cluster Resource Manager verplaatst toohello voorkeur domein zo snel mogelijk weer.</span><span class="sxs-lookup"><span data-stu-id="5de8e-137">If this new location isn't in hello preferred domain, hello Cluster Resource Manager moves it back toohello preferred domain as soon as possible.</span></span> <span data-ttu-id="5de8e-138">Deze instelling is natuurlijk alleen wel zinvol voor stateful services.</span><span class="sxs-lookup"><span data-stu-id="5de8e-138">Naturally this setting only makes sense for stateful services.</span></span> <span data-ttu-id="5de8e-139">Dit beleid is vooral nuttig in clusters die zijn spanned over verschillende Azure-regio's of meerdere datacenters maar services die liever plaatsing op een bepaalde locatie hebben.</span><span class="sxs-lookup"><span data-stu-id="5de8e-139">This policy is most useful in clusters that are spanned across Azure regions or multiple datacenters but have services that prefer placement in a certain location.</span></span> <span data-ttu-id="5de8e-140">Houden primaire sluiten tootheir gebruikers of andere services die helpt om lagere latentie te bieden met name voor leesbewerkingen, die zijn verwerkt door de primaire standaard.</span><span class="sxs-lookup"><span data-stu-id="5de8e-140">Keeping Primaries close tootheir users or other services helps provide lower latency, especially for reads, which are handled by Primaries by default.</span></span>

<span data-ttu-id="5de8e-141"><center>
![Primaire Voorkeursdomeinen en Failover][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="5de8e-141"><center>
![Preferred Primary Domains and Failover][Image3]
</center></span></span>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="5de8e-142">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5de8e-142">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a><span data-ttu-id="5de8e-143">Replica distributiepunten vereisen en verbieden verpakking</span><span class="sxs-lookup"><span data-stu-id="5de8e-143">Requiring replica distribution and disallowing packing</span></span>
<span data-ttu-id="5de8e-144">Replica's _normaal_ verdeeld over de fout en upgrade domeinen als Hallo cluster goed.</span><span class="sxs-lookup"><span data-stu-id="5de8e-144">Replicas are _normally_ distributed across fault and upgrade domains when hello cluster is healthy.</span></span> <span data-ttu-id="5de8e-145">Er zijn echter gevallen waarbij meer dan één replica voor een bepaalde partitie uiteindelijk tijdelijk ingepakte in één domein.</span><span class="sxs-lookup"><span data-stu-id="5de8e-145">However, there are cases where more than one replica for a given partition may end up temporarily packed into a single domain.</span></span> <span data-ttu-id="5de8e-146">Bijvoorbeeld, Stel dat cluster Hallo heeft negen knooppunten in drie domeinen met fouten, fd: / 0, fd: / 1 en fd: / 2.</span><span class="sxs-lookup"><span data-stu-id="5de8e-146">For example, let's say that hello cluster has nine nodes in three fault domains, fd:/0, fd:/1, and fd:/2.</span></span> <span data-ttu-id="5de8e-147">Stel dat uw service drie replica's heeft.</span><span class="sxs-lookup"><span data-stu-id="5de8e-147">Let's also say that your service has three replicas.</span></span> <span data-ttu-id="5de8e-148">Stel dat Hallo knooppunten die zijn gebruikt voor deze replica's in fd: / 1 en fd: / 2 werd afgesloten.</span><span class="sxs-lookup"><span data-stu-id="5de8e-148">Let's say that hello nodes that were being used for those replicas in fd:/1 and fd:/2 went down.</span></span> <span data-ttu-id="5de8e-149">Normaal gesproken liever Hallo Cluster Resource Manager andere knooppunten in die dezelfde domeinen met fouten.</span><span class="sxs-lookup"><span data-stu-id="5de8e-149">Normally hello Cluster Resource Manager would prefer other nodes in those same fault domains.</span></span> <span data-ttu-id="5de8e-150">In dit geval laten we dat vanwege problemen met toocapacity geen Hallo andere knooppunten in die domeinen zijn geldig.</span><span class="sxs-lookup"><span data-stu-id="5de8e-150">In this case, let's say due toocapacity issues none of hello other nodes in those domains were valid.</span></span> <span data-ttu-id="5de8e-151">Als Hallo Cluster Resource Manager builds vervangingen voor deze replica's, zou deze toochoose knooppunten hebben in fd: / 0.</span><span class="sxs-lookup"><span data-stu-id="5de8e-151">If hello Cluster Resource Manager builds replacements for those replicas, it would have toochoose nodes in fd:/0.</span></span> <span data-ttu-id="5de8e-152">Echter, doen _die_ maakt een situatie waarin Hallo Foutdomein beperking wordt geschonden.</span><span class="sxs-lookup"><span data-stu-id="5de8e-152">However, doing _that_ creates a situation where hello Fault Domain constraint is violated.</span></span> <span data-ttu-id="5de8e-153">Replica's toeneemt Hallo kans dat gehele replicaset Hallo verpakking kan uitvallen of verloren gaan.</span><span class="sxs-lookup"><span data-stu-id="5de8e-153">Packing replicas increases hello chance that hello whole replica set could go down or be lost.</span></span> 

> [!NOTE]
> <span data-ttu-id="5de8e-154">Voor meer informatie over de beperkingen en beperking in het algemeen uitchecken van prioriteiten [in dit onderwerp](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span><span class="sxs-lookup"><span data-stu-id="5de8e-154">For more information on constraints and constraint priorities generally, check out [this topic](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span></span>
>

<span data-ttu-id="5de8e-155">Als u ooit zag een health-bericht, zoals '`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`', en vervolgens hebt u dit probleem of ongeveer het bereikt.</span><span class="sxs-lookup"><span data-stu-id="5de8e-155">If you've ever seen a health message such as "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", then you've hit this condition or something like it.</span></span> <span data-ttu-id="5de8e-156">Meestal slechts één of twee replica's zijn bijeengebracht tijdelijk.</span><span class="sxs-lookup"><span data-stu-id="5de8e-156">Usually only one or two replicas are packed together temporarily.</span></span> <span data-ttu-id="5de8e-157">Zolang er minder dan een quorum van replica's in een bepaald domein zijn, bent u veilig.</span><span class="sxs-lookup"><span data-stu-id="5de8e-157">So long as there are fewer than a quorum of replicas in a given domain, you're safe.</span></span> <span data-ttu-id="5de8e-158">Verpakking zelden voorkomt, maar dit kan gebeuren en meestal deze situaties tijdelijke omdat Hallo knooppunten keert u terug.</span><span class="sxs-lookup"><span data-stu-id="5de8e-158">Packing is rare, but it can happen, and usually these situations are transient since hello nodes come back.</span></span> <span data-ttu-id="5de8e-159">Als Hallo knooppunten omlaag blijven en Hallo Cluster Resource Manager toobuild vervangingen moet, zijn meestal er andere knooppunten beschikbaar in de ideale foutdomeinen Hallo.</span><span class="sxs-lookup"><span data-stu-id="5de8e-159">If hello nodes do stay down and hello Cluster Resource Manager needs toobuild replacements, usually there are other nodes available in hello ideal fault domains.</span></span>

<span data-ttu-id="5de8e-160">Sommige werkbelastingen liever steeds Hallo doelaantal replica's, zelfs als ze worden verpakt in minder domeinen.</span><span class="sxs-lookup"><span data-stu-id="5de8e-160">Some workloads would prefer always having hello target number of replicas, even if they are packed into fewer domains.</span></span> <span data-ttu-id="5de8e-161">Deze werkbelastingen zijn gokken tegen fouten in de totale gelijktijdige permanente domeinnaam en lokale staat gewoonlijk kunnen herstellen.</span><span class="sxs-lookup"><span data-stu-id="5de8e-161">These workloads are betting against total simultaneous permanent domain failures and can usually recover local state.</span></span> <span data-ttu-id="5de8e-162">Andere werkbelastingen in plaats daarvan voert u Hallo uitvaltijd ouder is dan het risico op juistheid of verlies van gegevens.</span><span class="sxs-lookup"><span data-stu-id="5de8e-162">Other workloads would rather take hello downtime earlier than risk correctness or loss of data.</span></span> <span data-ttu-id="5de8e-163">De meeste productie-workloads uitvoeren met meer dan drie replica's, meer dan drie domeinen met fouten en veel geldig knooppunten per domein met fouten.</span><span class="sxs-lookup"><span data-stu-id="5de8e-163">Most production workloads run with more than three replicas, more than three fault domains, and many valid nodes per fault domain.</span></span> <span data-ttu-id="5de8e-164">Als gevolg hiervan kunt standaardgedrag Hallo domein verpakking standaard.</span><span class="sxs-lookup"><span data-stu-id="5de8e-164">Because of this, hello default behavior allows domain packing by default.</span></span> <span data-ttu-id="5de8e-165">Hallo standaardgedrag kunt normale taakverdeling en failover toohandle deze uitzonderlijke gevallen, zelfs als dit betekent dat de tijdelijke domein verpakken.</span><span class="sxs-lookup"><span data-stu-id="5de8e-165">hello default behavior allows normal balancing and failover toohandle these extreme cases, even if that means temporary domain packing.</span></span>

<span data-ttu-id="5de8e-166">Als u wilt dat toodisable samenhangende voor een bepaalde werkbelasting, kunt u Hallo `RequireDomainDistribution` beleid op Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="5de8e-166">If you want toodisable such packing for a given workload, you can specify hello `RequireDomainDistribution` policy on hello service.</span></span> <span data-ttu-id="5de8e-167">Als dit beleid is ingesteld, zorgt Hallo Cluster Resource Manager geen twee replica's van Hallo dezelfde partitie in Hallo dezelfde fault of upgradedomein worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5de8e-167">When this policy is set, hello Cluster Resource Manager ensures no two replicas from hello same partition run in hello same fault or upgrade domain.</span></span>

<span data-ttu-id="5de8e-168">Code:</span><span class="sxs-lookup"><span data-stu-id="5de8e-168">Code:</span></span>

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

<span data-ttu-id="5de8e-169">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5de8e-169">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

<span data-ttu-id="5de8e-170">Nu, zou deze mogelijk toouse worden deze configuraties voor services in een cluster dat is niet geografisch omspannen?</span><span class="sxs-lookup"><span data-stu-id="5de8e-170">Now, would it be possible toouse these configurations for services in a cluster that was not geographically spanned?</span></span> <span data-ttu-id="5de8e-171">U kunt, maar er is een goede reden te.</span><span class="sxs-lookup"><span data-stu-id="5de8e-171">You could, but there’s not a great reason too.</span></span> <span data-ttu-id="5de8e-172">Hallo moeten vereist, is ongeldig en aanbevolen domeinconfiguraties worden vermeden tenzij Hallo scenario's ze nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="5de8e-172">hello required, invalid, and preferred domain configurations should be avoided unless hello scenarios require them.</span></span> <span data-ttu-id="5de8e-173">Niet dat u zin tootry tooforce een bepaalde werkbelasting toorun in een Eén rek of tooprefer sommige segment van uw lokale cluster op een andere.</span><span class="sxs-lookup"><span data-stu-id="5de8e-173">It doesn't make any sense tootry tooforce a given workload toorun in a single rack, or tooprefer some segment of your local cluster over another.</span></span> <span data-ttu-id="5de8e-174">Verschillende hardwareconfiguraties moeten worden verdeeld over de domeinen met fouten en verwerkt via de normale plaatsingsbeperkingen en eigenschappen van het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="5de8e-174">Different hardware configurations should be spread across fault domains and handled via normal placement constraints and node properties.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5de8e-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5de8e-175">Next steps</span></span>
- <span data-ttu-id="5de8e-176">Voor meer informatie over het configureren van services, [meer informatie over het configureren van Services](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="5de8e-176">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png

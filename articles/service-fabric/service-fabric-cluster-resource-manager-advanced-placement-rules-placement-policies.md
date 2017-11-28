---
title: Service Fabric Cluster Resource Manager - Plaatsingsbeleid | Microsoft Docs
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
ms.openlocfilehash: 6c11d49d5fdb3148b0534c9448f815358fa8cab3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="placement-policies-for-service-fabric-services"></a><span data-ttu-id="9c9cd-103">Plaatsingsbeleid voor service fabric-services</span><span class="sxs-lookup"><span data-stu-id="9c9cd-103">Placement policies for service fabric services</span></span>
<span data-ttu-id="9c9cd-104">Plaatsing beleidsregels zijn extra regels die kunnen worden gebruikt om te bepalen van de plaatsing van de service in een aantal specifieke, minder algemene scenario's.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-104">Placement policies are additional rules that can be used to govern service placement in some specific, less-common scenarios.</span></span> <span data-ttu-id="9c9cd-105">Er zijn enkele voorbeelden van de scenario's:</span><span class="sxs-lookup"><span data-stu-id="9c9cd-105">Some examples of those scenarios are:</span></span>

- <span data-ttu-id="9c9cd-106">Service Fabric-cluster omvat geografische afstanden, zoals meerdere lokale datacenters of tussen Azure-regio 's</span><span class="sxs-lookup"><span data-stu-id="9c9cd-106">Your Service Fabric cluster spans geographic distances, such as multiple on-premises datacenters or across Azure regions</span></span>
- <span data-ttu-id="9c9cd-107">Uw omgeving omvat meerdere gebieden van geopolitieke of een juridische of enige andere geval waar u beleid hebt grenzen die u wilt afdwingen</span><span class="sxs-lookup"><span data-stu-id="9c9cd-107">Your environment spans multiple areas of geopolitical or legal control, or some other case where you have policy boundaries you need to enforce</span></span>
- <span data-ttu-id="9c9cd-108">Er zijn communicatie prestaties of de latentie-overwegingen vanwege grote afstanden of het gebruik van een tragere of minder betrouwbaar netwerkkoppelingen</span><span class="sxs-lookup"><span data-stu-id="9c9cd-108">There are communication performance or latency considerations due to large distances or use of slower or less reliable network links</span></span>
- <span data-ttu-id="9c9cd-109">U moet ervoor zorgen bepaalde werkbelastingen geplaatste als een zo goed mogelijke poging met andere werkbelastingen of in de buurt aan klanten</span><span class="sxs-lookup"><span data-stu-id="9c9cd-109">You need to keep certain workloads collocated as a best effort, either with other workloads or in proximity to customers</span></span>

<span data-ttu-id="9c9cd-110">De meeste van deze vereisten zijn afgestemd op de fysieke indeling van het cluster, weergegeven als de domeinen met fouten van het cluster.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-110">Most of these requirements align with the physical layout of the cluster, represented as the fault domains of the cluster.</span></span> 

<span data-ttu-id="9c9cd-111">De geavanceerde plaatsing beleidsregels die helpen bij de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="9c9cd-111">The advanced placement policies that help address these scenarios are:</span></span>

1. <span data-ttu-id="9c9cd-112">Ongeldige domeinen</span><span class="sxs-lookup"><span data-stu-id="9c9cd-112">Invalid domains</span></span>
2. <span data-ttu-id="9c9cd-113">Vereiste domeinen</span><span class="sxs-lookup"><span data-stu-id="9c9cd-113">Required domains</span></span>
3. <span data-ttu-id="9c9cd-114">Voorkeursdomeinen</span><span class="sxs-lookup"><span data-stu-id="9c9cd-114">Preferred domains</span></span>
4. <span data-ttu-id="9c9cd-115">Replica verpakking verbieden</span><span class="sxs-lookup"><span data-stu-id="9c9cd-115">Disallowing replica packing</span></span>

<span data-ttu-id="9c9cd-116">De meeste van de volgende besturingselementen kan worden geconfigureerd via de eigenschappen van het knooppunt en plaatsingsbeperkingen, maar sommige ingewikkelder.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-116">Most of the following controls could be configured via node properties and placement constraints, but some are more complicated.</span></span> <span data-ttu-id="9c9cd-117">Voor een eenvoudiger dingen het Service Fabric Cluster Resource Manager biedt deze extra plaatsingsbeleid.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-117">To make things simpler, the Service Fabric Cluster Resource Manager provides these additional placement policies.</span></span> <span data-ttu-id="9c9cd-118">Plaatsing beleidsregels zijn geconfigureerd op basis van service per benoemde exemplaar.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-118">Placement policies are configured on a per-named service instance basis.</span></span> <span data-ttu-id="9c9cd-119">Ze kunnen ook dynamisch worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-119">They can also be updated dynamically.</span></span>

## <a name="specifying-invalid-domains"></a><span data-ttu-id="9c9cd-120">Ongeldige domeinen opgeven</span><span class="sxs-lookup"><span data-stu-id="9c9cd-120">Specifying invalid domains</span></span>
<span data-ttu-id="9c9cd-121">De **InvalidDomain** plaatsing beleid kunt u opgeven dat een bepaalde Foutdomein ongeldig voor een specifieke service is.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-121">The **InvalidDomain** placement policy allows you to specify that a particular Fault Domain is invalid for a specific service.</span></span> <span data-ttu-id="9c9cd-122">Dit beleid zorgt ervoor dat een bepaalde service nooit wordt uitgevoerd op een bepaald gebied, bijvoorbeeld voor geopolitieke of zakelijke beleidsredenen.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-122">This policy ensures that a particular service never runs in a particular area, for example for geopolitical or corporate policy reasons.</span></span> <span data-ttu-id="9c9cd-123">Meerdere ongeldige domeinen kunnen worden opgegeven via afzonderlijke beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-123">Multiple invalid domains may be specified via separate policies.</span></span>

<span data-ttu-id="9c9cd-124"><center>
![Voorbeeld van een domein is ongeldig][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="9c9cd-124"><center>
![Invalid Domain Example][Image1]
</center></span></span>

<span data-ttu-id="9c9cd-125">Code:</span><span class="sxs-lookup"><span data-stu-id="9c9cd-125">Code:</span></span>

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="9c9cd-126">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9c9cd-126">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a><span data-ttu-id="9c9cd-127">Vereiste domeinen opgeven</span><span class="sxs-lookup"><span data-stu-id="9c9cd-127">Specifying required domains</span></span>
<span data-ttu-id="9c9cd-128">Het vereiste domeinbeleid plaatsing vereist dat de service alleen toegestaan in het opgegeven domein is.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-128">The required domain placement policy requires that the service is present only in the specified domain.</span></span> <span data-ttu-id="9c9cd-129">Meerdere vereist domeinen kunnen worden opgegeven via afzonderlijke beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-129">Multiple required domains can be specified via separate policies.</span></span>

<span data-ttu-id="9c9cd-130"><center>
![Voorbeeld van een domein te verstrekken][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="9c9cd-130"><center>
![Required Domain Example][Image2]
</center></span></span>

<span data-ttu-id="9c9cd-131">Code:</span><span class="sxs-lookup"><span data-stu-id="9c9cd-131">Code:</span></span>

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

<span data-ttu-id="9c9cd-132">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9c9cd-132">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-the-primary-replicas-of-a-stateful-service"></a><span data-ttu-id="9c9cd-133">Een voorkeur domein voor de primaire replica's van een stateful service opgeven</span><span class="sxs-lookup"><span data-stu-id="9c9cd-133">Specifying a preferred domain for the primary replicas of a stateful service</span></span>
<span data-ttu-id="9c9cd-134">Het primaire domein voor de voorkeur geeft het foutdomein voor de primaire in plaatsen.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-134">The Preferred Primary Domain specifies the fault domain to place the Primary in.</span></span> <span data-ttu-id="9c9cd-135">De primaire belandt in dit domein als alles goed.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-135">The Primary ends up in this domain when everything is healthy.</span></span> <span data-ttu-id="9c9cd-136">Als het domein of de primaire replica mislukt of is afgesloten, wordt de primaire verplaatst naar een andere locatie in het ideale geval in hetzelfde domein.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-136">If the domain or the Primary replica fails or shuts down, the Primary moves to some other location, ideally in the same domain.</span></span> <span data-ttu-id="9c9cd-137">Als deze nieuwe locatie niet in het gewenste domein, verplaatst de Cluster Resource Manager terug naar het gewenste domein zo snel mogelijk.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-137">If this new location isn't in the preferred domain, the Cluster Resource Manager moves it back to the preferred domain as soon as possible.</span></span> <span data-ttu-id="9c9cd-138">Deze instelling is natuurlijk alleen wel zinvol voor stateful services.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-138">Naturally this setting only makes sense for stateful services.</span></span> <span data-ttu-id="9c9cd-139">Dit beleid is vooral nuttig in clusters die zijn spanned over verschillende Azure-regio's of meerdere datacenters maar services die liever plaatsing op een bepaalde locatie hebben.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-139">This policy is most useful in clusters that are spanned across Azure regions or multiple datacenters but have services that prefer placement in a certain location.</span></span> <span data-ttu-id="9c9cd-140">Primaire houden dicht bij hun gebruikers- of andere services bieden helpt lagere latentie met name voor leesbewerkingen die zijn verwerkt door de primaire standaard.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-140">Keeping Primaries close to their users or other services helps provide lower latency, especially for reads, which are handled by Primaries by default.</span></span>

<span data-ttu-id="9c9cd-141"><center>
![Primaire Voorkeursdomeinen en Failover][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="9c9cd-141"><center>
![Preferred Primary Domains and Failover][Image3]
</center></span></span>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="9c9cd-142">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9c9cd-142">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a><span data-ttu-id="9c9cd-143">Replica distributiepunten vereisen en verbieden verpakking</span><span class="sxs-lookup"><span data-stu-id="9c9cd-143">Requiring replica distribution and disallowing packing</span></span>
<span data-ttu-id="9c9cd-144">Replica's _normaal_ verdeeld over de fout en upgrade domeinen als het cluster goed.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-144">Replicas are _normally_ distributed across fault and upgrade domains when the cluster is healthy.</span></span> <span data-ttu-id="9c9cd-145">Er zijn echter gevallen waarbij meer dan één replica voor een bepaalde partitie uiteindelijk tijdelijk ingepakte in één domein.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-145">However, there are cases where more than one replica for a given partition may end up temporarily packed into a single domain.</span></span> <span data-ttu-id="9c9cd-146">Bijvoorbeeld, Stel dat het cluster negen knooppunten in drie domeinen met fouten, fd heeft: / 0, fd: / 1 en fd: / 2.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-146">For example, let's say that the cluster has nine nodes in three fault domains, fd:/0, fd:/1, and fd:/2.</span></span> <span data-ttu-id="9c9cd-147">Stel dat uw service drie replica's heeft.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-147">Let's also say that your service has three replicas.</span></span> <span data-ttu-id="9c9cd-148">Stel dat de knooppunten die zijn gebruikt voor deze replica's in fd: / 1 en fd: / 2 werd afgesloten.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-148">Let's say that the nodes that were being used for those replicas in fd:/1 and fd:/2 went down.</span></span> <span data-ttu-id="9c9cd-149">De Cluster Resource Manager liever normaal andere knooppunten in die dezelfde domeinen met fouten.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-149">Normally the Cluster Resource Manager would prefer other nodes in those same fault domains.</span></span> <span data-ttu-id="9c9cd-150">In dit geval Stel vanwege capaciteitsproblemen met de van dat de andere knooppunten in die domeinen zijn geldig.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-150">In this case, let's say due to capacity issues none of the other nodes in those domains were valid.</span></span> <span data-ttu-id="9c9cd-151">Als de Cluster Resource Manager builds vervangingen voor deze replica's, zou het moeten Kies knooppunten in fd: / 0.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-151">If the Cluster Resource Manager builds replacements for those replicas, it would have to choose nodes in fd:/0.</span></span> <span data-ttu-id="9c9cd-152">Echter, doen _die_ maakt een situatie waarin de beperking van het Foutdomein wordt geschonden.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-152">However, doing _that_ creates a situation where the Fault Domain constraint is violated.</span></span> <span data-ttu-id="9c9cd-153">Inpakken van replica's verhoogt kan de kans dat de hele replicaset uitvallen of verloren gaan.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-153">Packing replicas increases the chance that the whole replica set could go down or be lost.</span></span> 

> [!NOTE]
> <span data-ttu-id="9c9cd-154">Voor meer informatie over de beperkingen en beperking in het algemeen uitchecken van prioriteiten [in dit onderwerp](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span><span class="sxs-lookup"><span data-stu-id="9c9cd-154">For more information on constraints and constraint priorities generally, check out [this topic](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span></span>
>

<span data-ttu-id="9c9cd-155">Als u ooit zag een health-bericht, zoals '`The Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating the Constraint: FaultDomain`', en vervolgens hebt u dit probleem of ongeveer het bereikt.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-155">If you've ever seen a health message such as "`The Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating the Constraint: FaultDomain`", then you've hit this condition or something like it.</span></span> <span data-ttu-id="9c9cd-156">Meestal slechts één of twee replica's zijn bijeengebracht tijdelijk.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-156">Usually only one or two replicas are packed together temporarily.</span></span> <span data-ttu-id="9c9cd-157">Zolang er minder dan een quorum van replica's in een bepaald domein zijn, bent u veilig.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-157">So long as there are fewer than a quorum of replicas in a given domain, you're safe.</span></span> <span data-ttu-id="9c9cd-158">Verpakking zelden voorkomt, maar dit kan gebeuren en meestal deze situaties tijdelijke omdat de knooppunten keert u terug.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-158">Packing is rare, but it can happen, and usually these situations are transient since the nodes come back.</span></span> <span data-ttu-id="9c9cd-159">Als de knooppunten omlaag blijven en de Cluster Resource Manager moet vervangingen bouwen, zijn meestal er andere knooppunten beschikbaar in het ideale foutdomeinen.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-159">If the nodes do stay down and the Cluster Resource Manager needs to build replacements, usually there are other nodes available in the ideal fault domains.</span></span>

<span data-ttu-id="9c9cd-160">Sommige werkbelastingen liever altijd met het doelaantal replica's, zelfs als ze worden verpakt in minder domeinen.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-160">Some workloads would prefer always having the target number of replicas, even if they are packed into fewer domains.</span></span> <span data-ttu-id="9c9cd-161">Deze werkbelastingen zijn gokken tegen fouten in de totale gelijktijdige permanente domeinnaam en lokale staat gewoonlijk kunnen herstellen.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-161">These workloads are betting against total simultaneous permanent domain failures and can usually recover local state.</span></span> <span data-ttu-id="9c9cd-162">Andere werkbelastingen in plaats daarvan voert u de uitvaltijd ouder is dan het risico op juistheid of verlies van gegevens.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-162">Other workloads would rather take the downtime earlier than risk correctness or loss of data.</span></span> <span data-ttu-id="9c9cd-163">De meeste productie-workloads uitvoeren met meer dan drie replica's, meer dan drie domeinen met fouten en veel geldig knooppunten per domein met fouten.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-163">Most production workloads run with more than three replicas, more than three fault domains, and many valid nodes per fault domain.</span></span> <span data-ttu-id="9c9cd-164">Daarom kan het standaardgedrag domein verpakking standaard.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-164">Because of this, the default behavior allows domain packing by default.</span></span> <span data-ttu-id="9c9cd-165">Het standaardgedrag kunt normale taakverdeling en failover voor het afhandelen van deze uitzonderlijke gevallen, zelfs als dit betekent dat de tijdelijke domein verpakken.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-165">The default behavior allows normal balancing and failover to handle these extreme cases, even if that means temporary domain packing.</span></span>

<span data-ttu-id="9c9cd-166">Als u uitschakelen voor een bepaalde werkbelasting samenhangende wilt, kunt u de `RequireDomainDistribution` beleid op de service.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-166">If you want to disable such packing for a given workload, you can specify the `RequireDomainDistribution` policy on the service.</span></span> <span data-ttu-id="9c9cd-167">Wanneer deze dit beleid is ingesteld, wordt de Cluster Resource Manager dat geen twee replica's uit dezelfde partitie worden uitgevoerd in hetzelfde domein of upgrade van de fout.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-167">When this policy is set, the Cluster Resource Manager ensures no two replicas from the same partition run in the same fault or upgrade domain.</span></span>

<span data-ttu-id="9c9cd-168">Code:</span><span class="sxs-lookup"><span data-stu-id="9c9cd-168">Code:</span></span>

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

<span data-ttu-id="9c9cd-169">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9c9cd-169">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

<span data-ttu-id="9c9cd-170">Nu het mogelijk om deze configuraties voor services in een cluster dat is niet geografisch omspannen gebruiken?</span><span class="sxs-lookup"><span data-stu-id="9c9cd-170">Now, would it be possible to use these configurations for services in a cluster that was not geographically spanned?</span></span> <span data-ttu-id="9c9cd-171">U kunt, maar er is een goede reden te.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-171">You could, but there’s not a great reason too.</span></span> <span data-ttu-id="9c9cd-172">De vereist, is ongeldig en aanbevolen domeinconfiguraties moeten worden vermeden, tenzij ze in de scenario's nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-172">The required, invalid, and preferred domain configurations should be avoided unless the scenarios require them.</span></span> <span data-ttu-id="9c9cd-173">Niet dat u eventuele om te proberen voor een bepaalde werkbelasting in één rack uit te voeren of om de voorkeur sommige segment van uw lokale cluster op een andere te forceren.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-173">It doesn't make any sense to try to force a given workload to run in a single rack, or to prefer some segment of your local cluster over another.</span></span> <span data-ttu-id="9c9cd-174">Verschillende hardwareconfiguraties moeten worden verdeeld over de domeinen met fouten en verwerkt via de normale plaatsingsbeperkingen en eigenschappen van het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9c9cd-174">Different hardware configurations should be spread across fault domains and handled via normal placement constraints and node properties.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c9cd-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9c9cd-175">Next steps</span></span>
- <span data-ttu-id="9c9cd-176">Voor meer informatie over het configureren van services, [meer informatie over het configureren van Services](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="9c9cd-176">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png

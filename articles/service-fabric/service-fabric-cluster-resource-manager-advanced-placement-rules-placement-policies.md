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
# <a name="placement-policies-for-service-fabric-services"></a>Plaatsingsbeleid voor service fabric-services
Plaatsing beleidsregels zijn extra regels die plaatsing van de service gebruikte toogovern in enkele specifieke, minder algemene scenario's kunnen worden. Er zijn enkele voorbeelden van de scenario's:

- Service Fabric-cluster omvat geografische afstanden, zoals meerdere lokale datacenters of tussen Azure-regio 's
- Uw omgeving omvat meerdere gebieden van geopolitieke of een juridische of enige andere geval waar u de grenzen van het beleid hebt u nodig hebt tooenforce
- Er zijn communicatie prestaties of de latentie-overwegingen vanwege toolarge afstanden of het gebruik van een tragere of minder betrouwbaar netwerkkoppelingen
- U moet tookeep bepaalde werkbelastingen geplaatste als een zo goed mogelijke poging met andere werkbelastingen of in de buurt toocustomers

De meeste van deze vereisten zijn afgestemd op Hallo fysieke indeling van Hallo-cluster, zoals Hallo domeinen met fouten van Hallo-cluster. 

Hallo geavanceerde plaatsing beleidsregels die helpen bij die de volgende scenario's:

1. Ongeldige domeinen
2. Vereiste domeinen
3. Voorkeursdomeinen
4. Replica verpakking verbieden

De meeste Hallo volgende besturingselementen kan worden geconfigureerd via de eigenschappen van het knooppunt en plaatsingsbeperkingen, maar sommige ingewikkelder zijn. toomake zaken eenvoudiger, Hallo Service Fabric-Cluster Resource Manager biedt deze extra plaatsingsbeleid. Plaatsing beleidsregels zijn geconfigureerd op basis van service per benoemde exemplaar. Ze kunnen ook dynamisch worden bijgewerkt.

## <a name="specifying-invalid-domains"></a>Ongeldige domeinen opgeven
Hallo **InvalidDomain** plaatsing beleid kunt u toospecify dat een bepaalde Foutdomein ongeldig voor een specifieke service is. Dit beleid zorgt ervoor dat een bepaalde service nooit wordt uitgevoerd op een bepaald gebied, bijvoorbeeld voor geopolitieke of zakelijke beleidsredenen. Meerdere ongeldige domeinen kunnen worden opgegeven via afzonderlijke beleidsregels.

<center>
![Voorbeeld van een domein is ongeldig][Image1]
</center>

Code:

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a>Vereiste domeinen opgeven
Hallo vereist domein plaatsing beleid vereist dat Hallo-service alleen toegestaan in Hallo opgegeven domein is. Meerdere vereist domeinen kunnen worden opgegeven via afzonderlijke beleidsregels.

<center>
![Voorbeeld van een domein te verstrekken][Image2]
</center>

Code:

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a>Een voorkeur domein voor Hallo primaire replica's van een stateful service opgeven
Hallo primair domein voorkeur geeft Hallo veroorzaakt domein tooplace Hallo primaire in. Hallo primaire belandt in dit domein als alles goed. Als Hallo domein of de primaire replica Hallo mislukt of is afgesloten, Hallo primaire verplaatst toosome andere locatie, bij voorkeur in Hallo hetzelfde domein. Als deze nieuwe locatie niet in de gewenste domein hello, Hallo Cluster Resource Manager verplaatst toohello voorkeur domein zo snel mogelijk weer. Deze instelling is natuurlijk alleen wel zinvol voor stateful services. Dit beleid is vooral nuttig in clusters die zijn spanned over verschillende Azure-regio's of meerdere datacenters maar services die liever plaatsing op een bepaalde locatie hebben. Houden primaire sluiten tootheir gebruikers of andere services die helpt om lagere latentie te bieden met name voor leesbewerkingen, die zijn verwerkt door de primaire standaard.

<center>
![Primaire Voorkeursdomeinen en Failover][Image3]
</center>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a>Replica distributiepunten vereisen en verbieden verpakking
Replica's _normaal_ verdeeld over de fout en upgrade domeinen als Hallo cluster goed. Er zijn echter gevallen waarbij meer dan één replica voor een bepaalde partitie uiteindelijk tijdelijk ingepakte in één domein. Bijvoorbeeld, Stel dat cluster Hallo heeft negen knooppunten in drie domeinen met fouten, fd: / 0, fd: / 1 en fd: / 2. Stel dat uw service drie replica's heeft. Stel dat Hallo knooppunten die zijn gebruikt voor deze replica's in fd: / 1 en fd: / 2 werd afgesloten. Normaal gesproken liever Hallo Cluster Resource Manager andere knooppunten in die dezelfde domeinen met fouten. In dit geval laten we dat vanwege problemen met toocapacity geen Hallo andere knooppunten in die domeinen zijn geldig. Als Hallo Cluster Resource Manager builds vervangingen voor deze replica's, zou deze toochoose knooppunten hebben in fd: / 0. Echter, doen _die_ maakt een situatie waarin Hallo Foutdomein beperking wordt geschonden. Replica's toeneemt Hallo kans dat gehele replicaset Hallo verpakking kan uitvallen of verloren gaan. 

> [!NOTE]
> Voor meer informatie over de beperkingen en beperking in het algemeen uitchecken van prioriteiten [in dit onderwerp](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).
>

Als u ooit zag een health-bericht, zoals '`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`', en vervolgens hebt u dit probleem of ongeveer het bereikt. Meestal slechts één of twee replica's zijn bijeengebracht tijdelijk. Zolang er minder dan een quorum van replica's in een bepaald domein zijn, bent u veilig. Verpakking zelden voorkomt, maar dit kan gebeuren en meestal deze situaties tijdelijke omdat Hallo knooppunten keert u terug. Als Hallo knooppunten omlaag blijven en Hallo Cluster Resource Manager toobuild vervangingen moet, zijn meestal er andere knooppunten beschikbaar in de ideale foutdomeinen Hallo.

Sommige werkbelastingen liever steeds Hallo doelaantal replica's, zelfs als ze worden verpakt in minder domeinen. Deze werkbelastingen zijn gokken tegen fouten in de totale gelijktijdige permanente domeinnaam en lokale staat gewoonlijk kunnen herstellen. Andere werkbelastingen in plaats daarvan voert u Hallo uitvaltijd ouder is dan het risico op juistheid of verlies van gegevens. De meeste productie-workloads uitvoeren met meer dan drie replica's, meer dan drie domeinen met fouten en veel geldig knooppunten per domein met fouten. Als gevolg hiervan kunt standaardgedrag Hallo domein verpakking standaard. Hallo standaardgedrag kunt normale taakverdeling en failover toohandle deze uitzonderlijke gevallen, zelfs als dit betekent dat de tijdelijke domein verpakken.

Als u wilt dat toodisable samenhangende voor een bepaalde werkbelasting, kunt u Hallo `RequireDomainDistribution` beleid op Hallo-service. Als dit beleid is ingesteld, zorgt Hallo Cluster Resource Manager geen twee replica's van Hallo dezelfde partitie in Hallo dezelfde fault of upgradedomein worden uitgevoerd.

Code:

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

Nu, zou deze mogelijk toouse worden deze configuraties voor services in een cluster dat is niet geografisch omspannen? U kunt, maar er is een goede reden te. Hallo moeten vereist, is ongeldig en aanbevolen domeinconfiguraties worden vermeden tenzij Hallo scenario's ze nodig hebt. Niet dat u zin tootry tooforce een bepaalde werkbelasting toorun in een Eén rek of tooprefer sommige segment van uw lokale cluster op een andere. Verschillende hardwareconfiguraties moeten worden verdeeld over de domeinen met fouten en verwerkt via de normale plaatsingsbeperkingen en eigenschappen van het knooppunt.

## <a name="next-steps"></a>Volgende stappen
- Voor meer informatie over het configureren van services, [meer informatie over het configureren van Services](service-fabric-cluster-resource-manager-configure-services.md)

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png

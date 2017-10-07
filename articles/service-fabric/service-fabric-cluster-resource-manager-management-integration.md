---
title: aaaService Fabric Cluster Resource Manager - Management-integratie | Microsoft Docs
description: Een overzicht van Hallo integratiepunten tussen Hallo Cluster Resource Manager en Service Fabric-beheer.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 956cd0b8-b6e3-4436-a224-8766320e8cd7
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9a24c9de121fbe2e8e5e8e4d117e64686918936a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-integration-with-service-fabric-cluster-management"></a>Cluster resource manager-integratie met Service Fabric-Clusterbeheer
Hallo Service Fabric-Cluster Resource Manager biedt geen upgrades station in Service Fabric, maar het is betrokken. Hallo eerste manier die Hallo Cluster Resource Manager helpt met management door bijhouden Hallo gewenste status van het Hallo-cluster en Hallo services binnen het. Hallo Cluster Resource Manager verzendt statusrapporten wanneer deze kan niet Hallo cluster in de gewenste configuratie Hallo zet. Bijvoorbeeld, als er onvoldoende verzendt capaciteit Hallo Cluster Resource Manager health-waarschuwingen en fouten die wijzen op Hallo probleem. Een andere stukje integratie heeft toodo met de werking van upgrades. Hallo Cluster Resource Manager verandert het gedrag enigszins tijdens upgrades.  

## <a name="health-integration"></a>Health-integratie
Hallo Cluster Resource Manager houdt voortdurend Hallo regels die u hebt gedefinieerd voor de plaatsing van uw services. Het houdt ook Hallo resterende capaciteit voor elke metriek op Hallo knooppunten en Hallo-cluster en Hallo cluster als geheel. Als deze kan niet voldoen aan deze regels of als er onvoldoende capaciteit, status, waarschuwingen en fouten verzonden. Bijvoorbeeld, als een knooppunt op de capaciteit en Hallo zal Cluster Resource Manager toofix Hallo situatie proberen door te verplaatsen van services. Als deze niet kan Hallo situatie verhelpen zendt het een waarschuwing die aangeeft welk knooppunt is overbelast en voor welke metrische gegevens.

Een ander voorbeeld van Hallo Resource Manager-waarschuwingen is schendingen van plaatsingsbeperkingen. Bijvoorbeeld, als u een beperking voor de plaatsing hebt gedefinieerd (zoals `“NodeColor == Blue”`) en Hallo Resource Manager detecteert een schending van deze beperking, het verzendt een waarschuwing. Dit geldt voor aangepaste beperkingen en Hallo standaardbeperkingen (zoals Hallo Foutdomein en het upgraden van domein beperkingen).

Hier volgt een voorbeeld van een dergelijke statusrapport. In dit geval is Hallo statusrapport voor een van de partities Hallo systeemservice. Hallo-bericht van status geeft aan Hallo replica's van de betreffende partitie tijdelijk worden verpakt in te weinig domeinen upgraden.

```posh
PS C:\Users\User > Get-WindowsFabricPartitionHealth -PartitionId '00000000-0000-0000-0000-000000000001'


PartitionId           : 00000000-0000-0000-0000-000000000001
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.PLB', Property='ReplicaConstraintViolation_UpgradeDomain', HealthState='Warning', ConsiderWarningAsError=false.

ReplicaHealthStates   :
                        ReplicaId             : 130766528804733380
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577821
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528854889931
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577822
                        AggregatedHealthState : Ok

                        ReplicaId             : 130837073190680024
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.PLB
                        Property              : ReplicaConstraintViolation_UpgradeDomain
                        HealthState           : Warning
                        SequenceNumber        : 130837100116930204
                        SentAt                : 8/10/2015 7:53:31 PM
                        ReceivedAt            : 8/10/2015 7:53:33 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer has detected a Constraint Violation for this Replica: fabric:/System/FailoverManagerService Secondary Partition 00000000-0000-0000-0000-000000000001 is
                        violating hello Constraint: UpgradeDomain Details: UpgradeDomain ID -- 4, Replica on NodeName -- Node.8 Currently Upgrading -- false Distribution Policy -- Packing
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Ok->Warning = 8/10/2015 7:13:02 PM, LastError = 1/1/0001 12:00:00 AM
```

Dit is wat dit bericht health zorgt ervoor dat ons is:

1. Alle replica's Hallo zichzelf zijn in orde: elk AggregatedHealthState heeft: Ok
2. Hallo upgraden domein distributie-beperking is momenteel wordt geschonden. Dit betekent dat een bepaald domein voor het upgraden meer replica's van deze partitie dan nodig is.
3. Welk knooppunt bevat Hallo replica veroorzaakt Hallo schending. In dit geval het knooppunt met de naam van de Hallo 'Node.8' Hallo is
4. Hiermee wordt aangegeven of een upgrade die momenteel gebeurt er voor deze partitie ('momenteel upgraden--false")
5. Hallo distributiebeleid voor deze service: 'Distributie beleid--verpakking'. Hiermee wordt bepaald door Hallo `RequireDomainDistribution` [plaatsing beleid](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing). 'Verpakking' geeft aan dat in dit geval DomainDistribution _niet_ vereist, zodat de juiste plaatsing beleid is niet opgegeven voor deze service. 
6. Wanneer Hallo rapport is er gebeurd - 8-10-2015 7:13:02 PM

Informatie, zoals deze bevoegdheden waarschuwingen dat brand in productie toolet u weet iets is een fout opgetreden en is ook toodetect gebruikt en onjuiste upgrades is gestopt. In dit geval zou willen we toosee als we kunt achterhalen waarom Hallo Resource Manager toopack Hallo replica's in Hallo domein Upgrade had. Meestal verpakking is tijdelijke omdat Hallo knooppunten in Hallo andere domeinen upgraden, bijvoorbeeld zijn.

Stel dat Hallo Cluster Resource Manager probeert tooplace sommige services, maar er oplossingen die werken niet. Wanneer services kunnen niet worden geplaatst, is het meestal voor een van de volgende redenen Hallo:

1. Sommige tijdelijke toestand is het geworden onmogelijk tooplace deze service-exemplaar of de replica correct
2. Hallo-service plaatsing vereisten zijn ongeldig.

In dergelijke gevallen statusrapporten van Hallo Cluster Resource Manager kunnen u bepalen waarom Hallo-service kan niet worden geplaatst. We noemen deze reeks proces Hallo beperking elimineren. Tijdens het wordt Hallo-systeem begeleid bij Hallo geconfigureerd beperkingen die invloed hebben op Hallo-service en registreert wat het elimineren. Deze manier wanneer de services niet kunnen toobe geplaatst, kunt u zien welke knooppunten zijn geëlimineerd en waarom.

## <a name="constraint-types"></a>Beperkingstypen
Laten we spreken over elk van de andere beperkingen Hallo in deze health-rapporten. U ziet health berichten gerelateerde toothese beperkingen als replica's kunnen niet worden geplaatst.

* **ReplicaExclusionStatic** en **ReplicaExclusionDynamic**: deze beperkingen geeft aan dat er een oplossing is afgewezen omdat twee serviceobjecten van dezelfde partitie Hallo zou hebben toobe geplaatst op Hallo hetzelfde knooppunt. Dit is niet toegestaan omdat vervolgens fout van dat knooppunt overmatig gevolgen zou hebben voor deze partitie. ReplicaExclusionStatic en ReplicaExclusionDynamic zijn bijna Hallo dezelfde regel en Hallo verschillen niet echt uitmaken. Als u een beperking eliminatie reeks die beide Hallo ReplicaExclusionStatic of ReplicaExclusionDynamic beperking, Hallo Cluster Resource Manager bevat denkt dat er niet voldoende knooppunten ziet. Hiervoor moet de resterende oplossingen toouse deze ongeldige plaatsingen die zijn niet toegestaan. Hallo wordt andere beperkingen in volgorde van Hallo meestal Vertel ons waarom de knooppunten in de eerste plaats Hallo worden wordt geëlimineerd.
* **PlacementConstraint**: als u dit bericht ziet, betekent dit dat we sommige knooppunten geëlimineerd omdat ze niet overeenkomen met de plaatsingsbeperkingen Hallo-service. We traceren uit plaatsingsbeperkingen Hallo die momenteel zijn geconfigureerd als onderdeel van dit bericht. Dit is normaal als er een plaatsing-beperking gedefinieerd. Echter, als de beperking van de plaatsing van onjuist wordt veroorzaakt door te veel knooppunten toobe geëlimineerd dit is hoe merkt u.
* **NodeCapacity**: deze beperking betekent dat Cluster Resource Manager Hallo replica's kunnen niet plaats op Hallo Hallo aangegeven knooppunten omdat die ze via capaciteit plaatst.
* **Affiniteit**: deze beperking geeft aan dat we Hallo replica kan niet plaats op Hallo van invloed op een knooppunten omdat hierdoor een schending van beperking van Hallo affiniteit. Meer informatie over de affiniteit is in [in dit artikel](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
* **FaultDomain** en **UpgradeDomain**: deze beperking knooppunten elimineert als brengen Hallo replica op Hallo aangegeven knooppunten zou leiden tot verpakken in een bepaalde fout of een upgradedomein. Enkele voorbeelden voor het bespreken van deze beperking wordt weergegeven in het onderwerp Hallo op [probleem- en upgrade domain-beperkingen en het resulterende gedrag](service-fabric-cluster-resource-manager-cluster-description.md)
* **PreferredLocation**: er mag niet deze beperking verwijderen van knooppunten uit Hallo oplossing omdat deze wordt uitgevoerd als een optimalisatie standaard normaal. Hallo bij voorkeur locatiebeperking is ook aanwezig zijn tijdens upgrades. Tijdens de upgrade is het gebruikte toomove services back toowhere bij Hallo bijwerken gestart.

## <a name="blocklisting-nodes"></a>Blocklisting knooppunten
Een ander bericht Hallo Cluster Resource Manager statusrapporten is wanneer knooppunten zijn blocklisted. U kunt blocklisting beschouwen als een tijdelijke beperking die automatisch voor u is toegepast. Knooppunten krijgen blocklisted wanneer ze herhaalde fouten optreden tijdens het starten van exemplaren van dat servicetype. Knooppunten zijn blocklisted op basis van de per-service-type. Een knooppunt is mogelijk blocklisted voor één service-type maar niet nog een. 

Ziet u blocklisting kick in vaak tijdens de ontwikkeling: sommige bug zorgt ervoor dat uw service host toocrash bij het opstarten. Service Fabric probeert toocreate Hallo ServiceHost een paar keer en Hallo fout blijft optreden. Na enkele pogingen Hallo knooppunt opgehaald blocklisted en Hallo Cluster Resource Manager probeert elders toocreate Hallo-service. Als deze fout op meerdere knooppunten voordoet blijft, is het mogelijk dat alle geldige knooppunten Hallo in Hallo cluster uiteindelijk geblokkeerd. Blocklisting kan ook zo veel knooppunten dat niet voldoende Hallo service toomeet Hallo gewenste schaal met succes kunt starten verwijderen. Doorgaans ziet u extra fouten of waarschuwingen van Hallo Cluster Resource Manager waarmee wordt aangegeven dat Hallo service hieronder Hallo gewenste replica of aantal exemplaren, evenals de health-berichten die aangeven welke Hallo-fout is ontstaan die toohello blocklisting in de eerste plaats Hallo.

Blocklisting is geen permanente voorwaarde. Hallo-knooppunt is verwijderd uit Hallo blocklist na een paar minuten en Service Fabric Hallo-services op het knooppunt opnieuw activeren. Als services kunnen toofail blijven, is Hallo knooppunt blocklisted voor dat servicetype opnieuw. 

### <a name="constraint-priorities"></a>Beperking prioriteiten

> [!WARNING]
> Beperking prioriteiten wijzigen wordt niet aangeraden en mogelijk belangrijke nadelige gevolgen hebben voor uw cluster. Hallo onderstaande informatie is beschikbaar voor verwijzing van Hallo default-beperking prioriteiten en hun gedrag. 
>

Met alle van deze beperkingen u mogelijk hebt is denkt 'Hey – ik denk dat dat veroorzaakt domein beperkingen Hallo belangrijkste in mijn systeem zijn. In de volgorde tooensure hello veroorzaakt domeinbeperking niet is geschonden, ik ben bereid tooviolate andere beperkingen. "

Beperkingen kunnen worden geconfigureerd met verschillende prioriteitsniveaus. Dit zijn:

   - 'harde' (0)
   - 'soft' (1)
   - 'optimalisatie' (2)
   - "off" (-1). 
   
De meeste Hallo beperkingen zijn standaard geconfigureerd als harde beperkingen.

Het is ongewoon Hallo prioriteit van beperkingen wijzigen. Er zijn keren waar beperking prioriteiten toochange, meestal toowork rond een andere fout of probleem dat invloed had op Hallo-omgeving nodig zijn. In het algemeen Hallo flexibiliteit van Hallo beperking prioriteit infrastructuur uitstekend heeft gewerkt, maar vaak is niet nodig. Meestal zijn Hallo alles bevindt zich op hun Standaardprioriteiten. 

Hallo prioriteitsniveaus niet inhouden dat een bepaalde beperking _wordt_ worden geschonden, evenmin dat zal altijd worden voldaan. Beperking prioriteiten definiëren de volgorde waarin u beperkingen gelden. Prioriteiten Hallo-en nadelen wanneer het onmogelijk toosatisfy alle beperkingen definiëren. Alle Hallo beperkingen kunnen meestal worden voldaan, tenzij er iets anders in Hallo omgeving aan de hand. Enkele voorbeelden van scenario's die tooconstraint schendingen leiden zijn strijdige beperkingen of grote aantallen gelijktijdige fouten.

U kunt in geavanceerde situaties Hallo beperking prioriteiten wijzigen. Stel dat u deze wilde tooensure zouden affiniteit altijd geschonden wanneer nodig toosolve knooppunt capaciteit uitgeeft. tooachieve deze u kan Hallo prioriteit van Hallo affiniteit beperking te 'soft' (1) instellen en laat Hallo capaciteit beperking te 'harde' instellen (0).

Hallo standaardwaarden prioriteit voor Hallo andere beperkingen zijn opgegeven in Hallo config te volgen:

ClusterManifest.xml

```xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PlacementConstraintPriority" Value="0" />
            <Parameter Name="CapacityConstraintPriority" Value="0" />
            <Parameter Name="AffinityConstraintPriority" Value="0" />
            <Parameter Name="FaultDomainConstraintPriority" Value="0" />
            <Parameter Name="UpgradeDomainConstraintPriority" Value="1" />
            <Parameter Name="PreferredLocationConstraintPriority" Value="2" />
        </Section>
```

gehoste clusters via ClusterConfig.json voor zelfstandige implementaties of Template.json voor Azure:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PlacementConstraintPriority",
          "value": "0"
      },
      {
          "name": "CapacityConstraintPriority",
          "value": "0"
      },
      {
          "name": "AffinityConstraintPriority",
          "value": "0"
      },
      {
          "name": "FaultDomainConstraintPriority",
          "value": "0"
      },
      {
          "name": "UpgradeDomainConstraintPriority",
          "value": "1"
      },
      {
          "name": "PreferredLocationConstraintPriority",
          "value": "2"
      }
    ]
  }
]
```

## <a name="fault-domain-and-upgrade-domain-constraints"></a>Beperkingen voor fouttolerantie domein- en domein
Hallo Cluster Resource Manager wil tookeep services verdeeld tussen domeinen met fouten en upgrade. Deze modellen dit als een beperking in Hallo Cluster Resource Manager van engine. Voor meer informatie over hoe ze worden gebruikt en hun gedrag bij specifieke uitchecken Hallo artikel op [clusterconfiguratie](service-fabric-cluster-resource-manager-cluster-description.md#fault-and-upgrade-domain-constraints-and-resulting-behavior).

Hallo Cluster Resource Manager wellicht toopack een aantal replica's in een upgradedomein in volgorde toodeal met upgrades, fouten of andere schendingen van plaatsingsbeperkingen. Normaal gesproken verpakken in domeinen met fouten of upgrade gebeurt alleen als er zijn enkele fouten of andere verloop in Hallo-systeem voorkomen dat de correcte plaatsing. Als u tooprevent verpakking zelfs tijdens deze situaties wenst, kunt u gebruikmaken van Hallo `RequireDomainDistribution` [plaatsing beleid](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing). Houd er rekening mee dat dit mogelijk servicebeschikbaarheid en betrouwbaarheid als een neveneffect van invloed zijn op, dus zorgvuldig rekening te houden.

Hallo-omgeving juist is geconfigureerd, alle beperkingen zijn volledig in acht genomen, zelfs tijdens upgrades. Hallo belangrijk ding is dat Cluster Resource Manager uit voor uw beperkingen bekijkt hello. Als er een schending gedetecteerd wordt onmiddellijk gerapporteerd en toocorrect Hallo probleem probeert.

## <a name="hello-preferred-location-constraint"></a>de locatiebeperking Hallo voorkeur
Hallo PreferredLocation beperking is enigszins verschillen, als er twee verschillende manieren worden gebruikt. Er is een gebruik van deze beperking tijdens toepassingsupgrades. Hallo Cluster Resource Manager beheert automatisch deze beperking tijdens upgrades. Het gebruikte tooensure is dat wanneer upgrades zijn voltooid of replica's retourneren tootheir initiële locaties. Hallo andere Hallo PreferredLocation beperking wordt gebruikt bij Hallo [ `PreferredPrimaryDomain` plaatsing beleid](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md). Deze optimalisaties zijn, en is daarom Hallo PreferredLocation beperking Hallo alleen ingestelde-beperking te 'Optimalisatie' standaard.

## <a name="upgrades"></a>Upgrades
Er kunnen ook Hallo Cluster Resource Manager tijdens de toepassing en cluster, upgrades, waarin deze twee taken bevat:

* Zorg ervoor dat de regels van de cluster Hallo Hallo niet worden gecompromitteerd
* Probeer toohelp Hallo upgrade Ga soepel

### <a name="keep-enforcing-hello-rules"></a>Houd Hallo regels afdwingen
Hallo van groot belang dat toobe op de hoogte van is dat Hallo regels – Hallo strikte beperkingen zoals plaatsingsbeperkingen en capaciteit - nog steeds worden afgedwongen tijdens upgrades. Plaatsingsbeperkingen Zorg ervoor dat de werkbelasting van uw alleen uitgevoerd waar ze zijn toegestaan, zelfs tijdens upgrades. Wanneer services maximaal worden beperkt, kunnen upgrades langer duren. Voor een update die er enkele opties zijn mogelijk voor waar gaan wanneer Hallo service of deze wordt uitgevoerd op Hallo-knooppunt wordt verbroken.

### <a name="smart-replacements"></a>Smart vervangingen
Wanneer een upgrade wordt gestart, maakt Hallo Resource Manager een momentopname van huidige rangschikking Hallo van Hallo-cluster. Als u elk domein Upgrade is voltooid, probeert tooreturn Hallo services die in het upgraden van domein tootheir oorspronkelijke overeenkomst. Op deze manier zijn er maximaal twee overgangen voor een service tijdens het Hallo-upgrade. Er is een verplaatsing uit van Hallo van invloed op een knooppunt en een teruggaan in. Retourneren van Hallo cluster of de service toohow die deze was voordat de upgrade Hallo zorgt er ook voor Hallo upgrade heeft geen invloed op Hallo lay-out van Hallo-cluster. 

### <a name="reduced-churn"></a>Verminderde verloop
Een andere wat er tijdens upgrades gebeurt is die Hallo Cluster Resource Manager uitgeschakeld Netwerktaakverdeling wordt. Zo wordt voorkomen dat netwerktaakverdeling voorkomt u dat onnodige reacties toohello upgrade zelf, zoals het verplaatsen van services in knooppunten die u voor de upgrade Hallo hebt verwijderd. Als betrokken Hallo-upgrade de upgrade van een Cluster is, vervolgens Hallo gehele cluster is niet in balans tijdens de upgrade Hallo. Beperking controles blijft actief, alleen verkeer op basis van de proactieve verdeling van Hallo van metrische gegevens is uitgeschakeld.

### <a name="buffered-capacity--upgrade"></a>Buffer capaciteit & Upgrade
Doorgaans wilt u Hallo upgrade toocomplete als Hallo cluster toofull beperkte of sluiten. Hallo-capaciteit van Hallo cluster beheren is zelfs belangrijker tijdens upgrades dan normaal. Afhankelijk van Hallo worden aantal upgradedomeinen tussen 5 en 20 procent van de capaciteit gemigreerd als hello upgrade via Hallo-cluster totaliseert. Die werken heeft toogo ergens. Dit is waar begrip Hallo [gebufferd capaciteiten](service-fabric-cluster-resource-manager-cluster-description.md#buffered-capacity) is nuttig. De capaciteit van de buffer is tijdens de normale werking in acht genomen. Hallo Cluster Resource Manager mogelijk vult u knooppunten van de totale capaciteit tootheir (verbruikt Hallo buffer) tijdens upgrades indien nodig.

## <a name="next-steps"></a>Volgende stappen
* Vanaf Hallo begin starten en [ophalen van een inleiding toohello Service Fabric-Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)

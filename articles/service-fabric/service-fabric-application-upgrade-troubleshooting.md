---
title: aaaTroubleshooting toepassingsupgrades | Microsoft Docs
description: In dit artikel bevat enkele veelvoorkomende problemen rond het upgraden van een Service Fabric-toepassing en hoe tooresolve ze.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 19ad152e-ec50-4327-9f19-065c875c003c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 0f56fa61db9b4e32824623f162dc1bfe7fda0f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-upgrades"></a>Problemen met toepassingsupgrades oplossen
In dit artikel bevat informatie over een aantal veelvoorkomende problemen rond het upgraden van een Azure Service Fabric-toepassing hello en hoe tooresolve ze.

## <a name="troubleshoot-a-failed-application-upgrade"></a>Een upgrade van de mislukte toepassing oplossen
Wanneer een upgrade mislukt, Hallo uitvoer Hallo **Get-ServiceFabricApplicationUpgrade** -opdracht bevat aanvullende informatie voor foutopsporing Hallo-fout.  Hallo volgende lijst geeft aan hoe Hallo aanvullende informatie kan worden gebruikt:

1. Type van de fout Hallo identificeren.
2. Reden voor fout Hallo identificeren.
3. Een of meer onderdelen mislukken voor verder onderzoek isoleren.

Deze informatie is beschikbaar wanneer het Service Fabric detecteert Hallo fout ongeacht of hello **FailureAction** tooroll back of onderbreken Hallo upgrade.

### <a name="identify-hello-failure-type"></a>Type van de fout Hallo identificeren
In de uitvoer Hallo van **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identificeert de tijdstempel van de Hallo (in UTC-Notatie) waarmee een upgrade mislukt is gedetecteerd door de Service Fabric en  **FailureAction** is geactiveerd. **FailureReason** identificeert een van drie op hoog niveau mogelijke oorzaken van Hallo-fout:

1. UpgradeDomainTimeout - geeft aan dat een bepaalde upgradedomein toocomplete te lang duurde en **UpgradeDomainTimeout** verlopen.
2. OverallUpgradeTimeout - geeft aan dat de algemene upgrade Hallo toocomplete te lang duurde en **UpgradeTimeout** verlopen.
3. Statuscontrole - geeft aan dat na de upgrade van een updatedomein Hallo toepassing nog steeds niet in orde toohello volgens opgegeven statusbeleid en **HealthCheckRetryTimeout** verlopen.

Deze vermeldingen alleen weergegeven in de uitvoer van de Hallo wanneer Hallo upgrade mislukt en wordt gestart door terug te draaien. Meer informatie wordt weergegeven, afhankelijk van Hallo type Hallo-fout.

### <a name="investigate-upgrade-timeouts"></a>Upgrade-outs onderzoeken
Time-out fouten meestal door problemen met de servicebeschikbaarheid veroorzaakt worden bijwerken. Hallo-uitvoer hieronder is Typerend voor upgrades waarin service replica's of exemplaren niet toostart in Hallo nieuwe code-versie. Hallo **UpgradeDomainProgressAtFailure** veld bevat een momentopname van in behandeling upgrade werk gelijktijdig Hallo met fout.

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                : fabric:/DemoApp
ApplicationTypeName            : DemoAppType
TargetApplicationTypeVersion   : v2
ApplicationParameters          : {}
StartTimestampUtc              : 4/14/2015 9:26:38 PM
FailureTimestampUtc            : 4/14/2015 9:27:05 PM
FailureReason                  : UpgradeDomainTimeout
UpgradeDomainProgressAtFailure : MYUD1

                                 NodeName            : Node4
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 744c8d9f-1d26-417e-a60e-cd48f5c098f0

                                 NodeName            : Node1
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 4b43f4d8-b26b-424e-9307-7a7a62e79750
UpgradeState                   : RollingBackCompleted
UpgradeDuration                : 00:00:46
CurrentUpgradeDomainDuration   : 00:00:00
NextUpgradeDomain              :
UpgradeDomainsStatus           : { "MYUD1" = "Completed";
                                 "MYUD2" = "Completed";
                                 "MYUD3" = "Completed" }
UpgradeKind                    : Rolling
RollingUpgradeMode             : UnmonitoredAuto
ForceRestart                   : False
UpgradeReplicaSetCheckTimeout  : 00:00:00
```

In dit voorbeeld Hallo-upgrade is mislukt op upgradedomein *MYUD1* en twee partities (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* en *4b43f4d8-b26b-424e-9307-7a7a62e79750*) zijn vastgelopen. Hallo-partities zijn vastgelopen omdat Hallo runtime niet kan tooplace primaire replica's (*WaitForPrimaryPlacement*) op de doelknooppunten *knooppunt1* en *Knooppunt4*.

Hallo **Get-ServiceFabricNode** opdracht kan worden gebruikt tooverify die deze twee knooppunten in het upgradedomein *MYUD1*. Hallo *UpgradePhase* zegt *PostUpgradeSafetyCheck*, wat betekent dat deze controles veiligheid plaatsvinden nadat alle knooppunten in het upgradedomein Hallo bijgewerkt hebt. Deze informatie verwijst tooa potentiële probleem met de nieuwe versie Hallo van Hallo toepassingscode. de meest voorkomende problemen Hallo zijn service fouten in Hallo open of promotie tooprimary codepaden.

Een *UpgradePhase* van *PreUpgradeSafetyCheck* betekent dat er zijn problemen Hallo upgradedomein voorbereiden voordat deze werd uitgevoerd. de meest voorkomende problemen Hallo zijn in dit geval service fouten in Hallo sluiten of degradatie van primaire codepaden.

huidige Hallo **UpgradeState** is *RollingBackCompleted*, zodat de oorspronkelijke Hallo-upgrade moet worden uitgevoerd met een rollback **FailureAction**, die automatisch Hallo upgrade bij een fout wordt teruggedraaid. Als de oorspronkelijke Hallo-upgrade is uitgevoerd met een handmatige **FailureAction**, en vervolgens de upgrade Hallo in plaats daarvan in een live foutopsporing van toepassing hello onderbroken status tooallow zou worden.

### <a name="investigate-health-check-failures"></a>Health selectievakje fouten onderzoeken
Health selectievakje fouten kunnen worden geactiveerd door verschillende problemen die kunnen ontstaan nadat alle knooppunten in een upgradedomein upgraden en alle controles van de veiligheid wordt doorgegeven. Hallo-uitvoer hieronder is Typerend voor een upgrade mislukt vanwege toofailed statuscontroles. Hallo **UnhealthyEvaluations** veld bevat een momentopname van statuscontroles die niet bij Hallo Hallo upgrade toohello opgegeven volgens [statusbeleid](service-fabric-health-introduction.md).

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                         : fabric:/DemoApp
ApplicationTypeName                     : DemoAppType
TargetApplicationTypeVersion            : v4
ApplicationParameters                   : {}
StartTimestampUtc                       : 4/24/2015 2:42:31 AM
UpgradeState                            : RollingForwardPending
UpgradeDuration                         : 00:00:27
CurrentUpgradeDomainDuration            : 00:00:27
NextUpgradeDomain                       : MYUD2
UpgradeDomainsStatus                    : { "MYUD1" = "Completed";
                                          "MYUD2" = "Pending";
                                          "MYUD3" = "Pending" }
UnhealthyEvaluations                    :
                                          Unhealthy services: 50% (2/4), ServiceType='PersistedServiceType', MaxPercentUnhealthyServices=0%.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc3', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='3a9911f6-a2e5-452d-89a8-09271e7e49a8', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc2', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='744c8d9f-1d26-417e-a60e-cd48f5c098f0', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

UpgradeKind                             : Rolling
RollingUpgradeMode                      : Monitored
FailureAction                           : Manual
ForceRestart                            : False
UpgradeReplicaSetCheckTimeout           : 49710.06:28:15
HealthCheckWaitDuration                 : 00:00:00
HealthCheckStableDuration               : 00:00:10
HealthCheckRetryTimeout                 : 00:00:10
UpgradeDomainTimeout                    : 10675199.02:48:05.4775807
UpgradeTimeout                          : 10675199.02:48:05.4775807
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :
```

Een goed begrip van Service Fabric-statusmodel Hallo health selectievakje fouten onderzoeken eerst worden vereist. Maar zelfs zonder een diepgaand inzicht, ziet u twee services zijn slecht: *fabric: / DemoApp/Svc3* en *fabric: / DemoApp/Svc2*, samen met statusrapporten Hallo-fout ("InjectedFault 'in dit geval). In dit voorbeeld twee vier services zijn beschadigd, wat minder is dan Hallo standaard doel van 0% slecht (*MaxPercentUnhealthyServices*).

Hallo upgrade is onderbroken op mislukken door te geven een **FailureAction** van handmatige wanneer upgrade vanaf Hallo. Deze modus kan wij tooinvestigate Hallo live systeem status Hallo is mislukt voordat u geen verdere actie.

### <a name="recover-from-a-suspended-upgrade"></a>Herstellen van een onderbroken upgrade
Met terugdraaien **FailureAction**, er is geen herstel nodig omdat Hallo upgrade automatisch teruggedraaid in bij mislukken. Met een handmatige **FailureAction**, er zijn verschillende opties voor herstel:

1.  trigger terugdraaien
2. Hallo overige Hallo upgrade handmatig doorlopen
3. Hervatten Hallo bewaakt upgrade

Hallo **Start ServiceFabricApplicationRollback** opdracht kan worden gebruikt op een tijd toostart toepassing hello terugdraaien. Zodra het Hallo-opdracht geretourneerd met succes, wordt Hallo terugdraaien van de aanvraag is geregistreerd in Hallo systeem en start het kort nadien.

Hallo **hervatten ServiceFabricApplicationUpgrade** opdracht kan worden gebruikt tooproceed in Hallo rest Hallo handmatig, één upgradedomein tegelijk bijwerken. In deze modus worden alleen veiligheid controles uitgevoerd door Hallo-systeem. Niet meer health controles worden uitgevoerd. Met deze opdracht kan alleen worden gebruikt wanneer hello *UpgradeState* toont *RollingForwardPending*, wat betekent dat Hallo Huidig upgradedomein upgraden is voltooid maar hello naast een is niet gestart (in behandeling).

Hallo **Update ServiceFabricApplicationUpgrade** opdracht kan worden gebruikt tooresume Hallo bewaakt upgrade met veiligheid en de gezondheid controles worden uitgevoerd.

```
PS D:\temp> Update-ServiceFabricApplicationUpgrade fabric:/DemoApp -UpgradeMode Monitored

UpgradeMode                             : Monitored
ForceRestart                            :
UpgradeReplicaSetCheckTimeout           :
FailureAction                           :
HealthCheckWaitDuration                 :
HealthCheckStableDuration               :
HealthCheckRetryTimeout                 :
UpgradeTimeout                          :
UpgradeDomainTimeout                    :
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :

PS D:\temp>
```

Hallo upgrade blijft van Hallo upgradedomein waar deze het laatst werd onderbroken en gebruik Hallo dezelfde parameters en statusbeleid als vóór upgrade. Indien nodig, kan een van de parameters voor het bijwerken van Hallo en statusbeleid wordt weergegeven in de voorgaande uitvoer Hallo worden gewijzigd in Hallo dezelfde opdracht als Hallo upgrade wordt hervat. Hallo-upgrade is in dit voorbeeld hervat in de bewaakte modus Hallo parameters en Hallo statusbeleid ongewijzigd.

## <a name="further-troubleshooting"></a>Meer informatie over
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a>Service Fabric volgt is niet opgegeven Hallo statusbeleid
Mogelijke oorzaak 1:

Service Fabric kan alle percentages in het werkelijke aantal entiteiten (bijvoorbeeld, replica's, partities en services) voor de statusevaluatie en altijd Rondt naar boven toowhole entiteiten. Bijvoorbeeld, als hello maximale *MaxPercentUnhealthyReplicasPerPartition* 21% is en er zijn vijf replica's, en vervolgens de Service Fabric kunt up tootwo slecht replica's (dat wil zeggen,`Math.Ceiling (5*0.21)`). Statusbeleid moeten dus dienovereenkomstig worden ingesteld.

Mogelijke oorzaak 2:

Statusbeleid worden opgegeven in termen van percentage van totale services en niet specifiek service-exemplaren. Bijvoorbeeld, voordat u een upgrade uitvoert als een toepassing vier heeft service-exemplaren A, B, C en D, waarbij D service niet in orde is, maar met weinig invloed toohello toepassing. We willen tooignore Hallo slecht service D bekend tijdens de upgrade en stel Hallo parameter *MaxPercentUnhealthyServices* toobe 25%, ervan uitgaande dat alleen A, B en C moet toobe in orde.

Tijdens de upgrade Hallo kan D worden echter in orde terwijl C slecht. Hallo upgrade zou desondanks slagen omdat alleen 25% van het Hallo-services slecht zijn. Echter kan resulteren in onverwachte fouten vanwege tooC wordt onverwacht slecht in plaats van D. In dit geval D gemodelleerd als een andere servicetype uit A, B en c Omdat statusbeleid per servicetype zijn opgegeven, kunnen ander slecht percentage drempelwaarden toegepaste toodifferent services zijn. 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a>Ik een statusbeleid voor upgrade van de toepassing niet is opgegeven, maar Hallo upgrade nog steeds niet voor bepaalde time-outs die ik nooit opgegeven
Wanneer u statusbeleid zijn niet toohello upgradeaanvraag opgeeft, worden ze overgenomen van Hallo *ApplicationManifest.xml* van de huidige versie van toepassing hello. Bijvoorbeeld, als u een X van de toepassing van versie 1.0 tooversion 2.0 upgrade uitvoert, statusbeleid voor toepassing opgegeven voor versie 1.0 gebruikt. Als een andere statusbeleid moet worden gebruikt voor Hallo upgrade, moet Hallo beleid toobe opgegeven als onderdeel van Hallo toepassing upgrade API-aanroep. Hallo-beleidsregels die zijn opgegeven als deel van Hallo API-aanroep zijn alleen van toepassing tijdens de upgrade Hallo. Zodra het Hallo-upgrade is voltooid, Hallo beleid moet worden opgegeven in Hallo *ApplicationManifest.xml* worden gebruikt.

### <a name="incorrect-time-outs-are-specified"></a>Onjuiste time-outs zijn opgegeven
U zich mogelijk afgevraagd over wat er gebeurt wanneer time-outs inconsistent worden ingesteld. Bijvoorbeeld, u wellicht een *UpgradeTimeout* lager is dan Hallo *UpgradeDomainTimeout*. Hallo-antwoord is dat er een fout is geretourneerd. Fouten worden geretourneerd als hello *UpgradeDomainTimeout* kleiner is dan de som van Hallo *HealthCheckWaitDuration* en *HealthCheckRetryTimeout*, of als  *UpgradeDomainTimeout* kleiner is dan de som van Hallo *HealthCheckWaitDuration* en *HealthCheckStableDuration*.

### <a name="my-upgrades-are-taking-too-long"></a>Mijn upgrades duurt te lang
Hallo-tijd voor een upgrade toocomplete, is afhankelijk van statuscontroles Hallo en time-outs opgegeven. Afhankelijk van hoe lang het duurt toocopy, implementeren en regulering toepassing hello statuscontroles en time-outs. Wordt te agressief met time-outs kan het zijn dat meer mislukte upgrades, zodat u het beste eerst conservatieve met langer time-outs.

Dit is een snelle refresher op de wisselwerking tussen Hallo time-outs met Hallo upgrade tijden:

Voert een upgrade voor een upgradedomein kan niet worden voltooid sneller dan *HealthCheckWaitDuration* + *HealthCheckStableDuration*.

Upgrade mislukt is niet mogelijk sneller dan *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.

Hallo tijd voor de upgrade voor een upgradedomein, wordt beperkt door *UpgradeDomainTimeout*.  Als *HealthCheckRetryTimeout* en *HealthCheckStableDuration* zijn beide niet gelijk is aan nul en Hallo status van de toepassing hello houdt heen en weer schakelen en vervolgens de upgrade Hallo uiteindelijk een time-out optreedt op  *UpgradeDomainTimeout*. *UpgradeDomainTimeout* begint tellen omlaag eenmaal Hallo upgrade voor de huidige upgradedomein Hallo begint.

## <a name="next-steps"></a>Volgende stappen
[Een upgrade van uw toepassing met behulp van Visual Studio](service-fabric-application-upgrade-tutorial.md) begeleidt u bij een upgrade van de toepassing met Visual Studio.

[Een upgrade van uw toepassing met behulp van Powershell](service-fabric-application-upgrade-tutorial-powershell.md) begeleidt u bij een upgrade van de toepassing met behulp van PowerShell.

Bepalen hoe uw toepassing wordt bijgewerkt met behulp van [Parameters Upgrade](service-fabric-application-upgrade-parameters.md).

Uw toepassingsupgrades compatibel maken door leren hoe toouse [serialisatie van gegevens](service-fabric-application-upgrade-data-serialization.md).

Meer informatie over hoe toouse geavanceerde functies tijdens het bijwerken van uw toepassing door ernaar te verwijzen[geavanceerde onderwerpen](service-fabric-application-upgrade-advanced.md).

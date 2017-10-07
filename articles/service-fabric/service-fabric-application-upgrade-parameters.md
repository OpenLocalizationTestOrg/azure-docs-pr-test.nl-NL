---
title: 'Upgrade van de toepassing: upgrade parameters | Microsoft Docs'
description: Hierin wordt beschreven parameters gerelateerde tooupgrading een Service Fabric-toepassing, waaronder health controles tooperform en beleidsregels tooautomatically ongedaan maken Hallo upgrade.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a4170ac6-192e-44a8-b93d-7e39c92a347e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: abd0ba48c223be9aa0909c7a0100ba5986430db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-upgrade-parameters"></a>Parameters toepassingsupgrade
Dit artikel wordt beschreven Hallo verschillende parameters die van toepassing tijdens het Hallo-van een Azure Service Fabric-toepassing upgrade. Hallo parameters bevatten Hallo-naam en versie van de toepassing hello. Deze knoppen waarmee Hallo time-outs en statuscontroles die worden toegepast tijdens de upgrade Hallo zijn en ze verwijzen naar Hallo-beleidsregels die moeten worden toegepast wanneer een upgrade mislukt.

<br>

| Parameter | Beschrijving |
| --- | --- |
| ApplicationName |Naam van het Hallo-toepassing die wordt bijgewerkt. Voorbeelden: fabric: / VisualObjects, fabric: / ClusterMonitor |
| TargetApplicationTypeVersion |Hallo-versie van Hallo toepassingstype dat Hallo upgrade doelen. |
| FailureAction |Hallo actie op die door de Service Fabric als Hallo-upgrade is mislukt. Hallo-toepassing kan worden teruggedraaid toohello vooraf updateversie (rollback) of Hallo upgrade op Hallo Huidig upgradedomein kan worden gestopt. Hallo upgrademodus is in de laatste geval Hallo ook gewijzigde tooManual. Toegestane waarden zijn terugdraaien en voor handmatig. |
| HealthCheckWaitDurationSec |Hallo tijd toowait (in seconden) na de upgrade Hallo op Hallo upgradedomein is voltooid voordat de Service Fabric Hallo status van de toepassing hello evalueert. Deze duur kan ook worden beschouwd als een toepassing moet worden uitgevoerd voordat deze kan worden overwogen in orde Hallo-tijd. Als het Hallo statuscontrole verstrijkt, door het upgradeproces Hallo toohello volgende upgradedomein.  Als u Hallo health controle mislukt, wacht de Service Fabric voor een interval (hello UpgradeHealthCheckInterval) voordat u probeert de statuscontrole Hallo pas weer Hallo die healthcheckretrytimeout is bereikt. Hallo standaard en aanbevolen waarde is 0 seconden. |
| HealthCheckRetryTimeoutSec |Hallo duur (in seconden) dat Service Fabric tooperform evalueren blijft voordat er wordt gemeld Hallo upgrade mislukt. Hallo standaardwaarde is 600 seconden. Deze duur wordt gestart nadat HealthCheckWaitDuration is bereikt. Service Fabric mogelijk meerdere statuscontroles van de toepassingsstatus Hallo uitvoeren binnen deze HealthCheckRetryTimeout. Hallo-standaardwaarde is 10 minuten en moet op de juiste wijze worden aangepast voor uw toepassing. |
| HealthCheckStableDurationSec |Hallo tooverify duur (in seconden) dat de toepassing hello stabiel is voordat bewegende toohello volgende upgradedomein of upgrade voltooien Hallo. Deze wachttijd duur is wijzigingen van de juiste status gebruikte tooprevent niet gedetecteerd nadat Hallo statuscontrole wordt uitgevoerd. Hallo-standaardwaarde is 120 seconden en moet op de juiste wijze worden aangepast voor uw toepassing. |
| UpgradeDomainTimeoutSec |Maximale tijd (in seconden) voor het upgraden van een enkel upgradedomein. Als de time-outwaarde is bereikt, wordt Hallo upgrade gestopt en wordt voortgezet op basis van de instelling Hallo voor UpgradeFailureAction. de standaardwaarde Hallo is nooit (oneindig) en moet op de juiste wijze worden aangepast voor uw toepassing. |
| UpgradeTimeout |Er is een time-out (in seconden) die voor de hele Hallo-upgrade geldt. Als de time-outwaarde is bereikt, stopt de upgrade Hallo en UpgradeFailureAction wordt geactiveerd. de standaardwaarde Hallo is nooit (oneindig) en moet op de juiste wijze worden aangepast voor uw toepassing. |
| UpgradeHealthCheckInterval |Hallo frequentie dat Hallo gezondheidsstatus is ingeschakeld. Deze parameter is opgegeven in de sectie ClusterManager Hallo Hallo *cluster* *manifest*, en niet is opgegeven als onderdeel van de upgrade Hallo-cmdlet. Hallo-standaardwaarde is 60 seconden. |

<br>

## <a name="service-health-evaluation-during-application-upgrade"></a>Evaluatie van de health service tijdens de upgrade van de toepassing
<br>
evaluatie van criteria voor Hallo zijn optioneel. Als criteria voor evaluatie Hallo niet zijn opgegeven wanneer een upgrade wordt gestart, Service Fabric Hallo statusbeleid voor toepassing opgegeven in Hallo ApplicationManifest.xml van het toepassingsexemplaar Hallo gebruikt.

<br>

| Parameter | Beschrijving |
| --- | --- |
| ConsiderWarningAsError |Standaardwaarde is ONWAAR. Hallo waarschuwingsgebeurtenissen status voor de toepassing hello als fouten behandelen bij het evalueren van Hallo status van de toepassing hello tijdens de upgrade. Standaard Service Fabric kunnen niet worden geëvalueerd waarschuwing health gebeurtenissen toobe fouten (fouten), zodat het Hallo-upgrade kan worden voortgezet zelfs als er waarschuwingen zijn. |
| MaxPercentUnhealthyDeployedApplications |Standaard- en aanbevolen waarde is 0. Maximum aantal geïmplementeerde toepassingen Hallo opgeven (Zie Hallo [Health sectie](service-fabric-health-introduction.md)) die kan worden niet in orde voordat Hallo toepassing is in orde beschouwd en mislukt de upgrade Hallo. Deze parameter bepaalt Hallo toepassingsstatus op Hallo-knooppunt en kunt u problemen detecteren tijdens de upgrade. Normaal gesproken ophalen Hallo replica's van de toepassing hello taakverdeling toohello andere knooppunt waarmee Hallo toepassing tooappear orde is, zodat de upgrade tooproceed Hallo. Door te geven de status van een strikte MaxPercentUnhealthyDeployedApplications, Service Fabric snel een probleem met het toepassingspakket Hallo detecteren en te produceren van een snelle upgrade mislukken. |
| MaxPercentUnhealthyServices |Standaard- en aanbevolen waarde is 0. Geef Hallo kunt u het maximale aantal services in Hallo toepassingsexemplaar die beschadigd worden kan voordat de toepassing hello is in orde beschouwd en Hallo-upgrade is mislukt. |
| MaxPercentUnhealthyPartitionsPerService |Standaard- en aanbevolen waarde is 0. Geef Hallo kunt u het maximum aantal partities in een service die niet in orde zijn mag voordat het Hallo-service wordt beschouwd als niet in orde. |
| MaxPercentUnhealthyReplicasPerPartition |Standaard- en aanbevolen waarde is 0. Geef Hallo kunt u het maximale aantal replica's in de partitie die beschadigd worden kan voordat Hallo partitie wordt beschouwd als niet in orde. |
| UpgradeReplicaSetCheckTimeout |**Staatloze service**--binnen één upgradedomein, probeert de Service Fabric tooensure dat extra exemplaren van Hallo service beschikbaar zijn. Als exemplaren Hallo-doel meer dan één is, wacht Service Fabric is meer dan één exemplaar toobe beschikbaar up tooa maximale time-outwaarde. De time-outwaarde is opgegeven met behulp van Hallo UpgradeReplicaSetCheckTimeout eigenschap. Als het Hallo time-out is verlopen, door het Service Fabric met Hallo-upgrade, ongeacht het aantal exemplaren van de service Hallo. Aantal exemplaren op Hallo doel is, Service Fabric wacht niet als onmiddellijk wordt voortgezet met Hallo upgrade. **Stateful service**--binnen één upgradedomein, probeert de Service Fabric tooensure die replica Hallo set een quorum heeft. Service Fabric wacht tot een quorum toobe beschikbaar up tooa maximale time-outwaarde (opgegeven door Hallo UpgradeReplicaSetCheckTimeout eigenschap). Als het Hallo time-out is verlopen, door het Service Fabric met Hallo-upgrade, ongeacht het quorum. Deze instelling is ingesteld als nooit (oneindig) bij het implementeren van doorsturen en 900 seconden wanneer door terug te draaien. |
| ForceRestart |Als u een configuratie of een gegevenspakket zonder bij te werken Hallo servicecode bijwerkt, Hallo service opnieuw wordt gestart alleen als Hallo ForceRestart eigenschap tootrue is ingesteld. Wanneer het Hallo-update is voltooid, waarschuwt Service Fabric Hallo service dat een nieuwe configuratie of gegevenspakket beschikbaar is. Hallo-service is verantwoordelijk voor het toepassen van Hallo wijzigingen. Indien nodig, Hallo service kan opnieuw worden gestart zelf. |

<br>
<br>
Hallo MaxPercentUnhealthyServices MaxPercentUnhealthyPartitionsPerService en MaxPercentUnhealthyReplicasPerPartition criteria kunnen per type voor een exemplaar van de service worden opgegeven. Instellen van deze parameters per service kunt u een toepassing toocontain verschillende services typen met beleidsregels voor verschillende evaluatie. Een stateless gateway servicetype kan bijvoorbeeld een MaxPercentUnhealthyPartitionsPerService die verschilt van een type stateful-engine-service voor een bepaalde toepassingsexemplaar hebben.

## <a name="next-steps"></a>Volgende stappen
[Een upgrade van uw toepassing met behulp van Visual Studio](service-fabric-application-upgrade-tutorial.md) begeleidt u bij een upgrade van de toepassing met Visual Studio.

[Een upgrade van uw toepassing met behulp van Powershell](service-fabric-application-upgrade-tutorial-powershell.md) begeleidt u bij een upgrade van de toepassing met behulp van PowerShell.

[Bijwerken van uw toepassing met behulp van Service Fabric CLI op Linux](service-fabric-application-lifecycle-sfctl.md#upgrade-application) begeleidt u bij een upgrade van de toepassing met behulp van Service Fabric CLI.

[Bijwerken van uw toepassing met behulp van Service Fabric Eclipse-invoegtoepassing](service-fabric-get-started-eclipse.md#upgrade-your-service-fabric-java-application)

Uw toepassingsupgrades compatibel maken door leren hoe toouse [serialisatie van gegevens](service-fabric-application-upgrade-data-serialization.md).

Meer informatie over hoe toouse geavanceerde functies tijdens het bijwerken van uw toepassing door ernaar te verwijzen[geavanceerde onderwerpen](service-fabric-application-upgrade-advanced.md).

Veelvoorkomende problemen oplossen in toepassingsupgrades door te verwijzen toohello stappen in [toepassingsupgrades probleemoplossing](service-fabric-application-upgrade-troubleshooting.md).

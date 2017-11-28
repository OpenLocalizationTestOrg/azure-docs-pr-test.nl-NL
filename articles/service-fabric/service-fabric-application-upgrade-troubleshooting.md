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
# <a name="troubleshoot-application-upgrades"></a><span data-ttu-id="36ac6-103">Problemen met toepassingsupgrades oplossen</span><span class="sxs-lookup"><span data-stu-id="36ac6-103">Troubleshoot application upgrades</span></span>
<span data-ttu-id="36ac6-104">In dit artikel bevat informatie over een aantal veelvoorkomende problemen rond het upgraden van een Azure Service Fabric-toepassing hello en hoe tooresolve ze.</span><span class="sxs-lookup"><span data-stu-id="36ac6-104">This article covers some of hello common issues around upgrading an Azure Service Fabric application and how tooresolve them.</span></span>

## <a name="troubleshoot-a-failed-application-upgrade"></a><span data-ttu-id="36ac6-105">Een upgrade van de mislukte toepassing oplossen</span><span class="sxs-lookup"><span data-stu-id="36ac6-105">Troubleshoot a failed application upgrade</span></span>
<span data-ttu-id="36ac6-106">Wanneer een upgrade mislukt, Hallo uitvoer Hallo **Get-ServiceFabricApplicationUpgrade** -opdracht bevat aanvullende informatie voor foutopsporing Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="36ac6-106">When an upgrade fails, hello output of hello **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging hello failure.</span></span>  <span data-ttu-id="36ac6-107">Hallo volgende lijst geeft aan hoe Hallo aanvullende informatie kan worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="36ac6-107">hello following list specifies how hello additional information can be used:</span></span>

1. <span data-ttu-id="36ac6-108">Type van de fout Hallo identificeren.</span><span class="sxs-lookup"><span data-stu-id="36ac6-108">Identify hello failure type.</span></span>
2. <span data-ttu-id="36ac6-109">Reden voor fout Hallo identificeren.</span><span class="sxs-lookup"><span data-stu-id="36ac6-109">Identify hello failure reason.</span></span>
3. <span data-ttu-id="36ac6-110">Een of meer onderdelen mislukken voor verder onderzoek isoleren.</span><span class="sxs-lookup"><span data-stu-id="36ac6-110">Isolate one or more failing components for further investigation.</span></span>

<span data-ttu-id="36ac6-111">Deze informatie is beschikbaar wanneer het Service Fabric detecteert Hallo fout ongeacht of hello **FailureAction** tooroll back of onderbreken Hallo upgrade.</span><span class="sxs-lookup"><span data-stu-id="36ac6-111">This information is available when Service Fabric detects hello failure regardless of whether hello **FailureAction** is tooroll back or suspend hello upgrade.</span></span>

### <a name="identify-hello-failure-type"></a><span data-ttu-id="36ac6-112">Type van de fout Hallo identificeren</span><span class="sxs-lookup"><span data-stu-id="36ac6-112">Identify hello failure type</span></span>
<span data-ttu-id="36ac6-113">In de uitvoer Hallo van **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identificeert de tijdstempel van de Hallo (in UTC-Notatie) waarmee een upgrade mislukt is gedetecteerd door de Service Fabric en  **FailureAction** is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="36ac6-113">In hello output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies hello timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span></span> <span data-ttu-id="36ac6-114">**FailureReason** identificeert een van drie op hoog niveau mogelijke oorzaken van Hallo-fout:</span><span class="sxs-lookup"><span data-stu-id="36ac6-114">**FailureReason** identifies one of three potential high-level causes of hello failure:</span></span>

1. <span data-ttu-id="36ac6-115">UpgradeDomainTimeout - geeft aan dat een bepaalde upgradedomein toocomplete te lang duurde en **UpgradeDomainTimeout** verlopen.</span><span class="sxs-lookup"><span data-stu-id="36ac6-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long toocomplete and **UpgradeDomainTimeout** expired.</span></span>
2. <span data-ttu-id="36ac6-116">OverallUpgradeTimeout - geeft aan dat de algemene upgrade Hallo toocomplete te lang duurde en **UpgradeTimeout** verlopen.</span><span class="sxs-lookup"><span data-stu-id="36ac6-116">OverallUpgradeTimeout - Indicates that hello overall upgrade took too long toocomplete and **UpgradeTimeout** expired.</span></span>
3. <span data-ttu-id="36ac6-117">Statuscontrole - geeft aan dat na de upgrade van een updatedomein Hallo toepassing nog steeds niet in orde toohello volgens opgegeven statusbeleid en **HealthCheckRetryTimeout** verlopen.</span><span class="sxs-lookup"><span data-stu-id="36ac6-117">HealthCheck - Indicates that after upgrading an update domain, hello application remained unhealthy according toohello specified health policies and **HealthCheckRetryTimeout** expired.</span></span>

<span data-ttu-id="36ac6-118">Deze vermeldingen alleen weergegeven in de uitvoer van de Hallo wanneer Hallo upgrade mislukt en wordt gestart door terug te draaien.</span><span class="sxs-lookup"><span data-stu-id="36ac6-118">These entries only show up in hello output when hello upgrade fails and starts rolling back.</span></span> <span data-ttu-id="36ac6-119">Meer informatie wordt weergegeven, afhankelijk van Hallo type Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="36ac6-119">Further information is displayed depending on hello type of hello failure.</span></span>

### <a name="investigate-upgrade-timeouts"></a><span data-ttu-id="36ac6-120">Upgrade-outs onderzoeken</span><span class="sxs-lookup"><span data-stu-id="36ac6-120">Investigate upgrade timeouts</span></span>
<span data-ttu-id="36ac6-121">Time-out fouten meestal door problemen met de servicebeschikbaarheid veroorzaakt worden bijwerken.</span><span class="sxs-lookup"><span data-stu-id="36ac6-121">Upgrade timeout failures are most commonly caused by service availability issues.</span></span> <span data-ttu-id="36ac6-122">Hallo-uitvoer hieronder is Typerend voor upgrades waarin service replica's of exemplaren niet toostart in Hallo nieuwe code-versie.</span><span class="sxs-lookup"><span data-stu-id="36ac6-122">hello output following this paragraph is typical of upgrades where service replicas or instances fail toostart in hello new code version.</span></span> <span data-ttu-id="36ac6-123">Hallo **UpgradeDomainProgressAtFailure** veld bevat een momentopname van in behandeling upgrade werk gelijktijdig Hallo met fout.</span><span class="sxs-lookup"><span data-stu-id="36ac6-123">hello **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at hello time of failure.</span></span>

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

<span data-ttu-id="36ac6-124">In dit voorbeeld Hallo-upgrade is mislukt op upgradedomein *MYUD1* en twee partities (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* en *4b43f4d8-b26b-424e-9307-7a7a62e79750*) zijn vastgelopen.</span><span class="sxs-lookup"><span data-stu-id="36ac6-124">In this example, hello upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span></span> <span data-ttu-id="36ac6-125">Hallo-partities zijn vastgelopen omdat Hallo runtime niet kan tooplace primaire replica's (*WaitForPrimaryPlacement*) op de doelknooppunten *knooppunt1* en *Knooppunt4*.</span><span class="sxs-lookup"><span data-stu-id="36ac6-125">hello partitions were stuck because hello runtime was unable tooplace primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span></span>

<span data-ttu-id="36ac6-126">Hallo **Get-ServiceFabricNode** opdracht kan worden gebruikt tooverify die deze twee knooppunten in het upgradedomein *MYUD1*.</span><span class="sxs-lookup"><span data-stu-id="36ac6-126">hello **Get-ServiceFabricNode** command can be used tooverify that these two nodes are in upgrade domain *MYUD1*.</span></span> <span data-ttu-id="36ac6-127">Hallo *UpgradePhase* zegt *PostUpgradeSafetyCheck*, wat betekent dat deze controles veiligheid plaatsvinden nadat alle knooppunten in het upgradedomein Hallo bijgewerkt hebt.</span><span class="sxs-lookup"><span data-stu-id="36ac6-127">hello *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in hello upgrade domain have finished upgrading.</span></span> <span data-ttu-id="36ac6-128">Deze informatie verwijst tooa potentiële probleem met de nieuwe versie Hallo van Hallo toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="36ac6-128">All this information points tooa potential issue with hello new version of hello application code.</span></span> <span data-ttu-id="36ac6-129">de meest voorkomende problemen Hallo zijn service fouten in Hallo open of promotie tooprimary codepaden.</span><span class="sxs-lookup"><span data-stu-id="36ac6-129">hello most common issues are service errors in hello open or promotion tooprimary code paths.</span></span>

<span data-ttu-id="36ac6-130">Een *UpgradePhase* van *PreUpgradeSafetyCheck* betekent dat er zijn problemen Hallo upgradedomein voorbereiden voordat deze werd uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="36ac6-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing hello upgrade domain before it was performed.</span></span> <span data-ttu-id="36ac6-131">de meest voorkomende problemen Hallo zijn in dit geval service fouten in Hallo sluiten of degradatie van primaire codepaden.</span><span class="sxs-lookup"><span data-stu-id="36ac6-131">hello most common issues in this case are service errors in hello close or demotion from primary code paths.</span></span>

<span data-ttu-id="36ac6-132">huidige Hallo **UpgradeState** is *RollingBackCompleted*, zodat de oorspronkelijke Hallo-upgrade moet worden uitgevoerd met een rollback **FailureAction**, die automatisch Hallo upgrade bij een fout wordt teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="36ac6-132">hello current **UpgradeState** is *RollingBackCompleted*, so hello original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back hello upgrade upon failure.</span></span> <span data-ttu-id="36ac6-133">Als de oorspronkelijke Hallo-upgrade is uitgevoerd met een handmatige **FailureAction**, en vervolgens de upgrade Hallo in plaats daarvan in een live foutopsporing van toepassing hello onderbroken status tooallow zou worden.</span><span class="sxs-lookup"><span data-stu-id="36ac6-133">If hello original upgrade was performed with a manual **FailureAction**, then hello upgrade would instead be in a suspended state tooallow live debugging of hello application.</span></span>

### <a name="investigate-health-check-failures"></a><span data-ttu-id="36ac6-134">Health selectievakje fouten onderzoeken</span><span class="sxs-lookup"><span data-stu-id="36ac6-134">Investigate health check failures</span></span>
<span data-ttu-id="36ac6-135">Health selectievakje fouten kunnen worden geactiveerd door verschillende problemen die kunnen ontstaan nadat alle knooppunten in een upgradedomein upgraden en alle controles van de veiligheid wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="36ac6-135">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span></span> <span data-ttu-id="36ac6-136">Hallo-uitvoer hieronder is Typerend voor een upgrade mislukt vanwege toofailed statuscontroles.</span><span class="sxs-lookup"><span data-stu-id="36ac6-136">hello output following this paragraph is typical of an upgrade failure due toofailed health checks.</span></span> <span data-ttu-id="36ac6-137">Hallo **UnhealthyEvaluations** veld bevat een momentopname van statuscontroles die niet bij Hallo Hallo upgrade toohello opgegeven volgens [statusbeleid](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="36ac6-137">hello **UnhealthyEvaluations** field captures a snapshot of health checks that failed at hello time of hello upgrade according toohello specified [health policy](service-fabric-health-introduction.md).</span></span>

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

<span data-ttu-id="36ac6-138">Een goed begrip van Service Fabric-statusmodel Hallo health selectievakje fouten onderzoeken eerst worden vereist.</span><span class="sxs-lookup"><span data-stu-id="36ac6-138">Investigating health check failures first requires an understanding of hello Service Fabric health model.</span></span> <span data-ttu-id="36ac6-139">Maar zelfs zonder een diepgaand inzicht, ziet u twee services zijn slecht: *fabric: / DemoApp/Svc3* en *fabric: / DemoApp/Svc2*, samen met statusrapporten Hallo-fout ("InjectedFault 'in dit geval).</span><span class="sxs-lookup"><span data-stu-id="36ac6-139">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with hello error health reports ("InjectedFault" in this case).</span></span> <span data-ttu-id="36ac6-140">In dit voorbeeld twee vier services zijn beschadigd, wat minder is dan Hallo standaard doel van 0% slecht (*MaxPercentUnhealthyServices*).</span><span class="sxs-lookup"><span data-stu-id="36ac6-140">In this example, two out of four services are unhealthy, which is below hello default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span></span>

<span data-ttu-id="36ac6-141">Hallo upgrade is onderbroken op mislukken door te geven een **FailureAction** van handmatige wanneer upgrade vanaf Hallo.</span><span class="sxs-lookup"><span data-stu-id="36ac6-141">hello upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting hello upgrade.</span></span> <span data-ttu-id="36ac6-142">Deze modus kan wij tooinvestigate Hallo live systeem status Hallo is mislukt voordat u geen verdere actie.</span><span class="sxs-lookup"><span data-stu-id="36ac6-142">This mode allows us tooinvestigate hello live system in hello failed state before taking any further action.</span></span>

### <a name="recover-from-a-suspended-upgrade"></a><span data-ttu-id="36ac6-143">Herstellen van een onderbroken upgrade</span><span class="sxs-lookup"><span data-stu-id="36ac6-143">Recover from a suspended upgrade</span></span>
<span data-ttu-id="36ac6-144">Met terugdraaien **FailureAction**, er is geen herstel nodig omdat Hallo upgrade automatisch teruggedraaid in bij mislukken.</span><span class="sxs-lookup"><span data-stu-id="36ac6-144">With a rollback **FailureAction**, there is no recovery needed since hello upgrade automatically rolls back upon failing.</span></span> <span data-ttu-id="36ac6-145">Met een handmatige **FailureAction**, er zijn verschillende opties voor herstel:</span><span class="sxs-lookup"><span data-stu-id="36ac6-145">With a manual **FailureAction**, there are several recovery options:</span></span>

1.  <span data-ttu-id="36ac6-146">trigger terugdraaien</span><span class="sxs-lookup"><span data-stu-id="36ac6-146">trigger a rollback</span></span>
2. <span data-ttu-id="36ac6-147">Hallo overige Hallo upgrade handmatig doorlopen</span><span class="sxs-lookup"><span data-stu-id="36ac6-147">Proceed through hello remainder of hello upgrade manually</span></span>
3. <span data-ttu-id="36ac6-148">Hervatten Hallo bewaakt upgrade</span><span class="sxs-lookup"><span data-stu-id="36ac6-148">Resume hello monitored upgrade</span></span>

<span data-ttu-id="36ac6-149">Hallo **Start ServiceFabricApplicationRollback** opdracht kan worden gebruikt op een tijd toostart toepassing hello terugdraaien.</span><span class="sxs-lookup"><span data-stu-id="36ac6-149">hello **Start-ServiceFabricApplicationRollback** command can be used at any time toostart rolling back hello application.</span></span> <span data-ttu-id="36ac6-150">Zodra het Hallo-opdracht geretourneerd met succes, wordt Hallo terugdraaien van de aanvraag is geregistreerd in Hallo systeem en start het kort nadien.</span><span class="sxs-lookup"><span data-stu-id="36ac6-150">Once hello command returns successfully, hello rollback request has been registered in hello system and starts shortly thereafter.</span></span>

<span data-ttu-id="36ac6-151">Hallo **hervatten ServiceFabricApplicationUpgrade** opdracht kan worden gebruikt tooproceed in Hallo rest Hallo handmatig, één upgradedomein tegelijk bijwerken.</span><span class="sxs-lookup"><span data-stu-id="36ac6-151">hello **Resume-ServiceFabricApplicationUpgrade** command can be used tooproceed through hello remainder of hello upgrade manually, one upgrade domain at a time.</span></span> <span data-ttu-id="36ac6-152">In deze modus worden alleen veiligheid controles uitgevoerd door Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="36ac6-152">In this mode, only safety checks are performed by hello system.</span></span> <span data-ttu-id="36ac6-153">Niet meer health controles worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="36ac6-153">No more health checks are performed.</span></span> <span data-ttu-id="36ac6-154">Met deze opdracht kan alleen worden gebruikt wanneer hello *UpgradeState* toont *RollingForwardPending*, wat betekent dat Hallo Huidig upgradedomein upgraden is voltooid maar hello naast een is niet gestart (in behandeling).</span><span class="sxs-lookup"><span data-stu-id="36ac6-154">This command can only be used when hello *UpgradeState* shows *RollingForwardPending*, which means that hello current upgrade domain has finished upgrading but hello next one has not started (pending).</span></span>

<span data-ttu-id="36ac6-155">Hallo **Update ServiceFabricApplicationUpgrade** opdracht kan worden gebruikt tooresume Hallo bewaakt upgrade met veiligheid en de gezondheid controles worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="36ac6-155">hello **Update-ServiceFabricApplicationUpgrade** command can be used tooresume hello monitored upgrade with both safety and health checks being performed.</span></span>

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

<span data-ttu-id="36ac6-156">Hallo upgrade blijft van Hallo upgradedomein waar deze het laatst werd onderbroken en gebruik Hallo dezelfde parameters en statusbeleid als vóór upgrade.</span><span class="sxs-lookup"><span data-stu-id="36ac6-156">hello upgrade continues from hello upgrade domain where it was last suspended and use hello same upgrade parameters and health policies as before.</span></span> <span data-ttu-id="36ac6-157">Indien nodig, kan een van de parameters voor het bijwerken van Hallo en statusbeleid wordt weergegeven in de voorgaande uitvoer Hallo worden gewijzigd in Hallo dezelfde opdracht als Hallo upgrade wordt hervat.</span><span class="sxs-lookup"><span data-stu-id="36ac6-157">If needed, any of hello upgrade parameters and health policies shown in hello preceding output can be changed in hello same command when hello upgrade resumes.</span></span> <span data-ttu-id="36ac6-158">Hallo-upgrade is in dit voorbeeld hervat in de bewaakte modus Hallo parameters en Hallo statusbeleid ongewijzigd.</span><span class="sxs-lookup"><span data-stu-id="36ac6-158">In this example, hello upgrade was resumed in Monitored mode, with hello parameters and hello health policies unchanged.</span></span>

## <a name="further-troubleshooting"></a><span data-ttu-id="36ac6-159">Meer informatie over</span><span class="sxs-lookup"><span data-stu-id="36ac6-159">Further troubleshooting</span></span>
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a><span data-ttu-id="36ac6-160">Service Fabric volgt is niet opgegeven Hallo statusbeleid</span><span class="sxs-lookup"><span data-stu-id="36ac6-160">Service Fabric is not following hello specified health policies</span></span>
<span data-ttu-id="36ac6-161">Mogelijke oorzaak 1:</span><span class="sxs-lookup"><span data-stu-id="36ac6-161">Possible Cause 1:</span></span>

<span data-ttu-id="36ac6-162">Service Fabric kan alle percentages in het werkelijke aantal entiteiten (bijvoorbeeld, replica's, partities en services) voor de statusevaluatie en altijd Rondt naar boven toowhole entiteiten.</span><span class="sxs-lookup"><span data-stu-id="36ac6-162">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up toowhole entities.</span></span> <span data-ttu-id="36ac6-163">Bijvoorbeeld, als hello maximale *MaxPercentUnhealthyReplicasPerPartition* 21% is en er zijn vijf replica's, en vervolgens de Service Fabric kunt up tootwo slecht replica's (dat wil zeggen,`Math.Ceiling (5*0.21)`).</span><span class="sxs-lookup"><span data-stu-id="36ac6-163">For example, if hello maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up tootwo unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span></span> <span data-ttu-id="36ac6-164">Statusbeleid moeten dus dienovereenkomstig worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="36ac6-164">Thus, health policies should be set accordingly.</span></span>

<span data-ttu-id="36ac6-165">Mogelijke oorzaak 2:</span><span class="sxs-lookup"><span data-stu-id="36ac6-165">Possible Cause 2:</span></span>

<span data-ttu-id="36ac6-166">Statusbeleid worden opgegeven in termen van percentage van totale services en niet specifiek service-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="36ac6-166">Health policies are specified in terms of percentages of total services and not specific service instances.</span></span> <span data-ttu-id="36ac6-167">Bijvoorbeeld, voordat u een upgrade uitvoert als een toepassing vier heeft service-exemplaren A, B, C en D, waarbij D service niet in orde is, maar met weinig invloed toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="36ac6-167">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact toohello application.</span></span> <span data-ttu-id="36ac6-168">We willen tooignore Hallo slecht service D bekend tijdens de upgrade en stel Hallo parameter *MaxPercentUnhealthyServices* toobe 25%, ervan uitgaande dat alleen A, B en C moet toobe in orde.</span><span class="sxs-lookup"><span data-stu-id="36ac6-168">We want tooignore hello known unhealthy service D during upgrade and set hello parameter *MaxPercentUnhealthyServices* toobe 25%, assuming only A, B, and C need toobe healthy.</span></span>

<span data-ttu-id="36ac6-169">Tijdens de upgrade Hallo kan D worden echter in orde terwijl C slecht.</span><span class="sxs-lookup"><span data-stu-id="36ac6-169">However, during hello upgrade, D may become healthy while C becomes unhealthy.</span></span> <span data-ttu-id="36ac6-170">Hallo upgrade zou desondanks slagen omdat alleen 25% van het Hallo-services slecht zijn.</span><span class="sxs-lookup"><span data-stu-id="36ac6-170">hello upgrade would still succeed because only 25% of hello services are unhealthy.</span></span> <span data-ttu-id="36ac6-171">Echter kan resulteren in onverwachte fouten vanwege tooC wordt onverwacht slecht in plaats van D. In dit geval D gemodelleerd als een andere servicetype uit A, B en c Omdat statusbeleid per servicetype zijn opgegeven, kunnen ander slecht percentage drempelwaarden toegepaste toodifferent services zijn.</span><span class="sxs-lookup"><span data-stu-id="36ac6-171">However, it might result in unanticipated errors due tooC being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied toodifferent services.</span></span> 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a><span data-ttu-id="36ac6-172">Ik een statusbeleid voor upgrade van de toepassing niet is opgegeven, maar Hallo upgrade nog steeds niet voor bepaalde time-outs die ik nooit opgegeven</span><span class="sxs-lookup"><span data-stu-id="36ac6-172">I did not specify a health policy for application upgrade, but hello upgrade still fails for some time-outs that I never specified</span></span>
<span data-ttu-id="36ac6-173">Wanneer u statusbeleid zijn niet toohello upgradeaanvraag opgeeft, worden ze overgenomen van Hallo *ApplicationManifest.xml* van de huidige versie van toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="36ac6-173">When health policies aren't provided toohello upgrade request, they are taken from hello *ApplicationManifest.xml* of hello current application version.</span></span> <span data-ttu-id="36ac6-174">Bijvoorbeeld, als u een X van de toepassing van versie 1.0 tooversion 2.0 upgrade uitvoert, statusbeleid voor toepassing opgegeven voor versie 1.0 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="36ac6-174">For example, if you're upgrading Application X from version 1.0 tooversion 2.0, application health policies specified for in version 1.0 are used.</span></span> <span data-ttu-id="36ac6-175">Als een andere statusbeleid moet worden gebruikt voor Hallo upgrade, moet Hallo beleid toobe opgegeven als onderdeel van Hallo toepassing upgrade API-aanroep.</span><span class="sxs-lookup"><span data-stu-id="36ac6-175">If a different health policy should be used for hello upgrade, then hello policy needs toobe specified as part of hello application upgrade API call.</span></span> <span data-ttu-id="36ac6-176">Hallo-beleidsregels die zijn opgegeven als deel van Hallo API-aanroep zijn alleen van toepassing tijdens de upgrade Hallo.</span><span class="sxs-lookup"><span data-stu-id="36ac6-176">hello policies specified as part of hello API call only apply during hello upgrade.</span></span> <span data-ttu-id="36ac6-177">Zodra het Hallo-upgrade is voltooid, Hallo beleid moet worden opgegeven in Hallo *ApplicationManifest.xml* worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="36ac6-177">Once hello upgrade is complete, hello policies specified in hello *ApplicationManifest.xml* are used.</span></span>

### <a name="incorrect-time-outs-are-specified"></a><span data-ttu-id="36ac6-178">Onjuiste time-outs zijn opgegeven</span><span class="sxs-lookup"><span data-stu-id="36ac6-178">Incorrect time-outs are specified</span></span>
<span data-ttu-id="36ac6-179">U zich mogelijk afgevraagd over wat er gebeurt wanneer time-outs inconsistent worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="36ac6-179">You may have wondered about what happens when time-outs are set inconsistently.</span></span> <span data-ttu-id="36ac6-180">Bijvoorbeeld, u wellicht een *UpgradeTimeout* lager is dan Hallo *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="36ac6-180">For example, you may have an *UpgradeTimeout* that's less than hello *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="36ac6-181">Hallo-antwoord is dat er een fout is geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="36ac6-181">hello answer is that an error is returned.</span></span> <span data-ttu-id="36ac6-182">Fouten worden geretourneerd als hello *UpgradeDomainTimeout* kleiner is dan de som van Hallo *HealthCheckWaitDuration* en *HealthCheckRetryTimeout*, of als  *UpgradeDomainTimeout* kleiner is dan de som van Hallo *HealthCheckWaitDuration* en *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="36ac6-182">Errors are returned if hello *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span></span>

### <a name="my-upgrades-are-taking-too-long"></a><span data-ttu-id="36ac6-183">Mijn upgrades duurt te lang</span><span class="sxs-lookup"><span data-stu-id="36ac6-183">My upgrades are taking too long</span></span>
<span data-ttu-id="36ac6-184">Hallo-tijd voor een upgrade toocomplete, is afhankelijk van statuscontroles Hallo en time-outs opgegeven.</span><span class="sxs-lookup"><span data-stu-id="36ac6-184">hello time for an upgrade toocomplete depends on hello health checks and time-outs specified.</span></span> <span data-ttu-id="36ac6-185">Afhankelijk van hoe lang het duurt toocopy, implementeren en regulering toepassing hello statuscontroles en time-outs.</span><span class="sxs-lookup"><span data-stu-id="36ac6-185">Health checks and time-outs depend on how long it takes toocopy, deploy, and stabilize hello application.</span></span> <span data-ttu-id="36ac6-186">Wordt te agressief met time-outs kan het zijn dat meer mislukte upgrades, zodat u het beste eerst conservatieve met langer time-outs.</span><span class="sxs-lookup"><span data-stu-id="36ac6-186">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span></span>

<span data-ttu-id="36ac6-187">Dit is een snelle refresher op de wisselwerking tussen Hallo time-outs met Hallo upgrade tijden:</span><span class="sxs-lookup"><span data-stu-id="36ac6-187">Here's a quick refresher on how hello time-outs interact with hello upgrade times:</span></span>

<span data-ttu-id="36ac6-188">Voert een upgrade voor een upgradedomein kan niet worden voltooid sneller dan *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="36ac6-188">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span></span>

<span data-ttu-id="36ac6-189">Upgrade mislukt is niet mogelijk sneller dan *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span><span class="sxs-lookup"><span data-stu-id="36ac6-189">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span></span>

<span data-ttu-id="36ac6-190">Hallo tijd voor de upgrade voor een upgradedomein, wordt beperkt door *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="36ac6-190">hello upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span></span>  <span data-ttu-id="36ac6-191">Als *HealthCheckRetryTimeout* en *HealthCheckStableDuration* zijn beide niet gelijk is aan nul en Hallo status van de toepassing hello houdt heen en weer schakelen en vervolgens de upgrade Hallo uiteindelijk een time-out optreedt op  *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="36ac6-191">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and hello health of hello application keeps switching back and forth, then hello upgrade eventually times out on *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="36ac6-192">*UpgradeDomainTimeout* begint tellen omlaag eenmaal Hallo upgrade voor de huidige upgradedomein Hallo begint.</span><span class="sxs-lookup"><span data-stu-id="36ac6-192">*UpgradeDomainTimeout* starts counting down once hello upgrade for hello current upgrade domain begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36ac6-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="36ac6-193">Next steps</span></span>
<span data-ttu-id="36ac6-194">[Een upgrade van uw toepassing met behulp van Visual Studio](service-fabric-application-upgrade-tutorial.md) begeleidt u bij een upgrade van de toepassing met Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="36ac6-194">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="36ac6-195">[Een upgrade van uw toepassing met behulp van Powershell](service-fabric-application-upgrade-tutorial-powershell.md) begeleidt u bij een upgrade van de toepassing met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36ac6-195">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="36ac6-196">Bepalen hoe uw toepassing wordt bijgewerkt met behulp van [Parameters Upgrade](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="36ac6-196">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="36ac6-197">Uw toepassingsupgrades compatibel maken door leren hoe toouse [serialisatie van gegevens](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="36ac6-197">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="36ac6-198">Meer informatie over hoe toouse geavanceerde functies tijdens het bijwerken van uw toepassing door ernaar te verwijzen[geavanceerde onderwerpen](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="36ac6-198">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>

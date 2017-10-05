---
title: Het oplossen van problemen toepassingsupgrades | Microsoft Docs
description: In dit artikel bevat enkele veelvoorkomende problemen rond een upgrade van een Service Fabric-toepassing en hoe u deze kunt oplossen.
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
ms.openlocfilehash: f7f6bc0c29e2b43fbc8e451c5a4a50110b78349e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-application-upgrades"></a><span data-ttu-id="a3179-103">Problemen met toepassingsupgrades oplossen</span><span class="sxs-lookup"><span data-stu-id="a3179-103">Troubleshoot application upgrades</span></span>
<span data-ttu-id="a3179-104">In dit artikel bevat informatie over enkele van de algemene problemen rond een upgrade van een Azure Service Fabric-toepassing en hoe u deze kunt oplossen.</span><span class="sxs-lookup"><span data-stu-id="a3179-104">This article covers some of the common issues around upgrading an Azure Service Fabric application and how to resolve them.</span></span>

## <a name="troubleshoot-a-failed-application-upgrade"></a><span data-ttu-id="a3179-105">Een upgrade van de mislukte toepassing oplossen</span><span class="sxs-lookup"><span data-stu-id="a3179-105">Troubleshoot a failed application upgrade</span></span>
<span data-ttu-id="a3179-106">Wanneer een upgrade mislukt, de uitvoer van de **Get-ServiceFabricApplicationUpgrade** -opdracht bevat aanvullende informatie voor foutopsporing van de fout.</span><span class="sxs-lookup"><span data-stu-id="a3179-106">When an upgrade fails, the output of the **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging the failure.</span></span>  <span data-ttu-id="a3179-107">De volgende lijst geeft aan hoe de aanvullende informatie kan worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="a3179-107">The following list specifies how the additional information can be used:</span></span>

1. <span data-ttu-id="a3179-108">Identificeer het type is mislukt.</span><span class="sxs-lookup"><span data-stu-id="a3179-108">Identify the failure type.</span></span>
2. <span data-ttu-id="a3179-109">Identificeer de reden is mislukt.</span><span class="sxs-lookup"><span data-stu-id="a3179-109">Identify the failure reason.</span></span>
3. <span data-ttu-id="a3179-110">Een of meer onderdelen mislukken voor verder onderzoek isoleren.</span><span class="sxs-lookup"><span data-stu-id="a3179-110">Isolate one or more failing components for further investigation.</span></span>

<span data-ttu-id="a3179-111">Deze informatie is beschikbaar wanneer het Service Fabric de fout ongeacht of detecteert de **FailureAction** is terugdraait of onderbreken van de upgrade.</span><span class="sxs-lookup"><span data-stu-id="a3179-111">This information is available when Service Fabric detects the failure regardless of whether the **FailureAction** is to roll back or suspend the upgrade.</span></span>

### <a name="identify-the-failure-type"></a><span data-ttu-id="a3179-112">Identificatie van het fouttype</span><span class="sxs-lookup"><span data-stu-id="a3179-112">Identify the failure type</span></span>
<span data-ttu-id="a3179-113">In de uitvoer van **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identificeert de tijdstempel (in UTC-Notatie) waarmee een upgrade mislukt is gedetecteerd door de Service Fabric en  **FailureAction** is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="a3179-113">In the output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies the timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span></span> <span data-ttu-id="a3179-114">**FailureReason** identificeert een van drie op hoog niveau mogelijke oorzaken van de fout:</span><span class="sxs-lookup"><span data-stu-id="a3179-114">**FailureReason** identifies one of three potential high-level causes of the failure:</span></span>

1. <span data-ttu-id="a3179-115">UpgradeDomainTimeout - geeft aan dat een bepaald domein upgrade duurt te lang om te voltooien en **UpgradeDomainTimeout** verlopen.</span><span class="sxs-lookup"><span data-stu-id="a3179-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long to complete and **UpgradeDomainTimeout** expired.</span></span>
2. <span data-ttu-id="a3179-116">OverallUpgradeTimeout - geeft aan dat de algehele upgrade duurt te lang om te voltooien en **UpgradeTimeout** verlopen.</span><span class="sxs-lookup"><span data-stu-id="a3179-116">OverallUpgradeTimeout - Indicates that the overall upgrade took too long to complete and **UpgradeTimeout** expired.</span></span>
3. <span data-ttu-id="a3179-117">Statuscontrole - geeft aan dat na de upgrade van een updatedomein de toepassing nog steeds niet in orde volgens de opgegeven statusbeleid en **HealthCheckRetryTimeout** verlopen.</span><span class="sxs-lookup"><span data-stu-id="a3179-117">HealthCheck - Indicates that after upgrading an update domain, the application remained unhealthy according to the specified health policies and **HealthCheckRetryTimeout** expired.</span></span>

<span data-ttu-id="a3179-118">Deze vermeldingen alleen weergegeven in de uitvoer wanneer de upgrade mislukt en wordt gestart door terug te draaien.</span><span class="sxs-lookup"><span data-stu-id="a3179-118">These entries only show up in the output when the upgrade fails and starts rolling back.</span></span> <span data-ttu-id="a3179-119">Meer informatie wordt weergegeven, afhankelijk van het type van de fout.</span><span class="sxs-lookup"><span data-stu-id="a3179-119">Further information is displayed depending on the type of the failure.</span></span>

### <a name="investigate-upgrade-timeouts"></a><span data-ttu-id="a3179-120">Upgrade-outs onderzoeken</span><span class="sxs-lookup"><span data-stu-id="a3179-120">Investigate upgrade timeouts</span></span>
<span data-ttu-id="a3179-121">Time-out fouten meestal door problemen met de servicebeschikbaarheid veroorzaakt worden bijwerken.</span><span class="sxs-lookup"><span data-stu-id="a3179-121">Upgrade timeout failures are most commonly caused by service availability issues.</span></span> <span data-ttu-id="a3179-122">De uitvoer hieronder is Typerend voor upgrades waarbij service replica's of exemplaren niet worden gestart in de nieuwe codeversie.</span><span class="sxs-lookup"><span data-stu-id="a3179-122">The output following this paragraph is typical of upgrades where service replicas or instances fail to start in the new code version.</span></span> <span data-ttu-id="a3179-123">De **UpgradeDomainProgressAtFailure** veld een momentopname van in behandeling upgrade werk op het moment van de fout wordt vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="a3179-123">The **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at the time of failure.</span></span>

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

<span data-ttu-id="a3179-124">In dit voorbeeld wordt de upgrade is mislukt op upgradedomein *MYUD1* en twee partities (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* en *4b43f4d8-b26b-424e-9307-7a7a62e79750*) zijn vastgelopen.</span><span class="sxs-lookup"><span data-stu-id="a3179-124">In this example, the upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span></span> <span data-ttu-id="a3179-125">De partities zijn vastgelopen omdat de runtime kan plaatsen van de primaire replica's (*WaitForPrimaryPlacement*) op de doelknooppunten *knooppunt1* en *Knooppunt4*.</span><span class="sxs-lookup"><span data-stu-id="a3179-125">The partitions were stuck because the runtime was unable to place primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span></span>

<span data-ttu-id="a3179-126">De **Get-ServiceFabricNode** opdracht kan worden gebruikt om te controleren of deze twee knooppunten in het upgradedomein *MYUD1*.</span><span class="sxs-lookup"><span data-stu-id="a3179-126">The **Get-ServiceFabricNode** command can be used to verify that these two nodes are in upgrade domain *MYUD1*.</span></span> <span data-ttu-id="a3179-127">De *UpgradePhase* zegt *PostUpgradeSafetyCheck*, wat betekent dat deze controles veiligheid plaatsvinden nadat alle knooppunten in het upgradedomein bijgewerkt hebt.</span><span class="sxs-lookup"><span data-stu-id="a3179-127">The *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in the upgrade domain have finished upgrading.</span></span> <span data-ttu-id="a3179-128">Deze informatie verwijst naar een mogelijk probleem met de nieuwe versie van de toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="a3179-128">All this information points to a potential issue with the new version of the application code.</span></span> <span data-ttu-id="a3179-129">De meest voorkomende problemen zijn fouten in de open of promotie tot primaire codepaden-service.</span><span class="sxs-lookup"><span data-stu-id="a3179-129">The most common issues are service errors in the open or promotion to primary code paths.</span></span>

<span data-ttu-id="a3179-130">Een *UpgradePhase* van *PreUpgradeSafetyCheck* betekent dat er zijn problemen met het voorbereiden van het upgradedomein voordat deze werd uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a3179-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing the upgrade domain before it was performed.</span></span> <span data-ttu-id="a3179-131">De meest voorkomende problemen zijn in dit geval fouten in de sluiten of degradatie uit naar de primaire code van de service.</span><span class="sxs-lookup"><span data-stu-id="a3179-131">The most common issues in this case are service errors in the close or demotion from primary code paths.</span></span>

<span data-ttu-id="a3179-132">De huidige **UpgradeState** is *RollingBackCompleted*, zodat de oorspronkelijke upgrade moet worden uitgevoerd met een rollback **FailureAction**, die automatisch samengevouwen back-de upgrade mislukt.</span><span class="sxs-lookup"><span data-stu-id="a3179-132">The current **UpgradeState** is *RollingBackCompleted*, so the original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back the upgrade upon failure.</span></span> <span data-ttu-id="a3179-133">Als de oorspronkelijke upgrade is uitgevoerd met een handmatige **FailureAction**, en vervolgens de upgrade wordt in plaats daarvan worden in een onderbroken staat om toe te staan live foutopsporing van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a3179-133">If the original upgrade was performed with a manual **FailureAction**, then the upgrade would instead be in a suspended state to allow live debugging of the application.</span></span>

### <a name="investigate-health-check-failures"></a><span data-ttu-id="a3179-134">Health selectievakje fouten onderzoeken</span><span class="sxs-lookup"><span data-stu-id="a3179-134">Investigate health check failures</span></span>
<span data-ttu-id="a3179-135">Health selectievakje fouten kunnen worden geactiveerd door verschillende problemen die kunnen ontstaan nadat alle knooppunten in een upgradedomein upgraden en alle controles van de veiligheid wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="a3179-135">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span></span> <span data-ttu-id="a3179-136">De uitvoer hieronder is standaard een upgrade mislukt vanwege een mislukte statuscontroles.</span><span class="sxs-lookup"><span data-stu-id="a3179-136">The output following this paragraph is typical of an upgrade failure due to failed health checks.</span></span> <span data-ttu-id="a3179-137">De **UnhealthyEvaluations** veld bevat een momentopname van statuscontroles die niet op het moment van de upgrade volgens de opgegeven [statusbeleid](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a3179-137">The **UnhealthyEvaluations** field captures a snapshot of health checks that failed at the time of the upgrade according to the specified [health policy](service-fabric-health-introduction.md).</span></span>

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

<span data-ttu-id="a3179-138">Een goed begrip van de Service Fabric-statusmodel health selectievakje fouten onderzoeken eerst worden vereist.</span><span class="sxs-lookup"><span data-stu-id="a3179-138">Investigating health check failures first requires an understanding of the Service Fabric health model.</span></span> <span data-ttu-id="a3179-139">Maar zelfs zonder een diepgaand inzicht, ziet u twee services zijn slecht: *fabric: / DemoApp/Svc3* en *fabric: / DemoApp/Svc2*, samen met de foutenrapporten health ('InjectedFault' in dit geval).</span><span class="sxs-lookup"><span data-stu-id="a3179-139">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with the error health reports ("InjectedFault" in this case).</span></span> <span data-ttu-id="a3179-140">In dit voorbeeld twee vier services zijn beschadigd, wat minder is dan het doel van de standaard van 0% slecht (*MaxPercentUnhealthyServices*).</span><span class="sxs-lookup"><span data-stu-id="a3179-140">In this example, two out of four services are unhealthy, which is below the default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span></span>

<span data-ttu-id="a3179-141">De upgrade van het mislukken is onderbroken door te geven een **FailureAction** handmatig bij het starten van de upgrade.</span><span class="sxs-lookup"><span data-stu-id="a3179-141">The upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting the upgrade.</span></span> <span data-ttu-id="a3179-142">Deze modus, kunnen wij voor het onderzoeken van het live systeem in de mislukte status alvorens verdere actie te ondernemen.</span><span class="sxs-lookup"><span data-stu-id="a3179-142">This mode allows us to investigate the live system in the failed state before taking any further action.</span></span>

### <a name="recover-from-a-suspended-upgrade"></a><span data-ttu-id="a3179-143">Herstellen van een onderbroken upgrade</span><span class="sxs-lookup"><span data-stu-id="a3179-143">Recover from a suspended upgrade</span></span>
<span data-ttu-id="a3179-144">Met terugdraaien **FailureAction**, er is geen herstel nodig omdat de upgrade automatisch teruggedraaid in bij mislukken.</span><span class="sxs-lookup"><span data-stu-id="a3179-144">With a rollback **FailureAction**, there is no recovery needed since the upgrade automatically rolls back upon failing.</span></span> <span data-ttu-id="a3179-145">Met een handmatige **FailureAction**, er zijn verschillende opties voor herstel:</span><span class="sxs-lookup"><span data-stu-id="a3179-145">With a manual **FailureAction**, there are several recovery options:</span></span>

1.  <span data-ttu-id="a3179-146">trigger terugdraaien</span><span class="sxs-lookup"><span data-stu-id="a3179-146">trigger a rollback</span></span>
2. <span data-ttu-id="a3179-147">Volg de stappen in de rest van de upgrade handmatig</span><span class="sxs-lookup"><span data-stu-id="a3179-147">Proceed through the remainder of the upgrade manually</span></span>
3. <span data-ttu-id="a3179-148">De bewaakte upgrade hervatten</span><span class="sxs-lookup"><span data-stu-id="a3179-148">Resume the monitored upgrade</span></span>

<span data-ttu-id="a3179-149">De **Start ServiceFabricApplicationRollback** opdracht kan worden gebruikt op elk gewenst moment worden gestart met het terugdraaien van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a3179-149">The **Start-ServiceFabricApplicationRollback** command can be used at any time to start rolling back the application.</span></span> <span data-ttu-id="a3179-150">Zodra de opdracht is retourneert, wordt de rollback-aanvraag is geregistreerd in het systeem en kort nadien begint.</span><span class="sxs-lookup"><span data-stu-id="a3179-150">Once the command returns successfully, the rollback request has been registered in the system and starts shortly thereafter.</span></span>

<span data-ttu-id="a3179-151">De **hervatten ServiceFabricApplicationUpgrade** opdracht kan worden gebruikt om door te gaan in de rest van de upgrade handmatig één upgradedomein tegelijk.</span><span class="sxs-lookup"><span data-stu-id="a3179-151">The **Resume-ServiceFabricApplicationUpgrade** command can be used to proceed through the remainder of the upgrade manually, one upgrade domain at a time.</span></span> <span data-ttu-id="a3179-152">In deze modus worden alleen veiligheid controles uitgevoerd door het systeem.</span><span class="sxs-lookup"><span data-stu-id="a3179-152">In this mode, only safety checks are performed by the system.</span></span> <span data-ttu-id="a3179-153">Niet meer health controles worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a3179-153">No more health checks are performed.</span></span> <span data-ttu-id="a3179-154">Met deze opdracht kan alleen worden gebruikt wanneer de *UpgradeState* toont *RollingForwardPending*, wat betekent dat het upgraden van het huidige upgradedomein is voltooid, maar de volgende gateway niet gestart is (in behandeling).</span><span class="sxs-lookup"><span data-stu-id="a3179-154">This command can only be used when the *UpgradeState* shows *RollingForwardPending*, which means that the current upgrade domain has finished upgrading but the next one has not started (pending).</span></span>

<span data-ttu-id="a3179-155">De **Update ServiceFabricApplicationUpgrade** opdracht kan worden gebruikt voor het hervatten van de bewaakte upgrade met beide veiligheid en health controleert wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a3179-155">The **Update-ServiceFabricApplicationUpgrade** command can be used to resume the monitored upgrade with both safety and health checks being performed.</span></span>

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

<span data-ttu-id="a3179-156">De upgrade blijft van het upgradedomein waar deze het laatst werd onderbroken en gebruik dezelfde parameters en statusbeleid als vóór upgrade.</span><span class="sxs-lookup"><span data-stu-id="a3179-156">The upgrade continues from the upgrade domain where it was last suspended and use the same upgrade parameters and health policies as before.</span></span> <span data-ttu-id="a3179-157">Indien nodig, kan een van de parameters voor het bijwerken en statusbeleid wordt weergegeven in de voorgaande uitvoer worden gewijzigd in dezelfde opdracht als de upgrade wordt hervat.</span><span class="sxs-lookup"><span data-stu-id="a3179-157">If needed, any of the upgrade parameters and health policies shown in the preceding output can be changed in the same command when the upgrade resumes.</span></span> <span data-ttu-id="a3179-158">In dit voorbeeld is de upgrade in de bewaakte modus met de parameters en het statusbeleid ongewijzigd hervat.</span><span class="sxs-lookup"><span data-stu-id="a3179-158">In this example, the upgrade was resumed in Monitored mode, with the parameters and the health policies unchanged.</span></span>

## <a name="further-troubleshooting"></a><span data-ttu-id="a3179-159">Meer informatie over</span><span class="sxs-lookup"><span data-stu-id="a3179-159">Further troubleshooting</span></span>
### <a name="service-fabric-is-not-following-the-specified-health-policies"></a><span data-ttu-id="a3179-160">Service Fabric volgt niet het opgegeven statusbeleid</span><span class="sxs-lookup"><span data-stu-id="a3179-160">Service Fabric is not following the specified health policies</span></span>
<span data-ttu-id="a3179-161">Mogelijke oorzaak 1:</span><span class="sxs-lookup"><span data-stu-id="a3179-161">Possible Cause 1:</span></span>

<span data-ttu-id="a3179-162">Service Fabric alle percentages vertaalt in het werkelijke aantal entiteiten (bijvoorbeeld, replica's, partities en services) voor de statusevaluatie en altijd rondt af naar boven op hele entiteiten.</span><span class="sxs-lookup"><span data-stu-id="a3179-162">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up to whole entities.</span></span> <span data-ttu-id="a3179-163">Bijvoorbeeld, als de maximale *MaxPercentUnhealthyReplicasPerPartition* 21% is en er zijn vijf replica's, en vervolgens de Service Fabric kan maximaal twee slecht replica's (dat wil zeggen,`Math.Ceiling (5*0.21)`).</span><span class="sxs-lookup"><span data-stu-id="a3179-163">For example, if the maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up to two unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span></span> <span data-ttu-id="a3179-164">Statusbeleid moeten dus dienovereenkomstig worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a3179-164">Thus, health policies should be set accordingly.</span></span>

<span data-ttu-id="a3179-165">Mogelijke oorzaak 2:</span><span class="sxs-lookup"><span data-stu-id="a3179-165">Possible Cause 2:</span></span>

<span data-ttu-id="a3179-166">Statusbeleid worden opgegeven in termen van percentage van totale services en niet specifiek service-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="a3179-166">Health policies are specified in terms of percentages of total services and not specific service instances.</span></span> <span data-ttu-id="a3179-167">Bijvoorbeeld, voordat u een upgrade uitvoert als een toepassing vier heeft service-exemplaren A, B, C en D, waarbij D service niet in orde is, maar weinig invloed hebben op de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a3179-167">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact to the application.</span></span> <span data-ttu-id="a3179-168">We willen het negeren van de bekende slecht service D tijdens de upgrade en stel de parameter *MaxPercentUnhealthyServices* 25%, ervan uitgaande dat alleen A, B en C moet worden in orde.</span><span class="sxs-lookup"><span data-stu-id="a3179-168">We want to ignore the known unhealthy service D during upgrade and set the parameter *MaxPercentUnhealthyServices* to be 25%, assuming only A, B, and C need to be healthy.</span></span>

<span data-ttu-id="a3179-169">Tijdens de upgrade kan D worden echter in orde terwijl C slecht.</span><span class="sxs-lookup"><span data-stu-id="a3179-169">However, during the upgrade, D may become healthy while C becomes unhealthy.</span></span> <span data-ttu-id="a3179-170">De upgrade zou desondanks slagen omdat alleen 25% van de services slecht zijn.</span><span class="sxs-lookup"><span data-stu-id="a3179-170">The upgrade would still succeed because only 25% of the services are unhealthy.</span></span> <span data-ttu-id="a3179-171">Het kan echter leiden tot onverwachte fouten als gevolg van C wordt onverwacht slecht in plaats van D. In dit geval D gemodelleerd als een andere servicetype uit A, B en c Omdat statusbeleid per servicetype zijn opgegeven, kan ander slecht percentage drempelwaarden kunnen worden toegepast met andere services.</span><span class="sxs-lookup"><span data-stu-id="a3179-171">However, it might result in unanticipated errors due to C being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied to different services.</span></span> 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-the-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a><span data-ttu-id="a3179-172">Ik een statusbeleid voor upgrade van de toepassing niet is opgegeven, maar nog steeds mislukt de upgrade voor een aantal time-outs die ik nooit opgegeven</span><span class="sxs-lookup"><span data-stu-id="a3179-172">I did not specify a health policy for application upgrade, but the upgrade still fails for some time-outs that I never specified</span></span>
<span data-ttu-id="a3179-173">Wanneer statusbeleid zijn niet opgegeven voor de update-aanvraag, ze van overgenomen worden de *ApplicationManifest.xml* van de huidige toepassingsversie.</span><span class="sxs-lookup"><span data-stu-id="a3179-173">When health policies aren't provided to the upgrade request, they are taken from the *ApplicationManifest.xml* of the current application version.</span></span> <span data-ttu-id="a3179-174">Bijvoorbeeld, als u een X van de toepassing van versie 1.0 naar versie 2.0, statusbeleid voor toepassing opgegeven upgrade uitvoert voor versie 1.0 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a3179-174">For example, if you're upgrading Application X from version 1.0 to version 2.0, application health policies specified for in version 1.0 are used.</span></span> <span data-ttu-id="a3179-175">Als een andere statusbeleid moet worden gebruikt voor de upgrade, klikt u vervolgens moet het beleid worden opgegeven als onderdeel van de toepassing upgrade API-aanroep.</span><span class="sxs-lookup"><span data-stu-id="a3179-175">If a different health policy should be used for the upgrade, then the policy needs to be specified as part of the application upgrade API call.</span></span> <span data-ttu-id="a3179-176">Het beleid dat is opgegeven als onderdeel van de API-aanroep zijn alleen van toepassing tijdens de upgrade.</span><span class="sxs-lookup"><span data-stu-id="a3179-176">The policies specified as part of the API call only apply during the upgrade.</span></span> <span data-ttu-id="a3179-177">Zodra de upgrade voltooid is, het beleid moet worden opgegeven in de *ApplicationManifest.xml* worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a3179-177">Once the upgrade is complete, the policies specified in the *ApplicationManifest.xml* are used.</span></span>

### <a name="incorrect-time-outs-are-specified"></a><span data-ttu-id="a3179-178">Onjuiste time-outs zijn opgegeven</span><span class="sxs-lookup"><span data-stu-id="a3179-178">Incorrect time-outs are specified</span></span>
<span data-ttu-id="a3179-179">U zich mogelijk afgevraagd over wat er gebeurt wanneer time-outs inconsistent worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a3179-179">You may have wondered about what happens when time-outs are set inconsistently.</span></span> <span data-ttu-id="a3179-180">Bijvoorbeeld, u wellicht een *UpgradeTimeout* dat kleiner is dan het *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="a3179-180">For example, you may have an *UpgradeTimeout* that's less than the *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="a3179-181">Het antwoord is dat er een fout is geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="a3179-181">The answer is that an error is returned.</span></span> <span data-ttu-id="a3179-182">Fouten worden geretourneerd als de *UpgradeDomainTimeout* kleiner is dan de som van *HealthCheckWaitDuration* en *HealthCheckRetryTimeout*, of als  *UpgradeDomainTimeout* kleiner is dan de som van *HealthCheckWaitDuration* en *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="a3179-182">Errors are returned if the *UpgradeDomainTimeout* is less than the sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than the sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span></span>

### <a name="my-upgrades-are-taking-too-long"></a><span data-ttu-id="a3179-183">Mijn upgrades duurt te lang</span><span class="sxs-lookup"><span data-stu-id="a3179-183">My upgrades are taking too long</span></span>
<span data-ttu-id="a3179-184">De tijd voor een upgrade is voltooid, is afhankelijk van de statuscontroles en time-outs opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a3179-184">The time for an upgrade to complete depends on the health checks and time-outs specified.</span></span> <span data-ttu-id="a3179-185">Statuscontroles en time-outs afhankelijk van hoe lang het duurt om te kopiëren, implementeren en regulering van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a3179-185">Health checks and time-outs depend on how long it takes to copy, deploy, and stabilize the application.</span></span> <span data-ttu-id="a3179-186">Wordt te agressief met time-outs kan het zijn dat meer mislukte upgrades, zodat u het beste eerst conservatieve met langer time-outs.</span><span class="sxs-lookup"><span data-stu-id="a3179-186">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span></span>

<span data-ttu-id="a3179-187">Dit is een snelle refresher op hoe de time-outs met de upgrade tijden communiceren:</span><span class="sxs-lookup"><span data-stu-id="a3179-187">Here's a quick refresher on how the time-outs interact with the upgrade times:</span></span>

<span data-ttu-id="a3179-188">Voert een upgrade voor een upgradedomein kan niet worden voltooid sneller dan *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="a3179-188">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span></span>

<span data-ttu-id="a3179-189">Upgrade mislukt is niet mogelijk sneller dan *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span><span class="sxs-lookup"><span data-stu-id="a3179-189">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span></span>

<span data-ttu-id="a3179-190">De tijd voor de upgrade voor een upgradedomein wordt beperkt door *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="a3179-190">The upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span></span>  <span data-ttu-id="a3179-191">Als *HealthCheckRetryTimeout* en *HealthCheckStableDuration* zijn beide niet gelijk is aan nul en de status van de toepassing blijft heen en weer schakelen en vervolgens de upgrade uiteindelijk een optreedt op time-out*UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="a3179-191">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and the health of the application keeps switching back and forth, then the upgrade eventually times out on *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="a3179-192">*UpgradeDomainTimeout* begint te tellen omlaag eenmaal de upgrade voor het huidige upgradedomein begint.</span><span class="sxs-lookup"><span data-stu-id="a3179-192">*UpgradeDomainTimeout* starts counting down once the upgrade for the current upgrade domain begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3179-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a3179-193">Next steps</span></span>
<span data-ttu-id="a3179-194">[Een upgrade van uw toepassing met behulp van Visual Studio](service-fabric-application-upgrade-tutorial.md) begeleidt u bij een upgrade van de toepassing met Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3179-194">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="a3179-195">[Een upgrade van uw toepassing met behulp van Powershell](service-fabric-application-upgrade-tutorial-powershell.md) begeleidt u bij een upgrade van de toepassing met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3179-195">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="a3179-196">Bepalen hoe uw toepassing wordt bijgewerkt met behulp van [Parameters Upgrade](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="a3179-196">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="a3179-197">Uw toepassingsupgrades compatibel maken door te leren hoe u [serialisatie van gegevens](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="a3179-197">Make your application upgrades compatible by learning how to use [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="a3179-198">Informatie over het gebruik van geavanceerde functionaliteit tijdens het bijwerken van uw toepassing door te verwijzen naar [geavanceerde onderwerpen](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="a3179-198">Learn how to use advanced functionality while upgrading your application by referring to [Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>

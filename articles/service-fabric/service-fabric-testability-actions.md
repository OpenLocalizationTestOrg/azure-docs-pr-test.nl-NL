---
title: aaaSimulate fouten in Azure microservices | Microsoft Docs
description: In dit artikel wordt gesproken over Hallo testbaarheid acties gevonden in Microsoft Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a><span data-ttu-id="6f0c9-103">Testbaarheid acties</span><span class="sxs-lookup"><span data-stu-id="6f0c9-103">Testability actions</span></span>
<span data-ttu-id="6f0c9-104">In volgorde toosimulate een onbetrouwbare infrastructuur biedt Azure Service Fabric u Hallo-ontwikkelaars met manieren toosimulate verschillende echte fouten en statusovergangen.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-104">In order toosimulate an unreliable infrastructure, Azure Service Fabric provides you, hello developer, with ways toosimulate various real-world failures and state transitions.</span></span> <span data-ttu-id="6f0c9-105">Deze zijn beschikbaar als testbaarheid acties.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-105">These are exposed as testability actions.</span></span> <span data-ttu-id="6f0c9-106">Hallo acties zijn Hallo op laag niveau API's die ertoe leiden dat een specifieke fout injectie, statusovergang of validatie.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-106">hello actions are hello low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="6f0c9-107">U kunt uitgebreide Testscenario's voor uw services schrijven door een combinatie van deze acties.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="6f0c9-108">Service Fabric bevat dat enkele algemene scenario's voor test bestaan uit deze acties.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="6f0c9-109">Het is raadzaam dat u gebruikmaken van deze ingebouwde scenario's, zorgvuldig worden gekozen tootest algemene statusovergangen en mislukte aanvragen.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen tootest common state transitions and failure cases.</span></span> <span data-ttu-id="6f0c9-110">Acties kunnen echter aangepaste Testscenario's gebruikte toocreate zijn als u wilt dat tooadd dekking voor scenario's die zijn niet wordt gedekt door ingebouwde Hallo-scenario's nog of die aangepaste speciaal afgestemd op uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-110">However, actions can be used toocreate custom test scenarios when you want tooadd coverage for scenarios that are not covered by hello built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="6f0c9-111">C#-implementaties van Hallo acties zijn gevonden in Hallo System.Fabric.dll assembly.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-111">C# implementations of hello actions are found in hello System.Fabric.dll assembly.</span></span> <span data-ttu-id="6f0c9-112">Hallo System Fabric PowerShell-module is gevonden in Hallo Microsoft.ServiceFabric.Powershell.dll assembly.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-112">hello System Fabric PowerShell module is found in hello Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="6f0c9-113">Hallo ServiceFabric PowerShell-module is als onderdeel van de runtime-installatie geïnstalleerde tooallow voor eenvoudig te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-113">As part of runtime installation, hello ServiceFabric PowerShell module is installed tooallow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="6f0c9-114">Correcte versus geforceerde afsluiting veroorzaakt acties</span><span class="sxs-lookup"><span data-stu-id="6f0c9-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="6f0c9-115">Testbaarheid acties worden ingedeeld in twee belangrijke buckets:</span><span class="sxs-lookup"><span data-stu-id="6f0c9-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="6f0c9-116">Geforceerde afsluiting fouten: deze fouten simuleren fouten zoals machine opnieuw is opgestart en crashes verwerken.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="6f0c9-117">In dergelijke gevallen van fouten Hallo uitvoeringscontext van proces abrupt.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-117">In such cases of failures, hello execution context of process stops abruptly.</span></span> <span data-ttu-id="6f0c9-118">Dit betekent dat er geen opschoning van Hallo staat kunt uitvoeren voordat de toepassing hello opnieuw is gestart.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-118">This means no cleanup of hello state can run before hello application starts up again.</span></span>
* <span data-ttu-id="6f0c9-119">Correcte fouten: deze fouten simuleren correcte acties zoals replica wordt verplaatst en verwijdert geactiveerd door de taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="6f0c9-120">In dergelijke gevallen Hallo-service een melding van Hallo sluiten opgehaald en opschonen Hallo status voordat u afsluit.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-120">In such cases, hello service gets a notification of hello close and can clean up hello state before exiting.</span></span>

<span data-ttu-id="6f0c9-121">Hallo-service voor betere validatie van de kwaliteit, uitvoeren en zakelijke werkbelasting bij verschillende systemen op correct wijze en geforceerde afsluiting fouten veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-121">For better quality validation, run hello service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="6f0c9-122">Geforceerde afsluiting fouten oefenen scenario's waarbij Hallo-serviceproces in het midden van een werkstroom Hallo abrupt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-122">Ungraceful faults exercise scenarios where hello service process abruptly exits in hello middle of some workflow.</span></span> <span data-ttu-id="6f0c9-123">Deze tests Hallo herstelpad zodra de Hallo service replica is hersteld door de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-123">This tests  hello recovery path once hello service replica is restored by Service Fabric.</span></span> <span data-ttu-id="6f0c9-124">Dit helpt testen gegevensconsistentie en of de servicestatus Hallo correct wordt bijgehouden na fouten.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-124">This will help test data consistency and whether hello service state is maintained correctly after failures.</span></span> <span data-ttu-id="6f0c9-125">Hallo andere set van fouten (Hallo correcte fouten) testen dat Hallo-service juist wordt verplaatst op door de Service Fabric tooreplicas reageert.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-125">hello other set of failures (hello graceful failures) test that hello service correctly reacts tooreplicas being moved around by Service Fabric.</span></span> <span data-ttu-id="6f0c9-126">Dit webtests verwerking van de annulering op Hallo RunAsync-methode.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-126">This tests handling of cancellation in hello RunAsync method.</span></span> <span data-ttu-id="6f0c9-127">Hallo-service moet toocheck voor Hallo annulering token wordt instellen, de status goed opslaan en sluiten Hallo RunAsync-methode.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-127">hello service needs toocheck for hello cancellation token being set, correctly save its state, and exit hello RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="6f0c9-128">Lijst van acties testbaarheid</span><span class="sxs-lookup"><span data-stu-id="6f0c9-128">Testability actions list</span></span>
| <span data-ttu-id="6f0c9-129">Actie</span><span class="sxs-lookup"><span data-stu-id="6f0c9-129">Action</span></span> | <span data-ttu-id="6f0c9-130">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6f0c9-130">Description</span></span> | <span data-ttu-id="6f0c9-131">Beheerde API</span><span class="sxs-lookup"><span data-stu-id="6f0c9-131">Managed API</span></span> | <span data-ttu-id="6f0c9-132">PowerShell-cmdlet</span><span class="sxs-lookup"><span data-stu-id="6f0c9-132">PowerShell cmdlet</span></span> | <span data-ttu-id="6f0c9-133">Correcte/geforceerde afsluiting fouten</span><span class="sxs-lookup"><span data-stu-id="6f0c9-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="6f0c9-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="6f0c9-134">CleanTestState</span></span> |<span data-ttu-id="6f0c9-135">Verwijdert alle Hallo teststatus van Hallo-cluster in geval van een onjuist afsluiten van het stuurprogramma voor Hallo-test.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-135">Removes all hello test state from hello cluster in case of a bad shutdown of hello test driver.</span></span> |<span data-ttu-id="6f0c9-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="6f0c9-136">CleanTestStateAsync</span></span> |<span data-ttu-id="6f0c9-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="6f0c9-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="6f0c9-138">Niet van toepassing</span><span class="sxs-lookup"><span data-stu-id="6f0c9-138">Not applicable</span></span> |
| <span data-ttu-id="6f0c9-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="6f0c9-139">InvokeDataLoss</span></span> |<span data-ttu-id="6f0c9-140">Induceert verlies van gegevens in een service-partitie.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="6f0c9-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="6f0c9-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="6f0c9-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="6f0c9-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="6f0c9-143">Correcte</span><span class="sxs-lookup"><span data-stu-id="6f0c9-143">Graceful</span></span> |
| <span data-ttu-id="6f0c9-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="6f0c9-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="6f0c9-145">De partitie van een bepaalde stateful service plaatst in quorumverlies.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="6f0c9-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="6f0c9-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="6f0c9-147">Aanroepen ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="6f0c9-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="6f0c9-148">Correcte</span><span class="sxs-lookup"><span data-stu-id="6f0c9-148">Graceful</span></span> |
| <span data-ttu-id="6f0c9-149">Primaire verplaatsen</span><span class="sxs-lookup"><span data-stu-id="6f0c9-149">Move Primary</span></span> |<span data-ttu-id="6f0c9-150">Verplaatst Hallo opgegeven primaire replica van een clusterknooppunt stateful service toohello opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-150">Moves hello specified primary replica of a stateful service toohello specified cluster node.</span></span> |<span data-ttu-id="6f0c9-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="6f0c9-151">MovePrimaryAsync</span></span> |<span data-ttu-id="6f0c9-152">Verplaatsing ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="6f0c9-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="6f0c9-153">Correcte</span><span class="sxs-lookup"><span data-stu-id="6f0c9-153">Graceful</span></span> |
| <span data-ttu-id="6f0c9-154">Secundaire verplaatsen</span><span class="sxs-lookup"><span data-stu-id="6f0c9-154">Move Secondary</span></span> |<span data-ttu-id="6f0c9-155">Hallo huidige secundaire replica van een stateful service tooa ander clusterknooppunt verplaatst.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-155">Moves hello current secondary replica of a stateful service tooa different cluster node.</span></span> |<span data-ttu-id="6f0c9-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="6f0c9-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="6f0c9-157">Verplaatsing ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="6f0c9-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="6f0c9-158">Correcte</span><span class="sxs-lookup"><span data-stu-id="6f0c9-158">Graceful</span></span> |
| <span data-ttu-id="6f0c9-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="6f0c9-159">RemoveReplica</span></span> |<span data-ttu-id="6f0c9-160">Een replica-fout simuleert door het verwijderen van een replica van een cluster.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="6f0c9-161">Dit Hallo replica wordt gesloten en verandert deze toorole 'None', verwijderen van alle van de status van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-161">This will close hello replica and will transition it toorole 'None', removing all of its state from hello cluster.</span></span> |<span data-ttu-id="6f0c9-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="6f0c9-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="6f0c9-163">Verwijder ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="6f0c9-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="6f0c9-164">Correcte</span><span class="sxs-lookup"><span data-stu-id="6f0c9-164">Graceful</span></span> |
| <span data-ttu-id="6f0c9-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="6f0c9-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="6f0c9-166">Simuleert een fout in het pakket code door een codepakket geïmplementeerd op een knooppunt in een cluster opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="6f0c9-167">Hiermee annuleert Hallo code pakket proces dat wordt alle Hallo gebruiker service replica's die worden gehost in het proces opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-167">This aborts hello code package process, which will restart all hello user service replicas hosted in that process.</span></span> |<span data-ttu-id="6f0c9-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="6f0c9-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="6f0c9-169">Opnieuw opstarten ServiceFabricDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="6f0c9-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="6f0c9-170">Geforceerde afsluiting</span><span class="sxs-lookup"><span data-stu-id="6f0c9-170">Ungraceful</span></span> |
| <span data-ttu-id="6f0c9-171">Restartnode uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="6f0c9-171">RestartNode</span></span> |<span data-ttu-id="6f0c9-172">Simuleert een knooppuntfout voor Service Fabric-cluster door een knooppunt opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="6f0c9-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="6f0c9-173">RestartNodeAsync</span></span> |<span data-ttu-id="6f0c9-174">Opnieuw opstarten ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="6f0c9-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="6f0c9-175">Geforceerde afsluiting</span><span class="sxs-lookup"><span data-stu-id="6f0c9-175">Ungraceful</span></span> |
| <span data-ttu-id="6f0c9-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="6f0c9-176">RestartPartition</span></span> |<span data-ttu-id="6f0c9-177">Simuleert een datacenter onleesbaar of cluster onleesbaar scenario door enkele of alle replica's van een partitie opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="6f0c9-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="6f0c9-178">RestartPartitionAsync</span></span> |<span data-ttu-id="6f0c9-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="6f0c9-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="6f0c9-180">Correcte</span><span class="sxs-lookup"><span data-stu-id="6f0c9-180">Graceful</span></span> |
| <span data-ttu-id="6f0c9-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="6f0c9-181">RestartReplica</span></span> |<span data-ttu-id="6f0c9-182">Simuleert een replica mislukt door een persistente replica opnieuw te starten in een cluster, Hallo replica sluiten en vervolgens opnieuw te openen.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing hello replica and then reopening it.</span></span> |<span data-ttu-id="6f0c9-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="6f0c9-183">RestartReplicaAsync</span></span> |<span data-ttu-id="6f0c9-184">Opnieuw opstarten ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="6f0c9-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="6f0c9-185">Correcte</span><span class="sxs-lookup"><span data-stu-id="6f0c9-185">Graceful</span></span> |
| <span data-ttu-id="6f0c9-186">StartNode</span><span class="sxs-lookup"><span data-stu-id="6f0c9-186">StartNode</span></span> |<span data-ttu-id="6f0c9-187">Start een knooppunt in een cluster dat is al gestopt.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="6f0c9-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="6f0c9-188">StartNodeAsync</span></span> |<span data-ttu-id="6f0c9-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="6f0c9-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="6f0c9-190">Niet van toepassing</span><span class="sxs-lookup"><span data-stu-id="6f0c9-190">Not applicable</span></span> |
| <span data-ttu-id="6f0c9-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="6f0c9-191">StopNode</span></span> |<span data-ttu-id="6f0c9-192">Simuleert een storing op een knooppunt door het stoppen van een knooppunt in een cluster.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="6f0c9-193">Hallo knooppunt blijft omlaag totdat beginknooppunt wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-193">hello node will stay down until StartNode is called.</span></span> |<span data-ttu-id="6f0c9-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="6f0c9-194">StopNodeAsync</span></span> |<span data-ttu-id="6f0c9-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="6f0c9-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="6f0c9-196">Geforceerde afsluiting</span><span class="sxs-lookup"><span data-stu-id="6f0c9-196">Ungraceful</span></span> |
| <span data-ttu-id="6f0c9-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="6f0c9-197">ValidateApplication</span></span> |<span data-ttu-id="6f0c9-198">Hallo beschikbaarheid en de status van alle Service Fabric-services in een toepassing, meestal na een bepaalde fout veroorzaken in Hallo systeem gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-198">Validates hello availability and health of all Service Fabric services within an application, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="6f0c9-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="6f0c9-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="6f0c9-200">Test ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="6f0c9-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="6f0c9-201">Niet van toepassing</span><span class="sxs-lookup"><span data-stu-id="6f0c9-201">Not applicable</span></span> |
| <span data-ttu-id="6f0c9-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="6f0c9-202">ValidateService</span></span> |<span data-ttu-id="6f0c9-203">Valideert Hallo beschikbaarheid en status van een Service Fabric-service, meestal na een bepaalde fout veroorzaken in Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-203">Validates hello availability and health of a Service Fabric service, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="6f0c9-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="6f0c9-204">ValidateServiceAsync</span></span> |<span data-ttu-id="6f0c9-205">Test ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="6f0c9-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="6f0c9-206">Niet van toepassing</span><span class="sxs-lookup"><span data-stu-id="6f0c9-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="6f0c9-207">Uitvoeren van een testbaarheid actie met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f0c9-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="6f0c9-208">Deze zelfstudie leert u hoe toorun een actie testbaarheid met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-208">This tutorial shows you how toorun a testability action by using PowerShell.</span></span> <span data-ttu-id="6f0c9-209">U leert hoe toorun een actie testbaarheid op basis van een lokaal (1-box)-cluster of een Azure-cluster.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-209">You will learn how toorun a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="6f0c9-210">Microsoft.Fabric.Powershell.dll--hello Service Fabric PowerShell-module wordt automatisch geïnstalleerd wanneer u Microsoft Service Fabric MSI Hallo installeert.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-210">Microsoft.Fabric.Powershell.dll--hello Service Fabric PowerShell module--is installed automatically when you install hello Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="6f0c9-211">Hallo-module wordt automatisch geladen wanneer u een PowerShell-prompt opent.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-211">hello module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="6f0c9-212">Zelfstudie segmenten:</span><span class="sxs-lookup"><span data-stu-id="6f0c9-212">Tutorial segments:</span></span>

* [<span data-ttu-id="6f0c9-213">Een actie uitvoeren op een cluster met één verpakking</span><span class="sxs-lookup"><span data-stu-id="6f0c9-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="6f0c9-214">Een actie uitvoeren op een Azure-cluster</span><span class="sxs-lookup"><span data-stu-id="6f0c9-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="6f0c9-215">Een actie uitvoeren op een cluster met één verpakking</span><span class="sxs-lookup"><span data-stu-id="6f0c9-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="6f0c9-216">toorun een testbaarheid actie tegen een lokaal cluster voor de eerste verbinding toohello cluster en open Hallo PowerShell-prompt in de beheerdersmodus.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-216">toorun a testability action against a local cluster, first connect toohello cluster and open hello PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="6f0c9-217">Laat het ons bekijkt hello **herstart ServiceFabricNode** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-217">Let us look at hello **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="6f0c9-218">Hier Hallo actie **herstart ServiceFabricNode** wordt uitgevoerd op een knooppunt met de naam 'Knooppunt1'.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-218">Here hello action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="6f0c9-219">Hallo voltooiing modus geeft aan dat deze niet controleren moet of Hallo herstart knooppunt actie daadwerkelijk is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-219">hello completion mode specifies that it should not verify whether hello restart-node action actually succeeded.</span></span> <span data-ttu-id="6f0c9-220">Geven Hallo voltooiing modus als 'Verifiëren' zal deze tooverify of actie Hallo daadwerkelijk is voltooid.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-220">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="6f0c9-221">In plaats van Hallo knooppunt direct met de naam op te geven, kunt u deze via een partitie sleutel en Hallo soort replica, als volgt opgeven:</span><span class="sxs-lookup"><span data-stu-id="6f0c9-221">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="6f0c9-222">**Opnieuw opstarten ServiceFabricNode** gebruikte toorestart een Service Fabric-knooppunt in een cluster moet worden.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-222">**Restart-ServiceFabricNode** should be used toorestart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="6f0c9-223">Hiermee stopt u Hallo Fabric.exe proces, dat alle Hallo system service en de gebruiker service replica's die worden gehost op dat knooppunt wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-223">This will stop hello Fabric.exe process, which will restart all of hello system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="6f0c9-224">Met deze API tootest helpt uw service onthullen bugs langs Hallo failover herstel paden.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-224">Using this API tootest your service helps uncover bugs along hello failover recovery paths.</span></span> <span data-ttu-id="6f0c9-225">Zo kunt u knooppuntfouten in Hallo cluster simuleren.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-225">It helps simulate node failures in hello cluster.</span></span>

<span data-ttu-id="6f0c9-226">Hallo volgende schermafbeelding ziet u Hallo **herstart ServiceFabricNode** testbaarheid opdracht in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-226">hello following screenshot shows hello **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="6f0c9-227">Hallo uitvoer Hallo eerst **Get-ServiceFabricNode** (een cmdlet uit Hallo Service Fabric PowerShell-module) wordt aangegeven dat Hallo lokale cluster bevat vijf knooppunten: Node.1 tooNode.5.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-227">hello output of hello first **Get-ServiceFabricNode** (a cmdlet from hello Service Fabric PowerShell module) shows that hello local cluster has five nodes: Node.1 tooNode.5.</span></span> <span data-ttu-id="6f0c9-228">Na Hallo testbaarheid actie (cmdlet) **herstart ServiceFabricNode** op Hallo-knooppunt wordt uitgevoerd met de naam Node.4, zien we dat Hallo-knooppunt bedrijfstijd is opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-228">After hello testability action (cmdlet) **Restart-ServiceFabricNode** is executed on hello node, named Node.4, we see that hello node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="6f0c9-229">Een actie uitvoeren op een Azure-cluster</span><span class="sxs-lookup"><span data-stu-id="6f0c9-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="6f0c9-230">Met het uitvoeren van een actie testbaarheid (via PowerShell) in een Azure-cluster is vergelijkbaar toorunning Hallo actie tegen een lokaal cluster.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-230">Running a testability action (by using PowerShell) against an Azure cluster is similar toorunning hello action against a local cluster.</span></span> <span data-ttu-id="6f0c9-231">Hallo alleen verschil dat, is voordat u Hallo actie, in plaats van verbindende toohello lokale cluster uitvoeren kunt, moet u tooconnect toohello Azure eerst het cluster.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-231">hello only difference is that before you can run hello action, instead of connecting toohello local cluster, you need tooconnect toohello Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="6f0c9-232">Uitvoeren van een testbaarheid actie met C &#35;</span><span class="sxs-lookup"><span data-stu-id="6f0c9-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="6f0c9-233">toorun een actie testbaarheid met behulp van C#, moet u eerst tooconnect toohello cluster met behulp van FabricClient.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-233">toorun a testability action by using C#, first you need tooconnect toohello cluster by using FabricClient.</span></span> <span data-ttu-id="6f0c9-234">Zodoende Hallo parameters nodig toorun Hallo actie.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-234">Then obtain hello parameters needed toorun hello action.</span></span> <span data-ttu-id="6f0c9-235">Andere parameters kunnen worden gebruikt toorun Hallo dezelfde actie.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-235">Different parameters can be used toorun hello same action.</span></span>
<span data-ttu-id="6f0c9-236">Kijken Hallo RestartServiceFabricNode actie eenrichtingssessie toorun is met behulp van Hallo knooppuntgegevens (naam van het knooppunt en knooppunt exemplaar-ID) in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-236">Looking at hello RestartServiceFabricNode action, one way toorun it is by using hello node information (node name and node instance ID) in hello cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="6f0c9-237">Uitleg van de parameter:</span><span class="sxs-lookup"><span data-stu-id="6f0c9-237">Parameter explanation:</span></span>

* <span data-ttu-id="6f0c9-238">**CompleteMode** geeft die Hallo-modus niet moet controleren of Hallo herstart actie daadwerkelijk is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-238">**CompleteMode** specifies that hello mode should not verify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="6f0c9-239">Geven Hallo voltooiing modus als 'Verifiëren' zal deze tooverify of actie Hallo daadwerkelijk is voltooid.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-239">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span>  
* <span data-ttu-id="6f0c9-240">**OperationTimeout** sets Hallo Hallo bewerking toofinish tijd voordat een TimeoutException-uitzondering is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-240">**OperationTimeout** sets hello amount of time for hello operation toofinish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="6f0c9-241">**CancellationToken** kunt u een aanroep van in behandeling toobe geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-241">**CancellationToken** enables a pending call toobe canceled.</span></span>

<span data-ttu-id="6f0c9-242">In plaats van Hallo knooppunt direct met de naam op te geven, kunt u dit via een partitie sleutel en Hallo soort replica opgeven.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-242">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica.</span></span>

<span data-ttu-id="6f0c9-243">Zie voor meer informatie [PartitionSelector en ReplicaSelector](#partition_replica_selector).</span><span class="sxs-lookup"><span data-stu-id="6f0c9-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="6f0c9-244">PartitionSelector en ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="6f0c9-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="6f0c9-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="6f0c9-245">PartitionSelector</span></span>
<span data-ttu-id="6f0c9-246">PartitionSelector is een helper worden weergegeven in testbaarheid en is gebruikte tooselect een specifieke partitie op welke tooperform Hallo testbaarheid acties.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-246">PartitionSelector is a helper exposed in testability and is used tooselect a specific partition on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="6f0c9-247">Het zijn gebruikte tooselect een specifieke partitie als de partitie-ID Hallo vooraf bekend.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-247">It can be used tooselect a specific partition if hello partition ID is known beforehand.</span></span> <span data-ttu-id="6f0c9-248">Of, kunt u de partitiesleutel Hallo en Hallo bewerking intern Hallo partitie-ID wordt opgelost.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-248">Or, you can provide hello partition key and hello operation will resolve hello partition ID internally.</span></span> <span data-ttu-id="6f0c9-249">U hebt ook Hallo-optie van het selecteren van een willekeurige partitie.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-249">You also have hello option of selecting a random partition.</span></span>

<span data-ttu-id="6f0c9-250">toouse deze helper Hallo PartitionSelector object maken en selecteer Hallo-partitie met behulp van een Hallo Select * methoden.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-250">toouse this helper, create hello PartitionSelector object and select hello partition by using one of hello Select* methods.</span></span> <span data-ttu-id="6f0c9-251">Vervolgens worden doorgegeven in Hallo PartitionSelector object toohello API dat vereist is.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-251">Then pass in hello PartitionSelector object toohello API that requires it.</span></span> <span data-ttu-id="6f0c9-252">Als geen optie is geselecteerd, wordt standaard tooa willekeurige partitie.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-252">If no option is selected, it defaults tooa random partition.</span></span>

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a><span data-ttu-id="6f0c9-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="6f0c9-253">ReplicaSelector</span></span>
<span data-ttu-id="6f0c9-254">ReplicaSelector is een helper worden weergegeven in testbaarheid en is gebruikte toohelp selecteert u een replica op welke tooperform Hallo testbaarheid acties.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-254">ReplicaSelector is a helper exposed in testability and is used toohelp select a replica on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="6f0c9-255">Het zijn gebruikte tooselect een specifieke replica als de replica-ID Hallo vooraf bekend.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-255">It can be used tooselect a specific replica if hello replica ID is known beforehand.</span></span> <span data-ttu-id="6f0c9-256">Bovendien hebt u de optie Hallo van het selecteren van een primaire replica of een willekeurige secundaire site.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-256">In addition, you have hello option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="6f0c9-257">ReplicaSelector is afgeleid van PartitionSelector, dus moet u tooselect Hallo beide replica en Hallo partitie waarop u wilt dat tooperform Hallo testbaarheid bewerking.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-257">ReplicaSelector derives from PartitionSelector, so you need tooselect both hello replica and hello partition on which you wish tooperform hello testability operation.</span></span>

<span data-ttu-id="6f0c9-258">toouse deze helper maken van een object ReplicaSelector en Hallo gewenste tooselect Hallo replica en Hallo partitie ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-258">toouse this helper, create a ReplicaSelector object and set hello way you want tooselect hello replica and hello partition.</span></span> <span data-ttu-id="6f0c9-259">U kunt deze vervolgens doorgeven in Hallo-API die dit vereist is.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-259">You can then pass it into hello API that requires it.</span></span> <span data-ttu-id="6f0c9-260">Als geen optie is geselecteerd, wordt het standaard tooa willekeurige replica en willekeurige partitie.</span><span class="sxs-lookup"><span data-stu-id="6f0c9-260">If no option is selected, it defaults tooa random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="6f0c9-261">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6f0c9-261">Next steps</span></span>
* [<span data-ttu-id="6f0c9-262">Testbaarheid scenario 's</span><span class="sxs-lookup"><span data-stu-id="6f0c9-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="6f0c9-263">Hoe tootest uw service</span><span class="sxs-lookup"><span data-stu-id="6f0c9-263">How tootest your service</span></span>
  * [<span data-ttu-id="6f0c9-264">Fouten tijdens de service werkbelastingen simuleren</span><span class="sxs-lookup"><span data-stu-id="6f0c9-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="6f0c9-265">Fouten in de service-naar-service</span><span class="sxs-lookup"><span data-stu-id="6f0c9-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)


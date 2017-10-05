---
title: Fouten in Azure microservices simuleren | Microsoft Docs
description: In dit artikel wordt gesproken over de acties testbaarheid is gevonden in Microsoft Azure Service Fabric.
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
ms.openlocfilehash: c8ddc7732999ae555323bebaef60aa34c8f2ec17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="testability-actions"></a><span data-ttu-id="ff31a-103">Testbaarheid acties</span><span class="sxs-lookup"><span data-stu-id="ff31a-103">Testability actions</span></span>
<span data-ttu-id="ff31a-104">Om te simuleren een onbetrouwbare infrastructuur, biedt u de ontwikkelaar, manieren om te simuleren verschillende echte fouten en statusovergangen van Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ff31a-104">In order to simulate an unreliable infrastructure, Azure Service Fabric provides you, the developer, with ways to simulate various real-world failures and state transitions.</span></span> <span data-ttu-id="ff31a-105">Deze zijn beschikbaar als testbaarheid acties.</span><span class="sxs-lookup"><span data-stu-id="ff31a-105">These are exposed as testability actions.</span></span> <span data-ttu-id="ff31a-106">De acties zijn de op laag niveau API's die ertoe leiden een specifieke fout injectie, statusovergang of validatie dat.</span><span class="sxs-lookup"><span data-stu-id="ff31a-106">The actions are the low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="ff31a-107">U kunt uitgebreide Testscenario's voor uw services schrijven door een combinatie van deze acties.</span><span class="sxs-lookup"><span data-stu-id="ff31a-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="ff31a-108">Service Fabric bevat dat enkele algemene scenario's voor test bestaan uit deze acties.</span><span class="sxs-lookup"><span data-stu-id="ff31a-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="ff31a-109">Het is raadzaam dat u gebruikmaken van deze ingebouwde scenario's, zorgvuldig worden gekozen voor het testen van algemene statusovergangen en mislukte aanvragen.</span><span class="sxs-lookup"><span data-stu-id="ff31a-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen to test common state transitions and failure cases.</span></span> <span data-ttu-id="ff31a-110">Acties kunnen echter worden gebruikt voor het maken van aangepaste Testscenario's wanneer u wilt toevoegen voor scenario's die zijn niet wordt gedekt door de ingebouwde scenario's nog of die aangepaste speciaal afgestemd op uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ff31a-110">However, actions can be used to create custom test scenarios when you want to add coverage for scenarios that are not covered by the built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="ff31a-111">C#-implementaties van de acties die zijn gevonden in de assembly System.Fabric.dll.</span><span class="sxs-lookup"><span data-stu-id="ff31a-111">C# implementations of the actions are found in the System.Fabric.dll assembly.</span></span> <span data-ttu-id="ff31a-112">De System Fabric PowerShell-module is gevonden in de assembly Microsoft.ServiceFabric.Powershell.dll.</span><span class="sxs-lookup"><span data-stu-id="ff31a-112">The System Fabric PowerShell module is found in the Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="ff31a-113">Als onderdeel van de runtime-installatie, wordt de ServiceFabric PowerShell-module geïnstalleerd zodat voor eenvoudig te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ff31a-113">As part of runtime installation, the ServiceFabric PowerShell module is installed to allow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="ff31a-114">Correcte versus geforceerde afsluiting veroorzaakt acties</span><span class="sxs-lookup"><span data-stu-id="ff31a-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="ff31a-115">Testbaarheid acties worden ingedeeld in twee belangrijke buckets:</span><span class="sxs-lookup"><span data-stu-id="ff31a-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="ff31a-116">Geforceerde afsluiting fouten: deze fouten simuleren fouten zoals machine opnieuw is opgestart en crashes verwerken.</span><span class="sxs-lookup"><span data-stu-id="ff31a-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="ff31a-117">In dergelijke gevallen van fouten uitvoeringscontext van proces abrupt.</span><span class="sxs-lookup"><span data-stu-id="ff31a-117">In such cases of failures, the execution context of process stops abruptly.</span></span> <span data-ttu-id="ff31a-118">Dit betekent dat er geen opschoning van de status kunt uitvoeren voordat de toepassing opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="ff31a-118">This means no cleanup of the state can run before the application starts up again.</span></span>
* <span data-ttu-id="ff31a-119">Correcte fouten: deze fouten simuleren correcte acties zoals replica wordt verplaatst en verwijdert geactiveerd door de taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="ff31a-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="ff31a-120">In dergelijke gevallen de service opgehaald van een melding van het sluiten en de status van de op te ruimen voordat u afsluit.</span><span class="sxs-lookup"><span data-stu-id="ff31a-120">In such cases, the service gets a notification of the close and can clean up the state before exiting.</span></span>

<span data-ttu-id="ff31a-121">Voor betere quality-validatie uitvoeren, de service en zakelijke werkbelasting terwijl verschillende systemen op correct wijze en geforceerde afsluiting fouten veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="ff31a-121">For better quality validation, run the service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="ff31a-122">Geforceerde afsluiting fouten oefenen scenario's waar het serviceproces onverwacht wordt afgesloten in het midden van een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="ff31a-122">Ungraceful faults exercise scenarios where the service process abruptly exits in the middle of some workflow.</span></span> <span data-ttu-id="ff31a-123">Deze test het herstelpad zodra de service-replica is hersteld door de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ff31a-123">This tests  the recovery path once the service replica is restored by Service Fabric.</span></span> <span data-ttu-id="ff31a-124">Dit helpt testen gegevensconsistentie en of de blijft de servicestatus goed na fouten.</span><span class="sxs-lookup"><span data-stu-id="ff31a-124">This will help test data consistency and whether the service state is maintained correctly after failures.</span></span> <span data-ttu-id="ff31a-125">De andere set van fouten (de correcte fouten) testen dat de service juist reageert op de replica's door de Service Fabric wordt verplaatst.</span><span class="sxs-lookup"><span data-stu-id="ff31a-125">The other set of failures (the graceful failures) test that the service correctly reacts to replicas being moved around by Service Fabric.</span></span> <span data-ttu-id="ff31a-126">Dit verwerking van de annulering wordt getest in de RunAsync-methode.</span><span class="sxs-lookup"><span data-stu-id="ff31a-126">This tests handling of cancellation in the RunAsync method.</span></span> <span data-ttu-id="ff31a-127">De service moet controleren voor de annulering-token wordt ingesteld, wordt de status goed opslaan en sluiten van de RunAsync-methode.</span><span class="sxs-lookup"><span data-stu-id="ff31a-127">The service needs to check for the cancellation token being set, correctly save its state, and exit the RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="ff31a-128">Lijst van acties testbaarheid</span><span class="sxs-lookup"><span data-stu-id="ff31a-128">Testability actions list</span></span>
| <span data-ttu-id="ff31a-129">Actie</span><span class="sxs-lookup"><span data-stu-id="ff31a-129">Action</span></span> | <span data-ttu-id="ff31a-130">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ff31a-130">Description</span></span> | <span data-ttu-id="ff31a-131">Beheerde API</span><span class="sxs-lookup"><span data-stu-id="ff31a-131">Managed API</span></span> | <span data-ttu-id="ff31a-132">PowerShell-cmdlet</span><span class="sxs-lookup"><span data-stu-id="ff31a-132">PowerShell cmdlet</span></span> | <span data-ttu-id="ff31a-133">Correcte/geforceerde afsluiting fouten</span><span class="sxs-lookup"><span data-stu-id="ff31a-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="ff31a-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="ff31a-134">CleanTestState</span></span> |<span data-ttu-id="ff31a-135">Hiermee verwijdert u alle statussen van de test uit het cluster in geval van een onjuist afsluiten van het stuurprogramma voor de test.</span><span class="sxs-lookup"><span data-stu-id="ff31a-135">Removes all the test state from the cluster in case of a bad shutdown of the test driver.</span></span> |<span data-ttu-id="ff31a-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="ff31a-136">CleanTestStateAsync</span></span> |<span data-ttu-id="ff31a-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="ff31a-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="ff31a-138">Niet van toepassing</span><span class="sxs-lookup"><span data-stu-id="ff31a-138">Not applicable</span></span> |
| <span data-ttu-id="ff31a-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="ff31a-139">InvokeDataLoss</span></span> |<span data-ttu-id="ff31a-140">Induceert verlies van gegevens in een service-partitie.</span><span class="sxs-lookup"><span data-stu-id="ff31a-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="ff31a-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="ff31a-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="ff31a-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="ff31a-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="ff31a-143">Correcte</span><span class="sxs-lookup"><span data-stu-id="ff31a-143">Graceful</span></span> |
| <span data-ttu-id="ff31a-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="ff31a-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="ff31a-145">De partitie van een bepaalde stateful service plaatst in quorumverlies.</span><span class="sxs-lookup"><span data-stu-id="ff31a-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="ff31a-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="ff31a-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="ff31a-147">Aanroepen ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="ff31a-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="ff31a-148">Correcte</span><span class="sxs-lookup"><span data-stu-id="ff31a-148">Graceful</span></span> |
| <span data-ttu-id="ff31a-149">Primaire verplaatsen</span><span class="sxs-lookup"><span data-stu-id="ff31a-149">Move Primary</span></span> |<span data-ttu-id="ff31a-150">De opgegeven primaire replica van een stateful service verplaatst naar het gespecificeerde clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="ff31a-150">Moves the specified primary replica of a stateful service to the specified cluster node.</span></span> |<span data-ttu-id="ff31a-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="ff31a-151">MovePrimaryAsync</span></span> |<span data-ttu-id="ff31a-152">Verplaatsing ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="ff31a-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="ff31a-153">Correcte</span><span class="sxs-lookup"><span data-stu-id="ff31a-153">Graceful</span></span> |
| <span data-ttu-id="ff31a-154">Secundaire verplaatsen</span><span class="sxs-lookup"><span data-stu-id="ff31a-154">Move Secondary</span></span> |<span data-ttu-id="ff31a-155">De huidige secundaire replica van een stateful service verplaatst naar een ander clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="ff31a-155">Moves the current secondary replica of a stateful service to a different cluster node.</span></span> |<span data-ttu-id="ff31a-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="ff31a-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="ff31a-157">Verplaatsing ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="ff31a-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="ff31a-158">Correcte</span><span class="sxs-lookup"><span data-stu-id="ff31a-158">Graceful</span></span> |
| <span data-ttu-id="ff31a-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="ff31a-159">RemoveReplica</span></span> |<span data-ttu-id="ff31a-160">Een replica-fout simuleert door het verwijderen van een replica van een cluster.</span><span class="sxs-lookup"><span data-stu-id="ff31a-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="ff31a-161">Dit de replica wordt gesloten en verandert deze in rol 'None', verwijderen van alle van de status van het cluster.</span><span class="sxs-lookup"><span data-stu-id="ff31a-161">This will close the replica and will transition it to role 'None', removing all of its state from the cluster.</span></span> |<span data-ttu-id="ff31a-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="ff31a-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="ff31a-163">Verwijder ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="ff31a-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="ff31a-164">Correcte</span><span class="sxs-lookup"><span data-stu-id="ff31a-164">Graceful</span></span> |
| <span data-ttu-id="ff31a-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="ff31a-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="ff31a-166">Simuleert een fout in het pakket code door een codepakket geïmplementeerd op een knooppunt in een cluster opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="ff31a-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="ff31a-167">Hiermee annuleert het proces voor het pakket van code, die wordt alle gebruiker service replica's die worden gehost in het proces opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="ff31a-167">This aborts the code package process, which will restart all the user service replicas hosted in that process.</span></span> |<span data-ttu-id="ff31a-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="ff31a-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="ff31a-169">Opnieuw opstarten ServiceFabricDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="ff31a-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="ff31a-170">Geforceerde afsluiting</span><span class="sxs-lookup"><span data-stu-id="ff31a-170">Ungraceful</span></span> |
| <span data-ttu-id="ff31a-171">Restartnode uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="ff31a-171">RestartNode</span></span> |<span data-ttu-id="ff31a-172">Simuleert een knooppuntfout voor Service Fabric-cluster door een knooppunt opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="ff31a-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="ff31a-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="ff31a-173">RestartNodeAsync</span></span> |<span data-ttu-id="ff31a-174">Opnieuw opstarten ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="ff31a-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="ff31a-175">Geforceerde afsluiting</span><span class="sxs-lookup"><span data-stu-id="ff31a-175">Ungraceful</span></span> |
| <span data-ttu-id="ff31a-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="ff31a-176">RestartPartition</span></span> |<span data-ttu-id="ff31a-177">Simuleert een datacenter onleesbaar of cluster onleesbaar scenario door enkele of alle replica's van een partitie opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="ff31a-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="ff31a-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="ff31a-178">RestartPartitionAsync</span></span> |<span data-ttu-id="ff31a-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="ff31a-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="ff31a-180">Correcte</span><span class="sxs-lookup"><span data-stu-id="ff31a-180">Graceful</span></span> |
| <span data-ttu-id="ff31a-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="ff31a-181">RestartReplica</span></span> |<span data-ttu-id="ff31a-182">Simuleert een replica mislukt door een persistente replica opnieuw te starten in een cluster, het sluiten van de replica en het vervolgens opnieuw te openen.</span><span class="sxs-lookup"><span data-stu-id="ff31a-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing the replica and then reopening it.</span></span> |<span data-ttu-id="ff31a-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="ff31a-183">RestartReplicaAsync</span></span> |<span data-ttu-id="ff31a-184">Opnieuw opstarten ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="ff31a-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="ff31a-185">Correcte</span><span class="sxs-lookup"><span data-stu-id="ff31a-185">Graceful</span></span> |
| <span data-ttu-id="ff31a-186">StartNode</span><span class="sxs-lookup"><span data-stu-id="ff31a-186">StartNode</span></span> |<span data-ttu-id="ff31a-187">Start een knooppunt in een cluster dat is al gestopt.</span><span class="sxs-lookup"><span data-stu-id="ff31a-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="ff31a-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="ff31a-188">StartNodeAsync</span></span> |<span data-ttu-id="ff31a-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="ff31a-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="ff31a-190">Niet van toepassing</span><span class="sxs-lookup"><span data-stu-id="ff31a-190">Not applicable</span></span> |
| <span data-ttu-id="ff31a-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="ff31a-191">StopNode</span></span> |<span data-ttu-id="ff31a-192">Simuleert een storing op een knooppunt door het stoppen van een knooppunt in een cluster.</span><span class="sxs-lookup"><span data-stu-id="ff31a-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="ff31a-193">Het knooppunt blijft omlaag totdat beginknooppunt wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ff31a-193">The node will stay down until StartNode is called.</span></span> |<span data-ttu-id="ff31a-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="ff31a-194">StopNodeAsync</span></span> |<span data-ttu-id="ff31a-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="ff31a-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="ff31a-196">Geforceerde afsluiting</span><span class="sxs-lookup"><span data-stu-id="ff31a-196">Ungraceful</span></span> |
| <span data-ttu-id="ff31a-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="ff31a-197">ValidateApplication</span></span> |<span data-ttu-id="ff31a-198">Valideert de beschikbaarheid en de status van alle Service Fabric-services in een toepassing, meestal na een bepaalde fout veroorzaken in het systeem.</span><span class="sxs-lookup"><span data-stu-id="ff31a-198">Validates the availability and health of all Service Fabric services within an application, usually after inducing some fault into the system.</span></span> |<span data-ttu-id="ff31a-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="ff31a-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="ff31a-200">Test ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="ff31a-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="ff31a-201">Niet van toepassing</span><span class="sxs-lookup"><span data-stu-id="ff31a-201">Not applicable</span></span> |
| <span data-ttu-id="ff31a-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="ff31a-202">ValidateService</span></span> |<span data-ttu-id="ff31a-203">Valideert de beschikbaarheid en de status van een Service Fabric-service, meestal na een bepaalde fout veroorzaken in het systeem.</span><span class="sxs-lookup"><span data-stu-id="ff31a-203">Validates the availability and health of a Service Fabric service, usually after inducing some fault into the system.</span></span> |<span data-ttu-id="ff31a-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="ff31a-204">ValidateServiceAsync</span></span> |<span data-ttu-id="ff31a-205">Test ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="ff31a-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="ff31a-206">Niet van toepassing</span><span class="sxs-lookup"><span data-stu-id="ff31a-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="ff31a-207">Uitvoeren van een testbaarheid actie met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff31a-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="ff31a-208">Deze zelfstudie laat zien hoe u een actie testbaarheid uitvoert met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff31a-208">This tutorial shows you how to run a testability action by using PowerShell.</span></span> <span data-ttu-id="ff31a-209">U leert hoe u een actie testbaarheid uitvoert op basis van een lokaal (1-box)-cluster of een Azure-cluster.</span><span class="sxs-lookup"><span data-stu-id="ff31a-209">You will learn how to run a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="ff31a-210">Microsoft.Fabric.Powershell.dll--de Service Fabric PowerShell-module wordt automatisch geïnstalleerd tijdens de installatie van het Microsoft-Service Fabric-MSI-bestand.</span><span class="sxs-lookup"><span data-stu-id="ff31a-210">Microsoft.Fabric.Powershell.dll--the Service Fabric PowerShell module--is installed automatically when you install the Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="ff31a-211">De module wordt automatisch geladen bij het openen van een PowerShell-prompt.</span><span class="sxs-lookup"><span data-stu-id="ff31a-211">The module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="ff31a-212">Zelfstudie segmenten:</span><span class="sxs-lookup"><span data-stu-id="ff31a-212">Tutorial segments:</span></span>

* [<span data-ttu-id="ff31a-213">Een actie uitvoeren op een cluster met één verpakking</span><span class="sxs-lookup"><span data-stu-id="ff31a-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="ff31a-214">Een actie uitvoeren op een Azure-cluster</span><span class="sxs-lookup"><span data-stu-id="ff31a-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="ff31a-215">Een actie uitvoeren op een cluster met één verpakking</span><span class="sxs-lookup"><span data-stu-id="ff31a-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="ff31a-216">Als u wilt een testbaarheid actie uitvoeren op een lokaal cluster, eerst verbinding met het cluster en open de PowerShell-prompt in de beheerdersmodus.</span><span class="sxs-lookup"><span data-stu-id="ff31a-216">To run a testability action against a local cluster, first connect to the cluster and open the PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="ff31a-217">Laat het ons Bekijk de **herstart ServiceFabricNode** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="ff31a-217">Let us look at the **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="ff31a-218">Hier de actie **herstart ServiceFabricNode** wordt uitgevoerd op een knooppunt met de naam 'Knooppunt1'.</span><span class="sxs-lookup"><span data-stu-id="ff31a-218">Here the action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="ff31a-219">De voltooiing van modus geeft aan dat deze niet controleren moet of het knooppunt opnieuw opstarten actie daadwerkelijk is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="ff31a-219">The completion mode specifies that it should not verify whether the restart-node action actually succeeded.</span></span> <span data-ttu-id="ff31a-220">De voltooiing modus op te geven als 'Verifiëren' gaan om te controleren of de actie opnieuw opstarten daadwerkelijk verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ff31a-220">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span></span> <span data-ttu-id="ff31a-221">In plaats van het knooppunt direct met de naam op te geven, kunt u deze via een partitiesleutel en het soort replica, als volgt:</span><span class="sxs-lookup"><span data-stu-id="ff31a-221">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="ff31a-222">**Opnieuw opstarten ServiceFabricNode** moet worden gebruikt om een Service Fabric-knooppunt in een cluster opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="ff31a-222">**Restart-ServiceFabricNode** should be used to restart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="ff31a-223">Hiermee stopt u het proces Fabric.exe, die alle van de systeem-service en de gebruiker service replica's die worden gehost op dat knooppunt wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="ff31a-223">This will stop the Fabric.exe process, which will restart all of the system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="ff31a-224">Deze API voor het testen van uw service kunt beter onthullen bugs langs de paden voor de failover-herstel.</span><span class="sxs-lookup"><span data-stu-id="ff31a-224">Using this API to test your service helps uncover bugs along the failover recovery paths.</span></span> <span data-ttu-id="ff31a-225">Zo kunt u simuleren knooppuntfouten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="ff31a-225">It helps simulate node failures in the cluster.</span></span>

<span data-ttu-id="ff31a-226">De volgende schermafbeelding ziet u de **herstart ServiceFabricNode** testbaarheid opdracht in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="ff31a-226">The following screenshot shows the **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="ff31a-227">De uitvoer van de eerste **Get-ServiceFabricNode** (een cmdlet uit de Service Fabric PowerShell-module) wordt aangegeven dat het lokale cluster vijf knooppunten bevat: Node.1 naar Node.5.</span><span class="sxs-lookup"><span data-stu-id="ff31a-227">The output of the first **Get-ServiceFabricNode** (a cmdlet from the Service Fabric PowerShell module) shows that the local cluster has five nodes: Node.1 to Node.5.</span></span> <span data-ttu-id="ff31a-228">Nadat de actie testbaarheid (cmdlet) **herstart ServiceFabricNode** wordt uitgevoerd op het knooppunt met de naam Node.4, zien we dat de beschikbaarheid van het knooppunt is teruggezet.</span><span class="sxs-lookup"><span data-stu-id="ff31a-228">After the testability action (cmdlet) **Restart-ServiceFabricNode** is executed on the node, named Node.4, we see that the node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="ff31a-229">Een actie uitvoeren op een Azure-cluster</span><span class="sxs-lookup"><span data-stu-id="ff31a-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="ff31a-230">Met het uitvoeren van een actie testbaarheid (via PowerShell) in een Azure-cluster is vergelijkbaar met het uitvoeren van de actie tegen een lokaal cluster.</span><span class="sxs-lookup"><span data-stu-id="ff31a-230">Running a testability action (by using PowerShell) against an Azure cluster is similar to running the action against a local cluster.</span></span> <span data-ttu-id="ff31a-231">Het enige verschil is voordat u de actie, in plaats van de verbinding met het lokale cluster kunt uitvoeren moet u eerst verbinding met de Azure-cluster.</span><span class="sxs-lookup"><span data-stu-id="ff31a-231">The only difference is that before you can run the action, instead of connecting to the local cluster, you need to connect to the Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="ff31a-232">Uitvoeren van een testbaarheid actie met C &#35;</span><span class="sxs-lookup"><span data-stu-id="ff31a-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="ff31a-233">Een testbaarheid als actie wilt uitvoeren met behulp van C#, moet u eerst verbinding met het cluster via FabricClient.</span><span class="sxs-lookup"><span data-stu-id="ff31a-233">To run a testability action by using C#, first you need to connect to the cluster by using FabricClient.</span></span> <span data-ttu-id="ff31a-234">Moet u de parameters die nodig zijn voor de actie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="ff31a-234">Then obtain the parameters needed to run the action.</span></span> <span data-ttu-id="ff31a-235">Andere parameters kunnen worden gebruikt om uit te voeren dezelfde actie.</span><span class="sxs-lookup"><span data-stu-id="ff31a-235">Different parameters can be used to run the same action.</span></span>
<span data-ttu-id="ff31a-236">De actie RestartServiceFabricNode bekijkt, is een manier uit te voeren met behulp van de knooppuntgegevens (naam van het knooppunt en knooppunt exemplaar-ID) in het cluster.</span><span class="sxs-lookup"><span data-stu-id="ff31a-236">Looking at the RestartServiceFabricNode action, one way to run it is by using the node information (node name and node instance ID) in the cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="ff31a-237">Uitleg van de parameter:</span><span class="sxs-lookup"><span data-stu-id="ff31a-237">Parameter explanation:</span></span>

* <span data-ttu-id="ff31a-238">**CompleteMode** geeft aan dat de modus niet controleren moet of de herstart actie daadwerkelijk is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="ff31a-238">**CompleteMode** specifies that the mode should not verify whether the restart action actually succeeded.</span></span> <span data-ttu-id="ff31a-239">De voltooiing modus op te geven als 'Verifiëren' gaan om te controleren of de actie opnieuw opstarten daadwerkelijk verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ff31a-239">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span></span>  
* <span data-ttu-id="ff31a-240">**OperationTimeout** stelt u de hoeveelheid tijd voor de bewerking is voltooid voordat een TimeoutException-uitzondering is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="ff31a-240">**OperationTimeout** sets the amount of time for the operation to finish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="ff31a-241">**CancellationToken** kunt u een aanroep van in behandeling worden geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="ff31a-241">**CancellationToken** enables a pending call to be canceled.</span></span>

<span data-ttu-id="ff31a-242">In plaats van het knooppunt direct met de naam op te geven, kunt u deze via een partitiesleutel en de aard van de replica.</span><span class="sxs-lookup"><span data-stu-id="ff31a-242">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica.</span></span>

<span data-ttu-id="ff31a-243">Zie voor meer informatie [PartitionSelector en ReplicaSelector](#partition_replica_selector).</span><span class="sxs-lookup"><span data-stu-id="ff31a-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference to System.Fabric.Testability.dll and System.Fabric.dll
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
            //Restart the node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way to restart node is by using nodeName and nodeInstanceId
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

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="ff31a-244">PartitionSelector en ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="ff31a-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="ff31a-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="ff31a-245">PartitionSelector</span></span>
<span data-ttu-id="ff31a-246">PartitionSelector is een helper worden weergegeven in testbaarheid en wordt gebruikt om een specifieke partitie waarop moet worden uitgevoerd op een van de acties testbaarheid te selecteren.</span><span class="sxs-lookup"><span data-stu-id="ff31a-246">PartitionSelector is a helper exposed in testability and is used to select a specific partition on which to perform any of the testability actions.</span></span> <span data-ttu-id="ff31a-247">Het kan worden gebruikt om te selecteren van een specifieke partitie als de partitie-ID vooraf bekend.</span><span class="sxs-lookup"><span data-stu-id="ff31a-247">It can be used to select a specific partition if the partition ID is known beforehand.</span></span> <span data-ttu-id="ff31a-248">Of u kunt de partitiesleutel bieden en de bewerking wordt de partitie-ID intern opgelost.</span><span class="sxs-lookup"><span data-stu-id="ff31a-248">Or, you can provide the partition key and the operation will resolve the partition ID internally.</span></span> <span data-ttu-id="ff31a-249">U hebt ook de optie van het selecteren van een willekeurige partitie.</span><span class="sxs-lookup"><span data-stu-id="ff31a-249">You also have the option of selecting a random partition.</span></span>

<span data-ttu-id="ff31a-250">Het object PartitionSelector niet maken voor het gebruik van deze helper en selecteren van de partitie met behulp van een van de methoden Select *.</span><span class="sxs-lookup"><span data-stu-id="ff31a-250">To use this helper, create the PartitionSelector object and select the partition by using one of the Select* methods.</span></span> <span data-ttu-id="ff31a-251">Vervolgens worden in het PartitionSelector-object doorgegeven aan de API dat vereist is.</span><span class="sxs-lookup"><span data-stu-id="ff31a-251">Then pass in the PartitionSelector object to the API that requires it.</span></span> <span data-ttu-id="ff31a-252">Als er geen optie is geselecteerd, wordt standaard een willekeurige partitie.</span><span class="sxs-lookup"><span data-stu-id="ff31a-252">If no option is selected, it defaults to a random partition.</span></span>

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

### <a name="replicaselector"></a><span data-ttu-id="ff31a-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="ff31a-253">ReplicaSelector</span></span>
<span data-ttu-id="ff31a-254">ReplicaSelector is een helper worden weergegeven in testbaarheid en wordt gebruikt om te selecteren van een replica waarop een van de testbaarheid acties uitvoert.</span><span class="sxs-lookup"><span data-stu-id="ff31a-254">ReplicaSelector is a helper exposed in testability and is used to help select a replica on which to perform any of the testability actions.</span></span> <span data-ttu-id="ff31a-255">Het kan worden gebruikt om te selecteren van een specifieke replica als de replica-ID vooraf bekend.</span><span class="sxs-lookup"><span data-stu-id="ff31a-255">It can be used to select a specific replica if the replica ID is known beforehand.</span></span> <span data-ttu-id="ff31a-256">Bovendien hebt u de mogelijkheid van het selecteren van een primaire replica of een willekeurige secundaire site.</span><span class="sxs-lookup"><span data-stu-id="ff31a-256">In addition, you have the option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="ff31a-257">ReplicaSelector is afgeleid van PartitionSelector, dus moet u de replica en de partitie waarop u wilt uitvoeren van de bewerking testbaarheid selecteren.</span><span class="sxs-lookup"><span data-stu-id="ff31a-257">ReplicaSelector derives from PartitionSelector, so you need to select both the replica and the partition on which you wish to perform the testability operation.</span></span>

<span data-ttu-id="ff31a-258">Voor het gebruik van het hulpprogramma een ReplicaSelector-object maken en de manier waarop u wilt selecteren, de replica en de partitie ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ff31a-258">To use this helper, create a ReplicaSelector object and set the way you want to select the replica and the partition.</span></span> <span data-ttu-id="ff31a-259">U kunt deze vervolgens doorgeven in de API die dit vereist is.</span><span class="sxs-lookup"><span data-stu-id="ff31a-259">You can then pass it into the API that requires it.</span></span> <span data-ttu-id="ff31a-260">Als er geen optie is geselecteerd, wordt standaard een willekeurige replica en willekeurige partitie.</span><span class="sxs-lookup"><span data-stu-id="ff31a-260">If no option is selected, it defaults to a random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select the primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select the replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="ff31a-261">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ff31a-261">Next steps</span></span>
* [<span data-ttu-id="ff31a-262">Testbaarheid scenario 's</span><span class="sxs-lookup"><span data-stu-id="ff31a-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="ff31a-263">Het testen van uw service</span><span class="sxs-lookup"><span data-stu-id="ff31a-263">How to test your service</span></span>
  * [<span data-ttu-id="ff31a-264">Fouten tijdens de service werkbelastingen simuleren</span><span class="sxs-lookup"><span data-stu-id="ff31a-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="ff31a-265">Fouten in de service-naar-service</span><span class="sxs-lookup"><span data-stu-id="ff31a-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)


---
title: Service Fabric aaaAzure verschillen tussen de Linux- en Windows | Microsoft Docs
description: Verschillen tussen hello Azure Service Fabric Preview op Linux- en Azure Service Fabric in Windows.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 7a16a440dfc8d9006e274f46951be1562e6f10d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a><span data-ttu-id="99e69-103">Verschillen tussen Service Fabric in Linux (preview) en Service Fabric in Windows (algemeen beschikbaar)</span><span class="sxs-lookup"><span data-stu-id="99e69-103">Differences between Service Fabric on Linux (preview) and Windows (generally available)</span></span>

<span data-ttu-id="99e69-104">Omdat Service Fabric in Linux een preview-versie is, zijn er enkele functies die wel worden ondersteund in Windows, maar nog niet in Linux.</span><span class="sxs-lookup"><span data-stu-id="99e69-104">Since Service Fabric on Linux is a preview, there are some features that are supported on Windows, but not yet on Linux.</span></span> <span data-ttu-id="99e69-105">Uiteindelijk zich Hallo functiesets aan pariteit zodra het Service Fabric op Linux in het algemeen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="99e69-105">Eventually, hello feature sets will be at parity when Service Fabric on Linux becomes generally available.</span></span> <span data-ttu-id="99e69-106">In toekomstige versies worden de verschillen in functies steeds kleiner.</span><span class="sxs-lookup"><span data-stu-id="99e69-106">With upcoming releases, this feature gap will shrink.</span></span> <span data-ttu-id="99e69-107">Hallo volgende verschillen bestaan tussen Hallo meest recente beschikbare versies (dat wil zeggen, tussen versie 5.6 voor Windows en versie 5.5 op Linux):</span><span class="sxs-lookup"><span data-stu-id="99e69-107">hello following differences exist between hello latest available releases (that is, between version 5.6 on Windows and version 5.5 on Linux):</span></span> 

* <span data-ttu-id="99e69-108">Betrouwbare verzamelingen (en betrouwbare stateful services)</span><span class="sxs-lookup"><span data-stu-id="99e69-108">Reliable Collections (and Reliable Stateful Services)</span></span> 
* <span data-ttu-id="99e69-109">ReverseProxy</span><span class="sxs-lookup"><span data-stu-id="99e69-109">ReverseProxy</span></span> 
* <span data-ttu-id="99e69-110">Zelfstandig installatieprogramma</span><span class="sxs-lookup"><span data-stu-id="99e69-110">Standalone installer</span></span> 
* <span data-ttu-id="99e69-111">XML-schemavalidatie voor manifestbestanden</span><span class="sxs-lookup"><span data-stu-id="99e69-111">XML schema validation for manifest files</span></span> 
* <span data-ttu-id="99e69-112">Consoleomleiding</span><span class="sxs-lookup"><span data-stu-id="99e69-112">Console redirection</span></span> 
* <span data-ttu-id="99e69-113">Hallo veroorzaakt Analysis Service (door)</span><span class="sxs-lookup"><span data-stu-id="99e69-113">hello Fault Analysis Service (FAS)</span></span>
* <span data-ttu-id="99e69-114">Docker Compose-volume en logboekregistratiestuurprogramma's voor containers</span><span class="sxs-lookup"><span data-stu-id="99e69-114">Docker compose and volume and logging drivers for containers</span></span> 
* <span data-ttu-id="99e69-115">Resourcebeheer voor containers en services</span><span class="sxs-lookup"><span data-stu-id="99e69-115">Resource governance for containers and services</span></span> 
* <span data-ttu-id="99e69-116">DNS-service</span><span class="sxs-lookup"><span data-stu-id="99e69-116">DNS service</span></span>
* <span data-ttu-id="99e69-117">Ondersteuning van Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99e69-117">Azure Active Directory support</span></span>
* <span data-ttu-id="99e69-118">CLI-opdrachtequivalenten van bepaalde Powershell-opdrachten</span><span class="sxs-lookup"><span data-stu-id="99e69-118">CLI command equivalents of certain Powershell commands</span></span> 
* <span data-ttu-id="99e69-119">Alleen een subset van de Powershell-opdrachten kan worden uitgevoerd op een Linux-cluster (zoals uitgevouwen in de volgende sectie Hallo).</span><span class="sxs-lookup"><span data-stu-id="99e69-119">Only a subset of Powershell commands can be run against a Linux cluster (as expanded in hello next section).</span></span>

>[!NOTE]
><span data-ttu-id="99e69-120">Console-omleiding wordt niet ondersteund in productieclusters, ook niet in Windows.</span><span class="sxs-lookup"><span data-stu-id="99e69-120">Console redirection is not supported in production clusters, even on Windows.</span></span>

<span data-ttu-id="99e69-121">De hulpmiddelen voor ontwikkelaars verschillen ook tussen Windows en Linux.</span><span class="sxs-lookup"><span data-stu-id="99e69-121">Development tooling is also different between Windows and Linux.</span></span> <span data-ttu-id="99e69-122">VisualStudio, Powershell VSTS en ETW worden gebruikt op Windows terwijl Yeoman, Eclipse, Jenkins en LTTng op Linux worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="99e69-122">VisualStudio, Powershell, VSTS, and ETW are used on Windows while Yeoman, Eclipse, Jenkins, and LTTng are used on Linux.</span></span>

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a><span data-ttu-id="99e69-123">PowerShell-cmdlets die niet werken voor een Service Fabric-cluster in Linux</span><span class="sxs-lookup"><span data-stu-id="99e69-123">Powershell cmdlets that do not work against a Linux Service Fabric cluster</span></span>

* <span data-ttu-id="99e69-124">Invoke-ServiceFabricChaosTestScenario</span><span class="sxs-lookup"><span data-stu-id="99e69-124">Invoke-ServiceFabricChaosTestScenario</span></span>
* <span data-ttu-id="99e69-125">Invoke-ServiceFabricFailoverTestScenario</span><span class="sxs-lookup"><span data-stu-id="99e69-125">Invoke-ServiceFabricFailoverTestScenario</span></span>
* <span data-ttu-id="99e69-126">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="99e69-126">Invoke-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="99e69-127">Invoke-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="99e69-127">Invoke-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="99e69-128">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="99e69-128">Restart-ServiceFabricPartition</span></span>
* <span data-ttu-id="99e69-129">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="99e69-129">Start-ServiceFabricNode</span></span>
* <span data-ttu-id="99e69-130">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="99e69-130">Stop-ServiceFabricNode</span></span>
* <span data-ttu-id="99e69-131">Get-ServiceFabricImageStoreContent</span><span class="sxs-lookup"><span data-stu-id="99e69-131">Get-ServiceFabricImageStoreContent</span></span>
* <span data-ttu-id="99e69-132">Get-ServiceFabricChaosReport</span><span class="sxs-lookup"><span data-stu-id="99e69-132">Get-ServiceFabricChaosReport</span></span>
* <span data-ttu-id="99e69-133">Get-ServiceFabricNodeTransitionProgress</span><span class="sxs-lookup"><span data-stu-id="99e69-133">Get-ServiceFabricNodeTransitionProgress</span></span>
* <span data-ttu-id="99e69-134">Get-ServiceFabricPartitionDataLossProgress</span><span class="sxs-lookup"><span data-stu-id="99e69-134">Get-ServiceFabricPartitionDataLossProgress</span></span>
* <span data-ttu-id="99e69-135">Get-ServiceFabricPartitionQuorumLossProgress</span><span class="sxs-lookup"><span data-stu-id="99e69-135">Get-ServiceFabricPartitionQuorumLossProgress</span></span>
* <span data-ttu-id="99e69-136">Get-ServiceFabricPartitionRestartProgress</span><span class="sxs-lookup"><span data-stu-id="99e69-136">Get-ServiceFabricPartitionRestartProgress</span></span>
* <span data-ttu-id="99e69-137">Get-ServiceFabricTestCommandStatusList</span><span class="sxs-lookup"><span data-stu-id="99e69-137">Get-ServiceFabricTestCommandStatusList</span></span>
* <span data-ttu-id="99e69-138">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="99e69-138">Remove-ServiceFabricTestState</span></span>
* <span data-ttu-id="99e69-139">Start-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="99e69-139">Start-ServiceFabricChaos</span></span>
* <span data-ttu-id="99e69-140">Start-ServiceFabricNodeTransition</span><span class="sxs-lookup"><span data-stu-id="99e69-140">Start-ServiceFabricNodeTransition</span></span>
* <span data-ttu-id="99e69-141">Start-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="99e69-141">Start-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="99e69-142">Start-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="99e69-142">Start-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="99e69-143">Start-ServiceFabricPartitionRestart</span><span class="sxs-lookup"><span data-stu-id="99e69-143">Start-ServiceFabricPartitionRestart</span></span>
* <span data-ttu-id="99e69-144">Stop-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="99e69-144">Stop-ServiceFabricChaos</span></span>
* <span data-ttu-id="99e69-145">Stop-ServiceFabricTestCommand</span><span class="sxs-lookup"><span data-stu-id="99e69-145">Stop-ServiceFabricTestCommand</span></span>
* <span data-ttu-id="99e69-146">Cmd</span><span class="sxs-lookup"><span data-stu-id="99e69-146">Cmd</span></span>
* <span data-ttu-id="99e69-147">Get-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="99e69-147">Get-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="99e69-148">Get-ServiceFabricClusterConfiguration</span><span class="sxs-lookup"><span data-stu-id="99e69-148">Get-ServiceFabricClusterConfiguration</span></span>
* <span data-ttu-id="99e69-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span><span class="sxs-lookup"><span data-stu-id="99e69-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span></span>
* <span data-ttu-id="99e69-150">Get-ServiceFabricPackageDebugParameters</span><span class="sxs-lookup"><span data-stu-id="99e69-150">Get-ServiceFabricPackageDebugParameters</span></span>
* <span data-ttu-id="99e69-151">New-ServiceFabricPackageDebugParameter</span><span class="sxs-lookup"><span data-stu-id="99e69-151">New-ServiceFabricPackageDebugParameter</span></span>
* <span data-ttu-id="99e69-152">New-ServiceFabricPackageSharingPolicy</span><span class="sxs-lookup"><span data-stu-id="99e69-152">New-ServiceFabricPackageSharingPolicy</span></span>
* <span data-ttu-id="99e69-153">Add-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="99e69-153">Add-ServiceFabricNode</span></span>
* <span data-ttu-id="99e69-154">Copy-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="99e69-154">Copy-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="99e69-155">Get-ServiceFabricRuntimeSupportedVersion</span><span class="sxs-lookup"><span data-stu-id="99e69-155">Get-ServiceFabricRuntimeSupportedVersion</span></span>
* <span data-ttu-id="99e69-156">Get-ServiceFabricRuntimeUpgradeVersion</span><span class="sxs-lookup"><span data-stu-id="99e69-156">Get-ServiceFabricRuntimeUpgradeVersion</span></span>
* <span data-ttu-id="99e69-157">New-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="99e69-157">New-ServiceFabricCluster</span></span>
* <span data-ttu-id="99e69-158">New-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="99e69-158">New-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="99e69-159">Remove-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="99e69-159">Remove-ServiceFabricCluster</span></span>
* <span data-ttu-id="99e69-160">Remove-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="99e69-160">Remove-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="99e69-161">Remove-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="99e69-161">Remove-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="99e69-162">Test-ServiceFabricClusterManifest</span><span class="sxs-lookup"><span data-stu-id="99e69-162">Test-ServiceFabricClusterManifest</span></span>
* <span data-ttu-id="99e69-163">Test-ServiceFabricConfiguration</span><span class="sxs-lookup"><span data-stu-id="99e69-163">Test-ServiceFabricConfiguration</span></span>
* <span data-ttu-id="99e69-164">Update-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="99e69-164">Update-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="99e69-165">Approve-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="99e69-165">Approve-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="99e69-166">Complete-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="99e69-166">Complete-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="99e69-167">Get-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="99e69-167">Get-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="99e69-168">Invoke-ServiceFabricDecryptText</span><span class="sxs-lookup"><span data-stu-id="99e69-168">Invoke-ServiceFabricDecryptText</span></span>
* <span data-ttu-id="99e69-169">Invoke-ServiceFabricEncryptSecret</span><span class="sxs-lookup"><span data-stu-id="99e69-169">Invoke-ServiceFabricEncryptSecret</span></span>
* <span data-ttu-id="99e69-170">Invoke-ServiceFabricEncryptText</span><span class="sxs-lookup"><span data-stu-id="99e69-170">Invoke-ServiceFabricEncryptText</span></span>
* <span data-ttu-id="99e69-171">Invoke-ServiceFabricInfrastructureCommand</span><span class="sxs-lookup"><span data-stu-id="99e69-171">Invoke-ServiceFabricInfrastructureCommand</span></span>
* <span data-ttu-id="99e69-172">Invoke-ServiceFabricInfrastructureQuery</span><span class="sxs-lookup"><span data-stu-id="99e69-172">Invoke-ServiceFabricInfrastructureQuery</span></span>
* <span data-ttu-id="99e69-173">Remove-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="99e69-173">Remove-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="99e69-174">Start-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="99e69-174">Start-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="99e69-175">Stop-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="99e69-175">Stop-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="99e69-176">Update-ServiceFabricRepairTaskHealthPolicy</span><span class="sxs-lookup"><span data-stu-id="99e69-176">Update-ServiceFabricRepairTaskHealthPolicy</span></span>



## <a name="next-steps"></a><span data-ttu-id="99e69-177">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="99e69-177">Next steps</span></span>
* [<span data-ttu-id="99e69-178">Uw ontwikkelomgeving voorbereiden in Linux</span><span class="sxs-lookup"><span data-stu-id="99e69-178">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="99e69-179">Uw ontwikkelomgeving voorbereiden in OSX</span><span class="sxs-lookup"><span data-stu-id="99e69-179">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="99e69-180">Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van Yeoman</span><span class="sxs-lookup"><span data-stu-id="99e69-180">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="99e69-181">Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van de Service Fabric-invoegtoepassing voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="99e69-181">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="99e69-182">Uw eerste CSharp-toepassing in Linux maken</span><span class="sxs-lookup"><span data-stu-id="99e69-182">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="99e69-183">Hallo Service Fabric CLI toomanage uw toepassingen gebruiken</span><span class="sxs-lookup"><span data-stu-id="99e69-183">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)

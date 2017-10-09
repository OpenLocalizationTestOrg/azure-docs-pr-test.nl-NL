---
title: aaaConfigure hello upgrade van een Service Fabric-toepassing | Microsoft Docs
description: Meer informatie over hoe tooconfigure instellingen Hallo voor het upgraden van een Service Fabric-toepassing met behulp van Microsoft Visual Studio.
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="c951b-103">Hallo-upgrade van een Service Fabric-toepassing in Visual Studio configureren</span><span class="sxs-lookup"><span data-stu-id="c951b-103">Configure hello upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="c951b-104">Visual Studio tools voor Azure Service Fabric bieden upgrade ondersteuning voor het publiceren van toolocal of externe clusters.</span><span class="sxs-lookup"><span data-stu-id="c951b-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing toolocal or remote clusters.</span></span> <span data-ttu-id="c951b-105">Er zijn drie scenario's waarin u tooupgrade uw toepassing tooa nieuwere versie in plaats van de vervangen toepassing hello wilt tijdens het testen en foutopsporing:</span><span class="sxs-lookup"><span data-stu-id="c951b-105">There are three scenarios in which you want tooupgrade your application tooa newer version instead of replacing hello application during testing and debugging:</span></span>

* <span data-ttu-id="c951b-106">Toepassingsgegevens niet verloren gaan tijdens het Hallo-upgrade.</span><span class="sxs-lookup"><span data-stu-id="c951b-106">Application data won't be lost during hello upgrade.</span></span>
* <span data-ttu-id="c951b-107">Beschikbaarheid blijft hoge zodat er niet serviceonderbreking tijdens de upgrade hello, als er dat voldoende service-exemplaren verspreid over upgradedomeinen.</span><span class="sxs-lookup"><span data-stu-id="c951b-107">Availability remains high so there won't be any service interruption during hello upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="c951b-108">Tests kunnen worden uitgevoerd op basis van een toepassing, terwijl deze wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c951b-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-tooupgrade"></a><span data-ttu-id="c951b-109">Parameters nodig tooupgrade</span><span class="sxs-lookup"><span data-stu-id="c951b-109">Parameters needed tooupgrade</span></span>
<span data-ttu-id="c951b-110">U kunt kiezen uit twee soorten implementatie: reguliere of de upgrade.</span><span class="sxs-lookup"><span data-stu-id="c951b-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="c951b-111">Een gewone implementatie worden gewist alle vorige implementatie-informatie en gegevens op het Hallo-cluster, terwijl een upgrade-implementatie behouden deze blijft.</span><span class="sxs-lookup"><span data-stu-id="c951b-111">A regular deployment erases any previous deployment information and data on hello cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="c951b-112">Wanneer u een Service Fabric-toepassing in Visual Studio bijwerkt, moet u de upgrade toepassingsparameters tooprovide en statusbeleid voor controle.</span><span class="sxs-lookup"><span data-stu-id="c951b-112">When you upgrade a Service Fabric application in Visual Studio, you need tooprovide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="c951b-113">Upgrade van de toepassing parameters te regelen Hallo upgrade terwijl controle statusbeleid bepalen of Hallo-upgrade is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="c951b-113">Application upgrade parameters help control hello upgrade, while health check policies determine whether hello upgrade was successful.</span></span> <span data-ttu-id="c951b-114">Zie [upgrade van de Service Fabric-toepassing: upgrade parameters](service-fabric-application-upgrade-parameters.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c951b-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="c951b-115">Er zijn drie upgrade modi: *bewaakte*, *UnmonitoredAuto*, en *UnmonitoredManual*.</span><span class="sxs-lookup"><span data-stu-id="c951b-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="c951b-116">De upgrade van een bewaakte automatiseert het Hallo-upgrade en toepassing statuscontrole.</span><span class="sxs-lookup"><span data-stu-id="c951b-116">A Monitored upgrade automates hello upgrade and application health check.</span></span>
* <span data-ttu-id="c951b-117">Een upgrade UnmonitoredAuto automatiseert het Hallo-upgrade, maar slaat het Hallo statuscontrole van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c951b-117">An UnmonitoredAuto upgrade automates hello upgrade, but skips hello application health check.</span></span>
* <span data-ttu-id="c951b-118">Wanneer u een upgrade UnmonitoredManual doet, moet u toomanually elk upgradedomein upgraden.</span><span class="sxs-lookup"><span data-stu-id="c951b-118">When you do an UnmonitoredManual upgrade, you need toomanually upgrade each upgrade domain.</span></span>

<span data-ttu-id="c951b-119">Elke upgrademodus vereist verschillende sets van parameters.</span><span class="sxs-lookup"><span data-stu-id="c951b-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="c951b-120">Zie [parameters voor het bijwerken van toepassing](service-fabric-application-upgrade-parameters.md) toolearn meer informatie over de beschikbare upgradeopties Hallo.</span><span class="sxs-lookup"><span data-stu-id="c951b-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) toolearn more about hello available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="c951b-121">Upgrade van een Service Fabric-toepassing in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c951b-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="c951b-122">Als u Hallo Visual Studio Service Fabric extra tooupgrade Service Fabric-toepassing, kunt u een proces publiceren toobe opgeven van een upgrade in plaats van een normale implementatie door te controleren Hallo **upgrade uitvoert voor de toepassing hello** controleren vak.</span><span class="sxs-lookup"><span data-stu-id="c951b-122">If you’re using hello Visual Studio Service Fabric tools tooupgrade a Service Fabric application, you can specify a publish process toobe an upgrade rather than a regular deployment by checking hello **Upgrade hello application** check box.</span></span>

### <a name="tooconfigure-hello-upgrade-parameters"></a><span data-ttu-id="c951b-123">upgrade tooconfigure Hallo-parameters</span><span class="sxs-lookup"><span data-stu-id="c951b-123">tooconfigure hello upgrade parameters</span></span>
1. <span data-ttu-id="c951b-124">Klik op Hallo **instellingen** knop volgende toohello selectievakje.</span><span class="sxs-lookup"><span data-stu-id="c951b-124">Click hello **Settings** button next toohello check box.</span></span> <span data-ttu-id="c951b-125">Hallo **Upgrade Parameters bewerken** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c951b-125">hello **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="c951b-126">Hallo **Upgrade Parameters bewerken** in het dialoogvenster ondersteunt Hallo bewaakte UnmonitoredAuto en UnmonitoredManual upgrade modi.</span><span class="sxs-lookup"><span data-stu-id="c951b-126">hello **Edit Upgrade Parameters** dialog box supports hello Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="c951b-127">Selecteer de upgrademodus Hallo dat u toouse wilt en vult u Hallo parameter raster.</span><span class="sxs-lookup"><span data-stu-id="c951b-127">Select hello upgrade mode that you want toouse and then fill out hello parameter grid.</span></span>

    <span data-ttu-id="c951b-128">Elke parameter heeft standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="c951b-128">Each parameter has default values.</span></span> <span data-ttu-id="c951b-129">optionele parameter Hallo *DefaultServiceTypeHealthPolicy* een hash-tabel invoer.</span><span class="sxs-lookup"><span data-stu-id="c951b-129">hello optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="c951b-130">Hier volgt een voorbeeld van Hallo hash-tabel invoerindeling voor *DefaultServiceTypeHealthPolicy*:</span><span class="sxs-lookup"><span data-stu-id="c951b-130">Here’s an example of hello hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="c951b-131">*Servicetypehealthpolicymap; deze* is een andere optionele parameter waarmee een hash-Tabelinvoer in Hallo de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="c951b-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in hello following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="c951b-132">Hier volgt een voorbeeld van de praktijk:</span><span class="sxs-lookup"><span data-stu-id="c951b-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="c951b-133">Als u de upgrademodus UnmonitoredManual selecteert, moet u handmatig starten van een PowerShell-console toocontinue en klaar bent met het upgradeproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="c951b-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console toocontinue and finish hello upgrade process.</span></span> <span data-ttu-id="c951b-134">Raadpleeg te[upgrade van de Service Fabric-toepassing: geavanceerde onderwerpen](service-fabric-application-upgrade-advanced.md) toolearn hoe handmatige upgrade werkt.</span><span class="sxs-lookup"><span data-stu-id="c951b-134">Refer too[Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) toolearn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="c951b-135">Upgrade van een toepassing met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="c951b-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="c951b-136">U kunt de PowerShell-cmdlets tooupgrade Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c951b-136">You can use PowerShell cmdlets tooupgrade a Service Fabric application.</span></span> <span data-ttu-id="c951b-137">Zie [upgrade zelfstudie over Service Fabric](service-fabric-application-upgrade-tutorial.md) en [Start ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="c951b-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a><span data-ttu-id="c951b-138">Geef een selectievakje statusbeleid in het manifestbestand van de toepassing hello</span><span class="sxs-lookup"><span data-stu-id="c951b-138">Specify a health check policy in hello application manifest file</span></span>
<span data-ttu-id="c951b-139">Elke service in een Service Fabric-toepassing kan een eigen parameters voor het beleid van health dat voorrang boven de standaardwaarden Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="c951b-139">Every service in a Service Fabric application can have its own health policy parameters that override hello default values.</span></span> <span data-ttu-id="c951b-140">U kunt deze parameterwaarden in het manifestbestand van de toepassing hello opgeven.</span><span class="sxs-lookup"><span data-stu-id="c951b-140">You can provide these parameter values in hello application manifest file.</span></span>

<span data-ttu-id="c951b-141">Hallo volgende voorbeeld ziet u hoe een unieke health tooapply beleid voor elke service in het toepassingsmanifest Hallo controleren.</span><span class="sxs-lookup"><span data-stu-id="c951b-141">hello following example shows how tooapply a unique health check policy for each service in hello application manifest.</span></span>

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="c951b-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c951b-142">Next steps</span></span>
<span data-ttu-id="c951b-143">Zie voor meer informatie over het implementeren van een toepassing [implementeren van een bestaande toepassing in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="c951b-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>
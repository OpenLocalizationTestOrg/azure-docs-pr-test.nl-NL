---
title: aaaSet van een ontwikkelomgeving voor Azure microservices | Microsoft Docs
description: Installeer Hallo runtime, SDK en hulpprogramma's en maak een lokaal ontwikkelcluster. Na het voltooien van deze installatie, kunt u zich gereed toobuild toepassingen.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="68dd1-104">Uw ontwikkelomgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="68dd1-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="68dd1-105">Windows</span><span class="sxs-lookup"><span data-stu-id="68dd1-105">Windows</span></span>](service-fabric-get-started.md) 
> * [<span data-ttu-id="68dd1-106">Linux</span><span class="sxs-lookup"><span data-stu-id="68dd1-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="68dd1-107">OSX</span><span class="sxs-lookup"><span data-stu-id="68dd1-107">OSX</span></span>](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="68dd1-108">toobuild en voer [Azure Service Fabric-toepassingen] [ 1] installeren op uw ontwikkelcomputer Hallo runtime, SDK en hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="68dd1-108">toobuild and run [Azure Service Fabric applications][1] on your development machine, install hello runtime, SDK, and tools.</span></span> <span data-ttu-id="68dd1-109">U moet ook tooenable uitvoering van Windows PowerShell-scripts Hallo opgenomen in Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="68dd1-109">You also need tooenable execution of hello Windows PowerShell scripts included in hello SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68dd1-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="68dd1-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="68dd1-111">Ondersteunde versies van besturingssystemen</span><span class="sxs-lookup"><span data-stu-id="68dd1-111">Supported operating system versions</span></span>
<span data-ttu-id="68dd1-112">Hallo volgende versies van besturingssystemen worden ondersteund voor ontwikkeling:</span><span class="sxs-lookup"><span data-stu-id="68dd1-112">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="68dd1-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="68dd1-113">Windows 7</span></span>
* <span data-ttu-id="68dd1-114">Windows 8/Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="68dd1-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="68dd1-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="68dd1-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="68dd1-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="68dd1-116">Windows Server 2016</span></span>
* <span data-ttu-id="68dd1-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="68dd1-117">Windows 10</span></span>

> [!NOTE]
> <span data-ttu-id="68dd1-118">Windows 7 bevat standaard alleen Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="68dd1-118">Windows 7 only includes Windows PowerShell 2.0 by default.</span></span> <span data-ttu-id="68dd1-119">Voor Service Fabric PowerShell-cmdlets is PowerShell 3.0 of hoger vereist.</span><span class="sxs-lookup"><span data-stu-id="68dd1-119">Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher.</span></span> <span data-ttu-id="68dd1-120">U kunt [Windows PowerShell 5.0 downloaden] [ powershell5-download] van Hallo Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="68dd1-120">You can [download Windows PowerShell 5.0][powershell5-download] from hello Microsoft Download Center.</span></span>
> 
> 

## <a name="install-hello-sdk-and-tools"></a><span data-ttu-id="68dd1-121">Hallo SDK en hulpprogramma's installeren</span><span class="sxs-lookup"><span data-stu-id="68dd1-121">Install hello SDK and tools</span></span>
### <a name="toouse-visual-studio-2017"></a><span data-ttu-id="68dd1-122">Visual Studio 2017 toouse</span><span class="sxs-lookup"><span data-stu-id="68dd1-122">toouse Visual Studio 2017</span></span>
<span data-ttu-id="68dd1-123">Service Fabric-programma's maken deel uit van de Azure-ontwikkeling en het beheer werkbelasting Hallo in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="68dd1-123">Service Fabric Tools are part of hello Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="68dd1-124">Schakel deze workload in als onderdeel van de Visual Studio-installatie.</span><span class="sxs-lookup"><span data-stu-id="68dd1-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="68dd1-125">Bovendien moet u tooinstall Hallo Microsoft Azure Service Fabric SDK, met behulp van Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="68dd1-125">In addition, you need tooinstall hello Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="68dd1-126">[Hallo Microsoft Azure Service Fabric SDK installeren][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="68dd1-126">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="68dd1-127">toouse Visual Studio 2015 (Visual Studio 2015 Update 2 of hoger vereist)</span><span class="sxs-lookup"><span data-stu-id="68dd1-127">toouse Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="68dd1-128">Service Fabric-hulpprogramma's zijn voor Visual Studio 2015 geïnstalleerd samen met de Hallo SDK, met behulp van Hallo Web Platform Installer:</span><span class="sxs-lookup"><span data-stu-id="68dd1-128">For Visual Studio 2015, Service Fabric tools are installed together with hello SDK, using hello Web Platform Installer:</span></span>

* <span data-ttu-id="68dd1-129">[Hallo Microsoft Azure Service Fabric SDK en hulpprogramma's installeren][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="68dd1-129">[Install hello Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="68dd1-130">Alleen SDK-installatie</span><span class="sxs-lookup"><span data-stu-id="68dd1-130">SDK installation only</span></span>
<span data-ttu-id="68dd1-131">Als u alleen Hallo SDK hoeft, kunt u dit pakket installeren:</span><span class="sxs-lookup"><span data-stu-id="68dd1-131">If you only need hello SDK, you can install this package:</span></span>
* <span data-ttu-id="68dd1-132">[Hallo Microsoft Azure Service Fabric SDK installeren][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="68dd1-132">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="68dd1-133">Hallo huidige versies zijn:</span><span class="sxs-lookup"><span data-stu-id="68dd1-133">hello current versions are:</span></span>
* <span data-ttu-id="68dd1-134">Service Fabric SDK 2.7.198</span><span class="sxs-lookup"><span data-stu-id="68dd1-134">Service Fabric SDK 2.7.198</span></span>
* <span data-ttu-id="68dd1-135">Service Fabric runtime 5.7.198</span><span class="sxs-lookup"><span data-stu-id="68dd1-135">Service Fabric runtime 5.7.198</span></span>
* <span data-ttu-id="68dd1-136">Service Fabric Tools voor Visual Studio 2015 1.7.50721</span><span class="sxs-lookup"><span data-stu-id="68dd1-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span></span>
* <span data-ttu-id="68dd1-137">Visual Studio 2017 Update 2 bevat Service Fabric Tools voor Visual Studio 1.6.20170504</span><span class="sxs-lookup"><span data-stu-id="68dd1-137">Visual Studio 2017 Update 2 includes Service Fabric Tools for Visual Studio 1.6.20170504</span></span>
* <span data-ttu-id="68dd1-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) bevat Service Fabric Tools voor Visual Studio 1.7.20170721</span><span class="sxs-lookup"><span data-stu-id="68dd1-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) includes Service Fabric Tools for Visual Studio 1.7.20170721</span></span>

<span data-ttu-id="68dd1-139">Zie [Ondersteuning voor Service Fabric](service-fabric-support.md) voor een lijst met ondersteunde versies.</span><span class="sxs-lookup"><span data-stu-id="68dd1-139">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="68dd1-140">Uitvoering van PowerShell-script inschakelen</span><span class="sxs-lookup"><span data-stu-id="68dd1-140">Enable PowerShell script execution</span></span>
<span data-ttu-id="68dd1-141">Service Fabric gebruikt Windows PowerShell-scripts om een lokaal ontwikkelcluster te maken en om toepassingen vanuit Visual Studio te implementeren.</span><span class="sxs-lookup"><span data-stu-id="68dd1-141">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="68dd1-142">Standaard worden deze scripts door Windows geblokkeerd zodat ze niet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="68dd1-142">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="68dd1-143">tooenable ze, moet u uw PowerShell-uitvoeringsbeleid wijzigen.</span><span class="sxs-lookup"><span data-stu-id="68dd1-143">tooenable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="68dd1-144">Open PowerShell als beheerder en voert u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="68dd1-144">Open PowerShell as an administrator and enter hello following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="68dd1-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="68dd1-145">Next steps</span></span>
<span data-ttu-id="68dd1-146">Nu u uw ontwikkelingsomgeving hebt ingesteld, kunt u apps ontwikkelen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="68dd1-146">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="68dd1-147">Uw eerste Service Fabric-toepassing in Visual Studio maken</span><span class="sxs-lookup"><span data-stu-id="68dd1-147">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="68dd1-148">Meer informatie over hoe toodeploy en beheren van toepassingen op uw lokale cluster</span><span class="sxs-lookup"><span data-stu-id="68dd1-148">Learn how toodeploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="68dd1-149">Meer informatie over Hallo programming modellen: Reliable Services en Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="68dd1-149">Learn about hello programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="68dd1-150">Bekijk Hallo Service Fabric-codevoorbeelden op GitHub</span><span class="sxs-lookup"><span data-stu-id="68dd1-150">Check out hello Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="68dd1-151">Uw cluster visualiseren door gebruik te maken van Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="68dd1-151">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="68dd1-152">Ga als volgt Hallo Service Fabric learning pad tooget een brede inleiding toohello platform</span><span class="sxs-lookup"><span data-stu-id="68dd1-152">Follow hello Service Fabric learning path tooget a broad introduction toohello platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="68dd1-153">Meer informatie over [ondersteuningsopties voor Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="68dd1-153">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric-campagnepagina"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI-koppeling"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI-koppeling"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI-koppeling"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395

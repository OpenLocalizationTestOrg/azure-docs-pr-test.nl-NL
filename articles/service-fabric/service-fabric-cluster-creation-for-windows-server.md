---
title: aaaCreate zelfstandige Azure Service Fabric-cluster | Microsoft Docs
description: Een Azure Service Fabric-cluster maken op elke computer (fysiek of virtueel) Windows Server, of het lokale of uitgevoerd in een cloud.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="8405b-103">Een zelfstandige cluster met Windows Server maken</span><span class="sxs-lookup"><span data-stu-id="8405b-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="8405b-104">U kunt Azure Service Fabric toocreate Service Fabric-clusters op elke virtuele machines of computers met Windows Server gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8405b-104">You can use Azure Service Fabric toocreate Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="8405b-105">Dit betekent dat u kunt implementeren en Service Fabric-toepassingen uitvoeren in een omgeving die een set met elkaar verbonden computers met Windows Server bevat, worden deze on-premises of bij een cloudprovider.</span><span class="sxs-lookup"><span data-stu-id="8405b-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="8405b-106">Service Fabric bevat een setup-pakket toocreate die service Fabric-clusters Hallo zelfstandig pakket met Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8405b-106">Service Fabric provides a setup package toocreate Service Fabric clusters called hello standalone Windows Server package.</span></span>

<span data-ttu-id="8405b-107">Dit artikel begeleidt u bij Hallo stappen voor het maken van een zelfstandige Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="8405b-107">This article walks you through hello steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="8405b-108">Dit zelfstandige Windows Server-pakket is commercieel beschikbaar en kan worden gebruikt voor productie-implementaties.</span><span class="sxs-lookup"><span data-stu-id="8405b-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="8405b-109">Dit pakket bevat nieuwe Service Fabric-functies die 'in Preview' zijn.</span><span class="sxs-lookup"><span data-stu-id="8405b-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="8405b-110">Schuif naar beneden te'[Preview-functies die zijn opgenomen in dit pakket](#previewfeatures_anchor). "</span><span class="sxs-lookup"><span data-stu-id="8405b-110">Scroll down too"[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="8405b-111">de sectie voor Hallo lijst van Hallo preview-functies.</span><span class="sxs-lookup"><span data-stu-id="8405b-111">section for hello list of hello preview features.</span></span> <span data-ttu-id="8405b-112">U kunt [download een exemplaar van Hallo overeenkomst](http://go.microsoft.com/fwlink/?LinkID=733084) nu.</span><span class="sxs-lookup"><span data-stu-id="8405b-112">You can [download a copy of hello EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="8405b-113">Ondersteuning krijgen voor Hallo Service Fabric voor Windows Server-pakket</span><span class="sxs-lookup"><span data-stu-id="8405b-113">Get support for hello Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="8405b-114">Vraag het Hallo-community over Hallo Service Fabric zelfstandige pakket voor Windows Server in Hallo [Azure Service Fabric-forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span><span class="sxs-lookup"><span data-stu-id="8405b-114">Ask hello community about hello Service Fabric standalone package for Windows Server in hello [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="8405b-115">Open een serviceticket voor [Professional-ondersteuning voor Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span><span class="sxs-lookup"><span data-stu-id="8405b-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="8405b-116">Meer informatie over ondersteuning van Microsoft-professionals [hier](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="8405b-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="8405b-117">U kunt ook ondersteuning voor dit pakket als onderdeel van [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span><span class="sxs-lookup"><span data-stu-id="8405b-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="8405b-118">Zie voor meer informatie [opties voor ondersteuning van Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span><span class="sxs-lookup"><span data-stu-id="8405b-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="8405b-119">toocollect logboeken voor ondersteuning, Voer Hallo [Service Fabric zelfstandige logboekverzamelaar](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="8405b-119">toocollect logs for support purposes, run hello [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="8405b-120">Hallo-Service Fabric voor Windows Server downloaden</span><span class="sxs-lookup"><span data-stu-id="8405b-120">Download hello Service Fabric for Windows Server package</span></span>
<span data-ttu-id="8405b-121">toocreate hello cluster, gebruik Hallo Service Fabric voor Windows Server-pakket (Windows Server 2012 R2 en nieuwer) hier vinden:</span><span class="sxs-lookup"><span data-stu-id="8405b-121">toocreate hello cluster, use hello Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="8405b-122">
[Link - Service Fabric zelfstandige Package - Windows-Server downloaden](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="8405b-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="8405b-123">Meer informatie vinden van inhoud van pakket Hallo [hier](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="8405b-123">Find details on contents of hello package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="8405b-124">Hallo Service Fabric-runtime-pakket is automatisch gedownload tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="8405b-124">hello Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="8405b-125">Als het implementeren van een virtuele machine niet verbonden toohello internet, download Hallo runtime-pakket buiten-bandbeheer van hier:</span><span class="sxs-lookup"><span data-stu-id="8405b-125">If deploying from a machine not connected toohello internet, please download hello runtime package out of band from here:</span></span> <br><span data-ttu-id="8405b-126">
[Link - Service Fabric-Runtime - Windows-Server downloaden](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="8405b-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="8405b-127">Voorbeelden van de zelfstandige configuratie van het Cluster op zoeken:</span><span class="sxs-lookup"><span data-stu-id="8405b-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="8405b-128">
[Voorbeelden van zelfstandige clusterconfiguratie](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="8405b-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a><span data-ttu-id="8405b-129">Hallo-cluster maken</span><span class="sxs-lookup"><span data-stu-id="8405b-129">Create hello cluster</span></span>
<span data-ttu-id="8405b-130">Service Fabric geïmplementeerde tooa één machine ontwikkelcluster kan worden met behulp van Hallo *ClusterConfig.Unsecure.DevCluster.json* bestand in [voorbeelden](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="8405b-130">Service Fabric can be deployed tooa one-machine development cluster by using hello *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="8405b-131">Uitpakken Hallo zelfstandige pakket tooyour machine, kopie Hallo voorbeeld config bestand toohello lokale computer en Voer Hallo *CreateServiceFabricCluster.ps1* script via een beheerder PowerShell-sessie van Hallo zelfstandige Pakketmap:</span><span class="sxs-lookup"><span data-stu-id="8405b-131">Unpack hello standalone package tooyour machine, copy hello sample config file toohello local machine, then run hello *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from hello standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="8405b-132">Stap 1A: een onbeveiligde lokaal ontwikkelcluster maken</span><span class="sxs-lookup"><span data-stu-id="8405b-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="8405b-133">Zie de sectie omgeving in te stellen op Hallo [plannen en voorbereiden van uw implementatie van het cluster](service-fabric-cluster-standalone-deployment-preparation.md) voor de details voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="8405b-133">See hello Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="8405b-134">Als u actieve ontwikkelscenario's hebt voltooid, kunt u Hallo Service Fabric-cluster verwijderen uit de Hallo machine door te verwijzen toosteps in sectie '[verwijderen van een cluster](#removecluster_anchor)'.</span><span class="sxs-lookup"><span data-stu-id="8405b-134">If you're finished running development scenarios, you can remove hello Service Fabric cluster from hello machine by referring toosteps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="8405b-135">Stap 1B: een cluster met meerdere machines maken</span><span class="sxs-lookup"><span data-stu-id="8405b-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="8405b-136">Nadat u hebt doorlopen Hallo plannen en de voorbereidende stappen op gedetailleerde op Hallo onderstaande koppeling, u bent klaar toocreate uw productiecluster met behulp van het configuratiebestand van het cluster.</span><span class="sxs-lookup"><span data-stu-id="8405b-136">After you have gone through hello planning and preparation steps detailed at hello below link, you are ready toocreate your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="8405b-137">
[Plannen en voorbereiden van uw implementatie van het cluster](service-fabric-cluster-standalone-deployment-preparation.md)</span><span class="sxs-lookup"><span data-stu-id="8405b-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="8405b-138">Hallo-configuratiebestand u hebt geschreven door het uitvoeren van Hallo valideren *TestConfiguration.ps1* script vanaf Hallo zelfstandige pakketmap:</span><span class="sxs-lookup"><span data-stu-id="8405b-138">Validate hello configuration file you have written by running hello *TestConfiguration.ps1* script from hello standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="8405b-139">Ziet u uitvoer zoals hieronder.</span><span class="sxs-lookup"><span data-stu-id="8405b-139">You should see output like below.</span></span> <span data-ttu-id="8405b-140">Als Hallo onder veld 'Passed' wordt geretourneerd als 'True', bevestigingen hebt doorgegeven en Hallo cluster lijkt toobe geïmplementeerd op basis van invoer Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="8405b-140">If hello bottom field "Passed" is returned as "True", sanity checks have passed and hello cluster looks toobe deployable based on hello input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
    Running Best Practices Analyzer...
    Best Practices Analyzer completed successfully.
    
    LocalAdminPrivilege        : True
    IsJsonValid                : True
    IsCabValid                 : True
    RequiredPortsOpen          : True
    RemoteRegistryAvailable    : True
    FirewallAvailable          : True
    RpcCheckPassed             : True
    NoConflictingInstallations : True
    FabricInstallable          : True
    Passed                     : True
    ```

2. <span data-ttu-id="8405b-141">Hallo-cluster maken: Hallo uitvoeren *CreateServiceFabricCluster.ps1* script toodeploy Hallo Service Fabric-cluster op elke computer in Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="8405b-141">Create hello cluster:  Run hello *CreateServiceFabricCluster.ps1* script toodeploy hello Service Fabric cluster across each machine in hello configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="8405b-142">Implementatie traceringen worden geschreven toohello VM/machine waarop u Hallo CreateServiceFabricCluster.ps1 PowerShell-script is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8405b-142">Deployment traces are written toohello VM/machine on which you ran hello CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="8405b-143">U vindt deze in Hallo submap DeploymentTraces, op basis van Hallo directory van welke Hallo script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8405b-143">These can be found in hello subfolder DeploymentTraces, based in hello directory from which hello script was run.</span></span> <span data-ttu-id="8405b-144">toosee als Service Fabric is correct is geïmplementeerd tooa machine, Hallo geïnstalleerd bestanden gevonden in de directory van het Hallo FabricDataRoot, zoals beschreven in het configuratiebestand voor Hallo cluster FabricSettings sectie (met standaard c:\ProgramData\SF).</span><span class="sxs-lookup"><span data-stu-id="8405b-144">toosee if Service Fabric was deployed correctly tooa machine, find hello installed files in hello FabricDataRoot directory, as detailed in hello cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="8405b-145">FabricHost.exe en Fabric.exe processen kunnen ook worden gezien uitgevoerd in Taakbeheer.</span><span class="sxs-lookup"><span data-stu-id="8405b-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="8405b-146">Stap 1C: een offline (op internet verbroken)-cluster maken</span><span class="sxs-lookup"><span data-stu-id="8405b-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="8405b-147">Hallo Service Fabric-runtime-pakket wordt automatisch bij het maken van het cluster gedownload.</span><span class="sxs-lookup"><span data-stu-id="8405b-147">hello Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="8405b-148">Wanneer het implementeren van een cluster toomachines niet toohello verbonden internet, moet u toodownload Hallo Service Fabric runtime afzonderlijk pakket en bieden Hallo pad tooit bij het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="8405b-148">When deploying a cluster toomachines not connected toohello internet, you will need toodownload hello Service Fabric runtime package separately, and provide hello path tooit at cluster creation.</span></span>
<span data-ttu-id="8405b-149">Hallo runtime-pakket kan afzonderlijk worden gedownload, vanaf een andere computer verbonden toohello internet, op [- Service Fabric-Runtime - koppeling Download Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span><span class="sxs-lookup"><span data-stu-id="8405b-149">hello runtime package can be downloaded separately, from another machine connected toohello internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="8405b-150">Kopieer Hallo runtime pakket toowhere u implementeert Hallo offline cluster uit en Hallo cluster maken door het uitvoeren van `CreateServiceFabricCluster.ps1` Hello `-FabricRuntimePackagePath` parameter opgenomen, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="8405b-150">Copy hello runtime package toowhere you are deploying hello offline cluster from, and create hello cluster by running `CreateServiceFabricCluster.ps1` with hello `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="8405b-151">waar `.\ClusterConfig.json` en `.\MicrosoftAzureServiceFabric.cab` zijn respectievelijk Hallo paden toohello clusterconfiguratie en Hallo runtime CAB-bestand.</span><span class="sxs-lookup"><span data-stu-id="8405b-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are hello paths toohello cluster configuration and hello runtime .cab file respectively.</span></span>


### <a name="step-2-connect-toohello-cluster"></a><span data-ttu-id="8405b-152">Stap 2: Verbinding maken met cluster toohello</span><span class="sxs-lookup"><span data-stu-id="8405b-152">Step 2: Connect toohello cluster</span></span>
<span data-ttu-id="8405b-153">tooconnect tooa beveiligde cluster, Zie [Service fabric-cluster toosecure verbinding](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="8405b-153">tooconnect tooa secure cluster, see [Service fabric connect toosecure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="8405b-154">tooconnect tooan onbeveiligde cluster Hallo volgende PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8405b-154">tooconnect tooan unsecure cluster, run hello following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="8405b-155">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8405b-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="8405b-156">Stap 3: Online zetten van de Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="8405b-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="8405b-157">Nu u toohello cluster verbinding met Service Fabric Explorer vanuit een van de machines Hallo http://localhost:19080/Explorer/index.html of op afstand met http://&lt maken kunt;*IPAddressofaMachine*>: 19080 / Explorer/index.HTML.</span><span class="sxs-lookup"><span data-stu-id="8405b-157">Now you can connect toohello cluster with Service Fabric Explorer either directly from one of hello machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="8405b-158">Toevoegen en verwijderen van knooppunten</span><span class="sxs-lookup"><span data-stu-id="8405b-158">Add and remove nodes</span></span>
<span data-ttu-id="8405b-159">U kunt toevoegen of verwijderen van knooppunten tooyour zelfstandige Service Fabric-cluster als uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="8405b-159">You can add or remove nodes tooyour standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="8405b-160">Zie [toevoegen of verwijderen van knooppunten tooa Service Fabric-cluster voor zelfstandige](service-fabric-cluster-windows-server-add-remove-nodes.md) voor gedetailleerde stappen.</span><span class="sxs-lookup"><span data-stu-id="8405b-160">See [Add or Remove nodes tooa Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="8405b-161">Verwijderen van een cluster</span><span class="sxs-lookup"><span data-stu-id="8405b-161">Remove a cluster</span></span>
<span data-ttu-id="8405b-162">tooremove een cluster uitvoert Hallo *RemoveServiceFabricCluster.ps1* PowerShell-script van de pakketmap Hallo en geeft u Hallo pad toohello JSON-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="8405b-162">tooremove a cluster, run hello *RemoveServiceFabricCluster.ps1* PowerShell script from hello package folder and pass in hello path toohello JSON configuration file.</span></span> <span data-ttu-id="8405b-163">U kunt optioneel een locatie voor Hallo logboek van Hallo verwijdering opgeven.</span><span class="sxs-lookup"><span data-stu-id="8405b-163">You can optionally specify a location for hello log of hello deletion.</span></span>

<span data-ttu-id="8405b-164">Dit script kan worden uitgevoerd op een machine met de beheerder toegang tooall Hallo machines die worden vermeld als knooppunten in het configuratiebestand Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="8405b-164">This script can be run on any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster configuration file.</span></span> <span data-ttu-id="8405b-165">Hallo-machine die op dit script wordt uitgevoerd heeft geen toobe onderdeel van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="8405b-165">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a><span data-ttu-id="8405b-166">Telemetrische gegevens verzameld en hoe tooopt buiten het</span><span class="sxs-lookup"><span data-stu-id="8405b-166">Telemetry data collected and how tooopt out of it</span></span>
<span data-ttu-id="8405b-167">Standaard verzamelt Hallo product telemetrie op Hallo Service Fabric-gebruik tooimprove Hallo product.</span><span class="sxs-lookup"><span data-stu-id="8405b-167">As a default, hello product collects telemetry on hello Service Fabric usage tooimprove hello product.</span></span> <span data-ttu-id="8405b-168">Hallo Best Practices Analyzer die wordt uitgevoerd als een deel van Hallo setup voor connectiviteit te controleert[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span><span class="sxs-lookup"><span data-stu-id="8405b-168">hello Best Practice Analyzer that runs as a part of hello setup checks for connectivity too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="8405b-169">Als dit niet bereikbaar is, mislukt de installatie van de Hallo tenzij u telemetrie afmelden.</span><span class="sxs-lookup"><span data-stu-id="8405b-169">If it is not reachable, hello setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="8405b-170">Hallo telemetrie pijplijn probeert tooupload Hallo gegevens te volgen[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) eenmaal voor elke dag.</span><span class="sxs-lookup"><span data-stu-id="8405b-170">hello telemetry pipeline tries tooupload hello following data too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="8405b-171">Het uploaden van een best effort is en heeft geen invloed op Hallo clusterfunctionaliteit.</span><span class="sxs-lookup"><span data-stu-id="8405b-171">It is a best-effort upload and has no impact on hello cluster functionality.</span></span> <span data-ttu-id="8405b-172">Hallo telemetrie wordt alleen verzonden van het Hallo-knooppunt dat wordt uitgevoerd failover manager primaire Hallo.</span><span class="sxs-lookup"><span data-stu-id="8405b-172">hello telemetry is only sent from hello node that runs hello failover manager primary.</span></span> <span data-ttu-id="8405b-173">Er zijn geen andere knooppunten verzenden telemetrie.</span><span class="sxs-lookup"><span data-stu-id="8405b-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="8405b-174">Hallo telemetrie bestaat uit Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="8405b-174">hello telemetry consists of hello following:</span></span>

* <span data-ttu-id="8405b-175">Aantal services</span><span class="sxs-lookup"><span data-stu-id="8405b-175">Number of services</span></span>
* <span data-ttu-id="8405b-176">Aantal ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="8405b-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="8405b-177">Aantal toepassingen</span><span class="sxs-lookup"><span data-stu-id="8405b-177">Number of Applications</span></span>
* <span data-ttu-id="8405b-178">Aantal ApplicationUpgrades</span><span class="sxs-lookup"><span data-stu-id="8405b-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="8405b-179">Aantal FailoverUnits</span><span class="sxs-lookup"><span data-stu-id="8405b-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="8405b-180">Aantal InBuildFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="8405b-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="8405b-181">Aantal UnhealthyFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="8405b-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="8405b-182">Aantal replica 's</span><span class="sxs-lookup"><span data-stu-id="8405b-182">Number of Replicas</span></span>
* <span data-ttu-id="8405b-183">Aantal InBuildReplicas</span><span class="sxs-lookup"><span data-stu-id="8405b-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="8405b-184">Aantal StandByReplicas</span><span class="sxs-lookup"><span data-stu-id="8405b-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="8405b-185">Aantal OfflineReplicas</span><span class="sxs-lookup"><span data-stu-id="8405b-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="8405b-186">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="8405b-186">CommonQueueLength</span></span>
* <span data-ttu-id="8405b-187">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="8405b-187">QueryQueueLength</span></span>
* <span data-ttu-id="8405b-188">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="8405b-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="8405b-189">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="8405b-189">CommitQueueLength</span></span>
* <span data-ttu-id="8405b-190">Het aantal knooppunten</span><span class="sxs-lookup"><span data-stu-id="8405b-190">Number of Nodes</span></span>
* <span data-ttu-id="8405b-191">IsContextComplete: True/False</span><span class="sxs-lookup"><span data-stu-id="8405b-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="8405b-192">ClusterId: Dit is een willekeurig gegenereerd voor elk cluster GUID</span><span class="sxs-lookup"><span data-stu-id="8405b-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="8405b-193">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="8405b-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="8405b-194">IP-adres van Hallo of machine uit welke Hallo telemetrie is geüpload</span><span class="sxs-lookup"><span data-stu-id="8405b-194">IP address of hello virtual machine or machine from which hello telemetry is uploaded</span></span>

<span data-ttu-id="8405b-195">toodisable-telemetrie hello te volgende toevoegen*eigenschappen* in uw cluster-config: *enableTelemetry: false*.</span><span class="sxs-lookup"><span data-stu-id="8405b-195">toodisable telemetry, add hello following too*properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="8405b-196">Preview-functies die zijn opgenomen in dit pakket</span><span class="sxs-lookup"><span data-stu-id="8405b-196">Preview features included in this package</span></span>
<span data-ttu-id="8405b-197">Geen.</span><span class="sxs-lookup"><span data-stu-id="8405b-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="8405b-198">Beginnen met nieuwe Hallo [GA-versie van Hallo zelfstandige cluster voor Windows Server (versie 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), kunt u uw cluster toofuture versies upgraden handmatig of automatisch.</span><span class="sxs-lookup"><span data-stu-id="8405b-198">Starting with hello new [GA version of hello standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster toofuture releases, manually or automatically.</span></span> <span data-ttu-id="8405b-199">Raadpleeg te[upgraden van een zelfstandige Service Fabric-cluster versie](service-fabric-cluster-upgrade-windows-server.md) document voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8405b-199">Refer too[Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8405b-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8405b-200">Next steps</span></span>
* [<span data-ttu-id="8405b-201">Implementeren en verwijderen van toepassingen met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="8405b-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="8405b-202">Configuratie-instellingen voor zelfstandige Windows-cluster</span><span class="sxs-lookup"><span data-stu-id="8405b-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="8405b-203">Toevoegen of verwijderen van knooppunten tooa zelfstandige Service Fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="8405b-203">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="8405b-204">Een zelfstandige Service Fabric-cluster versie upgraden</span><span class="sxs-lookup"><span data-stu-id="8405b-204">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="8405b-205">Een zelfstandige Service Fabric-cluster maken met Azure Virtual machines waarop Windows wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="8405b-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="8405b-206">Beveiligen van een zelfstandige cluster op Windows met behulp van Windows-beveiliging</span><span class="sxs-lookup"><span data-stu-id="8405b-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="8405b-207">Beveiligen van een zelfstandige cluster op Windows met behulp van X509 certificaten</span><span class="sxs-lookup"><span data-stu-id="8405b-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png

---
title: Een zelfstandige Azure Service Fabric-cluster maken | Microsoft Docs
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
ms.openlocfilehash: 6aa2905a97ec6b8c125f2ab9572a8e40bf525b27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="e8d7f-103">Een zelfstandige cluster met Windows Server maken</span><span class="sxs-lookup"><span data-stu-id="e8d7f-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="e8d7f-104">U kunt Azure Service Fabric gebruiken voor het maken van Service Fabric-clusters op alle virtuele machines of de computers waarop Windows Server wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-104">You can use Azure Service Fabric to create Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="e8d7f-105">Dit betekent dat u kunt implementeren en Service Fabric-toepassingen uitvoeren in een omgeving die een set met elkaar verbonden computers met Windows Server bevat, worden deze on-premises of bij een cloudprovider.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="e8d7f-106">Service Fabric bevat een installatiepakket voor het maken van Service Fabric-clusters die het zelfstandige pakket met Windows Server genoemd.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-106">Service Fabric provides a setup package to create Service Fabric clusters called the standalone Windows Server package.</span></span>

<span data-ttu-id="e8d7f-107">Dit artikel begeleidt u bij de stappen voor het maken van een zelfstandige Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-107">This article walks you through the steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="e8d7f-108">Dit zelfstandige Windows Server-pakket is commercieel beschikbaar en kan worden gebruikt voor productie-implementaties.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="e8d7f-109">Dit pakket bevat nieuwe Service Fabric-functies die 'in Preview' zijn.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="e8d7f-110">Schuif omlaag naar '[Preview-functies die zijn opgenomen in dit pakket](#previewfeatures_anchor). "</span><span class="sxs-lookup"><span data-stu-id="e8d7f-110">Scroll down to "[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="e8d7f-111">de sectie voor een lijst van de preview-functies.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-111">section for the list of the preview features.</span></span> <span data-ttu-id="e8d7f-112">U kunt [download een exemplaar van de gebruiksrechtovereenkomst](http://go.microsoft.com/fwlink/?LinkID=733084) nu.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-112">You can [download a copy of the EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-the-service-fabric-for-windows-server-package"></a><span data-ttu-id="e8d7f-113">Ondersteuning voor het Service Fabric voor Windows Server-pakket</span><span class="sxs-lookup"><span data-stu-id="e8d7f-113">Get support for the Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="e8d7f-114">De community vragen over de zelfstandige Service Fabric-pakket voor Windows-Server in de [Azure Service Fabric-forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span><span class="sxs-lookup"><span data-stu-id="e8d7f-114">Ask the community about the Service Fabric standalone package for Windows Server in the [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="e8d7f-115">Open een serviceticket voor [Professional-ondersteuning voor Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span><span class="sxs-lookup"><span data-stu-id="e8d7f-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="e8d7f-116">Meer informatie over ondersteuning van Microsoft-professionals [hier](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="e8d7f-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="e8d7f-117">U kunt ook ondersteuning voor dit pakket als onderdeel van [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span><span class="sxs-lookup"><span data-stu-id="e8d7f-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="e8d7f-118">Zie voor meer informatie [opties voor ondersteuning van Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span><span class="sxs-lookup"><span data-stu-id="e8d7f-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="e8d7f-119">Uitvoeren voor het verzamelen van Logboeken ter ondersteuning van de [Service Fabric zelfstandige logboekverzamelaar](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="e8d7f-119">To collect logs for support purposes, run the [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-the-service-fabric-for-windows-server-package"></a><span data-ttu-id="e8d7f-120">De Service Fabric voor Windows Server downloaden</span><span class="sxs-lookup"><span data-stu-id="e8d7f-120">Download the Service Fabric for Windows Server package</span></span>
<span data-ttu-id="e8d7f-121">Voor het maken van het cluster gebruikt het Service Fabric voor Windows Server-pakket (Windows Server 2012 R2 en nieuwer) hier vinden:</span><span class="sxs-lookup"><span data-stu-id="e8d7f-121">To create the cluster, use the Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="e8d7f-122">
[Link - Service Fabric zelfstandige Package - Windows-Server downloaden](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="e8d7f-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="e8d7f-123">Meer informatie vinden van inhoud van het pakket [hier](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="e8d7f-123">Find details on contents of the package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="e8d7f-124">Het Service Fabric-runtime-pakket is automatisch gedownload tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-124">The Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="e8d7f-125">Als het implementeren van een virtuele machine niet is verbonden met internet, download u het pakket runtime buiten-band van hier:</span><span class="sxs-lookup"><span data-stu-id="e8d7f-125">If deploying from a machine not connected to the internet, please download the runtime package out of band from here:</span></span> <br><span data-ttu-id="e8d7f-126">
[Link - Service Fabric-Runtime - Windows-Server downloaden](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="e8d7f-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="e8d7f-127">Voorbeelden van de zelfstandige configuratie van het Cluster op zoeken:</span><span class="sxs-lookup"><span data-stu-id="e8d7f-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="e8d7f-128">
[Voorbeelden van zelfstandige clusterconfiguratie](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="e8d7f-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-the-cluster"></a><span data-ttu-id="e8d7f-129">Het cluster maken</span><span class="sxs-lookup"><span data-stu-id="e8d7f-129">Create the cluster</span></span>
<span data-ttu-id="e8d7f-130">Service Fabric kan worden geïmplementeerd naar een cluster met één machine ontwikkeling met behulp van de *ClusterConfig.Unsecure.DevCluster.json* bestand in [voorbeelden](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="e8d7f-130">Service Fabric can be deployed to a one-machine development cluster by using the *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="e8d7f-131">Uitpakken van het pakket zelfstandige naar uw computer, het voorbeeldbestand config kopiëren naar de lokale computer en voer vervolgens de *CreateServiceFabricCluster.ps1* script via een PowerShell-sessie van de beheerder van de pakketmap zelfstandige:</span><span class="sxs-lookup"><span data-stu-id="e8d7f-131">Unpack the standalone package to your machine, copy the sample config file to the local machine, then run the *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from the standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="e8d7f-132">Stap 1A: een onbeveiligde lokaal ontwikkelcluster maken</span><span class="sxs-lookup"><span data-stu-id="e8d7f-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="e8d7f-133">Zie de sectie omgeving in te stellen op [plannen en voorbereiden van uw implementatie van het cluster](service-fabric-cluster-standalone-deployment-preparation.md) voor de details voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-133">See the Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="e8d7f-134">Als u actieve ontwikkelscenario's hebt voltooid, kunt u de Service Fabric-cluster verwijderen van de machine met een verwijzing naar de stappen in de sectie '[verwijderen van een cluster](#removecluster_anchor)'.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-134">If you're finished running development scenarios, you can remove the Service Fabric cluster from the machine by referring to steps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="e8d7f-135">Stap 1B: een cluster met meerdere machines maken</span><span class="sxs-lookup"><span data-stu-id="e8d7f-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="e8d7f-136">Nadat u hebt doorlopen de planning en de voorbereidende stappen op gedetailleerde op de onderstaande koppeling, bent u klaar om uw productiecluster met behulp van het configuratiebestand van de cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-136">After you have gone through the planning and preparation steps detailed at the below link, you are ready to create your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="e8d7f-137">
[Plannen en voorbereiden van uw implementatie van het cluster](service-fabric-cluster-standalone-deployment-preparation.md)</span><span class="sxs-lookup"><span data-stu-id="e8d7f-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="e8d7f-138">Valideren van het configuratiebestand dat u hebt geschreven door het uitvoeren van de *TestConfiguration.ps1* script van de pakketmap zelfstandige:</span><span class="sxs-lookup"><span data-stu-id="e8d7f-138">Validate the configuration file you have written by running the *TestConfiguration.ps1* script from the standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="e8d7f-139">Ziet u uitvoer zoals hieronder.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-139">You should see output like below.</span></span> <span data-ttu-id="e8d7f-140">Het veld onder is 'Doorgegeven' geretourneerd als 'True', zijn geslaagd voor bevestigingen en het cluster gecontroleerd worden geïmplementeerd op basis van de configuratie van de invoer.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-140">If the bottom field "Passed" is returned as "True", sanity checks have passed and the cluster looks to be deployable based on the input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written to existing trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
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

2. <span data-ttu-id="e8d7f-141">Maken van het cluster: Voer de *CreateServiceFabricCluster.ps1* script voor het implementeren van de Service Fabric-cluster op elke computer in de configuratie.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-141">Create the cluster:  Run the *CreateServiceFabricCluster.ps1* script to deploy the Service Fabric cluster across each machine in the configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="e8d7f-142">Implementatie traceringen worden geschreven naar de virtuele machine/machine waarop u het CreateServiceFabricCluster.ps1 PowerShell-script is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-142">Deployment traces are written to the VM/machine on which you ran the CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="e8d7f-143">U vindt deze in de submap DeploymentTraces, op basis van de map van waaruit het script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-143">These can be found in the subfolder DeploymentTraces, based in the directory from which the script was run.</span></span> <span data-ttu-id="e8d7f-144">Als u wilt zien als Service Fabric correct is geïmplementeerd op een computer, de geïnstalleerde bestanden niet vinden in de map FabricDataRoot, zoals beschreven in het configuratiebestand van het cluster FabricSettings sectie (met standaard c:\ProgramData\SF).</span><span class="sxs-lookup"><span data-stu-id="e8d7f-144">To see if Service Fabric was deployed correctly to a machine, find the installed files in the FabricDataRoot directory, as detailed in the cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="e8d7f-145">FabricHost.exe en Fabric.exe processen kunnen ook worden gezien uitgevoerd in Taakbeheer.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="e8d7f-146">Stap 1C: een offline (op internet verbroken)-cluster maken</span><span class="sxs-lookup"><span data-stu-id="e8d7f-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="e8d7f-147">Het Service Fabric-runtime-pakket wordt automatisch bij het maken van het cluster gedownload.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-147">The Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="e8d7f-148">Wanneer u een cluster implementeert op computers die niet is verbonden met internet, moet u het Service Fabric-runtime-pakket afzonderlijk downloaden en geef het pad naar het bij het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-148">When deploying a cluster to machines not connected to the internet, you will need to download the Service Fabric runtime package separately, and provide the path to it at cluster creation.</span></span>
<span data-ttu-id="e8d7f-149">Het pakket runtime kan afzonderlijk worden gedownload vanaf een andere computer is verbonden met internet, op [- Service Fabric-Runtime - koppeling Download Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span><span class="sxs-lookup"><span data-stu-id="e8d7f-149">The runtime package can be downloaded separately, from another machine connected to the internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="e8d7f-150">De runtime-pakket kopiëren naar waar u implementeert het offline cluster uit en het cluster maken door het uitvoeren van `CreateServiceFabricCluster.ps1` met de `-FabricRuntimePackagePath` parameter opgenomen, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e8d7f-150">Copy the runtime package to where you are deploying the offline cluster from, and create the cluster by running `CreateServiceFabricCluster.ps1` with the `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="e8d7f-151">waar `.\ClusterConfig.json` en `.\MicrosoftAzureServiceFabric.cab` respectievelijk de paden naar de clusterconfiguratie en het runtime CAB-bestand zijn.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are the paths to the cluster configuration and the runtime .cab file respectively.</span></span>


### <a name="step-2-connect-to-the-cluster"></a><span data-ttu-id="e8d7f-152">Stap 2: Verbinding maken met het cluster</span><span class="sxs-lookup"><span data-stu-id="e8d7f-152">Step 2: Connect to the cluster</span></span>
<span data-ttu-id="e8d7f-153">Zie voor verbinding met een beveiligde cluster, [Service fabric verbinding maken met veilige cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e8d7f-153">To connect to a secure cluster, see [Service fabric connect to secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="e8d7f-154">Voor verbinding met een niet-beveiligde cluster, moet u de volgende PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e8d7f-154">To connect to an unsecure cluster, run the following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="e8d7f-155">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e8d7f-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="e8d7f-156">Stap 3: Online zetten van de Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="e8d7f-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="e8d7f-157">Nu u verbinding met het cluster met Service Fabric Explorer vanuit een van de machines http://localhost:19080/Explorer/index.html of op afstand met http://&lt maken kunt;*IPAddressofaMachine*>: 19080/Explorer/index.html.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-157">Now you can connect to the cluster with Service Fabric Explorer either directly from one of the machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="e8d7f-158">Toevoegen en verwijderen van knooppunten</span><span class="sxs-lookup"><span data-stu-id="e8d7f-158">Add and remove nodes</span></span>
<span data-ttu-id="e8d7f-159">U kunt toevoegen of knooppunten aan uw zelfstandige Service Fabric-cluster verwijderen als uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-159">You can add or remove nodes to your standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="e8d7f-160">Zie [toevoegen of verwijderen van knooppunten aan een zelfstandige Service Fabric-cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) voor gedetailleerde stappen.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-160">See [Add or Remove nodes to a Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="e8d7f-161">Verwijderen van een cluster</span><span class="sxs-lookup"><span data-stu-id="e8d7f-161">Remove a cluster</span></span>
<span data-ttu-id="e8d7f-162">Als u een cluster wilt verwijderen, voert u het PowerShell-script *RemoveServiceFabricCluster.ps1* uit vanuit de pakketmap en geeft u daarbij het pad op naar het JSON-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-162">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span></span> <span data-ttu-id="e8d7f-163">Optioneel kunt u een locatie voor het verwijderingslogboek opgeven.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-163">You can optionally specify a location for the log of the deletion.</span></span>

<span data-ttu-id="e8d7f-164">Dit script kan worden uitgevoerd op een machine met beheerdersrechten op alle machines die worden vermeld als knooppunten in het configuratiebestand van het cluster.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-164">This script can be run on any machine that has administrator access to all the machines that are listed as nodes in the cluster configuration file.</span></span> <span data-ttu-id="e8d7f-165">Dit script wordt uitgevoerd op de machine geen deel uitmaken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-165">The machine that this script is run on does not have to be part of the cluster.</span></span>

```
# Removes Service Fabric from each machine in the configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from the current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-to-opt-out-of-it"></a><span data-ttu-id="e8d7f-166">Telemetrische gegevens verzameld en hoe deze afmelden</span><span class="sxs-lookup"><span data-stu-id="e8d7f-166">Telemetry data collected and how to opt out of it</span></span>
<span data-ttu-id="e8d7f-167">Standaard verzamelt het product telemetrie van de Service Fabric-gebruik voor het verbeteren van het product.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-167">As a default, the product collects telemetry on the Service Fabric usage to improve the product.</span></span> <span data-ttu-id="e8d7f-168">De Best Practices Analyzer die wordt uitgevoerd als onderdeel van het installatieprogramma controleert voor connectiviteit met [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span><span class="sxs-lookup"><span data-stu-id="e8d7f-168">The Best Practice Analyzer that runs as a part of the setup checks for connectivity to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="e8d7f-169">Als dit niet bereikbaar is, wordt de installatie mislukt, tenzij u telemetrie afmelden.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-169">If it is not reachable, the setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="e8d7f-170">De pijplijn telemetrie probeert te uploaden van de volgende gegevens op [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) eenmaal voor elke dag.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-170">The telemetry pipeline tries to upload the following data to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="e8d7f-171">Het uploaden van een best effort is en heeft geen invloed op de clusterfunctionaliteit.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-171">It is a best-effort upload and has no impact on the cluster functionality.</span></span> <span data-ttu-id="e8d7f-172">De telemetrie alleen wordt verzonden via het knooppunt waarop de failover manager primaire.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-172">The telemetry is only sent from the node that runs the failover manager primary.</span></span> <span data-ttu-id="e8d7f-173">Er zijn geen andere knooppunten verzenden telemetrie.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="e8d7f-174">De telemetrie bestaat uit het volgende:</span><span class="sxs-lookup"><span data-stu-id="e8d7f-174">The telemetry consists of the following:</span></span>

* <span data-ttu-id="e8d7f-175">Aantal services</span><span class="sxs-lookup"><span data-stu-id="e8d7f-175">Number of services</span></span>
* <span data-ttu-id="e8d7f-176">Aantal ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="e8d7f-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="e8d7f-177">Aantal toepassingen</span><span class="sxs-lookup"><span data-stu-id="e8d7f-177">Number of Applications</span></span>
* <span data-ttu-id="e8d7f-178">Aantal ApplicationUpgrades</span><span class="sxs-lookup"><span data-stu-id="e8d7f-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="e8d7f-179">Aantal FailoverUnits</span><span class="sxs-lookup"><span data-stu-id="e8d7f-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="e8d7f-180">Aantal InBuildFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="e8d7f-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="e8d7f-181">Aantal UnhealthyFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="e8d7f-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="e8d7f-182">Aantal replica 's</span><span class="sxs-lookup"><span data-stu-id="e8d7f-182">Number of Replicas</span></span>
* <span data-ttu-id="e8d7f-183">Aantal InBuildReplicas</span><span class="sxs-lookup"><span data-stu-id="e8d7f-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="e8d7f-184">Aantal StandByReplicas</span><span class="sxs-lookup"><span data-stu-id="e8d7f-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="e8d7f-185">Aantal OfflineReplicas</span><span class="sxs-lookup"><span data-stu-id="e8d7f-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="e8d7f-186">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="e8d7f-186">CommonQueueLength</span></span>
* <span data-ttu-id="e8d7f-187">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="e8d7f-187">QueryQueueLength</span></span>
* <span data-ttu-id="e8d7f-188">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="e8d7f-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="e8d7f-189">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="e8d7f-189">CommitQueueLength</span></span>
* <span data-ttu-id="e8d7f-190">Het aantal knooppunten</span><span class="sxs-lookup"><span data-stu-id="e8d7f-190">Number of Nodes</span></span>
* <span data-ttu-id="e8d7f-191">IsContextComplete: True/False</span><span class="sxs-lookup"><span data-stu-id="e8d7f-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="e8d7f-192">ClusterId: Dit is een willekeurig gegenereerd voor elk cluster GUID</span><span class="sxs-lookup"><span data-stu-id="e8d7f-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="e8d7f-193">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="e8d7f-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="e8d7f-194">IP-adres van de virtuele machine of de computer van waaruit de telemetrie is geüpload</span><span class="sxs-lookup"><span data-stu-id="e8d7f-194">IP address of the virtual machine or machine from which the telemetry is uploaded</span></span>

<span data-ttu-id="e8d7f-195">Als u wilt uitschakelen telemetrie, het volgende toevoegen aan *eigenschappen* in uw cluster-config: *enableTelemetry: false*.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-195">To disable telemetry, add the following to *properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="e8d7f-196">Preview-functies die zijn opgenomen in dit pakket</span><span class="sxs-lookup"><span data-stu-id="e8d7f-196">Preview features included in this package</span></span>
<span data-ttu-id="e8d7f-197">Geen.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="e8d7f-198">Beginnen met de nieuwe [GA-versie van het cluster zelfstandige voor Windows Server (versie 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), kunt u uw cluster upgraden naar toekomstige releases handmatig of automatisch.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-198">Starting with the new [GA version of the standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster to future releases, manually or automatically.</span></span> <span data-ttu-id="e8d7f-199">Raadpleeg [upgraden van een zelfstandige Service Fabric-cluster versie](service-fabric-cluster-upgrade-windows-server.md) document voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e8d7f-199">Refer to [Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e8d7f-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e8d7f-200">Next steps</span></span>
* [<span data-ttu-id="e8d7f-201">Implementeren en verwijderen van toepassingen met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8d7f-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="e8d7f-202">Configuratie-instellingen voor zelfstandige Windows-cluster</span><span class="sxs-lookup"><span data-stu-id="e8d7f-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="e8d7f-203">Toevoegen of verwijderen van knooppunten aan een zelfstandige Service Fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="e8d7f-203">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="e8d7f-204">Een zelfstandige Service Fabric-cluster versie upgraden</span><span class="sxs-lookup"><span data-stu-id="e8d7f-204">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="e8d7f-205">Een zelfstandige Service Fabric-cluster maken met Azure Virtual machines waarop Windows wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="e8d7f-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="e8d7f-206">Beveiligen van een zelfstandige cluster op Windows met behulp van Windows-beveiliging</span><span class="sxs-lookup"><span data-stu-id="e8d7f-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="e8d7f-207">Beveiligen van een zelfstandige cluster op Windows met behulp van X509 certificaten</span><span class="sxs-lookup"><span data-stu-id="e8d7f-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png

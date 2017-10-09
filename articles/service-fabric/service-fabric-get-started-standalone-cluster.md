---
title: aaaSet een zelfstandige Azure Service Fabric-cluster | Microsoft Docs
description: Maken van een zelfstandige ontwikkelcluster met drie knooppunten uitgevoerd op Hallo dezelfde computer. Na het voltooien van deze installatie, kunt u zich gereed toocreate cluster met meerdere machines.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: e4d0ea9fc3b8475160bd8ed19fd3716463791cc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a><span data-ttu-id="d2b79-104">Uw eerste zelfstandige Service Fabric-cluster maken</span><span class="sxs-lookup"><span data-stu-id="d2b79-104">Create your first Service Fabric standalone cluster</span></span>
<span data-ttu-id="d2b79-105">U kunt een zelfstandige Service Fabric-cluster maken op elke virtuele machines of computers waarop Windows Server 2012 R2 of Windows Server 2016, lokaal of in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="d2b79-105">You can create a Service Fabric standalone cluster on any virtual machines or computers running Windows Server 2012 R2 or Windows Server 2016, on-premises or in hello cloud.</span></span> <span data-ttu-id="d2b79-106">Deze snelstartgids kunt u een zelfstandige ontwikkelcluster toocreate in slechts enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="d2b79-106">This quickstart helps you toocreate a development standalone cluster in just a few minutes.</span></span>  <span data-ttu-id="d2b79-107">Wanneer u klaar bent, hebt u een cluster met drie knooppunten die worden uitgevoerd op één computer. Hierop kunt u vervolgens apps implementeren.</span><span class="sxs-lookup"><span data-stu-id="d2b79-107">When you're finished, you have a three-node cluster running on a single computer that you can deploy apps to.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d2b79-108">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="d2b79-108">Before you begin</span></span>
<span data-ttu-id="d2b79-109">Service Fabric bevat een setup-pakket toocreate Service Fabric zelfstandige clusters.</span><span class="sxs-lookup"><span data-stu-id="d2b79-109">Service Fabric provides a setup package toocreate Service Fabric standalone clusters.</span></span>  <span data-ttu-id="d2b79-110">[Hallo-installatiepakket downloaden](http://go.microsoft.com/fwlink/?LinkId=730690).</span><span class="sxs-lookup"><span data-stu-id="d2b79-110">[Download hello setup package](http://go.microsoft.com/fwlink/?LinkId=730690).</span></span>  <span data-ttu-id="d2b79-111">Pak Hallo setup tooa pakketmap op Hallo computer of virtuele machine waar u Hallo ontwikkelcluster instelt.</span><span class="sxs-lookup"><span data-stu-id="d2b79-111">Unzip hello setup package tooa folder on hello computer or virtual machine where you are setting up hello development cluster.</span></span>  <span data-ttu-id="d2b79-112">Hallo-inhoud van het Hallo-installatiepakket worden gedetailleerd beschreven [hier](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="d2b79-112">hello contents of hello setup package are described in detail [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="d2b79-113">Hallo Clusterbeheer implementeren en configureren van Hallo cluster moet administrator-bevoegdheden hebben op Hallo-computer.</span><span class="sxs-lookup"><span data-stu-id="d2b79-113">hello cluster administrator deploying and configuring hello cluster must have administrator privileges on hello computer.</span></span> <span data-ttu-id="d2b79-114">U kunt Service Fabric niet installeren op een domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="d2b79-114">You cannot install Service Fabric on a domain controller.</span></span>

## <a name="validate-hello-environment"></a><span data-ttu-id="d2b79-115">Hallo-omgeving valideren</span><span class="sxs-lookup"><span data-stu-id="d2b79-115">Validate hello environment</span></span>
<span data-ttu-id="d2b79-116">Hallo *TestConfiguration.ps1* script in Hallo zelfstandige pakket wordt gebruikt als een best practices analyzer toovalidate of een cluster kan worden geïmplementeerd op een bepaalde omgeving.</span><span class="sxs-lookup"><span data-stu-id="d2b79-116">hello *TestConfiguration.ps1* script in hello standalone package is used as a best practices analyzer toovalidate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="d2b79-117">[Implementatie voorbereiden](service-fabric-cluster-standalone-deployment-preparation.md) lijsten Hallo vereisten en vereisten.</span><span class="sxs-lookup"><span data-stu-id="d2b79-117">[Deployment preparation](service-fabric-cluster-standalone-deployment-preparation.md) lists hello pre-requisites and environment requirements.</span></span> <span data-ttu-id="d2b79-118">Hallo script tooverify uitvoeren als u Hallo ontwikkelcluster kunt maken:</span><span class="sxs-lookup"><span data-stu-id="d2b79-118">Run hello script tooverify if you can create hello development cluster:</span></span>

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-hello-cluster"></a><span data-ttu-id="d2b79-119">Hallo-cluster maken</span><span class="sxs-lookup"><span data-stu-id="d2b79-119">Create hello cluster</span></span>
<span data-ttu-id="d2b79-120">Verschillende cluster configuratie voorbeeldbestanden worden geïnstalleerd met Hallo-installatiepakket.</span><span class="sxs-lookup"><span data-stu-id="d2b79-120">Several sample cluster configuration files are installed with hello setup package.</span></span> <span data-ttu-id="d2b79-121">*ClusterConfig.Unsecure.DevCluster.json* is de eenvoudigste clusterconfiguratie Hallo: een onbeveiligde, drie-node cluster uitgevoerd op een enkele computer.</span><span class="sxs-lookup"><span data-stu-id="d2b79-121">*ClusterConfig.Unsecure.DevCluster.json* is hello simplest cluster configuration: an unsecure, three-node cluster running on a single computer.</span></span>  <span data-ttu-id="d2b79-122">Andere configuratiebestanden beschrijven clusters voor één of meerdere machines die zijn beveiligd met een x.509-certificaat of met Windows-beveiliging.</span><span class="sxs-lookup"><span data-stu-id="d2b79-122">Other config files describe single or multi-machine clusters secured with X.509 certificates or Windows security.</span></span>  <span data-ttu-id="d2b79-123">U niet toomodify Hallo standaard configuratie-instellingen nodig voor deze zelfstudie, maar bekijkt hello configuratiebestand en raken met het Hallo-instellingen.</span><span class="sxs-lookup"><span data-stu-id="d2b79-123">You don't need toomodify any of hello default config settings for this tutorial, but look through hello config file and get familiar with hello settings.</span></span>  <span data-ttu-id="d2b79-124">Hallo **knooppunten** sectie wordt beschreven Hallo drie knooppunten in cluster Hallo: naam, IP-adres, [knooppunttype foutdomein en upgradedomein](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="d2b79-124">hello **nodes** section describes hello three nodes in hello cluster: name, IP address, [node type, fault domain, and upgrade domain](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span></span>  <span data-ttu-id="d2b79-125">Hallo **eigenschappen** sectie definieert Hallo [beveiliging, niveau van betrouwbaarheid, de verzameling diagnostische gegevens en soorten knooppunten](service-fabric-cluster-manifest.md#cluster-properties) voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="d2b79-125">hello **properties** section defines hello [security, reliability level, diagnostics collection, and types of nodes](service-fabric-cluster-manifest.md#cluster-properties) for hello cluster.</span></span>

<span data-ttu-id="d2b79-126">Dit cluster is onveilig.</span><span class="sxs-lookup"><span data-stu-id="d2b79-126">This cluster is unsecure.</span></span>  <span data-ttu-id="d2b79-127">Iedereen kan anoniem verbinding maken en beheerbewerkingen uitvoeren. Productieclusters moeten dus altijd worden beveiligd met X.509-certificaten of Windows-beveiliging.</span><span class="sxs-lookup"><span data-stu-id="d2b79-127">Anyone can connect anonymously and perform management operations, so production clusters should always be secured using X.509 certificates or Windows security.</span></span>  <span data-ttu-id="d2b79-128">Beveiliging alleen tijdens het maken van een cluster is geconfigureerd en is niet mogelijk tooenable beveiliging nadat Hallo-cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d2b79-128">Security is only configured at cluster creation time and it is not possible tooenable security after hello cluster is created.</span></span>  <span data-ttu-id="d2b79-129">Lees [beveiligen van een cluster](service-fabric-cluster-security.md) toolearn meer over de beveiliging van de Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="d2b79-129">Read [Secure a cluster](service-fabric-cluster-security.md) toolearn more about Service Fabric cluster security.</span></span>  

<span data-ttu-id="d2b79-130">toocreate hello drie knooppunten ontwikkelcluster, Voer Hallo *CreateServiceFabricCluster.ps1* script van een beheerder PowerShell-sessie:</span><span class="sxs-lookup"><span data-stu-id="d2b79-130">toocreate hello three-node development cluster, run hello *CreateServiceFabricCluster.ps1* script from an administrator PowerShell session:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="d2b79-131">Hallo Service Fabric-runtime-pakket wordt automatisch gedownload en geïnstalleerd tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="d2b79-131">hello Service Fabric runtime package is automatically downloaded and installed at time of cluster creation.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="d2b79-132">Verbinding maken met cluster toohello</span><span class="sxs-lookup"><span data-stu-id="d2b79-132">Connect toohello cluster</span></span>
<span data-ttu-id="d2b79-133">Het ontwikkelingscluster met drie knooppunten wordt nu uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d2b79-133">Your three-node development cluster is now running.</span></span> <span data-ttu-id="d2b79-134">Hallo runtime is Hallo ServiceFabric PowerShell-module geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d2b79-134">hello ServiceFabric PowerShell module is installed with hello runtime.</span></span>  <span data-ttu-id="d2b79-135">U kunt controleren dat Hallo-cluster wordt uitgevoerd op Hallo dezelfde computer of vanaf een externe computer met Hallo Service Fabric-runtime.</span><span class="sxs-lookup"><span data-stu-id="d2b79-135">You can verify that hello cluster is running from hello same computer or from a remote computer with hello Service Fabric runtime.</span></span>  <span data-ttu-id="d2b79-136">Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet stelt een verbinding toohello-cluster.</span><span class="sxs-lookup"><span data-stu-id="d2b79-136">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
<span data-ttu-id="d2b79-137">Zie [Connect tooa beveiligde cluster](service-fabric-connect-to-secure-cluster.md) voor andere voorbeelden van verbindende tooa cluster.</span><span class="sxs-lookup"><span data-stu-id="d2b79-137">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="d2b79-138">Na het maken van verbinding toohello-cluster gebruiken Hallo [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay cmdlet een lijst met knooppunten in het Hallo-cluster en de status van informatie voor elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="d2b79-138">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="d2b79-139">**HealthState** moet *OK* zijn voor elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="d2b79-139">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="d2b79-140">Hallo-cluster met Service Fabric explorer visualiseren</span><span class="sxs-lookup"><span data-stu-id="d2b79-140">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="d2b79-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is een goed hulpmiddel om een cluster te visualiseren en toepassingen te beheren.</span><span class="sxs-lookup"><span data-stu-id="d2b79-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="d2b79-142">Service Fabric Explorer is een service die wordt uitgevoerd in Hallo-cluster dat u via een browser openen door te navigeren[http://localhost: 19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="d2b79-142">Service Fabric Explorer is a service that runs in hello cluster, which you access using a browser by navigating too[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> 

<span data-ttu-id="d2b79-143">Hallo cluster-dashboard biedt een overzicht van uw cluster, inclusief een overzicht van de toepassing en het knooppunt status.</span><span class="sxs-lookup"><span data-stu-id="d2b79-143">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="d2b79-144">Hallo knooppunt weergave toont de fysieke indeling Hallo van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="d2b79-144">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="d2b79-145">Voor elk knooppunt kunt u controleren voor welke toepassingen er op het knooppunt code is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="d2b79-145">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-hello-cluster"></a><span data-ttu-id="d2b79-147">Hallo-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="d2b79-147">Remove hello cluster</span></span>
<span data-ttu-id="d2b79-148">tooremove een cluster uitvoert Hallo *RemoveServiceFabricCluster.ps1* PowerShell-script van de pakketmap Hallo en geeft u Hallo pad toohello JSON-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="d2b79-148">tooremove a cluster, run hello *RemoveServiceFabricCluster.ps1* PowerShell script from hello package folder and pass in hello path toohello JSON configuration file.</span></span> <span data-ttu-id="d2b79-149">U kunt optioneel een locatie voor Hallo logboek van Hallo verwijdering opgeven.</span><span class="sxs-lookup"><span data-stu-id="d2b79-149">You can optionally specify a location for hello log of hello deletion.</span></span>

```powershell
# Removes Service Fabric cluster nodes from each computer in hello configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

<span data-ttu-id="d2b79-150">tooremove hello Service Fabric-runtime vanaf Hallo-computer, Hallo volgende PowerShell-script uit Hallo pakketmap worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d2b79-150">tooremove hello Service Fabric runtime from hello computer, run hello following PowerShell script from hello package folder.</span></span>

```powershell
# Removes Service Fabric from hello current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a><span data-ttu-id="d2b79-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d2b79-151">Next steps</span></span>
<span data-ttu-id="d2b79-152">Nu u een zelfstandige ontwikkelcluster hebt ingesteld, proberen Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d2b79-152">Now that you have set up a development standalone cluster, try hello following articles:</span></span>
* <span data-ttu-id="d2b79-153">[Een zelfstandig cluster met meerdere machines instellen](service-fabric-cluster-creation-for-windows-server.md) en beveiliging inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d2b79-153">[Set up a multi-machine standalone cluster](service-fabric-cluster-creation-for-windows-server.md) and enable security.</span></span>
* [<span data-ttu-id="d2b79-154">Apps implementeren met behulp van Powershell</span><span class="sxs-lookup"><span data-stu-id="d2b79-154">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png

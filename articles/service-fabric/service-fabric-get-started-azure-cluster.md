---
title: aaaSet een Azure Service Fabric-cluster | Microsoft Docs
description: Quick Start - Maak een Service Fabric-cluster voor Windows of Linux in Azure.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a><span data-ttu-id="701d4-103">Uw eerste Service Fabric-cluster maken in Azure</span><span class="sxs-lookup"><span data-stu-id="701d4-103">Create your first Service Fabric cluster on Azure</span></span>
<span data-ttu-id="701d4-104">Een [Service Fabric-cluster](service-fabric-deploy-anywhere.md) is een met het netwerk verbonden reeks virtuele of fysieke machines waarop uw microservices worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="701d4-104">A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed.</span></span> <span data-ttu-id="701d4-105">Deze snelstartgids kunt u een cluster met vijf knooppunten, uitgevoerd op Windows of Linux, via Hallo toocreate [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) of [Azure-portal](http://portal.azure.com) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="701d4-105">This quickstart helps you toocreate a five-node cluster, running on either Windows or Linux, through hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) or [Azure portal](http://portal.azure.com) in just a few minutes.</span></span>  

<span data-ttu-id="701d4-106">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="701d4-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="use-hello-azure-portal"></a><span data-ttu-id="701d4-107">Gebruik hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="701d4-107">Use hello Azure portal</span></span>

<span data-ttu-id="701d4-108">Meld u bij toohello Azure-portal op [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="701d4-108">Log in toohello Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

### <a name="create-hello-cluster"></a><span data-ttu-id="701d4-109">Hallo-cluster maken</span><span class="sxs-lookup"><span data-stu-id="701d4-109">Create hello cluster</span></span>

1. <span data-ttu-id="701d4-110">Klik op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="701d4-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>
2. <span data-ttu-id="701d4-111">Selecteer **Compute** van Hallo **nieuw** blade en selecteer vervolgens **Service Fabric-Cluster** van Hallo **Compute** blade.</span><span class="sxs-lookup"><span data-stu-id="701d4-111">Select **Compute** from hello **New** blade and then select **Service Fabric Cluster** from hello **Compute** blade.</span></span>
3. <span data-ttu-id="701d4-112">Hallo Service Fabric invullen **basisbeginselen** formulier.</span><span class="sxs-lookup"><span data-stu-id="701d4-112">Fill out hello Service Fabric **Basics** form.</span></span> <span data-ttu-id="701d4-113">Voor **besturingssysteem**, selecteer Hallo-versie van Windows of Linux die u wilt dat cluster knooppunten toorun Hallo.</span><span class="sxs-lookup"><span data-stu-id="701d4-113">For **Operating system**, select hello version of Windows or Linux you want hello cluster nodes toorun.</span></span> <span data-ttu-id="701d4-114">Hallo-gebruikersnaam en wachtwoord die u hier invoert is gebruikte toolog in toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="701d4-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="701d4-115">Selecteer een **resourcegroep** of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="701d4-115">For **Resource group**, create a new one.</span></span> <span data-ttu-id="701d4-116">Een resourcegroep is een logische container waarin Azure-resources worden gemaakt en waarin ze collectief worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="701d4-116">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="701d4-117">Na het voltooien klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="701d4-117">When complete, click **OK**.</span></span>

    ![Cluster-installatieuitvoer][cluster-setup-basics]

4. <span data-ttu-id="701d4-119">Hallo invullen **clusterconfiguratie** formulier.</span><span class="sxs-lookup"><span data-stu-id="701d4-119">Fill out hello **Cluster configuration** form.</span></span>  <span data-ttu-id="701d4-120">Voer voor **Aantal knooppunttype** de waarde '1' in.</span><span class="sxs-lookup"><span data-stu-id="701d4-120">For **Node type count**, enter "1".</span></span>

5. <span data-ttu-id="701d4-121">Selecteer **knooppunttype 1 (primair)** en invullen Hallo **type knooppuntconfiguratie** formulier.</span><span class="sxs-lookup"><span data-stu-id="701d4-121">Select **Node type 1 (Primary)** and fill out hello **Node type configuration** form.</span></span>  <span data-ttu-id="701d4-122">Voer de naam van een knooppunt en stel Hallo [duurzaamheid laag](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) te 'Brons'.</span><span class="sxs-lookup"><span data-stu-id="701d4-122">Enter a node type name and set hello [Durability tier](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) too"Bronze."</span></span>  <span data-ttu-id="701d4-123">Selecteer een VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="701d4-123">Select a VM size.</span></span>

    <span data-ttu-id="701d4-124">Knooppunttypen definiëren Hallo VM-grootte, het aantal virtuele machines, aangepaste eindpunten en andere instellingen voor virtuele machines van dat type Hallo.</span><span class="sxs-lookup"><span data-stu-id="701d4-124">Node types define hello VM size, number of VMs, custom endpoints, and other settings for hello VMs of that type.</span></span> <span data-ttu-id="701d4-125">Elk knooppunttype gedefinieerd is ingesteld als een afzonderlijke virtuele-machineschaalset weergeven, die gebruikt toodeploy en beheerde virtuele machines als een set is.</span><span class="sxs-lookup"><span data-stu-id="701d4-125">Each node type defined is set up as a separate virtual machine scale set, which is used toodeploy and managed virtual machines as a set.</span></span> <span data-ttu-id="701d4-126">Elk knooppunttype kan onafhankelijk omhoog of omlaag worden geschaald, verschillende open poorten bevatten en verschillende capaciteitsstatistieken hebben.</span><span class="sxs-lookup"><span data-stu-id="701d4-126">Each node type can be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>  <span data-ttu-id="701d4-127">Hallo eerste of primaire, knooppunttype is waar systeemservices Service Fabric worden gehost en vijf of meer virtuele machines moeten hebben.</span><span class="sxs-lookup"><span data-stu-id="701d4-127">hello first, or primary, node type is where Service Fabric system services are hosted and must have five or more VMs.</span></span>

    <span data-ttu-id="701d4-128">Bij elke implementatie voor productie is [capaciteitsplanning](service-fabric-cluster-capacity.md) van groot belang.</span><span class="sxs-lookup"><span data-stu-id="701d4-128">For any production deployment, [capacity planning](service-fabric-cluster-capacity.md) is an important step.</span></span>  <span data-ttu-id="701d4-129">Voor deze Quick Start voert u echter geen toepassingen uit, dus selecteert u de VM-grootte *DS1_v2 Standard*.</span><span class="sxs-lookup"><span data-stu-id="701d4-129">For this quick start, however, you aren't running applications so select a *DS1_v2 Standard* VM size.</span></span>  <span data-ttu-id="701d4-130">Selecteer 'Silver' voor Hallo [betrouwbaarheidslaag](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) en een eerste virtuele-machineschaalset capaciteit van 5 instellen.</span><span class="sxs-lookup"><span data-stu-id="701d4-130">Select "Silver" for hello [reliability tier](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) and an initial virtual machine scale set capacity of 5.</span></span>  

    <span data-ttu-id="701d4-131">Aangepaste eindpunten openen van poorten in hello Azure load balancer zodat u verbinding kunt maken met toepassingen die worden uitgevoerd op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="701d4-131">Custom endpoints open up ports in hello Azure load balancer so that you can connect with applications running on hello cluster.</span></span>  <span data-ttu-id="701d4-132">Voer "80, 8172" tooopen up poorten 80 en 8172.</span><span class="sxs-lookup"><span data-stu-id="701d4-132">Enter "80, 8172" tooopen up ports 80 and 8172.</span></span>

    <span data-ttu-id="701d4-133">Hallo niet controleren **geavanceerde instellingen configureren** vak dat wordt gebruikt voor het aanpassen van TCP/HTTP-eindpunten voor beheer, poortbereiken van toepassing, [plaatsingsbeperkingen](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), en [capaciteit eigenschappen](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="701d4-133">Do not check hello **Configure advanced settings** box, which is used for customizing TCP/HTTP management endpoints, application port ranges, [placement constraints](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), and [capacity properties](service-fabric-cluster-resource-manager-metrics.md).</span></span>    

    <span data-ttu-id="701d4-134">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="701d4-134">Select **OK**.</span></span>

6. <span data-ttu-id="701d4-135">In Hallo **clusterconfiguratie** vormen, stelt u **Diagnostics** te**op**.</span><span class="sxs-lookup"><span data-stu-id="701d4-135">In hello **Cluster configuration** form, set **Diagnostics** too**On**.</span></span>  <span data-ttu-id="701d4-136">Voor deze snelstartgids, hoeft u niet tooenter ieder [fabric instelling](service-fabric-cluster-fabric-settings.md) eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="701d4-136">For this quickstart, you do not need tooenter any [fabric setting](service-fabric-cluster-fabric-settings.md) properties.</span></span>  <span data-ttu-id="701d4-137">In **Fabric-versie**, selecteer **automatische** upgrademodus zodat Microsoft hello versie van Hallo fabric code die wordt uitgevoerd Hallo cluster automatisch bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="701d4-137">In **Fabric version**, select **Automatic** upgrade mode so that Microsoft automatically updates hello version of hello fabric code running hello cluster.</span></span>  <span data-ttu-id="701d4-138">Hallo-modus te instellen**handmatige** desgewenst te[kiest u een ondersteunde versie](service-fabric-cluster-upgrade.md) tooupgrade aan.</span><span class="sxs-lookup"><span data-stu-id="701d4-138">Set hello mode too**Manual** if you want too[choose a supported version](service-fabric-cluster-upgrade.md) tooupgrade to.</span></span> 

    ![Configuratie van knooppunttypen][node-type-config]

    <span data-ttu-id="701d4-140">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="701d4-140">Select **OK**.</span></span>

7. <span data-ttu-id="701d4-141">Hallo invullen **beveiliging** formulier.</span><span class="sxs-lookup"><span data-stu-id="701d4-141">Fill out hello **Security** form.</span></span>  <span data-ttu-id="701d4-142">Voor deze Quick Start selecteert u **Onbeveiligd**.</span><span class="sxs-lookup"><span data-stu-id="701d4-142">For this quick start select **Unsecure**.</span></span>  <span data-ttu-id="701d4-143">U wordt ten zeerste aanbevolen toocreate een beveiligde cluster voor productieworkloads, echter, aangezien iedereen anoniem verbinding kunt tooan niet-beveiligde cluster en beheerbewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="701d4-143">It is highly recommended toocreate a secure cluster for production workloads, however, since anyone can anonymously connect tooan unsecure cluster and perform management operations.</span></span>  

    <span data-ttu-id="701d4-144">Certificaten worden gebruikt in Service Fabric tooprovide verificatie en versleuteling toosecure verschillende aspecten van een cluster en de toepassingen.</span><span class="sxs-lookup"><span data-stu-id="701d4-144">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="701d4-145">Zie [Service Fabric-clusterbeveiligingsscenario's](service-fabric-cluster-security.md) voor meer informatie over hoe certificaten worden gebruikt in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="701d4-145">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md).</span></span>  <span data-ttu-id="701d4-146">tooenable gebruikersverificatie met Azure Active Directory of tooset van certificaten voor Toepassingsbeveiliging, [een cluster maken van een Resource Manager-sjabloon](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="701d4-146">tooenable user authentication using Azure Active Directory or tooset up certificates for application security, [create a cluster from a Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span>

    <span data-ttu-id="701d4-147">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="701d4-147">Select **OK**.</span></span>

8. <span data-ttu-id="701d4-148">Controleer de hello samenvatting.</span><span class="sxs-lookup"><span data-stu-id="701d4-148">Review hello summary.</span></span>  <span data-ttu-id="701d4-149">Als u wilt toodownload Resource Manager-sjabloon samengesteld uit Hallo-instellingen hebt ingevoerd, selecteert u **sjabloon en parameters downloaden**.</span><span class="sxs-lookup"><span data-stu-id="701d4-149">If you'd like toodownload a Resource Manager template built from hello settings you entered, select **Download template and parameters**.</span></span>  <span data-ttu-id="701d4-150">Selecteer **maken** toocreate Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="701d4-150">Select **Create** toocreate hello cluster.</span></span>

    <span data-ttu-id="701d4-151">Voortgang van het Hallo maken in kennisgevingen hello, kunt u zien.</span><span class="sxs-lookup"><span data-stu-id="701d4-151">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="701d4-152">(Klik op Hallo ' ' belpictogram bijna Hallo statusbalk Hallo rechterbovenhoek van het scherm). Als u hebt geklikt **pincode tooStartboard** tijdens het Hallo-cluster maken, ziet u **Service Fabric-Cluster implementeren** vastgemaakt toohello **Start** mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="701d4-152">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-cluster-status"></a><span data-ttu-id="701d4-153">De clusterstatus bekijken</span><span class="sxs-lookup"><span data-stu-id="701d4-153">View cluster status</span></span>
<span data-ttu-id="701d4-154">Zodra het cluster is gemaakt, kunt u uw cluster in Hallo inspecteren **overzicht** blade in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="701d4-154">Once your cluster is created, you can inspect your cluster in hello **Overview** blade in hello portal.</span></span> <span data-ttu-id="701d4-155">U ziet nu Hallo details van het cluster in Hallo-dashboard, met inbegrip van het cluster Hallo openbaar eindpunt en een koppeling tooService Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="701d4-155">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

![De clusterstatus][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="701d4-157">Hallo-cluster met Service Fabric explorer visualiseren</span><span class="sxs-lookup"><span data-stu-id="701d4-157">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="701d4-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is een goed hulpmiddel om een cluster te visualiseren en toepassingen te beheren.</span><span class="sxs-lookup"><span data-stu-id="701d4-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="701d4-159">Service Fabric Explorer is een service die wordt uitgevoerd in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="701d4-159">Service Fabric Explorer is a service that runs in hello cluster.</span></span>  <span data-ttu-id="701d4-160">Toegang tot dit met een webbrowser door te klikken op Hallo **Service Fabric Explorer** koppeling van Hallo cluster **overzicht** pagina in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="701d4-160">Access it using a web browser by clicking hello **Service Fabric Explorer** link of hello cluster **Overview** page in hello portal.</span></span>  <span data-ttu-id="701d4-161">U kunt ook Hallo adres invoeren rechtstreeks in de browser Hallo: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span><span class="sxs-lookup"><span data-stu-id="701d4-161">You can also enter hello address directly into hello browser: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span></span>

<span data-ttu-id="701d4-162">Hallo cluster-dashboard biedt een overzicht van uw cluster, inclusief een overzicht van de toepassing en het knooppunt status.</span><span class="sxs-lookup"><span data-stu-id="701d4-162">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="701d4-163">Hallo knooppunt weergave toont de fysieke indeling Hallo van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="701d4-163">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="701d4-164">Voor elk knooppunt kunt u controleren voor welke toepassingen er op het knooppunt code is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="701d4-164">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a><span data-ttu-id="701d4-166">Verbinding maken met behulp van PowerShell toohello-cluster</span><span class="sxs-lookup"><span data-stu-id="701d4-166">Connect toohello cluster using PowerShell</span></span>
<span data-ttu-id="701d4-167">Controleer of dat Hallo-cluster wordt uitgevoerd door verbinding te maken met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="701d4-167">Verify that hello cluster is running by connecting using PowerShell.</span></span>  <span data-ttu-id="701d4-168">Hallo ServiceFabric PowerShell-module is geïnstalleerd met Hallo [Service Fabric SDK](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="701d4-168">hello ServiceFabric PowerShell module is installed with hello [Service Fabric SDK](service-fabric-get-started.md).</span></span>  <span data-ttu-id="701d4-169">Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet stelt een verbinding toohello-cluster.</span><span class="sxs-lookup"><span data-stu-id="701d4-169">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
<span data-ttu-id="701d4-170">Zie [Connect tooa beveiligde cluster](service-fabric-connect-to-secure-cluster.md) voor andere voorbeelden van verbindende tooa cluster.</span><span class="sxs-lookup"><span data-stu-id="701d4-170">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="701d4-171">Na het maken van verbinding toohello-cluster gebruiken Hallo [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay cmdlet een lijst met knooppunten in het Hallo-cluster en de status van informatie voor elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="701d4-171">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="701d4-172">**HealthState** moet *OK* zijn voor elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="701d4-172">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a><span data-ttu-id="701d4-173">Hallo-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="701d4-173">Remove hello cluster</span></span>
<span data-ttu-id="701d4-174">Service Fabric-cluster is opgebouwd uit andere Azure-resources bovendien toohello clusterbron zelf.</span><span class="sxs-lookup"><span data-stu-id="701d4-174">A Service Fabric cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="701d4-175">Zodat toocompletely verwijdert een Service Fabric-cluster moet u ook alle resources die wordt gemaakt van Hallo toodelete.</span><span class="sxs-lookup"><span data-stu-id="701d4-175">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span> <span data-ttu-id="701d4-176">Hallo eenvoudigste manier toodelete Hallo cluster en alle Hallo resources verbruikt is toodelete Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="701d4-176">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> <span data-ttu-id="701d4-177">Voor andere manieren toodelete een cluster of toodelete enkele (maar niet alle) Hallo-resources in een resourcegroep, Zie [een cluster verwijderen](service-fabric-cluster-delete.md)</span><span class="sxs-lookup"><span data-stu-id="701d4-177">For other ways toodelete a cluster or toodelete some (but not all) hello resources in a resource group, see [Delete a cluster](service-fabric-cluster-delete.md)</span></span>

<span data-ttu-id="701d4-178">Verwijderen van een resourcegroep in hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="701d4-178">Delete a resource group in hello Azure portal:</span></span>
1. <span data-ttu-id="701d4-179">Navigeer toohello gewenste toodelete Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="701d4-179">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
2. <span data-ttu-id="701d4-180">Klik op Hallo **resourcegroep** naam op Hallo cluster essentials pagina.</span><span class="sxs-lookup"><span data-stu-id="701d4-180">Click hello **Resource Group** name on hello cluster essentials page.</span></span>
3. <span data-ttu-id="701d4-181">In Hallo **Resource groep Essentials** pagina, klikt u op **resourcegroep verwijderen** en volg Hallo-instructies op die pagina toocomplete Hallo verwijdering van de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="701d4-181">In hello **Resource Group Essentials** page, click **Delete resource group** and follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>
    <span data-ttu-id="701d4-182">![Hallo-resourcegroep verwijderen][cluster-delete]</span><span class="sxs-lookup"><span data-stu-id="701d4-182">![Delete hello resource group][cluster-delete]</span></span>


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a><span data-ttu-id="701d4-183">Azure Powershell toodeploy een beveiligde cluster gebruiken</span><span class="sxs-lookup"><span data-stu-id="701d4-183">Use Azure Powershell toodeploy a secure cluster</span></span>
1. <span data-ttu-id="701d4-184">Hallo downloaden [Azure Powershell-moduleversie 4.0 of hoger](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) op uw computer.</span><span class="sxs-lookup"><span data-stu-id="701d4-184">Download hello [Azure Powershell module version 4.0 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) on your machine.</span></span>

2. <span data-ttu-id="701d4-185">Open een Windows PowerShell-venster uitvoeren Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="701d4-185">Open a Windows PowerShell window, Run hello following command.</span></span> 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    <span data-ttu-id="701d4-186">U ziet een uitvoer vergelijkbare toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="701d4-186">You should see an output similar toohello following.</span></span>

    ![ps-list][ps-list]

3. <span data-ttu-id="701d4-188">Aanmelding tooAzure en selecteer Hallo abonnement toowhich u toocreate Hallo cluster wilt toevoegen</span><span class="sxs-lookup"><span data-stu-id="701d4-188">Login tooAzure and Select hello subscription toowhich you want toocreate hello cluster</span></span>

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. <span data-ttu-id="701d4-189">Voer Hallo opdracht toonow na een beveiligde cluster maken.</span><span class="sxs-lookup"><span data-stu-id="701d4-189">Run hello following command toonow create a secure cluster.</span></span> <span data-ttu-id="701d4-190">Vergeet niet toocustomize Hallo parameters.</span><span class="sxs-lookup"><span data-stu-id="701d4-190">Do not forget toocustomize hello parameters.</span></span> 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    <span data-ttu-id="701d4-191">Hallo-opdracht kan duren 10 minuten too30 minuten toocomplete aan Hallo einde van het, krijgt u een vergelijkbare toohello volgende voor uitvoer.</span><span class="sxs-lookup"><span data-stu-id="701d4-191">hello command can take anywhere from 10 minutes too30 minutes toocomplete, at hello end of it, you should get an output similar toohello following.</span></span> <span data-ttu-id="701d4-192">Hallo uitvoer bevat informatie over Hallo certificaat Hallo KeyVault waar deze is geüpload naar, en Hallo lokale map waarin Hallo-certificaat is gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="701d4-192">hello output has information about hello certificate, hello KeyVault where it was uploaded to, and hello local folder where hello certificate is copied.</span></span> 

    ![ps-out][ps-out]

5. <span data-ttu-id="701d4-194">Kopieer de gehele uitvoer Hallo en tooa-tekstbestand opslaan als we toorefer tooit nodig.</span><span class="sxs-lookup"><span data-stu-id="701d4-194">Copy hello entire output and save tooa text file as we need toorefer tooit.</span></span> <span data-ttu-id="701d4-195">Maak een notitie van de volgende informatie uit de uitvoer Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="701d4-195">Make a note of hello following information from hello output.</span></span> 

    - <span data-ttu-id="701d4-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span><span class="sxs-lookup"><span data-stu-id="701d4-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span></span>
    - <span data-ttu-id="701d4-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span><span class="sxs-lookup"><span data-stu-id="701d4-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span></span>
    - <span data-ttu-id="701d4-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span><span class="sxs-lookup"><span data-stu-id="701d4-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span></span>
    - <span data-ttu-id="701d4-199">**ClientConnectionEndpointPort** : 19000</span><span class="sxs-lookup"><span data-stu-id="701d4-199">**ClientConnectionEndpointPort** : 19000</span></span>

### <a name="install-hello-certificate-on-your-local-machine"></a><span data-ttu-id="701d4-200">Hallo-certificaat installeren op uw lokale computer</span><span class="sxs-lookup"><span data-stu-id="701d4-200">Install hello certificate on your local machine</span></span>
  
<span data-ttu-id="701d4-201">tooconnect toohello cluster, moet u tooinstall Hallo certificaat in archief van het persoonlijke (Mijn) van de huidige gebruiker Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="701d4-201">tooconnect toohello cluster, you need tooinstall hello certificate into hello Personal (My) store of hello current user.</span></span> 

<span data-ttu-id="701d4-202">Hallo na PowerShell uitvoeren</span><span class="sxs-lookup"><span data-stu-id="701d4-202">Run hello following PowerShell</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

<span data-ttu-id="701d4-203">U bent nu klaar tooconnect tooyour beveiligde cluster.</span><span class="sxs-lookup"><span data-stu-id="701d4-203">You are now ready tooconnect tooyour secure cluster.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="701d4-204">Verbinding maken met de beveiligde cluster tooa</span><span class="sxs-lookup"><span data-stu-id="701d4-204">Connect tooa secure cluster</span></span> 

<span data-ttu-id="701d4-205">Hallo volgende PowerShell-opdracht tooconnect tooa beveiligde cluster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="701d4-205">Run hello following PowerShell command tooconnect tooa secure cluster.</span></span> <span data-ttu-id="701d4-206">Hallo certificaatdetails moeten overeenkomen met een certificaat dat gebruikt tooset Hallo-cluster is.</span><span class="sxs-lookup"><span data-stu-id="701d4-206">hello certificate details must match a certificate that was used tooset up hello cluster.</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


<span data-ttu-id="701d4-207">Hallo volgende voorbeeld toont Hallo voltooid parameters:</span><span class="sxs-lookup"><span data-stu-id="701d4-207">hello following example shows hello completed parameters:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="701d4-208">Voer Hallo na de opdracht toocheck dat u verbonden bent en Hallo-cluster is in orde.</span><span class="sxs-lookup"><span data-stu-id="701d4-208">Run hello following command toocheck that you are connected and hello cluster is healthy.</span></span>

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a><span data-ttu-id="701d4-209">Publiceren van uw apps tooyour cluster vanuit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="701d4-209">Publish your apps tooyour cluster from Visual Studio</span></span>

<span data-ttu-id="701d4-210">Nu dat u een Azure-cluster hebt ingesteld, kunt u uw tooit toepassingen vanuit Visual Studio door de volgende Hallo publiceren [publiceren tooan cluster](service-fabric-publish-app-remote-cluster.md) document.</span><span class="sxs-lookup"><span data-stu-id="701d4-210">Now that you have set up an Azure cluster, you can publish your applications tooit from Visual Studio by following hello [Publish tooan cluster](service-fabric-publish-app-remote-cluster.md) document.</span></span> 

### <a name="remove-hello-cluster"></a><span data-ttu-id="701d4-211">Hallo-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="701d4-211">Remove hello cluster</span></span>
<span data-ttu-id="701d4-212">Een cluster is opgebouwd uit andere Azure-resources bovendien toohello clusterbron zelf.</span><span class="sxs-lookup"><span data-stu-id="701d4-212">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="701d4-213">Hallo eenvoudigste manier toodelete Hallo cluster en alle Hallo resources verbruikt is toodelete Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="701d4-213">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a><span data-ttu-id="701d4-214">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="701d4-214">Next steps</span></span>
<span data-ttu-id="701d4-215">Nu u een ontwikkelcluster hebt ingesteld, proberen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="701d4-215">Now that you have set up a development cluster, try hello following:</span></span>
* [<span data-ttu-id="701d4-216">Maken van een beveiligde cluster in Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="701d4-216">Create a secure cluster in hello portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="701d4-217">Een cluster maken op basis van een sjabloon</span><span class="sxs-lookup"><span data-stu-id="701d4-217">Create a cluster from a template</span></span>](service-fabric-cluster-creation-via-arm.md) 
* [<span data-ttu-id="701d4-218">Apps implementeren met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="701d4-218">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG

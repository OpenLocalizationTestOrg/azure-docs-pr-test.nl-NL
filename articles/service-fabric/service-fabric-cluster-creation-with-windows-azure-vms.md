---
title: aaaCreate zelfstandige cluster met virtuele Azure-machines met Windows | Microsoft Docs
description: Meer informatie over hoe toocreate en beheren van een Azure Service Fabric-cluster op virtuele machines in Azure waarop Windows Server wordt uitgevoerd.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="92b9b-103">Drie knooppunten zelfstandige Service Fabric-cluster maken met virtuele machines in Azure waarop Windows Server wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="92b9b-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="92b9b-104">Dit artikel wordt beschreven hoe toocreate een cluster op Windows gebaseerde virtuele Azure-machines (VM's) met behulp van Hallo van zelfstandige Service Fabric-installatieprogramma voor Windows Server.</span><span class="sxs-lookup"><span data-stu-id="92b9b-104">This article describes how toocreate a cluster on Windows-based Azure virtual machines (VMs), using hello standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="92b9b-105">Hallo-scenario is een speciaal geval van [maken en beheren van een cluster met Windows Server](service-fabric-cluster-creation-for-windows-server.md) waar Hallo VM's zijn [Azure VM's met Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), maar u geen maakt [een Azure cloud-gebaseerde Service Fabric-cluster](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="92b9b-105">hello scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where hello VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="92b9b-106">Hallo verschil in de volgende dit patroon is dat Hallo zelfstandige Service Fabric-cluster gemaakt door de volgende stappen uit Hallo volledig wordt beheerd door u, terwijl hello Azure cloud-gebaseerde Service Fabric-clusters worden beheerd en bijgewerkt door Hallo Service Fabric resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="92b9b-106">hello distinction in following this pattern is that hello standalone Service Fabric cluster created by hello following steps is entirely managed by you, whereas hello Azure cloud-based Service Fabric clusters are managed and upgraded by hello Service Fabric resource provider.</span></span>

## <a name="steps-toocreate-hello-standalone-cluster"></a><span data-ttu-id="92b9b-107">Stappen toocreate Hallo zelfstandige cluster</span><span class="sxs-lookup"><span data-stu-id="92b9b-107">Steps toocreate hello standalone cluster</span></span>
1. <span data-ttu-id="92b9b-108">Meld u aan toohello Azure-portal en een nieuwe Windows Server 2012 R2 Datacenter of Windows Server 2016 Datacenter VM in een resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="92b9b-108">Sign in toohello Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="92b9b-109">Hallo-artikel lezen [maken van een virtuele machine van Windows in hello Azure-portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="92b9b-109">Read hello article [Create a Windows VM in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="92b9b-110">Toevoegen van een aantal meer virtuele machines toohello dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="92b9b-110">Add a couple more VMs toohello same resource group.</span></span> <span data-ttu-id="92b9b-111">Zorg ervoor dat elk Hallo VMs heeft Hallo dezelfde beheerdersgebruikersnaam en hetzelfde wachtwoord tijdens het maken.</span><span class="sxs-lookup"><span data-stu-id="92b9b-111">Ensure that each of hello VMs has hello same administrator user name and password when created.</span></span> <span data-ttu-id="92b9b-112">Nadat deze is gemaakt ziet u alle drie virtuele machines in Hallo hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="92b9b-112">Once created you should see all three VMs in hello same virtual network.</span></span>
3. <span data-ttu-id="92b9b-113">Verbinding maken tooeach Hallo VM's en Hallo uitschakelen met Windows Firewall met Hallo [Server Manager dashboard van de lokale Server](https://technet.microsoft.com/library/jj134147.aspx).</span><span class="sxs-lookup"><span data-stu-id="92b9b-113">Connect tooeach of hello VMs and turn off hello Windows Firewall using hello [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="92b9b-114">Dit zorgt ervoor dat het Hallo-netwerkverkeer tussen Hallo-machines communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="92b9b-114">This ensures that hello network traffic can communicate between hello machines.</span></span> <span data-ttu-id="92b9b-115">Ophalen tijdens verbonden tooeach machine Hallo IP-adres door een opdrachtprompt openen en te typen `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="92b9b-115">While connected tooeach machine, get hello IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="92b9b-116">U kunt ook ziet u Hallo IP-adres van elke computer op Hallo-portal door te selecteren Hallo virtueel netwerk resource voor de resourcegroep Hallo en Hallo netwerkinterfaces gemaakt voor elk van deze machines te controleren.</span><span class="sxs-lookup"><span data-stu-id="92b9b-116">Alternatively you can see hello IP address of each machine on hello portal, by selecting hello virtual network resource for hello resource group and checking hello network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="92b9b-117">Verbind tooone Hallo VM's en test die u kunt pingen Hallo andere twee virtuele machines is.</span><span class="sxs-lookup"><span data-stu-id="92b9b-117">Connect tooone of hello VMs and test that you can ping hello other two VMs successfully.</span></span>
5. <span data-ttu-id="92b9b-118">Tooone Hallo virtuele machines verbinding en [downloaden Hallo zelfstandige Service Fabric-pakket voor Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) naar een nieuwe map op Hallo van de computer en pak Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="92b9b-118">Connect tooone of hello VMs and [download hello standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on hello machine and extract hello package.</span></span>
6. <span data-ttu-id="92b9b-119">Open Hallo *ClusterConfig.Unsecure.MultiMachine.json* -bestand in Kladblok en bewerken van elk knooppunt met Hallo drie IP-adressen van Hallo-machines.</span><span class="sxs-lookup"><span data-stu-id="92b9b-119">Open hello *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with hello three IP addresses of hello machines.</span></span> <span data-ttu-id="92b9b-120">De clusternaam Hallo Hallo boven wijzigen en sla Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="92b9b-120">Change hello cluster name at hello top and save hello file.</span></span>  <span data-ttu-id="92b9b-121">Een voorbeeld van een gedeeltelijke van het clustermanifest Hallo worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="92b9b-121">A partial example of hello cluster manifest is shown below.</span></span>
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. <span data-ttu-id="92b9b-122">Als u van plan deze toobe een beveiligde cluster bent, moet u bepalen Hallo beveiligingsmaatregel u wilt toouse en volg de stappen Hallo op Hallo koppeling die is gekoppeld: [X509-certificaat](service-fabric-windows-cluster-x509-security.md) of [Windows-beveiliging](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="92b9b-122">If you intend this toobe a secure cluster, decide hello security measure you would like toouse and follow hello steps at hello associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="92b9b-123">Als het Hallo-cluster met behulp van Windows-beveiliging instelt, moet u tooset van een domeincontroller toomanage Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92b9b-123">If setting up hello cluster using Windows Security, you will need tooset up a domain controller toomanage Active Directory.</span></span> <span data-ttu-id="92b9b-124">Houd er rekening mee dat met een computer op een domeincontroller in een domein als een Service Fabric knooppunt wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="92b9b-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="92b9b-125">Open een [PowerShell ISE-venster](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span><span class="sxs-lookup"><span data-stu-id="92b9b-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="92b9b-126">Navigeer toohello map waarin u Hallo gedownloade zelfstandige installer-pakket hebt uitgepakt en Hallo cluster configuratiebestand opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="92b9b-126">Navigate toohello folder where you extracted hello downloaded standalone installer package and saved hello cluster configuration file.</span></span> <span data-ttu-id="92b9b-127">Voer Hallo PowerShell-opdracht toodeploy Hallo cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="92b9b-127">Run hello following PowerShell command toodeploy hello cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="92b9b-128">Hallo script Hallo Service Fabric-cluster op afstand configureert en voortgang moet worden gerapporteerd als wordt via de implementatie.</span><span class="sxs-lookup"><span data-stu-id="92b9b-128">hello script will remotely configure hello Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="92b9b-129">Na ongeveer een minuut, u controleren kunt of Hallo cluster operationele is door verbinding te maken toohello Service Fabric Explorer met behulp van een van de machine Hallo IP-adressen, bijvoorbeeld met behulp van `http://10.1.0.5:19080/Explorer/index.html`.</span><span class="sxs-lookup"><span data-stu-id="92b9b-129">After about a minute, you can check if hello cluster is operational by connecting toohello Service Fabric Explorer using one of hello machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="92b9b-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="92b9b-130">Next steps</span></span>
* [<span data-ttu-id="92b9b-131">Create standalone Service Fabric clusters on Windows Server or Linux (Zelfstandige Service Fabric-clusters maken in Windows Server of Linux)</span><span class="sxs-lookup"><span data-stu-id="92b9b-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="92b9b-132">Toevoegen of verwijderen van knooppunten tooa zelfstandige Service Fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="92b9b-132">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="92b9b-133">Configuratie-instellingen voor zelfstandige Windows-cluster</span><span class="sxs-lookup"><span data-stu-id="92b9b-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="92b9b-134">Beveiligen van een zelfstandige cluster op Windows met behulp van Windows-beveiliging</span><span class="sxs-lookup"><span data-stu-id="92b9b-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="92b9b-135">Beveiligen van een zelfstandige cluster op Windows met behulp van X509 certificaten</span><span class="sxs-lookup"><span data-stu-id="92b9b-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)


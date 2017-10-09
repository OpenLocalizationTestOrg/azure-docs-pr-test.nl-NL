---
title: aaaPowerShell script toodeploy Linux HPC-cluster | Microsoft Docs
description: Voer een PowerShell-script toodeploy een Linux HPC Pack 2012 R2-cluster in Azure virtuele machines
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 885b03fa2fd604827dc388803fc21debab730979
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="e0caf-103">Een Linux high performance computing (HPC)-cluster maken met de Hallo HPC Pack IaaS-implementatiescript</span><span class="sxs-lookup"><span data-stu-id="e0caf-103">Create a Linux high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="e0caf-104">Hallo HPC Pack IaaS implementatie PowerShell script toodeploy een volledige HPC Pack 2012 R2-cluster voor Linux-werkbelastingen in virtuele Azure-machines uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e0caf-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Linux workloads in Azure virtual machines.</span></span> <span data-ttu-id="e0caf-105">Hallo cluster bestaat uit een op die lid zijn van Active Directory hoofdknooppunt met Windows Server en Microsoft HPC Pack en rekenknooppunten met een van de hello wordt ondersteund door HPC Pack Linux-distributies.</span><span class="sxs-lookup"><span data-stu-id="e0caf-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and compute nodes that run one of hello Linux distributions supported by HPC Pack.</span></span> <span data-ttu-id="e0caf-106">Als u een HPC Pack-cluster in Azure voor Windows werkbelasting toodeploy wilt, Zie [maken van een Windows HPC-cluster met Hallo HPC Pack IaaS-implementatiescript](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0caf-106">If you want toodeploy an HPC Pack cluster in Azure for Windows workloads, see [Create a Windows HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="e0caf-107">U kunt ook een Azure Resource Manager-sjabloon toodeploy een HPC Pack-cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e0caf-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="e0caf-108">Zie voor een voorbeeld [een HPC-cluster maken met Linux-rekenknooppunten](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span><span class="sxs-lookup"><span data-stu-id="e0caf-108">For an example, see [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e0caf-109">Hallo PowerShell-script dat wordt beschreven in dit artikel maakt een Microsoft HPC Pack 2012 R2-cluster in Azure met behulp van het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="e0caf-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="e0caf-110">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e0caf-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="e0caf-111">Hallo-script dat wordt beschreven in dit artikel biedt bovendien geen ondersteuning voor HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="e0caf-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a><span data-ttu-id="e0caf-112">Voorbeeld-configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="e0caf-112">Example configuration file</span></span>
<span data-ttu-id="e0caf-113">Hallo volgende configuratiebestand maakt een domeincontroller en de domein-forest en implementeert een HPC Pack-cluster met één hoofdknooppunt met lokale databases en 10 Linux-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="e0caf-113">hello following configuration file creates a domain controller and domain forest and deploys an HPC Pack cluster which has one head node with local databases and 10 Linux compute nodes.</span></span> <span data-ttu-id="e0caf-114">Alle Hallo cloud-services worden rechtstreeks in de locatie Oost-Azië Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e0caf-114">All hello cloud services are created directly in hello East Asia location.</span></span> <span data-ttu-id="e0caf-115">Hallo worden Linux-rekenknooppunten gemaakt in twee cloudservices en twee storage-accounts (dat wil zeggen, *MyLnxCN 0001* naar *MyLnxCN 0005* in *MyLnxCNService01* en *mylnxstorage01*, en *MyLnxCN 0006* naar *MyLnxCN 0010* in *MyLnxCNService02* en *mylnxstorage02* ).</span><span class="sxs-lookup"><span data-stu-id="e0caf-115">hello Linux compute nodes are created in two cloud services and two storage accounts (that is, *MyLnxCN-0001* to *MyLnxCN-0005* in *MyLnxCNService01* and *mylnxstorage01*, and *MyLnxCN-0006* to *MyLnxCN-0010* in *MyLnxCNService02* and *mylnxstorage02*).</span></span> <span data-ttu-id="e0caf-116">Hallo rekenknooppunten worden gemaakt van een installatiekopie van een OpenLogic CentOS versie 7.0 Linux.</span><span class="sxs-lookup"><span data-stu-id="e0caf-116">hello compute nodes are created from an OpenLogic CentOS version 7.0 Linux image.</span></span> 

<span data-ttu-id="e0caf-117">Vervangt door uw eigen waarden voor uw abonnementsnaam en het Hallo-account en service namen.</span><span class="sxs-lookup"><span data-stu-id="e0caf-117">Substitute your own values for your subscription name and hello account and service names.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
    </DomainController>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a><span data-ttu-id="e0caf-118">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="e0caf-118">Troubleshooting</span></span>
* <span data-ttu-id="e0caf-119">**Fout 'Bestaat niet VNet'**.</span><span class="sxs-lookup"><span data-stu-id="e0caf-119">**“VNet doesn’t exist” error**.</span></span> <span data-ttu-id="e0caf-120">Als u Hallo HPC Pack IaaS implementatie script toodeploy meerdere clusters in Azure gelijktijdig uitgevoerd onder een abonnement, een of meer implementaties mislukken met fout Hallo ' VNet *VNet\_naam* bestaat niet ".</span><span class="sxs-lookup"><span data-stu-id="e0caf-120">If you run hello HPC Pack IaaS deployment script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="e0caf-121">Hallo-script voor de implementatie van Hallo kan niet opnieuw uitvoeren als deze fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="e0caf-121">If this error occurs, rerun hello script for hello failed deployment.</span></span>
* <span data-ttu-id="e0caf-122">**Probleem bij toegang tot Internet Hallo van Hallo virtuele Azure-netwerk**.</span><span class="sxs-lookup"><span data-stu-id="e0caf-122">**Problem accessing hello Internet from hello Azure virtual network**.</span></span> <span data-ttu-id="e0caf-123">Als u een cluster HPC Pack met een nieuwe domeincontroller maakt met behulp van het implementatiescript hello, of u handmatig een hoofdknooppunt VM toodomain domeincontroller promoveren, treden netwerkverbindingsproblemen Hallo VM's in Hallo virtuele Azure-netwerk toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="e0caf-123">If you create an HPC Pack cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs in hello Azure virtual network toohello Internet.</span></span> <span data-ttu-id="e0caf-124">Dit kan gebeuren als een DNS-doorstuurserver server automatisch geconfigureerd op de domeincontroller Hallo en deze doorstuurserver DNS-server kan niet correct worden omgezet.</span><span class="sxs-lookup"><span data-stu-id="e0caf-124">This can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="e0caf-125">toowork om dit probleem zich aanmelden op de domeincontroller toohello en beide verwijderen Hallo doorstuurserver configuratie-instelling of een geldige doorstuurserver DNS-server configureren.</span><span class="sxs-lookup"><span data-stu-id="e0caf-125">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="e0caf-126">dit door in Serverbeheer klikt u op toodo **extra** > **DNS** tooopen DNS-beheer en dubbelklik vervolgens op **doorstuurservers**.</span><span class="sxs-lookup"><span data-stu-id="e0caf-126">toodo this, in Server Manager click **Tools** > **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0caf-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e0caf-127">Next steps</span></span>
* <span data-ttu-id="e0caf-128">Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](hpcpack-cluster.md) voor informatie over ondersteunde Linux-distributies, verplaatsen van gegevens en verzenden van taken tooan HPC Pack cluster met Linux rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="e0caf-128">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for information about supported Linux distributions, moving data, and submitting jobs tooan HPC Pack cluster with Linux compute nodes.</span></span>
* <span data-ttu-id="e0caf-129">Voor de zelfstudies die gebruikmaken van Hallo script toocreate een cluster en een Linux HPC-werkbelasting uitvoeren, Zie:</span><span class="sxs-lookup"><span data-stu-id="e0caf-129">For tutorials that use hello script toocreate a cluster and run a Linux HPC workload, see:</span></span>
  * [<span data-ttu-id="e0caf-130">Voer NAMD met Microsoft HPC Pack op Linux-rekenknooppunten in Azure</span><span class="sxs-lookup"><span data-stu-id="e0caf-130">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
  * [<span data-ttu-id="e0caf-131">Voer OpenFOAM met Microsoft HPC Pack op Linux-rekenknooppunten in Azure</span><span class="sxs-lookup"><span data-stu-id="e0caf-131">Run OpenFOAM with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-openfoam.md)
  * [<span data-ttu-id="e0caf-132">Uitvoeren van de STER-CCM + met Microsoft HPC Pack op Linux rekenknooppunten in Azure</span><span class="sxs-lookup"><span data-stu-id="e0caf-132">Run STAR-CCM+ with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-starccm.md)


---
title: aaaLinux compute virtuele machines in een cluster HPC Pack | Microsoft Docs
description: Meer informatie over hoe toocreate en gebruik een Pack HPC-cluster in Azure voor Linux van de high performance computing (HPC)-workloads
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="e0332-103">Aan de slag met Linux-rekenknooppunten in een HPC Pack-cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="e0332-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="e0332-104">Instellen van een [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure met een hoofdknooppunt met Windows Server en meerdere rekenknooppunten met een ondersteunde Linux-distributie.</span><span class="sxs-lookup"><span data-stu-id="e0332-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="e0332-105">Verken opties toomove gegevens tussen Hallo Linux-knooppunten en Hallo Windows-hoofdknooppunt van het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="e0332-105">Explore options toomove data among hello Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="e0332-106">Meer informatie over hoe toosubmit Linux HPC cluster toohello taken.</span><span class="sxs-lookup"><span data-stu-id="e0332-106">Learn how toosubmit Linux HPC jobs toohello cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="e0332-107">Op een hoog niveau hello volgende diagram toont Hallo HPC Pack cluster u maken en bewerken.</span><span class="sxs-lookup"><span data-stu-id="e0332-107">At a high level, hello following diagram shows hello HPC Pack cluster you create and work with.</span></span>

![HPC Pack cluster met Linux-knooppunten][scenario]

<span data-ttu-id="e0332-109">Voor andere opties toorun Linux HPC werkbelastingen in Azure, Zie [technische bronnen voor batchverwerking en high performance computing](../../../batch/big-compute-resources.md).</span><span class="sxs-lookup"><span data-stu-id="e0332-109">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="e0332-110">Een HPC Pack cluster met Linux-rekenknooppunten implementeren</span><span class="sxs-lookup"><span data-stu-id="e0332-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="e0332-111">Dit artikel ziet u twee opties toodeploy een HPC Pack-cluster in Azure met Linux-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="e0332-111">This article shows you two options toodeploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="e0332-112">Beide methoden gebruiken een Marketplace-installatiekopie van Windows Server met HPC Pack toocreate Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="e0332-112">Both methods use a Marketplace image of Windows Server with HPC Pack toocreate hello head node.</span></span> 

* <span data-ttu-id="e0332-113">**Azure Resource Manager-sjabloon** -een sjabloon uit Azure Marketplace hello of een snelstartsjabloon van Hallo-community, tooautomate maken van Hallo-cluster in Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="e0332-113">**Azure Resource Manager template** - Use a template from hello Azure Marketplace, or a quickstart template from hello community, tooautomate creation of hello cluster in hello Resource Manager deployment model.</span></span> <span data-ttu-id="e0332-114">Bijvoorbeeld, Hallo [HPC Pack cluster voor Linux-werkbelastingen](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) sjabloon in hello Azure Marketplace maakt een complete HPC Pack clusterinfrastructuur voor Linux HPC werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="e0332-114">For example, hello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="e0332-115">**PowerShell-script** -gebruik Hallo [Microsoft HPC Pack IaaS-implementatiescript](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**nieuw HpcIaaSCluster.ps1**) tooautomate een volledige Clusterimplementatie Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="e0332-115">**PowerShell script** - Use hello [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate a complete cluster deployment in hello classic deployment model.</span></span> <span data-ttu-id="e0332-116">Deze Azure PowerShell-script maakt gebruik van een installatiekopie van een HPC Pack VM in hello Azure Marketplace voor snelle implementatie en biedt een uitgebreide set configuratie parameters toodeploy Linux-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="e0332-116">This Azure PowerShell script uses an HPC Pack VM image in hello Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters toodeploy Linux compute nodes.</span></span>

<span data-ttu-id="e0332-117">Zie voor meer informatie over opties voor de implementatie van HPC Pack cluster in Azure [toocreate opties en beheren van een cluster high performance computing (HPC) in Azure met Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0332-117">For more information about HPC Pack cluster deployment options in Azure, see [Options toocreate and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e0332-118">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e0332-118">Prerequisites</span></span>
* <span data-ttu-id="e0332-119">**Azure-abonnement** -kunt u een abonnement in beide hello Azure globale of Azure China-service.</span><span class="sxs-lookup"><span data-stu-id="e0332-119">**Azure subscription** - You can use a subscription in either hello Azure Global or Azure China service.</span></span> <span data-ttu-id="e0332-120">Als u geen account hebt, kunt u een [gratis account](https://azure.microsoft.com/pricing/free-trial/) binnen een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="e0332-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="e0332-121">**Quotum voor kernen** -moet u mogelijk tooincrease Hallo quotum van kernen, met name als u verschillende clusterknooppunten met multicore VM-grootten toodeploy kiezen.</span><span class="sxs-lookup"><span data-stu-id="e0332-121">**Cores quota** - You might need tooincrease hello quota of cores, especially if you choose toodeploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="e0332-122">tooincrease een quotum, opent u een ondersteuningsaanvraag online klant zonder kosten.</span><span class="sxs-lookup"><span data-stu-id="e0332-122">tooincrease a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="e0332-123">**Linux-distributies** -momenteel HPC Pack Hallo volgende Linux-distributies rekenknooppunten ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="e0332-123">**Linux distributions** - Currently HPC Pack supports hello following Linux distributions for compute nodes.</span></span> <span data-ttu-id="e0332-124">U kunt Marketplace-versies van deze verdelingen gebruiken indien beschikbaar, of geef uw eigen.</span><span class="sxs-lookup"><span data-stu-id="e0332-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="e0332-125">**Op basis van centOS**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span><span class="sxs-lookup"><span data-stu-id="e0332-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="e0332-126">**Red Hat Enterprise Linux**: 6.7, 6,8, 7.2</span><span class="sxs-lookup"><span data-stu-id="e0332-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="e0332-127">**SUSE Linux Enterprise Server**: SLES 12 SLES 12 (Premium) SLES 12 SP1, SLES 12 SP1 (Premium) SLES 12 voor HPC SLES 12 voor HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="e0332-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="e0332-128">**Ubuntu Server**: 14.04 TNS, 16.04 TNS</span><span class="sxs-lookup"><span data-stu-id="e0332-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="e0332-129">toouse hello Azure RDMA-netwerk met een van de RDMA-compatibele Hallo VM-grootten, Geef een SUSE Linux Enterprise Server 12 HPC of op basis van CentOS HPC-installatiekopie uit hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e0332-129">toouse hello Azure RDMA network with one of hello RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from hello Azure Marketplace.</span></span> <span data-ttu-id="e0332-130">Zie voor meer informatie [hoge prestaties compute-VM-grootten](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0332-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="e0332-131">Aanvullende vereisten toodeploy Hallo-cluster met behulp van Hallo HPC Pack IaaS-implementatiescript:</span><span class="sxs-lookup"><span data-stu-id="e0332-131">Additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="e0332-132">**Clientcomputer** -u moet een implementatiescript van Windows-clientapparaten computer toorun Hallo cluster.</span><span class="sxs-lookup"><span data-stu-id="e0332-132">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="e0332-133">**Azure PowerShell** - [installeren en configureren van Azure PowerShell](/powershell/azure/overview) (versie 0.8.10 of hoger) op de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="e0332-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="e0332-134">**HPC Pack IaaS-implementatiescript** - downloaden en uitpakken Hallo meest recente versie van script Hallo van Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="e0332-134">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="e0332-135">U kunt Hallo-versie van script Hallo controleren door te voeren `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="e0332-135">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="e0332-136">In dit artikel is gebaseerd op versie 4.4.1 of hoger van Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="e0332-136">This article is based on version 4.4.1 or later of hello script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="e0332-137">Implementatieoptie 1.</span><span class="sxs-lookup"><span data-stu-id="e0332-137">Deployment option 1.</span></span> <span data-ttu-id="e0332-138">Een Resource Manager-sjabloon gebruiken</span><span class="sxs-lookup"><span data-stu-id="e0332-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="e0332-139">Ga toohello [HPC Pack cluster voor Linux-werkbelastingen](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) sjabloon in Azure Marketplace Hallo en klik op **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="e0332-139">Go toohello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="e0332-140">In Azure-portal hello, Hallo informatie bekijken en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="e0332-140">In hello Azure portal, review hello information and then click **Create**.</span></span>
   
    ![Maken van de portal][portal]
3. <span data-ttu-id="e0332-142">Op Hallo **basisbeginselen** blade een naam voor het Hallo-cluster, die ook de namen van hoofdknooppunt Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="e0332-142">On hello **Basics** blade, enter a name for hello cluster, which also names hello head node VM.</span></span> <span data-ttu-id="e0332-143">U kunt een bestaande resourcegroep kiezen of een groep voor de implementatie van Hallo maken in een locatie die beschikbaar tooyou.</span><span class="sxs-lookup"><span data-stu-id="e0332-143">You can choose an existing resource group or create a group for hello deployment in a location that's available tooyou.</span></span> <span data-ttu-id="e0332-144">Hallo locatie is van invloed op Hallo beschikbaarheid van bepaalde VM-grootten en andere Azure-services (Zie [producten die beschikbaar zijn in elke regio](https://azure.microsoft.com/regions/services/)).</span><span class="sxs-lookup"><span data-stu-id="e0332-144">hello location affects hello availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="e0332-145">Op Hallo **Head knooppunt instellingen** blade voor een eerste implementatie, kunt u in het algemeen Hallo standaardinstellingen accepteren.</span><span class="sxs-lookup"><span data-stu-id="e0332-145">On hello **Head node settings** blade, for a first deployment, you can generally accept hello default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e0332-146">Hallo **post-configuratiescript URL** is een optionele instelling toospecify openbaar beschikbare Windows PowerShell-script dat u toorun op Hallo hoofdknooppunt VM wilt nadat deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e0332-146">hello **Post-configuration script URL** is an optional setting toospecify a publicly available Windows PowerShell script that you want toorun on hello head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="e0332-147">Op Hallo **Compute knooppunt instellingen** blade selecteren van een naamgevingspatroon uit voor het Hallo-knooppunten, Hallo aantal en grootte van Hallo knooppunten en Linux-distributie toodeploy Hallo.</span><span class="sxs-lookup"><span data-stu-id="e0332-147">On hello **Compute node settings** blade, select a naming pattern for hello nodes, hello number and size of hello nodes, and hello Linux distribution toodeploy.</span></span>
6. <span data-ttu-id="e0332-148">Op Hallo **infrastructuurinstellingen** blade Voer namen voor Hallo virtueel netwerk en Active Directory domain, domein en VM-beheerdersreferenties en naamgevingspatroon uit een voor Hallo storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="e0332-148">On hello **Infrastructure settings** blade, enter names for hello virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for hello storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e0332-149">HPC Pack Hallo Active Directory-domein tooauthenticate cluster gebruikers gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e0332-149">HPC Pack uses hello Active Directory domain tooauthenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="e0332-150">Nadat de validatietests Hallo uitgevoerd en u de gebruiksvoorwaarden Hallo bekijken, klikt u op **aankoop**.</span><span class="sxs-lookup"><span data-stu-id="e0332-150">After hello validation tests run and you review hello terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a><span data-ttu-id="e0332-151">Implementatieoptie 2.</span><span class="sxs-lookup"><span data-stu-id="e0332-151">Deployment option 2.</span></span> <span data-ttu-id="e0332-152">Hallo IaaS-implementatiescript gebruiken</span><span class="sxs-lookup"><span data-stu-id="e0332-152">Use hello IaaS deployment script</span></span>
<span data-ttu-id="e0332-153">Hieronder vindt u aanvullende vereisten toodeploy Hallo cluster met behulp van Hallo HPC Pack IaaS-implementatiescript:</span><span class="sxs-lookup"><span data-stu-id="e0332-153">Following are additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="e0332-154">**Clientcomputer** -u moet een implementatiescript van Windows-clientapparaten computer toorun Hallo cluster.</span><span class="sxs-lookup"><span data-stu-id="e0332-154">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="e0332-155">**Azure PowerShell** - [installeren en configureren van Azure PowerShell](/powershell/azure/overview) (versie 0.8.10 of hoger) op de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="e0332-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="e0332-156">**HPC Pack IaaS-implementatiescript** - downloaden en uitpakken Hallo meest recente versie van script Hallo van Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="e0332-156">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="e0332-157">U kunt Hallo-versie van script Hallo controleren door te voeren `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="e0332-157">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="e0332-158">In dit artikel is gebaseerd op versie 4.4.1 of hoger van Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="e0332-158">This article is based on version 4.4.1 or later of hello script.</span></span>

<span data-ttu-id="e0332-159">**XML-configuratiebestand**</span><span class="sxs-lookup"><span data-stu-id="e0332-159">**XML configuration file**</span></span>

<span data-ttu-id="e0332-160">een XML-configuratiebestand Hallo HPC Pack IaaS-implementatiescript gebruikt als invoer toodescribe Hallo HPC-cluster.</span><span class="sxs-lookup"><span data-stu-id="e0332-160">hello HPC Pack IaaS deployment script uses an XML configuration file as input toodescribe hello  HPC cluster.</span></span> <span data-ttu-id="e0332-161">Hallo geeft volgende voorbeeldconfiguratiebestand een kort cluster die bestaan uit een hoofdknooppunt HPC Pack en twee grootte A7 CentOS 7.0 Linux-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="e0332-161">hello following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="e0332-162">Hallo-bestand aanpassen nodig zijn voor uw omgeving en de configuratie van het gewenste cluster en sla het bestand met een naam, zoals HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="e0332-162">Modify hello file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="e0332-163">U moet bijvoorbeeld toosupply de abonnementsnaam van uw en een unieke opslagaccountnaam en de naam van cloud-service.</span><span class="sxs-lookup"><span data-stu-id="e0332-163">For example, you need toosupply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="e0332-164">U kunt bovendien toochoose een andere Linux installatiekopie Hallo rekenknooppunten ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e0332-164">Additionally, you might want toochoose a different supported Linux image for hello compute nodes.</span></span> <span data-ttu-id="e0332-165">Zie voor meer informatie over het Hallo-elementen in het configuratiebestand Hallo Hallo Manual.rtf bestand in map voor Hallo-script en [een HPC-cluster maken met Hallo HPC Pack IaaS-implementatiescript](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0332-165">For more information about hello elements in hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="e0332-166">**toorun hello HPC Pack IaaS-implementatiescript**</span><span class="sxs-lookup"><span data-stu-id="e0332-166">**toorun hello HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="e0332-167">Open Windows PowerShell op de clientcomputer Hallo als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e0332-167">Open Windows PowerShell on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="e0332-168">Wijziging toohello uit de map waar het Hallo-script is geïnstalleerd (E:\IaaSClusterScript in dit voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="e0332-168">Change directory toohello folder where hello script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="e0332-169">Hallo na de opdracht toodeploy Hallo HPC Pack cluster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e0332-169">Run hello following command toodeploy hello HPC Pack cluster.</span></span> <span data-ttu-id="e0332-170">In dit voorbeeld wordt ervan uitgegaan dat configuratiebestand Hallo bevindt zich in E:\HPCDemoConfig.xml</span><span class="sxs-lookup"><span data-stu-id="e0332-170">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="e0332-171">a.</span><span class="sxs-lookup"><span data-stu-id="e0332-171">a.</span></span> <span data-ttu-id="e0332-172">Omdat Hallo **AdminPassword** is niet opgegeven in Hallo voorafgaand aan de opdracht, bent u na vragen aan gebruiker tooenter Hallo wachtwoord voor gebruiker *MyAdminName*.</span><span class="sxs-lookup"><span data-stu-id="e0332-172">Because hello **AdminPassword** is not specified in hello preceding command, you are prompted tooenter hello password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="e0332-173">b.</span><span class="sxs-lookup"><span data-stu-id="e0332-173">b.</span></span> <span data-ttu-id="e0332-174">Hallo-script wordt gestart toovalidate Hallo-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="e0332-174">hello script then starts toovalidate hello configuration file.</span></span> <span data-ttu-id="e0332-175">Tooseveral minuten, afhankelijk van de netwerkverbinding Hallo kan duren.</span><span class="sxs-lookup"><span data-stu-id="e0332-175">It can take up tooseveral minutes depending on hello network connection.</span></span>
   
    ![Validatie][validate]
   
    <span data-ttu-id="e0332-177">c.</span><span class="sxs-lookup"><span data-stu-id="e0332-177">c.</span></span> <span data-ttu-id="e0332-178">Nadat de validaties doorgeven, bevat Hallo script Hallo cluster resources toocreate.</span><span class="sxs-lookup"><span data-stu-id="e0332-178">After validations pass, hello script lists hello cluster resources toocreate.</span></span> <span data-ttu-id="e0332-179">Voer *Y* toocontinue.</span><span class="sxs-lookup"><span data-stu-id="e0332-179">Enter *Y* toocontinue.</span></span>
   
    ![Resources][resources]
   
    <span data-ttu-id="e0332-181">d.</span><span class="sxs-lookup"><span data-stu-id="e0332-181">d.</span></span> <span data-ttu-id="e0332-182">Hallo script start toodeploy Hallo HPC Pack cluster en Hallo-configuratie zonder verdere handmatige stappen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e0332-182">hello script starts toodeploy hello HPC Pack cluster and completes hello configuration without further manual steps.</span></span> <span data-ttu-id="e0332-183">Hallo-script kunt uitvoeren voor enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="e0332-183">hello script can run for several minutes.</span></span>
   
    ![Implementeren][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="e0332-185">In dit voorbeeld Hallo script genereert een logboekbestand automatisch sinds Hallo **- LogFile** parameter is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e0332-185">In this example, hello script generates a log file automatically since hello **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="e0332-186">Hallo-Logboeken in realtime niet worden geschreven, maar worden verzameld achter Hallo Hallo validatie en Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="e0332-186">hello logs aren't written in real time, but are collected at hello end of hello validation and hello deployment.</span></span> <span data-ttu-id="e0332-187">Als Hallo PowerShell-proces is gestopt tijdens het Hallo-script wordt uitgevoerd, is enkele logboeken gaan verloren.</span><span class="sxs-lookup"><span data-stu-id="e0332-187">If hello PowerShell process is stopped while hello script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-toohello-head-node"></a><span data-ttu-id="e0332-188">Verbinding maken met het hoofdknooppunt toohello</span><span class="sxs-lookup"><span data-stu-id="e0332-188">Connect toohello head node</span></span>
<span data-ttu-id="e0332-189">Nadat u Hallo HPC Pack cluster in Azure worden geïmplementeerd [verbinding maken met extern bureaublad](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello hoofdknooppunt VM gebruik Hallo domeinreferenties die u hebt opgegeven tijdens de implementatie Hallo-cluster (bijvoorbeeld *hpc\\ clusteradmin*).</span><span class="sxs-lookup"><span data-stu-id="e0332-189">After you deploy hello HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="e0332-190">U beheren Hallo cluster vanaf het hoofdknooppunt Hallo.</span><span class="sxs-lookup"><span data-stu-id="e0332-190">You manage hello cluster from hello head node.</span></span>

<span data-ttu-id="e0332-191">Start op het hoofdknooppunt Hallo HPC Cluster Manager toocheck Hallo status van Hallo HPC Pack cluster.</span><span class="sxs-lookup"><span data-stu-id="e0332-191">On hello head node, start HPC Cluster Manager toocheck hello status of hello HPC Pack cluster.</span></span> <span data-ttu-id="e0332-192">U kunt beheren en bewaken van Linux-rekenknooppunten hello dezelfde manier werken met Windows rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="e0332-192">You can manage and monitor Linux compute nodes hello same way you work with Windows compute nodes.</span></span> <span data-ttu-id="e0332-193">Zie bijvoorbeeld Hallo Linux-knooppunten die worden vermeld in **bronbeheer** (deze knooppunten worden geïmplementeerd met Hallo **LinuxNode** sjabloon).</span><span class="sxs-lookup"><span data-stu-id="e0332-193">For example, you see hello Linux nodes listed in **Resource Management** (these nodes are deployed with hello **LinuxNode** template).</span></span>

![Knooppunt Management][management]

<span data-ttu-id="e0332-195">U ziet ook Hallo Linux-knooppunten in Hallo **Heatmap** weergeven.</span><span class="sxs-lookup"><span data-stu-id="e0332-195">You also see hello Linux nodes in hello **Heat Map** view.</span></span>

![Heatmap][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="e0332-197">Hoe toomove gegevens in een cluster met Linux-knooppunten</span><span class="sxs-lookup"><span data-stu-id="e0332-197">How toomove data in a cluster with Linux nodes</span></span>
<span data-ttu-id="e0332-198">U hebt verschillende opties toomove gegevens tussen Linux-knooppunten en Hallo Windows-hoofdknooppunt van het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="e0332-198">You have several choices toomove data among Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="e0332-199">Hier volgen drie algemene methoden in de volgende secties Hallo uitvoeriger beschreven:</span><span class="sxs-lookup"><span data-stu-id="e0332-199">Here are three common methods, described in more detail in hello following sections:</span></span>

* <span data-ttu-id="e0332-200">**Azure File** -gegarandeerd dat een beheerde SMB-share toostore bestandsgegevens in Azure-opslag-bestanden.</span><span class="sxs-lookup"><span data-stu-id="e0332-200">**Azure File** - Exposes a managed SMB file share toostore data files in Azure storage.</span></span> <span data-ttu-id="e0332-201">Knooppunten voor Windows en Linux-knooppunten een Azure-bestandsshare kunnen koppelen als een station of een map op Hallo dezelfde tijd, zelfs als ze zijn geïmplementeerd in verschillende virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="e0332-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at hello same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="e0332-202">**Hoofdknooppunt SMB-share** -koppelt een standaard gedeelde Windows-map van het hoofdknooppunt Hallo op Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="e0332-202">**Head node SMB share** - Mounts a standard Windows shared folder of hello head node on Linux nodes.</span></span>
* <span data-ttu-id="e0332-203">**HEAD knooppunt NFS-server** -biedt een oplossing voor het delen van bestanden voor een gemengde omgeving van Windows en Linux.</span><span class="sxs-lookup"><span data-stu-id="e0332-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="e0332-204">Azure File storage</span><span class="sxs-lookup"><span data-stu-id="e0332-204">Azure File storage</span></span>
<span data-ttu-id="e0332-205">Hallo [Azure File](https://azure.microsoft.com/services/storage/files/) -service geeft bestandsshares met behulp van Hallo standaard SMB 2.1-protocol.</span><span class="sxs-lookup"><span data-stu-id="e0332-205">hello [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using hello standard SMB 2.1 protocol.</span></span> <span data-ttu-id="e0332-206">Azure virtuele machines en cloudservices kunnen bestandsgegevens delen tussen toepassingsonderdelen via gekoppelde shares en on-premises toepassingen hebben toegang tot bestandsgegevens in een share via Hallo File storage-API.</span><span class="sxs-lookup"><span data-stu-id="e0332-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through hello File storage API.</span></span> 

<span data-ttu-id="e0332-207">Zie voor gedetailleerde stappen toocreate een Azure-bestand delen en koppel deze aan Hallo hoofdknooppunt [aan de slag met Azure File storage in Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span><span class="sxs-lookup"><span data-stu-id="e0332-207">For detailed steps toocreate an Azure File share and mount it on hello head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="e0332-208">toomount hello Azure-bestandsshare op Hallo van Linux-knooppunten, Zie [hoe toouse Azure File storage met Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e0332-208">toomount hello Azure File share on hello Linux nodes, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="e0332-209">Zie tooset persistent maken verbindingen [Persisting verbindingen tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0332-209">tooset up persisting connections, see [Persisting connections tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="e0332-210">In Hallo voorbeeld te volgen, maakt u een Azure-bestandsshare op een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e0332-210">In hello following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="e0332-211">Hallo toomount delen op Hallo hoofdknooppunt, open een opdrachtprompt en voert u Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="e0332-211">toomount hello share on hello head node, open a Command Prompt and enter hello following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="e0332-212">In dit voorbeeld allvhdsje is de naam van uw opslagaccount, storageaccountkey is de sleutel van uw opslagaccount en rdma is hello Azure File-sharenaam.</span><span class="sxs-lookup"><span data-stu-id="e0332-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is hello Azure File share name.</span></span> <span data-ttu-id="e0332-213">Hello Azure-bestandsshare is gekoppeld als Z: op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="e0332-213">hello Azure File share is mounted as Z: on hello head node.</span></span>

<span data-ttu-id="e0332-214">toomount hello Azure-bestandsshare op Linux-knooppunten, voer een **clusrun** opdracht op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="e0332-214">toomount hello Azure File share on Linux nodes, run a **clusrun** command on hello head node.</span></span> <span data-ttu-id="e0332-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)**  is een nuttig HPC Pack hulpprogramma toocarry administratieve taken op meerdere knooppunten.</span><span class="sxs-lookup"><span data-stu-id="e0332-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool toocarry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="e0332-216">(Zie ook [Clusrun voor Linux-knooppunten](#Clusrun-for-Linux-nodes) in dit artikel.)</span><span class="sxs-lookup"><span data-stu-id="e0332-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="e0332-217">Open een Windows PowerShell-venster en Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="e0332-217">Open a Windows PowerShell window and enter hello following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="e0332-218">de eerste opdracht Hallo maakt een map met de naam /rdma op alle knooppunten in Hallo LinuxNodes groep.</span><span class="sxs-lookup"><span data-stu-id="e0332-218">hello first command creates a folder named /rdma on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="e0332-219">de tweede opdracht Hallo koppelt hello Azure File share allvhdsjw.file.core.windows.net/rdma op Hallo /rdma map met dir en de bestandsnaam modus bits set too777.</span><span class="sxs-lookup"><span data-stu-id="e0332-219">hello second command mounts hello Azure File share allvhdsjw.file.core.windows.net/rdma onto hello /rdma folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="e0332-220">In de tweede opdracht Hallo allvhdsje is de naam van uw opslagaccount en storageaccountkey is sleutel van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e0332-220">In hello second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="e0332-221">Hallo '\\`' symbool in de tweede opdracht Hallo is een escapeteken voor PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0332-221">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="e0332-222">"\\`, 'betekent dat Hallo', ' (door komma's teken) maakt deel uit van Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="e0332-222">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="e0332-223">Hoofdknooppunt share</span><span class="sxs-lookup"><span data-stu-id="e0332-223">Head node share</span></span>
<span data-ttu-id="e0332-224">U kunt ook een gedeelde map van het hoofdknooppunt Hallo op Linux-knooppunten koppelen.</span><span class="sxs-lookup"><span data-stu-id="e0332-224">Alternatively, mount a shared folder of hello head node on Linux nodes.</span></span> <span data-ttu-id="e0332-225">Een share bevat Hallo eenvoudigste manier waarop tooshare bestanden, maar Hallo hoofdknooppunt en alle Linux-knooppunten moeten worden geïmplementeerd in Hallo hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="e0332-225">A share provides hello simplest way tooshare files, but hello head node and all Linux nodes must be deployed in hello same virtual network.</span></span> <span data-ttu-id="e0332-226">Hier volgen de stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="e0332-226">Here are hello steps.</span></span>

1. <span data-ttu-id="e0332-227">Maak een map op het hoofdknooppunt Hallo en tooEveryone delen met de machtiging lezen/schrijven.</span><span class="sxs-lookup"><span data-stu-id="e0332-227">Create a folder on hello head node and share it tooEveryone with Read/Write permissions.</span></span> <span data-ttu-id="e0332-228">Bijvoorbeeld D:\OpenFOAM delen op Hallo hoofdknooppunt als \\CentOS7RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="e0332-228">For example, share D:\OpenFOAM on hello head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="e0332-229">Hier volgt CentOS7RDMA HN Hallo hostname van Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="e0332-229">Here CentOS7RDMA-HN is hello hostname of hello head node.</span></span>
   
    ![Machtigingen voor de bestandsshare][fileshareperms]
   
    ![Delen van bestanden][filesharing]
2. <span data-ttu-id="e0332-232">Open een Windows PowerShell-venster en Voer Hallo volgende opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="e0332-232">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="e0332-233">de eerste opdracht Hallo maakt een map met de naam /openfoam op alle knooppunten in Hallo LinuxNodes groep.</span><span class="sxs-lookup"><span data-stu-id="e0332-233">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="e0332-234">de tweede opdracht Hallo koppelt Hallo gedeelde map //CentOS7RDMA-HN/OpenFOAM op Hallo-map met dir en de bestandsnaam modus bits set too777.</span><span class="sxs-lookup"><span data-stu-id="e0332-234">hello second command mounts hello shared folder //CentOS7RDMA-HN/OpenFOAM onto hello folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="e0332-235">Hallo moet gebruikersnaam en wachtwoord in Hallo-opdracht Hallo gebruikersnaam en wachtwoord van een gebruiker van het cluster op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="e0332-235">hello username and password in hello command should be hello username and password of a cluster user on hello head node.</span></span> <span data-ttu-id="e0332-236">(Zie [toevoegen of verwijderen cluster gebruikers](https://technet.microsoft.com/library/ff919330.aspx).)</span><span class="sxs-lookup"><span data-stu-id="e0332-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="e0332-237">Hallo '\\`' symbool in de tweede opdracht Hallo is een escapeteken voor PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0332-237">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="e0332-238">"\\`, 'betekent dat Hallo', ' (door komma's teken) maakt deel uit van Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="e0332-238">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="e0332-239">NFS-server</span><span class="sxs-lookup"><span data-stu-id="e0332-239">NFS server</span></span>
<span data-ttu-id="e0332-240">Hallo NFS-service kunt u tooshare en migreren van bestanden tussen computers met besturingssystemen Hallo Windows Server 2012 met behulp van SMB-protocol Hallo en met Hallo NFS-protocol op basis van Linux-computers.</span><span class="sxs-lookup"><span data-stu-id="e0332-240">hello NFS service enables you tooshare and migrate files between computers running hello Windows Server 2012 operating system using hello SMB protocol and Linux-based computers using hello NFS protocol.</span></span> <span data-ttu-id="e0332-241">Hallo NFS-server en alle andere knooppunten hebben geïmplementeerd in Hallo toobe hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="e0332-241">hello NFS server and all other nodes have toobe deployed in hello same virtual network.</span></span> <span data-ttu-id="e0332-242">Dit biedt betere compatibiliteit met Linux-knooppunten vergeleken met een SMB-share.</span><span class="sxs-lookup"><span data-stu-id="e0332-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="e0332-243">Bijvoorbeeld: het bestandskoppelingen ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="e0332-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="e0332-244">tooinstall en stelt u de NFS-server stappen Hallo in [Server voor Network File System-eerste Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0332-244">tooinstall and set up an NFS server, follow hello steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="e0332-245">Maak bijvoorbeeld een NFS-share met de naam nfs Hello volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="e0332-245">For example, create an NFS share named nfs with hello following properties:</span></span>
   
    ![NFS-autorisatie][nfsauth]
   
    ![NFS-sharemachtigingen][nfsshare]
   
    ![NFS-NTFS-machtigingen][nfsperm]
   
    ![Eigenschappen van de NFS-beheer][nfsmanage]
2. <span data-ttu-id="e0332-250">Open een Windows PowerShell-venster en Voer Hallo volgende opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="e0332-250">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="e0332-251">de eerste opdracht Hallo maakt een map met de naam /nfsshared op alle knooppunten in Hallo LinuxNodes groep.</span><span class="sxs-lookup"><span data-stu-id="e0332-251">hello first command creates a folder named /nfsshared on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="e0332-252">Hallo tweede opdracht koppelingen Hallo NFS delen CentOS7RDMA HN: / nfs op Hallo map.</span><span class="sxs-lookup"><span data-stu-id="e0332-252">hello second command mounts hello NFS share CentOS7RDMA-HN:/nfs onto hello folder.</span></span> <span data-ttu-id="e0332-253">Hier CentOS7RDMA HN:-nfs Hallo extern pad van de NFS-share is.</span><span class="sxs-lookup"><span data-stu-id="e0332-253">Here CentOS7RDMA-HN:/nfs is hello remote path of your NFS share.</span></span>

## <a name="how-toosubmit-jobs"></a><span data-ttu-id="e0332-254">Hoe toosubmit taken</span><span class="sxs-lookup"><span data-stu-id="e0332-254">How toosubmit jobs</span></span>
<span data-ttu-id="e0332-255">Er zijn verschillende manieren toosubmit taken toohello HPC Pack cluster:</span><span class="sxs-lookup"><span data-stu-id="e0332-255">There are several ways toosubmit jobs toohello HPC Pack cluster:</span></span>

* <span data-ttu-id="e0332-256">HPC Cluster Manager of HPC Job Manager GUI</span><span class="sxs-lookup"><span data-stu-id="e0332-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="e0332-257">HPC-webportal</span><span class="sxs-lookup"><span data-stu-id="e0332-257">HPC web portal</span></span>
* <span data-ttu-id="e0332-258">REST API</span><span class="sxs-lookup"><span data-stu-id="e0332-258">REST API</span></span>

<span data-ttu-id="e0332-259">Verzending van de taak toohello cluster in Azure via HPC Pack GUI-hulpprogramma's en Hallo HPC-webportal Hallo zijn dezelfde als voor Windows-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="e0332-259">Job submission toohello cluster in Azure via HPC Pack GUI tools and hello HPC web portal are hello same as for Windows compute nodes.</span></span> <span data-ttu-id="e0332-260">Zie [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) en [hoe toosubmit taken uit een on-premises clientcomputer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0332-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How toosubmit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="e0332-261">toosubmit-taken via Hallo REST-API te verwijzen[maken en verzenden van taken op met de REST-API in Microsoft HPC Pack Hallo](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0332-261">toosubmit jobs via hello REST API, refer too[Creating and Submitting Jobs by Using hello REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="e0332-262">toosubmit taken van een Linux-client ook verwijzen toohello Python voorbeeld in Hallo [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span><span class="sxs-lookup"><span data-stu-id="e0332-262">toosubmit jobs from a Linux client, also refer toohello Python sample in hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="e0332-263">Clusrun voor Linux-knooppunten</span><span class="sxs-lookup"><span data-stu-id="e0332-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="e0332-264">HPC Pack Hallo [clusrun](https://technet.microsoft.com/library/cc947685.aspx) hulpprogramma kan worden gebruikt tooexecute opdrachten op Linux-knooppunten via een opdrachtprompt of HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="e0332-264">hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used tooexecute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="e0332-265">Hier volgen enkele eenvoudige voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="e0332-265">Following are some basic examples.</span></span>

* <span data-ttu-id="e0332-266">Huidige gebruikersnamen op alle knooppunten in cluster Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="e0332-266">Show current user names on all nodes in hello cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="e0332-267">Hallo installeren **gdb** foutopsporingsprogramma met **yum** op alle knooppunten in Hallo linuxnodes groeperen en Hallo knooppunten na 10 minuten opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="e0332-267">Install hello **gdb** debugger tool with **yum** on all nodes in hello linuxnodes group and then restart hello nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="e0332-268">Een weergave van elk getal van 1 tot en met 10 voor één seconde op elk knooppunt van Linux in Hallo cluster shell-script maken, uitvoeren en de uitvoer van Hallo knooppunten onmiddellijk weergeven.</span><span class="sxs-lookup"><span data-stu-id="e0332-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in hello cluster, run it, and show output from hello nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="e0332-269">Mogelijk moet u toouse bepaalde escape-tekens in **clusrun** opdrachten.</span><span class="sxs-lookup"><span data-stu-id="e0332-269">You might need toouse certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="e0332-270">Zoals u in dit voorbeeld, gebruik ^ in een opdrachtprompt tooescape Hallo ' > ' symbool.</span><span class="sxs-lookup"><span data-stu-id="e0332-270">As shown in this example, use ^ in a Command Prompt tooescape hello ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e0332-271">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e0332-271">Next steps</span></span>
* <span data-ttu-id="e0332-272">Probeer schaalt Hallo cluster tooa groter aantal knooppunten of het uitvoeren van een Linux-werkbelasting op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="e0332-272">Try scaling up hello cluster tooa larger number of nodes, or try running a Linux workload on hello cluster.</span></span> <span data-ttu-id="e0332-273">Zie voor een voorbeeld [NAMD uitvoeren met Microsoft HPC Pack op Linux-rekenknooppunten in Azure](hpcpack-cluster-namd.md).</span><span class="sxs-lookup"><span data-stu-id="e0332-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="e0332-274">Probeer een cluster met [RDMA-functionaliteit, rekenintensieve VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI-belastingen.</span><span class="sxs-lookup"><span data-stu-id="e0332-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI workloads.</span></span> <span data-ttu-id="e0332-275">Zie voor een voorbeeld [OpenFOAM uitvoeren met Microsoft HPC Pack op een Linux RDMA-cluster in Azure](hpcpack-cluster-openfoam.md).</span><span class="sxs-lookup"><span data-stu-id="e0332-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="e0332-276">Als u geïnteresseerd bent in het werken met Linux-knooppunten in een on-premises HPC Pack-cluster, raadpleegt u Hallo [TechNet richtlijnen](https://technet.microsoft.com/library/mt595803.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0332-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see hello [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png

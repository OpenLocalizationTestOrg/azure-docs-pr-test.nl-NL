---
title: Linux VM's in een cluster HPC Pack compute | Microsoft Docs
description: Meer informatie over het maken en gebruiken van een HPC Pack-cluster in Azure voor Linux van de high performance computing (HPC)-workloads
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
ms.openlocfilehash: 809d3944311badf265117d353b65642e044d900c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="2c4af-103">Aan de slag met Linux-rekenknooppunten in een HPC Pack-cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="2c4af-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="2c4af-104">Instellen van een [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure met een hoofdknooppunt met Windows Server en meerdere rekenknooppunten met een ondersteunde Linux-distributie.</span><span class="sxs-lookup"><span data-stu-id="2c4af-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="2c4af-105">Gebruik de opties voor het verplaatsen van gegevens tussen de Linux-knooppunten en het Windows-hoofdknooppunt van het cluster.</span><span class="sxs-lookup"><span data-stu-id="2c4af-105">Explore options to move data among the Linux nodes and the Windows head node of the cluster.</span></span> <span data-ttu-id="2c4af-106">Informatie over het verzenden van Linux HPC-taken voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="2c4af-106">Learn how to submit Linux HPC jobs to the cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="2c4af-107">Op een hoog niveau ziet het volgende diagram u het cluster HPC Pack u maken en bewerken.</span><span class="sxs-lookup"><span data-stu-id="2c4af-107">At a high level, the following diagram shows the HPC Pack cluster you create and work with.</span></span>

![HPC Pack cluster met Linux-knooppunten][scenario]

<span data-ttu-id="2c4af-109">Zie voor andere opties voor het gebruik van de Linux HPC workloads in Azure, [technische bronnen voor batchverwerking en high performance computing](../../../batch/big-compute-resources.md).</span><span class="sxs-lookup"><span data-stu-id="2c4af-109">For other options to run Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="2c4af-110">Een HPC Pack cluster met Linux-rekenknooppunten implementeren</span><span class="sxs-lookup"><span data-stu-id="2c4af-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="2c4af-111">Dit artikel ziet u twee opties voor het implementeren van een HPC Pack-cluster in Azure met Linux-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="2c4af-111">This article shows you two options to deploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="2c4af-112">Beide methoden voor het gebruik van een Marketplace-installatiekopie van Windows Server met HPC Pack te maken van het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="2c4af-112">Both methods use a Marketplace image of Windows Server with HPC Pack to create the head node.</span></span> 

* <span data-ttu-id="2c4af-113">**Azure Resource Manager-sjabloon** -een sjabloon uit Azure Marketplace, of een sjabloon Quick Start van de community gebruiken voor het automatiseren van het maken van het cluster in het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="2c4af-113">**Azure Resource Manager template** - Use a template from the Azure Marketplace, or a quickstart template from the community, to automate creation of the cluster in the Resource Manager deployment model.</span></span> <span data-ttu-id="2c4af-114">Bijvoorbeeld, de [HPC Pack cluster voor Linux-werkbelastingen](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) sjabloon in Azure Marketplace maakt een complete HPC Pack clusterinfrastructuur voor Linux HPC werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="2c4af-114">For example, the [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in the Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="2c4af-115">**PowerShell-script** -gebruik de [Microsoft HPC Pack IaaS-implementatiescript](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**nieuw HpcIaaSCluster.ps1**) voor het automatiseren van een implementatie van het volledige cluster in het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="2c4af-115">**PowerShell script** - Use the [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) to automate a complete cluster deployment in the classic deployment model.</span></span> <span data-ttu-id="2c4af-116">Deze Azure PowerShell-script maakt gebruik van een installatiekopie van een HPC Pack VM in Azure Marketplace voor snelle implementatie en biedt een uitgebreide set parameters voor de configuratie voor het implementeren van Linux-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="2c4af-116">This Azure PowerShell script uses an HPC Pack VM image in the Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters to deploy Linux compute nodes.</span></span>

<span data-ttu-id="2c4af-117">Zie voor meer informatie over opties voor de implementatie van HPC Pack cluster in Azure [opties voor het maken en beheren van een high performance computing (HPC)-cluster in Azure met Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c4af-117">For more information about HPC Pack cluster deployment options in Azure, see [Options to create and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2c4af-118">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2c4af-118">Prerequisites</span></span>
* <span data-ttu-id="2c4af-119">**Azure-abonnement** -kunt u een abonnement in de globale Azure of Azure China-service.</span><span class="sxs-lookup"><span data-stu-id="2c4af-119">**Azure subscription** - You can use a subscription in either the Azure Global or Azure China service.</span></span> <span data-ttu-id="2c4af-120">Als u geen account hebt, kunt u een [gratis account](https://azure.microsoft.com/pricing/free-trial/) binnen een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="2c4af-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="2c4af-121">**Quotum voor kernen** -moet u mogelijk verhogen van het quotum van kernen, vooral als u kiest voor het implementeren van verschillende clusterknooppunten multicore VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="2c4af-121">**Cores quota** - You might need to increase the quota of cores, especially if you choose to deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="2c4af-122">U kunt een quotum verhogen, door een ondersteuningsaanvraag online klant kosteloos te openen.</span><span class="sxs-lookup"><span data-stu-id="2c4af-122">To increase a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="2c4af-123">**Linux-distributies** -momenteel HPC Pack ondersteunt de volgende Linux-distributies voor rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="2c4af-123">**Linux distributions** - Currently HPC Pack supports the following Linux distributions for compute nodes.</span></span> <span data-ttu-id="2c4af-124">U kunt Marketplace-versies van deze verdelingen gebruiken indien beschikbaar, of geef uw eigen.</span><span class="sxs-lookup"><span data-stu-id="2c4af-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="2c4af-125">**Op basis van centOS**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span><span class="sxs-lookup"><span data-stu-id="2c4af-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="2c4af-126">**Red Hat Enterprise Linux**: 6.7, 6,8, 7.2</span><span class="sxs-lookup"><span data-stu-id="2c4af-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="2c4af-127">**SUSE Linux Enterprise Server**: SLES 12 SLES 12 (Premium) SLES 12 SP1, SLES 12 SP1 (Premium) SLES 12 voor HPC SLES 12 voor HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="2c4af-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="2c4af-128">**Ubuntu Server**: 14.04 TNS, 16.04 TNS</span><span class="sxs-lookup"><span data-stu-id="2c4af-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="2c4af-129">Geef voor het gebruik van het Azure RDMA-netwerk met een van de RDMA-compatibele VM-grootten, een SUSE Linux Enterprise Server 12 HPC of op basis van CentOS HPC-installatiekopie uit Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2c4af-129">To use the Azure RDMA network with one of the RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from the Azure Marketplace.</span></span> <span data-ttu-id="2c4af-130">Zie voor meer informatie [hoge prestaties compute-VM-grootten](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c4af-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="2c4af-131">Aanvullende vereisten voor het implementeren van het cluster met behulp van het implementatiescript HPC Pack IaaS:</span><span class="sxs-lookup"><span data-stu-id="2c4af-131">Additional prerequisites to deploy the cluster by using the HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="2c4af-132">**Clientcomputer** -moet u een Windows-clientcomputer om uit te voeren een script voor de implementatie van het cluster.</span><span class="sxs-lookup"><span data-stu-id="2c4af-132">**Client computer** - You need a Windows-based client computer to run the cluster deployment script.</span></span>
* <span data-ttu-id="2c4af-133">**Azure PowerShell** - [installeren en configureren van Azure PowerShell](/powershell/azure/overview) (versie 0.8.10 of hoger) op de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="2c4af-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="2c4af-134">**HPC Pack IaaS-implementatiescript** - downloaden en uitpakken van de meest recente versie van het script van de [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="2c4af-134">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="2c4af-135">U kunt de versie van het script controleren door te voeren `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="2c4af-135">You can check the version of the script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="2c4af-136">In dit artikel is gebaseerd op versie 4.4.1 of hoger van het script.</span><span class="sxs-lookup"><span data-stu-id="2c4af-136">This article is based on version 4.4.1 or later of the script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="2c4af-137">Implementatieoptie 1.</span><span class="sxs-lookup"><span data-stu-id="2c4af-137">Deployment option 1.</span></span> <span data-ttu-id="2c4af-138">Een Resource Manager-sjabloon gebruiken</span><span class="sxs-lookup"><span data-stu-id="2c4af-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="2c4af-139">Ga naar de [HPC Pack cluster voor Linux-werkbelastingen](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) sjabloon in de Azure Marketplace en op **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="2c4af-139">Go to the [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in the Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="2c4af-140">Lees de informatie in de Azure portal en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="2c4af-140">In the Azure portal, review the information and then click **Create**.</span></span>
   
    ![Maken van de portal][portal]
3. <span data-ttu-id="2c4af-142">Op de **basisbeginselen** blade een naam voor het cluster, die ook de namen van de VM in het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="2c4af-142">On the **Basics** blade, enter a name for the cluster, which also names the head node VM.</span></span> <span data-ttu-id="2c4af-143">U kunt een bestaande resourcegroep kiezen of maken van een groep voor de implementatie op een locatie die voor u beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="2c4af-143">You can choose an existing resource group or create a group for the deployment in a location that's available to you.</span></span> <span data-ttu-id="2c4af-144">De locatie is van invloed op de beschikbaarheid van bepaalde VM-grootten en andere Azure-services (Zie [producten die beschikbaar zijn in elke regio](https://azure.microsoft.com/regions/services/)).</span><span class="sxs-lookup"><span data-stu-id="2c4af-144">The location affects the availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="2c4af-145">Op de **Head knooppunt instellingen** blade voor een eerste implementatie, kunt u in het algemeen de standaardinstellingen accepteren.</span><span class="sxs-lookup"><span data-stu-id="2c4af-145">On the **Head node settings** blade, for a first deployment, you can generally accept the default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="2c4af-146">De **post-configuratiescript URL** is een optionele instelling om op te geven van een openbaar beschikbare Windows PowerShell-script dat u uitvoeren op het hoofdknooppunt VM wilt nadat deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2c4af-146">The **Post-configuration script URL** is an optional setting to specify a publicly available Windows PowerShell script that you want to run on the head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="2c4af-147">Op de **Compute knooppunt instellingen** blade, selecteer een naming patroon voor de knooppunten, het aantal en de grootte van de knooppunten en de Linux-distributie te implementeren.</span><span class="sxs-lookup"><span data-stu-id="2c4af-147">On the **Compute node settings** blade, select a naming pattern for the nodes, the number and size of the nodes, and the Linux distribution to deploy.</span></span>
6. <span data-ttu-id="2c4af-148">Op de **infrastructuurinstellingen** blade invoeren voor het virtuele netwerk en Active Directory-domein, domein en VM-beheerdersreferenties en naamgevingspatroon uit een voor de storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="2c4af-148">On the **Infrastructure settings** blade, enter names for the virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for the storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2c4af-149">HPC Pack maakt gebruik van de Active Directory-domein om gebruikers van de cluster te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="2c4af-149">HPC Pack uses the Active Directory domain to authenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="2c4af-150">Nadat de validatietests worden uitgevoerd en u de gebruiksvoorwaarden bekijken, klikt u op **aankoop**.</span><span class="sxs-lookup"><span data-stu-id="2c4af-150">After the validation tests run and you review the terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-the-iaas-deployment-script"></a><span data-ttu-id="2c4af-151">Implementatieoptie 2.</span><span class="sxs-lookup"><span data-stu-id="2c4af-151">Deployment option 2.</span></span> <span data-ttu-id="2c4af-152">Gebruik het script voor IaaS-implementatie</span><span class="sxs-lookup"><span data-stu-id="2c4af-152">Use the IaaS deployment script</span></span>
<span data-ttu-id="2c4af-153">Hieronder vindt u aanvullende vereisten voor het implementeren van het cluster met behulp van het implementatiescript HPC Pack IaaS:</span><span class="sxs-lookup"><span data-stu-id="2c4af-153">Following are additional prerequisites to deploy the cluster by using the HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="2c4af-154">**Clientcomputer** -moet u een Windows-clientcomputer om uit te voeren een script voor de implementatie van het cluster.</span><span class="sxs-lookup"><span data-stu-id="2c4af-154">**Client computer** - You need a Windows-based client computer to run the cluster deployment script.</span></span>
* <span data-ttu-id="2c4af-155">**Azure PowerShell** - [installeren en configureren van Azure PowerShell](/powershell/azure/overview) (versie 0.8.10 of hoger) op de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="2c4af-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="2c4af-156">**HPC Pack IaaS-implementatiescript** - downloaden en uitpakken van de meest recente versie van het script van de [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="2c4af-156">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="2c4af-157">U kunt de versie van het script controleren door te voeren `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="2c4af-157">You can check the version of the script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="2c4af-158">In dit artikel is gebaseerd op versie 4.4.1 of hoger van het script.</span><span class="sxs-lookup"><span data-stu-id="2c4af-158">This article is based on version 4.4.1 or later of the script.</span></span>

<span data-ttu-id="2c4af-159">**XML-configuratiebestand**</span><span class="sxs-lookup"><span data-stu-id="2c4af-159">**XML configuration file**</span></span>

<span data-ttu-id="2c4af-160">Het implementatiescript HPC Pack IaaS maakt gebruik van een XML-configuratiebestand als invoer om te beschrijven de HPC-cluster.</span><span class="sxs-lookup"><span data-stu-id="2c4af-160">The HPC Pack IaaS deployment script uses an XML configuration file as input to describe the  HPC cluster.</span></span> <span data-ttu-id="2c4af-161">Het volgende voorbeeld-configuratiebestand bevat een kleine cluster die bestaan uit een hoofdknooppunt HPC Pack en twee grootte A7 CentOS 7.0 Linux-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="2c4af-161">The following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="2c4af-162">Wijzigen van het bestand nodig zijn voor uw omgeving en de configuratie van het gewenste cluster en sla het bestand met een naam, zoals HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="2c4af-162">Modify the file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="2c4af-163">Bijvoorbeeld, moet u de abonnementsnaam van uw en de naam van een uniek account op te geven en in de cloud servicenaam.</span><span class="sxs-lookup"><span data-stu-id="2c4af-163">For example, you need to supply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="2c4af-164">U wilt ook kiezen een andere ondersteunde Linux-afbeelding voor de rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="2c4af-164">Additionally, you might want to choose a different supported Linux image for the compute nodes.</span></span> <span data-ttu-id="2c4af-165">Zie het bestand Manual.rtf in de scriptmap voor meer informatie over de elementen in het configuratiebestand en [een HPC-cluster maken met het implementatiescript HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c4af-165">For more information about the elements in the configuration file, see the Manual.rtf file in the script folder and [Create an HPC cluster with the HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

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

<span data-ttu-id="2c4af-166">**Het implementatiescript HPC Pack IaaS uitvoeren**</span><span class="sxs-lookup"><span data-stu-id="2c4af-166">**To run the HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="2c4af-167">Open Windows PowerShell op de clientcomputer als beheerder.</span><span class="sxs-lookup"><span data-stu-id="2c4af-167">Open Windows PowerShell on the client computer as an administrator.</span></span>
2. <span data-ttu-id="2c4af-168">Wijzig de directory naar de map waarin het script is geïnstalleerd (E:\IaaSClusterScript in dit voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="2c4af-168">Change directory to the folder where the script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="2c4af-169">Voer de volgende opdracht voor het implementeren van het cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="2c4af-169">Run the following command to deploy the HPC Pack cluster.</span></span> <span data-ttu-id="2c4af-170">In dit voorbeeld wordt ervan uitgegaan dat het configuratiebestand in E:\HPCDemoConfig.xml bevinden zich</span><span class="sxs-lookup"><span data-stu-id="2c4af-170">This example assumes that the configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="2c4af-171">a.</span><span class="sxs-lookup"><span data-stu-id="2c4af-171">a.</span></span> <span data-ttu-id="2c4af-172">Omdat de **AdminPassword** niet is opgegeven in de voorgaande opdracht u wordt gevraagd het wachtwoord invoeren voor de gebruiker *MyAdminName*.</span><span class="sxs-lookup"><span data-stu-id="2c4af-172">Because the **AdminPassword** is not specified in the preceding command, you are prompted to enter the password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="2c4af-173">b.</span><span class="sxs-lookup"><span data-stu-id="2c4af-173">b.</span></span> <span data-ttu-id="2c4af-174">Het script vervolgens valideren van het configuratiebestand wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2c4af-174">The script then starts to validate the configuration file.</span></span> <span data-ttu-id="2c4af-175">Het kan enkele minuten duren, afhankelijk van de netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="2c4af-175">It can take up to several minutes depending on the network connection.</span></span>
   
    ![Validatie][validate]
   
    <span data-ttu-id="2c4af-177">c.</span><span class="sxs-lookup"><span data-stu-id="2c4af-177">c.</span></span> <span data-ttu-id="2c4af-178">Nadat de validatie slaagt, worden het script de clusterbronnen maken.</span><span class="sxs-lookup"><span data-stu-id="2c4af-178">After validations pass, the script lists the cluster resources to create.</span></span> <span data-ttu-id="2c4af-179">Voer *Y* om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="2c4af-179">Enter *Y* to continue.</span></span>
   
    ![Resources][resources]
   
    <span data-ttu-id="2c4af-181">d.</span><span class="sxs-lookup"><span data-stu-id="2c4af-181">d.</span></span> <span data-ttu-id="2c4af-182">Het script begint met de implementatie van het cluster HPC Pack en de configuratie zonder verdere handmatige stappen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="2c4af-182">The script starts to deploy the HPC Pack cluster and completes the configuration without further manual steps.</span></span> <span data-ttu-id="2c4af-183">Het script kunt uitvoeren voor enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="2c4af-183">The script can run for several minutes.</span></span>
   
    ![Implementeren][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="2c4af-185">In dit voorbeeld genereert het script een logboekbestand automatisch aangezien de **- LogFile** parameter is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2c4af-185">In this example, the script generates a log file automatically since the **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="2c4af-186">De logboeken in realtime niet worden geschreven, maar worden verzameld aan het einde van de validatie en de implementatie.</span><span class="sxs-lookup"><span data-stu-id="2c4af-186">The logs aren't written in real time, but are collected at the end of the validation and the deployment.</span></span> <span data-ttu-id="2c4af-187">Als het PowerShell-proces wordt gestopt terwijl het script wordt uitgevoerd, is enkele logboeken gaan verloren.</span><span class="sxs-lookup"><span data-stu-id="2c4af-187">If the PowerShell process is stopped while the script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-to-the-head-node"></a><span data-ttu-id="2c4af-188">Verbinding maken met het hoofdknooppunt</span><span class="sxs-lookup"><span data-stu-id="2c4af-188">Connect to the head node</span></span>
<span data-ttu-id="2c4af-189">Nadat u het HPC Pack cluster in Azure worden geïmplementeerd [verbinding maken met extern bureaublad](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) met het hoofdknooppunt VM gebruikmaken van het domein referenties u opgegeven bij de implementatie van het cluster (bijvoorbeeld *hpc\\clusteradmin*).</span><span class="sxs-lookup"><span data-stu-id="2c4af-189">After you deploy the HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to the head node VM using the domain credentials you provided when you deployed the cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="2c4af-190">U beheren het cluster vanaf het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="2c4af-190">You manage the cluster from the head node.</span></span>

<span data-ttu-id="2c4af-191">Start op het hoofdknooppunt HPC Cluster Manager om de status van het cluster HPC Pack te controleren.</span><span class="sxs-lookup"><span data-stu-id="2c4af-191">On the head node, start HPC Cluster Manager to check the status of the HPC Pack cluster.</span></span> <span data-ttu-id="2c4af-192">U kunt beheren en bewaken Linux rekenknooppunten dezelfde manier als u werkt met Windows rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="2c4af-192">You can manage and monitor Linux compute nodes the same way you work with Windows compute nodes.</span></span> <span data-ttu-id="2c4af-193">Bijvoorbeeld, ziet u de Linux-knooppunten die worden vermeld in **bronbeheer** (deze knooppunten worden geïmplementeerd met de **LinuxNode** sjabloon).</span><span class="sxs-lookup"><span data-stu-id="2c4af-193">For example, you see the Linux nodes listed in **Resource Management** (these nodes are deployed with the **LinuxNode** template).</span></span>

![Knooppunt Management][management]

<span data-ttu-id="2c4af-195">U ziet ook de Linux-knooppunten in de **Heatmap** weergeven.</span><span class="sxs-lookup"><span data-stu-id="2c4af-195">You also see the Linux nodes in the **Heat Map** view.</span></span>

![Heatmap][heatmap]

## <a name="how-to-move-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="2c4af-197">Het verplaatsen van gegevens in een cluster met Linux-knooppunten</span><span class="sxs-lookup"><span data-stu-id="2c4af-197">How to move data in a cluster with Linux nodes</span></span>
<span data-ttu-id="2c4af-198">U hebt verschillende mogelijkheden om gegevens tussen Linux-knooppunten en het Windows-hoofdknooppunt van het cluster te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="2c4af-198">You have several choices to move data among Linux nodes and the Windows head node of the cluster.</span></span> <span data-ttu-id="2c4af-199">Hier volgen drie algemene methoden uitgebreid beschreven in de volgende secties:</span><span class="sxs-lookup"><span data-stu-id="2c4af-199">Here are three common methods, described in more detail in the following sections:</span></span>

* <span data-ttu-id="2c4af-200">**Azure File** -beschrijft een beheerde SMB-bestandsshare voor het opslaan van gegevensbestanden in Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="2c4af-200">**Azure File** - Exposes a managed SMB file share to store data files in Azure storage.</span></span> <span data-ttu-id="2c4af-201">Knooppunten voor Windows en Linux-knooppunten kunnen koppelen een Azure-bestandsshare als een station of een map op hetzelfde moment, zelfs als ze zijn geïmplementeerd in verschillende virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="2c4af-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at the same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="2c4af-202">**Hoofdknooppunt SMB-share** -koppelt een standaard gedeelde Windows-map van het hoofdknooppunt op Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="2c4af-202">**Head node SMB share** - Mounts a standard Windows shared folder of the head node on Linux nodes.</span></span>
* <span data-ttu-id="2c4af-203">**HEAD knooppunt NFS-server** -biedt een oplossing voor het delen van bestanden voor een gemengde omgeving van Windows en Linux.</span><span class="sxs-lookup"><span data-stu-id="2c4af-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="2c4af-204">Azure File storage</span><span class="sxs-lookup"><span data-stu-id="2c4af-204">Azure File storage</span></span>
<span data-ttu-id="2c4af-205">De [Azure File](https://azure.microsoft.com/services/storage/files/) -service geeft bestandsshares met behulp van het standaard SMB 2.1-protocol.</span><span class="sxs-lookup"><span data-stu-id="2c4af-205">The [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using the standard SMB 2.1 protocol.</span></span> <span data-ttu-id="2c4af-206">Azure virtuele machines en cloudservices kunnen bestandsgegevens delen tussen toepassingsonderdelen via gekoppelde shares en on-premises toepassingen hebben toegang tot bestandsgegevens in een share via de File storage-API.</span><span class="sxs-lookup"><span data-stu-id="2c4af-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through the File storage API.</span></span> 

<span data-ttu-id="2c4af-207">Zie voor gedetailleerde stappen voor een Azure-bestandsshare maken en koppelen van het hoofdknooppunt van het [aan de slag met Azure File storage in Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span><span class="sxs-lookup"><span data-stu-id="2c4af-207">For detailed steps to create an Azure File share and mount it on the head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="2c4af-208">De Azure-bestandsshare koppelen op de Linux-knooppunten, Zie [Azure File storage gebruiken met Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2c4af-208">To mount the Azure File share on the Linux nodes, see [How to use Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="2c4af-209">Zie voor het persistent maken verbindingen instellen [Persisting verbindingen met Microsoft Azure-bestanden](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c4af-209">To set up persisting connections, see [Persisting connections to Microsoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="2c4af-210">In het volgende voorbeeld wordt een Azure-bestandsshare te maken van een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="2c4af-210">In the following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="2c4af-211">De share op het hoofdknooppunt koppelen, open een opdrachtprompt en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="2c4af-211">To mount the share on the head node, open a Command Prompt and enter the following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="2c4af-212">In dit voorbeeld allvhdsje is de naam van uw opslagaccount, storageaccountkey is de sleutel van uw opslagaccount en rdma is de sharenaam van de Azure-bestand.</span><span class="sxs-lookup"><span data-stu-id="2c4af-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is the Azure File share name.</span></span> <span data-ttu-id="2c4af-213">De Azure-bestandsshare is gekoppeld als Z: op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="2c4af-213">The Azure File share is mounted as Z: on the head node.</span></span>

<span data-ttu-id="2c4af-214">Koppelen van de Azure-bestandsshare op Linux-knooppunten, voer een **clusrun** opdracht op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="2c4af-214">To mount the Azure File share on Linux nodes, run a **clusrun** command on the head node.</span></span> <span data-ttu-id="2c4af-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)**  is een nuttig hulpmiddel HPC Pack bij het uitvoeren van beheertaken op meerdere knooppunten.</span><span class="sxs-lookup"><span data-stu-id="2c4af-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool to carry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="2c4af-216">(Zie ook [Clusrun voor Linux-knooppunten](#Clusrun-for-Linux-nodes) in dit artikel.)</span><span class="sxs-lookup"><span data-stu-id="2c4af-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="2c4af-217">Open een Windows PowerShell-venster en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="2c4af-217">Open a Windows PowerShell window and enter the following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="2c4af-218">De eerste opdracht maakt een map met de naam /rdma op alle knooppunten in de groep LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="2c4af-218">The first command creates a folder named /rdma on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="2c4af-219">De tweede opdracht koppelt de allvhdsjw.file.core.windows.net/rdma Azure File share naar de map /rdma met dir en de bestandsmodus ingesteld op 777.</span><span class="sxs-lookup"><span data-stu-id="2c4af-219">The second command mounts the Azure File share allvhdsjw.file.core.windows.net/rdma onto the /rdma folder with dir and file mode bits set to 777.</span></span> <span data-ttu-id="2c4af-220">In de tweede opdracht allvhdsje is de naam van uw opslagaccount en storageaccountkey is de sleutel van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="2c4af-220">In the second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="2c4af-221">De '\\`' symbool in de tweede opdracht is een escapeteken voor PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2c4af-221">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="2c4af-222">"\\`, ' betekent dat de","(kommateken) een onderdeel van de opdracht is.</span><span class="sxs-lookup"><span data-stu-id="2c4af-222">“\\`,” means that the “,” (comma character) is a part of the command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="2c4af-223">Hoofdknooppunt share</span><span class="sxs-lookup"><span data-stu-id="2c4af-223">Head node share</span></span>
<span data-ttu-id="2c4af-224">U kunt ook een gedeelde map van het hoofdknooppunt op Linux-knooppunten koppelen.</span><span class="sxs-lookup"><span data-stu-id="2c4af-224">Alternatively, mount a shared folder of the head node on Linux nodes.</span></span> <span data-ttu-id="2c4af-225">Een share biedt de eenvoudigste manier om bestanden te delen, maar het hoofdknooppunt en alle Linux-knooppunten in hetzelfde virtuele netwerk moeten worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="2c4af-225">A share provides the simplest way to share files, but the head node and all Linux nodes must be deployed in the same virtual network.</span></span> <span data-ttu-id="2c4af-226">Hier volgen de stappen.</span><span class="sxs-lookup"><span data-stu-id="2c4af-226">Here are the steps.</span></span>

1. <span data-ttu-id="2c4af-227">Maak een map op het hoofdknooppunt en delen voor iedereen met machtigingen voor lezen/schrijven.</span><span class="sxs-lookup"><span data-stu-id="2c4af-227">Create a folder on the head node and share it to Everyone with Read/Write permissions.</span></span> <span data-ttu-id="2c4af-228">Bijvoorbeeld D:\OpenFOAM delen op het hoofdknooppunt als \\CentOS7RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="2c4af-228">For example, share D:\OpenFOAM on the head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="2c4af-229">Hier volgt CentOS7RDMA HN de hostnaam van het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="2c4af-229">Here CentOS7RDMA-HN is the hostname of the head node.</span></span>
   
    ![Machtigingen voor de bestandsshare][fileshareperms]
   
    ![Delen van bestanden][filesharing]
2. <span data-ttu-id="2c4af-232">Open een Windows PowerShell-venster en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="2c4af-232">Open a Windows PowerShell window and run the following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="2c4af-233">De eerste opdracht maakt een map met de naam /openfoam op alle knooppunten in de groep LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="2c4af-233">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="2c4af-234">De tweede opdracht koppelt de gedeelde map //CentOS7RDMA-HN/OpenFOAM naar de map met dir en de bestandsmodus ingesteld op 777.</span><span class="sxs-lookup"><span data-stu-id="2c4af-234">The second command mounts the shared folder //CentOS7RDMA-HN/OpenFOAM onto the folder with dir and file mode bits set to 777.</span></span> <span data-ttu-id="2c4af-235">De gebruikersnaam en wachtwoord in de opdracht moet de gebruikersnaam en het wachtwoord van een gebruiker van het cluster op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="2c4af-235">The username and password in the command should be the username and password of a cluster user on the head node.</span></span> <span data-ttu-id="2c4af-236">(Zie [toevoegen of verwijderen cluster gebruikers](https://technet.microsoft.com/library/ff919330.aspx).)</span><span class="sxs-lookup"><span data-stu-id="2c4af-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="2c4af-237">De '\\`' symbool in de tweede opdracht is een escapeteken voor PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2c4af-237">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="2c4af-238">"\\`, ' betekent dat de","(kommateken) een onderdeel van de opdracht is.</span><span class="sxs-lookup"><span data-stu-id="2c4af-238">“\\`,” means that the “,” (comma character) is a part of the command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="2c4af-239">NFS-server</span><span class="sxs-lookup"><span data-stu-id="2c4af-239">NFS server</span></span>
<span data-ttu-id="2c4af-240">De NFS-service kunt u delen en migreren van bestanden tussen de computers waarop het besturingssysteem van Windows Server 2012 met behulp van het SMB-protocol en Linux-computers met de NFS-protocol.</span><span class="sxs-lookup"><span data-stu-id="2c4af-240">The NFS service enables you to share and migrate files between computers running the Windows Server 2012 operating system using the SMB protocol and Linux-based computers using the NFS protocol.</span></span> <span data-ttu-id="2c4af-241">De NFS-server en alle andere knooppunten moeten worden geïmplementeerd in hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="2c4af-241">The NFS server and all other nodes have to be deployed in the same virtual network.</span></span> <span data-ttu-id="2c4af-242">Dit biedt betere compatibiliteit met Linux-knooppunten vergeleken met een SMB-share.</span><span class="sxs-lookup"><span data-stu-id="2c4af-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="2c4af-243">Bijvoorbeeld: het bestandskoppelingen ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="2c4af-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="2c4af-244">Volg de stappen in wilt installeren en instellen van een NFS-server, [Server voor Network File System-eerste Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c4af-244">To install and set up an NFS server, follow the steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="2c4af-245">Maak bijvoorbeeld een NFS-share met de naam nfs met de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="2c4af-245">For example, create an NFS share named nfs with the following properties:</span></span>
   
    ![NFS-autorisatie][nfsauth]
   
    ![NFS-sharemachtigingen][nfsshare]
   
    ![NFS-NTFS-machtigingen][nfsperm]
   
    ![Eigenschappen van de NFS-beheer][nfsmanage]
2. <span data-ttu-id="2c4af-250">Open een Windows PowerShell-venster en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="2c4af-250">Open a Windows PowerShell window and run the following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="2c4af-251">De eerste opdracht maakt een map met de naam /nfsshared op alle knooppunten in de groep LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="2c4af-251">The first command creates a folder named /nfsshared on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="2c4af-252">De tweede opdracht koppelt de NFS-share CentOS7RDMA HN: / nfs naar de map.</span><span class="sxs-lookup"><span data-stu-id="2c4af-252">The second command mounts the NFS share CentOS7RDMA-HN:/nfs onto the folder.</span></span> <span data-ttu-id="2c4af-253">Hier CentOS7RDMA HN:-nfs is de externe pad van de NFS-share.</span><span class="sxs-lookup"><span data-stu-id="2c4af-253">Here CentOS7RDMA-HN:/nfs is the remote path of your NFS share.</span></span>

## <a name="how-to-submit-jobs"></a><span data-ttu-id="2c4af-254">Het verzenden van taken</span><span class="sxs-lookup"><span data-stu-id="2c4af-254">How to submit jobs</span></span>
<span data-ttu-id="2c4af-255">Er zijn verschillende manieren om taken voor het cluster HPC Pack te verzenden:</span><span class="sxs-lookup"><span data-stu-id="2c4af-255">There are several ways to submit jobs to the HPC Pack cluster:</span></span>

* <span data-ttu-id="2c4af-256">HPC Cluster Manager of HPC Job Manager GUI</span><span class="sxs-lookup"><span data-stu-id="2c4af-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="2c4af-257">HPC-webportal</span><span class="sxs-lookup"><span data-stu-id="2c4af-257">HPC web portal</span></span>
* <span data-ttu-id="2c4af-258">REST API</span><span class="sxs-lookup"><span data-stu-id="2c4af-258">REST API</span></span>

<span data-ttu-id="2c4af-259">Verzenden van de taak aan het cluster in Azure via HPC Pack GUI-hulpprogramma's en de HPC-webportal zijn hetzelfde als voor Windows rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="2c4af-259">Job submission to the cluster in Azure via HPC Pack GUI tools and the HPC web portal are the same as for Windows compute nodes.</span></span> <span data-ttu-id="2c4af-260">Zie [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) en [het verzenden van taken van een on-premises clientcomputer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c4af-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How to submit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="2c4af-261">Raadpleeg voor het verzenden van taken via de REST-API [maken en verzenden van taken met behulp van de REST-API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c4af-261">To submit jobs via the REST API, refer to [Creating and Submitting Jobs by Using the REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="2c4af-262">Voor het verzenden van taken van een Linux-client ook verwijzen naar het Python-voorbeeld in de [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span><span class="sxs-lookup"><span data-stu-id="2c4af-262">To submit jobs from a Linux client, also refer to the Python sample in the [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="2c4af-263">Clusrun voor Linux-knooppunten</span><span class="sxs-lookup"><span data-stu-id="2c4af-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="2c4af-264">De HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) hulpprogramma kan worden gebruikt voor het uitvoeren van opdrachten op Linux-knooppunten via een opdrachtprompt of HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="2c4af-264">The HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used to execute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="2c4af-265">Hier volgen enkele eenvoudige voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="2c4af-265">Following are some basic examples.</span></span>

* <span data-ttu-id="2c4af-266">Huidige gebruikersnamen weergeven op alle knooppunten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="2c4af-266">Show current user names on all nodes in the cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="2c4af-267">Installeer de **gdb** foutopsporingsprogramma met **yum** op alle knooppunten in de linuxnodes groep en de knooppunten na 10 minuten opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="2c4af-267">Install the **gdb** debugger tool with **yum** on all nodes in the linuxnodes group and then restart the nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="2c4af-268">Maken van een shell-script weergeven van elk getal van 1 tot en met 10 voor één seconde op elke Linux-knooppunt in het cluster, uitvoeren en uitvoer van de knooppunten onmiddellijk weergeven.</span><span class="sxs-lookup"><span data-stu-id="2c4af-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in the cluster, run it, and show output from the nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="2c4af-269">Mogelijk moet u bepaalde escapetekens in gebruiken **clusrun** opdrachten.</span><span class="sxs-lookup"><span data-stu-id="2c4af-269">You might need to use certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="2c4af-270">Zoals u in dit voorbeeld, gebruik ^ in een opdrachtprompt als escape voor de ' > ' symbool.</span><span class="sxs-lookup"><span data-stu-id="2c4af-270">As shown in this example, use ^ in a Command Prompt to escape the ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2c4af-271">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2c4af-271">Next steps</span></span>
* <span data-ttu-id="2c4af-272">Probeer schalen van het cluster naar een groter aantal knooppunten, of een werkbelasting Linux wordt uitgevoerd op het cluster.</span><span class="sxs-lookup"><span data-stu-id="2c4af-272">Try scaling up the cluster to a larger number of nodes, or try running a Linux workload on the cluster.</span></span> <span data-ttu-id="2c4af-273">Zie voor een voorbeeld [NAMD uitvoeren met Microsoft HPC Pack op Linux-rekenknooppunten in Azure](hpcpack-cluster-namd.md).</span><span class="sxs-lookup"><span data-stu-id="2c4af-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="2c4af-274">Probeer een cluster met [RDMA-functionaliteit, rekenintensieve VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) MPI-workloads uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2c4af-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to run MPI workloads.</span></span> <span data-ttu-id="2c4af-275">Zie voor een voorbeeld [OpenFOAM uitvoeren met Microsoft HPC Pack op een Linux RDMA-cluster in Azure](hpcpack-cluster-openfoam.md).</span><span class="sxs-lookup"><span data-stu-id="2c4af-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="2c4af-276">Als u geïnteresseerd bent in het werken met Linux-knooppunten in een on-premises HPC Pack-cluster, raadpleegt u de [TechNet richtlijnen](https://technet.microsoft.com/library/mt595803.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c4af-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see the [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

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

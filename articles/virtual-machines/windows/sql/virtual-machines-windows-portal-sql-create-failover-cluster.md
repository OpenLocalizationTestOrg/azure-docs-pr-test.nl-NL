---
title: aaaSQL Server FCI - Azure Virtual Machines | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe toocreate Failover-Cluster van SQL Server-instantie op Azure Virtual Machines.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="85096-103">Exemplaar van SQL Server-failovercluster configureren op virtuele Machines in Azure</span><span class="sxs-lookup"><span data-stu-id="85096-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="85096-104">Dit artikel wordt uitgelegd hoe toocreate een SQL Serverfailover Cluster Instance (FCI) op Azure virtuele machines in de Resource Manager-model.</span><span class="sxs-lookup"><span data-stu-id="85096-104">This article explains how toocreate a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="85096-105">Deze oplossing gebruikt [Windows Server 2016 Datacenter edition opslagruimten Direct \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) als een op software gebaseerde virtueel SAN waarmee Hallo opslag (gegevensschijven) gesynchroniseerd tussen Hallo knooppunten (virtuele Azure-machines) in een Windows-Cluster.</span><span class="sxs-lookup"><span data-stu-id="85096-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes hello storage (data disks) between hello nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="85096-106">S2D is nieuw in Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="85096-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="85096-107">Hallo volgende diagram ziet u de volledige oplossing Hallo op Azure virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="85096-107">hello following diagram shows hello complete solution on Azure virtual machines:</span></span>

![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="85096-109">Hallo voorgaande diagram laat zien welke:</span><span class="sxs-lookup"><span data-stu-id="85096-109">hello preceding diagram shows:</span></span>

- <span data-ttu-id="85096-110">Twee virtuele Azure-machines in een Windows-failovercluster.</span><span class="sxs-lookup"><span data-stu-id="85096-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="85096-111">Wanneer een virtuele machine in een failovercluster wordt ook wel een *clusterknooppunt*, of *knooppunten*.</span><span class="sxs-lookup"><span data-stu-id="85096-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="85096-112">Elke virtuele machine heeft twee of meer gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="85096-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="85096-113">S2D hello gegevens op Hallo gegevensschijf gesynchroniseerd en geeft de opslag Hallo gesynchroniseerd als een opslaggroep.</span><span class="sxs-lookup"><span data-stu-id="85096-113">S2D synchronizes hello data on hello data disk and presents hello synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="85096-114">Hallo opslaggroep geeft een cluster shared volume (CSV) toohello failover-cluster.</span><span class="sxs-lookup"><span data-stu-id="85096-114">hello storage pool presents a cluster shared volume (CSV) toohello failover cluster.</span></span>
- <span data-ttu-id="85096-115">functie Hallo FCI van SQL Server-cluster maakt gebruik van Hallo CSV voor Hallo gegevensstations.</span><span class="sxs-lookup"><span data-stu-id="85096-115">hello SQL Server FCI cluster role uses hello CSV for hello data drives.</span></span>
- <span data-ttu-id="85096-116">Een Azure-load balancer toohold Hallo IP-adres voor Hallo FCI van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="85096-116">An Azure load balancer toohold hello IP address for hello SQL Server FCI.</span></span>
- <span data-ttu-id="85096-117">Een Azure beschikbaarheidsset bevat alle Hallo-resources.</span><span class="sxs-lookup"><span data-stu-id="85096-117">An Azure availability set holds all hello resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="85096-118">Alle Azure-resources zijn in Hallo diagram zijn in Hallo dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="85096-118">All Azure resources are in hello diagram are in hello same resource group.</span></span>

<span data-ttu-id="85096-119">Zie voor meer informatie over S2D [Windows Server 2016 Datacenter edition opslagruimten Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span><span class="sxs-lookup"><span data-stu-id="85096-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="85096-120">S2D ondersteunt twee soorten architecturen - geconvergeerde en hyper-geconvergeerde.</span><span class="sxs-lookup"><span data-stu-id="85096-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="85096-121">Hallo-architectuur in dit document is hyper-geconvergeerde.</span><span class="sxs-lookup"><span data-stu-id="85096-121">hello architecture in this document is hyper-converged.</span></span> <span data-ttu-id="85096-122">Een hyper-geconvergeerde infrastructuur plaatsen Hallo opslag op Hallo van dezelfde servers die host Hallo geclusterde toepassing.</span><span class="sxs-lookup"><span data-stu-id="85096-122">A hyper-converged infrastructure places hello storage on hello same servers that host hello clustered application.</span></span> <span data-ttu-id="85096-123">In deze architectuur is Hallo opslag op elk knooppunt FCI van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="85096-123">In this architecture, hello storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="85096-124">Voorbeeld van de Azure-sjabloon</span><span class="sxs-lookup"><span data-stu-id="85096-124">Example Azure template</span></span>

<span data-ttu-id="85096-125">U kunt Hallo hele oplossing in Azure maken van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="85096-125">You can create hello entire solution in Azure from a template.</span></span> <span data-ttu-id="85096-126">Een voorbeeld van een sjabloon is beschikbaar in GitHub hello [Azure-Snelstartsjablonen](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span><span class="sxs-lookup"><span data-stu-id="85096-126">An example of a template is available in hello GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="85096-127">In dit voorbeeld is niet ontworpen of getest voor een specifieke werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="85096-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="85096-128">U kunt op een SQL Server-FCI Hallo sjabloon toocreate uitvoeren met S2D opslag verbonden tooyour domein.</span><span class="sxs-lookup"><span data-stu-id="85096-128">You can run hello template toocreate a SQL Server FCI with S2D storage connected tooyour domain.</span></span> <span data-ttu-id="85096-129">U kunt evalueren Hallo sjabloon en aanpassen voor uw doeleinden.</span><span class="sxs-lookup"><span data-stu-id="85096-129">You can evaluate hello template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="85096-130">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="85096-130">Before you begin</span></span>

<span data-ttu-id="85096-131">Er zijn enkele dingen die u moet tooknow en een aantal dingen die u nodig hebt voldaan voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="85096-131">There are a few things you need tooknow and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-tooknow"></a><span data-ttu-id="85096-132">Welke tooknow</span><span class="sxs-lookup"><span data-stu-id="85096-132">What tooknow</span></span>
<span data-ttu-id="85096-133">U hebt een operationeel inzicht in Hallo technologieën te volgen:</span><span class="sxs-lookup"><span data-stu-id="85096-133">You should have an operational understanding of hello following technologies:</span></span>

- [<span data-ttu-id="85096-134">Windows cluster-technologieën</span><span class="sxs-lookup"><span data-stu-id="85096-134">Windows cluster technologies</span></span>](http://technet.microsoft.com/library/hh831579.aspx)
-  <span data-ttu-id="85096-135">[Exemplaren van SQL Server-failovercluster](http://msdn.microsoft.com/library/ms189134.aspx).</span><span class="sxs-lookup"><span data-stu-id="85096-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="85096-136">Bovendien hebt u een algemeen begrip van Hallo technologieën te volgen:</span><span class="sxs-lookup"><span data-stu-id="85096-136">Also, you should have a general understanding of hello following technologies:</span></span>

- [<span data-ttu-id="85096-137">Hyper-geconvergeerde oplossing met behulp van opslagruimten Direct in Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="85096-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [<span data-ttu-id="85096-138">Azure-resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="85096-138">Azure resource groups</span></span>](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a><span data-ttu-id="85096-139">Welke toohave</span><span class="sxs-lookup"><span data-stu-id="85096-139">What toohave</span></span>

<span data-ttu-id="85096-140">Voordat u Hallo-instructies in dit artikel, hebt u al:</span><span class="sxs-lookup"><span data-stu-id="85096-140">Before following hello instructions in this article, you should already have:</span></span>

- <span data-ttu-id="85096-141">Een Microsoft Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="85096-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="85096-142">Een Windows-domein op virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="85096-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="85096-143">Een account met machtigingen toocreate objecten in hello Azure virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="85096-143">An account with permission toocreate objects in hello Azure virtual machine.</span></span>
- <span data-ttu-id="85096-144">Een virtuele Azure-netwerk en subnet met voldoende IP-adresruimte voor Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="85096-144">An Azure virtual network and subnet with sufficient IP address space for hello following components:</span></span>
   - <span data-ttu-id="85096-145">Beide virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="85096-145">Both virtual machines.</span></span>
   - <span data-ttu-id="85096-146">IP-adres voor Hallo failover-cluster.</span><span class="sxs-lookup"><span data-stu-id="85096-146">hello failover cluster IP address.</span></span>
   - <span data-ttu-id="85096-147">Een IP-adres voor elke FCI.</span><span class="sxs-lookup"><span data-stu-id="85096-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="85096-148">DNS wordt geconfigureerd op Hallo Azure-netwerk, wijzen toohello-domeincontrollers.</span><span class="sxs-lookup"><span data-stu-id="85096-148">DNS configured on hello Azure Network, pointing toohello domain controllers.</span></span>

<span data-ttu-id="85096-149">Met deze vereisten is voldaan, kunt u doorgaan met het bouwen van uw failover-cluster.</span><span class="sxs-lookup"><span data-stu-id="85096-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="85096-150">de eerste stap Hallo is toocreate Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="85096-150">hello first step is toocreate hello virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="85096-151">Stap 1: Virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="85096-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="85096-152">Meld u bij toohello [Azure-portal](http://portal.azure.com) met uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="85096-152">Log in toohello [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="85096-153">[Maken van een Azure beschikbaarheidsset](../tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="85096-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="85096-154">Hallo beschikbaarheid instellen groepen virtuele machines tussen domeinen met fouten en domeinen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="85096-154">hello availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="85096-155">Hallo beschikbaarheidsset zorgt ervoor dat uw toepassing is niet van invloed op een individuele foutpunten, zoals het Hallo-netwerkswitch of Hallo power-eenheid van een rek met servers.</span><span class="sxs-lookup"><span data-stu-id="85096-155">hello availability set makes sure that your application is not affected by single points of failure, like hello network switch or hello power unit of a rack of servers.</span></span>

   <span data-ttu-id="85096-156">Als u geen Hallo resourcegroep hebt gemaakt voor uw virtuele machines, moet u het doen wanneer u een Azure beschikbaarheidsset maakt.</span><span class="sxs-lookup"><span data-stu-id="85096-156">If you have not created hello resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="85096-157">Als u hello Azure portal toocreate hello beschikbaarheidsset, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="85096-157">If you're using hello Azure portal toocreate hello availability set, do hello following steps:</span></span>

   - <span data-ttu-id="85096-158">Klik in hello Azure-portal, op  **+**  tooopen hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="85096-158">In hello Azure portal, click **+** tooopen hello Azure Marketplace.</span></span> <span data-ttu-id="85096-159">Zoeken naar **beschikbaarheidsset**.</span><span class="sxs-lookup"><span data-stu-id="85096-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="85096-160">Klik op **beschikbaarheidsset**.</span><span class="sxs-lookup"><span data-stu-id="85096-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="85096-161">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="85096-161">Click **Create**.</span></span>
   - <span data-ttu-id="85096-162">Op Hallo **beschikbaarheidsset maken** blade set Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="85096-162">On hello **Create availability set** blade, set hello following values:</span></span>
      - <span data-ttu-id="85096-163">**Naam**: een naam voor de beschikbaarheidsset Hallo.</span><span class="sxs-lookup"><span data-stu-id="85096-163">**Name**: A name for hello availability set.</span></span>
      - <span data-ttu-id="85096-164">**Abonnement**: uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="85096-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="85096-165">**Resourcegroep**: als u wilt dat toouse een bestaande groep, klikt u op **gebruik bestaande** en selecteer Hallo groep uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="85096-165">**Resource group**: If you want toouse an existing group, click **Use existing** and select hello group from hello drop-down list.</span></span> <span data-ttu-id="85096-166">Kies anders **nieuw** en typ een naam voor de groep Hallo.</span><span class="sxs-lookup"><span data-stu-id="85096-166">Otherwise choose **Create New** and type a name for hello group.</span></span>
      - <span data-ttu-id="85096-167">**Locatie**: Stel Hallo locatie waar u van plan toocreate bent in uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="85096-167">**Location**: Set hello location where you plan toocreate your virtual machines.</span></span>
      - <span data-ttu-id="85096-168">**Fault-domeinen**: Hallo-standaard (3).</span><span class="sxs-lookup"><span data-stu-id="85096-168">**Fault domains**: Use hello default (3).</span></span>
      - <span data-ttu-id="85096-169">**Bijwerken van domeinen**: Hallo-standaard (5).</span><span class="sxs-lookup"><span data-stu-id="85096-169">**Update domains**: Use hello default (5).</span></span>
   - <span data-ttu-id="85096-170">Klik op **maken** toocreate hello beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="85096-170">Click **Create** toocreate hello availability set.</span></span>

1. <span data-ttu-id="85096-171">Hallo virtuele machines maken in beschikbaarheidsset Hallo.</span><span class="sxs-lookup"><span data-stu-id="85096-171">Create hello virtual machines in hello availability set.</span></span>

   <span data-ttu-id="85096-172">Twee SQL Server virtuele machines inrichten in hello Azure beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="85096-172">Provision two SQL Server virtual machines in hello Azure availability set.</span></span> <span data-ttu-id="85096-173">Zie voor instructies [een SQL Server-machine inrichten in hello Azure-portal](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="85096-173">For instructions, see [Provision a SQL Server virtual machine in hello Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="85096-174">Plaats beide virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="85096-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="85096-175">In Hallo is dezelfde Azure-resourcegroep die uw beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="85096-175">In hello same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="85096-176">Op Hallo netwerk als uw domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="85096-176">On hello same network as your domain controller.</span></span>
   - <span data-ttu-id="85096-177">In een subnet met voldoende IP-adresruimte voor virtuele machines en alle Failoverclusterinstanties die u uiteindelijk op dit cluster kan gebruiken.</span><span class="sxs-lookup"><span data-stu-id="85096-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="85096-178">In hello Azure beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="85096-178">In hello Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="85096-179">U niet instellen of wijzigen van de beschikbaarheidsset nadat een virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="85096-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="85096-180">Een afbeelding kiezen uit hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="85096-180">Choose an image from hello Azure Marketplace.</span></span> <span data-ttu-id="85096-181">U kunt een Marketplace installatiekopie met die Windows Server en SQL Server of alleen Hallo Windows Server bevat.</span><span class="sxs-lookup"><span data-stu-id="85096-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just hello Windows Server.</span></span> <span data-ttu-id="85096-182">Zie voor meer informatie [overzicht van SQL Server op Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span><span class="sxs-lookup"><span data-stu-id="85096-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="85096-183">Hallo officiële SQL Server-installatiekopieën in hello Azure-galerie omvatten een geïnstalleerde SQL Server-exemplaar plus Hallo SQL Server-installatie van software en Hallo sleutel.</span><span class="sxs-lookup"><span data-stu-id="85096-183">hello official SQL Server images in hello Azure Gallery include an installed SQL Server instance, plus hello SQL Server installation software, and hello required key.</span></span>

   <span data-ttu-id="85096-184">Hallo juiste installatiekopie volgens toohow gewenste toopay voor SQL Server-licentie Hallo kiezen:</span><span class="sxs-lookup"><span data-stu-id="85096-184">Choose hello right image according toohow you want toopay for hello SQL Server license:</span></span>

   - <span data-ttu-id="85096-185">**Betalen per gebruik licentieverlening**: Hallo per minuut kosten van deze installatiekopieën omvat Hallo SQL Server-licentieverlening:</span><span class="sxs-lookup"><span data-stu-id="85096-185">**Pay per usage licensing**: hello per-minute cost of these images includes hello SQL Server licensing:</span></span>
      - <span data-ttu-id="85096-186">**SQL Server 2016 Enterprise op Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="85096-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="85096-187">**SQL Server 2016 Standard op Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="85096-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="85096-188">**SQL Server 2016 Developer op Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="85096-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="85096-189">**Bring-your-eigenaar-license (BYOL)**</span><span class="sxs-lookup"><span data-stu-id="85096-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="85096-190">**{BYOL} SQL Server 2016 Enterprise op Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="85096-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="85096-191">**{BYOL} SQL Server 2016 Standard op Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="85096-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="85096-192">Nadat u Hallo virtuele machine hebt gemaakt, verwijdert u Hallo vooraf geïnstalleerde zelfstandige SQL Server-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="85096-192">After you create hello virtual machine, remove hello pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="85096-193">U gebruikt Hallo vooraf geïnstalleerde SQL Server media toocreate Hallo FCI van SQL Server nadat u Hallo failover-cluster en S2D configureren.</span><span class="sxs-lookup"><span data-stu-id="85096-193">You will use hello pre-installed SQL Server media toocreate hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span>

   <span data-ttu-id="85096-194">U kunt ook Azure Marketplace-installatiekopieën gebruiken met NET Hallo-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="85096-194">Alternatively, you can use Azure Marketplace images with just hello operating system.</span></span> <span data-ttu-id="85096-195">Kies een **Windows Server 2016 Datacenter** installatiekopie en Hallo FCI van SQL Server te installeren nadat u het failovercluster Hallo en S2D configureren.</span><span class="sxs-lookup"><span data-stu-id="85096-195">Choose a **Windows Server 2016 Datacenter** image and install hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span> <span data-ttu-id="85096-196">Deze installatiekopie bevat geen SQL Server-installatiemedia.</span><span class="sxs-lookup"><span data-stu-id="85096-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="85096-197">Hallo-installatiemedia plaatsen op een locatie waar u Hallo SQL Server-installatie voor elke server kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="85096-197">Place hello installation media in a location where you can run hello SQL Server installation for each server.</span></span>

1. <span data-ttu-id="85096-198">Nadat uw virtuele machines is gemaakt in Azure, moet u tooeach virtuele machine verbinden met RDP.</span><span class="sxs-lookup"><span data-stu-id="85096-198">After Azure creates your virtual machines, connect tooeach virtual machine with RDP.</span></span>

   <span data-ttu-id="85096-199">Als u tooa virtuele machine voor het eerst verbinding met RDP, desgewenst Hallo computer tooallow deze PC toobe op Hallo netwerk kunnen worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="85096-199">When you first connect tooa virtual machine with RDP, hello computer asks if you want tooallow this PC toobe discoverable on hello network.</span></span> <span data-ttu-id="85096-200">Klik op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="85096-200">Click **Yes**.</span></span>

1. <span data-ttu-id="85096-201">Als u van een virtuele machine op basis van SQL Server-installatiekopieën hello gebruikmaakt, verwijdert u Hallo SQL Server-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="85096-201">If you are using one of hello SQL Server-based virtual machine images, remove hello SQL Server instance.</span></span>

   - <span data-ttu-id="85096-202">In **programma's en onderdelen**, met de rechtermuisknop op **Microsoft SQL Server 2016 (64-bits)** en klik op **verwijderen/wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="85096-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="85096-203">Klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="85096-203">Click **Remove**.</span></span>
   - <span data-ttu-id="85096-204">Selecteer het standaardexemplaar Hallo.</span><span class="sxs-lookup"><span data-stu-id="85096-204">Select hello default instance.</span></span>
   - <span data-ttu-id="85096-205">Verwijder alle onderdelen onder **Database Engine-Services**.</span><span class="sxs-lookup"><span data-stu-id="85096-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="85096-206">Verwijder niet **gedeelde onderdelen**.</span><span class="sxs-lookup"><span data-stu-id="85096-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="85096-207">Zie de volgende afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="85096-207">See hello following picture:</span></span>

      ![Onderdelen verwijderen](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="85096-209">Klik op **volgende**, en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="85096-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="85096-210"><a name="ports"></a>Open Hallo firewall-poorten.</span><span class="sxs-lookup"><span data-stu-id="85096-210"><a name="ports"></a>Open hello firewall ports.</span></span>

   <span data-ttu-id="85096-211">Open op elke virtuele machine, Hallo poorten op Hallo Windows Firewall te volgen.</span><span class="sxs-lookup"><span data-stu-id="85096-211">On each virtual machine, open hello following ports on hello Windows Firewall.</span></span>

   | <span data-ttu-id="85096-212">Doel</span><span class="sxs-lookup"><span data-stu-id="85096-212">Purpose</span></span> | <span data-ttu-id="85096-213">TCP-poort</span><span class="sxs-lookup"><span data-stu-id="85096-213">TCP Port</span></span> | <span data-ttu-id="85096-214">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="85096-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="85096-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="85096-215">SQL Server</span></span> | <span data-ttu-id="85096-216">1433</span><span class="sxs-lookup"><span data-stu-id="85096-216">1433</span></span> | <span data-ttu-id="85096-217">Normale poort voor standaardexemplaren van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="85096-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="85096-218">Als u een installatiekopie van het uit de galerie Hallo gebruikt, worden deze poort wordt automatisch geopend.</span><span class="sxs-lookup"><span data-stu-id="85096-218">If you used an image from hello gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="85096-219">De statuscontrole</span><span class="sxs-lookup"><span data-stu-id="85096-219">Health probe</span></span> | <span data-ttu-id="85096-220">59999</span><span class="sxs-lookup"><span data-stu-id="85096-220">59999</span></span> | <span data-ttu-id="85096-221">Een open TCP-poort.</span><span class="sxs-lookup"><span data-stu-id="85096-221">Any open TCP port.</span></span> <span data-ttu-id="85096-222">In een later stadium Hallo load balancer configureren [health test](#probe) en Hallo cluster toouse deze poort.</span><span class="sxs-lookup"><span data-stu-id="85096-222">In a later step, configure hello load balancer [health probe](#probe) and hello cluster toouse this port.</span></span>  

1. <span data-ttu-id="85096-223">Opslag toohello virtuele machine toevoegen.</span><span class="sxs-lookup"><span data-stu-id="85096-223">Add storage toohello virtual machine.</span></span> <span data-ttu-id="85096-224">Zie voor gedetailleerde informatie [opslag toevoegen](../../../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="85096-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="85096-225">Beide virtuele machines nodig ten minste twee schijven.</span><span class="sxs-lookup"><span data-stu-id="85096-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="85096-226">Koppel onbewerkte schijven - geen NTFS-geformatteerde schijven.</span><span class="sxs-lookup"><span data-stu-id="85096-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="85096-227">Als u NTFS-geformatteerde schijven koppelt, kunt u alleen S2D inschakelen met geen controle van de schijf in aanmerking komt.</span><span class="sxs-lookup"><span data-stu-id="85096-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="85096-228">Koppel een minimum van twee Premium-opslag (SSD-schijven) tooeach VM.</span><span class="sxs-lookup"><span data-stu-id="85096-228">Attach a minimum of two Premium Storage (SSD disks) tooeach VM.</span></span> <span data-ttu-id="85096-229">Het is raadzaam ten minste P30 schijven (1 TB).</span><span class="sxs-lookup"><span data-stu-id="85096-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="85096-230">Set-hostcaching te**alleen-lezen**.</span><span class="sxs-lookup"><span data-stu-id="85096-230">Set host caching too**Read-only**.</span></span>

   <span data-ttu-id="85096-231">Hallo opslagcapaciteit die u gebruik in productieomgevingen, is afhankelijk van uw workload.</span><span class="sxs-lookup"><span data-stu-id="85096-231">hello storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="85096-232">Hallo-waarden die worden beschreven in dit artikel zijn voor de demonstratie en testen.</span><span class="sxs-lookup"><span data-stu-id="85096-232">hello values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="85096-233">[Hallo virtuele machines tooyour vooraf bestaande domein toevoegen](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="85096-233">[Add hello virtual machines tooyour pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="85096-234">Nadat het Hallo virtuele machines worden gemaakt en geconfigureerd, kunt u Hallo failover-cluster configureren.</span><span class="sxs-lookup"><span data-stu-id="85096-234">After hello virtual machines are created and configured, you can configure hello failover cluster.</span></span>

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a><span data-ttu-id="85096-235">Stap 2: Hallo Windows Failover Cluster met S2D configureren</span><span class="sxs-lookup"><span data-stu-id="85096-235">Step 2: Configure hello Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="85096-236">de volgende stap Hallo is tooconfigure Hallo-failovercluster met S2D.</span><span class="sxs-lookup"><span data-stu-id="85096-236">hello next step is tooconfigure hello failover cluster with S2D.</span></span> <span data-ttu-id="85096-237">In deze stap doet u Hallo volgende substappen:</span><span class="sxs-lookup"><span data-stu-id="85096-237">In this step, you will do hello following substeps:</span></span>

1. <span data-ttu-id="85096-238">Windows Failover Clustering-functie toevoegen</span><span class="sxs-lookup"><span data-stu-id="85096-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="85096-239">Hallo cluster valideren</span><span class="sxs-lookup"><span data-stu-id="85096-239">Validate hello cluster</span></span>
1. <span data-ttu-id="85096-240">Hallo failover-cluster maken</span><span class="sxs-lookup"><span data-stu-id="85096-240">Create hello failover cluster</span></span>
1. <span data-ttu-id="85096-241">Hallo cloud witness maken</span><span class="sxs-lookup"><span data-stu-id="85096-241">Create hello cloud witness</span></span>
1. <span data-ttu-id="85096-242">Opslag toevoegen</span><span class="sxs-lookup"><span data-stu-id="85096-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="85096-243">Windows Failover Clustering-functie toevoegen</span><span class="sxs-lookup"><span data-stu-id="85096-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="85096-244">toobegin, toohello eerste virtuele machine verbinden met RDP met een domeinaccount dat lid is van de lokale groep administrators en machtigingen toocreate objecten heeft in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="85096-244">toobegin, connect toohello first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions toocreate objects in Active Directory.</span></span> <span data-ttu-id="85096-245">Dit account wordt gebruikt voor de rest Hallo van Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="85096-245">Use this account for hello rest of hello configuration.</span></span>

1. <span data-ttu-id="85096-246">[Failover Clustering functie tooeach virtuele machine toevoegen](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="85096-246">[Add Failover Clustering feature tooeach virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="85096-247">tooinstall functie Failover Clustering van Hallo-gebruikersinterface Hallo volgende stappen uit op beide virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="85096-247">tooinstall Failover Clustering feature from hello UI, do hello following steps on both virtual machines.</span></span>
   - <span data-ttu-id="85096-248">In **Serverbeheer**, klikt u op **beheren**, en klik vervolgens op **functies en onderdelen toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="85096-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="85096-249">In **Wizard Functies toevoegen en onderdelen**, klikt u op **volgende** totdat u te**onderdelen selecteren**.</span><span class="sxs-lookup"><span data-stu-id="85096-249">In **Add Roles and Features Wizard**, click **Next** until you get too**Select Features**.</span></span>
   - <span data-ttu-id="85096-250">In **onderdelen selecteren**, klikt u op **Failoverclustering**.</span><span class="sxs-lookup"><span data-stu-id="85096-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="85096-251">Alle vereiste onderdelen en Hallo beheerhulpprogramma's bevatten.</span><span class="sxs-lookup"><span data-stu-id="85096-251">Include all required features and hello management tools.</span></span> <span data-ttu-id="85096-252">Klik op **functies toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="85096-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="85096-253">Klik op **volgende** en klik vervolgens op **voltooien** tooinstall Hallo functies.</span><span class="sxs-lookup"><span data-stu-id="85096-253">Click **Next** and then click **Finish** tooinstall hello features.</span></span>

   <span data-ttu-id="85096-254">tooinstall hello functie Failover Clustering met PowerShell Hallo script van een beheerder PowerShell-sessie te volgen op een van de Hallo virtuele machines worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="85096-254">tooinstall hello Failover Clustering feature with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="85096-255">Voor een verwijzing naar de volgende stappen Hallo instructies Hallo onder stap 3 van [Hyper-geconvergeerde oplossing met behulp van opslagruimten Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="85096-255">For reference, hello next steps follow hello instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-hello-cluster"></a><span data-ttu-id="85096-256">Hallo cluster valideren</span><span class="sxs-lookup"><span data-stu-id="85096-256">Validate hello cluster</span></span>

<span data-ttu-id="85096-257">Deze handleiding verwijst tooinstructions onder [cluster valideren](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span><span class="sxs-lookup"><span data-stu-id="85096-257">This guide refers tooinstructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="85096-258">Hallo-clusters in Hallo gebruikersinterface of met PowerShell valideren.</span><span class="sxs-lookup"><span data-stu-id="85096-258">Validate hello cluster in hello UI or with PowerShell.</span></span>

<span data-ttu-id="85096-259">toovalidate hello cluster met Hallo-gebruikersinterface Hallo volgende stappen uit een van Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="85096-259">toovalidate hello cluster with hello UI, do hello following steps from one of hello virtual machines.</span></span>

1. <span data-ttu-id="85096-260">In **Serverbeheer**, klikt u op **extra**, klikt u vervolgens op **Failoverclusterbeheer**.</span><span class="sxs-lookup"><span data-stu-id="85096-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="85096-261">In **Failoverclusterbeheer**, klikt u op **actie**, klikt u vervolgens op **configuratie valideren...** .</span><span class="sxs-lookup"><span data-stu-id="85096-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="85096-262">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="85096-262">Click **Next**.</span></span>
1. <span data-ttu-id="85096-263">Op **Servers selecteren of een Cluster**, Hallo-typenaam van beide virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="85096-263">On **Select Servers or a Cluster**, type hello name of both virtual machines.</span></span>
1. <span data-ttu-id="85096-264">Op **testopties**, kies **alleen mij geselecteerde tests uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="85096-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="85096-265">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="85096-265">Click **Next**.</span></span>
1. <span data-ttu-id="85096-266">Op **selectie testen**, nemen alle tests uit behalve **opslag**.</span><span class="sxs-lookup"><span data-stu-id="85096-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="85096-267">Zie de volgende afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="85096-267">See hello following picture:</span></span>

   ![Valideren van Tests](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="85096-269">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="85096-269">Click **Next**.</span></span>
1. <span data-ttu-id="85096-270">Op **bevestiging**, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="85096-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="85096-271">Hallo **Wizard een configuratie valideren** wordt uitgevoerd Hallo validatietests.</span><span class="sxs-lookup"><span data-stu-id="85096-271">hello **Validate a Configuration Wizard** runs hello validation tests.</span></span>

<span data-ttu-id="85096-272">toovalidate hello cluster PowerShell Hallo script van een beheerder PowerShell-sessie te volgen op een van de Hallo virtuele machines worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="85096-272">toovalidate hello cluster with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="85096-273">Nadat u Hallo cluster valideren, Hallo failover-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="85096-273">After you validate hello cluster, create hello failover cluster.</span></span>

### <a name="create-hello-failover-cluster"></a><span data-ttu-id="85096-274">Hallo failover-cluster maken</span><span class="sxs-lookup"><span data-stu-id="85096-274">Create hello failover cluster</span></span>

<span data-ttu-id="85096-275">Deze handleiding verwijst te[Hallo failover-cluster maken](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span><span class="sxs-lookup"><span data-stu-id="85096-275">This guide refers too[Create hello failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="85096-276">toocreate hello failover-cluster, moet u de:</span><span class="sxs-lookup"><span data-stu-id="85096-276">toocreate hello failover cluster, you need:</span></span>
- <span data-ttu-id="85096-277">Hallo-namen van Hallo virtuele machines die Hallo clusterknooppunten worden.</span><span class="sxs-lookup"><span data-stu-id="85096-277">hello names of hello virtual machines that become hello cluster nodes.</span></span>
- <span data-ttu-id="85096-278">Een naam op voor Hallo failover-cluster</span><span class="sxs-lookup"><span data-stu-id="85096-278">A name for hello failover cluster</span></span>
- <span data-ttu-id="85096-279">Een IP-adres voor Hallo failover-cluster.</span><span class="sxs-lookup"><span data-stu-id="85096-279">An IP address for hello failover cluster.</span></span> <span data-ttu-id="85096-280">U kunt een IP-adres dat niet wordt gebruikt op Hallo gebruiken hetzelfde virtuele Azure-netwerk en subnet als Hallo clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="85096-280">You can use an IP address that is not used on hello same Azure virtual network and subnet as hello cluster nodes.</span></span>

<span data-ttu-id="85096-281">Hallo PowerShell na maakt een failover-cluster.</span><span class="sxs-lookup"><span data-stu-id="85096-281">hello following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="85096-282">Hallo-script met Hallo namen van Hallo knooppunten (namen Hallo virtuele machine) en een beschikbaar IP-adres uit hello Azure VNET bijwerken:</span><span class="sxs-lookup"><span data-stu-id="85096-282">Update hello script with hello names of hello nodes (hello virtual machine names) and an available IP address from hello Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="85096-283">Maken van een cloud-witness</span><span class="sxs-lookup"><span data-stu-id="85096-283">Create a cloud witness</span></span>

<span data-ttu-id="85096-284">Cloud-Witness is een nieuw type clusterquorum-witness is opgeslagen in een Azure Storage-Blob.</span><span class="sxs-lookup"><span data-stu-id="85096-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="85096-285">Hiermee verwijdert u Hallo behoeften van een afzonderlijke virtuele machine die als host fungeert voor een witness-share.</span><span class="sxs-lookup"><span data-stu-id="85096-285">This removes hello need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="85096-286">[Maken van een cloud-witness voor het failovercluster Hallo](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="85096-286">[Create a cloud witness for hello failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="85096-287">Maak een blob-container.</span><span class="sxs-lookup"><span data-stu-id="85096-287">Create a blob container.</span></span>

1. <span data-ttu-id="85096-288">Hallo toegangstoetsen en de URL van de opslagcontainer Hallo opslaan.</span><span class="sxs-lookup"><span data-stu-id="85096-288">Save hello access keys and hello container URL.</span></span>

1. <span data-ttu-id="85096-289">Hallo failover cluster clusterquorum-witness configureren.</span><span class="sxs-lookup"><span data-stu-id="85096-289">Configure hello failover cluster cluster quorum witness.</span></span> <span data-ttu-id="85096-290">Zie, [configureren Hallo quorumwitness in de gebruikersinterface Hallo]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in Hallo gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="85096-290">See, [Configure hello quorum witness in hello user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in hello UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="85096-291">Opslag toevoegen</span><span class="sxs-lookup"><span data-stu-id="85096-291">Add storage</span></span>

<span data-ttu-id="85096-292">Hallo-schijven voor S2D moeten toobe leeg en zonder partities of andere gegevens.</span><span class="sxs-lookup"><span data-stu-id="85096-292">hello disks for S2D need toobe empty and without partitions or other data.</span></span> <span data-ttu-id="85096-293">Volg tooclean schijven [Hallo stappen in deze handleiding](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span><span class="sxs-lookup"><span data-stu-id="85096-293">tooclean disks follow [hello steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="85096-294">[Store inschakelen opslagruimten Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="85096-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="85096-295">Hallo na PowerShell kunt opslagruimten direct.</span><span class="sxs-lookup"><span data-stu-id="85096-295">hello following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="85096-296">In **Failoverclusterbeheer**, ziet u nu Hallo-opslaggroep.</span><span class="sxs-lookup"><span data-stu-id="85096-296">In **Failover Cluster Manager**, you can now see hello storage pool.</span></span>

1. <span data-ttu-id="85096-297">[Een volume maken](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span><span class="sxs-lookup"><span data-stu-id="85096-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="85096-298">Een van de functies Hallo van S2D is dat er een opslaggroep automatisch gemaakt wanneer u dit inschakelen.</span><span class="sxs-lookup"><span data-stu-id="85096-298">One of hello features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="85096-299">U bent nu klaar toocreate een volume.</span><span class="sxs-lookup"><span data-stu-id="85096-299">You are now ready toocreate a volume.</span></span> <span data-ttu-id="85096-300">PowerShell-commandlet Hallo `New-Volume` automatiseert Hallo volume maken, met inbegrip van de opmaak, toohello cluster toe te voegen en het maken van een gedeeld clustervolume (CSV).</span><span class="sxs-lookup"><span data-stu-id="85096-300">hello PowerShell commandlet `New-Volume` automates hello volume creation process, including formatting, adding toohello cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="85096-301">Hallo volgende voorbeeld maakt een 800 GB (Gigabyte) CSV.</span><span class="sxs-lookup"><span data-stu-id="85096-301">hello following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="85096-302">Nadat u deze opdracht is voltooid, wordt een 800 GB-volume als clusterbron gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="85096-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="85096-303">Hallo volume loopt `C:\ClusterStorage\Volume1\`.</span><span class="sxs-lookup"><span data-stu-id="85096-303">hello volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="85096-304">Hallo volgende diagram ziet u een gedeeld clustervolume met S2D:</span><span class="sxs-lookup"><span data-stu-id="85096-304">hello following diagram shows a cluster shared volume with S2D:</span></span>

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="85096-306">Stap 3: Failover clusterfailover testen</span><span class="sxs-lookup"><span data-stu-id="85096-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="85096-307">In Failoverclusterbeheer, Controleer of dat u Hallo storage resource toohello andere clusterknooppunt verplaatsen kunt.</span><span class="sxs-lookup"><span data-stu-id="85096-307">In Failover Cluster Manager, verify that you can move hello storage resource toohello other cluster node.</span></span> <span data-ttu-id="85096-308">Als u verbinding kunt maken toohello failover-cluster met **Failoverclusterbeheer** en Hallo opslag verplaatsen van één knooppunt toohello andere, bent u klaar tooconfigure Hallo FCI.</span><span class="sxs-lookup"><span data-stu-id="85096-308">If you can connect toohello failover cluster with **Failover Cluster Manager** and move hello storage from one node toohello other, you are ready tooconfigure hello FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="85096-309">Stap 4: SQL Server FCI maken</span><span class="sxs-lookup"><span data-stu-id="85096-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="85096-310">Nadat u Hallo failover-cluster en alle clusteronderdelen inclusief opslag hebt geconfigureerd, kunt u Hallo FCI van SQL Server maken.</span><span class="sxs-lookup"><span data-stu-id="85096-310">After you have configured hello failover cluster and all cluster components including storage, you can create hello SQL Server FCI.</span></span>

1. <span data-ttu-id="85096-311">Toohello eerste virtuele machine verbinden met RDP.</span><span class="sxs-lookup"><span data-stu-id="85096-311">Connect toohello first virtual machine with RDP.</span></span>

1. <span data-ttu-id="85096-312">In **Failoverclusterbeheer**, zorg ervoor dat alle clusterkernresources op Hallo eerste virtuele machine zijn.</span><span class="sxs-lookup"><span data-stu-id="85096-312">In **Failover Cluster Manager**, make sure all cluster core resources are on hello first virtual machine.</span></span> <span data-ttu-id="85096-313">Indien nodig, verplaatst u alle resources toothis virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="85096-313">If necessary, move all resources toothis virtual machine.</span></span>

1. <span data-ttu-id="85096-314">Zoek Hallo-installatiemedia.</span><span class="sxs-lookup"><span data-stu-id="85096-314">Locate hello installation media.</span></span> <span data-ttu-id="85096-315">Als Hallo virtuele machine gebruikmaakt van een van de hello Azure Marketplace-installatiekopieën, Hallo media bevindt zich op `C:\SQLServer_<version number>_Full`.</span><span class="sxs-lookup"><span data-stu-id="85096-315">If hello virtual machine uses one of hello Azure Marketplace images, hello media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="85096-316">Klik op **Setup**.</span><span class="sxs-lookup"><span data-stu-id="85096-316">Click **Setup**.</span></span>

1. <span data-ttu-id="85096-317">In Hallo **Installatiecentrum van SQL Server**, klikt u op **installatie**.</span><span class="sxs-lookup"><span data-stu-id="85096-317">In hello **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="85096-318">Klik op **New SQL Server failover cluster installation**.</span><span class="sxs-lookup"><span data-stu-id="85096-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="85096-319">Volg de instructies Hallo in Hallo wizard tooinstall Hallo FCI van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="85096-319">Follow hello instructions in hello wizard tooinstall hello SQL Server FCI.</span></span>

   <span data-ttu-id="85096-320">Hallo FCI gegevensmappen moeten toobe op geclusterde opslag.</span><span class="sxs-lookup"><span data-stu-id="85096-320">hello FCI data directories need toobe on clustered storage.</span></span> <span data-ttu-id="85096-321">Met S2D is het niet een gedeelde schijf, maar een volume koppelen punt tooa op elke server.</span><span class="sxs-lookup"><span data-stu-id="85096-321">With S2D, it's not a shared disk, but a mount point tooa volume on each server.</span></span> <span data-ttu-id="85096-322">S2D synchroniseert Hallo volume tussen beide knooppunten.</span><span class="sxs-lookup"><span data-stu-id="85096-322">S2D synchronizes hello volume between both nodes.</span></span> <span data-ttu-id="85096-323">Hallo-volume wordt gepresenteerd toohello cluster een cluster shared volume.</span><span class="sxs-lookup"><span data-stu-id="85096-323">hello volume is presented toohello cluster as a cluster shared volume.</span></span> <span data-ttu-id="85096-324">Hallo CSV koppelpunt voor gegevensmappen hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="85096-324">Use hello CSV mount point for hello data directories.</span></span>

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="85096-326">Nadat u Hallo wizard hebt voltooid, installeert Setup een FCI SQL Server op Hallo eerste knooppunt.</span><span class="sxs-lookup"><span data-stu-id="85096-326">After you complete hello wizard, Setup will install a SQL Server FCI on hello first node.</span></span>

1. <span data-ttu-id="85096-327">Nadat Setup is Hallo FCI is geïnstalleerd op het eerste knooppunt hello, verbinding maken met het tweede knooppunt toohello met RDP.</span><span class="sxs-lookup"><span data-stu-id="85096-327">After Setup successfully installs hello FCI on hello first node, connect toohello second node with RDP.</span></span>

1. <span data-ttu-id="85096-328">Open Hallo **Installatiecentrum van SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="85096-328">Open hello **SQL Server Installation Center**.</span></span> <span data-ttu-id="85096-329">Klik op **installatie**.</span><span class="sxs-lookup"><span data-stu-id="85096-329">Click **Installation**.</span></span>

1. <span data-ttu-id="85096-330">Klik op **toevoegen knooppunt tooa SQL Server-failovercluster**.</span><span class="sxs-lookup"><span data-stu-id="85096-330">Click **Add node tooa SQL Server failover cluster**.</span></span> <span data-ttu-id="85096-331">Volg de instructies Hallo in Hallo wizard tooinstall SQL server en voeg deze server toohello FCI.</span><span class="sxs-lookup"><span data-stu-id="85096-331">Follow hello instructions in hello wizard tooinstall SQL server and add this server toohello FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="85096-332">Als u een installatiekopie van de galerie van Azure Marketplace met SQL Server gebruikt, zijn SQL Server-hulpprogramma's opgenomen in de installatiekopie van het Hallo.</span><span class="sxs-lookup"><span data-stu-id="85096-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with hello image.</span></span> <span data-ttu-id="85096-333">Als u deze installatiekopie niet gebruikt, afzonderlijk Hallo SQL Server-hulpprogramma's installeren.</span><span class="sxs-lookup"><span data-stu-id="85096-333">If you did not use this image, install hello SQL Server tools separately.</span></span> <span data-ttu-id="85096-334">Zie [downloaden van SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="85096-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="85096-335">Stap 5: Azure load balancer maken</span><span class="sxs-lookup"><span data-stu-id="85096-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="85096-336">Clusters gebruik op virtuele machines in Azure, een load balancer toohold een IP-adres dat toobe op één clusterknooppunt tegelijk moet.</span><span class="sxs-lookup"><span data-stu-id="85096-336">On Azure virtual machines, clusters use a load balancer toohold an IP address that needs toobe on one cluster node at a time.</span></span> <span data-ttu-id="85096-337">In deze oplossing bevat Hallo load balancer Hallo IP-adres voor Hallo FCI van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="85096-337">In this solution, hello load balancer holds hello IP address for hello SQL Server FCI.</span></span>

<span data-ttu-id="85096-338">[Maken en configureren van een Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="85096-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="85096-339">Hallo load balancer maken in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="85096-339">Create hello load balancer in hello Azure portal</span></span>

<span data-ttu-id="85096-340">toocreate hello load balancer:</span><span class="sxs-lookup"><span data-stu-id="85096-340">toocreate hello load balancer:</span></span>

1. <span data-ttu-id="85096-341">Ga in de Azure-portal hello, toohello resourcegroep met Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="85096-341">In hello Azure portal, go toohello Resource Group with hello virtual machines.</span></span>

1. <span data-ttu-id="85096-342">Klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="85096-342">Click **+ Add**.</span></span> <span data-ttu-id="85096-343">Zoeken Hallo Marketplace voor **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="85096-343">Search hello Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="85096-344">Klik op **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="85096-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="85096-345">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="85096-345">Click **Create**.</span></span>

1. <span data-ttu-id="85096-346">Hallo load balancer met configureren:</span><span class="sxs-lookup"><span data-stu-id="85096-346">Configure hello load balancer with:</span></span>

   - <span data-ttu-id="85096-347">**Naam**: een naam waarmee Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="85096-347">**Name**: A name that identifies hello load balancer.</span></span>
   - <span data-ttu-id="85096-348">**Type**: Hallo load balancer mag openbare of particuliere.</span><span class="sxs-lookup"><span data-stu-id="85096-348">**Type**: hello load balancer can be either public or private.</span></span> <span data-ttu-id="85096-349">Een persoonlijke load balancer toegankelijk is vanuit Hallo hetzelfde VNET.</span><span class="sxs-lookup"><span data-stu-id="85096-349">A private load balancer can be accessed from within hello same VNET.</span></span> <span data-ttu-id="85096-350">De meeste Azure toepassingen kunnen gebruikmaken van een persoonlijke load balancer.</span><span class="sxs-lookup"><span data-stu-id="85096-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="85096-351">Als uw toepassing toegang tooSQL Server rechtstreeks via Internet hello moet, gebruikt u een openbare load balancer.</span><span class="sxs-lookup"><span data-stu-id="85096-351">If your application needs access tooSQL Server directly over hello Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="85096-352">**Virtueel netwerk**: Hallo netwerk als Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="85096-352">**Virtual Network**: hello same network as hello virtual machines.</span></span>
   - <span data-ttu-id="85096-353">**Subnet**: Hallo hetzelfde subnet als Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="85096-353">**Subnet**: hello same subnet as hello virtual machines.</span></span>
   - <span data-ttu-id="85096-354">**Privé IP-adres**: Hallo hetzelfde IP-adres dat u toohello FCI van SQL Server-clusterbron in het netwerk worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="85096-354">**Private IP address**: hello same IP address that you assigned toohello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="85096-355">**abonnement**: uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="85096-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="85096-356">**Resourcegroep**: gebruik Hallo dezelfde resourcegroep als uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="85096-356">**Resource Group**: Use hello same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="85096-357">**Locatie**: gebruik dezelfde hello Azure-locatie als uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="85096-357">**Location**: Use hello same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="85096-358">Zie de volgende afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="85096-358">See hello following picture:</span></span>

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a><span data-ttu-id="85096-360">Back-endpool van Hallo load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="85096-360">Configure hello load balancer backend pool</span></span>

1. <span data-ttu-id="85096-361">Toohello Azure-resourcegroep met Hallo virtuele machines retourneren en Ga naar Hallo nieuwe load balancer.</span><span class="sxs-lookup"><span data-stu-id="85096-361">Return toohello Azure Resource Group with hello virtual machines and locate hello new load balancer.</span></span> <span data-ttu-id="85096-362">Wellicht hebt u toorefresh Hallo weergave op Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="85096-362">You may have toorefresh hello view on hello Resource Group.</span></span> <span data-ttu-id="85096-363">Klik op Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="85096-363">Click hello load balancer.</span></span>

1. <span data-ttu-id="85096-364">Klik op Hallo load balancer blade **back-endpools**.</span><span class="sxs-lookup"><span data-stu-id="85096-364">On hello load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="85096-365">Klik op **+ toevoegen** tooadd een back-endpool.</span><span class="sxs-lookup"><span data-stu-id="85096-365">Click **+ Add** tooadd a backend pool.</span></span>

1. <span data-ttu-id="85096-366">Typ een naam voor de back-endpool Hallo.</span><span class="sxs-lookup"><span data-stu-id="85096-366">Type a name for hello backend pool.</span></span>

1. <span data-ttu-id="85096-367">Klik op **toevoegen van een virtuele machine**.</span><span class="sxs-lookup"><span data-stu-id="85096-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="85096-368">Op Hallo **virtuele machines kiezen** blade, klikt u op **een beschikbaarheidsset kiezen**.</span><span class="sxs-lookup"><span data-stu-id="85096-368">On hello **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="85096-369">Kies Hallo beschikbaarheidsset u Hallo SQL Server-virtuele machines in hebt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="85096-369">Choose hello availability set that you placed hello SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="85096-370">Op Hallo **virtuele machines kiezen** blade, klikt u op **Hallo virtuele machines kiezen**.</span><span class="sxs-lookup"><span data-stu-id="85096-370">On hello **Choose virtual machines** blade, click **Choose hello virtual machines**.</span></span>

   <span data-ttu-id="85096-371">Uw Azure-portal moet eruitzien als Hallo volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="85096-371">Your Azure portal should look like hello following picture:</span></span>

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="85096-373">Klik op **Selecteer** op Hallo **virtuele machines kiezen** blade.</span><span class="sxs-lookup"><span data-stu-id="85096-373">Click **Select** on hello **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="85096-374">Klik op **OK** twee keer.</span><span class="sxs-lookup"><span data-stu-id="85096-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="85096-375">Een load balancer-test health configureren</span><span class="sxs-lookup"><span data-stu-id="85096-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="85096-376">Klik op Hallo load balancer blade **statuscontroles**.</span><span class="sxs-lookup"><span data-stu-id="85096-376">On hello load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="85096-377">Klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="85096-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="85096-378">Op Hallo **toevoegen health test** blade <a name="probe"> </a>Hallo health test parameters instellen:</span><span class="sxs-lookup"><span data-stu-id="85096-378">On hello **Add health probe** blade, <a name="probe"></a>Set hello health probe parameters:</span></span>

   - <span data-ttu-id="85096-379">**Naam**: een naam voor de Hallo health test.</span><span class="sxs-lookup"><span data-stu-id="85096-379">**Name**: A name for hello health probe.</span></span>
   - <span data-ttu-id="85096-380">**Protocol**: TCP.</span><span class="sxs-lookup"><span data-stu-id="85096-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="85096-381">**Poort**: tooan beschikbare TCP-poort ingesteld.</span><span class="sxs-lookup"><span data-stu-id="85096-381">**Port**: Set tooan available TCP port.</span></span> <span data-ttu-id="85096-382">Deze poort moet een firewallpoort worden geopend.</span><span class="sxs-lookup"><span data-stu-id="85096-382">This port requires an open firewall port.</span></span> <span data-ttu-id="85096-383">Gebruik Hallo [dezelfde poort](#ports) u instellen voor de Hallo health test op Hallo firewall.</span><span class="sxs-lookup"><span data-stu-id="85096-383">Use hello [same port](#ports) you set for hello health probe at hello firewall.</span></span>
   - <span data-ttu-id="85096-384">**Interval**: 5 seconden.</span><span class="sxs-lookup"><span data-stu-id="85096-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="85096-385">**Drempelwaarde voor onjuiste status**: 2 achtereenvolgende mislukte pogingen.</span><span class="sxs-lookup"><span data-stu-id="85096-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="85096-386">Klik op OK.</span><span class="sxs-lookup"><span data-stu-id="85096-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="85096-387">Taakverdelingsregels instellen</span><span class="sxs-lookup"><span data-stu-id="85096-387">Set load balancing rules</span></span>

1. <span data-ttu-id="85096-388">Klik op Hallo load balancer blade **Taakverdelingsregels**.</span><span class="sxs-lookup"><span data-stu-id="85096-388">On hello load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="85096-389">Klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="85096-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="85096-390">Hallo load balancing regels parameters instellen:</span><span class="sxs-lookup"><span data-stu-id="85096-390">Set hello load balancing rules parameters:</span></span>

   - <span data-ttu-id="85096-391">**Naam**: een naam op voor Hallo load-balancingregels.</span><span class="sxs-lookup"><span data-stu-id="85096-391">**Name**: A name for hello load balancing rules.</span></span>
   - <span data-ttu-id="85096-392">**Frontend IP-adres**: Hallo IP-adres gebruiken voor Hallo netwerkbron FCI van SQL Server-cluster.</span><span class="sxs-lookup"><span data-stu-id="85096-392">**Frontend IP address**: Use hello IP address for hello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="85096-393">**Poort**: ingesteld voor Hallo SQL Server FCI TCP-poort.</span><span class="sxs-lookup"><span data-stu-id="85096-393">**Port**: Set for hello SQL Server FCI TCP port.</span></span> <span data-ttu-id="85096-394">Hallo exemplaar standaardpoort is 1433.</span><span class="sxs-lookup"><span data-stu-id="85096-394">hello default instance port is 1433.</span></span>
   - <span data-ttu-id="85096-395">**Back-endpoort**: deze waarde gebruikt Hallo dezelfde poort als Hallo **poort** waarde wanneer u inschakelt **zwevend IP (direct server return)**.</span><span class="sxs-lookup"><span data-stu-id="85096-395">**Backend port**: This value uses hello same port as hello **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="85096-396">**Back-endpool**: gebruik Hallo back-end Poolnaam die u eerder hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="85096-396">**Backend pool**: Use hello backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="85096-397">**De statuscontrole van**: gebruik Hallo health test op die u eerder hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="85096-397">**Health probe**: Use hello health probe that you configured earlier.</span></span>
   - <span data-ttu-id="85096-398">**Sessiepersistentie**: geen.</span><span class="sxs-lookup"><span data-stu-id="85096-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="85096-399">**Time-out (minuten)**: 4.</span><span class="sxs-lookup"><span data-stu-id="85096-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="85096-400">**Zwevend IP (direct server return)**: ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="85096-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="85096-401">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="85096-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="85096-402">Stap 6: Configureren voor de test-cluster</span><span class="sxs-lookup"><span data-stu-id="85096-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="85096-403">Stel Hallo cluster test poortparameter in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="85096-403">Set hello cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="85096-404">tooset Hallo cluster test poortparameter, update variabelen in het volgende script uit uw omgeving Hallo.</span><span class="sxs-lookup"><span data-stu-id="85096-404">tooset hello cluster probe port parameter, update variables in hello following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="85096-405">Stap 7: Testen FCI failover</span><span class="sxs-lookup"><span data-stu-id="85096-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="85096-406">Failover van Hallo FCI toovalidate clusterfunctionaliteit wilt testen.</span><span class="sxs-lookup"><span data-stu-id="85096-406">Test failover of hello FCI toovalidate cluster functionality.</span></span> <span data-ttu-id="85096-407">Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="85096-407">Do hello following steps:</span></span>

1. <span data-ttu-id="85096-408">Tooone van clusterknooppunten voor SQL Server FCI Hallo met RDP verbinding.</span><span class="sxs-lookup"><span data-stu-id="85096-408">Connect tooone of hello SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="85096-409">Open **Failoverclusterbeheer**.</span><span class="sxs-lookup"><span data-stu-id="85096-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="85096-410">Klik op **rollen**.</span><span class="sxs-lookup"><span data-stu-id="85096-410">Click **Roles**.</span></span> <span data-ttu-id="85096-411">De aankondiging welk knooppunt eigenaar van Hallo FCI van SQL Server-rol.</span><span class="sxs-lookup"><span data-stu-id="85096-411">Notice which node owns hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="85096-412">Met de rechtermuisknop op Hallo FCI van SQL Server-rol.</span><span class="sxs-lookup"><span data-stu-id="85096-412">Right-click hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="85096-413">Klik op **verplaatsen** en klik op **Best mogelijke knooppunt**.</span><span class="sxs-lookup"><span data-stu-id="85096-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="85096-414">**Failover Cluster Manager** toont Hallo rol en de daarbij behorende bronnen offline gaan.</span><span class="sxs-lookup"><span data-stu-id="85096-414">**Failover Cluster Manager** shows hello role and its resources go offline.</span></span> <span data-ttu-id="85096-415">Hallo resources Verplaats en online komen op Hallo andere knooppunt.</span><span class="sxs-lookup"><span data-stu-id="85096-415">hello resources then move and come online on hello other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="85096-416">Connectiviteit testen</span><span class="sxs-lookup"><span data-stu-id="85096-416">Test connectivity</span></span>

<span data-ttu-id="85096-417">tootest connectiviteit, log in tooanother virtuele machine in Hallo hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="85096-417">tootest connectivity, log in tooanother virtual machine in hello same virtual network.</span></span> <span data-ttu-id="85096-418">Open **SQL Server Management Studio** en verbinding maken met de naam van de SQL Server FCI toohello.</span><span class="sxs-lookup"><span data-stu-id="85096-418">Open **SQL Server Management Studio** and connect toohello SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="85096-419">Zo nodig u kunt [SQL Server Management Studio downloaden](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="85096-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="85096-420">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="85096-420">Limitations</span></span>
<span data-ttu-id="85096-421">Op virtuele machines in Azure, wordt Microsoft Distributed Transaction Coordinator (DTC) niet ondersteund op Failoverclusterinstanties omdat Hallo RPC-poort wordt niet ondersteund door Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="85096-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because hello RPC port is not supported by hello load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="85096-422">Zie ook</span><span class="sxs-lookup"><span data-stu-id="85096-422">See Also</span></span>

[<span data-ttu-id="85096-423">Setup S2D met extern bureaublad (Azure)</span><span class="sxs-lookup"><span data-stu-id="85096-423">Setup S2D with remote desktop (Azure)</span></span>](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

<span data-ttu-id="85096-424">[Hyper-geconvergeerde oplossing met opslagruimten direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="85096-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

[<span data-ttu-id="85096-425">Directe opslag ruimte-overzicht</span><span class="sxs-lookup"><span data-stu-id="85096-425">Storage Space Direct Overview</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[<span data-ttu-id="85096-426">SQL Server-ondersteuning voor S2D</span><span class="sxs-lookup"><span data-stu-id="85096-426">SQL Server support for S2D</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)

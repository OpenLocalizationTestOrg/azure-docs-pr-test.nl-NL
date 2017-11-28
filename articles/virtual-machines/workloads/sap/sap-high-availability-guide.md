---
title: hoge beschikbaarheid van de virtuele Machines voor SAP NetWeaver aaaAzure | Microsoft Docs
description: Hoge beschikbaarheid-handleiding voor SAP NetWeaver op Azure Virtual Machines
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 662dd793390d7f6138b160ed86259d13391336aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a><span data-ttu-id="f540f-103">Azure virtuele Machines hoge beschikbaarheid voor SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="f540f-103">Azure Virtual Machines high availability for SAP NetWeaver</span></span>

[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:./media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:./media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:./media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:./media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:./media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:./media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:./media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:./media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:./media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:./media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:./media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:./media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:./media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:./media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:./media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:./media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:./media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:./media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:./media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:./media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:./media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:./media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:./media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:./media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:./media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:./media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:./media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:./media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:./media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:./media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:./media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:./media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:./media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:./media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:./media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:./media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:./media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:./media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:./media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:./media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:./media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:./media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:./media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:./media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:./media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:./media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:./media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:./media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:./media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:./media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:./media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:./media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:./media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:./media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:./media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:./media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:./media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:./media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:./media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:./media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:./media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:./media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:./media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md



<span data-ttu-id="f540f-109">Virtuele Machines in Azure is Hallo-oplossing voor organisaties die berekenings-, opslag- en netwerkbronnen, in de minimale tijd en zonder langdurige inkoop cycli moeten.</span><span class="sxs-lookup"><span data-stu-id="f540f-109">Azure Virtual Machines is hello solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="f540f-110">U kunt Azure Virtual Machines toodeploy klassieke toepassingen zoals SAP NetWeaver gebaseerde ABAP, Java en een ABAP + Java-stack gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f540f-110">You can use Azure Virtual Machines toodeploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="f540f-111">Betrouwbaarheid en beschikbaarheid zonder dat extra on-premises resources uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="f540f-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="f540f-112">Virtuele Machines in Azure ondersteunt cross-premises connectiviteit, zodat u kunt Azure Virtual Machines integreren in uw organisatie lokale domeinen, privéclouds en SAP system Liggend.</span><span class="sxs-lookup"><span data-stu-id="f540f-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="f540f-113">In dit artikel wordt uitgelegd we Hallo stappen die u toodeploy SAP-systemen voor hoge beschikbaarheid in Azure ondernemen kunt met hello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="f540f-113">In this article, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="f540f-114">We helpt u bij deze belangrijke taken:</span><span class="sxs-lookup"><span data-stu-id="f540f-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="f540f-115">Hallo zoeken rechts SAP-opmerkingen en installatie implementatiehandleidingen, die worden vermeld in Hallo [Resources] [ sap-ha-guide-2] sectie.</span><span class="sxs-lookup"><span data-stu-id="f540f-115">Find hello right SAP Notes and installation guides, listed in hello [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="f540f-116">In dit artikel is een aanvulling op de documentatie voor SAP-installatie en SAP-opmerkingen, de primaire Hallo-bronnen waarmee u kunnen installeren en SAP software implementeren op specifieke platforms.</span><span class="sxs-lookup"><span data-stu-id="f540f-116">This article complements SAP installation documentation and SAP Notes, which are hello primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="f540f-117">Meer informatie over Hallo verschillen tussen hello Azure Resource Manager-implementatiemodel en hello Azure klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="f540f-117">Learn hello differences between hello Azure Resource Manager deployment model and hello Azure classic deployment model.</span></span>
* <span data-ttu-id="f540f-118">Meer informatie over Windows Server Failover Clustering quorum-modi, zodat u Hallo model dat geschikt is voor uw Azure-implementatie kunt selecteren.</span><span class="sxs-lookup"><span data-stu-id="f540f-118">Learn about Windows Server Failover Clustering quorum modes, so you can select hello model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="f540f-119">Meer informatie over Windows Server Failover Clustering gedeelde opslag in Azure-services.</span><span class="sxs-lookup"><span data-stu-id="f540f-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="f540f-120">Meer informatie over hoe de onderdelen van één punt van fout zoals geavanceerde Business Application Programming (ABAP) SAP centrale Services (ASC's) voor het beveiligen van toohelp / SAP centrale Services (SCS) en databasebeheersystemen (DBMS) en redundante componenten zoals SAP Toepassingsserver in Azure.</span><span class="sxs-lookup"><span data-stu-id="f540f-120">Learn how toohelp protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="f540f-121">Ga als volgt een voorbeeld van een stapsgewijze van een installatie en configuratie van een SAP-systeem voor hoge beschikbaarheid in een cluster met Windows Server Failover Clustering in Azure met Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f540f-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="f540f-122">Meer informatie over extra stappen vereist toouse Windows Server Failover Clustering in Azure, maar die niet nodig zijn in een on-premises implementatie.</span><span class="sxs-lookup"><span data-stu-id="f540f-122">Learn about additional steps required toouse Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="f540f-123">toosimplify implementatie en configuratie in dit artikel gebruiken we Hallo SAP drie lagen hoge beschikbaarheid Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="f540f-123">toosimplify deployment and configuration, in this article, we use hello SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="f540f-124">Hallo sjablonen automatisering van Hallo gehele infrastructuur die u nodig hebt voor een hoge beschikbaarheid SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="f540f-124">hello templates automate deployment of hello entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="f540f-125">Hallo-infrastructuur ondersteunt ook het formaat van uw systeem SAP SAP toepassing prestaties Standard (SAP's).</span><span class="sxs-lookup"><span data-stu-id="f540f-125">hello infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="f540f-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="f540f-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="f540f-127">Zorg voordat u begint, dat u voldoet aan de Hallo vereisten die worden beschreven in Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="f540f-127">Before you start, make sure that you meet hello prerequisites that are described in hello following sections.</span></span> <span data-ttu-id="f540f-128">Wees ook zeker toocheck alle resources die worden vermeld in Hallo [Resources] [ sap-ha-guide-2] sectie.</span><span class="sxs-lookup"><span data-stu-id="f540f-128">Also, be sure toocheck all resources listed in hello [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="f540f-129">In dit artikel gebruiken we Azure Resource Manager-sjablonen voor [drie lagen SAP NetWeaver schijven beheerd](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span><span class="sxs-lookup"><span data-stu-id="f540f-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver using Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span></span> <span data-ttu-id="f540f-130">Zie voor een handig overzicht van sjablonen [SAP Azure Resource Manager-sjablonen](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span><span class="sxs-lookup"><span data-stu-id="f540f-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="f540f-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a>Resources</span><span class="sxs-lookup"><span data-stu-id="f540f-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="f540f-132">Deze artikelen omvatten SAP-implementaties in Azure:</span><span class="sxs-lookup"><span data-stu-id="f540f-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="f540f-133">[Azure virtuele Machines, planning en implementatie voor SAP NetWeaver][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="f540f-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="f540f-134">[Azure virtuele Machines-implementatie voor SAP NetWeaver][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="f540f-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="f540f-135">[Azure virtuele Machines DBMS-implementatie voor SAP NetWeaver][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="f540f-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="f540f-136">[Azure virtuele Machines hoge beschikbaarheid voor SAP NetWeaver (deze handleiding)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="f540f-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="f540f-137">Waar mogelijk, geven wij u een koppeling toohello SAP installatiehandleiding verwijzen (Zie Hallo [SAP installatiehandleidingen][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="f540f-137">Whenever possible, we give you a link toohello referring SAP installation guide (see hello [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="f540f-138">Voor vereisten en informatie over het Hallo-installatieproces, het een goed idee tooread Hallo SAP NetWeaver installatie zorgvuldig leidt.</span><span class="sxs-lookup"><span data-stu-id="f540f-138">For prerequisites and information about hello installation process, it's a good idea tooread hello SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="f540f-139">Dit artikel behandelt alleen specifieke taken voor SAP NetWeaver-gebaseerde computers die u met Azure Virtual Machines gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="f540f-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="f540f-140">Deze opmerkingen SAP zijn verwante toohello onderwerp van SAP in Azure:</span><span class="sxs-lookup"><span data-stu-id="f540f-140">These SAP Notes are related toohello topic of SAP in Azure:</span></span>

| <span data-ttu-id="f540f-141">Het nummer</span><span class="sxs-lookup"><span data-stu-id="f540f-141">Note number</span></span> | <span data-ttu-id="f540f-142">Titel</span><span class="sxs-lookup"><span data-stu-id="f540f-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="f540f-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="f540f-143">[1928533]</span></span> |<span data-ttu-id="f540f-144">SAP-toepassingen in Azure: ondersteunde producten en schaling</span><span class="sxs-lookup"><span data-stu-id="f540f-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="f540f-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="f540f-145">[2015553]</span></span> |<span data-ttu-id="f540f-146">SAP op Microsoft Azure: ondersteuning voor vereisten</span><span class="sxs-lookup"><span data-stu-id="f540f-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="f540f-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="f540f-147">[1999351]</span></span> |<span data-ttu-id="f540f-148">Verbeterde Azure bewaking voor SAP</span><span class="sxs-lookup"><span data-stu-id="f540f-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="f540f-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="f540f-149">[2178632]</span></span> |<span data-ttu-id="f540f-150">Sleutel bewaking van metrische gegevens voor SAP op Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f540f-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="f540f-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="f540f-151">[1999351]</span></span> |<span data-ttu-id="f540f-152">Virtualisatie in Windows: uitgebreide bewaking</span><span class="sxs-lookup"><span data-stu-id="f540f-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="f540f-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="f540f-153">[2243692]</span></span> |<span data-ttu-id="f540f-154">Gebruik van Azure Premium-SSD-opslag voor SAP DBMS exemplaar</span><span class="sxs-lookup"><span data-stu-id="f540f-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="f540f-155">Meer informatie over Hallo [beperkingen van de Azure-abonnementen][azure-subscription-service-limits-subscription], waaronder algemene standaardbeperkingen en maximale beperkingen.</span><span class="sxs-lookup"><span data-stu-id="f540f-155">Learn more about hello [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="f540f-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>Hoge beschikbaarheid SAP met Azure Resource Manager versus hello Azure klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="f540f-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. hello Azure classic deployment model</span></span>
<span data-ttu-id="f540f-157">Hello Azure Resource Manager en Azure klassieke implementatiemodel zijn verschillende in Hallo gebieden te volgen:</span><span class="sxs-lookup"><span data-stu-id="f540f-157">hello Azure Resource Manager and Azure classic deployment models are different in hello following areas:</span></span>

- <span data-ttu-id="f540f-158">Resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="f540f-158">Resource groups</span></span>
- <span data-ttu-id="f540f-159">Azure interne load balancer-afhankelijkheid van hello Azure-resourcegroep</span><span class="sxs-lookup"><span data-stu-id="f540f-159">Azure internal load balancer dependency on hello Azure resource group</span></span>
- <span data-ttu-id="f540f-160">Ondersteuning voor SAP multi-SID-scenario 's</span><span class="sxs-lookup"><span data-stu-id="f540f-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="f540f-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a>Resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="f540f-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="f540f-162">In Azure Resource Manager kunt u resource groepen toomanage alle Hallo toepassingsresources in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f540f-162">In Azure Resource Manager, you can use resource groups toomanage all hello application resources in your Azure subscription.</span></span> <span data-ttu-id="f540f-163">Een geïntegreerde benadering, in een resourcegroep van alle resources hebben Hallo dezelfde levenscyclus.</span><span class="sxs-lookup"><span data-stu-id="f540f-163">An integrated approach, in a resource group, all resources have hello same life cycle.</span></span> <span data-ttu-id="f540f-164">Bijvoorbeeld, alle resources worden gemaakt op Hallo dezelfde tijd en ze worden verwijderd op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="f540f-164">For example, all resources are created at hello same time and they are deleted at hello same time.</span></span> <span data-ttu-id="f540f-165">Meer informatie over [resourcegroepen](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="f540f-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="f540f-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure interne load balancer-afhankelijkheid van hello Azure-resourcegroep</span><span class="sxs-lookup"><span data-stu-id="f540f-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on hello Azure resource group</span></span>

<span data-ttu-id="f540f-167">Hello Azure klassieke implementatiemodel is er een afhankelijkheid tussen hello Azure interne load balancer (Azure Load Balancer-service) en het Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="f540f-167">In hello Azure classic deployment model, there is a dependency between hello Azure internal load balancer (Azure Load Balancer service) and hello cloud service.</span></span> <span data-ttu-id="f540f-168">Elke interne load balancer moet een service in de cloud.</span><span class="sxs-lookup"><span data-stu-id="f540f-168">Every internal load balancer needs one cloud service.</span></span>

<span data-ttu-id="f540f-169">In Azure Resource Manager elk Azure-resource moet toobe in een Azure-resourcegroep geplaatst en dit is ook geldig voor de Load Balancer van Azure.</span><span class="sxs-lookup"><span data-stu-id="f540f-169">In Azure Resource Manager, every Azure resource needs toobe placed into an Azure resource group, and this is valid for Azure Load Balancer as well.</span></span> <span data-ttu-id="f540f-170">Maar er is geen groep nodig toohave één Azure-resource per Azure-load balancer, bijvoorbeeld één Azure-resourcegroep meerdere Azure Load Balancers kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="f540f-170">However, there is no need toohave one Azure resource group per Azure load balancer, e.g. one Azure resource group can contain multiple Azure Load Balancers.</span></span> <span data-ttu-id="f540f-171">Hallo-omgeving is eenvoudiger en flexibeler.</span><span class="sxs-lookup"><span data-stu-id="f540f-171">hello environment is simpler and more flexible.</span></span> 

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="f540f-172">Ondersteuning voor SAP multi-SID-scenario 's</span><span class="sxs-lookup"><span data-stu-id="f540f-172">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="f540f-173">In Azure Resource Manager kunt u meerdere SAP systeem-id (SID) ASC's / SCS exemplaren in één cluster installeren.</span><span class="sxs-lookup"><span data-stu-id="f540f-173">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="f540f-174">Multi-SID-exemplaren zijn mogelijk vanwege ondersteuning voor meerdere IP-adressen voor elke Azure interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="f540f-174">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="f540f-175">toouse hello Azure klassieke implementatiemodel, voert u de procedures op Hallo van [SAP NetWeaver in Azure: Clustering SAP ASC's / SCS exemplaren met behulp van Windows Server Failover Clustering in Azure met SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span><span class="sxs-lookup"><span data-stu-id="f540f-175">toouse hello Azure classic deployment model, follow hello procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f540f-176">Het is raadzaam dat u hello Azure Resource Manager-implementatiemodel voor uw SAP-installaties.</span><span class="sxs-lookup"><span data-stu-id="f540f-176">We strongly recommend that you use hello Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="f540f-177">Dit biedt veel voordelen die niet beschikbaar in het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="f540f-177">It offers many benefits that are not available in hello classic deployment model.</span></span> <span data-ttu-id="f540f-178">Meer informatie over Azure [implementatiemodellen][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span><span class="sxs-lookup"><span data-stu-id="f540f-178">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="f540f-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a>Windows Serverfailover Clustering</span><span class="sxs-lookup"><span data-stu-id="f540f-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="f540f-180">Windows Server Failover Clustering is Hallo-basis van een hoge beschikbaarheid SAP ASC's / SCS installatie en DBMS in Windows.</span><span class="sxs-lookup"><span data-stu-id="f540f-180">Windows Server Failover Clustering is hello foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="f540f-181">Een failovercluster is een groep 1 + n onafhankelijke servers (knooppunten) die samenwerken tooincrease Hallo beschikbaarheid van toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="f540f-181">A failover cluster is a group of 1+n independent servers (nodes) that work together tooincrease hello availability of applications and services.</span></span> <span data-ttu-id="f540f-182">Als een knooppuntfout optreedt, Windows Server Failover Clustering berekent het aantal fouten die zich voordoen kunnen tijdens het onderhoud van een gezonde Hallo cluster tooprovide toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="f540f-182">If a node failure occurs, Windows Server Failover Clustering calculates hello number of failures that can occur while maintaining a healthy cluster tooprovide applications and services.</span></span> <span data-ttu-id="f540f-183">U kunt kiezen uit andere quorum-modi tooachieve Failoverclustering.</span><span class="sxs-lookup"><span data-stu-id="f540f-183">You can choose from different quorum modes tooachieve failover clustering.</span></span>

### <span data-ttu-id="f540f-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a>Quorum-modi</span><span class="sxs-lookup"><span data-stu-id="f540f-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="f540f-185">U kunt kiezen uit vier quorum-modi wanneer u Windows Server Failover Clustering:</span><span class="sxs-lookup"><span data-stu-id="f540f-185">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="f540f-186">**Knooppuntmeerderheid**.</span><span class="sxs-lookup"><span data-stu-id="f540f-186">**Node Majority**.</span></span> <span data-ttu-id="f540f-187">Elk knooppunt van Hallo kunt stemmen.</span><span class="sxs-lookup"><span data-stu-id="f540f-187">Each node of hello cluster can vote.</span></span> <span data-ttu-id="f540f-188">Hallo cluster werkt alleen met een meerderheid van stemmen, dat wil zeggen, met meer dan de helft Hallo stemmen.</span><span class="sxs-lookup"><span data-stu-id="f540f-188">hello cluster functions only with a majority of votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="f540f-189">U wordt aangeraden deze optie voor clusters met een oneven aantal knooppunten.</span><span class="sxs-lookup"><span data-stu-id="f540f-189">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="f540f-190">Bijvoorbeeld drie knooppunten in een cluster met zeven knooppunten kunnen mislukken en Hallo cluster tussen beelden meerderheid bereikt en toorun blijft.</span><span class="sxs-lookup"><span data-stu-id="f540f-190">For example, three nodes in a seven-node cluster can fail, and hello cluster stills achieves a majority and continues toorun.</span></span>  
* <span data-ttu-id="f540f-191">**Knooppunt en schijfmeerderheid**.</span><span class="sxs-lookup"><span data-stu-id="f540f-191">**Node and Disk Majority**.</span></span> <span data-ttu-id="f540f-192">Elk knooppunt en een aangewezen schijf (een schijfwitness) in de clusteropslag Hallo kunnen stemmen wanneer ze beschikbaar zijn en in de communicatie.</span><span class="sxs-lookup"><span data-stu-id="f540f-192">Each node and a designated disk (a disk witness) in hello cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="f540f-193">Hallo cluster werkt alleen met een meerderheid van Hallo stemmen, dat wil zeggen, met meer dan de helft Hallo stemmen.</span><span class="sxs-lookup"><span data-stu-id="f540f-193">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="f540f-194">Deze modus is wel zinvol in een clusteromgeving met een even aantal knooppunten.</span><span class="sxs-lookup"><span data-stu-id="f540f-194">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="f540f-195">Als Hallo schijf en half Hallo knooppunten online zijn, blijft Hallo-cluster in een foutloze toestand bevindt.</span><span class="sxs-lookup"><span data-stu-id="f540f-195">If half hello nodes and hello disk are online, hello cluster remains in a healthy state.</span></span>
* <span data-ttu-id="f540f-196">**Knooppunt en de meeste bestandsshare**.</span><span class="sxs-lookup"><span data-stu-id="f540f-196">**Node and File Share Majority**.</span></span> <span data-ttu-id="f540f-197">Elk knooppunt plus een aangewezen bestandsshare (een bestandssharewitness) die Hallo beheerder maakt kunt stemmen, ongeacht of Hallo knooppunten en bestandsshare beschikbaar zijn en bij communicatie.</span><span class="sxs-lookup"><span data-stu-id="f540f-197">Each node plus a designated file share (a file share witness) that hello administrator creates can vote, regardless of whether hello nodes and file share are available and in communication.</span></span> <span data-ttu-id="f540f-198">Hallo cluster werkt alleen met een meerderheid van Hallo stemmen, dat wil zeggen, met meer dan de helft Hallo stemmen.</span><span class="sxs-lookup"><span data-stu-id="f540f-198">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="f540f-199">Deze modus is wel zinvol in een clusteromgeving met een even aantal knooppunten.</span><span class="sxs-lookup"><span data-stu-id="f540f-199">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="f540f-200">Het is vergelijkbaar toohello knooppunt en schijfmeerderheid modus, maar een witness-bestandsshare wordt gebruikt in plaats van een witness-schijf.</span><span class="sxs-lookup"><span data-stu-id="f540f-200">It's similar toohello Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="f540f-201">Deze modus is eenvoudig tooimplement, maar als het Hallo-bestandsshare zelf is niet maximaal beschikbaar, het mogelijk een potentieel risico.</span><span class="sxs-lookup"><span data-stu-id="f540f-201">This mode is easy tooimplement, but if hello file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="f540f-202">**Geen meerderheid: Alleen schijf**.</span><span class="sxs-lookup"><span data-stu-id="f540f-202">**No Majority: Disk Only**.</span></span> <span data-ttu-id="f540f-203">Hallo-cluster heeft quorum als één knooppunt beschikbaar en communicatie met een specifieke schijf in de clusteropslag Hallo is.</span><span class="sxs-lookup"><span data-stu-id="f540f-203">hello cluster has a quorum if one node is available and in communication with a specific disk in hello cluster storage.</span></span> <span data-ttu-id="f540f-204">Alleen Hallo knooppunten die ook in de communicatie met die schijf kunnen Hallo-cluster toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f540f-204">Only hello nodes that also are in communication with that disk can join hello cluster.</span></span> <span data-ttu-id="f540f-205">Het is raadzaam dat u deze modus niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f540f-205">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="f540f-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a>Windows Serverfailover Clustering van on-premises</span><span class="sxs-lookup"><span data-stu-id="f540f-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="f540f-207">Afbeelding 1 ziet u een cluster met twee knooppunten.</span><span class="sxs-lookup"><span data-stu-id="f540f-207">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="f540f-208">Als hello netwerkverbinding tussen de knooppunten Hallo mislukt en beide knooppunten blijven en wordt uitgevoerd, een quorum schijf of bestandsshare bepaalt welk knooppunt blijft tooprovide Hallo cluster toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="f540f-208">If hello network connection between hello nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue tooprovide hello cluster's applications and services.</span></span> <span data-ttu-id="f540f-209">Hallo-knooppunt dat toegang toohello quorumschijf of de bestandsshare is Hallo-knooppunt dat ervoor zorgt dat services kunnen blijven.</span><span class="sxs-lookup"><span data-stu-id="f540f-209">hello node that has access toohello quorum disk or file share is hello node that ensures that services continue.</span></span>

<span data-ttu-id="f540f-210">Omdat in dit voorbeeld een cluster met twee knooppunten wordt, gebruiken we Hallo knooppunt en bestandssharemeerderheid quorum-modus.</span><span class="sxs-lookup"><span data-stu-id="f540f-210">Because this example uses a two-node cluster, we use hello Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="f540f-211">Hallo knooppunt en schijfmeerderheid is ook een geldige optie.</span><span class="sxs-lookup"><span data-stu-id="f540f-211">hello Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="f540f-212">U wordt aangeraden dat u een quorumschijf in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f540f-212">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="f540f-213">U kunt system technologie toomake van netwerk- en deze maximaal beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="f540f-213">You can use network and storage system technology toomake it highly available.</span></span>

![Afbeelding 1: Voorbeeld van een configuratie voor Windows Server Failover Clustering voor SAP ASC's / SCS in Azure][sap-ha-guide-figure-1000]

<span data-ttu-id="f540f-215">_**Afbeelding 1:** voorbeeld van een configuratie voor Windows Server Failover Clustering voor SAP ASC's / SCS in Azure_</span><span class="sxs-lookup"><span data-stu-id="f540f-215">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="f540f-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a>Gedeelde opslag</span><span class="sxs-lookup"><span data-stu-id="f540f-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="f540f-217">Afbeelding 1 wordt ook een cluster met twee knooppunten gedeelde opslag.</span><span class="sxs-lookup"><span data-stu-id="f540f-217">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="f540f-218">Alle knooppunten in cluster Hallo detecteren in een cluster van de gedeelde opslag lokale gedeelde opslag.</span><span class="sxs-lookup"><span data-stu-id="f540f-218">In an on-premises shared storage cluster, all nodes in hello cluster detect shared storage.</span></span> <span data-ttu-id="f540f-219">Een vergrendelingsfout mechanisme beschermt Hallo gegevens tegen beschadiging.</span><span class="sxs-lookup"><span data-stu-id="f540f-219">A locking mechanism protects hello data from corruption.</span></span> <span data-ttu-id="f540f-220">Alle knooppunten kunnen detecteren als een ander knooppunt mislukt.</span><span class="sxs-lookup"><span data-stu-id="f540f-220">All nodes can detect if another node fails.</span></span> <span data-ttu-id="f540f-221">Als een knooppunt is mislukt, wordt het resterende knooppunt hello wordt eigenaar van opslagbronnen Hallo en zorgt ervoor Hallo beschikbaarheid van services.</span><span class="sxs-lookup"><span data-stu-id="f540f-221">If one node fails, hello remaining node takes ownership of hello storage resources and ensures hello availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="f540f-222">U hoeft geen gedeelde schijven voor hoge beschikbaarheid bij sommige toepassingen DBMS zoals met SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f540f-222">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="f540f-223">SQL Server Always On repliceert DBMS gegevens en logboekbestanden bestanden van de lokale schijf Hallo van één cluster knooppunt toohello lokale schijf van een ander clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="f540f-223">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="f540f-224">Configuratie van het cluster Windows hello hoeft in dat geval niet een gedeelde schijf.</span><span class="sxs-lookup"><span data-stu-id="f540f-224">In that case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="f540f-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a>Netwerk- en naamomzetting</span><span class="sxs-lookup"><span data-stu-id="f540f-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="f540f-226">Clientcomputers bereiken Hallo-cluster via een virtueel IP-adres en de naam van een virtuele host op die Hallo DNS-server biedt.</span><span class="sxs-lookup"><span data-stu-id="f540f-226">Client computers reach hello cluster over a virtual IP address and a virtual host name that hello DNS server provides.</span></span> <span data-ttu-id="f540f-227">Hallo on-premises knooppunten en Hallo DNS-server kan meerdere IP-adressen verwerken.</span><span class="sxs-lookup"><span data-stu-id="f540f-227">hello on-premises nodes and hello DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="f540f-228">In een typische installatie gebruikt u twee of meer netwerkverbindingen:</span><span class="sxs-lookup"><span data-stu-id="f540f-228">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="f540f-229">Een speciale verbinding toohello opslag</span><span class="sxs-lookup"><span data-stu-id="f540f-229">A dedicated connection toohello storage</span></span>
* <span data-ttu-id="f540f-230">Een cluster interne netwerkverbinding voor Hallo heartbeat</span><span class="sxs-lookup"><span data-stu-id="f540f-230">A cluster-internal network connection for hello heartbeat</span></span>
* <span data-ttu-id="f540f-231">Een openbaar netwerk dat clients tooconnect toohello cluster gebruiken</span><span class="sxs-lookup"><span data-stu-id="f540f-231">A public network that clients use tooconnect toohello cluster</span></span>

## <span data-ttu-id="f540f-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a>Windows Serverfailover Clustering in Azure</span><span class="sxs-lookup"><span data-stu-id="f540f-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="f540f-233">Vergeleken toobare metal of privécloud implementaties, Azure Virtual Machines vereist extra stappen tooconfigure Windows Server Failover Clustering.</span><span class="sxs-lookup"><span data-stu-id="f540f-233">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="f540f-234">Als u een gedeelde clusterschijf bouwen, moet u de namen van verschillende IP-adressen en virtuele host tooset voor Hallo SAP ASC's / SCS exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f540f-234">When you build a shared cluster disk, you need tooset several IP addresses and virtual host names for hello SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="f540f-235">In dit artikel hoofdconcepten bespreken we en Hallo extra stappen vereist toobuild een SAP-services met hoge beschikbaarheid centrale cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="f540f-235">In this article, we discuss key concepts and hello additional steps required toobuild an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="f540f-236">We zien u hoe tooset up Hallo hulpprogramma van derden SIOS DataKeeper en hoe tooconfigure hello Azure interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="f540f-236">We show you how tooset up hello third-party tool SIOS DataKeeper, and how tooconfigure hello Azure internal load balancer.</span></span> <span data-ttu-id="f540f-237">U kunt deze hulpprogramma's voor toocreate een failover-cluster van Windows gebruiken met een bestandsshare-witness in Azure.</span><span class="sxs-lookup"><span data-stu-id="f540f-237">You can use these tools toocreate a Windows failover cluster with a file share witness in Azure.</span></span>

![Afbeelding 2: Windows Server Failover Clustering configuratie in Azure zonder een gedeelde schijf][sap-ha-guide-figure-1001]

<span data-ttu-id="f540f-239">_**Afbeelding 2:** configuratie Windows Server Failover Clustering in Azure zonder een gedeelde schijf_</span><span class="sxs-lookup"><span data-stu-id="f540f-239">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="f540f-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a>Gedeelde schijf in Azure met SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="f540f-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="f540f-241">U moet gedeelde opslag voor een hoge beschikbaarheid SAP ASC's / SCS-exemplaar in de cluster.</span><span class="sxs-lookup"><span data-stu-id="f540f-241">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="f540f-242">Zoals van September 2016 Azure niet gedeelde opslag die biedt kunt u toocreate een cluster met gedeelde opslag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f540f-242">As of September 2016, Azure doesn't offer shared storage that you can use toocreate a shared storage cluster.</span></span> <span data-ttu-id="f540f-243">U kunt software van derden SIOS DataKeeper Cluster Edition toocreate een gespiegelde opslagruimte die gedeelde clusteropslag simuleert.</span><span class="sxs-lookup"><span data-stu-id="f540f-243">You can use third-party software SIOS DataKeeper Cluster Edition toocreate a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="f540f-244">Hallo SIOS oplossing biedt realtime synchrone gegevensreplicatie.</span><span class="sxs-lookup"><span data-stu-id="f540f-244">hello SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="f540f-245">Dit is hoe u een gedeelde schijfbron voor een cluster kunt maken:</span><span class="sxs-lookup"><span data-stu-id="f540f-245">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="f540f-246">Koppel een extra schijf tooeach van Hallo virtuele machines (VM's) in de configuratie van een Windows-cluster.</span><span class="sxs-lookup"><span data-stu-id="f540f-246">Attach an additional disk tooeach of hello virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="f540f-247">SIOS DataKeeper Cluster Edition wordt uitgevoerd op beide knooppunten van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f540f-247">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="f540f-248">SIOS DataKeeper Cluster Edition configureren zodat deze overeenkomt met inhoud van Hallo extra schijf die is gekoppeld volume van Hallo bron virtuele machine toohello extra schijf die is gekoppeld volume van de virtuele doelmachine Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="f540f-248">Configure SIOS DataKeeper Cluster Edition so that it mirrors hello content of hello additional disk attached volume from hello source virtual machine toohello additional disk attached volume of hello target virtual machine.</span></span> <span data-ttu-id="f540f-249">SIOS DataKeeper isoleert Hallo bron en doel lokale volumes en geeft ze tooWindows Server Failover Clustering als één gedeelde schijf.</span><span class="sxs-lookup"><span data-stu-id="f540f-249">SIOS DataKeeper abstracts hello source and target local volumes, and then presents them tooWindows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="f540f-250">Vindt u meer informatie over [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="f540f-250">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Afbeelding 3: Configuratie van Windows Server Failover Clustering in Azure met SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="f540f-252">_**Afbeelding 3:** configuratie Windows Server Failover Clustering in Azure met SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="f540f-252">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="f540f-253">U hoeft geen gedeelde schijven voor hoge beschikbaarheid met sommige DBMS-producten, zoals SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f540f-253">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="f540f-254">SQL Server Always On repliceert DBMS gegevens en logboekbestanden bestanden van de lokale schijf Hallo van één cluster knooppunt toohello lokale schijf van een ander clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="f540f-254">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="f540f-255">Hallo Windows cluster-configuratie nodig niet in dit geval een gedeelde schijf.</span><span class="sxs-lookup"><span data-stu-id="f540f-255">In this case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="f540f-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a>Naamomzetting in Azure</span><span class="sxs-lookup"><span data-stu-id="f540f-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="f540f-257">Hello Azure-cloud-platform biedt geen Hallo optie tooconfigure virtuele IP-adressen, zoals zwevend IP-adressen te bieden.</span><span class="sxs-lookup"><span data-stu-id="f540f-257">hello Azure cloud platform doesn't offer hello option tooconfigure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="f540f-258">U moet een alternatieve oplossing tooset van een virtueel IP-adres tooreach Hallo clusterbron in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="f540f-258">You need an alternative solution tooset up a virtual IP address tooreach hello cluster resource in hello cloud.</span></span>
<span data-ttu-id="f540f-259">Azure heeft een interne load balancer in hello Azure Load Balancer-service.</span><span class="sxs-lookup"><span data-stu-id="f540f-259">Azure has an internal load balancer in hello Azure Load Balancer service.</span></span> <span data-ttu-id="f540f-260">Met Hallo interne load balancer bereiken clients Hallo cluster via Hallo cluster virtuele IP-adres.</span><span class="sxs-lookup"><span data-stu-id="f540f-260">With hello internal load balancer, clients reach hello cluster over hello cluster virtual IP address.</span></span>
<span data-ttu-id="f540f-261">U moet toodeploy Hallo interne load balancer in Hallo resourcegroep die de clusterknooppunten Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="f540f-261">You need toodeploy hello internal load balancer in hello resource group that contains hello cluster nodes.</span></span> <span data-ttu-id="f540f-262">Configureer vervolgens alle benodigde poorttoewijzing regels met Hallo test poorten van Hallo interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="f540f-262">Then, configure all necessary port forwarding rules with hello probe ports of hello internal load balancer.</span></span>
<span data-ttu-id="f540f-263">Hallo-clients kunnen verbinding maken via de naam van de virtuele host Hallo.</span><span class="sxs-lookup"><span data-stu-id="f540f-263">hello clients can connect via hello virtual host name.</span></span> <span data-ttu-id="f540f-264">Hallo DNS-server wordt omgezet Hallo cluster IP-adres en Hallo interne load balancer-ingangen poorttoewijzing toohello actieve knooppunt van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f540f-264">hello DNS server resolves hello cluster IP address, and hello internal load balancer handles port forwarding toohello active node of hello cluster.</span></span>

## <span data-ttu-id="f540f-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a>SAP NetWeaver hoge beschikbaarheid in een Azure-infrastructuur-as-a-Service (IaaS)</span><span class="sxs-lookup"><span data-stu-id="f540f-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="f540f-266">tooachieve SAP-toepassing hoge beschikbaarheid, zoals SAP-softwareonderdelen, moet u tooprotect Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="f540f-266">tooachieve SAP application high availability, such as for SAP software components, you need tooprotect hello following components:</span></span>

* <span data-ttu-id="f540f-267">SAP Application Server-exemplaar</span><span class="sxs-lookup"><span data-stu-id="f540f-267">SAP Application Server instance</span></span>
* <span data-ttu-id="f540f-268">SAP ASC's / SCS-exemplaar</span><span class="sxs-lookup"><span data-stu-id="f540f-268">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="f540f-269">DBMS-server</span><span class="sxs-lookup"><span data-stu-id="f540f-269">DBMS server</span></span>

<span data-ttu-id="f540f-270">Zie voor meer informatie over het beveiligen van SAP-onderdelen in scenario's voor hoge beschikbaarheid [Azure Virtual Machines planning en implementatie voor SAP NetWeaver][planning-guide-11].</span><span class="sxs-lookup"><span data-stu-id="f540f-270">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-11].</span></span>

### <span data-ttu-id="f540f-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a>Hoge beschikbaarheid SAP-toepassingsserver</span><span class="sxs-lookup"><span data-stu-id="f540f-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="f540f-272">Normaal gesproken hoeft u niet een bepaalde oplossing voor hoge beschikbaarheid voor Hallo SAP-toepassingsserver en dialoogvenster exemplaren.</span><span class="sxs-lookup"><span data-stu-id="f540f-272">You usually don't need a specific high-availability solution for hello SAP Application Server and dialog instances.</span></span> <span data-ttu-id="f540f-273">Een maximale beschikbaarheid realiseren door redundantie en configureert u meerdere exemplaren van het dialoogvenster in verschillende exemplaren van Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="f540f-273">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="f540f-274">U hebt ten minste twee SAP exemplaren van een toepassing in twee exemplaren van Azure Virtual Machines geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f540f-274">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Afbeelding 4: Hoge beschikbaarheid SAP-toepassingsserver][sap-ha-guide-figure-2000]

<span data-ttu-id="f540f-276">_**Afbeelding 4:** hoge beschikbaarheid SAP-toepassingsserver_</span><span class="sxs-lookup"><span data-stu-id="f540f-276">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="f540f-277">U moet alle virtuele machines dat SAP-toepassingsserver instanties van hosts in dezelfde Azure beschikbaarheidsset Hallo plaatsen.</span><span class="sxs-lookup"><span data-stu-id="f540f-277">You must place all virtual machines that host SAP Application Server instances in hello same Azure availability set.</span></span> <span data-ttu-id="f540f-278">Een Azure beschikbaarheidsset zorgt ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="f540f-278">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="f540f-279">Alle virtuele machines deel uitmaken van Hallo dezelfde upgradedomein.</span><span class="sxs-lookup"><span data-stu-id="f540f-279">All virtual machines are part of hello same upgrade domain.</span></span> <span data-ttu-id="f540f-280">Een upgradedomein bijvoorbeeld zorgt ervoor dat Hallo virtuele machines zijn niet op Hallo bijgewerkt hetzelfde moment tijdens gepland onderhoud uitval.</span><span class="sxs-lookup"><span data-stu-id="f540f-280">An upgrade domain, for example, makes sure that hello virtual machines aren't updated at hello same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="f540f-281">Alle virtuele machines deel uitmaken van Hallo hetzelfde foutdomein.</span><span class="sxs-lookup"><span data-stu-id="f540f-281">All virtual machines are part of hello same fault domain.</span></span> <span data-ttu-id="f540f-282">Een foutdomein bijvoorbeeld ervoor zorgt dat virtuele machines zodat er geen storingspunt is van invloed op Hallo beschikbaarheid van alle virtuele machines zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f540f-282">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects hello availability of all virtual machines.</span></span>

<span data-ttu-id="f540f-283">Meer informatie over het te[Hallo beschikbaarheid van virtuele machines beheren][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="f540f-283">Learn more about how too[manage hello availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="f540f-284">Alleen niet-beheerde schijf: omdat hello Azure storage-account een potentieel storingspunt is, is het belangrijk toohave ten minste twee Azure storage-accounts, waarbij ten minste twee virtuele machines worden gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="f540f-284">Unmanaged disk only: Because hello Azure storage account is a potential single point of failure, it's important toohave at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="f540f-285">In een ideaal setup wordt Hallo schijven van elke virtuele machine die wordt uitgevoerd een SAP-dialoogvenster-exemplaar geïmplementeerd in een ander opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="f540f-285">In an ideal setup, hello disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="f540f-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a>Hoge beschikbaarheid SAP ASC's / SCS exemplaar</span><span class="sxs-lookup"><span data-stu-id="f540f-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="f540f-287">Afbeelding 5 is een voorbeeld van een exemplaar van de SAP ASC's / SCS hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="f540f-287">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Afbeelding 5: Hoge beschikbaarheid SAP ASC's / SCS exemplaar][sap-ha-guide-figure-2001]

<span data-ttu-id="f540f-289">_**Afbeelding 5:** hoge beschikbaarheid SAP ASC's / SCS-exemplaar_</span><span class="sxs-lookup"><span data-stu-id="f540f-289">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="f540f-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a>SAP ASC's / SCS exemplaar hoge beschikbaarheid met Windows Server Failover Clustering in Azure</span><span class="sxs-lookup"><span data-stu-id="f540f-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="f540f-291">Vergeleken toobare metal of privécloud implementaties, Azure Virtual Machines vereist extra stappen tooconfigure Windows Server Failover Clustering.</span><span class="sxs-lookup"><span data-stu-id="f540f-291">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="f540f-292">toobuild een failover-cluster van Windows, moet u een gedeelde clusterschijf, verschillende IP-adressen, verschillende namen van de virtuele host en een Azure interne load balancer voor een exemplaar SAP ASC's / SCS clustering.</span><span class="sxs-lookup"><span data-stu-id="f540f-292">toobuild a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="f540f-293">Dit bespreken we in meer detail verderop in Hallo artikel.</span><span class="sxs-lookup"><span data-stu-id="f540f-293">We discuss this in more detail later in hello article.</span></span>

![Afbeelding 6: Windows Server Failover Clustering voor een SAP ASC's / SCS-configuratie in Azure met behulp van SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="f540f-295">_**Afbeelding 6:** Windows Server Failover Clustering voor een SAP ASC's / SCS-configuratie in Azure met SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="f540f-295">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="f540f-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Hoge beschikbaarheid DBMS exemplaar</span><span class="sxs-lookup"><span data-stu-id="f540f-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="f540f-297">Hallo DBMS is ook een aanspreekpunt in een SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="f540f-297">hello DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="f540f-298">U moet tooprotect deze met behulp van een oplossing voor hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="f540f-298">You need tooprotect it by using a high-availability solution.</span></span> <span data-ttu-id="f540f-299">Afbeelding 7 toont een hoge beschikbaarheid SQL Server Always On oplossing in Azure, met Windows Server Failover Clustering en hello Azure interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="f540f-299">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and hello Azure internal load balancer.</span></span> <span data-ttu-id="f540f-300">SQL Server Always On repliceert DBMS gegevens en logboekbestanden bestanden met behulp van een eigen DBMS-replicatie.</span><span class="sxs-lookup"><span data-stu-id="f540f-300">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="f540f-301">In dit geval nodig u niet clusteren gedeelde schijven die vereenvoudigt Hallo volledige installatie.</span><span class="sxs-lookup"><span data-stu-id="f540f-301">In this case, you don't need cluster shared disks, which simplifies hello entire setup.</span></span>

![Afbeelding 7: Voorbeeld van een hoge beschikbaarheid SAP DBMS, met SQL Server Always On][sap-ha-guide-figure-2003]

<span data-ttu-id="f540f-303">_**Afbeelding 7:** voorbeeld van een hoge beschikbaarheid SAP DBMS, met SQL Server Always On_</span><span class="sxs-lookup"><span data-stu-id="f540f-303">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="f540f-304">Zie voor meer informatie over SQL Server in Azure met Azure Resource Manager-implementatiemodel Hallo clustering deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="f540f-304">For more information about clustering SQL Server in Azure by using hello Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="f540f-305">[AlwaysOn-beschikbaarheidsgroep in Azure Virtual Machines handmatig configureren met behulp van Resource Manager] [virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="f540f-305">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="f540f-306">[Een Azure interne load balancer voor een AlwaysOn-beschikbaarheidsgroep configureren in Azure] [virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="f540f-306">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="f540f-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a>End-to-end hoge beschikbaarheid implementatiescenario 's</span><span class="sxs-lookup"><span data-stu-id="f540f-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="f540f-308">Implementatiescenario met architectuur sjabloon 1</span><span class="sxs-lookup"><span data-stu-id="f540f-308">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="f540f-309">Afbeelding 8 toont een voorbeeld van een SAP NetWeaver hoge beschikbaarheid-architectuur in Azure voor **één** SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="f540f-309">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="f540f-310">Dit scenario is als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="f540f-310">This scenario is set up as follows:</span></span>

- <span data-ttu-id="f540f-311">Een speciale cluster wordt gebruikt voor Hallo SAP ASC's / SCS exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f540f-311">One dedicated cluster is used for hello SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="f540f-312">Een speciale cluster wordt gebruikt voor Hallo DBMS exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f540f-312">One dedicated cluster is used for hello DBMS instance.</span></span>
- <span data-ttu-id="f540f-313">SAP Application Server-exemplaren zijn in hun eigen toegewezen virtuele machines geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f540f-313">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Afbeelding 8: Hoge beschikbaarheid architectuur sjabloon 1, met speciale cluster voor ASC's / SCS en DBMS SAP][sap-ha-guide-figure-2004]

<span data-ttu-id="f540f-315">_**Afbeelding 8:** SAP-architectuur sjabloon 1 hoge beschikbaarheid, speciale clusters voor ASC's / SCS en DBMS_</span><span class="sxs-lookup"><span data-stu-id="f540f-315">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="f540f-316">Implementatiescenario met behulp van architectuur sjabloon 2</span><span class="sxs-lookup"><span data-stu-id="f540f-316">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="f540f-317">Afbeelding 9 toont een voorbeeld van een SAP NetWeaver hoge beschikbaarheid-architectuur in Azure voor **één** SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="f540f-317">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="f540f-318">Dit scenario is als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="f540f-318">This scenario is set up as follows:</span></span>

- <span data-ttu-id="f540f-319">Een speciale cluster wordt gebruikt voor **beide** Hallo SAP ASC's / SCS-instantie en Hallo DBMS.</span><span class="sxs-lookup"><span data-stu-id="f540f-319">One dedicated cluster is used for **both** hello SAP ASCS/SCS instance and hello DBMS.</span></span>
- <span data-ttu-id="f540f-320">SAP Application Server-exemplaren zijn in de eigen toegewezen virtuele machines geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f540f-320">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Afbeelding 9: Hoge beschikbaarheid architectuur sjabloon 2, met een speciale voor ASC's / SCS als een cluster toegewezen voor DBMS SAP][sap-ha-guide-figure-2005]

<span data-ttu-id="f540f-322">_**Afbeelding 9:** hoge beschikbaarheid architectuur sjabloon 2, met een speciale voor ASC's / SCS als een cluster toegewezen voor DBMS SAP_</span><span class="sxs-lookup"><span data-stu-id="f540f-322">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="f540f-323">Implementatiescenario met architectuur sjabloon 3</span><span class="sxs-lookup"><span data-stu-id="f540f-323">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="f540f-324">Afbeelding 10 toont een voorbeeld van een SAP NetWeaver hoge beschikbaarheid-architectuur in Azure voor **twee** SAP-systemen, met &lt;SID1&gt; en &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="f540f-324">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="f540f-325">Dit scenario is als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="f540f-325">This scenario is set up as follows:</span></span>

- <span data-ttu-id="f540f-326">Een speciale cluster wordt gebruikt voor **beide** Hallo SAP ASC's / SCS SID1 exemplaar *en* Hallo SAP ASC's / SCS SID2 exemplaar (één cluster).</span><span class="sxs-lookup"><span data-stu-id="f540f-326">One dedicated cluster is used for **both** hello SAP ASCS/SCS SID1 instance *and* hello SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="f540f-327">Een speciale cluster wordt gebruikt voor DBMS SID1 en een ander toegewezen cluster wordt gebruikt voor DBMS SID2 (twee clusters).</span><span class="sxs-lookup"><span data-stu-id="f540f-327">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="f540f-328">SAP Application Server-exemplaren voor Hallo SAP-systeem SID1 hebben hun eigen toegewezen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f540f-328">SAP Application Server instances for hello SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="f540f-329">SAP Application Server-exemplaren voor Hallo SAP-systeem SID2 hebben hun eigen toegewezen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f540f-329">SAP Application Server instances for hello SAP system SID2 have their own dedicated VMs.</span></span>

![Afbeelding 10: SAP hoge beschikbaarheid architectuur sjabloon 3, met een cluster toegewezen voor verschillende ASC's / SCS-exemplaren][sap-ha-guide-figure-6003]

<span data-ttu-id="f540f-331">_**Afbeelding 10:** SAP-hoge beschikbaarheid architectuur sjabloon 3, met een cluster toegewezen voor verschillende ASC's / SCS-exemplaren_</span><span class="sxs-lookup"><span data-stu-id="f540f-331">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="f540f-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Hallo-infrastructuur voorbereiden</span><span class="sxs-lookup"><span data-stu-id="f540f-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare hello infrastructure</span></span>

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a><span data-ttu-id="f540f-333">Hallo-infrastructuur voorbereiden voor architecturale sjabloon 1</span><span class="sxs-lookup"><span data-stu-id="f540f-333">Prepare hello infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="f540f-334">Azure Resource Manager-sjablonen voor SAP vereenvoudigen implementatie van de vereiste resources.</span><span class="sxs-lookup"><span data-stu-id="f540f-334">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="f540f-335">Hallo drie lagen sjablonen in Azure Resource Manager ondersteunen ook scenario's met hoge beschikbaarheid, zoals in de architectuur sjabloon 1, met twee clusters.</span><span class="sxs-lookup"><span data-stu-id="f540f-335">hello three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="f540f-336">Elk cluster is een SAP storingspunt voor SAP ASC's / SCS en DBMS.</span><span class="sxs-lookup"><span data-stu-id="f540f-336">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="f540f-337">Dit is waarop u Azure Resource Manager-sjablonen kunt ophalen voor Hallo voorbeeldscenario die in dit artikel worden beschreven:</span><span class="sxs-lookup"><span data-stu-id="f540f-337">Here's where you can get Azure Resource Manager templates for hello example scenario we describe in this article:</span></span>

* [<span data-ttu-id="f540f-338">Azure Marketplace-installatiekopie</span><span class="sxs-lookup"><span data-stu-id="f540f-338">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="f540f-339">Azure Marketplace-installatiekopie met schijven beheerd</span><span class="sxs-lookup"><span data-stu-id="f540f-339">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [<span data-ttu-id="f540f-340">Aangepaste installatiekopie</span><span class="sxs-lookup"><span data-stu-id="f540f-340">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [<span data-ttu-id="f540f-341">Aangepaste installatiekopie met schijven beheerd</span><span class="sxs-lookup"><span data-stu-id="f540f-341">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

<span data-ttu-id="f540f-342">tooprepare hello infrastructuur voor architecturale sjabloon 1:</span><span class="sxs-lookup"><span data-stu-id="f540f-342">tooprepare hello infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="f540f-343">In de Azure-portal op Hallo Hallo **Parameters** blade in Hallo **SYSTEMAVAILABILITY** de optie **HA**.</span><span class="sxs-lookup"><span data-stu-id="f540f-343">In hello Azure portal, on hello **Parameters** blade, in hello **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Afbeelding 11: Stel SAP-parameters voor hoge beschikbaarheid Azure Resource Manager][sap-ha-guide-figure-3000]

<span data-ttu-id="f540f-345">_**Afbeelding 11:** ingesteld SAP-parameters voor hoge beschikbaarheid Azure Resource Manager_</span><span class="sxs-lookup"><span data-stu-id="f540f-345">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="f540f-346">Hallo-sjablonen maken:</span><span class="sxs-lookup"><span data-stu-id="f540f-346">hello templates create:</span></span>

  * <span data-ttu-id="f540f-347">**Virtuele machines**:</span><span class="sxs-lookup"><span data-stu-id="f540f-347">**Virtual machines**:</span></span>
    * <span data-ttu-id="f540f-348">SAP-toepassingsserver virtuele machines: <*SAPSystemSID*> - di - <*getal*></span><span class="sxs-lookup"><span data-stu-id="f540f-348">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="f540f-349">ASC's / SCS cluster virtuele machines: <*SAPSystemSID*> - ASC - 's <*getal*></span><span class="sxs-lookup"><span data-stu-id="f540f-349">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="f540f-350">DBMS-cluster: <*SAPSystemSID*> - db - <*getal*></span><span class="sxs-lookup"><span data-stu-id="f540f-350">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="f540f-351">**Netwerkkaarten voor alle virtuele machines met bijbehorende IP-adressen**:</span><span class="sxs-lookup"><span data-stu-id="f540f-351">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="f540f-352"><*SAPSystemSID*> - nic - di - <*getal*></span><span class="sxs-lookup"><span data-stu-id="f540f-352"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="f540f-353"><*SAPSystemSID*> - nic - ASC's - <*getal*></span><span class="sxs-lookup"><span data-stu-id="f540f-353"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="f540f-354"><*SAPSystemSID*> - nic - db - <*getal*></span><span class="sxs-lookup"><span data-stu-id="f540f-354"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="f540f-355">**Azure storage-accounts (alleen niet-beheerde schijven)**</span><span class="sxs-lookup"><span data-stu-id="f540f-355">**Azure storage accounts (unmanaged disks only)**</span></span>

  * <span data-ttu-id="f540f-356">**Beschikbaarheidsgroepen** voor:</span><span class="sxs-lookup"><span data-stu-id="f540f-356">**Availability groups** for:</span></span>
    * <span data-ttu-id="f540f-357">SAP-toepassingsserver virtuele machines: <*SAPSystemSID*> - avset - di</span><span class="sxs-lookup"><span data-stu-id="f540f-357">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="f540f-358">SAP ASC's / SCS cluster virtuele machines: <*SAPSystemSID*> - avset - ASC's</span><span class="sxs-lookup"><span data-stu-id="f540f-358">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="f540f-359">DBMS cluster virtuele machines: <*SAPSystemSID*> - avset - db</span><span class="sxs-lookup"><span data-stu-id="f540f-359">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="f540f-360">**Azure interne load balancer**:</span><span class="sxs-lookup"><span data-stu-id="f540f-360">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="f540f-361">Met alle poorten voor Hallo ASC's / SCS exemplaar en IP-adres <*SAPSystemSID*> - lb - ASC's</span><span class="sxs-lookup"><span data-stu-id="f540f-361">With all ports for hello ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="f540f-362">Met alle poorten voor de SQL Server-DBMS en IP-adres Hallo <*SAPSystemSID*> - lb - db</span><span class="sxs-lookup"><span data-stu-id="f540f-362">With all ports for hello SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="f540f-363">**Netwerkbeveiligingsgroep**: <*SAPSystemSID*> - nsg - ASC's-0</span><span class="sxs-lookup"><span data-stu-id="f540f-363">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="f540f-364">Met een open externe Remote Desktop Protocol (RDP)-poort toohello <*SAPSystemSID*> - ASC's - 0 virtuele machine</span><span class="sxs-lookup"><span data-stu-id="f540f-364">With an open external Remote Desktop Protocol (RDP) port toohello <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="f540f-365">Alle IP-adressen van Hallo netwerkkaarten en Azure interne load balancers zijn **dynamische** standaard.</span><span class="sxs-lookup"><span data-stu-id="f540f-365">All IP addresses of hello network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="f540f-366">Ze ook wijzigen**statische** IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="f540f-366">Change them too**static** IP addresses.</span></span> <span data-ttu-id="f540f-367">We beschrijven hoe toodo dit later op Hallo artikel.</span><span class="sxs-lookup"><span data-stu-id="f540f-367">We describe how toodo this later in hello article.</span></span>
>
>

### <span data-ttu-id="f540f-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Virtuele machines implementeren met het bedrijfsnetwerk connectiviteit (cross-premises) toouse in productie</span><span class="sxs-lookup"><span data-stu-id="f540f-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) toouse in production</span></span>
<span data-ttu-id="f540f-369">Voor productiesystemen SAP, Azure virtuele machines implementeren met [bedrijfsnetwerk connectiviteit (cross-premises)] [ planning-guide-2.2] met behulp van Azure Site-naar-Site VPN- of Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f540f-369">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="f540f-370">U kunt uw Azure Virtual Network-exemplaar gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f540f-370">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="f540f-371">Hallo virtueel netwerk en subnet zijn al gemaakt en voorbereid.</span><span class="sxs-lookup"><span data-stu-id="f540f-371">hello virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="f540f-372">In de Azure-portal op Hallo Hallo **Parameters** blade in Hallo **NEWOREXISTINGSUBNET** de optie **bestaande**.</span><span class="sxs-lookup"><span data-stu-id="f540f-372">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="f540f-373">In Hallo **SUBNETID** Voeg Hallo volledige tekenreeks van het voorbereide Azure netwerk SubnetID waar u van plan toodeploy uw virtuele machines in Azure bent.</span><span class="sxs-lookup"><span data-stu-id="f540f-373">In hello **SUBNETID** box, add hello full string of your prepared Azure network SubnetID where you plan toodeploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="f540f-374">een lijst met alle Azure-netwerksubnetten tooget deze PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f540f-374">tooget a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="f540f-375">Hallo **ID** veld bevat Hallo **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="f540f-375">hello **ID** field shows hello **SUBNETID**.</span></span>
4. <span data-ttu-id="f540f-376">een lijst met alle tooget **SUBNETID** waarden, deze PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f540f-376">tooget a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="f540f-377">Hallo **SUBNETID** ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="f540f-377">hello **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="f540f-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a>Alleen in de cloud SAP-exemplaren voor test- en demo implementeren</span><span class="sxs-lookup"><span data-stu-id="f540f-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="f540f-379">U kunt uw SAP-systeem voor hoge beschikbaarheid in een cloudconfiguratie implementatiemodel implementeren.</span><span class="sxs-lookup"><span data-stu-id="f540f-379">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="f540f-380">Dit type implementatie is vooral nuttig voor demo en test gebruiksvoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="f540f-380">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="f540f-381">Het niet geschikt voor gebruiksvoorbeelden voor productie.</span><span class="sxs-lookup"><span data-stu-id="f540f-381">It's not suited for production use cases.</span></span>

- <span data-ttu-id="f540f-382">In de Azure-portal op Hallo Hallo **Parameters** blade in Hallo **NEWOREXISTINGSUBNET** de optie **nieuwe**.</span><span class="sxs-lookup"><span data-stu-id="f540f-382">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="f540f-383">Hallo laat **SUBNETID** veld leeg.</span><span class="sxs-lookup"><span data-stu-id="f540f-383">Leave hello **SUBNETID** field empty.</span></span>

  <span data-ttu-id="f540f-384">Hallo SAP Azure Resource Manager sjabloon automatisch maakt Hallo virtuele Azure-netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="f540f-384">hello SAP Azure Resource Manager template automatically creates hello Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="f540f-385">U moet ook toodeploy ten minste één virtuele machine specifiek zijn voor Active Directory en DNS-server in Hallo hetzelfde exemplaar van Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="f540f-385">You also need toodeploy at least one dedicated virtual machine for Active Directory and DNS in hello same Azure Virtual Network instance.</span></span> <span data-ttu-id="f540f-386">Hallo-sjabloon maakt geen deze virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f540f-386">hello template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a><span data-ttu-id="f540f-387">Hallo-infrastructuur voorbereiden voor architecturale sjabloon 2</span><span class="sxs-lookup"><span data-stu-id="f540f-387">Prepare hello infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="f540f-388">U kunt deze Azure Resource Manager-sjabloon gebruiken voor toohelp SAP-implementatie van resources van de vereiste infrastructuur voor SAP architectuur sjabloon 2 vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="f540f-388">You can use this Azure Resource Manager template for SAP toohelp simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="f540f-389">Dit is waarop u Azure Resource Manager-sjablonen kunt ophalen voor deze implementatiescenario:</span><span class="sxs-lookup"><span data-stu-id="f540f-389">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="f540f-390">Azure Marketplace-installatiekopie</span><span class="sxs-lookup"><span data-stu-id="f540f-390">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="f540f-391">Azure Marketplace-installatiekopie met schijven beheerd</span><span class="sxs-lookup"><span data-stu-id="f540f-391">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [<span data-ttu-id="f540f-392">Aangepaste installatiekopie</span><span class="sxs-lookup"><span data-stu-id="f540f-392">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [<span data-ttu-id="f540f-393">Aangepaste installatiekopie met schijven beheerd</span><span class="sxs-lookup"><span data-stu-id="f540f-393">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a><span data-ttu-id="f540f-394">Hallo-infrastructuur voorbereiden voor architecturale sjabloon 3</span><span class="sxs-lookup"><span data-stu-id="f540f-394">Prepare hello infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="f540f-395">U kunt Hallo infrastructuur voorbereiden en configureren van SAP voor **multi-SID**.</span><span class="sxs-lookup"><span data-stu-id="f540f-395">You can prepare hello infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="f540f-396">U kunt bijvoorbeeld een extra exemplaar SAP ASC's / SCS in toevoegen een *bestaande* clusterconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="f540f-396">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="f540f-397">Zie voor meer informatie [configureren van een extra exemplaar SAP ASC's / SCS in een bestaand cluster configuratie toocreate een SAP multi-SID-configuratie in Azure Resource Manager][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="f540f-397">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration toocreate an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="f540f-398">Als u een nieuw cluster met meerdere SID toocreate wilt, kunt u Hallo multi-SID [Quick Start-sjablonen op GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="f540f-398">If you want toocreate a new multi-SID cluster, you can use hello multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="f540f-399">een nieuw cluster met meerdere SID toocreate, moet u toodeploy Hallo drie sjablonen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f540f-399">toocreate a new multi-SID cluster, you need toodeploy hello following three templates:</span></span>

* [<span data-ttu-id="f540f-400">ASC's / SCS-sjabloon</span><span class="sxs-lookup"><span data-stu-id="f540f-400">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="f540f-401">Database-sjabloon</span><span class="sxs-lookup"><span data-stu-id="f540f-401">Database template</span></span>](#database-template)
* [<span data-ttu-id="f540f-402">Toepassingssjabloon voor servers</span><span class="sxs-lookup"><span data-stu-id="f540f-402">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="f540f-403">Hallo hebben volgende secties meer informatie over het Hallo-sjablonen en moet u tooprovide in sjablonen Hallo Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="f540f-403">hello following sections have more details about hello templates and hello parameters you need tooprovide in hello templates.</span></span>

#### <span data-ttu-id="f540f-404"><a name="ASCS-SCS-template"></a>ASC's / SCS-sjabloon</span><span class="sxs-lookup"><span data-stu-id="f540f-404"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="f540f-405">Hallo ASC's / SCS sjabloon implementeert twee virtuele machines dat u een failover-cluster van Windows Server die als host fungeert voor meerdere exemplaren van ASC's / SCS toocreate kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f540f-405">hello ASCS/SCS template deploys two virtual machines that you can use toocreate a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="f540f-406">tooset van de sjabloon Hallo ASC's / SCS multi-SID in Hallo [ASC's / SCS multi-SID sjabloon] [ sap-templates-3-tier-multisid-xscs-marketplace-image] of [ASC's / SCS multi-SID-sjabloon met gebruik van schijven beheerd] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], voer waarden in voor Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="f540f-406">tooset up hello ASCS/SCS multi-SID template, in hello [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image] or [ASCS/SCS multi-SID template using Managed Disks][sap-templates-3-tier-multisid-xscs-marketplace-image-md], enter values for hello following parameters:</span></span>

  - <span data-ttu-id="f540f-407">**Resource-voorvoegsel**.</span><span class="sxs-lookup"><span data-stu-id="f540f-407">**Resource Prefix**.</span></span>  <span data-ttu-id="f540f-408">Hallo resource voorvoegsel, namelijk gebruikte tooprefix alle resources die zijn gemaakt tijdens de implementatie van Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f540f-408">Set hello resource prefix, which is used tooprefix all resources that are created during hello deployment.</span></span> <span data-ttu-id="f540f-409">Omdat Hallo bronnen geen deel van een SAP-systeem tooonly uitmaken, is Hallo-voorvoegsel van Hallo resource niet Hallo SID van een SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="f540f-409">Because hello resources do not belong tooonly one SAP system, hello prefix of hello resource is not hello SID of one SAP system.</span></span>  <span data-ttu-id="f540f-410">Hallo-voorvoegsel moet liggen tussen **drie tot zes tekens**.</span><span class="sxs-lookup"><span data-stu-id="f540f-410">hello prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="f540f-411">**Stack is Type**.</span><span class="sxs-lookup"><span data-stu-id="f540f-411">**Stack Type**.</span></span> <span data-ttu-id="f540f-412">Selecteer Hallo stack type Hallo SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="f540f-412">Select hello stack type of hello SAP system.</span></span> <span data-ttu-id="f540f-413">Afhankelijk van het type van de stack hello heeft Azure Load Balancer een (ABAP of alleen Java) of twee (ABAP + Java) privé IP-adressen per SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="f540f-413">Depending on hello stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="f540f-414">**Type besturingssysteem**.</span><span class="sxs-lookup"><span data-stu-id="f540f-414">**OS Type**.</span></span> <span data-ttu-id="f540f-415">Selecteer de besturingssysteem Hallo Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f540f-415">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="f540f-416">**SAP System aantal**.</span><span class="sxs-lookup"><span data-stu-id="f540f-416">**SAP System Count**.</span></span> <span data-ttu-id="f540f-417">Selecteer Hallo nummer SAP-systemen dat u wilt dat tooinstall in dit cluster.</span><span class="sxs-lookup"><span data-stu-id="f540f-417">Select hello number of SAP systems you want tooinstall in this cluster.</span></span>
  -  <span data-ttu-id="f540f-418">**Beschikbaarheid van het systeem**.</span><span class="sxs-lookup"><span data-stu-id="f540f-418">**System Availability**.</span></span> <span data-ttu-id="f540f-419">Selecteer **HA**.</span><span class="sxs-lookup"><span data-stu-id="f540f-419">Select **HA**.</span></span>
  -  <span data-ttu-id="f540f-420">**Gebruikersnaam en het beheerder beheerderswachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f540f-420">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="f540f-421">Maak een nieuwe gebruiker die gebruikt toosign in toohello machine worden kan.</span><span class="sxs-lookup"><span data-stu-id="f540f-421">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="f540f-422">**Nieuwe of bestaande Subnet**.</span><span class="sxs-lookup"><span data-stu-id="f540f-422">**New Or Existing Subnet**.</span></span> <span data-ttu-id="f540f-423">Instellen of een nieuw virtueel netwerk en subnet moeten worden gemaakt of een bestaand subnet moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f540f-423">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="f540f-424">Als u al een virtueel netwerk dat is verbonden tooyour on-premises netwerk hebt, selecteert u **bestaande**.</span><span class="sxs-lookup"><span data-stu-id="f540f-424">If you already have a virtual network that is connected tooyour on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="f540f-425">**Subnet-Id**. Set Hallo-ID van Hallo subnet toowhich Hallo virtuele machines moet zijn verbonden.</span><span class="sxs-lookup"><span data-stu-id="f540f-425">**Subnet Id**. Set hello ID of hello subnet toowhich hello virtual machines should be connected.</span></span> <span data-ttu-id="f540f-426">Selecteer subnet Hallo van uw virtueel particulier netwerk (VPN) of ExpressRoute virtueel netwerk tooconnect Hallo virtuele machine tooyour on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="f540f-426">Select hello subnet of your virtual private network (VPN) or ExpressRoute virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="f540f-427">Hallo-ID ziet er meestal als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="f540f-427">hello ID usually looks like this:</span></span>

   <span data-ttu-id="f540f-428">/Subscriptions/ <*abonnements-id*> /resourceGroups/ <*Resourcegroepnaam*> /providers/Microsoft.Network/virtualNetworks/ <*virtuele-netwerknaam*> /subnets/ <*subnetnaam*></span><span class="sxs-lookup"><span data-stu-id="f540f-428">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="f540f-429">Hallo sjabloon implementeert één Load Balancer van Azure-instantie, die ondersteuning biedt voor meerdere SAP-systemen.</span><span class="sxs-lookup"><span data-stu-id="f540f-429">hello template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="f540f-430">Hallo ASC's exemplaren worden geconfigureerd voor exemplaarnummer 00, 10, 20...</span><span class="sxs-lookup"><span data-stu-id="f540f-430">hello ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="f540f-431">Hallo SCS exemplaren worden geconfigureerd voor exemplaarnummer 01, 11, 21...</span><span class="sxs-lookup"><span data-stu-id="f540f-431">hello SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="f540f-432">Hallo ASC's in de wachtrij plaatsen replicatie Server (gebruikers) (alleen voor Linux) exemplaren worden geconfigureerd voor exemplaarnummer 02, 12, 22...</span><span class="sxs-lookup"><span data-stu-id="f540f-432">hello ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="f540f-433">Hallo SCS Ebruikers (alleen voor Linux) exemplaren worden geconfigureerd voor exemplaarnummer 03, 13, 23...</span><span class="sxs-lookup"><span data-stu-id="f540f-433">hello SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="f540f-434">Hallo load balancer bevat 1 (2 voor Linux) VIP(s), 1 x-VIP voor ASC's / SCS en 1 x-VIP voor Ebruikers (alleen voor Linux).</span><span class="sxs-lookup"><span data-stu-id="f540f-434">hello load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="f540f-435">Hallo bevat volgende lijst alle load-balancingregels (waarbij x staat voor Hallo aantal Hallo SAP-systeem, bijvoorbeeld 1, 2, 3...):</span><span class="sxs-lookup"><span data-stu-id="f540f-435">hello following list contains all load balancing rules (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="f540f-436">Windows-specifieke poorten voor elke SAP-systeem: 445, 5985</span><span class="sxs-lookup"><span data-stu-id="f540f-436">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="f540f-437">ASC's poorten (exemplaarnummer x0): 32 x 0, 36 x 0, 39 x 0, 81 x 0, 5 x 013, 5 x 014, 5 x 016</span><span class="sxs-lookup"><span data-stu-id="f540f-437">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="f540f-438">SCS-poorten (exemplaarnummer x1): 32 x 1 33 x 1, 39 x 1, 81 x 1, 5 x 113, 5 x 114, 5 x 116</span><span class="sxs-lookup"><span data-stu-id="f540f-438">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="f540f-439">ASCS ERS poorten op Linux (exemplaarnummer x2): 33 x 2, 5 x 213, 5 x 214, 5 x 216</span><span class="sxs-lookup"><span data-stu-id="f540f-439">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="f540f-440">SCS ERS poorten op Linux (exemplaarnummer x3): 33 x 3, 5 x 313, 5 x 314, 5 x 316</span><span class="sxs-lookup"><span data-stu-id="f540f-440">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="f540f-441">Hallo load balancer is geconfigureerde toouse Hallo test-poorten (waarbij x staat voor Hallo aantal Hallo SAP-systeem, bijvoorbeeld 1, 2, 3...) te volgen:</span><span class="sxs-lookup"><span data-stu-id="f540f-441">hello load balancer is configured toouse hello following probe ports (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="f540f-442">ASC's / SCS interne load balancer-testpoort: 620 0 x</span><span class="sxs-lookup"><span data-stu-id="f540f-442">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="f540f-443">Ebruikers interne load balancer-testpoort (alleen voor Linux): 621 x 2</span><span class="sxs-lookup"><span data-stu-id="f540f-443">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="f540f-444"><a name="database-template"></a>Database-sjabloon</span><span class="sxs-lookup"><span data-stu-id="f540f-444"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="f540f-445">Hallo databasesjabloon implementeert een of twee virtuele machines waarmee u tooinstall kunt Hallo relationele databasebeheersysteem (RDBMS) voor een SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="f540f-445">hello database template deploys one or two virtual machines that you can use tooinstall hello relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="f540f-446">Bijvoorbeeld, als u een sjabloon ASC's / SCS voor vijf SAP-systemen implementeert, moet u toodeploy deze sjabloon vijf keer.</span><span class="sxs-lookup"><span data-stu-id="f540f-446">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="f540f-447">tooset up Hallo database multi-SID sjabloon in Hallo [multi-SID databasesjabloon] [ sap-templates-3-tier-multisid-db-marketplace-image] of [multi-SID databasesjabloon beheerd schijven] [ sap-templates-3-tier-multisid-db-marketplace-image-md], voer waarden in voor Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="f540f-447">tooset up hello database multi-SID template, in hello [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image] or [database multi-SID template using Managed Disks][sap-templates-3-tier-multisid-db-marketplace-image-md], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="f540f-448">**SAP-Id van het systeem**. Voer Hallo SAP systeem-ID van Hallo gewenste tooinstall SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="f540f-448">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="f540f-449">Hallo-ID wordt als voorvoegsel worden gebruikt voor Hallo-resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f540f-449">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="f540f-450">**Type besturingssysteem**.</span><span class="sxs-lookup"><span data-stu-id="f540f-450">**Os Type**.</span></span> <span data-ttu-id="f540f-451">Selecteer de besturingssysteem Hallo Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f540f-451">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="f540f-452">**DbType**.</span><span class="sxs-lookup"><span data-stu-id="f540f-452">**Dbtype**.</span></span> <span data-ttu-id="f540f-453">Selecteer Hallo type Hallo database dat u wilt dat tooinstall op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f540f-453">Select hello type of hello database you want tooinstall on hello cluster.</span></span> <span data-ttu-id="f540f-454">Selecteer **SQL** als u wilt dat tooinstall Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f540f-454">Select **SQL** if you want tooinstall Microsoft SQL Server.</span></span> <span data-ttu-id="f540f-455">Selecteer **HANA** als u van plan tooinstall SAP HANA Hallo virtuele machines bent.</span><span class="sxs-lookup"><span data-stu-id="f540f-455">Select **HANA** if you plan tooinstall SAP HANA on hello virtual machines.</span></span> <span data-ttu-id="f540f-456">Zorg ervoor dat tooselect Hallo juiste operationele systeemtype: Selecteer **Windows** voor SQL, en selecteer een Linux-distributiepunt voor HANA.</span><span class="sxs-lookup"><span data-stu-id="f540f-456">Make sure tooselect hello correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="f540f-457">Hello Azure Load Balancer die is verbonden toohello virtuele machines worden geconfigureerd toosupport Hallo geselecteerd databasetype:</span><span class="sxs-lookup"><span data-stu-id="f540f-457">hello Azure Load Balancer that is connected toohello virtual machines will be configured toosupport hello selected database type:</span></span>
    * <span data-ttu-id="f540f-458">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="f540f-458">**SQL**.</span></span> <span data-ttu-id="f540f-459">Hallo load balancer wordt verdelen poort 1433.</span><span class="sxs-lookup"><span data-stu-id="f540f-459">hello load balancer will load-balance port 1433.</span></span> <span data-ttu-id="f540f-460">Zorg ervoor dat toouse deze poort voor de installatie van SQL Server Always On.</span><span class="sxs-lookup"><span data-stu-id="f540f-460">Make sure toouse this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="f540f-461">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="f540f-461">**HANA**.</span></span> <span data-ttu-id="f540f-462">Hallo load balancer wordt verdelen poorten 35015 en 35017.</span><span class="sxs-lookup"><span data-stu-id="f540f-462">hello load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="f540f-463">Zorg ervoor dat tooinstall SAP HANA met exemplaarnummer **50**.</span><span class="sxs-lookup"><span data-stu-id="f540f-463">Make sure tooinstall SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="f540f-464">Hallo load balancer wordt testpoort 62550 gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f540f-464">hello load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="f540f-465">**Grootte van het SAP**.</span><span class="sxs-lookup"><span data-stu-id="f540f-465">**Sap System Size**.</span></span> <span data-ttu-id="f540f-466">Set Hallo aantal nieuwe Hallo-systeem SAP's bieden.</span><span class="sxs-lookup"><span data-stu-id="f540f-466">Set hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="f540f-467">Als u niet zeker hoeveel SAP's Hallo systeem is vereist weet, vraagt u uw SAP-technologie Partner of System Integrator.</span><span class="sxs-lookup"><span data-stu-id="f540f-467">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="f540f-468">**Beschikbaarheid van het systeem**.</span><span class="sxs-lookup"><span data-stu-id="f540f-468">**System Availability**.</span></span> <span data-ttu-id="f540f-469">Selecteer **HA**.</span><span class="sxs-lookup"><span data-stu-id="f540f-469">Select **HA**.</span></span>
  -  <span data-ttu-id="f540f-470">**Gebruikersnaam en het beheerder beheerderswachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f540f-470">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="f540f-471">Maak een nieuwe gebruiker die gebruikt toosign in toohello machine worden kan.</span><span class="sxs-lookup"><span data-stu-id="f540f-471">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="f540f-472">**Subnet-Id**. Hallo-ID van het Hallo-subnet dat u hebt gebruikt tijdens de implementatie van Hallo ASC's / SCS sjabloon Hallo of Hallo-ID van Hallo-subnet dat is gemaakt als onderdeel van Hallo ASC's / SCS sjabloonimplementatie invoeren.</span><span class="sxs-lookup"><span data-stu-id="f540f-472">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="f540f-473"><a name="application-servers-template"></a>Toepassingssjabloon voor servers</span><span class="sxs-lookup"><span data-stu-id="f540f-473"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="f540f-474">Hallo-toepassingssjabloon servers implementeert twee of meer virtuele machines die kan worden gebruikt als SAP-toepassingsserver exemplaren voor een SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="f540f-474">hello application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="f540f-475">Bijvoorbeeld, als u een sjabloon ASC's / SCS voor vijf SAP-systemen implementeert, moet u toodeploy deze sjabloon vijf keer.</span><span class="sxs-lookup"><span data-stu-id="f540f-475">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="f540f-476">tooset up Hallo servers multi-SID toepassingssjabloon, in Hallo [toepassingssjabloon servers multi-SID] [ sap-templates-3-tier-multisid-apps-marketplace-image] of [servers multi-SID toepassingssjabloon beheerd schijven] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], voer waarden in voor Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="f540f-476">tooset up hello application servers multi-SID template, in hello [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image] or [application servers multi-SID template using Managed Disks][sap-templates-3-tier-multisid-apps-marketplace-image-md], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="f540f-477">**SAP-Id van het systeem**. Voer Hallo SAP systeem-ID van Hallo gewenste tooinstall SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="f540f-477">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="f540f-478">Hallo-ID wordt als voorvoegsel worden gebruikt voor Hallo-resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f540f-478">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="f540f-479">**Type besturingssysteem**.</span><span class="sxs-lookup"><span data-stu-id="f540f-479">**Os Type**.</span></span> <span data-ttu-id="f540f-480">Selecteer de besturingssysteem Hallo Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f540f-480">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="f540f-481">**Grootte van het SAP**.</span><span class="sxs-lookup"><span data-stu-id="f540f-481">**Sap System Size**.</span></span> <span data-ttu-id="f540f-482">Hallo aantal nieuwe Hallo-systeem SAP's bieden.</span><span class="sxs-lookup"><span data-stu-id="f540f-482">hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="f540f-483">Als u niet zeker hoeveel SAP's Hallo systeem is vereist weet, vraagt u uw SAP-technologie Partner of System Integrator.</span><span class="sxs-lookup"><span data-stu-id="f540f-483">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="f540f-484">**Beschikbaarheid van het systeem**.</span><span class="sxs-lookup"><span data-stu-id="f540f-484">**System Availability**.</span></span> <span data-ttu-id="f540f-485">Selecteer **HA**.</span><span class="sxs-lookup"><span data-stu-id="f540f-485">Select **HA**.</span></span>
  -  <span data-ttu-id="f540f-486">**Gebruikersnaam en het beheerder beheerderswachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f540f-486">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="f540f-487">Maak een nieuwe gebruiker die gebruikt toosign in toohello machine worden kan.</span><span class="sxs-lookup"><span data-stu-id="f540f-487">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="f540f-488">**Subnet-Id**. Hallo-ID van het Hallo-subnet dat u hebt gebruikt tijdens de implementatie van Hallo ASC's / SCS sjabloon Hallo of Hallo-ID van Hallo-subnet dat is gemaakt als onderdeel van Hallo ASC's / SCS sjabloonimplementatie invoeren.</span><span class="sxs-lookup"><span data-stu-id="f540f-488">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="f540f-489"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a>Virtuele Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="f540f-489"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="f540f-490">In ons voorbeeld is de adresruimte Hallo Hallo virtuele Azure-netwerk 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="f540f-490">In our example, hello address space of hello Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="f540f-491">Er is één subnet met de naam **Subnet**, met een adresbereik van 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="f540f-491">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="f540f-492">Alle virtuele machines en interne load balancers worden geïmplementeerd in dit virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="f540f-492">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f540f-493">Breng geen wijzigingen toohello netwerkinstellingen in het gastbesturingssysteem Hallo.</span><span class="sxs-lookup"><span data-stu-id="f540f-493">Don't make any changes toohello network settings inside hello guest operating system.</span></span> <span data-ttu-id="f540f-494">Dit omvat het IP-adressen, DNS-servers en subnet.</span><span class="sxs-lookup"><span data-stu-id="f540f-494">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="f540f-495">De netwerkinstellingen configureren in Azure.</span><span class="sxs-lookup"><span data-stu-id="f540f-495">Configure all your network settings in Azure.</span></span> <span data-ttu-id="f540f-496">Hallo Dynamic Host Configuration Protocol (DHCP)-service geeft uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="f540f-496">hello Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="f540f-497"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a>DNS IP-adressen</span><span class="sxs-lookup"><span data-stu-id="f540f-497"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="f540f-498">Hallo tooset vereist dat DNS IP-adressen, Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="f540f-498">tooset hello required DNS IP addresses, do hello following steps.</span></span>

1.  <span data-ttu-id="f540f-499">In de Azure-portal op Hallo Hallo **DNS-servers** blade, zorg ervoor dat het virtuele netwerk **DNS-servers** optie is ingesteld, te**aangepaste DNS**.</span><span class="sxs-lookup"><span data-stu-id="f540f-499">In hello Azure portal, on hello **DNS servers** blade, make sure that your virtual network **DNS servers** option is set too**Custom DNS**.</span></span>
2.  <span data-ttu-id="f540f-500">Selecteer uw instellingen op basis van Hallo type netwerk die u hebben.</span><span class="sxs-lookup"><span data-stu-id="f540f-500">Select your settings based on hello type of network you have.</span></span> <span data-ttu-id="f540f-501">Zie voor meer informatie Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="f540f-501">For more information, see hello following resources:</span></span>
    * <span data-ttu-id="f540f-502">[Zakelijke netwerkverbinding (cross-premises)][planning-guide-2.2]: Hallo IP-adressen van Hallo lokale DNS-servers toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f540f-502">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add hello IP addresses of hello on-premises DNS servers.</span></span>  
    <span data-ttu-id="f540f-503">U kunt de lokale DNS-servers toohello virtuele machines die worden uitgevoerd in Azure uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="f540f-503">You can extend on-premises DNS servers toohello virtual machines that are running in Azure.</span></span> <span data-ttu-id="f540f-504">In dit scenario, voegt u toe Hallo IP-adressen van hello Azure virtuele machines waarop u Hallo DNS-service uitvoert.</span><span class="sxs-lookup"><span data-stu-id="f540f-504">In that scenario, you can add hello IP addresses of hello Azure virtual machines on which you run hello DNS service.</span></span>
    * <span data-ttu-id="f540f-505">[Cloud-implementatie][planning-guide-2.1]: een extra virtuele machine implementeren in Hallo hetzelfde virtuele netwerk-exemplaar dat als een DNS-server fungeert.</span><span class="sxs-lookup"><span data-stu-id="f540f-505">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in hello same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="f540f-506">Toevoegen van Hallo IP-adressen van hello Azure virtuele machines die u toorun DNS-service hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f540f-506">Add hello IP addresses of hello Azure virtual machines that you've set up toorun DNS service.</span></span>

    ![Afbeelding 12: DNS-servers configureren voor Azure Virtual Network][sap-ha-guide-figure-3001]

    <span data-ttu-id="f540f-508">_**Afbeelding 12:** configureren DNS-servers voor Azure Virtual Network_</span><span class="sxs-lookup"><span data-stu-id="f540f-508">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="f540f-509">Als u Hallo IP-adressen van Hallo DNS-servers wijzigt, moet u toorestart hello Azure virtuele machines tooapply Hallo wijzigen en propageren Hallo nieuwe DNS-servers.</span><span class="sxs-lookup"><span data-stu-id="f540f-509">If you change hello IP addresses of hello DNS servers, you need toorestart hello Azure virtual machines tooapply hello change and propagate hello new DNS servers.</span></span>
  >
  >

<span data-ttu-id="f540f-510">Hallo DNS-service is geïnstalleerd en geconfigureerd op deze virtuele machines van Windows in ons voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f540f-510">In our example, hello DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="f540f-511">De rol virtuele machine</span><span class="sxs-lookup"><span data-stu-id="f540f-511">Virtual machine role</span></span> | <span data-ttu-id="f540f-512">Hostnaam van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="f540f-512">Virtual machine host name</span></span> | <span data-ttu-id="f540f-513">Naam van de netwerk-kaart</span><span class="sxs-lookup"><span data-stu-id="f540f-513">Network card name</span></span> | <span data-ttu-id="f540f-514">Statisch IP-adres</span><span class="sxs-lookup"><span data-stu-id="f540f-514">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f540f-515">Eerste DNS-server</span><span class="sxs-lookup"><span data-stu-id="f540f-515">First DNS server</span></span> |<span data-ttu-id="f540f-516">domcontr 0</span><span class="sxs-lookup"><span data-stu-id="f540f-516">domcontr-0</span></span> |<span data-ttu-id="f540f-517">PR1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="f540f-517">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="f540f-518">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="f540f-518">10.0.0.10</span></span> |
| <span data-ttu-id="f540f-519">Tweede DNS-server</span><span class="sxs-lookup"><span data-stu-id="f540f-519">Second DNS server</span></span> |<span data-ttu-id="f540f-520">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="f540f-520">domcontr-1</span></span> |<span data-ttu-id="f540f-521">PR1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="f540f-521">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="f540f-522">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="f540f-522">10.0.0.11</span></span> |

### <span data-ttu-id="f540f-523"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Hostnamen en statische IP-adressen voor Hallo SAP ASC's / SCS geclusterde exemplaar en DBMS geclusterd exemplaar</span><span class="sxs-lookup"><span data-stu-id="f540f-523"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for hello SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="f540f-524">Voor on-premises implementatie moet u deze gereserveerde hostnamen en IP-adressen:</span><span class="sxs-lookup"><span data-stu-id="f540f-524">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="f540f-525">Virtuele host naam rol</span><span class="sxs-lookup"><span data-stu-id="f540f-525">Virtual host name role</span></span> | <span data-ttu-id="f540f-526">De naam van de virtuele host</span><span class="sxs-lookup"><span data-stu-id="f540f-526">Virtual host name</span></span> | <span data-ttu-id="f540f-527">Virtuele vaste IP-adres</span><span class="sxs-lookup"><span data-stu-id="f540f-527">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f540f-528">SAP ASC's / SCS eerste virtuele host clusternaam (voor cluster)</span><span class="sxs-lookup"><span data-stu-id="f540f-528">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="f540f-529">PR1-ASC's-vir</span><span class="sxs-lookup"><span data-stu-id="f540f-529">pr1-ascs-vir</span></span> |<span data-ttu-id="f540f-530">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="f540f-530">10.0.0.42</span></span> |
| <span data-ttu-id="f540f-531">Naam van de virtuele host op het exemplaar van SAP ASC's / SCS</span><span class="sxs-lookup"><span data-stu-id="f540f-531">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="f540f-532">PR1 ASC's sap</span><span class="sxs-lookup"><span data-stu-id="f540f-532">pr1-ascs-sap</span></span> |<span data-ttu-id="f540f-533">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="f540f-533">10.0.0.43</span></span> |
| <span data-ttu-id="f540f-534">SAP DBMS tweede virtuele host clusternaam (cluster management)</span><span class="sxs-lookup"><span data-stu-id="f540f-534">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="f540f-535">PR1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="f540f-535">pr1-dbms-vir</span></span> |<span data-ttu-id="f540f-536">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="f540f-536">10.0.0.32</span></span> |

<span data-ttu-id="f540f-537">Wanneer u Hallo-cluster maakt, maakt u Hallo virtuele hostnamen **pr1-ASC's-vir** en **pr1-dbms-vir** en Hallo bijbehorende IP-adressen die Hallo cluster zelf beheren.</span><span class="sxs-lookup"><span data-stu-id="f540f-537">When you create hello cluster, create hello virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and hello associated IP addresses that manage hello cluster itself.</span></span> <span data-ttu-id="f540f-538">Voor informatie over het toodo deze, Zie [verzamelen clusterknooppunten in een clusterconfiguratie][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="f540f-538">For information about how toodo this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="f540f-539">U kunt Hallo handmatig maken andere twee virtuele hostnamen **pr1 ASC's sap** en **pr1 dbms sap**, en Hallo bijbehorende IP-adressen op Hallo DNS-server.</span><span class="sxs-lookup"><span data-stu-id="f540f-539">You can manually create hello other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and hello associated IP addresses, on hello DNS server.</span></span> <span data-ttu-id="f540f-540">Hallo geclusterde SAP ASC's / SCS-instantie en Hallo geclusterde DBMS instantie deze resources gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f540f-540">hello clustered SAP ASCS/SCS instance and hello clustered DBMS instance use these resources.</span></span> <span data-ttu-id="f540f-541">Voor informatie over het toodo deze, Zie [maken van een virtuele host-naam voor een geclusterd exemplaar van de SAP ASC's / SCS][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="f540f-541">For information about how toodo this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="f540f-542"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Statische IP-adressen voor virtuele machines die Hallo SAP instellen</span><span class="sxs-lookup"><span data-stu-id="f540f-542"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for hello SAP virtual machines</span></span>
<span data-ttu-id="f540f-543">Nadat u Hallo virtuele machines toouse in uw cluster implementeert, moet u tooset statische IP-adressen voor alle virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f540f-543">After you deploy hello virtual machines toouse in your cluster, you need tooset static IP addresses for all virtual machines.</span></span> <span data-ttu-id="f540f-544">Dit doen in hello Azure Virtual Network-configuratie en niet in het gastbesturingssysteem Hallo.</span><span class="sxs-lookup"><span data-stu-id="f540f-544">Do this in hello Azure Virtual Network configuration, and not in hello guest operating system.</span></span>

1.  <span data-ttu-id="f540f-545">Selecteer in de Azure-portal hello, **resourcegroep** > **netwerkkaart** > **instellingen** > **IP-adres** .</span><span class="sxs-lookup"><span data-stu-id="f540f-545">In hello Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="f540f-546">Op Hallo **IP-adressen** blade onder **toewijzing**, selecteer **statische**.</span><span class="sxs-lookup"><span data-stu-id="f540f-546">On hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="f540f-547">In Hallo **IP-adres** Voer Hallo IP-adres dat u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="f540f-547">In hello **IP address** box, enter hello IP address that you want toouse.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f540f-548">Als u Hallo IP-adres van de netwerkkaart Hallo wijzigt, moet u toorestart hello Azure virtuele machines tooapply Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f540f-548">If you change hello IP address of hello network card, you need toorestart hello Azure virtual machines tooapply hello change.</span></span>  
  >
  >

  ![Afbeelding 13: Statische IP-adressen voor de netwerkkaart Hallo van elke virtuele machine instellen][sap-ha-guide-figure-3002]

  <span data-ttu-id="f540f-550">_**Afbeelding 13:** statische IP-adressen voor de netwerkkaart Hallo van elke virtuele machine instellen_</span><span class="sxs-lookup"><span data-stu-id="f540f-550">_**Figure 13:** Set static IP addresses for hello network card of each virtual machine_</span></span>

  <span data-ttu-id="f540f-551">Herhaal deze stap voor alle netwerkinterfaces, dat wil zeggen, voor alle virtuele machines, met inbegrip van virtuele machines wilt u toouse voor uw Active Directory en DNS-service.</span><span class="sxs-lookup"><span data-stu-id="f540f-551">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want toouse for your Active Directory/DNS service.</span></span>

<span data-ttu-id="f540f-552">In ons voorbeeld hebben we deze virtuele machines en statische IP-adressen:</span><span class="sxs-lookup"><span data-stu-id="f540f-552">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="f540f-553">De rol virtuele machine</span><span class="sxs-lookup"><span data-stu-id="f540f-553">Virtual machine role</span></span> | <span data-ttu-id="f540f-554">Hostnaam van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="f540f-554">Virtual machine host name</span></span> | <span data-ttu-id="f540f-555">Naam van de netwerk-kaart</span><span class="sxs-lookup"><span data-stu-id="f540f-555">Network card name</span></span> | <span data-ttu-id="f540f-556">Statisch IP-adres</span><span class="sxs-lookup"><span data-stu-id="f540f-556">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f540f-557">Eerste SAP Application Server-exemplaar</span><span class="sxs-lookup"><span data-stu-id="f540f-557">First SAP Application Server instance</span></span> |<span data-ttu-id="f540f-558">PR1-di-0</span><span class="sxs-lookup"><span data-stu-id="f540f-558">pr1-di-0</span></span> |<span data-ttu-id="f540f-559">PR1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="f540f-559">pr1-nic-di-0</span></span> |<span data-ttu-id="f540f-560">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="f540f-560">10.0.0.50</span></span> |
| <span data-ttu-id="f540f-561">Tweede SAP Application Server-exemplaar</span><span class="sxs-lookup"><span data-stu-id="f540f-561">Second SAP Application Server instance</span></span> |<span data-ttu-id="f540f-562">PR1-di-1</span><span class="sxs-lookup"><span data-stu-id="f540f-562">pr1-di-1</span></span> |<span data-ttu-id="f540f-563">PR1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="f540f-563">pr1-nic-di-1</span></span> |<span data-ttu-id="f540f-564">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="f540f-564">10.0.0.51</span></span> |
| <span data-ttu-id="f540f-565">...</span><span class="sxs-lookup"><span data-stu-id="f540f-565">...</span></span> |<span data-ttu-id="f540f-566">...</span><span class="sxs-lookup"><span data-stu-id="f540f-566">...</span></span> |<span data-ttu-id="f540f-567">...</span><span class="sxs-lookup"><span data-stu-id="f540f-567">...</span></span> |<span data-ttu-id="f540f-568">...</span><span class="sxs-lookup"><span data-stu-id="f540f-568">...</span></span> |
| <span data-ttu-id="f540f-569">Laatste SAP Application Server-exemplaar</span><span class="sxs-lookup"><span data-stu-id="f540f-569">Last SAP Application Server instance</span></span> |<span data-ttu-id="f540f-570">PR1-di-5</span><span class="sxs-lookup"><span data-stu-id="f540f-570">pr1-di-5</span></span> |<span data-ttu-id="f540f-571">PR1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="f540f-571">pr1-nic-di-5</span></span> |<span data-ttu-id="f540f-572">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="f540f-572">10.0.0.55</span></span> |
| <span data-ttu-id="f540f-573">Eerste clusterknooppunt voor ASC's / SCS-exemplaar</span><span class="sxs-lookup"><span data-stu-id="f540f-573">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="f540f-574">PR1-ASC's-0</span><span class="sxs-lookup"><span data-stu-id="f540f-574">pr1-ascs-0</span></span> |<span data-ttu-id="f540f-575">PR1-nic-ASC's-0</span><span class="sxs-lookup"><span data-stu-id="f540f-575">pr1-nic-ascs-0</span></span> |<span data-ttu-id="f540f-576">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="f540f-576">10.0.0.40</span></span> |
| <span data-ttu-id="f540f-577">Tweede clusterknooppunt voor ASC's / SCS-exemplaar</span><span class="sxs-lookup"><span data-stu-id="f540f-577">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="f540f-578">PR1-ASC's-1</span><span class="sxs-lookup"><span data-stu-id="f540f-578">pr1-ascs-1</span></span> |<span data-ttu-id="f540f-579">PR1-nic-ASC's-1</span><span class="sxs-lookup"><span data-stu-id="f540f-579">pr1-nic-ascs-1</span></span> |<span data-ttu-id="f540f-580">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="f540f-580">10.0.0.41</span></span> |
| <span data-ttu-id="f540f-581">Eerste clusterknooppunt voor DBMS-exemplaar</span><span class="sxs-lookup"><span data-stu-id="f540f-581">First cluster node for DBMS instance</span></span> |<span data-ttu-id="f540f-582">PR1-db-0</span><span class="sxs-lookup"><span data-stu-id="f540f-582">pr1-db-0</span></span> |<span data-ttu-id="f540f-583">PR1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="f540f-583">pr1-nic-db-0</span></span> |<span data-ttu-id="f540f-584">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="f540f-584">10.0.0.30</span></span> |
| <span data-ttu-id="f540f-585">Tweede clusterknooppunt voor DBMS-exemplaar</span><span class="sxs-lookup"><span data-stu-id="f540f-585">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="f540f-586">PR1-db-1</span><span class="sxs-lookup"><span data-stu-id="f540f-586">pr1-db-1</span></span> |<span data-ttu-id="f540f-587">PR1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="f540f-587">pr1-nic-db-1</span></span> |<span data-ttu-id="f540f-588">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="f540f-588">10.0.0.31</span></span> |

### <span data-ttu-id="f540f-589"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Een statisch IP-adres instellen voor hello Azure interne load balancer</span><span class="sxs-lookup"><span data-stu-id="f540f-589"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for hello Azure internal load balancer</span></span>

<span data-ttu-id="f540f-590">Hallo SAP Azure Resource Manager-sjabloon maakt u een Azure interne load balancer die wordt gebruikt voor Hallo SAP ASC's / SCS exemplaar als Hallo DBMS-cluster.</span><span class="sxs-lookup"><span data-stu-id="f540f-590">hello SAP Azure Resource Manager template creates an Azure internal load balancer that is used for hello SAP ASCS/SCS instance cluster and hello DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f540f-591">Hallo IP-adres van de naam van de virtuele host Hallo Hallo SAP ASC's / SCS is Hallo dezelfde als de IP-adres Hallo Hallo SAP ASC's / SCS interne load balancer: **pr1-lb-ASC's**.</span><span class="sxs-lookup"><span data-stu-id="f540f-591">hello IP address of hello virtual host name of hello SAP ASCS/SCS is hello same as hello IP address of hello SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="f540f-592">Hallo IP-adres van de virtuele naam Hallo Hallo DBMS is Hallo dezelfde als de IP-adres Hallo Hallo DBMS interne load balancer: **pr1-lb-dbms**.</span><span class="sxs-lookup"><span data-stu-id="f540f-592">hello IP address of hello virtual name of hello DBMS is hello same as hello IP address of hello DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="f540f-593">tooset een statisch IP-adres voor hello Azure interne load balancer:</span><span class="sxs-lookup"><span data-stu-id="f540f-593">tooset a static IP address for hello Azure internal load balancer:</span></span>

1.  <span data-ttu-id="f540f-594">Hallo initiële implementatie ingesteld Hallo interne load balancer IP-adres te**dynamische**.</span><span class="sxs-lookup"><span data-stu-id="f540f-594">hello initial deployment sets hello internal load balancer IP address too**Dynamic**.</span></span> <span data-ttu-id="f540f-595">In de Azure-portal op Hallo Hallo **IP-adressen** blade onder **toewijzing**, selecteer **statische**.</span><span class="sxs-lookup"><span data-stu-id="f540f-595">In hello Azure portal, on hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="f540f-596">Stel Hallo IP-adres van Hallo interne load balancer **pr1-lb-ASC's** toohello IP-adres van de naam van de virtuele host Hallo van Hallo SAP ASC's / SCS-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f540f-596">Set hello IP address of hello internal load balancer **pr1-lb-ascs** toohello IP address of hello virtual host name of hello SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="f540f-597">Stel Hallo IP-adres van Hallo interne load balancer **pr1-lb-dbms** toohello IP-adres van de naam van de virtuele host Hallo van Hallo DBMS-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f540f-597">Set hello IP address of hello internal load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

  ![Afbeelding 14: Statische IP-adressen voor interne load balancer Hallo voor Hallo SAP ASC's / SCS exemplaar instellen][sap-ha-guide-figure-3003]

  <span data-ttu-id="f540f-599">_**Afbeelding 14:** statische IP-adressen voor interne load balancer Hallo voor Hallo SAP ASC's / SCS exemplaar instellen_</span><span class="sxs-lookup"><span data-stu-id="f540f-599">_**Figure 14:** Set static IP addresses for hello internal load balancer for hello SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="f540f-600">In ons voorbeeld hebben we twee Azure interne load balancers die deze statische IP-adressen:</span><span class="sxs-lookup"><span data-stu-id="f540f-600">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="f540f-601">Azure interne load balancer-rol</span><span class="sxs-lookup"><span data-stu-id="f540f-601">Azure internal load balancer role</span></span> | <span data-ttu-id="f540f-602">Naam Azure interne load balancer</span><span class="sxs-lookup"><span data-stu-id="f540f-602">Azure internal load balancer name</span></span> | <span data-ttu-id="f540f-603">Statisch IP-adres</span><span class="sxs-lookup"><span data-stu-id="f540f-603">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f540f-604">SAP ASC's / SCS exemplaar interne load balancer</span><span class="sxs-lookup"><span data-stu-id="f540f-604">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="f540f-605">PR1-lb-ASC 's</span><span class="sxs-lookup"><span data-stu-id="f540f-605">pr1-lb-ascs</span></span> |<span data-ttu-id="f540f-606">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="f540f-606">10.0.0.43</span></span> |
| <span data-ttu-id="f540f-607">SAP DBMS interne load balancer</span><span class="sxs-lookup"><span data-stu-id="f540f-607">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="f540f-608">PR1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="f540f-608">pr1-lb-dbms</span></span> |<span data-ttu-id="f540f-609">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="f540f-609">10.0.0.33</span></span> |


### <span data-ttu-id="f540f-610"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Standaard ASC's / SCS taakverdelingsregels voor hello Azure interne load balancer</span><span class="sxs-lookup"><span data-stu-id="f540f-610"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="f540f-611">Hallo SAP Azure Resource Manager-sjabloon maakt Hallo-poorten die u nodig:</span><span class="sxs-lookup"><span data-stu-id="f540f-611">hello SAP Azure Resource Manager template creates hello ports you need:</span></span>
* <span data-ttu-id="f540f-612">Een exemplaar ABAP ASCS met Hallo standaard exemplaarnummer **00**</span><span class="sxs-lookup"><span data-stu-id="f540f-612">An ABAP ASCS instance, with hello default instance number **00**</span></span>
* <span data-ttu-id="f540f-613">Een Java-SCS-exemplaar, met Hallo standaard exemplaarnummer **01**</span><span class="sxs-lookup"><span data-stu-id="f540f-613">A Java SCS instance, with hello default instance number **01**</span></span>

<span data-ttu-id="f540f-614">Wanneer u uw exemplaar SAP ASC's / SCS installeert, moet u Hallo standaard exemplaarnummer **00** voor uw ABAP ASCS exemplaar en het Hallo standaard exemplaar **01** voor uw Java-SCS-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f540f-614">When you install your SAP ASCS/SCS instance, you must use hello default instance number **00** for your ABAP ASCS instance and hello default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="f540f-615">Vervolgens maakt u een vereiste voor de interne load balancer-eindpunten voor Hallo SAP NetWeaver poorten.</span><span class="sxs-lookup"><span data-stu-id="f540f-615">Next, create required internal load balancing endpoints for hello SAP NetWeaver ports.</span></span>

<span data-ttu-id="f540f-616">toocreate vereist interne load balancing eindpunten, maakt u eerst deze taakverdeling eindpunten voor Hallo SAP NetWeaver ABAP ASC's poorten:</span><span class="sxs-lookup"><span data-stu-id="f540f-616">toocreate required internal load balancing endpoints, first, create these load balancing endpoints for hello SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="f540f-617">Service/load balancing regelnaam</span><span class="sxs-lookup"><span data-stu-id="f540f-617">Service/load balancing rule name</span></span> | <span data-ttu-id="f540f-618">Standaardpoortnummers</span><span class="sxs-lookup"><span data-stu-id="f540f-618">Default port numbers</span></span> | <span data-ttu-id="f540f-619">Concrete poorten voor (ASC's exemplaar met exemplaarnummer 00) (uit met 10)</span><span class="sxs-lookup"><span data-stu-id="f540f-619">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f540f-620">In de wachtrij plaatsen Server / *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="f540f-620">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="f540f-621">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="f540f-621">32<*InstanceNumber*></span></span> |<span data-ttu-id="f540f-622">3200</span><span class="sxs-lookup"><span data-stu-id="f540f-622">3200</span></span> |
| <span data-ttu-id="f540f-623">ABAP berichtenserver / *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="f540f-623">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="f540f-624">36 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="f540f-624">36<*InstanceNumber*></span></span> |<span data-ttu-id="f540f-625">3600</span><span class="sxs-lookup"><span data-stu-id="f540f-625">3600</span></span> |
| <span data-ttu-id="f540f-626">Interne ABAP bericht / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="f540f-626">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="f540f-627">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="f540f-627">39<*InstanceNumber*></span></span> |<span data-ttu-id="f540f-628">3900</span><span class="sxs-lookup"><span data-stu-id="f540f-628">3900</span></span> |
| <span data-ttu-id="f540f-629">Server-HTTP-bericht / *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="f540f-629">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="f540f-630">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="f540f-630">81<*InstanceNumber*></span></span> |<span data-ttu-id="f540f-631">8100</span><span class="sxs-lookup"><span data-stu-id="f540f-631">8100</span></span> |
| <span data-ttu-id="f540f-632">SAP Start Service ASC's HTTP / *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="f540f-632">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="f540f-633">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="f540f-633">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="f540f-634">50013</span><span class="sxs-lookup"><span data-stu-id="f540f-634">50013</span></span> |
| <span data-ttu-id="f540f-635">SAP Start Service ASC's HTTPS / *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="f540f-635">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="f540f-636">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="f540f-636">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="f540f-637">50014</span><span class="sxs-lookup"><span data-stu-id="f540f-637">50014</span></span> |
| <span data-ttu-id="f540f-638">Replicatie van de wachtrij plaatsen / *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="f540f-638">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="f540f-639">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="f540f-639">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="f540f-640">50016</span><span class="sxs-lookup"><span data-stu-id="f540f-640">50016</span></span> |
| <span data-ttu-id="f540f-641">SAP Start Service Ebruikers HTTP *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="f540f-641">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="f540f-642">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="f540f-642">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="f540f-643">51013</span><span class="sxs-lookup"><span data-stu-id="f540f-643">51013</span></span> |
| <span data-ttu-id="f540f-644">SAP Start Service Ebruikers HTTP *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="f540f-644">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="f540f-645">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="f540f-645">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="f540f-646">51014</span><span class="sxs-lookup"><span data-stu-id="f540f-646">51014</span></span> |
| <span data-ttu-id="f540f-647">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="f540f-647">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="f540f-648">5985</span><span class="sxs-lookup"><span data-stu-id="f540f-648">5985</span></span> |
| <span data-ttu-id="f540f-649">Bestandsshare *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="f540f-649">File Share *Lbrule445*</span></span> | |<span data-ttu-id="f540f-650">445</span><span class="sxs-lookup"><span data-stu-id="f540f-650">445</span></span> |

<span data-ttu-id="f540f-651">_**Tabel 1:** poortnummers van Hallo SAP NetWeaver ABAP ASC's exemplaren_</span><span class="sxs-lookup"><span data-stu-id="f540f-651">_**Table 1:** Port numbers of hello SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="f540f-652">Vervolgens maakt u deze load balancing-eindpunten voor Hallo SAP NetWeaver Java SCS poorten:</span><span class="sxs-lookup"><span data-stu-id="f540f-652">Then, create these load balancing endpoints for hello SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="f540f-653">Service/load balancing regelnaam</span><span class="sxs-lookup"><span data-stu-id="f540f-653">Service/load balancing rule name</span></span> | <span data-ttu-id="f540f-654">Standaardpoortnummers</span><span class="sxs-lookup"><span data-stu-id="f540f-654">Default port numbers</span></span> | <span data-ttu-id="f540f-655">Concrete poorten voor (exemplaar met exemplaarnummer 01 SCS) (Ebruikers met 11)</span><span class="sxs-lookup"><span data-stu-id="f540f-655">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f540f-656">In de wachtrij plaatsen Server / *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="f540f-656">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="f540f-657">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="f540f-657">32<*InstanceNumber*></span></span> |<span data-ttu-id="f540f-658">3201</span><span class="sxs-lookup"><span data-stu-id="f540f-658">3201</span></span> |
| <span data-ttu-id="f540f-659">Gateway-Server / *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="f540f-659">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="f540f-660">33 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="f540f-660">33<*InstanceNumber*></span></span> |<span data-ttu-id="f540f-661">3301</span><span class="sxs-lookup"><span data-stu-id="f540f-661">3301</span></span> |
| <span data-ttu-id="f540f-662">Java berichtenserver / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="f540f-662">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="f540f-663">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="f540f-663">39<*InstanceNumber*></span></span> |<span data-ttu-id="f540f-664">3901</span><span class="sxs-lookup"><span data-stu-id="f540f-664">3901</span></span> |
| <span data-ttu-id="f540f-665">Server-HTTP-bericht / *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="f540f-665">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="f540f-666">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="f540f-666">81<*InstanceNumber*></span></span> |<span data-ttu-id="f540f-667">8101</span><span class="sxs-lookup"><span data-stu-id="f540f-667">8101</span></span> |
| <span data-ttu-id="f540f-668">SAP Start Service SCS HTTP / *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="f540f-668">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="f540f-669">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="f540f-669">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="f540f-670">50113</span><span class="sxs-lookup"><span data-stu-id="f540f-670">50113</span></span> |
| <span data-ttu-id="f540f-671">SAP Start Service SCS HTTPS / *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="f540f-671">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="f540f-672">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="f540f-672">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="f540f-673">50114</span><span class="sxs-lookup"><span data-stu-id="f540f-673">50114</span></span> |
| <span data-ttu-id="f540f-674">Replicatie van de wachtrij plaatsen / *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="f540f-674">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="f540f-675">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="f540f-675">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="f540f-676">50116</span><span class="sxs-lookup"><span data-stu-id="f540f-676">50116</span></span> |
| <span data-ttu-id="f540f-677">SAP Start Service Ebruikers HTTP *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="f540f-677">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="f540f-678">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="f540f-678">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="f540f-679">51113</span><span class="sxs-lookup"><span data-stu-id="f540f-679">51113</span></span> |
| <span data-ttu-id="f540f-680">SAP Start Service Ebruikers HTTP *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="f540f-680">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="f540f-681">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="f540f-681">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="f540f-682">51114</span><span class="sxs-lookup"><span data-stu-id="f540f-682">51114</span></span> |
| <span data-ttu-id="f540f-683">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="f540f-683">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="f540f-684">5985</span><span class="sxs-lookup"><span data-stu-id="f540f-684">5985</span></span> |
| <span data-ttu-id="f540f-685">Bestandsshare *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="f540f-685">File Share *Lbrule445*</span></span> | |<span data-ttu-id="f540f-686">445</span><span class="sxs-lookup"><span data-stu-id="f540f-686">445</span></span> |

<span data-ttu-id="f540f-687">_**Tabel 2:** poortnummers van Hallo SAP NetWeaver Java SCS exemplaren_</span><span class="sxs-lookup"><span data-stu-id="f540f-687">_**Table 2:** Port numbers of hello SAP NetWeaver Java SCS instances_</span></span>

![Afbeelding 15: Standaard ASC's / SCS taakverdelingsregels voor hello Azure interne load balancer][sap-ha-guide-figure-3004]

<span data-ttu-id="f540f-689">_**Afbeelding 15:** standaard ASC's / SCS load-balancingregels voor hello Azure interne load balancer_</span><span class="sxs-lookup"><span data-stu-id="f540f-689">_**Figure 15:** Default ASCS/SCS load balancing rules for hello Azure internal load balancer_</span></span>

<span data-ttu-id="f540f-690">Stel IP-adres Hallo Hallo load balancer **pr1-lb-dbms** toohello IP-adres van de naam van de virtuele host Hallo van Hallo DBMS-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f540f-690">Set hello IP address of hello load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

### <span data-ttu-id="f540f-691"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Hallo ASC's / SCS standaard load-balancingregels voor hello Azure interne load balancer wijzigen</span><span class="sxs-lookup"><span data-stu-id="f540f-691"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="f540f-692">Als u verschillende aantallen toouse voor Hallo SAP ASC's of SCS exemplaren wilt, moet u Hallo namen en waarden van de poorten wijzigen van standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="f540f-692">If you want toouse different numbers for hello SAP ASCS or SCS instances, you must change hello names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="f540f-693">Selecteer in de Azure-portal hello,  **<* SID*> - lb - ASC's load balancer ** > **Load Balancing regels**.</span><span class="sxs-lookup"><span data-stu-id="f540f-693">In hello Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="f540f-694">Voor alle load-balancingregels die deel uitmaken van toohello SAP ASC's of SCS exemplaar, deze waarden te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="f540f-694">For all load balancing rules that belong toohello SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="f540f-695">Naam</span><span class="sxs-lookup"><span data-stu-id="f540f-695">Name</span></span>
  * <span data-ttu-id="f540f-696">Poort</span><span class="sxs-lookup"><span data-stu-id="f540f-696">Port</span></span>
  * <span data-ttu-id="f540f-697">Back-end-poort</span><span class="sxs-lookup"><span data-stu-id="f540f-697">Back-end port</span></span>

  <span data-ttu-id="f540f-698">Bijvoorbeeld, als u toochange Hallo ASC's exemplaar standaardnummer van 00 too31 wilt, moet u toomake Hallo wijzigingen voor alle poorten die worden vermeld in tabel 1.</span><span class="sxs-lookup"><span data-stu-id="f540f-698">For example, if you want toochange hello default ASCS instance number from 00 too31, you need toomake hello changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="f540f-699">Hier volgt een voorbeeld van een update voor poort *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="f540f-699">Here's an example of an update for port *lbrule3200*.</span></span>

  ![Afbeelding 16: Hallo ASC's / SCS standaard load-balancingregels voor hello Azure interne load balancer wijzigen][sap-ha-guide-figure-3005]

  <span data-ttu-id="f540f-701">_**Afbeelding 16:** wijziging Hallo ASC's / SCS standaard load-balancingregels voor hello Azure interne load balancer_</span><span class="sxs-lookup"><span data-stu-id="f540f-701">_**Figure 16:** Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer_</span></span>

### <span data-ttu-id="f540f-702"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Windows virtuele machines toohello domein toevoegen</span><span class="sxs-lookup"><span data-stu-id="f540f-702"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines toohello domain</span></span>

<span data-ttu-id="f540f-703">Nadat u een statisch IP-adres toohello virtuele machines toegewezen, voegt u Hallo virtuele machines toohello domein toe.</span><span class="sxs-lookup"><span data-stu-id="f540f-703">After you assign a static IP address toohello virtual machines, add hello virtual machines toohello domain.</span></span>

![Afbeelding 17: Een virtuele machine tooa-domein toevoegen][sap-ha-guide-figure-3006]

<span data-ttu-id="f540f-705">_**Afbeelding 17:** een virtuele machine tooa domein toevoegen_</span><span class="sxs-lookup"><span data-stu-id="f540f-705">_**Figure 17:** Add a virtual machine tooa domain_</span></span>

### <span data-ttu-id="f540f-706"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Registervermeldingen op beide clusterknooppunten van Hallo SAP ASC's / SCS exemplaar toe te voegen</span><span class="sxs-lookup"><span data-stu-id="f540f-706"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance</span></span>

<span data-ttu-id="f540f-707">Azure Load Balancer heeft een interne load balancer die wordt gesloten verbindingen als Hallo verbindingen niet actief gedurende een bepaalde zijn time (niet-actieve time-out).</span><span class="sxs-lookup"><span data-stu-id="f540f-707">Azure Load Balancer has an internal load balancer that closes connections when hello connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="f540f-708">SAP werkprocessen in de wachtrij plaatsen van dialoogvenster exemplaren geopende verbindingen toohello SAP verwerken zodra Hallo eerste in de wachtrij plaatsen/in wachtrij behoeften toobe verzonden aanvragen.</span><span class="sxs-lookup"><span data-stu-id="f540f-708">SAP work processes in dialog instances open connections toohello SAP enqueue process as soon as hello first enqueue/dequeue request needs toobe sent.</span></span> <span data-ttu-id="f540f-709">Deze verbindingen meestal blijven tot stand gebrachte tot Hallo werkproces of Hallo in de wachtrij plaatsen proces opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="f540f-709">These connections usually remain established until hello work process or hello enqueue process restarts.</span></span> <span data-ttu-id="f540f-710">Echter, als Hallo verbinding gedurende een bepaalde tijd inactief is, hello Azure interne load balancer wordt gesloten Hallo verbindingen.</span><span class="sxs-lookup"><span data-stu-id="f540f-710">However, if hello connection is idle for a set period of time, hello Azure internal load balancer closes hello connections.</span></span> <span data-ttu-id="f540f-711">Dit geen probleem omdat Hallo SAP-werkproces toohello Hallo-wachtrij plaatsen verbindingsproces herstelt als het niet meer bestaat.</span><span class="sxs-lookup"><span data-stu-id="f540f-711">This isn't a problem because hello SAP work process reestablishes hello connection toohello enqueue process if it no longer exists.</span></span> <span data-ttu-id="f540f-712">Deze activiteiten zijn gedocumenteerd in Hallo developer traceringen SAP-processen, maar ze een grote hoeveelheid extra inhoud in deze traceringen maken.</span><span class="sxs-lookup"><span data-stu-id="f540f-712">These activities are documented in hello developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="f540f-713">Het is een goed idee toochange Hallo TCP/IP `KeepAliveTime` en `KeepAliveInterval` op beide clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="f540f-713">It's a good idea toochange hello TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="f540f-714">Deze wijzigingen in Hallo TCP/IP-parameters met SAP profiel parameters, dat wordt beschreven in artikel hello later worden gecombineerd.</span><span class="sxs-lookup"><span data-stu-id="f540f-714">Combine these changes in hello TCP/IP parameters with SAP profile parameters, described later in hello article.</span></span>

<span data-ttu-id="f540f-715">op beide clusterknooppunten Windows toevoegen tooadd registervermeldingen op beide clusterknooppunten van Hallo SAP ASC's / SCS instantie eerst deze registervermeldingen Windows voor SAP ASC's / SCS:</span><span class="sxs-lookup"><span data-stu-id="f540f-715">tooadd registry entries on both cluster nodes of hello SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="f540f-716">Pad</span><span class="sxs-lookup"><span data-stu-id="f540f-716">Path</span></span> | <span data-ttu-id="f540f-717">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="f540f-717">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="f540f-718">Naam variabele</span><span class="sxs-lookup"><span data-stu-id="f540f-718">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="f540f-719">Type variabele</span><span class="sxs-lookup"><span data-stu-id="f540f-719">Variable type</span></span> |<span data-ttu-id="f540f-720">REG_DWORD (decimaal)</span><span class="sxs-lookup"><span data-stu-id="f540f-720">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="f540f-721">Waarde</span><span class="sxs-lookup"><span data-stu-id="f540f-721">Value</span></span> |<span data-ttu-id="f540f-722">120000</span><span class="sxs-lookup"><span data-stu-id="f540f-722">120000</span></span> |
| <span data-ttu-id="f540f-723">Koppeling toodocumentation</span><span class="sxs-lookup"><span data-stu-id="f540f-723">Link toodocumentation</span></span> |[<span data-ttu-id="f540f-724">https://technet.Microsoft.com/en-us/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="f540f-724">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="f540f-725">_**Tabel 3:** wijziging Hallo eerste TCP/IP-parameter_</span><span class="sxs-lookup"><span data-stu-id="f540f-725">_**Table 3:** Change hello first TCP/IP parameter_</span></span>

<span data-ttu-id="f540f-726">Voegt u deze Windows-registervermeldingen op beide clusterknooppunten Windows voor SAP ASC's / SCS:</span><span class="sxs-lookup"><span data-stu-id="f540f-726">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="f540f-727">Pad</span><span class="sxs-lookup"><span data-stu-id="f540f-727">Path</span></span> | <span data-ttu-id="f540f-728">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="f540f-728">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="f540f-729">Naam variabele</span><span class="sxs-lookup"><span data-stu-id="f540f-729">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="f540f-730">Type variabele</span><span class="sxs-lookup"><span data-stu-id="f540f-730">Variable type</span></span> |<span data-ttu-id="f540f-731">REG_DWORD (decimaal)</span><span class="sxs-lookup"><span data-stu-id="f540f-731">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="f540f-732">Waarde</span><span class="sxs-lookup"><span data-stu-id="f540f-732">Value</span></span> |<span data-ttu-id="f540f-733">120000</span><span class="sxs-lookup"><span data-stu-id="f540f-733">120000</span></span> |
| <span data-ttu-id="f540f-734">Koppeling toodocumentation</span><span class="sxs-lookup"><span data-stu-id="f540f-734">Link toodocumentation</span></span> |[<span data-ttu-id="f540f-735">https://technet.Microsoft.com/en-us/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="f540f-735">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="f540f-736">_**Tabel 4:** wijziging Hallo tweede TCP/IP-parameter_</span><span class="sxs-lookup"><span data-stu-id="f540f-736">_**Table 4:** Change hello second TCP/IP parameter_</span></span>

<span data-ttu-id="f540f-737">**tooapply hello verandert, opnieuw opstarten van beide clusterknooppunten**.</span><span class="sxs-lookup"><span data-stu-id="f540f-737">**tooapply hello changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="f540f-738"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a>Een cluster met Windows Server Failover Clustering voor een SAP ASC's / SCS-instantie instellen</span><span class="sxs-lookup"><span data-stu-id="f540f-738"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="f540f-739">Instellen van een cluster met Windows Server Failover Clustering voor een SAP ASC's / SCS-exemplaar, moet deze taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f540f-739">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="f540f-740">Hallo clusterknooppunten in een clusterconfiguratie verzamelen</span><span class="sxs-lookup"><span data-stu-id="f540f-740">Collecting hello cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="f540f-741">Een cluster bestandsshare-witness configureren</span><span class="sxs-lookup"><span data-stu-id="f540f-741">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="f540f-742"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Hallo clusterknooppunten in een clusterconfiguratie verzamelen</span><span class="sxs-lookup"><span data-stu-id="f540f-742"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect hello cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="f540f-743">In Hallo functie toevoegen en de Wizard Functies toevoegen voor failover clustering tooboth clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="f540f-743">In hello Add Role and Features Wizard, add failover clustering tooboth cluster nodes.</span></span>
2.  <span data-ttu-id="f540f-744">Hallo failover-cluster instellen met behulp van Failoverclusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="f540f-744">Set up hello failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="f540f-745">Selecteer in Failoverclusterbeheer **Cluster maken**, en voegt u alleen Hallo naam van de eerste cluster hello, knooppunt A. Voeg het tweede knooppunt Hallo nog; het tweede knooppunt Hallo voegt u in een later stadium.</span><span class="sxs-lookup"><span data-stu-id="f540f-745">In Failover Cluster Manager, select **Create Cluster**, and then add only hello name of hello first cluster, node A. Do not add hello second node yet; you'll add hello second node in a later step.</span></span>

  ![Afbeelding 18: Hallo-server of de naam van de virtuele machine van de eerste clusterknooppunt Hallo toevoegen][sap-ha-guide-figure-3007]

  <span data-ttu-id="f540f-747">_**Afbeelding 18:** toevoegen Hallo server of de virtuele machine de naam van het eerste clusterknooppunt Hallo_</span><span class="sxs-lookup"><span data-stu-id="f540f-747">_**Figure 18:** Add hello server or virtual machine name of hello first cluster node_</span></span>

3.  <span data-ttu-id="f540f-748">Voer Hallo netwerknaam (virtuele host-naam) van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f540f-748">Enter hello network name (virtual host name) of hello cluster.</span></span>

  ![Afbeelding 19: Voer de clusternaam Hallo][sap-ha-guide-figure-3008]

  <span data-ttu-id="f540f-750">_**Afbeelding 19:** Enter Hallo clusternaam_</span><span class="sxs-lookup"><span data-stu-id="f540f-750">_**Figure 19:** Enter hello cluster name_</span></span>

4.  <span data-ttu-id="f540f-751">Nadat u Hallo cluster hebt gemaakt, voert u een clustervalidatietest.</span><span class="sxs-lookup"><span data-stu-id="f540f-751">After you've created hello cluster, run a cluster validation test.</span></span>

  ![Afbeelding van 20: Hallo cluster validatiecontrole uitvoeren][sap-ha-guide-figure-3009]

  <span data-ttu-id="f540f-753">_**Afbeelding van 20:** Hallo cluster validatiecontrole uitvoeren_</span><span class="sxs-lookup"><span data-stu-id="f540f-753">_**Figure 20:** Run hello cluster validation check_</span></span>

  <span data-ttu-id="f540f-754">U kunt waarschuwingen met betrekking tot schijven op dit moment in Hallo proces negeren.</span><span class="sxs-lookup"><span data-stu-id="f540f-754">You can ignore any warnings about disks at this point in hello process.</span></span> <span data-ttu-id="f540f-755">U voegt dat een bestandssharewitness en Hallo SIOS gedeelde schijven later.</span><span class="sxs-lookup"><span data-stu-id="f540f-755">You'll add a file share witness and hello SIOS shared disks later.</span></span> <span data-ttu-id="f540f-756">In dit stadium hoeft u geen tooworry over het hebben van een quorum.</span><span class="sxs-lookup"><span data-stu-id="f540f-756">At this stage, you don't need tooworry about having a quorum.</span></span>

  ![Afbeelding 21: Er is geen quorumschijf is gevonden.][sap-ha-guide-figure-3010]

  <span data-ttu-id="f540f-758">_**Afbeelding 21:** geen quorumschijf is gevonden_</span><span class="sxs-lookup"><span data-stu-id="f540f-758">_**Figure 21:** No quorum disk is found_</span></span>

  ![Afbeelding 22: Core cluster-bron moet een nieuw IP-adres][sap-ha-guide-figure-3011]

  <span data-ttu-id="f540f-760">_**Afbeelding 22:** Core cluster-bron moet een nieuw IP-adres_</span><span class="sxs-lookup"><span data-stu-id="f540f-760">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="f540f-761">Hallo IP-adres van Hallo core cluster-service wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f540f-761">Change hello IP address of hello core cluster service.</span></span> <span data-ttu-id="f540f-762">Hallo-cluster starten niet totdat u Hallo IP-adres van de clusterservice Hallo-core, wijzigt omdat Hallo IP-adres van de server Hallo tooone van knooppunten van de virtuele machine Hallo verwijst.</span><span class="sxs-lookup"><span data-stu-id="f540f-762">hello cluster can't start until you change hello IP address of hello core cluster service, because hello IP address of hello server points tooone of hello virtual machine nodes.</span></span> <span data-ttu-id="f540f-763">Dit doen op Hallo **eigenschappen** pagina van Hallo core cluster-service van IP-resource.</span><span class="sxs-lookup"><span data-stu-id="f540f-763">Do this on hello **Properties** page of hello core cluster service's IP resource.</span></span>

  <span data-ttu-id="f540f-764">Bijvoorbeeld, moeten we tooassign een IP-adres (in ons voorbeeld **10.0.0.42**) voor de naam van de virtuele host cluster Hallo **pr1-ASC's-vir**.</span><span class="sxs-lookup"><span data-stu-id="f540f-764">For example, we need tooassign an IP address (in our example, **10.0.0.42**) for hello cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![Afbeelding 23: In Hallo eigenschappen in het dialoogvenster Hallo IP-adres wijzigen][sap-ha-guide-figure-3012]

  <span data-ttu-id="f540f-766">_**Afbeelding 23:** In Hallo **eigenschappen** in het dialoogvenster, wijziging Hallo IP-adres_</span><span class="sxs-lookup"><span data-stu-id="f540f-766">_**Figure 23:** In hello **Properties** dialog box, change hello IP address_</span></span>

  ![Afbeelding 24: Hallo IP-adres dat is gereserveerd voor Hallo cluster toewijzen][sap-ha-guide-figure-3013]

  <span data-ttu-id="f540f-768">_**Afbeelding 24:** Hallo IP-adres dat is gereserveerd voor Hallo cluster toewijzen_</span><span class="sxs-lookup"><span data-stu-id="f540f-768">_**Figure 24:** Assign hello IP address that is reserved for hello cluster_</span></span>

6.  <span data-ttu-id="f540f-769">Hallo virtuele host clusternaam online brengen.</span><span class="sxs-lookup"><span data-stu-id="f540f-769">Bring hello cluster virtual host name online.</span></span>

  ![Afbeelding 25: Core de clusterservice actief is en uitgevoerd en Hello Corrigeer IP-adres][sap-ha-guide-figure-3014]

  <span data-ttu-id="f540f-771">_**Afbeelding 25:** core de clusterservice actief is en uitgevoerd, en met Hallo Corrigeer IP-adres_</span><span class="sxs-lookup"><span data-stu-id="f540f-771">_**Figure 25:** Cluster core service is up and running, and with hello correct IP address_</span></span>

7.  <span data-ttu-id="f540f-772">De tweede clusterknooppunt Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f540f-772">Add hello second cluster node.</span></span>

  <span data-ttu-id="f540f-773">Nu Hallo core cluster-service actief is, kunt u de tweede clusterknooppunt Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f540f-773">Now that hello core cluster service is up and running, you can add hello second cluster node.</span></span>

  ![Afbeelding 26: Hallo tweede clusterknooppunt toevoegen][sap-ha-guide-figure-3015]

  <span data-ttu-id="f540f-775">_**Afbeelding 26:** toevoegen Hallo tweede clusterknooppunt_</span><span class="sxs-lookup"><span data-stu-id="f540f-775">_**Figure 26:** Add hello second cluster node_</span></span>

8.  <span data-ttu-id="f540f-776">Voer een naam voor Hallo tweede knooppunt clusterhost.</span><span class="sxs-lookup"><span data-stu-id="f540f-776">Enter a name for hello second cluster node host.</span></span>

  ![Afbeelding 27: Voer Hallo tweede hostnaam voor het clusterknooppunt][sap-ha-guide-figure-3016]

  <span data-ttu-id="f540f-778">_**Afbeelding 27:** Enter Hallo tweede hostnaam voor het clusterknooppunt_</span><span class="sxs-lookup"><span data-stu-id="f540f-778">_**Figure 27:** Enter hello second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="f540f-779">Zorg dat Hallo **Voeg alle in aanmerking komende opslag toohello cluster** selectievakje **niet** geselecteerde.</span><span class="sxs-lookup"><span data-stu-id="f540f-779">Be sure that hello **Add all eligible storage toohello cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Afbeelding 28: Schakel niet Hallo selectievakje][sap-ha-guide-figure-3017]

  <span data-ttu-id="f540f-781">_**Afbeelding 28:** doen **niet** Selecteer Hallo selectievakje_</span><span class="sxs-lookup"><span data-stu-id="f540f-781">_**Figure 28:** Do **not** select hello check box_</span></span>

  <span data-ttu-id="f540f-782">U kunt waarschuwingen over quorum en schijven negeren.</span><span class="sxs-lookup"><span data-stu-id="f540f-782">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="f540f-783">Stelt u Hallo quorum en -share Hallo schijf later, zoals beschreven in [SIOS DataKeeper Cluster Edition installeren voor de clusterschijf share SAP ASC's / SCS][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="f540f-783">You'll set hello quorum and share hello disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Afbeelding 29: Negeren van waarschuwingen over Hallo schijf quorum][sap-ha-guide-figure-3018]

  <span data-ttu-id="f540f-785">_**Afbeelding 29:** negeren van waarschuwingen over Hallo schijf quorum_</span><span class="sxs-lookup"><span data-stu-id="f540f-785">_**Figure 29:** Ignore warnings about hello disk quorum_</span></span>


#### <span data-ttu-id="f540f-786"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a>Een cluster bestandsshare-witness configureren</span><span class="sxs-lookup"><span data-stu-id="f540f-786"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="f540f-787">Een cluster bestandsshare-witness configureren, moet deze taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f540f-787">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="f540f-788">Een bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="f540f-788">Creating a file share</span></span>
- <span data-ttu-id="f540f-789">Instelling Hallo bestand bestandsshare-witness quorum in Failoverclusterbeheer</span><span class="sxs-lookup"><span data-stu-id="f540f-789">Setting hello file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="f540f-790"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a>Een bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="f540f-790"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="f540f-791">Selecteer een bestandssharewitness in plaats van een quorumschijf.</span><span class="sxs-lookup"><span data-stu-id="f540f-791">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="f540f-792">SIOS DataKeeper ondersteunt deze optie.</span><span class="sxs-lookup"><span data-stu-id="f540f-792">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="f540f-793">In Hallo voorbeelden in dit artikel is het Hallo bestandssharewitness op Hallo Active Directory en DNS-server die wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="f540f-793">In hello examples in this article, hello file share witness is on hello Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="f540f-794">Hallo bestandsshare-witness wordt aangeroepen **domcontr 0**.</span><span class="sxs-lookup"><span data-stu-id="f540f-794">hello file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="f540f-795">Omdat u zou een VPN-verbinding tooAzure (via Site-naar-Site VPN- of Azure ExpressRoute) hebt geconfigureerd, kunt u met uw Active Directory en DNS-service is on-premises en is niet geschikt toorun een bestand witness delen.</span><span class="sxs-lookup"><span data-stu-id="f540f-795">Because you would have configured a VPN connection tooAzure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable toorun a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f540f-796">Als uw Active Directory en DNS-service wordt uitgevoerd alleen lokale, niet de bestandsshare-witness configureren op Hallo Active Directory en DNS-Windows-besturingssysteem die lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f540f-796">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on hello Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="f540f-797">Netwerklatentie tussen clusterknooppunten uitgevoerd in Azure en Active Directory en DNS-on-premises mogelijk te groot zijn en leiden tot problemen met de netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="f540f-797">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="f540f-798">Worden ervoor tooconfigure Hallo bestandssharewitness op een virtuele machine van Azure met sluiten toohello clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="f540f-798">Be sure tooconfigure hello file share witness on an Azure virtual machine that is running close toohello cluster node.</span></span>  
  >
  >

  <span data-ttu-id="f540f-799">Hallo quorumstation moet ten minste 1024 MB vrije ruimte.</span><span class="sxs-lookup"><span data-stu-id="f540f-799">hello quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="f540f-800">We raden 2048 MB aan vrije ruimte voor Hallo quorum-station aan.</span><span class="sxs-lookup"><span data-stu-id="f540f-800">We recommend 2,048 MB of free space for hello quorum drive.</span></span>

2.  <span data-ttu-id="f540f-801">Hallo clusternaamobject toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f540f-801">Add hello cluster name object.</span></span>

  ![Afbeelding 30: Hallo-machtigingen op Hallo share voor Hallo clusternaamobject toewijzen][sap-ha-guide-figure-3019]

  <span data-ttu-id="f540f-803">_**Afbeelding 30:** Hallo-machtigingen op Hallo share voor Hallo clusternaamobject toewijzen_</span><span class="sxs-lookup"><span data-stu-id="f540f-803">_**Figure 30:** Assign hello permissions on hello share for hello cluster name object_</span></span>

  <span data-ttu-id="f540f-804">Zorg dat Hallo machtigingen Hallo autoriteit toochange gegevens in Hallo share voor Hallo clusternaamobject bevatten (in ons voorbeeld **pr1-ASC's-vir$**).</span><span class="sxs-lookup"><span data-stu-id="f540f-804">Be sure that hello permissions include hello authority toochange data in hello share for hello cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="f540f-805">tooadd hello cluster naam toohello objectenlijst, selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f540f-805">tooadd hello cluster name object toohello list, select **Add**.</span></span> <span data-ttu-id="f540f-806">Hallo filter toocheck voor computerobjecten in toevoeging toothose wordt weergegeven in afbeelding 31 wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f540f-806">Change hello filter toocheck for computer objects, in addition toothose shown in Figure 31.</span></span>

  ![Afbeelding 31: Hallo objecttypen tooinclude computers wijzigen][sap-ha-guide-figure-3020]

  <span data-ttu-id="f540f-808">_**Afbeelding 31:** Hallo objecttypen tooinclude computers wijzigen_</span><span class="sxs-lookup"><span data-stu-id="f540f-808">_**Figure 31:** Change hello Object Types tooinclude computers_</span></span>

  ![Afbeelding 32: Selectievakje Hallo Computers][sap-ha-guide-figure-3021]

  <span data-ttu-id="f540f-810">_**Afbeelding 32:** Selecteer Hallo **Computers** selectievakje_</span><span class="sxs-lookup"><span data-stu-id="f540f-810">_**Figure 32:** Select hello **Computers** check box_</span></span>

4.  <span data-ttu-id="f540f-811">Voer Hallo clusternaamobject zoals in afbeelding 31.</span><span class="sxs-lookup"><span data-stu-id="f540f-811">Enter hello cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="f540f-812">Omdat Hallo record al is gemaakt, kunt u Hallo-machtigingen kunt wijzigen, zoals wordt weergegeven in afbeelding 30.</span><span class="sxs-lookup"><span data-stu-id="f540f-812">Because hello record has already been created, you can change hello permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="f540f-813">Selecteer Hallo **beveiliging** tabblad van het Hallo-share- en vervolgens moet u meer gedetailleerde machtigingen voor Hallo clusternaamobject.</span><span class="sxs-lookup"><span data-stu-id="f540f-813">Select hello **Security** tab of hello share, and then set more detailed permissions for hello cluster name object.</span></span>

  ![Afbeelding 33: Hallo beveiligingskenmerken instellen voor clusternaamobject Hallo Hallo file share quorum][sap-ha-guide-figure-3022]

  <span data-ttu-id="f540f-815">_**Afbeelding 33:** Hallo beveiligingskenmerken instellen voor clusternaamobject Hallo Hallo file share quorum_</span><span class="sxs-lookup"><span data-stu-id="f540f-815">_**Figure 33:** Set hello security attributes for hello cluster name object on hello file share quorum_</span></span>

##### <span data-ttu-id="f540f-816"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Set Hallo bestand bestandsshare-witness quorum in Failoverclusterbeheer</span><span class="sxs-lookup"><span data-stu-id="f540f-816"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set hello file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="f540f-817">Open Hallo Wizard configureren Quorum-instelling.</span><span class="sxs-lookup"><span data-stu-id="f540f-817">Open hello Configure Quorum Setting Wizard.</span></span>

  ![Afbeelding 34: Start Hallo Wizard instelling clusterquorum configureren][sap-ha-guide-figure-3023]

  <span data-ttu-id="f540f-819">_**Afbeelding 34:** Start de Wizard clusterquorum configureren instelling Hallo_</span><span class="sxs-lookup"><span data-stu-id="f540f-819">_**Figure 34:** Start hello Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="f540f-820">Op Hallo **quorumconfiguratie selecteren** pagina **hello quorumwitness selecteren**.</span><span class="sxs-lookup"><span data-stu-id="f540f-820">On hello **Select Quorum Configuration** page, select **Select hello quorum witness**.</span></span>

  ![Afbeelding 35: Quorumconfiguraties u kunt kiezen uit][sap-ha-guide-figure-3024]

  <span data-ttu-id="f540f-822">_**Afbeelding 35:** quorumconfiguraties kunt u kiezen uit_</span><span class="sxs-lookup"><span data-stu-id="f540f-822">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="f540f-823">Op Hallo **Quorumwitness selecteren** pagina **een bestandssharewitness configureren**.</span><span class="sxs-lookup"><span data-stu-id="f540f-823">On hello **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![Afbeelding 36: Selecteer Hallo bestandsshare-witness][sap-ha-guide-figure-3025]

  <span data-ttu-id="f540f-825">_**Afbeelding 36:** Hallo bestandssharewitness selecteren_</span><span class="sxs-lookup"><span data-stu-id="f540f-825">_**Figure 36:** Select hello file share witness_</span></span>

4.  <span data-ttu-id="f540f-826">Voer Hallo UNC-pad toohello bestandsshare (in ons voorbeeld \\domcontr 0\FSW).</span><span class="sxs-lookup"><span data-stu-id="f540f-826">Enter hello UNC path toohello file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="f540f-827">een lijst met Hallo wijzigingen kunt u, selecteer toosee **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f540f-827">toosee a list of hello changes you can make, select **Next**.</span></span>

  ![Afbeelding 37: Hallo bestandsshare-locatie voor de witness-share Hallo definiëren][sap-ha-guide-figure-3026]

  <span data-ttu-id="f540f-829">_**Afbeelding 37:** Hallo bestandsshare-locatie voor de witness-share Hallo definiëren_</span><span class="sxs-lookup"><span data-stu-id="f540f-829">_**Figure 37:** Define hello file share location for hello witness share_</span></span>

5.  <span data-ttu-id="f540f-830">Selecteer Hallo wijzigingen die u wilt en selecteer vervolgens **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f540f-830">Select hello changes you want, and then select **Next**.</span></span> <span data-ttu-id="f540f-831">U moet toosuccessfully Hallo clusterconfiguratie configureren zoals wordt weergegeven in afbeelding 38.</span><span class="sxs-lookup"><span data-stu-id="f540f-831">You need toosuccessfully reconfigure hello cluster configuration as shown in Figure 38.</span></span>  

  ![Afbeelding 38: Bevestiging dat u opnieuw hebt geconfigureerd Hallo-cluster][sap-ha-guide-figure-3027]

  <span data-ttu-id="f540f-833">_**Afbeelding 38:** bevestiging dat u opnieuw hebt geconfigureerd Hallo-cluster_</span><span class="sxs-lookup"><span data-stu-id="f540f-833">_**Figure 38:** Confirmation that you've reconfigured hello cluster_</span></span>

<span data-ttu-id="f540f-834">Na de installatie is Windows Failover Cluster hello, moeten de wijzigingen toobe toosome drempelwaarden tooadapt failover detectie tooconditions aangebracht in Azure.</span><span class="sxs-lookup"><span data-stu-id="f540f-834">After installing hello Windows Failover Cluster successfully, changes need toobe made toosome thresholds tooadapt failover detection tooconditions in Azure.</span></span> <span data-ttu-id="f540f-835">Hallo parameters toobe gewijzigd, worden beschreven in deze blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/.</span><span class="sxs-lookup"><span data-stu-id="f540f-835">hello parameters toobe changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="f540f-836">Ervan uitgaande dat uw twee virtuele machines die bouwen Hallo zijn Windows Cluster-configuratie voor ASC's / SCS in hetzelfde SubNet hello, hello volgende parameters moeten toobe gewijzigd toothese waarden:</span><span class="sxs-lookup"><span data-stu-id="f540f-836">Assuming that your two VMs that build hello Windows Cluster Configuration for ASCS/SCS are in hello same SubNet, hello following parameters need toobe changed toothese values:</span></span>
- <span data-ttu-id="f540f-837">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="f540f-837">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="f540f-838">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="f540f-838">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="f540f-839">Deze instellingen zijn getest met klanten en een goede inbreuk toobe robuust genoeg opgegeven Hallo-een-zijde.</span><span class="sxs-lookup"><span data-stu-id="f540f-839">These settings were tested with customers and provided a good compromise toobe resilient enough on hello one side.</span></span> <span data-ttu-id="f540f-840">Op Hallo daarentegen deze instellingen zijn bieden snel genoeg failover in een echte foutcondities op SAP-software of het knooppunt/VM-fout.</span><span class="sxs-lookup"><span data-stu-id="f540f-840">On hello other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="f540f-841"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>SIOS DataKeeper Cluster Edition voor Hallo SAP ASC's / SCS clusterschijf delen installeren</span><span class="sxs-lookup"><span data-stu-id="f540f-841"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="f540f-842">U hebt nu een werkende configuratie van Windows Server Failover Clustering in Azure.</span><span class="sxs-lookup"><span data-stu-id="f540f-842">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="f540f-843">Maar tooinstall een SAP ASC's / SCS-exemplaar, moet u een gedeelde schijf-resource.</span><span class="sxs-lookup"><span data-stu-id="f540f-843">But, tooinstall an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="f540f-844">U kunt Hallo gedeelde schijfbronnen die u nodig in Azure maken.</span><span class="sxs-lookup"><span data-stu-id="f540f-844">You cannot create hello shared disk resources you need in Azure.</span></span> <span data-ttu-id="f540f-845">SIOS DataKeeper Cluster Edition is een oplossing van derden, kunt u de schijfbronnen toocreate gedeeld.</span><span class="sxs-lookup"><span data-stu-id="f540f-845">SIOS DataKeeper Cluster Edition is a third-party solution you can use toocreate shared disk resources.</span></span>

<span data-ttu-id="f540f-846">Het installeren van SIOS DataKeeper Cluster Edition voor Hallo SAP ASC's / SCS omvat share clusterschijf deze taken:</span><span class="sxs-lookup"><span data-stu-id="f540f-846">Installing SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="f540f-847">Hallo .NET Framework 3.5 toevoegen</span><span class="sxs-lookup"><span data-stu-id="f540f-847">Adding hello .NET Framework 3.5</span></span>
- <span data-ttu-id="f540f-848">SIOS DataKeeper installeren</span><span class="sxs-lookup"><span data-stu-id="f540f-848">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="f540f-849">SIOS DataKeeper instellen</span><span class="sxs-lookup"><span data-stu-id="f540f-849">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="f540f-850"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Hallo .NET Framework 3.5 toevoegen</span><span class="sxs-lookup"><span data-stu-id="f540f-850"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add hello .NET Framework 3.5</span></span>
<span data-ttu-id="f540f-851">Hallo Microsoft .NET Framework 3.5 is niet automatisch geactiveerd of Windows Server 2012 R2 is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f540f-851">hello Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="f540f-852">Omdat SIOS DataKeeper Hallo .NET Framework toobe op alle knooppunten die u vereist op DataKeeper installeert, moet u Hallo .NET Framework 3.5 installeren op Hallo gastbesturingssysteem van alle virtuele machines in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f540f-852">Because SIOS DataKeeper requires hello .NET Framework toobe on all nodes that you install DataKeeper on, you must install hello .NET Framework 3.5 on hello guest operating system of all virtual machines in hello cluster.</span></span>

<span data-ttu-id="f540f-853">Er zijn twee manieren tooadd Hallo .NET Framework 3.5:</span><span class="sxs-lookup"><span data-stu-id="f540f-853">There are two ways tooadd hello .NET Framework 3.5:</span></span>

- <span data-ttu-id="f540f-854">Gebruik Wizard Hallo toevoegen functies en onderdelen in Windows zoals in afbeelding 39.</span><span class="sxs-lookup"><span data-stu-id="f540f-854">Use hello Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Afbeelding 39: Hallo .NET Framework 3.5 installeren met behulp van de Wizard Hallo toevoegen functies en onderdelen][sap-ha-guide-figure-3028]

  <span data-ttu-id="f540f-856">_**Afbeelding 39:** installeren Hallo .NET Framework 3.5 met behulp van de Wizard Hallo toevoegen functies en onderdelen_</span><span class="sxs-lookup"><span data-stu-id="f540f-856">_**Figure 39:** Install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

  ![Afbeelding 40: Installatie van de voortgangsbalk wanneer u Hallo .NET Framework 3.5 installeren met behulp van de Wizard Hallo toevoegen functies en onderdelen][sap-ha-guide-figure-3029]

  <span data-ttu-id="f540f-858">_**Afbeelding 40:** installatie van de voortgangsbalk wanneer u Hallo .NET Framework 3.5 installeren met behulp van de Wizard Hallo toevoegen functies en onderdelen_</span><span class="sxs-lookup"><span data-stu-id="f540f-858">_**Figure 40:** Installation progress bar when you install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="f540f-859">Gebruik Hallo opdrachtregelprogramma dism.exe.</span><span class="sxs-lookup"><span data-stu-id="f540f-859">Use hello command-line tool dism.exe.</span></span> <span data-ttu-id="f540f-860">Voor dit type installatie moet u tooaccess Hallo SxS-map op de installatiemedia voor Windows hello.</span><span class="sxs-lookup"><span data-stu-id="f540f-860">For this type of installation, you need tooaccess hello SxS directory on hello Windows installation media.</span></span> <span data-ttu-id="f540f-861">Typ bij een opdrachtprompt met verhoogde bevoegdheid:</span><span class="sxs-lookup"><span data-stu-id="f540f-861">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="f540f-862"><a name="dd41d5a2-8083-415b-9878-839652812102"></a>SIOS DataKeeper installeren</span><span class="sxs-lookup"><span data-stu-id="f540f-862"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="f540f-863">SIOS DataKeeper Cluster Edition installeren op elk knooppunt in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f540f-863">Install SIOS DataKeeper Cluster Edition on each node in hello cluster.</span></span> <span data-ttu-id="f540f-864">toocreate virtuele gedeelde opslag met SIOS DataKeeper, maakt u een gesynchroniseerde mirror en vervolgens simuleren gedeelde clusteropslag.</span><span class="sxs-lookup"><span data-stu-id="f540f-864">toocreate virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="f540f-865">Voordat u Hallo SIOS software installeert, maken de domeingebruiker Hallo **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="f540f-865">Before you install hello SIOS software, create hello domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="f540f-866">Hallo toevoegen **DataKeeperSvc** gebruiker toohello **lokale beheerder** groep op beide clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="f540f-866">Add hello **DataKeeperSvc** user toohello **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="f540f-867">tooinstall SIOS DataKeeper:</span><span class="sxs-lookup"><span data-stu-id="f540f-867">tooinstall SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="f540f-868">Hallo SIOS software installeren op beide clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="f540f-868">Install hello SIOS software on both cluster nodes.</span></span>

  ![SIOS installatieprogramma][sap-ha-guide-figure-3030]

  ![Afbeelding 41: Eerste pagina van Hallo SIOS DataKeeper installatie][sap-ha-guide-figure-3031]

  <span data-ttu-id="f540f-871">_**Afbeelding 41:** eerste pagina van Hallo SIOS DataKeeper installatie_</span><span class="sxs-lookup"><span data-stu-id="f540f-871">_**Figure 41:** First page of hello SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="f540f-872">Selecteer Hallo in het dialoogvenster wordt weergegeven in afbeelding 42 **Ja**.</span><span class="sxs-lookup"><span data-stu-id="f540f-872">In hello dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Afbeelding 42: DataKeeper informeert u dat een service wordt uitgeschakeld][sap-ha-guide-figure-3032]

  <span data-ttu-id="f540f-874">_**Afbeelding 42:** DataKeeper informeert u dat een service wordt uitgeschakeld_</span><span class="sxs-lookup"><span data-stu-id="f540f-874">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="f540f-875">Hallo in het dialoogvenster wordt weergegeven in afbeelding 43 wordt aangeraden dat u selecteert **domein of de Server account**.</span><span class="sxs-lookup"><span data-stu-id="f540f-875">In hello dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Afbeelding 43: Selectie van de de gebruiker voor SIOS DataKeeper][sap-ha-guide-figure-3033]

  <span data-ttu-id="f540f-877">_**Afbeelding 43:** gebruikersselectie voor SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="f540f-877">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="f540f-878">Voer Hallo account domeingebruikersnaam en wachtwoorden op dat u hebt gemaakt voor SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="f540f-878">Enter hello domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Afbeelding 44: Hallo domeingebruikersnaam en wachtwoord invoeren voor Hallo SIOS DataKeeper installatie][sap-ha-guide-figure-3034]

  <span data-ttu-id="f540f-880">_**Afbeelding 44:** Hallo domeingebruikersnaam en wachtwoord invoeren voor Hallo SIOS DataKeeper installatie_</span><span class="sxs-lookup"><span data-stu-id="f540f-880">_**Figure 44:** Enter hello domain user name and password for hello SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="f540f-881">De licentiesleutel Hallo voor uw exemplaar SIOS DataKeeper zoals in afbeelding 45 installeren.</span><span class="sxs-lookup"><span data-stu-id="f540f-881">Install hello license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Afbeelding 45: Voer uw licentiecode SIOS DataKeeper][sap-ha-guide-figure-3035]

  <span data-ttu-id="f540f-883">_**Afbeelding 45:** uw licentiesleutel SIOS DataKeeper invoeren_</span><span class="sxs-lookup"><span data-stu-id="f540f-883">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="f540f-884">Wanneer u wordt gevraagd, moet u Hallo virtuele machine opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="f540f-884">When prompted, restart hello virtual machine.</span></span>

#### <span data-ttu-id="f540f-885"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a>SIOS DataKeeper instellen</span><span class="sxs-lookup"><span data-stu-id="f540f-885"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="f540f-886">Nadat u SIOS DataKeeper op beide knooppunten hebt geïnstalleerd, moet u toostart Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="f540f-886">After you install SIOS DataKeeper on both nodes, you need toostart hello configuration.</span></span> <span data-ttu-id="f540f-887">Hallo-doel van Hallo-configuratie is toohave synchrone gegevensreplicatie tussen Hallo extra schijven tooeach van Hallo virtuele machines die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="f540f-887">hello goal of hello configuration is toohave synchronous data replication between hello additional disks attached tooeach of hello virtual machines.</span></span>

1.  <span data-ttu-id="f540f-888">Hallo DataKeeper beheer en hulpprogramma voor serverconfiguratie starten en selecteer vervolgens **verbinding maken met Server**.</span><span class="sxs-lookup"><span data-stu-id="f540f-888">Start hello DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="f540f-889">(In de afbeelding 46 deze optie is met een rode cirkel.)</span><span class="sxs-lookup"><span data-stu-id="f540f-889">(In Figure 46, this option is circled in red.)</span></span>

  ![46 afbeelding: De SIOS DataKeeper beheer en het hulpprogramma voor serverconfiguratie][sap-ha-guide-figure-3036]

  <span data-ttu-id="f540f-891">_**Afbeelding 46:** SIOS DataKeeper beheer en de configuratie-hulpprogramma_</span><span class="sxs-lookup"><span data-stu-id="f540f-891">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="f540f-892">Hallo naam invoeren of TCP/IP-adres van Hallo eerste knooppunt Hallo beheer en de configuratie-hulpprogramma moet verbinding maken, en, in een tweede stap van de tweede Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="f540f-892">Enter hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and, in a second step, hello second node.</span></span>

  ![Afbeelding 47: Insert Hallo naam of TCP/IP-adres van Hallo eerste knooppunt Hallo beheer en de configuratie-hulpprogramma moet verbinding maken, en in een tweede stap van het tweede knooppunt Hallo][sap-ha-guide-figure-3037]

  <span data-ttu-id="f540f-894">_**Afbeelding 47:** Insert Hallo naam of TCP/IP-adres van Hallo eerste knooppunt Hallo beheer en de configuratie-hulpprogramma verbinding moet maken, en in een tweede stap van het tweede knooppunt Hallo_</span><span class="sxs-lookup"><span data-stu-id="f540f-894">_**Figure 47:** Insert hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and in a second step, hello second node_</span></span>

3.  <span data-ttu-id="f540f-895">Hallo replicatie taak tussen twee knooppunten Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="f540f-895">Create hello replication job between hello two nodes.</span></span>

  ![Afbeelding van 48: Een replicatie-taak maken][sap-ha-guide-figure-3038]

  <span data-ttu-id="f540f-897">_**Afbeelding van 48:** een replicatie-taak maken_</span><span class="sxs-lookup"><span data-stu-id="f540f-897">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="f540f-898">Een wizard leidt u door het Hallo-proces voor het maken van een taak voor replicatie.</span><span class="sxs-lookup"><span data-stu-id="f540f-898">A wizard guides you through hello process of creating a replication job.</span></span>
4.  <span data-ttu-id="f540f-899">Hallo-naam, de TCP/IP-adres en de schijfvolume van het bronknooppunt Hallo definiëren.</span><span class="sxs-lookup"><span data-stu-id="f540f-899">Define hello name, TCP/IP address, and disk volume of hello source node.</span></span>

  ![Afbeelding 49: Hallo-naam van Hallo replicatie taak definiëren][sap-ha-guide-figure-3039]

  <span data-ttu-id="f540f-901">_**Afbeelding 49:** definiëren Hallo-naam van Hallo replicatie taak_</span><span class="sxs-lookup"><span data-stu-id="f540f-901">_**Figure 49:** Define hello name of hello replication job_</span></span>

  ![Afbeelding 50: Basisgegevens voor Hallo-knooppunt, de huidige bronknooppunt Hallo moet Hallo definiëren][sap-ha-guide-figure-3040]

  <span data-ttu-id="f540f-903">_**Afbeelding 50:** basisgegevens voor Hallo-knooppunt, de huidige bronknooppunt Hallo moet Hallo definiëren_</span><span class="sxs-lookup"><span data-stu-id="f540f-903">_**Figure 50:** Define hello base data for hello node, which should be hello current source node_</span></span>

5.  <span data-ttu-id="f540f-904">Hallo-naam, de TCP/IP-adres en de schijfvolume van het doelknooppunt Hallo definiëren.</span><span class="sxs-lookup"><span data-stu-id="f540f-904">Define hello name, TCP/IP address, and disk volume of hello target node.</span></span>

  ![Afbeelding 51: Basisgegevens voor Hallo-knooppunt, de huidige doelknooppunt Hallo moet Hallo definiëren][sap-ha-guide-figure-3041]

  <span data-ttu-id="f540f-906">_**Afbeelding 51:** basisgegevens voor Hallo-knooppunt, de huidige doelknooppunt Hallo moet Hallo definiëren_</span><span class="sxs-lookup"><span data-stu-id="f540f-906">_**Figure 51:** Define hello base data for hello node, which should be hello current target node_</span></span>

6.  <span data-ttu-id="f540f-907">Hallo compressie algoritmen definiëren.</span><span class="sxs-lookup"><span data-stu-id="f540f-907">Define hello compression algorithms.</span></span> <span data-ttu-id="f540f-908">In ons voorbeeld is het raadzaam dat u Hallo replicatiestroom comprimeren.</span><span class="sxs-lookup"><span data-stu-id="f540f-908">In our example, we recommend that you compress hello replication stream.</span></span> <span data-ttu-id="f540f-909">Met name in situaties hersynchronisatie minder Hallo-compressie van Hallo replicatiestroom aanzienlijk hersynchronisatie-tijd.</span><span class="sxs-lookup"><span data-stu-id="f540f-909">Especially in resynchronization situations, hello compression of hello replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="f540f-910">Houd er rekening mee dat compressie Hallo CPU en RAM-geheugen van een virtuele machine verbruikt.</span><span class="sxs-lookup"><span data-stu-id="f540f-910">Note that compression uses hello CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="f540f-911">Als Hallo compressie snelheid toeneemt, dus Hallo volume aan CPU-resources die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f540f-911">As hello compression rate increases, so does hello volume of CPU resources used.</span></span> <span data-ttu-id="f540f-912">Ook kunt u aanpassen deze instelling later.</span><span class="sxs-lookup"><span data-stu-id="f540f-912">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="f540f-913">Een andere instelling die u moet toocheck is of Hallo replicatie synchroon of asynchroon.</span><span class="sxs-lookup"><span data-stu-id="f540f-913">Another setting you need toocheck is whether hello replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="f540f-914">*Wanneer u SAP ASC's / SCS configuraties beveiligt, moet u synchrone replicatie*.</span><span class="sxs-lookup"><span data-stu-id="f540f-914">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Afbeelding 52: Replicatiedetails definiëren][sap-ha-guide-figure-3042]

  <span data-ttu-id="f540f-916">_**Afbeelding 52:** replicatiedetails definiëren_</span><span class="sxs-lookup"><span data-stu-id="f540f-916">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="f540f-917">Definieer of Hallo volume die is gerepliceerd door Hallo taak vertegenwoordigde tooa Windows Server Failover Clustering clusterconfiguratie als gedeelde schijf moet zijn.</span><span class="sxs-lookup"><span data-stu-id="f540f-917">Define whether hello volume that is replicated by hello replication job should be represented tooa Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="f540f-918">Hallo SAP ASC's / SCS configuratie, selecteert u **Ja** zodat Hallo Windows cluster ziet Hallo gerepliceerde volume als een gedeelde schijf die kan worden gebruikt als een clustervolume.</span><span class="sxs-lookup"><span data-stu-id="f540f-918">For hello SAP ASCS/SCS configuration, select **Yes** so that hello Windows cluster sees hello replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![Afbeelding 53: Selecteer Ja tooset Hallo gerepliceerd volume als een clustervolume][sap-ha-guide-figure-3043]

  <span data-ttu-id="f540f-920">_**Afbeelding 53:** Selecteer **Ja** tooset Hallo gerepliceerd volume als een clustervolume_</span><span class="sxs-lookup"><span data-stu-id="f540f-920">_**Figure 53:** Select **Yes** tooset hello replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="f540f-921">Nadat Hallo volume is gemaakt, ziet u Hallo DataKeeper beheer en de configuratie-hulpprogramma dat taak Hallo-replicatie is actief.</span><span class="sxs-lookup"><span data-stu-id="f540f-921">After hello volume is created, hello DataKeeper Management and Configuration tool shows that hello replication job is active.</span></span>

  ![Afbeelding 54: Synchroon spiegelen van DataKeeper voor Hallo SAP ASC's / SCS share schijf actief is.][sap-ha-guide-figure-3044]

  <span data-ttu-id="f540f-923">_**Afbeelding 54:** DataKeeper synchroon spiegelen voor hello SAP ASC's / SCS schijf delen is actief_</span><span class="sxs-lookup"><span data-stu-id="f540f-923">_**Figure 54:** DataKeeper synchronous mirroring for hello SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="f540f-924">Hallo-schijf als een schijf DataKeeper weergegeven Failoverclusterbeheer nu zoals in afbeelding 55.</span><span class="sxs-lookup"><span data-stu-id="f540f-924">Failover Cluster Manager now shows hello disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![Afbeelding 55: Failover Cluster Manager toont Hallo-schijf die DataKeeper gerepliceerd][sap-ha-guide-figure-3045]

  <span data-ttu-id="f540f-926">_**Afbeelding 55:** Failover Cluster Manager toont Hallo schijf die is gerepliceerd DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="f540f-926">_**Figure 55:** Failover Cluster Manager shows hello disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="f540f-927"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Hallo SAP NetWeaver systeem installeert</span><span class="sxs-lookup"><span data-stu-id="f540f-927"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install hello SAP NetWeaver system</span></span>

<span data-ttu-id="f540f-928">Hallo DBMS setup won't worden beschreven omdat instellingen variëren, afhankelijk van Hallo DBMS systeem u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f540f-928">We won’t describe hello DBMS setup because setups vary depending on hello DBMS system you use.</span></span> <span data-ttu-id="f540f-929">Echter, gaan we ervan uit dat hoge beschikbaarheid weergegeven met de Hallo DBMS worden aangepakt met Hallo functionaliteiten Hallo verschillende DBMS leveranciers ondersteuning voor Azure.</span><span class="sxs-lookup"><span data-stu-id="f540f-929">However, we assume that high-availability concerns with hello DBMS are addressed with hello functionalities hello different DBMS vendors support for Azure.</span></span> <span data-ttu-id="f540f-930">Bijvoorbeeld altijd op of database mirroring voor SQL Server en Oracle Data Guard voor Oracle-databases.</span><span class="sxs-lookup"><span data-stu-id="f540f-930">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="f540f-931">We toevoegen niet meer bescherming toohello DBMS in Hallo scenario we in dit artikel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f540f-931">In hello scenario we use in this article, we didn't add more protection toohello DBMS.</span></span>

<span data-ttu-id="f540f-932">Er zijn geen speciale overwegingen bij verschillende DBMS services met dit soort clusterconfiguratie SAP ASC's / SCS in Azure communiceren.</span><span class="sxs-lookup"><span data-stu-id="f540f-932">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="f540f-933">Hallo installatieprocedures van SAP NetWeaver ABAP systemen, Java-systemen en ABAP + Java systemen zijn bijna identiek.</span><span class="sxs-lookup"><span data-stu-id="f540f-933">hello installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="f540f-934">Hallo belangrijkste verschil is dat een SAP ABAP systeem een exemplaar van de ASC's heeft.</span><span class="sxs-lookup"><span data-stu-id="f540f-934">hello most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="f540f-935">Hallo SAP Java systeem heeft een SCS-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f540f-935">hello SAP Java system has one SCS instance.</span></span> <span data-ttu-id="f540f-936">Hallo SAP ABAP + Java systeem heeft een exemplaar van de ASC's en één SCS-exemplaar in Hallo dezelfde Microsoft failover cluster-groep.</span><span class="sxs-lookup"><span data-stu-id="f540f-936">hello SAP ABAP+Java system has one ASCS instance and one SCS instance running in hello same Microsoft failover cluster group.</span></span> <span data-ttu-id="f540f-937">Eventuele verschillen installatie voor elke installatie SAP NetWeaver stack worden expliciet vermeld.</span><span class="sxs-lookup"><span data-stu-id="f540f-937">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="f540f-938">Alle andere onderdelen zijn dezelfde hello, kunt u aannemen.</span><span class="sxs-lookup"><span data-stu-id="f540f-938">You can assume that all other parts are hello same.</span></span>  
>
>

### <span data-ttu-id="f540f-939"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a>SAP installeren met een hoge beschikbaarheid ASC's / SCS-exemplaar</span><span class="sxs-lookup"><span data-stu-id="f540f-939"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f540f-940">Zorg ervoor dat geen tooplace uw pagina bestand op DataKeeper gespiegelde volumes.</span><span class="sxs-lookup"><span data-stu-id="f540f-940">Be sure not tooplace your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="f540f-941">DataKeeper biedt geen ondersteuning voor gespiegelde volumes.</span><span class="sxs-lookup"><span data-stu-id="f540f-941">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="f540f-942">U kunt uw wisselbestand op Hallo tijdelijke station D van een virtuele machine van Azure, laten Hallo standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="f540f-942">You can leave your page file on hello temporary drive D of an Azure virtual machine, which is hello default.</span></span> <span data-ttu-id="f540f-943">Als deze nog niet is gebeurd, verplaatst u Hallo Windows pagina bestand toodrive D: van uw Azure-machine.</span><span class="sxs-lookup"><span data-stu-id="f540f-943">If it's not already there, move hello Windows page file toodrive D: of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="f540f-944">SAP installeren met een exemplaar van de ASC's / SCS hoge beschikbaarheid, moet deze taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f540f-944">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="f540f-945">Maken van een virtuele host-naam voor geclusterde Hallo SAP ASC's / SCS exemplaar</span><span class="sxs-lookup"><span data-stu-id="f540f-945">Creating a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="f540f-946">Eerste Hallo SAP-clusterknooppunt installeren</span><span class="sxs-lookup"><span data-stu-id="f540f-946">Installing hello SAP first cluster node</span></span>
- <span data-ttu-id="f540f-947">Hallo SAP-profiel van Hallo ASC's / SCS-exemplaar wijzigen</span><span class="sxs-lookup"><span data-stu-id="f540f-947">Modifying hello SAP profile of hello ASCS/SCS instance</span></span>
- <span data-ttu-id="f540f-948">Een testpoort toevoegen</span><span class="sxs-lookup"><span data-stu-id="f540f-948">Adding a probe port</span></span>
- <span data-ttu-id="f540f-949">Hallo Windows firewall-testpoort openen</span><span class="sxs-lookup"><span data-stu-id="f540f-949">Opening hello Windows firewall probe port</span></span>

#### <span data-ttu-id="f540f-950"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Een virtuele host-naam voor geclusterde Hallo SAP ASC's / SCS exemplaar maken</span><span class="sxs-lookup"><span data-stu-id="f540f-950"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="f540f-951">Maak een DNS-vermelding voor de naam van de virtuele host Hallo van Hallo ASC's / SCS exemplaar in Hallo Windows DNS-beheer.</span><span class="sxs-lookup"><span data-stu-id="f540f-951">In hello Windows DNS manager, create a DNS entry for hello virtual host name of hello ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="f540f-952">Hallo IP-adres dat u de naam van de virtuele host toohello Hallo ASC's / SCS-exemplaar moet toewijzen Hallo dezelfde als Hallo IP-adres dat aan u toegewezen tooAzure Load Balancer (**<*SID*> - lb - ASC's **).</span><span class="sxs-lookup"><span data-stu-id="f540f-952">hello IP address that you assign toohello virtual host name of hello ASCS/SCS instance must be hello same as hello IP address that you assigned tooAzure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="f540f-953">Hallo IP-adres van de virtuele SAP ASC's / SCS Hallo-hostnaam (**pr1 ASC's sap**) is dezelfde als Hallo IP-adres van de Load Balancer van Azure Hallo (**pr1-lb-ASC's**).</span><span class="sxs-lookup"><span data-stu-id="f540f-953">hello IP address of hello virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is hello same as hello IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Afbeelding 56: Definieer Hallo DNS-vermelding voor de virtuele clusternaam Hallo SAP ASC's / SCS en TCP/IP-adres][sap-ha-guide-figure-3046]

  <span data-ttu-id="f540f-955">_**Afbeelding 56:** Hallo DNS-vermelding voor de virtuele clusternaam Hallo SAP ASC's / SCS en TCP/IP-adres definiëren_</span><span class="sxs-lookup"><span data-stu-id="f540f-955">_**Figure 56:** Define hello DNS entry for hello SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="f540f-956">toodefine hello IP-adres is toegewezen toohello naam virtuele host op, selecteer **DNS-beheer** > **domein**.</span><span class="sxs-lookup"><span data-stu-id="f540f-956">toodefine hello IP address assigned toohello virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![57 afbeelding: De nieuwe virtuele naam en het TCP/IP-adres voor de clusterconfiguratie SAP ASC's / SCS][sap-ha-guide-figure-3047]

  <span data-ttu-id="f540f-958">_**Afbeelding 57:** nieuwe virtuele naam en het TCP/IP-adres voor SAP ASC's / SCS-clusterconfiguratie_</span><span class="sxs-lookup"><span data-stu-id="f540f-958">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="f540f-959"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Eerste Hallo SAP-clusterknooppunt installeren</span><span class="sxs-lookup"><span data-stu-id="f540f-959"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install hello SAP first cluster node</span></span>

1.  <span data-ttu-id="f540f-960">Hallo eerste cluster knooppunt optie op clusterknooppunt A. uitvoeren Bijvoorbeeld: op Hallo **pr1-ASC's-0** host.</span><span class="sxs-lookup"><span data-stu-id="f540f-960">Execute hello first cluster node option on cluster node A. For example, on hello **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="f540f-961">tookeep Hallo-standaardpoorten voor hello Azure interne load balancer, selecteren:</span><span class="sxs-lookup"><span data-stu-id="f540f-961">tookeep hello default ports for hello Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="f540f-962">**ABAP system**: **ASC's** exemplaar nummer **00**</span><span class="sxs-lookup"><span data-stu-id="f540f-962">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="f540f-963">**Java-systeem**: **SCS** exemplaar nummer **01**</span><span class="sxs-lookup"><span data-stu-id="f540f-963">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="f540f-964">**ABAP + Java system**: **ASC's** exemplaar nummer **00** en **SCS** exemplaar nummer **01**</span><span class="sxs-lookup"><span data-stu-id="f540f-964">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="f540f-965">toouse exemplaar getallen andere dan 00 voor Hallo ABAP ASCS exemplaar en 01 voor Hallo Java SCS exemplaar, moet u eerst toochange hello Azure interne load balancer standaard load-balancingregels beschreven in [wijziging Hallo ASC's / SCS standaard laden regels voor hello Azure interne load balancer Balancing][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="f540f-965">toouse instance numbers other than 00 for hello ABAP ASCS instance and 01 for hello Java SCS instance, first you need toochange hello Azure internal load balancer default load balancing rules, described in [Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="f540f-966">Hello worden niet volgende enkele taken beschreven in Hallo standaard SAP documentatie voor de installatie.</span><span class="sxs-lookup"><span data-stu-id="f540f-966">hello next few tasks aren't described in hello standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="f540f-967">Hallo SAP installatie documentatie wordt beschreven hoe tooinstall Hallo eerste ASC's / SCS-clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="f540f-967">hello SAP installation documentation describes how tooinstall hello first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="f540f-968"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Hallo SAP-profiel van Hallo ASC's / SCS-exemplaar wijzigen</span><span class="sxs-lookup"><span data-stu-id="f540f-968"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify hello SAP profile of hello ASCS/SCS instance</span></span>

<span data-ttu-id="f540f-969">U moet een nieuwe profiel-parameter tooadd.</span><span class="sxs-lookup"><span data-stu-id="f540f-969">You need tooadd a new profile parameter.</span></span> <span data-ttu-id="f540f-970">Hallo profiel parameter voorkomt dat verbindingen tussen processen SAP en Hallo in de wachtrij plaatsen server af te sluiten wanneer ze niet actief is te lang zijn.</span><span class="sxs-lookup"><span data-stu-id="f540f-970">hello profile parameter prevents connections between SAP work processes and hello enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="f540f-971">Gezegd Hallo probleem scenario in [registervermeldingen toe te voegen op beide clusterknooppunten van Hallo SAP ASC's / SCS exemplaar][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="f540f-971">We mentioned hello problem scenario in [Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="f540f-972">In deze sectie geïntroduceerd we ook twee wijzigingen toosome eenvoudige TCP/IP-verbindingsparameters.</span><span class="sxs-lookup"><span data-stu-id="f540f-972">In that section, we also introduced two changes toosome basic TCP/IP connection parameters.</span></span> <span data-ttu-id="f540f-973">In een tweede stap moet u tooset Hallo in de wachtrij plaatsen server toosend een `keep_alive` signaal zodat Hallo verbindingen niet hello Azure interne load balancer niet-actieve drempelwaarde bereikt.</span><span class="sxs-lookup"><span data-stu-id="f540f-973">In a second step, you need tooset hello enqueue server toosend a `keep_alive` signal so that hello connections don't hit hello Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="f540f-974">toomodify hello SAP-profiel van Hallo ASC's / SCS exemplaar:</span><span class="sxs-lookup"><span data-stu-id="f540f-974">toomodify hello SAP profile of hello ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="f540f-975">Dit profiel parameter toohello SAP ASC's / SCS exemplaar profiel toevoegen:</span><span class="sxs-lookup"><span data-stu-id="f540f-975">Add this profile parameter toohello SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="f540f-976">In ons voorbeeld Hallo pad als volgt:</span><span class="sxs-lookup"><span data-stu-id="f540f-976">In our example, hello path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="f540f-977">Bijvoorbeeld toohello SAP SCS exemplaar profiel en het bijbehorende pad:</span><span class="sxs-lookup"><span data-stu-id="f540f-977">For example, toohello SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="f540f-978">tooapply hello wijzigingen, Hallo SAP ASC's /SCS exemplaar opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="f540f-978">tooapply hello changes, restart hello SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="f540f-979"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a>Een testpoort toevoegen</span><span class="sxs-lookup"><span data-stu-id="f540f-979"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="f540f-980">Hallo interne load balancer-test functionaliteit toomake Hallo clusteroplossing configuratiewerk gebruiken met Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="f540f-980">Use hello internal load balancer's probe functionality toomake hello entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="f540f-981">Hello Azure interne load balancer distribueert meestal Hallo binnenkomende werkbelasting gelijkmatig tussen deelnemende virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f540f-981">hello Azure internal load balancer usually distributes hello incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="f540f-982">Echter werkt dat niet in bepaalde clusterconfiguraties omdat er slechts één exemplaar actief is.</span><span class="sxs-lookup"><span data-stu-id="f540f-982">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="f540f-983">Hallo andere exemplaar is passieve en kan niet alle Hallo werkbelasting accepteren.</span><span class="sxs-lookup"><span data-stu-id="f540f-983">hello other instance is passive and can’t accept any of hello workload.</span></span> <span data-ttu-id="f540f-984">Een test-functionaliteit helpt wanneer hello Azure interne load balancer wordt toegewezen alleen tooan actieve sessie werkt.</span><span class="sxs-lookup"><span data-stu-id="f540f-984">A probe functionality helps when hello Azure internal load balancer assigns work only tooan active instance.</span></span> <span data-ttu-id="f540f-985">Hallo interne load balancer kan met Hallo test functionaliteit detecteren welke exemplaren actief zijn en vervolgens de doelinstantie alleen Hallo met Hallo werklast.</span><span class="sxs-lookup"><span data-stu-id="f540f-985">With hello probe functionality, hello internal load balancer can detect which instances are active, and then target only hello instance with hello workload.</span></span>

<span data-ttu-id="f540f-986">tooadd een testpoort:</span><span class="sxs-lookup"><span data-stu-id="f540f-986">tooadd a probe port:</span></span>

1.  <span data-ttu-id="f540f-987">Controleer de huidige Hallo **ProbePort** instellen door het volgende PowerShell-opdracht Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f540f-987">Check hello current **ProbePort** setting by running hello following PowerShell command.</span></span> <span data-ttu-id="f540f-988">Deze niet binnen één Hallo virtuele machines worden uitgevoerd in Hallo clusterconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="f540f-988">Execute it from within one of hello virtual machines in hello cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="f540f-989">Definieer een testpoort.</span><span class="sxs-lookup"><span data-stu-id="f540f-989">Define a probe port.</span></span> <span data-ttu-id="f540f-990">Hallo test standaardpoortnummer is **0**.</span><span class="sxs-lookup"><span data-stu-id="f540f-990">hello default probe port number is **0**.</span></span> <span data-ttu-id="f540f-991">In ons voorbeeld gebruiken we de testpoort **62000**.</span><span class="sxs-lookup"><span data-stu-id="f540f-991">In our example, we use probe port **62000**.</span></span>

  ![Afbeelding 58: Hallo cluster configuratie de testpoort is 0 standaard][sap-ha-guide-figure-3048]

  <span data-ttu-id="f540f-993">_**Afbeelding 58:** Hallo cluster configuration test standaardpoort is 0_</span><span class="sxs-lookup"><span data-stu-id="f540f-993">_**Figure 58:** hello default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="f540f-994">Hallo-poortnummer is gedefinieerd in SAP Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="f540f-994">hello port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="f540f-995">U kunt Hallo poortnummer in PowerShell kunt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="f540f-995">You can assign hello port number in PowerShell.</span></span>

  <span data-ttu-id="f540f-996">een nieuwe ProbePort-waarde voor Hallo tooset  **SAP <*SID*> IP-** clusterbron, Hallo volgende PowerShell-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f540f-996">tooset a new ProbePort value for hello **SAP <*SID*> IP** cluster resource, run hello following PowerShell script.</span></span> <span data-ttu-id="f540f-997">Hallo PowerShell variabelen voor uw omgeving bijwerken.</span><span class="sxs-lookup"><span data-stu-id="f540f-997">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="f540f-998">Nadat het Hallo-script wordt uitgevoerd, moet u na vragen aan gebruiker toorestart Hallo SAP cluster tooactivate Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="f540f-998">After hello script runs, you'll be prompted toorestart hello SAP cluster group tooactivate hello changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  <span data-ttu-id="f540f-999">Nadat u Hallo brengt  **SAP <*SID*> ** cluster online rol, Controleer **ProbePort** toohello nieuwe waarde is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f540f-999">After you bring hello **SAP <*SID*>** cluster role online, verify that **ProbePort** is set toohello new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Afbeelding 59: Test Hallo cluster poort nadat u de nieuwe waarde Hallo instellen][sap-ha-guide-figure-3049]

  <span data-ttu-id="f540f-1001">_**Afbeelding 59:** Probe Hallo cluster poort nadat u de nieuwe waarde Hallo instellen_</span><span class="sxs-lookup"><span data-stu-id="f540f-1001">_**Figure 59:** Probe hello cluster port after you set hello new value_</span></span>

#### <span data-ttu-id="f540f-1002"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Hallo Windows firewall-testpoort openen</span><span class="sxs-lookup"><span data-stu-id="f540f-1002"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open hello Windows firewall probe port</span></span>

<span data-ttu-id="f540f-1003">U moet een Windows firewall-test poort op beide clusterknooppunten tooopen.</span><span class="sxs-lookup"><span data-stu-id="f540f-1003">You need tooopen a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="f540f-1004">Gebruik Hallo script tooopen een test-poort van Windows firewall te volgen.</span><span class="sxs-lookup"><span data-stu-id="f540f-1004">Use hello following script tooopen a Windows firewall probe port.</span></span> <span data-ttu-id="f540f-1005">Hallo PowerShell variabelen voor uw omgeving bijwerken.</span><span class="sxs-lookup"><span data-stu-id="f540f-1005">Update hello PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="f540f-1006">Hallo **ProbePort** te is ingesteld,**62000**.</span><span class="sxs-lookup"><span data-stu-id="f540f-1006">hello **ProbePort** is set too**62000**.</span></span> <span data-ttu-id="f540f-1007">Nu u toegang hebt tot de bestandsshare Hallo  **\\\ascsha-clsap\sapmnt** met andere hosts, zoals als van **ascsha-DBA's**.</span><span class="sxs-lookup"><span data-stu-id="f540f-1007">Now you can access hello file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="f540f-1008"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Hallo-database-exemplaar installeren</span><span class="sxs-lookup"><span data-stu-id="f540f-1008"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install hello database instance</span></span>

<span data-ttu-id="f540f-1009">tooinstall hello database-exemplaar, voert u de Hallo-proces dat wordt beschreven in Hallo SAP-documentatie voor installatie.</span><span class="sxs-lookup"><span data-stu-id="f540f-1009">tooinstall hello database instance, follow hello process described in hello SAP installation documentation.</span></span>

### <span data-ttu-id="f540f-1010"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>De tweede clusterknooppunt Hallo installeren</span><span class="sxs-lookup"><span data-stu-id="f540f-1010"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install hello second cluster node</span></span>

<span data-ttu-id="f540f-1011">tooinstall hello tweede cluster, volg de stappen Hallo in Hallo SAP installatiehandleiding.</span><span class="sxs-lookup"><span data-stu-id="f540f-1011">tooinstall hello second cluster, follow hello steps in hello SAP installation guide.</span></span>

### <span data-ttu-id="f540f-1012"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Hallo het starttype Hallo SAP Ebruikers Windows service-exemplaar wijzigen</span><span class="sxs-lookup"><span data-stu-id="f540f-1012"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change hello start type of hello SAP ERS Windows service instance</span></span>

<span data-ttu-id="f540f-1013">Het starttype Hallo Hallo SAP Ebruikers Windows-service ook wijzigen**automatisch (vertraagd starten)** op beide clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="f540f-1013">Change hello start type of hello SAP ERS Windows service too**Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Afbeelding 60: Hallo servicetype voor Hallo SAP Ebruikers exemplaar toodelayed automatische wijzigen][sap-ha-guide-figure-3050]

<span data-ttu-id="f540f-1015">_**Afbeelding 60:** Hallo servicetype voor Hallo SAP Ebruikers exemplaar toodelayed automatische wijzigen_</span><span class="sxs-lookup"><span data-stu-id="f540f-1015">_**Figure 60:** Change hello service type for hello SAP ERS instance toodelayed automatic_</span></span>

### <span data-ttu-id="f540f-1016"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Hallo SAP primaire toepassingsserver installeren</span><span class="sxs-lookup"><span data-stu-id="f540f-1016"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install hello SAP Primary Application Server</span></span>

<span data-ttu-id="f540f-1017">Hallo primaire Application Server (PAS)-exemplaar installeren <*SID*> - di - 0 op Hallo virtuele machine die u hebt opgegeven toohost Hallo Pa's.</span><span class="sxs-lookup"><span data-stu-id="f540f-1017">Install hello Primary Application Server (PAS) instance <*SID*>-di-0 on hello virtual machine that you've designated toohost hello PAS.</span></span> <span data-ttu-id="f540f-1018">Er zijn geen afhankelijkheden op Azure of DataKeeper-specifieke instellingen.</span><span class="sxs-lookup"><span data-stu-id="f540f-1018">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="f540f-1019"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Hallo SAP aanvullende toepassingsserver installeren</span><span class="sxs-lookup"><span data-stu-id="f540f-1019"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install hello SAP Additional Application Server</span></span>

<span data-ttu-id="f540f-1020">Een SAP aanvullende Application Server (AAS) installeren op alle Hallo virtuele machines dat u hebt aangewezen toohost een SAP Application Server-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f540f-1020">Install an SAP Additional Application Server (AAS) on all hello virtual machines that you've designated toohost an SAP Application Server instance.</span></span> <span data-ttu-id="f540f-1021">Bijvoorbeeld: op <*SID*> - di - 1 te <*SID*> - di -&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="f540f-1021">For example, on <*SID*>-di-1 too<*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="f540f-1022">Dit is voltooid Hallo-installatie van een hoge beschikbaarheid SAP NetWeaver-systeem.</span><span class="sxs-lookup"><span data-stu-id="f540f-1022">This finishes hello installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="f540f-1023">Vervolgens gaat u verder met het testen van failover.</span><span class="sxs-lookup"><span data-stu-id="f540f-1023">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="f540f-1024"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Hallo SAP ASC's / SCS exemplaar failover en SIOS replicatie testen</span><span class="sxs-lookup"><span data-stu-id="f540f-1024"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test hello SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="f540f-1025">Het is gemakkelijk tootest en een SAP ASC's / SCS exemplaar failover en SIOS schijfreplicatie bewaken met behulp van Failoverclusterbeheer en Hallo SIOS DataKeeper beheer en de configuratie-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="f540f-1025">It's easy tootest and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and hello SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="f540f-1026"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a>SAP ASC's / SCS-exemplaar wordt uitgevoerd op een clusterknooppunt A</span><span class="sxs-lookup"><span data-stu-id="f540f-1026"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="f540f-1027">Hallo **SAP PR1** clustergroep wordt uitgevoerd op een clusterknooppunt A. Bijvoorbeeld: op **pr1-ASC's-0**.</span><span class="sxs-lookup"><span data-stu-id="f540f-1027">hello **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="f540f-1028">Toewijzen van gedeelde Hallo schijfstation S, die deel uitmaakt van Hallo **SAP PR1** cluster groep en welk Hallo ASC's / SCS-exemplaar gebruikt, toocluster knooppunt A.</span><span class="sxs-lookup"><span data-stu-id="f540f-1028">Assign hello shared disk drive S, which is part of hello **SAP PR1** cluster group, and which hello ASCS/SCS instance uses, toocluster node A.</span></span>

![Afbeelding 61: Failover Cluster Manager: Hallo SAP < SID > clustergroep wordt uitgevoerd op een clusterknooppunt A][sap-ha-guide-figure-5000]

<span data-ttu-id="f540f-1030">_**Afbeelding 61:** Failoverclusterbeheer: SAP Hallo <*SID*> clustergroep wordt uitgevoerd op een clusterknooppunt A_</span><span class="sxs-lookup"><span data-stu-id="f540f-1030">_**Figure 61:** Failover Cluster Manager: hello SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="f540f-1031">In het Hallo SIOS DataKeeper beheer en hulpprogramma voor serverconfiguratie ziet u dat Hallo gedeelde schijf gegevens synchroon worden gerepliceerd vanaf Hallo bron volume station S op clusterknooppunt een toohello volume doelstation S op clusterknooppunt B. Bijvoorbeeld, worden gerepliceerd van **pr1 ASC's 0 [10.0.0.40]** te**pr1-ASC's-1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="f540f-1031">In hello SIOS DataKeeper Management and Configuration tool, you can see that hello shared disk data is synchronously replicated from hello source volume drive S on cluster node A toohello target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** too**pr1-ascs-1 [10.0.0.41]**.</span></span>

![Afbeelding 62: In SIOS DataKeeper, repliceert u Hallo lokaal volume van het clusterknooppunt een knooppunt toocluster B][sap-ha-guide-figure-5001]

<span data-ttu-id="f540f-1033">_**Afbeelding 62:** repliceren In SIOS DataKeeper, Hallo lokaal volume van het clusterknooppunt een knooppunt toocluster B_</span><span class="sxs-lookup"><span data-stu-id="f540f-1033">_**Figure 62:** In SIOS DataKeeper, replicate hello local volume from cluster node A toocluster node B_</span></span>

### <span data-ttu-id="f540f-1034"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Failover van knooppunt A toonode B</span><span class="sxs-lookup"><span data-stu-id="f540f-1034"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A toonode B</span></span>

1.  <span data-ttu-id="f540f-1035">Kies een van deze opties tooinitiate een failover van Hallo SAP <*SID*> clustergroep van knooppunt A toocluster clusterknooppunt B:</span><span class="sxs-lookup"><span data-stu-id="f540f-1035">Choose one of these options tooinitiate a failover of hello SAP <*SID*> cluster group from cluster node A toocluster node B:</span></span>
  - <span data-ttu-id="f540f-1036">Gebruik Failoverclusterbeheer</span><span class="sxs-lookup"><span data-stu-id="f540f-1036">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="f540f-1037">Failover-Cluster PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="f540f-1037">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="f540f-1038">Start opnieuw op een van de cluster-knooppunt in Hallo Windows-gastbesturingssysteem (Hiermee initieert u een automatische failover Hallo SAP <*SID*> clustergroep van knooppunt A toonode B).</span><span class="sxs-lookup"><span data-stu-id="f540f-1038">Restart cluster node A within hello Windows guest operating system (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
3.  <span data-ttu-id="f540f-1039">Start opnieuw op een van de cluster-knooppunt van hello Azure-portal (Hiermee initieert u een automatische failover Hallo SAP <*SID*> clustergroep van knooppunt A toonode B).</span><span class="sxs-lookup"><span data-stu-id="f540f-1039">Restart cluster node A from hello Azure portal (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
4.  <span data-ttu-id="f540f-1040">Cluster-knooppunt een starten met Azure PowerShell (Hiermee initieert u een automatische failover Hallo SAP <*SID*> clustergroep van knooppunt A toonode B).</span><span class="sxs-lookup"><span data-stu-id="f540f-1040">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>

  <span data-ttu-id="f540f-1041">Na een failover Hallo SAP <*SID*> clustergroep wordt uitgevoerd op een clusterknooppunt B. Bijvoorbeeld, deze wordt uitgevoerd op **pr1-ASC's-1**.</span><span class="sxs-lookup"><span data-stu-id="f540f-1041">After failover, hello SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![Afbeelding 63: In Failoverclusterbeheer Hallo SAP < SID > clustergroep wordt uitgevoerd op het clusterknooppunt B][sap-ha-guide-figure-5002]

  <span data-ttu-id="f540f-1043">_**Afbeelding 63**: In Failoverclusterbeheer, Hallo SAP <*SID*> clustergroep wordt uitgevoerd op een clusterknooppunt B_</span><span class="sxs-lookup"><span data-stu-id="f540f-1043">_**Figure 63**: In Failover Cluster Manager, hello SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="f540f-1044">Hallo gedeelde schijf is nu gekoppeld op cluster knooppunt B. SIOS DataKeeper is repliceren van gegevens vanaf bron volume station S op knooppunt B tootarget volume clusterstation S op clusterknooppunt A. Bijvoorbeeld, van repliceren **pr1-ASC's-1 [10.0.0.41]** te**pr1 ASC's 0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="f540f-1044">hello shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B tootarget volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** too**pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![Afbeelding 64: SIOS DataKeeper repliceert Hallo lokaal volume van knooppunt B toocluster clusterknooppunt A][sap-ha-guide-figure-5003]

  <span data-ttu-id="f540f-1046">_**Afbeelding 64:** SIOS DataKeeper repliceert Hallo lokaal volume van knooppunt B toocluster clusterknooppunt A_</span><span class="sxs-lookup"><span data-stu-id="f540f-1046">_**Figure 64:** SIOS DataKeeper replicates hello local volume from cluster node B toocluster node A_</span></span>

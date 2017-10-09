---
title: hoge beschikbaarheid virtuele Machines voor SAP NetWeaver op SUSE Linux Enterprise Server voor SAP-toepassingen aaaAzure | Microsoft Docs
description: Hoge beschikbaarheid handleiding voor SAP NetWeaver op SUSE Linux Enterprise Server voor SAP-toepassingen
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
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
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a><span data-ttu-id="cdb8e-103">Hoge beschikbaarheid voor SAP NetWeaver op Azure VM's op SUSE Linux Enterprise Server voor SAP-toepassingen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-103">High availability for SAP NetWeaver on Azure VMs on SUSE Linux Enterprise Server for SAP applications</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

<span data-ttu-id="cdb8e-113">Dit artikel wordt beschreven hoe toodeploy Hallo virtuele machines Hallo virtuele machines configureren, Hallo cluster framework hebt geïnstalleerd en een maximaal beschikbare SAP NetWeaver 7,50 systeem installeren.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-113">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework and install a highly available SAP NetWeaver 7.50 system.</span></span>
<span data-ttu-id="cdb8e-114">In Hallo voorbeeldconfiguraties, enzovoort-opdrachten voor installatie. ASC's exemplaarnummer 00, Ebruikers exemplaarnummer 02 en SAP-systeem kan NWS-ID wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-114">In hello example configurations, installation commands etc. ASCS instance number 00, ERS instance number 02 and SAP System ID NWS is used.</span></span> <span data-ttu-id="cdb8e-115">Hallo namen van Hallo resources (bijvoorbeeld virtuele machines, virtuele netwerken) in Hallo voorbeeld wordt ervan uitgegaan dat u hebt gebruikt dat Hallo [geconvergeerde sjabloon] [ template-converged] met SAP ID NWS toocreate Hallo systeembronnen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-115">hello names of hello resources (for example virtual machines, virtual networks) in hello example assume that you have used hello [converged template][template-converged] with SAP system ID NWS toocreate hello resources.</span></span>

<span data-ttu-id="cdb8e-116">Hallo eerst na de SAP-opmerkingen en documenten lezen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-116">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="cdb8e-117">SAP-notitie [1928533], die is:</span><span class="sxs-lookup"><span data-stu-id="cdb8e-117">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="cdb8e-118">Lijst met Azure VM-grootten die worden ondersteund voor de implementatie van Hallo van SAP-software</span><span class="sxs-lookup"><span data-stu-id="cdb8e-118">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="cdb8e-119">Informatie over belangrijke capaciteit voor Azure VM-grootten</span><span class="sxs-lookup"><span data-stu-id="cdb8e-119">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="cdb8e-120">Ondersteunde SAP-software en besturingssysteem (OS) en combinaties van de database</span><span class="sxs-lookup"><span data-stu-id="cdb8e-120">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="cdb8e-121">Vereiste SAP-kernel-versie voor Windows en Linux op Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="cdb8e-121">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="cdb8e-122">SAP-notitie [2015553] bevat vereisten voor software-implementaties SAP SAP ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-122">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="cdb8e-123">SAP-notitie [2205917] heeft aanbevolen OS-instellingen voor SUSE Linux Enterprise Server voor SAP-toepassingen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-123">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="cdb8e-124">SAP-notitie [1944799] heeft SAP HANA richtlijnen voor SUSE Linux Enterprise Server voor SAP-toepassingen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-124">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="cdb8e-125">SAP-notitie [2178632] bevat gedetailleerde informatie over alle bewaking metrische gegevens die zijn gerapporteerd voor SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-125">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="cdb8e-126">SAP-notitie [2191498] Hallo vereist SAP Host Agent-versie voor Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-126">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="cdb8e-127">SAP-notitie [2243692] bevat informatie over SAP licentieverlening op Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-127">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="cdb8e-128">SAP-notitie [1984787] heeft algemene informatie over SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-128">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="cdb8e-129">SAP-notitie [1999351] bevat aanvullende informatie over probleemoplossing voor hello Azure verbeterde extensie Monitoring voor SAP.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-129">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="cdb8e-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) heeft alle SAP-opmerkingen voor Linux vereist.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="cdb8e-131">[Azure virtuele Machines, planning en implementatie voor SAP op Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="cdb8e-131">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="cdb8e-132">[Azure virtuele Machines-implementatie voor SAP op Linux (in dit artikel)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="cdb8e-132">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="cdb8e-133">[Azure virtuele Machines DBMS-implementatie voor SAP op Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="cdb8e-133">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="cdb8e-134">[Scenario voor optimale SAP HANA SR prestaties][suse-hana-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="cdb8e-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide]</span></span>  
  <span data-ttu-id="cdb8e-135">Hallo handleiding bevat alle vereiste gegevens tooset van SAP HANA System Replication on-premises.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-135">hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="cdb8e-136">Deze handleiding gebruiken als basislijn.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-136">Use this guide as a baseline.</span></span>
* <span data-ttu-id="cdb8e-137">[Maximaal beschikbare NFS opslag met DRBD en pacemaker heeft] [ suse-drbd-guide] Hallo handleiding bevat alle vereiste gegevens tooset van een maximaal beschikbare NFS-server.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] hello guide contains all required information tooset up a highly available NFS server.</span></span> <span data-ttu-id="cdb8e-138">Deze handleiding gebruiken als basislijn.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-138">Use this guide as a baseline.</span></span>


## <a name="overview"></a><span data-ttu-id="cdb8e-139">Overzicht</span><span class="sxs-lookup"><span data-stu-id="cdb8e-139">Overview</span></span>

<span data-ttu-id="cdb8e-140">tooachieve hoge beschikbaarheid, SAP NetWeaver vereist dat een NFS-server.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-140">tooachieve high availability, SAP NetWeaver requires an NFS server.</span></span> <span data-ttu-id="cdb8e-141">Hallo NFS-server is geconfigureerd in een cluster met afzonderlijke en kan worden gebruikt door meerdere SAP-systemen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-141">hello NFS server is configured in a separate cluster and can be used by multiple SAP systems.</span></span>

![SAP NetWeaver hoge beschikbaarheid-overzicht](./media/high-availability-guide-suse/img_001.png)

<span data-ttu-id="cdb8e-143">Hallo NFS-server, SAP NetWeaver ASC's, SAP NetWeaver SCS, SAP NetWeaver Ebruikers en Hallo SAP HANA-database gebruiken virtuele hostnaam en virtuele IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-143">hello NFS server, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS and hello SAP HANA database use virtual hostname and virtual IP addresses.</span></span> <span data-ttu-id="cdb8e-144">In Azure is een load balancer vereist toouse een virtueel IP-adres.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-144">On Azure, a load balancer is required toouse a virtual IP address.</span></span> <span data-ttu-id="cdb8e-145">Hallo bevat volgende lijst Hallo configuratie van Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-145">hello following list shows hello configuration of hello load balancer.</span></span>

### <a name="nfs-server"></a><span data-ttu-id="cdb8e-146">NFS-Server</span><span class="sxs-lookup"><span data-stu-id="cdb8e-146">NFS Server</span></span>
* <span data-ttu-id="cdb8e-147">Frontend configuratie</span><span class="sxs-lookup"><span data-stu-id="cdb8e-147">Frontend configuration</span></span>
  * <span data-ttu-id="cdb8e-148">IP-adres 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="cdb8e-148">IP address 10.0.0.4</span></span>
* <span data-ttu-id="cdb8e-149">Back-endconfiguratie</span><span class="sxs-lookup"><span data-stu-id="cdb8e-149">Backend configuration</span></span>
  * <span data-ttu-id="cdb8e-150">Netwerkinterfaces tooprimary van alle virtuele machines die deel uitmaken van Hallo NFS cluster moeten worden verbonden</span><span class="sxs-lookup"><span data-stu-id="cdb8e-150">Connected tooprimary network interfaces of all virtual machines that should be part of hello NFS cluster</span></span>
* <span data-ttu-id="cdb8e-151">De Testpoort</span><span class="sxs-lookup"><span data-stu-id="cdb8e-151">Probe Port</span></span>
  * <span data-ttu-id="cdb8e-152">Poort 61000</span><span class="sxs-lookup"><span data-stu-id="cdb8e-152">Port 61000</span></span>
* <span data-ttu-id="cdb8e-153">Loadbalancing regels</span><span class="sxs-lookup"><span data-stu-id="cdb8e-153">Loadbalancing rules</span></span>
  * <span data-ttu-id="cdb8e-154">2049 TCP</span><span class="sxs-lookup"><span data-stu-id="cdb8e-154">2049 TCP</span></span> 
  * <span data-ttu-id="cdb8e-155">2049 UDP</span><span class="sxs-lookup"><span data-stu-id="cdb8e-155">2049 UDP</span></span>

### <a name="ascs"></a><span data-ttu-id="cdb8e-156">(A) SCS</span><span class="sxs-lookup"><span data-stu-id="cdb8e-156">(A)SCS</span></span>
* <span data-ttu-id="cdb8e-157">Frontend configuratie</span><span class="sxs-lookup"><span data-stu-id="cdb8e-157">Frontend configuration</span></span>
  * <span data-ttu-id="cdb8e-158">IP-adres 10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="cdb8e-158">IP address 10.0.0.10</span></span>
* <span data-ttu-id="cdb8e-159">Back-endconfiguratie</span><span class="sxs-lookup"><span data-stu-id="cdb8e-159">Backend configuration</span></span>
  * <span data-ttu-id="cdb8e-160">Netwerkinterfaces verbonden tooprimary van alle virtuele machines die deel van hello (A) SCS Ebruikers/cluster uitmaken moet</span><span class="sxs-lookup"><span data-stu-id="cdb8e-160">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="cdb8e-161">De Testpoort</span><span class="sxs-lookup"><span data-stu-id="cdb8e-161">Probe Port</span></span>
  * <span data-ttu-id="cdb8e-162">Poort 620**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="cdb8e-162">Port 620**&lt;nr&gt;**</span></span>
* <span data-ttu-id="cdb8e-163">Loadbalancing regels</span><span class="sxs-lookup"><span data-stu-id="cdb8e-163">Loadbalancing rules</span></span>
  * <span data-ttu-id="cdb8e-164">32**&lt;nr&gt;**  TCP</span><span class="sxs-lookup"><span data-stu-id="cdb8e-164">32**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="cdb8e-165">36**&lt;nr&gt;**  TCP</span><span class="sxs-lookup"><span data-stu-id="cdb8e-165">36**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="cdb8e-166">39**&lt;nr&gt;**  TCP</span><span class="sxs-lookup"><span data-stu-id="cdb8e-166">39**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="cdb8e-167">81**&lt;nr&gt;**  TCP</span><span class="sxs-lookup"><span data-stu-id="cdb8e-167">81**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="cdb8e-168">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="cdb8e-168">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="cdb8e-169">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="cdb8e-169">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="cdb8e-170">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="cdb8e-170">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="ers"></a><span data-ttu-id="cdb8e-171">EBRUIKERS</span><span class="sxs-lookup"><span data-stu-id="cdb8e-171">ERS</span></span>
* <span data-ttu-id="cdb8e-172">Frontend configuratie</span><span class="sxs-lookup"><span data-stu-id="cdb8e-172">Frontend configuration</span></span>
  * <span data-ttu-id="cdb8e-173">IP-adres 10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="cdb8e-173">IP address 10.0.0.11</span></span>
* <span data-ttu-id="cdb8e-174">Back-endconfiguratie</span><span class="sxs-lookup"><span data-stu-id="cdb8e-174">Backend configuration</span></span>
  * <span data-ttu-id="cdb8e-175">Netwerkinterfaces verbonden tooprimary van alle virtuele machines die deel van hello (A) SCS Ebruikers/cluster uitmaken moet</span><span class="sxs-lookup"><span data-stu-id="cdb8e-175">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="cdb8e-176">De Testpoort</span><span class="sxs-lookup"><span data-stu-id="cdb8e-176">Probe Port</span></span>
  * <span data-ttu-id="cdb8e-177">Poort 621**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="cdb8e-177">Port 621**&lt;nr&gt;**</span></span>
* <span data-ttu-id="cdb8e-178">Loadbalancing regels</span><span class="sxs-lookup"><span data-stu-id="cdb8e-178">Loadbalancing rules</span></span>
  * <span data-ttu-id="cdb8e-179">33**&lt;nr&gt;**  TCP</span><span class="sxs-lookup"><span data-stu-id="cdb8e-179">33**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="cdb8e-180">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="cdb8e-180">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="cdb8e-181">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="cdb8e-181">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="cdb8e-182">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="cdb8e-182">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="sap-hana"></a><span data-ttu-id="cdb8e-183">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cdb8e-183">SAP HANA</span></span>
* <span data-ttu-id="cdb8e-184">Frontend configuratie</span><span class="sxs-lookup"><span data-stu-id="cdb8e-184">Frontend configuration</span></span>
  * <span data-ttu-id="cdb8e-185">IP-adres 10.0.0.12</span><span class="sxs-lookup"><span data-stu-id="cdb8e-185">IP address 10.0.0.12</span></span>
* <span data-ttu-id="cdb8e-186">Back-endconfiguratie</span><span class="sxs-lookup"><span data-stu-id="cdb8e-186">Backend configuration</span></span>
  * <span data-ttu-id="cdb8e-187">Netwerkinterfaces tooprimary van alle virtuele machines die deel uitmaken van Hallo HANA cluster moeten worden verbonden</span><span class="sxs-lookup"><span data-stu-id="cdb8e-187">Connected tooprimary network interfaces of all virtual machines that should be part of hello HANA cluster</span></span>
* <span data-ttu-id="cdb8e-188">De Testpoort</span><span class="sxs-lookup"><span data-stu-id="cdb8e-188">Probe Port</span></span>
  * <span data-ttu-id="cdb8e-189">Poort 625**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="cdb8e-189">Port 625**&lt;nr&gt;**</span></span>
* <span data-ttu-id="cdb8e-190">Loadbalancing regels</span><span class="sxs-lookup"><span data-stu-id="cdb8e-190">Loadbalancing rules</span></span>
  * <span data-ttu-id="cdb8e-191">3**&lt;nr&gt;**15 TCP</span><span class="sxs-lookup"><span data-stu-id="cdb8e-191">3**&lt;nr&gt;**15 TCP</span></span>
  * <span data-ttu-id="cdb8e-192">3**&lt;nr&gt;**17 TCP</span><span class="sxs-lookup"><span data-stu-id="cdb8e-192">3**&lt;nr&gt;**17 TCP</span></span>

## <a name="setting-up-a-highly-available-nfs-server"></a><span data-ttu-id="cdb8e-193">Een maximaal beschikbare NFS-server instellen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-193">Setting up a highly available NFS server</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="cdb8e-194">Linux implementeren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-194">Deploying Linux</span></span>

<span data-ttu-id="cdb8e-195">Hello Azure Marketplace bevat een afbeelding voor SUSE Linux Enterprise Server voor SAP-toepassingen 12 waarmee u toodeploy nieuwe virtuele machines kunt.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-195">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span>
<span data-ttu-id="cdb8e-196">Kunt u een van Hallo snel starten-sjablonen op github toodeploy alle vereiste bronnen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-196">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="cdb8e-197">Hallo sjabloon implementeert Hallo virtuele machines, Hallo load balancer, beschikbaarheidsset enzovoort. Volg deze stappen toodeploy Hallo sjabloon:</span><span class="sxs-lookup"><span data-stu-id="cdb8e-197">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="cdb8e-198">Open Hallo [SAP-server de sjabloon] [ template-file-server] in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="cdb8e-198">Open hello [SAP file server template][template-file-server] in hello Azure portal</span></span>   
1. <span data-ttu-id="cdb8e-199">Hallo volgende parameters opgeven</span><span class="sxs-lookup"><span data-stu-id="cdb8e-199">Enter hello following parameters</span></span>
   1. <span data-ttu-id="cdb8e-200">Resource-voorvoegsel</span><span class="sxs-lookup"><span data-stu-id="cdb8e-200">Resource Prefix</span></span>  
      <span data-ttu-id="cdb8e-201">Voer gewenste toouse Hallo-voorvoegsel in.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-201">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="cdb8e-202">Hallo-waarde wordt gebruikt als een voorvoegsel voor Hallo-resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-202">hello value is used as a prefix for hello resources that are deployed.</span></span>
   2. <span data-ttu-id="cdb8e-203">Type besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="cdb8e-203">Os Type</span></span>  
      <span data-ttu-id="cdb8e-204">Selecteer een van de Linux-distributies Hallo.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-204">Select one of hello Linux distributions.</span></span> <span data-ttu-id="cdb8e-205">Selecteer voor dit voorbeeld SLES 12</span><span class="sxs-lookup"><span data-stu-id="cdb8e-205">For this example, select SLES 12</span></span>
   3. <span data-ttu-id="cdb8e-206">Gebruikersnaam van de beheerder en het wachtwoord van beheerder</span><span class="sxs-lookup"><span data-stu-id="cdb8e-206">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="cdb8e-207">Een nieuwe gebruiker gemaakt, dat de gebruikte toolog op toohello machine kunnen worden.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-207">A new user is created that can be used toolog on toohello machine.</span></span>
   4. <span data-ttu-id="cdb8e-208">Subnet-Id</span><span class="sxs-lookup"><span data-stu-id="cdb8e-208">Subnet Id</span></span>  
      <span data-ttu-id="cdb8e-209">Hallo-ID van Hallo subnet toowhich Hallo virtuele machines moet worden aangesloten.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-209">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="cdb8e-210">Laat leeg als u toocreate een nieuw virtueel netwerk wilt of subnet Hallo van uw VPN- of Express Route virtueel netwerk tooconnect Hallo virtuele machine tooyour on-premises netwerk selecteert.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-210">Leave empty if you want toocreate a new virtual network or select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="cdb8e-211">Hallo-ID meestal ziet eruit als /subscriptions/**&lt;abonnements-id&gt;**/resourceGroups/**&lt;Resourcegroepnaam&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;virtuele-netwerknaam&gt;**/subnets/**&lt;subnetnaam&gt;**</span><span class="sxs-lookup"><span data-stu-id="cdb8e-211">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="cdb8e-212">Installeren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-212">Installation</span></span>

<span data-ttu-id="cdb8e-213">Hallo volgende items, worden voorafgegaan door een **[A]** -knooppunten van de toepasselijke tooall, **[1]** -alleen van toepassing toonode 1 of **[2]** -alleen van toepassing toonode 2.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-213">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="cdb8e-214">**[A]**  SLES bijwerken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-214">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="cdb8e-215">**[1]**  Ssh toegang inschakelen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-215">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="cdb8e-216">**[2]**  Ssh toegang inschakelen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-216">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="cdb8e-217">**[1]**  Ssh toegang inschakelen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-217">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="cdb8e-218">**[A]**  Installeren HA-uitbreiding</span><span class="sxs-lookup"><span data-stu-id="cdb8e-218">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="cdb8e-219">**[A]**  Hostnamen instellen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-219">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="cdb8e-220">U kunt een DNS-server gebruiken of Hallo/etc/hosts op alle knooppunten wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-220">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="cdb8e-221">Dit voorbeeld toont hoe toouse Hallo/etc/hosts-bestand.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-221">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="cdb8e-222">Hallo IP-adres en hostnaam in de volgende opdrachten Hallo Hallo vervangen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-222">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="cdb8e-223">Invoegen Hallo regels te/etc/hosts te volgen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-223">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="cdb8e-224">Uw omgeving voor het IP-adres en hostnaam toomatch Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-224">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. <span data-ttu-id="cdb8e-225">**[1]**  Cluster installeren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-225">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="cdb8e-226">**[2]**  Knooppunt toocluster toevoegen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-226">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="cdb8e-227">**[A]**  Wijziging hacluster wachtwoord toohello hetzelfde wachtwoord</span><span class="sxs-lookup"><span data-stu-id="cdb8e-227">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="cdb8e-228">**[A]**  Configureren corosync toouse andere transport en nodelist toevoegen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-228">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="cdb8e-229">Cluster werkt niet anders.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-229">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="cdb8e-230">Hallo volgende vet inhoud toohello toevoegen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-230">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="cdb8e-231">Hallo corosync service opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="cdb8e-231">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="cdb8e-232">**[A]**  Drbd-onderdelen installeren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-232">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="cdb8e-233">**[A]**  Maken van een partitie voor Hallo drbd apparaat</span><span class="sxs-lookup"><span data-stu-id="cdb8e-233">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="cdb8e-234">**[A]**  Configuraties LVM maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-234">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. <span data-ttu-id="cdb8e-235">**[A]**  Maken Hallo NFS drbd apparaat</span><span class="sxs-lookup"><span data-stu-id="cdb8e-235">**[A]** Create hello NFS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   <span data-ttu-id="cdb8e-236">Hallo-configuratie voor Hallo nieuwe drbd apparaat en afsluiten invoegen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-236">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="cdb8e-237">Hallo drbd apparaat maken en start deze</span><span class="sxs-lookup"><span data-stu-id="cdb8e-237">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="cdb8e-238">**[1]**  Overslaan van de initiële synchronisatie</span><span class="sxs-lookup"><span data-stu-id="cdb8e-238">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="cdb8e-239">**[1]**  Set Hallo primaire knooppunt</span><span class="sxs-lookup"><span data-stu-id="cdb8e-239">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="cdb8e-240">**[1]**  Wacht totdat het Hallo nieuwe drbd apparaten worden gesynchroniseerd</span><span class="sxs-lookup"><span data-stu-id="cdb8e-240">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="cdb8e-241">**[1]**  Bestandssystemen op Hallo drbd apparaten maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-241">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="cdb8e-242">Cluster-Framework configureren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-242">Configure Cluster Framework</span></span>

1. <span data-ttu-id="cdb8e-243">**[1]**  Hello standaardinstellingen wijzigen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-243">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="cdb8e-244">**[1]**  Toevoegen Hallo NFS drbd toohello cluster apparaatconfiguratie</span><span class="sxs-lookup"><span data-stu-id="cdb8e-244">**[1]** Add hello NFS drbd device toohello cluster configuration</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="cdb8e-245">**[1]**  Hello NFS-server maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-245">**[1]** Create hello NFS server</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="cdb8e-246">**[1]**  Hello NFS File System resources maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-246">**[1]** Create hello NFS File System resources</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="cdb8e-247">**[1]**  Hello NFS exports maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-247">**[1]** Create hello NFS exports</span></span>

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="cdb8e-248">**[1]**  Een virtueel IP-resource en de statuscontrole voor Hallo interne load balancer maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-248">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="cdb8e-249">STONITH apparaat maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-249">Create STONITH device</span></span>

<span data-ttu-id="cdb8e-250">Hallo STONITH apparaat maakt gebruik van een Service-Principal tooauthorize tegen Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-250">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="cdb8e-251">Volg deze stappen toocreate een Service-Principal.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-251">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="cdb8e-252">Ga te<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="cdb8e-252">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="cdb8e-253">Open hello Azure Active Directory-blade</span><span class="sxs-lookup"><span data-stu-id="cdb8e-253">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="cdb8e-254">Ga tooProperties en schrijf Hallo Directory-id. Dit is Hallo **tenant-id**.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-254">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="cdb8e-255">Klik op App-registraties</span><span class="sxs-lookup"><span data-stu-id="cdb8e-255">Click App registrations</span></span>
1. <span data-ttu-id="cdb8e-256">Klik op Add.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-256">Click Add</span></span>
1. <span data-ttu-id="cdb8e-257">Voer een naam, selecteer toepassingstype 'Web-app /-API, een aanmeldings-URL (bijvoorbeeld http://localhost) en klik op maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-257">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="cdb8e-258">Hallo aanmeldings-URL kan niet wordt gebruikt en geldige URL</span><span class="sxs-lookup"><span data-stu-id="cdb8e-258">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="cdb8e-259">Selecteer de nieuwe App Hallo en sleutels op in het tabblad Hallo-instellingen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-259">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="cdb8e-260">Voer een beschrijving voor een nieuwe sleutel, selecteer 'Verloopt nooit' en klik op Opslaan</span><span class="sxs-lookup"><span data-stu-id="cdb8e-260">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="cdb8e-261">Schrijf Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-261">Write down hello Value.</span></span> <span data-ttu-id="cdb8e-262">Deze wordt gebruikt als Hallo **wachtwoord** voor Hallo Service-Principal</span><span class="sxs-lookup"><span data-stu-id="cdb8e-262">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="cdb8e-263">Schrijf Hallo toepassings-id. Deze wordt gebruikt als gebruikersnaam Hallo (**aanmeldings-id** in de onderstaande stappen voor Hallo) Hallo Service-Principal</span><span class="sxs-lookup"><span data-stu-id="cdb8e-263">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="cdb8e-264">Hallo Service-Principal heeft geen machtigingen tooaccess uw Azure-resources standaard.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-264">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="cdb8e-265">Moet u toogive Hallo Service-Principal machtigingen toostart en gestopt (toewijzing ongedaan maken) alle virtuele machines van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-265">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="cdb8e-266">Ga toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="cdb8e-266">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="cdb8e-267">Open de blade van alle resources Hallo</span><span class="sxs-lookup"><span data-stu-id="cdb8e-267">Open hello All resources blade</span></span>
1. <span data-ttu-id="cdb8e-268">Selecteer Hallo virtuele machine</span><span class="sxs-lookup"><span data-stu-id="cdb8e-268">Select hello virtual machine</span></span>
1. <span data-ttu-id="cdb8e-269">Klik op toegangsbeheer (IAM)</span><span class="sxs-lookup"><span data-stu-id="cdb8e-269">Click Access control (IAM)</span></span>
1. <span data-ttu-id="cdb8e-270">Klik op Add.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-270">Click Add</span></span>
1. <span data-ttu-id="cdb8e-271">Selecteer Hallo rol eigenaar</span><span class="sxs-lookup"><span data-stu-id="cdb8e-271">Select hello role Owner</span></span>
1. <span data-ttu-id="cdb8e-272">Voer de naam Hallo van Hallo-toepassing die u hierboven hebt gemaakt</span><span class="sxs-lookup"><span data-stu-id="cdb8e-272">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="cdb8e-273">Klik op OK</span><span class="sxs-lookup"><span data-stu-id="cdb8e-273">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="cdb8e-274">**[1]**  Hello STONITH apparaten maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-274">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="cdb8e-275">Nadat u machtigingen voor virtuele machines die Hallo Hallo bewerkt, kunt u Hallo STONITH apparaten kunt configureren in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-275">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="cdb8e-276">**[1]**  Hello gebruik van een apparaat STONITH inschakelen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-276">**[1]** Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a><span data-ttu-id="cdb8e-277">(A) SCS instellen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-277">Setting up (A)SCS</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="cdb8e-278">Linux implementeren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-278">Deploying Linux</span></span>

<span data-ttu-id="cdb8e-279">Hello Azure Marketplace bevat een afbeelding voor SUSE Linux Enterprise Server voor SAP-toepassingen 12 waarmee u toodeploy nieuwe virtuele machines kunt.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-279">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span> <span data-ttu-id="cdb8e-280">Hallo marketplace-installatiekopie bevat Hallo resource-agent voor SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-280">hello marketplace image contains hello resource agent for SAP NetWeaver.</span></span>

<span data-ttu-id="cdb8e-281">Kunt u een van Hallo snel starten-sjablonen op github toodeploy alle vereiste bronnen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-281">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="cdb8e-282">Hallo sjabloon implementeert Hallo virtuele machines, Hallo load balancer, beschikbaarheidsset enzovoort. Volg deze stappen toodeploy Hallo sjabloon:</span><span class="sxs-lookup"><span data-stu-id="cdb8e-282">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="cdb8e-283">Open Hallo [ASC's / SCS Multi SID sjabloon] [ template-multisid-xscs] of Hallo [geconvergeerde sjabloon] [ template-converged] op Hallo Azure portal Hallo ASC's / SCS sjabloon alleen Hiermee maakt Hallo load balancing regels voor Hallo SAP NetWeaver ASC's / SCS en Ebruikers (alleen voor Linux)-exemplaren dat Hallo geconvergeerde sjabloon ook Hallo-taakverdeling regels voor een database (bijvoorbeeld Microsoft SQL Server of SAP HANA maakt).</span><span class="sxs-lookup"><span data-stu-id="cdb8e-283">Open hello [ASCS/SCS Multi SID template][template-multisid-xscs] or hello [converged template][template-converged] on hello Azure portal hello ASCS/SCS template only creates hello load-balancing rules for hello SAP NetWeaver ASCS/SCS and ERS (Linux only) instances whereas hello converged template also creates hello load-balancing rules for a database (for example Microsoft SQL Server or SAP HANA).</span></span> <span data-ttu-id="cdb8e-284">Als u van plan een SAP NetWeaver gebaseerd systeem tooinstall bent en u ook tooinstall Hallo database wilt op dezelfde machines hello, gebruikt u Hallo [geconvergeerde sjabloon][template-converged].</span><span class="sxs-lookup"><span data-stu-id="cdb8e-284">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello database on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="cdb8e-285">Hallo volgende parameters opgeven</span><span class="sxs-lookup"><span data-stu-id="cdb8e-285">Enter hello following parameters</span></span>
   1. <span data-ttu-id="cdb8e-286">Resource-voorvoegsel (alleen ASC's / SCS Multi SID-sjabloon)</span><span class="sxs-lookup"><span data-stu-id="cdb8e-286">Resource Prefix (ASCS/SCS Multi SID template only)</span></span>  
      <span data-ttu-id="cdb8e-287">Voer gewenste toouse Hallo-voorvoegsel in.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-287">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="cdb8e-288">Hallo-waarde wordt gebruikt als een voorvoegsel voor Hallo-resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-288">hello value is used as a prefix for hello resources that are deployed.</span></span>
   3. <span data-ttu-id="cdb8e-289">SAP systeem-Id (alleen geconvergeerde sjabloon)</span><span class="sxs-lookup"><span data-stu-id="cdb8e-289">Sap System Id (converged template only)</span></span>  
      <span data-ttu-id="cdb8e-290">Voer Hallo SAP-systeem Id Hallo gewenste tooinstall SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-290">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="cdb8e-291">Hallo-Id wordt gebruikt als een voorvoegsel voor Hallo-resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-291">hello Id is used as a prefix for hello resources that are deployed.</span></span>
   4. <span data-ttu-id="cdb8e-292">Stack-Type</span><span class="sxs-lookup"><span data-stu-id="cdb8e-292">Stack Type</span></span>  
      <span data-ttu-id="cdb8e-293">Hallo SAP NetWeaver stack-type selecteren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-293">Select hello SAP NetWeaver stack type</span></span>
   5. <span data-ttu-id="cdb8e-294">Type besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="cdb8e-294">Os Type</span></span>  
      <span data-ttu-id="cdb8e-295">Selecteer een van de Linux-distributies Hallo.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-295">Select one of hello Linux distributions.</span></span> <span data-ttu-id="cdb8e-296">Selecteer voor dit voorbeeld SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="cdb8e-296">For this example, select SLES 12 BYOS</span></span>
   6. <span data-ttu-id="cdb8e-297">DB-Type</span><span class="sxs-lookup"><span data-stu-id="cdb8e-297">Db Type</span></span>  
      <span data-ttu-id="cdb8e-298">Selecteer HANA</span><span class="sxs-lookup"><span data-stu-id="cdb8e-298">Select HANA</span></span>
   7. <span data-ttu-id="cdb8e-299">Grootte van het SAP</span><span class="sxs-lookup"><span data-stu-id="cdb8e-299">Sap System Size</span></span>  
      <span data-ttu-id="cdb8e-300">Hallo hoeveelheid SAP's Hallo nieuw systeem biedt.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-300">hello amount of SAPS hello new system provides.</span></span> <span data-ttu-id="cdb8e-301">Als u niet zeker weet hoeveel SAP's Hallo systeem vereist is, vraag uw SAP-technologie Partner of System Integrator</span><span class="sxs-lookup"><span data-stu-id="cdb8e-301">If you are not sure how many SAPS hello system requires, please ask your SAP Technology Partner or System Integrator</span></span>
   8. <span data-ttu-id="cdb8e-302">Beschikbaarheid van het systeem</span><span class="sxs-lookup"><span data-stu-id="cdb8e-302">System Availability</span></span>  
      <span data-ttu-id="cdb8e-303">Selecteer HA</span><span class="sxs-lookup"><span data-stu-id="cdb8e-303">Select HA</span></span>
   9. <span data-ttu-id="cdb8e-304">Gebruikersnaam van de beheerder en het wachtwoord van beheerder</span><span class="sxs-lookup"><span data-stu-id="cdb8e-304">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="cdb8e-305">Een nieuwe gebruiker gemaakt, dat de gebruikte toolog op toohello machine kunnen worden.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-305">A new user is created that can be used toolog on toohello machine.</span></span>
   10. <span data-ttu-id="cdb8e-306">Subnet-Id</span><span class="sxs-lookup"><span data-stu-id="cdb8e-306">Subnet Id</span></span>  
   <span data-ttu-id="cdb8e-307">Hallo-ID van Hallo subnet toowhich Hallo virtuele machines moet worden aangesloten.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-307">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span>  <span data-ttu-id="cdb8e-308">Laat leeg als u toocreate een nieuw virtueel netwerk wilt of Selecteer hetzelfde subnet die u gebruikt of gemaakt als onderdeel van de NFS-serverimplementatie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-308">Leave empty if you want toocreate a new virtual network or select hello same subnet that you used or created as part of hello NFS server deployment.</span></span> <span data-ttu-id="cdb8e-309">Hallo-ID meestal ziet eruit als /subscriptions/**&lt;abonnements-id&gt;**/resourceGroups/**&lt;Resourcegroepnaam&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;virtuele-netwerknaam&gt;**/subnets/**&lt;subnetnaam&gt;**</span><span class="sxs-lookup"><span data-stu-id="cdb8e-309">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="cdb8e-310">Installeren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-310">Installation</span></span>

<span data-ttu-id="cdb8e-311">Hallo volgende items, worden voorafgegaan door een **[A]** -knooppunten van de toepasselijke tooall, **[1]** -alleen van toepassing toonode 1 of **[2]** -alleen van toepassing toonode 2.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-311">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="cdb8e-312">**[A]**  SLES bijwerken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-312">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="cdb8e-313">**[1]**  Ssh toegang inschakelen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-313">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="cdb8e-314">**[2]**  Ssh toegang inschakelen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-314">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="cdb8e-315">**[1]**  Ssh toegang inschakelen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-315">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="cdb8e-316">**[A]**  Installeren HA-uitbreiding</span><span class="sxs-lookup"><span data-stu-id="cdb8e-316">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="cdb8e-317">**[A]**  Update SAP resource agents</span><span class="sxs-lookup"><span data-stu-id="cdb8e-317">**[A]** Update SAP resource agents</span></span>  
   
   <span data-ttu-id="cdb8e-318">Er is een fout opgetreden in een patch voor Hallo resource agents pakket vereist toouse Hallo nieuwe configuratie, die in dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-318">A patch for hello resource-agents package is required toouse hello new configuration, that is described in this article.</span></span> <span data-ttu-id="cdb8e-319">U kunt controleren als Hallo patch is al geïnstalleerd met de volgende opdracht Hallo</span><span class="sxs-lookup"><span data-stu-id="cdb8e-319">You can check, if hello patch is already installed with hello following command</span></span>

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   <span data-ttu-id="cdb8e-320">Hallo-uitvoer moet er ongeveer als</span><span class="sxs-lookup"><span data-stu-id="cdb8e-320">hello output should be similar to</span></span>

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   <span data-ttu-id="cdb8e-321">Als Hallo grep opdracht geen Hallo IS_ERS parameter vindt, moet u tooinstall Hallo patch vermeld op [Hallo SUSE downloadpagina](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span><span class="sxs-lookup"><span data-stu-id="cdb8e-321">If hello grep command does not find hello IS_ERS parameter, you need tooinstall hello patch listed on [hello SUSE download page](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span></span>

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. <span data-ttu-id="cdb8e-322">**[A]**  Hostnamen instellen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-322">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="cdb8e-323">U kunt een DNS-server gebruiken of Hallo/etc/hosts op alle knooppunten wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-323">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="cdb8e-324">Dit voorbeeld toont hoe toouse Hallo/etc/hosts-bestand.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-324">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="cdb8e-325">Hallo IP-adres en hostnaam in de volgende opdrachten Hallo Hallo vervangen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-325">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="cdb8e-326">Invoegen Hallo regels te/etc/hosts te volgen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-326">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="cdb8e-327">Uw omgeving voor het IP-adres en hostnaam toomatch Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-327">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. <span data-ttu-id="cdb8e-328">**[1]**  Cluster installeren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-328">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="cdb8e-329">**[2]**  Knooppunt toocluster toevoegen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-329">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="cdb8e-330">**[A]**  Wijziging hacluster wachtwoord toohello hetzelfde wachtwoord</span><span class="sxs-lookup"><span data-stu-id="cdb8e-330">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="cdb8e-331">**[A]**  Configureren corosync toouse andere transport en nodelist toevoegen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-331">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="cdb8e-332">Cluster werkt niet anders.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-332">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="cdb8e-333">Hallo volgende vet inhoud toohello toevoegen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-333">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="cdb8e-334">Hallo corosync service opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="cdb8e-334">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="cdb8e-335">**[A]**  Drbd-onderdelen installeren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-335">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="cdb8e-336">**[A]**  Maken van een partitie voor Hallo drbd apparaat</span><span class="sxs-lookup"><span data-stu-id="cdb8e-336">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="cdb8e-337">**[A]**  Configuraties LVM maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-337">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. <span data-ttu-id="cdb8e-338">**[A]**  Maken Hallo SCS drbd apparaat</span><span class="sxs-lookup"><span data-stu-id="cdb8e-338">**[A]** Create hello SCS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   <span data-ttu-id="cdb8e-339">Hallo-configuratie voor Hallo nieuwe drbd apparaat en afsluiten invoegen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-339">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="cdb8e-340">Hallo drbd apparaat maken en start deze</span><span class="sxs-lookup"><span data-stu-id="cdb8e-340">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. <span data-ttu-id="cdb8e-341">**[A]**  Maken Hallo Ebruikers drbd apparaat</span><span class="sxs-lookup"><span data-stu-id="cdb8e-341">**[A]** Create hello ERS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   <span data-ttu-id="cdb8e-342">Hallo-configuratie voor Hallo nieuwe drbd apparaat en afsluiten invoegen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-342">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="cdb8e-343">Hallo drbd apparaat maken en start deze</span><span class="sxs-lookup"><span data-stu-id="cdb8e-343">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="cdb8e-344">**[1]**  Overslaan van de initiële synchronisatie</span><span class="sxs-lookup"><span data-stu-id="cdb8e-344">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="cdb8e-345">**[1]**  Set Hallo primaire knooppunt</span><span class="sxs-lookup"><span data-stu-id="cdb8e-345">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="cdb8e-346">**[1]**  Wacht totdat het Hallo nieuwe drbd apparaten worden gesynchroniseerd</span><span class="sxs-lookup"><span data-stu-id="cdb8e-346">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="cdb8e-347">**[1]**  Bestandssystemen op Hallo drbd apparaten maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-347">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="cdb8e-348">Cluster-Framework configureren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-348">Configure Cluster Framework</span></span>

<span data-ttu-id="cdb8e-349">**[1]**  Hello standaardinstellingen wijzigen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-349">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a><span data-ttu-id="cdb8e-350">SAP NetWeaver installatie voorbereiden</span><span class="sxs-lookup"><span data-stu-id="cdb8e-350">Prepare for SAP NetWeaver installation</span></span>

1. <span data-ttu-id="cdb8e-351">**[A]**  Maken Hallo gedeelde mappen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-351">**[A]** Create hello shared directories</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. <span data-ttu-id="cdb8e-352">**[A]**  Autofs configureren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-352">**[A]** Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="cdb8e-353">Maak een bestand met</span><span class="sxs-lookup"><span data-stu-id="cdb8e-353">Create a file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   <span data-ttu-id="cdb8e-354">Opnieuw opstarten autofs toomount Hallo nieuwe shares</span><span class="sxs-lookup"><span data-stu-id="cdb8e-354">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="cdb8e-355">**[A]**  Bestand WISSELEN configureren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-355">**[A]** Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="cdb8e-356">Opnieuw Hallo Agent tooactivate Hallo wijziging</span><span class="sxs-lookup"><span data-stu-id="cdb8e-356">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a><span data-ttu-id="cdb8e-357">SAP NetWeaver ASC's / Ebruikers installeren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-357">Installing SAP NetWeaver ASCS/ERS</span></span>

1. <span data-ttu-id="cdb8e-358">**[1]**  Een virtueel IP-resource en de statuscontrole voor Hallo interne load balancer maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-358">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="cdb8e-359">Zorg ervoor dat de clusterstatus Hallo ok is en dat alle resources worden gestart.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-359">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="cdb8e-360">Het is niet belangrijk welke bronnen van de Hallo knooppunt worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-360">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. <span data-ttu-id="cdb8e-361">**[1]**  SAP NetWeaver ASC's installeren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-361">**[1]** Install SAP NetWeaver ASCS</span></span>  

   <span data-ttu-id="cdb8e-362">SAP NetWeaver ASC's installeren als hoofdmap op Hallo van de eerste knooppunt met behulp van een virtuele hostnaam die is toegewezen toohello IP-adres van de load balancer frontend-configuratie voor Hallo ASC's Hallo bijvoorbeeld <b>nws-ASC's</b>, <b>10.0.0.10</b>en Hallo exemplaarnummer die u voor de test Hallo Hallo load balancer bijvoorbeeld gebruikt <b>00</b>.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-362">Install SAP NetWeaver ASCS as root on hello first node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ASCS for example <b>nws-ascs</b>, <b>10.0.0.10</b> and hello instance number that you used for hello probe of hello load balancer for example <b>00</b>.</span></span>

   <span data-ttu-id="cdb8e-363">U kunt Hallo sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow een niet-hoofdgebruiker tooconnect toosapinst gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-363">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="cdb8e-364">**[1]**  Een virtueel IP-resource en de statuscontrole voor Hallo interne load balancer maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-364">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   <span data-ttu-id="cdb8e-365">Zorg ervoor dat de clusterstatus Hallo ok is en dat alle resources worden gestart.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-365">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="cdb8e-366">Het is niet belangrijk welke bronnen van de Hallo knooppunt worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-366">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="cdb8e-367">**[2]**  SAP NetWeaver Ebruikers installeren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-367">**[2]** Install SAP NetWeaver ERS</span></span>  

   <span data-ttu-id="cdb8e-368">SAP NetWeaver Ebruikers installeren als hoofdmap op Hallo van de tweede knooppunt met behulp van een virtuele hostnaam die is toegewezen toohello IP-adres van de load balancer frontend-configuratie voor Hallo Ebruikers Hallo bijvoorbeeld <b>nws ebruikers</b>, <b>10.0.0.11</b> en Hallo exemplaarnummer die u voor de test Hallo Hallo load balancer bijvoorbeeld gebruikt <b>02</b>.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-368">Install SAP NetWeaver ERS as root on hello second node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ERS for example <b>nws-ers</b>, <b>10.0.0.11</b> and hello instance number that you used for hello probe of hello load balancer for example <b>02</b>.</span></span>

   <span data-ttu-id="cdb8e-369">U kunt Hallo sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow een niet-hoofdgebruiker tooconnect toosapinst gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-369">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > <span data-ttu-id="cdb8e-370">Gebruik SWPM SP 20 PL 05 of hoger.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-370">Please use SWPM SP 20 PL 05 or higher.</span></span> <span data-ttu-id="cdb8e-371">Lagere versies Hallo machtigingen niet correct instelt en Hallo-installatie mislukt.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-371">Lower versions do not set hello permissions correctly and hello installation will fail.</span></span>
   > 

1. <span data-ttu-id="cdb8e-372">**[1]**  Hello ASC's / SCS en Ebruikers exemplaar profielen aanpassen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-372">**[1]** Adapt hello ASCS/SCS and ERS instance profiles</span></span>
 
   * <span data-ttu-id="cdb8e-373">ASC's / SCS-profiel</span><span class="sxs-lookup"><span data-stu-id="cdb8e-373">ASCS/SCS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * <span data-ttu-id="cdb8e-374">Ebruikers profiel</span><span class="sxs-lookup"><span data-stu-id="cdb8e-374">ERS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. <span data-ttu-id="cdb8e-375">**[A]**  Keep-Alive configureren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-375">**[A]** Configure Keep Alive</span></span>

   <span data-ttu-id="cdb8e-376">Hallo-communicatie tussen Hallo SAP NetWeaver toepassingsserver en Hallo ASC's / SCS wordt via een software load balancer doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-376">hello communication between hello SAP NetWeaver application server and hello ASCS/SCS is routed through a software load balancer.</span></span> <span data-ttu-id="cdb8e-377">Hallo load balancer wordt niet-actieve verbindingen na een configureerbare time-out verbroken.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-377">hello load balancer disconnects inactive connections after a configurable timeout.</span></span> <span data-ttu-id="cdb8e-378">tooprevent dit u moet een parameter in Hallo SAP NetWeaver ASC's / SCS profiel tooset en Hallo Linux systeeminstellingen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-378">tooprevent this you need tooset a parameter in hello SAP NetWeaver ASCS/SCS profile and change hello Linux system settings.</span></span> <span data-ttu-id="cdb8e-379">Lees [SAP-notitie 1410736] [ 1410736] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-379">Please read [SAP Note 1410736][1410736] for more information.</span></span>
   
   <span data-ttu-id="cdb8e-380">Hallo ASC's / SCS profiel parameter CLR niet/encni/set_so_keepalive is al toegevoegd in de laatste stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-380">hello ASCS/SCS profile parameter enque/encni/set_so_keepalive was already added in hello last step.</span></span>

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. <span data-ttu-id="cdb8e-381">**[A]**  Hello SAP gebruikers na de installatie van de Hallo configureren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-381">**[A]** Configure hello SAP users after hello installation</span></span>
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. <span data-ttu-id="cdb8e-382">**[1]**  Hello ASC's en Ebruikers SAP services toohello sapservice bestand toevoegen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-382">**[1]** Add hello ASCS and ERS SAP services toohello sapservice file</span></span>

   <span data-ttu-id="cdb8e-383">Hallo ASC's service vermelding toohello tweede knooppunt en de kopie Hallo Ebruikers service vermelding toohello eerste knooppunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-383">Add hello ASCS service entry toohello second node and copy hello ERS service entry toohello first node.</span></span>

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. <span data-ttu-id="cdb8e-384">**[1]**  Hello SAP-clusterbronnen maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-384">**[1]** Create hello SAP cluster resources</span></span>

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   <span data-ttu-id="cdb8e-385">Zorg ervoor dat de clusterstatus Hallo ok is en dat alle resources worden gestart.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-385">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="cdb8e-386">Het is niet belangrijk welke bronnen van de Hallo knooppunt worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-386">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="cdb8e-387">STONITH apparaat maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-387">Create STONITH device</span></span>

<span data-ttu-id="cdb8e-388">Hallo STONITH apparaat maakt gebruik van een Service-Principal tooauthorize tegen Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-388">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="cdb8e-389">Volg deze stappen toocreate een Service-Principal.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-389">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="cdb8e-390">Ga te<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="cdb8e-390">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="cdb8e-391">Open hello Azure Active Directory-blade</span><span class="sxs-lookup"><span data-stu-id="cdb8e-391">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="cdb8e-392">Ga tooProperties en schrijf Hallo Directory-id. Dit is Hallo **tenant-id**.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-392">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="cdb8e-393">Klik op App-registraties</span><span class="sxs-lookup"><span data-stu-id="cdb8e-393">Click App registrations</span></span>
1. <span data-ttu-id="cdb8e-394">Klik op Add.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-394">Click Add</span></span>
1. <span data-ttu-id="cdb8e-395">Voer een naam, selecteer toepassingstype 'Web-app /-API, een aanmeldings-URL (bijvoorbeeld http://localhost) en klik op maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-395">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="cdb8e-396">Hallo aanmeldings-URL kan niet wordt gebruikt en geldige URL</span><span class="sxs-lookup"><span data-stu-id="cdb8e-396">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="cdb8e-397">Selecteer de nieuwe App Hallo en sleutels op in het tabblad Hallo-instellingen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-397">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="cdb8e-398">Voer een beschrijving voor een nieuwe sleutel, selecteer 'Verloopt nooit' en klik op Opslaan</span><span class="sxs-lookup"><span data-stu-id="cdb8e-398">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="cdb8e-399">Schrijf Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-399">Write down hello Value.</span></span> <span data-ttu-id="cdb8e-400">Deze wordt gebruikt als Hallo **wachtwoord** voor Hallo Service-Principal</span><span class="sxs-lookup"><span data-stu-id="cdb8e-400">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="cdb8e-401">Schrijf Hallo toepassings-id. Deze wordt gebruikt als gebruikersnaam Hallo (**aanmeldings-id** in de onderstaande stappen voor Hallo) Hallo Service-Principal</span><span class="sxs-lookup"><span data-stu-id="cdb8e-401">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="cdb8e-402">Hallo Service-Principal heeft geen machtigingen tooaccess uw Azure-resources standaard.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-402">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="cdb8e-403">Moet u toogive Hallo Service-Principal machtigingen toostart en gestopt (toewijzing ongedaan maken) alle virtuele machines van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-403">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="cdb8e-404">Ga toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="cdb8e-404">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="cdb8e-405">Open de blade van alle resources Hallo</span><span class="sxs-lookup"><span data-stu-id="cdb8e-405">Open hello All resources blade</span></span>
1. <span data-ttu-id="cdb8e-406">Selecteer Hallo virtuele machine</span><span class="sxs-lookup"><span data-stu-id="cdb8e-406">Select hello virtual machine</span></span>
1. <span data-ttu-id="cdb8e-407">Klik op toegangsbeheer (IAM)</span><span class="sxs-lookup"><span data-stu-id="cdb8e-407">Click Access control (IAM)</span></span>
1. <span data-ttu-id="cdb8e-408">Klik op Add.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-408">Click Add</span></span>
1. <span data-ttu-id="cdb8e-409">Selecteer Hallo rol eigenaar</span><span class="sxs-lookup"><span data-stu-id="cdb8e-409">Select hello role Owner</span></span>
1. <span data-ttu-id="cdb8e-410">Voer de naam Hallo van Hallo-toepassing die u hierboven hebt gemaakt</span><span class="sxs-lookup"><span data-stu-id="cdb8e-410">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="cdb8e-411">Klik op OK</span><span class="sxs-lookup"><span data-stu-id="cdb8e-411">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="cdb8e-412">**[1]**  Hello STONITH apparaten maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-412">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="cdb8e-413">Nadat u machtigingen voor virtuele machines die Hallo Hallo bewerkt, kunt u Hallo STONITH apparaten kunt configureren in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-413">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="cdb8e-414">**[1]**  Hello gebruik van een apparaat STONITH inschakelen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-414">**[1]** Enable hello use of a STONITH device</span></span>

<span data-ttu-id="cdb8e-415">Hallo-gebruik van een apparaat STONITH inschakelen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-415">Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a><span data-ttu-id="cdb8e-416">Installeren van de database</span><span class="sxs-lookup"><span data-stu-id="cdb8e-416">Install database</span></span>

<span data-ttu-id="cdb8e-417">In dit voorbeeld is een SAP HANA System Replication geïnstalleerd en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-417">In this example an SAP HANA System Replication is installed and configured.</span></span> <span data-ttu-id="cdb8e-418">SAP HANA in hetzelfde cluster als Hallo SAP NetWeaver ASC's / SCS en Ebruikers Hallo uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-418">SAP HANA will run in hello same cluster as hello SAP NetWeaver ASCS/SCS and ERS.</span></span> <span data-ttu-id="cdb8e-419">U kunt ook een SAP HANA installeren op een cluster toegewezen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-419">You can also install SAP HANA on a dedicated cluster.</span></span> <span data-ttu-id="cdb8e-420">Zie [hoge beschikbaarheid van SAP HANA op Azure Virtual Machines (VM's)] [ sap-hana-ha] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-420">See [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha] for more information.</span></span>

### <a name="prepare-for-sap-hana-installation"></a><span data-ttu-id="cdb8e-421">Voorbereiden voor SAP HANA-installatie</span><span class="sxs-lookup"><span data-stu-id="cdb8e-421">Prepare for SAP HANA installation</span></span>

<span data-ttu-id="cdb8e-422">In het algemeen wordt aangeraden met LVM voor volumes die bij het opslaan van gegevens en logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-422">We generally recommend using LVM for volumes that store data and log files.</span></span> <span data-ttu-id="cdb8e-423">U kunt ook toostore Hallo gegevens en logboekbestanden bestand rechtstreeks op een gewone schijf kiezen voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-423">For testing purposes, you can also choose toostore hello data and log file directly on a plain disk.</span></span>

1. <span data-ttu-id="cdb8e-424">**[A]**  LVM</span><span class="sxs-lookup"><span data-stu-id="cdb8e-424">**[A]** LVM</span></span>  
   <span data-ttu-id="cdb8e-425">Hallo in het volgende voorbeeld wordt ervan uitgegaan dat Hallo virtuele machines vier gegevensschijven gekoppeld die gebruikt toocreate twee volumes worden moeten.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-425">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
   
   <span data-ttu-id="cdb8e-426">Fysieke volumes voor alle schijven die u toouse wilt maken.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-426">Create physical volumes for all disks that you want toouse.</span></span>
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   <span data-ttu-id="cdb8e-427">Een volume-groep voor gegevensbestanden hello, één volume groep Hallo-logboekbestanden en één voor de gedeelde map Hallo van SAP HANA maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-427">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   <span data-ttu-id="cdb8e-428">Hallo logische volumes maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-428">Create hello logical volumes</span></span>
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   <span data-ttu-id="cdb8e-429">Hallo koppelpunt mappen maken en kopieer Hallo UUID van alle logische volumes</span><span class="sxs-lookup"><span data-stu-id="cdb8e-429">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   <span data-ttu-id="cdb8e-430">Autofs vermeldingen voor Hallo drie logische volumes maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-430">Create autofs entries for hello three logical volumes</span></span>
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   <span data-ttu-id="cdb8e-431">Deze regel toosudo vi /etc/auto.direct invoegen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-431">Insert this line toosudo vi /etc/auto.direct</span></span>
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   <span data-ttu-id="cdb8e-432">Hallo nieuwe volumes koppelen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-432">Mount hello new volumes</span></span>
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. <span data-ttu-id="cdb8e-433">**[A]**  Gewone schijven</span><span class="sxs-lookup"><span data-stu-id="cdb8e-433">**[A]** Plain Disks</span></span>  

   <span data-ttu-id="cdb8e-434">Voor kleine of demo-systemen, kunt u uw bestanden HANA gegevens en logboekbestanden op één schijf plaatsen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-434">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="cdb8e-435">Hallo volgende opdrachten een partitie maken op /dev/sdc en formatteert u het met xfs.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-435">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   <span data-ttu-id="cdb8e-436">Deze regel too/etc/auto.direct invoegen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-436">Insert this line too/etc/auto.direct</span></span>
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   <span data-ttu-id="cdb8e-437">Hallo doelmap maken en Hallo schijf koppelen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-437">Create hello target directory and mount hello disk.</span></span>
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a><span data-ttu-id="cdb8e-438">SAP HANA installeren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-438">Installing SAP HANA</span></span>

<span data-ttu-id="cdb8e-439">Hallo volgende stappen zijn gebaseerd op hoofdstuk 4 Hallo [SAP HANA SR prestaties geoptimaliseerd Scenario handleiding] [ suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-439">hello following steps are based on chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span> <span data-ttu-id="cdb8e-440">Lees dit voordat u Hallo-installatie doorgaat.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-440">Please read it before you continue hello installation.</span></span>

1. <span data-ttu-id="cdb8e-441">**[A]**  Hdblcm vanaf HANA DVD hello uitvoeren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-441">**[A]** Run hdblcm from hello HANA DVD</span></span>
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. <span data-ttu-id="cdb8e-442">**[A]**  SAP Hostagent bijwerken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-442">**[A]** Upgrade SAP Host Agent</span></span>

   <span data-ttu-id="cdb8e-443">Hallo nieuwste SAP Hostagent archief downloaden van Hallo [SAP Softwarecenter] [ sap-swcenter] en uitvoeren hello na de opdracht tooupgrade Hallo agent.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-443">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="cdb8e-444">Hallo pad toohello archief toopoint toohello door u gedownloade bestand vervangen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-444">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. <span data-ttu-id="cdb8e-445">**[1]**  Maken HANA-replicatie (als root)</span><span class="sxs-lookup"><span data-stu-id="cdb8e-445">**[1]** Create HANA replication (as root)</span></span>  

   <span data-ttu-id="cdb8e-446">Hallo volgende opdracht worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-446">Run hello following command.</span></span> <span data-ttu-id="cdb8e-447">Zorg ervoor dat tooreplace vet tekenreeksen (HANA systeem-ID HDB en exemplaar getal 03) met Hallo waarden van de SAP HANA-installatie.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-447">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. <span data-ttu-id="cdb8e-448">**[A]**  Keystore-vermelding (als root) maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-448">**[A]** Create keystore entry (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. <span data-ttu-id="cdb8e-449">**[1]**  Backup database (als root)</span><span class="sxs-lookup"><span data-stu-id="cdb8e-449">**[1]** Backup database (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. <span data-ttu-id="cdb8e-450">**[1]**  Toohello HANA sapsid gebruiker wisselen en maak Hallo primaire site.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-450">**[1]** Switch toohello HANA sapsid user and create hello primary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. <span data-ttu-id="cdb8e-451">**[2]**  Toohello HANA sapsid gebruiker wisselen en Hallo secundaire site maken.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-451">**[2]** Switch toohello HANA sapsid user and create hello secondary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. <span data-ttu-id="cdb8e-452">**[1]**  Clusterbronnen SAP HANA maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-452">**[1]** Create SAP HANA cluster resources</span></span>

   <span data-ttu-id="cdb8e-453">Maak eerst Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-453">First, create hello topology.</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   <span data-ttu-id="cdb8e-454">Maak vervolgens Hallo HANA resources</span><span class="sxs-lookup"><span data-stu-id="cdb8e-454">Next, create hello HANA resources</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="cdb8e-455">Zorg ervoor dat de clusterstatus Hallo ok is en dat alle resources worden gestart.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-455">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="cdb8e-456">Het is niet belangrijk welke bronnen van de Hallo knooppunt worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-456">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="cdb8e-457">**[1]**  Installatie Hallo SAP NetWeaver database-exemplaar</span><span class="sxs-lookup"><span data-stu-id="cdb8e-457">**[1]** Install hello SAP NetWeaver database instance</span></span>

   <span data-ttu-id="cdb8e-458">Installatie Hallo SAP NetWeaver database-exemplaar als hoofdmap met behulp van een virtuele hostnaam die is toegewezen toohello IP-adres van de load balancer frontend-configuratie voor de database Hallo Hallo bijvoorbeeld <b>nws-db</b> en <b>10.0.0.12</b>.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-458">Install hello SAP NetWeaver database instance as root using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello database for example <b>nws-db</b> and <b>10.0.0.12</b>.</span></span>

   <span data-ttu-id="cdb8e-459">U kunt Hallo sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow een niet-hoofdgebruiker tooconnect toosapinst gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-459">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a><span data-ttu-id="cdb8e-460">SAP NetWeaver application server-installatie</span><span class="sxs-lookup"><span data-stu-id="cdb8e-460">SAP NetWeaver application server installation</span></span>

<span data-ttu-id="cdb8e-461">Volg deze stappen tooinstall een SAP-toepassingsserver.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-461">Follow these steps tooinstall an SAP application server.</span></span> <span data-ttu-id="cdb8e-462">Hallo stappen onderstaande wordt ervan uitgegaan dat u de toepassingsserver Hallo op een server die verschilt van Hallo ASC's / SCS en HANA servers installeert.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-462">hello steps bellow assume that you install hello application server on a server different from hello ASCS/SCS and HANA servers.</span></span> <span data-ttu-id="cdb8e-463">Anders zijn bepaalde Hallo stappen hieronder (zoals het configureren van hostnamen) niet nodig.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-463">Otherwise some of hello steps below (like configuring host name resolution) are not needed.</span></span>

1. <span data-ttu-id="cdb8e-464">Setup van hostnaamomzetting</span><span class="sxs-lookup"><span data-stu-id="cdb8e-464">Setup host name resolution</span></span>    
   <span data-ttu-id="cdb8e-465">U kunt een DNS-server gebruiken of Hallo/etc/hosts op alle knooppunten wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-465">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="cdb8e-466">Dit voorbeeld toont hoe toouse Hallo/etc/hosts-bestand.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-466">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="cdb8e-467">Hallo IP-adres en hostnaam in de volgende opdrachten Hallo Hallo vervangen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-467">Replace hello IP address and hello hostname in hello following commands</span></span>
   ```bash
   sudo vi /etc/hosts
   ```
   <span data-ttu-id="cdb8e-468">Invoegen Hallo regels te/etc/hosts te volgen.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-468">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="cdb8e-469">Uw omgeving voor het IP-adres en hostnaam toomatch Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-469">Change hello IP address and hostname toomatch your environment</span></span>    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. <span data-ttu-id="cdb8e-470">Hallo sapmnt map maken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-470">Create hello sapmnt directory</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. <span data-ttu-id="cdb8e-471">Autofs configureren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-471">Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="cdb8e-472">Maak een nieuw bestand met</span><span class="sxs-lookup"><span data-stu-id="cdb8e-472">Create a new file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   <span data-ttu-id="cdb8e-473">Opnieuw opstarten autofs toomount Hallo nieuwe shares</span><span class="sxs-lookup"><span data-stu-id="cdb8e-473">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="cdb8e-474">Wisselbestand configureren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-474">Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="cdb8e-475">Opnieuw Hallo Agent tooactivate Hallo wijziging</span><span class="sxs-lookup"><span data-stu-id="cdb8e-475">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. <span data-ttu-id="cdb8e-476">SAP NetWeaver application server installeren</span><span class="sxs-lookup"><span data-stu-id="cdb8e-476">Install SAP NetWeaver application server</span></span>

   <span data-ttu-id="cdb8e-477">Een primaire of extra SAP NetWeaver toepassingsserver installeren.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-477">Install a primary or additional SAP NetWeaver applications server.</span></span>

   <span data-ttu-id="cdb8e-478">U kunt Hallo sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow een niet-hoofdgebruiker tooconnect toosapinst gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-478">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="cdb8e-479">SAP HANA secure store bijwerken</span><span class="sxs-lookup"><span data-stu-id="cdb8e-479">Update SAP HANA secure store</span></span>

   <span data-ttu-id="cdb8e-480">Update Hallo SAP HANA beveiligde toopoint toohello virtuele naam van Hallo SAP HANA System replicatie-instellingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="cdb8e-480">Update hello SAP HANA secure store toopoint toohello virtual name of hello SAP HANA System Replication setup.</span></span>
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a><span data-ttu-id="cdb8e-481">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cdb8e-481">Next steps</span></span>
* <span data-ttu-id="cdb8e-482">[Azure virtuele Machines, planning en implementatie voor SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="cdb8e-482">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="cdb8e-483">[Azure virtuele Machines-implementatie voor SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="cdb8e-483">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="cdb8e-484">[Azure virtuele Machines DBMS-implementatie voor SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="cdb8e-484">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="cdb8e-485">hoe tooestablish hoge beschikbaarheid en herstel na noodgevallen van SAP HANA plannen in Azure (grote exemplaren), Zie toolearn [SAP HANA (grote exemplaren) hoge beschikbaarheid en herstel na noodgevallen op Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="cdb8e-485">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
* <span data-ttu-id="cdb8e-486">hoe tooestablish hoge beschikbaarheid en herstel na noodgevallen van SAP HANA plannen op Azure Virtual machines, Zie toolearn [hoge beschikbaarheid van SAP HANA op Azure Virtual Machines (VM's)][sap-hana-ha]</span><span class="sxs-lookup"><span data-stu-id="cdb8e-486">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure VMs, see [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha]</span></span>

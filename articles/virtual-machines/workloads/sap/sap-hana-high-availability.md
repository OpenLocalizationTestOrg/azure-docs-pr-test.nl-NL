---
title: aaaHigh beschikbaarheid van SAP HANA op Azure Virtual Machines (VM's) | Microsoft Docs
description: Hoge beschikbaarheid van SAP HANA op Azure virtuele Machines (VM's) maken.
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="402a0-103">Hoge beschikbaarheid van SAP HANA op Azure virtuele Machines (VM's)</span><span class="sxs-lookup"><span data-stu-id="402a0-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

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

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="402a0-113">On-premises kunt u beide HANA System-replicatie gebruiken of gedeelde opslag tooestablish hoge beschikbaarheid voor SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="402a0-113">On-premises, you can use either HANA System Replication or use shared storage tooestablish high availability for SAP HANA.</span></span>
<span data-ttu-id="402a0-114">Wordt alleen ondersteund HANA System Replication instellen in Azure.</span><span class="sxs-lookup"><span data-stu-id="402a0-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="402a0-115">SAP HANA replicatie bestaat uit één hoofdknooppunt en ten minste één slave knooppunt.</span><span class="sxs-lookup"><span data-stu-id="402a0-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="402a0-116">Wijzigingen toohello gegevens op het hoofdknooppunt Hallo zijn gerepliceerd toohello slave knooppunten synchroon of asynchroon.</span><span class="sxs-lookup"><span data-stu-id="402a0-116">Changes toohello data on hello master node are replicated toohello slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="402a0-117">Dit artikel wordt beschreven hoe toodeploy Hallo virtuele machines Hallo virtuele machines configureren, Hallo cluster framework hebt geïnstalleerd, installeren en configureren SAP HANA System Replication.</span><span class="sxs-lookup"><span data-stu-id="402a0-117">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="402a0-118">Installatie opdrachten enzovoort exemplaarnummer 03 in Hallo Voorbeeldconfiguraties en HANA systeem-ID HDB wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="402a0-118">In hello example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="402a0-119">Hallo eerst na de SAP-opmerkingen en documenten lezen</span><span class="sxs-lookup"><span data-stu-id="402a0-119">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="402a0-120">SAP-notitie [1928533], die is:</span><span class="sxs-lookup"><span data-stu-id="402a0-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="402a0-121">Lijst met Azure VM-grootten die worden ondersteund voor de implementatie van Hallo van SAP-software</span><span class="sxs-lookup"><span data-stu-id="402a0-121">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="402a0-122">Informatie over belangrijke capaciteit voor Azure VM-grootten</span><span class="sxs-lookup"><span data-stu-id="402a0-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="402a0-123">Ondersteunde SAP-software en besturingssysteem (OS) en combinaties van de database</span><span class="sxs-lookup"><span data-stu-id="402a0-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="402a0-124">Vereiste SAP-kernel-versie voor Windows en Linux op Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="402a0-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="402a0-125">SAP-notitie [2015553] bevat vereisten voor software-implementaties SAP SAP ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="402a0-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="402a0-126">SAP-notitie [2205917] heeft aanbevolen OS-instellingen voor SUSE Linux Enterprise Server voor SAP-toepassingen</span><span class="sxs-lookup"><span data-stu-id="402a0-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="402a0-127">SAP-notitie [1944799] heeft SAP HANA richtlijnen voor SUSE Linux Enterprise Server voor SAP-toepassingen</span><span class="sxs-lookup"><span data-stu-id="402a0-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="402a0-128">SAP-notitie [2178632] bevat gedetailleerde informatie over alle bewaking metrische gegevens die zijn gerapporteerd voor SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="402a0-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="402a0-129">SAP-notitie [2191498] Hallo vereist SAP Host Agent-versie voor Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="402a0-129">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="402a0-130">SAP-notitie [2243692] bevat informatie over SAP licentieverlening op Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="402a0-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="402a0-131">SAP-notitie [1984787] heeft algemene informatie over SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="402a0-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="402a0-132">SAP-notitie [1999351] bevat aanvullende informatie over probleemoplossing voor hello Azure verbeterde extensie Monitoring voor SAP.</span><span class="sxs-lookup"><span data-stu-id="402a0-132">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="402a0-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) heeft alle SAP-opmerkingen voor Linux vereist.</span><span class="sxs-lookup"><span data-stu-id="402a0-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="402a0-134">[Azure virtuele Machines, planning en implementatie voor SAP op Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="402a0-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="402a0-135">[Azure virtuele Machines-implementatie voor SAP op Linux (in dit artikel)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="402a0-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="402a0-136">[Azure virtuele Machines DBMS-implementatie voor SAP op Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="402a0-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="402a0-137">[SAP HANA SR prestaties geoptimaliseerd Scenario] [ suse-hana-ha-guide] Hallo handleiding bevat alle vereiste gegevens tooset van SAP HANA System Replication on-premises.</span><span class="sxs-lookup"><span data-stu-id="402a0-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="402a0-138">Deze handleiding gebruiken als basislijn.</span><span class="sxs-lookup"><span data-stu-id="402a0-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="402a0-139">Linux implementeren</span><span class="sxs-lookup"><span data-stu-id="402a0-139">Deploying Linux</span></span>

<span data-ttu-id="402a0-140">Hallo resource agent voor SAP HANA is opgenomen in SUSE Linux Enterprise Server voor SAP-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="402a0-140">hello resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="402a0-141">Hello Azure Marketplace bevat een afbeelding voor SUSE Linux Enterprise Server voor SAP-toepassingen 12 met BYOS (uw eigen abonnement Bring) waarmee u toodeploy nieuwe virtuele machines kunt.</span><span class="sxs-lookup"><span data-stu-id="402a0-141">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use toodeploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="402a0-142">Handmatige implementatie</span><span class="sxs-lookup"><span data-stu-id="402a0-142">Manual Deployment</span></span>

1. <span data-ttu-id="402a0-143">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="402a0-143">Create a Resource Group</span></span>
1. <span data-ttu-id="402a0-144">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="402a0-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="402a0-145">Twee Storage-Accounts maken</span><span class="sxs-lookup"><span data-stu-id="402a0-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="402a0-146">Een Beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="402a0-146">Create an Availability Set</span></span>  
   <span data-ttu-id="402a0-147">De maximale updatedomein instellen</span><span class="sxs-lookup"><span data-stu-id="402a0-147">Set max update domain</span></span>
1. <span data-ttu-id="402a0-148">Maak een Load Balancer (intern)</span><span class="sxs-lookup"><span data-stu-id="402a0-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="402a0-149">Selecteer VNET van de bovenstaande stap</span><span class="sxs-lookup"><span data-stu-id="402a0-149">Select VNET of step above</span></span>
1. <span data-ttu-id="402a0-150">Virtuele Machine 1 maken</span><span class="sxs-lookup"><span data-stu-id="402a0-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="402a0-151">https://Portal.Azure.com/#Create/SUSE-byos.SLES-for-SAP-byos12-SP1</span><span class="sxs-lookup"><span data-stu-id="402a0-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="402a0-152">SLES voor SAP toepassingen 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="402a0-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="402a0-153">Selecteer de Storage-Account 1</span><span class="sxs-lookup"><span data-stu-id="402a0-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="402a0-154">Beschikbaarheidsset selecteren</span><span class="sxs-lookup"><span data-stu-id="402a0-154">Select Availability Set</span></span>  
1. <span data-ttu-id="402a0-155">Virtuele Machine 2 maken</span><span class="sxs-lookup"><span data-stu-id="402a0-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="402a0-156">https://Portal.Azure.com/#Create/SUSE-byos.SLES-for-SAP-byos12-SP1</span><span class="sxs-lookup"><span data-stu-id="402a0-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="402a0-157">SLES voor SAP toepassingen 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="402a0-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="402a0-158">Selecteer Opslagaccount 2</span><span class="sxs-lookup"><span data-stu-id="402a0-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="402a0-159">Beschikbaarheidsset selecteren</span><span class="sxs-lookup"><span data-stu-id="402a0-159">Select Availability Set</span></span>  
1. <span data-ttu-id="402a0-160">Gegevensschijven toevoegen</span><span class="sxs-lookup"><span data-stu-id="402a0-160">Add Data Disks</span></span>
1. <span data-ttu-id="402a0-161">Hallo load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="402a0-161">Configure hello load balancer</span></span>
    1. <span data-ttu-id="402a0-162">Een frontend-IP-adresgroep maken</span><span class="sxs-lookup"><span data-stu-id="402a0-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="402a0-163">Hallo load balancer te openen, selecteer frontend-IP-adresgroep en klik op toevoegen</span><span class="sxs-lookup"><span data-stu-id="402a0-163">Open hello load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="402a0-164">Voer de naam Hallo van Hallo nieuwe frontend IP-adresgroep (bijvoorbeeld hana-frontend)</span><span class="sxs-lookup"><span data-stu-id="402a0-164">Enter hello name of hello new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="402a0-165">Klik op OK</span><span class="sxs-lookup"><span data-stu-id="402a0-165">Click OK</span></span>
        1. <span data-ttu-id="402a0-166">Na het Hallo nieuwe frontend-IP-adresgroep is gemaakt, noteer de IP-adres</span><span class="sxs-lookup"><span data-stu-id="402a0-166">After hello new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="402a0-167">Een back endpool maken</span><span class="sxs-lookup"><span data-stu-id="402a0-167">Create a backend pool</span></span>
        1. <span data-ttu-id="402a0-168">Hallo load balancer te openen, selecteer back-endpools en klikt u op toevoegen</span><span class="sxs-lookup"><span data-stu-id="402a0-168">Open hello load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="402a0-169">Voer de naam Hallo van Hallo nieuwe back-endpool (bijvoorbeeld hana-back-end)</span><span class="sxs-lookup"><span data-stu-id="402a0-169">Enter hello name of hello new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="402a0-170">Klik op een virtuele machine toevoegen</span><span class="sxs-lookup"><span data-stu-id="402a0-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="402a0-171">Selecteer Hallo Beschikbaarheidsset u eerder hebt gemaakt</span><span class="sxs-lookup"><span data-stu-id="402a0-171">Select hello Availability Set you created earlier</span></span>
        1. <span data-ttu-id="402a0-172">Selecteer de virtuele machines Hallo van Hallo SAP HANA-cluster</span><span class="sxs-lookup"><span data-stu-id="402a0-172">Select hello virtual machines of hello SAP HANA cluster</span></span>
        1. <span data-ttu-id="402a0-173">Klik op OK</span><span class="sxs-lookup"><span data-stu-id="402a0-173">Click OK</span></span>
    1. <span data-ttu-id="402a0-174">Een health test maken</span><span class="sxs-lookup"><span data-stu-id="402a0-174">Create a health probe</span></span>
       1. <span data-ttu-id="402a0-175">Hallo load balancer openen, selecteer statuscontroles en klikt u op toevoegen</span><span class="sxs-lookup"><span data-stu-id="402a0-175">Open hello load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="402a0-176">Voer de naam Hallo van Hallo nieuwe health test (bijvoorbeeld hana-hp)</span><span class="sxs-lookup"><span data-stu-id="402a0-176">Enter hello name of hello new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="402a0-177">Selecteer TCP als protocol, poort 625**03**, houd Interval 5 en de drempelwaarde voor onjuiste status 2</span><span class="sxs-lookup"><span data-stu-id="402a0-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="402a0-178">Klik op OK</span><span class="sxs-lookup"><span data-stu-id="402a0-178">Click OK</span></span>
    1. <span data-ttu-id="402a0-179">Taakverdelingsregels maken</span><span class="sxs-lookup"><span data-stu-id="402a0-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="402a0-180">Open Hallo load balancer en taakverdelingsregels Selecteer klikt u op toevoegen</span><span class="sxs-lookup"><span data-stu-id="402a0-180">Open hello load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="402a0-181">Voer Hallo-naam van de nieuwe regel voor load balancer hello (bijvoorbeeld hana-lb-3**03**15)</span><span class="sxs-lookup"><span data-stu-id="402a0-181">Enter hello name of hello new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="402a0-182">Selecteer Hallo frontend-IP-adres, back-endpool en health test u eerder hebt gemaakt (bijvoorbeeld hana-frontend)</span><span class="sxs-lookup"><span data-stu-id="402a0-182">Select hello frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="402a0-183">Protocol TCP houden, voert u poort 3**03**15</span><span class="sxs-lookup"><span data-stu-id="402a0-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="402a0-184">Minuten van inactiviteit too30 verhogen</span><span class="sxs-lookup"><span data-stu-id="402a0-184">Increase idle timeout too30 minutes</span></span>
       1. <span data-ttu-id="402a0-185">**Zorg ervoor dat tooenable zwevend IP**</span><span class="sxs-lookup"><span data-stu-id="402a0-185">**Make sure tooenable Floating IP**</span></span>
        1. <span data-ttu-id="402a0-186">Klik op OK</span><span class="sxs-lookup"><span data-stu-id="402a0-186">Click OK</span></span>
        1. <span data-ttu-id="402a0-187">Hallo bovenstaande stappen herhalen voor poort 3**03**17</span><span class="sxs-lookup"><span data-stu-id="402a0-187">Repeat hello steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="402a0-188">Implementeren met sjabloon</span><span class="sxs-lookup"><span data-stu-id="402a0-188">Deploy with template</span></span>
<span data-ttu-id="402a0-189">Kunt u een van Hallo snel starten-sjablonen op github toodeploy alle vereiste bronnen.</span><span class="sxs-lookup"><span data-stu-id="402a0-189">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="402a0-190">Hallo sjabloon implementeert Hallo virtuele machines, Hallo load balancer, beschikbaarheidsset enzovoort. Volg deze stappen toodeploy Hallo sjabloon:</span><span class="sxs-lookup"><span data-stu-id="402a0-190">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="402a0-191">Open Hallo [databasesjabloon] [ template-multisid-db] of Hallo [geconvergeerde sjabloon] [ template-converged] op Hallo Azure Portal maakt Hallo databasesjabloon alleen Hallo regels voor taakverdeling voor een database hello terwijl Hallo geconvergeerde sjabloon ook maakt taakverdeling regels voor een ASC's / SCS en Ebruikers (alleen voor Linux)-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="402a0-191">Open hello [database template][template-multisid-db] or hello [converged template][template-converged] on hello Azure Portal hello database template only creates hello load-balancing rules for a database whereas hello converged template also creates hello load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="402a0-192">Als u van plan een SAP NetWeaver gebaseerd systeem tooinstall bent en u ook tooinstall Hallo wilt ASC's / SCS exemplaar op Hallo dezelfde machines, gebruik Hallo [geconvergeerde sjabloon][template-converged].</span><span class="sxs-lookup"><span data-stu-id="402a0-192">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello ASCS/SCS instance on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="402a0-193">Hallo volgende parameters opgeven</span><span class="sxs-lookup"><span data-stu-id="402a0-193">Enter hello following parameters</span></span>
    1. <span data-ttu-id="402a0-194">SAP-systeem-Id</span><span class="sxs-lookup"><span data-stu-id="402a0-194">Sap System Id</span></span>  
       <span data-ttu-id="402a0-195">Voer Hallo SAP-systeem Id Hallo gewenste tooinstall SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="402a0-195">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="402a0-196">Hallo-Id wordt gebruikt als een voorvoegsel voor Hallo-resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="402a0-196">hello Id will be used as a prefix for hello resources that are deployed.</span></span>
    1. <span data-ttu-id="402a0-197">Stack-Type (alleen van toepassing als u Hallo geconvergeerde sjabloon gebruikt)</span><span class="sxs-lookup"><span data-stu-id="402a0-197">Stack Type (only applicable if you use hello converged template)</span></span>  
       <span data-ttu-id="402a0-198">Hallo SAP NetWeaver stack-type selecteren</span><span class="sxs-lookup"><span data-stu-id="402a0-198">Select hello SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="402a0-199">Type besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="402a0-199">Os Type</span></span>  
       <span data-ttu-id="402a0-200">Selecteer een van de Linux-distributies Hallo.</span><span class="sxs-lookup"><span data-stu-id="402a0-200">Select one of hello Linux distributions.</span></span> <span data-ttu-id="402a0-201">Selecteer voor dit voorbeeld SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="402a0-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="402a0-202">DB-Type</span><span class="sxs-lookup"><span data-stu-id="402a0-202">Db Type</span></span>  
       <span data-ttu-id="402a0-203">Selecteer HANA</span><span class="sxs-lookup"><span data-stu-id="402a0-203">Select HANA</span></span>
    1. <span data-ttu-id="402a0-204">Grootte van het SAP</span><span class="sxs-lookup"><span data-stu-id="402a0-204">Sap System Size</span></span>  
       <span data-ttu-id="402a0-205">Hallo hoeveelheid SAP's Hallo nieuw systeem bieden.</span><span class="sxs-lookup"><span data-stu-id="402a0-205">hello amount of SAPS hello new system will provide.</span></span> <span data-ttu-id="402a0-206">Als u niet zeker weet hoeveel SAP's Hallo systeem is vereist, vraag uw SAP-technologie Partner of System Integrator</span><span class="sxs-lookup"><span data-stu-id="402a0-206">If you are not sure how many SAPS hello system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="402a0-207">Beschikbaarheid van het systeem</span><span class="sxs-lookup"><span data-stu-id="402a0-207">System Availability</span></span>  
       <span data-ttu-id="402a0-208">Selecteer HA</span><span class="sxs-lookup"><span data-stu-id="402a0-208">Select HA</span></span>
    1. <span data-ttu-id="402a0-209">Gebruikersnaam van de beheerder en het wachtwoord van beheerder</span><span class="sxs-lookup"><span data-stu-id="402a0-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="402a0-210">Een nieuwe gebruiker gemaakt, dat de gebruikte toolog op toohello machine kunnen worden.</span><span class="sxs-lookup"><span data-stu-id="402a0-210">A new user is created that can be used toolog on toohello machine.</span></span>
    1. <span data-ttu-id="402a0-211">Nieuwe of bestaande Subnet</span><span class="sxs-lookup"><span data-stu-id="402a0-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="402a0-212">Bepaalt of een nieuw virtueel netwerk en subnet moeten worden gemaakt of een bestaand subnet moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="402a0-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="402a0-213">Als u al een virtueel netwerk dat is verbonden tooyour on-premises netwerk hebt, selecteert u de bestaande.</span><span class="sxs-lookup"><span data-stu-id="402a0-213">If you already have a virtual network that is connected tooyour on-premises network, select existing.</span></span>
    1. <span data-ttu-id="402a0-214">Subnet-Id</span><span class="sxs-lookup"><span data-stu-id="402a0-214">Subnet Id</span></span>  
    <span data-ttu-id="402a0-215">Hallo-ID van Hallo subnet toowhich Hallo virtuele machines moet worden aangesloten.</span><span class="sxs-lookup"><span data-stu-id="402a0-215">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="402a0-216">Selecteer subnet Hallo van uw VPN- of Express Route virtueel netwerk tooconnect Hallo virtuele machine tooyour on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="402a0-216">Select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="402a0-217">Hallo-ID meestal ziet eruit als /subscriptions/`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`></span><span class="sxs-lookup"><span data-stu-id="402a0-217">hello ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="402a0-218">Instellen van Linux HA</span><span class="sxs-lookup"><span data-stu-id="402a0-218">Setting up Linux HA</span></span>

<span data-ttu-id="402a0-219">Hallo volgende items worden voorafgegaan door een [A] - knooppunten van de toepasselijke tooall, [1] - alleen van toepassing toonode 1 of [2] - alleen van toepassing toonode 2.</span><span class="sxs-lookup"><span data-stu-id="402a0-219">hello following items are prefixed with either [A] - applicable tooall nodes, [1] - only applicable toonode 1 or [2] - only applicable toonode 2.</span></span>

1. <span data-ttu-id="402a0-220">[A] SLES voor SAP BYOS alleen - registreren SLES toobe kunnen toouse Hallo opslagplaatsen</span><span class="sxs-lookup"><span data-stu-id="402a0-220">[A] SLES for SAP BYOS only - Register SLES toobe able toouse hello repositories</span></span>
1. <span data-ttu-id="402a0-221">[A] SLES voor SAP BYOS alleen - toevoegen openbare cloud module</span><span class="sxs-lookup"><span data-stu-id="402a0-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="402a0-222">[A] SLES bijwerken</span><span class="sxs-lookup"><span data-stu-id="402a0-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="402a0-223">[1] ssh toegang inschakelen</span><span class="sxs-lookup"><span data-stu-id="402a0-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="402a0-224">[2] ssh toegang inschakelen</span><span class="sxs-lookup"><span data-stu-id="402a0-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="402a0-225">[1] ssh toegang inschakelen</span><span class="sxs-lookup"><span data-stu-id="402a0-225">[1] Enable ssh access</span></span>
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="402a0-226">[A] HA-uitbreiding installeren</span><span class="sxs-lookup"><span data-stu-id="402a0-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="402a0-227">[A] indeling van setup-schijf</span><span class="sxs-lookup"><span data-stu-id="402a0-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="402a0-228">LVM</span><span class="sxs-lookup"><span data-stu-id="402a0-228">LVM</span></span>  
    <span data-ttu-id="402a0-229">In het algemeen wordt aangeraden toouse LVM voor volumes die bij het opslaan van gegevens en logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="402a0-229">We generally recommend toouse LVM for volumes that store data and log files.</span></span> <span data-ttu-id="402a0-230">Hallo in het volgende voorbeeld wordt ervan uitgegaan dat Hallo virtuele machines vier gegevensschijven gekoppeld die gebruikt toocreate twee volumes worden moeten.</span><span class="sxs-lookup"><span data-stu-id="402a0-230">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
        * <span data-ttu-id="402a0-231">Fysieke volumes voor alle schijven die u toouse wilt maken.</span><span class="sxs-lookup"><span data-stu-id="402a0-231">Create physical volumes for all disks that you want toouse.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="402a0-232">Een volume-groep voor gegevensbestanden hello, één volume groep Hallo-logboekbestanden en één voor de gedeelde map Hallo van SAP HANA maken</span><span class="sxs-lookup"><span data-stu-id="402a0-232">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="402a0-233">Hallo logische volumes maken</span><span class="sxs-lookup"><span data-stu-id="402a0-233">Create hello logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="402a0-234">Hallo koppelpunt mappen maken en kopieer Hallo UUID van alle logische volumes</span><span class="sxs-lookup"><span data-stu-id="402a0-234">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="402a0-235">Fstab-vermeldingen voor Hallo drie logische volumes maken</span><span class="sxs-lookup"><span data-stu-id="402a0-235">Create fstab entries for hello three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="402a0-236">Deze regel te/etc/fstab invoegen</span><span class="sxs-lookup"><span data-stu-id="402a0-236">Insert this line too/etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="402a0-237">Hallo nieuwe volumes koppelen</span><span class="sxs-lookup"><span data-stu-id="402a0-237">Mount hello new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="402a0-238">Gewone schijven</span><span class="sxs-lookup"><span data-stu-id="402a0-238">Plain Disks</span></span>  
       <span data-ttu-id="402a0-239">Voor kleine of demo-systemen, kunt u uw bestanden HANA gegevens en logboekbestanden op één schijf plaatsen.</span><span class="sxs-lookup"><span data-stu-id="402a0-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="402a0-240">Hallo volgende opdrachten een partitie maken op /dev/sdc en formatteert u het met xfs.</span><span class="sxs-lookup"><span data-stu-id="402a0-240">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a><span data-ttu-id="402a0-241">Schrijf Hallo-id van /dev/sdc1</span><span class="sxs-lookup"><span data-stu-id="402a0-241">write down hello id of /dev/sdc1</span></span>
    <span data-ttu-id="402a0-242">sudo/sbin/blkid sudo vi/etc/fstab-fouten</span><span class="sxs-lookup"><span data-stu-id="402a0-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="402a0-243">[A] setup hostnaamomzetting voor alle hosts</span><span class="sxs-lookup"><span data-stu-id="402a0-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="402a0-244">U kunt een DNS-server gebruiken of Hallo/etc/hosts op alle knooppunten wijzigen.</span><span class="sxs-lookup"><span data-stu-id="402a0-244">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="402a0-245">Dit voorbeeld toont hoe toouse Hallo/etc/hosts-bestand.</span><span class="sxs-lookup"><span data-stu-id="402a0-245">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="402a0-246">Hallo IP-adres en hostnaam in de volgende opdrachten Hallo Hallo vervangen</span><span class="sxs-lookup"><span data-stu-id="402a0-246">Replace hello IP address and hello hostname in hello following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="402a0-247">Invoegen Hallo regels te/etc/hosts te volgen.</span><span class="sxs-lookup"><span data-stu-id="402a0-247">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="402a0-248">Uw omgeving voor het IP-adres en hostnaam toomatch Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="402a0-248">Change hello IP address and hostname toomatch your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="402a0-249">[1] Cluster installeren</span><span class="sxs-lookup"><span data-stu-id="402a0-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="402a0-250">[2] knooppunt toocluster toevoegen</span><span class="sxs-lookup"><span data-stu-id="402a0-250">[2] Add node toocluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="402a0-251">[A] wijziging hacluster wachtwoord toohello hetzelfde wachtwoord</span><span class="sxs-lookup"><span data-stu-id="402a0-251">[A] Change hacluster password toohello same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="402a0-252">[A] configureren corosync toouse andere transport en nodelist toevoegen.</span><span class="sxs-lookup"><span data-stu-id="402a0-252">[A] Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="402a0-253">Cluster werkt niet anders.</span><span class="sxs-lookup"><span data-stu-id="402a0-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="402a0-254">Hallo volgende vet inhoud toohello toevoegen.</span><span class="sxs-lookup"><span data-stu-id="402a0-254">Add hello following bold content toohello file.</span></span>
    
    <pre><code> 
    [...]
      interface { 
          [...] 
      }
      <b>transport:      udpu</b>
    } 
    <b>nodelist {
      node {
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    <span data-ttu-id="402a0-255">Hallo corosync service opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="402a0-255">Then restart hello corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="402a0-256">[A] HANA HA-pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="402a0-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="402a0-257">SAP HANA installeren</span><span class="sxs-lookup"><span data-stu-id="402a0-257">Installing SAP HANA</span></span>

<span data-ttu-id="402a0-258">Ga als volgt hoofdstuk 4 Hallo [SAP HANA SR prestaties geoptimaliseerd Scenario handleiding] [ suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span><span class="sxs-lookup"><span data-stu-id="402a0-258">Follow chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span>

1. <span data-ttu-id="402a0-259">[A] hdblcm vanaf HANA DVD hello uitvoeren</span><span class="sxs-lookup"><span data-stu-id="402a0-259">[A] Run hdblcm from hello HANA DVD</span></span>
    * <span data-ttu-id="402a0-260">Installatie te kiezen,-1 ></span><span class="sxs-lookup"><span data-stu-id="402a0-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="402a0-261">Selecteer extra onderdelen voor installatie-1 ></span><span class="sxs-lookup"><span data-stu-id="402a0-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="402a0-262">Voer installatiepad [/ hana/gedeelde]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="402a0-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="402a0-263">Voer de naam van de lokale Host [.]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="402a0-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="402a0-264">Wilt u tooadd extra hosts toohello system?</span><span class="sxs-lookup"><span data-stu-id="402a0-264">Do you want tooadd additional hosts toohello system?</span></span> <span data-ttu-id="402a0-265">(j/n) [n]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="402a0-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="402a0-266">Voer SAP HANA systeem-ID:<SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="402a0-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="402a0-267">Voer exemplaarnummer [00]:</span><span class="sxs-lookup"><span data-stu-id="402a0-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="402a0-268">HANA exemplaarnummer.</span><span class="sxs-lookup"><span data-stu-id="402a0-268">HANA Instance number.</span></span> <span data-ttu-id="402a0-269">03 gebruiken als u hello Azure-sjabloon gebruikt of gevolgd Hallo in bovenstaand voorbeeld</span><span class="sxs-lookup"><span data-stu-id="402a0-269">Use 03 if you used hello Azure Template or followed hello example above</span></span>
    * <span data-ttu-id="402a0-270">Selecteer Database modus / Index [1] op Enter: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="402a0-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="402a0-271">Selecteer systeemgebruik / Voer Index [4]:</span><span class="sxs-lookup"><span data-stu-id="402a0-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="402a0-272">Selecteer Hallo systeem gebruik</span><span class="sxs-lookup"><span data-stu-id="402a0-272">Select hello system Usage</span></span>
    * <span data-ttu-id="402a0-273">Geef de locatie van gegevensvolumes [/ data/hana/HDB]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="402a0-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="402a0-274">Geef de locatie van Logboekvolumes [/ log/hana/HDB]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="402a0-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="402a0-275">Maximale geheugentoewijzing beperken?</span><span class="sxs-lookup"><span data-stu-id="402a0-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="402a0-276">[n]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="402a0-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="402a0-277">Geef '...' Host-naam van het certificaat voor Host [...]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="402a0-277">Enter Certificate Host Name For Host '...' [...]: -> ENTER</span></span>
    * <span data-ttu-id="402a0-278">Voer SAP Host Agent gebruiker (sapadm) wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="402a0-278">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="402a0-279">SAP Host Agent gebruiker (sapadm) wachtwoord bevestigen:</span><span class="sxs-lookup"><span data-stu-id="402a0-279">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="402a0-280">Voer de systeembeheerder (hdbadm) wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="402a0-280">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="402a0-281">Systeembeheerder (hdbadm) wachtwoord bevestigen:</span><span class="sxs-lookup"><span data-stu-id="402a0-281">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="402a0-282">Voer systeembeheerder basismap [/ usr/sap/HDB/home]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="402a0-282">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="402a0-283">Voer systeembeheerder aanmeldingsshell [/ bin/servicel]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="402a0-283">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="402a0-284">Voer systeembeheerder gebruikers-ID [1001]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="402a0-284">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="402a0-285">Voer-ID van gebruikersgroep (sapsys) [79]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="402a0-285">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="402a0-286">Geef het wachtwoord voor Database gebruiker (systeem):</span><span class="sxs-lookup"><span data-stu-id="402a0-286">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="402a0-287">Bevestig Database gebruikerswachtwoord (systeem):</span><span class="sxs-lookup"><span data-stu-id="402a0-287">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="402a0-288">Systeem opnieuw opstarten nadat de computer opnieuw is opgestart?</span><span class="sxs-lookup"><span data-stu-id="402a0-288">Restart system after machine reboot?</span></span> <span data-ttu-id="402a0-289">[n]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="402a0-289">[n]: -> ENTER</span></span>
    * <span data-ttu-id="402a0-290">Wilt u toocontinue?</span><span class="sxs-lookup"><span data-stu-id="402a0-290">Do you want toocontinue?</span></span> <span data-ttu-id="402a0-291">(j/n):</span><span class="sxs-lookup"><span data-stu-id="402a0-291">(y/n):</span></span>  
  <span data-ttu-id="402a0-292">Hallo samenvatting valideren en y toocontinue invoeren</span><span class="sxs-lookup"><span data-stu-id="402a0-292">Validate hello summary and enter y toocontinue</span></span>
1. <span data-ttu-id="402a0-293">[A] SAP Hostagent bijwerken</span><span class="sxs-lookup"><span data-stu-id="402a0-293">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="402a0-294">Hallo nieuwste SAP Hostagent archief downloaden van Hallo [SAP Softwarecenter] [ sap-swcenter] en uitvoeren hello na de opdracht tooupgrade Hallo agent.</span><span class="sxs-lookup"><span data-stu-id="402a0-294">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="402a0-295">Hallo pad toohello archief toopoint toohello door u gedownloade bestand vervangen.</span><span class="sxs-lookup"><span data-stu-id="402a0-295">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. <span data-ttu-id="402a0-296">[1] HANA replicatie maken (als root)</span><span class="sxs-lookup"><span data-stu-id="402a0-296">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="402a0-297">Hallo volgende opdracht worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="402a0-297">Run hello following command.</span></span> <span data-ttu-id="402a0-298">Zorg ervoor dat tooreplace vet tekenreeksen (HANA systeem-ID HDB en exemplaar getal 03) met Hallo waarden van de SAP HANA-installatie.</span><span class="sxs-lookup"><span data-stu-id="402a0-298">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="402a0-299">[A] keystore-vermelding maken (als root)</span><span class="sxs-lookup"><span data-stu-id="402a0-299">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="402a0-300">[1] back-updatabase (als root)</span><span class="sxs-lookup"><span data-stu-id="402a0-300">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="402a0-301">[1] toohello sapsid gebruiker (bijvoorbeeld hdbadm) switch en maak Hallo primaire site.</span><span class="sxs-lookup"><span data-stu-id="402a0-301">[1] Switch toohello sapsid user (for example hdbadm) and create hello primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="402a0-302">[2] overschakelen toohello sapsid gebruiker (bijvoorbeeld hdbadm) en Hallo secundaire site maken.</span><span class="sxs-lookup"><span data-stu-id="402a0-302">[2] Switch toohello sapsid user (for example hdbadm) and create hello secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="402a0-303">Cluster-Framework configureren</span><span class="sxs-lookup"><span data-stu-id="402a0-303">Configure Cluster Framework</span></span>

<span data-ttu-id="402a0-304">Hallo standaardinstellingen wijzigen</span><span class="sxs-lookup"><span data-stu-id="402a0-304">Change hello default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="402a0-305">Nu laden we Hallo toohello bestandscluster</span><span class="sxs-lookup"><span data-stu-id="402a0-305">now we load hello file toohello cluster</span></span>
<span data-ttu-id="402a0-306">sudo crm load update crm-defaults.txt configureren</span><span class="sxs-lookup"><span data-stu-id="402a0-306">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="402a0-307">STONITH apparaat maken</span><span class="sxs-lookup"><span data-stu-id="402a0-307">Create STONITH device</span></span>

<span data-ttu-id="402a0-308">Hallo STONITH apparaat maakt gebruik van een Service-Principal tooauthorize tegen Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="402a0-308">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="402a0-309">Volg deze stappen toocreate een Service-Principal.</span><span class="sxs-lookup"><span data-stu-id="402a0-309">Please follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="402a0-310">Ga te<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="402a0-310">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="402a0-311">Open hello Azure Active Directory-blade</span><span class="sxs-lookup"><span data-stu-id="402a0-311">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="402a0-312">Ga tooProperties en schrijf Hallo Directory-id. Dit is Hallo **tenant-id**.</span><span class="sxs-lookup"><span data-stu-id="402a0-312">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="402a0-313">Klik op App-registraties</span><span class="sxs-lookup"><span data-stu-id="402a0-313">Click App registrations</span></span>
1. <span data-ttu-id="402a0-314">Klik op Add.</span><span class="sxs-lookup"><span data-stu-id="402a0-314">Click Add</span></span>
1. <span data-ttu-id="402a0-315">Voer een naam, selecteer toepassingstype 'Web-app /-API, een aanmeldings-URL (bijvoorbeeld http://localhost) en klik op maken</span><span class="sxs-lookup"><span data-stu-id="402a0-315">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="402a0-316">Hallo aanmeldings-URL kan niet wordt gebruikt en geldige URL</span><span class="sxs-lookup"><span data-stu-id="402a0-316">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="402a0-317">Selecteer de nieuwe App Hallo en sleutels op in het tabblad Hallo-instellingen</span><span class="sxs-lookup"><span data-stu-id="402a0-317">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="402a0-318">Voer een beschrijving voor een nieuwe sleutel, selecteer 'Verloopt nooit' en klik op Opslaan</span><span class="sxs-lookup"><span data-stu-id="402a0-318">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="402a0-319">Schrijf Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="402a0-319">Write down hello Value.</span></span> <span data-ttu-id="402a0-320">Deze wordt gebruikt als Hallo **wachtwoord** voor Hallo Service-Principal</span><span class="sxs-lookup"><span data-stu-id="402a0-320">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="402a0-321">Schrijf Hallo toepassings-id. Deze wordt gebruikt als gebruikersnaam Hallo (**aanmeldings-id** in de onderstaande stappen voor Hallo) Hallo Service-Principal</span><span class="sxs-lookup"><span data-stu-id="402a0-321">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="402a0-322">Hallo Service-Principal heeft geen machtigingen tooaccess uw Azure-resources standaard.</span><span class="sxs-lookup"><span data-stu-id="402a0-322">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="402a0-323">Moet u toogive Hallo Service-Principal machtigingen toostart en gestopt (toewijzing ongedaan maken) alle virtuele machines van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="402a0-323">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="402a0-324">Ga toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="402a0-324">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="402a0-325">Open de blade van alle resources Hallo</span><span class="sxs-lookup"><span data-stu-id="402a0-325">Open hello All resources blade</span></span>
1. <span data-ttu-id="402a0-326">Selecteer Hallo virtuele machine</span><span class="sxs-lookup"><span data-stu-id="402a0-326">Select hello virtual machine</span></span>
1. <span data-ttu-id="402a0-327">Klik op toegangsbeheer (IAM)</span><span class="sxs-lookup"><span data-stu-id="402a0-327">Click Access control (IAM)</span></span>
1. <span data-ttu-id="402a0-328">Klik op Add.</span><span class="sxs-lookup"><span data-stu-id="402a0-328">Click Add</span></span>
1. <span data-ttu-id="402a0-329">Selecteer Hallo rol eigenaar</span><span class="sxs-lookup"><span data-stu-id="402a0-329">Select hello role Owner</span></span>
1. <span data-ttu-id="402a0-330">Voer de naam Hallo van Hallo-toepassing die u hierboven hebt gemaakt</span><span class="sxs-lookup"><span data-stu-id="402a0-330">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="402a0-331">Klik op OK</span><span class="sxs-lookup"><span data-stu-id="402a0-331">Click OK</span></span>

<span data-ttu-id="402a0-332">Nadat u machtigingen voor virtuele machines die Hallo Hallo bewerkt, kunt u Hallo STONITH apparaten kunt configureren in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="402a0-332">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="402a0-333">Nu laden we Hallo toohello bestandscluster</span><span class="sxs-lookup"><span data-stu-id="402a0-333">now we load hello file toohello cluster</span></span>
<span data-ttu-id="402a0-334">sudo crm load update crm-fencing.txt configureren</span><span class="sxs-lookup"><span data-stu-id="402a0-334">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="402a0-335">SAP HANA-resources maken</span><span class="sxs-lookup"><span data-stu-id="402a0-335">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="402a0-336">Nu laden we Hallo toohello bestandscluster</span><span class="sxs-lookup"><span data-stu-id="402a0-336">now we load hello file toohello cluster</span></span>
<span data-ttu-id="402a0-337">sudo crm load update crm-saphanatop.txt configureren</span><span class="sxs-lookup"><span data-stu-id="402a0-337">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="402a0-338">Nu laden we Hallo toohello bestandscluster</span><span class="sxs-lookup"><span data-stu-id="402a0-338">now we load hello file toohello cluster</span></span>
<span data-ttu-id="402a0-339">sudo crm load update crm-saphana.txt configureren</span><span class="sxs-lookup"><span data-stu-id="402a0-339">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="402a0-340">Test-cluster instellen</span><span class="sxs-lookup"><span data-stu-id="402a0-340">Test cluster setup</span></span>
<span data-ttu-id="402a0-341">Hallo volgende hoofdstuk wordt beschreven hoe u uw instellingen kunt testen.</span><span class="sxs-lookup"><span data-stu-id="402a0-341">hello following chapter describe how you can test your setup.</span></span> <span data-ttu-id="402a0-342">Elke test wordt ervan uitgegaan dat u hoofdmap en Hallo SAP HANA-master wordt uitgevoerd op Hallo virtuele machine saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="402a0-342">Every test assumes that you are root and hello SAP HANA master is running on hello virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="402a0-343">Hekwerk Test</span><span class="sxs-lookup"><span data-stu-id="402a0-343">Fencing Test</span></span>

<span data-ttu-id="402a0-344">Hallo-setup van Hallo hekwerk agent kunt u testen door de netwerkinterface Hallo op knooppunt saphanavm1 uit te schakelen.</span><span class="sxs-lookup"><span data-stu-id="402a0-344">You can test hello setup of hello fencing agent by disabling hello network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="402a0-345">Hallo virtuele machine moet nu ophalen opnieuw gestart of gestopt, afhankelijk van uw clusterconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="402a0-345">hello virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="402a0-346">Als u Hallo stonith actie toooff instelt, Hallo virtuele machine wordt gestopt en Hallo bronnen gemigreerde toohello virtuele machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="402a0-346">If you set hello stonith-action toooff, hello virtual machine will be stopped and hello resources are migrated toohello running virtual machine.</span></span>

<span data-ttu-id="402a0-347">Zodra u Hallo virtuele machine opnieuw start, Hallo SAP HANA-resource toostart als secundaire zal mislukken als u AUTOMATED_REGISTER instellen = "false".</span><span class="sxs-lookup"><span data-stu-id="402a0-347">Once you start hello virtual machine again, hello SAP HANA resource will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="402a0-348">In dit geval moet u tooconfigure Hallo HANA exemplaar als secundaire door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="402a0-348">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="402a0-349">Een handmatige failover testen</span><span class="sxs-lookup"><span data-stu-id="402a0-349">Testing a manual failover</span></span>

<span data-ttu-id="402a0-350">U kunt een handmatige failover testen Hallo pacemaker heeft door service te stoppen op knooppunt saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="402a0-350">You can test a manual failover by stopping hello pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="402a0-351">U kunt Hallo-service opnieuw starten na een failover Hallo.</span><span class="sxs-lookup"><span data-stu-id="402a0-351">After hello failover, you can start hello service again.</span></span> <span data-ttu-id="402a0-352">Hallo SAP HANA-bron op saphanavm1 toostart als secundaire zal mislukken als u AUTOMATED_REGISTER instellen = "false".</span><span class="sxs-lookup"><span data-stu-id="402a0-352">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="402a0-353">In dit geval moet u tooconfigure Hallo HANA exemplaar als secundaire door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="402a0-353">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="402a0-354">Een migratie testen</span><span class="sxs-lookup"><span data-stu-id="402a0-354">Testing a migration</span></span>

<span data-ttu-id="402a0-355">U kunt Hallo SAP HANA-hoofdknooppunt migreren door het uitvoeren van de volgende opdracht Hallo</span><span class="sxs-lookup"><span data-stu-id="402a0-355">You can migrate hello SAP HANA master node by executing hello following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="402a0-356">Dit moet migreren Hallo SAP HANA-hoofdknooppunt en Hallo-groep die Hallo virtuele IP-adres toosaphanavm2 bevat.</span><span class="sxs-lookup"><span data-stu-id="402a0-356">This should migrate hello SAP HANA master node and hello group that contains hello virtual IP address toosaphanavm2.</span></span>
<span data-ttu-id="402a0-357">Hallo SAP HANA-bron op saphanavm1 toostart als secundaire zal mislukken als u AUTOMATED_REGISTER instellen = "false".</span><span class="sxs-lookup"><span data-stu-id="402a0-357">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="402a0-358">In dit geval moet u tooconfigure Hallo HANA exemplaar als secundaire door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="402a0-358">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="402a0-359">Hallo migratie maakt locatie beperkingen die toobe opnieuw verwijderd moeten.</span><span class="sxs-lookup"><span data-stu-id="402a0-359">hello migration creates location contraints that need toobe deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="402a0-360">U moet ook toocleanup Hallo status van Hallo secundair knooppunt resource</span><span class="sxs-lookup"><span data-stu-id="402a0-360">You also need toocleanup hello state of hello secondary node resource</span></span>

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="402a0-361">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="402a0-361">Next steps</span></span>
* <span data-ttu-id="402a0-362">[Azure virtuele Machines, planning en implementatie voor SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="402a0-362">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="402a0-363">[Azure virtuele Machines-implementatie voor SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="402a0-363">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="402a0-364">[Azure virtuele Machines DBMS-implementatie voor SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="402a0-364">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="402a0-365">hoe tooestablish hoge beschikbaarheid en herstel na noodgevallen van SAP HANA plannen in Azure (grote exemplaren), Zie toolearn [SAP HANA (grote exemplaren) hoge beschikbaarheid en herstel na noodgevallen op Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="402a0-365">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 

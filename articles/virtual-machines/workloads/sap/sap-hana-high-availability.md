---
title: Hoge beschikbaarheid van SAP HANA op Azure virtuele Machines (VM's) | Microsoft Docs
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
ms.openlocfilehash: 951150e621d21037b0adde7287b9f985290d8d11
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="cef0d-103">Hoge beschikbaarheid van SAP HANA op Azure virtuele Machines (VM's)</span><span class="sxs-lookup"><span data-stu-id="cef0d-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

<span data-ttu-id="cef0d-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span><span class="sxs-lookup"><span data-stu-id="cef0d-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span></span>
<span data-ttu-id="cef0d-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span><span class="sxs-lookup"><span data-stu-id="cef0d-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span></span>
<span data-ttu-id="cef0d-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="cef0d-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="cef0d-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="cef0d-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="cef0d-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="cef0d-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="cef0d-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span><span class="sxs-lookup"><span data-stu-id="cef0d-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span></span>
<span data-ttu-id="cef0d-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="cef0d-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>
<span data-ttu-id="cef0d-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span><span class="sxs-lookup"><span data-stu-id="cef0d-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span></span>
<span data-ttu-id="cef0d-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="cef0d-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="cef0d-113">On-premises kunt u kunt gebruiken beide HANA System Replication of gedeelde opslag gebruiken om hoge beschikbaarheid voor SAP HANA stand te brengen.</span><span class="sxs-lookup"><span data-stu-id="cef0d-113">On-premises, you can use either HANA System Replication or use shared storage to establish high availability for SAP HANA.</span></span>
<span data-ttu-id="cef0d-114">Wordt alleen ondersteund HANA System Replication instellen in Azure.</span><span class="sxs-lookup"><span data-stu-id="cef0d-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="cef0d-115">SAP HANA replicatie bestaat uit één hoofdknooppunt en ten minste één slave knooppunt.</span><span class="sxs-lookup"><span data-stu-id="cef0d-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="cef0d-116">Wijzigingen in de gegevens op het hoofdknooppunt worden gerepliceerd naar de knooppunten slave synchroon of asynchroon.</span><span class="sxs-lookup"><span data-stu-id="cef0d-116">Changes to the data on the master node are replicated to the slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="cef0d-117">In dit artikel wordt beschreven hoe de virtuele machines te implementeren, configureren van de virtuele machines, cluster-framework hebt geïnstalleerd, installeren en configureren van SAP HANA System Replication.</span><span class="sxs-lookup"><span data-stu-id="cef0d-117">This article describes how to deploy the virtual machines, configure the virtual machines, install the cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="cef0d-118">Installatie opdrachten enzovoort exemplaarnummer 03 en HANA systeem-ID HDB wordt gebruikt in de voorbeeldconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="cef0d-118">In the example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="cef0d-119">Lees eerst de volgende opmerkingen bij de SAP en documenten</span><span class="sxs-lookup"><span data-stu-id="cef0d-119">Read the following SAP Notes and papers first</span></span>

* <span data-ttu-id="cef0d-120">SAP-notitie [1928533], die is:</span><span class="sxs-lookup"><span data-stu-id="cef0d-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="cef0d-121">Lijst met Azure VM-grootten die worden ondersteund voor de implementatie van SAP-software</span><span class="sxs-lookup"><span data-stu-id="cef0d-121">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="cef0d-122">Informatie over belangrijke capaciteit voor Azure VM-grootten</span><span class="sxs-lookup"><span data-stu-id="cef0d-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="cef0d-123">Ondersteunde SAP-software en besturingssysteem (OS) en combinaties van de database</span><span class="sxs-lookup"><span data-stu-id="cef0d-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="cef0d-124">Vereiste SAP-kernel-versie voor Windows en Linux op Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="cef0d-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="cef0d-125">SAP-notitie [2015553] bevat vereisten voor software-implementaties SAP SAP ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="cef0d-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="cef0d-126">SAP-notitie [2205917] heeft aanbevolen OS-instellingen voor SUSE Linux Enterprise Server voor SAP-toepassingen</span><span class="sxs-lookup"><span data-stu-id="cef0d-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="cef0d-127">SAP-notitie [1944799] heeft SAP HANA richtlijnen voor SUSE Linux Enterprise Server voor SAP-toepassingen</span><span class="sxs-lookup"><span data-stu-id="cef0d-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="cef0d-128">SAP-notitie [2178632] bevat gedetailleerde informatie over alle bewaking metrische gegevens die zijn gerapporteerd voor SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="cef0d-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="cef0d-129">SAP-notitie [2191498] heeft de vereiste Hostagent SAP-versie voor Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="cef0d-129">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="cef0d-130">SAP-notitie [2243692] bevat informatie over SAP licentieverlening op Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="cef0d-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="cef0d-131">SAP-notitie [1984787] heeft algemene informatie over SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="cef0d-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="cef0d-132">SAP-notitie [1999351] bevat aanvullende informatie over probleemoplossing voor de Azure verbeterde extensie Monitoring voor SAP.</span><span class="sxs-lookup"><span data-stu-id="cef0d-132">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="cef0d-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) heeft alle SAP-opmerkingen voor Linux vereist.</span><span class="sxs-lookup"><span data-stu-id="cef0d-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="cef0d-134">[Azure virtuele Machines, planning en implementatie voor SAP op Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="cef0d-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="cef0d-135">[Azure virtuele Machines-implementatie voor SAP op Linux (in dit artikel)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="cef0d-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="cef0d-136">[Azure virtuele Machines DBMS-implementatie voor SAP op Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="cef0d-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="cef0d-137">[SAP HANA SR prestaties geoptimaliseerd Scenario] [ suse-hana-ha-guide] de handleiding bevat alle benodigde informatie voor het instellen van SAP HANA System Replication on-premises.</span><span class="sxs-lookup"><span data-stu-id="cef0d-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] The guide contains all required information to set up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="cef0d-138">Deze handleiding gebruiken als basislijn.</span><span class="sxs-lookup"><span data-stu-id="cef0d-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="cef0d-139">Linux implementeren</span><span class="sxs-lookup"><span data-stu-id="cef0d-139">Deploying Linux</span></span>

<span data-ttu-id="cef0d-140">De resource-agent voor SAP HANA is opgenomen in SUSE Linux Enterprise Server voor SAP-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="cef0d-140">The resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="cef0d-141">Azure Marketplace bevat een afbeelding voor SUSE Linux Enterprise Server voor SAP-toepassingen 12 met BYOS (uw eigen abonnement Bring) die u gebruiken kunt om nieuwe virtuele machines te implementeren.</span><span class="sxs-lookup"><span data-stu-id="cef0d-141">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use to deploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="cef0d-142">Handmatige implementatie</span><span class="sxs-lookup"><span data-stu-id="cef0d-142">Manual Deployment</span></span>

1. <span data-ttu-id="cef0d-143">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="cef0d-143">Create a Resource Group</span></span>
1. <span data-ttu-id="cef0d-144">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="cef0d-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="cef0d-145">Twee Storage-Accounts maken</span><span class="sxs-lookup"><span data-stu-id="cef0d-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="cef0d-146">Een Beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="cef0d-146">Create an Availability Set</span></span>  
   <span data-ttu-id="cef0d-147">De maximale updatedomein instellen</span><span class="sxs-lookup"><span data-stu-id="cef0d-147">Set max update domain</span></span>
1. <span data-ttu-id="cef0d-148">Maak een Load Balancer (intern)</span><span class="sxs-lookup"><span data-stu-id="cef0d-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="cef0d-149">Selecteer VNET van de bovenstaande stap</span><span class="sxs-lookup"><span data-stu-id="cef0d-149">Select VNET of step above</span></span>
1. <span data-ttu-id="cef0d-150">Virtuele Machine 1 maken</span><span class="sxs-lookup"><span data-stu-id="cef0d-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="cef0d-151">https://Portal.Azure.com/#Create/SUSE-byos.SLES-for-SAP-byos12-SP1</span><span class="sxs-lookup"><span data-stu-id="cef0d-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="cef0d-152">SLES voor SAP toepassingen 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="cef0d-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="cef0d-153">Selecteer de Storage-Account 1</span><span class="sxs-lookup"><span data-stu-id="cef0d-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="cef0d-154">Beschikbaarheidsset selecteren</span><span class="sxs-lookup"><span data-stu-id="cef0d-154">Select Availability Set</span></span>  
1. <span data-ttu-id="cef0d-155">Virtuele Machine 2 maken</span><span class="sxs-lookup"><span data-stu-id="cef0d-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="cef0d-156">https://Portal.Azure.com/#Create/SUSE-byos.SLES-for-SAP-byos12-SP1</span><span class="sxs-lookup"><span data-stu-id="cef0d-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="cef0d-157">SLES voor SAP toepassingen 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="cef0d-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="cef0d-158">Selecteer Opslagaccount 2</span><span class="sxs-lookup"><span data-stu-id="cef0d-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="cef0d-159">Beschikbaarheidsset selecteren</span><span class="sxs-lookup"><span data-stu-id="cef0d-159">Select Availability Set</span></span>  
1. <span data-ttu-id="cef0d-160">Gegevensschijven toevoegen</span><span class="sxs-lookup"><span data-stu-id="cef0d-160">Add Data Disks</span></span>
1. <span data-ttu-id="cef0d-161">De load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="cef0d-161">Configure the load balancer</span></span>
    1. <span data-ttu-id="cef0d-162">Een frontend-IP-adresgroep maken</span><span class="sxs-lookup"><span data-stu-id="cef0d-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="cef0d-163">Openen van de load balancer, selecteer frontend-IP-adresgroep en klik op toevoegen</span><span class="sxs-lookup"><span data-stu-id="cef0d-163">Open the load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="cef0d-164">Voer de naam van de nieuwe frontend IP-adresgroep (bijvoorbeeld hana-frontend)</span><span class="sxs-lookup"><span data-stu-id="cef0d-164">Enter the name of the new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="cef0d-165">Klik op OK</span><span class="sxs-lookup"><span data-stu-id="cef0d-165">Click OK</span></span>
        1. <span data-ttu-id="cef0d-166">Nadat de nieuwe frontend-IP-adresgroep is gemaakt, noteert u het IP-adres</span><span class="sxs-lookup"><span data-stu-id="cef0d-166">After the new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="cef0d-167">Een back endpool maken</span><span class="sxs-lookup"><span data-stu-id="cef0d-167">Create a backend pool</span></span>
        1. <span data-ttu-id="cef0d-168">Openen van de load balancer, back-endpools selecteren en klik op toevoegen</span><span class="sxs-lookup"><span data-stu-id="cef0d-168">Open the load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="cef0d-169">Voer de naam van de nieuwe back-endpool (bijvoorbeeld hana-back-end)</span><span class="sxs-lookup"><span data-stu-id="cef0d-169">Enter the name of the new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="cef0d-170">Klik op een virtuele machine toevoegen</span><span class="sxs-lookup"><span data-stu-id="cef0d-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="cef0d-171">Selecteer de Beschikbaarheidsset u eerder hebt gemaakt</span><span class="sxs-lookup"><span data-stu-id="cef0d-171">Select the Availability Set you created earlier</span></span>
        1. <span data-ttu-id="cef0d-172">Selecteer de virtuele machines van het SAP HANA-cluster</span><span class="sxs-lookup"><span data-stu-id="cef0d-172">Select the virtual machines of the SAP HANA cluster</span></span>
        1. <span data-ttu-id="cef0d-173">Klik op OK</span><span class="sxs-lookup"><span data-stu-id="cef0d-173">Click OK</span></span>
    1. <span data-ttu-id="cef0d-174">Een health test maken</span><span class="sxs-lookup"><span data-stu-id="cef0d-174">Create a health probe</span></span>
       1. <span data-ttu-id="cef0d-175">Openen van de load balancer, statuscontroles selecteren en klik op toevoegen</span><span class="sxs-lookup"><span data-stu-id="cef0d-175">Open the load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="cef0d-176">Voer de naam van de nieuwe health test (bijvoorbeeld hana-hp)</span><span class="sxs-lookup"><span data-stu-id="cef0d-176">Enter the name of the new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="cef0d-177">Selecteer TCP als protocol, poort 625**03**, houd Interval 5 en de drempelwaarde voor onjuiste status 2</span><span class="sxs-lookup"><span data-stu-id="cef0d-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="cef0d-178">Klik op OK</span><span class="sxs-lookup"><span data-stu-id="cef0d-178">Click OK</span></span>
    1. <span data-ttu-id="cef0d-179">Taakverdelingsregels maken</span><span class="sxs-lookup"><span data-stu-id="cef0d-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="cef0d-180">Open de load balancer en taakverdelingsregels Selecteer klikt u op toevoegen</span><span class="sxs-lookup"><span data-stu-id="cef0d-180">Open the load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="cef0d-181">Voer de naam van de load balancer-regel (bijvoorbeeld hana-lb-3**03**15)</span><span class="sxs-lookup"><span data-stu-id="cef0d-181">Enter the name of the new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="cef0d-182">Selecteer de frontend-IP-adres, back-endpool en health test u eerder hebt gemaakt (bijvoorbeeld hana-frontend)</span><span class="sxs-lookup"><span data-stu-id="cef0d-182">Select the frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="cef0d-183">Protocol TCP houden, voert u poort 3**03**15</span><span class="sxs-lookup"><span data-stu-id="cef0d-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="cef0d-184">Verhoog de time-out voor inactiviteit tot 30 minuten</span><span class="sxs-lookup"><span data-stu-id="cef0d-184">Increase idle timeout to 30 minutes</span></span>
       1. <span data-ttu-id="cef0d-185">**Zorg ervoor dat u kunt zwevend IP inschakelen**</span><span class="sxs-lookup"><span data-stu-id="cef0d-185">**Make sure to enable Floating IP**</span></span>
        1. <span data-ttu-id="cef0d-186">Klik op OK</span><span class="sxs-lookup"><span data-stu-id="cef0d-186">Click OK</span></span>
        1. <span data-ttu-id="cef0d-187">Herhaal de stappen hierboven voor poort 3**03**17</span><span class="sxs-lookup"><span data-stu-id="cef0d-187">Repeat the steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="cef0d-188">Implementeren met sjabloon</span><span class="sxs-lookup"><span data-stu-id="cef0d-188">Deploy with template</span></span>
<span data-ttu-id="cef0d-189">U kunt een van de snel starten-sjablonen op github gebruiken voor het implementeren van alle vereiste bronnen.</span><span class="sxs-lookup"><span data-stu-id="cef0d-189">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="cef0d-190">De sjabloon wordt geïmplementeerd voor de virtuele machines, de load balancer, beschikbaarheidsset enzovoort. Volg deze stappen voor het implementeren van de sjabloon:</span><span class="sxs-lookup"><span data-stu-id="cef0d-190">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="cef0d-191">Open de [databasesjabloon] [ template-multisid-db] of de [geconvergeerde sjabloon] [ template-converged] in de Azure Portal maakt de databasesjabloon alleen de regels voor taakverdeling voor een database terwijl de geconvergeerde sjabloon ook de regels voor taakverdeling voor een ASC's / SCS en Ebruikers (alleen voor Linux)-exemplaar maakt.</span><span class="sxs-lookup"><span data-stu-id="cef0d-191">Open the [database template][template-multisid-db] or the [converged template][template-converged] on the Azure Portal The database template only creates the load-balancing rules for a database whereas the converged template also creates the load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="cef0d-192">Als u van plan bent een SAP NetWeaver gebaseerd systeem installeren en u ook wilt voor het exemplaar ASC's / SCS installeren op de dezelfde machines, gebruikt u de [geconvergeerde sjabloon][template-converged].</span><span class="sxs-lookup"><span data-stu-id="cef0d-192">If you plan to install an SAP NetWeaver based system and you also want to install the ASCS/SCS instance on the same machines, use the [converged template][template-converged].</span></span>
1. <span data-ttu-id="cef0d-193">Voer de volgende parameters</span><span class="sxs-lookup"><span data-stu-id="cef0d-193">Enter the following parameters</span></span>
    1. <span data-ttu-id="cef0d-194">SAP-systeem-Id</span><span class="sxs-lookup"><span data-stu-id="cef0d-194">Sap System Id</span></span>  
       <span data-ttu-id="cef0d-195">Voer het SAP-systeem Id van het SAP-systeem die u wilt installeren.</span><span class="sxs-lookup"><span data-stu-id="cef0d-195">Enter the SAP system Id of the SAP system you want to install.</span></span> <span data-ttu-id="cef0d-196">De Id zal worden gebruikt als een voorvoegsel voor de resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="cef0d-196">The Id will be used as a prefix for the resources that are deployed.</span></span>
    1. <span data-ttu-id="cef0d-197">Stack-Type (alleen van toepassing als u de sjabloon geconvergeerde gebruikt)</span><span class="sxs-lookup"><span data-stu-id="cef0d-197">Stack Type (only applicable if you use the converged template)</span></span>  
       <span data-ttu-id="cef0d-198">Selecteer het type van de stack SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="cef0d-198">Select the SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="cef0d-199">Type besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="cef0d-199">Os Type</span></span>  
       <span data-ttu-id="cef0d-200">Selecteer een van de Linux-distributies.</span><span class="sxs-lookup"><span data-stu-id="cef0d-200">Select one of the Linux distributions.</span></span> <span data-ttu-id="cef0d-201">Selecteer voor dit voorbeeld SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="cef0d-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="cef0d-202">DB-Type</span><span class="sxs-lookup"><span data-stu-id="cef0d-202">Db Type</span></span>  
       <span data-ttu-id="cef0d-203">Selecteer HANA</span><span class="sxs-lookup"><span data-stu-id="cef0d-203">Select HANA</span></span>
    1. <span data-ttu-id="cef0d-204">Grootte van het SAP</span><span class="sxs-lookup"><span data-stu-id="cef0d-204">Sap System Size</span></span>  
       <span data-ttu-id="cef0d-205">De hoeveelheid SAP's u het nieuwe systeem krijgt.</span><span class="sxs-lookup"><span data-stu-id="cef0d-205">The amount of SAPS the new system will provide.</span></span> <span data-ttu-id="cef0d-206">Als u niet zeker weet hoeveel SAP's u het systeem moet, vraag uw SAP-technologie Partner of System Integrator</span><span class="sxs-lookup"><span data-stu-id="cef0d-206">If you are not sure how many SAPS the system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="cef0d-207">Beschikbaarheid van het systeem</span><span class="sxs-lookup"><span data-stu-id="cef0d-207">System Availability</span></span>  
       <span data-ttu-id="cef0d-208">Selecteer HA</span><span class="sxs-lookup"><span data-stu-id="cef0d-208">Select HA</span></span>
    1. <span data-ttu-id="cef0d-209">Gebruikersnaam van de beheerder en het wachtwoord van beheerder</span><span class="sxs-lookup"><span data-stu-id="cef0d-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="cef0d-210">Een nieuwe gebruiker wordt gemaakt die kunnen worden gebruikt voor aanmelding bij de computer.</span><span class="sxs-lookup"><span data-stu-id="cef0d-210">A new user is created that can be used to log on to the machine.</span></span>
    1. <span data-ttu-id="cef0d-211">Nieuwe of bestaande Subnet</span><span class="sxs-lookup"><span data-stu-id="cef0d-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="cef0d-212">Bepaalt of een nieuw virtueel netwerk en subnet moeten worden gemaakt of een bestaand subnet moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cef0d-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="cef0d-213">Als u al een virtueel netwerk dat is verbonden met uw on-premises netwerk hebt, selecteert u de bestaande.</span><span class="sxs-lookup"><span data-stu-id="cef0d-213">If you already have a virtual network that is connected to your on-premises network, select existing.</span></span>
    1. <span data-ttu-id="cef0d-214">Subnet-Id</span><span class="sxs-lookup"><span data-stu-id="cef0d-214">Subnet Id</span></span>  
    <span data-ttu-id="cef0d-215">De ID van het subnet waarmee de virtuele machines moet worden verbonden.</span><span class="sxs-lookup"><span data-stu-id="cef0d-215">The ID of the subnet to which the virtual machines should be connected to.</span></span> <span data-ttu-id="cef0d-216">Selecteer het subnet van het VPN- of Express Route virtuele netwerk verbinding maken met de virtuele machine van uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="cef0d-216">Select the subnet of your VPN or Express Route virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="cef0d-217">De ID meestal ziet eruit als /subscriptions/`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`></span><span class="sxs-lookup"><span data-stu-id="cef0d-217">The ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="cef0d-218">Instellen van Linux HA</span><span class="sxs-lookup"><span data-stu-id="cef0d-218">Setting up Linux HA</span></span>

<span data-ttu-id="cef0d-219">De volgende items worden voorafgegaan door [A] - van toepassing op alle knooppunten [1] - alleen van toepassing op knooppunt 1 of [2] - alleen van toepassing op knooppunt 2.</span><span class="sxs-lookup"><span data-stu-id="cef0d-219">The following items are prefixed with either [A] - applicable to all nodes, [1] - only applicable to node 1 or [2] - only applicable to node 2.</span></span>

1. <span data-ttu-id="cef0d-220">[A] SLES voor SAP BYOS alleen - SLES om het gebruik van de opslagplaatsen te kunnen registreren</span><span class="sxs-lookup"><span data-stu-id="cef0d-220">[A] SLES for SAP BYOS only - Register SLES to be able to use the repositories</span></span>
1. <span data-ttu-id="cef0d-221">[A] SLES voor SAP BYOS alleen - toevoegen openbare cloud module</span><span class="sxs-lookup"><span data-stu-id="cef0d-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="cef0d-222">[A] SLES bijwerken</span><span class="sxs-lookup"><span data-stu-id="cef0d-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="cef0d-223">[1] ssh toegang inschakelen</span><span class="sxs-lookup"><span data-stu-id="cef0d-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy the public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="cef0d-224">[2] ssh toegang inschakelen</span><span class="sxs-lookup"><span data-stu-id="cef0d-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert the public key you copied in the last step into the authorized keys file on the second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy the public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="cef0d-225">[1] ssh toegang inschakelen</span><span class="sxs-lookup"><span data-stu-id="cef0d-225">[1] Enable ssh access</span></span>
    ```bash
    # insert the public key you copied in the last step into the authorized keys file on the first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="cef0d-226">[A] HA-uitbreiding installeren</span><span class="sxs-lookup"><span data-stu-id="cef0d-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="cef0d-227">[A] indeling van setup-schijf</span><span class="sxs-lookup"><span data-stu-id="cef0d-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="cef0d-228">LVM</span><span class="sxs-lookup"><span data-stu-id="cef0d-228">LVM</span></span>  
    <span data-ttu-id="cef0d-229">In het algemeen wordt aangeraden met LVM voor volumes die bij het opslaan van gegevens en logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="cef0d-229">We generally recommend to use LVM for volumes that store data and log files.</span></span> <span data-ttu-id="cef0d-230">Het volgende voorbeeld wordt ervan uitgegaan dat de virtuele machines vier gegevensschijven gekoppeld die moeten worden gebruikt voor het maken van twee volumes hebben.</span><span class="sxs-lookup"><span data-stu-id="cef0d-230">The example below assumes that the virtual machines have four data disks attached that should be used to create two volumes.</span></span>
        * <span data-ttu-id="cef0d-231">Maak fysieke volumes voor alle schijven die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cef0d-231">Create physical volumes for all disks that you want to use.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="cef0d-232">Maak een groep volume voor de gegevensbestanden, één volume groep voor de logboekbestanden en één voor de gedeelde map van SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cef0d-232">Create a volume group for the data files, one volume group for the log files and one for the shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="cef0d-233">De logische volumes maken</span><span class="sxs-lookup"><span data-stu-id="cef0d-233">Create the logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="cef0d-234">Maak de mappen koppelen en kopieer de UUID van alle logische volumes</span><span class="sxs-lookup"><span data-stu-id="cef0d-234">Create the mount directories and copy the UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down the id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="cef0d-235">Fstab-vermeldingen voor de drie logische volumes maken</span><span class="sxs-lookup"><span data-stu-id="cef0d-235">Create fstab entries for the three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="cef0d-236">Deze regel moet worden /etc/fstab invoegen</span><span class="sxs-lookup"><span data-stu-id="cef0d-236">Insert this line to /etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="cef0d-237">Koppel de nieuwe volumes</span><span class="sxs-lookup"><span data-stu-id="cef0d-237">Mount the new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="cef0d-238">Gewone schijven</span><span class="sxs-lookup"><span data-stu-id="cef0d-238">Plain Disks</span></span>  
       <span data-ttu-id="cef0d-239">Voor kleine of demo-systemen, kunt u uw bestanden HANA gegevens en logboekbestanden op één schijf plaatsen.</span><span class="sxs-lookup"><span data-stu-id="cef0d-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="cef0d-240">De volgende opdrachten een partitie maken op /dev/sdc en formatteert u het met xfs.</span><span class="sxs-lookup"><span data-stu-id="cef0d-240">The following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-the-id-of-devsdc1"></a><span data-ttu-id="cef0d-241">Noteer de id van /dev/sdc1</span><span class="sxs-lookup"><span data-stu-id="cef0d-241">write down the id of /dev/sdc1</span></span>
    <span data-ttu-id="cef0d-242">sudo/sbin/blkid sudo vi/etc/fstab-fouten</span><span class="sxs-lookup"><span data-stu-id="cef0d-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line to /etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create the target directory and mount the disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="cef0d-243">[A] setup hostnaamomzetting voor alle hosts</span><span class="sxs-lookup"><span data-stu-id="cef0d-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="cef0d-244">U kunt gebruik van een DNS-server of wijzig de/etc/hosts op alle knooppunten.</span><span class="sxs-lookup"><span data-stu-id="cef0d-244">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="cef0d-245">In dit voorbeeld laat zien hoe het bestand/etc/hosts te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cef0d-245">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="cef0d-246">Het IP-adres en de hostnaam in de volgende opdrachten vervangen</span><span class="sxs-lookup"><span data-stu-id="cef0d-246">Replace the IP address and the hostname in the following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="cef0d-247">Voeg de volgende regels/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="cef0d-247">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="cef0d-248">Wijzig de IP-adres en hostnaam overeenkomen met uw omgeving</span><span class="sxs-lookup"><span data-stu-id="cef0d-248">Change the IP address and hostname to match your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="cef0d-249">[1] Cluster installeren</span><span class="sxs-lookup"><span data-stu-id="cef0d-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want to continue anyway? [y/N] -> y
    # Network address to bind to (e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish to use SBD? [y/N] -> N
    # Do you wish to configure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="cef0d-250">[2] knooppunt toevoegen aan cluster</span><span class="sxs-lookup"><span data-stu-id="cef0d-250">[2] Add node to cluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured to start at system boot.
    # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
    # Do you want to continue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="cef0d-251">[A] wachtwoord van de wijzigen hacluster naar hetzelfde wachtwoord</span><span class="sxs-lookup"><span data-stu-id="cef0d-251">[A] Change hacluster password to the same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="cef0d-252">[A] corosync voor het gebruik van andere transport en voeg nodelist configureren.</span><span class="sxs-lookup"><span data-stu-id="cef0d-252">[A] Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="cef0d-253">Cluster werkt niet anders.</span><span class="sxs-lookup"><span data-stu-id="cef0d-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="cef0d-254">De volgende vet inhoud toevoegen aan het bestand.</span><span class="sxs-lookup"><span data-stu-id="cef0d-254">Add the following bold content to the file.</span></span>
    
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

    <span data-ttu-id="cef0d-255">Start de service corosync opnieuw</span><span class="sxs-lookup"><span data-stu-id="cef0d-255">Then restart the corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="cef0d-256">[A] HANA HA-pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="cef0d-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="cef0d-257">SAP HANA installeren</span><span class="sxs-lookup"><span data-stu-id="cef0d-257">Installing SAP HANA</span></span>

<span data-ttu-id="cef0d-258">Ga als volgt hoofdstuk 4 van de [SAP HANA SR prestaties geoptimaliseerd Scenario handleiding] [ suse-hana-ha-guide] om SAP HANA System replicatie te installeren.</span><span class="sxs-lookup"><span data-stu-id="cef0d-258">Follow chapter 4 of the [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] to install SAP HANA System Replication.</span></span>

1. <span data-ttu-id="cef0d-259">[A] hdblcm uitvoeren vanaf de DVD HANA</span><span class="sxs-lookup"><span data-stu-id="cef0d-259">[A] Run hdblcm from the HANA DVD</span></span>
    * <span data-ttu-id="cef0d-260">Installatie te kiezen,-1 ></span><span class="sxs-lookup"><span data-stu-id="cef0d-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="cef0d-261">Selecteer extra onderdelen voor installatie-1 ></span><span class="sxs-lookup"><span data-stu-id="cef0d-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="cef0d-262">Voer installatiepad [/ hana/gedeelde]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="cef0d-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="cef0d-263">Voer de naam van de lokale Host [.]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="cef0d-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="cef0d-264">Wilt u extra hosts toevoegen aan het systeem?</span><span class="sxs-lookup"><span data-stu-id="cef0d-264">Do you want to add additional hosts to the system?</span></span> <span data-ttu-id="cef0d-265">(j/n) [n]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="cef0d-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="cef0d-266">Voer SAP HANA systeem-ID:<SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="cef0d-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="cef0d-267">Voer exemplaarnummer [00]:</span><span class="sxs-lookup"><span data-stu-id="cef0d-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="cef0d-268">HANA exemplaarnummer.</span><span class="sxs-lookup"><span data-stu-id="cef0d-268">HANA Instance number.</span></span> <span data-ttu-id="cef0d-269">03 gebruiken als u de Azure-sjabloon gebruikt of in het bovenstaande voorbeeld gevolgd</span><span class="sxs-lookup"><span data-stu-id="cef0d-269">Use 03 if you used the Azure Template or followed the example above</span></span>
    * <span data-ttu-id="cef0d-270">Selecteer Database modus / Index [1] op Enter: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="cef0d-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="cef0d-271">Selecteer systeemgebruik / Voer Index [4]:</span><span class="sxs-lookup"><span data-stu-id="cef0d-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="cef0d-272">Selecteer de informatie over het gebruik van het systeem</span><span class="sxs-lookup"><span data-stu-id="cef0d-272">Select the system Usage</span></span>
    * <span data-ttu-id="cef0d-273">Geef de locatie van gegevensvolumes [/ data/hana/HDB]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="cef0d-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="cef0d-274">Geef de locatie van Logboekvolumes [/ log/hana/HDB]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="cef0d-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="cef0d-275">Maximale geheugentoewijzing beperken?</span><span class="sxs-lookup"><span data-stu-id="cef0d-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="cef0d-276">[n]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="cef0d-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="cef0d-277">Geef '...' Host-naam van het certificaat voor Host</span><span class="sxs-lookup"><span data-stu-id="cef0d-277">Enter Certificate Host Name For Host '...'</span></span> <span data-ttu-id="cef0d-278">[...]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="cef0d-278">[...]: -> ENTER</span></span>
    * <span data-ttu-id="cef0d-279">Voer SAP Host Agent gebruiker (sapadm) wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="cef0d-279">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="cef0d-280">SAP Host Agent gebruiker (sapadm) wachtwoord bevestigen:</span><span class="sxs-lookup"><span data-stu-id="cef0d-280">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="cef0d-281">Voer de systeembeheerder (hdbadm) wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="cef0d-281">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="cef0d-282">Systeembeheerder (hdbadm) wachtwoord bevestigen:</span><span class="sxs-lookup"><span data-stu-id="cef0d-282">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="cef0d-283">Voer systeembeheerder basismap [/ usr/sap/HDB/home]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="cef0d-283">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="cef0d-284">Voer systeembeheerder aanmeldingsshell [/ bin/servicel]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="cef0d-284">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="cef0d-285">Voer systeembeheerder gebruikers-ID [1001]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="cef0d-285">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="cef0d-286">Voer-ID van gebruikersgroep (sapsys) [79]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="cef0d-286">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="cef0d-287">Geef het wachtwoord voor Database gebruiker (systeem):</span><span class="sxs-lookup"><span data-stu-id="cef0d-287">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="cef0d-288">Bevestig Database gebruikerswachtwoord (systeem):</span><span class="sxs-lookup"><span data-stu-id="cef0d-288">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="cef0d-289">Systeem opnieuw opstarten nadat de computer opnieuw is opgestart?</span><span class="sxs-lookup"><span data-stu-id="cef0d-289">Restart system after machine reboot?</span></span> <span data-ttu-id="cef0d-290">[n]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="cef0d-290">[n]: -> ENTER</span></span>
    * <span data-ttu-id="cef0d-291">Wilt u doorgaan?</span><span class="sxs-lookup"><span data-stu-id="cef0d-291">Do you want to continue?</span></span> <span data-ttu-id="cef0d-292">(j/n):</span><span class="sxs-lookup"><span data-stu-id="cef0d-292">(y/n):</span></span>  
  <span data-ttu-id="cef0d-293">Valideren van de samenvatting en voer j om door te gaan</span><span class="sxs-lookup"><span data-stu-id="cef0d-293">Validate the summary and enter y to continue</span></span>
1. <span data-ttu-id="cef0d-294">[A] SAP Hostagent bijwerken</span><span class="sxs-lookup"><span data-stu-id="cef0d-294">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="cef0d-295">Download de meest recente Hostagent SAP-archief van de [SAP Softwarecenter] [ sap-swcenter] en voer de volgende opdracht om de agent bijwerken.</span><span class="sxs-lookup"><span data-stu-id="cef0d-295">Download the latest SAP Host Agent archive from the [SAP Softwarecenter][sap-swcenter] and run the following command to upgrade the agent.</span></span> <span data-ttu-id="cef0d-296">Het pad naar het archief verwijzen naar de door u gedownloade bestand vervangen.</span><span class="sxs-lookup"><span data-stu-id="cef0d-296">Replace the path to the archive to point to the file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path to SAP Host Agent SAR>
    ```

1. <span data-ttu-id="cef0d-297">[1] HANA replicatie maken (als root)</span><span class="sxs-lookup"><span data-stu-id="cef0d-297">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="cef0d-298">Voer de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="cef0d-298">Run the following command.</span></span> <span data-ttu-id="cef0d-299">Zorg ervoor dat vet tekenreeksen (HANA systeem-ID HDB en exemplaar getal 03) vervangen door de waarden van de SAP HANA-installatie.</span><span class="sxs-lookup"><span data-stu-id="cef0d-299">Make sure to replace bold strings (HANA System ID HDB and instance number 03) with the values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN TO <b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="cef0d-300">[A] keystore-vermelding maken (als root)</span><span class="sxs-lookup"><span data-stu-id="cef0d-300">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="cef0d-301">[1] back-updatabase (als root)</span><span class="sxs-lookup"><span data-stu-id="cef0d-301">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="cef0d-302">[1] overschakelen naar de gebruiker sapsid (bijvoorbeeld hdbadm) en de primaire site maken.</span><span class="sxs-lookup"><span data-stu-id="cef0d-302">[1] Switch to the sapsid user (for example hdbadm) and create the primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="cef0d-303">[2] overschakelen naar de gebruiker sapsid (bijvoorbeeld hdbadm) en de secundaire site maken.</span><span class="sxs-lookup"><span data-stu-id="cef0d-303">[2] Switch to the sapsid user (for example hdbadm) and create the secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="cef0d-304">Cluster-Framework configureren</span><span class="sxs-lookup"><span data-stu-id="cef0d-304">Configure Cluster Framework</span></span>

<span data-ttu-id="cef0d-305">De standaardinstellingen wijzigen</span><span class="sxs-lookup"><span data-stu-id="cef0d-305">Change the default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter the following to crm-defaults.txt
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

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="cef0d-306">Nu we het bestand aan het cluster niet laden</span><span class="sxs-lookup"><span data-stu-id="cef0d-306">now we load the file to the cluster</span></span>
<span data-ttu-id="cef0d-307">sudo crm load update crm-defaults.txt configureren</span><span class="sxs-lookup"><span data-stu-id="cef0d-307">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="cef0d-308">STONITH apparaat maken</span><span class="sxs-lookup"><span data-stu-id="cef0d-308">Create STONITH device</span></span>

<span data-ttu-id="cef0d-309">Het apparaat STONITH maakt gebruik van een Service-Principal worden geautoriseerd op basis van Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cef0d-309">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="cef0d-310">Volg deze stappen voor het maken van een Service-Principal.</span><span class="sxs-lookup"><span data-stu-id="cef0d-310">Please follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="cef0d-311">Ga naar <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="cef0d-311">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="cef0d-312">Open de blade van Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cef0d-312">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="cef0d-313">Ga naar eigenschappen en noteer de id van de Directory.</span><span class="sxs-lookup"><span data-stu-id="cef0d-313">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="cef0d-314">Dit is de **tenant-id**.</span><span class="sxs-lookup"><span data-stu-id="cef0d-314">This is the **tenant id**.</span></span>
1. <span data-ttu-id="cef0d-315">Klik op App-registraties</span><span class="sxs-lookup"><span data-stu-id="cef0d-315">Click App registrations</span></span>
1. <span data-ttu-id="cef0d-316">Klik op Add.</span><span class="sxs-lookup"><span data-stu-id="cef0d-316">Click Add</span></span>
1. <span data-ttu-id="cef0d-317">Voer een naam, selecteer toepassingstype 'Web-app /-API, een aanmeldings-URL (bijvoorbeeld http://localhost) en klik op maken</span><span class="sxs-lookup"><span data-stu-id="cef0d-317">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="cef0d-318">De aanmeldings-URL kan niet wordt gebruikt en geldige URL</span><span class="sxs-lookup"><span data-stu-id="cef0d-318">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="cef0d-319">Selecteer de nieuwe App en sleutels op in het tabblad instellingen</span><span class="sxs-lookup"><span data-stu-id="cef0d-319">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="cef0d-320">Voer een beschrijving voor een nieuwe sleutel, selecteer 'Verloopt nooit' en klik op Opslaan</span><span class="sxs-lookup"><span data-stu-id="cef0d-320">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="cef0d-321">Noteer de waarde in.</span><span class="sxs-lookup"><span data-stu-id="cef0d-321">Write down the Value.</span></span> <span data-ttu-id="cef0d-322">Deze wordt gebruikt als de **wachtwoord** voor de Service-Principal</span><span class="sxs-lookup"><span data-stu-id="cef0d-322">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="cef0d-323">Noteer de toepassings-id.</span><span class="sxs-lookup"><span data-stu-id="cef0d-323">Write down the Application Id.</span></span> <span data-ttu-id="cef0d-324">Deze wordt gebruikt als de gebruikersnaam (**aanmeldings-id** in de onderstaande stappen) van de Service-Principal</span><span class="sxs-lookup"><span data-stu-id="cef0d-324">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="cef0d-325">De Service-Principal heeft geen machtigingen voor toegang tot uw Azure-resources standaard.</span><span class="sxs-lookup"><span data-stu-id="cef0d-325">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="cef0d-326">U moet de Service-Principal machtigingen geven om te starten en stoppen (ongedaan gemaakt) alle virtuele machines van het cluster.</span><span class="sxs-lookup"><span data-stu-id="cef0d-326">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="cef0d-327">Ga naar https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="cef0d-327">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="cef0d-328">Open de blade met alle bronnen</span><span class="sxs-lookup"><span data-stu-id="cef0d-328">Open the All resources blade</span></span>
1. <span data-ttu-id="cef0d-329">Selecteer de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="cef0d-329">Select the virtual machine</span></span>
1. <span data-ttu-id="cef0d-330">Klik op toegangsbeheer (IAM)</span><span class="sxs-lookup"><span data-stu-id="cef0d-330">Click Access control (IAM)</span></span>
1. <span data-ttu-id="cef0d-331">Klik op Add.</span><span class="sxs-lookup"><span data-stu-id="cef0d-331">Click Add</span></span>
1. <span data-ttu-id="cef0d-332">Selecteer de rol van eigenaar</span><span class="sxs-lookup"><span data-stu-id="cef0d-332">Select the role Owner</span></span>
1. <span data-ttu-id="cef0d-333">Voer de naam van de toepassing die u hierboven hebt gemaakt</span><span class="sxs-lookup"><span data-stu-id="cef0d-333">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="cef0d-334">Klik op OK</span><span class="sxs-lookup"><span data-stu-id="cef0d-334">Click OK</span></span>

<span data-ttu-id="cef0d-335">Nadat u de machtigingen voor de virtuele machines hebt bewerkt, kunt u de apparaten STONITH configureren in het cluster.</span><span class="sxs-lookup"><span data-stu-id="cef0d-335">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter the following to crm-fencing.txt
# replace the bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="cef0d-336">Nu we het bestand aan het cluster niet laden</span><span class="sxs-lookup"><span data-stu-id="cef0d-336">now we load the file to the cluster</span></span>
<span data-ttu-id="cef0d-337">sudo crm load update crm-fencing.txt configureren</span><span class="sxs-lookup"><span data-stu-id="cef0d-337">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="cef0d-338">SAP HANA-resources maken</span><span class="sxs-lookup"><span data-stu-id="cef0d-338">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter the following to crm-saphana.txt
# replace the bold string with your instance number and HANA system id
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

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="cef0d-339">Nu we het bestand aan het cluster niet laden</span><span class="sxs-lookup"><span data-stu-id="cef0d-339">now we load the file to the cluster</span></span>
<span data-ttu-id="cef0d-340">sudo crm load update crm-saphanatop.txt configureren</span><span class="sxs-lookup"><span data-stu-id="cef0d-340">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter the following to crm-saphana.txt
# replace the bold string with your instance number, HANA system id and the frontend IP address of the Azure load balancer. 
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

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="cef0d-341">Nu we het bestand aan het cluster niet laden</span><span class="sxs-lookup"><span data-stu-id="cef0d-341">now we load the file to the cluster</span></span>
<span data-ttu-id="cef0d-342">sudo crm load update crm-saphana.txt configureren</span><span class="sxs-lookup"><span data-stu-id="cef0d-342">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="cef0d-343">Test-cluster instellen</span><span class="sxs-lookup"><span data-stu-id="cef0d-343">Test cluster setup</span></span>
<span data-ttu-id="cef0d-344">Het volgende hoofdstuk wordt beschreven hoe u uw instellingen kunt testen.</span><span class="sxs-lookup"><span data-stu-id="cef0d-344">The following chapter describe how you can test your setup.</span></span> <span data-ttu-id="cef0d-345">Elke test wordt ervan uitgegaan dat u hoofdmap en de SAP HANA-master wordt uitgevoerd op de virtuele machine saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="cef0d-345">Every test assumes that you are root and the SAP HANA master is running on the virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="cef0d-346">Hekwerk Test</span><span class="sxs-lookup"><span data-stu-id="cef0d-346">Fencing Test</span></span>

<span data-ttu-id="cef0d-347">U kunt de installatie van de agent hekwerk testen door de netwerkinterface op knooppunt saphanavm1 uit te schakelen.</span><span class="sxs-lookup"><span data-stu-id="cef0d-347">You can test the setup of the fencing agent by disabling the network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="cef0d-348">De virtuele machine moet nu opnieuw gestart of gestopt, afhankelijk van uw clusterconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="cef0d-348">The virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="cef0d-349">Als u de stonith-actie die moet worden uitgeschakeld instelt, wordt de virtuele machine wordt gestopt en de bronnen worden gemigreerd naar de actieve virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="cef0d-349">If you set the stonith-action to off, the virtual machine will be stopped and the resources are migrated to the running virtual machine.</span></span>

<span data-ttu-id="cef0d-350">Zodra u de virtuele machine opnieuw start, zijn de SAP HANA-bron niet worden gestart als secundaire als u AUTOMATED_REGISTER instelt = "false".</span><span class="sxs-lookup"><span data-stu-id="cef0d-350">Once you start the virtual machine again, the SAP HANA resource will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="cef0d-351">In dit geval moet u het exemplaar HANA als secundaire configureren door het uitvoeren van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="cef0d-351">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="cef0d-352">Een handmatige failover testen</span><span class="sxs-lookup"><span data-stu-id="cef0d-352">Testing a manual failover</span></span>

<span data-ttu-id="cef0d-353">U kunt een handmatige failover testen door het stoppen van de service pacemaker heeft op het knooppunt saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="cef0d-353">You can test a manual failover by stopping the pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="cef0d-354">U kunt de service opnieuw starten na de failover.</span><span class="sxs-lookup"><span data-stu-id="cef0d-354">After the failover, you can start the service again.</span></span> <span data-ttu-id="cef0d-355">De SAP HANA-resource op saphanavm1 niet worden gestart als secundaire als u AUTOMATED_REGISTER instelt = "false".</span><span class="sxs-lookup"><span data-stu-id="cef0d-355">The SAP HANA resource on saphanavm1 will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="cef0d-356">In dit geval moet u het exemplaar HANA als secundaire configureren door het uitvoeren van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="cef0d-356">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="cef0d-357">Een migratie testen</span><span class="sxs-lookup"><span data-stu-id="cef0d-357">Testing a migration</span></span>

<span data-ttu-id="cef0d-358">U kunt het hoofdknooppunt SAP HANA migreren door de volgende opdracht wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="cef0d-358">You can migrate the SAP HANA master node by executing the following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="cef0d-359">Dit moet de SAP HANA-hoofdknooppunt en de groep waartoe het virtuele IP-adres saphanavm2 migreren.</span><span class="sxs-lookup"><span data-stu-id="cef0d-359">This should migrate the SAP HANA master node and the group that contains the virtual IP address to saphanavm2.</span></span>
<span data-ttu-id="cef0d-360">De SAP HANA-resource op saphanavm1 niet worden gestart als secundaire als u AUTOMATED_REGISTER instelt = "false".</span><span class="sxs-lookup"><span data-stu-id="cef0d-360">The SAP HANA resource on saphanavm1 will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="cef0d-361">In dit geval moet u het exemplaar HANA als secundaire configureren door het uitvoeren van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="cef0d-361">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="cef0d-362">De migratie maakt locatie beperkingen moeten opnieuw worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="cef0d-362">The migration creates location contraints that need to be deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like the following contraint. You should have two contraints, one for the SAP HANA resource and one for the IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="cef0d-363">U moet ook opruimen van de status van de bron van het secundaire knooppunt</span><span class="sxs-lookup"><span data-stu-id="cef0d-363">You also need to cleanup the state of the secondary node resource</span></span>

<pre><code>
# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="cef0d-364">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cef0d-364">Next steps</span></span>
* <span data-ttu-id="cef0d-365">[Azure virtuele Machines, planning en implementatie voor SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="cef0d-365">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="cef0d-366">[Azure virtuele Machines-implementatie voor SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="cef0d-366">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="cef0d-367">[Azure virtuele Machines DBMS-implementatie voor SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="cef0d-367">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="cef0d-368">Zie voor meer informatie over hoe u hoge beschikbaarheid en herstel na noodgevallen van SAP HANA plannen in Azure (grote exemplaren), [SAP HANA (grote exemplaren) hoge beschikbaarheid en herstel na noodgevallen op Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="cef0d-368">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 

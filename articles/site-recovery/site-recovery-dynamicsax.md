---
title: Een meerlaagse Dynamics AX-implementatie met behulp van Azure Site Recovery repliceren | Microsoft Docs
description: Dit artikel wordt beschreven hoe repliceren en Dynamics AX met Azure Site Recovery beveiligen
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: 03127c8f4841b67436c4819628319705af0b2cd5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="b994d-103">Een toepassing met meerdere lagen Dynamics AX met Azure Site Recovery repliceren</span><span class="sxs-lookup"><span data-stu-id="b994d-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="b994d-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b994d-104">Overview</span></span>


<span data-ttu-id="b994d-105">Microsoft Dynamics AX is een van de meest populaire ERP-oplossing tussen ondernemingen gestandaardiseerde proces verschillende locaties, beheren van resources en de naleving te vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="b994d-105">Microsoft Dynamics AX is one of the most popular ERP solution among enterprises to standardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="b994d-106">Considering de toepassing essentieel voor een organisatie bedrijf is is het belangrijk dat u moet u ervoor zorgen dat als elke ramp toepassing kan worden uitgevoerd en in de minimale tijd.</span><span class="sxs-lookup"><span data-stu-id="b994d-106">Considering the application is business critical to an organization it is very important to be sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="b994d-107">Vandaag de dag biedt Microsoft Dynamics AX geen een out-of-the-box-noodherstel herstelfuncties.</span><span class="sxs-lookup"><span data-stu-id="b994d-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="b994d-108">Microsoft Dynamics AX bestaat uit veel serveronderdelen, zoals AOS-Server, Active Directory (AD), SQL Database-Server, SharePoint Server, Reporting Server, enzovoort. Voor het beheren van de sitedatabase is herstellen van elk van deze onderdelen handmatig niet alleen dure, maar ook gevoelig voor fouten.</span><span class="sxs-lookup"><span data-stu-id="b994d-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. To manage the disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="b994d-109">Dit artikel wordt uitgelegd in detail over hoe u een noodherstel voor uw Dynamics AX-toepassing met maken kunt [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b994d-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="b994d-110">Het omvat tevens geplande en ongeplande/testen failovers met één klik herstelplan, ondersteunde configuraties en vereisten.</span><span class="sxs-lookup"><span data-stu-id="b994d-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="b994d-111">Azure Site Recovery op basis van noodherstel is volledig getest, gecertificeerd en aanbevolen door Microsoft Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="b994d-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="b994d-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b994d-112">Prerequisites</span></span>

<span data-ttu-id="b994d-113">Herstel na noodgevallen voor Dynamics AX-toepassing met Azure Site Recovery implementeert, moet de volgende vereisten is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b994d-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires the following pre-requisites completed.</span></span>

<span data-ttu-id="b994d-114">• Een on-premises Dynamics AX-implementatie is ingesteld</span><span class="sxs-lookup"><span data-stu-id="b994d-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="b994d-115">• Azure Site Recovery Services-kluis is gemaakt in Microsoft Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="b994d-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="b994d-116">• Als Azure uw site recovery de Azure virtuele Machine Readiness Assessment hulpprogramma uitvoeren op virtuele machines om ervoor te zorgen dat ze compatibel met Azure VM's en Azure Site Recovery-Services zijn</span><span class="sxs-lookup"><span data-stu-id="b994d-116">•   If Azure is your recovery site, run the Azure Virtual Machine Readiness Assessment tool  on VMs to ensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="b994d-117">Site Recovery-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="b994d-117">Site Recovery support</span></span>

<span data-ttu-id="b994d-118">In dit artikel maakt, omwille van de werden virtuele VMware-machines met Dynamics AX 2012R3 op Windows Server 2012 R2 Enterprise gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b994d-118">For the purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="b994d-119">Als replicatie van site recovery networkdirect van toepassing is, worden de aanbevelingen die in de volgende scenario's evenals verwacht.</span><span class="sxs-lookup"><span data-stu-id="b994d-119">As site recovery replication is application agnostic, the recommendations provided here are expected to hold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="b994d-120">Bron en doel</span><span class="sxs-lookup"><span data-stu-id="b994d-120">Source and target</span></span>

<span data-ttu-id="b994d-121">**Scenario**</span><span class="sxs-lookup"><span data-stu-id="b994d-121">**Scenario**</span></span> | <span data-ttu-id="b994d-122">**Een secundaire site**</span><span class="sxs-lookup"><span data-stu-id="b994d-122">**To a secondary site**</span></span> | <span data-ttu-id="b994d-123">**Naar Azure**</span><span class="sxs-lookup"><span data-stu-id="b994d-123">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="b994d-124">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="b994d-124">**Hyper-V**</span></span> | <span data-ttu-id="b994d-125">Ja</span><span class="sxs-lookup"><span data-stu-id="b994d-125">Yes</span></span> | <span data-ttu-id="b994d-126">Ja</span><span class="sxs-lookup"><span data-stu-id="b994d-126">Yes</span></span>
<span data-ttu-id="b994d-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="b994d-127">**VMware**</span></span> | <span data-ttu-id="b994d-128">Ja</span><span class="sxs-lookup"><span data-stu-id="b994d-128">Yes</span></span> | <span data-ttu-id="b994d-129">Ja</span><span class="sxs-lookup"><span data-stu-id="b994d-129">Yes</span></span>
<span data-ttu-id="b994d-130">**Fysieke server**</span><span class="sxs-lookup"><span data-stu-id="b994d-130">**Physical server**</span></span> | <span data-ttu-id="b994d-131">Ja</span><span class="sxs-lookup"><span data-stu-id="b994d-131">Yes</span></span> | <span data-ttu-id="b994d-132">Ja</span><span class="sxs-lookup"><span data-stu-id="b994d-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="b994d-133">DR van Dynamics AX-toepassing met Azure Site Recovery inschakelen</span><span class="sxs-lookup"><span data-stu-id="b994d-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="b994d-134">Uw toepassing Dynamics AX beveiligen</span><span class="sxs-lookup"><span data-stu-id="b994d-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="b994d-135">Elk onderdeel van de Dynamics AX moet worden beveiligd, zodat de replicatie van de volledige toepassing en het herstel.</span><span class="sxs-lookup"><span data-stu-id="b994d-135">Each component of the Dynamics AX needs to be protected to enable the complete application replication and recovery.</span></span> <span data-ttu-id="b994d-136">Deze sectie worden behandeld:</span><span class="sxs-lookup"><span data-stu-id="b994d-136">This section covers:</span></span>

<span data-ttu-id="b994d-137">**1. Bescherming van Active Directory**</span><span class="sxs-lookup"><span data-stu-id="b994d-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="b994d-138">**2. Beveiliging van SQL-laag**</span><span class="sxs-lookup"><span data-stu-id="b994d-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="b994d-139">**3. Beveiliging van de App en Web lagen**</span><span class="sxs-lookup"><span data-stu-id="b994d-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="b994d-140">**4. Netwerkconfiguratie**</span><span class="sxs-lookup"><span data-stu-id="b994d-140">**4. Networking configuration**</span></span>

<span data-ttu-id="b994d-141">**5. Plan voor herstel**</span><span class="sxs-lookup"><span data-stu-id="b994d-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="b994d-142">1. Setup AD- en DNS-replicatie</span><span class="sxs-lookup"><span data-stu-id="b994d-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="b994d-143">Active Directory is vereist op de site DR voor Dynamics AX-toepassing naar de functie.</span><span class="sxs-lookup"><span data-stu-id="b994d-143">Active Directory is required on the DR site for Dynamics AX application to function.</span></span> <span data-ttu-id="b994d-144">Er zijn twee aanbevolen keuzes op basis van de complexiteit van de klant on-premises omgeving.</span><span class="sxs-lookup"><span data-stu-id="b994d-144">There are two recommended choices based on the complexity of the customer’s on-premises environment.</span></span>

<span data-ttu-id="b994d-145">**Optie 1**</span><span class="sxs-lookup"><span data-stu-id="b994d-145">**Option 1**</span></span>

<span data-ttu-id="b994d-146">Als de klant heeft een klein aantal toepassingen en één domeincontroller voor de gehele on-premises site en zal worden failover van de hele site samen, en vervolgens wordt u ASR-replicatie aangeraden naar de DC-machine repliceren naar secundaire site (van toepassing op zowel Site naar Site als Site naar Azure).</span><span class="sxs-lookup"><span data-stu-id="b994d-146">If the customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over the entire site together, then we recommend using ASR-Replication to replicate the DC machine to secondary site (applicable for both Site to Site and Site to Azure).</span></span>

<span data-ttu-id="b994d-147">**Optie 2**</span><span class="sxs-lookup"><span data-stu-id="b994d-147">**Option 2**</span></span>

<span data-ttu-id="b994d-148">Als de klant heeft een groot aantal toepassingen en een Active Directory-forest wordt uitgevoerd en wordt failover-paar toepassingen op een tijdstip, wordt aangeraden een extra domeincontroller op de DR-site instellen (secundaire site of in Azure).</span><span class="sxs-lookup"><span data-stu-id="b994d-148">If the customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on the DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="b994d-149">Raadpleeg [aanvullende handleiding op het beschikbaar maken van een domeincontroller op DR-site](site-recovery-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="b994d-149">Please refer to [companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="b994d-150">Voor de rest van dit document wordt ervan uitgegaan dat een domeincontroller beschikbaar is op DR-site.</span><span class="sxs-lookup"><span data-stu-id="b994d-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="b994d-151">2. Setup van SQL Server-replicatie</span><span class="sxs-lookup"><span data-stu-id="b994d-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="b994d-152">Raadpleeg de handleiding voor gedetailleerde richtlijnen voor technische op de aanbevolen optie voor het beveiligen van [SQL laag](site-recovery-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b994d-152">Please refer to companion guide  for detailed technical guidance on the recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="b994d-153">3. Schakel de beveiliging voor de Dynamics AX-client- en AOS-virtuele machines</span><span class="sxs-lookup"><span data-stu-id="b994d-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="b994d-154">Voer een relevante Azure Site Recovery-configuratie op basis van het feit of de virtuele machines op zijn geïmplementeerd [Hyper-V](site-recovery-hyper-v-site-to-azure.md) of op [VMware](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="b994d-154">Perform relevant Azure Site Recovery configuration based on whether the VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="b994d-155">Is 15 minuten Crash consistent frequentie aanbevolen als u wilt configureren.</span><span class="sxs-lookup"><span data-stu-id="b994d-155">Recommended Crash consistent frequency to configure is 15 minutes.</span></span>
>

<span data-ttu-id="b994d-156">De hieronder momentopname toont u de beveiligingsstatus van Dynamics onderdeel VM's in beveiligingsscenario VMware-site naar Azure.</span><span class="sxs-lookup"><span data-stu-id="b994d-156">The below snapshot shows the protection status of Dynamics component VMs in ‘VMware site to Azure’ protection scenario.</span></span>
<span data-ttu-id="b994d-157">![Beveiligde items](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="b994d-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="b994d-158">4. Netwerken configureren</span><span class="sxs-lookup"><span data-stu-id="b994d-158">4. Configure Networking</span></span>
<span data-ttu-id="b994d-159">Configureer VM berekenen en -instellingen</span><span class="sxs-lookup"><span data-stu-id="b994d-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="b994d-160">Voor de AX-client en de virtuele machines AOS-netwerkinstellingen configureren in Azure Site Recovery zodat de VM-netwerken ophalen gekoppeld aan het juiste DR-netwerk na een failover.</span><span class="sxs-lookup"><span data-stu-id="b994d-160">For the AX client and AOS VMs configure network settings in Azure Site Recovery so that the VM networks get attached to the right DR network after failover.</span></span> <span data-ttu-id="b994d-161">Zorg ervoor dat het netwerk DR voor deze lagen routeerbaar zijn naar de SQL-laag.</span><span class="sxs-lookup"><span data-stu-id="b994d-161">Ensure the DR network for these tiers is routable to the SQL tier.</span></span>

<span data-ttu-id="b994d-162">U kunt de virtuele machine selecteren in de gerepliceerde items voor het configureren van de netwerkinstellingen, zoals wordt weergegeven in de onderstaande momentopname.</span><span class="sxs-lookup"><span data-stu-id="b994d-162">You can select the VM in the replicated items to configure the network settings as shown in the snapshot below.</span></span>

* <span data-ttu-id="b994d-163">Selecteer de juiste beschikbaarheid voor AOS-servers.</span><span class="sxs-lookup"><span data-stu-id="b994d-163">For AOS servers select the correct availability set.</span></span>

* <span data-ttu-id="b994d-164">Als u met behulp van een statische IP-adres en geeft u het IP-adres dat u wilt dat de virtuele machine moet worden uitgevoerd de **IP-adres doel** veld ![netwerkinstellingen](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span><span class="sxs-lookup"><span data-stu-id="b994d-164">If you are using a static IP then specify the IP that you want the virtual machine to take in the **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="b994d-165">5. Een herstelplan maken</span><span class="sxs-lookup"><span data-stu-id="b994d-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="b994d-166">U kunt een herstelplan maken in Azure Site Recovery voor de failover te automatiseren.</span><span class="sxs-lookup"><span data-stu-id="b994d-166">You can create a recovery plan in Azure Site Recovery to automate the failover process.</span></span> <span data-ttu-id="b994d-167">App-laag en weblaag toevoegen in het herstelplan.</span><span class="sxs-lookup"><span data-stu-id="b994d-167">Add app tier and web tier in the Recovery Plan.</span></span> <span data-ttu-id="b994d-168">In verschillende groepen zo gerangschikt dat het front-afsluiten voordat de app-laag.</span><span class="sxs-lookup"><span data-stu-id="b994d-168">Order them in different groups so that the front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="b994d-169">Selecteer de Azure Site Recovery-kluis in uw abonnement en klik op de tegel 'Herstelplannen'.</span><span class="sxs-lookup"><span data-stu-id="b994d-169">Select the Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="b994d-170">Klik op ' + herstel plannen en geef een naam op.</span><span class="sxs-lookup"><span data-stu-id="b994d-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="b994d-171">Selecteer de 'Source' en 'Target'.</span><span class="sxs-lookup"><span data-stu-id="b994d-171">Select the ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="b994d-172">Het doel mag Azure of een secundaire site.</span><span class="sxs-lookup"><span data-stu-id="b994d-172">The target can be Azure or secondary site.</span></span> <span data-ttu-id="b994d-173">Als u Azure kiest, moet u het implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="b994d-173">In case you choose Azure, you must specify the deployment model</span></span>

![Herstelplan maken](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="b994d-175">Selecteer de AOS en de client virtuele machines aan het herstelplan en klik ✓.</span><span class="sxs-lookup"><span data-stu-id="b994d-175">Select the AOS and client VMs to the recovery plan and click ✓.</span></span>
<span data-ttu-id="b994d-176">![Herstelplan maken](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="b994d-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![Plan voor herstel](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="b994d-178">U kunt het herstelplan voor Dynamics AX-toepassing aanpassen door verschillende stappen toe te voegen zoals hieronder wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="b994d-178">You can customize the recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="b994d-179">De momentopname van de bovenstaande ziet u het volledige herstelplan na het toevoegen van alle stappen.</span><span class="sxs-lookup"><span data-stu-id="b994d-179">The above snapshot shows the complete recovery plan after adding all the steps.</span></span>

<span data-ttu-id="b994d-180">*Stappen:*</span><span class="sxs-lookup"><span data-stu-id="b994d-180">*Steps:*</span></span>

<span data-ttu-id="b994d-181">*1. SQL Server failover stappen*</span><span class="sxs-lookup"><span data-stu-id="b994d-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="b994d-182">Raadpleeg [DR van SQL Server-oplossing](site-recovery-sql.md) aanvullende handleiding voor meer informatie over specifieke herstelstappen voor het SQL server.</span><span class="sxs-lookup"><span data-stu-id="b994d-182">Refer to [‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific to SQL server.</span></span>

<span data-ttu-id="b994d-183">*2. Failover-groep 1: Een failover de AOS-virtuele machines*</span><span class="sxs-lookup"><span data-stu-id="b994d-183">*2. Failover Group 1: Fail over the AOS VMs*</span></span>

<span data-ttu-id="b994d-184">Zorg ervoor dat het geselecteerde herstelpunt zo dicht mogelijk bij de database PIT maar niet verder gaan is.</span><span class="sxs-lookup"><span data-stu-id="b994d-184">Make sure that the recovery point selected is as close as possible to the database PIT but not ahead.</span></span>

<span data-ttu-id="b994d-185">*3. Script: Toevoegen load balancer (alleen E-A)* toevoegen aan een load balancer toevoegen wordt een script (via Azure automation) na AOS VM-groep.</span><span class="sxs-lookup"><span data-stu-id="b994d-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up to add a load balancer to it.</span></span> <span data-ttu-id="b994d-186">Een script kunt u deze taak.</span><span class="sxs-lookup"><span data-stu-id="b994d-186">You can use a script to do this task.</span></span> <span data-ttu-id="b994d-187">Raadpleeg artikel [load balancer voor de toepassing met meerdere lagen DR toevoegen](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="b994d-187">Refer article [how to add load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="b994d-188">*4. Failover-groep 2: Een failover de virtuele machines van de AX-client.*</span><span class="sxs-lookup"><span data-stu-id="b994d-188">*4. Failover Group 2: Fail over the AX client VMs.*</span></span>
<span data-ttu-id="b994d-189">Failover van de weblaag virtuele machines als onderdeel van het herstelplan.</span><span class="sxs-lookup"><span data-stu-id="b994d-189">Fail over the web tier VMs as part of the recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="b994d-190">Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b994d-190">Doing a test failover</span></span>

<span data-ttu-id="b994d-191">Raadpleeg de AD-DR-oplossing en de SQL Server-DR-oplossing aanvullende handleidingen voor specifieke aandachtspunten met AD en SQL server respectievelijk tijdens de Testfailover.</span><span class="sxs-lookup"><span data-stu-id="b994d-191">Refer to ‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific to AD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="b994d-192">Ga naar de Azure-portal en selecteer de Site Recovery-kluis.</span><span class="sxs-lookup"><span data-stu-id="b994d-192">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="b994d-193">Klik op het herstelplan gemaakt voor Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="b994d-193">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="b994d-194">Klik op 'Testfailover'.</span><span class="sxs-lookup"><span data-stu-id="b994d-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="b994d-195">Selecteer het virtuele netwerk om de test failover-proces te starten.</span><span class="sxs-lookup"><span data-stu-id="b994d-195">Select the virtual network to start the test fail-over process.</span></span>
5.  <span data-ttu-id="b994d-196">Als de secundaire-omgeving is, kunt u uw validaties kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b994d-196">Once the secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="b994d-197">Zodra de validaties voltooid zijn, kunt u 'Validaties voltooid' en de testfailoveromgeving wordt gereinigd.</span><span class="sxs-lookup"><span data-stu-id="b994d-197">Once the validations are complete, you can select ‘Validations complete’ and the test failover environment will be cleaned.</span></span>

<span data-ttu-id="b994d-198">Ga als volgt [in deze richtlijnen](site-recovery-test-failover-to-azure.md) een testfailover uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b994d-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="b994d-199">U een failover uitvoert</span><span class="sxs-lookup"><span data-stu-id="b994d-199">Doing a failover</span></span>

1.  <span data-ttu-id="b994d-200">Ga naar de Azure-portal en selecteer de Site Recovery-kluis.</span><span class="sxs-lookup"><span data-stu-id="b994d-200">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="b994d-201">Klik op het herstelplan gemaakt voor Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="b994d-201">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="b994d-202">Klik op 'Failover' en 'Failover' selecteren.</span><span class="sxs-lookup"><span data-stu-id="b994d-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="b994d-203">Selecteer het doelnetwerk en klik op ✓ om de failoverproces te starten.</span><span class="sxs-lookup"><span data-stu-id="b994d-203">Select the target network and click ✓ to start the failover process.</span></span>

<span data-ttu-id="b994d-204">Ga als volgt [in deze richtlijnen](site-recovery-failover.md) bij het uitvoeren van een failover.</span><span class="sxs-lookup"><span data-stu-id="b994d-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="b994d-205">Een Failback uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b994d-205">Perform a Failback</span></span>

<span data-ttu-id="b994d-206">Raadpleeg de SQL Server-DR-oplossing aanvullende handleiding voor overwegingen met betrekking tot specifieke met SQL server tijdens de Failback.</span><span class="sxs-lookup"><span data-stu-id="b994d-206">Refer to ‘SQL Server DR Solution ’ companion guide for considerations specific to SQL server during Failback.</span></span>

1.  <span data-ttu-id="b994d-207">Ga naar de Azure-portal en selecteer de Site Recovery-kluis.</span><span class="sxs-lookup"><span data-stu-id="b994d-207">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="b994d-208">Klik op het herstelplan gemaakt voor Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="b994d-208">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="b994d-209">Klik op 'Failover' en selecteer failover.</span><span class="sxs-lookup"><span data-stu-id="b994d-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="b994d-210">Klik op 'Wijziging richting'.</span><span class="sxs-lookup"><span data-stu-id="b994d-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="b994d-211">Selecteer de gewenste opties - synchronisatie van gegevens en opties voor het maken van VM</span><span class="sxs-lookup"><span data-stu-id="b994d-211">Select the appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="b994d-212">Klik op ✓ om het te starten 'Failback'.</span><span class="sxs-lookup"><span data-stu-id="b994d-212">Click ✓ to start the ‘Failback’ process.</span></span>


<span data-ttu-id="b994d-213">Ga als volgt [in deze richtlijnen](site-recovery-failback-azure-to-vmware.md) bij het uitvoeren van een failback.</span><span class="sxs-lookup"><span data-stu-id="b994d-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="b994d-214">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="b994d-214">Summary</span></span>
<span data-ttu-id="b994d-215">Met Azure Site Recovery kunt u een herstelplan volledig geautomatiseerd noodherstel voor uw Dynamics AX-toepassing maken.</span><span class="sxs-lookup"><span data-stu-id="b994d-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="b994d-216">U kunt de failover start binnen enkele seconden vanaf elke locatie in het geval van een onderbreking en ophalen van de toepassing binnen de minuten.</span><span class="sxs-lookup"><span data-stu-id="b994d-216">You can initiate the failover within seconds from anywhere in the event of a disruption and get the application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b994d-217">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b994d-217">Next steps</span></span>
<span data-ttu-id="b994d-218">Lees [welke workloads kan ik beveiligen?](site-recovery-workload.md) voor meer informatie over het beveiligen van enterprise-werkbelastingen met Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b994d-218">Read [What workloads can I protect?](site-recovery-workload.md) to learn more about protecting enterprise workloads with Azure Site Recovery.</span></span>

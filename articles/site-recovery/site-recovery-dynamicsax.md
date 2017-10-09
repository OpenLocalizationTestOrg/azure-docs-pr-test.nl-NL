---
title: een meerlaagse Dynamics AX-implementatie met behulp van Azure Site Recovery aaaReplicate | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooreplicate en Dynamics AX met Azure Site Recovery beveiligen
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
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="d591d-103">Een toepassing met meerdere lagen Dynamics AX met Azure Site Recovery repliceren</span><span class="sxs-lookup"><span data-stu-id="d591d-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="d591d-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d591d-104">Overview</span></span>


<span data-ttu-id="d591d-105">Microsoft Dynamics AX is een van de meest populaire ERP-oplossing Hallo tussen ondernemingen toostandardized proces verschillende locaties, beheren van resources en de naleving te vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="d591d-105">Microsoft Dynamics AX is one of hello most popular ERP solution among enterprises toostandardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="d591d-106">Considering toepassing hello kritieke tooan bedrijfsorganisatie is is erg belangrijk toobe ervoor dat als elke ramp toepassing actief en werkend in de minimale tijd moet.</span><span class="sxs-lookup"><span data-stu-id="d591d-106">Considering hello application is business critical tooan organization it is very important toobe sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="d591d-107">Vandaag de dag biedt Microsoft Dynamics AX geen een out-of-the-box-noodherstel herstelfuncties.</span><span class="sxs-lookup"><span data-stu-id="d591d-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="d591d-108">Microsoft Dynamics AX bestaat uit veel serveronderdelen, zoals AOS-Server, Active Directory (AD), SQL Database-Server, SharePoint Server, Reporting Server enzovoort toomanage Hallo herstel na noodgevallen van elk van deze onderdelen handmatig is niet alleen dure maar ook gevoelig voor fouten.</span><span class="sxs-lookup"><span data-stu-id="d591d-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. toomanage hello disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="d591d-109">Dit artikel wordt uitgelegd in detail over hoe u een noodherstel voor uw Dynamics AX-toepassing met maken kunt [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d591d-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="d591d-110">Het omvat tevens geplande en ongeplande/testen failovers met één klik herstelplan, ondersteunde configuraties en vereisten.</span><span class="sxs-lookup"><span data-stu-id="d591d-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="d591d-111">Azure Site Recovery op basis van noodherstel is volledig getest, gecertificeerd en aanbevolen door Microsoft Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="d591d-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="d591d-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d591d-112">Prerequisites</span></span>

<span data-ttu-id="d591d-113">Hallo vereisten voltooid na implementatie van herstel na noodgevallen voor Dynamics AX-toepassing met Azure Site Recovery worden vereist.</span><span class="sxs-lookup"><span data-stu-id="d591d-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires hello following pre-requisites completed.</span></span>

<span data-ttu-id="d591d-114">• Een on-premises Dynamics AX-implementatie is ingesteld</span><span class="sxs-lookup"><span data-stu-id="d591d-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="d591d-115">• Azure Site Recovery Services-kluis is gemaakt in Microsoft Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="d591d-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="d591d-116">• Als uw site recovery is Azure hello Azure virtuele Machine Readiness Assessment hulpprogramma uitvoeren op virtuele machines tooensure dat ze compatibel zijn met de Azure VM's en Azure Site Recovery Services</span><span class="sxs-lookup"><span data-stu-id="d591d-116">•   If Azure is your recovery site, run hello Azure Virtual Machine Readiness Assessment tool  on VMs tooensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="d591d-117">Site Recovery-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="d591d-117">Site Recovery support</span></span>

<span data-ttu-id="d591d-118">Voor Hallo doel van het maken van dit artikel, werden virtuele VMware-machines met Dynamics AX 2012R3 op Windows Server 2012 R2 Enterprise gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d591d-118">For hello purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="d591d-119">Als de replicatie van site recovery networkdirect van toepassing is, voorziet in Hallo aanbevelingen zijn hier verwachte toohold op de volgende scenario's ook.</span><span class="sxs-lookup"><span data-stu-id="d591d-119">As site recovery replication is application agnostic, hello recommendations provided here are expected toohold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="d591d-120">Bron en doel</span><span class="sxs-lookup"><span data-stu-id="d591d-120">Source and target</span></span>

<span data-ttu-id="d591d-121">**Scenario**</span><span class="sxs-lookup"><span data-stu-id="d591d-121">**Scenario**</span></span> | <span data-ttu-id="d591d-122">**de secundaire site tooa**</span><span class="sxs-lookup"><span data-stu-id="d591d-122">**tooa secondary site**</span></span> | <span data-ttu-id="d591d-123">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="d591d-123">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="d591d-124">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="d591d-124">**Hyper-V**</span></span> | <span data-ttu-id="d591d-125">Ja</span><span class="sxs-lookup"><span data-stu-id="d591d-125">Yes</span></span> | <span data-ttu-id="d591d-126">Ja</span><span class="sxs-lookup"><span data-stu-id="d591d-126">Yes</span></span>
<span data-ttu-id="d591d-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="d591d-127">**VMware**</span></span> | <span data-ttu-id="d591d-128">Ja</span><span class="sxs-lookup"><span data-stu-id="d591d-128">Yes</span></span> | <span data-ttu-id="d591d-129">Ja</span><span class="sxs-lookup"><span data-stu-id="d591d-129">Yes</span></span>
<span data-ttu-id="d591d-130">**Fysieke server**</span><span class="sxs-lookup"><span data-stu-id="d591d-130">**Physical server**</span></span> | <span data-ttu-id="d591d-131">Ja</span><span class="sxs-lookup"><span data-stu-id="d591d-131">Yes</span></span> | <span data-ttu-id="d591d-132">Ja</span><span class="sxs-lookup"><span data-stu-id="d591d-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="d591d-133">DR van Dynamics AX-toepassing met Azure Site Recovery inschakelen</span><span class="sxs-lookup"><span data-stu-id="d591d-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="d591d-134">Uw toepassing Dynamics AX beveiligen</span><span class="sxs-lookup"><span data-stu-id="d591d-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="d591d-135">Elk onderdeel van Hallo Dynamics AX behoeften toobe beveiligd tooenable Hallo volledige toepassing replicatie en herstel.</span><span class="sxs-lookup"><span data-stu-id="d591d-135">Each component of hello Dynamics AX needs toobe protected tooenable hello complete application replication and recovery.</span></span> <span data-ttu-id="d591d-136">Deze sectie worden behandeld:</span><span class="sxs-lookup"><span data-stu-id="d591d-136">This section covers:</span></span>

<span data-ttu-id="d591d-137">**1. Bescherming van Active Directory**</span><span class="sxs-lookup"><span data-stu-id="d591d-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="d591d-138">**2. Beveiliging van SQL-laag**</span><span class="sxs-lookup"><span data-stu-id="d591d-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="d591d-139">**3. Beveiliging van de App en Web lagen**</span><span class="sxs-lookup"><span data-stu-id="d591d-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="d591d-140">**4. Netwerkconfiguratie**</span><span class="sxs-lookup"><span data-stu-id="d591d-140">**4. Networking configuration**</span></span>

<span data-ttu-id="d591d-141">**5. Plan voor herstel**</span><span class="sxs-lookup"><span data-stu-id="d591d-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="d591d-142">1. Setup AD- en DNS-replicatie</span><span class="sxs-lookup"><span data-stu-id="d591d-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="d591d-143">Active Directory is vereist op Hallo DR-site voor toofunction van Dynamics AX-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d591d-143">Active Directory is required on hello DR site for Dynamics AX application toofunction.</span></span> <span data-ttu-id="d591d-144">Er zijn twee aanbevolen keuzes op basis van de complexiteit Hallo van van de klant Hallo on-premises omgeving.</span><span class="sxs-lookup"><span data-stu-id="d591d-144">There are two recommended choices based on hello complexity of hello customer’s on-premises environment.</span></span>

<span data-ttu-id="d591d-145">**Optie 1**</span><span class="sxs-lookup"><span data-stu-id="d591d-145">**Option 1**</span></span>

<span data-ttu-id="d591d-146">Als klant Hallo heeft een klein aantal toepassingen en één domeincontroller voor de gehele on-premises site en wordt samen gedurende de gehele site Hallo mislukken wordt aangeraden ASR-replicatie tooreplicate Hallo DC machine toosecondary site ( van toepassing voor zowel tooSite Site als Site tooAzure).</span><span class="sxs-lookup"><span data-stu-id="d591d-146">If hello customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over hello entire site together, then we recommend using ASR-Replication tooreplicate hello DC machine toosecondary site (applicable for both Site tooSite and Site tooAzure).</span></span>

<span data-ttu-id="d591d-147">**Optie 2**</span><span class="sxs-lookup"><span data-stu-id="d591d-147">**Option 2**</span></span>

<span data-ttu-id="d591d-148">Als klant Hallo heeft een groot aantal toepassingen en een Active Directory-forest wordt uitgevoerd en wordt failover-paar toepassingen op een tijdstip, wordt aangeraden een extra domeincontroller op Hallo DR-site instellen (secundaire site of in Azure).</span><span class="sxs-lookup"><span data-stu-id="d591d-148">If hello customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on hello DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="d591d-149">Raadpleeg het te[aanvullende handleiding op het beschikbaar maken van een domeincontroller op DR-site](site-recovery-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="d591d-149">Please refer too[companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="d591d-150">Voor de rest van dit document wordt ervan uitgegaan dat een domeincontroller beschikbaar is op DR-site.</span><span class="sxs-lookup"><span data-stu-id="d591d-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="d591d-151">2. Setup van SQL Server-replicatie</span><span class="sxs-lookup"><span data-stu-id="d591d-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="d591d-152">Raadpleeg de handleiding toocompanion voor gedetailleerde technische richtlijnen voor aanbevolen optie voor het beveiligen van Hallo [SQL laag](site-recovery-sql.md).</span><span class="sxs-lookup"><span data-stu-id="d591d-152">Please refer toocompanion guide  for detailed technical guidance on hello recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="d591d-153">3. Schakel de beveiliging voor de Dynamics AX-client- en AOS-virtuele machines</span><span class="sxs-lookup"><span data-stu-id="d591d-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="d591d-154">Voer een relevante Azure Site Recovery-configuratie op basis van of Hallo virtuele machines zijn geïmplementeerd op [Hyper-V](site-recovery-hyper-v-site-to-azure.md) of op [VMware](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="d591d-154">Perform relevant Azure Site Recovery configuration based on whether hello VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="d591d-155">Aanbevolen Crash consistent frequentie tooconfigure is 15 minuten.</span><span class="sxs-lookup"><span data-stu-id="d591d-155">Recommended Crash consistent frequency tooconfigure is 15 minutes.</span></span>
>

<span data-ttu-id="d591d-156">Hallo onder momentopname bevat Hallo beveiligingsstatus van Dynamics onderdeel VM's in 'VMware site tooAzure' beveiligingsscenario.</span><span class="sxs-lookup"><span data-stu-id="d591d-156">hello below snapshot shows hello protection status of Dynamics component VMs in ‘VMware site tooAzure’ protection scenario.</span></span>
<span data-ttu-id="d591d-157">![Beveiligde items](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="d591d-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="d591d-158">4. Netwerken configureren</span><span class="sxs-lookup"><span data-stu-id="d591d-158">4. Configure Networking</span></span>
<span data-ttu-id="d591d-159">Configureer VM berekenen en -instellingen</span><span class="sxs-lookup"><span data-stu-id="d591d-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="d591d-160">Voor Hallo AX-client- en AOS-VMs netwerkinstellingen configureren in Azure Site Recovery zodat Hallo VM-netwerken beschikken over gekoppelde toohello rechts DR netwerk na een failover.</span><span class="sxs-lookup"><span data-stu-id="d591d-160">For hello AX client and AOS VMs configure network settings in Azure Site Recovery so that hello VM networks get attached toohello right DR network after failover.</span></span> <span data-ttu-id="d591d-161">Zorg ervoor dat Hallo DR-netwerk voor deze lagen routeerbaar toohello SQL laag is.</span><span class="sxs-lookup"><span data-stu-id="d591d-161">Ensure hello DR network for these tiers is routable toohello SQL tier.</span></span>

<span data-ttu-id="d591d-162">U kunt selecteren Hallo VM in Hallo gerepliceerd items tooconfigure Hallo netwerkinstellingen, zoals weergegeven in de onderstaande Hallo-momentopname.</span><span class="sxs-lookup"><span data-stu-id="d591d-162">You can select hello VM in hello replicated items tooconfigure hello network settings as shown in hello snapshot below.</span></span>

* <span data-ttu-id="d591d-163">Voor de juiste beschikbaarheidsset Hallo AOS-servers selecteren</span><span class="sxs-lookup"><span data-stu-id="d591d-163">For AOS servers select hello correct availability set.</span></span>

* <span data-ttu-id="d591d-164">Als u met behulp van een statische IP-adres opgeven Hallo IP die u wilt dat virtuele machine tootake in Hallo Hallo **IP-adres doel** veld ![netwerkinstellingen](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span><span class="sxs-lookup"><span data-stu-id="d591d-164">If you are using a static IP then specify hello IP that you want hello virtual machine tootake in hello **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="d591d-165">5. Een herstelplan maken</span><span class="sxs-lookup"><span data-stu-id="d591d-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="d591d-166">U kunt een herstelplan maken in Azure Site Recovery tooautomate Hallo failover-proces.</span><span class="sxs-lookup"><span data-stu-id="d591d-166">You can create a recovery plan in Azure Site Recovery tooautomate hello failover process.</span></span> <span data-ttu-id="d591d-167">App-laag en weblaag in Hallo herstelplan toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d591d-167">Add app tier and web tier in hello Recovery Plan.</span></span> <span data-ttu-id="d591d-168">Bestellen in verschillende groepen zodat die Hallo front-afsluiten voordat de app-laag.</span><span class="sxs-lookup"><span data-stu-id="d591d-168">Order them in different groups so that hello front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="d591d-169">Selecteer hello Azure Site Recovery-kluis in uw abonnement en klik op de tegel 'Herstelplannen'.</span><span class="sxs-lookup"><span data-stu-id="d591d-169">Select hello Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="d591d-170">Klik op ' + herstel plannen en geef een naam op.</span><span class="sxs-lookup"><span data-stu-id="d591d-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="d591d-171">Selecteer Hallo 'Source' en 'Target'.</span><span class="sxs-lookup"><span data-stu-id="d591d-171">Select hello ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="d591d-172">Hallo doel mag Azure of een secundaire site.</span><span class="sxs-lookup"><span data-stu-id="d591d-172">hello target can be Azure or secondary site.</span></span> <span data-ttu-id="d591d-173">Als u Azure kiest, moet u Hallo-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="d591d-173">In case you choose Azure, you must specify hello deployment model</span></span>

![Herstelplan maken](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="d591d-175">Hallo AOS en client VMs toohello herstelplan selecteren en klik op ✓.</span><span class="sxs-lookup"><span data-stu-id="d591d-175">Select hello AOS and client VMs toohello recovery plan and click ✓.</span></span>
<span data-ttu-id="d591d-176">![Herstelplan maken](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="d591d-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![Plan voor herstel](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="d591d-178">U kunt plannen voor Dynamics AX-toepassing hello herstel aanpassen door verschillende stappen toe te voegen zoals hieronder wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="d591d-178">You can customize hello recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="d591d-179">Hallo hierboven momentopname toont Hallo voltooid herstelplan na het toevoegen van alle Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="d591d-179">hello above snapshot shows hello complete recovery plan after adding all hello steps.</span></span>

<span data-ttu-id="d591d-180">*Stappen:*</span><span class="sxs-lookup"><span data-stu-id="d591d-180">*Steps:*</span></span>

<span data-ttu-id="d591d-181">*1. SQL Server failover stappen*</span><span class="sxs-lookup"><span data-stu-id="d591d-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="d591d-182">Raadpleeg te[DR van SQL Server-oplossing](site-recovery-sql.md) aanvullende handleiding voor meer informatie over specifieke tooSQL van de herstelserver stappen.</span><span class="sxs-lookup"><span data-stu-id="d591d-182">Refer too[‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific tooSQL server.</span></span>

<span data-ttu-id="d591d-183">*2. Failover-groep 1: Een failover Hallo AOS-virtuele machines*</span><span class="sxs-lookup"><span data-stu-id="d591d-183">*2. Failover Group 1: Fail over hello AOS VMs*</span></span>

<span data-ttu-id="d591d-184">Zorg ervoor dat Hallo herstelpunt geselecteerd zo dicht mogelijk toohello database PIT maar niet verder gaan is.</span><span class="sxs-lookup"><span data-stu-id="d591d-184">Make sure that hello recovery point selected is as close as possible toohello database PIT but not ahead.</span></span>

<span data-ttu-id="d591d-185">*3. Script: Toevoegen load balancer (alleen E-A)* voegt een script toe (via Azure automation) na AOS VM groep tooadd een load balancer tooit voordoet.</span><span class="sxs-lookup"><span data-stu-id="d591d-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up tooadd a load balancer tooit.</span></span> <span data-ttu-id="d591d-186">U kunt een script toodo Gebruik deze taak.</span><span class="sxs-lookup"><span data-stu-id="d591d-186">You can use a script toodo this task.</span></span> <span data-ttu-id="d591d-187">Raadpleeg artikel [hoe tooadd load balancer voor DR-toepassing met meerdere lagen](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="d591d-187">Refer article [how tooadd load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="d591d-188">*4. Failover-groep 2: Een failover Hallo AX-client virtuele machines.*</span><span class="sxs-lookup"><span data-stu-id="d591d-188">*4. Failover Group 2: Fail over hello AX client VMs.*</span></span>
<span data-ttu-id="d591d-189">Hallo weblaag virtuele machines als onderdeel van het herstelplan Hallo een failover.</span><span class="sxs-lookup"><span data-stu-id="d591d-189">Fail over hello web tier VMs as part of hello recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="d591d-190">Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d591d-190">Doing a test failover</span></span>

<span data-ttu-id="d591d-191">Raadpleeg too'AD DR Solution ' en de aanvullende handleidingen DR van SQL Server-oplossing voor specifieke tooAD overwegingen en SQL server respectievelijk tijdens de Testfailover.</span><span class="sxs-lookup"><span data-stu-id="d591d-191">Refer too‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific tooAD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="d591d-192">Ga tooAzure portal en selecteer de Site Recovery-kluis.</span><span class="sxs-lookup"><span data-stu-id="d591d-192">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="d591d-193">Klik op Hallo herstelplan is gemaakt voor Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="d591d-193">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="d591d-194">Klik op 'Testfailover'.</span><span class="sxs-lookup"><span data-stu-id="d591d-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="d591d-195">Selecteer Hallo virtueel netwerk toostart Hallo test failover-proces.</span><span class="sxs-lookup"><span data-stu-id="d591d-195">Select hello virtual network toostart hello test fail-over process.</span></span>
5.  <span data-ttu-id="d591d-196">Wanneer secundaire Hallo-omgeving is, kunt u uw validaties kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d591d-196">Once hello secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="d591d-197">Zodra Hallo validaties voltooid zijn, kunt u 'Validaties voltooid' en de testfailoveromgeving hello wordt gereinigd.</span><span class="sxs-lookup"><span data-stu-id="d591d-197">Once hello validations are complete, you can select ‘Validations complete’ and hello test failover environment will be cleaned.</span></span>

<span data-ttu-id="d591d-198">Ga als volgt [in deze richtlijnen](site-recovery-test-failover-to-azure.md) toodo een testfailover.</span><span class="sxs-lookup"><span data-stu-id="d591d-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="d591d-199">U een failover uitvoert</span><span class="sxs-lookup"><span data-stu-id="d591d-199">Doing a failover</span></span>

1.  <span data-ttu-id="d591d-200">Ga tooAzure portal en selecteer de Site Recovery-kluis.</span><span class="sxs-lookup"><span data-stu-id="d591d-200">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="d591d-201">Klik op Hallo herstelplan is gemaakt voor Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="d591d-201">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="d591d-202">Klik op 'Failover' en 'Failover' selecteren.</span><span class="sxs-lookup"><span data-stu-id="d591d-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="d591d-203">Hallo-doelnetwerk selecteren en op ✓ toostart Hallo failover-proces.</span><span class="sxs-lookup"><span data-stu-id="d591d-203">Select hello target network and click ✓ toostart hello failover process.</span></span>

<span data-ttu-id="d591d-204">Ga als volgt [in deze richtlijnen](site-recovery-failover.md) bij het uitvoeren van een failover.</span><span class="sxs-lookup"><span data-stu-id="d591d-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="d591d-205">Een Failback uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d591d-205">Perform a Failback</span></span>

<span data-ttu-id="d591d-206">Raadpleeg too'SQL Server DR-oplossing is aanvullende handleiding voor overwegingen met betrekking tot specifieke tooSQL server tijdens de Failback.</span><span class="sxs-lookup"><span data-stu-id="d591d-206">Refer too‘SQL Server DR Solution ’ companion guide for considerations specific tooSQL server during Failback.</span></span>

1.  <span data-ttu-id="d591d-207">Ga tooAzure portal en selecteer de Site Recovery-kluis.</span><span class="sxs-lookup"><span data-stu-id="d591d-207">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="d591d-208">Klik op Hallo herstelplan is gemaakt voor Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="d591d-208">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="d591d-209">Klik op 'Failover' en selecteer failover.</span><span class="sxs-lookup"><span data-stu-id="d591d-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="d591d-210">Klik op 'Wijziging richting'.</span><span class="sxs-lookup"><span data-stu-id="d591d-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="d591d-211">Hallo juiste opties selecteren - synchronisatie van gegevens en opties voor het maken van VM</span><span class="sxs-lookup"><span data-stu-id="d591d-211">Select hello appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="d591d-212">Klik op ✓ toostart Hallo 'Failback' proces.</span><span class="sxs-lookup"><span data-stu-id="d591d-212">Click ✓ toostart hello ‘Failback’ process.</span></span>


<span data-ttu-id="d591d-213">Ga als volgt [in deze richtlijnen](site-recovery-failback-azure-to-vmware.md) bij het uitvoeren van een failback.</span><span class="sxs-lookup"><span data-stu-id="d591d-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="d591d-214">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="d591d-214">Summary</span></span>
<span data-ttu-id="d591d-215">Met Azure Site Recovery kunt u een herstelplan volledig geautomatiseerd noodherstel voor uw Dynamics AX-toepassing maken.</span><span class="sxs-lookup"><span data-stu-id="d591d-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="d591d-216">U kunt het Hallo failover initiëren binnen enkele seconden vanaf elke locatie in Hallo-gebeurtenis van een onderbreking van de en krijgt u de toepassing hello up-to-date en worden uitgevoerd in minuten.</span><span class="sxs-lookup"><span data-stu-id="d591d-216">You can initiate hello failover within seconds from anywhere in hello event of a disruption and get hello application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d591d-217">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d591d-217">Next steps</span></span>
<span data-ttu-id="d591d-218">Lees [welke workloads kan ik beveiligen?](site-recovery-workload.md) toolearn meer over het beveiligen van enterprise-werkbelastingen met Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d591d-218">Read [What workloads can I protect?](site-recovery-workload.md) toolearn more about protecting enterprise workloads with Azure Site Recovery.</span></span>

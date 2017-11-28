---
title: Een Citrix XenDesktop en XenApp implementatie van meerdere lagen met Azure Site Recovery repliceren | Microsoft Docs
description: In dit artikel wordt beschreven hoe beveiligen en herstellen van Citrix XenDesktop en XenApp implementaties met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: dc064352b1841ff346b705dc63186b12d79350b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="64dfa-103">Een Citrix XenApp en XenDesktop implementatie van meerdere lagen met Azure Site Recovery repliceren</span><span class="sxs-lookup"><span data-stu-id="64dfa-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="64dfa-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="64dfa-104">Overview</span></span>

<span data-ttu-id="64dfa-105">Citrix XenDesktop is een bureaublad-virtualisatie-oplossing die bureaubladen en toepassingen als een ondemand-service aan een gebruiker een willekeurige plaats biedt.</span><span class="sxs-lookup"><span data-stu-id="64dfa-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service to any user, anywhere.</span></span> <span data-ttu-id="64dfa-106">Met de FlexCast levering technologie kunt XenDesktop snel en veilig leveren toepassingen en bureaubladen voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="64dfa-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops to users.</span></span>
<span data-ttu-id="64dfa-107">Vandaag de dag biedt Citrix XenApp geen elke ramp herstelfuncties.</span><span class="sxs-lookup"><span data-stu-id="64dfa-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="64dfa-108">Een goede noodhersteloplossing mag modellering van herstelplannen rond de bovenstaande complexe toepassingsarchitecturen en hebben de mogelijkheid aangepaste stappen voor het afhandelen van de toepassingstoewijzingen tussen verschillende lagen daarom bieden een éénkliks-toevoegen Controleer of de schermopname oplossing er in een noodsituatie leidt tot een lagere RTO.</span><span class="sxs-lookup"><span data-stu-id="64dfa-108">A good disaster recovery solution, should allow modeling of recovery plans around the above complex application architectures and also have the ability to add customized steps to handle application mappings between various tiers hence providing a single-click sure shot solution in the event of a disaster leading to a lower RTO.</span></span>

<span data-ttu-id="64dfa-109">Dit document bevat een stapsgewijze instructies voor het bouwen van een noodherstel voor uw on-premises Citrix XenApp implementaties op Hyper-V- en VMware vSphere-platforms.</span><span class="sxs-lookup"><span data-stu-id="64dfa-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="64dfa-110">Dit document beschrijft ook hoe u een testfailover (drill disaster recovery) en niet-geplande failover naar Azure met herstelplannen, de ondersteunde configuraties en vereisten.</span><span class="sxs-lookup"><span data-stu-id="64dfa-110">This document also describes how to perform a test failover(disaster recovery drill) and unplanned failover to Azure using recovery plans, the supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="64dfa-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="64dfa-111">Prerequisites</span></span>

<span data-ttu-id="64dfa-112">Voordat u begint, zorg er dan voor dat u het volgende weten:</span><span class="sxs-lookup"><span data-stu-id="64dfa-112">Before you start, make sure you understand the following:</span></span>

1. [<span data-ttu-id="64dfa-113">Een virtuele machine repliceren naar Azure</span><span class="sxs-lookup"><span data-stu-id="64dfa-113">Replicating a virtual machine to Azure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="64dfa-114">Hoe [ontwerpen van een netwerk herstel](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="64dfa-114">How to [design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="64dfa-115">Een testfailover uitvoeren naar Azure</span><span class="sxs-lookup"><span data-stu-id="64dfa-115">Doing a test failover to Azure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="64dfa-116">U een failover naar Azure</span><span class="sxs-lookup"><span data-stu-id="64dfa-116">Doing a failover to Azure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="64dfa-117">Hoe [repliceren van een domeincontroller](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="64dfa-117">How to [replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="64dfa-118">Hoe [SQL-Server repliceren](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="64dfa-118">How to [replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="64dfa-119">Implementaties</span><span class="sxs-lookup"><span data-stu-id="64dfa-119">Deployment patterns</span></span>

<span data-ttu-id="64dfa-120">Een farm Citrix XenApp en XenDesktop heeft meestal de volgende implementatie-patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="64dfa-120">A Citrix XenApp and XenDesktop farm typically has the following deployment pattern:</span></span>

<span data-ttu-id="64dfa-121">**Patroon van de implementatie**</span><span class="sxs-lookup"><span data-stu-id="64dfa-121">**Deployment pattern**</span></span>

<span data-ttu-id="64dfa-122">Citrix XenApp en XenDesktop implementatie met AD DNS-server, SQL databaseserver server, Citrix levering Controller, winkel, XenApp Master (VDA), Citrix XenApp licentieserver</span><span class="sxs-lookup"><span data-stu-id="64dfa-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![Implementatie-patroon 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="64dfa-124">Site Recovery-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="64dfa-124">Site Recovery support</span></span>

<span data-ttu-id="64dfa-125">In dit artikel wordt Citrix-implementaties op virtuele VMware-machines worden beheerd door vSphere 6.0-System Center VMM 2012 R2 zijn gebruikt voor het instellen van Noodherstel.</span><span class="sxs-lookup"><span data-stu-id="64dfa-125">For the purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used to setup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="64dfa-126">Bron en doel</span><span class="sxs-lookup"><span data-stu-id="64dfa-126">Source and target</span></span>

<span data-ttu-id="64dfa-127">**Scenario**</span><span class="sxs-lookup"><span data-stu-id="64dfa-127">**Scenario**</span></span> | <span data-ttu-id="64dfa-128">**Een secundaire site**</span><span class="sxs-lookup"><span data-stu-id="64dfa-128">**To a secondary site**</span></span> | <span data-ttu-id="64dfa-129">**Naar Azure**</span><span class="sxs-lookup"><span data-stu-id="64dfa-129">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="64dfa-130">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="64dfa-130">**Hyper-V**</span></span> | <span data-ttu-id="64dfa-131">Niet binnen het bereik</span><span class="sxs-lookup"><span data-stu-id="64dfa-131">Not in scope</span></span> | <span data-ttu-id="64dfa-132">Ja</span><span class="sxs-lookup"><span data-stu-id="64dfa-132">Yes</span></span>
<span data-ttu-id="64dfa-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="64dfa-133">**VMware**</span></span> | <span data-ttu-id="64dfa-134">Niet binnen het bereik</span><span class="sxs-lookup"><span data-stu-id="64dfa-134">Not in scope</span></span> | <span data-ttu-id="64dfa-135">Ja</span><span class="sxs-lookup"><span data-stu-id="64dfa-135">Yes</span></span>
<span data-ttu-id="64dfa-136">**Fysieke server**</span><span class="sxs-lookup"><span data-stu-id="64dfa-136">**Physical server**</span></span> | <span data-ttu-id="64dfa-137">Niet binnen het bereik</span><span class="sxs-lookup"><span data-stu-id="64dfa-137">Not in scope</span></span> | <span data-ttu-id="64dfa-138">Ja</span><span class="sxs-lookup"><span data-stu-id="64dfa-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="64dfa-139">Versies</span><span class="sxs-lookup"><span data-stu-id="64dfa-139">Versions</span></span>
<span data-ttu-id="64dfa-140">Klanten kunnen XenApp onderdelen implementeren als virtuele Machines waarop Hyper-V- of VMware of fysieke Servers.</span><span class="sxs-lookup"><span data-stu-id="64dfa-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="64dfa-141">Azure Site Recovery kan fysieke en virtuele implementaties naar Azure te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="64dfa-141">Azure Site Recovery can protect both physical and virtual deployments to Azure.</span></span>
<span data-ttu-id="64dfa-142">Aangezien XenApp 7,7 of hoger wordt ondersteund in Azure, kunnen alleen implementaties met deze versies failover naar Azure voor herstel na noodgevallen of migratie.</span><span class="sxs-lookup"><span data-stu-id="64dfa-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over to Azure for Disaster Recovery or migration.</span></span>

### <a name="things-to-keep-in-mind"></a><span data-ttu-id="64dfa-143">Houd er rekening mee houden</span><span class="sxs-lookup"><span data-stu-id="64dfa-143">Things to keep in mind</span></span>

1. <span data-ttu-id="64dfa-144">Beveiliging en herstel van lokale implementaties met Server OS machines leveren XenApp gepubliceerde apps en XenApp gepubliceerd bureaubladen wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="64dfa-144">Protection and recovery of on-premises deployments using Server OS machines to deliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="64dfa-145">Beveiliging en herstel van on-premises implementaties bureaublad OS-machines met VDI Desktop leveren voor client virtuele bureaubladen, met inbegrip van Windows 10, wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="64dfa-145">Protection and recovery of on-premises deployments using desktop OS machines to deliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="64dfa-146">Dit is omdat het herstel van computers met bureaublad OS'es biedt geen ondersteuning voor ASR.</span><span class="sxs-lookup"><span data-stu-id="64dfa-146">This is because ASR does not support the recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="64dfa-147">Bovendien sommige client virtueel bureaublad aroma's (bv.</span><span class="sxs-lookup"><span data-stu-id="64dfa-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="64dfa-148">Windows 7) zijn nog niet ondersteund voor licentieverlening in Azure.</span><span class="sxs-lookup"><span data-stu-id="64dfa-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="64dfa-149">[Meer informatie](https://azure.microsoft.com/pricing/licensing-faq/) over licentieverlening voor clientbureaubladen en serverdesktops in Azure.</span><span class="sxs-lookup"><span data-stu-id="64dfa-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="64dfa-150">Azure Site Recovery kan niet repliceren en de bestaande lokale MCS of PV's klonen beveiligen.</span><span class="sxs-lookup"><span data-stu-id="64dfa-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="64dfa-151">U moet deze met Azure RM inrichten vanuit levering domeincontroller klonen opnieuw.</span><span class="sxs-lookup"><span data-stu-id="64dfa-151">You need to recreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="64dfa-152">NetScaler kan niet worden beveiligd met Azure Site Recovery zoals NetScaler is gebaseerd op FreeBSD en Azure Site Recovery biedt geen ondersteuning voor beveiliging van het besturingssysteem FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="64dfa-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="64dfa-153">U moet implementeren en configureren van een nieuw toestel NetScaler van Azure-marktplaats na een failover naar Azure.</span><span class="sxs-lookup"><span data-stu-id="64dfa-153">You would need to deploy and configure a new NetScaler appliance from Azure Market place after failover to Azure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="64dfa-154">Repliceren van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="64dfa-154">Replicating virtual machines</span></span>

<span data-ttu-id="64dfa-155">De volgende onderdelen van de Citrix XenApp-implementatie moeten worden beveiligd, zodat de replicatie en herstel.</span><span class="sxs-lookup"><span data-stu-id="64dfa-155">The following components of the Citrix XenApp deployment need to be protected to enable replication and recovery.</span></span>

* <span data-ttu-id="64dfa-156">Beveiliging van AD DNS-server</span><span class="sxs-lookup"><span data-stu-id="64dfa-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="64dfa-157">Beveiliging van SQL database-server</span><span class="sxs-lookup"><span data-stu-id="64dfa-157">Protection of SQL database server</span></span>
* <span data-ttu-id="64dfa-158">Beveiliging van Citrix levering Controller</span><span class="sxs-lookup"><span data-stu-id="64dfa-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="64dfa-159">Beveiliging van server winkel.</span><span class="sxs-lookup"><span data-stu-id="64dfa-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="64dfa-160">Beveiliging van XenApp Master (VDA)</span><span class="sxs-lookup"><span data-stu-id="64dfa-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="64dfa-161">Beveiliging van de licentieserver Citrix XenApp</span><span class="sxs-lookup"><span data-stu-id="64dfa-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="64dfa-162">**AD DNS-server-replicatie**</span><span class="sxs-lookup"><span data-stu-id="64dfa-162">**AD DNS server replication**</span></span>

<span data-ttu-id="64dfa-163">Raadpleeg [beveiligen van Active Directory en DNS met Azure Site Recovery](site-recovery-active-directory.md) op richtlijnen voor het repliceren van en het configureren van een domeincontroller in Azure.</span><span class="sxs-lookup"><span data-stu-id="64dfa-163">Please refer to [Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="64dfa-164">**SQL Server databasereplicatie**</span><span class="sxs-lookup"><span data-stu-id="64dfa-164">**SQL database Server replication**</span></span>

<span data-ttu-id="64dfa-165">Raadpleeg [SQL-Server beveiligen met SQL Server-noodherstel en Azure Site Recovery](site-recovery-sql.md) voor gedetailleerde technische richtlijnen voor de aanbevolen opties voor het beveiligen van SQL-servers.</span><span class="sxs-lookup"><span data-stu-id="64dfa-165">Please refer to [Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on the recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="64dfa-166">Ga als volgt [in deze richtlijnen](site-recovery-vmware-to-azure.md) naar het andere onderdeel virtuele machines repliceren naar Azure.</span><span class="sxs-lookup"><span data-stu-id="64dfa-166">Follow [this guidance](site-recovery-vmware-to-azure.md) to start replicating the other component virtual machines to Azure.</span></span>

![Beveiliging van XenApp onderdelen](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="64dfa-168">**Reken- en netwerkinstellingen**</span><span class="sxs-lookup"><span data-stu-id="64dfa-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="64dfa-169">Nadat de computers zijn beveiligd (status wordt weergegeven als 'Beveiligde' onder gerepliceerde Items), de instellingen van de berekenings- en moeten worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="64dfa-169">After the machines are protected (status shows as “Protected” under Replicated Items), the Compute and Network settings need to be configured.</span></span>
<span data-ttu-id="64dfa-170">In de berekening en netwerk > Compute-eigenschappen, kunt u de Azure VM-naam en doel-grootte.</span><span class="sxs-lookup"><span data-stu-id="64dfa-170">In Compute and Network > Compute properties, you can specify the Azure VM name and target size.</span></span>
<span data-ttu-id="64dfa-171">De naam om te voldoen aan de Azure-vereisten als u wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="64dfa-171">Modify the name to comply with Azure requirements if you need to.</span></span> <span data-ttu-id="64dfa-172">U kunt ook bekijken en informatie over het doelnetwerk, subnet en IP-adres dat wordt toegewezen aan de Azure VM toevoegen.</span><span class="sxs-lookup"><span data-stu-id="64dfa-172">You can also view and add information about the target network, subnet, and IP address that will be assigned to the Azure VM.</span></span>

<span data-ttu-id="64dfa-173">Houd rekening met het volgende:</span><span class="sxs-lookup"><span data-stu-id="64dfa-173">Note the following:</span></span>

* <span data-ttu-id="64dfa-174">U kunt het doel-IP-adres instellen.</span><span class="sxs-lookup"><span data-stu-id="64dfa-174">You can set the target IP address.</span></span> <span data-ttu-id="64dfa-175">Als u geen adres opgeeft, maakt de machine waarvoor een failover is uitgevoerd, gebruik van DHCP.</span><span class="sxs-lookup"><span data-stu-id="64dfa-175">If you don't provide an address, the failed over machine will use DHCP.</span></span> <span data-ttu-id="64dfa-176">Als u een adres dat is niet beschikbaar bij een failover, werkt de failover niet.</span><span class="sxs-lookup"><span data-stu-id="64dfa-176">If you set an address that isn't available at failover, the failover won't work.</span></span> <span data-ttu-id="64dfa-177">Hetzelfde doel-IP-adres kan worden gebruikt voor een testfailover als het adres beschikbaar is in het testfailovernetwerk.</span><span class="sxs-lookup"><span data-stu-id="64dfa-177">The same target IP address can be used for test failover if the address is available in the test failover network.</span></span>

* <span data-ttu-id="64dfa-178">Voor de AD-en DNS-server kunt het lokale adres behouden u hetzelfde adres opgeven als de DNS-server voor het virtuele Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="64dfa-178">For the AD/DNS server, retaining the on-premises address lets you specify the same address as the DNS server for the Azure Virtual network.</span></span>

<span data-ttu-id="64dfa-179">Het aantal netwerkadapters wordt bepaald door de grootte die u voor de virtuele doelmachine opgeeft. Dat werkt als volgt:</span><span class="sxs-lookup"><span data-stu-id="64dfa-179">The number of network adapters is dictated by the size you specify for the target virtual machine, as follows:</span></span>

*   <span data-ttu-id="64dfa-180">Als het aantal netwerkadapters op de bronmachine kleiner is dan of gelijk is aan het aantal adapters dat is toegestaan voor de grootte van de doelmachine, heeft het doel hetzelfde aantal adapters als de bron.</span><span class="sxs-lookup"><span data-stu-id="64dfa-180">If the number of network adapters on the source machine is less than or equal to the number of adapters allowed for the target machine size, then the target will have the same number of adapters as the source.</span></span>
*   <span data-ttu-id="64dfa-181">Als het aantal adapters voor de virtuele bronmachine meer is dan is toegestaan voor de doelgrootte, wordt het maximum voor de doelgrootte gebruikt.</span><span class="sxs-lookup"><span data-stu-id="64dfa-181">If the number of adapters for the source virtual machine exceeds the number allowed for the target size then the target size maximum will be used.</span></span>
* <span data-ttu-id="64dfa-182">Als een bronmachine bijvoorbeeld twee netwerkadapters heeft en met de grootte van de doelmachine vier netwerkadapters worden ondersteund, heeft de doelcomputer twee adapters.</span><span class="sxs-lookup"><span data-stu-id="64dfa-182">For example, if a source machine has two network adapters and the target machine size supports four, the target machine will have two adapters.</span></span> <span data-ttu-id="64dfa-183">Als de bronmachine twee adapters heeft, maar met de ondersteunde doelgrootte slechts één wordt ondersteund, heeft de doelcomputer slechts één adapter.</span><span class="sxs-lookup"><span data-stu-id="64dfa-183">If the source machine has two adapters but the supported target size only supports one then the target machine will have only one adapter.</span></span>
*   <span data-ttu-id="64dfa-184">Als de virtuele machine meerdere netwerkadapters die worden deze allemaal verbonden met hetzelfde netwerk heeft.</span><span class="sxs-lookup"><span data-stu-id="64dfa-184">If the virtual machine has multiple network adapters they will all connect to the same network.</span></span>
*   <span data-ttu-id="64dfa-185">Als de virtuele machine meerdere netwerkadapters heeft, wordt het eerste beheerpunt dat wordt weergegeven in de lijst met de standaard-netwerkadapter in de virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="64dfa-185">If the virtual machine has multiple network adapters, then the first one shown in the list becomes the Default network adapter in the Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="64dfa-186">Een herstelplan maken</span><span class="sxs-lookup"><span data-stu-id="64dfa-186">Creating a recovery plan</span></span>

<span data-ttu-id="64dfa-187">Nadat replicatie is ingeschakeld voor de virtuele machines XenApp-component, wordt de volgende stap is het maken van een herstelplan.</span><span class="sxs-lookup"><span data-stu-id="64dfa-187">After replication is enabled for the XenApp component VMs, the next step is to create a recovery plan.</span></span>
<span data-ttu-id="64dfa-188">Een herstelplan groepen samen virtuele machines met vergelijkbare vereisten voor failover en herstel.</span><span class="sxs-lookup"><span data-stu-id="64dfa-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="64dfa-189">**Stappen voor het maken van een herstelplan**</span><span class="sxs-lookup"><span data-stu-id="64dfa-189">**Steps to create a recovery plan**</span></span>

1. <span data-ttu-id="64dfa-190">De XenApp onderdeel virtuele machines in het herstelplan toevoegen.</span><span class="sxs-lookup"><span data-stu-id="64dfa-190">Add the XenApp component virtual machines in the Recovery Plan.</span></span>
2. <span data-ttu-id="64dfa-191">Klik op de herstelplannen -> + herstelplan.</span><span class="sxs-lookup"><span data-stu-id="64dfa-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="64dfa-192">Geef een intuïtieve naam voor het herstelplan.</span><span class="sxs-lookup"><span data-stu-id="64dfa-192">Provide an intuitive name for the recovery plan.</span></span>
3. <span data-ttu-id="64dfa-193">Voor virtuele VMware-machines: bron selecteren als processerver VMware, doel als Microsoft Azure en implementatiemodel als Resource Manager en klik op items selecteren.</span><span class="sxs-lookup"><span data-stu-id="64dfa-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="64dfa-194">Voor Hyper-V virtuele machines: bron selecteren als VMM-server, als Microsoft Azure en als Resource Manager-implementatiemodel zijn gericht en klik op items selecteren en selecteer vervolgens de implementatie XenApp virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="64dfa-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select the XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-to-failover-groups"></a><span data-ttu-id="64dfa-195">Virtuele machines worden toegevoegd aan failover-groepen</span><span class="sxs-lookup"><span data-stu-id="64dfa-195">Adding virtual machines to failover groups</span></span>

<span data-ttu-id="64dfa-196">Plannen voor herstel kunnen worden aangepast voor het toevoegen van failover-groepen voor specifieke opstartvolgorde scripts of handmatige acties.</span><span class="sxs-lookup"><span data-stu-id="64dfa-196">Recovery plans can be customized to add failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="64dfa-197">De volgende groepen moeten worden toegevoegd aan het herstelplan.</span><span class="sxs-lookup"><span data-stu-id="64dfa-197">The following groups need to be added to the recovery plan.</span></span>

1. <span data-ttu-id="64dfa-198">Failover Group1: AD DNS</span><span class="sxs-lookup"><span data-stu-id="64dfa-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="64dfa-199">Failover-Group2: SQL Server-VM's</span><span class="sxs-lookup"><span data-stu-id="64dfa-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="64dfa-200">Failover groep3: VDA Master installatiekopie VM</span><span class="sxs-lookup"><span data-stu-id="64dfa-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="64dfa-201">Failover Group4: De levering van Controller en de winkel server VMs</span><span class="sxs-lookup"><span data-stu-id="64dfa-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-to-the-recovery-plan"></a><span data-ttu-id="64dfa-202">Scripts toe te voegen aan het herstelplan</span><span class="sxs-lookup"><span data-stu-id="64dfa-202">Adding scripts to the recovery plan</span></span>

<span data-ttu-id="64dfa-203">Scripts kunnen worden uitgevoerd vóór of na een bepaalde groep in een plan voor herstel.</span><span class="sxs-lookup"><span data-stu-id="64dfa-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="64dfa-204">Handmatige acties kunnen worden ook worden opgenomen en tijdens de failover is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="64dfa-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="64dfa-205">Het aangepaste herstelplan lijkt op het onderstaande:</span><span class="sxs-lookup"><span data-stu-id="64dfa-205">The customized recovery plan looks like the below:</span></span>

1. <span data-ttu-id="64dfa-206">Failover Group1: AD DNS</span><span class="sxs-lookup"><span data-stu-id="64dfa-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="64dfa-207">Failover-Group2: SQL Server-VM's</span><span class="sxs-lookup"><span data-stu-id="64dfa-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="64dfa-208">Failover groep3: VDA Master installatiekopie VM</span><span class="sxs-lookup"><span data-stu-id="64dfa-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="64dfa-209">Stap 4, 6 en 7 handmatig of script of acties die van toepassing zijn op alleen een lokale XenApp >-omgeving met MCS/PV's catalogussen.</span><span class="sxs-lookup"><span data-stu-id="64dfa-209">Steps 4, 6 and 7 containing manual or script actions are applicable to only an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="64dfa-210">De actie handmatig of script groep 3: master VDA VM de Master VDA VM afsluiten wanneer een failover naar Azure worden actief is.</span><span class="sxs-lookup"><span data-stu-id="64dfa-210">Group 3 Manual or script action: Shutdown master VDA VM The Master VDA VM when failed over to Azure will be in a running state.</span></span> <span data-ttu-id="64dfa-211">Voor het maken van nieuwe MCS catalogussen met behulp van Azure ARM die als host fungeert de master VDA VM is vereist om te worden gestopt (de toegewezen) staat.</span><span class="sxs-lookup"><span data-stu-id="64dfa-211">To create new MCS catalogs using Azure ARM hosting, the master VDA VM is required to be in Stopped (de allocated) state.</span></span> <span data-ttu-id="64dfa-212">De virtuele machine van Azure-Portal wordt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="64dfa-212">Shutdown the VM from Azure Portal.</span></span>

5. <span data-ttu-id="64dfa-213">Failover Group4: De levering van Controller en de winkel server VMs</span><span class="sxs-lookup"><span data-stu-id="64dfa-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="64dfa-214">Groep3 handmatig of script actie 1:</span><span class="sxs-lookup"><span data-stu-id="64dfa-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="64dfa-215">***Azure RM hostverbinding toevoegen***</span><span class="sxs-lookup"><span data-stu-id="64dfa-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="64dfa-216">Azure ARM hostverbinding maken in de bezorging Controller machine voor het inrichten van nieuwe MCS catalogussen in Azure.</span><span class="sxs-lookup"><span data-stu-id="64dfa-216">Create Azure ARM host connection in Delivery Controller machine to provision new MCS catalogs in Azure.</span></span> <span data-ttu-id="64dfa-217">Volg de stappen zoals wordt beschreven in dit [artikel](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span><span class="sxs-lookup"><span data-stu-id="64dfa-217">Follow the steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="64dfa-218">Groep3 handmatig of script actie 2:</span><span class="sxs-lookup"><span data-stu-id="64dfa-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="64dfa-219">***MCS-catalogussen in Azure opnieuw maken***</span><span class="sxs-lookup"><span data-stu-id="64dfa-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="64dfa-220">De bestaande MCS of PV's klonen op de primaire site wordt niet gerepliceerd naar Azure.</span><span class="sxs-lookup"><span data-stu-id="64dfa-220">The existing MCS or PVS clones on the primary site will not be replicated to Azure.</span></span> <span data-ttu-id="64dfa-221">U moet deze met behulp van de gerepliceerde master VDA en Azure ARM inrichten vanuit levering domeincontroller klonen opnieuw. Volg de stappen zoals wordt beschreven in dit [artikel](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) MCS catalogussen maken in Azure.</span><span class="sxs-lookup"><span data-stu-id="64dfa-221">You need to recreate these clones using the replicated master VDA and Azure ARM provisioning from Delivery controller.Follow the steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) to create MCS catalogs in Azure.</span></span>

![Plan voor herstel voor XenApp onderdelen](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="64dfa-223">U kunt scripts op de [locatie](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) bijwerken van de DNS-server met de nieuwe IP-adressen van de mislukte via > virtuele machines of koppelen van een load balancer op de mislukte via de virtuele machine, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="64dfa-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) to update the DNS with the new IPs of the failed over >virtual machines or to attach a load balancer on the failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="64dfa-224">Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="64dfa-224">Doing a test failover</span></span>

<span data-ttu-id="64dfa-225">Ga als volgt [in deze richtlijnen](site-recovery-test-failover-to-azure.md) een testfailover uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="64dfa-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

![Plan voor herstel](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="64dfa-227">U een failover uitvoert</span><span class="sxs-lookup"><span data-stu-id="64dfa-227">Doing a failover</span></span>

<span data-ttu-id="64dfa-228">Ga als volgt [in deze richtlijnen](site-recovery-failover.md) bij het uitvoeren van een failover.</span><span class="sxs-lookup"><span data-stu-id="64dfa-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64dfa-229">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="64dfa-229">Next steps</span></span>

<span data-ttu-id="64dfa-230">U kunt [meer](https://aka.ms/citrix-xenapp-xendesktop-with-asr) over Citrix XenApp en XenDesktop implementaties in deze white paper repliceren.</span><span class="sxs-lookup"><span data-stu-id="64dfa-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="64dfa-231">Bekijk de richtlijnen voor [andere toepassingen repliceren](site-recovery-workload.md) met Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="64dfa-231">Look at the guidance to [replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>

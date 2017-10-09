---
title: een Citrix XenDesktop en XenApp implementatie van meerdere lagen met Azure Site Recovery aaaReplicate | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooprotect en herstel Citrix XenDesktop en XenApp implementaties met Azure Site Recovery.
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
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="b9817-103">Een Citrix XenApp en XenDesktop implementatie van meerdere lagen met Azure Site Recovery repliceren</span><span class="sxs-lookup"><span data-stu-id="b9817-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="b9817-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b9817-104">Overview</span></span>

<span data-ttu-id="b9817-105">Citrix XenDesktop is een bureaublad-virtualisatie-oplossing die bureaubladen en toepassingen als ondemand service tooany gebruiker met een willekeurige plaats levert.</span><span class="sxs-lookup"><span data-stu-id="b9817-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service tooany user, anywhere.</span></span> <span data-ttu-id="b9817-106">Met de FlexCast levering technologie kunt XenDesktop snel en veilig leveren toepassingen en bureaubladen toousers.</span><span class="sxs-lookup"><span data-stu-id="b9817-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops toousers.</span></span>
<span data-ttu-id="b9817-107">Vandaag de dag biedt Citrix XenApp geen elke ramp herstelfuncties.</span><span class="sxs-lookup"><span data-stu-id="b9817-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="b9817-108">Een goede noodhersteloplossing moet modellering van herstelplannen rond Hallo hierboven architecturen voor complexe toepassingen bevatten en ook Hallo mogelijkheid tooadd aangepast stappen toohandle Toepassingstoewijzingen tussen verschillende lagen daarom bieden een één klik ervoor oplossing maken in geval van een noodgeval voorloopspaties tooa Hallo RTO verlagen.</span><span class="sxs-lookup"><span data-stu-id="b9817-108">A good disaster recovery solution, should allow modeling of recovery plans around hello above complex application architectures and also have hello ability tooadd customized steps toohandle application mappings between various tiers hence providing a single-click sure shot solution in hello event of a disaster leading tooa lower RTO.</span></span>

<span data-ttu-id="b9817-109">Dit document bevat een stapsgewijze instructies voor het bouwen van een noodherstel voor uw on-premises Citrix XenApp implementaties op Hyper-V- en VMware vSphere-platforms.</span><span class="sxs-lookup"><span data-stu-id="b9817-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="b9817-110">Dit document beschrijft ook hoe tooperform een testfailover (drill disaster recovery) en niet-geplande failover tooAzure met herstelplannen, Hallo ondersteunde configuraties en vereisten.</span><span class="sxs-lookup"><span data-stu-id="b9817-110">This document also describes how tooperform a test failover(disaster recovery drill) and unplanned failover tooAzure using recovery plans, hello supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b9817-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b9817-111">Prerequisites</span></span>

<span data-ttu-id="b9817-112">Voordat u begint, zorg er dan voor dat u begrijpt Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="b9817-112">Before you start, make sure you understand hello following:</span></span>

1. [<span data-ttu-id="b9817-113">Een virtuele machine tooAzure repliceren</span><span class="sxs-lookup"><span data-stu-id="b9817-113">Replicating a virtual machine tooAzure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="b9817-114">Hoe te[ontwerpen van een netwerk herstel](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="b9817-114">How too[design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="b9817-115">Tijdens het doorzoeken van een failover-test tooAzure</span><span class="sxs-lookup"><span data-stu-id="b9817-115">Doing a test failover tooAzure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="b9817-116">Tijdens het doorzoeken van een failover-tooAzure</span><span class="sxs-lookup"><span data-stu-id="b9817-116">Doing a failover tooAzure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="b9817-117">Hoe te[repliceren van een domeincontroller](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="b9817-117">How too[replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="b9817-118">Hoe te[SQL-Server repliceren](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="b9817-118">How too[replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="b9817-119">Implementaties</span><span class="sxs-lookup"><span data-stu-id="b9817-119">Deployment patterns</span></span>

<span data-ttu-id="b9817-120">Een farm Citrix XenApp en XenDesktop heeft doorgaans Hallo implementatie patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="b9817-120">A Citrix XenApp and XenDesktop farm typically has hello following deployment pattern:</span></span>

<span data-ttu-id="b9817-121">**Patroon van de implementatie**</span><span class="sxs-lookup"><span data-stu-id="b9817-121">**Deployment pattern**</span></span>

<span data-ttu-id="b9817-122">Citrix XenApp en XenDesktop implementatie met AD DNS-server, SQL databaseserver server, Citrix levering Controller, winkel, XenApp Master (VDA), Citrix XenApp licentieserver</span><span class="sxs-lookup"><span data-stu-id="b9817-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![Implementatie-patroon 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="b9817-124">Site Recovery-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="b9817-124">Site Recovery support</span></span>

<span data-ttu-id="b9817-125">Citrix-implementaties op virtuele VMware-machines worden beheerd door vSphere 6.0-System Center VMM 2012 R2 zijn gebruikte toosetup DR voor Hallo doel van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="b9817-125">For hello purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used toosetup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="b9817-126">Bron en doel</span><span class="sxs-lookup"><span data-stu-id="b9817-126">Source and target</span></span>

<span data-ttu-id="b9817-127">**Scenario**</span><span class="sxs-lookup"><span data-stu-id="b9817-127">**Scenario**</span></span> | <span data-ttu-id="b9817-128">**de secundaire site tooa**</span><span class="sxs-lookup"><span data-stu-id="b9817-128">**tooa secondary site**</span></span> | <span data-ttu-id="b9817-129">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="b9817-129">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="b9817-130">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="b9817-130">**Hyper-V**</span></span> | <span data-ttu-id="b9817-131">Niet binnen het bereik</span><span class="sxs-lookup"><span data-stu-id="b9817-131">Not in scope</span></span> | <span data-ttu-id="b9817-132">Ja</span><span class="sxs-lookup"><span data-stu-id="b9817-132">Yes</span></span>
<span data-ttu-id="b9817-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="b9817-133">**VMware**</span></span> | <span data-ttu-id="b9817-134">Niet binnen het bereik</span><span class="sxs-lookup"><span data-stu-id="b9817-134">Not in scope</span></span> | <span data-ttu-id="b9817-135">Ja</span><span class="sxs-lookup"><span data-stu-id="b9817-135">Yes</span></span>
<span data-ttu-id="b9817-136">**Fysieke server**</span><span class="sxs-lookup"><span data-stu-id="b9817-136">**Physical server**</span></span> | <span data-ttu-id="b9817-137">Niet binnen het bereik</span><span class="sxs-lookup"><span data-stu-id="b9817-137">Not in scope</span></span> | <span data-ttu-id="b9817-138">Ja</span><span class="sxs-lookup"><span data-stu-id="b9817-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="b9817-139">Versies</span><span class="sxs-lookup"><span data-stu-id="b9817-139">Versions</span></span>
<span data-ttu-id="b9817-140">Klanten kunnen XenApp onderdelen implementeren als virtuele Machines waarop Hyper-V- of VMware of fysieke Servers.</span><span class="sxs-lookup"><span data-stu-id="b9817-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="b9817-141">Azure Site Recovery kunt beveiligen beide tooAzure fysieke en virtuele-implementaties.</span><span class="sxs-lookup"><span data-stu-id="b9817-141">Azure Site Recovery can protect both physical and virtual deployments tooAzure.</span></span>
<span data-ttu-id="b9817-142">Aangezien XenApp 7,7 of hoger wordt ondersteund in Azure, alleen implementaties met deze versies failover mogelijk tooAzure voor herstel na noodgevallen of migratie.</span><span class="sxs-lookup"><span data-stu-id="b9817-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over tooAzure for Disaster Recovery or migration.</span></span>

### <a name="things-tookeep-in-mind"></a><span data-ttu-id="b9817-143">Dingen tookeep rekening</span><span class="sxs-lookup"><span data-stu-id="b9817-143">Things tookeep in mind</span></span>

1. <span data-ttu-id="b9817-144">Beveiliging en herstel van lokale implementaties met behulp van Server-besturingssysteem machines toodeliver XenApp gepubliceerde apps en XenApp gepubliceerd bureaubladen wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b9817-144">Protection and recovery of on-premises deployments using Server OS machines toodeliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="b9817-145">Beveiliging en herstel van on-premises implementaties met bureaublad OS machines toodeliver VDI Desktop voor client virtuele bureaubladen, met inbegrip van Windows 10, wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b9817-145">Protection and recovery of on-premises deployments using desktop OS machines toodeliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="b9817-146">Dit is omdat ASR Hallo herstel van machines met bureaublad OS'es niet ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="b9817-146">This is because ASR does not support hello recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="b9817-147">Bovendien sommige client virtueel bureaublad aroma's (bv.</span><span class="sxs-lookup"><span data-stu-id="b9817-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="b9817-148">Windows 7) zijn nog niet ondersteund voor licentieverlening in Azure.</span><span class="sxs-lookup"><span data-stu-id="b9817-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="b9817-149">[Meer informatie](https://azure.microsoft.com/pricing/licensing-faq/) over licentieverlening voor clientbureaubladen en serverdesktops in Azure.</span><span class="sxs-lookup"><span data-stu-id="b9817-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="b9817-150">Azure Site Recovery kan niet repliceren en de bestaande lokale MCS of PV's klonen beveiligen.</span><span class="sxs-lookup"><span data-stu-id="b9817-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="b9817-151">U moet deze met Azure RM inrichten vanuit levering domeincontroller klonen toorecreate.</span><span class="sxs-lookup"><span data-stu-id="b9817-151">You need toorecreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="b9817-152">NetScaler kan niet worden beveiligd met Azure Site Recovery zoals NetScaler is gebaseerd op FreeBSD en Azure Site Recovery biedt geen ondersteuning voor beveiliging van het besturingssysteem FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="b9817-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="b9817-153">U zou toodeploy nodig hebt en een nieuw toestel NetScaler van Azure-marktplaats na failover tooAzure configureren.</span><span class="sxs-lookup"><span data-stu-id="b9817-153">You would need toodeploy and configure a new NetScaler appliance from Azure Market place after failover tooAzure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="b9817-154">Repliceren van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="b9817-154">Replicating virtual machines</span></span>

<span data-ttu-id="b9817-155">Hallo volgende onderdelen van Hallo Citrix XenApp implementatie moet toobe beveiligd tooenable replicatie en herstel.</span><span class="sxs-lookup"><span data-stu-id="b9817-155">hello following components of hello Citrix XenApp deployment need toobe protected tooenable replication and recovery.</span></span>

* <span data-ttu-id="b9817-156">Beveiliging van AD DNS-server</span><span class="sxs-lookup"><span data-stu-id="b9817-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="b9817-157">Beveiliging van SQL database-server</span><span class="sxs-lookup"><span data-stu-id="b9817-157">Protection of SQL database server</span></span>
* <span data-ttu-id="b9817-158">Beveiliging van Citrix levering Controller</span><span class="sxs-lookup"><span data-stu-id="b9817-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="b9817-159">Beveiliging van server winkel.</span><span class="sxs-lookup"><span data-stu-id="b9817-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="b9817-160">Beveiliging van XenApp Master (VDA)</span><span class="sxs-lookup"><span data-stu-id="b9817-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="b9817-161">Beveiliging van de licentieserver Citrix XenApp</span><span class="sxs-lookup"><span data-stu-id="b9817-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="b9817-162">**AD DNS-server-replicatie**</span><span class="sxs-lookup"><span data-stu-id="b9817-162">**AD DNS server replication**</span></span>

<span data-ttu-id="b9817-163">Raadpleeg het te[beveiligen van Active Directory en DNS met Azure Site Recovery](site-recovery-active-directory.md) op richtlijnen voor het repliceren van en het configureren van een domeincontroller in Azure.</span><span class="sxs-lookup"><span data-stu-id="b9817-163">Please refer too[Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="b9817-164">**SQL Server databasereplicatie**</span><span class="sxs-lookup"><span data-stu-id="b9817-164">**SQL database Server replication**</span></span>

<span data-ttu-id="b9817-165">Raadpleeg het te[SQL-Server beveiligen met SQL Server-noodherstel en Azure Site Recovery](site-recovery-sql.md) voor gedetailleerde technische richtlijnen voor Hallo aanbevolen opties voor het beveiligen van SQL-servers.</span><span class="sxs-lookup"><span data-stu-id="b9817-165">Please refer too[Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on hello recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="b9817-166">Ga als volgt [in deze richtlijnen](site-recovery-vmware-to-azure.md) toostart repliceren Hallo andere tooAzure van onderdeel virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b9817-166">Follow [this guidance](site-recovery-vmware-to-azure.md) toostart replicating hello other component virtual machines tooAzure.</span></span>

![Beveiliging van XenApp onderdelen](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="b9817-168">**Reken- en netwerkinstellingen**</span><span class="sxs-lookup"><span data-stu-id="b9817-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="b9817-169">Nadat Hallo-machines zijn beveiligd (status wordt weergegeven als 'Beveiligde' onder gerepliceerde Items), Compute Hallo en netwerkinstellingen moeten toobe geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="b9817-169">After hello machines are protected (status shows as “Protected” under Replicated Items), hello Compute and Network settings need toobe configured.</span></span>
<span data-ttu-id="b9817-170">In de berekening en netwerk > Compute-eigenschappen, kunt u de naam en doel van de grootte van virtuele machine van Azure Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="b9817-170">In Compute and Network > Compute properties, you can specify hello Azure VM name and target size.</span></span>
<span data-ttu-id="b9817-171">Hallo naam toocomply met Azure-vereisten wijzigen als u wilt.</span><span class="sxs-lookup"><span data-stu-id="b9817-171">Modify hello name toocomply with Azure requirements if you need to.</span></span> <span data-ttu-id="b9817-172">U kunt ook bekijken en informatie over het doelnetwerk hello, subnet en IP-adres dat wordt toegewezen toohello virtuele Azure-machine toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b9817-172">You can also view and add information about hello target network, subnet, and IP address that will be assigned toohello Azure VM.</span></span>

<span data-ttu-id="b9817-173">Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="b9817-173">Note hello following:</span></span>

* <span data-ttu-id="b9817-174">U kunt IP-adres van Hallo doel instellen.</span><span class="sxs-lookup"><span data-stu-id="b9817-174">You can set hello target IP address.</span></span> <span data-ttu-id="b9817-175">Als u een adres niet opgeeft, wordt Hallo failover machine DHCP gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b9817-175">If you don't provide an address, hello failed over machine will use DHCP.</span></span> <span data-ttu-id="b9817-176">Als u een adres dat is niet beschikbaar bij een failover, werkt Hallo failover niet.</span><span class="sxs-lookup"><span data-stu-id="b9817-176">If you set an address that isn't available at failover, hello failover won't work.</span></span> <span data-ttu-id="b9817-177">Hallo hetzelfde IP-adres van doel kan worden gebruikt voor een testfailover als Hallo adres in het testfailovernetwerk Hallo beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="b9817-177">hello same target IP address can be used for test failover if hello address is available in hello test failover network.</span></span>

* <span data-ttu-id="b9817-178">Voor Hallo AD en DNS-server, bewaren Hallo on-premises adres-kunt die u dezelfde adres Hallo opgeven als Hallo DNS-server voor hello Azure Virtual network.</span><span class="sxs-lookup"><span data-stu-id="b9817-178">For hello AD/DNS server, retaining hello on-premises address lets you specify hello same address as hello DNS server for hello Azure Virtual network.</span></span>

<span data-ttu-id="b9817-179">Hallo aantal netwerkadapters wordt bepaald door Hallo-grootte die u voor Hallo doel-virtuele machine, als volgt opgeeft:</span><span class="sxs-lookup"><span data-stu-id="b9817-179">hello number of network adapters is dictated by hello size you specify for hello target virtual machine, as follows:</span></span>

*   <span data-ttu-id="b9817-180">Als het aantal netwerkadapters op de bronmachine Hallo Hallo kleiner dan of gelijk aantal adapters toohello toegestaan voor de doelgrootte machine Hallo vervolgens Hallo doel hetzelfde aantal adapters als bron Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b9817-180">If hello number of network adapters on hello source machine is less than or equal toohello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
*   <span data-ttu-id="b9817-181">Als het aantal adapters voor de virtuele bronmachine Hallo HALLO hallo maximum overschrijden voor Hallo doelgrootte, wordt maximaal Hallo doel wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b9817-181">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size then hello target size maximum will be used.</span></span>
* <span data-ttu-id="b9817-182">Als een bronmachine twee netwerkadapters heeft en de grootte van Hallo doelmachine vier ondersteunt, wordt Hallo doelmachine twee adapters hebben.</span><span class="sxs-lookup"><span data-stu-id="b9817-182">For example, if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="b9817-183">Als Hallo-bronmachine twee adapters heeft, maar hello ondersteunde doelgrootte biedt alleen ondersteuning voor een hebben Hallo doelmachine slechts één adapter.</span><span class="sxs-lookup"><span data-stu-id="b9817-183">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>
*   <span data-ttu-id="b9817-184">Als Hallo virtuele machine meerdere netwerkadapters heeft worden deze allemaal verbonden toohello hetzelfde netwerk.</span><span class="sxs-lookup"><span data-stu-id="b9817-184">If hello virtual machine has multiple network adapters they will all connect toohello same network.</span></span>
*   <span data-ttu-id="b9817-185">Als Hallo virtuele machine meerdere netwerkadapters heeft, wordt hello eerste is weergegeven in de lijst hello vervolgens Hallo standaard-netwerkadapter in hello Azure virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b9817-185">If hello virtual machine has multiple network adapters, then hello first one shown in hello list becomes hello Default network adapter in hello Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="b9817-186">Een herstelplan maken</span><span class="sxs-lookup"><span data-stu-id="b9817-186">Creating a recovery plan</span></span>

<span data-ttu-id="b9817-187">Nadat de replicatie is ingeschakeld voor Hallo XenApp onderdeel VM's, is de volgende stap Hallo toocreate een herstelplan.</span><span class="sxs-lookup"><span data-stu-id="b9817-187">After replication is enabled for hello XenApp component VMs, hello next step is toocreate a recovery plan.</span></span>
<span data-ttu-id="b9817-188">Een herstelplan groepen samen virtuele machines met vergelijkbare vereisten voor failover en herstel.</span><span class="sxs-lookup"><span data-stu-id="b9817-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="b9817-189">**Stappen toocreate een herstelplan**</span><span class="sxs-lookup"><span data-stu-id="b9817-189">**Steps toocreate a recovery plan**</span></span>

1. <span data-ttu-id="b9817-190">Hallo XenApp onderdeel virtual machines toevoegen in Hallo herstelplan.</span><span class="sxs-lookup"><span data-stu-id="b9817-190">Add hello XenApp component virtual machines in hello Recovery Plan.</span></span>
2. <span data-ttu-id="b9817-191">Klik op de herstelplannen -> + herstelplan.</span><span class="sxs-lookup"><span data-stu-id="b9817-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="b9817-192">Geef een intuïtieve naam voor het herstelplan Hallo.</span><span class="sxs-lookup"><span data-stu-id="b9817-192">Provide an intuitive name for hello recovery plan.</span></span>
3. <span data-ttu-id="b9817-193">Voor virtuele VMware-machines: bron selecteren als processerver VMware, doel als Microsoft Azure en implementatiemodel als Resource Manager en klik op items selecteren.</span><span class="sxs-lookup"><span data-stu-id="b9817-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="b9817-194">Voor Hyper-V virtuele machines: bron selecteren als VMM-server, zoals Microsoft Azure en als Resource Manager-implementatiemodel zijn gericht en klik op items selecteren en selecteer Hallo XenApp implementatie virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b9817-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select hello XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-toofailover-groups"></a><span data-ttu-id="b9817-195">Toevoegen van virtuele machines toofailover groepen</span><span class="sxs-lookup"><span data-stu-id="b9817-195">Adding virtual machines toofailover groups</span></span>

<span data-ttu-id="b9817-196">Plannen voor herstel kunnen worden aangepast tooadd failover groepen voor starten van de specifieke volgorde, scripts of handmatige acties.</span><span class="sxs-lookup"><span data-stu-id="b9817-196">Recovery plans can be customized tooadd failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="b9817-197">Hallo na groepen moet toobe toegevoegde toohello herstelplan.</span><span class="sxs-lookup"><span data-stu-id="b9817-197">hello following groups need toobe added toohello recovery plan.</span></span>

1. <span data-ttu-id="b9817-198">Failover Group1: AD DNS</span><span class="sxs-lookup"><span data-stu-id="b9817-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="b9817-199">Failover-Group2: SQL Server-VM's</span><span class="sxs-lookup"><span data-stu-id="b9817-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="b9817-200">Failover groep3: VDA Master installatiekopie VM</span><span class="sxs-lookup"><span data-stu-id="b9817-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="b9817-201">Failover Group4: De levering van Controller en de winkel server VMs</span><span class="sxs-lookup"><span data-stu-id="b9817-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-toohello-recovery-plan"></a><span data-ttu-id="b9817-202">Het herstelplan toohello toe te voegen scripts</span><span class="sxs-lookup"><span data-stu-id="b9817-202">Adding scripts toohello recovery plan</span></span>

<span data-ttu-id="b9817-203">Scripts kunnen worden uitgevoerd vóór of na een bepaalde groep in een plan voor herstel.</span><span class="sxs-lookup"><span data-stu-id="b9817-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="b9817-204">Handmatige acties kunnen worden ook worden opgenomen en tijdens de failover is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b9817-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="b9817-205">de aangepaste herstelplan Hallo ziet er Hallo hieronder:</span><span class="sxs-lookup"><span data-stu-id="b9817-205">hello customized recovery plan looks like hello below:</span></span>

1. <span data-ttu-id="b9817-206">Failover Group1: AD DNS</span><span class="sxs-lookup"><span data-stu-id="b9817-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="b9817-207">Failover-Group2: SQL Server-VM's</span><span class="sxs-lookup"><span data-stu-id="b9817-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="b9817-208">Failover groep3: VDA Master installatiekopie VM</span><span class="sxs-lookup"><span data-stu-id="b9817-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="b9817-209">Stap 4, 6 en 7 met handmatige of script acties zijn van toepassing tooonly een lokale XenApp >-omgeving met MCS/PV's catalogussen.</span><span class="sxs-lookup"><span data-stu-id="b9817-209">Steps 4, 6 and 7 containing manual or script actions are applicable tooonly an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="b9817-210">De actie handmatig of script groep 3: afsluiten master VDA VM Hallo Master VDA VM na een failover uitgevoerd tooAzure zich in een actieve status.</span><span class="sxs-lookup"><span data-stu-id="b9817-210">Group 3 Manual or script action: Shutdown master VDA VM hello Master VDA VM when failed over tooAzure will be in a running state.</span></span> <span data-ttu-id="b9817-211">toocreate nieuwe MCS catalogussen met behulp van Azure ARM die als host fungeert, Hallo master VDA VM is vereist toobe in gestopt (de toegewezen) staat.</span><span class="sxs-lookup"><span data-stu-id="b9817-211">toocreate new MCS catalogs using Azure ARM hosting, hello master VDA VM is required toobe in Stopped (de allocated) state.</span></span> <span data-ttu-id="b9817-212">Afsluiten hello VM van Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b9817-212">Shutdown hello VM from Azure Portal.</span></span>

5. <span data-ttu-id="b9817-213">Failover Group4: De levering van Controller en de winkel server VMs</span><span class="sxs-lookup"><span data-stu-id="b9817-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="b9817-214">Groep3 handmatig of script actie 1:</span><span class="sxs-lookup"><span data-stu-id="b9817-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="b9817-215">***Azure RM hostverbinding toevoegen***</span><span class="sxs-lookup"><span data-stu-id="b9817-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="b9817-216">Azure ARM hostverbinding maken in levering Controller machine tooprovision nieuwe MCS catalogussen in Azure.</span><span class="sxs-lookup"><span data-stu-id="b9817-216">Create Azure ARM host connection in Delivery Controller machine tooprovision new MCS catalogs in Azure.</span></span> <span data-ttu-id="b9817-217">Hallo stappen zoals wordt beschreven in dit [artikel](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span><span class="sxs-lookup"><span data-stu-id="b9817-217">Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="b9817-218">Groep3 handmatig of script actie 2:</span><span class="sxs-lookup"><span data-stu-id="b9817-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="b9817-219">***MCS-catalogussen in Azure opnieuw maken***</span><span class="sxs-lookup"><span data-stu-id="b9817-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="b9817-220">Hallo bestaande MCS of PV's klonen op Hallo primaire site worden niet gerepliceerd tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b9817-220">hello existing MCS or PVS clones on hello primary site will not be replicated tooAzure.</span></span> <span data-ttu-id="b9817-221">U moet deze met behulp van Hallo klonen gerepliceerd master VDA en Azure ARM-inrichting van levering controller toorecreate. Hallo stappen zoals wordt beschreven in dit [artikel](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catalogus maken in Azure.</span><span class="sxs-lookup"><span data-stu-id="b9817-221">You need toorecreate these clones using hello replicated master VDA and Azure ARM provisioning from Delivery controller.Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catalogs in Azure.</span></span>

![Plan voor herstel voor XenApp onderdelen](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="b9817-223">U kunt scripts op de [locatie](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello, DNS-Hello nieuwe IP-adressen van Hallo failover > virtuele machines of tooattach een load balancer op Hallo failover virtuele machine, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="b9817-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS with hello new IPs of hello failed over >virtual machines or tooattach a load balancer on hello failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="b9817-224">Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b9817-224">Doing a test failover</span></span>

<span data-ttu-id="b9817-225">Ga als volgt [in deze richtlijnen](site-recovery-test-failover-to-azure.md) toodo een testfailover.</span><span class="sxs-lookup"><span data-stu-id="b9817-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

![Plan voor herstel](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="b9817-227">U een failover uitvoert</span><span class="sxs-lookup"><span data-stu-id="b9817-227">Doing a failover</span></span>

<span data-ttu-id="b9817-228">Ga als volgt [in deze richtlijnen](site-recovery-failover.md) bij het uitvoeren van een failover.</span><span class="sxs-lookup"><span data-stu-id="b9817-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9817-229">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b9817-229">Next steps</span></span>

<span data-ttu-id="b9817-230">U kunt [meer](https://aka.ms/citrix-xenapp-xendesktop-with-asr) over Citrix XenApp en XenDesktop implementaties in deze white paper repliceren.</span><span class="sxs-lookup"><span data-stu-id="b9817-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="b9817-231">Bekijkt hello richtlijnen te[andere toepassingen repliceren](site-recovery-workload.md) met Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b9817-231">Look at hello guidance too[replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>

---
title: aaaReplicate Hyper-V-machines in VMM tooa secundaire site met PowerShell (Azure Resource Manager) | Microsoft Docs
description: Hierin wordt beschreven hoe toodeploy Azure Site Recovery tooorchestrate replicatie, failovers en herstel van Hyper-V-machines in VMM clouds tooa secundaire VMM-site met behulp van PowerShell (Resource Manager)
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="bf798-103">Hyper-V virtuele machines in VMM-clouds tooa secundaire VMM-site met behulp van PowerShell (Resource Manager) repliceren</span><span class="sxs-lookup"><span data-stu-id="bf798-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf798-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bf798-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="bf798-105">Klassieke portal</span><span class="sxs-lookup"><span data-stu-id="bf798-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="bf798-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bf798-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="bf798-107">Welkom tooAzure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="bf798-107">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="bf798-108">Gebruik dit artikel als u wilt dat tooreplicate lokale Hyper-V virtuele machines die worden beheerd in System Center Virtual Machine Manager (VMM) clouds tooa secundaire site.</span><span class="sxs-lookup"><span data-stu-id="bf798-108">Use this article if you want tooreplicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooa secondary site.</span></span>

<span data-ttu-id="bf798-109">Dit artikel laat zien hoe toouse PowerShell tooautomate algemene taken moet u tooperform bij het instellen van Azure Site Recovery tooreplicate Hyper-V virtuele machines in System Center VMM-clouds tooSystem Center VMM-clouds in de secundaire site.</span><span class="sxs-lookup"><span data-stu-id="bf798-109">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooSystem Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="bf798-110">Hallo artikel bevat vereisten voor Hallo scenario en laat zien u</span><span class="sxs-lookup"><span data-stu-id="bf798-110">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="bf798-111">Hoe tooset van een Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="bf798-111">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="bf798-112">Hello Azure Site Recovery Provider installeren op de bronserver VMM Hallo en Hallo doel-VMM-server</span><span class="sxs-lookup"><span data-stu-id="bf798-112">Install hello Azure Site Recovery Provider on hello source VMM server and hello target VMM server</span></span>
* <span data-ttu-id="bf798-113">Hallo VMM server (s) in Hallo kluis registreren</span><span class="sxs-lookup"><span data-stu-id="bf798-113">Register hello VMM server(s) in hello vault</span></span>
* <span data-ttu-id="bf798-114">Replicatiebeleid voor Hallo VMM-Cloud te configureren.</span><span class="sxs-lookup"><span data-stu-id="bf798-114">Configure replication policy for hello VMM Cloud.</span></span> <span data-ttu-id="bf798-115">Hallo replicatie-instellingen in het Hallo-beleid worden toegepast tooall beveiligde virtuele machines</span><span class="sxs-lookup"><span data-stu-id="bf798-115">hello replication settings in hello policy will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="bf798-116">Schakel de beveiliging voor Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="bf798-116">Enable protection for hello virtual machines.</span></span>
* <span data-ttu-id="bf798-117">Hallo testfailover van virtuele machines afzonderlijk of als onderdeel van een herstel plan toomake controleren of alles werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="bf798-117">Test hello failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>
* <span data-ttu-id="bf798-118">Voer een geplande of een niet-geplande failover van virtuele machines afzonderlijk of als onderdeel van een plan toomake voor herstel controleren of dat alles werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="bf798-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>

<span data-ttu-id="bf798-119">Als u problemen bij het instellen van dit scenario, stel uw vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="bf798-119">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="bf798-120">Azure heeft twee verschillende [implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md) voor het maken van en werken met resources: Azure Resource Manager en het klassieke model.</span><span class="sxs-lookup"><span data-stu-id="bf798-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="bf798-121">Azure heeft bovendien twee portals: de klassieke Azure-portal die ondersteuning biedt voor het klassieke implementatiemodel Hallo Hallo en hello Azure-portal met ondersteuning voor beide implementatiemodellen.</span><span class="sxs-lookup"><span data-stu-id="bf798-121">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="bf798-122">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="bf798-122">This article covers hello Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="bf798-123">Vereisten voor on-premises</span><span class="sxs-lookup"><span data-stu-id="bf798-123">On-premises prerequisites</span></span>
<span data-ttu-id="bf798-124">Dit is wat u nodig hebt in Hallo primaire en secundaire on-premises sites toodeploy van dit scenario:</span><span class="sxs-lookup"><span data-stu-id="bf798-124">Here's what you'll need in hello primary and secondary on-premises sites toodeploy this scenario:</span></span>

| <span data-ttu-id="bf798-125">**Vereisten**</span><span class="sxs-lookup"><span data-stu-id="bf798-125">**Prerequisites**</span></span> | <span data-ttu-id="bf798-126">**Details**</span><span class="sxs-lookup"><span data-stu-id="bf798-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="bf798-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="bf798-127">**VMM**</span></span> |<span data-ttu-id="bf798-128">Het is raadzaam om de implementatie van een VMM-beheerserver in Hallo primaire site en een VMM-server op Hallo secundaire site.</span><span class="sxs-lookup"><span data-stu-id="bf798-128">We recommend you deploy a VMM server in hello primary site and a VMM server in hello secondary site.</span></span><br/><br/> <span data-ttu-id="bf798-129">U kunt ook [repliceren tussen clouds op één VMM-server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span><span class="sxs-lookup"><span data-stu-id="bf798-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="bf798-130">toodo dit moet u ten minste twee clouds die zijn geconfigureerd op Hallo VMM-server.</span><span class="sxs-lookup"><span data-stu-id="bf798-130">toodo this you'll need at least two clouds configured on hello VMM server.</span></span><br/><br/> <span data-ttu-id="bf798-131">VMM-servers waarop ten minste System Center 2012 SP1 met de nieuwste updates Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf798-131">VMM servers should be running at least System Center 2012 SP1 with hello latest updates.</span></span><br/><br/> <span data-ttu-id="bf798-132">Elke VMM-server moet op een of meer clouds zijn geconfigureerd en alle clouds moeten Hallo Hyper-V capaciteitsprofiel instellen.</span><span class="sxs-lookup"><span data-stu-id="bf798-132">Each VMM server must have at one or more clouds configured and all clouds must have hello Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="bf798-133">Clouds moeten een of meer VMM-hostgroepen bevatten.</span><span class="sxs-lookup"><span data-stu-id="bf798-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="bf798-134">Meer informatie over het instellen van VMM-clouds in [configureren Hallo VMM fabric cloud](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), en [overzicht: privéclouds maken met System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf798-134">Learn more about setting up VMM clouds in [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="bf798-135">VMM-servers moeten toegang tot internet hebben.</span><span class="sxs-lookup"><span data-stu-id="bf798-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="bf798-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="bf798-136">**Hyper-V**</span></span> |<span data-ttu-id="bf798-137">Hyper-V-servers moeten ten minste draaien op Windows Server 2012 met Hallo Hyper-V-rol en hebben Hallo nieuwste updates zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="bf798-137">Hyper-V servers must be running at least Windows Server 2012 with hello Hyper-V role and have hello latest updates installed.</span></span><br/><br/> <span data-ttu-id="bf798-138">Een Hyper-V-server moet een of meer virtuele machines bevatten.</span><span class="sxs-lookup"><span data-stu-id="bf798-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="bf798-139">Hyper-V-hostservers moeten zich in hostgroepen in Hallo primaire en secundaire VMM-clouds.</span><span class="sxs-lookup"><span data-stu-id="bf798-139">Hyper-V host servers should be located in host groups in hello primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="bf798-140">Als u Hyper-V in een cluster op Windows Server 2012 R2 moet u eerst installeren [2961977 bijwerken](https://support.microsoft.com/kb/2961977)</span><span class="sxs-lookup"><span data-stu-id="bf798-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="bf798-141">Als u werkt met Hyper-V in een cluster op Windows Server 2012-opmerking die clusterbroker niet automatisch gemaakt als u een statische IP-adressen gebaseerde cluster hebt.</span><span class="sxs-lookup"><span data-stu-id="bf798-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="bf798-142">U moet tooconfigure hello clusterbroker handmatig.</span><span class="sxs-lookup"><span data-stu-id="bf798-142">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="bf798-143">[Lees meer](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf798-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="bf798-144">**Provider**</span><span class="sxs-lookup"><span data-stu-id="bf798-144">**Provider**</span></span> |<span data-ttu-id="bf798-145">Tijdens de implementatie van Site Recovery kunt u hello Azure Site Recovery Provider installeren op VMM-servers.</span><span class="sxs-lookup"><span data-stu-id="bf798-145">During Site Recovery deployment you install hello Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="bf798-146">Hallo Provider communiceert met Site Recovery via HTTPS 443 tooorchestrate replicatie.</span><span class="sxs-lookup"><span data-stu-id="bf798-146">hello Provider communicates with Site Recovery over HTTPS 443 tooorchestrate replication.</span></span> <span data-ttu-id="bf798-147">Gegevensreplicatie plaatsvindt tussen Hallo primaire en secundaire servers voor Hyper-V via LAN hello of een VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="bf798-147">Data replication occurs between hello primary and secondary Hyper-V servers over hello LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="bf798-148">Hallo Provider die op Hallo VMM-server wordt uitgevoerd moet toegang tot toothese URL's: *. hypervrecoverymanager.windowsazure.com; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. blob.core.windows.net; *. store.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="bf798-148">hello Provider running on hello VMM server needs access toothese URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="bf798-149">Bovendien toestaan firewall communicatie van Hallo VMM-servers toohello [Azure datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653) en Hallo HTTPS (443)-protocol toe te staan.</span><span class="sxs-lookup"><span data-stu-id="bf798-149">In addition allow firewall communication from hello VMM servers toohello [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow hello HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="bf798-150">Vereisten voor netwerktoewijzing</span><span class="sxs-lookup"><span data-stu-id="bf798-150">Network mapping prerequisites</span></span>
<span data-ttu-id="bf798-151">Koppelingen van Netwerktoewijzingen tussen VMM VM-netwerken op Hallo primaire en secundaire VMM-servers:</span><span class="sxs-lookup"><span data-stu-id="bf798-151">Network mapping maps between VMM VM networks on hello primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="bf798-152">Replica-VM optimaal op secundaire Hyper-V-hosts plaatsen na een failover.</span><span class="sxs-lookup"><span data-stu-id="bf798-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="bf798-153">Verbinding met het maken van replica VMs tooappropriate VM-netwerken.</span><span class="sxs-lookup"><span data-stu-id="bf798-153">Connect replica VMs tooappropriate VM networks.</span></span>
* <span data-ttu-id="bf798-154">Als u geen netwerk configureert toewijzing replica VMs niet verbonden tooany netwerk na een failover.</span><span class="sxs-lookup"><span data-stu-id="bf798-154">If you don't configure network mapping replica VMs won't be connected tooany network after failover.</span></span>
* <span data-ttu-id="bf798-155">Als u wilt dat tooset netwerk is toewijzen tijdens het siteherstel implementatie hier wat u nodig hebt:</span><span class="sxs-lookup"><span data-stu-id="bf798-155">If you want tooset up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="bf798-156">Zorg ervoor dat virtuele machines op Hallo bron Hyper-V-hostserver verbonden tooa VMM VM-netwerk.</span><span class="sxs-lookup"><span data-stu-id="bf798-156">Make sure that VMs on hello source Hyper-V host server are connected tooa VMM VM network.</span></span> <span data-ttu-id="bf798-157">Dit netwerk moet gekoppelde tooa logisch netwerk dat is gekoppeld aan Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="bf798-157">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
  * <span data-ttu-id="bf798-158">Controleer of Hallo secundaire cloud die u voor herstel heeft een bijbehorende VM-netwerk is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="bf798-158">Verify that hello secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="bf798-159">Deze VM-netwerk moet gekoppelde tooa logisch netwerk dat is gekoppeld aan Hallo secundaire cloud.</span><span class="sxs-lookup"><span data-stu-id="bf798-159">That VM network should be linked tooa logical network that's associated with hello secondary cloud.</span></span>

<span data-ttu-id="bf798-160">Meer informatie over het configureren van netwerken in VMM in Hallo hieronder artikelen</span><span class="sxs-lookup"><span data-stu-id="bf798-160">Learn more about configuring VMM networks in hello below articles</span></span>

* [<span data-ttu-id="bf798-161">Hoe tooconfigure logische netwerken in VMM</span><span class="sxs-lookup"><span data-stu-id="bf798-161">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="bf798-162">Hoe tooconfigure VM-netwerken en gateways in VMM</span><span class="sxs-lookup"><span data-stu-id="bf798-162">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="bf798-163">[Meer informatie](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) over hoe netwerktoewijzing werkt.</span><span class="sxs-lookup"><span data-stu-id="bf798-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="bf798-164">PowerShell-vereisten</span><span class="sxs-lookup"><span data-stu-id="bf798-164">PowerShell prerequisites</span></span>
<span data-ttu-id="bf798-165">Zorg ervoor dat u Azure PowerShell gereed toogo hebt.</span><span class="sxs-lookup"><span data-stu-id="bf798-165">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="bf798-166">Als u al van PowerShell gebruikmaakt, moet u tooupgrade tooversion 0.8.10 of hoger.</span><span class="sxs-lookup"><span data-stu-id="bf798-166">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="bf798-167">Zie voor informatie over het instellen van PowerShell Hallo [tooinstall te leiden en configureer Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="bf798-167">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="bf798-168">Zodra u hebt ingesteld en geconfigureerd PowerShell, kunt u alle beschikbare Hallo-cmdlets voor Hallo service weergeven [hier](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bf798-168">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="bf798-169">toolearn over tips waarmee u Hallo-cmdlets, zoals hoe parameterwaarden, in- en uitgangen doorgaans worden uitgevoerd in Azure PowerShell gebruiken kunt Zie Hallo [tooget slag met Azure-Cmdlets begeleiden](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="bf798-169">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="bf798-170">Stap 1: Stel Hallo-abonnement</span><span class="sxs-lookup"><span data-stu-id="bf798-170">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="bf798-171">Van Azure powershell, aanmelding tooyour Azure-account: met behulp van de volgende cmdlets Hallo</span><span class="sxs-lookup"><span data-stu-id="bf798-171">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="bf798-172">Een lijst van uw abonnementen ophalen.</span><span class="sxs-lookup"><span data-stu-id="bf798-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="bf798-173">Dit worden Hallo subscriptionIDs voor elk Hallo abonnementen vermeld.</span><span class="sxs-lookup"><span data-stu-id="bf798-173">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="bf798-174">Noteer Hallo abonnements-id van het Hallo-abonnement waarmee u toocreate Hallo recovery services-kluis wenst</span><span class="sxs-lookup"><span data-stu-id="bf798-174">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="bf798-175">Hallo-abonnement in welke Hallo recovery services-kluis gemaakt is door de vermelding Hallo abonnements-ID toobe instellen</span><span class="sxs-lookup"><span data-stu-id="bf798-175">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="bf798-176">Stap 2: Maak een Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="bf798-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="bf798-177">Een Azure Resource Manager-resourcegroep maken als u nog niet hebt</span><span class="sxs-lookup"><span data-stu-id="bf798-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="bf798-178">Een nieuwe Recovery Services-kluis maken en opslaan van Hallo ASR kluis object is gemaakt in een variabele (later worden gebruikt).</span><span class="sxs-lookup"><span data-stu-id="bf798-178">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="bf798-179">U kunt ook Hallo ASR kluis post maken van het object met de cmdlet Get-AzureRMRecoveryServicesVault Hallo ophalen:-</span><span class="sxs-lookup"><span data-stu-id="bf798-179">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="bf798-180">Stap 3: Hallo Recovery Services-kluis context instellen</span><span class="sxs-lookup"><span data-stu-id="bf798-180">Step 3: Set hello Recovery Services Vault context</span></span>
1. <span data-ttu-id="bf798-181">Als u een kluis hebt gemaakt hebt, uitgevoerd Hallo onderstaande opdracht tooget Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="bf798-181">If you have a vault already created, run hello below command tooget hello vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="bf798-182">Hallo kluis context instellen door te voeren Hallo onder opdracht.</span><span class="sxs-lookup"><span data-stu-id="bf798-182">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="bf798-183">Stap 4: Hello Azure Site Recovery Provider installeren</span><span class="sxs-lookup"><span data-stu-id="bf798-183">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="bf798-184">Maak een map door het uitvoeren van de volgende opdracht Hallo op Hallo-VMM-machine:</span><span class="sxs-lookup"><span data-stu-id="bf798-184">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="bf798-185">Hallo-bestanden met behulp van de provider Hallo gedownload door het uitvoeren van de volgende opdracht Hallo uitpakken</span><span class="sxs-lookup"><span data-stu-id="bf798-185">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="bf798-186">Hallo-provider met behulp van de volgende opdrachten Hallo installeren:</span><span class="sxs-lookup"><span data-stu-id="bf798-186">Install hello provider using hello following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="bf798-187">Wachten op Hallo installatie toofinish.</span><span class="sxs-lookup"><span data-stu-id="bf798-187">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="bf798-188">Hallo-server registreren in met behulp van de volgende opdracht Hallo Hallo-kluis:</span><span class="sxs-lookup"><span data-stu-id="bf798-188">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="bf798-189">Stap 5: Maken en koppelen van een beleid voor wachtwoordreplicatie</span><span class="sxs-lookup"><span data-stu-id="bf798-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="bf798-190">Maak een Hyper-V 2012 R2 replicatie-beleid door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="bf798-190">Create a Hyper-V 2012 R2 replication policy by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="bf798-191">Hallo VMM-cloud Hyper-V-hosts met verschillende versies van Windows Server (zoals vermeld in de Hyper-V-vereisten Hallo) kan bevatten, maar Hallo replicatiebeleid specifieke versie van het besturingssysteem is.</span><span class="sxs-lookup"><span data-stu-id="bf798-191">hello VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in hello Hyper-V prerequisites), but hello replication policy is OS version specific.</span></span> <span data-ttu-id="bf798-192">Als u andere hosts die worden uitgevoerd op verschillende besturingssysteemversies hebt, maakt u afzonderlijke replicatiegroepen beleid voor elk type van de versie van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="bf798-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="bf798-193">Voor bijvoorbeeld: als u vijf hosts die worden uitgevoerd op Windows-Servers 2012 en drie op Windows Server 2012 R2 hebt, maakt u twee replicatie beleidsregels: één voor elk type besturingssysteemversies.</span><span class="sxs-lookup"><span data-stu-id="bf798-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="bf798-194">Hallo primaire beveiligingscontainer (primaire VMM-Cloud) en herstel de beveiligingscontainer (herstelserver VMM-Cloud) door het uitvoeren van de volgende opdrachten Hallo ophalen:</span><span class="sxs-lookup"><span data-stu-id="bf798-194">Get hello primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running hello following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="bf798-195">Hallo-beleid die u hebt gemaakt in stap 1 ophalen Hallo beschrijvende naam van het Hallo-beleid</span><span class="sxs-lookup"><span data-stu-id="bf798-195">Retrieve hello policy you created in step 1 using hello friendly name of hello policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="bf798-196">Hallo koppeling van Hallo beveiligingscontainer (VMM-Cloud) beginnen met het replicatiebeleid Hallo:</span><span class="sxs-lookup"><span data-stu-id="bf798-196">Start hello association of hello protection container (VMM Cloud) with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="bf798-197">Wachten op Hallo beleid koppeling taak toocomplete.</span><span class="sxs-lookup"><span data-stu-id="bf798-197">Wait for hello policy association job toocomplete.</span></span> <span data-ttu-id="bf798-198">U kunt controleren als Hallo-taak is voltooid met behulp van de volgende PowerShell-codefragment Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf798-198">You can check if hello job has completed using hello following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="bf798-199">Nadat het Hallo taak zijn verwerkt, voert u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="bf798-199">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="bf798-200">Hallo-bewerking is toocheck Hallo voltooid Hallo stappen in [Monitoractiviteit](#monitor).</span><span class="sxs-lookup"><span data-stu-id="bf798-200">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="bf798-201">Stap 6: Netwerktoewijzing configureren</span><span class="sxs-lookup"><span data-stu-id="bf798-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="bf798-202">de eerste opdracht Hallo opgehaald servers voor de huidige Azure Site Recovery-kluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf798-202">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="bf798-203">Hallo opdracht slaat Hallo Microsoft Azure Site Recovery-servers in Hallo $Servers matrixvariabele.</span><span class="sxs-lookup"><span data-stu-id="bf798-203">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="bf798-204">Hallo hieronder opdrachten ophalen Hallo site recovery-netwerk voor Hallo bron-VMM-server en Hallo doel-VMM-server.</span><span class="sxs-lookup"><span data-stu-id="bf798-204">hello below commands get hello site recovery network for hello source VMM server and hello target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="bf798-205">Hallo bron-VMM-server kan worden Hallo eerste of tweede matrix van één in Hallo servers Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf798-205">hello source VMM server can be hello first one or hello second one in hello servers array.</span></span> <span data-ttu-id="bf798-206">Hallo-namen van Hallo VMM-servers controleren en Hallo netwerken op de juiste wijze ophalen</span><span class="sxs-lookup"><span data-stu-id="bf798-206">Check hello names of hello VMM servers and get hello networks appropriately</span></span>


1. <span data-ttu-id="bf798-207">Hallo laatste cmdlet een toewijzing gemaakt tussen het primaire netwerk Hallo en Hallo herstel.</span><span class="sxs-lookup"><span data-stu-id="bf798-207">hello final cmdlet creates a mapping between hello primary network and hello recovery network.</span></span> <span data-ttu-id="bf798-208">Hallo cmdlet geeft Hallo primaire netwerk als eerste element van $PrimaryNetworks en Hallo herstel netwerk als het eerste element van $RecoveryNetworks Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf798-208">hello cmdlet specifies hello primary network as hello first element of $PrimaryNetworks and hello recovery network as hello first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="bf798-209">Stap 7: De toewijzing van opslag configureren</span><span class="sxs-lookup"><span data-stu-id="bf798-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="bf798-210">Hallo onder opdracht ophalen Hallo lijst met opslagclassificaties in $storageclassifications-variabele.</span><span class="sxs-lookup"><span data-stu-id="bf798-210">hello below command gets hello list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="bf798-211">Hallo hieronder opdrachten Hallo bron classificatie in de variabele $SourceClassificaion en doel classificatie in $TargetClassification-variabele ophalen.</span><span class="sxs-lookup"><span data-stu-id="bf798-211">hello below commands get hello source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="bf798-212">Hallo-bron en doel classificaties kunnen elk element in Hallo matrix zijn.</span><span class="sxs-lookup"><span data-stu-id="bf798-212">hello source and target classifications can be any element in hello array.</span></span> <span data-ttu-id="bf798-213">Raadpleeg toohello uitvoer van Hallo onderstaande opdracht toofigure Hallo index van de bron en doel classificaties in $storageclassifications matrix.</span><span class="sxs-lookup"><span data-stu-id="bf798-213">Refer toohello output of hello below command toofigure hello index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="bf798-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object - eigenschap FriendlyName, Id | Tabel opmaken</span><span class="sxs-lookup"><span data-stu-id="bf798-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="bf798-215">Hallo hieronder cmdlet een toewijzing gemaakt tussen Hallo bron classificatie en Hallo doel classificatie.</span><span class="sxs-lookup"><span data-stu-id="bf798-215">hello below cmdlet creates a mapping between hello source classification and hello target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="bf798-216">Stap 8: Beveiliging voor virtuele machines inschakelen</span><span class="sxs-lookup"><span data-stu-id="bf798-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="bf798-217">Nadat het Hallo-servers, clouds en netwerken correct zijn geconfigureerd, kunt u beveiliging voor virtuele machines in de cloud Hallo inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bf798-217">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

1. <span data-ttu-id="bf798-218">tooenable beveiliging Hallo opdracht tooget hello beveiligingscontainer volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bf798-218">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="bf798-219">Hallo beveiligde entiteit (VM) door het uitvoeren van de volgende opdracht Hallo ophalen:</span><span class="sxs-lookup"><span data-stu-id="bf798-219">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="bf798-220">Replicatie inschakelen voor Hallo VM door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="bf798-220">Enable replication for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="bf798-221">Uw implementatie testen</span><span class="sxs-lookup"><span data-stu-id="bf798-221">Test your deployment</span></span>
<span data-ttu-id="bf798-222">tootest plannen voor uw implementatie kunt u een testfailover voor één virtuele machine uitvoeren of maken van een herstelplan dat bestaat uit meerdere virtuele machines en een testfailover voor Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bf798-222">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="bf798-223">Met een testfailover wordt uw failover- en herstelmechanisme in een geïsoleerd netwerk gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="bf798-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="bf798-224">U kunt een herstelplan maken voor uw toepassing in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="bf798-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="bf798-225">Hallo-bewerking is toocheck Hallo voltooid Hallo stappen in [Monitoractiviteit](#monitor).</span><span class="sxs-lookup"><span data-stu-id="bf798-225">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="bf798-226">Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="bf798-226">Run a test failover</span></span>
1. <span data-ttu-id="bf798-227">Hallo hieronder cmdlets tooget Hallo VM-netwerk toowhich die u uw virtuele machines naar tootest failover wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bf798-227">Run hello below cmdlets tooget hello VM network toowhich you want tootest failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="bf798-228">Voer een testfailover uitgevoerd van een virtuele machine door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="bf798-228">Perform a test failover of a VM by doing hello following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="bf798-229">Voer een testfailover uitgevoerd van een herstelplan door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="bf798-229">Perform a test failover of a recovery plan by doing hello following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="bf798-230">Een geplande failover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="bf798-230">Run a planned failover</span></span>
1. <span data-ttu-id="bf798-231">Voer een geplande failover van een virtuele machine door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="bf798-231">Perform a planned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="bf798-232">Voer een geplande failover van een herstelplan door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="bf798-232">Perform a planned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="bf798-233">Een niet-geplande failover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="bf798-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="bf798-234">Voer een niet-geplande failover van een virtuele machine door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="bf798-234">Perform an unplanned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="bf798-235">2. Voer een niet-geplande failover van een herstelplan door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="bf798-235">2.Perform an unplanned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="bf798-236"><a name=monitor></a>Voor Monitoractiviteit</span><span class="sxs-lookup"><span data-stu-id="bf798-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="bf798-237">Gebruik hello opdrachten toomonitor Hallo activiteit te volgen.</span><span class="sxs-lookup"><span data-stu-id="bf798-237">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="bf798-238">Houd er rekening mee dat u toowait Between-taken voor Hallo verwerking toofinish hebt.</span><span class="sxs-lookup"><span data-stu-id="bf798-238">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="bf798-239">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bf798-239">Next steps</span></span>
<span data-ttu-id="bf798-240">[Lees meer](/powershell/module/azurerm.recoveryservices.backup/#recovery) over Azure Site Recovery met Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="bf798-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>

---
title: Toepassingen (Azure-Azure) repliceren | Microsoft Docs
description: In dit artikel wordt beschreven hoe de replicatie van virtuele machines in een Azure-regio naar een andere regio in Azure instellen.
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: f9f97cf840b722c8cfee169dd1640e0682f287ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-virtual-machines-to-another-azure-region"></a><span data-ttu-id="72e32-103">Azure virtuele machines repliceren naar een andere Azure-regio</span><span class="sxs-lookup"><span data-stu-id="72e32-103">Replicate Azure virtual machines to another Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="72e32-104">Site Recovery replicatie voor virtuele machines in Azure is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="72e32-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="72e32-105">In dit artikel wordt beschreven hoe de replicatie van virtuele machines in een Azure-regio naar een andere Azure-regio instellen.</span><span class="sxs-lookup"><span data-stu-id="72e32-105">This article describes how to set up replication of virtual machines running in one Azure region to another Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72e32-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="72e32-106">Prerequisites</span></span>

* <span data-ttu-id="72e32-107">Het artikel wordt ervan uitgegaan dat u al over de Site Recovery en de Recovery Services-kluis weet.</span><span class="sxs-lookup"><span data-stu-id="72e32-107">The article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="72e32-108">U moet een 'Recovery services-kluis' vooraf gemaakt hebben.</span><span class="sxs-lookup"><span data-stu-id="72e32-108">You need to have a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="72e32-109">Het verdient aanbeveling dat u de 'Recovery services-kluis' op de locatie waar u uw virtuele machines maken worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="72e32-109">It is recommended that you create the 'Recovery services vault' in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="72e32-110">Als uw doellocatie 'VS-midden', bijvoorbeeld kluis in 'VS-midden' maken.</span><span class="sxs-lookup"><span data-stu-id="72e32-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="72e32-111">Als u regels van de Netwerkbeveiligingsgroep groepen (NSG) of firewall-proxy gebruikt toegang tot uitgaande internetverbinding op de Azure VM's, zorg ervoor dat u goedgekeurde IP-adressen de vereiste URL's of IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="72e32-111">If you are using Network Security Groups (NSG) rules or firewall proxy to control access to outbound internet connectivity on the Azure VMs, ensure that you whitelist the required URLs or IPs.</span></span> <span data-ttu-id="72e32-112">Raadpleeg [leidraad voor netwerken](./site-recovery-azure-to-azure-networking-guidance.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="72e32-112">Refer to [Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="72e32-113">Als u een ExpressRoute- of een VPN-verbinding tussen on-premises en de bronlocatie in Azure hebt, voert u de [Site Recovery-overwegingen voor Azure voor de lokale ExpressRoute / VPN-configuratie](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span><span class="sxs-lookup"><span data-stu-id="72e32-113">If you have an ExpressRoute or a VPN connection between on-premises and the source location in Azure, follow [Site Recovery Considerations for Azure to on-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="72e32-114">Uw Azure gebruikersaccount moet zijn bepaalde [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) replicatie van Azure een virtuele machine in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="72e32-114">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="72e32-115">Uw Azure-abonnement moet worden ingeschakeld voor het maken van virtuele machines in de doellocatie die u wilt gebruiken als DR regio.</span><span class="sxs-lookup"><span data-stu-id="72e32-115">Your Azure subscription should be enabled to create VMs in the target location you want to use as DR region.</span></span> <span data-ttu-id="72e32-116">Neem contact op met ondersteuning om in te schakelen van de quota voor vereist.</span><span class="sxs-lookup"><span data-stu-id="72e32-116">You can contact support to enable the required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="72e32-117">Schakel replicatie van Azure Site Recovery-kluis</span><span class="sxs-lookup"><span data-stu-id="72e32-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="72e32-118">Virtuele we voor deze afbeelding wordt uitgevoerd in de Oost-Azië-machines repliceren naar de locatie, Zuidoost-Azië ' Azure-locatie.</span><span class="sxs-lookup"><span data-stu-id="72e32-118">For this illustration, we will replicate VMs running  in the ‘East Asia’ Azure location to the ‘South East Asia’ location.</span></span> <span data-ttu-id="72e32-119">De stappen zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="72e32-119">The steps are as follows:</span></span>

 <span data-ttu-id="72e32-120">Klik op **+ repliceren** in de kluis replicatie voor de virtuele machines in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="72e32-120">Click **+Replicate** in the vault to enable replication for the virtual machines.</span></span>

1. <span data-ttu-id="72e32-121">**Bron:** deze verwijst naar het punt van oorsprong van de machines die in dit geval **Azure**.</span><span class="sxs-lookup"><span data-stu-id="72e32-121">**Source:** It refers to the point of origin of the machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="72e32-122">**Bronlocatie:** is de Azure-regio waar u wilt beveiligen van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="72e32-122">**Source location:** It is the Azure region from where you want to protect your virtual machines.</span></span> <span data-ttu-id="72e32-123">In dit voorbeeld worden de bronlocatie Oost-Azië</span><span class="sxs-lookup"><span data-stu-id="72e32-123">For this illustration, the source location will be 'East Asia'</span></span>

3. <span data-ttu-id="72e32-124">**Implementatiemodel:** het verwijst naar het model van de Azure-implementatie van de bronmachine.</span><span class="sxs-lookup"><span data-stu-id="72e32-124">**Deployment model:** It refers to the Azure deployment model of the source machines.</span></span> <span data-ttu-id="72e32-125">U kunt ofwel classic selecteren of resourcemanager en de machines die horen bij het specifieke model wordt weergegeven voor beveiliging in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="72e32-125">You can select either classic or resource manager and machines belonging to the specific model will be listed for protection in the next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="72e32-126">U kunt alleen een klassieke virtuele machine repliceren en deze herstellen als een klassieke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="72e32-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="72e32-127">U kunt deze niet herstellen als de virtuele machine van een Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="72e32-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="72e32-128">**Resourcegroep:** is de resourcegroep waartoe uw virtuele bronmachines behoren.</span><span class="sxs-lookup"><span data-stu-id="72e32-128">**Resource Group:** It’s the resource group to which your source virtual machines belong.</span></span> <span data-ttu-id="72e32-129">Alle VM's onder de geselecteerde resourcegroep wordt vermeld voor beveiliging in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="72e32-129">All the VMs under the selected resource group will be listed for protection in the next step.</span></span>

    ![Replicatie inschakelen](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="72e32-131">In **virtuele Machines > Selecteer de virtuele machines**en op elke machine die u wilt repliceren.</span><span class="sxs-lookup"><span data-stu-id="72e32-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="72e32-132">U kunt alleen machines selecteren waarvoor replicatie kan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="72e32-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="72e32-133">Klik vervolgens op OK.</span><span class="sxs-lookup"><span data-stu-id="72e32-133">Then click OK.</span></span>
    <span data-ttu-id="72e32-134">![Replicatie inschakelen](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="72e32-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="72e32-135">Onder de sectie instellingen kunt u doel voor site-eigenschappen configureren</span><span class="sxs-lookup"><span data-stu-id="72e32-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="72e32-136">**Doellocatie:** dit is de locatie waar de brongegevens van de virtuele machine wordt gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="72e32-136">**Target Location:**  This is the location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="72e32-137">Afhankelijk van uw locatie voor geselecteerde machines, biedt Site Recovery u de lijst met doelregio geschikt is.</span><span class="sxs-lookup"><span data-stu-id="72e32-137">Depending upon your selected machines location, Site Recovery will provide you the list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="72e32-138">Het verdient aanbeveling dat doellocatie dezelfde vanaf uw recovery services-kluis.</span><span class="sxs-lookup"><span data-stu-id="72e32-138">It is recommended to keep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="72e32-139">**Doelresourcegroep:** is de resourcegroep waarin alle uw gerepliceerde virtuele machines behoort. Standaard maakt ASR een nieuwe resourcegroep in de doelregio met naam 'asr' achtervoegsel heeft.</span><span class="sxs-lookup"><span data-stu-id="72e32-139">**Target resource group :** It is the resource group to which all your replicated virtual machines will belong.By default ASR will create a new resource group in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="72e32-140">Als de resourcegroep die zijn gemaakt door ASR al bestaat, wordt opnieuw gebruikt. U kunt ook aanpassen zoals weergegeven in de onderstaande sectie.</span><span class="sxs-lookup"><span data-stu-id="72e32-140">In case resource group created by ASR already exist, it will be reused.You can also choose to customize it as shown in the section below.</span></span>    
3. <span data-ttu-id="72e32-141">**Virtuele doelnetwerk:** standaard ASR maakt een nieuw virtueel netwerk in de doelregio met naam 'asr' achtervoegsel heeft.</span><span class="sxs-lookup"><span data-stu-id="72e32-141">**Target Virtual Network:** By default, ASR will create a new virtual network in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="72e32-142">Dit worden toegewezen aan de bron-netwerk en wordt gebruikt voor alle toekomstige beveiliging.</span><span class="sxs-lookup"><span data-stu-id="72e32-142">This will be mapped to your source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="72e32-143">[Controleer de gegevens van de netwerken](site-recovery-network-mapping-azure-to-azure.md) voor meer informatie over de netwerktoewijzing.</span><span class="sxs-lookup"><span data-stu-id="72e32-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) to know more about network mapping.</span></span>

4. <span data-ttu-id="72e32-144">**Storage-accounts als doel:** standaard ASR maakt de nieuwe doelaccount opslag mimicking de opslagconfiguratie van de bron-VM.</span><span class="sxs-lookup"><span data-stu-id="72e32-144">**Target Storage accounts:** By default, ASR will create the new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="72e32-145">Als storage-account gemaakt door ASR al bestaat, wordt opnieuw gebruikt.</span><span class="sxs-lookup"><span data-stu-id="72e32-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="72e32-146">**Storage-accounts in de cache:** ASR moet extra opslagruimte account met de naam van cache-opslag in de regio van de bron.</span><span class="sxs-lookup"><span data-stu-id="72e32-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in the source region.</span></span> <span data-ttu-id="72e32-147">Alle wijzigingen die plaatsvinden op de bron-VM's worden bijgehouden en verzonden naar de cache storage-account voordat deze naar de doellocatie te repliceren.</span><span class="sxs-lookup"><span data-stu-id="72e32-147">All the changes happening on the source VMs are tracked and sent to cache storage account before replicating those to the target location.</span></span>

6. <span data-ttu-id="72e32-148">**Beschikbaarheidsset:** ASR maakt standaard een nieuwe beschikbaarheidsset voor de doelregio met naam 'asr' achtervoegsel heeft.</span><span class="sxs-lookup"><span data-stu-id="72e32-148">**Availability set :** By default, ASR will create a new availability set in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="72e32-149">Als beschikbaarheidsset gemaakt door ASR al bestaat, wordt opnieuw gebruikt.</span><span class="sxs-lookup"><span data-stu-id="72e32-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="72e32-150">**Beleid voor wachtwoordreplicatie:** definieert de instellingen voor herstelpunt bewaren geschiedenis en app consistent de frequentie van momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="72e32-150">**Replication Policy:** It defines the settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="72e32-151">Standaard maakt ASR een nieuw replicatiebeleid voor met de standaardinstellingen van 24 uur voor herstel bewaarperiode en "60 minuten voor de frequentie van app-consistente momentopname te maken.</span><span class="sxs-lookup"><span data-stu-id="72e32-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![Replicatie inschakelen](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="72e32-153">Doelresources aanpassen</span><span class="sxs-lookup"><span data-stu-id="72e32-153">Customize target resources</span></span>

<span data-ttu-id="72e32-154">Als u de standaardwaarden die worden gebruikt door ASR hebt gewijzigd wilt, kunt u de instellingen op basis van uw behoeften kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="72e32-154">In case you want to change the defaults used by ASR, you can change the settings based on your needs.</span></span>

1. <span data-ttu-id="72e32-155">**Aanpassen:** Klik hierop om te wijzigen van de standaardwaarden die worden gebruikt door ASR.</span><span class="sxs-lookup"><span data-stu-id="72e32-155">**Customize:** Click it to change the defaults used by ASR.</span></span>

2. <span data-ttu-id="72e32-156">**Doelresourcegroep:** kunt u de resourcegroep uit de lijst met alle resourcegroepen die aanwezig is in de doellocatie in het abonnement.</span><span class="sxs-lookup"><span data-stu-id="72e32-156">**Target resource group :**  You can select the resource group from the list of all the resource groups existing in the target location within the subscription.</span></span>

3. <span data-ttu-id="72e32-157">**Virtuele doelnetwerk:** vindt u de lijst van het virtuele netwerk in de doellocatie.</span><span class="sxs-lookup"><span data-stu-id="72e32-157">**Target Virtual Network:** You can find the list of all the virtual network in the target location.</span></span>

4. <span data-ttu-id="72e32-158">**Beschikbaarheidsset:** u kunt alleen instellingen voor beschikbaarheid sets toevoegen aan de virtuele machines die deel van de beschikbaarheid in regio van de bron uitmaken.</span><span class="sxs-lookup"><span data-stu-id="72e32-158">**Availability set :** You can only add availability sets settings to the virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="72e32-159">**Doel Storage-accounts:**</span><span class="sxs-lookup"><span data-stu-id="72e32-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="72e32-160">![Replicatie inschakelen](./media/site-recovery-replicate-azure-to-azure/customize.PNG) klikt u op **doelbron maken** en replicatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="72e32-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="72e32-161">Wanneer virtuele machines zijn beveiligd kunt u de status van de status van de virtuele machines onder controleren **gerepliceerde items**</span><span class="sxs-lookup"><span data-stu-id="72e32-161">Once virtual machines are protected you can check the status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="72e32-162">Kan tijdens de periode van de initiële replicatie er een kans dat status kost tijd om te vernieuwen en er geen uitgevoerd gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="72e32-162">During the time of initial replication there could a possibility that status takes time to refresh and you don't see progress for some time.</span></span> <span data-ttu-id="72e32-163">U kunt klikken op de knop Vernieuwen boven aan de blade om op te halen van de meest recente status.</span><span class="sxs-lookup"><span data-stu-id="72e32-163">You can click the Refresh button on the top of the blade to get the latest status.</span></span>
>

![Replicatie inschakelen](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="72e32-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="72e32-165">Next steps</span></span>
- <span data-ttu-id="72e32-166">[Meer informatie](site-recovery-test-failover-to-azure.md) over het uitvoeren van een testfailover.</span><span class="sxs-lookup"><span data-stu-id="72e32-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="72e32-167">[Meer informatie](site-recovery-failover.md) over verschillende soorten failovers en hoe ze uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="72e32-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how to run them.</span></span>
- <span data-ttu-id="72e32-168">Meer informatie over [met herstelplannen](site-recovery-create-recovery-plans.md) te verminderen RTO.</span><span class="sxs-lookup"><span data-stu-id="72e32-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) to reduce RTO.</span></span>
- <span data-ttu-id="72e32-169">Meer informatie over [andere virtuele Azure-machines](site-recovery-how-to-reprotect.md) na een failover.</span><span class="sxs-lookup"><span data-stu-id="72e32-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>

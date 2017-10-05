---
title: Plannen van capaciteit en de schaalbaarheid van de machine van Hyper-V-replicatie (zonder VMM) naar Azure met Azure Site Recovery | Microsoft Docs
description: Dit artikel voor plan capaciteit en de schaal gebruiken als Hyper-V-machines repliceren naar Azure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8687af60-5b50-481c-98ee-0750cbbc2c57
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: c7891c188c2cecbbf056fa79672a13bb16fa7fcf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-to-azure-replication"></a><span data-ttu-id="65f9e-103">Stap 3: Plannen van capaciteit en schalen voor Hyper-V naar Azure replicatie</span><span class="sxs-lookup"><span data-stu-id="65f9e-103">Step 3: Plan capacity and scaling for Hyper-V to Azure replication</span></span>

<span data-ttu-id="65f9e-104">In dit artikel gebruiken om te achterhalen plannen van capaciteit en de schaling bij het lokale Hyper-V-machines (zonder de System Center VMM) repliceren naar Azure met [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65f9e-104">Use this article to figure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs (without System Center VMM) to Azure with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="65f9e-105">Na het lezen van dit artikel, eventuele opmerkingen posten onder of technische vragen op de [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="65f9e-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="65f9e-106">Hoe start capaciteitsplanning?</span><span class="sxs-lookup"><span data-stu-id="65f9e-106">How do I start capacity planning?</span></span>


<span data-ttu-id="65f9e-107">U informatie verzamelen over uw replicatieomgeving, en vervolgens plannen van capaciteit met behulp van deze informatie, samen met de overwegingen gemarkeerd in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="65f9e-107">You gather information about your replication environment, and then plan capacity using this information, together with the considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="65f9e-108">Informatie verzamelen</span><span class="sxs-lookup"><span data-stu-id="65f9e-108">Gather information</span></span>

1. <span data-ttu-id="65f9e-109">Informatie verzamelen over uw replicatieomgeving, waaronder informatie over de virtuele machines, het aantal schijven per virtuele machine en de opslag per schijf.</span><span class="sxs-lookup"><span data-stu-id="65f9e-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="65f9e-110">De snelheid van uw dagelijkse wijzigen (verloop) voor gerepliceerde gegevens identificeren.</span><span class="sxs-lookup"><span data-stu-id="65f9e-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="65f9e-111">Download de [Hyper-V-hulpprogramma voor capaciteitsplanning](https://www.microsoft.com/download/details.aspx?id=39057) de wijzigingssnelheid ophalen.</span><span class="sxs-lookup"><span data-stu-id="65f9e-111">Download the [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) to get the change rate.</span></span> <span data-ttu-id="65f9e-112">U wordt aangeraden dat u dit hulpprogramma uitvoeren via een week om vast te leggen gemiddelden.</span><span class="sxs-lookup"><span data-stu-id="65f9e-112">We recommend you run this tool over a week to capture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="65f9e-113">Capaciteit te achterhalen</span><span class="sxs-lookup"><span data-stu-id="65f9e-113">Figure out capacity</span></span>

<span data-ttu-id="65f9e-114">Op basis van de informatie verzamelen die u hebt, voer de [Site Recovery-Capaciteitsplanner](http://aka.ms/asr-capacity-planner-excel) schatten bandbreedte behoeften en serverbronnen voor de bronlocatie en de resources (virtuele machines en opslag, enzovoort), die u nodig hebt in de doellocatie voor het analyseren van uw bronomgeving en werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="65f9e-114">Based on the information you've gather, you run the [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) to analyze your source environment and workloads, estimate bandwidth needs and server resources for the source location, and the resources (virtual machines and storage etc), that you need in the target location.</span></span> <span data-ttu-id="65f9e-115">U kunt het hulpprogramma uitvoeren in een aantal modi:</span><span class="sxs-lookup"><span data-stu-id="65f9e-115">You can run the tool in a couple of modes:</span></span>

- <span data-ttu-id="65f9e-116">Snelle planning: Voer het hulpprogramma in deze modus netwerk- en projecties ophalen op basis van een gemiddelde aantal virtuele machines, schijven, opslag en wijzigingssnelheid.</span><span class="sxs-lookup"><span data-stu-id="65f9e-116">Quick planning: Run the tool in this mode to get network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="65f9e-117">Detail te plannen: het hulpprogramma uitvoeren in deze modus en Geef details op van elke werkbelasting op het niveau van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="65f9e-117">Detailed planning: Run the tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="65f9e-118">VM-compatibiliteit analyseren en netwerk- en projecties ophalen.</span><span class="sxs-lookup"><span data-stu-id="65f9e-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="65f9e-119">Nu u het hulpprogramma uitvoert:</span><span class="sxs-lookup"><span data-stu-id="65f9e-119">Now run the tool:</span></span>

1. <span data-ttu-id="65f9e-120">Download de [hulpprogramma](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="65f9e-120">Download the [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="65f9e-121">Ga als volgt de snelle planner voeren, [deze instructies](site-recovery-capacity-planner.md#run-the-quick-planner), en selecteert u het scenario **Hyper-V naar Azure**.</span><span class="sxs-lookup"><span data-stu-id="65f9e-121">To run the quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select the scenario **Hyper-V to Azure**.</span></span>
3. <span data-ttu-id="65f9e-122">Ga als volgt de gedetailleerde planner voeren, [deze instructies](site-recovery-capacity-planner.md#run-the-detailed-planner), en selecteert u het scenario **Hyper-V naar Azure**.</span><span class="sxs-lookup"><span data-stu-id="65f9e-122">To run the detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select the scenario **Hyper-V to Azure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="65f9e-123">Netwerkbandbreedte</span><span class="sxs-lookup"><span data-stu-id="65f9e-123">Control network bandwidth</span></span>

<span data-ttu-id="65f9e-124">Nadat u de bandbreedte die u nodig hebt berekend, hebt u een aantal opties voor het beheren van de hoeveelheid bandbreedte die wordt gebruikt voor replicatie:</span><span class="sxs-lookup"><span data-stu-id="65f9e-124">After you've calculated the bandwidth you need, you have a couple of options for controlling the amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="65f9e-125">**Bandbreedte beperken**: Hyper-V-verkeer dat wordt gerepliceerd naar Azure verloopt via een specifieke Hyper-V-host.</span><span class="sxs-lookup"><span data-stu-id="65f9e-125">**Throttle bandwidth**: Hyper-V traffic that replicates to Azure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="65f9e-126">U kunt de bandbreedte op de hostserver beperken.</span><span class="sxs-lookup"><span data-stu-id="65f9e-126">You can throttle bandwidth on the host server.</span></span>
* <span data-ttu-id="65f9e-127">**Netwerkbandbreedte beïnvloeden**: U kunt de bandbreedte die wordt gebruikt voor replicatie via diverse registersleutels beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="65f9e-127">**Influence bandwidth**: You can influence the bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="65f9e-128">Bandbreedte beperken</span><span class="sxs-lookup"><span data-stu-id="65f9e-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="65f9e-129">Open de Microsoft Azure Backup MMC-module op de Hyper-V-hostserver.</span><span class="sxs-lookup"><span data-stu-id="65f9e-129">Open the Microsoft Azure Backup MMC snap-in on the Hyper-V host server.</span></span> <span data-ttu-id="65f9e-130">Standaard is er een snelkoppeling naar Microsoft Azure Backup beschikbaar op het bureaublad of in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="65f9e-130">By default a shortcut for Microsoft Azure Backup is available on the desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="65f9e-131">Klik in de module op **Eigenschappen wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="65f9e-131">In the snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="65f9e-132">Selecteer op het tabblad **Beperken** de optie **Internetbandbreedtebeperking inschakelen voor back-upbewerkingen** en stel de limieten in voor werktijden en voor tijden waarop niet wordt gewerkt.</span><span class="sxs-lookup"><span data-stu-id="65f9e-132">On the **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set the limits for work and non-work hours.</span></span> <span data-ttu-id="65f9e-133">Het geldige bereik ligt tussen 512 Kbps en 102 Mbps.</span><span class="sxs-lookup"><span data-stu-id="65f9e-133">Valid ranges are from 512 Kbps to 102 Mbps per second.</span></span>

    ![Bandbreedte beperken](./media/hyper-v-site-walkthrough-capacity/throttle2.png)

<span data-ttu-id="65f9e-135">U kunt ook de cmdlet [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) gebruiken om een beperking in te stellen.</span><span class="sxs-lookup"><span data-stu-id="65f9e-135">You can also use the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet to set throttling.</span></span> <span data-ttu-id="65f9e-136">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="65f9e-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="65f9e-137">**Set-OBMachineSetting -NoThrottle** geeft aan dat er geen beperking is vereist.</span><span class="sxs-lookup"><span data-stu-id="65f9e-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="65f9e-138">Netwerkbandbreedte beïnvloeden</span><span class="sxs-lookup"><span data-stu-id="65f9e-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="65f9e-139">Navigeer in het register naar **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span><span class="sxs-lookup"><span data-stu-id="65f9e-139">In the registry navigate to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="65f9e-140">Wijzig de waarde ter bepaling van de bandbreedte-verkeer op de replicerende schijf, de **UploadThreadsPerVM**, of maak de sleutel als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="65f9e-140">To influence the bandwidth traffic on a replicating disk, modify the value the **UploadThreadsPerVM**, or create the key if it doesn't exist.</span></span>
   * <span data-ttu-id="65f9e-141">Wijzig de waarde ter bepaling van de bandbreedte voor failbackverkeer vanuit Azure **DownloadThreadsPerVM**.</span><span class="sxs-lookup"><span data-stu-id="65f9e-141">To influence the bandwidth for failback traffic from Azure, modify the value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="65f9e-142">De standaardwaarde is 4.</span><span class="sxs-lookup"><span data-stu-id="65f9e-142">The default value is 4.</span></span> <span data-ttu-id="65f9e-143">In netwerken met overprovisioning moeten deze registersleutels zodanig worden gewijzigd dat niet de standaardwaarden worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="65f9e-143">In an “overprovisioned” network, these registry keys should be changed from the default values.</span></span> <span data-ttu-id="65f9e-144">Het maximum is 32.</span><span class="sxs-lookup"><span data-stu-id="65f9e-144">The maximum is 32.</span></span> <span data-ttu-id="65f9e-145">Houd het verkeer in de gaten om de waarde te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="65f9e-145">Monitor traffic to optimize the value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65f9e-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="65f9e-146">Next steps</span></span>

<span data-ttu-id="65f9e-147">Ga naar [stap 4: Plan netwerken](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="65f9e-147">Go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>

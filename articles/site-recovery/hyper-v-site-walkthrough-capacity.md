---
title: aaaPlan capaciteit en schaal voor de virtuele machine van Hyper-V-replicatie (zonder VMM) tooAzure met Azure Site Recovery | Microsoft Docs
description: Dit artikel tooplan capaciteit en de schaal gebruiken bij het repliceren van Hyper-V-machines tooAzure met Azure Site Recovery
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
ms.openlocfilehash: f5b029f273e51c01c7d918d176832f6d1735b5f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-tooazure-replication"></a><span data-ttu-id="c33d4-103">Stap 3: Plannen van capaciteit en schalen voor Hyper-V tooAzure-replicatie</span><span class="sxs-lookup"><span data-stu-id="c33d4-103">Step 3: Plan capacity and scaling for Hyper-V tooAzure replication</span></span>

<span data-ttu-id="c33d4-104">Gebruik dit artikel toofigure uit het plannen van capaciteit en de schaling bij het repliceren van lokale Hyper-V-machines (zonder de System Center VMM) tooAzure met [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c33d4-104">Use this article toofigure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs (without System Center VMM) tooAzure with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="c33d4-105">Na het lezen van dit artikel, eventuele opmerkingen posten Hallo onderin of technische vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c33d4-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="c33d4-106">Hoe start capaciteitsplanning?</span><span class="sxs-lookup"><span data-stu-id="c33d4-106">How do I start capacity planning?</span></span>


<span data-ttu-id="c33d4-107">U informatie verzamelen over uw replicatieomgeving, en vervolgens plannen van capaciteit met behulp van deze informatie, samen met de Hallo overwegingen gemarkeerd in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c33d4-107">You gather information about your replication environment, and then plan capacity using this information, together with hello considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="c33d4-108">Informatie verzamelen</span><span class="sxs-lookup"><span data-stu-id="c33d4-108">Gather information</span></span>

1. <span data-ttu-id="c33d4-109">Informatie verzamelen over uw replicatieomgeving, waaronder informatie over de virtuele machines, het aantal schijven per virtuele machine en de opslag per schijf.</span><span class="sxs-lookup"><span data-stu-id="c33d4-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="c33d4-110">De snelheid van uw dagelijkse wijzigen (verloop) voor gerepliceerde gegevens identificeren.</span><span class="sxs-lookup"><span data-stu-id="c33d4-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="c33d4-111">Hallo downloaden [Hyper-V-hulpprogramma voor capaciteitsplanning](https://www.microsoft.com/download/details.aspx?id=39057) tooget Hallo wijzigingssnelheid.</span><span class="sxs-lookup"><span data-stu-id="c33d4-111">Download hello [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello change rate.</span></span> <span data-ttu-id="c33d4-112">U wordt aangeraden dat u gemiddelden dit hulpprogramma via een week toocapture uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c33d4-112">We recommend you run this tool over a week toocapture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="c33d4-113">Capaciteit te achterhalen</span><span class="sxs-lookup"><span data-stu-id="c33d4-113">Figure out capacity</span></span>

<span data-ttu-id="c33d4-114">Op basis van Hallo verzamelen die u hebt, Voer Hallo [Site Recovery-Capaciteitsplanner](http://aka.ms/asr-capacity-planner-excel) tooanalyze uw bronomgeving en werkbelastingen, schatting van de behoeften van de bandbreedte en serverbronnen voor Hallo bronlocatie en Hallo resources (virtuele machines en opslag, enzovoort), die u nodig hebt in Hallo target-locatie.</span><span class="sxs-lookup"><span data-stu-id="c33d4-114">Based on hello information you've gather, you run hello [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) tooanalyze your source environment and workloads, estimate bandwidth needs and server resources for hello source location, and hello resources (virtual machines and storage etc), that you need in hello target location.</span></span> <span data-ttu-id="c33d4-115">U kunt Hallo hulpprogramma uitvoeren in een aantal modi:</span><span class="sxs-lookup"><span data-stu-id="c33d4-115">You can run hello tool in a couple of modes:</span></span>

- <span data-ttu-id="c33d4-116">Snelle planning: Hallo hulpprogramma uitvoeren in deze modus tooget netwerk- en projecties op basis van een gemiddelde aantal virtuele machines, schijven, opslag en wijzigingssnelheid.</span><span class="sxs-lookup"><span data-stu-id="c33d4-116">Quick planning: Run hello tool in this mode tooget network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="c33d4-117">Detail te plannen: Hallo hulpprogramma uitvoeren in deze modus en Geef details op van elke werkbelasting op het niveau van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c33d4-117">Detailed planning: Run hello tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="c33d4-118">VM-compatibiliteit analyseren en netwerk- en projecties ophalen.</span><span class="sxs-lookup"><span data-stu-id="c33d4-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="c33d4-119">Hallo hulpprogramma nu uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c33d4-119">Now run hello tool:</span></span>

1. <span data-ttu-id="c33d4-120">Hallo downloaden [hulpprogramma](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="c33d4-120">Download hello [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="c33d4-121">snelle planner toorun hello, volg [deze instructies](site-recovery-capacity-planner.md#run-the-quick-planner), en selecteer Hallo scenario **Hyper-V tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="c33d4-121">toorun hello quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>
3. <span data-ttu-id="c33d4-122">toorun gedetailleerde planner hello, voert u de [deze instructies](site-recovery-capacity-planner.md#run-the-detailed-planner), en selecteer Hallo scenario **Hyper-V tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="c33d4-122">toorun hello detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="c33d4-123">Netwerkbandbreedte</span><span class="sxs-lookup"><span data-stu-id="c33d4-123">Control network bandwidth</span></span>

<span data-ttu-id="c33d4-124">Nadat u de berekende Hallo bandbreedte die u nodig hebt, hebt u een aantal opties voor het beheren Hallo hoeveelheid bandbreedte die wordt gebruikt voor replicatie:</span><span class="sxs-lookup"><span data-stu-id="c33d4-124">After you've calculated hello bandwidth you need, you have a couple of options for controlling hello amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="c33d4-125">**Bandbreedte beperken**: Hyper-V-verkeer dat wordt gerepliceerd tooAzure verloopt via een specifieke Hyper-V-host.</span><span class="sxs-lookup"><span data-stu-id="c33d4-125">**Throttle bandwidth**: Hyper-V traffic that replicates tooAzure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="c33d4-126">U kunt de bandbreedte op Hallo hostserver beperken.</span><span class="sxs-lookup"><span data-stu-id="c33d4-126">You can throttle bandwidth on hello host server.</span></span>
* <span data-ttu-id="c33d4-127">**Netwerkbandbreedte beïnvloeden**: U kunt zelf bepalen hoeveel Hallo-bandbreedte die wordt gebruikt voor replicatie via diverse registersleutels.</span><span class="sxs-lookup"><span data-stu-id="c33d4-127">**Influence bandwidth**: You can influence hello bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="c33d4-128">Bandbreedte beperken</span><span class="sxs-lookup"><span data-stu-id="c33d4-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="c33d4-129">Hallo Microsoft Azure Backup MMC-module openen op Hallo Hyper-V-hostserver.</span><span class="sxs-lookup"><span data-stu-id="c33d4-129">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host server.</span></span> <span data-ttu-id="c33d4-130">Een snelkoppeling naar Microsoft Azure Backup is standaard beschikbaar zijn op Hallo bureaublad of in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="c33d4-130">By default a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="c33d4-131">Klik in de module Hallo **eigenschappen wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="c33d4-131">In hello snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="c33d4-132">Op Hallo **bandbreedtebeperking** tabblad Selecteer **inschakelen voor gebruik van internetbandbreedte voor back-upbewerkingen**, en Hallo limieten instellen voor werk en niet-werk uren.</span><span class="sxs-lookup"><span data-stu-id="c33d4-132">On hello **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set hello limits for work and non-work hours.</span></span> <span data-ttu-id="c33d4-133">Geldige bereiken zijn afkomstig van 512 Kbps too102 Mbps per seconde.</span><span class="sxs-lookup"><span data-stu-id="c33d4-133">Valid ranges are from 512 Kbps too102 Mbps per second.</span></span>

    ![Bandbreedte beperken](./media/hyper-v-site-walkthrough-capacity/throttle2.png)

<span data-ttu-id="c33d4-135">U kunt ook Hallo [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset beperking.</span><span class="sxs-lookup"><span data-stu-id="c33d4-135">You can also use hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset throttling.</span></span> <span data-ttu-id="c33d4-136">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c33d4-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="c33d4-137">**Set-OBMachineSetting -NoThrottle** geeft aan dat er geen beperking is vereist.</span><span class="sxs-lookup"><span data-stu-id="c33d4-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="c33d4-138">Netwerkbandbreedte beïnvloeden</span><span class="sxs-lookup"><span data-stu-id="c33d4-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="c33d4-139">Navigeer te in Hallo register**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span><span class="sxs-lookup"><span data-stu-id="c33d4-139">In hello registry navigate too**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="c33d4-140">tooinfluence hello bandbreedte netwerkverkeer op een schijf replicerende wijzigen Hallo waarde Hallo **UploadThreadsPerVM**, of maak Hallo sleutel aan als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="c33d4-140">tooinfluence hello bandwidth traffic on a replicating disk, modify hello value hello **UploadThreadsPerVM**, or create hello key if it doesn't exist.</span></span>
   * <span data-ttu-id="c33d4-141">tooinfluence hello bandbreedte voor failbackverkeer vanuit Azure, Hallo waarde wijzigen **DownloadThreadsPerVM**.</span><span class="sxs-lookup"><span data-stu-id="c33d4-141">tooinfluence hello bandwidth for failback traffic from Azure, modify hello value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="c33d4-142">Hallo-standaardwaarde is 4.</span><span class="sxs-lookup"><span data-stu-id="c33d4-142">hello default value is 4.</span></span> <span data-ttu-id="c33d4-143">In een netwerk 'overprovisioning', moeten deze registersleutels van Hallo standaardwaarden worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c33d4-143">In an “overprovisioned” network, these registry keys should be changed from hello default values.</span></span> <span data-ttu-id="c33d4-144">Hallo maximum is 32.</span><span class="sxs-lookup"><span data-stu-id="c33d4-144">hello maximum is 32.</span></span> <span data-ttu-id="c33d4-145">Verkeer toooptimize Hallo waarde bewaken.</span><span class="sxs-lookup"><span data-stu-id="c33d4-145">Monitor traffic toooptimize hello value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c33d4-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c33d4-146">Next steps</span></span>

<span data-ttu-id="c33d4-147">Ga te[stap 4: Plan netwerken](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="c33d4-147">Go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>

---
title: aaaPlan capaciteit en schaal voor de virtuele machine van Hyper-V-replicatie (met VMM) tooAzure met Azure Site Recovery | Microsoft Docs
description: Dit artikel tooplan capaciteit en de schaal gebruiken bij het repliceren van Hyper-V-machines in VMM clouds tooAzure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 9818ada9bb21f60ac00b3894696201b06630cb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-with-vmm-tooazure-replication"></a>Stap 3: Plannen capaciteit en schaal voor de replicatie van Hyper-V (met VMM) tooAzure

Nadat u hebt doorgenomen Hallo [implementatievereisten](vmm-to-azure-walkthrough-prerequisites.md), gebruik dit artikel toofigure uit het plannen van capaciteit en schaal, bij het repliceren van on-premises Hyper-V-machines in System Center Virtual Machine Manager (VMM) clouds tooAzure, met [Azure Site Recovery](site-recovery-overview.md).

Na het lezen van dit artikel, eventuele opmerkingen posten Hallo onderin of technische vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="how-do-i-start-capacity-planning"></a>Hoe start capaciteitsplanning?


U verzamelen gegevens over uw replicatieomgeving en plan capaciteit Hallo-gegevens, evenals de Hallo overwegingen gemarkeerd in dit artikel.


## <a name="gather-information"></a>Informatie verzamelen

1. Informatie verzamelen over uw replicatieomgeving, waaronder informatie over de virtuele machines, het aantal schijven per virtuele machine en de opslag per schijf.
2. De snelheid van uw dagelijkse wijzigen (verloop) voor gerepliceerde gegevens identificeren. Hallo downloaden [Hyper-V-hulpprogramma voor capaciteitsplanning](https://www.microsoft.com/download/details.aspx?id=39057) tooget Hallo wijzigingssnelheid. U wordt aangeraden dat u gemiddelden dit hulpprogramma via een week toocapture uitvoeren.
 

## <a name="figure-out-capacity"></a>Capaciteit te achterhalen

Op basis van Hallo verzamelen die u hebt, Voer Hallo [Site Recovery-Capaciteitsplanner](http://aka.ms/asr-capacity-planner-excel) tooanalyze uw bronomgeving en werkbelastingen, schatting van de behoeften van de bandbreedte en serverbronnen voor Hallo bronlocatie en Hallo resources (virtuele machines en opslag, enzovoort), die u nodig hebt in Hallo target-locatie. U kunt Hallo hulpprogramma uitvoeren in een aantal modi:

- Snelle planning: Hallo hulpprogramma uitvoeren in deze modus tooget netwerk- en projecties op basis van een gemiddelde aantal virtuele machines, schijven, opslag en wijzigingssnelheid.
- Detail te plannen: Hallo hulpprogramma uitvoeren in deze modus en Geef details op van elke werkbelasting op het niveau van de virtuele machine. VM-compatibiliteit analyseren en netwerk- en projecties ophalen.

Hallo hulpprogramma nu uitvoeren:

1. Hallo downloaden [hulpprogramma](http://aka.ms/asr-capacity-planner-excel)
2. snelle planner toorun hello, volg [deze instructies](site-recovery-capacity-planner.md#run-the-quick-planner), en selecteer Hallo scenario **Hyper-V tooAzure**.
3. toorun gedetailleerde planner hello, voert u de [deze instructies](site-recovery-capacity-planner.md#run-the-detailed-planner), en selecteer Hallo scenario **Hyper-V tooAzure**.

## <a name="control-network-bandwidth"></a>Netwerkbandbreedte

Nadat u de berekende Hallo bandbreedte die u nodig hebt, hebt u een aantal opties voor het beheren Hallo hoeveelheid bandbreedte die wordt gebruikt voor replicatie:

* **Bandbreedte beperken**: Hyper-V-verkeer dat wordt gerepliceerd tooAzure verloopt via een specifieke Hyper-V-host. U kunt de bandbreedte op Hallo hostserver beperken.
* **Netwerkbandbreedte beïnvloeden**: U kunt zelf bepalen hoeveel Hallo-bandbreedte die wordt gebruikt voor replicatie via diverse registersleutels.

### <a name="throttle-bandwidth"></a>Bandbreedte beperken
1. Hallo Microsoft Azure Backup MMC-module openen op Hallo Hyper-V-hostserver. Een snelkoppeling naar Microsoft Azure Backup is standaard beschikbaar zijn op Hallo bureaublad of in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Klik in de module Hallo **eigenschappen wijzigen**.
3. Op Hallo **bandbreedtebeperking** tabblad Selecteer **inschakelen voor gebruik van internetbandbreedte voor back-upbewerkingen**, en Hallo limieten instellen voor werk en niet-werk uren. Geldige bereiken zijn afkomstig van 512 Kbps too102 Mbps per seconde.

    ![Bandbreedte beperken](./media/vmm-to-azure-walkthrough-capacity/throttle2.png)

U kunt ook Hallo [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset beperking. Hier volgt een voorbeeld:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** geeft aan dat er geen beperking is vereist.

### <a name="influence-network-bandwidth"></a>Netwerkbandbreedte beïnvloeden
1. Navigeer te in Hallo register**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * tooinfluence hello bandbreedte netwerkverkeer op een schijf replicerende wijzigen Hallo waarde Hallo **UploadThreadsPerVM**, of maak Hallo sleutel aan als deze niet bestaat.
   * tooinfluence hello bandbreedte voor failbackverkeer vanuit Azure, Hallo waarde wijzigen **DownloadThreadsPerVM**.
2. Hallo-standaardwaarde is 4. In een netwerk 'overprovisioning', moeten deze registersleutels van Hallo standaardwaarden worden gewijzigd. Hallo maximum is 32. Verkeer toooptimize Hallo waarde bewaken.

## <a name="next-steps"></a>Volgende stappen

Ga te[stap 4: Plan netwerken](vmm-to-azure-walkthrough-network.md).

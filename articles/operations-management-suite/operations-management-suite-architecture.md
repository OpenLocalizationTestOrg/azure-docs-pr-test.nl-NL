---
title: aaaOperations architectuur Management Suite (OMS) | Microsoft Docs
description: Microsoft Operations Management Suite (OMS) is een cloudoplossing voor IT-beheer van Microsoft waarmee u uw on-premises en cloudinfrastructuur kunt beheren en beveiligen.  In dit artikel Hallo verschillende services die worden opgenomen in OMS identificeert en vindt u koppelingen tootheir gedetailleerde inhoud.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 40e41686-7e35-4d85-bbe8-edbcb295a534
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: fa3227aa9c19219009ebe363b7fd2d6565cec59c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="oms-architecture"></a>OMS-architectuur
[Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/services/operations-management-suite/) is een verzameling cloudservices voor beheer van on-premises en cloudomgevingen.  Dit artikel wordt beschreven Hallo verschillende on-premises en cloud-onderdelen van OMS en hun architectuur, hoog niveau cloud computing.  U kunt toohello documentatie verwijzen voor elke service voor meer informatie.

## <a name="log-analytics"></a>Log Analytics
Alle gegevens verzameld door [logboekanalyse](https://azure.microsoft.com/documentation/services/log-analytics/) wordt opgeslagen in Hallo OMS-opslagplaats die wordt gehost in Azure.  Verbonden bronnen genereren gegevens verzameld in Hallo OMS-opslagplaats.  Er zijn momenteel drie soorten verbonden bronnen die worden ondersteund.

* Een agent geïnstalleerd op een [Windows](../log-analytics/log-analytics-windows-agents.md) of [Linux](../log-analytics/log-analytics-linux-agents.md) computer verbonden rechtstreeks tooOMS.
* Een beheergroep van System Center Operations Manager (SCOM) [tooLog Analytics verbonden](../log-analytics/log-analytics-om-agents.md) .  SCOM-agents blijven toocommunicate met beheerservers die voor het doorsturen van gebeurtenissen en prestaties gegevens tooLog Analytics.
* Een [Azure-opslagaccount](../log-analytics/log-analytics-azure-storage.md) waarmee [Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md)-gegevens van een werkrol, webrol of virtuele machine in Azure worden verzameld.

Gegevensbronnen definiëren Hallo-gegevens die Log Analytics uit verbonden bronnen, met inbegrip van gebeurtenislogboeken en prestatiemeteritems verzamelt.  Oplossingen functionaliteit tooOMS toevoegen en kunnen eenvoudig worden toegevoegd tooyour werkruimte van Hallo [galerie met OMS oplossingen](../log-analytics/log-analytics-add-solutions.md).  Sommige oplossingen kunnen een rechtstreekse verbinding tooLog Analytics van SCOM-agents vereisen, terwijl anderen mogelijk een toobe extra agent is geïnstalleerd.

Log Analytics is een portal op Internet dat u kunt toomanage OMS-bronnen gebruiken, toevoegen en oplossingen voor OMS configureren en weergeven en in Hallo OMS-opslagplaats analyseren.

![Hoogwaardige Log Analytics-architectuur](media/operations-management-suite-architecture/log-analytics.png)

## <a name="azure-automation"></a>Azure Automation
[Azure Automation-runbooks](http://azure.microsoft.com/documentation/services/automation) worden uitgevoerd in hello Azure-cloud en toegang tot bronnen in Azure, in andere cloudservices of toegankelijk is vanaf Hallo openbare Internet.  U kunt ook met [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md) on-premises computers opgeven in uw lokale datacenter, zodat runbooks toegang hebben tot lokale resources.

[DSC-configuraties](../automation/automation-dsc-overview.md) opgeslagen in Azure Automation rechtstreeks toegepaste tooAzure virtuele machines kunnen worden.  Andere fysieke en virtuele machines kunnen configuraties van hello Azure Automation DSC-pull-server aanvragen.

Azure Automation heeft een OMS-oplossing die geeft de statistieken weer en koppelingen toolaunch hello Azure-portal voor alle bewerkingen.

![Hoogwaardige Azure Automation-architectuur](media/operations-management-suite-architecture/automation.png)

## <a name="azure-backup"></a>Azure Backup
Beveiligde gegevens in [Azure Backup](http://azure.microsoft.com/documentation/services/backup) worden opgeslagen in een Backup-kluis in een bepaalde geografische regio.  Hallo-gegevens worden gerepliceerd binnen dezelfde regio Hallo en, afhankelijk van Hallo type kluis, mogelijk ook gerepliceerde tooanother regio voor verdere redundantie.

Azure Backup heeft drie fundamentele scenario's.

* Windows-computer met Azure Backup-agent.  Hiermee kunt u toobackup bestanden en mappen van elke WindowsServer of client rechtstreeks tooyour Azure Backup-kluis.  
* System Center Data Protection Manager- (DPM) of Microsoft Azure Backup-server. Hiermee kunt u tooleverage DPM of de Microsoft Azure Backup-Server toobackup bestanden en mappen bovendien tooapplication werkbelastingen zoals SQL en SharePoint toolocal opslag en vervolgens repliceren tooyour Azure Backup-kluis.
* Extensies voor virtuele Azure-machines.  Hiermee kunt u toobackup virtuele Azure-machines tooyour Azure Backup-kluis.

Azure Backup heeft een OMS-oplossing die geeft de statistieken weer en koppelingen toolaunch hello Azure-portal voor alle bewerkingen.

![Hoogwaardige Azure Backup-architectuur](media/operations-management-suite-architecture/backup.png)

## <a name="azure-site-recovery"></a>Azure Site Recovery
Met [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) wordt de replicatie, failover en failback van virtuele machines en fysieke servers gecoördineerd. Replicatiegegevens uitgewisseld tussen Hyper-V-hosts, VMware-hypervisors en fysieke servers in de primaire en secundaire datacenters of tussen Hallo datacenter- en Azure-opslag.  Met Site Recovery worden metagegevens opgeslagen in kluizen in een bepaalde geografische Azure-regio. Er is geen gerepliceerde gegevens worden opgeslagen door Hallo Site Recovery-service.

Azure Site Recovery heeft drie fundamentele replicatiescenario's.

**Virtuele Hyper-V-machines repliceren**

* Als Hyper-V virtuele machines in VMM-clouds worden beheerd, kunt u tooa secundaire center of tooAzure gegevensopslag repliceren.  Replicatie tooAzure is via een beveiligde internetverbinding.  Replicatie tooa secundair datacenter is via Hallo LAN.
* Als Hyper-V virtuele machines worden niet beheerd door VMM, kunt u alleen tooAzure opslag repliceren.  Replicatie tooAzure is via een beveiligde internetverbinding.

**Virtuele VMware-machines repliceren**

* U kunt repliceren VMware virtuele machines tooa secundair datacenter waarop VMware of tooAzure opslag wordt uitgevoerd.  Replicatie tooAzure kan plaatsvinden via een site-naar-site VPN of Azure ExpressRoute of via een beveiligde internetverbinding. Replicatie tooa secundair datacenter vindt plaats via Hallo InMage Scout gegevenskanaal.

**Fysieke Windows- en Linux-servers repliceren** 

* U kunt fysieke servers tooa secundaire datacenter of tooAzure opslag repliceren. Replicatie tooAzure kan plaatsvinden via een site-naar-site VPN of Azure ExpressRoute of via een beveiligde internetverbinding. Replicatie tooa secundair datacenter vindt plaats via Hallo InMage Scout gegevenskanaal.  Azure Site Recovery heeft een OMS-oplossing die een aantal statistieken worden weergegeven, maar moet u hello Azure-portal gebruiken voor alle bewerkingen.

![Hoogwaardige Azure Site Recovery-architectuur](media/operations-management-suite-architecture/site-recovery.png)

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* Meer informatie over [Azure Automation](https://azure.microsoft.com/documentation/services/automation).
* Meer informatie over [Azure Backup](http://azure.microsoft.com/documentation/services/backup).
* Meer informatie over [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).


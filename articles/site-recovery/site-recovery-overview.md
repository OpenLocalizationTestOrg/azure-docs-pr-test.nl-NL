---
title: aaaWhat is Azure Site Recovery? | Microsoft Docs
description: Biedt een overzicht van hello Azure Site Recovery-service en een overzicht van implementatiescenario's.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: e9b97b00-0c92-4970-ae92-5166a4d43b68
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: da6755654b8036a03314ec836f014b64428d5518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-site-recovery"></a>Wat is Site Recovery?

Welkom toohello Azure Site Recovery-service. Dit artikel bevat een overzicht van Hallo-service.

## <a name="business-continuity-and-disaster-recovery-bcdr-with-azure-recovery-services"></a>Bedrijfscontinuïteit en herstel na noodgevallen (BCDR) met Azure Recovery Services

Als een organisatie moet u toofigure uit hoe u tookeep uw gegevens veilig gaat en apps/werkbelastingen die worden uitgevoerd wanneer de geplande en ongeplande storingen optreden.

Azure Recovery Services bijdragen tooyour BCDR-strategie:

- **Site Recovery-service**: met Site Recovery bent u verzekerd van bedrijfscontinuïteit door uw apps uit te voeren op virtuele machines en fysieke servers die beschikbaar zijn als een site uitvalt. Site Recovery repliceert werkbelastingen die worden uitgevoerd op virtuele machines en fysieke servers, zodat ze beschikbaar op een secundaire locatie blijven als de primaire site Hallo niet beschikbaar. Deze herstelt werkbelastingen toohello primaire site wanneer deze actief is en opnieuw uit te voeren.
- **Backup-service**: bovendien Hallo [Azure Backup](https://docs.microsoft.com/azure/backup/) service houdt uw gegevens veilig en herstelbaar door back-up tooAzure.

Met Site Recovery kunt u replicatie beheren voor:

- Azure-VM's die worden gerepliceerd tussen Azure-regio's.
- On-premises virtuele machines en fysieke servers repliceren tooAzure of tooa secundaire site.


## <a name="what-does-site-recovery-provide"></a>Wat biedt Site Recovery?

**Functie** | **Details**
--- | ---
**Een eenvoudige BCDR-oplossing implementeren** | Met Site Recovery, kunt u instellen en beheren van replicatie, failover en failback vanaf één locatie in hello Azure-portal.
**Azure-VM's repliceren** | U kunt uw BCDR-strategie zo instellen dat Azure-VM's worden gerepliceerd tussen Azure-regio's.
**On-premises VM's offsite repliceren** | U kunt repliceren lokale virtuele machines en fysieke servers tooAzure of tooa secundaire on-premises locatie. Replicatie tooAzure elimineert Hallo kosten en complexiteit van het onderhouden van een secundair datacenter.
**Workloads repliceren** | U kunt alle workloads repliceren die worden uitgevoerd op ondersteunde Azure-VM's, on-premises Hyper-V-VM's, VMware-VM's en fysieke Windows-/Linux-servers.
**Gegevens flexibel en veilig bewaren** | Met Site Recovery deelt u replicatie in zonder toepassingsgegevens te onderscheppen. Gerepliceerde gegevens worden opgeslagen in Azure-opslag met Hallo herstelmogelijkheden die biedt. Wanneer failover plaatsvindt, worden virtuele Azure-machines op basis van Hallo gerepliceerde gegevens gemaakt.
**Voldoen aan de RTO's en RPO's** | Zorg dat de beoogde hersteltijden (RTO) en beoogde herstelpunten (RPO) binnen de organisatielimieten blijven. Site Recovery biedt continue replicatie voor Azure-VM's en VMware-VM's en een lage replicatiefrequentie van slechts 30 seconden voor Hyper-V. U kunt beoogde hersteltijden (RTO) verder beperken door de integratie met [Azure Traffic Manager](https://azure.microsoft.com/blog/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/).
**Apps consistent houden bij failover** | U kunt herstelpunten configureren met toepassingsconsistente momentopnamen. Met toepassingsconsistente momentopnamen kunt u schijfgegevens, alle gegevens in het geheugen en alle lopende transacties vastleggen.
**Testen zonder onderbreking** | U kunt eenvoudig testfailovers toosupport noodhersteloefeningen, uitvoeren zonder de lopende replicatie.
**Flexibele failovers uitvoeren** | U kunt bij verwachte uitval geplande failovers uitvoeren zonder gegevensverlies en bij onverwachte noodsituaties ongeplande failovers uitvoeren met minimaal gegevensverlies (afhankelijk van de replicatiefrequentie). U kunt eenvoudig back tooyour primaire site mislukken wanneer deze weer beschikbaar is.
**Herstelplannen maken** | U kunt failovers en herstel van toepassingen met meerdere lagen op meerdere virtuele machines aanpassen en indelen met herstelplannen. U groepeert machines binnen plannen en voegt scripts en handmatige acties toe. Herstelplannen kunnen worden geïntegreerd met Azure Automation-runbooks.
**Integreren met bestaande BCDR-technologieën** | Met Site Recovery kunt u integreren met andere BCDR-technologieën. U kunt bijvoorbeeld de Site Recovery tooprotect Hallo SQL Server-back-end van zakelijke workloads, met inbegrip van systeemeigen ondersteuning voor SQL Server AlwaysOn toomanage Hallo failovers van beschikbaarheidsgroepen.
**Integreren met Hallo automation-bibliotheek** | Een uitgebreide Azure Automation-bibliotheek met toepassingsspecifieke scripts die klaar zijn voor gebruik en kunnen worden gedownload en geïntegreerd met Site Recovery.
**Netwerkinstellingen beheren** | Site Recovery kan worden geïntegreerd met Azure voor eenvoudig toepassingsnetwerkbeheer, waaronder het reserveren van IP-adressen, het configureren van load balancers en het integreren van Azure Traffic Manager voor het efficiënt schakelen tussen netwerken.


## <a name="what-can-i-replicate"></a>Wat kan ik repliceren?

**Ondersteund** | **Details**
--- | ---
**Wat kan ik repliceren?** | Azure-VM's tussen Azure-regio's (in preview)<br/><br/>  Lokale virtuele VMware-machines, Hyper-V-machines fysieke servers (Windows en Linux) tooAzure < br /<br/> Een on-premises virtuele VMware-machines, Hyper-V-machines fysieke servers tooa secundaire site. Voor Hyper-V-machines worden replicatie tooa secundaire site wordt alleen ondersteund als Hyper-V-hosts worden beheerd door System Center VMM.
**Welke regio's worden ondersteund voor Site Recovery?** | [Ondersteunde regio's](https://azure.microsoft.com/regions/services/) |
**Welke besturingssystemen zijn vereist voor gerepliceerde machines?** | [Vereisten voor Azure-VM's](site-recovery-support-matrix-azure-to-azure.md#support-for-replicated-machine-os-versions)<br></br>[Vereisten voor VMware-VM's](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)<br/><br/> Voor Hyper-V-VM's worden alle [gastbesturingssystemen](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) ondersteund die door Azure en Hyper-V worden ondersteund.<br/><br/> [Vereisten voor fysieke servers](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)
**Welke VMware-servers/-hosts moet ik gebruiken?** | VMware-VM's kunnen zich bevinden op [ondersteunde vSphere-hosts/vCenter-servers](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)
**Welke workloads kan ik repliceren?** | U kunt iedere werkload repliceren die wordt uitgevoerd op een ondersteunde replicatiemachine. Bovendien Hallo Site Recovery-team hebt uitgevoerd testen van de app-specifiek voor een [aantal apps](site-recovery-workload.md#workload-summary).


## <a name="azure-portal-considerations"></a>Overwegingen voor Azure Portal

* Site Recovery kan worden geïmplementeerd in Hallo [Azure-portal](https://portal.azure.com).
* U kunt Site Recovery in de klassieke Azure-portal Hallo beheren met Hallo-model voor het beheer van klassieke services.
- klassieke portal Hallo moet alleen gebruikte toomaintain bestaande Site Recovery-implementaties. U kunt nieuwe kluizen niet maken in de klassieke portal Hallo.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [workloadondersteuning](site-recovery-workload.md)
* Aan de slag met [Azure VM-replicatie tussen regio's](site-recovery-azure-to-azure.md), [VMware replicatie tooAzure](vmware-walkthrough-overview.md), of [Hyper-V-replicatie tooAzure](hyper-v-site-walkthrough-overview.md).

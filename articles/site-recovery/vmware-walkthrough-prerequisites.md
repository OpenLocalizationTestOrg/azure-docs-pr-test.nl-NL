---
title: aaaPrerequisites voor VMware tooAzure replicatie met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo-vereisten voor het repliceren van de werkbelasting op virtuele VMware-machines tooAzure, met behulp van hello Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 318156ba-793b-48d0-98d4-cc5436bf28a3
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 14f8e9713b42a1d8da71223fbbb7a6b7c4303adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-vmware-tooazure-replication"></a>Stap 2: Controleer de vereisten voor VMware tooAzure replicatie Hallo

Hallo vereisten samengevat in de volgende tabel Hallo lezen.

**Vereiste** | **Details**
--- | ---
**Azure** | Meer informatie over [Azure-vereisten](site-recovery-prereq.md#azure-requirements)
**On-premises configuratieserver** | U moet een VMware VM waarop Windows Server 2012 R2 of hoger. U kunt instellen om deze server tijdens de implementatie van Site Recovery.<br/><br/> Hallo standaardproces worden server en de hoofddoelserver ook geïnstalleerd op deze virtuele machine. Als u opschalen, u een afzonderlijk proces-server moet mogelijk en Hallo heeft dezelfde vereisten als Hallo configuratieserver.<br/><br/> Meer informatie over deze onderdelen [hier](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)
**On-premises VMware-servers** | Een of meer VMware vSphere servers, 6.5, 6.0, 5.5, 5.1 uitgevoerd met de meest recente updates. Servers moeten zich bevinden in Hallo netwerk als de configuratieserver hello (of een afzonderlijk processerver).<br/><br/> We raden aan een vCenter-server toomanage hosts met 6.5, 6.0 of 5.5 met de nieuwste updates Hallo.
**On-premises virtuele machines** | Virtuele machines die u wilt dat tooreplicate moet worden uitgevoerd een [ondersteund besturingssysteem](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), en voldoet aan de [vereisten voor Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). VM moet VMware-hulpprogramma's hebben.
**URL 's** | Hallo configuratieserver moet toegang tot toothese URL's:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Als u IP-adressen gebaseerde firewallregels, moet u dat ze tooAzure communicatie toestaan.<br/></br> Hallo toestaan [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653), en Hallo HTTPS (443)-poort.<br/></br> IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West (gebruikt voor toegangsbeheer en identiteitsbeheer) toestaan.<br/><br/> Toestaan dat deze URL voor het downloaden van Hallo MySQL: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Mobility-service** | Geïnstalleerd op elke gerepliceerde virtuele machine.




## <a name="limitations"></a>Beperkingen

Zorg ervoor dat u begrijpt Hallo beperkingen samengevat in Hallo tabel voordat u implementeert.

**Beperking** | **Details**
--- | ---
**Azure** | Accounts voor opslag en netwerk moet zich in Hallo dezelfde regio bevinden als Hallo kluis<br/><br/> Als u een premium storage-account gebruikt, moet u ook een standaard account toostore replicatielogboeken worden opgeslagen<br/><br/> Accounts in het midden- en Zuid, India toopremium kan niet worden gerepliceerd.
**On-premises configuratieserver** | VMware VM adaptertype moet VMXNET3. Dit niet het geval is, [deze update installeert](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> vSphere PowerCLI 6.0 moet worden geïnstalleerd.<br/><br> Hallo machine mag niet een domeincontroller zijn. Hallo-machine moet een statisch IP-adres hebben.<br/><br/> Hallo-hostnaam moet 15 tekens of korter is, en het besturingssysteem moet in het Engels.
**VMware** | Site Recovery biedt geen ondersteuning voor nieuwe vCenter en vSphere 6.5 en 6.0 functies zoals cross vCenter vMotion, virtuele volumes en opslagruimten DRS.
**VM's** | Controleer of [beperkingen van de virtuele machine in Azure](site-recovery-prereq.md#azure-requirements)<br/><br/> U kunt virtuele machines met versleutelde schijven of virtuele machines met UEFI/EFI-opstarten kan niet repliceren.<br/><br> Gedeelde schijf worden niet ondersteund. Als de bron-Hallo VM heeft NIC-koppeling, wordt deze geconverteerd tooa enkel NIC na een failover.<br/><br/> Als VMs een iSCSI-schijf hebt, converteert deze Site Recovery tooa VHD-bestand na een failover. Als Hallo iSCSI-doel kan worden bereikt door Hallo virtuele Azure-machine, verbindt tooit en ziet deze en Hallo VHD. Als dit gebeurt, moet u Hallo iSCSI-doel.<br/><br/> Als u wilt dat tooenable multi-VM consistentie, waardoor de virtuele machines met dezelfde werkbelasting toobe hersteld hello wordt samen tooa consistente gegevens punt, open poort 20004 op Hallo VM.<br/><br/> Windows moet worden geïnstalleerd op Hallo C-station. Hallo besturingssysteemschijf moet de basis- en geen dynamische. Hallo gegevensschijf kan niet dynamisch zijn.<br/><br/> Linux/etc/hosts bestanden op virtuele machines moeten vermeldingen die zijn toegewezen Hallo lokale host naam tooIP adressen die zijn gekoppeld aan alle netwerkadapters bevatten. Hallo hostnaam, koppelpunten, apparaatnaam, systeempaden en bestandsnamen (/ enzovoort; /usr) mag alleen in het Engels zijn.<br/><br/> Specifieke typen [Linux opslag](site-recovery-support-matrix-to-azure.md#support-for-storage) worden ondersteund.<br/><br/>Maken of in te stellen **disk.enableUUID=true** in Hallo VM-instellingen. Dit biedt een consistente UUID toohello VMDK, zodat deze correct koppelt en zorgt ervoor dat alleen nog deltawijzigingen overgedragen back tooon lokale tijdens de failback zonder een volledige replicatie zijn.


## <a name="next-steps"></a>Volgende stappen

- Als u een volledige implementatie uitvoert, gaat u verder te[stap 3: plannen van capaciteit](vmware-walkthrough-capacity.md)
- Als u een eenvoudige testimplementatie uitvoert, gaat u verder te[stap 4: Plan netwerken](vmware-walkthrough-network.md).

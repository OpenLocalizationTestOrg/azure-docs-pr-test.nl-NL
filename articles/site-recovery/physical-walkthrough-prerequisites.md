---
title: aaaPrerequisites voor replicatie van fysieke server tooAzure met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo-vereisten voor het repliceren van workloads die worden uitgevoerd op fysieke Windows of Linux-servers tooAzure, met behulp van hello Azure Site Recovery-service.
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
ms.openlocfilehash: b0ed53a143079877a2ad21ee17aae5510e0dc058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-physical-server-tooazure-replication"></a>Stap 2: Controleer Hallo-vereisten voor de fysieke server tooAzure replicatie

Bekijk samengevat in de tabel Hallo Hallo-vereisten.


**Vereiste** | **Details**
--- | ---
**Azure** | Meer informatie over [Azure-vereisten](site-recovery-prereq.md#azure-requirements)
**On-premises configuratieserver** | U moet een fysieke server (of logische VMware VM), zoals met Windows Server 2012 R2 of hoger. U kunt instellen om deze server tijdens de implementatie van Site Recovery.<br/><br/> Standaardproces Hallo zijn-server en de hoofddoelserver ook geïnstalleerd op deze machine. Wanneer u opschalen, moet u mogelijk een afzonderlijk proces-server. Als u dit doet, heeft het Hallo dezelfde vereisten als Hallo configuratieserver.<br/><br/> [Meer informatie](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).
**On-premises virtuele machines** | Computers die u wilt dat tooreplicate moet worden uitgevoerd een [ondersteund besturingssysteem](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) en voldoet aan de [vereisten voor Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URL 's** | Hallo configuratieserver moet toegang tot toothese URL's:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Als u IP-adressen gebaseerde firewallregels, moet u dat ze tooAzure communicatie toestaan.<br/></br> Hallo toestaan [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653), en Hallo HTTPS (443)-poort.<br/></br> IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West (gebruikt voor toegangsbeheer en identiteitsbeheer) toestaan.<br/><br/> Toestaan dat deze URL voor het downloaden van Hallo MySQL: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Mobility-service** | Geïnstalleerd op elke server die is gerepliceerd.




## <a name="limitations"></a>Beperkingen

Houd er rekening mee Hallo beperkingen samengevat in Hallo tabel voordat u implementeert.

**Beperking** | **Details**
--- | ---
**Azure** | Accounts voor opslag en netwerk moet zich in Hallo dezelfde regio bevinden als Hallo kluis<br/><br/> Als u een premium storage-account gebruikt, moet u ook een standaard account toostore replicatielogboeken worden opgeslagen<br/><br/> Accounts in het midden- en Zuid, India toopremium kan niet worden gerepliceerd.
**On-premises configuratieserver** | Als u een VMware VM als Hallo configuratie server-machine, moet Hallo VMware VM adaptertype VMXNET3. Dit niet het geval is, [deze update installeert](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> Voor een VM VMware moet vSphere PowerCLI 6.0 worden geïnstalleerd.<br/><br> Hallo machine mag niet een domeincontroller zijn.<br/><br/> Hallo-machine moet een statisch IP-adres hebben.<br/><br/> Hallo-hostnaam moet 15 tekens of korter is, en het besturingssysteem moet in het Engels.
**Machines repliceren** | Controleer of [beperkingen van de virtuele machine in Azure](site-recovery-prereq.md#azure-requirements)<br/><br/> U kunt virtuele machines met versleutelde schijven of virtuele machines met UEFI/EFI-opstarten kan niet repliceren.<br/><br> Gedeelde schijf worden niet ondersteund. Als de bron-Hallo VM heeft NIC-koppeling, wordt deze geconverteerd tooa enkel NIC na een failover.<br/><br/> Als VMs een iSCSI-schijf hebt, converteert deze Site Recovery tooa VHD-bestand na een failover. Als Hallo iSCSI-doel kan worden bereikt door Hallo virtuele Azure-machine, verbindt tooit en ziet deze en Hallo VHD. Als dit gebeurt, moet u Hallo iSCSI-doel.<br/><br/> Als u wilt dat tooenable multi-VM consistentie, waardoor de virtuele machines met dezelfde werkbelasting toobe hersteld hello wordt samen tooa consistente gegevens punt, open poort 20004 op Hallo VM.<br/><br/> Windows moet worden geïnstalleerd op Hallo C-station. Hallo besturingssysteemschijf moet de basis- en geen dynamische. Hallo gegevensschijf kan niet dynamisch zijn.<br/><br/> Linux/etc/hosts bestanden op virtuele machines moeten vermeldingen die zijn toegewezen Hallo lokale host naam tooIP adressen die zijn gekoppeld aan alle netwerkadapters bevatten. Hallo hostnaam, koppelpunten, apparaatnaam, systeempaden en bestandsnamen (/ enzovoort; /usr) mag alleen in het Engels zijn.<br/><br/> Specifieke typen [Linux opslag](site-recovery-support-matrix-to-azure.md#support-for-storage) worden ondersteund.<br/><br/>Maken of in te stellen **disk.enableUUID=true** in Hallo VM-instellingen. Dit biedt een consistente UUID toohello VMDK, zodat deze correct koppelt en zorgt ervoor dat alleen nog deltawijzigingen overgedragen back tooon lokale tijdens de failback zonder een volledige replicatie zijn.


## <a name="next-steps"></a>Volgende stappen

- Als u een volledige implementatie uitvoert, gaat u verder te[stap 3: plannen van capaciteit](physical-walkthrough-capacity.md)
- Als u een eenvoudige testimplementatie uitvoert, gaat u verder te[stap 4: Plan netwerken](physical-walkthrough-network.md).

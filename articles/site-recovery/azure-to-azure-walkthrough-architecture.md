---
title: Hallo-architectuur voor de replicatie van Azure VM's tussen Azure-regio's aaaReview | Microsoft Docs
description: Dit artikel bevat een overzicht van de onderdelen en de architectuur die wordt gebruikt voor het virtuele Azure-machines repliceren tussen Azure-regio's met behulp van hello Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a>Stap 1: Bekijk Hallo-architectuur voor replicatie van de virtuele machine van Azure tussen Azure-regio 's


Nadat u hebt bekeken Hallo [overzicht stappen](azure-to-azure-walkthrough-overview.md) voor deze implementatie Lees dit artikel toounderstand Hallo onderdelen en -processen die worden gebruikt bij het repliceren en herstellen van de virtuele Azure-machines (VM's) van een Azure-regio tooanother, met behulp van [Azure Site Recovery](site-recovery-overview.md).

- Wanneer u klaar bent met Hallo artikel, moet u een duidelijk beeld van de werking van Azure VM replicatie tooanother regio hebben.
- Eventuele opmerkingen onder Hallo van dit artikel plaatsen of vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
>Azure VM-replicatie met Hallo Site Recovery-service is momenteel in preview.



## <a name="architectural-components"></a>Architectuuronderdelen

Hallo volgende diagram toont een globaal overzicht van een virtuele machine van Azure-omgeving in een specifieke regio (in dit voorbeeld Hallo locatie VS-Oost). In een virtuele machine van Azure-omgeving:
- Apps kunnen worden uitgevoerd op virtuele machines met schijven die zijn verdeeld over de storage-accounts.
- Hallo virtuele machines kan worden opgenomen in een of meer subnetten binnen een virtueel netwerk.

![klant-omgeving](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a>Replicatieproces

### <a name="step-1"></a>Stap 1

Wanneer u Azure VM-replicatie in hello Azure-portal inschakelt, Hallo bronnen die in het volgende Hallo diagram en de tabel automatisch worden gemaakt in Hallo doelregio. Resources worden gemaakt op basis van regio broninstellingen standaard. Hallo-doelinstellingen zo nodig kunt u aanpassen. [Meer informatie](site-recovery-replicate-azure-to-azure.md).

![Stap 1 replicatieproces inschakelen](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

**Resource** | **Details**
--- | ---
**Doelresourcegroep** | Hallo resource groep toowhich gerepliceerde virtuele machines na een failover behoren.
**Doel virtueel netwerk** | Hallo-netwerk waarin gerepliceerde virtuele machines zich bevinden na een failover. Een netwerktoewijzing wordt gemaakt tussen bron- en virtuele netwerken, en vice versa.
**Cache-opslagaccounts** | Voordat u wijzigingen op de bron-VM's zijn gerepliceerd toohello doel storage-account, worden ze bijgehouden en toohello cache storage-account in de doellocatie Hallo verzonden. Dit zorgt ervoor minimale gevolgen voor de productie-apps die worden uitgevoerd op Hallo VM.
**Doel storage-accounts**  | Storage-accounts in Hallo doel toowhich Hallo locatiegegevens wordt gerepliceerd.
**Doel-beschikbaarheidssets**  | Beschikbaarheidssets in welke Hallo gerepliceerde virtuele machines zich bevinden na een failover.

### <a name="step-2"></a>Stap 2

Als replicatie is ingeschakeld, wordt automatisch Hallo Site Recovery-extensie Mobility-service op Hallo VM geïnstalleerd. Hallo volgende gebeurt:

1. Hallo VM is geregistreerd met Site Recovery.

2. Continue replicatie is geconfigureerd voor Hallo VM. Schrijft gegevens op Hallo VM met schijven zijn continu toohello cache storage-account in de bronlocatie Hallo overgedragen.

   ![Stap 2 replicatieproces inschakelen](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  Houd er rekening mee dat de Site Recovery nooit moet binnenkomende verbindingen toohello VM. Alleen uitgaande connectiviteit tooSite Recovery-service-URL's of het IP-adressen, Office 365-verificatie-URL's of het IP-adressen en IP-adressen van cache storage-account nodig. 

## <a name="continuous-replication-process"></a>Continue replicatie in proces

Nadat u continue replicatie werkt, overgedragen schijf schrijfbewerkingen onmiddellijk zijn toohello cache storage-account. Site Recovery Hallo gegevens verwerkt en verzendt het toohello doel storage-account. Nadat het Hallo-gegevens zijn verwerkt, worden herstelpunten gegenereerd in Hallo doel storage-account om de paar minuten.

## <a name="failover-process"></a>Failover-proces

Wanneer u een failover initieert, doel virtuele machines worden gemaakt in de doelresourcegroep hello, virtuele doelnetwerk, Doelsubnet Hallo en Hallo-beschikbaarheidsset. U kunt een willekeurig herstelpunt gebruiken tijdens een failover.

![Failover-proces](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a>Volgende stappen

Ga te[stap 2: Controleer of de vereisten en beperkingen](azure-to-azure-walkthrough-prerequisites.md)

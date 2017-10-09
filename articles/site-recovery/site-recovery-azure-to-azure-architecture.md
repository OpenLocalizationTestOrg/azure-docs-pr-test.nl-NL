---
title: aaaHow ondersteunt de virtuele machine van Azure replicatie tussen de werkzaamheden van de Azure-regio's in Azure Site Recovery?  | Microsoft Docs
description: Dit artikel bevat een overzicht van de onderdelen en de architectuur die wordt gebruikt voor het virtuele Azure-machines repliceren tussen Azure-regio's met behulp van hello Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a>Hoe werkt Azure VM-replicatie in Site Recovery?


Dit artikel wordt beschreven Hallo-onderdelen en -processen betrokken bij repliceren en herstellen van de virtuele Azure-machines (VM's) van één regio tooanother met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service.

>[!NOTE]
>Azure VM-replicatie met Hallo Site Recovery-service is momenteel in preview.

Eventuele opmerkingen onder Hallo van dit artikel plaatsen of vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architectural-components"></a>Architectuuronderdelen

Hallo volgende diagram toont een globaal overzicht van een virtuele machine van Azure-omgeving in een specifieke regio (in dit voorbeeld Hallo locatie VS-Oost). In een virtuele machine van Azure-omgeving:
- Apps kunnen worden uitgevoerd op virtuele machines met schijven die zijn verdeeld over de storage-accounts.
- Hallo virtuele machines kan worden opgenomen in een of meer subnetten binnen een virtueel netwerk.

![klant-omgeving](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

Meer informatie over de implementatievereisten Hallo en vereisten op Hallo [ondersteuningsmatrix](site-recovery-support-matrix-azure-to-azure.md).

## <a name="replication-process"></a>Replicatieproces

### <a name="step-1"></a>Stap 1

Wanneer u Azure VM-replicatie in hello Azure-portal inschakelt, Hallo bronnen die in het volgende Hallo diagram en de tabel automatisch worden gemaakt in Hallo doelregio. Resources worden gemaakt op basis van regio broninstellingen standaard. Hallo-doelinstellingen zo nodig kunt u aanpassen. [Meer informatie](site-recovery-replicate-azure-to-azure.md).

![Stap 1 replicatieproces inschakelen](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

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

   ![Stap 2 replicatieproces inschakelen](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > Site Recovery moet nooit binnenkomende verbindingen toohello VM. Hallo VM moet alleen uitgaande verbinding tooSite Recovery service-URL's of het IP-adressen, Office 365-verificatie URL's of het IP-adressen en IP-adressen van cache storage-account. Zie voor meer informatie, Hallo [netwerken richtlijnen voor het repliceren van virtuele machines in Azure](site-recovery-azure-to-azure-networking-guidance.md) artikel.

## <a name="continuous-replication-process"></a>Continue replicatie in proces

Nadat u continue replicatie werkt, overgedragen schijf schrijfbewerkingen onmiddellijk zijn toohello cache storage-account. Site Recovery Hallo gegevens verwerkt en verzendt het toohello doel storage-account. Nadat het Hallo-gegevens zijn verwerkt, worden herstelpunten gegenereerd in Hallo doel storage-account om de paar minuten.

## <a name="failover-process"></a>Failover-proces

Wanneer u een failover initieert, doel virtuele machines worden gemaakt in de doelresourcegroep hello, virtuele doelnetwerk, Doelsubnet Hallo en Hallo-beschikbaarheidsset. U kunt een willekeurig herstelpunt gebruiken tijdens een failover.

![Failover-proces](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [netwerken](site-recovery-azure-to-azure-networking-guidance.md) voor replicatie van de virtuele machine van Azure.
- Ga als volgt een overzicht te[virtuele Azure-machines repliceren.](site-recovery-azure-to-azure.md)

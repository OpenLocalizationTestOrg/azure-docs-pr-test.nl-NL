---
title: aaaReplicate toepassingen (Azure tooAzure) | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooset van de replicatie van de virtuele machines die wordt uitgevoerd in een Azure-regio te een andere regio in Azure.
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
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a>Virtuele machines in Azure tooanother Azure-regio worden gerepliceerd.



>[!NOTE]
>
> Site Recovery replicatie voor virtuele machines in Azure is momenteel in preview.

Dit artikel wordt beschreven hoe tooset van de replicatie van de virtuele machines die wordt uitgevoerd in een Azure-regio tooanother Azure-regio.

## <a name="prerequisites"></a>Vereisten

* Hallo artikel wordt ervan uitgegaan dat u al over de Site Recovery en de Recovery Services-kluis weet. U moet toohave een 'Recovery services-kluis' vooraf gemaakt.

    >[!NOTE]
    >
    > Het verdient aanbeveling om in te maken Hallo 'Recovery services-kluis' hello locatie waar u uw virtuele machines tooreplicate. Als uw doellocatie 'VS-midden', bijvoorbeeld kluis in 'VS-midden' maken.

* Als u regels van de Netwerkbeveiligingsgroep groepen (NSG) of firewall proxy toocontrol toegang toooutbound internetverbinding op Hallo Azure Virtual machines gebruikt, zorg ervoor dat geaccepteerde u Hallo URL's of IP-adressen vereist. Raadpleeg te[leidraad voor netwerken](./site-recovery-azure-to-azure-networking-guidance.md) voor meer informatie.

* Als u een ExpressRoute- of een VPN-verbinding tussen on-premises en Hallo bronlocatie in Azure, voert u de [overwegingen voor het herstel voor ExpressRoute Azure tooon-premises Site / VPN-configuratie](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.

* Uw Azure gebruikersaccount moet toohave bepaalde [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicatie van een virtuele machine van Azure.

* Uw Azure-abonnement moet worden ingeschakeld toocreate virtuele machines in de doellocatie Hallo gewenste toouse als DR regio. Neem contact op met ondersteuning tooenable Hallo vereist quotum.

## <a name="enable-replication-from-azure-site-recovery-vault"></a>Schakel replicatie van Azure Site Recovery-kluis
In dit voorbeeld wordt er VM's worden uitgevoerd in toohello voor Azure-locatie in Hallo Oost-Azië, Zuidoost-Azië ' locatie gerepliceerd. Hallo stappen zijn als volgt:

 Klik op **+ repliceren** in Hallo kluis tooenable replicatie voor Hallo virtuele machines.

1. **Bron:** toohello punt van oorsprong Hallo machines die in dit geval verwijst **Azure**.

2. **Bronlocatie:** is hello Azure-regio waar u tooprotect uw virtuele machines wilt. In dit voorbeeld worden Hallo bronlocatie Oost-Azië

3. **Implementatiemodel:** toohello Azure implementatiemodel Hallo bron machines verwijst. U kunt ofwel classic selecteren of resourcemanager en de machines die horen toohello specifiek model voor beveiliging in de volgende stap hello wordt weergegeven.

      >[!NOTE]
      >
      > U kunt alleen een klassieke virtuele machine repliceren en deze herstellen als een klassieke virtuele machine. U kunt deze niet herstellen als de virtuele machine van een Resource Manager.

4. **Resourcegroep:** de Hallo resource groep toowhich deel uitmaken van uw virtuele bronmachines. Alle Hallo VM's onder de geselecteerde resourcegroep hello wordt vermeld voor beveiliging in de volgende stap Hallo.

    ![Replicatie inschakelen](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

In **virtuele Machines > Selecteer de virtuele machines**en klik op elke machine die u wilt dat tooreplicate selecteren. U kunt alleen machines selecteren waarvoor replicatie kan worden ingeschakeld. Klik vervolgens op OK.
    ![Replicatie inschakelen](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)


Onder de sectie instellingen kunt u doel voor site-eigenschappen configureren

1. **Doellocatie:** dit is Hallo-locatie waar de brongegevens van de virtuele machine wordt gerepliceerd. Afhankelijk van uw locatie voor geselecteerde machines, biedt Site Recovery dat u een lijst met doelregio geschikte Hallo.

    > [!TIP]
    > Het verdient aanbeveling tookeep doellocatie dezelfde vanaf uw recovery services-kluis.

2. **Doelresourcegroep:** is Hallo resource groep toowhich uw gerepliceerde virtuele machines deel van uitmaakt. Standaard maakt ASR een nieuwe resourcegroep in Hallo doelregio met naam 'asr' achtervoegsel heeft. Als de resourcegroep die zijn gemaakt door ASR al bestaat, wordt opnieuw gebruikt. U kunt ook toocustomize deze zoals weergegeven in onderstaande Hallo-sectie.    
3. **Virtuele doelnetwerk:** standaard ASR maakt een nieuw virtueel netwerk in Hallo doelregio met naam 'asr' achtervoegsel heeft. Dit is de toegewezen tooyour Bronnetwerk en wordt gebruikt voor alle toekomstige beveiliging.

    > [!NOTE]
    > [Controleer de gegevens van de netwerken](site-recovery-network-mapping-azure-to-azure.md) tooknow meer informatie over de netwerktoewijzing.

4. **Storage-accounts als doel:** ASR maakt standaard Hallo nieuwe opslag doelaccount mimicking de opslagconfiguratie van de bron-VM. Als storage-account gemaakt door ASR al bestaat, wordt opnieuw gebruikt.

5. **Storage-accounts in de cache:** ASR moet extra opslagruimte account met de naam van cache-opslag in Hallo bron regio. Alle Hallo wijzigingen die plaatsvinden op Hallo Bronmachines worden bijgehouden en toocache opslagaccount verzonden voordat de doellocatie toohello repliceren.

6. **Beschikbaarheidsset:** ASR maakt standaard een nieuwe beschikbaarheidsset Hallo doelregio met naam 'asr' achtervoegsel heeft. Als beschikbaarheidsset gemaakt door ASR al bestaat, wordt opnieuw gebruikt.

7.  **Beleid voor wachtwoordreplicatie:** het Hallo-instellingen voor herstelpunt bewaartermijn geschiedenis en app consistente momentopname upfrequentie definieert. Standaard maakt ASR een nieuw replicatiebeleid voor met de standaardinstellingen van 24 uur voor herstel bewaarperiode en "60 minuten voor de frequentie van app-consistente momentopname te maken.

    ![Replicatie inschakelen](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a>Doelresources aanpassen

Als u wilt dat toochange Hallo standaardwaarden door ASR gebruikt, kunt u het Hallo-instellingen op basis van uw behoeften kunt wijzigen.

1. **Aanpassen:** klikt u op het toochange Hallo standaardwaarden worden gebruikt door ASR.

2. **Doelresourcegroep:** kunt u de resourcegroep Hallo uit Hallo lijst met alle Hallo resourcegroepen in de doellocatie Hallo binnen Hallo abonnement bestaande.

3. **Virtuele doelnetwerk:** vindt u Hallo-lijst van alle Hallo virtueel netwerk in Hallo target-locatie.

4. **Beschikbaarheidsset:** kunt u alleen beschikbaarheid sets instellingen toohello van virtuele machines die deel van de beschikbaarheid in regio bron uitmaken toevoegen.

5. **Doel Storage-accounts:**

![Replicatie inschakelen](./media/site-recovery-replicate-azure-to-azure/customize.PNG) klikt u op **doelbron maken** en replicatie inschakelen


Wanneer virtuele machines zijn beveiligd kunt u Hallo status van de status van de virtuele machines onder controleren **gerepliceerde items**

>[!NOTE]
>Tijdens het Hallo kan tijd van de initiële replicatie er een kans dat status tijd toorefresh duurt en dat er geen uitgevoerd gedurende een bepaalde periode. U kunt klikken Hallo vernieuwen op Hallo Hallo blade tooget Hallo laatste status bovenaan.
>

![Replicatie inschakelen](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a>Volgende stappen
- [Meer informatie](site-recovery-test-failover-to-azure.md) over het uitvoeren van een testfailover.
- [Meer informatie](site-recovery-failover.md) over verschillende soorten failovers, en hoe toorun ze.
- Meer informatie over [met herstelplannen](site-recovery-create-recovery-plans.md) tooreduce RTO.
- Meer informatie over [andere virtuele Azure-machines](site-recovery-how-to-reprotect.md) na een failover.

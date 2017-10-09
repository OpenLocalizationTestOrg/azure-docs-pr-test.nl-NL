---
title: aaaEnable replicatie voor virtuele Azure-machines tooanother Azure-regio met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen moet u tooenable replicatie tooanother Azure-regio voor Azure VM's met behulp van hello Azure Site Recovery-service
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a>Stap 5: Replicatie inschakelen voor Azure Virtual machines


Na het instellen van een [Recovery Services-kluis](azure-to-azure-walkthrough-vault.md), gebruiken deze artikel tooenable replicatie van virtuele machines (VM's), tooanother Azure-regio met [Azure Site Recovery](site-recovery-overview.md). tooenable replicatie, het instellen van de bron en doel-instellingen controleren van het replicatiebeleid Hallo en selecteert u virtuele machines die u wilt dat tooreplicate.

- Wanneer u klaar bent Hallo artikel uw Azure VM's moet worden gerepliceerd als toohello secundaire Azure-regio.
- Eventuele opmerkingen onder Hallo van dit artikel plaatsen of vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> Replicatie van Azure VM is momenteel in preview.


## <a name="select-hello-source"></a>Hallo bron selecteren 

1. Klik in de Recovery Services-kluizen op Hallo kluisnaam > **+ repliceren**.
2. In **bron**, selecteer **Azure - PREVIEW**.
2. In **bronlocatie**, selecteer Hallo bron Azure-regio waarin uw virtuele machines worden uitgevoerd.
3. Selecteer Hallo **virtuele machine van Azure-implementatiemodel** voor virtuele machines: **Resource Manager** of **klassieke**.
4. Selecteer Hallo **resourcegroep** voor Resource Manager-VM's of **cloudservice** voor klassieke virtuele machines.
5. Klik op **OK** toosave Hallo instellingen.

    ![Hallo bron configureren](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a>Hallo virtuele machines selecteren

Site Recovery wordt een lijst met virtuele machines die zijn gekoppeld aan het Hallo-abonnement en de resource-group/cloudservice Hallo opgehaald.

1. In **virtuele Machines**, Hallo VMs u tooreplicate wilt selecteren.
2. Klik op **OK**.

    ![Selecteer de virtuele machines](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a>Instellingen configureren

Site Recovery standaardinstellingen voor Hallo doelregio (op basis van de regio broninstellingen Hallo), bepalingen en Hallo replicatiebeleid:

   - **Doellocatie**: Hallo doelregio gewenste toouse voor herstel na noodgevallen. U wordt aangeraden Hallo-locatie van de Site Recovery-kluis Hallo komt overeen met Hallo target-locatie.
   - **Doelresourcegroep**: Resource groep toowhich Azure VM's in de doelregio Hallo behoort na een failover. Site Recovery maakt standaard een nieuwe resourcegroep in Hallo doelregio met een achtervoegsel 'asr'. 
   - **Virtuele doelnetwerk**: Hallo netwerk in welke Azure VM's in Hallo doelregio geplaatst na een failover worden. Site Recovery maakt standaard een nieuw virtueel netwerk (en subnetten) in de doelregio Hallo met een achtervoegsel 'asr'. Dit netwerk is toegewezen tooyour Bronnetwerk. Houd er rekening mee dat u een specifiek IP-adres na een failover van een virtuele machine kunt toewijzen, als u tooretain Hallo moet dezelfde IP-adres van de bron- en doellocaties Hallo. 
   - **Storage-accounts in de cache**: Site Recovery maakt gebruik van een opslagaccount in Hallo bron regio. Wijzigingen op de bron-VM's verzonden toothis account voordat replicatie toohello target-locatie. 
   - **Storage-accounts zijn gericht**: Site Recovery maakt standaard een nieuw opslagaccount in Hallo doelregio, toomirror Hallo bron VM storage-account.
   -  **Beschikbaarheidssets doel**: Site Recovery maakt standaard een nieuwe beschikbaarheidsset voor de doelregio Hallo met Hallo 'asr' achtervoegsel. 
   - **Replicatie-beleidsnaam**: de naam van beleid.
   - **Herstel bewaarperiode**: standaard Site Recovery herstelpunten blijft gedurende 24 uur. U kunt een waarde tussen 1 en 72 uur configureren.
   - **App-consistente momentopname frequentie**: standaard Site Recovery maakt een app-consistente momentopname elke 4 uur. U kunt een waarde tussen 1 en 12 uur. Gegevens worden continu gerepliceerd:
    - Crashconsistent herstelpunten onderhouden consistente gegevens schrijven-volgorde wanneer gemaakt. Dit type herstelpunt is meestal voldoende als uw app ontworpen toorecover van een crash zonder gegevensinconsistenties
    - Crashconsistente herstelpunten worden gegenereerd om de paar minuten. Met deze punten herstel toofail via en herstel biedt uw virtuele machines een herstel Herstelpuntdoel (RPO) in de volgorde Hallo van minuten.
    - Toepassingsconsistente herstelpunten (in aanvulling toowrite volgorde consistentie) Zorg ervoor dat actief apps alle bewerkingen voltooid en buffers toodisk (toepassing stilleggen leegmaken). U wordt aangeraden dat u deze herstelpunten gebruiken voor database-apps, zoals SQL Server, Oracle en Exchange.
        
    ![Instellingen configureren](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a>Instellingen wijzigen

Als u toomodify doel- en replicatie beleidsinstellingen wilt, Hallo te volgen:

1. tooview of doelinstellingen wijzigen, klikt u op **instellingen**.
2. toooverride hello doel standaardinstellingen, en klik op **aanpassen**. U kunt een doelresourcegroep, virtueel netwerk, beschikbaarheidsset en doel storage-account opgeven. U kunt alleen beschikbaarheidssets toevoegen als virtuele machines deel van een set in Hallo bron regio uitmaken.

    ![Instellingen configureren](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. Klik op toooverride replicatie-instellingen voor herstelpunten en toepassingsconsistente momentopnamen **aanpassen** volgende te**replicatiebeleid**.
 
    ![Instellingen configureren](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. toostart inrichting Hallo doelresources, klikt u op **doelresources maken**. Inrichting duurt een minuut. Sluit de blade Hallo niet tijdens het inrichten of hebt u toostart via.




## <a name="enable-replication"></a>Replicatie inschakelen

1. In **instellingen**, klikt u op **replicatie inschakelen**. Hierdoor kan de initiële replicatie van Hallo virtuele machines die u hebt geselecteerd. Status van de initiële replicatie kan sommige toorefresh tijd duren. Klik op **vernieuwen** tooget Hallo laatste status.

2. U kunt de voortgang van Hallo volgen **beveiliging inschakelen** taak **instellingen** > **taken** > **Site Recovery-taken**.

3. In **instellingen** > **gerepliceerde Items**, kunt u weergeven Hallo status van virtuele machines en Hallo initiële replicatie uitgevoerd. Klik op Hallo VM toodrill omlaag in de instellingen ervan.



## <a name="next-steps"></a>Volgende stappen

Ga te[stap 6: een testfailover uitvoeren](azure-to-azure-walkthrough-test-failover.md)

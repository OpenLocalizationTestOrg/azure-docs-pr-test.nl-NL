---
title: aaaSet van een beleid voor wachtwoordreplicatie voor Hyper-V-replicatie tooa secundaire site met Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven hoe tooset van een beleid voor Hyper-V VM replicatie tooa secundaire VMM-site met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5d9b79cf-89f2-4af9-ac8e-3a32ad8c6c4d
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 6d008e3bb3fa0b666e91678cf6de3693dd712ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy"></a>Stap 8: Een replicatiebeleid instellen

Na het configureren van [netwerktoewijzing](vmm-to-vmm-walkthrough-network-mapping.md), gebruik dit artikel tooset van een beleid voor wachtwoordreplicatie voor Hyper-V virtuele machine (VM) replicatie tooa secundaire site met behulp van [Azure Site Recovery](site-recovery-overview.md).

Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Voordat u begint

- Wanneer u een beleid voor wachtwoordreplicatie maakt, moet alle hosts met behulp van beleid Hallo hetzelfde besturingssysteem hebt Hallo. Hallo VMM-cloud Hyper-V-hosts met verschillende versies van Windows Server kan bevatten, maar in dit geval moet u meerdere beleidsregels voor replicatie.
- U kunt Hallo offline initiële replicatie uitvoeren.

## <a name="configure-replication-settings"></a>Replicatie-instellingen configureren

1. toocreate een nieuw replicatiebeleid, klikt u op **infrastructuur voorbereiden** > **replicatie-instellingen** > **+ maken en koppelen**.

    ![Netwerk](./media/vmm-to-vmm-walkthrough-replication/gs-replication.png)
2. Geef in **Beleid maken en koppelen** een beleidsnaam op. Hallo bron en doel-type moet **Hyper-V**.
3. In **versie van Hyper-V-host**, selecteer welk besturingssysteem wordt uitgevoerd op Hallo host.
4. In **verificatietype** en **verificatiepoort**, opgeven hoe verkeer wordt geverifieerd tussen primaire Hallo en herstel Hyper-V-hostservers. Selecteer **certificaat** tenzij u beschikken over een werkende Kerberos-omgeving. Azure Site Recovery configureert automatisch certificaten voor HTTPS-verificatie. U hoeft niet toodo iets handmatig. Standaard wordt poort 8083 en 8084 (voor certificaten) in Hallo Windows Firewall op Hallo Hyper-V-hostservers worden geopend. Als u selecteert **Kerberos**, een Kerberos-ticket wordt gebruikt voor wederzijdse verificatie van Hallo host-servers. Houd er rekening mee dat deze instelling is alleen relevant voor Hyper-V-host-servers waarop Windows Server 2012 R2.
5. In **Kopieerfrequentie**, geef aan hoe vaak u tooreplicate deltagegevens na de initiële replicatie van hello (elke 30 seconden, 5 of 15 minuten).
6. In **herstel bewaarperiode**, in uren opgeven hoe lang de retentieperiode Hallo wordt worden voor elk herstelpunt. Beveiligde machines kunnen worden hersteld tooany punt in een venster.
7. In **App-consistente momentopname frequentie**, opgeven hoe vaak (1-12 uur) herstelpunten met toepassingsconsistente momentopnamen worden gemaakt. Hyper-V gebruikt twee soorten momentopnamen: standaardmomentopnamen waarmee een incrementele momentopname van Hallo volledige virtuele machine en een toepassingsconsistente momentopnamen waarmee een momentopname van een punt in tijd van de toepassingsgegevens Hallo in Hallo virtuele machine. Toepassingsconsistente momentopnamen gebruiken Volume Shadow Copy Service (VSS) tooensure die toepassingen zich in een consistente status wanneer Hallo momentopname wordt gemaakt. Als u toepassingsconsistente momentopnamen inschakelt, wordt het Hallo-prestaties van toepassingen die worden uitgevoerd op virtuele bronmachines beïnvloeden. Zorg ervoor dat Hallo-waarde lager dan Hallo aantal aanvullende herstelpunten dat u configureert.
8. In **gegevensoverdracht compressie**, opgeven of de gerepliceerde gegevens die worden overgedragen moeten worden gecomprimeerd.
9. Selecteer **replica verwijderen VM**, toospecify die Hallo replica virtuele machine moet worden verwijderd als u beveiliging voor Hallo bron-VM uitschakelt. Als u deze instelling inschakelt wanneer u beveiliging voor Hallo bron-VM wordt deze verwijderd uit de Site Recovery-console Hallo uitschakelt, Site Recovery-instellingen voor Hallo VMM worden verwijderd uit de VMM-console Hallo en Hallo replica is verwijderd.
10. In **initiële replicatiemethode**, als u via netwerk hello repliceert, opgeven of toostart Hallo initiële replicatie of plannen. toosave netwerkbandbreedte, kunt u tooschedule deze buiten de drukste tijden. Klik vervolgens op **OK**.

     ![Beleid voor replicatie](./media/vmm-to-vmm-walkthrough-replication/gs-replication2.png)
11. Wanneer u een nieuw beleid maakt is deze automatisch gekoppeld aan Hallo VMM-cloud. In **replicatiebeleid**, klikt u op **OK**. U kunt aanvullende VMM-Clouds (en Hallo virtuele machines erin) koppelen aan dit replicatiebeleid in **replicatie** > beleidsnaam > **VMM-Cloud koppelen**.

     ![Beleid voor replicatie](./media/vmm-to-vmm-walkthrough-replication/policy-associate.png)



## <a name="prepare-for-offline-initial-replication"></a>Voorbereiden voor de offline initiële replicatie

U kunt doen offline replicatie voor Hallo initiële gegevens kopiëren. U kunt dit als volgt voorbereiden:

* Op de bronserver hello geeft u de padlocatie van een van welke Hallo exporteren van gegevens wordt gehouden. Volledig beheer voor machtigingen voor NTFS en deelmachtigingen toohello VMM-service op Hallo exportpad toewijzen. Op de doelserver hello geeft u een locatie waarvan Hallo gegevens importeren wordt uitgevoerd. Hallo dezelfde machtigingen voor dit pad importeren toewijzen.
* Als hello importeren of exporteren pad wordt gedeeld, Administrator, Hoofdgebruikers, Print Operators of Server Operator groepslidmaatschap voor Hallo VMM-serviceaccount op de externe computer Hallo toewijzen welke Hallo gedeeld zich bevindt.
* Als u geen Run As-accounts tooadd hosts, op Hallo importeren en exporteren van paden, lezen toewijzen en schrijfmachtigingen toohello-Run As-accounts in VMM.
* Hallo importeren en exporteren van shares niet moet zich bevinden op een computer die wordt gebruikt als een Hyper-V-hostserver, omdat de loopback-configuratie wordt niet ondersteund door Hyper-V.
* In Active Directory is op elke Hyper-V-hostserver die bevat virtuele machines die u wilt dat tooprotect, inschakelen en configureren van beperkte delegering tootrust Hallo externe computers op welke Hallo importeren en exporteren paden zich bevinden, als volgt:
  1. Open op de domeincontroller hello, **Active Directory: gebruikers en Computers**.
  2. Klik in de consolestructuur Hallo **DomainName** > **Computers**.
  3. Klik met de rechtermuisknop Hallo Hyper-V-host-servernaam > **eigenschappen**.
  4. Op Hallo **delegering** tabblad **deze computer alleen overdracht toospecified services**.
  5. Klik op **elk verificatieprotocol voor gebruiken**.
  6. Klik op **toevoegen** > **gebruikers en Computers**.
  7. Hallo-typenaam van Hallo-computer die als host fungeert voor Hallo exportpad > **OK**. Hallo-lijst met beschikbare services, Hallo CTRL-toets ingedrukt en klik op **cifs** > **OK**. Herhaal voor Hallo naam van de computer Hallo dat pad hosts Hallo importeren. Herhaal zo nodig voor extra Hyper-V-hostservers.



## <a name="next-steps"></a>Volgende stappen

Ga te[stap 9: replicatie inschakelen](vmm-to-vmm-walkthrough-enable-replication.md).

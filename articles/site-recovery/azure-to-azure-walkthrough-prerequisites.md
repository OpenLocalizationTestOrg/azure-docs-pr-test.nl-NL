---
title: starten van de replicatie van Azure Virtual machines tooanother regio aaaBefore | Microsoft-Docs
description: Geeft een overzicht van Hallo stappen die u nodig hebt tootake voordat de virtuele Azure-machines repliceren tussen Azure-regio's, met behulp van hello Azure Site Recovery-service
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 7fa633075eeb52d0c184a1dd8d53ccc15644f518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-before-you-start"></a>Stap 2: Voordat u begint

Nadat u hebt doorgenomen Hallo [architectuur](azure-to-azure-walkthrough-architecture.md) voor het repliceren van virtuele Azure-machines (VM's) tussen Azure-regio's [Azure Site Recovery](site-recovery-overview.md), gebruikt u de vereisten van dit artikel tooverify. 

- Wanneer u klaar bent met Hallo artikel, moet u een duidelijk inzicht in wat is er nodig toomake Hallo implementatie werken en Hallo vereiste stappen hebt voltooid.
- Eventuele opmerkingen onder Hallo van dit artikel plaatsen of vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
>
> Replicatie van Azure VM is momenteel in preview.



## <a name="support-recommendations"></a>Aanbevelingen voor ondersteuning

Bekijk Hallo in de volgende tabel.

**Onderdeel** | **Vereiste**
--- | ---
**Recovery Services-kluis** | U wordt aangeraden dat u een Recovery Services-kluis maken in Hallo doel-Azure-regio wilt u toouse voor herstel na noodgevallen. Bijvoorbeeld, als u tooreplicate bronmachines in VS-Oost tooCentral VS wilt, maken Hallo kluis in VS-midden.
**Azure-abonnement** | Uw Azure-abonnement moet zijn ingeschakeld toocreate VM's in Hallo target-locatie die u toouse als Hallo disaster recovery regio wilt. Neem contact op met ondersteuning tooenable Hallo vereist quota.
**Doel regio capaciteit** | Hallo-abonnement hebt in Hallo doel-Azure-regio, voldoende capaciteit voor virtuele machines, opslagaccounts en netwerkonderdelen.
**Storage** | Gebruik Hallo [richtlijnen voor opslag](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) voor uw Azure Virtual machines tooavoid prestatieproblemen met de gegevensbron.<br/><br/> Storage-accounts moeten zich in Hallo dezelfde regio als Hallo-kluis.<br/><br/> Accounts in het midden- en Zuid, India toopremium kan niet worden gerepliceerd.<br/><br/> Als u replicatie met standaardinstellingen Hallo implementeert, maakt Site Recovery Hallo vereist storage-accounts op basis van Hallo bron configuratie. Als u instellingen aanpassen, volgt u Hallo [schaalbaarheidsdoelen voor VM-schijven](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
**Netwerken** | Uitgaande verbinding tooallow van Azure VM's, moet u voor specifieke URL's of het IP-adresbereiken.<br/><br/> Netwerkaccounts moeten in Hallo dezelfde regio als Hallo-kluis. 
**Azure VM** | Zorg ervoor dat de meest recente basiscertificaten Hallo allemaal op Hallo Windows of Linux Azure VM. Als ze niet, niet kunnen tooregister Hallo VM in Site Recovery vanwege beveiligingsbeperkingen.
**Azure-gebruikersaccount** | Uw Azure gebruikersaccount moet toohave bepaalde [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicatie van een virtuele machine van Azure.

Ophalen van een volledige lijst met ondersteuningsvereisten in Hallo [ondersteuningsmatrix](site-recovery-support-matrix-azure-to-azure.md)


## <a name="set-permissions-on-hello-account"></a>Machtigingen instellen op Hallo-account

1. Meer informatie over Hallo [machtigingen](site-recovery-role-based-linked-access-control.md) u nodig hebt voor replicatie.
2. Volg deze [instructies](../active-directory/role-based-access-control-configure.md#add-access) tooadd machtigingen.


## <a name="verify-target-resources"></a>Controleer of de doelresources

1. Inschakelen van uw Azure-abonnement tooallow toocreate virtuele machines in Hallo gericht regio toouse voor herstel na noodgevallen dat u wilt dat toouse als Hallo disaster recovery regio. Neem contact op met ondersteuning tooenable Hallo vereist quota.
2. Zorg ervoor dat uw abonnement heeft onvoldoende bronnen tooenable virtuele machines met grootten die overeenkomen met uw virtuele bronmachines. Standaard bij het instellen van de replicatie van Site Recovery uitgelicht Hallo even groot zijn voor Hallo doel VM of Hallo dichtstbijzijnde grootte. Meer informatie over [probleemoplossing](site-recovery-azure-to-azure-troubleshoot-errors.md#azure-resource-quota-issues-error-code-150097) resources zijn gericht.

## <a name="verify-azure-vm-certificates"></a>Controleer of de certificaten van de virtuele machine in Azure

1. Controleer of alle Hallo nieuwste basiscertificaten op Hallo Windows of Linux-machines die u wilt dat tooreplicate aanwezig zijn. Als de meest recente basiscertificaten Hallo niet aanwezig zijn, niet Hallo VM geregistreerde tooSite herstel vanwege toosecurity beperkingen worden.
2. Windows virtuele machines, Hallo te volgen:

    - Installeer alle Hallo meest recente Windows-updates op Hallo VM zodat alle Hallo vertrouwde basiscertificaten op Hallo machine.
    - Volg Hallo standaard Windows Update-proces en certificaat updateproces in uw organisatie, tooget Hallo nieuwste basiscertificaten en bijgewerkte CRL, op Hallo virtuele machines in een omgeving zonder verbinding.
3. Ga als volgt Hallo richtlijnen bij uw Linux distributor tooget Hallo nieuwste vertrouwde basiscertificaten en Hallo laatste certificaatintrekkingslijst op Hallo VM voor Linux-machines. Meer informatie over [probleemoplossing](site-recovery-azure-to-azure-troubleshoot-errors.md#trusted-root-certificates-error-code-151066) vertrouwde basis-problemen.


## <a name="next-steps"></a>Volgende stappen

Ga te[stap 3: plannen netwerken](azure-to-azure-walkthrough-network.md) tooset uitgaande connectiviteit.

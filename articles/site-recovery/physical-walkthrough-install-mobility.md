---
title: aaaInstall hello Mobility-service voor replicatie van fysieke server tooAzure | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooinstall Hallo Mobility-service-agent op de fysieke servers repliceren tooAzure met hello Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a>Stap 9: Hallo Mobility-service installeren


Dit artikel wordt beschreven hoe tooinstall Hallo Mobility-service zijn bij het repliceren van lokale Windows-/ Linux fysieke servers tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.

Hallo Mobility-service worden vastgelegd op een machine weggeschreven en stuurt ze toohello processerver. Het moet worden geïnstalleerd op elke server die u wilt dat tooreplicate tooAzure.

U kunt Hallo Mobility-service handmatig te installeren of met behulp van een push-installatie van Hallo Site Recovery-server wanneer replicatie is ingeschakeld, of verwerken met een hulpprogramma zoals System Center Configuration Manager. Als u push-installatie gebruikt, wordt Hallo-service is geïnstalleerd op Hallo server wanneer u replicatie inschakelt.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>De installatie handmatig uitvoeren

1. Controleer de Hallo [vereisten](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) voor handmatige installatie.
2. Ga als volgt [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) voor handmatige installatie met Hallo-portal.
3. Als u liever tooinstall vanaf de opdrachtregel hello, voert u de [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Installeren vanaf de processerver Hallo

Als u wilt dat toopush Hallo installatie van de Mobility-service van de processerver Hallo wanneer u replicatie voor een machine inschakelt, moet u een account dat kan worden gebruikt door Hallo proces tooaccess Hallo-servercomputer. Hallo-account wordt alleen gebruikt voor Hallo push-installatie.

1. Als u een account dat nog niet hebt gemaakt, doen met behulp van deze richtlijnen:

    - U kunt een domein of lokale account gebruiken
    - Voor Windows, als u niet een domeinaccount, moet u toodisable externe gebruiker toegangsbeheer op Hallo lokale machine. dit in Hallo registreert onder toodo **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, Hallo DWORD-vermelding toevoegen **LocalAccountTokenFilterPolicy**, met een waarde van 1.
    - Als u tooadd Hallo register-item voor Windows vanuit een CLI wilt, typt u:

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - Voor Linux moet Hallo account basiscertificaat op de bronserver Linux Hallo.

2. Volg [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) als u wilt dat toopush Hallo Mobility-service op Windows of Linux-machines.

## <a name="other-installation-methods"></a>Andere installatiemethoden

- [Meer informatie over](site-recovery-install-mobility-service-using-sccm.md) Hallo Mobility-service met Configuration Manager installeren
- [Meer informatie over](site-recovery-automate-mobility-service-install.md) installeren met Azure Automation DSC.


## <a name="next-steps"></a>Volgende stappen

Ga te[stap 10: replicatie inschakelen](physical-walkthrough-enable-replication.md)

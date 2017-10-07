---
title: aaaInstall Mobility-Service (VMware of fysieke tooAzure) | Microsoft Docs
description: Meer informatie over hoe tooinstall Hallo Mobility-Service agent tooprotect uw lokale computers.
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: f7836e6b35d3838bae1eff927838ce4b245b9f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a>Installeren van de Mobility-Service (VMware of fysieke tooAzure)
Azure Site Recovery Mobility-Service gegevens schrijfbewerkingen op een computer vastlegt en stuurt ze toohello processerver. Mobility-Service tooevery computer (VMware VM of fysieke server die u tooreplicate tooAzure wilt) implementeren. U kunt de Mobility-Service toohello servers dat u met behulp van de volgende methoden Hallo tooprotect wilt implementeren:


* [Installeren van de Mobility-Service met behulp van software-implementatieprogramma's zoals System Center Configuration Manager](site-recovery-install-mobility-service-using-sccm.md)
* [Installeren van de Mobility-Service met behulp van Azure Automation en Desired State Configuration (DSC automatisering)](site-recovery-automate-mobility-service-install.md)
* [Mobility-Service handmatig te installeren met behulp van Hallo grafische gebruikersinterface (GUI)](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [Installeer de Mobility-Service handmatig bij een opdrachtprompt](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [Installeren van de Mobility-Service met push-installatie van Azure Site Recovery](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> Vanaf versie 9.7.0.0, op virtuele machines (VM's) van Windows hello Mobility-Service installeert installatieprogramma ook Hallo meest recente beschikbare [Azure VM-agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent). Wanneer een computer via tooAzure mislukt Hallo-computer voldoet aan de vereisten voor het gebruik van een VM-extensie Hallo agent-installatie.

## <a name="prerequisites"></a>Vereisten
Deze vereiste stappen voltooien voordat u Mobility-Service handmatig op uw server installeren:
1. Meld u aan de configuratieserver tooyour en open een opdrachtpromptvenster als administrator.
2. Hallo directory toohello bin-map wijzigen en vervolgens een wachtwoordzin-bestand maken:

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. Hallo wachtwoordzin bestand opslaan op een veilige locatie. Tijdens de installatie van de Mobility-Service Hallo Hallo-bestand wordt gebruikt.
4. Installatieprogramma's van Mobility-Service voor alle ondersteunde besturingssystemen zijn in Hallo %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository map.

### <a name="mobility-service-installer-to-operating-system-mapping"></a>Systeemtoewijzing voor installatieprogramma voor besturingssystemen van Mobility-Service

| Naam van het installatiebestand sjabloon| Besturingssysteem |
|---|--|
|Microsoft ASR\_UA\*Windows\*release.exe | Windows Server 2008 R2 SP1 (64-bits) </br> WindowsServer 2012 (64-bits) </br> Windows Server 2012 R2 (64-bits) |
|Microsoft ASR\_UA\*RHEL6 64*release.tar.gz| Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6,8 (alleen 64-bits) </br> CentOS 6.4, 6.5, 6.6, 6.7, 6,8 (alleen 64-bits) |
|Microsoft ASR\_UA\*RHEL7 64\*release.tar.gz | Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (alleen 64-bits) </br> CentOS 7.0, 7.1, 7.2 (alleen 64-bits)</br> CentOs 7.3 (alleen migratie) |
|Microsoft ASR\_UA\*SLES11-SP3-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP3 (alleen 64-bits)|
|Microsoft ASR\_UA\*SLES11-SP4-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP4 (alleen 64-bits)|
|Microsoft ASR\_UA\*OL6 64\*release.tar.gz | Oracle Enterprise Linux 6.4, 6.5 (alleen 64-bits)|
|Microsoft ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz | Ubuntu Linux 14.04 (alleen 64-bits)|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a>Mobility-Service handmatig te installeren met behulp van Hallo GUI

>[!IMPORTANT]
> Als u een **configuratieserver** tooreplicate **Azure IaaS virtuele machines** van een Azure-abonnement/gebied tooanother vervolgens **Hallo opdrachtregelprogramma gebaseerde installatie gebruiken**  methode

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a>Installeer de Mobility-Service handmatig bij een opdrachtprompt

### <a name="command-line-installation-on-a-windows-computer"></a>Opdrachtregelparameters voor de installatie op een Windows-computer
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a>Opdrachtregelparameters voor de installatie op een Linux-computer
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a>Installeren van de Mobility-Service met push-installatie van Azure Site Recovery
een push-installatie van Mobility-Service met behulp van Site Recovery toodo, alle doelcomputers moeten voldoen aan Hallo vereisten te volgen.

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
Nadat de Mobility-Service is geïnstalleerd, in hello Azure-portal, selecteert u Hallo **repliceren** knop toostart beveiligen van deze virtuele machines.

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a>Verwijder de Mobility-Service op een computer met Windows Server
Gebruik een van de Hallo methoden toouninstall Mobility-Service op een Windows Server-computer te volgen.

### <a name="uninstall-by-using-hello-gui"></a>Verwijder met behulp van Hallo GUI
1. Selecteer in het Configuratiescherm **programma's**.
2. Selecteer **Microsoft Azure Site Recovery Mobility Service/hoofddoelserver**, en selecteer vervolgens **verwijderen**.

### <a name="uninstall-at-a-command-prompt"></a>Bij een opdrachtprompt verwijderen
1. Open een opdrachtpromptvenster als administrator.
2. toouninstall Mobility-Service Hallo volgende opdracht uitvoeren:

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a>Verwijder de Mobility-Service op een Linux-computer
1. Op uw Linux-server, moet u zich aanmelden als een **hoofdmap** gebruiker.
2. Ga in een terminal te/gebruiker/local/ASR.
3. toouninstall Mobility-Service Hallo volgende opdracht uitvoeren:

```
uninstall.sh -Y
```

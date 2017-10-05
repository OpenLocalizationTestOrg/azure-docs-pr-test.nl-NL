---
title: Installeren van de Mobility-Service (VMware of fysieke naar Azure) | Microsoft Docs
description: Informatie over het installeren van de Mobility-Service-agent voor het beveiligen van uw lokale computers.
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
ms.openlocfilehash: 848284f37ae2470a169d8f8a8c9c0bb5b926abe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="install-mobility-service-vmware-or-physical-to-azure"></a>Installeren van de Mobility-Service (VMware of fysieke naar Azure)
Azure Site Recovery Mobility-Service gegevens schrijfbewerkingen op een computer vastlegt en ze doorstuurt naar de processerver. Implementeer Mobility-Service op elke computer (VMware VM of fysieke server) die u wilt repliceren naar Azure. U kunt de Mobility-Service implementeren op de servers die u beveiligen wilt met behulp van de volgende methoden:


* [Installeren van de Mobility-Service met behulp van software-implementatieprogramma's zoals System Center Configuration Manager](site-recovery-install-mobility-service-using-sccm.md)
* [Installeren van de Mobility-Service met behulp van Azure Automation en Desired State Configuration (DSC automatisering)](site-recovery-automate-mobility-service-install.md)
* [Mobility-Service handmatig te installeren met behulp van de grafische gebruikersinterface (GUI)](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [Installeer de Mobility-Service handmatig bij een opdrachtprompt](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [Installeren van de Mobility-Service met push-installatie van Azure Site Recovery](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> Vanaf versie 9.7.0.0, op Windows virtuele machines (VM's), de Mobility-Service installeert installatieprogramma ook de meest recente beschikbare [Azure VM-agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent). Als een computer failover naar Azure wordt uitgevoerd, is de computer voldoet aan de vereisten voor het gebruik van een VM-extensie agentinstallatie.

## <a name="prerequisites"></a>Vereisten
Deze vereiste stappen voltooien voordat u Mobility-Service handmatig op uw server installeren:
1. Aanmelden bij uw configuratieserver en open een opdrachtpromptvenster als administrator.
2. Wijzig de directory in de map bin en vervolgens een wachtwoordzin-bestand maken:

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. Sla het bestand wachtwoordzin op een veilige locatie. Het bestand wordt gebruikt tijdens de installatie van de Mobility-Service.
4. Installatieprogramma's van Mobility-Service voor alle ondersteunde besturingssystemen zijn in de map %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository.

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


## <a name="install-mobility-service-manually-by-using-the-gui"></a>Mobility-Service handmatig te installeren met behulp van de gebruikersinterface

>[!IMPORTANT]
> Als u een **configuratieserver** repliceren **Azure IaaS virtuele machines** van één Azure abonnement/regio naar een andere vervolgens **gebruikt u de installatie vanaf de opdrachtregel op basis van** methode

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a>Installeer de Mobility-Service handmatig bij een opdrachtprompt

### <a name="command-line-installation-on-a-windows-computer"></a>Opdrachtregelparameters voor de installatie op een Windows-computer
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a>Opdrachtregelparameters voor de installatie op een Linux-computer
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a>Installeren van de Mobility-Service met push-installatie van Azure Site Recovery
Alle doelcomputers moeten voldoen aan de volgende vereisten hiervoor een push-installatie van Mobility-Service met behulp van Site Recovery.

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
Nadat de Mobility-Service is geïnstalleerd, in de Azure portal, selecteert u de **repliceren** knop om te beginnen met het beveiligen van deze virtuele machines.

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a>Verwijder de Mobility-Service op een computer met Windows Server
Gebruik een van de volgende methoden om het verwijderen van de Mobility-Service op een computer met Windows Server.

### <a name="uninstall-by-using-the-gui"></a>Verwijder met behulp van de gebruikersinterface
1. Selecteer in het Configuratiescherm **programma's**.
2. Selecteer **Microsoft Azure Site Recovery Mobility Service/hoofddoelserver**, en selecteer vervolgens **verwijderen**.

### <a name="uninstall-at-a-command-prompt"></a>Bij een opdrachtprompt verwijderen
1. Open een opdrachtpromptvenster als administrator.
2. Voer de volgende opdracht voor het verwijderen van de Mobility-Service:

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a>Verwijder de Mobility-Service op een Linux-computer
1. Op uw Linux-server, moet u zich aanmelden als een **hoofdmap** gebruiker.
2. Ga in een terminal naar /user/local/ASR.
3. Voer de volgende opdracht voor het verwijderen van de Mobility-Service:

```
uninstall.sh -Y
```

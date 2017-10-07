---
title: " Een Scale-out processerver beheren in Azure Site Recovery | Microsoft Docs"
description: Dit artikel wordt beschreven hoe tooset en beheren van een Scale-out processerver in Azure Site Recovery.
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
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a>Een Scale-out processerver beheren

Scale-out processerver fungeert als een coördinator voor gegevensoverdracht tussen Hallo Site Recovery services en uw on-premises infrastructuur. Dit artikel wordt beschreven hoe u kunt instellen, configureren en beheren van de processerver van een Scale-out.

## <a name="prerequisites"></a>Vereisten
Hallo hieronder vindt u Hallo aanbevolen hardware, software en netwerk configuratie vereist tooset van een Scale-out proces-Server.

> [!NOTE]
> [Capaciteitsplanning](site-recovery-capacity-planner.md) is een belangrijke stap tooensure die u Hallo processerver Scale-out met een configuratie die suites implementeert uw vereisten voor het laden. Lees meer over [kenmerken schalen voor een Scale-out processerver](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a>Hallo Scale-out processerver software downloaden
1. Meld u aan toohello Azure-portal en blader tooyour Recovery Services-kluis.
2. Te bladeren**Site Recovery-infrastructuur** > **configuratieservers** (onder voor VMware en fysieke Machines).
3. Selecteer uw server configuration toodrill omlaag in de detailpagina Hallo configuratieserver.
4. Klik op Hallo **+ processerver** knop.
5. In Hallo **toevoegen processerver** pagina **implementeren een Scale-out processerver lokale** optie uit Hallo **kiezen waar u toodeploy uw processerver** vervolgkeuzelijst.

  ![Pagina Servers toevoegen](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. Klik op Hallo **Hallo downloaden van Microsoft Azure Site Recovery Unified Setup** koppeling toodownload Hallo meest recente versie van de installatie van de processerver Hallo Scale-out.

  > [!WARNING]
  Hallo versie van de processerver Scale-out moet gelijk zijn tooor minder dan Hallo configuratieserver versie uitvoert in uw omgeving. Een eenvoudige manier tooensure versiecompatibiliteit is toouse Hallo dezelfde installatieprogramma bits dat u recent tooinstall of bij te werken de configuratieserver gebruikte.

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a>Installeren en registreren van de processerver Scale-out van de gebruikersinterface
Als u tooscale uit uw implementatie dan 200 bronmachines, of een totale dagelijkse verloop in verhouding van meer dan 2 TB, moet u extra proces servers toohandle Hallo-netwerkverkeer.

Controleer Hallo [grootte aanbevelingen voor het processervers](#size-recommendations-for-the-process-server), en volg deze instructies tooset Hallo proces server. Na het instellen van Hallo-server, die u migreert bron machines toouse deze.

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a>Installeren en registreren van een Scale-out processerver met opdrachtregel

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a>Voorbeeld van gebruik
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a>Scale-out processerver installatieprogramma opdrachtregelargumenten.
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a>Maak een configuratiebestand van de proxy-instellingen
De parameter ProxySettingsFilePath Neem een bestand als invoer. Bestand met behulp van Hallo volgende formatteren en geven deze als invoerparameter ProxySettingsFilePath maken.
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a>Proxy-instellingen voor de processerver Scale-out wijzigen
1. Meld u aan bij de processerver van uw Scale-out.
2. Open een opdrachtvenster Admin PowerShell.
3. Hallo volgende opdracht uitvoeren
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. Naast bladeren toohello directory **%PROGRAMDATA%\ASR\Agent** en Voer Hallo de volgende opdracht
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a>Een Scale-out processerver opnieuw te registreren
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* Naast open een opdrachtprompt beheerder.
* Bladeren door mappen toohello **%PROGRAMDATA%\ASR\Agent** en voer de opdracht Hallo

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a>Upgraden van een Scale-out processerver
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a>Buiten gebruik stellen van een Scale-out processerver
1. Zorg ervoor dat:
  - Status van de verbinding van de configuratieserver wordt weergegeven als **verbonden** in hello Azure-portal
  - Processerver is wel toocommunicate met Hallo configuratieserver.
2. De processerver toohello aanmelden als beheerder
3. Open het Configuratiescherm > programma > programma's verwijderen
4. Hallo's verwijderen in Hallo reeks gegeven te volgen:
  * Microsoft Azure Site Recovery-configuratieserver Server-proces
  * Microsoft Azure Site Recovery configuratie Server afhankelijkheden
  * Microsoft Azure Recovery Services-agent

Het kan tot too15 minuten duren voordat Hallo processerver verwijdering tooreflect in hello Azure-portal.

  > [!NOTE]
  Als de processerver Hallo niet kan toocommunicate Hello configuratieserver is (status in de portal verbinding wordt verbroken), moet u toofollow Hallo volgende stappen toopurge deze van Hallo configuratieserver.

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a>De registratie van een niet-verbonden processerver van Scale-out van een configuratie-Server

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a>Vereisten voor een Scale-out processerver schaling

| **Aanvullende processerver** | **Cachegrootte van de schijf** | **Snelheid van de gegevens wijzigen** | **Beveiligde machines** |
| --- | --- | --- | --- |
|4 vcpu's (2-sockets * 2 kernen @ 2,5 GHz), 8 GB geheugen |300 GB |250 GB of minder |85 of minder machines repliceren. |
|8 vcpu's (2-sockets * 4 kernen @ 2,5 GHz), 12 GB geheugen |600 GB |250 GB too1 TB |Repliceren tussen 85 150-machines. |
|12 vcpu's (2-sockets * 6 kernen @ 2,5 GHz) 24 GB geheugen |1 TB |1 TB too2 TB |Repliceren tussen 150 225 machines. |

---
title: " Een configuratieserver beheren in Azure Site Recovery | Microsoft Docs"
description: Dit artikel wordt beschreven hoe tooset en beheren van een Server Configuration.
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
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a>Een configuratieserver beheren

Configuratieserver fungeert als een coördinator tussen Hallo Site Recovery services en uw on-premises infrastructuur. Dit artikel wordt beschreven hoe u kunt instellen, configureren en beheren Hallo configuratieserver.

## <a name="prerequisites"></a>Vereisten
Hallo volgen Hallo minimale hardware, software en netwerk configuratie vereist tooset van een configuratie-Server.

> [!NOTE]
> [Capaciteitsplanning](site-recovery-capacity-planner.md) is een belangrijke stap tooensure die u Hallo configuratieserver met een configuratie die suites implementeert uw vereisten voor het laden. Lees meer over [formaat van de vereisten voor een Server Configuration](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a>Hallo configuratieserver software downloaden
1. Meld u aan toohello Azure-portal en blader tooyour Recovery Services-kluis.
2. Te bladeren**Site Recovery-infrastructuur** > **configuratieservers** (onder voor VMware en fysieke Machines).

  ![Pagina Servers toevoegen](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. Klik op Hallo **+ Servers** knop.
4. Op Hallo **Server toevoegen** pagina, klikt u op Hallo downloaden knop toodownload Hallo registratiesleutel. U moet deze sleutel tijdens Hallo configuratieserver installatie tooregister met Azure Site Recovery-service.
5. Klik op Hallo **Hallo downloaden van Microsoft Azure Site Recovery Unified Setup** koppeling toodownload Hallo meest recente versie van Hallo configuratieserver.

  ![Downloadpagina](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  Meest recente versie van Hallo configuratieserver kan worden gedownload rechtstreeks vanuit [downloadpagina van Microsoft Download Center](http://aka.ms/unifiedsetup)

## <a name="installing-and-registering-a-configuration-server-from-gui"></a>Installeren en registreren van een configuratieserver uit de gebruikersinterface
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a>Installeren en registreren van een configuratie-Server met behulp van de opdrachtregel

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a>Voorbeeld van gebruik
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a>Configuratie Server installatieprogramma opdrachtregelargumenten.
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a>Maak een MySql-bestand voor referenties
De parameter MySQLCredsFilePath Neem een bestand als invoer. Hallo-bestand met behulp van Hallo volgende formatteren en geven deze als invoerparameter MySQLCredsFilePath maken.
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a>Maak een configuratiebestand van de proxy-instellingen
De parameter ProxySettingsFilePath Neem een bestand als invoer. Hallo-bestand met behulp van Hallo volgende formatteren en geven deze als invoerparameter ProxySettingsFilePath maken.

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a>Proxy-instellingen voor de configuratieserver wijzigen
1. Aanmelding tooyour configuratieserver.
2. Start Hallo cspsconfigtool.exe met Hallo-snelkoppeling op uw.
3. Klik op Hallo **kluis registratie** tabblad.
4. Download een nieuw bestand voor de registratie van de kluis van Hallo-portal en geef deze als invoer toohello hulpprogramma.

  ![register-configuratie-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. Geef details op Hallo nieuwe Proxy-Server en klik op Hallo **registreren** knop.
6. Open een opdrachtvenster Admin PowerShell.
7. Hallo volgende opdracht uitvoeren
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  Als u Scale-out processervers toothis configuratieserver gekoppeld, moet u te[Hallo proxy-instellingen herstellen op alle servers van Hallo scale-out proces](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in uw implementatie.

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a>Registreer de Server van een configuratie met Hallo opnieuw dezelfde Recovery Services-kluis
  1. Aanmelding tooyour configuratieserver.
  2. Start Hallo cspsconfigtool.exe met Hallo-snelkoppeling op het bureaublad.
  3. Klik op Hallo **kluis registratie** tabblad.
  4. Download een nieuw registratiebestand van Hallo-portal en geef deze als invoer toohello hulpprogramma.
        ![register-configuratie-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
  5. Geef details op Hallo proxyserver en klikt u op Hallo **registreren** knop.  
  6. Open een opdrachtvenster Admin PowerShell.
  7. Hallo volgende opdracht uitvoeren

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  Als u Scale-out processervers toothis configuratieserver gekoppeld, moet u te[alle Hallo scale-out processervers opnieuw registreren](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in uw implementatie.

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a>Een configuratie-Server registreren met een andere Recovery Services-kluis.
1. Aanmelding tooyour configuratieserver.
2. vanaf een opdrachtprompt admin Hallo-opdracht uitvoeren

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. Start Hallo cspsconfigtool.exe met Hallo-snelkoppeling op uw.
4. Klik op Hallo **kluis registratie** tabblad.
5. Download een nieuw registratiebestand van Hallo-portal en geef deze als invoer toohello hulpprogramma.

    ![register-configuratie-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. Geef details op Hallo proxyserver en klikt u op Hallo **registreren** knop.  
7. Open een opdrachtvenster Admin PowerShell.
8. Hallo volgende opdracht uitvoeren
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a>Een configuratieserver buiten gebruik stellen
Zorg ervoor dat Hallo volgende voordat u begint met het buiten gebruik stellen van de configuratieserver.
1. Schakel de beveiliging voor alle virtuele machines op deze Server Configuration.
2. Alle beleidsregels voor replicatie van Hallo configuratieserver loskoppelen.
3. Verwijder alle Vcenter-servers/vSphere-hosts die gekoppeld toohello configuratieserver zijn.

### <a name="delete-hello-configuration-server-from-azure-portal"></a>Hallo configuratieserver verwijderen vanuit Azure-portal
1. In Azure-portal te bladeren**Site Recovery-infrastructuur** > **configuratieservers** in Hallo kluismenu.
2. Klik op Hallo configuratieserver dat u wilt dat toodecommission.
3. Klik op de detailpagina Hallo Configuration Server op de knop verwijderen Hallo.

  ![Delete-configuratie-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. Klik op **Ja** tooconfirm Hallo verwijdering van Hallo-server.

  >[!WARNING]
  Als u alle virtuele machines, beleidsregels voor replicatie of vCenter servers/vSphere hosts die zijn gekoppeld aan deze Server configuratie hebt, kunt u het Hallo-server niet verwijderen. Deze entiteiten verwijderen voordat u toodelete Hallo kluis probeert.

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a>Hallo configuratieserver software en de bijbehorende afhankelijkheden verwijderen
  > [!TIP]
  Als u van plan tooreuse Hallo configuratieserver met Azure Site Recovery opnieuw bent, kunt klikt u vervolgens u overslaan toostep 4 rechtstreeks

1. Toohello configuratieserver aanmelden als beheerder.
2. Open het Configuratiescherm > programma > programma's verwijderen
3. Hallo-programma's in Hallo sequence volgende verwijderen:
  * Microsoft Azure Recovery Services-agent
  * Microsoft Azure Site Recovery Mobility Service/hoofddoelserver
  * Microsoft Azure Site Recovery Provider
  * Microsoft Azure Site Recovery-configuratieserver Server-proces
  * Microsoft Azure Site Recovery configuratie Server afhankelijkheden
  * MySQL-Server 5.5
4. Hallo volgende opdracht uit en opdrachtprompt beheerder uitvoeren.
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a>Configuratie Server Secure Socket Layer(SSL) certificaten vernieuwen
Hallo configuratieserver heeft een ingebouwde webserver, die activiteiten Hallo Hallo Mobility-Service, proces-Servers, ingedeeld en hoofddoel servers verbonden toohello configuratieserver. Hallo Configuration Server webserver gebruikt een SSL-certificaat tooauthenticate de clients. Dit certificaat heeft een verloopdatum van drie jaar en kan worden vernieuwd op elk gewenst moment Hallo methode te volgen:

> [!WARNING]
Verloopdatum voor certificaten kan alleen worden uitgevoerd op versie 9.4.XXXX. X of hoger. Alle hello Azure Site Recovery onderdelen (configuratieserver, processerver, Hoofddoelserver, Mobility-Service) bijwerken voordat u begint met Hallo certificaten vernieuwen werkstroom.

1. Op Hallo van Azure-portal, tooyour kluis Bladeren > Site Recovery-infrastructuur > configuratieserver.
2. Klik op de configuratieserver Hallo waarvoor u toorenew moet Hallo SSL-certificaat voor.
3. Onder Hallo configuratieserver health ziet u de vervaldatum Hallo voor Hallo SSL-certificaat.
4. Hallo-certificaat vernieuwen door te klikken op Hallo **certificaten vernieuwen** actie, zoals wordt weergegeven in Hallo installatiekopie te volgen:

  ![Delete-configuratie-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a>Secure Socket Layer waarschuwing. certificaat verlopen

> [!NOTE]
Hallo geldigheid van de SSL-certificaat voor alle installaties die hebben plaatsgevonden vóór mei 2016 is ingesteld tooone jaar. u hebt gestart met het certificaat verlopen-meldingen weergegeven in de hello Azure-portal te zien.

1. Als er Hallo Configuration Server SSL-certificaat tooexpire in Hallo volgende twee maanden, Hallo-service wordt gestart voor het verwittigen van gebruikers via hello Azure-portal & e-mailadres (u moet toobe geabonneerd tooAzure Site Recovery meldingen). U start een meldingsbanner zien op de resourcepagina Hallo-kluis.

  ![certificaat-melding](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. Klik op Hallo banner tooget meer informatie over het Hallo-verloopdatum voor certificaten.

  ![details van certificaat](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  Als in plaats van een **nu vernieuwen** knop u ziet een **nu bijwerken** knop. Dit betekent dat er een aantal onderdelen in uw omgeving die nog niet bijgewerkt too9.4.xxxx.x of hoger zijn zijn.

## <a name="sizing-requirements-for-a-configuration-server"></a>Formaat van de vereisten voor een configuratie-Server

| **CPU** | **Geheugen** | **Cachegrootte van de schijf** | **Snelheid van de gegevens wijzigen** | **Beveiligde machines** |
| --- | --- | --- | --- | --- |
| 8 vcpu's (2-sockets * @ 2,5 GHz-4 kernen) |16 GB |300 GB |500 GB of minder |Minder dan 100 machines repliceren. |
| 12 vcpu's (2-sockets * @ 2,5 GHz-6 kernen) |18 GB |600 GB |500 GB too1 TB |100 tot 150-machines repliceren. |
| 16 vcpu's (2-sockets * @ 2,5 GHz-8 kernen) |32 GB |1 TB |1 TB too2 TB |Repliceren tussen 150 tot 200-machines. |

  >[!TIP]
  Als uw dagelijkse gegevensverloop groter is dan 2 TB, of u van plan tooreplicate meer dan 200 virtuele machines bent, is het raadzaam toodeploy aanvullende processen servers tooload saldo Hallo met replicatieverkeer. Meer informatie over hoe toodeploy proces Scale-out-servers.


## <a name="common-issues"></a>Algemene problemen
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]

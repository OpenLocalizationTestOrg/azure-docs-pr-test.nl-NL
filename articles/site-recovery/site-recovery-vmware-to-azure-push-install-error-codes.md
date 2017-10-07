---
title: aaaAzure siteherstel probleemoplossing van VMware tooAzure | Microsoft Docs
description: Het oplossen van problemen bij het repliceren van virtuele machines in Azure
services: site-recovery
documentationcenter: 
author: asgang
manager: srinathv
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/24/2017
ms.author: asgang
ms.openlocfilehash: 912097c8892540dd798ba025e0b10374ca51d664
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-mobility-service-push-install-issues"></a>Het oplossen van problemen met de installatie van de Mobility-Service push

Dit artikel wordt uitgelegd Hallo veelvoorkomende problemen bij het tooinstall Hallo Mobility-Service op de server toosource voor het inschakelen van beveiliging.

## <a name="error-code-95107-protection-could-not-be-enabled"></a>(Foutcode 95107) Beveiliging kan niet worden ingeschakeld.
**Foutcode** | **Mogelijke oorzaken** | **Fout-specifieke aanbevelingen**
--- | --- | ---
95107 </br>***Bericht -*** Push-installatie van toohello bronmachine voor Hallo mobility-service is mislukt met foutcode ***EP0858***. <br> De dat Hallo referenties tooinstall mobility-service verstrekt is onjuist of Hallo gebruikersaccount heeft onvoldoende bevoegdheden | Gebruikersreferenties opgegeven tooinstall mobility-service op de bronmachine is onjuist | Zorg ervoor dat Hallo opgegeven gebruikersreferenties voor de bronmachine Hallo op de configuratieserver juist zijn. <br> de gebruikersreferenties tooadd/bewerken: Ga tooconfiguration server > Cspsconfigtool pictogram >-account beheren. </br> Zorg tevens onderstaande vereisten zijn voltooid push ingeschakelde toosuccessfully installeren.

## <a name="error-code-95015-protection-could-not-be-enabled"></a>(Foutcode 95015) Beveiliging kan niet worden ingeschakeld.
**Foutcode** | **Mogelijke oorzaken** | **Fout-specifieke aanbevelingen**
--- | --- | ---
95105 </br>***Bericht -*** Push-installatie van toohello bronmachine voor Hallo mobility-service is mislukt met foutcode ***EP0856***. <br> Ofwel 'Bestand-en printerdeling' niet toegestaan op de bronmachine Hallo of er zijn problemen met de netwerkverbinding tussen de processerver Hallo en Hallo-bronmachine| Bestands- en printerdeling is niet ingeschakeld | In Windows Firewall, Ga toohello bronmachine Hallo toestaan 'Bestand-en printerdeling' op de bronmachine Hallo > onder Windows Firewall-Instellingen > 'Voor het toestaan van een app of functie via Firewall' > 'Bestands- en printerdeling voor alle profielen' selecteren. </br> Zorg tevens onderstaande vereisten zijn voltooid push ingeschakelde toosuccessfully installeren.

## <a name="error-code-95117-protection-could-not-be-enabled"></a>(Foutcode 95117) Beveiliging kan niet worden ingeschakeld.
**Foutcode** | **Mogelijke oorzaken** | **Fout-specifieke aanbevelingen**
--- | --- | ---
95117 </br>***Bericht -*** Push-installatie van toohello bronmachine voor Hallo mobility-service is mislukt met foutcode ***EP0865***. <br> Hallo-bronmachine wordt niet uitgevoerd, of er zijn problemen met de netwerkverbinding tussen de processerver Hallo en Hallo-bronmachine | Netwerkverbinding tussen de processerver en de bronserver | Controleer de verbinding tussen de processerver en de bronserver. </br> Zorg tevens onderstaande vereisten zijn voltooid push ingeschakelde toosuccessfully installeren.

## <a name="error-code-95103-protection-could-not-be-enabled"></a>(Foutcode 95103) Beveiliging kan niet worden ingeschakeld.
**Foutcode** | **Mogelijke oorzaken** | **Fout-specifieke aanbevelingen**
--- | --- | ---
95103 </br>***Bericht -*** Push-installatie van toohello bronmachine voor Hallo mobility-service is mislukt met foutcode ***EP0854***. <br> "Windows Management Instrumentation (WMI)" is niet toegestaan op de bronmachine hello, of er zijn problemen met de netwerkverbinding tussen de processerver Hallo en Hallo-bronmachine| Windows Management Instrumentation (WMI) in Hallo Windows Firewall wordt geblokkeerd | Windows Management Instrumentation (WMI) in Windows Firewall Hallo toestaan. Onder Windows Firewall-Instellingen > 'Voor het toestaan van een app of functie via Firewall' > 'WMI selecteren voor alle profielen'. </br> Zorg tevens onderstaande vereisten zijn voltooid push ingeschakelde toosuccessfully installeren.

## <a name="check-push-install-logs-for-errors"></a>Push-installatie logboeken voor fouten

Navigeer op Hallo Configuration/processerver, toofile 'PushinstallService' zich bevindt op <Microsoft Azure Site Recovery Install Location>\home\svsystems\pushinstallsvc\ toounderstand Hallo bron van het Hallo-probleem en gebruik onderstaande stappen tooresolve Hallo probleem op te lossen.</br>
![pushiinstalllogs](./media/site-recovery-protection-common-errors/pushinstalllogs.png)

## <a name="push-install-pre-requisites-for-windows"></a>Push-installatie aan vereisten voor Windows
### <a name="ensure-file-and-printer-sharing-is-enabled"></a>Zorg dat 'Bestand-en printerdeling' is ingeschakeld
'Bestand-en printerdeling' en 'Windows Management Instrumentation' op de bronmachine Hallo in Windows Firewall Hallo toestaan </br>
#### <a name="if-source-machine-is-domain-joined-br"></a>Als de bronmachine lid van een domein is: </br>
Firewall-instellingen met behulp van de Console Groepsbeleidbeheer (GPMC) configureren.
1. Aanmelding tooActive directory-domein als beheerder van de computer en open de Console Groepsbeleidsbeheer (GPMC. MSC uitvoeren vanaf een Start > uitvoeren).</br>
3. Als GPMC niet is geïnstalleerd, voert u de koppeling hello te[installeren Hallo GPMC](https://technet.microsoft.com/library/cc725932.aspx) </br>
4. Dubbelklik op Group Policy Objects in Hallo forest en domein in Hallo GPMC-consolestructuur en te navigeren 'Standaarddomeinbeleid'. </br>
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png) </br>
</br>
5. Met de rechtermuisknop op "Standaarddomeinbeleid" > Bewerken > een nieuw 'Groepsbeleidsbeheer-Editor'-venster wordt geopend. </br>
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png) </br>
</br>
6. Navigeer in de Editor voor Groepsbeleidsbeheer Hallo tooComputer Configuration > beleidsregels > Beheersjablonen > netwerk > Netwerkverbindingen > Windows Firewall. </br>
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png) </br>
</br>
7. Hallo-na-instellingen voor het domeinprofiel en de standaardprofiel inschakelen </br>
een) Dubbelklik op op de uitzondering ' Windows Firewall: binnenkomende bestanden en printers delen uitzondering '. Selecteer ingeschakeld en klik op OK. </br>
b) dubbelklikt u op de uitzondering ' Windows Firewall: uitzondering voor binnenkomende extern beheer toestaan '. Selecteer ingeschakeld en klik op OK. </br>
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png) </br>
</br>

###### <a name="if-source-machine-is-not-domain-joined-and-part-of-workgroup-br"></a>Als de bronmachine is niet verbonden met het domein en deel uit van werkgroep </br>
Firewall-instellingen configureren op de externe computer (voor werkgroep):
1. Ga toohello bronmachine,</br>
2. Onder Windows Firewall-Instellingen > 'Voor het toestaan van een app of functie via Firewall' > 'Bestands- en printerdeling voor alle profielen' selecteren. </br>
3. Onder Windows Firewall-Instellingen > 'Voor het toestaan van een app of functie via Firewall' > 'WMI selecteren voor alle profielen'. </br>

#### <a name="disable-remote-user-account-control-uac"></a>Schakel externe Gebruikersaccountbeheer (UAC)
UAC met registry key toopush Hallo mobility-service uitschakelen.
1. Klik op Start > uitvoeren > Typ regedit > ENTER
2. Zoek en klik op Hallo volgende registersubsleutel: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
3. Ga als volgt als Hallo LocalAccountTokenFilterPolicy registervermelding niet bestaat:
4. In de menu Bewerken Hallo > Nieuw > op DWORD-waarde.
5. Typ LocalAccountTokenFilterPolicy en druk op ENTER.
6. Met de rechtermuisknop op LocalAccountTokenFilterPolicy en klik op wijzigen.
7. Typ 1 in het vak Waardegegevens hello, en klik op OK.
8. Sluit Register-Editor.


## <a name="push-install-pre-requisites-for-linux"></a>Push-installatie aan vereisten voor Linux:

1. Maak een Hoofdgebruiker op de bronserver Linux Hallo. (Dit account alleen gebruiken voor Hallo push-installatie en -updates)</br>
2. Controleer dat bestand Hallo/etc/hosts op de bron Hallo Linux-server heeft vermeldingen die zijn toegewezen Hallo lokale hostnaam tooIP adressen die zijn gekoppeld aan alle netwerkadapters. </br>
3. Controleer of de meest recente openssh, openssh-server en openssl pakketten Hallo zijn geïnstalleerd op Linux-bronserver. </br>
Controleer of ssh poort 22 ingeschakeld en worden uitgevoerd is. </br>
4. Controleer als verouderde vermeldingen van agents die al aanwezig op de bronserver hello, verwijder oudere agenten van Hallo en Hallo-server opnieuw opgestart, -agent opnieuw installeren. </br>

#### <a name="enable-sftp-subsystem-and-password-authentication-in-hello-sshdconfig-file"></a>SFTP subsysteem voor verificatie en wachtwoord in Hallo sshd_config bestand inschakelen
1. Op de bronserver, moet u zich aanmelden als hoofdmap. </br>
2. In het Hallo-bestand /etc/ssh/sshd_config</br> Hallo-regel die met PasswordAuthentication begint vinden. </br>
3. d.   Hallo regel Opmerking verwijderen en waarde van 'no' hello te 'Ja' wijzigen. </br>
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)
4. Hallo-regel die met 'Subsysteem begint' vinden en verwijder de opmerkingen Hallo regel. </br>
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)
5. Hallo wijzigingen opslaan en Hallo sshd-service opnieuw starten. </br>

## <a name="push-installation-checks-on-configurationprocess-server"></a>Push-installatie controles op configuratieproces/server.
#### <a name="validate-credentials-for-discovery-and-installation"></a>De referenties voor detectie en installatie valideren

1. Starten van de configuratieserver, Cspsconfigtool</br>
![WMItestConnect5](./media/site-recovery-protection-common-errors/wmitestconnect5.png) </br>

2. Zorg ervoor dat Hallo account dat wordt gebruikt voor beveiliging administrator-rechten op de bronmachine Hallo heeft. </br>

#### <a name="check-connectivity-between-process-server-and-source-server"></a>Controleer de verbinding tussen de processerver en de bronserver
1. Zorg ervoor dat de dat processerver internetverbinding heeft.
2. WMI-verbinding controleren met behulp wbemtest.exe. </br>
Op de processerver hello, klik op Start > uitvoeren > wbemtest.exe > Windows Management Instrumentation Tester venster wordt geopend, zoals wordt weergegeven.</br>
   ![WMItestConnect1](./media/site-recovery-protection-common-errors/wmitestconnect1.png) </br>
   </br>
Klik op verbinden > Hallo bron server-IP in Hallo Namespace invoer-gebruikersnaam en wachtwoord invoeren (als de bronmachine verbonden met het domein is, bieden de domeinnaam Hallo samen met de naam van de gebruiker als "Domeinnaam\gebruikersnaam". Als de bronmachine in een werkgroep is, bieden alleen Hallo-gebruikersnaam.) Selecteer Hallo verificatieniveau als Pakketprivacy. </br>
![WMItestConnect2](./media/site-recovery-protection-common-errors/wmitestconnect2.png) </br>
   </br>
   Klik op verbinding maken. Nu Hallo WMI-verbinding is voltooid met de opgegeven gegevens zijn hello en Hallo Windows Management Instrumentation Tester venster moet worden weergegeven, zoals hieronder wordt weergegeven: </br>
   ![WMItestConnect3](./media/site-recovery-protection-common-errors/wmitestconnect3.png) </br>
</br>
   Als WMI-verbinding niet geslaagd is zal er een foutbericht pop-upvenster. Hallo onderstaande schermafbeelding ziet u een mislukte poging als WMI/Remote Administration is niet ingeschakeld in Windows firewall app toegestaan. </br>
   ![WMItestConnect4](./media/site-recovery-protection-common-errors/wmitestconnect4.png) </br>
</br>

3. Controleren op Hallo WMI-status en de verbinding.</br>
Op Hallo configuratieproces /-server </br>
Klik op start > uitvoeren > wmimgmt.msc > Acties > meer acties > Verbind tooanother computer (bronmachine). </br>
Voer referenties op Hallo van Hallo account dat wordt gebruikt voor beveiliging en controle als de verbinding goed is. </br>

#### <a name="verify-network-shared-folders-of-source-machine-is-accessible-from-process-server-ps-remotely-using-specified-credentials"></a>Controleer of de gedeelde netwerkmappen van de bronmachine is toegankelijk vanuit proces Server (PS) op afstand met opgegeven referenties.
  1. Open Windows Verkenner-aanmelding tooProcess Server (PS) machine > In de balk adrestype Hallo > '\\\source-machine-ip\C$ "> klikt u op Enter. </br>
  ![Fileshare1](./media/site-recovery-protection-common-errors/fileshare1.png) </br>
  2. Windows Verkenner wordt om referenties gevraagd. Hallo-gebruikersnaam en wachtwoord invoeren > Klik op OK.</br>
   Als de bronmachine verbonden met het domein is, moet u de domeinnaam Hallo samen met de gebruikersnaam van de opgeven als "Domeinnaam\gebruikersnaam".</br>
   Als de bronmachine in een werkgroep is, geeft u alleen Hallo 'gebruikersnaam'. </br>
  ![Fileshare2](./media/site-recovery-protection-common-errors/fileshare2.png) </br>
  3. Als de verbinding geslaagd is, kunt u Hallo mappen van de bronmachine op afstand van proces Server (PS) weergeven </br>
  ![Fileshare3](./media/site-recovery-protection-common-errors/fileshare3.png) </br>

> [!NOTE] 
> Als verbinding mislukt is, controleert u of aan alle vereisten wordt voldaan.
>

Als u niet wilt dat tooopen 'Windows Management Instrumentation', kunt u mobility-service ook handmatig installeren op de bronmachine Hallo.</br> [Handmatig via de gebruikersinterface van de Mobility-Service installeren](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) </br>
[Via configuration manager richtlijnen installatie](site-recovery-install-mobility-service-using-sccm.md) </br>

## <a name="next-steps"></a>Volgende stappen
- [Schakel replicatie voor virtuele VMware-machines](vmware-walkthrough-enable-replication.md)

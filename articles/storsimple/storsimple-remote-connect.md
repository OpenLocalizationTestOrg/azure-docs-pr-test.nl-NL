---
title: aaaConnect op afstand tooyour StorSimple-apparaat | Microsoft Docs
description: Legt uit hoe tooconfigure uw apparaat voor extern beheer en hoe tooconnect tooWindows PowerShell voor StorSimple via HTTP of HTTPS.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 55ed8fcdd997901301e0adc164a302216cde0332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a>Tooyour StorSimple 8000 series apparaat op afstand verbinding maken

## <a name="overview"></a>Overzicht
U kunt Windows PowerShell voor externe toegang tooconnect tooyour StorSimple-apparaat gebruiken. Als u op deze manier verbinding, ziet u een menu. (Ziet u een menu alleen als u de seriële console Hallo op Hallo apparaat tooconnect gebruiken.) Met Windows PowerShell op afstand, moet u specifieke runspace tooa verbinden. U kunt ook de weergavetaal Hallo opgeven. 

Voor meer informatie over het gebruik van Windows PowerShell voor externe toegang toomanage uw apparaat gaat te[gebruik Windows PowerShell voor StorSimple tooadminister uw StorSimple-apparaat](storsimple-windows-powershell-administration.md).

Deze zelfstudie wordt uitgelegd hoe tooconfigure uw apparaat voor extern beheer en klikt u vervolgens het tooconnect tooWindows PowerShell voor StorSimple. Hier kunt u HTTP of HTTPS tooconnect via Windows PowerShell op afstand. Echter, wanneer u beslist hoe tooconnect tooWindows PowerShell voor StorSimple, houd rekening met Hallo volgende: 

* Toohello rechtstreeks verbinding maken de seriële console apparaat beveiligd is, maar verbindende toohello seriële console via netwerkswitches is niet. Wees voorzichtig met van Hallo beveiligingsrisico, omdat het toohello de seriële console apparaat via netwerkswitches verbinding te maken. 
* Verbinding maken via een HTTP-sessie biedt meer beveiliging dan verbinding maken via de seriële console Hallo via Hallo netwerk mogelijk. Hoewel dit niet de meest beveiligde methode hello, is het is acceptabel in vertrouwde netwerken. 
* Verbinding maken via een HTTPS-sessie met een zelfondertekend certificaat is Hallo veiligste en aanbevolen optie Hallo.

U kunt verbinden op afstand toohello Windows PowerShell-interface. Externe toegang tooyour StorSimple-apparaat via Windows PowerShell-interface Hallo is echter niet standaard ingeschakeld. U moet extern beheer van de tooenable op Hallo apparaat eerst en klik vervolgens op Hallo client die wordt gebruikt tooaccess uw apparaat.

Hallo stappen in dit artikel zijn uitgevoerd op een hostsysteem met Windows Server 2012 R2.

## <a name="connect-through-http"></a>Verbinding maken via HTTP
Een tooWindows PowerShell voor StorSimple verbinding via een HTTP-sessie, biedt betere beveiliging dan verbinding maken via de seriële console Hallo van uw StorSimple-apparaat. Hoewel dit niet de meest beveiligde methode hello, is het is acceptabel in vertrouwde netwerken.

U kunt Hallo klassieke Azure-portal of Hallo seriële console tooconfigure extern beheer gebruiken. Selecteer een van de Hallo procedures te volgen:

* [Hello Azure classic portal tooenable extern beheer via HTTP gebruiken](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [Hallo seriële console tooenable extern beheer via HTTP gebruiken](#use-the-serial-console-to-enable-remote-management-over-http)

Nadat u extern beheer inschakelen, gebruikt u hello te volgen procedure tooprepare Hallo-client voor een externe verbinding.

* [Hallo-client voorbereiden voor externe verbinding](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-http"></a>Hello Azure classic portal tooenable extern beheer via HTTP gebruiken
Voer Hallo stappen te volgen in hello Azure classic portal tooenable extern beheer via HTTP.

#### <a name="tooenable-remote-management-through-hello-azure-classic-portal"></a>extern beheer via de klassieke Azure-portal Hallo tooenable
1. Toegang **apparaten** > **configureren** voor uw apparaat.
2. Schuif omlaag toohello **extern beheer** sectie.
3. Stel **extern beheer inschakelen** te**Ja**.
4. U kunt nu tooconnect via HTTP. (Hallo standaardwaarde is tooconnect via HTTPS). Zorg ervoor dat HTTP is geselecteerd.
   
   > [!NOTE]
   > Verbinding maken via HTTP is alleen acceptabel in vertrouwde netwerken.
   > 
   > 
5. Klik op **opslaan** Hallo Hallo pagina onderaan in.

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a>Hallo seriële console tooenable extern beheer via HTTP gebruiken
Hallo volgende stappen uit op Hallo apparaat seriële console tooenable extern beheer uitvoeren.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>extern beheer via de seriële console van Hallo apparaat tooenable
1. Selecteer optie 1 Hallo seriële consolemenu. Voor meer informatie over het gebruik van de seriële console Hallo op Hallo apparaat gaat te[tooWindows PowerShell voor StorSimple-verbinding via de seriële console apparaat](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. Hallo opdrachtprompt, typt u:`Enable-HcsRemoteManagement –AllowHttp`
3. U wordt gewaarschuwd over Hallo beveiligingsproblemen van het gebruik van HTTP-tooconnect toohello apparaat. Bevestig door op te geven wanneer u wordt gevraagd, **Y**.
4. Controleer of HTTP is ingeschakeld door te typen:`Get-HcsSystem`
5. Controleer of deze Hallo **RemoteManagementMode** veld bevat **HttpsAndHttpEnabled**.hello volgende afbeelding ziet u deze instellingen in de PuTTY.
   
     ![Seriële HTTPS en HTTP-ingeschakeld](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a>Hallo-client voorbereiden voor externe verbinding
Hallo volgende stappen uit op Hallo client tooenable extern beheer uitvoeren.

#### <a name="tooprepare-hello-client-for-remote-connection"></a>tooprepare Hallo-client voor externe verbinding
1. Start een Windows PowerShell-sessie als administrator.
2. Type Hallo volgende opdracht tooadd Hallo IP-adres van de lijst met vertrouwde hosts Hallo StorSimple-apparaat toohello van client: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     Vervang <*device_ip*> met Hallo IP-adres van uw apparaat; bijvoorbeeld: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Type Hallo opdracht toosave Hallo apparaat referenties in een variabele te volgen: 
   
    ```
    $cred = Get-Credential
    ```
    
4. In het dialoogvenster Hallo die wordt weergegeven:
   
   1. Typ de gebruikersnaam in deze indeling Hallo: *device_ip\SSAdmin*.
   2. Typ beheerderswachtwoord van het Hallo-apparaat dat is ingesteld wanneer het Hallo-apparaat is geconfigureerd met de wizard setup Hallo. is het standaardwachtwoord Hallo *Wachtwoord1*.
5. Start een Windows PowerShell-sessie op Hallo apparaat door deze opdracht te typen:
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > toocreate een Windows PowerShell-sessie voor gebruik met Hallo virtuele StorSimple-apparaat, append Hallo `–Port` parameter en geef Hallo openbare poort die u hebt geconfigureerd in externe toegang voor virtueel StorSimple-apparaat.
   > 
   > 
   
     Op dit moment hebt u een actieve externe Windows PowerShell-sessie toohello apparaat.
   
    ![Externe communicatie via HTTP met PowerShell](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a>Verbinding maken via HTTPS
Een tooWindows PowerShell voor StorSimple verbinding via een HTTPS-sessie Hallo veiligste en aanbevolen methode van Microsoft Azure StorSimple-apparaat voor op afstand verbinding tooyour. Hallo volgen procedures wordt uitgelegd hoe tooset up Hallo seriële console en client-computers zodat u kunt HTTPS tooconnect tooWindows PowerShell voor StorSimple.

U kunt Hallo klassieke Azure-portal of Hallo seriële console tooconfigure extern beheer gebruiken. Selecteer een van de Hallo procedures te volgen:

* [Hello Azure classic portal tooenable extern beheer via HTTPS gebruiken](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [Hallo seriële console tooenable extern beheer via HTTPS gebruiken](#use-the-serial-console-to-enable-remote-management-over-https)

Nadat u extern beheer inschakelen, Hallo procedures tooprepare Hallo host voor een extern beheer na gebruik en toohello apparaat verbinden van de externe host Hallo.

* [Hallo host voorbereiden voor extern beheer](#prepare-the-host-for-remote-management)
* [Verbinding maken met toohello apparaat van de externe host Hallo](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-https"></a>Hello Azure classic portal tooenable extern beheer via HTTPS gebruiken
Voer Hallo stappen te volgen in hello Azure classic portal tooenable extern beheer via HTTPS.

#### <a name="tooenable-remote-management-over-https-from-hello-azure-classic-portal"></a>tooenable remote management via HTTPS van Hallo klassieke Azure-portal
1. Toegang **apparaten** > **configureren** voor uw apparaat.
2. Schuif omlaag toohello **extern beheer** sectie.
3. Stel **extern beheer inschakelen** te**Ja**.
4. U kunt nu tooconnect via HTTPS. (Hallo standaardwaarde is tooconnect via HTTPS). Zorg ervoor dat HTTPS is geselecteerd. 
5. Klik op **certificaat voor extern beheer downloaden**. Geef een locatie toosave dit bestand. U moet dit certificaat op de client of hostcomputer computer Hallo die u tooconnect toohello apparaat gebruikt tooinstall.
6. Klik op **opslaan** Hallo Hallo pagina onderaan in.

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a>Hallo seriële console tooenable extern beheer via HTTPS gebruiken
Hallo volgende stappen uit op Hallo apparaat seriële console tooenable extern beheer uitvoeren.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>extern beheer via de seriële console van Hallo apparaat tooenable
1. Selecteer optie 1 Hallo seriële consolemenu. Voor meer informatie over het gebruik van de seriële console Hallo op Hallo apparaat gaat te[tooWindows PowerShell voor StorSimple-verbinding via de seriële console apparaat](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. Hallo opdrachtprompt, typt u: 
   
     `Enable-HcsRemoteManagement`
   
    Dit moet HTTPS inschakelen op uw apparaat.
3. Controleer of HTTPS is ingeschakeld door te typen: 
   
     `Get-HcsSystem`
   
    Zorg ervoor dat Hallo **RemoteManagementMode** veld bevat **HttpsEnabled**.hello volgende afbeelding ziet u deze instellingen in de PuTTY.
   
     ![Seriële HTTPS-functionaliteit](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. Vanuit de uitvoer Hallo van `Get-HcsSystem`, serienummer Hallo Hallo apparaat kopiëren en opslaan voor later gebruik.
   
   > [!NOTE]
   > Hallo serienummer maps toohello CN-naam in Hallo certificaat.
   > 
   > 
5. Een certificaat voor extern beheer verkrijgen door te typen: 
   
     `Get-HcsRemoteManagementCert`
   
    Een certificaat vergelijkbare toohello volgende wordt weergegeven.
   
    ![Extern beheercertificaat ophalen](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. Hallo gegevens kopiëren in Hallo-certificaat van **---BEGIN CERTIFICATE---** te**---EINDCERTIFICAAT---** in een teksteditor zoals Kladblok en sla deze op te geven als een .cer-bestand. (Kopieert u dit bestand tooyour externe host wanneer u Hallo host voorbereidt.)
   
   > [!NOTE]
   > een nieuw certificaat toogenerate gebruiken Hallo `Set-HcsRemoteManagementCert` cmdlet.
   > 
   > 

### <a name="prepare-hello-host-for-remote-management"></a>Hallo host voorbereiden voor extern beheer
het Hallo-hostcomputer tooprepare voor een externe verbinding die gebruikmaakt van een HTTPS-sessie uitvoeren Hallo procedures te volgen:

* [Importeren Hallo cer-bestand in de basisarchief Hallo van Hallo-client of de externe host](#to-import-the-certificate-on-the-remote-host).
* [Hallo apparaat serienummers toohello hosts-bestand op de externe host toevoegen](#to-add-device-serial-numbers-to-the-remote-host).

Elk van deze procedures wordt hieronder beschreven.

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a>tooimport hello certificaat op de externe host Hallo
1. Met de rechtermuisknop op Hallo cer-bestand en selecteer **installeren certificaat**. Hiermee start u Hallo Wizard Certificaat importeren.
   
    ![Wizard Certificaat importeren 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. Voor **archieflocatie**, selecteer **lokale Machine**, en klik vervolgens op **volgende**.
3. Selecteer **alle certificaten in Hallo volgende archief plaatsen**, en klik vervolgens op **Bladeren**. Navigeer toohello basisarchief van de externe host, en klik vervolgens op **volgende**.
   
    ![Wizard Certificaat importeren 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. Klik op **Voltooien**. Er verschijnt een bericht dat aangeeft dat Hallo importeren geslaagd is.
   
    ![Wizard Certificaat importeren 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a>tooadd apparaat serienummers toohello externe host
1. Kladblok start als beheerder en open vervolgens Hallo hosts-bestand op \Windows\System32\Drivers\etc.
2. Hallo na drie vermeldingen tooyour hosts-bestand toevoegen: **DATA 0-IP-adres**, **Controller 0 vast IP-adres**, en **Controller 1 vast IP-adres**.
3. Voer het serienummer van het Hallo-apparaat dat u eerder hebt opgeslagen. Dit toohello IP-adres toewijzen zoals weergegeven in Hallo installatiekopie te volgen. Voor Controller 0 en Controller 1 toevoegen **Controller0** en **Controller1** aan Hallo einde van het serienummer hello (CN-naam).
   
    ![CN-naam toohosts bestand toe te voegen](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. Hallo hosts-bestand opslaan.

### <a name="connect-toohello-device-from-hello-remote-host"></a>Verbinding maken met toohello apparaat van de externe host Hallo
Gebruik Windows PowerShell- en SSL tooenter een SSAdmin-sessie op uw apparaat vanaf een externe host of de client. Hallo SSAdmin sessie toegewezen toooption 1 in Hallo [seriële console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu van uw apparaat.

Hallo na de procedure op Hallo computer van waaruit u toomake Hallo externe Windows PowerShell verbinding wilt uitvoeren.

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a>tooenter een SSAdmin-sessie op Hallo apparaat via Windows PowerShell- en SSL
1. Start een Windows PowerShell-sessie als administrator.
2. Hallo IP-adres toohello apparaatclient van vertrouwde hosts toevoegen door te typen:
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    Waarbij <*device_ip*> Hallo IP-adres van uw apparaat is; bijvoorbeeld: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Een nieuwe referentie maken door te typen: 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    Waarbij <*IP-adres van het doelapparaat*> Hallo IP-adres van de DATA 0 voor uw apparaat; bijvoorbeeld **10.126.173.90** zoals weergegeven in de voorafgaande aan de installatiekopie van het hosts-bestand Hallo Hallo. Hallo beheerderswachtwoord voor uw apparaat ook opgeven.
4. Een sessie maken door te typen:
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    Hallo - ComputerName parameter in Hallo-cmdlet, bieden Hallo <*serienummer van het doelapparaat*>. Dit serienummer is toegewezen toohello IP-adres van de DATA 0 Hallo hostbestand op de externe host; bijvoorbeeld: **SHX0991003G44MT** zoals weergegeven in Hallo installatiekopie te volgen.
5. Type: 
   
     `Enter-PSSession $session`
6. U toowait moet een paar minuten en vervolgens kunt u zich verbonden tooyour apparaat via HTTPS via SSL. U ziet een bericht waarin wordt aangegeven dat u verbonden tooyour apparaat.
   
    ![PowerShell voor externe toegang met behulp van HTTPS- en SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [uw StorSimple-apparaat met behulp van Windows PowerShell tooadminister](storsimple-windows-powershell-administration.md).
* Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-manager-service-administration.md).


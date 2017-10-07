---
title: een Windows-VHD tooupload tooAzure aaaPrepare | Microsoft Docs
description: Hoe tooprepare een Windows-VHD of VHDX voordat u uploadt tooAzure
services: virtual-machines-windows
documentationcenter: 
author: glimoli
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7802489d-33ec-4302-82a4-91463d03887a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: genli
ms.openlocfilehash: 530390e4c6a4f66ddfd4da23338f9bb3708c299f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-windows-vhd-or-vhdx-tooupload-tooazure"></a>Een Windows-VHD of VHDX tooupload tooAzure voorbereiden
Voordat u een virtuele Windows-machines (VM) van de lokale tooMicrosoft Azure uploaden, moet u Hallo virtuele harde schijf (VHD of VHDX) voorbereiden. Azure ondersteunt alleen generatie 1 virtuele machines die in Hallo VHD-indeling en een schijf met vaste grootte hebben. Hallo toegestane maximale lengte voor Hallo dat VHD is 1023 GB. U kunt een generatie 1 VM van Hallo VHDX-bestand system tooVHD en van een dynamisch uitbreidbare schijf toofixed-formaat converteren. Maar als u de generatie van een virtuele machine niet wijzigen. Zie voor meer informatie [maak ik een generatie 1 of 2 VM in Hyper-V](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).

Zie voor meer informatie over het Hallo-ondersteuningsbeleid voor virtuele machine van Azure [Microsoft server software-ondersteuning voor Microsoft Azure Virtual machines](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).

> [!Note]
> Hallo-instructies in dit artikel van toepassing toohello 64-bits versie van Windows Server 2008 R2 en hoger Windows server-besturingssysteem. Zie voor informatie over de uitgevoerde 32-bits versie van besturingssysteem in Azure, [ondersteuning voor 32-bits besturingssystemen in virtuele machines in Azure](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines).

## <a name="convert-hello-virtual-disk-toovhd-and-fixed-size-disk"></a>Hallo virtuele schijf tooVHD en de schijf met vaste grootte converteren 
Als u tooconvert moet vereist de virtuele schijf toohello indeling voor Azure, gebruik een van de methoden Hallo in deze sectie. Back-up Hallo VM voordat u Hallo virtuele schijf conversieproces uitvoert en zorg ervoor dat Windows VHD correct op de lokale server Hallo werkt Hallo. Los eventuele fouten in de virtuele machine zelf Hallo voordat u tooconvert probeert of tooAzure te uploaden.

Nadat u Hallo schijf converteert, maakt u een virtuele machine die gebruikmaakt van schijf Hallo geconverteerd. Start en meld u aan toohello VM toofinish Hallo VM voorbereiden voor het uploaden.

### <a name="convert-disk-using-hyper-v-manager"></a>Converteert de schijf met behulp van Hyper-V-beheer
1. Open Hyper-V-beheer en selecteer uw lokale computer aan de linkerkant Hallo. Hallo menu boven Hallo computerlijst en klik op **actie** > **schijf bewerken**.
2. Op Hallo **virtuele hardeschijf zoeken** scherm, zoekt en selecteert u de virtuele schijf.
3. Op Hallo **actie kiezen** scherm en selecteer vervolgens **converteren** en **volgende**.
4. Als u tooconvert vanaf VHDX nodig hebt, selecteert u **VHD** en klik vervolgens op **volgende**
5. Als u tooconvert vanaf een dynamisch uitbreidbare schijf nodig hebt, selecteert u **een vaste grootte** en klik vervolgens op **volgende**
6. Zoek en selecteer een pad toosave Hallo nieuwe VHD-bestand op.
7. Klik op **Voltooien**.

>[!NOTE]
>Hallo-opdrachten in dit artikel moeten worden uitgevoerd op een PowerShell-sessie met verhoogde bevoegdheden.

### <a name="convert-disk-by-using-powershell"></a>Converteert de schijf met behulp van PowerShell
U kunt een virtuele schijf converteren via Hallo [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) opdracht in Windows PowerShell. Selecteer **als administrator uitvoeren** wanneer u start PowerShell. 

Hallo converteert volgende voorbeeldopdracht vanaf VHDX tooVHD en vanaf een dynamisch uitbreidbare toofixed-schijfgrootte:

```Powershell
Convert-VHD –Path c:\test\MY-VM.vhdx –DestinationPath c:\test\MY-NEW-VM.vhd -VHDType Fixed
```
Vervang in deze opdracht Hallo-waarde voor '-pad ' met Hallo pad toohello virtuele harde schijf die u wilt dat tooconvert en Hallo waarde voor '-doelpad ' hello nieuwe pad en naam van Hallo geconverteerd schijf.

### <a name="convert-from-vmware-vmdk-disk-format"></a>Converteren van VMware VMDK schijf-indeling
Als er een virtuele machine van Windows-installatiekopie in Hallo [VMDK-indeling](https://en.wikipedia.org/wiki/VMDK), tooa VHD converteren via Hallo [Microsoft VM Converter](https://www.microsoft.com/download/details.aspx?id=42497). Zie voor meer informatie, Hallo blog artikel [hoe een VMware VMDK tooHyper-V-VHD tooConvert](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx).

## <a name="set-windows-configurations-for-azure"></a>Windows-configuraties voor Azure instellen

Op de virtuele machine die u van plan bent Hallo tooupload tooAzure, alle opdrachten uitvoert in de volgende Hallo stappen van een [opdrachtpromptvenster](https://technet.microsoft.com/library/cc947813.aspx):

1. Statische permanente route op Hallo routeringstabel verwijderen:
   
   * tooview hello routetabel, voeren `route print` bij de opdrachtprompt Hallo.
   * Controleer de Hallo **persistentie Routes** secties. Als er een permanente route is, gebruikt u [route verwijderen](https://technet.microsoft.com/library/cc739598.apx) tooremove deze.
2. Hallo WinHTTP proxy verwijderen:
   
    ```PowerShell
    netsh winhttp reset proxy
    ```
3. Hallo schijf SAN-beleid te ingesteld[Onlineall](https://technet.microsoft.com/library/gg252636.aspx). 
   
    ```PowerShell
    diskpart 
    ```
    Typ in Hallo open opdrachtpromptvenster Hallo volgende opdrachten:

     ```DISKPART
    san policy=onlineall
    exit   
    ```

4. Tijd Coordinated Universal Time (UTC) ingesteld voor Windows en opstarttype Hallo Windows Time (w32time)-service te Hallo**automatisch**:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\TimeZoneInformation' -name "RealTimeIsUniversal" 1 -Type DWord

    Set-Service -Name w32time -StartupType Auto
    ```
5. Stel Hallo power profiel toohello **hoge prestaties**:

    ```PowerShell
    powercfg /setactive SCHEME_MIN
    ```

## <a name="check-hello-windows-services"></a>Controleer de Hallo Windows services
Zorg ervoor dat elk van de Windows-services te volgen Hallo toohello is ingesteld **Windows standaardwaarden**. Dit zijn Hallo minimumaantal services die moeten worden ingesteld toomake ervoor dat Hallo VM is verbonden. tooreset hello opstartinstellingen Hallo volgende opdrachten uitvoeren:
   
```PowerShell
Set-Service -Name bfe -StartupType Auto
Set-Service -Name dhcp -StartupType Auto
Set-Service -Name dnscache -StartupType Auto
Set-Service -Name IKEEXT -StartupType Auto
Set-Service -Name iphlpsvc -StartupType Auto
Set-Service -Name netlogon -StartupType Manual
Set-Service -Name netman -StartupType Manual
Set-Service -Name nsi -StartupType Auto
Set-Service -Name termService -StartupType Manual
Set-Service -Name MpsSvc -StartupType Auto
Set-Service -Name RemoteRegistry -StartupType Auto
```

## <a name="update-remote-desktop-registry-settings"></a>Instellingen voor extern bureaublad-register bijwerken
Zorg ervoor dat Hallo na instellingen correct zijn geconfigureerd voor verbinding met extern bureaublad:

>[!Note] 
>U wordt een foutbericht weergegeven wanneer u Hallo uitvoert **Set-ItemProperty-pad ' HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services - naam &lt;objectnaam&gt; &lt;waarde&gt;** in deze stappen. Fout bij het Hallo-bericht kan worden genegeerd. Dit betekent dat alleen dat domein Hallo pusht niet dat de configuratie door middel van een groepsbeleidsobject.
>
>

1. Remote Desktop Protocol (RDP) is ingeschakeld:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDenyTSConnections" -Value 0 -Type DWord
    ```
   
2. Hallo RDP-poort juist is ingesteld (standaard poort 3389):
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "PortNumber" 3389 -Type DWord
    ```
    Wanneer u een virtuele machine implementeert, worden de standaardregels Hallo tegen poort 3389 gemaakt. Als u wilt dat toochange Hallo-poortnummer, dat doen nadat Hallo VM is geïmplementeerd in Azure.

3. Hallo-listener luistert in elke netwerkinterface:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "LanAdapter" 0 -Type DWord
   ```
4. Hallo verificatie op netwerkniveau modus configureren voor Hallo RDP-verbindingen:
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SecurityLayer" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "fAllowSecProtocolNegotiation" 1 -Type DWord
     ```

5. Stel Hallo keepalive-waarde:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveEnable" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveInterval" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "KeepAliveTimeout" 1 -Type DWord
    ```
6. Verbinding:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDisableAutoReconnect" 0 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fInheritReconnectSame" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fReconnectSame" 0 -Type DWord
    ```
7. Hallo aantal gelijktijdige verbindingen beperken:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "MaxInstanceCount" 4294967295 -Type DWord
    ```
8. Als er zelfondertekende certificaten toohello RDP-listener gekoppeld, u deze verwijderen:
    
    ```PowerShell
    Remove-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SSLCertificateSHA1Hash"
    ```
    Dit is toomake zeker dat u verbinding aan Hallo begin maken kunt bij het implementeren van Hallo VM. U kunt dit ook bekijken op een later stadium na Hallo die VM is geïmplementeerd in Azure, indien nodig.

9. Als Hallo VM deel van een domein uitmaken zal, controleert u dat alle Hallo na instellingen toomake ervoor dat de voormalige Hallo-instellingen worden niet hersteld. Hallo-beleidsregels die moeten worden gecontroleerd zijn Hallo volgende:
    
    - RDP is ingeschakeld:

         Computer Computerconfiguratie\Beleid\Windows Settings\Administrative Templates\ onderdelen\Extern bureaublad bureaublad-sessiehost\Verbindingen:
         
         **Toestaan dat de gebruikers tooconnect op afstand via Extern bureaublad**

    - NLA-Groepsbeleid:

        Settings\Administrative Templates\Components\Remote Desktop-bureaublad sessie\Beveiliging: 
        
        **Gebruiker-verificatie voor externe verbindingen met behulp van verificatie op netwerkniveau vereisen**
    
    - Houd Alive-instellingen:

        Computer Computerconfiguratie\Beleid\Windows Settings\Administrative Templates\Windows onderdelen\Extern bureaublad bureaublad-sessiehost\Verbindingen: 
        
        **Keep-alive verbinding interval configureren**

    - Instellingen voor verbinding:

        Computer Computerconfiguratie\Beleid\Windows Settings\Administrative Templates\Windows onderdelen\Extern bureaublad bureaublad-sessiehost\Verbindingen: 
        
        **Automatisch opnieuw verbinden**

    - Het aantal verbindingsinstellingen Hallo beperken:

        Computer Computerconfiguratie\Beleid\Windows Settings\Administrative Templates\Windows onderdelen\Extern bureaublad bureaublad-sessiehost\Verbindingen: 
        
        **Aantal verbindingen beperken**

## <a name="configure-windows-firewall-rules"></a>Configureer Windows Firewall-regels
1. Windows Firewall inschakelen op Hallo drie profielen (domein, Standard en openbaar):

   ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\DomainProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\PublicProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\Standardprofile' -name "EnableFirewall" -Value 1 -Type DWord
   ```

2. Voer Hallo volgende opdracht in PowerShell tooallow WinRM via Hallo drie firewallprofielen (Domain, Private en openbare) en Hallo externe PowerShell-service inschakelen:
   
   ```PowerShell
    Enable-PSRemoting -force
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   ```
3. Hallo volgende firewall-regels tooallow Hallo RDP-verkeer inschakelen 

   ```PowerShell
    netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes
   ```   
4. Hello bestand- en printerdeling regel inschakelen zodat hello VM tooa ping-opdracht in Hallo virtueel netwerk reageren kan:

   ```PowerShell
    netsh advfirewall firewall set rule dir=in name="File and Printer Sharing (Echo Request - ICMPv4-In)" new enable=yes
   ``` 
5. Als Hallo VM deel van een domein uitmaken zal, controleert u Hallo na instellingen toomake ervoor dat de voormalige Hallo-instellingen worden niet hersteld. Hallo AD-beleidsregels die moeten worden gecontroleerd zijn Hallo volgende:

    - Hallo Windows Firewall-profielen inschakelen

        Computer Computerconfiguratie\Beleid\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **alle netwerkverbindingen beveiligen**

       Computer Computerconfiguratie\Beleid\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **alle netwerkverbindingen beveiligen**

    - Schakelt u RDP 

        Computer Computerconfiguratie\Beleid\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **inkomende extern bureaublad-uitzonderingen toestaan**

        Computer Computerconfiguratie\Beleid\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **inkomende extern bureaublad-uitzonderingen toestaan**

    - ICMP-V4 inschakelen

        Computer Computerconfiguratie\Beleid\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **uitzonderingen voor ICMP toestaan**

        Computer Computerconfiguratie\Beleid\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **uitzonderingen voor ICMP toestaan**

## <a name="verify-vm-is-healthy-secure-and-accessible-with-rdp"></a>Controleer of dat de VM bevindt zich in orde, veilige en toegankelijk zijn met RDP 
1. toomake ervoor Hallo schijf is in orde en consistent is, een selectievakje schijfbewerking op Hallo VM opnieuw uitvoeren:

    ```PowerShell
    Chkdsk /f
    ```
    Zorg ervoor dat Hallo rapport ziet u een schone en in goede orde schijf.

2. Hallo gegevens BCD (Boot Configuration)-instellingen. 

    > [!Note]
    > Zorg ervoor dat u deze opdrachten uitvoeren op een verhoogde CMD-venster en **niet** op PowerShell:
   
   ```CMD
   bcdedit /set {bootmgr} integrityservices enable
   
   bcdedit /set {default} device partition=C:
   
   bcdedit /set {default} integrityservices enable
   
   bcdedit /set {default} recoveryenabled Off
   
   bcdedit /set {default} osdevice partition=C:
   
   bcdedit /set {default} bootstatuspolicy IgnoreAllFailures
   ```
3. Controleer of dat die Hallo Windows Management Instrumentation-opslagplaats consistent is. tooperform deze, Voer Hallo volgende opdracht:

    ```PowerShell
    winmgmt /verifyrepository
    ```
    Als het Hallo-opslagplaats is beschadigd, raadpleegt u [WMI: beschadiging van de opslagplaats of niet](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not).

4. Zorg ervoor dat een andere toepassing geen gebruik van Hallo poort 3389 maakt. Deze poort wordt gebruikt voor Hallo RDP-service in Azure. U kunt uitvoeren **netstat - anob** toosee welke poorten in op Hallo VM gebruikt worden:

    ```PowerShell
    netstat -anob
    ```

5. Als Windows-VHD die u wilt dat tooupload Hallo een domeincontroller is, klikt u vervolgens als volgt:

    A. Ga als volgt [deze extra stappen](https://support.microsoft.com/kb/2904015) tooprepare Hallo schijf.

    B. Zorg ervoor dat u het DSRM-wachtwoord Hallo kent geval hebt u toostart Hallo VM in DSRM op een bepaald moment. Desgewenst kunt u toorefer toothis koppelen tooset Hallo [DSRM-wachtwoord](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx).

6. Zorg ervoor dat Hallo ingebouwde Administrator-account en wachtwoord tooyou bekend. U kunt tooreset Hallo huidige lokale administrator-wachtwoord wilt en zorg ervoor dat u kunt dit account toosign in tooWindows via Hallo RDP-verbinding gebruiken. Deze toegangsmachtiging wordt bepaald door Hallo 'Aanmelden toestaan via Extern bureaublad-Services' Group Policy object. U kunt dit object bekijken in de Editor voor lokaal groepsbeleid Hallo onder:

    Computer Configuration\Windows Settings\Security Beveiligingsinstellingen\Lokaal beleid\gebruikersrechten toewijzen

7. Controleer Hallo AD na het beleid toomake zeker dat u niet door uw RDP-toegang via RDP en ook niet vanaf het netwerk Hallo zijn geblokkeerd:

    - Computer Configuration\Windows Settings\Security Beveiligingsinstellingen\Lokaal beleid\gebruikersrechten rechten Assignment\Deny toegang toothis computer vanaf het Hallo-netwerk

    - Computer Configuration\Windows Settings\Security Beveiligingsinstellingen\Lokaal beleid\gebruikersrechten rechten Assignment\Deny aanmelden via Extern bureaublad-Services


8. Opnieuw opstarten Hallo VM toomake ervoor dat Windows nog steeds in orde is, kan worden bereikt met behulp van Hallo RDP-verbinding. U kunt op dit moment wilt toocreate een virtuele machine in uw lokale Hyper-V toomake ervoor Hallo die VM volledig wordt gestart en vervolgens controleren of het RDP bereikbaar is.

9. Verwijder eventuele extra Transport Driver Interface filters, zoals software waarmee TCP worden geanalyseerd pakketten of extra firewalls. U kunt dit ook bekijken op een later stadium na Hallo die VM is geïmplementeerd in Azure, indien nodig.

10. Verwijder alle andere software van derden en een stuurprogramma dat gerelateerde toophysical onderdelen of andere virtualisatietechnologie bevindt.

### <a name="install-windows-updates"></a>Windows-Updates installeren
Hallo ideaal configuratie is te**Hallo patch niveau van de machine op de meest recente Hallo Hallo**. Als dit niet mogelijk is, zorg er dan voor dat die Hallo volgende updates zijn geïnstalleerd:

|                       |                   |           |                                       Minimale versie x64       |                                      |                                      |                            |
|-------------------------|-------------------|------------------------------------|---------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|
| Onderdeel               | Binaire            | Windows 7 en Windows Server 2008 R2 | Windows 8 en WindowsServer 2012             | Windows 8.1 en Windows Server 2012 R2 | Windows 10 en Windows Server 2016 RS1 | Windows 10 RS2             |
| Storage                 | Disk.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17638 / 6.2.9200.21757 - KB3137061 | 6.3.9600.18203 - KB3137061           | -                                    | -                          |
|                         | Storport.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17188 / 6.2.9200.21306 - KB3018489 | 6.3.9600.18573 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.332             |
|                         | NTFS.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17623 / 6.2.9200.21743 - KB3121255 | 6.3.9600.18654 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.447             |
|                         | Iologmsg.dll      | 6.1.7601.23403 - KB3125574         | 6.2.9200.16384 - KB2995387                  | -                                    | -                                    | -                          |
|                         | Classpnp.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17061 / 6.2.9200.21180 - KB2995387 | 6.3.9600.18334 - KB3172614           | 10.0.14393.953 - KB4022715           | -                          |
|                         | Volsnap.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17047 / 6.2.9200.21165 - KB2975331 | 6.3.9600.18265 - KB3145384           | -                                    | 10.0.15063.0               |
|                         | partmgr.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.16681 - KB2877114                  | 6.3.9600.17401 - KB3000850           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | volmgr.sys        |                                    |                                             |                                      |                                      | 10.0.15063.0               |
|                         | Volmgrx.sys       | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | 10.0.15063.0               |
|                         | Msiscsi.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.21006 - KB2955163                  | 6.3.9600.18624 - KB4022726           | 10.0.14393.1066 - KB4022715          | 10.0.15063.447             |
|                         | Msdsm.sys         | 6.1.7601.23403 - KB3125574         | 6.2.9200.21474 - KB3046101                  | 6.3.9600.18592 - KB4022726           | -                                    | -                          |
|                         | MPIO.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.21190 - KB3046101                  | 6.3.9600.18616 - KB4022726           | 10.0.14393.1198 - KB4022715          | -                          |
|                         | Fveapi.dll        | 6.1.7601.23311 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.18294 - KB3172614           | 10.0.14393.576 - KB4022715           | -                          |
|                         | Fveapibase.dll    | 6.1.7601.23403 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.17415 - KB3172614           | 10.0.14393.206 - KB4022715           | -                          |
| Netwerk                 | netvsc.sys        | -                                  | -                                           | -                                    | 10.0.14393.1198 - KB4022715          | 10.0.15063.250 - KB4020001 |
|                         | mrxsmb10.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.22108 - KB4022724                  | 6.3.9600.18603 - KB4022726           | 10.0.14393.479 - KB4022715           | 10.0.15063.483             |
|                         | mrxsmb20.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.21548 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.483             |
|                         | Mrxsmb.sys        | 6.1.7601.23816 - KB4022722         | 6.2.9200.22074 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | Tcpip.sys         | 6.1.7601.23761 - KB4022722         | 6.2.9200.22070 - KB4022724                  | 6.3.9600.18478 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.447             |
|                         | HTTP.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17285 - KB3042553                  | 6.3.9600.18574 - KB4022726           | 10.0.14393.251 - KB4022715           | 10.0.15063.483             |
|                         | vmswitch.sys      | 6.1.7601.23727 - KB4022719         | 6.2.9200.22117 - KB4022724                  | 6.3.9600.18654 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.138             |
| Kern                    | Ntoskrnl.exe      | 6.1.7601.23807 - KB4022719         | 6.2.9200.22170 - KB4022718                  | 6.3.9600.18696 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.483             |
| Externe bureaubladservices | rdpcorets.dll     | 6.2.9200.21506 - KB4022719         | 6.2.9200.22104 - KB4022724                  | 6.3.9600.18619 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.0               |
|                         | TERMSRV.dll       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17048 - KB2973501                  | 6.3.9600.17415 - KB3000850           | 10.0.14393.0 - KB4022715             | 10.0.15063.0               |
|                         | termdd.sys        | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | Win32k.sys        | 6.1.7601.23807 - KB4022719         | 6.2.9200.22168 - KB4022718                  | 6.3.9600.18698 - KB4022726           | 10.0.14393.594 - KB4022715           | -                          |
|                         | rdpdd.dll         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | Rdpwd.sys         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
| Beveiliging                | Vervaldatum tooWannaCrypt | KB4012212                          | KB4012213                                   | KB4012213                            | KB4012606                            | KB4012606                  |
|                         |                   |                                    | KB4012216                                   |                                      | KB4013198                            | KB4013198                  |
|                         |                   | KB4012215                          | KB4012214                                   | KB4012216                            | KB4013429                            | KB4013429                  |
|                         |                   |                                    | KB4012217                                   |                                      | KB4013429                            | KB4013429                  |
       
### Wanneer toouse sysprep<a id="step23"></a>    

Sysprep is een proces dat kan worden uitgevoerd in een installatie van windows die wordt opnieuw ingesteld Hallo-installatie van Hallo systeem en wordt er een 'out of box Hallo ervaring' door te verwijderen van alle persoonlijke gegevens en het opnieuw instellen van verschillende onderdelen. U dit meestal doen als u wilt dat toocreate een sjabloon van waaruit u kunt verschillende andere VM's die een specifieke configuratie hebben. Dit wordt genoemd, een **gegeneraliseerd installatiekopie**.

Als in plaats daarvan u wilt dat alleen toocreate een VM van de ene schijf u hebt geen toouse sysprep. In dit geval maakt u alleen Hallo VM van wat wordt ook wel een **gespecialiseerde installatiekopie**.

Voor meer informatie over hoe toocreate een virtuele machine vanaf een speciale schijf, Zie:

- [Een virtuele machine vanaf een speciale schijf maken](create-vm-specialized.md)
- [Een virtuele machine vanaf een speciale VHD-schijf maken](https://azure.microsoft.com/resources/templates/201-vm-specialized-vhd/)

Als u een algemene installatiekopie toocreate wilt, moet u toorun sysprep. Zie voor meer informatie over Sysprep [hoe tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx). 

Ondersteunt deze generaliseren niet elke rol of de toepassing die op een Windows-computer geïnstalleerd. Dus voordat u deze procedure uitvoert, raadpleeg dan toohello volgende artikel toomake ervoor dat wordt die rol Hallo van die computer ondersteund door sysprep. Voor meer informatie [Sysprep-ondersteuning voor serverrollen](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

### <a name="steps-toogeneralize-a-vhd"></a>Stappen toogeneralize een VHD

>[!NOTE]
> Nadat u sysprep.exe als de opgegeven in de Hallo stappen te volgen uitvoert, Hallo VM uitschakelen en kan niet deze weer inschakelen totdat u een installatiekopie van het in Azure maakt.

1. Meld u aan toohello virtuele machine van Windows.
2. Voer **opdrachtprompt** als beheerder. 
3. Hallo-map te wijzigen: **%windir%\system32\sysprep**, en voer vervolgens **sysprep.exe**.
3. In Hallo **hulpprogramma voor systeemvoorbereiding** dialoogvenster, **System Voer Out-of-Box Experience (OOBE)**, en zorg ervoor dat Hallo **Generalize** selectievakje is ingeschakeld.

    ![Hulpprogramma voor systeemvoorbereiding](media/prepare-for-upload-vhd-image/syspre.png)
4. In **afsluitopties**, selecteer **afsluiten**.
5. Klik op **OK**.
6. Wanneer Sysprep is voltooid, sluit u Hallo VM. Gebruik geen **opnieuw** tooshut omlaag Hallo VM.
7. Hallo is VHD nu gereed toobe geüpload. Voor meer informatie over hoe toocreate een virtuele machine van een gegeneraliseerde schijf zien [een gegeneraliseerde VHD uploaden en toocreate een nieuwe virtuele machines in Azure gebruiken](sa-upload-generalized.md).


## <a name="complete-recommended-configurations"></a>Voert u de aanbevolen configuraties
Hallo na instellingen hebben geen invloed op de VHD uploaden. Echter, wordt aangeraden dat u ze had geconfigureerd.

* Hallo installeren [Azure VM's Agent](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Vervolgens kunt u VM-extensies inschakelen. Hallo VM-extensies implementeren de meeste essentiële functionaliteit Hallo dat u mogelijk wilt toouse met uw VMs zoals het opnieuw instellen van wachtwoorden, RDP configureren, enzovoort. Zie voor meer informatie:

    - [VM-Agent en -extensies: deel 1](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/)
    - [VM-Agent en -extensies – deel 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)
* Hallo Dump logboek kan helpen bij het oplossen van problemen met het vastlopen van Windows worden. Hallo Dump logboekverzameling inschakelen:
  
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "AutoReboot" -Value 0 -Type DWord
    New-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps'
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
    Als u ontvangt fouten tijdens een Hallo procedurele stappen in dit artikel, betekent dit dat de registersleutels Hallo al bestaat. In dit geval gebruiken Hallo opdrachten in plaats daarvan te volgen:

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
*  Nadat Hallo VM is gemaakt in Azure, wordt u aangeraden dat u Hallo wisselbestand op Hallo 'Tijdelijke station' volume tooimprove prestaties plaatst. U kunt instellen dit als volgt:

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management' -name "PagingFiles" -Value "D:\pagefile"
    ```
Als er een gegevensschijf die is aangesloten toohello VM, is Hallo tijdelijke stationsvolume stationsletter doorgaans "D" Deze aanwijzing mogelijk verschillen, afhankelijk van Hallo aantal beschikbare stations en Hallo-instellingen die u aanbrengt.

## <a name="next-steps"></a>Volgende stappen
* [Uploaden van een virtuele machine van Windows-installatiekopie tooAzure voor implementaties van Resource Manager](upload-generalized-managed.md)


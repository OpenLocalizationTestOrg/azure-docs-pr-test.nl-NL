<!--author=alkohli last changed: 03/17/16-->

#### <a name="toodownload-hotfixes"></a>toodownload hotfixes
Volgende stappen toodownload Hallo software-update vanaf Microsoft Update-catalogus Hallo Hallo uitvoeren.

1. Start Internet Explorer en navigeer te[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Als dit de eerste keer dat u Microsoft Update-catalogus Hallo op deze computer is, klikt u op **installeren** wanneer na vragen aan gebruiker tooinstall Hallo-invoegtoepassing voor Microsoft Update-catalogus.
    ![Installeren van de catalogus](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)
3. In het zoekvak Hallo Hallo Microsoft Update-catalogus, invoeren Hallo-Knowledge Base (KB) van de hotfix Hallo gewenste toodownload, bijvoorbeeld **3121901**, en klik vervolgens op **Search**.
   
    Hallo hotfix wordt weergegeven, bijvoorbeeld **cumulatieve Software bundel Update 2.0 voor StorSimple 8000-serie**.
   
    ![Catalogus doorzoeken](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. Klik op **Add**. Hallo-update is toohello mandje toegevoegd.
5. Zoeken naar aanvullende hotfixes die worden vermeld in de bovenstaande Hallo-tabel (**3121900**, **3080728**, **3090322**, en **3121899**), en elk toevoegen Hallo mandje.
6. Klik op **Mandje weergeven**.
7. Klik op **Downloaden**. Opgeven of **Bladeren** tooa lokale locatie waar u Hallo tooappear downloadt. Hallo-updates worden gedownload toohello opgegeven locatie en in een submap met dezelfde naam als de update Hallo Hallo geplaatst. Hallo-map kan ook worden gekopieerde tooa netwerkshare zijn die bereikbaar is vanaf het Hallo-apparaat.

> [!NOTE]
> Hallo hotfixes moet toegankelijk is vanaf beide domeincontrollers toodetect een potentiële fout van berichten van Hallo peer-controller.
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall en controleer of de normale modus hotfixes
Hallo tooinstall stappen te volgen uitvoeren en controleer of de normale modus hotfixes. Als u deze hebt geïnstalleerd met behulp van hello Azure-Portal, gaat u verder te[installeren en testen van onderhoud modus hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).

1. tooinstall hello hotfixes toegang Hallo Windows PowerShell-interface op de seriële console van het StorSimple-apparaat. Ga als volgt Hallo gedetailleerde instructies in [PuTTy gebruiken tooconnect toohello seriële console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). Bij de opdrachtprompt hello, drukt u op **Enter**.
2. Selecteer **optie 1** toolog op toohello apparaat met volledige toegang.
3. tooinstall hello hotfix op Hallo-opdrachtprompt, typt:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Gebruik IP in plaats van DNS in sharepad in Hallo hierboven opdracht. de parameter credential Hallo wordt alleen gebruikt als u toegang een geverifieerde share tot.
   
    Het is raadzaam dat u Hallo referentie parameter tooaccess shares. Zelfs shares die geopend te zijn 'iedereen' zijn meestal toounauthenticated gebruikers niet worden geopend.
   
    Hieronder ziet u een voorbeeld van de uitvoer.
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```
4. Type **Y** wanneer na vragen aan gebruiker tooconfirm Hallo hotfix-installatie.
5. Hallo-update controleren met behulp van Hallo `Get-HcsUpdateStatus` cmdlet.
   
    Hallo ziet volgende voorbeelduitvoer Hallo update uitgevoerd. Hallo `RunInprogress` worden `True` wanneer Hallo update wordt uitgevoerd.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 12/21/2015 10:36:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Hallo voorbeelduitvoer na geeft aan dat of Hallo-update is voltooid. Hallo `RunInProgress` worden `False` wanneer Hallo-update is voltooid.
   
    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 12/21/2015 10:59:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > In sommige gevallen kan Hallo cmdlet rapporten `False` wanneer hello wordt nog steeds bijgewerkt. tooensure die Hallo hotfix is voltooid, wacht een paar minuten, voer deze opdracht opnieuw uit en controleer of deze Hallo `RunInProgress` is `False`. Hallo-hotfix is voltooid, als het.

6. Na het Hallo-software is-update voltooid, herhaalt u stap 3-5 tooinstall en monitor Hallo SaaS agent en MDS-agent. Zorg ervoor dat `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` is geïnstalleerd voordat het `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.
7. Controleer of softwareversies Hallo-systeem. Type:
   
    `Get-HcsSystem`
   
    U ziet de volgende versies Hallo:
   
   * HcsSoftwareVersion: 6.3.9600.17673
   * CisAgentVersion: 1.0.9150.0
   * MdsAgentVersion: 30.0.4698.13
     
     Als Hallo versienummers niet wijzigen nadat Hallo update hebt toegepast, geeft u aan dat deze hotfix Hallo tooapply is mislukt. Neem in dat geval contact op met [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) voor verdere hulp.
8. Herhaal stap 3-5 tooinstall Hallo resterende hotfixes reguliere-modus.
   
   * Hallo LSI stuurprogramma - KB3121900
   * Hallo Storport-update - KB3080728
   * Hallo Spaceport update - KB3090322

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall en onderhoud modus hotfixes controleren
Gebruik KB3121899 tooinstall schijf firmware-updates. Deze updates zijn verstoren en toocomplete ongeveer 30 minuten duren. U kunt tooinstall deze in een gepland onderhoud-venster door de verbindende toohello seriële console van apparaat.

Houd er rekening mee dat als de firmware van de schijf al bijgewerkt is, u niet tooinstall deze updates hoeft. Voer Hallo `Get-HcsUpdateAvailability` cmdlet uit Hallo apparaat seriële console toocheck als updates beschikbaar zijn en of Hallo-updates zijn verstoren (onderhoudsmodus) of ononderbroken (normale modus) updates.

tooinstall hello schijf firmware-updates, volgt u onderstaande Hallo-instructies.

1. Hallo-apparaat in hello onderhoudsmodus plaatsen. Houd er rekening mee dat u Windows PowerShell op afstand niet gebruiken moet bij het verbinden van tooa apparaat in de onderhoudsmodus. In plaats daarvan deze cmdlet uitvoeren op Hallo apparaat controller wanneer verbonden zijn via de seriële console van Hallo apparaat. Type:
   
    `Enter-HcsMaintenanceMode`
   
    Hieronder ziet u een voorbeeld van de uitvoer.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17664
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    Beide domeincontrollers Hallo start opnieuw op in de onderhoudsmodus.
2. tooinstall hello schijf firmware-update, type:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Hieronder ziet u een voorbeeld van de uitvoer.
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. Monitor Hallo installeren uitgevoerd met `Get-HcsUpdateStatus` opdracht. Hallo update is voltooid wanneer hello `RunInProgress` wijzigingen te`False`.
4. Nadat het Hallo-installatie is voltooid, wordt een Hallo controller welke Hallo onderhoud modus hotfix is geïnstalleerd wordt opnieuw gestart. Meld u aan als optie 1 met volledige toegang en controleer of firmwareversie Hallo-schijf. Type:
   
   `Get-HcsFirmwareVersion`
   
   Hallo verwacht schijf firmware-versies zijn:
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   Hieronder ziet u een voorbeeld van de uitvoer.
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17664
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
         ActiveBIOS:0.45.0006
         BackupBIOS:0.45.0008
         MainCPLD:17.0.0005
         ActiveBMCRoot:2.0.000E
         BackupBMCRoot:2.0.000E
         BMCBoot:2.0.0001
         LsiFirmware:19.00.00.00
         LsiBios:07.37.00.00
         Battery1Firmware:06.29
         Battery2Firmware:06.29
         DomFirmware:X231600
         CanisterFirmware:3.5.0.32
         CanisterBootloader:5.03
         CanisterConfigCRC:0xD1B030A4
         CanisterVPDStructure:0x06
         CanisterGEMCPLD:0x17
         CanisterVPDCRC:0xEE3504B4
         MidplaneVPDStructure:0x0C
         MidplaneVPDCRC:0xA6BD4F64
         MidplaneCPLD:0x10
         PCM1Firmware:1.00|1.05
         PCM1VPDStructure:0x05
         PCM1VPDCRC:0x41BEF99C
         PCM2Firmware:1.00|1.05
         PCM2VPDStructure:0x05
         PCM2VPDCRC:0x41BEF99C
   
         DisksFirmware
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
   
    Voer Hallo `Get-HcsFirmwareVersion` opdracht in het tweede controller tooverify hello, die de softwareversie Hallo is bijgewerkt. Vervolgens kunt u de onderhoudsmodus Hallo afsluiten. toodo dus, typt u na de opdracht voor elke domeincontroller apparaat Hallo:
   
   `Exit-HcsMaintenanceMode`
5. Hallo-controllers opnieuw opstarten bij het afsluiten van de onderhoudsmodus. Na het Hallo schijf firmware updates met succes zijn toegepast en Hallo apparaat onderhoudsmodus, return toohello klassieke Azure-portal is afgesloten. Houd er rekening mee dat Hallo-portal niet altijd weergegeven dat u Hallo onderhoud modus updates geïnstalleerd voor 24 uur.


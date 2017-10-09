<!--author=alkohli last changed: 08/21/17-->

#### <a name="toodownload-hotfixes"></a>toodownload hotfixes

Volgende stappen toodownload Hallo software-update vanaf Microsoft Update-catalogus Hallo Hallo uitvoeren.

1. Start Internet Explorer en navigeer te[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Als dit de eerste keer dat u Microsoft Update-catalogus Hallo op deze computer is, klikt u op **installeren** wanneer na vragen aan gebruiker tooinstall Hallo-invoegtoepassing voor Microsoft Update-catalogus.

    ![Catalogus installeren](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. In het zoekvak Hallo Hallo Microsoft Update-catalogus, invoeren Hallo-Knowledge Base (KB) van de hotfix Hallo gewenste toodownload, bijvoorbeeld **4037264**, en klik vervolgens op **Search**.
   
    Hallo hotfix wordt weergegeven, bijvoorbeeld **cumulatieve Software bundel Update 5.0 voor StorSimple 8000-serie**.
   
    ![Catalogus doorzoeken](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. Klik op **Downloaden**. Opgeven of **Bladeren** tooa lokale locatie waar u Hallo tooappear downloadt. Klik op Hallo bestanden toodownload toohello opgegeven locatie en de map. Hallo-map kan ook worden gekopieerde tooa netwerkshare zijn die bereikbaar is vanaf het Hallo-apparaat.
5. Zoeken naar aanvullende hotfixes die worden vermeld in de bovenstaande Hallo-tabel (**4037266**), en specifieke mappen toohello downloaden Hallo overeenkomt bestanden zoals vermeld in de voorgaande tabel Hallo.

> [!NOTE]
> Hallo hotfixes moet toegankelijk is vanaf beide domeincontrollers toodetect een potentiële fout van berichten van Hallo peer-controller.
>
> Hallo hotfixes moeten in 3 afzonderlijke mappen worden gekopieerd. Bijvoorbeeld, Hallo apparaat Cis/software/MDS agentupdate kan worden gekopieerd _FirstOrderUpdate_ map alle Hallo andere ononderbroken updates kunnen worden gekopieerd in Hallo _SecondOrderUpdate_ map, en Onderhoud modus updates gekopieerd _ThirdOrderUpdate_ map.

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall en controleer of de normale modus hotfixes

Hallo tooinstall stappen te volgen uitvoeren en controleer of de normale modus hotfixes. Als u deze hebt geïnstalleerd met behulp van hello Azure-portal, gaat u verder te[installeren en testen van onderhoud modus hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).

1. tooinstall hello hotfixes toegang Hallo Windows PowerShell-interface op de seriële console van het StorSimple-apparaat. Ga als volgt Hallo gedetailleerde instructies in [PuTTy gebruiken tooconnect toohello seriële console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console). Bij de opdrachtprompt hello, drukt u op **Enter**.
2. Selecteer **optie 1** toolog op toohello apparaat met volledige toegang. Het is raadzaam dat u Hallo hotfix op Hallo passieve domeincontroller eerst installeren.
3. tooinstall hello hotfix op Hallo-opdrachtprompt, typt:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Gebruik IP in plaats van DNS in sharepad in Hallo hierboven opdracht. de parameter credential Hallo wordt alleen gebruikt als u toegang een geverifieerde share tot.
   
    Het is raadzaam dat u Hallo referentie parameter tooaccess shares. Zelfs shares die geopend te zijn 'iedereen' zijn meestal toounauthenticated gebruikers niet worden geopend.
   
4. Hallo wachtwoord wanneer u wordt gevraagd op te geven. Een voorbeeld van uitvoer voor de installatie Hallo eerste volgorde updates worden hieronder weergegeven. Hallo eerste volgorde bijwerken moet u toopoint toohello specifiek bestand.

    >[!NOTE] 
    > Installeer Hallo _HcsSoftwareUpdate.exe_ eerste. Nadat deze installatie is voltooid, installeer _CisMdsAgentUpdate.exe_.
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. Type **Y** wanneer na vragen aan gebruiker tooconfirm Hallo hotfix-installatie.
6. Hallo-update controleren met behulp van Hallo `Get-HcsUpdateStatus` cmdlet. Hallo update wordt eerst op Hallo passieve controller voltooid. Zodra Hallo passieve domeincontroller wordt bijgewerkt, zal er een failover en Hallo update worden vervolgens toegepast op Hallo andere domeincontroller. Hallo-update is voltooid wanneer beide domeincontrollers Hallo zijn bijgewerkt.
   
    Hallo ziet volgende voorbeelduitvoer Hallo update uitgevoerd. Hallo `RunInprogress` is `True` wanneer Hallo update wordt uitgevoerd.

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Hallo voorbeelduitvoer na geeft aan dat of Hallo-update is voltooid. Hallo `RunInProgress` is `False` wanneer Hallo-update is voltooid.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > In sommige gevallen kan Hallo cmdlet rapporten `False` wanneer hello wordt nog steeds bijgewerkt. tooensure die Hallo hotfix is voltooid, wacht een paar minuten, voer deze opdracht opnieuw uit en controleer of deze Hallo `RunInProgress` is `False`. Hallo-hotfix is voltooid, als het.

7. Nadat het Hallo software-update is voltooid, controleert u of softwareversies Hallo-systeem. Type:
   
    `Get-HcsSystem`
   
    U ziet de volgende versies Hallo:
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    Hallo-versienummer niet worden gewijzigd nadat Hallo update hebt toegepast, geeft aan dat hotfix Hallo tooapply is mislukt. Neem in dat geval contact op met [Microsoft Support](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) voor verdere hulp.
     
    > [!IMPORTANT]
    > U moet opnieuw opstarten Hallo actieve controller via Hallo `Restart-HcsController` cmdlet alvorens toe te passen Hallo volgende update.
     
8. Herhaal stap 3-6 tooinstall hello _CisMDSAgentupdate.exe_ agent gedownload tooyour _FirstOrderUpdate_ map.
8. Herhaal stap 3-6 tooinstall Hallo tweede volgorde updates. 

    > [!NOTE] 
    > Tweede volgorde updates, meerdere updates kunnen worden geïnstalleerd door het uitvoeren van alleen Hallo `Start-HcsHotfix cmdlet` en toohello map tweede volgorde updates aan te wijzen. Hallo-cmdlet wordt alle Hallo-updates die beschikbaar zijn in de map Hallo uitgevoerd. Als een update is al geïnstalleerd, wordt de logica voor het bijwerken van Hallo detecteren die en die update niet van toepassing.

    Nadat alle Hallo-hotfixes zijn geïnstalleerd, gebruikt u Hallo `Get-HcsSystem` cmdlet. Hallo-versies worden:
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall en onderhoud modus hotfixes controleren

Gebruik KB4037263 tooinstall schijf firmware-updates. Deze updates zijn verstoren en toocomplete ongeveer 30 minuten duren. U kunt tooinstall deze in een gepland onderhoud-venster door de verbindende toohello seriële console van apparaat.

> [!NOTE] 
> Als de firmware van de schijf al bijgewerkt is, hoeft u niet tooinstall deze updates. Voer Hallo `Get-HcsUpdateAvailability` cmdlet uit Hallo apparaat seriële console toocheck als updates beschikbaar zijn en of Hallo-updates zijn verstoren (onderhoudsmodus) of ononderbroken (normale modus) updates.

tooinstall hello schijf firmware-updates, volgt u onderstaande Hallo-instructies.

1. Hallo-apparaat in hello onderhoudsmodus plaatsen. 

    > [!NOTE] 
    > Gebruik geen Windows PowerShell op afstand verbinding te maken met tooa apparaat in de onderhoudsmodus. In plaats daarvan deze cmdlet uitvoeren op Hallo apparaat controller wanneer verbonden zijn via de seriële console van Hallo apparaat.

    tooplace hello controller in de onderhoudsmodus bevindt, typt u:
   
    `Enter-HcsMaintenanceMode`
   
    Hieronder ziet u een voorbeeld van de uitvoer.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
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
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
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
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   Hieronder ziet u een voorbeeld van de uitvoer.
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17845
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
           ActiveBIOS:0.45.0010
              BackupBIOS:0.45.0006
              MainCPLD:17.0.000b
              ActiveBMCRoot:2.0.001F
              BackupBMCRoot:2.0.001F
              BMCBoot:2.0.0002
              LsiFirmware:20.00.04.00
              LsiBios:07.37.00.00
              Battery1Firmware:06.2C
              Battery2Firmware:06.2C
              DomFirmware:X231600
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0x9134777A
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x19
              CanisterVPDCRC:0x142F7DC2
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:1.00|1.05
              PCM1VPDStructure:0x05
              PCM1VPDCRC:0x41BEF99C
              PCM2Firmware:1.00|1.05
              PCM2VPDStructure:0x05
              PCM2VPDCRC:0x41BEF99C

           EbodFirmware
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0xB23150F8
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x14
              CanisterVPDCRC:0xBAA55828
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:3.11
              PCM1VPDStructure:0x03
              PCM1VPDCRC:0x6B58AD13
              PCM2Firmware:3.11
              PCM2VPDStructure:0x03
              PCM2VPDCRC:0x6B58AD13

           DisksFirmware
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
   
    Voer Hallo `Get-HcsFirmwareVersion` opdracht in het tweede controller tooverify hello, die de softwareversie Hallo is bijgewerkt. Vervolgens kunt u de onderhoudsmodus Hallo afsluiten. toodo dus, typt u na de opdracht voor elke domeincontroller apparaat Hallo:
   
   `Exit-HcsMaintenanceMode`

5. Hallo-controllers opnieuw opstarten bij het afsluiten van de onderhoudsmodus. Na het Hallo schijf firmware updates met succes zijn toegepast en Hallo apparaat onderhoudsmodus, return toohello Azure-portal is afgesloten. Houd er rekening mee dat Hallo-portal niet altijd weergegeven dat u Hallo onderhoud modus updates geïnstalleerd voor 24 uur.


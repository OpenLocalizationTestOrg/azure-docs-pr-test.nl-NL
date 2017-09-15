<!--author=alkohli last changed: 02/10/17-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="56907-101">Hotfixes downloaden</span><span class="sxs-lookup"><span data-stu-id="56907-101">To download hotfixes</span></span>

<span data-ttu-id="56907-102">Voer de volgende stappen uit om de software-update te downloaden uit de Microsoft Update-catalogus.</span><span class="sxs-lookup"><span data-stu-id="56907-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="56907-103">Start Internet Explorer en blader naar [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="56907-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="56907-104">Als dit de eerste keer is dat u de Microsoft Update-catalogus op deze computer gebruikt, klikt u op **Installeren** wanneer u wordt gevraagd of u de invoegtoepassing voor de Microsoft Update-catalogus wilt installeren.</span><span class="sxs-lookup"><span data-stu-id="56907-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

    ![Catalogus installeren](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="56907-106">Voer in het zoekvak van de Microsoft Update-catalogus het KB-nummer (Knowledge Base) in van de hotfix die u wilt downloaden, bijvoorbeeld **4011839**. Klik vervolgens op **Zoeken**.</span><span class="sxs-lookup"><span data-stu-id="56907-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **4011839**, and then click **Search**.</span></span>
   
    <span data-ttu-id="56907-107">De lijst met hotfixes wordt weergegeven, bijvoorbeeld **Cumulatieve softwarebundel update 4.0 voor StorSimple 8000-serie**.</span><span class="sxs-lookup"><span data-stu-id="56907-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 4.0 for StorSimple 8000 Series**.</span></span>
   
    ![Catalogus doorzoeken](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)

4. <span data-ttu-id="56907-109">Klik op **Downloaden**.</span><span class="sxs-lookup"><span data-stu-id="56907-109">Click **Download**.</span></span> <span data-ttu-id="56907-110">Typ of **blader naar** een lokale locatie waar u de downloads wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="56907-110">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="56907-111">Klik op de bestanden te downloaden naar de opgegeven locatie en de map.</span><span class="sxs-lookup"><span data-stu-id="56907-111">Click the files to download to the specified location and folder.</span></span> <span data-ttu-id="56907-112">De map kan ook worden gekopieerd naar een netwerkshare die bereikbaar is vanaf het apparaat.</span><span class="sxs-lookup"><span data-stu-id="56907-112">The folder can also be copied to a network share that is reachable from the device.</span></span>
5. <span data-ttu-id="56907-113">Zoeken naar aanvullende hotfixes die worden vermeld in de bovenstaande tabel (**4011841**), en de bijbehorende bestanden downloaden naar de specifieke mappen zoals vermeld in de voorgaande tabel.</span><span class="sxs-lookup"><span data-stu-id="56907-113">Search for any additional hotfixes listed in the table above (**4011841**), and download the corresponding files to the specific folders as listed in the preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="56907-114">De hotfixes moet toegankelijk zijn via beide domeincontrollers voor het detecteren van mogelijke foutberichten van de peer-controller.</span><span class="sxs-lookup"><span data-stu-id="56907-114">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
>
> <span data-ttu-id="56907-115">De hotfixes moeten naar 3 afzonderlijke mappen worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="56907-115">The hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="56907-116">Bijvoorbeeld, het bijwerken van het configuratie-items/software/MDS agent kan worden gekopieerd _FirstOrderUpdate_ map, alle andere ononderbroken updates kunnen worden gekopieerd de _SecondOrderUpdate_ map, en Onderhoud modus updates gekopieerd _ThirdOrderUpdate_ map.</span><span class="sxs-lookup"><span data-stu-id="56907-116">For example, the device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all the other non-disruptive updates could be copied in the _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="56907-117">Hotfixes in de normale modus installeren en controleren</span><span class="sxs-lookup"><span data-stu-id="56907-117">To install and verify regular mode hotfixes</span></span>

<span data-ttu-id="56907-118">Voer de volgende stappen uit om hotfixes in de normale modus te installeren en te controleren.</span><span class="sxs-lookup"><span data-stu-id="56907-118">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="56907-119">Als u deze al hebt geïnstalleerd met de klassieke Azure-portal, gaat u verder met [Hotfixes in de onderhoudsmodus installeren en controleren](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="56907-119">If you already installed them using the Azure classic portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="56907-120">U installeert de hotfixes door de Windows PowerShell-interface op de seriële console van het StorSimple-apparaat te openen.</span><span class="sxs-lookup"><span data-stu-id="56907-120">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="56907-121">Volg de gedetailleerde instructies in [PuTTY gebruiken om verbinding te maken met de seriële console van het apparaat](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="56907-121">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="56907-122">Druk op de opdrachtregel op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="56907-122">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="56907-123">Selecteer **Optie 1** als u zich met volledige toegang wilt aanmelden bij het apparaat.</span><span class="sxs-lookup"><span data-stu-id="56907-123">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="56907-124">U wordt geadviseerd om de hotfix eerst op de passieve controller te installeren.</span><span class="sxs-lookup"><span data-stu-id="56907-124">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="56907-125">Installeer de hotfix door achter de opdrachtprompt het volgende te typen:</span><span class="sxs-lookup"><span data-stu-id="56907-125">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="56907-126">Gebruik in bovenstaande opdracht IP in plaats van DNS in het Pad naar share.</span><span class="sxs-lookup"><span data-stu-id="56907-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="56907-127">De referentieparameter wordt alleen gebruikt voor toegang tot een geverifieerde share.</span><span class="sxs-lookup"><span data-stu-id="56907-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="56907-128">U wordt geadviseerd om de referentieparameter te gebruiken voor toegang tot shares.</span><span class="sxs-lookup"><span data-stu-id="56907-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="56907-129">Zelfs shares die voor 'iedereen' zijn geopend, zijn gewoonlijk niet geopend voor niet-geverifieerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="56907-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="56907-130">Geef het wachtwoord op wanneer dit wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="56907-130">Supply the password when prompted.</span></span>
   
    <span data-ttu-id="56907-131">Hieronder ziet u een voorbeeld van de uitvoer voor de installatie van belangrijkste updates.</span><span class="sxs-lookup"><span data-stu-id="56907-131">A sample output for installing the first order updates is shown below.</span></span> <span data-ttu-id="56907-132">Voor de eerste update order moet u verwijzen naar het specifieke bestand.</span><span class="sxs-lookup"><span data-stu-id="56907-132">For the first order update, you need to point to the specific file.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. <span data-ttu-id="56907-133">Typ **J** wanneer u wordt gevraagd de hotfixinstallatie te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="56907-133">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="56907-134">Bewaak de update met behulp van de cmdlet `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="56907-134">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="56907-135">De update wordt eerst voltooid op de passieve controller.</span><span class="sxs-lookup"><span data-stu-id="56907-135">The update will first complete on the passive controller.</span></span> <span data-ttu-id="56907-136">Zodra de passieve controller is bijgewerkt, wordt er een failover uitgevoerd en wordt de update toegepast op de andere controller.</span><span class="sxs-lookup"><span data-stu-id="56907-136">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="56907-137">De update is voltooid wanneer beide controllers zijn bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="56907-137">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="56907-138">Hieronder ziet u een voorbeeld van uitvoer terwijl de update nog bezig is.</span><span class="sxs-lookup"><span data-stu-id="56907-138">The following sample output shows the update in progress.</span></span> <span data-ttu-id="56907-139">De `RunInprogress` is `True` wanneer de update nog bezig is.</span><span class="sxs-lookup"><span data-stu-id="56907-139">The `RunInprogress` will be `True` when the update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 02/03/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="56907-140">In de volgende voorbeelduitvoer wordt aangegeven dat de update is voltooid.</span><span class="sxs-lookup"><span data-stu-id="56907-140">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="56907-141">De `RunInProgress` is `False` wanneer de update is voltooid.</span><span class="sxs-lookup"><span data-stu-id="56907-141">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 02/03/2017 9:15:55 AM
    LastUpdateTimestamp : 02/03/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="56907-142">Af en toe meldt de cmdlet `False` wanneer de update nog wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="56907-142">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="56907-143">Als u er zeker van wilt zijn dat de hotfix is voltooid, wacht u enkele minuten en voert u deze opdracht opnieuw uit. Controleer of de `RunInProgress` `False` is.</span><span class="sxs-lookup"><span data-stu-id="56907-143">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="56907-144">Als dat het geval is, is de hotfix voltooid.</span><span class="sxs-lookup"><span data-stu-id="56907-144">If it is, then the hotfix has completed.</span></span>

6. <span data-ttu-id="56907-145">Wanneer de software-update is voltooid, controleert u de versies van de systeemsoftware.</span><span class="sxs-lookup"><span data-stu-id="56907-145">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="56907-146">Type:</span><span class="sxs-lookup"><span data-stu-id="56907-146">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="56907-147">De volgende versies moeten worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="56907-147">You should see the following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 4.0`
   *  `HcsSoftwareVersion: 6.3.9600.17820`
   
    <span data-ttu-id="56907-148">Als het versienummer niet is gewijzigd nadat de update is toegepast, kon de hotfix blijkbaar niet worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="56907-148">If the version number does not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="56907-149">Neem in dat geval contact op met [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) voor verdere hulp.</span><span class="sxs-lookup"><span data-stu-id="56907-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="56907-150">U moet opnieuw opstarten van de actieve controller via de `Restart-HcsController` cmdlet voordat u de volgende update.</span><span class="sxs-lookup"><span data-stu-id="56907-150">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the next update.</span></span>
     
7. <span data-ttu-id="56907-151">Herhaal stap 3-5 voor de installatie van de configuratie-items/MDS-agent die is gedownload naar uw _FirstOrderUpdate_ map.</span><span class="sxs-lookup"><span data-stu-id="56907-151">Repeat steps 3-5 to install the Cis/MDS agent downloaded to your _FirstOrderUpdate_ folder.</span></span> 
8. <span data-ttu-id="56907-152">Herhaal stap 3 t/m 5 om de tweede belangrijkste updates te installeren.</span><span class="sxs-lookup"><span data-stu-id="56907-152">Repeat steps 3-5 to install the second order updates.</span></span> <span data-ttu-id="56907-153">**Tweede volgorde updates, meerdere updates kunnen worden geïnstalleerd door het uitvoeren van alleen de `Start-HcsHotfix cmdlet` en die verwijst naar de map waar de tweede volgorde updates zich bevinden. De cmdlet wordt uitgevoerd van alle updates die beschikbaar zijn in de map.**</span><span class="sxs-lookup"><span data-stu-id="56907-153">**For second order updates, multiple updates can be installed by just running the `Start-HcsHotfix cmdlet` and pointing to the folder where second order updates are located. The cmdlet will execute all the updates available in the folder.**</span></span> <span data-ttu-id="56907-154">Als een update al is geïnstalleerd, wordt dit door de updatelogica gedetecteerd en wordt die update niet toegepast.</span><span class="sxs-lookup"><span data-stu-id="56907-154">If an update is already installed, the update logic will detect that and not apply that update.</span></span> 

<span data-ttu-id="56907-155">Nadat alle hotfixes zijn geïnstalleerd, gebruikt u de cmdlet `Get-HcsSystem`.</span><span class="sxs-lookup"><span data-stu-id="56907-155">After all the hotfixes are installed, use the `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="56907-156">De versies moeten zijn:</span><span class="sxs-lookup"><span data-stu-id="56907-156">The versions should be:</span></span>

   * `CisAgentVersion:  1.0.9441.0`
   * `MdsAgentVersion: 35.2.2.0`
   * `Lsisas2Version: 2.0.78.00`


#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="56907-157">Hotfixes in de onderhoudsmodus installeren en controleren</span><span class="sxs-lookup"><span data-stu-id="56907-157">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="56907-158">Gebruik KB4011837 om updates van de schijffirmware te installeren.</span><span class="sxs-lookup"><span data-stu-id="56907-158">Use KB4011837 to install disk firmware updates.</span></span> <span data-ttu-id="56907-159">Dit zijn updates waarvoor de computer opnieuw moet worden opgestart. De uitvoering ervan neemt ongeveer 30 minuten in beslag.</span><span class="sxs-lookup"><span data-stu-id="56907-159">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="56907-160">U kunt ervoor kiezen om deze te installeren in een gepland onderhoudsvenster door verbinding te maken met de console van het seriële apparaat.</span><span class="sxs-lookup"><span data-stu-id="56907-160">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="56907-161">Als de schijffirmware van de schijf al is bijgewerkt, hoeft u deze updates niet te installeren.</span><span class="sxs-lookup"><span data-stu-id="56907-161">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="56907-162">Voer de cmdlet `Get-HcsUpdateAvailability` uit vanaf de console van het seriële apparaat om te controleren of er updates beschikbaar zijn en of de computer voor de updates opnieuw moet worden opgestart (onderhoudsmodus) of niet (normale modus).</span><span class="sxs-lookup"><span data-stu-id="56907-162">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="56907-163">Volg onderstaande instructies om de updates van de schijffirmware te installeren.</span><span class="sxs-lookup"><span data-stu-id="56907-163">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="56907-164">Plaats het apparaat in de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="56907-164">Place the device in the maintenance mode.</span></span> <span data-ttu-id="56907-165">**Gebruik Windows PowerShell op afstand wanneer u verbinding maakt met een apparaat in de onderhoudsmodus. In plaats daarvan moet u deze cmdlet op de apparaatcontroller uitvoeren wanneer deze is verbonden via de console van het seriële apparaat.**</span><span class="sxs-lookup"><span data-stu-id="56907-165">**Note that you should not use Windows PowerShell remoting when connecting to a device in maintenance mode. Instead run this cmdlet on the device controller when connected through the device serial console.**</span></span> <span data-ttu-id="56907-166">Type:</span><span class="sxs-lookup"><span data-stu-id="56907-166">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="56907-167">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="56907-167">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="56907-168">Beide controllers starten vervolgens opnieuw op in de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="56907-168">Both the controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="56907-169">Typ het volgende om de update van de schijffirmware te installeren:</span><span class="sxs-lookup"><span data-stu-id="56907-169">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="56907-170">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="56907-170">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="56907-171">Bewaak de installatievoortgang met de opdracht `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="56907-171">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="56907-172">De update is voltooid als de `RunInProgress` verandert in `False`.</span><span class="sxs-lookup"><span data-stu-id="56907-172">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="56907-173">Wanneer de installatie is voltooid, wordt de controller waarop de hotfix van de onderhoudsmodus is geïnstalleerd, opnieuw opstart.</span><span class="sxs-lookup"><span data-stu-id="56907-173">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="56907-174">Meld u aan als in optie 1 met volledige toegang en controleer de versie van de schijffirmware.</span><span class="sxs-lookup"><span data-stu-id="56907-174">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="56907-175">Type:</span><span class="sxs-lookup"><span data-stu-id="56907-175">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="56907-176">De verwachte versies van de schijffirmware zijn:</span><span class="sxs-lookup"><span data-stu-id="56907-176">The expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N002, 0106`
   
   <span data-ttu-id="56907-177">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="56907-177">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17820
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
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
   
    <span data-ttu-id="56907-178">Voer op de tweede controller de opdracht `Get-HcsFirmwareVersion` uit om te controleren of de versie van de software is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="56907-178">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="56907-179">Daarna kunt u de onderhoudsmodus afsluiten.</span><span class="sxs-lookup"><span data-stu-id="56907-179">You can then exit the maintenance mode.</span></span> <span data-ttu-id="56907-180">Daartoe typt u de volgende opdracht voor elke apparaatcontroller:</span><span class="sxs-lookup"><span data-stu-id="56907-180">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="56907-181">De controllers starten opnieuw op wanneer u de onderhoudsmodus afsluit.</span><span class="sxs-lookup"><span data-stu-id="56907-181">The controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="56907-182">Wanneer de updates van de schijffirmware met succes zijn toegepast en de onderhoudsmodus is afgesloten, gaat u weer naar de klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="56907-182">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="56907-183">Het is mogelijk dat in de portal gedurende 24 uur niet wordt weergegeven dat u de updates van de onderhoudsmodus hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="56907-183">Note that the portal might not show that you installed the maintenance mode updates for 24 hours.</span></span>


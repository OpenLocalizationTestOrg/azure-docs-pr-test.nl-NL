<!--author=alkohli last changed: 08/21/17-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="c4dff-101">toodownload hotfixes</span><span class="sxs-lookup"><span data-stu-id="c4dff-101">toodownload hotfixes</span></span>

<span data-ttu-id="c4dff-102">Volgende stappen toodownload Hallo software-update vanaf Microsoft Update-catalogus Hallo Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c4dff-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="c4dff-103">Start Internet Explorer en navigeer te[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c4dff-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="c4dff-104">Als dit de eerste keer dat u Microsoft Update-catalogus Hallo op deze computer is, klikt u op **installeren** wanneer na vragen aan gebruiker tooinstall Hallo-invoegtoepassing voor Microsoft Update-catalogus.</span><span class="sxs-lookup"><span data-stu-id="c4dff-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

    ![Catalogus installeren](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="c4dff-106">In het zoekvak Hallo Hallo Microsoft Update-catalogus, invoeren Hallo-Knowledge Base (KB) van de hotfix Hallo gewenste toodownload, bijvoorbeeld **4037264**, en klik vervolgens op **Search**.</span><span class="sxs-lookup"><span data-stu-id="c4dff-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **4037264**, and then click **Search**.</span></span>
   
    <span data-ttu-id="c4dff-107">Hallo hotfix wordt weergegeven, bijvoorbeeld **cumulatieve Software bundel Update 5.0 voor StorSimple 8000-serie**.</span><span class="sxs-lookup"><span data-stu-id="c4dff-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 5.0 for StorSimple 8000 Series**.</span></span>
   
    ![Catalogus doorzoeken](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. <span data-ttu-id="c4dff-109">Klik op **Downloaden**.</span><span class="sxs-lookup"><span data-stu-id="c4dff-109">Click **Download**.</span></span> <span data-ttu-id="c4dff-110">Opgeven of **Bladeren** tooa lokale locatie waar u Hallo tooappear downloadt.</span><span class="sxs-lookup"><span data-stu-id="c4dff-110">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="c4dff-111">Klik op Hallo bestanden toodownload toohello opgegeven locatie en de map.</span><span class="sxs-lookup"><span data-stu-id="c4dff-111">Click hello files toodownload toohello specified location and folder.</span></span> <span data-ttu-id="c4dff-112">Hallo-map kan ook worden gekopieerde tooa netwerkshare zijn die bereikbaar is vanaf het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="c4dff-112">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
5. <span data-ttu-id="c4dff-113">Zoeken naar aanvullende hotfixes die worden vermeld in de bovenstaande Hallo-tabel (**4037266**), en specifieke mappen toohello downloaden Hallo overeenkomt bestanden zoals vermeld in de voorgaande tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="c4dff-113">Search for any additional hotfixes listed in hello table above (**4037266**), and download hello corresponding files toohello specific folders as listed in hello preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="c4dff-114">Hallo hotfixes moet toegankelijk is vanaf beide domeincontrollers toodetect een potentiële fout van berichten van Hallo peer-controller.</span><span class="sxs-lookup"><span data-stu-id="c4dff-114">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
>
> <span data-ttu-id="c4dff-115">Hallo hotfixes moeten in 3 afzonderlijke mappen worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="c4dff-115">hello hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="c4dff-116">Bijvoorbeeld, Hallo apparaat Cis/software/MDS agentupdate kan worden gekopieerd _FirstOrderUpdate_ map alle Hallo andere ononderbroken updates kunnen worden gekopieerd in Hallo _SecondOrderUpdate_ map, en Onderhoud modus updates gekopieerd _ThirdOrderUpdate_ map.</span><span class="sxs-lookup"><span data-stu-id="c4dff-116">For example, hello device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all hello other non-disruptive updates could be copied in hello _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="c4dff-117">tooinstall en controleer of de normale modus hotfixes</span><span class="sxs-lookup"><span data-stu-id="c4dff-117">tooinstall and verify regular mode hotfixes</span></span>

<span data-ttu-id="c4dff-118">Hallo tooinstall stappen te volgen uitvoeren en controleer of de normale modus hotfixes.</span><span class="sxs-lookup"><span data-stu-id="c4dff-118">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="c4dff-119">Als u deze hebt geïnstalleerd met behulp van hello Azure-portal, gaat u verder te[installeren en testen van onderhoud modus hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="c4dff-119">If you already installed them using hello Azure portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="c4dff-120">tooinstall hello hotfixes toegang Hallo Windows PowerShell-interface op de seriële console van het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="c4dff-120">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="c4dff-121">Ga als volgt Hallo gedetailleerde instructies in [PuTTy gebruiken tooconnect toohello seriële console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="c4dff-121">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="c4dff-122">Bij de opdrachtprompt hello, drukt u op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c4dff-122">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="c4dff-123">Selecteer **optie 1** toolog op toohello apparaat met volledige toegang.</span><span class="sxs-lookup"><span data-stu-id="c4dff-123">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="c4dff-124">Het is raadzaam dat u Hallo hotfix op Hallo passieve domeincontroller eerst installeren.</span><span class="sxs-lookup"><span data-stu-id="c4dff-124">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="c4dff-125">tooinstall hello hotfix op Hallo-opdrachtprompt, typt:</span><span class="sxs-lookup"><span data-stu-id="c4dff-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="c4dff-126">Gebruik IP in plaats van DNS in sharepad in Hallo hierboven opdracht.</span><span class="sxs-lookup"><span data-stu-id="c4dff-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="c4dff-127">de parameter credential Hallo wordt alleen gebruikt als u toegang een geverifieerde share tot.</span><span class="sxs-lookup"><span data-stu-id="c4dff-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="c4dff-128">Het is raadzaam dat u Hallo referentie parameter tooaccess shares.</span><span class="sxs-lookup"><span data-stu-id="c4dff-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="c4dff-129">Zelfs shares die geopend te zijn 'iedereen' zijn meestal toounauthenticated gebruikers niet worden geopend.</span><span class="sxs-lookup"><span data-stu-id="c4dff-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
4. <span data-ttu-id="c4dff-130">Hallo wachtwoord wanneer u wordt gevraagd op te geven.</span><span class="sxs-lookup"><span data-stu-id="c4dff-130">Supply hello password when prompted.</span></span> <span data-ttu-id="c4dff-131">Een voorbeeld van uitvoer voor de installatie Hallo eerste volgorde updates worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c4dff-131">A sample output for installing hello first order updates is shown below.</span></span> <span data-ttu-id="c4dff-132">Hallo eerste volgorde bijwerken moet u toopoint toohello specifiek bestand.</span><span class="sxs-lookup"><span data-stu-id="c4dff-132">For hello first order update, you need toopoint toohello specific file.</span></span>

    >[!NOTE] 
    > <span data-ttu-id="c4dff-133">Installeer Hallo _HcsSoftwareUpdate.exe_ eerste.</span><span class="sxs-lookup"><span data-stu-id="c4dff-133">You should install hello _HcsSoftwareUpdate.exe_ first.</span></span> <span data-ttu-id="c4dff-134">Nadat deze installatie is voltooid, installeer _CisMdsAgentUpdate.exe_.</span><span class="sxs-lookup"><span data-stu-id="c4dff-134">After this install has completed, then install _CisMdsAgentUpdate.exe_.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. <span data-ttu-id="c4dff-135">Type **Y** wanneer na vragen aan gebruiker tooconfirm Hallo hotfix-installatie.</span><span class="sxs-lookup"><span data-stu-id="c4dff-135">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
6. <span data-ttu-id="c4dff-136">Hallo-update controleren met behulp van Hallo `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4dff-136">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="c4dff-137">Hallo update wordt eerst op Hallo passieve controller voltooid.</span><span class="sxs-lookup"><span data-stu-id="c4dff-137">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="c4dff-138">Zodra Hallo passieve domeincontroller wordt bijgewerkt, zal er een failover en Hallo update worden vervolgens toegepast op Hallo andere domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="c4dff-138">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="c4dff-139">Hallo-update is voltooid wanneer beide domeincontrollers Hallo zijn bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c4dff-139">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="c4dff-140">Hallo ziet volgende voorbeelduitvoer Hallo update uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c4dff-140">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="c4dff-141">Hallo `RunInprogress` is `True` wanneer Hallo update wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c4dff-141">hello `RunInprogress` is `True` when hello update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="c4dff-142">Hallo voorbeelduitvoer na geeft aan dat of Hallo-update is voltooid.</span><span class="sxs-lookup"><span data-stu-id="c4dff-142">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="c4dff-143">Hallo `RunInProgress` is `False` wanneer Hallo-update is voltooid.</span><span class="sxs-lookup"><span data-stu-id="c4dff-143">hello `RunInProgress` is `False` when hello update is complete.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="c4dff-144">In sommige gevallen kan Hallo cmdlet rapporten `False` wanneer hello wordt nog steeds bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c4dff-144">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="c4dff-145">tooensure die Hallo hotfix is voltooid, wacht een paar minuten, voer deze opdracht opnieuw uit en controleer of deze Hallo `RunInProgress` is `False`.</span><span class="sxs-lookup"><span data-stu-id="c4dff-145">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="c4dff-146">Hallo-hotfix is voltooid, als het.</span><span class="sxs-lookup"><span data-stu-id="c4dff-146">If it is, then hello hotfix has completed.</span></span>

7. <span data-ttu-id="c4dff-147">Nadat het Hallo software-update is voltooid, controleert u of softwareversies Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="c4dff-147">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="c4dff-148">Type:</span><span class="sxs-lookup"><span data-stu-id="c4dff-148">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="c4dff-149">U ziet de volgende versies Hallo:</span><span class="sxs-lookup"><span data-stu-id="c4dff-149">You should see hello following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    <span data-ttu-id="c4dff-150">Hallo-versienummer niet worden gewijzigd nadat Hallo update hebt toegepast, geeft aan dat hotfix Hallo tooapply is mislukt.</span><span class="sxs-lookup"><span data-stu-id="c4dff-150">If hello version number does not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="c4dff-151">Neem in dat geval contact op met [Microsoft Support](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) voor verdere hulp.</span><span class="sxs-lookup"><span data-stu-id="c4dff-151">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="c4dff-152">U moet opnieuw opstarten Hallo actieve controller via Hallo `Restart-HcsController` cmdlet alvorens toe te passen Hallo volgende update.</span><span class="sxs-lookup"><span data-stu-id="c4dff-152">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello next update.</span></span>
     
8. <span data-ttu-id="c4dff-153">Herhaal stap 3-6 tooinstall hello _CisMDSAgentupdate.exe_ agent gedownload tooyour _FirstOrderUpdate_ map.</span><span class="sxs-lookup"><span data-stu-id="c4dff-153">Repeat steps 3-6 tooinstall hello _CisMDSAgentupdate.exe_ agent downloaded tooyour _FirstOrderUpdate_ folder.</span></span>
8. <span data-ttu-id="c4dff-154">Herhaal stap 3-6 tooinstall Hallo tweede volgorde updates.</span><span class="sxs-lookup"><span data-stu-id="c4dff-154">Repeat steps 3-6 tooinstall hello second order updates.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="c4dff-155">Tweede volgorde updates, meerdere updates kunnen worden geïnstalleerd door het uitvoeren van alleen Hallo `Start-HcsHotfix cmdlet` en toohello map tweede volgorde updates aan te wijzen.</span><span class="sxs-lookup"><span data-stu-id="c4dff-155">For second order updates, multiple updates can be installed by just running hello `Start-HcsHotfix cmdlet` and pointing toohello folder where second order updates are located.</span></span> <span data-ttu-id="c4dff-156">Hallo-cmdlet wordt alle Hallo-updates die beschikbaar zijn in de map Hallo uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c4dff-156">hello cmdlet will execute all hello updates available in hello folder.</span></span> <span data-ttu-id="c4dff-157">Als een update is al geïnstalleerd, wordt de logica voor het bijwerken van Hallo detecteren die en die update niet van toepassing.</span><span class="sxs-lookup"><span data-stu-id="c4dff-157">If an update is already installed, hello update logic will detect that and not apply that update.</span></span>

    <span data-ttu-id="c4dff-158">Nadat alle Hallo-hotfixes zijn geïnstalleerd, gebruikt u Hallo `Get-HcsSystem` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4dff-158">After all hello hotfixes are installed, use hello `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="c4dff-159">Hallo-versies worden:</span><span class="sxs-lookup"><span data-stu-id="c4dff-159">hello versions should be:</span></span>
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="c4dff-160">tooinstall en onderhoud modus hotfixes controleren</span><span class="sxs-lookup"><span data-stu-id="c4dff-160">tooinstall and verify maintenance mode hotfixes</span></span>

<span data-ttu-id="c4dff-161">Gebruik KB4037263 tooinstall schijf firmware-updates.</span><span class="sxs-lookup"><span data-stu-id="c4dff-161">Use KB4037263 tooinstall disk firmware updates.</span></span> <span data-ttu-id="c4dff-162">Deze updates zijn verstoren en toocomplete ongeveer 30 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="c4dff-162">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="c4dff-163">U kunt tooinstall deze in een gepland onderhoud-venster door de verbindende toohello seriële console van apparaat.</span><span class="sxs-lookup"><span data-stu-id="c4dff-163">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

> [!NOTE] 
> <span data-ttu-id="c4dff-164">Als de firmware van de schijf al bijgewerkt is, hoeft u niet tooinstall deze updates.</span><span class="sxs-lookup"><span data-stu-id="c4dff-164">If your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="c4dff-165">Voer Hallo `Get-HcsUpdateAvailability` cmdlet uit Hallo apparaat seriële console toocheck als updates beschikbaar zijn en of Hallo-updates zijn verstoren (onderhoudsmodus) of ononderbroken (normale modus) updates.</span><span class="sxs-lookup"><span data-stu-id="c4dff-165">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="c4dff-166">tooinstall hello schijf firmware-updates, volgt u onderstaande Hallo-instructies.</span><span class="sxs-lookup"><span data-stu-id="c4dff-166">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="c4dff-167">Hallo-apparaat in hello onderhoudsmodus plaatsen.</span><span class="sxs-lookup"><span data-stu-id="c4dff-167">Place hello device in hello maintenance mode.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="c4dff-168">Gebruik geen Windows PowerShell op afstand verbinding te maken met tooa apparaat in de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="c4dff-168">Do not use Windows PowerShell remoting when connecting tooa device in maintenance mode.</span></span> <span data-ttu-id="c4dff-169">In plaats daarvan deze cmdlet uitvoeren op Hallo apparaat controller wanneer verbonden zijn via de seriële console van Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="c4dff-169">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span>

    <span data-ttu-id="c4dff-170">tooplace hello controller in de onderhoudsmodus bevindt, typt u:</span><span class="sxs-lookup"><span data-stu-id="c4dff-170">tooplace hello controller in maintenance mode, type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="c4dff-171">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c4dff-171">A sample output is shown below.</span></span>
   
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
   
    <span data-ttu-id="c4dff-172">Beide domeincontrollers Hallo start opnieuw op in de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="c4dff-172">Both hello controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="c4dff-173">tooinstall hello schijf firmware-update, type:</span><span class="sxs-lookup"><span data-stu-id="c4dff-173">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="c4dff-174">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c4dff-174">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="c4dff-175">Monitor Hallo installeren uitgevoerd met `Get-HcsUpdateStatus` opdracht.</span><span class="sxs-lookup"><span data-stu-id="c4dff-175">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="c4dff-176">Hallo update is voltooid wanneer hello `RunInProgress` wijzigingen te`False`.</span><span class="sxs-lookup"><span data-stu-id="c4dff-176">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="c4dff-177">Nadat het Hallo-installatie is voltooid, wordt een Hallo controller welke Hallo onderhoud modus hotfix is geïnstalleerd wordt opnieuw gestart.</span><span class="sxs-lookup"><span data-stu-id="c4dff-177">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="c4dff-178">Meld u aan als optie 1 met volledige toegang en controleer of firmwareversie Hallo-schijf.</span><span class="sxs-lookup"><span data-stu-id="c4dff-178">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="c4dff-179">Type:</span><span class="sxs-lookup"><span data-stu-id="c4dff-179">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="c4dff-180">Hallo verwacht schijf firmware-versies zijn:</span><span class="sxs-lookup"><span data-stu-id="c4dff-180">hello expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   <span data-ttu-id="c4dff-181">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c4dff-181">A sample output is shown below.</span></span>
   
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
   
    <span data-ttu-id="c4dff-182">Voer Hallo `Get-HcsFirmwareVersion` opdracht in het tweede controller tooverify hello, die de softwareversie Hallo is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c4dff-182">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="c4dff-183">Vervolgens kunt u de onderhoudsmodus Hallo afsluiten.</span><span class="sxs-lookup"><span data-stu-id="c4dff-183">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="c4dff-184">toodo dus, typt u na de opdracht voor elke domeincontroller apparaat Hallo:</span><span class="sxs-lookup"><span data-stu-id="c4dff-184">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="c4dff-185">Hallo-controllers opnieuw opstarten bij het afsluiten van de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="c4dff-185">hello controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="c4dff-186">Na het Hallo schijf firmware updates met succes zijn toegepast en Hallo apparaat onderhoudsmodus, return toohello Azure-portal is afgesloten.</span><span class="sxs-lookup"><span data-stu-id="c4dff-186">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure portal.</span></span> <span data-ttu-id="c4dff-187">Houd er rekening mee dat Hallo-portal niet altijd weergegeven dat u Hallo onderhoud modus updates geïnstalleerd voor 24 uur.</span><span class="sxs-lookup"><span data-stu-id="c4dff-187">Note that hello portal might not show that you installed hello maintenance mode updates for 24 hours.</span></span>


<!--author=alkohli last changed: 03/17/16-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="e1158-101">toodownload hotfixes</span><span class="sxs-lookup"><span data-stu-id="e1158-101">toodownload hotfixes</span></span>
<span data-ttu-id="e1158-102">Volgende stappen toodownload Hallo software-update vanaf Microsoft Update-catalogus Hallo Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e1158-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="e1158-103">Start Internet Explorer en navigeer te[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e1158-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="e1158-104">Als dit de eerste keer dat u Microsoft Update-catalogus Hallo op deze computer is, klikt u op **installeren** wanneer na vragen aan gebruiker tooinstall Hallo-invoegtoepassing voor Microsoft Update-catalogus.</span><span class="sxs-lookup"><span data-stu-id="e1158-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="e1158-105">![Installeren van de catalogus](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="e1158-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="e1158-106">In het zoekvak Hallo Hallo Microsoft Update-catalogus, invoeren Hallo-Knowledge Base (KB) van de hotfix Hallo gewenste toodownload, bijvoorbeeld **3121901**, en klik vervolgens op **Search**.</span><span class="sxs-lookup"><span data-stu-id="e1158-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3121901**, and then click **Search**.</span></span>
   
    <span data-ttu-id="e1158-107">Hallo hotfix wordt weergegeven, bijvoorbeeld **cumulatieve Software bundel Update 2.0 voor StorSimple 8000-serie**.</span><span class="sxs-lookup"><span data-stu-id="e1158-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 2.0 for StorSimple 8000 Series**.</span></span>
   
    ![Catalogus doorzoeken](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="e1158-109">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="e1158-109">Click **Add**.</span></span> <span data-ttu-id="e1158-110">Hallo-update is toohello mandje toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e1158-110">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="e1158-111">Zoeken naar aanvullende hotfixes die worden vermeld in de bovenstaande Hallo-tabel (**3121900**, **3080728**, **3090322**, en **3121899**), en elk toevoegen Hallo mandje.</span><span class="sxs-lookup"><span data-stu-id="e1158-111">Search for any additional hotfixes listed in hello table above (**3121900**, **3080728**, **3090322**, and **3121899**), and add each hello basket.</span></span>
6. <span data-ttu-id="e1158-112">Klik op **Mandje weergeven**.</span><span class="sxs-lookup"><span data-stu-id="e1158-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="e1158-113">Klik op **Downloaden**.</span><span class="sxs-lookup"><span data-stu-id="e1158-113">Click **Download**.</span></span> <span data-ttu-id="e1158-114">Opgeven of **Bladeren** tooa lokale locatie waar u Hallo tooappear downloadt.</span><span class="sxs-lookup"><span data-stu-id="e1158-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="e1158-115">Hallo-updates worden gedownload toohello opgegeven locatie en in een submap met dezelfde naam als de update Hallo Hallo geplaatst.</span><span class="sxs-lookup"><span data-stu-id="e1158-115">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="e1158-116">Hallo-map kan ook worden gekopieerde tooa netwerkshare zijn die bereikbaar is vanaf het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="e1158-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="e1158-117">Hallo hotfixes moet toegankelijk is vanaf beide domeincontrollers toodetect een potentiële fout van berichten van Hallo peer-controller.</span><span class="sxs-lookup"><span data-stu-id="e1158-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="e1158-118">tooinstall en controleer of de normale modus hotfixes</span><span class="sxs-lookup"><span data-stu-id="e1158-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="e1158-119">Hallo tooinstall stappen te volgen uitvoeren en controleer of de normale modus hotfixes.</span><span class="sxs-lookup"><span data-stu-id="e1158-119">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="e1158-120">Als u deze hebt geïnstalleerd met behulp van hello Azure-Portal, gaat u verder te[installeren en testen van onderhoud modus hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="e1158-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="e1158-121">tooinstall hello hotfixes toegang Hallo Windows PowerShell-interface op de seriële console van het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="e1158-121">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="e1158-122">Ga als volgt Hallo gedetailleerde instructies in [PuTTy gebruiken tooconnect toohello seriële console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="e1158-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="e1158-123">Bij de opdrachtprompt hello, drukt u op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="e1158-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="e1158-124">Selecteer **optie 1** toolog op toohello apparaat met volledige toegang.</span><span class="sxs-lookup"><span data-stu-id="e1158-124">Select **Option 1** toolog on toohello device with full access.</span></span>
3. <span data-ttu-id="e1158-125">tooinstall hello hotfix op Hallo-opdrachtprompt, typt:</span><span class="sxs-lookup"><span data-stu-id="e1158-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="e1158-126">Gebruik IP in plaats van DNS in sharepad in Hallo hierboven opdracht.</span><span class="sxs-lookup"><span data-stu-id="e1158-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="e1158-127">de parameter credential Hallo wordt alleen gebruikt als u toegang een geverifieerde share tot.</span><span class="sxs-lookup"><span data-stu-id="e1158-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="e1158-128">Het is raadzaam dat u Hallo referentie parameter tooaccess shares.</span><span class="sxs-lookup"><span data-stu-id="e1158-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="e1158-129">Zelfs shares die geopend te zijn 'iedereen' zijn meestal toounauthenticated gebruikers niet worden geopend.</span><span class="sxs-lookup"><span data-stu-id="e1158-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="e1158-130">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e1158-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```
4. <span data-ttu-id="e1158-131">Type **Y** wanneer na vragen aan gebruiker tooconfirm Hallo hotfix-installatie.</span><span class="sxs-lookup"><span data-stu-id="e1158-131">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
5. <span data-ttu-id="e1158-132">Hallo-update controleren met behulp van Hallo `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e1158-132">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="e1158-133">Hallo ziet volgende voorbeelduitvoer Hallo update uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e1158-133">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="e1158-134">Hallo `RunInprogress` worden `True` wanneer Hallo update wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e1158-134">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 12/21/2015 10:36:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="e1158-135">Hallo voorbeelduitvoer na geeft aan dat of Hallo-update is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e1158-135">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="e1158-136">Hallo `RunInProgress` worden `False` wanneer Hallo-update is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e1158-136">hello `RunInProgress` will be `False` when hello update has completed.</span></span>
   
    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 12/21/2015 10:59:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="e1158-137">In sommige gevallen kan Hallo cmdlet rapporten `False` wanneer hello wordt nog steeds bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e1158-137">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="e1158-138">tooensure die Hallo hotfix is voltooid, wacht een paar minuten, voer deze opdracht opnieuw uit en controleer of deze Hallo `RunInProgress` is `False`.</span><span class="sxs-lookup"><span data-stu-id="e1158-138">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="e1158-139">Hallo-hotfix is voltooid, als het.</span><span class="sxs-lookup"><span data-stu-id="e1158-139">If it is, then hello hotfix has completed.</span></span>

6. <span data-ttu-id="e1158-140">Na het Hallo-software is-update voltooid, herhaalt u stap 3-5 tooinstall en monitor Hallo SaaS agent en MDS-agent.</span><span class="sxs-lookup"><span data-stu-id="e1158-140">After hello software update is complete, repeat steps 3-5 tooinstall and monitor hello SaaS agent and MDS agent .</span></span> <span data-ttu-id="e1158-141">Zorg ervoor dat `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` is geïnstalleerd voordat het `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span><span class="sxs-lookup"><span data-stu-id="e1158-141">Ensure that `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` is installed before `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span></span>
7. <span data-ttu-id="e1158-142">Controleer of softwareversies Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="e1158-142">Verify hello system software versions.</span></span> <span data-ttu-id="e1158-143">Type:</span><span class="sxs-lookup"><span data-stu-id="e1158-143">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="e1158-144">U ziet de volgende versies Hallo:</span><span class="sxs-lookup"><span data-stu-id="e1158-144">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="e1158-145">HcsSoftwareVersion: 6.3.9600.17673</span><span class="sxs-lookup"><span data-stu-id="e1158-145">HcsSoftwareVersion: 6.3.9600.17673</span></span>
   * <span data-ttu-id="e1158-146">CisAgentVersion: 1.0.9150.0</span><span class="sxs-lookup"><span data-stu-id="e1158-146">CisAgentVersion: 1.0.9150.0</span></span>
   * <span data-ttu-id="e1158-147">MdsAgentVersion: 30.0.4698.13</span><span class="sxs-lookup"><span data-stu-id="e1158-147">MdsAgentVersion: 30.0.4698.13</span></span>
     
     <span data-ttu-id="e1158-148">Als Hallo versienummers niet wijzigen nadat Hallo update hebt toegepast, geeft u aan dat deze hotfix Hallo tooapply is mislukt.</span><span class="sxs-lookup"><span data-stu-id="e1158-148">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="e1158-149">Neem in dat geval contact op met [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) voor verdere hulp.</span><span class="sxs-lookup"><span data-stu-id="e1158-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
8. <span data-ttu-id="e1158-150">Herhaal stap 3-5 tooinstall Hallo resterende hotfixes reguliere-modus.</span><span class="sxs-lookup"><span data-stu-id="e1158-150">Repeat steps 3-5 tooinstall hello remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="e1158-151">Hallo LSI stuurprogramma - KB3121900</span><span class="sxs-lookup"><span data-stu-id="e1158-151">hello LSI driver - KB3121900</span></span>
   * <span data-ttu-id="e1158-152">Hallo Storport-update - KB3080728</span><span class="sxs-lookup"><span data-stu-id="e1158-152">hello Storport update - KB3080728</span></span>
   * <span data-ttu-id="e1158-153">Hallo Spaceport update - KB3090322</span><span class="sxs-lookup"><span data-stu-id="e1158-153">hello Spaceport update - KB3090322</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="e1158-154">tooinstall en onderhoud modus hotfixes controleren</span><span class="sxs-lookup"><span data-stu-id="e1158-154">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="e1158-155">Gebruik KB3121899 tooinstall schijf firmware-updates.</span><span class="sxs-lookup"><span data-stu-id="e1158-155">Use KB3121899 tooinstall disk firmware updates.</span></span> <span data-ttu-id="e1158-156">Deze updates zijn verstoren en toocomplete ongeveer 30 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="e1158-156">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="e1158-157">U kunt tooinstall deze in een gepland onderhoud-venster door de verbindende toohello seriële console van apparaat.</span><span class="sxs-lookup"><span data-stu-id="e1158-157">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="e1158-158">Houd er rekening mee dat als de firmware van de schijf al bijgewerkt is, u niet tooinstall deze updates hoeft.</span><span class="sxs-lookup"><span data-stu-id="e1158-158">Note that if your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="e1158-159">Voer Hallo `Get-HcsUpdateAvailability` cmdlet uit Hallo apparaat seriële console toocheck als updates beschikbaar zijn en of Hallo-updates zijn verstoren (onderhoudsmodus) of ononderbroken (normale modus) updates.</span><span class="sxs-lookup"><span data-stu-id="e1158-159">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="e1158-160">tooinstall hello schijf firmware-updates, volgt u onderstaande Hallo-instructies.</span><span class="sxs-lookup"><span data-stu-id="e1158-160">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="e1158-161">Hallo-apparaat in hello onderhoudsmodus plaatsen.</span><span class="sxs-lookup"><span data-stu-id="e1158-161">Place hello device in hello Maintenance mode.</span></span> <span data-ttu-id="e1158-162">Houd er rekening mee dat u Windows PowerShell op afstand niet gebruiken moet bij het verbinden van tooa apparaat in de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="e1158-162">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="e1158-163">In plaats daarvan deze cmdlet uitvoeren op Hallo apparaat controller wanneer verbonden zijn via de seriële console van Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="e1158-163">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="e1158-164">Type:</span><span class="sxs-lookup"><span data-stu-id="e1158-164">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="e1158-165">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e1158-165">A sample output is shown below.</span></span>
   
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
   
    <span data-ttu-id="e1158-166">Beide domeincontrollers Hallo start opnieuw op in de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="e1158-166">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="e1158-167">tooinstall hello schijf firmware-update, type:</span><span class="sxs-lookup"><span data-stu-id="e1158-167">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="e1158-168">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e1158-168">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="e1158-169">Monitor Hallo installeren uitgevoerd met `Get-HcsUpdateStatus` opdracht.</span><span class="sxs-lookup"><span data-stu-id="e1158-169">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="e1158-170">Hallo update is voltooid wanneer hello `RunInProgress` wijzigingen te`False`.</span><span class="sxs-lookup"><span data-stu-id="e1158-170">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="e1158-171">Nadat het Hallo-installatie is voltooid, wordt een Hallo controller welke Hallo onderhoud modus hotfix is geïnstalleerd wordt opnieuw gestart.</span><span class="sxs-lookup"><span data-stu-id="e1158-171">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="e1158-172">Meld u aan als optie 1 met volledige toegang en controleer of firmwareversie Hallo-schijf.</span><span class="sxs-lookup"><span data-stu-id="e1158-172">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="e1158-173">Type:</span><span class="sxs-lookup"><span data-stu-id="e1158-173">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="e1158-174">Hallo verwacht schijf firmware-versies zijn:</span><span class="sxs-lookup"><span data-stu-id="e1158-174">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="e1158-175">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e1158-175">A sample output is shown below.</span></span>
   
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
   
    <span data-ttu-id="e1158-176">Voer Hallo `Get-HcsFirmwareVersion` opdracht in het tweede controller tooverify hello, die de softwareversie Hallo is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e1158-176">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="e1158-177">Vervolgens kunt u de onderhoudsmodus Hallo afsluiten.</span><span class="sxs-lookup"><span data-stu-id="e1158-177">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="e1158-178">toodo dus, typt u na de opdracht voor elke domeincontroller apparaat Hallo:</span><span class="sxs-lookup"><span data-stu-id="e1158-178">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="e1158-179">Hallo-controllers opnieuw opstarten bij het afsluiten van de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="e1158-179">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="e1158-180">Na het Hallo schijf firmware updates met succes zijn toegepast en Hallo apparaat onderhoudsmodus, return toohello klassieke Azure-portal is afgesloten.</span><span class="sxs-lookup"><span data-stu-id="e1158-180">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="e1158-181">Houd er rekening mee dat Hallo-portal niet altijd weergegeven dat u Hallo onderhoud modus updates geïnstalleerd voor 24 uur.</span><span class="sxs-lookup"><span data-stu-id="e1158-181">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>


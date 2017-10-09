<!--author=SharS last changed: 02/22/16-->

### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="b4d3c-101">tooconfigure en registreer Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="b4d3c-101">tooconfigure and register hello device</span></span>
1. <span data-ttu-id="b4d3c-102">Toegang tot Hallo Windows PowerShell-interface op de seriële console van het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="b4d3c-103">Zie [PuTTY gebruiken tooconnect toohello de seriële console apparaat](#use-putty-to-connect-to-the-device-serial-console) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-103">See [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="b4d3c-104">**Ervoor toofollow Hallo procedure exact worden of u zich niet kunnen tooaccess Hallo-console.**</span><span class="sxs-lookup"><span data-stu-id="b4d3c-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>
2. <span data-ttu-id="b4d3c-105">Druk op Enter één keer tooget vanaf de opdrachtprompt in Hallo-sessie die wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-105">In hello session that opens up, press Enter one time tooget a command prompt.</span></span> 
3. <span data-ttu-id="b4d3c-106">U zult na vragen aan gebruiker toochoose Hallo taal dat u tooset voor uw apparaat dat wilt.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="b4d3c-107">Hallo taal op te geven en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-107">Specify hello language, and then press Enter.</span></span> 
   
    ![Apparaat 1 configureren en registreren met StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="b4d3c-109">Kies optie 1 toolog op met volledige toegang in Hallo seriële consolemenu wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-109">In hello serial console menu that is presented, choose option 1 toolog on with full access.</span></span> 
   
    ![Apparaat 2 registreren met StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="b4d3c-111">Volgende stappen tooconfigure Hallo minimale vereiste netwerkinstellingen voor uw apparaat Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-111">Perform hello following steps tooconfigure hello minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="b4d3c-112">Deze configuratiestappen moeten toobe uitgevoerd op de actieve controller Hallo Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-112">These configuration steps need toobe performed on hello active controller of hello device.</span></span> <span data-ttu-id="b4d3c-113">menu van de seriële console Hallo geeft Hallo controllerstatus in de banner het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-113">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="b4d3c-114">Als u geen verbinding maken met actieve controller toohello, verbreken en maak verbinding toohello actieve controller.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-114">If you are not connect toohello active controller, disconnect and then connect toohello active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="b4d3c-115">Typ uw wachtwoord bij de opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-115">At hello command prompt, type your password.</span></span> <span data-ttu-id="b4d3c-116">Hallo standaardapparaatwachtwoord is **Wachtwoord1**.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-116">hello default device password is **Password1**.</span></span>
   2. <span data-ttu-id="b4d3c-117">Type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b4d3c-117">Type hello following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="b4d3c-118">Een setup-wizard verschijnt toohelp u Hallo netwerkinstellingen voor Hallo apparaat configureren.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-118">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="b4d3c-119">Geef Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="b4d3c-119">Supply hello following information:</span></span> 
      
      * <span data-ttu-id="b4d3c-120">IP-adres voor DATA 0-netwerkinterface</span><span class="sxs-lookup"><span data-stu-id="b4d3c-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="b4d3c-121">Subnetmasker</span><span class="sxs-lookup"><span data-stu-id="b4d3c-121">Subnet mask</span></span>
      * <span data-ttu-id="b4d3c-122">Gateway</span><span class="sxs-lookup"><span data-stu-id="b4d3c-122">Gateway</span></span>
      * <span data-ttu-id="b4d3c-123">IP-adres voor de primaire DNS-server</span><span class="sxs-lookup"><span data-stu-id="b4d3c-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="b4d3c-124">IP-adres voor de primaire NTP-server</span><span class="sxs-lookup"><span data-stu-id="b4d3c-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="b4d3c-125">Mogelijk hebt u toowait voor een paar minuten voordat het Hallo-subnetmasker en DNS-instellingen toobe toegepast.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-125">You may have toowait for a few minutes for hello subnet mask and DNS settings toobe applied.</span></span> 
      > 
      > 
   4. <span data-ttu-id="b4d3c-126">Configureer desgewenst uw webproxyserver.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="b4d3c-127">Hoewel webproxyconfiguratie optioneel is, worden op de hoogte gebracht als u een webproxy gebruikt, u alleen deze hier configureren kunt.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="b4d3c-128">Voor meer informatie gaat te[webproxy voor uw apparaat configureren](../articles/storsimple/storsimple-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="b4d3c-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span> 
      > 
      > 
6. <span data-ttu-id="b4d3c-129">Druk op Ctrl + C tooexit Hallo-installatiewizard.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-129">Press Ctrl + C tooexit hello setup wizard.</span></span>
7. <span data-ttu-id="b4d3c-130">Hallo-updates als volgt installeren:</span><span class="sxs-lookup"><span data-stu-id="b4d3c-130">Install hello updates as follows:</span></span>
   
   1. <span data-ttu-id="b4d3c-131">Hallo cmdlet tooset IP-adressen op beide domeincontrollers Hallo volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b4d3c-131">Use hello following cmdlet tooset IPs on both hello controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="b4d3c-132">Bij de opdrachtprompt Hallo uitvoeren `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-132">At hello command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="b4d3c-133">U moet een melding dat er updates beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="b4d3c-134">Voer `Start-HcsUpdate` uit.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="b4d3c-135">U kunt deze opdracht uitvoeren op een willekeurig knooppunt.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-135">You can run this command on any node.</span></span> <span data-ttu-id="b4d3c-136">Updates worden toegepast op de eerste domeincontroller hello, Hallo controller failover en vervolgens Hallo updates worden toegepast op andere domeincontrollers Hallo.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-136">Updates will be applied on hello first controller, hello controller will fail over, and then hello updates will be applied on hello other controller.</span></span>
      
      <span data-ttu-id="b4d3c-137">U kunt voortgang Hallo Hallo update door te voeren `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-137">You can monitor hello progress of hello update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="b4d3c-138">Hallo ziet volgende voorbeelduitvoer Hallo update uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-138">hello following sample output shows hello update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   : 
      ````
      
      <span data-ttu-id="b4d3c-139">Hallo voorbeelduitvoer na geeft aan dat of Hallo-update is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-139">hello following sample output indicates that hello update is finished.</span></span>
      
      ````
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      
      ````
      
      <span data-ttu-id="b4d3c-140">Het kan too11 uren tooapply alle updates, inclusief Hallo Hallo Windows-Updates duren.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-140">It may take up too11 hours tooapply all hello updates, including hello Windows Updates.</span></span>

8. <span data-ttu-id="b4d3c-141">Nadat alle zijn hello updates met succes is geïnstalleerd, voert hello volgende cmdlet tooconfirm die Hallo van software-updates correct zijn toegepast:</span><span class="sxs-lookup"><span data-stu-id="b4d3c-141">After all hello updates are successfully installed, run hello following cmdlet tooconfirm that hello software updates were applied correctly:</span></span>
   
     `Get-HcsSystem`
   
    <span data-ttu-id="b4d3c-142">U ziet de volgende versies Hallo:</span><span class="sxs-lookup"><span data-stu-id="b4d3c-142">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="b4d3c-143">HcsSoftwareVersion: 6.3.9600.17491</span><span class="sxs-lookup"><span data-stu-id="b4d3c-143">HcsSoftwareVersion: 6.3.9600.17491</span></span>
   * <span data-ttu-id="b4d3c-144">CisAgentVersion: 1.0.9037.0</span><span class="sxs-lookup"><span data-stu-id="b4d3c-144">CisAgentVersion: 1.0.9037.0</span></span>
   * <span data-ttu-id="b4d3c-145">MdsAgentVersion: 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="b4d3c-145">MdsAgentVersion: 26.0.4696.1433</span></span>
9. <span data-ttu-id="b4d3c-146">Voer Hallo cmdlet tooconfirm die firmware-update Hallo na is correct toegepast:</span><span class="sxs-lookup"><span data-stu-id="b4d3c-146">Run hello following cmdlet tooconfirm that hello firmware update was applied correctly:</span></span>
   
    <span data-ttu-id="b4d3c-147">`Start-HcsFirmwareCheck`.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-147">`Start-HcsFirmwareCheck`.</span></span>
   
     <span data-ttu-id="b4d3c-148">moet de status van Hallo firmware **UpToDate**.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-148">hello firmware status should be **UpToDate**.</span></span>
10. <span data-ttu-id="b4d3c-149">Hallo cmdlet toopoint Hallo apparaat toohello Microsoft Azure Government portal volgen (omdat deze toohello openbare klassieke Azure-portal standaard verwijst) worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-149">Run hello following cmdlet toopoint hello device toohello Microsoft Azure Government portal (because it points toohello public Azure classic portal by default).</span></span> <span data-ttu-id="b4d3c-150">Dit wordt opnieuw opgestart beide domeincontrollers.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-150">This will restart both controllers.</span></span> <span data-ttu-id="b4d3c-151">Het is raadzaam dat u twee PuTTY sessies toosimultaneously verbinding tooboth domeincontrollers, zodat u kunt zien als elke domeincontroller opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-151">We recommend that you use two PuTTY sessions toosimultaneously connect tooboth controllers so that you can see when each controller is restarted.</span></span>
    
     `Set-CloudPlatform -AzureGovt_US`
    
    <span data-ttu-id="b4d3c-152">Hier ziet u een bevestigingsbericht.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-152">You will see a confirmation message.</span></span> <span data-ttu-id="b4d3c-153">Accepteer de standaardinstelling hello (**Y**).</span><span class="sxs-lookup"><span data-stu-id="b4d3c-153">Accept hello default (**Y**).</span></span>
11. <span data-ttu-id="b4d3c-154">Hallo na de installatie van cmdlet tooresume uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b4d3c-154">Run hello following cmdlet tooresume setup:</span></span>
    
     `Invoke-HcsSetupWizard`
    
     ![De wizard setup hervatten](./media/storsimple-configure-and-register-device-gov/HCS_ResumeSetup-gov-include.png)
    
    <span data-ttu-id="b4d3c-156">Wanneer u setup wilt activeren, zich Hallo wizard Hallo Update 1-versie (die overeenkomt met tooversion 17469).</span><span class="sxs-lookup"><span data-stu-id="b4d3c-156">When you resume setup, hello wizard will be hello Update 1 version (which corresponds tooversion 17469).</span></span> 
12. <span data-ttu-id="b4d3c-157">Hallo-netwerkinstellingen accepteren.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-157">Accept hello network settings.</span></span> <span data-ttu-id="b4d3c-158">U ziet een validatiebericht nadat u elke instelling hebt geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-158">You will see a validation message after you accept each setting.</span></span>
13. <span data-ttu-id="b4d3c-159">Uit veiligheidsoverwegingen wachtwoord apparaatbeheerder Hallo na Hallo eerste sessie verlopen en moet u toochange deze nu.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-159">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="b4d3c-160">Als daarom wordt gevraagd, geeft u een beheerderswachtwoord voor het apparaat op.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-160">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="b4d3c-161">Een geldig beheerderswachtwoord voor een apparaat moet 8 tot 15 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-161">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="b4d3c-162">Hallo wachtwoord moet bevatten drie van de volgende Hallo: kleine letters, hoofdletters, numerieke en speciale tekens.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-162">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![Apparaat 5 registreren met StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice5_gov-include.png)
14. <span data-ttu-id="b4d3c-164">laatste stap in de wizard setup Hallo Hallo registreert uw apparaat bij Hallo StorSimple Manager-service.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-164">hello final step in hello setup wizard registers your device with hello StorSimple Manager service.</span></span> <span data-ttu-id="b4d3c-165">Hiervoor u serviceregistratiesleutel die u hebt verkregen in moet Hallo [stap 2: Get Hallo serviceregistratiesleutel](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="b4d3c-165">For this, you will need hello service registration key that you obtained in [Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="b4d3c-166">Nadat u de registratiesleutel Hallo opgeeft, moet u wellicht toowait 2-3 minuten voordat het Hallo-apparaat is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-166">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b4d3c-167">U drukt op Ctrl + C op een tijd tooexit Hallo setup-wizard.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-167">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="b4d3c-168">Als u alle Hallo netwerkinstellingen (IP-adres voor Data 0, subnetmasker en Gateway) hebt ingevoerd, wordt uw vermeldingen behouden blijft.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-168">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![Voortgang van de StorSimple-registratie](./media/storsimple-configure-and-register-device-gov/HCS_RegistrationProgress-gov-include.png)
15. <span data-ttu-id="b4d3c-170">Nadat het Hallo-apparaat is geregistreerd, weergegeven een gegevensversleutelingssleutel van Service.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-170">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="b4d3c-171">Kopieer deze sleutel en bewaar deze op een veilige plaats.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-171">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="b4d3c-172">**Deze sleutel is vereist bij het Hallo-service registratie sleutel tooregister extra apparaten Hello StorSimple Manager-service.**</span><span class="sxs-lookup"><span data-stu-id="b4d3c-172">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Manager service.**</span></span> <span data-ttu-id="b4d3c-173">Raadpleeg te[StorSimple security](../articles/storsimple/storsimple-security.md) voor meer informatie over deze sleutel.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-173">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Apparaat 7 registreren met StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="b4d3c-175">toocopy hello tekst uit Hallo seriële console-venster, selecteert u de tekst hello.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-175">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="b4d3c-176">U moet kunnen toopaste in Hallo Klembord of een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-176">You should then be able toopaste it in hello clipboard or any text editor.</span></span> 
    > 
    > <span data-ttu-id="b4d3c-177">Gebruik geen Ctrl + C toocopy Hallo service gegevensversleutelingssleutel.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-177">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="b4d3c-178">Gebruik Ctrl + c drukken zorgt ervoor dat u tooexit Hallo installatiewizard.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-178">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="b4d3c-179">Als gevolg hiervan Hallo apparaat administrator-wachtwoord worden niet gewijzigd en Hallo apparaat toohello standaardwachtwoord wordt teruggezet.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-179">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    > 
    > 
16. <span data-ttu-id="b4d3c-180">Exit Hallo seriële console.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-180">Exit hello serial console.</span></span>
17. <span data-ttu-id="b4d3c-181">Toohello Azure Government Portal terug en Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b4d3c-181">Return toohello Azure Government Portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="b4d3c-182">Dubbelklik op uw StorSimple Manager service tooaccess hello **Quick Start** pagina.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-182">Double-click your StorSimple Manager service tooaccess hello **Quick Start** page.</span></span>
    2. <span data-ttu-id="b4d3c-183">Klik op **Verbonden apparaten weergeven**.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-183">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="b4d3c-184">Op Hallo **apparaten** pagina, controleert u of Hallo apparaat verbinding heeft met toohello service door het opzoeken van Hallo status.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-184">On hello **Devices** page, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="b4d3c-185">Hallo Apparaatstatus moet **Online**.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-185">hello device status should be **Online**.</span></span>
       
        ![Pagina StorSimple-apparaten](./media/storsimple-configure-and-register-device-gov/HCS_DeviceOnline-gov-include.png) 
       
        <span data-ttu-id="b4d3c-187">Als de apparaatstatus Hallo **Offline**, wacht een paar minuten voor Hallo apparaat toocome online.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-187">If hello device status is **Offline**, wait for a couple of minutes for hello device toocome online.</span></span> 
       
        <span data-ttu-id="b4d3c-188">Als Hallo apparaat na een paar minuten nog steeds offline is, moet u ervoor dat uw firewallnetwerk is geconfigureerd zoals beschreven in toomake [netwerkvereisten voor uw StorSimple-apparaat](../articles/storsimple/storsimple-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="b4d3c-188">If hello device is still offline after a few minutes, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span> 
       
        <span data-ttu-id="b4d3c-189">Controleer of poort 9354 open is voor uitgaande communicatie als deze door Hallo servicebus wordt gebruikt voor communicatie met de StorSimple Manager-service-naar-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4d3c-189">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Manager service-to-device communication.</span></span>


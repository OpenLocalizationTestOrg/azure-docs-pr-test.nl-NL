<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="e47ec-101">tooconfigure en registreer Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="e47ec-101">tooconfigure and register hello device</span></span>

1. <span data-ttu-id="e47ec-102">Toegang tot Hallo Windows PowerShell-interface op de seriële console van het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="e47ec-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="e47ec-103">Zie [PuTTY gebruiken tooconnect toohello de seriële console apparaat](#use-putty-to-connect-to-the-device-serial-console) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="e47ec-103">See [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="e47ec-104">**Ervoor toofollow Hallo procedure exact worden of u zich niet kunnen tooaccess Hallo-console.**</span><span class="sxs-lookup"><span data-stu-id="e47ec-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>

2. <span data-ttu-id="e47ec-105">Hallo-sessie die wordt geopend, klikt u op **Enter** één keer tooget vanaf de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="e47ec-105">In hello session that opens up, press **Enter** one time tooget a command prompt.</span></span>

3. <span data-ttu-id="e47ec-106">U zult na vragen aan gebruiker toochoose Hallo taal dat u tooset voor uw apparaat dat wilt.</span><span class="sxs-lookup"><span data-stu-id="e47ec-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="e47ec-107">Hallo taal op te geven en druk vervolgens op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="e47ec-107">Specify hello language, and then press **Enter**.</span></span>

4. <span data-ttu-id="e47ec-108">Hallo seriële console menu wordt weergegeven, kies optie 1 te**aanmelden met volledige toegang**.</span><span class="sxs-lookup"><span data-stu-id="e47ec-108">In hello serial console menu that is presented, choose option 1 too**log in with full access**.</span></span>
     <span data-ttu-id="e47ec-109">Voltooi de stappen 5-12 tooconfigure Hallo minimale vereiste netwerkinstellingen voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="e47ec-109">Complete steps 5-12 tooconfigure hello minimum required network settings for your device.</span></span> <span data-ttu-id="e47ec-110">**Deze configuratiestappen moeten toobe uitgevoerd op de actieve controller Hallo Hallo-apparaat.**</span><span class="sxs-lookup"><span data-stu-id="e47ec-110">**These configuration steps need toobe performed on hello active controller of hello device.**</span></span> <span data-ttu-id="e47ec-111">menu van de seriële console Hallo geeft Hallo controllerstatus in de banner het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="e47ec-111">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="e47ec-112">Als u niet verbonden bent wordt toohello actieve controller, verbreken en sluit vervolgens toohello actieve controller.</span><span class="sxs-lookup"><span data-stu-id="e47ec-112">If you are not connected toohello active controller, disconnect and then connect toohello active controller.</span></span>

5. <span data-ttu-id="e47ec-113">Typ uw wachtwoord bij de opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="e47ec-113">At hello command prompt, type your password.</span></span> <span data-ttu-id="e47ec-114">Hallo standaardapparaatwachtwoord is **Wachtwoord1**.</span><span class="sxs-lookup"><span data-stu-id="e47ec-114">hello default device password is **Password1**.</span></span>

6. <span data-ttu-id="e47ec-115">Type Hallo volgende opdracht: `Invoke-HcsSetupWizard`.</span><span class="sxs-lookup"><span data-stu-id="e47ec-115">Type hello following command: `Invoke-HcsSetupWizard`.</span></span>

7. <span data-ttu-id="e47ec-116">Een setup-wizard verschijnt toohelp u Hallo netwerkinstellingen voor Hallo apparaat configureren.</span><span class="sxs-lookup"><span data-stu-id="e47ec-116">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="e47ec-117">Geef Hallo Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="e47ec-117">Supply hello hello following information:</span></span>
   
   * <span data-ttu-id="e47ec-118">IP-adres voor Hallo DATA 0-netwerkinterface</span><span class="sxs-lookup"><span data-stu-id="e47ec-118">IP address for hello DATA 0 network interface</span></span>
   * <span data-ttu-id="e47ec-119">Subnetmasker</span><span class="sxs-lookup"><span data-stu-id="e47ec-119">Subnet mask</span></span>
   * <span data-ttu-id="e47ec-120">Gateway</span><span class="sxs-lookup"><span data-stu-id="e47ec-120">Gateway</span></span>
   * <span data-ttu-id="e47ec-121">IP-adres voor de primaire DNS-server</span><span class="sxs-lookup"><span data-stu-id="e47ec-121">IP address for Primary DNS server</span></span>

   <span data-ttu-id="e47ec-122">Een voorbeeld van de uitvoer wordt hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e47ec-122">A sample output is presented below.</span></span>

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Active
        ---------------------------------------------------------------

        Your device needs toobe registered with hello Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' tooset up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like tooconfigure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    <span data-ttu-id="e47ec-123">In Hallo voorgaande voorbeeld van uitvoer, ziet u dat Hallo gevalideerd netwerkinstellingen na elke stap in Hallo-proces.</span><span class="sxs-lookup"><span data-stu-id="e47ec-123">In hello preceding sample output, you can see that hello system is validating network settings after each step in hello process.</span></span>

     > [!NOTE]
     > <span data-ttu-id="e47ec-124">Mogelijk hebt u toowait voor een paar minuten voordat het Hallo-subnetmasker en Hallo DNS-instellingen toobe toegepast.</span><span class="sxs-lookup"><span data-stu-id="e47ec-124">You may have toowait for a few minutes for hello subnet mask and hello DNS settings toobe applied.</span></span> <span data-ttu-id="e47ec-125">Als u krijgt een foutbericht 'Selectievakje Hallo network connectivity tooData 0', controleert u Hallo fysieke netwerkverbinding voor Hallo DATA 0-netwerkinterface van uw actieve controller.</span><span class="sxs-lookup"><span data-stu-id="e47ec-125">If you get a "Check hello network connectivity tooData 0" error message, check hello physical network connection on hello DATA 0 network interface of your active controller.</span></span>

8. <span data-ttu-id="e47ec-126">Configureer desgewenst uw webproxyserver.</span><span class="sxs-lookup"><span data-stu-id="e47ec-126">(Optional) configure your web proxy server.</span></span> <span data-ttu-id="e47ec-127">De configuratie van uw webproxy is weliswaar optioneel, maar **houd er rekening mee dat als u een webproxy gebruikt, deze alleen hier kan worden geconfigureerd**.</span><span class="sxs-lookup"><span data-stu-id="e47ec-127">Although web proxy configuration is optional, **be aware that if you use a web proxy, you can only configure it here**.</span></span> <span data-ttu-id="e47ec-128">Voor meer informatie gaat te[webproxy voor uw apparaat configureren](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="e47ec-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span></span>
9. <span data-ttu-id="e47ec-129">Configureer een primaire NTP-server voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="e47ec-129">Configure a Primary NTP server for your device.</span></span> <span data-ttu-id="e47ec-130">NTP-servers zijn vereist, omdat uw apparaat de tijd moet synchroniseren voor verificatie met uw cloudserviceproviders.</span><span class="sxs-lookup"><span data-stu-id="e47ec-130">NTP servers are required, as your device must synchronize time so that it can authenticate with your cloud service providers.</span></span> <span data-ttu-id="e47ec-131">Zorg ervoor dat uw netwerk NTP-verkeer toopass van uw datacenter toohello Internet toestaat.</span><span class="sxs-lookup"><span data-stu-id="e47ec-131">Ensure that your network allows NTP traffic toopass from your datacenter toohello Internet.</span></span> <span data-ttu-id="e47ec-132">Als dit niet mogelijk is, geeft u een interne NTP-server op.</span><span class="sxs-lookup"><span data-stu-id="e47ec-132">If this is not possible, specify an internal NTP server.</span></span>

    <span data-ttu-id="e47ec-133">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e47ec-133">A sample output is shown below.</span></span>

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. <span data-ttu-id="e47ec-134">Uit veiligheidsoverwegingen wachtwoord apparaatbeheerder Hallo na Hallo eerste sessie verlopen en moet u toochange deze nu.</span><span class="sxs-lookup"><span data-stu-id="e47ec-134">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="e47ec-135">Als daarom wordt gevraagd, geeft u een beheerderswachtwoord voor het apparaat op.</span><span class="sxs-lookup"><span data-stu-id="e47ec-135">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="e47ec-136">Een geldig beheerderswachtwoord voor een apparaat moet 8 tot 15 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="e47ec-136">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="e47ec-137">Hallo wachtwoord moet bevatten drie van de volgende Hallo: kleine letters, hoofdletters, numerieke en speciale tekens.</span><span class="sxs-lookup"><span data-stu-id="e47ec-137">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. <span data-ttu-id="e47ec-138">laatste stap in de wizard setup Hallo Hallo registreert uw apparaat bij Hallo StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="e47ec-138">hello final step in hello setup wizard registers your device with hello StorSimple Device Manager service.</span></span> <span data-ttu-id="e47ec-139">Hiervoor moet u Hallo serviceregistratiesleutel die u hebt verkregen in stap 2.</span><span class="sxs-lookup"><span data-stu-id="e47ec-139">For this, you will need hello service registration key that you obtained in step 2.</span></span> <span data-ttu-id="e47ec-140">Nadat u de registratiesleutel Hallo opgeeft, moet u wellicht toowait 2-3 minuten voordat het Hallo-apparaat is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="e47ec-140">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="e47ec-141">U drukt op Ctrl + C op een tijd tooexit Hallo setup-wizard.</span><span class="sxs-lookup"><span data-stu-id="e47ec-141">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="e47ec-142">Als u alle Hallo netwerkinstellingen (IP-adres voor Data 0, subnetmasker en Gateway) hebt ingevoerd, wordt uw vermeldingen behouden blijft.</span><span class="sxs-lookup"><span data-stu-id="e47ec-142">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    
    <span data-ttu-id="e47ec-143">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e47ec-143">A sample output is shown below.</span></span>

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. <span data-ttu-id="e47ec-144">Nadat het Hallo-apparaat is geregistreerd, weergegeven een gegevensversleutelingssleutel van Service.</span><span class="sxs-lookup"><span data-stu-id="e47ec-144">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="e47ec-145">Kopieer deze sleutel en bewaar deze op een veilige plaats.</span><span class="sxs-lookup"><span data-stu-id="e47ec-145">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="e47ec-146">**Deze sleutel is vereist bij het Hallo-service registratie sleutel tooregister extra apparaten Hello StorSimple-apparaat Manager-service.**</span><span class="sxs-lookup"><span data-stu-id="e47ec-146">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Device Manager service.**</span></span> <span data-ttu-id="e47ec-147">Raadpleeg te[StorSimple security](../articles/storsimple/storsimple-security.md) voor meer informatie over deze sleutel.</span><span class="sxs-lookup"><span data-stu-id="e47ec-147">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Apparaat 7 registreren met StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > <span data-ttu-id="e47ec-149">toocopy hello tekst uit Hallo seriële console-venster, selecteert u de tekst hello.</span><span class="sxs-lookup"><span data-stu-id="e47ec-149">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="e47ec-150">U moet kunnen toopaste in Hallo Klembord of een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="e47ec-150">You should then be able toopaste it in hello clipboard or any text editor.</span></span> <span data-ttu-id="e47ec-151">Gebruik geen Ctrl + C toocopy Hallo service gegevensversleutelingssleutel.</span><span class="sxs-lookup"><span data-stu-id="e47ec-151">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="e47ec-152">Gebruik Ctrl + c drukken zorgt ervoor dat u tooexit Hallo installatiewizard.</span><span class="sxs-lookup"><span data-stu-id="e47ec-152">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="e47ec-153">Als gevolg hiervan Hallo apparaat administrator-wachtwoord worden niet gewijzigd en Hallo apparaat toohello standaardwachtwoord wordt teruggezet.</span><span class="sxs-lookup"><span data-stu-id="e47ec-153">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    
13. <span data-ttu-id="e47ec-154">Exit Hallo seriële console.</span><span class="sxs-lookup"><span data-stu-id="e47ec-154">Exit hello serial console.</span></span>
14. <span data-ttu-id="e47ec-155">Retourneren van toohello Azure-portal en Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e47ec-155">Return toohello Azure portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="e47ec-156">Ga tooyour Apparaatbeheer StorSimple-service.</span><span class="sxs-lookup"><span data-stu-id="e47ec-156">Go tooyour StorSimple Device Manager service.</span></span>
    2. <span data-ttu-id="e47ec-157">Klik op **Apparaten**.</span><span class="sxs-lookup"><span data-stu-id="e47ec-157">Click **Devices**.</span></span>
    3. <span data-ttu-id="e47ec-158">Controleer in Hallo in tabelvorm lijst van apparaten, of dat Hallo apparaat verbinding heeft met toohello service door het opzoeken van Hallo status.</span><span class="sxs-lookup"><span data-stu-id="e47ec-158">In hello tabular listing of devices, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="e47ec-159">Hallo Apparaatstatus moet **tooset gereed**.</span><span class="sxs-lookup"><span data-stu-id="e47ec-159">hello device status should be **Ready tooset up**.</span></span>
       
        ![Pagina StorSimple-apparaten](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        <span data-ttu-id="e47ec-161">Mogelijk moet u toowait voor een paar minuten voor Hallo apparaat status toochange te**tooset gereed**.</span><span class="sxs-lookup"><span data-stu-id="e47ec-161">You may need toowait for a couple of minutes for hello device status toochange too**Ready tooset up**.</span></span>
       
        <span data-ttu-id="e47ec-162">Als Hallo-apparaat niet in deze lijst weergegeven wordt, moet u ervoor dat uw firewallnetwerk is geconfigureerd zoals beschreven in toomake [netwerkvereisten voor uw StorSimple-apparaat](../articles/storsimple/storsimple-8000-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="e47ec-162">If hello device does not show up in this list, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span></span> <span data-ttu-id="e47ec-163">Controleer of poort 9354 open is voor uitgaande communicatie als dit wordt gebruikt door Hallo servicebus voor Apparaatbeheer van StorSimple-service-naar-apparaat communicatie.</span><span class="sxs-lookup"><span data-stu-id="e47ec-163">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Device Manager service-to-device communication.</span></span>


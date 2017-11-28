<!--author=alkohli last changed: 01/18/2017-->


#### <a name="to-configure-and-register-the-device"></a><span data-ttu-id="3348b-101">Het apparaat configureren en registreren</span><span class="sxs-lookup"><span data-stu-id="3348b-101">To configure and register the device</span></span>

1. <span data-ttu-id="3348b-102">Open de Windows PowerShell-interface op de seriële console van het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="3348b-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="3348b-103">Zie [PuTTY gebruiken om verbinding te maken met de seriële console van het apparaat](#use-putty-to-connect-to-the-device-serial-console) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="3348b-103">See [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="3348b-104">**Volg de procedure exact, omdat u anders geen toegang hebt tot de console.**</span><span class="sxs-lookup"><span data-stu-id="3348b-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span></span>

2. <span data-ttu-id="3348b-105">Druk in de geopende sessie eenmaal op **Enter** om een opdrachtprompt weer te geven.</span><span class="sxs-lookup"><span data-stu-id="3348b-105">In the session that opens up, press **Enter** one time to get a command prompt.</span></span>

3. <span data-ttu-id="3348b-106">U wordt gevraagd de taal te kiezen die u voor uw apparaat wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="3348b-106">You will be prompted to choose the language that you would like to set for your device.</span></span> <span data-ttu-id="3348b-107">Geef de taal op en druk op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3348b-107">Specify the language, and then press **Enter**.</span></span>

4. <span data-ttu-id="3348b-108">Kies in het weergegeven menu van de seriële console optie 1 om **u aan te melden met volledige toegang**.</span><span class="sxs-lookup"><span data-stu-id="3348b-108">In the serial console menu that is presented, choose option 1 to **log in with full access**.</span></span>
     <span data-ttu-id="3348b-109">Voer de stappen 5 tot en met 12 uit om de minimale vereiste netwerkinstellingen voor uw apparaat te configureren.</span><span class="sxs-lookup"><span data-stu-id="3348b-109">Complete steps 5-12 to configure the minimum required network settings for your device.</span></span> <span data-ttu-id="3348b-110">**Deze configuratiestappen moeten worden uitgevoerd op de actieve controller van het apparaat.**</span><span class="sxs-lookup"><span data-stu-id="3348b-110">**These configuration steps need to be performed on the active controller of the device.**</span></span> <span data-ttu-id="3348b-111">In het menu van de seriële console wordt de controllerstatus in het bannerbericht aangegeven.</span><span class="sxs-lookup"><span data-stu-id="3348b-111">The serial console menu indicates the controller state in the banner message.</span></span> <span data-ttu-id="3348b-112">Als u niet met de actieve controller verbonden bent, verbreekt u de verbinding en maakt u vervolgens verbinding met de actieve controller.</span><span class="sxs-lookup"><span data-stu-id="3348b-112">If you are not connected to the active controller, disconnect and then connect to the active controller.</span></span>

5. <span data-ttu-id="3348b-113">Typ uw wachtwoord bij de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="3348b-113">At the command prompt, type your password.</span></span> <span data-ttu-id="3348b-114">Het standaardapparaatwachtwoord is **Password1**.</span><span class="sxs-lookup"><span data-stu-id="3348b-114">The default device password is **Password1**.</span></span>

6. <span data-ttu-id="3348b-115">Typ de volgende opdracht: `Invoke-HcsSetupWizard`.</span><span class="sxs-lookup"><span data-stu-id="3348b-115">Type the following command: `Invoke-HcsSetupWizard`.</span></span>

7. <span data-ttu-id="3348b-116">Er wordt een instellingenwizard weergegeven om u te helpen bij het configureren van de netwerkinstellingen voor het apparaat.</span><span class="sxs-lookup"><span data-stu-id="3348b-116">A setup wizard will appear to help you configure the network settings for the device.</span></span> <span data-ttu-id="3348b-117">Geef de volgende informatie op:</span><span class="sxs-lookup"><span data-stu-id="3348b-117">Supply the the following information:</span></span>
   
   * <span data-ttu-id="3348b-118">IP-adres voor de DATA 0-netwerkinterface</span><span class="sxs-lookup"><span data-stu-id="3348b-118">IP address for the DATA 0 network interface</span></span>
   * <span data-ttu-id="3348b-119">Subnetmasker</span><span class="sxs-lookup"><span data-stu-id="3348b-119">Subnet mask</span></span>
   * <span data-ttu-id="3348b-120">Gateway</span><span class="sxs-lookup"><span data-stu-id="3348b-120">Gateway</span></span>
   * <span data-ttu-id="3348b-121">IP-adres voor de primaire DNS-server</span><span class="sxs-lookup"><span data-stu-id="3348b-121">IP address for Primary DNS server</span></span>

   <span data-ttu-id="3348b-122">Een voorbeeld van de uitvoer wordt hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3348b-122">A sample output is presented below.</span></span>

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Active
        ---------------------------------------------------------------

        Your device needs to be registered with the Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' to set up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like to configure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    <span data-ttu-id="3348b-123">In het voorgaande voorbeeld van de uitvoer kunt u zien dat de netwerkinstellingen na elke stap in het proces worden gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="3348b-123">In the preceding sample output, you can see that the system is validating network settings after each step in the process.</span></span>

     > [!NOTE]
     > <span data-ttu-id="3348b-124">U moet misschien een paar minuten wachten tot het subnetmasker en de DNS-instellingen zijn toegepast.</span><span class="sxs-lookup"><span data-stu-id="3348b-124">You may have to wait for a few minutes for the subnet mask and the DNS settings to be applied.</span></span> <span data-ttu-id="3348b-125">Als het foutbericht Controleer de netwerkverbinding met Data 0 wordt weergegeven, controleert u de fysieke netwerkverbinding voor de DATA 0-netwerkinterface van uw actieve controller.</span><span class="sxs-lookup"><span data-stu-id="3348b-125">If you get a "Check the network connectivity to Data 0" error message, check the physical network connection on the DATA 0 network interface of your active controller.</span></span>

8. <span data-ttu-id="3348b-126">Configureer desgewenst uw webproxyserver.</span><span class="sxs-lookup"><span data-stu-id="3348b-126">(Optional) configure your web proxy server.</span></span> <span data-ttu-id="3348b-127">De configuratie van uw webproxy is weliswaar optioneel, maar **houd er rekening mee dat als u een webproxy gebruikt, deze alleen hier kan worden geconfigureerd**.</span><span class="sxs-lookup"><span data-stu-id="3348b-127">Although web proxy configuration is optional, **be aware that if you use a web proxy, you can only configure it here**.</span></span> <span data-ttu-id="3348b-128">Zie [Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md) (Webproxy voor uw apparaat configureren) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3348b-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span></span>
9. <span data-ttu-id="3348b-129">Configureer een primaire NTP-server voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="3348b-129">Configure a Primary NTP server for your device.</span></span> <span data-ttu-id="3348b-130">NTP-servers zijn vereist, omdat uw apparaat de tijd moet synchroniseren voor verificatie met uw cloudserviceproviders.</span><span class="sxs-lookup"><span data-stu-id="3348b-130">NTP servers are required, as your device must synchronize time so that it can authenticate with your cloud service providers.</span></span> <span data-ttu-id="3348b-131">Zorg ervoor dat in uw netwerk NTP-verkeer kan worden doorgegeven van uw datacenter naar internet.</span><span class="sxs-lookup"><span data-stu-id="3348b-131">Ensure that your network allows NTP traffic to pass from your datacenter to the Internet.</span></span> <span data-ttu-id="3348b-132">Als dit niet mogelijk is, geeft u een interne NTP-server op.</span><span class="sxs-lookup"><span data-stu-id="3348b-132">If this is not possible, specify an internal NTP server.</span></span>

    <span data-ttu-id="3348b-133">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3348b-133">A sample output is shown below.</span></span>

    ```
        Would you like to configure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. <span data-ttu-id="3348b-134">Uit veiligheidsoverwegingen is het beheerderswachtwoord van het apparaat na de eerste sessie verlopen en moet u het nu wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3348b-134">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span></span> <span data-ttu-id="3348b-135">Als daarom wordt gevraagd, geeft u een beheerderswachtwoord voor het apparaat op.</span><span class="sxs-lookup"><span data-stu-id="3348b-135">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="3348b-136">Een geldig beheerderswachtwoord voor een apparaat moet 8 tot 15 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="3348b-136">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="3348b-137">Het wachtwoord moet drie van de volgende elementen bevatten: kleine letters, hoofdletters, cijfers en speciale tekens.</span><span class="sxs-lookup"><span data-stu-id="3348b-137">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span></span>

    ```
        The device administrator password must be between 8 and 15 characters. The password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. <span data-ttu-id="3348b-138">Bij de laatste stap in de instellingenwizard wordt uw apparaat geregistreerd met de StorSimple-apparaatbeheerfunctie.</span><span class="sxs-lookup"><span data-stu-id="3348b-138">The final step in the setup wizard registers your device with the StorSimple Device Manager service.</span></span> <span data-ttu-id="3348b-139">Hiervoor hebt u de serviceregistratiesleutel nodig die u in stap 2 hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="3348b-139">For this, you will need the service registration key that you obtained in step 2.</span></span> <span data-ttu-id="3348b-140">Nadat u de registratiesleutel hebt opgegeven, moet u mogelijk twee tot drie minuten wachten voordat het apparaat is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="3348b-140">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="3348b-141">U kunt op elk gewenst moment op Ctrl+C drukken om de instellingenwizard af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="3348b-141">You can press Ctrl + C at any time to exit the setup wizard.</span></span> <span data-ttu-id="3348b-142">Als u alle netwerkinstellingen (IP-adres voor Data 0, subnetmasker en gateway) hebt ingevoerd, blijven uw gegevens behouden.</span><span class="sxs-lookup"><span data-stu-id="3348b-142">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    
    <span data-ttu-id="3348b-143">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3348b-143">A sample output is shown below.</span></span>

    ```
        The service registration key is available in the StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. <span data-ttu-id="3348b-144">Nadat het apparaat is geregistreerd, wordt er een gegevensversleutelingssleutel van de service weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3348b-144">After the device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="3348b-145">Kopieer deze sleutel en bewaar deze op een veilige plaats.</span><span class="sxs-lookup"><span data-stu-id="3348b-145">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="3348b-146">**Deze sleutel is vereist bij de serviceregistratiesleutel om extra apparaten te registreren met de StorSimple Manager-apparaatbeheerfunctie.**</span><span class="sxs-lookup"><span data-stu-id="3348b-146">**This key will be required with the service registration key to register additional devices with the StorSimple Device Manager service.**</span></span> <span data-ttu-id="3348b-147">Zie [StorSimple security](../articles/storsimple/storsimple-security.md) (StorSimple-beveiliging) voor meer informatie over deze sleutel.</span><span class="sxs-lookup"><span data-stu-id="3348b-147">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Apparaat 7 registreren met StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > <span data-ttu-id="3348b-149">Kopieer de tekst uit het venster van de seriële console gewoon door de tekst te selecteren.</span><span class="sxs-lookup"><span data-stu-id="3348b-149">To copy the text from the serial console window, simply select the text.</span></span> <span data-ttu-id="3348b-150">U kunt de tekst vervolgens op het klembord of in een teksteditor plakken.</span><span class="sxs-lookup"><span data-stu-id="3348b-150">You should then be able to paste it in the clipboard or any text editor.</span></span> <span data-ttu-id="3348b-151">Kopieer de gegevensversleutelingssleutel van de service NIET met Ctrl+C.</span><span class="sxs-lookup"><span data-stu-id="3348b-151">DO NOT use Ctrl + C to copy the service data encryption key.</span></span> <span data-ttu-id="3348b-152">Als u op Ctrl+C drukt, wordt de instellingenwizard afgesloten.</span><span class="sxs-lookup"><span data-stu-id="3348b-152">Using Ctrl + C will cause you to exit the setup wizard.</span></span> <span data-ttu-id="3348b-153">Als gevolg hiervan wordt het beheerderswachtwoord van het apparaat niet gewijzigd en wordt het standaardwachtwoord opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3348b-153">As a result, the device administrator password will not be changed and the device will revert to the default password.</span></span>
    
13. <span data-ttu-id="3348b-154">Sluit de seriële console af.</span><span class="sxs-lookup"><span data-stu-id="3348b-154">Exit the serial console.</span></span>
14. <span data-ttu-id="3348b-155">Ga terug naar de Azure Portal en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3348b-155">Return to the Azure portal, and complete the following steps:</span></span>
    
    1. <span data-ttu-id="3348b-156">Ga naar uw StorSimple-apparaatbeheerservice.</span><span class="sxs-lookup"><span data-stu-id="3348b-156">Go to your StorSimple Device Manager service.</span></span>
    2. <span data-ttu-id="3348b-157">Klik op **Apparaten**.</span><span class="sxs-lookup"><span data-stu-id="3348b-157">Click **Devices**.</span></span>
    3. <span data-ttu-id="3348b-158">Controleer in de lijst in tabelvorm met apparaten aan de hand van de status of het apparaat verbinding heeft met de service.</span><span class="sxs-lookup"><span data-stu-id="3348b-158">In the tabular listing of devices, verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="3348b-159">Het apparaat moet de status **Gereed voor configuratie** hebben.</span><span class="sxs-lookup"><span data-stu-id="3348b-159">The device status should be **Ready to set up**.</span></span>
       
        ![Pagina StorSimple-apparaten](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        <span data-ttu-id="3348b-161">U moet mogelijk enkele minuten wachten totdat de apparaatstatus is gewijzigd in **Gereed voor configuratie**.</span><span class="sxs-lookup"><span data-stu-id="3348b-161">You may need to wait for a couple of minutes for the device status to change to **Ready to set up**.</span></span>
       
        <span data-ttu-id="3348b-162">Als het apparaat niet in deze lijst wordt weergegeven, moet u ervoor zorgen dat uw firewallnetwerk is geconfigureerd zoals wordt beschreven in [Netwerkvereisten voor uw StorSimple-apparaat](../articles/storsimple/storsimple-8000-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="3348b-162">If the device does not show up in this list, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span></span> <span data-ttu-id="3348b-163">Controleer of poort 9354 open is voor uitgaande communicatie, omdat de servicebus deze poort gebruikt voor de communicatie van de StorSimple-apparaatbeheerfunctie naar het apparaat.</span><span class="sxs-lookup"><span data-stu-id="3348b-163">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Device Manager service-to-device communication.</span></span>


<!--author=SharS last changed: 02/22/2016-->

### <a name="to-configure-and-register-the-device"></a><span data-ttu-id="4c0a9-101">Het apparaat configureren en registreren</span><span class="sxs-lookup"><span data-stu-id="4c0a9-101">To configure and register the device</span></span>
1. <span data-ttu-id="4c0a9-102">Open de Windows PowerShell-interface op de seriële console van het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="4c0a9-103">Zie [PuTTY gebruiken om verbinding te maken met de seriële console van het apparaat](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-103">See [Use PuTTY to connect to the device serial console](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="4c0a9-104">**Volg de procedure exact, omdat u anders geen toegang hebt tot de console.**</span><span class="sxs-lookup"><span data-stu-id="4c0a9-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span></span>
2. <span data-ttu-id="4c0a9-105">Druk in de geopende sessie eenmaal op Enter om een opdrachtprompt weer te geven.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-105">In the session that opens up, press Enter one time to get a command prompt.</span></span>
3. <span data-ttu-id="4c0a9-106">U wordt gevraagd de taal te kiezen die u voor uw apparaat wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-106">You will be prompted to choose the language that you would like to set for your device.</span></span> <span data-ttu-id="4c0a9-107">Geef de taal op en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-107">Specify the language, and then press Enter.</span></span>
   
    ![Apparaat 1 configureren en registreren met StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="4c0a9-109">Kies in het weergegeven menu van de seriële console optie 1 om u aan te melden met volledige toegang.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-109">In the serial console menu that is presented, choose option 1 to log on with full access.</span></span>
   
    ![Apparaat 2 registreren met StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="4c0a9-111">Voer de volgende stappen uit voor het configureren van de minimale vereiste netwerkinstellingen voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-111">Perform the following steps to configure the minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="4c0a9-112">Deze configuratiestappen moeten worden uitgevoerd op de actieve controller van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-112">These configuration steps need to be performed on the active controller of the device.</span></span> <span data-ttu-id="4c0a9-113">In het menu van de seriële console wordt de controllerstatus in het bannerbericht aangegeven.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-113">The serial console menu indicates the controller state in the banner message.</span></span> <span data-ttu-id="4c0a9-114">Als u geen verbinding maken met de actieve controller, verbreken en maak verbinding met de actieve controller.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-114">If you are not connect to the active controller, disconnect and then connect to the active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="4c0a9-115">Typ uw wachtwoord bij de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-115">At the command prompt, type your password.</span></span> <span data-ttu-id="4c0a9-116">Het standaardapparaatwachtwoord is **Password1**.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-116">The default device password is **Password1**.</span></span>
   2. <span data-ttu-id="4c0a9-117">Typ de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="4c0a9-117">Type the following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="4c0a9-118">Er wordt een instellingenwizard weergegeven om u te helpen bij het configureren van de netwerkinstellingen voor het apparaat.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-118">A setup wizard will appear to help you configure the network settings for the device.</span></span> <span data-ttu-id="4c0a9-119">Geef de volgende gegevens:</span><span class="sxs-lookup"><span data-stu-id="4c0a9-119">Supply the following information:</span></span>
      
      * <span data-ttu-id="4c0a9-120">IP-adres voor DATA 0-netwerkinterface</span><span class="sxs-lookup"><span data-stu-id="4c0a9-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="4c0a9-121">Subnetmasker</span><span class="sxs-lookup"><span data-stu-id="4c0a9-121">Subnet mask</span></span>
      * <span data-ttu-id="4c0a9-122">Gateway</span><span class="sxs-lookup"><span data-stu-id="4c0a9-122">Gateway</span></span>
      * <span data-ttu-id="4c0a9-123">IP-adres voor de primaire DNS-server</span><span class="sxs-lookup"><span data-stu-id="4c0a9-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="4c0a9-124">IP-adres voor de primaire NTP-server</span><span class="sxs-lookup"><span data-stu-id="4c0a9-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="4c0a9-125">U moet wachten op een paar minuten voor het subnetmasker en DNS-instellingen worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-125">You may have to wait for a few minutes for the subnet mask and DNS settings to be applied.</span></span>
      > 
      > 
   4. <span data-ttu-id="4c0a9-126">Configureer desgewenst uw webproxyserver.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="4c0a9-127">Hoewel webproxyconfiguratie optioneel is, worden op de hoogte gebracht als u een webproxy gebruikt, u alleen deze hier configureren kunt.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="4c0a9-128">Zie [Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md) (Webproxy voor uw apparaat configureren) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span>
      > 
      > 
6. <span data-ttu-id="4c0a9-129">Druk op Ctrl + C om de wizard setup af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-129">Press Ctrl + C to exit the setup wizard.</span></span>
7. <span data-ttu-id="4c0a9-130">Als volgt te werk om de updates te installeren:</span><span class="sxs-lookup"><span data-stu-id="4c0a9-130">Install the updates as follows:</span></span>
   
   1. <span data-ttu-id="4c0a9-131">Gebruik de volgende cmdlet IP-adressen op beide domeincontrollers instellen:</span><span class="sxs-lookup"><span data-stu-id="4c0a9-131">Use the following cmdlet to set IPs on both the controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="4c0a9-132">Voer bij de opdrachtprompt `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-132">At the command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="4c0a9-133">U moet een melding dat er updates beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="4c0a9-134">Voer `Start-HcsUpdate` uit.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="4c0a9-135">U kunt deze opdracht uitvoeren op een willekeurig knooppunt.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-135">You can run this command on any node.</span></span> <span data-ttu-id="4c0a9-136">Updates worden toegepast op de eerste domeincontroller, de controller failover en vervolgens de updates worden toegepast op de andere controller.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-136">Updates will be applied on the first controller, the controller will fail over, and then the updates will be applied on the other controller.</span></span>
      
      <span data-ttu-id="4c0a9-137">U kunt de voortgang van de update door te voeren `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-137">You can monitor the progress of the update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="4c0a9-138">Hieronder ziet u een voorbeeld van uitvoer terwijl de update nog bezig is.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-138">The following sample output shows the update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      <span data-ttu-id="4c0a9-139">In de volgende voorbeelduitvoer wordt aangegeven dat de update is voltooid.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-139">The following sample output indicates that the update is finished.</span></span>
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      <span data-ttu-id="4c0a9-140">Het kan tot 11 uur duren om alle updates, met inbegrip van de Windows-Updates toepassen.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-140">It may take up to 11 hours to apply all the updates, including the Windows Updates.</span></span>
8. <span data-ttu-id="4c0a9-141">Voer de volgende cmdlet als het apparaat naar de portal voor Microsoft Azure Government (omdat deze naar de openbare klassieke Azure portal standaard verwijst).</span><span class="sxs-lookup"><span data-stu-id="4c0a9-141">Run the following cmdlet to point the device to the Microsoft Azure Government portal (because it points to the public Azure classic portal by default).</span></span> <span data-ttu-id="4c0a9-142">Dit wordt opnieuw opgestart beide domeincontrollers.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-142">This will restart both controllers.</span></span> <span data-ttu-id="4c0a9-143">Het is raadzaam dat u twee PuTTY sessies tegelijk verbinding maken met beide domeincontrollers zodat u kunt zien als elke domeincontroller opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-143">We recommend that you use two PuTTY sessions to simultaneously connect to both controllers so that you can see when each controller is restarted.</span></span>
   
    `Set-CloudPlatform -AzureGovt_US`
   
   <span data-ttu-id="4c0a9-144">Hier ziet u een bevestigingsbericht.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-144">You will see a confirmation message.</span></span> <span data-ttu-id="4c0a9-145">Accepteer de standaardinstelling (**Y**).</span><span class="sxs-lookup"><span data-stu-id="4c0a9-145">Accept the default (**Y**).</span></span>
9. <span data-ttu-id="4c0a9-146">Voer de volgende cmdlet als u wilt doorgaan met setup:</span><span class="sxs-lookup"><span data-stu-id="4c0a9-146">Run the following cmdlet to resume setup:</span></span>
   
    `Invoke-HcsSetupWizard`
   
    ![De wizard setup hervatten](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   <span data-ttu-id="4c0a9-148">Als u setup wilt activeren, de wizard worden de versie van de Update 2.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-148">When you resume setup, the wizard will be the Update 2 version.</span></span>
10. <span data-ttu-id="4c0a9-149">De netwerkinstellingen accepteren.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-149">Accept the network settings.</span></span> <span data-ttu-id="4c0a9-150">U ziet een validatiebericht nadat u elke instelling hebt geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-150">You will see a validation message after you accept each setting.</span></span>
11. <span data-ttu-id="4c0a9-151">Uit veiligheidsoverwegingen is het beheerderswachtwoord van het apparaat na de eerste sessie verlopen en moet u het nu wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-151">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span></span> <span data-ttu-id="4c0a9-152">Als daarom wordt gevraagd, geeft u een beheerderswachtwoord voor het apparaat op.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-152">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="4c0a9-153">Een geldig beheerderswachtwoord voor een apparaat moet 8 tot 15 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-153">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="4c0a9-154">Het wachtwoord moet drie van de volgende elementen bevatten: kleine letters, hoofdletters, cijfers en speciale tekens.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-154">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![Apparaat 5 registreren met StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. <span data-ttu-id="4c0a9-156">Bij de laatste stap in de instellingenwizard wordt uw apparaat geregistreerd met de StorSimple Manager-service.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-156">The final step in the setup wizard registers your device with the StorSimple Manager service.</span></span> <span data-ttu-id="4c0a9-157">Hiervoor moet u de serviceregistratiesleutel die u hebt verkregen in [stap 2: de serviceregistratiesleutel ophalen](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="4c0a9-157">For this, you will need the service registration key that you obtained in [Step 2: Get the service registration key](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="4c0a9-158">Nadat u de registratiesleutel hebt opgegeven, moet u mogelijk twee tot drie minuten wachten voordat het apparaat is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-158">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4c0a9-159">U kunt op elk gewenst moment op Ctrl+C drukken om de instellingenwizard af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-159">You can press Ctrl + C at any time to exit the setup wizard.</span></span> <span data-ttu-id="4c0a9-160">Als u alle netwerkinstellingen (IP-adres voor Data 0, subnetmasker en gateway) hebt ingevoerd, blijven uw gegevens behouden.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-160">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![Voortgang van de StorSimple-registratie](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. <span data-ttu-id="4c0a9-162">Nadat het apparaat is geregistreerd, wordt er een gegevensversleutelingssleutel van de service weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-162">After the device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="4c0a9-163">Kopieer deze sleutel en bewaar deze op een veilige plaats.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-163">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="4c0a9-164">**Deze sleutel is vereist bij de serviceregistratiesleutel om extra apparaten te registreren met de StorSimple Manager-service.**</span><span class="sxs-lookup"><span data-stu-id="4c0a9-164">**This key will be required with the service registration key to register additional devices with the StorSimple Manager service.**</span></span> <span data-ttu-id="4c0a9-165">Zie [StorSimple security](../articles/storsimple/storsimple-security.md) (StorSimple-beveiliging) voor meer informatie over deze sleutel.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-165">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Apparaat 7 registreren met StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="4c0a9-167">Kopieer de tekst uit het venster van de seriële console gewoon door de tekst te selecteren.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-167">To copy the text from the serial console window, simply select the text.</span></span> <span data-ttu-id="4c0a9-168">U kunt de tekst vervolgens op het klembord of in een teksteditor plakken.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-168">You should then be able to paste it in the clipboard or any text editor.</span></span>
    > 
    > <span data-ttu-id="4c0a9-169">Kopieer de gegevensversleutelingssleutel van de service NIET met Ctrl+C.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-169">DO NOT use Ctrl + C to copy the service data encryption key.</span></span> <span data-ttu-id="4c0a9-170">Als u op Ctrl+C drukt, wordt de instellingenwizard afgesloten.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-170">Using Ctrl + C will cause you to exit the setup wizard.</span></span> <span data-ttu-id="4c0a9-171">Als gevolg hiervan wordt het beheerderswachtwoord van het apparaat niet gewijzigd en wordt het standaardwachtwoord opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-171">As a result, the device administrator password will not be changed and the device will revert to the default password.</span></span>
    > 
    > 
14. <span data-ttu-id="4c0a9-172">Sluit de seriële console af.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-172">Exit the serial console.</span></span>
15. <span data-ttu-id="4c0a9-173">Terug naar de overheid van de Azure Portal en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="4c0a9-173">Return to the Azure Government Portal, and complete the following steps:</span></span>
    
    1. <span data-ttu-id="4c0a9-174">Dubbelklik op de StorSimple Manager-service om de pagina **Quick Start** te openen.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-174">Double-click your StorSimple Manager service to access the **Quick Start** page.</span></span>
    2. <span data-ttu-id="4c0a9-175">Klik op **Verbonden apparaten weergeven**.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-175">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="4c0a9-176">Controleer op de pagina **Apparaten** aan de hand van de status of het apparaat verbinding heeft met de service.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-176">On the **Devices** page, verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="4c0a9-177">Het apparaat moet de status **Online** hebben.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-177">The device status should be **Online**.</span></span>
       
        ![Pagina StorSimple-apparaten](./media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        <span data-ttu-id="4c0a9-179">Als de status van het apparaat **Offline** is, moet u een paar minuten wachten totdat het apparaat online is.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-179">If the device status is **Offline**, wait for a couple of minutes for the device to come online.</span></span>
       
        <span data-ttu-id="4c0a9-180">Als het apparaat na een paar minuten nog steeds offline is, moet u ervoor zorgen dat uw firewallnetwerk is geconfigureerd zoals wordt beschreven in [Netwerkvereisten voor uw StorSimple-apparaat](../articles/storsimple/storsimple-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="4c0a9-180">If the device is still offline after a few minutes, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span>
       
        <span data-ttu-id="4c0a9-181">Controleer of poort 9354 open is voor uitgaande communicatie, omdat de servicebus deze poort gebruikt voor de communicatie van de StorSimple Manager-service naar het apparaat.</span><span class="sxs-lookup"><span data-stu-id="4c0a9-181">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Manager Service-to-device communication.</span></span>


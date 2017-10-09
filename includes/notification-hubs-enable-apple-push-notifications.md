

## <a name="generate-hello-certificate-signing-request-file"></a><span data-ttu-id="66bec-101">Aanvraag voor Certificaatondertekening Hallo-bestand genereren</span><span class="sxs-lookup"><span data-stu-id="66bec-101">Generate hello Certificate Signing Request file</span></span>
<span data-ttu-id="66bec-102">Hallo Apple Push Notification Service (APNS) gebruikt certificaten tooauthenticate uw pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="66bec-102">hello Apple Push Notification Service (APNS) uses certificates tooauthenticate your push notifications.</span></span> <span data-ttu-id="66bec-103">Volg deze instructies toocreate Hallo nodig push-certificaat toosend en meldingen ontvangen.</span><span class="sxs-lookup"><span data-stu-id="66bec-103">Follow these instructions toocreate hello necessary push certificate toosend and receive notifications.</span></span> <span data-ttu-id="66bec-104">Zie voor meer informatie over deze begrippen Hallo officiële [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentatie.</span><span class="sxs-lookup"><span data-stu-id="66bec-104">For more information on these concepts see hello official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="66bec-105">Hallo Certificate Signing Request (CSR)-bestand genereren die worden gebruikt door Apple toogenerate een ondertekend pushcertificaat.</span><span class="sxs-lookup"><span data-stu-id="66bec-105">Generate hello Certificate Signing Request (CSR) file, which is used by Apple toogenerate a signed push certificate.</span></span>

1. <span data-ttu-id="66bec-106">Voer op uw Mac Hallo hulpprogramma Sleutelhangertoegang uit.</span><span class="sxs-lookup"><span data-stu-id="66bec-106">On your Mac, run hello Keychain Access tool.</span></span> <span data-ttu-id="66bec-107">Het kan worden geopend vanuit Hallo **hulpprogramma's** map of Hallo **andere** map op Hallo launchpad.</span><span class="sxs-lookup"><span data-stu-id="66bec-107">It can be opened from hello **Utilities** folder or hello **Other** folder on hello launch pad.</span></span>
2. <span data-ttu-id="66bec-108">Klik op **Toegang tot sleutelhanger**, vouw **Certificaatassistent** uit, klik vervolgens op **Een certificaat bij een certificaatautoriteit aanvragen...**.</span><span class="sxs-lookup"><span data-stu-id="66bec-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="66bec-109">Selecteer uw **e-mailadres gebruiker** en **algemene naam** , zorg ervoor dat **opgeslagen toodisk** is geselecteerd en klik vervolgens op **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="66bec-109">Select your **User Email Address** and **Common Name** , make sure that **Saved toodisk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="66bec-110">Hallo laat **e-mailadres CA** veld leeg als dit niet vereist is.</span><span class="sxs-lookup"><span data-stu-id="66bec-110">Leave hello **CA Email Address** field blank as it is not required.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="66bec-111">Typ een naam voor Hallo Certificate Signing Request (CSR) bestand in **OpslaanAls**, selecteert u de locatie Hallo in **waar**, klikt u vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="66bec-111">Type a name for hello Certificate Signing Request (CSR) file in **Save As**, select hello location in **Where**, then click **Save**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="66bec-112">Dit bespaart Hallo CSR-bestand in Hallo geselecteerd location; de standaardlocatie Hallo is Hallo bureaublad.</span><span class="sxs-lookup"><span data-stu-id="66bec-112">This saves hello CSR file in hello selected location; hello default location is in hello Desktop.</span></span> <span data-ttu-id="66bec-113">Onthoud Hallo-locatie voor dit bestand hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="66bec-113">Remember hello location chosen for this file.</span></span>

<span data-ttu-id="66bec-114">U wordt vervolgens uw app registreren bij Apple, pushmeldingen inschakelen en dit geëxporteerde CSR toocreate een push-certificaat uploaden.</span><span class="sxs-lookup"><span data-stu-id="66bec-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR toocreate a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="66bec-115">Uw app voor pushmeldingen registreren</span><span class="sxs-lookup"><span data-stu-id="66bec-115">Register your app for push notifications</span></span>
<span data-ttu-id="66bec-116">toobe kunnen toosend push notifications tooan iOS-app, moet u uw toepassing registreren bij Apple, en ook registreren voor pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="66bec-116">toobe able toosend push notifications tooan iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="66bec-117">Als u uw app nog niet hebt geregistreerd, gaat u toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS-Inrichtingsportal</a> Hallo Apple Developer Center, meld u aan met uw Apple-ID, klikt u op **id's**, klikt u vervolgens op **App-id's** , en klik tot slot op Hallo  **+**  tooregister een nieuwe app te ondertekenen.</span><span class="sxs-lookup"><span data-stu-id="66bec-117">If you have not already registered your app, navigate toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at hello Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on hello **+** sign tooregister a new app.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="66bec-118">Hallo na drie velden voor uw nieuwe app bijwerken en klik vervolgens op **doorgaan**:</span><span class="sxs-lookup"><span data-stu-id="66bec-118">Update hello following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="66bec-119">**Naam**: Typ een beschrijvende naam voor uw app in Hallo **naam** veld Hallo **beschrijving App-ID** sectie.</span><span class="sxs-lookup"><span data-stu-id="66bec-119">**Name**: Type a descriptive name for your app in hello **Name** field in hello **App ID Description** section.</span></span>
   * <span data-ttu-id="66bec-120">**Bundel-id**: onder Hallo **expliciete App-ID** sectie, voert u een **bundel-id** Hallo vorm `<Organization Identifier>.<Product Name>` zoals vermeld in Hallo [distributie Handleiding](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span><span class="sxs-lookup"><span data-stu-id="66bec-120">**Bundle Identifier**: Under hello **Explicit App ID** section, enter a **Bundle Identifier** in hello form `<Organization Identifier>.<Product Name>` as mentioned in hello [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="66bec-121">Hallo *organisatie-id* en *Productnaam* u gebruikt, moet overeenkomen met Hallo organisatie-id en productnaam die u gebruikt wanneer u uw XCode-project maken.</span><span class="sxs-lookup"><span data-stu-id="66bec-121">hello *Organization Identifier* and *Product Name* you use must match hello organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="66bec-122">In onderstaande Hallo schermopname wordt *NotificationHubs* wordt gebruikt als de organisatie-id en *GetStarted* wordt gebruikt als Hallo productnaam.</span><span class="sxs-lookup"><span data-stu-id="66bec-122">In hello screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as hello product name.</span></span> <span data-ttu-id="66bec-123">Zorg dat dit overeenkomt met Hallo-waarden die u in uw XCode-project gebruiken wilt kunt u toouse Hallo juiste publicatieprofiel met XCode.</span><span class="sxs-lookup"><span data-stu-id="66bec-123">Making sure this matches hello values you will use in your XCode project will allow you toouse hello correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="66bec-124">**Pushmeldingen**: selectievakje Hallo **Pushmeldingen** optie in Hallo **App Services** sectie.</span><span class="sxs-lookup"><span data-stu-id="66bec-124">**Push Notifications**: Check hello **Push Notifications** option in hello **App Services** section, .</span></span>
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="66bec-125">Dit genereert de App-ID en vraagt u tooconfirm Hallo informatie.</span><span class="sxs-lookup"><span data-stu-id="66bec-125">This generates your App ID and requests you tooconfirm hello information.</span></span> <span data-ttu-id="66bec-126">Klik op **registreren** tooconfirm Hallo nieuwe App-ID.</span><span class="sxs-lookup"><span data-stu-id="66bec-126">Click **Register** tooconfirm hello new App ID.</span></span>
     
      <span data-ttu-id="66bec-127">Nadat u op **registreren**, ziet u Hallo **registratie is voltooid** scherm, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="66bec-127">Once you click **Register**, you will see hello **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="66bec-128">Klik op **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="66bec-128">Click **Done**.</span></span>
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="66bec-129">Zoek in Hallo Developer Center onder de App-id's Hallo app-ID die u zojuist hebt gemaakt en klik op de rij.</span><span class="sxs-lookup"><span data-stu-id="66bec-129">In hello Developer Center, under App IDs, locate hello app ID that you just created, and click on its row.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="66bec-130">Te klikken op Hallo app-ID weergegeven Hallo app-gegevens.</span><span class="sxs-lookup"><span data-stu-id="66bec-130">Clicking on hello app ID will display hello app details.</span></span> <span data-ttu-id="66bec-131">Klik op Hallo **bewerken** knop Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="66bec-131">Click hello **Edit** button at hello bottom.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="66bec-132">Schuif toohello onderaan welkomstscherm en klikt u op Hallo **certificaat maken...**  knop onder sectie Hallo **ontwikkeling Push-SSL-certificaat**.</span><span class="sxs-lookup"><span data-stu-id="66bec-132">Scroll toohello bottom of hello screen, and click hello **Create Certificate...** button under hello section **Development Push SSL Certificate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="66bec-133">Hallo-assistent iOS-certificaat toevoegen' worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="66bec-133">This displays hello "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="66bec-134">In deze zelfstudie wordt een ontwikkelingscertificaat gebruikt.</span><span class="sxs-lookup"><span data-stu-id="66bec-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="66bec-135">Hallo hetzelfde proces wordt gebruikt bij het registreren van een productiecertificaat.</span><span class="sxs-lookup"><span data-stu-id="66bec-135">hello same process is used when registering a production certificate.</span></span> <span data-ttu-id="66bec-136">Zorg ervoor dat u Hallo met dezelfde certificaattype bij het verzenden van meldingen.</span><span class="sxs-lookup"><span data-stu-id="66bec-136">Just make sure that you use hello same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="66bec-137">Klik op **bestand kiezen**, bladeren toohello-locatie waar u Hallo CSR-bestand dat u hebt gemaakt in de eerste taak Hallo hebt opgeslagen en klik vervolgens op **genereren**.</span><span class="sxs-lookup"><span data-stu-id="66bec-137">Click **Choose File**, browse toohello location where you saved hello CSR file that you created in hello first task, then click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="66bec-138">Nadat het Hallo-certificaat is gemaakt door Hallo-portal, klikt u op Hallo **downloaden** en klik op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="66bec-138">After hello certificate is created by hello portal, click hello **Download** button, and click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="66bec-139">Dit certificaat Hallo downloadt en tooyour computer in de map Downloads opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="66bec-139">This downloads hello certificate and saves it tooyour computer in your Downloads folder.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="66bec-140">Standaard, Hallo gedownload bestand een ontwikkelingscertificaat heet **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="66bec-140">By default, hello downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="66bec-141">Dubbelklik op het gedownloade pushcertificaat hello **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="66bec-141">Double-click hello downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="66bec-142">Hiermee installeert u nieuw certificaat Hallo in Hallo sleutelhanger, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="66bec-142">This installs hello new certificate in hello Keychain, as shown below:</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="66bec-143">Hallo-naam in uw certificaat kan afwijken, maar deze worden voorafgegaan door **Apple Development iOS Push Services:**.</span><span class="sxs-lookup"><span data-stu-id="66bec-143">hello name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="66bec-144">In Sleutelhangertoegang met de rechtermuisknop op Hallo nieuwe pushcertificaat dat u hebt gemaakt in Hallo **certificaten** categorie.</span><span class="sxs-lookup"><span data-stu-id="66bec-144">In Keychain Access, right-click hello new push certificate that you created in hello **Certificates** category.</span></span> <span data-ttu-id="66bec-145">Klik op **exporteren**, Hallo-bestand een naam, selecteer Hallo **.p12** formatteren, en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="66bec-145">Click **Export**, name hello file, select hello **.p12** format, and then click **Save**.</span></span>
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="66bec-146">Een notitie van Hallo bestandsnaam en locatie van Hallo geëxporteerde .p12-certificaat maken.</span><span class="sxs-lookup"><span data-stu-id="66bec-146">Make a note of hello file name and location of hello exported .p12 certificate.</span></span> <span data-ttu-id="66bec-147">Gebruikte tooenable verificatie met APNS zal zijn.</span><span class="sxs-lookup"><span data-stu-id="66bec-147">It will be used tooenable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="66bec-148">Tijdens deze zelfstudie wordt een QuickStart.p12-bestand gemaakt.</span><span class="sxs-lookup"><span data-stu-id="66bec-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="66bec-149">De naam en locatie van uw bestand kunnen afwijken.</span><span class="sxs-lookup"><span data-stu-id="66bec-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a><span data-ttu-id="66bec-150">Maak een inrichtingsprofiel voor Hallo-app</span><span class="sxs-lookup"><span data-stu-id="66bec-150">Create a provisioning profile for hello app</span></span>
1. <span data-ttu-id="66bec-151">Terug in Hallo <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS-Inrichtingsportal</a>, selecteer **Inrichtingsprofielen**, selecteer **alle**, en klik vervolgens op Hallo  **+**  knop toocreate een nieuw profiel.</span><span class="sxs-lookup"><span data-stu-id="66bec-151">Back in hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click hello **+** button toocreate a new profile.</span></span> <span data-ttu-id="66bec-152">Dit start Hallo **iOS-Inrichtingsprofielen toevoegen** Wizard</span><span class="sxs-lookup"><span data-stu-id="66bec-152">This launches hello **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="66bec-153">Selecteer **ontwikkeling iOS-App** onder **ontwikkeling** als Hallo inrichtingsprofieltype en klik op **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="66bec-153">Select **iOS App Development** under **Development** as hello provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="66bec-154">Selecteer vervolgens Hallo app-ID die u zojuist hebt gemaakt van Hallo **App-ID** vervolgkeuzelijst en klik op **doorgaan**</span><span class="sxs-lookup"><span data-stu-id="66bec-154">Next, select hello app ID you just created from hello **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="66bec-155">In Hallo **Selecteer certificaten** scherm, selecteert u het ontwikkelingscertificaat gebruikt voor ondertekening van programmacode en klikt u op **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="66bec-155">In hello **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="66bec-156">Dit is geen Hallo push-certificaat die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="66bec-156">This is not hello push certificate you just created.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="66bec-157">Selecteer vervolgens Hallo **apparaten** toouse voor testen en klik op **doorgaan**</span><span class="sxs-lookup"><span data-stu-id="66bec-157">Next, select hello **Devices** toouse for testing, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="66bec-158">Kies tot slot een naam voor het Hallo-profiel in **profielnaam**, klikt u op **genereren**.</span><span class="sxs-lookup"><span data-stu-id="66bec-158">Finally, pick a name for hello profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="66bec-159">Tijdens het maken van nieuwe profiel voor inrichting Hallo Ga toodownload deze en installeer deze op uw ontwikkelcomputer Xcode.</span><span class="sxs-lookup"><span data-stu-id="66bec-159">When hello new provisioning profile is created click toodownload it and install it on your Xcode development machine.</span></span> <span data-ttu-id="66bec-160">Klik vervolgens op **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="66bec-160">Then click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)

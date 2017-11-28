

## <a name="generate-the-certificate-signing-request-file"></a><span data-ttu-id="da88e-101">Het bestand met de aanvraag voor certificaatondertekening genereren</span><span class="sxs-lookup"><span data-stu-id="da88e-101">Generate the Certificate Signing Request file</span></span>
<span data-ttu-id="da88e-102">De Apple Push Notification Service (APNS) gebruikt certificaten om uw pushmeldingen te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="da88e-102">The Apple Push Notification Service (APNS) uses certificates to authenticate your push notifications.</span></span> <span data-ttu-id="da88e-103">Volg deze instructies om het pushcertificaat te maken dat vereist is om meldingen te verzenden en te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="da88e-103">Follow these instructions to create the necessary push certificate to send and receive notifications.</span></span> <span data-ttu-id="da88e-104">Zie de officiële documentatie van de [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) voor meer informatie over deze concepten.</span><span class="sxs-lookup"><span data-stu-id="da88e-104">For more information on these concepts see the official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="da88e-105">Genereer het bestand met de aanvraag voor certificaatondertekening dat door Apple wordt gebruikt om een ondertekend pushcertificaat te genereren.</span><span class="sxs-lookup"><span data-stu-id="da88e-105">Generate the Certificate Signing Request (CSR) file, which is used by Apple to generate a signed push certificate.</span></span>

1. <span data-ttu-id="da88e-106">Voer op uw Mac het hulpprogramma Sleutelhangertoegang uit.</span><span class="sxs-lookup"><span data-stu-id="da88e-106">On your Mac, run the Keychain Access tool.</span></span> <span data-ttu-id="da88e-107">Dit kan worden gestart vanuit de map **Hulpprogramma's** of de map **Overige** in Launchpad.</span><span class="sxs-lookup"><span data-stu-id="da88e-107">It can be opened from the **Utilities** folder or the **Other** folder on the launch pad.</span></span>
2. <span data-ttu-id="da88e-108">Klik op **Toegang tot sleutelhanger**, vouw **Certificaatassistent** uit, klik vervolgens op **Een certificaat bij een certificaatautoriteit aanvragen...**.</span><span class="sxs-lookup"><span data-stu-id="da88e-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="da88e-109">Selecteer uw **gebruikers-e-mailadres** en **algemene naam**, controleer of **Opgeslagen op schijf** is geselecteerd en klik vervolgens op **Doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="da88e-109">Select your **User Email Address** and **Common Name** , make sure that **Saved to disk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="da88e-110">Laat het veld **E-mailadres CA** leeg omdat dit niet is vereist.</span><span class="sxs-lookup"><span data-stu-id="da88e-110">Leave the **CA Email Address** field blank as it is not required.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="da88e-111">Typ een naam voor het bestand met de aanvraag voor certificaatondertekening in **Opslaan als**, selecteer de locatie in **Waar**, klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="da88e-111">Type a name for the Certificate Signing Request (CSR) file in **Save As**, select the location in **Where**, then click **Save**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="da88e-112">Het bestand met de aanvraag voor certificaatondertekening wordt opgeslagen op de geselecteerde locatie; de standaardlocatie is op het Bureaublad.</span><span class="sxs-lookup"><span data-stu-id="da88e-112">This saves the CSR file in the selected location; the default location is in the Desktop.</span></span> <span data-ttu-id="da88e-113">Onthoud de locatie die u voor dit bestand hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="da88e-113">Remember the location chosen for this file.</span></span>

<span data-ttu-id="da88e-114">Vervolgens gaat u uw app registreren bij Apple, pushmeldingen inschakelen en dit geëxporteerde bestand met de aanvraag voor certificaatondertekening uploaden om een pushcertificaat te maken.</span><span class="sxs-lookup"><span data-stu-id="da88e-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR to create a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="da88e-115">Uw app voor pushmeldingen registreren</span><span class="sxs-lookup"><span data-stu-id="da88e-115">Register your app for push notifications</span></span>
<span data-ttu-id="da88e-116">U moet u app bij Apple registreren en u voor pushmeldingen registeren om pushmeldingen te kunnen verzenden naar een iOS-app.</span><span class="sxs-lookup"><span data-stu-id="da88e-116">To be able to send push notifications to an iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="da88e-117">Als u uw app nog niet hebt geregistreerd, gaat u naar de <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS-inrichtingsportal</a>, meldt u zich aan bij het Apple Developer Center met uw Apple ID, klikt u op **Id's**, klikt u vervolgens op **App-id's** en ten slotte op het **+**-teken om een nieuwe app te registreren.</span><span class="sxs-lookup"><span data-stu-id="da88e-117">If you have not already registered your app, navigate to the <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at the Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on the **+** sign to register a new app.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="da88e-118">Werk de volgende drie velden voor uw nieuwe app bij en klik vervolgens op **Doorgaan**:</span><span class="sxs-lookup"><span data-stu-id="da88e-118">Update the following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="da88e-119">**Naam**: typ een beschrijvende naam voor uw app in het veld **Naam** in de sectie **Beschrijving app-id**.</span><span class="sxs-lookup"><span data-stu-id="da88e-119">**Name**: Type a descriptive name for your app in the **Name** field in the **App ID Description** section.</span></span>
   * <span data-ttu-id="da88e-120">**Bundel-id**: onder de sectie **Expliciete app-id** typt u een **bundel-id** in het formulier `<Organization Identifier>.<Product Name>` zoals vermeld in de [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8) (Gids voor apps-distributie).</span><span class="sxs-lookup"><span data-stu-id="da88e-120">**Bundle Identifier**: Under the **Explicit App ID** section, enter a **Bundle Identifier** in the form `<Organization Identifier>.<Product Name>` as mentioned in the [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="da88e-121">De *organisatie-id* en *productnaam* die u gebruikt, moet overeenkomen met de organisatie-id en productnaam die u gebruikt als u een XCode-project gaat maken.</span><span class="sxs-lookup"><span data-stu-id="da88e-121">The *Organization Identifier* and *Product Name* you use must match the organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="da88e-122">In de onderstaande schermopname wordt *NotificationHubs* gebruikt als de organisatie-id en *GetStarted* als de productnaam.</span><span class="sxs-lookup"><span data-stu-id="da88e-122">In the screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as the product name.</span></span> <span data-ttu-id="da88e-123">Door ervoor te zorgen dat deze overeenkomen met waarden die u gaat gebruiken in uw XCode-project, is het mogelijk om het juiste publicatieprofiel met XCode te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="da88e-123">Making sure this matches the values you will use in your XCode project will allow you to use the correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="da88e-124">**Pushmeldingen**: selecteer de optie **Pushmeldingen** in de sectie **App Services**.</span><span class="sxs-lookup"><span data-stu-id="da88e-124">**Push Notifications**: Check the **Push Notifications** option in the **App Services** section, .</span></span>
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="da88e-125">Hiermee wordt uw app-id gegenereerd en wordt u gevraagd de gegevens te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="da88e-125">This generates your App ID and requests you to confirm the information.</span></span> <span data-ttu-id="da88e-126">Klik op **Registreren** om de nieuwe app-id te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="da88e-126">Click **Register** to confirm the new App ID.</span></span>
     
      <span data-ttu-id="da88e-127">Nadat u op **Registreren** hebt geklikt, wordt het scherm **Registratie voltooid** weergegeven, zoals u hieronder ziet.</span><span class="sxs-lookup"><span data-stu-id="da88e-127">Once you click **Register**, you will see the **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="da88e-128">Klik op **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="da88e-128">Click **Done**.</span></span>
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="da88e-129">Ga in het Developer Center onder de app-id’s naar de app-id die u zojuist hebt gemaakt en klik op de rij van die id.</span><span class="sxs-lookup"><span data-stu-id="da88e-129">In the Developer Center, under App IDs, locate the app ID that you just created, and click on its row.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="da88e-130">Door op de app-id te klikken, worden de gegevens van de app weergegeven.</span><span class="sxs-lookup"><span data-stu-id="da88e-130">Clicking on the app ID will display the app details.</span></span> <span data-ttu-id="da88e-131">Klik op de knop **Bewerken** onderaan.</span><span class="sxs-lookup"><span data-stu-id="da88e-131">Click the **Edit** button at the bottom.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="da88e-132">Ga naar de onderkant van het scherm en klik op de knop **Certificaat maken** onder de sectie **Ontwikkeling push-SSL-certificaat**.</span><span class="sxs-lookup"><span data-stu-id="da88e-132">Scroll to the bottom of the screen, and click the **Create Certificate...** button under the section **Development Push SSL Certificate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="da88e-133">Nu wordt de assistent IOS-certificaat toevoegen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="da88e-133">This displays the "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="da88e-134">In deze zelfstudie wordt een ontwikkelingscertificaat gebruikt.</span><span class="sxs-lookup"><span data-stu-id="da88e-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="da88e-135">Hetzelfde proces wordt gebruikt bij het registreren van een productiecertificaat.</span><span class="sxs-lookup"><span data-stu-id="da88e-135">The same process is used when registering a production certificate.</span></span> <span data-ttu-id="da88e-136">Zorg er wel voor dat u hetzelfde certificaattype gebruikt als u meldingen verzendt.</span><span class="sxs-lookup"><span data-stu-id="da88e-136">Just make sure that you use the same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="da88e-137">Klik op **Bestand kiezen**, blader naar de locatie waar u het bestand met de aanvraag voor certificaatondertekening hebt opgeslagen dat u in de eerste taak hebt gemaakt, en klik vervolgens op **Genereren**.</span><span class="sxs-lookup"><span data-stu-id="da88e-137">Click **Choose File**, browse to the location where you saved the CSR file that you created in the first task, then click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="da88e-138">Nadat het certificaat met de portal is gemaakt, klikt u op de knop **Downloaden** en klikt u vervolgens op **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="da88e-138">After the certificate is created by the portal, click the **Download** button, and click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="da88e-139">Het certificaat wordt nu gedownload en op uw computer in de map Downloads opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="da88e-139">This downloads the certificate and saves it to your computer in your Downloads folder.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="da88e-140">Standaard krijgt het gedownloade bestand, een ontwikkelingscertificaat, de naam **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="da88e-140">By default, the downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="da88e-141">Dubbelklik op het gedownloade pushcertificaat **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="da88e-141">Double-click the downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="da88e-142">Nu wordt het nieuwe certificaat in de sleutelhanger geïnstalleerd, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="da88e-142">This installs the new certificate in the Keychain, as shown below:</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="da88e-143">De naam in uw certificaat kan afwijken, maar wordt voorafgegaan door **Apple Development iOS Push Services:**.</span><span class="sxs-lookup"><span data-stu-id="da88e-143">The name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="da88e-144">In Sleutelhangertoegang klikt u met de rechtermuisknop op het nieuwe pushcertificaat dat u hebt gemaakt in de categorie **Certificaten**.</span><span class="sxs-lookup"><span data-stu-id="da88e-144">In Keychain Access, right-click the new push certificate that you created in the **Certificates** category.</span></span> <span data-ttu-id="da88e-145">Klik op **Exporteer**, geef het bestand een naam, selecteer de **.p12**-indeling en klik vervolgens op **Bewaar**.</span><span class="sxs-lookup"><span data-stu-id="da88e-145">Click **Export**, name the file, select the **.p12** format, and then click **Save**.</span></span>
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="da88e-146">Noteer de bestandsnaam en locatie van het geëxporteerde .p12-certificaat.</span><span class="sxs-lookup"><span data-stu-id="da88e-146">Make a note of the file name and location of the exported .p12 certificate.</span></span> <span data-ttu-id="da88e-147">Dit wordt gebruikt om verificatie met APNS mogelijk te maken.</span><span class="sxs-lookup"><span data-stu-id="da88e-147">It will be used to enable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="da88e-148">Tijdens deze zelfstudie wordt een QuickStart.p12-bestand gemaakt.</span><span class="sxs-lookup"><span data-stu-id="da88e-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="da88e-149">De naam en locatie van uw bestand kunnen afwijken.</span><span class="sxs-lookup"><span data-stu-id="da88e-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-the-app"></a><span data-ttu-id="da88e-150">Een inrichtingsprofiel voor de app maken</span><span class="sxs-lookup"><span data-stu-id="da88e-150">Create a provisioning profile for the app</span></span>
1. <span data-ttu-id="da88e-151">Terug in de <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS-inrichtingsportal</a> selecteert u **Inrichtingsprofielen**, selecteert u **Alle** en klikt u vervolgens op de knop met het **+**-teken om een nieuw profiel te maken.</span><span class="sxs-lookup"><span data-stu-id="da88e-151">Back in the <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click the **+** button to create a new profile.</span></span> <span data-ttu-id="da88e-152">Nu wordt de wizard **iOS-inrichtingsprofielen toevoegen** gestart.</span><span class="sxs-lookup"><span data-stu-id="da88e-152">This launches the **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="da88e-153">Selecteer **Ontwikkeling iOS-app** onder **Ontwikkeling** als het inrichtingsprofieltype en klik vervolgens op **Doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="da88e-153">Select **iOS App Development** under **Development** as the provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="da88e-154">Selecteer vervolgens in de vervolgkeuzelijst **App-id** de app-id die u zojuist hebt gemaakt en klik op **Doorgaan**</span><span class="sxs-lookup"><span data-stu-id="da88e-154">Next, select the app ID you just created from the **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="da88e-155">In het scherm **Certificaten selecteren** selecteert u het ontwikkelingscertificaat dat u doorgaans gebruikt voor het ondertekenen van programmacode en klikt u op **Doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="da88e-155">In the **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="da88e-156">Dit is niet het pushcertificaat dat u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="da88e-156">This is not the push certificate you just created.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="da88e-157">Selecteer vervolgens de **apparaten** die u voor de tests wilt gebruiken en klik op **Doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="da88e-157">Next, select the **Devices** to use for testing, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="da88e-158">Kies tot slot een naam voor het profiel in **Profielnaam** en klik op **Genereren**.</span><span class="sxs-lookup"><span data-stu-id="da88e-158">Finally, pick a name for the profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="da88e-159">Als het nieuwe inrichtingsprofiel is gemaakt, klikt u erop om het te downloaden en op uw machine met de Xcode-ontwikkelcode te installeren.</span><span class="sxs-lookup"><span data-stu-id="da88e-159">When the new provisioning profile is created click to download it and install it on your Xcode development machine.</span></span> <span data-ttu-id="da88e-160">Klik vervolgens op **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="da88e-160">Then click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)

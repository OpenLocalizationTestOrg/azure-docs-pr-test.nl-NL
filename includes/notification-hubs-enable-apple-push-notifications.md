

## <a name="generate-hello-certificate-signing-request-file"></a>Aanvraag voor Certificaatondertekening Hallo-bestand genereren
Hallo Apple Push Notification Service (APNS) gebruikt certificaten tooauthenticate uw pushmeldingen. Volg deze instructies toocreate Hallo nodig push-certificaat toosend en meldingen ontvangen. Zie voor meer informatie over deze begrippen Hallo officiële [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentatie.

Hallo Certificate Signing Request (CSR)-bestand genereren die worden gebruikt door Apple toogenerate een ondertekend pushcertificaat.

1. Voer op uw Mac Hallo hulpprogramma Sleutelhangertoegang uit. Het kan worden geopend vanuit Hallo **hulpprogramma's** map of Hallo **andere** map op Hallo launchpad.
2. Klik op **Toegang tot sleutelhanger**, vouw **Certificaatassistent** uit, klik vervolgens op **Een certificaat bij een certificaatautoriteit aanvragen...**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. Selecteer uw **e-mailadres gebruiker** en **algemene naam** , zorg ervoor dat **opgeslagen toodisk** is geselecteerd en klik vervolgens op **doorgaan**. Hallo laat **e-mailadres CA** veld leeg als dit niet vereist is.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. Typ een naam voor Hallo Certificate Signing Request (CSR) bestand in **OpslaanAls**, selecteert u de locatie Hallo in **waar**, klikt u vervolgens op **opslaan**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      Dit bespaart Hallo CSR-bestand in Hallo geselecteerd location; de standaardlocatie Hallo is Hallo bureaublad. Onthoud Hallo-locatie voor dit bestand hebt gekozen.

U wordt vervolgens uw app registreren bij Apple, pushmeldingen inschakelen en dit geëxporteerde CSR toocreate een push-certificaat uploaden.

## <a name="register-your-app-for-push-notifications"></a>Uw app voor pushmeldingen registreren
toobe kunnen toosend push notifications tooan iOS-app, moet u uw toepassing registreren bij Apple, en ook registreren voor pushmeldingen.  

1. Als u uw app nog niet hebt geregistreerd, gaat u toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS-Inrichtingsportal</a> Hallo Apple Developer Center, meld u aan met uw Apple-ID, klikt u op **id's**, klikt u vervolgens op **App-id's** , en klik tot slot op Hallo  **+**  tooregister een nieuwe app te ondertekenen.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. Hallo na drie velden voor uw nieuwe app bijwerken en klik vervolgens op **doorgaan**:
   
   * **Naam**: Typ een beschrijvende naam voor uw app in Hallo **naam** veld Hallo **beschrijving App-ID** sectie.
   * **Bundel-id**: onder Hallo **expliciete App-ID** sectie, voert u een **bundel-id** Hallo vorm `<Organization Identifier>.<Product Name>` zoals vermeld in Hallo [distributie Handleiding](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8). Hallo *organisatie-id* en *Productnaam* u gebruikt, moet overeenkomen met Hallo organisatie-id en productnaam die u gebruikt wanneer u uw XCode-project maken. In onderstaande Hallo schermopname wordt *NotificationHubs* wordt gebruikt als de organisatie-id en *GetStarted* wordt gebruikt als Hallo productnaam. Zorg dat dit overeenkomt met Hallo-waarden die u in uw XCode-project gebruiken wilt kunt u toouse Hallo juiste publicatieprofiel met XCode. 
   * **Pushmeldingen**: selectievakje Hallo **Pushmeldingen** optie in Hallo **App Services** sectie.
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      Dit genereert de App-ID en vraagt u tooconfirm Hallo informatie. Klik op **registreren** tooconfirm Hallo nieuwe App-ID.
     
      Nadat u op **registreren**, ziet u Hallo **registratie is voltooid** scherm, zoals hieronder wordt weergegeven. Klik op **Gereed**.
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. Zoek in Hallo Developer Center onder de App-id's Hallo app-ID die u zojuist hebt gemaakt en klik op de rij.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      Te klikken op Hallo app-ID weergegeven Hallo app-gegevens. Klik op Hallo **bewerken** knop Hallo onder aan.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. Schuif toohello onderaan welkomstscherm en klikt u op Hallo **certificaat maken...**  knop onder sectie Hallo **ontwikkeling Push-SSL-certificaat**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      Hallo-assistent iOS-certificaat toevoegen' worden weergegeven.
   
   > [!NOTE]
   > In deze zelfstudie wordt een ontwikkelingscertificaat gebruikt. Hallo hetzelfde proces wordt gebruikt bij het registreren van een productiecertificaat. Zorg ervoor dat u Hallo met dezelfde certificaattype bij het verzenden van meldingen.
   > 
   > 
3. Klik op **bestand kiezen**, bladeren toohello-locatie waar u Hallo CSR-bestand dat u hebt gemaakt in de eerste taak Hallo hebt opgeslagen en klik vervolgens op **genereren**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. Nadat het Hallo-certificaat is gemaakt door Hallo-portal, klikt u op Hallo **downloaden** en klik op **gedaan**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      Dit certificaat Hallo downloadt en tooyour computer in de map Downloads opgeslagen.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > Standaard, Hallo gedownload bestand een ontwikkelingscertificaat heet **aps_development.cer**.
   > 
   > 
5. Dubbelklik op het gedownloade pushcertificaat hello **aps_development.cer**.
   
      Hiermee installeert u nieuw certificaat Hallo in Hallo sleutelhanger, zoals hieronder wordt weergegeven:
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > Hallo-naam in uw certificaat kan afwijken, maar deze worden voorafgegaan door **Apple Development iOS Push Services:**.
   > 
   > 
6. In Sleutelhangertoegang met de rechtermuisknop op Hallo nieuwe pushcertificaat dat u hebt gemaakt in Hallo **certificaten** categorie. Klik op **exporteren**, Hallo-bestand een naam, selecteer Hallo **.p12** formatteren, en klik vervolgens op **opslaan**.
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    Een notitie van Hallo bestandsnaam en locatie van Hallo geëxporteerde .p12-certificaat maken. Gebruikte tooenable verificatie met APNS zal zijn.
   
   > [!NOTE]
   > Tijdens deze zelfstudie wordt een QuickStart.p12-bestand gemaakt. De naam en locatie van uw bestand kunnen afwijken.
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a>Maak een inrichtingsprofiel voor Hallo-app
1. Terug in Hallo <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS-Inrichtingsportal</a>, selecteer **Inrichtingsprofielen**, selecteer **alle**, en klik vervolgens op Hallo  **+**  knop toocreate een nieuw profiel. Dit start Hallo **iOS-Inrichtingsprofielen toevoegen** Wizard
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. Selecteer **ontwikkeling iOS-App** onder **ontwikkeling** als Hallo inrichtingsprofieltype en klik op **doorgaan**. 
3. Selecteer vervolgens Hallo app-ID die u zojuist hebt gemaakt van Hallo **App-ID** vervolgkeuzelijst en klik op **doorgaan**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. In Hallo **Selecteer certificaten** scherm, selecteert u het ontwikkelingscertificaat gebruikt voor ondertekening van programmacode en klikt u op **doorgaan**. Dit is geen Hallo push-certificaat die u zojuist hebt gemaakt.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. Selecteer vervolgens Hallo **apparaten** toouse voor testen en klik op **doorgaan**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. Kies tot slot een naam voor het Hallo-profiel in **profielnaam**, klikt u op **genereren**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. Tijdens het maken van nieuwe profiel voor inrichting Hallo Ga toodownload deze en installeer deze op uw ontwikkelcomputer Xcode. Klik vervolgens op **Gereed**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)

<!--author=alkohli last changed: 12/01/15-->


#### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure en registreer Hallo-apparaat
1. Toegang tot Hallo Windows PowerShell-interface op de seriële console van het StorSimple-apparaat. Zie [PuTTY gebruiken tooconnect toohello de seriële console apparaat](#use-putty-to-connect-to-the-device-serial-console) voor instructies. **Ervoor toofollow Hallo procedure exact worden of u zich niet kunnen tooaccess Hallo-console.**
2. Druk op Enter één keer tooget vanaf de opdrachtprompt in Hallo-sessie die wordt geopend. 
3. U zult na vragen aan gebruiker toochoose Hallo taal dat u tooset voor uw apparaat dat wilt. Hallo taal op te geven en druk op Enter. 
   
    ![Apparaat 1 configureren en registreren met StorSimple](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice1-include.png)
4. Kies optie 1 toolog op met volledige toegang in Hallo seriële consolemenu wordt weergegeven. 
   
    ![Apparaat 2 registreren met StorSimple](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice2-include.png)
   
     Voltooi de stappen 5-12 tooconfigure Hallo minimale vereiste netwerkinstellingen voor uw apparaat. **Deze configuratiestappen moeten toobe uitgevoerd op de actieve controller Hallo Hallo-apparaat.** menu van de seriële console Hallo geeft Hallo controllerstatus in de banner het Hallo-bericht. Als u niet verbonden bent wordt toohello actieve controller, verbreken en sluit vervolgens toohello actieve controller.
5. Typ uw wachtwoord bij de opdrachtprompt Hallo. Hallo standaardapparaatwachtwoord is **Wachtwoord1**.
6. Type Hallo volgende opdracht:
   
     `Invoke-HcsSetupWizard` 
7. Een setup-wizard verschijnt toohelp u Hallo netwerkinstellingen voor Hallo apparaat configureren. Geef Hallo Hallo volgende informatie: 
   
   * IP-adres voor Hallo DATA 0-netwerkinterface
   * Subnetmasker
   * Gateway
   * IP-adres voor de primaire DNS-server
   * IP-adres voor de primaire NTP-server
     
     > [!NOTE]
     > Mogelijk hebt u toowait voor een paar minuten voordat het Hallo-subnetmasker en Hallo DNS-instellingen toobe toegepast. Als u krijgt een 'Hallo-apparaat is niet gereed.' foutbericht op het selectievakje Hallo fysieke netwerkverbinding voor Hallo DATA 0-netwerkinterface van uw actieve controller.
     > 
     > 
8. Configureer desgewenst uw webproxyserver. De configuratie van uw webproxy is weliswaar optioneel, maar **houd er rekening mee dat als u een webproxy gebruikt, deze alleen hier kan worden geconfigureerd**. Voor meer informatie gaat te[webproxy voor uw apparaat configureren](../articles/storsimple/storsimple-configure-web-proxy.md). Als u problemen ondervindt tijdens deze stap, Raadpleeg de richtlijnen voor tootroubleshooting [fouten tijdens de webproxyconfiguratie](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-the-optional-web-proxy-settings).

     > [!NOTE]
     > U drukt op Ctrl + C op een tijd tooexit Hallo setup-wizard. Alle instellingen die u hebt toegepast voordat u deze opdracht gaf, blijven behouden.

1. Uit veiligheidsoverwegingen wachtwoord apparaatbeheerder Hallo na Hallo eerste sessie verlopen en moet u toochange voor volgende sessies. Als daarom wordt gevraagd, geeft u een beheerderswachtwoord voor het apparaat op. Een geldig beheerderswachtwoord voor een apparaat moet 8 tot 15 tekens bevatten. Hallo-wachtwoord moet een combinatie van kleine letters, hoofdletters, cijfers en speciale tekens bevatten.
2. Hallo StorSimple Snapshot Manager-wachtwoord wordt hier ook ingesteld. U kunt dit wachtwoord gebruiken wanneer u een apparaat verifieert met uw Windows-host waarop StorSimple Snapshot Manager wordt uitgevoerd. Geef desgevraagd een wachtwoord van 14 too15 tekens. Hallo wachtwoord moet bestaan uit een combinatie van drie van de volgende Hallo: kleine letters, hoofdletters, numerieke en speciale tekens. 
   
   ![Apparaat 4 registreren met StorSimple](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice4-include.png)
   
   U kunt Hallo StorSimple Snapshot Manager wachtwoord uit Hallo StorSimple Manager-service-interface opnieuw instellen. Voor gedetailleerde stappen gaat te[hello StorSimple-wachtwoorden met Hallo StorSimple Manager-service wijzigen](../articles/storsimple/storsimple-change-passwords.md).
   
   tootroubleshoot problemen tijdens deze stap, raadpleegt u tootroubleshooting richtlijnen voor [fouten met betrekking toopasswords](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-related-to-device-administrator-and-storsimple-snapshot-manager-passwords).
3. laatste stap in de wizard setup Hallo Hallo registreert uw apparaat bij Hallo StorSimple Manager-service. Hiervoor moet u Hallo serviceregistratiesleutel die u hebt verkregen in stap 2. Nadat u de registratiesleutel Hallo opgeeft, moet u wellicht toowait 2-3 minuten voordat het Hallo-apparaat is geregistreerd.
   
   tootroubleshoot mogelijk apparaat registratiefouten, Raadpleeg te[fouten tijdens de apparaatregistratie](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-device-registration). Voor gedetailleerde probleemoplossing, kunt u ook verwijzen te[voorbeeld van stapsgewijze probleemoplossing](../articles/storsimple/storsimple-troubleshoot-deployment.md#step-by-step-storsimple-troubleshooting-example).
4. Nadat het Hallo-apparaat is geregistreerd, weergegeven een gegevensversleutelingssleutel van Service. Kopieer deze sleutel en bewaar deze op een veilige plaats.
   
   > [!WARNING]
   > Deze sleutel is vereist bij het Hallo-service registratie sleutel tooregister extra apparaten Hello StorSimple Manager-service. Raadpleeg te[StorSimple security](../articles/storsimple/storsimple-security.md) voor meer informatie over deze sleutel.
   > 
   > 
   
    ![Apparaat 6 registreren met StorSimple](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice6-include.png)
   
    toocopy hello tekst uit Hallo seriële console-venster, selecteert u de tekst hello. U moet kunnen toopaste in Hallo Klembord of een teksteditor. Gebruik geen Ctrl + C toocopy Hallo service gegevensversleutelingssleutel. Gebruik Ctrl + c drukken zorgt ervoor dat u tooexit Hallo installatiewizard. Als gevolg hiervan beheerderswachtwoord Hallo-apparaat en het Hallo StorSimple Snapshot Manager wachtwoord worden niet gewijzigd en Hallo standaardwachtwoorden toohello standaard wachtwoorden.
5. Exit Hallo seriële console.
6. Retourneren van toohello klassieke Azure-portal en Voer Hallo stappen te volgen:
   
   1. Dubbelklik op uw StorSimple Manager service tooaccess hello **Quick Start** pagina.
   2. Klik op **Verbonden apparaten weergeven**.
   3. Op Hallo **apparaten** pagina, controleert u of Hallo apparaat verbinding heeft met toohello service door het opzoeken van Hallo status. Hallo Apparaatstatus moet **Online**. Als de apparaatstatus Hallo **Offline**, wacht een paar minuten voor Hallo apparaat toocome online.
   
   ![Pagina StorSimple-apparaten](./media/storsimple-configure-and-register-device/HCS_DevicesPageM-include.png) 
   
   > [!IMPORTANT]
   > Nadat het Hallo-apparaat online is, sluit Hallo netwerkkabels die u in het begin van deze stap Hallo netwerkkabels.
   > 
   > 

Nadat het Hallo-apparaat is geregistreerd en niet online is geleverd, kunt u Hallo uitvoeren `Test-HcsmConnection -Verbose` tooensure die Hallo netwerkverbinding in orde is. Voor Hallo gaat u gedetailleerde informatie over het gebruik van deze cmdlet te[cmdlet-naslaginformatie voor Test-HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx).

![Video beschikbaar](./media/storsimple-configure-and-register-device/Video_icon.png) **Video beschikbaar**

toowatch een video die u laat zien hoe tooconfigure en Registreer uw apparaat via Windows PowerShell voor StorSimple, klikt u op [hier](https://azure.microsoft.com/documentation/videos/initialize-the-storsimple-appliance/).


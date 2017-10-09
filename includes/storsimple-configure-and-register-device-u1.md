<!--author=alkohli last changed: 02/22/2016-->


### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure en registreer Hallo-apparaat
1. Toegang tot Hallo Windows PowerShell-interface op de seriële console van het StorSimple-apparaat. Zie [PuTTY gebruiken tooconnect toohello de seriële console apparaat](#use-putty-to-connect-to-the-device-serial-console) voor instructies. **Ervoor toofollow Hallo procedure exact worden of u zich niet kunnen tooaccess Hallo-console.**
2. Druk op Enter één keer tooget vanaf de opdrachtprompt in Hallo-sessie die wordt geopend. 
3. U zult na vragen aan gebruiker toochoose Hallo taal dat u tooset voor uw apparaat dat wilt. Hallo taal op te geven en druk op Enter. 
   
    ![Apparaat 1 configureren en registreren met StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice1-U1-include.png)
4. Kies optie 1 toolog op met volledige toegang in Hallo seriële consolemenu wordt weergegeven. 
   
    ![Apparaat 2 registreren met StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice2_U1-include.png)
   
     Voltooi de stappen 5-12 tooconfigure Hallo minimale vereiste netwerkinstellingen voor uw apparaat. **Deze configuratiestappen moeten toobe uitgevoerd op de actieve controller Hallo Hallo-apparaat.** menu van de seriële console Hallo geeft Hallo controllerstatus in de banner het Hallo-bericht. Als u niet verbonden bent wordt toohello actieve controller, verbreken en sluit vervolgens toohello actieve controller.
5. Typ uw wachtwoord bij de opdrachtprompt Hallo. Hallo standaardapparaatwachtwoord is **Wachtwoord1**.
6. Type Hallo volgende opdracht: `Invoke-HcsSetupWizard`. 
7. Een setup-wizard verschijnt toohelp u Hallo netwerkinstellingen voor Hallo apparaat configureren. Geef Hallo Hallo volgende informatie: 
   
   * IP-adres voor Hallo DATA 0-netwerkinterface
   * Subnetmasker
   * Gateway
   * IP-adres voor de primaire DNS-server
     
        Houd er rekening mee dat Hallo gevalideerd netwerkinstellingen na elke stap in Hallo-proces.
     
     > [!NOTE]
     > Mogelijk hebt u toowait voor een paar minuten voordat het Hallo-subnetmasker en Hallo DNS-instellingen toobe toegepast. Als u krijgt een foutbericht 'Selectievakje Hallo network connectivity tooData 0', controleert u Hallo fysieke netwerkverbinding voor Hallo DATA 0-netwerkinterface van uw actieve controller.
     > 
     > 
8. Configureer desgewenst uw webproxyserver. De configuratie van uw webproxy is weliswaar optioneel, maar **houd er rekening mee dat als u een webproxy gebruikt, deze alleen hier kan worden geconfigureerd**. Voor meer informatie gaat te[webproxy voor uw apparaat configureren](../articles/storsimple/storsimple-configure-web-proxy.md).
9. Configureer een primaire NTP-server voor uw apparaat. NTP-servers zijn vereist, omdat uw apparaat de tijd moet synchroniseren voor verificatie met uw cloudserviceproviders. Zorg ervoor dat uw netwerk NTP-verkeer toopass van uw datacenter toohello Internet toestaat. Als dit niet mogelijk is, geeft u een interne NTP-server op. 
10. Uit veiligheidsoverwegingen wachtwoord apparaatbeheerder Hallo na Hallo eerste sessie verlopen en moet u toochange deze nu. Als daarom wordt gevraagd, geeft u een beheerderswachtwoord voor het apparaat op. Een geldig beheerderswachtwoord voor een apparaat moet 8 tot 15 tekens bevatten. Hallo wachtwoord moet bevatten drie van de volgende Hallo: kleine letters, hoofdletters, numerieke en speciale tekens.
    
    <br/>![Apparaat 5 registreren met StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice5_U1-include.png)
11. laatste stap in de wizard setup Hallo Hallo registreert uw apparaat bij Hallo StorSimple Manager-service. Hiervoor moet u Hallo serviceregistratiesleutel die u hebt verkregen in stap 2. Nadat u de registratiesleutel Hallo opgeeft, moet u wellicht toowait 2-3 minuten voordat het Hallo-apparaat is geregistreerd.
    
    > [!NOTE]
    > U drukt op Ctrl + C op een tijd tooexit Hallo setup-wizard. Als u alle Hallo netwerkinstellingen (IP-adres voor Data 0, subnetmasker en Gateway) hebt ingevoerd, wordt uw vermeldingen behouden blijft.
    > 
    > 
    
    ![Apparaat 6 registreren met StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice6_U1-include.png)
12. Nadat het Hallo-apparaat is geregistreerd, weergegeven een gegevensversleutelingssleutel van Service. Kopieer deze sleutel en bewaar deze op een veilige plaats. **Deze sleutel is vereist bij het Hallo-service registratie sleutel tooregister extra apparaten Hello StorSimple Manager-service.** Raadpleeg te[StorSimple security](../articles/storsimple/storsimple-security.md) voor meer informatie over deze sleutel.
    
    ![Apparaat 7 registreren met StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice7_U1-include.png)    
    
    > [!NOTE]
    > toocopy hello tekst uit Hallo seriële console-venster, selecteert u de tekst hello. U moet kunnen toopaste in Hallo Klembord of een teksteditor. Gebruik geen Ctrl + C toocopy Hallo service gegevensversleutelingssleutel. Gebruik Ctrl + c drukken zorgt ervoor dat u tooexit Hallo installatiewizard. Als gevolg hiervan Hallo apparaat administrator-wachtwoord worden niet gewijzigd en Hallo apparaat toohello standaardwachtwoord wordt teruggezet.
    > 
    > 
13. Exit Hallo seriële console.
14. Retourneren van toohello klassieke Azure-portal en Voer Hallo stappen te volgen:
    
    1. Dubbelklik op uw StorSimple Manager service tooaccess hello **Quick Start** pagina.
    2. Klik op **Verbonden apparaten weergeven**.
    3. Op Hallo **apparaten** pagina, controleert u of Hallo apparaat verbinding heeft met toohello service door het opzoeken van Hallo status. Hallo Apparaatstatus moet **Online**.
       
        ![Pagina StorSimple-apparaten](./media/storsimple-configure-and-register-device-u1/HCS_DevicesPageM_U1-include.png) 
       
        Als de apparaatstatus Hallo **Offline**, wacht een paar minuten voor Hallo apparaat toocome online. 
       
        Als Hallo apparaat na een paar minuten nog steeds offline is, moet u ervoor dat uw firewallnetwerk is geconfigureerd zoals beschreven in toomake [netwerkvereisten voor uw StorSimple-apparaat](../articles/storsimple/storsimple-system-requirements.md). 
       
        Controleer of poort 9354 open is voor uitgaande communicatie als deze door Hallo servicebus wordt gebruikt voor communicatie van de StorSimple Manager-Service-naar-apparaat.


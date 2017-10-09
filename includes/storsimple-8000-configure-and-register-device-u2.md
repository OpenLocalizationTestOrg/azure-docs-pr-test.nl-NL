<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure en registreer Hallo-apparaat

1. Toegang tot Hallo Windows PowerShell-interface op de seriële console van het StorSimple-apparaat. Zie [PuTTY gebruiken tooconnect toohello de seriële console apparaat](#use-putty-to-connect-to-the-device-serial-console) voor instructies. **Ervoor toofollow Hallo procedure exact worden of u zich niet kunnen tooaccess Hallo-console.**

2. Hallo-sessie die wordt geopend, klikt u op **Enter** één keer tooget vanaf de opdrachtprompt.

3. U zult na vragen aan gebruiker toochoose Hallo taal dat u tooset voor uw apparaat dat wilt. Hallo taal op te geven en druk vervolgens op **Enter**.

4. Hallo seriële console menu wordt weergegeven, kies optie 1 te**aanmelden met volledige toegang**.
     Voltooi de stappen 5-12 tooconfigure Hallo minimale vereiste netwerkinstellingen voor uw apparaat. **Deze configuratiestappen moeten toobe uitgevoerd op de actieve controller Hallo Hallo-apparaat.** menu van de seriële console Hallo geeft Hallo controllerstatus in de banner het Hallo-bericht. Als u niet verbonden bent wordt toohello actieve controller, verbreken en sluit vervolgens toohello actieve controller.

5. Typ uw wachtwoord bij de opdrachtprompt Hallo. Hallo standaardapparaatwachtwoord is **Wachtwoord1**.

6. Type Hallo volgende opdracht: `Invoke-HcsSetupWizard`.

7. Een setup-wizard verschijnt toohelp u Hallo netwerkinstellingen voor Hallo apparaat configureren. Geef Hallo Hallo volgende informatie:
   
   * IP-adres voor Hallo DATA 0-netwerkinterface
   * Subnetmasker
   * Gateway
   * IP-adres voor de primaire DNS-server

   Een voorbeeld van de uitvoer wordt hieronder weergegeven.

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
    In Hallo voorgaande voorbeeld van uitvoer, ziet u dat Hallo gevalideerd netwerkinstellingen na elke stap in Hallo-proces.

     > [!NOTE]
     > Mogelijk hebt u toowait voor een paar minuten voordat het Hallo-subnetmasker en Hallo DNS-instellingen toobe toegepast. Als u krijgt een foutbericht 'Selectievakje Hallo network connectivity tooData 0', controleert u Hallo fysieke netwerkverbinding voor Hallo DATA 0-netwerkinterface van uw actieve controller.

8. Configureer desgewenst uw webproxyserver. De configuratie van uw webproxy is weliswaar optioneel, maar **houd er rekening mee dat als u een webproxy gebruikt, deze alleen hier kan worden geconfigureerd**. Voor meer informatie gaat te[webproxy voor uw apparaat configureren](../articles/storsimple/storsimple-8000-configure-web-proxy.md).
9. Configureer een primaire NTP-server voor uw apparaat. NTP-servers zijn vereist, omdat uw apparaat de tijd moet synchroniseren voor verificatie met uw cloudserviceproviders. Zorg ervoor dat uw netwerk NTP-verkeer toopass van uw datacenter toohello Internet toestaat. Als dit niet mogelijk is, geeft u een interne NTP-server op.

    Hieronder ziet u een voorbeeld van de uitvoer.

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. Uit veiligheidsoverwegingen wachtwoord apparaatbeheerder Hallo na Hallo eerste sessie verlopen en moet u toochange deze nu. Als daarom wordt gevraagd, geeft u een beheerderswachtwoord voor het apparaat op. Een geldig beheerderswachtwoord voor een apparaat moet 8 tot 15 tekens bevatten. Hallo wachtwoord moet bevatten drie van de volgende Hallo: kleine letters, hoofdletters, numerieke en speciale tekens.

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. laatste stap in de wizard setup Hallo Hallo registreert uw apparaat bij Hallo StorSimple-apparaat Manager-service. Hiervoor moet u Hallo serviceregistratiesleutel die u hebt verkregen in stap 2. Nadat u de registratiesleutel Hallo opgeeft, moet u wellicht toowait 2-3 minuten voordat het Hallo-apparaat is geregistreerd.
    
    > [!NOTE]
    > U drukt op Ctrl + C op een tijd tooexit Hallo setup-wizard. Als u alle Hallo netwerkinstellingen (IP-adres voor Data 0, subnetmasker en Gateway) hebt ingevoerd, wordt uw vermeldingen behouden blijft.
    
    Hieronder ziet u een voorbeeld van de uitvoer.

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. Nadat het Hallo-apparaat is geregistreerd, weergegeven een gegevensversleutelingssleutel van Service. Kopieer deze sleutel en bewaar deze op een veilige plaats. **Deze sleutel is vereist bij het Hallo-service registratie sleutel tooregister extra apparaten Hello StorSimple-apparaat Manager-service.** Raadpleeg te[StorSimple security](../articles/storsimple/storsimple-security.md) voor meer informatie over deze sleutel.
    
    ![Apparaat 7 registreren met StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > toocopy hello tekst uit Hallo seriële console-venster, selecteert u de tekst hello. U moet kunnen toopaste in Hallo Klembord of een teksteditor. Gebruik geen Ctrl + C toocopy Hallo service gegevensversleutelingssleutel. Gebruik Ctrl + c drukken zorgt ervoor dat u tooexit Hallo installatiewizard. Als gevolg hiervan Hallo apparaat administrator-wachtwoord worden niet gewijzigd en Hallo apparaat toohello standaardwachtwoord wordt teruggezet.
    
13. Exit Hallo seriële console.
14. Retourneren van toohello Azure-portal en Voer Hallo stappen te volgen:
    
    1. Ga tooyour Apparaatbeheer StorSimple-service.
    2. Klik op **Apparaten**.
    3. Controleer in Hallo in tabelvorm lijst van apparaten, of dat Hallo apparaat verbinding heeft met toohello service door het opzoeken van Hallo status. Hallo Apparaatstatus moet **tooset gereed**.
       
        ![Pagina StorSimple-apparaten](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        Mogelijk moet u toowait voor een paar minuten voor Hallo apparaat status toochange te**tooset gereed**.
       
        Als Hallo-apparaat niet in deze lijst weergegeven wordt, moet u ervoor dat uw firewallnetwerk is geconfigureerd zoals beschreven in toomake [netwerkvereisten voor uw StorSimple-apparaat](../articles/storsimple/storsimple-8000-system-requirements.md). Controleer of poort 9354 open is voor uitgaande communicatie als dit wordt gebruikt door Hallo servicebus voor Apparaatbeheer van StorSimple-service-naar-apparaat communicatie.


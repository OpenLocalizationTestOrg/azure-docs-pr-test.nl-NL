<!--author=SharS last changed: 06/22/2016-->

### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure en registreer Hallo-apparaat
1. Toegang tot Hallo Windows PowerShell-interface op de seriële console van het StorSimple-apparaat. Zie [PuTTY gebruiken tooconnect toohello de seriële console apparaat](../articles/storsimple/storsimple-8000-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) voor instructies. **Ervoor toofollow Hallo procedure exact worden of u zich niet kunnen tooaccess Hallo-console.**
2. Hallo-sessie die wordt geopend, klikt u op **Enter** één keer tooget vanaf de opdrachtprompt.
3. U zult na vragen aan gebruiker toochoose Hallo taal dat u tooset voor uw apparaat dat wilt. Hallo taal op te geven en druk vervolgens op **Enter**.
   
    ![Apparaat 1 configureren en registreren met StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. Kies optie 1 toolog op met volledige toegang in Hallo seriële consolemenu wordt weergegeven.
   
    ![Apparaat 2 registreren met StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. Volgende stappen tooconfigure Hallo minimale vereiste netwerkinstellingen voor uw apparaat Hallo uitvoeren.
   
   > [!IMPORTANT]
   > Deze configuratiestappen moeten toobe uitgevoerd op de actieve controller Hallo Hallo-apparaat. menu van de seriële console Hallo geeft Hallo controllerstatus in de banner het Hallo-bericht. Als u geen verbinding maken met actieve controller toohello, verbreken en maak verbinding toohello actieve controller.
   
   1. Typ uw wachtwoord bij de opdrachtprompt Hallo. Hallo standaardapparaatwachtwoord is **Wachtwoord1**.
   2. Type Hallo volgende opdracht:
      
        `Invoke-HcsSetupWizard`
   3. Een setup-wizard verschijnt toohelp u Hallo netwerkinstellingen voor Hallo apparaat configureren. Geef Hallo volgende informatie:
      
      * IP-adres voor DATA 0-netwerkinterface
      * Subnetmasker
      * Gateway
      * IP-adres voor de primaire DNS-server
      * IP-adres voor de primaire NTP-server
      
      > [!NOTE]
      > Mogelijk hebt u toowait voor een paar minuten voordat het Hallo-subnetmasker en DNS-instellingen toobe toegepast.
    
   4. Configureer desgewenst uw webproxyserver.
      
      > [!IMPORTANT]
      > Hoewel webproxyconfiguratie optioneel is, worden op de hoogte gebracht als u een webproxy gebruikt, u alleen deze hier configureren kunt. Voor meer informatie gaat te[webproxy voor uw apparaat configureren](../articles/storsimple/storsimple-configure-web-proxy.md).
     
6. Druk op Ctrl + C tooexit Hallo-installatiewizard.
8. Hallo cmdlet toopoint Hallo apparaat toohello Microsoft Azure Government portal volgen (omdat deze toohello openbare klassieke Azure-portal standaard verwijst) worden uitgevoerd. Dit wordt opnieuw opgestart beide domeincontrollers. Het is raadzaam dat u twee PuTTY sessies toosimultaneously verbinding tooboth domeincontrollers, zodat u kunt zien als elke domeincontroller opnieuw wordt gestart.
   
    `Set-CloudPlatform -AzureGovt_US`
   
   Hier ziet u een bevestigingsbericht. Accepteer de standaardinstelling hello (**Y**).
9. Hallo na de installatie van cmdlet tooresume uitvoeren:
   
    `Invoke-HcsSetupWizard`
   
    ![De wizard setup hervatten](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
10. Hallo-netwerkinstellingen accepteren. U ziet een validatiebericht nadat u elke instelling hebt geaccepteerd.
11. Uit veiligheidsoverwegingen wachtwoord apparaatbeheerder Hallo na Hallo eerste sessie verlopen en moet u toochange deze nu. Als daarom wordt gevraagd, geeft u een beheerderswachtwoord voor het apparaat op. Een geldig beheerderswachtwoord voor een apparaat moet 8 tot 15 tekens bevatten. Hallo wachtwoord moet bevatten drie van de volgende Hallo: kleine letters, hoofdletters, numerieke en speciale tekens.
    
    <br/>![Apparaat 5 registreren met StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. laatste stap in de wizard setup Hallo Hallo registreert uw apparaat bij Hallo StorSimple-apparaat Manager-service. Hiervoor u serviceregistratiesleutel die u hebt verkregen in moet Hallo [stap 2: Get Hallo serviceregistratiesleutel](../articles/storsimple/storsimple-8000-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key). Nadat u de registratiesleutel Hallo opgeeft, moet u wellicht toowait 2-3 minuten voordat het Hallo-apparaat is geregistreerd.
    
    > [!NOTE]
    > U drukt op Ctrl + C op een tijd tooexit Hallo setup-wizard. Als u alle Hallo netwerkinstellingen (IP-adres voor Data 0, subnetmasker en Gateway) hebt ingevoerd, wordt uw vermeldingen behouden blijft.
    
    ![Voortgang van de StorSimple-registratie](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. Nadat het Hallo-apparaat is geregistreerd, weergegeven een gegevensversleutelingssleutel van Service. Kopieer deze sleutel en bewaar deze op een veilige plaats. **Deze sleutel is vereist bij het Hallo-service registratie sleutel tooregister extra apparaten Hello StorSimple-apparaat Manager-service.** Raadpleeg te[StorSimple security](../articles/storsimple/storsimple-8000-security.md) voor meer informatie over deze sleutel.
    
    ![Apparaat 7 registreren met StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)
    > [!IMPORTANT]
    > toocopy hello tekst uit Hallo seriële console-venster, selecteert u de tekst hello. U moet kunnen toopaste in Hallo Klembord of een teksteditor.
    > 
    > Gebruik geen **Ctrl + c drukken** toocopy Hallo service gegevensversleutelingssleutel. Met behulp van **Ctrl + c drukken** veroorzaken tooexit Hallo-installatiewizard. Als gevolg hiervan Hallo apparaat administrator-wachtwoord worden niet gewijzigd en Hallo apparaat toohello standaardwachtwoord wordt teruggezet.
    
14. Exit Hallo seriële console.
15. Toohello Azure Government Portal terug en Voer Hallo stappen te volgen:
    
    1. Ga tooyour Apparaatbeheer StorSimple-service.
    2. Klik op **Apparaten**. Identificeren van de lijst met apparaten Hallo Hallo-apparaat dat u ddeploying bent. Controleer of dat het Hallo-apparaat verbinding heeft met toohello service door het opzoeken van Hallo status. Hallo Apparaatstatus moet **Online**.
            
        Als de apparaatstatus Hallo **Offline**, wacht een paar minuten voor Hallo apparaat toocome online.
       
        Als Hallo apparaat na een paar minuten nog steeds offline is, moet u ervoor dat uw firewallnetwerk is geconfigureerd zoals beschreven in toomake [netwerkvereisten voor uw StorSimple-apparaat](../articles/storsimple/storsimple-8000-system-requirements.md).
       
        Controleer of poort 9354 open is voor uitgaande communicatie als dit wordt gebruikt door Hallo servicebus voor Apparaatbeheer van StorSimple-Service-naar-apparaat communicatie.


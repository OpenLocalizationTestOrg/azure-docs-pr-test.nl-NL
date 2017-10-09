<!--author=SharS last changed: 12/01/15-->

### <a name="step-1-authorize-a-device-toochange-hello-service-data-encryption-key-in-hello-azure-classic-portal"></a>Stap 1: Machtig een apparaat toochange Hallo service gegevensversleutelingssleutel in Hallo klassieke Azure-portal
Hallo apparaatbeheerder wordt normaal gesproken aanvragen die service Hallo beheerder een apparaat toochange service gegevensversleutelingssleutels autoriseren. Hallo-servicebeheerder machtigen vervolgens toochange Hallo-Hallo apparaatsleutel.

Deze stap wordt uitgevoerd in Hallo klassieke Azure-portal. Hallo-servicebeheerder kunt u een apparaat selecteren uit een lijst weergegeven van Hallo-apparaten die in aanmerking komende toobe gemachtigd zijn. Hallo-apparaat is geautoriseerde toostart Hallo service gegevensversleutelingssleutel Wijzig proces.

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Welke apparaten kunnen worden geautoriseerd toochange service gegevensversleutelingssleutels?
Een apparaat moet voldoen aan de criteria na kan pas geautoriseerde tooinitiate service encryption key gegevenswijzigingen worden Hallo:

* Hallo-apparaat moet online toobe in aanmerking komen voor service data encryption wijziging autorisatie.
* U kunt autoriseren hello hetzelfde apparaat opnieuw na 30 minuten als Hallo sleutel wijzigen is niet geïnitieerd.
* U kunt een ander apparaat autoriseren mits Hallo wijziging is niet geïnitieerd door Hallo eerder gemachtigd apparaat. Nadat het nieuwe apparaat Hallo is verleend, kan Hallo oude apparaat Hallo wijziging niet starten.
* U kunt een apparaat kan niet machtigen terwijl Hallo rollover van de gegevensversleutelingssleutel van Hallo-service uitgevoerd wordt.
* Wanneer u enkele Hallo-apparaten die zijn geregistreerd bij service Hallo hebben deze over Hallo versleuteling terwijl andere gebruikers niet hebben, kunt u een apparaat autoriseren. In dergelijke gevallen zijn apparaten die in aanmerking Hallo Hallo die Hallo service encryption key gegevenswijziging hebt voltooid.

> [!NOTE]
> In de klassieke Azure-portal hello gemachtigd StorSimple virtuele apparaten worden niet weergegeven in het Hallo-lijst met apparaten die kunnen worden toostart Hallo sleutel wijzigen.
> 
> 

Volgende stappen tooselect Hallo uitvoeren en autoriseren van apparaat tooinitiate Hallo service encryption key gewijzigde gegevens.

#### <a name="tooauthorize-a-device-toochange-hello-key"></a>de sleutel van een apparaat toochange hello tooauthorize
1. Klik op service dashboardpagina Hallo **wijziging service gegevensversleutelingssleutel**.
   
    ![Versleutelingssleutel voor service wijzigen](./media/storsimple-change-data-encryption-key/HCS_ChangeServiceDataEncryptionKey-include.png)
2. In Hallo **wijziging service gegevensversleutelingssleutel** dialoogvenster vak en selecteer een apparaat tooinitiate Hallo service gegevens versleuteling belangrijke wijziging autoriseren. de vervolgkeuzelijst Hallo heeft alle Hallo verkiesbare apparaten dat kunnen worden geautoriseerd.
3. Klik op het vinkje Hallo ![vinkje](./media/storsimple-change-data-encryption-key/HCS_CheckIcon-include.png).

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>Stap 2: Gebruik Windows PowerShell voor StorSimple tooinitiate Hallo service gegevens encryption key wijzigen
Deze stap wordt uitgevoerd in Hallo Windows PowerShell voor StorSimple-interface op Hallo geautoriseerd StorSimple-apparaat.

> [!NOTE]
> Er zijn geen bewerkingen kunnen worden uitgevoerd in de klassieke Azure-portal van uw StorSimple Manager-service Hallo totdat Hallo sleutelrollover is voltooid.
> 
> 

Als u Hallo apparaat seriële console tooconnect toohello Windows PowerShell-interface gebruikt, voert u Hallo stappen te volgen.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>gegevensversleutelingssleutel van tooinitiate Hallo service wijzigen
1. Selecteer optie 1 toolog op met volledige toegang.
2. Typ het volgende achter de opdrachtprompt Hallo:
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Nadat het Hallo-cmdlet is voltooid, ontvangt u een nieuwe versleutelingssleutel van de service-gegevens. Kopieer en sla deze sleutel voor gebruik in stap 3 van dit proces. Deze sleutel worden gebruikt tooupdate alle Hallo resterende apparaten die zijn geregistreerd met Hallo StorSimple Manager-service.
   
   > [!NOTE]
   > Dit proces moet worden gestart binnen vier uur na het autoriseren van een StorSimple-apparaat.
   > 
   > 
   
   Deze nieuwe sleutel wordt toohello service toobe gepusht tooall Hallo apparaten die zijn geregistreerd met de Hallo service verzonden. Een waarschuwing wordt vervolgens weergegeven op het servicedashboard Hallo. Hallo-service wordt alle Hallo-bewerkingen op Hallo ingeschreven apparaten uitschakelen en Hallo apparaatbeheerder moet vervolgens tooupdate Hallo service gegevensversleutelingssleutel op Hallo andere apparaten. Echter worden hello i/o's (hosts verzenden gegevens toohello cloud) niet verstoord.
   
   Als u één apparaat geregistreerd tooyour service Hallo rollover-proces is voltooid en kunt u de volgende stap Hallo overslaan. Als u meerdere apparaten geregistreerde tooyour service hebt, gaat u verder toostep 3.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>Stap 3: Bijwerken Hallo gegevensversleutelingssleutel van service op andere StorSimple-apparaten
Deze stappen moeten worden uitgevoerd in Windows PowerShell-interface Hallo van uw StorSimple-apparaat als er meerdere apparaten geregistreerde tooyour StorSimple Manager-service. Hallo-sleutel die u hebt verkregen in stap 2: gebruik Windows PowerShell voor StorSimple tooinitiate Hallo gegevens versleuteling belangrijke wijziging van het gebruikte tooupdate alle Hallo resterende StorSimple-apparaat is geregistreerd bij Hallo StorSimple Manager-service moet zijn.

Hallo gegevensversleuteling voor stappen tooupdate Hallo-service op het apparaat na uitvoeren.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>gegevensversleutelingssleutel van tooupdate Hallo-service
1. Windows PowerShell voor StorSimple tooconnect toohello console gebruiken. Selecteer optie 1 toolog op met volledige toegang.
2. Typ het volgende achter de opdrachtprompt Hallo:
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Hallo-service gegevensversleutelingssleutel die u hebt verkregen in bieden [stap 2: gebruik Windows PowerShell voor StorSimple tooinitiate Hallo service encryption key gegevenswijziging](#to-initiate-the-service-data-encryption-key-change).


> [!div class="op_single_selector"]
> * [C op Windows](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [C op Linux](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [Node.js](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a>Overzicht van scenario's
In dit scenario die u maakt een apparaat dat verzendt telemetrie toohello externe controle te volgen Hallo [vooraf geconfigureerde oplossing][lnk-what-are-preconfig-solutions]:

* Externe temperatuur
* Interne temperatuur
* Vochtigheid

Eenvoud, Hallo-code op Hallo apparaat genereert voorbeeldwaarden, maar we raden u tooextend Hallo voorbeeld door de echte sensoren tooyour apparaat verbinding te maken en verzenden van telemetrie echte.

Hallo-apparaat is ook kunnen toorespond toomethods aangeroepen vanuit het dashboard van de oplossing Hallo en eigenschapswaarden ingesteld in het dashboard van de oplossing Hallo gewenst.

toocomplete in deze zelfstudie, moet u een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure][lnk-free-trial] voor meer informatie.

## <a name="before-you-start"></a>Voordat u begint
Voordat u code voor het apparaat gaat schrijven, moet u de vooraf geconfigureerde oplossing voor externe controle inrichten en een nieuw aangepast apparaat in die oplossing inrichten.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>De vooraf geconfigureerde oplossing voor externe controle inrichten
Hallo-apparaat in deze zelfstudie hebt u verzendt gegevens tooan exemplaar van Hallo [externe controle] [ lnk-remote-monitoring] vooraf geconfigureerde oplossing. Als u al vooraf geconfigureerde oplossing in uw Azure-account voor externe controle Hallo nog niet hebt ingericht, gebruikt u Hallo stappen te volgen:

1. Op Hallo <https://www.azureiotsuite.com/> pagina, klikt u op  **+**  toocreate een oplossing.
2. Klik op **Selecteer** op Hallo **externe controle** toocreate van uw oplossing het deelvenster.
3. Op Hallo **maken oplossing voor externe controle** pagina, voert u een **oplossingsnaam** van uw keuze, selecteer Hallo **regio** u wilt toodeploy naar en selecteer hello Azure abonnement toowant toouse. Klik vervolgens op **Oplossing maken**.
4. Wacht totdat het Hallo inrichtingsproces is voltooid.

> [!WARNING]
> Hallo vooraf geconfigureerde oplossingen gebruiken factureerbare Azure-services. Zorg ervoor dat tooremove Hallo vooraf geconfigureerde oplossing van uw abonnement wanneer u klaar bent met het tooavoid eventuele onnodige kosten. U kunt een vooraf geconfigureerde oplossing volledig verwijderen uit uw abonnement via Hallo <https://www.azureiotsuite.com/> pagina.
> 
> 

Wanneer Hallo proces voor het Hallo-oplossing voor externe controle inrichten is voltooid, klikt u op **starten** tooopen Hallo dashboard van de oplossing in uw browser.

![Dashboard van de oplossing][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>Uw apparaat bij Hallo oplossing voor externe controle inrichten
> [!NOTE]
> Als u al een apparaat in uw oplossing hebt ingericht, kunt u deze stap overslaan. Bij het maken van de client-toepassing hello moet u tooknow Hallo apparaat referenties.
> 
> 

Voor een apparaat tooconnect toohello vooraf geconfigureerde oplossing, deze moet zelfidentificatie tooIoT Hub met geldige referenties. U kunt Hallo apparaat referenties ophalen uit Hallo oplossing dashboard. Hallo apparaat referenties in uw clienttoepassing verderop in deze zelfstudie te nemen.

de oplossing voor externe controle van een apparaat-tooyour tooadd, volledige hello te volgen stappen in Hallo oplossing dashboard:

1. In Hallo linkerbenedenhoek van Hallo dashboard, klikt u op **een apparaat toevoegt**.
   
   ![Een apparaat toevoegen][1]
2. In Hallo **aangepast apparaat** -scherm, klikt u op **nieuwe toevoegen**.
   
   ![Een aangepast apparaat toevoegen][2]
3. Kies **Laat mij mijn eigen apparaat-id definiëren**. Voer een apparaat-ID zoals **mydevice**, klikt u op **cheque-ID** tooverify die naam niet al in gebruik en klik vervolgens op **maken** tooprovision Hallo apparaat.
   
   ![Apparaat-id toevoegen][3]
4. Een opmerking Hallo-apparaat referenties (apparaat-ID, hostnaam van de IoT-Hub en apparaatsleutel) maken. De clienttoepassing moet deze waarden tooconnect toohello oplossing voor externe controle. Klik vervolgens op **Gereed**.
   
    ![Apparaatreferenties weergeven][4]
5. Selecteer uw apparaat in de lijst met apparaten in het dashboard van de oplossing Hallo Hallo. Klik op Hallo **Apparaatdetails** -scherm, klikt u op **apparaat inschakelen**. Hallo-status van uw apparaat is nu **met**. Hallo-oplossing voor externe controle kan nu telemetrie van uw apparaat wordt ontvangen en methoden niet aanroepen voor het Hallo-apparaat.

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
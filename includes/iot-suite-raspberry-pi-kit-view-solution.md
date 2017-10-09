## <a name="view-hello-solution-dashboard"></a>Dashboard van oplossing Hallo weergeven

Hallo oplossing dashboard kunt u toomanage Hallo geïmplementeerd oplossing. U kunt bijvoorbeeld telemetrie weergeven, apparaten toevoegen en methoden aanroepen.

1. Wanneer Hallo inrichten is voltooid en Hallo tegel voor uw vooraf geconfigureerde oplossing geeft **gereed**, kies **starten** tooopen uw externe controle portal van de oplossing in een nieuw tabblad.

    ![Hallo vooraf geconfigureerde oplossing starten][img-launch-solution]

1. Standaard ziet u de oplossingsportal Hallo Hallo *dashboard*. U kunt tooother gebieden van de portal van de oplossing Hallo Hallo menu aan de linkerkant Hallo van Hallo pagina met navigeren.

    ![Vooraf geconfigureerd oplossingsdashboard voor externe controle][img-menu]

## <a name="add-a-device"></a>Een apparaat toevoegen

Voor een apparaat tooconnect toohello vooraf geconfigureerde oplossing, deze moet zelfidentificatie tooIoT Hub met geldige referenties. U kunt Hallo apparaat referenties ophalen uit Hallo oplossing dashboard. Hallo apparaat referenties in uw clienttoepassing verderop in deze zelfstudie te nemen.

Als u dit nog niet hebt gedaan, voegt u de oplossing voor externe controle van een aangepast apparaat-tooyour. Voltooi de stappen te volgen in het dashboard van de oplossing Hallo Hallo:

1. In Hallo linkerbenedenhoek van Hallo dashboard, klikt u op **een apparaat toevoegt**.

   ![Een apparaat toevoegen][1]

1. In Hallo **aangepast apparaat** -scherm, klikt u op **nieuwe toevoegen**.

   ![Een aangepast apparaat toevoegen][2]

1. Kies **Laat mij mijn eigen apparaat-id definiëren**. Voer een apparaat-ID zoals **rasppi**, klikt u op **cheque-ID** tooverify u dit nog niet hebt Hallo naam al gebruikt in uw oplossing en klik vervolgens op **maken** tooprovision Hallo apparaat.

   ![Apparaat-id toevoegen][3]

1. Referenties voor een apparaat van de Hallo notitie maken (**apparaat-ID**, **IoT Hub-hostnaam**, en **apparaatsleutel**). Uw clienttoepassing op Hallo frambozen Pi moet deze waarden tooconnect toohello oplossing voor externe controle. Klik vervolgens op **Gereed**.

    ![Apparaatreferenties weergeven][4]

1. Selecteer uw apparaat in de lijst met apparaten in het dashboard van de oplossing Hallo Hallo. Klik op Hallo **Apparaatdetails** -scherm, klikt u op **apparaat inschakelen**. Hallo-status van uw apparaat is nu **met**. Hallo-oplossing voor externe controle kan nu telemetrie van uw apparaat wordt ontvangen en methoden niet aanroepen voor het Hallo-apparaat.

[img-launch-solution]: media/iot-suite-raspberry-pi-kit-view-solution/launch.png
[img-menu]: media/iot-suite-raspberry-pi-kit-view-solution/menu.png
[1]: media/iot-suite-raspberry-pi-kit-view-solution/suite0.png
[2]: media/iot-suite-raspberry-pi-kit-view-solution/suite1.png
[3]: media/iot-suite-raspberry-pi-kit-view-solution/suite2.png
[4]: media/iot-suite-raspberry-pi-kit-view-solution/suite3.png
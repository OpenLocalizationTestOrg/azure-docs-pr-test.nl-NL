## <a name="view-device-telemetry-in-hello-dashboard"></a>De apparaattelemetrie weergave in Hallo-dashboard
Hallo-dashboard in Hallo voor externe controle oplossing kunt u tooview Hallo telemetrie uw apparaten verzenden tooIoT Hub.

1. In uw browser return toohello dashboard externe controle-oplossing, klikt u op **apparaten** in Hallo links Configuratiescherm toonavigate toohello **lijst met apparaten**.
2. In Hallo **lijst met apparaten**, ziet u dat Hallo status van uw apparaat is **met**. Als dit niet het geval is, klikt u op **apparaat inschakelen** in Hallo **Apparaatdetails** Configuratiescherm.
   
    ![Apparaatstatus weergeven][18]
3. Klik op **Dashboard** tooreturn toohello dashboard, selecteert u uw apparaat in Hallo **apparaat tooView** vervolgkeuzelijst tooview de telemetrie. Hallo telemetrie uit de voorbeeldtoepassing Hallo is 50 eenheden voor interne temperatuur, 55 eenheden voor de externe temperatuur en 50 eenheden voor vochtigheid.
   
    ![Telemetrie van apparaten weergeven][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a>Een methode op het apparaat aanroepen
Hallo-dashboard in Hallo-oplossing voor externe controle kunt u tooinvoke methoden op uw apparaten via IoT Hub. U kunt bijvoorbeeld een methode toosimulate opnieuw wordt opgestart nadat een apparaat aanroepen in Hallo oplossing voor externe controle.

1. In Hallo dashboard externe controle-oplossing, klikt u op **apparaten** in Hallo links Configuratiescherm toonavigate toohello **lijst met apparaten**.
2. Klik op **apparaat-ID** voor uw apparaat in Hallo **lijst met apparaten**.
3. In Hallo **Apparaatdetails** -scherm, klikt u op **methoden**.
   
    ![Apparaatmethoden][13]
4. In Hallo **methode** vervolgkeuzelijst, selecteer **InitiateFirmwareUpdate**, en klik vervolgens in **FWPACKAGEURI** een dummy-URL opgeven. Klik op **methode Invoke** toocall Hallo methode op Hallo-apparaat.
   
    ![Een apparaatmethode aanroepen][14]
   

5. U ziet een bericht in de apparaatcode van uw wordt uitgevoerd als Hallo apparaat Hallo methode verwerkt Hallo-console. Hallo-resultaten van Hallo-methode worden toohello geschiedenis in de oplossingsportal Hallo toegevoegd:

    ![Geschiedenis van methoden weergeven][img-method-history]

## <a name="next-steps"></a>Volgende stappen
Hallo artikel [aanpassen vooraf geconfigureerde oplossingen] [ lnk-customize] beschrijft enkele manieren waarop u dit voorbeeld kunt uitbreiden. Mogelijke uitbreidingen zijn het gebruik van echte sensoren en de implementatie van aanvullende opdrachten.

U kunt meer informatie over Hallo [machtigingen op Hallo azureiotsuite.com site][lnk-permissions].

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md

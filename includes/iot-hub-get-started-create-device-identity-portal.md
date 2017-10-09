## <a name="create-a-device-identity"></a>Een apparaat-id maken

In deze sectie gebruikt u Hallo [Azure-portal] [ lnk-azure-portal] toocreate een apparaat-id in Hallo identiteitenregister van uw IoT-hub. Een apparaat kan geen verbinding tooIoT hub maken, tenzij er een vermelding in het identiteitenregister Hallo. Zie voor meer informatie, Hallo 'Identiteitsregister' sectie Hallo [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity]. Hallo **apparaat Explorer** in Hallo portal kunt u een unieke apparaat-ID en sleutel dat uw apparaat tooidentify zelf gebruiken kunt wanneer verbinding wordt gemaakt van tooIoT Hub genereren. Apparaat-id's zijn hoofdlettergevoelig.

1. Zorg ervoor dat u bent aangemeld met toohello [Azure-portal][lnk-azure-portal].

1. Klik in de Snelbalk hello, **alle resources** en uw IoT hub bron vinden.

    ![Navigeer tooyour Iot-hub][img-find-iothub]

1. Wanneer uw IoT hub resource wordt geopend, klikt u op Hallo **apparaat Explorer** hulpprogramma en klik vervolgens op **toevoegen** Hallo bovenaan. Geef de naam Hallo voor het nieuwe apparaat, zoals **myDeviceId**, en klik op **opslaan**.

    ![Apparaat-id in de portal maken][img-create-device]

   Hiermee maakt u een nieuw apparaat-id voor uw iothub.

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. In Hallo **apparaat Explorer**van lijst met apparaten, klikt u op Hallo van een nieuw gemaakt apparaat en noteer Hallo **verbindingsreeks---primaire sleutel**. 

    ![Apparaat-verbindingsreeks][img-connection-string]

> [!NOTE]
> Hallo id-register IoT Hub bewaart alleen apparaat-id's tooenable veilige toegang toohello IoT-hub. Apparaat-id's en sleutels toouse worden opgeslagen als beveiligingsreferenties en waarmee u toodisable toegang tot een afzonderlijk apparaat kunt vlag voor ingeschakeld/uitgeschakeld. Als uw toepassing toostore andere apparaatspecifieke metagegevens moet, moet deze een toepassingsspecifieke opslagmethode gebruiken. Zie de [ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity] voor meer informatie.

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md


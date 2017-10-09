## <a name="create-a-device-identity"></a>Een apparaat-id maken

In deze sectie gebruikt u een Node.js-hulpprogramma aangeroepen [iothub explorer] [ iot-hub-explorer] toocreate een apparaat-id voor deze zelfstudie. Apparaat-id's zijn hoofdlettergevoelig.

1. Voer Hallo volgende in uw omgeving opdrachtregel:

    `npm install -g iothub-explorer@latest`

1. Voer vervolgens de volgende opdracht toologin tooyour hub Hallo. Vervang `{iot hub connection string}` Hello IoT Hub-verbindingsreeks die u eerder hebt gekopieerd:

    `iothub-explorer login "{iot hub connection string}"`

1. Maak ten slotte een nieuw apparaat-id genoemd `myDeviceId` met Hallo-opdracht:

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

Noteer Hallo apparaat verbindingsreeks uit het Hallo-resultaat. Deze verbindingsreeks van het apparaat wordt gebruikt door Hallo apparaat app tooconnect tooyour IoT-Hub als een apparaat.

![][img-identity]

Raadpleeg te[aan de slag met IoT Hub] [ lnk-getstarted] tooprogrammatically apparaat-id's maken.

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md

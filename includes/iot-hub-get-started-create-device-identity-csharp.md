## <a name="create-a-device-identity"></a>Een apparaat-id maken
In deze sectie maakt maken u een .NET-consoletoepassing die een apparaat-id in Hallo identiteitenregister van uw IoT-hub maakt. Een apparaat kan geen verbinding tooIoT hub maken, tenzij er een vermelding in het identiteitenregister Hallo. Zie voor meer informatie, Hallo 'Identiteitsregister' sectie Hallo [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity]. Wanneer u deze consoletoepassing uitvoert, wordt een unieke apparaat-ID gegenereerd en sleutel waarmee het apparaat tooidentify zelf kunt wanneer het apparaat-naar-cloud verzendt berichten tooIoT Hub. Apparaat-id's zijn hoofdlettergevoelig.

1. Voeg in Visual Studio een nieuwe oplossing voor Visual C# Classic Windows Desktop-project tooa met behulp van Hallo **Console-App (.NET Framework)** projectsjabloon. Zorg ervoor dat .NET Framework-versie Hallo 4.5.1 of later. Naam Hallo project **CreateDeviceIdentity** en naam Hallo oplossing **IoTHubGetStarted**.
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][10]
2. Klik in Solution Explorer met de rechtermuisknop op Hallo **CreateDeviceIdentity** project en klik vervolgens op **NuGet-pakketten beheren**.
3. In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **microsoft.azure.devices**, selecteer **installeren** tooinstall Hallo **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo. Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.
   
    ![Sluit het venster Nuget Package Manager.][11]
4. Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. Hallo na toohello velden toevoegen **programma** klasse. Vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. Hallo na methode toohello toevoegen **programma** klasse:
   
        private static async Task AddDeviceAsync()
        {
            string deviceId = "myFirstDevice";
            Device device;
            try
            {
                device = await registryManager.AddDeviceAsync(new Device(deviceId));
            }
            catch (DeviceAlreadyExistsException)
            {
                device = await registryManager.GetDeviceAsync(deviceId);
            }
            Console.WriteLine("Generated device key: {0}", device.Authentication.SymmetricKey.PrimaryKey);
        }
   
    Met deze methode maakt u de apparaat-id **myFirstDevice**. (Als deze apparaat-ID wordt al in het identiteitenregister hello bestaat, Hallo code gewoon haalt de bestaande apparaatgegevens Hallo.) Hallo app geeft Hallo primaire sleutel voor die identiteit weer. U gebruikt deze sleutel in Hallo gesimuleerd apparaat app tooconnect tooyour IoT-hub.
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. Voeg regels toohello na Hallo **Main** methode:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. Deze toepassing en noteer de apparaatsleutel Hallo.
   
    ![Apparaatsleutel die is gegenereerd door de toepassing hello][12]

> [!NOTE]
> Hallo id-register IoT Hub bewaart alleen apparaat-id's tooenable veilige toegang toohello IoT-hub. Apparaat-id's en sleutels toouse worden opgeslagen als beveiligingsreferenties en waarmee u toodisable toegang tot een afzonderlijk apparaat kunt vlag voor ingeschakeld/uitgeschakeld. Als uw toepassing toostore andere apparaatspecifieke metagegevens moet, moet deze een toepassingsspecifieke opslagmethode gebruiken. Zie de [ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity] voor meer informatie.
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

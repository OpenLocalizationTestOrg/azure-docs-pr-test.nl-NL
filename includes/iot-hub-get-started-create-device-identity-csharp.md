## <a name="create-a-device-identity"></a><span data-ttu-id="aa7e1-101">Een apparaat-id maken</span><span class="sxs-lookup"><span data-stu-id="aa7e1-101">Create a device identity</span></span>
<span data-ttu-id="aa7e1-102">In deze sectie maakt maken u een .NET-consoletoepassing die een apparaat-id in Hallo identiteitenregister van uw IoT-hub maakt.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-102">In this section, you create a .NET console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="aa7e1-103">Een apparaat kan geen verbinding tooIoT hub maken, tenzij er een vermelding in het identiteitenregister Hallo.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="aa7e1-104">Zie voor meer informatie, Hallo 'Identiteitsregister' sectie Hallo [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="aa7e1-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="aa7e1-105">Wanneer u deze consoletoepassing uitvoert, wordt een unieke apparaat-ID gegenereerd en sleutel waarmee het apparaat tooidentify zelf kunt wanneer het apparaat-naar-cloud verzendt berichten tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-105">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span> <span data-ttu-id="aa7e1-106">Apparaat-id's zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="aa7e1-107">Voeg in Visual Studio een nieuwe oplossing voor Visual C# Classic Windows Desktop-project tooa met behulp van Hallo **Console-App (.NET Framework)** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-107">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="aa7e1-108">Zorg ervoor dat .NET Framework-versie Hallo 4.5.1 of later.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-108">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="aa7e1-109">Naam Hallo project **CreateDeviceIdentity** en naam Hallo oplossing **IoTHubGetStarted**.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-109">Name hello project **CreateDeviceIdentity** and name hello solution **IoTHubGetStarted**.</span></span>
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][10]
2. <span data-ttu-id="aa7e1-111">Klik in Solution Explorer met de rechtermuisknop op Hallo **CreateDeviceIdentity** project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-111">In Solution Explorer, right-click hello **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="aa7e1-112">In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **microsoft.azure.devices**, selecteer **installeren** tooinstall Hallo **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-112">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="aa7e1-113">Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-113">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Sluit het venster Nuget Package Manager.][11]
4. <span data-ttu-id="aa7e1-115">Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="aa7e1-115">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="aa7e1-116">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-116">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="aa7e1-117">Vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-117">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="aa7e1-118">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="aa7e1-118">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="aa7e1-119">Met deze methode maakt u de apparaat-id **myFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="aa7e1-120">(Als deze apparaat-ID wordt al in het identiteitenregister hello bestaat, Hallo code gewoon haalt de bestaande apparaatgegevens Hallo.) Hallo app geeft Hallo primaire sleutel voor die identiteit weer.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-120">(If that device ID already exists in hello identity registry, hello code simply retrieves hello existing device information.) hello app then displays hello primary key for that identity.</span></span> <span data-ttu-id="aa7e1-121">U gebruikt deze sleutel in Hallo gesimuleerd apparaat app tooconnect tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-121">You use this key in hello simulated device app tooconnect tooyour IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="aa7e1-122">Voeg regels toohello na Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="aa7e1-122">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="aa7e1-123">Deze toepassing en noteer de apparaatsleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-123">Run this application, and make a note of hello device key.</span></span>
   
    ![Apparaatsleutel die is gegenereerd door de toepassing hello][12]

> [!NOTE]
> <span data-ttu-id="aa7e1-125">Hallo id-register IoT Hub bewaart alleen apparaat-id's tooenable veilige toegang toohello IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-125">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="aa7e1-126">Apparaat-id's en sleutels toouse worden opgeslagen als beveiligingsreferenties en waarmee u toodisable toegang tot een afzonderlijk apparaat kunt vlag voor ingeschakeld/uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-126">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="aa7e1-127">Als uw toepassing toostore andere apparaatspecifieke metagegevens moet, moet deze een toepassingsspecifieke opslagmethode gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-127">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="aa7e1-128">Zie de [ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="aa7e1-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

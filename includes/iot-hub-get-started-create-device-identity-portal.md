## <a name="create-a-device-identity"></a><span data-ttu-id="db888-101">Een apparaat-id maken</span><span class="sxs-lookup"><span data-stu-id="db888-101">Create a device identity</span></span>

<span data-ttu-id="db888-102">In deze sectie gebruikt u de [Azure-portal] [ lnk-azure-portal] maken van een apparaat-id in het identiteitenregister van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="db888-102">In this section, you use the [Azure portal][lnk-azure-portal] to create a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="db888-103">Een apparaat kan geen verbinding maken met de IoT-hub, tenzij het vermeld staat in het id-register.</span><span class="sxs-lookup"><span data-stu-id="db888-103">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="db888-104">Zie de sectie Id-register in de [ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="db888-104">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="db888-105">De **apparaat Explorer** in de portal kunt u een unieke apparaat-ID en sleutel die uw apparaat gebruiken kunt om zichzelf te identificeren wanneer deze verbinding met IoT Hub maakt genereren.</span><span class="sxs-lookup"><span data-stu-id="db888-105">The **Device Explorer** in the portal helps you generate a unique device ID and key that your device can use to identify itself when it connects to IoT Hub.</span></span> <span data-ttu-id="db888-106">Apparaat-id's zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="db888-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="db888-107">Zorg ervoor dat u bent aangemeld bij de [Azure-portal][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="db888-107">Make sure you are signed in to the [Azure portal][lnk-azure-portal].</span></span>

1. <span data-ttu-id="db888-108">Klik in de Snelbalk op **alle resources** en uw IoT hub bron vinden.</span><span class="sxs-lookup"><span data-stu-id="db888-108">In the Jumpbar, click **All resources** and find your IoT hub resource.</span></span>

    ![Navigeer naar uw Iot-hub][img-find-iothub]

1. <span data-ttu-id="db888-110">Wanneer uw IoT hub resource wordt geopend, klikt u op de **apparaat Explorer** hulpprogramma en klik vervolgens op **toevoegen** aan de bovenkant.</span><span class="sxs-lookup"><span data-stu-id="db888-110">When your IoT hub resource is opened, click the **Device Explorer** tool, and then click **Add** at the top.</span></span> <span data-ttu-id="db888-111">Geef de naam voor het nieuwe apparaat, zoals **myDeviceId**, en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="db888-111">Provide the name for your new device, such as **myDeviceId**, and click **Save**.</span></span>

    ![Apparaat-id in de portal maken][img-create-device]

   <span data-ttu-id="db888-113">Hiermee maakt u een nieuw apparaat-id voor uw iothub.</span><span class="sxs-lookup"><span data-stu-id="db888-113">This creates a new device identity for your IoT hub.</span></span>

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. <span data-ttu-id="db888-114">In de **apparaat Explorer**van lijst met apparaten, klikt u op het nieuwe apparaat en noteer de **verbindingsreeks---primaire sleutel**.</span><span class="sxs-lookup"><span data-stu-id="db888-114">In the **Device Explorer**'s device list, click the newly created device and make note of the **Connection string---primary key**.</span></span> 

    ![Apparaat-verbindingsreeks][img-connection-string]

> [!NOTE]
> <span data-ttu-id="db888-116">In het id-register van IoT Hub worden alleen apparaat-id's opgeslagen waarmee veilig toegang tot de IoT-hub kan worden verkregen.</span><span class="sxs-lookup"><span data-stu-id="db888-116">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="db888-117">De apparaat-id’s en sleutels worden opgeslagen en gebruikt als beveiligingsreferenties. Met de vlag voor ingeschakeld/uitgeschakeld kunt u toegang tot een afzonderlijk apparaat uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="db888-117">It stores device IDs and keys to use as security credentials, and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="db888-118">Als uw toepassing andere apparaatspecifieke metagegevens moet opslaan, moet deze een toepassingsspecifieke opslagmethode gebruiken.</span><span class="sxs-lookup"><span data-stu-id="db888-118">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="db888-119">Zie de [ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="db888-119">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md


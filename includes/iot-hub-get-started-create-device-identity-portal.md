## <a name="create-a-device-identity"></a><span data-ttu-id="bfaa0-101">Een apparaat-id maken</span><span class="sxs-lookup"><span data-stu-id="bfaa0-101">Create a device identity</span></span>

<span data-ttu-id="bfaa0-102">In deze sectie gebruikt u Hallo [Azure-portal] [ lnk-azure-portal] toocreate een apparaat-id in Hallo identiteitenregister van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="bfaa0-102">In this section, you use hello [Azure portal][lnk-azure-portal] toocreate a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="bfaa0-103">Een apparaat kan geen verbinding tooIoT hub maken, tenzij er een vermelding in het identiteitenregister Hallo.</span><span class="sxs-lookup"><span data-stu-id="bfaa0-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="bfaa0-104">Zie voor meer informatie, Hallo 'Identiteitsregister' sectie Hallo [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="bfaa0-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="bfaa0-105">Hallo **apparaat Explorer** in Hallo portal kunt u een unieke apparaat-ID en sleutel dat uw apparaat tooidentify zelf gebruiken kunt wanneer verbinding wordt gemaakt van tooIoT Hub genereren.</span><span class="sxs-lookup"><span data-stu-id="bfaa0-105">hello **Device Explorer** in hello portal helps you generate a unique device ID and key that your device can use tooidentify itself when it connects tooIoT Hub.</span></span> <span data-ttu-id="bfaa0-106">Apparaat-id's zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="bfaa0-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="bfaa0-107">Zorg ervoor dat u bent aangemeld met toohello [Azure-portal][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="bfaa0-107">Make sure you are signed in toohello [Azure portal][lnk-azure-portal].</span></span>

1. <span data-ttu-id="bfaa0-108">Klik in de Snelbalk hello, **alle resources** en uw IoT hub bron vinden.</span><span class="sxs-lookup"><span data-stu-id="bfaa0-108">In hello Jumpbar, click **All resources** and find your IoT hub resource.</span></span>

    ![Navigeer tooyour Iot-hub][img-find-iothub]

1. <span data-ttu-id="bfaa0-110">Wanneer uw IoT hub resource wordt geopend, klikt u op Hallo **apparaat Explorer** hulpprogramma en klik vervolgens op **toevoegen** Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="bfaa0-110">When your IoT hub resource is opened, click hello **Device Explorer** tool, and then click **Add** at hello top.</span></span> <span data-ttu-id="bfaa0-111">Geef de naam Hallo voor het nieuwe apparaat, zoals **myDeviceId**, en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bfaa0-111">Provide hello name for your new device, such as **myDeviceId**, and click **Save**.</span></span>

    ![Apparaat-id in de portal maken][img-create-device]

   <span data-ttu-id="bfaa0-113">Hiermee maakt u een nieuw apparaat-id voor uw iothub.</span><span class="sxs-lookup"><span data-stu-id="bfaa0-113">This creates a new device identity for your IoT hub.</span></span>

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. <span data-ttu-id="bfaa0-114">In Hallo **apparaat Explorer**van lijst met apparaten, klikt u op Hallo van een nieuw gemaakt apparaat en noteer Hallo **verbindingsreeks---primaire sleutel**.</span><span class="sxs-lookup"><span data-stu-id="bfaa0-114">In hello **Device Explorer**'s device list, click hello newly created device and make note of hello **Connection string---primary key**.</span></span> 

    ![Apparaat-verbindingsreeks][img-connection-string]

> [!NOTE]
> <span data-ttu-id="bfaa0-116">Hallo id-register IoT Hub bewaart alleen apparaat-id's tooenable veilige toegang toohello IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="bfaa0-116">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="bfaa0-117">Apparaat-id's en sleutels toouse worden opgeslagen als beveiligingsreferenties en waarmee u toodisable toegang tot een afzonderlijk apparaat kunt vlag voor ingeschakeld/uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="bfaa0-117">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="bfaa0-118">Als uw toepassing toostore andere apparaatspecifieke metagegevens moet, moet deze een toepassingsspecifieke opslagmethode gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bfaa0-118">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="bfaa0-119">Zie de [ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bfaa0-119">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md


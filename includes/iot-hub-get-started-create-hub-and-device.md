## <a name="create-an-iot-hub"></a><span data-ttu-id="a4f5a-101">Een IoT Hub maken</span><span class="sxs-lookup"><span data-stu-id="a4f5a-101">Create an IoT hub</span></span>

1. <span data-ttu-id="a4f5a-102">In Hallo [Azure-portal](https://portal.azure.com/), klikt u op **nieuw** > **Internet der dingen** > **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-102">In hello [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![Maken van een IoT-hub in hello Azure-portal](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. <span data-ttu-id="a4f5a-104">In Hallo **IoT-hub** deelvenster Voer Hallo-informatie voor uw IoT-hub te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4f5a-104">In hello **IoT hub** pane, enter hello following information for your IoT hub:</span></span>

     <span data-ttu-id="a4f5a-105">**Naam**: Hallo-naam van uw IoT-hub invoeren.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-105">**Name**: Enter hello name of your IoT hub.</span></span> <span data-ttu-id="a4f5a-106">Als Hallo-naam die u invoert geldig is, wordt er een groen vinkje weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-106">If hello name you enter is valid, a green check mark appears.</span></span>

     <span data-ttu-id="a4f5a-107">**Prijs-en schaal**: Selecteer Hallo **F1 - vrije** laag.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-107">**Pricing and scale tier**: Select hello **F1 - Free** tier.</span></span> <span data-ttu-id="a4f5a-108">Deze optie is voldoende voor deze demo.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-108">This option is sufficient for this demo.</span></span> <span data-ttu-id="a4f5a-109">Zie voor meer informatie, Hallo [prijs-en schaalniveau](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="a4f5a-109">For more information, see hello [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

     <span data-ttu-id="a4f5a-110">**Resourcegroep**: een resource groep toohost Hallo iothub maken of een bestaande gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-110">**Resource group**: Create a resource group toohost hello IoT hub or use an existing one.</span></span> <span data-ttu-id="a4f5a-111">Zie voor meer informatie [gebruik resourcegroepen toomanage uw Azure-resources](../articles/azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a4f5a-111">For more information, see [Use resource groups toomanage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span></span>

     <span data-ttu-id="a4f5a-112">**Locatie**: Selecteer Hallo dichtstbijzijnde locatie tooyou waar Hallo IoT-hub is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-112">**Location**: Select hello closest location tooyou where hello IoT hub is created.</span></span>

     <span data-ttu-id="a4f5a-113">**Pincode toodashboard**: Selecteer deze optie voor eenvoudige toegang tooyour iothub uit Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-113">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Voer informatie toocreate uw IoT-hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. <span data-ttu-id="a4f5a-115">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-115">Click **Create**.</span></span> <span data-ttu-id="a4f5a-116">Uw IoT-hub kan toocreate van enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-116">Your IoT hub might take a few minutes toocreate.</span></span> <span data-ttu-id="a4f5a-117">U kunt de voortgang in Hallo bekijken **meldingen** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-117">You can see progress in hello **Notifications** pane.</span></span>

   ![Meldingen over de voortgang van uw IoT-hub bekijken](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. <span data-ttu-id="a4f5a-119">Nadat uw IoT-hub is gemaakt, klikt u erop op Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-119">After your IoT hub is created, click it on hello dashboard.</span></span> <span data-ttu-id="a4f5a-120">Maak een notitie van Hallo **hostnaam**, en klik vervolgens op **gedeeld toegangsbeleid**.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-120">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>

   ![Hallo-hostnaam van uw IoT-hub ophalen](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. <span data-ttu-id="a4f5a-122">In Hallo **gedeeld toegangsbeleid** deelvenster, klikt u op Hallo **iothubowner** beleid, en vervolgens kopiëren en maak een notitie van Hallo **verbindingsreeks** van uw iothub.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-122">In hello **Shared access policies** pane, click hello **iothubowner** policy, and then copy and make a note of hello **Connection string** of your IoT hub.</span></span> <span data-ttu-id="a4f5a-123">Zie voor meer informatie [besturingselement toegang tooIoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span><span class="sxs-lookup"><span data-stu-id="a4f5a-123">For more information, see [Control access tooIoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span></span>

> [!NOTE] 
<span data-ttu-id="a4f5a-124">U hoeft deze iothubowner-verbindingsreeks niet te installeren voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-124">You will not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="a4f5a-125">Echter, moet u mogelijk het voor een aantal Hallo-zelfstudies voor verschillende IoT-scenario's na het voltooien van deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-125">However, you may need it for some of hello tutorials on different IoT scenarios after you complete this set-up.</span></span>

   ![Uw IoT-hub-verbindingsreeks ophalen](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a><span data-ttu-id="a4f5a-127">Een apparaat in Hallo IoT-hub voor uw apparaat registreren</span><span class="sxs-lookup"><span data-stu-id="a4f5a-127">Register a device in hello IoT hub for your device</span></span>

1. <span data-ttu-id="a4f5a-128">In Hallo [Azure-portal](https://portal.azure.com/), opent u uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-128">In hello [Azure portal](https://portal.azure.com/), open your IoT hub.</span></span>

2. <span data-ttu-id="a4f5a-129">Klik op **Apparatenverkenner**.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-129">Click **Device Explorer**.</span></span>
3. <span data-ttu-id="a4f5a-130">Klik in deelvenster apparaat Explorer Hallo op **toevoegen** tooadd een apparaat tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-130">In hello Device Explorer pane, click **Add** tooadd a device tooyour IoT hub.</span></span> <span data-ttu-id="a4f5a-131">Vervolgens Hallo na:</span><span class="sxs-lookup"><span data-stu-id="a4f5a-131">Then do hello following:</span></span>

   <span data-ttu-id="a4f5a-132">**Apparaat-ID**: Hallo-ID van het nieuwe apparaat Hallo invoeren.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-132">**Device ID**: Enter hello ID of hello new device.</span></span> <span data-ttu-id="a4f5a-133">Apparaat-id's zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-133">Device IDs are case sensitive.</span></span>

   <span data-ttu-id="a4f5a-134">**Verificatietype**: selecteer **Symmetrische sleutel**.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-134">**Authentication Type**: Select **Symmetric Key**.</span></span>

   <span data-ttu-id="a4f5a-135">**Automatisch sleutels genereren**: schakel dit selectievakje in.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-135">**Auto Generate Keys**: Select this check box.</span></span>

   <span data-ttu-id="a4f5a-136">**Verbinding maken met apparaat tooIoT Hub**: klik op **inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-136">**Connect device tooIoT Hub**: Click **Enable**.</span></span>

   ![Een apparaat in Hallo Explorer van uw iothub apparaat toevoegen](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. <span data-ttu-id="a4f5a-138">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-138">Click **Save**.</span></span>
5. <span data-ttu-id="a4f5a-139">Nadat het Hallo-apparaat is gemaakt, opent u Hallo-apparaat in Hallo **apparaat Explorer** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-139">After hello device is created, open hello device in hello **Device Explorer** pane.</span></span>
6. <span data-ttu-id="a4f5a-140">Noteer de primaire sleutel Hallo van Hallo-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="a4f5a-140">Make a note of hello primary key of hello connection string.</span></span>

   ![Hallo apparaat verbindingsreeks ophalen](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)

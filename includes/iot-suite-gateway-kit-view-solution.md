## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="97286-101">Dashboard van oplossing Hallo weergeven</span><span class="sxs-lookup"><span data-stu-id="97286-101">View hello solution dashboard</span></span>

<span data-ttu-id="97286-102">Hallo oplossing dashboard kunt u toomanage Hallo geïmplementeerd oplossing.</span><span class="sxs-lookup"><span data-stu-id="97286-102">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="97286-103">U kunt bijvoorbeeld telemetrie weergeven, apparaten toevoegen en methoden aanroepen.</span><span class="sxs-lookup"><span data-stu-id="97286-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="97286-104">Wanneer Hallo inrichten is voltooid en Hallo tegel voor uw vooraf geconfigureerde oplossing geeft **gereed**, kies **starten** tooopen uw externe controle portal van de oplossing in een nieuw tabblad.</span><span class="sxs-lookup"><span data-stu-id="97286-104">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Hallo vooraf geconfigureerde oplossing starten][img-launch-solution]

1. <span data-ttu-id="97286-106">Standaard ziet u de oplossingsportal Hallo Hallo *dashboard*.</span><span class="sxs-lookup"><span data-stu-id="97286-106">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="97286-107">Navigeer tooother gebieden van de portal van de oplossing Hallo Hallo menu aan de linkerkant Hallo van Hallo pagina met.</span><span class="sxs-lookup"><span data-stu-id="97286-107">Navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Vooraf geconfigureerd oplossingsdashboard voor externe controle][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="97286-109">Een apparaat toevoegen</span><span class="sxs-lookup"><span data-stu-id="97286-109">Add a device</span></span>

<span data-ttu-id="97286-110">Voor een apparaat tooconnect toohello vooraf geconfigureerde oplossing, deze moet zelfidentificatie tooIoT Hub met geldige referenties.</span><span class="sxs-lookup"><span data-stu-id="97286-110">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="97286-111">U kunt Hallo apparaat referenties ophalen uit Hallo oplossing dashboard.</span><span class="sxs-lookup"><span data-stu-id="97286-111">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="97286-112">Hallo apparaat referenties in uw clienttoepassing verderop in deze zelfstudie te nemen.</span><span class="sxs-lookup"><span data-stu-id="97286-112">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="97286-113">de oplossing voor externe controle van een apparaat-tooyour tooadd, volledige hello te volgen stappen in Hallo oplossing dashboard:</span><span class="sxs-lookup"><span data-stu-id="97286-113">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="97286-114">In Hallo linkerbenedenhoek van Hallo dashboard, klikt u op **een apparaat toevoegt**.</span><span class="sxs-lookup"><span data-stu-id="97286-114">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>

   ![Een apparaat toevoegen][1]

1. <span data-ttu-id="97286-116">In Hallo **aangepast apparaat** -scherm, klikt u op **nieuwe toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="97286-116">In hello **Custom Device** panel, click **Add new**.</span></span>

   ![Een aangepast apparaat toevoegen][2]

1. <span data-ttu-id="97286-118">Kies **Laat mij mijn eigen apparaat-id definiëren**.</span><span class="sxs-lookup"><span data-stu-id="97286-118">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="97286-119">Voer een apparaat-ID zoals **device01**, klikt u op **cheque-ID** tooverify u dit nog niet hebt Hallo naam al gebruikt in uw oplossing en klik vervolgens op **maken** tooprovision Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="97286-119">Enter a Device ID such as **device01**, click **Check ID** tooverify you haven't already used hello name in your solution, and then click **Create** tooprovision hello device.</span></span>

   ![Apparaat-id toevoegen][3]

1. <span data-ttu-id="97286-121">Referenties voor een apparaat van de Hallo notitie maken (**apparaat-ID**, **IoT Hub-hostnaam**, en **apparaatsleutel**).</span><span class="sxs-lookup"><span data-stu-id="97286-121">Make a note hello device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="97286-122">Uw clienttoepassing op Hallo Intel NUC moet deze waarden tooconnect toohello oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="97286-122">Your client application on hello Intel NUC needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="97286-123">Klik vervolgens op **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="97286-123">Then click **Done**.</span></span>

    ![Apparaatreferenties weergeven][4]

1. <span data-ttu-id="97286-125">Selecteer uw apparaat in de lijst met apparaten in het dashboard van de oplossing Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="97286-125">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="97286-126">Klik op Hallo **Apparaatdetails** -scherm, klikt u op **apparaat inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="97286-126">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="97286-127">Hallo-status van uw apparaat is nu **met**.</span><span class="sxs-lookup"><span data-stu-id="97286-127">hello status of your device is now **Running**.</span></span> <span data-ttu-id="97286-128">Hallo-oplossing voor externe controle kan nu telemetrie van uw apparaat wordt ontvangen en methoden niet aanroepen voor het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="97286-128">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-launch-solution]: media/iot-suite-gateway-kit-view-solution/launch.png
[img-menu]: media/iot-suite-gateway-kit-view-solution/menu.png
[1]: media/iot-suite-gateway-kit-view-solution/suite0.png
[2]: media/iot-suite-gateway-kit-view-solution/suite1.png
[3]: media/iot-suite-gateway-kit-view-solution/suite2.png
[4]: media/iot-suite-gateway-kit-view-solution/suite3.png
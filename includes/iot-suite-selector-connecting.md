> [!div class="op_single_selector"]
> * [<span data-ttu-id="00d3f-101">C op Windows</span><span class="sxs-lookup"><span data-stu-id="00d3f-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="00d3f-102">C op Linux</span><span class="sxs-lookup"><span data-stu-id="00d3f-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="00d3f-103">Node.js</span><span class="sxs-lookup"><span data-stu-id="00d3f-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="00d3f-104">Overzicht van scenario's</span><span class="sxs-lookup"><span data-stu-id="00d3f-104">Scenario overview</span></span>
<span data-ttu-id="00d3f-105">In dit scenario die u maakt een apparaat dat verzendt telemetrie toohello externe controle te volgen Hallo [vooraf geconfigureerde oplossing][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="00d3f-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="00d3f-106">Externe temperatuur</span><span class="sxs-lookup"><span data-stu-id="00d3f-106">External temperature</span></span>
* <span data-ttu-id="00d3f-107">Interne temperatuur</span><span class="sxs-lookup"><span data-stu-id="00d3f-107">Internal temperature</span></span>
* <span data-ttu-id="00d3f-108">Vochtigheid</span><span class="sxs-lookup"><span data-stu-id="00d3f-108">Humidity</span></span>

<span data-ttu-id="00d3f-109">Eenvoud, Hallo-code op Hallo apparaat genereert voorbeeldwaarden, maar we raden u tooextend Hallo voorbeeld door de echte sensoren tooyour apparaat verbinding te maken en verzenden van telemetrie echte.</span><span class="sxs-lookup"><span data-stu-id="00d3f-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="00d3f-110">Hallo-apparaat is ook kunnen toorespond toomethods aangeroepen vanuit het dashboard van de oplossing Hallo en eigenschapswaarden ingesteld in het dashboard van de oplossing Hallo gewenst.</span><span class="sxs-lookup"><span data-stu-id="00d3f-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="00d3f-111">toocomplete in deze zelfstudie, moet u een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="00d3f-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="00d3f-112">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="00d3f-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="00d3f-113">Zie [Gratis proefversie van Azure][lnk-free-trial] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="00d3f-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="00d3f-114">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="00d3f-114">Before you start</span></span>
<span data-ttu-id="00d3f-115">Voordat u code voor het apparaat gaat schrijven, moet u de vooraf geconfigureerde oplossing voor externe controle inrichten en een nieuw aangepast apparaat in die oplossing inrichten.</span><span class="sxs-lookup"><span data-stu-id="00d3f-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="00d3f-116">De vooraf geconfigureerde oplossing voor externe controle inrichten</span><span class="sxs-lookup"><span data-stu-id="00d3f-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="00d3f-117">Hallo-apparaat in deze zelfstudie hebt u verzendt gegevens tooan exemplaar van Hallo [externe controle] [ lnk-remote-monitoring] vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="00d3f-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="00d3f-118">Als u al vooraf geconfigureerde oplossing in uw Azure-account voor externe controle Hallo nog niet hebt ingericht, gebruikt u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="00d3f-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="00d3f-119">Op Hallo <https://www.azureiotsuite.com/> pagina, klikt u op  **+**  toocreate een oplossing.</span><span class="sxs-lookup"><span data-stu-id="00d3f-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="00d3f-120">Klik op **Selecteer** op Hallo **externe controle** toocreate van uw oplossing het deelvenster.</span><span class="sxs-lookup"><span data-stu-id="00d3f-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="00d3f-121">Op Hallo **maken oplossing voor externe controle** pagina, voert u een **oplossingsnaam** van uw keuze, selecteer Hallo **regio** u wilt toodeploy naar en selecteer hello Azure abonnement toowant toouse.</span><span class="sxs-lookup"><span data-stu-id="00d3f-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="00d3f-122">Klik vervolgens op **Oplossing maken**.</span><span class="sxs-lookup"><span data-stu-id="00d3f-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="00d3f-123">Wacht totdat het Hallo inrichtingsproces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="00d3f-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="00d3f-124">Hallo vooraf geconfigureerde oplossingen gebruiken factureerbare Azure-services.</span><span class="sxs-lookup"><span data-stu-id="00d3f-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="00d3f-125">Zorg ervoor dat tooremove Hallo vooraf geconfigureerde oplossing van uw abonnement wanneer u klaar bent met het tooavoid eventuele onnodige kosten.</span><span class="sxs-lookup"><span data-stu-id="00d3f-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="00d3f-126">U kunt een vooraf geconfigureerde oplossing volledig verwijderen uit uw abonnement via Hallo <https://www.azureiotsuite.com/> pagina.</span><span class="sxs-lookup"><span data-stu-id="00d3f-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="00d3f-127">Wanneer Hallo proces voor het Hallo-oplossing voor externe controle inrichten is voltooid, klikt u op **starten** tooopen Hallo dashboard van de oplossing in uw browser.</span><span class="sxs-lookup"><span data-stu-id="00d3f-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Dashboard van de oplossing][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="00d3f-129">Uw apparaat bij Hallo oplossing voor externe controle inrichten</span><span class="sxs-lookup"><span data-stu-id="00d3f-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="00d3f-130">Als u al een apparaat in uw oplossing hebt ingericht, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="00d3f-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="00d3f-131">Bij het maken van de client-toepassing hello moet u tooknow Hallo apparaat referenties.</span><span class="sxs-lookup"><span data-stu-id="00d3f-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="00d3f-132">Voor een apparaat tooconnect toohello vooraf geconfigureerde oplossing, deze moet zelfidentificatie tooIoT Hub met geldige referenties.</span><span class="sxs-lookup"><span data-stu-id="00d3f-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="00d3f-133">U kunt Hallo apparaat referenties ophalen uit Hallo oplossing dashboard.</span><span class="sxs-lookup"><span data-stu-id="00d3f-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="00d3f-134">Hallo apparaat referenties in uw clienttoepassing verderop in deze zelfstudie te nemen.</span><span class="sxs-lookup"><span data-stu-id="00d3f-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="00d3f-135">de oplossing voor externe controle van een apparaat-tooyour tooadd, volledige hello te volgen stappen in Hallo oplossing dashboard:</span><span class="sxs-lookup"><span data-stu-id="00d3f-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="00d3f-136">In Hallo linkerbenedenhoek van Hallo dashboard, klikt u op **een apparaat toevoegt**.</span><span class="sxs-lookup"><span data-stu-id="00d3f-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Een apparaat toevoegen][1]
2. <span data-ttu-id="00d3f-138">In Hallo **aangepast apparaat** -scherm, klikt u op **nieuwe toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="00d3f-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Een aangepast apparaat toevoegen][2]
3. <span data-ttu-id="00d3f-140">Kies **Laat mij mijn eigen apparaat-id definiëren**.</span><span class="sxs-lookup"><span data-stu-id="00d3f-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="00d3f-141">Voer een apparaat-ID zoals **mydevice**, klikt u op **cheque-ID** tooverify die naam niet al in gebruik en klik vervolgens op **maken** tooprovision Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="00d3f-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Apparaat-id toevoegen][3]
4. <span data-ttu-id="00d3f-143">Een opmerking Hallo-apparaat referenties (apparaat-ID, hostnaam van de IoT-Hub en apparaatsleutel) maken.</span><span class="sxs-lookup"><span data-stu-id="00d3f-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="00d3f-144">De clienttoepassing moet deze waarden tooconnect toohello oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="00d3f-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="00d3f-145">Klik vervolgens op **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="00d3f-145">Then click **Done**.</span></span>
   
    ![Apparaatreferenties weergeven][4]
5. <span data-ttu-id="00d3f-147">Selecteer uw apparaat in de lijst met apparaten in het dashboard van de oplossing Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="00d3f-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="00d3f-148">Klik op Hallo **Apparaatdetails** -scherm, klikt u op **apparaat inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="00d3f-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="00d3f-149">Hallo-status van uw apparaat is nu **met**.</span><span class="sxs-lookup"><span data-stu-id="00d3f-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="00d3f-150">Hallo-oplossing voor externe controle kan nu telemetrie van uw apparaat wordt ontvangen en methoden niet aanroepen voor het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="00d3f-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
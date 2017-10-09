## <a name="view-device-telemetry-in-hello-dashboard"></a><span data-ttu-id="2ce16-101">De apparaattelemetrie weergave in Hallo-dashboard</span><span class="sxs-lookup"><span data-stu-id="2ce16-101">View device telemetry in hello dashboard</span></span>
<span data-ttu-id="2ce16-102">Hallo-dashboard in Hallo voor externe controle oplossing kunt u tooview Hallo telemetrie uw apparaten verzenden tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2ce16-102">hello dashboard in hello remote monitoring solution enables you tooview hello telemetry your devices send tooIoT Hub.</span></span>

1. <span data-ttu-id="2ce16-103">In uw browser return toohello dashboard externe controle-oplossing, klikt u op **apparaten** in Hallo links Configuratiescherm toonavigate toohello **lijst met apparaten**.</span><span class="sxs-lookup"><span data-stu-id="2ce16-103">In your browser, return toohello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="2ce16-104">In Hallo **lijst met apparaten**, ziet u dat Hallo status van uw apparaat is **met**.</span><span class="sxs-lookup"><span data-stu-id="2ce16-104">In hello **Devices list**, you should see that hello status of your device is **Running**.</span></span> <span data-ttu-id="2ce16-105">Als dit niet het geval is, klikt u op **apparaat inschakelen** in Hallo **Apparaatdetails** Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="2ce16-105">If not, click **Enable Device** in hello **Device Details** panel.</span></span>
   
    ![Apparaatstatus weergeven][18]
3. <span data-ttu-id="2ce16-107">Klik op **Dashboard** tooreturn toohello dashboard, selecteert u uw apparaat in Hallo **apparaat tooView** vervolgkeuzelijst tooview de telemetrie.</span><span class="sxs-lookup"><span data-stu-id="2ce16-107">Click **Dashboard** tooreturn toohello dashboard, select your device in hello **Device tooView** drop-down tooview its telemetry.</span></span> <span data-ttu-id="2ce16-108">Hallo telemetrie uit de voorbeeldtoepassing Hallo is 50 eenheden voor interne temperatuur, 55 eenheden voor de externe temperatuur en 50 eenheden voor vochtigheid.</span><span class="sxs-lookup"><span data-stu-id="2ce16-108">hello telemetry from hello sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![Telemetrie van apparaten weergeven][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="2ce16-110">Een methode op het apparaat aanroepen</span><span class="sxs-lookup"><span data-stu-id="2ce16-110">Invoke a method on your device</span></span>
<span data-ttu-id="2ce16-111">Hallo-dashboard in Hallo-oplossing voor externe controle kunt u tooinvoke methoden op uw apparaten via IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2ce16-111">hello dashboard in hello remote monitoring solution enables you tooinvoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="2ce16-112">U kunt bijvoorbeeld een methode toosimulate opnieuw wordt opgestart nadat een apparaat aanroepen in Hallo oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="2ce16-112">For example, in hello remote monitoring solution you can invoke a method toosimulate rebooting a device.</span></span>

1. <span data-ttu-id="2ce16-113">In Hallo dashboard externe controle-oplossing, klikt u op **apparaten** in Hallo links Configuratiescherm toonavigate toohello **lijst met apparaten**.</span><span class="sxs-lookup"><span data-stu-id="2ce16-113">In hello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="2ce16-114">Klik op **apparaat-ID** voor uw apparaat in Hallo **lijst met apparaten**.</span><span class="sxs-lookup"><span data-stu-id="2ce16-114">Click **Device ID** for your device in hello **Devices list**.</span></span>
3. <span data-ttu-id="2ce16-115">In Hallo **Apparaatdetails** -scherm, klikt u op **methoden**.</span><span class="sxs-lookup"><span data-stu-id="2ce16-115">In hello **Device details** panel, click **Methods**.</span></span>
   
    ![Apparaatmethoden][13]
4. <span data-ttu-id="2ce16-117">In Hallo **methode** vervolgkeuzelijst, selecteer **InitiateFirmwareUpdate**, en klik vervolgens in **FWPACKAGEURI** een dummy-URL opgeven.</span><span class="sxs-lookup"><span data-stu-id="2ce16-117">In hello **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="2ce16-118">Klik op **methode Invoke** toocall Hallo methode op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="2ce16-118">Click **Invoke Method** toocall hello method on hello device.</span></span>
   
    ![Een apparaatmethode aanroepen][14]
   

5. <span data-ttu-id="2ce16-120">U ziet een bericht in de apparaatcode van uw wordt uitgevoerd als Hallo apparaat Hallo methode verwerkt Hallo-console.</span><span class="sxs-lookup"><span data-stu-id="2ce16-120">You see a message in hello console running your device code when hello device handles hello method.</span></span> <span data-ttu-id="2ce16-121">Hallo-resultaten van Hallo-methode worden toohello geschiedenis in de oplossingsportal Hallo toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="2ce16-121">hello results of hello method are added toohello history in hello solution portal:</span></span>

    ![Geschiedenis van methoden weergeven][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="2ce16-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2ce16-123">Next steps</span></span>
<span data-ttu-id="2ce16-124">Hallo artikel [aanpassen vooraf geconfigureerde oplossingen] [ lnk-customize] beschrijft enkele manieren waarop u dit voorbeeld kunt uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="2ce16-124">hello article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="2ce16-125">Mogelijke uitbreidingen zijn het gebruik van echte sensoren en de implementatie van aanvullende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="2ce16-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="2ce16-126">U kunt meer informatie over Hallo [machtigingen op Hallo azureiotsuite.com site][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="2ce16-126">You can learn more about hello [permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md

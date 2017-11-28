## <a name="view-device-telemetry-in-the-dashboard"></a><span data-ttu-id="4f7af-101">Telemetrie van apparaten weergeven in het dashboard</span><span class="sxs-lookup"><span data-stu-id="4f7af-101">View device telemetry in the dashboard</span></span>
<span data-ttu-id="4f7af-102">Via het dashboard van de oplossing voor externe controle kunt u de telemetrie bekijken die uw apparaten naar IoT Hub verzenden.</span><span class="sxs-lookup"><span data-stu-id="4f7af-102">The dashboard in the remote monitoring solution enables you to view the telemetry your devices send to IoT Hub.</span></span>

1. <span data-ttu-id="4f7af-103">Ga in de browser terug naar het dashboard van de oplossing voor externe controle en klik in het linkerdeelvenster op **Apparaten** om naar de **Lijst met apparaten** te navigeren.</span><span class="sxs-lookup"><span data-stu-id="4f7af-103">In your browser, return to the remote monitoring solution dashboard, click **Devices** in the left-hand panel to navigate to the **Devices list**.</span></span>
2. <span data-ttu-id="4f7af-104">In de **Lijst met apparaten** zou de status van uw apparaat nu **Wordt uitgevoerd** moeten zijn.</span><span class="sxs-lookup"><span data-stu-id="4f7af-104">In the **Devices list**, you should see that the status of your device is **Running**.</span></span> <span data-ttu-id="4f7af-105">Als dat niet zo is, klikt u in het deelvenster **Apparaatdetails** op **Apparaat inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="4f7af-105">If not, click **Enable Device** in the **Device Details** panel.</span></span>
   
    ![Apparaatstatus weergeven][18]
3. <span data-ttu-id="4f7af-107">Klik op **Dashboard** om terug te keren naar het dashboard en selecteer het apparaat in de vervolgkeuzelijst **Weer te geven apparaat** om de telemetrie ervan weer te geven.</span><span class="sxs-lookup"><span data-stu-id="4f7af-107">Click **Dashboard** to return to the dashboard, select your device in the **Device to View** drop-down to view its telemetry.</span></span> <span data-ttu-id="4f7af-108">De telemetrie uit de voorbeeldtoepassing is 50 eenheden voor de interne temperatuur, 55 eenheden voor de externe temperatuur en 50 eenheden voor de vochtigheid.</span><span class="sxs-lookup"><span data-stu-id="4f7af-108">The telemetry from the sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![Telemetrie van apparaten weergeven][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="4f7af-110">Een methode op het apparaat aanroepen</span><span class="sxs-lookup"><span data-stu-id="4f7af-110">Invoke a method on your device</span></span>
<span data-ttu-id="4f7af-111">Via het dashboard van de oplossing voor externe controle kunt u methoden op uw apparaten aanroepen via IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4f7af-111">The dashboard in the remote monitoring solution enables you to invoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="4f7af-112">U kunt in de oplossing voor externe controle bijvoorbeeld een methode aanroepen om het opnieuw opstarten van een apparaat te simuleren.</span><span class="sxs-lookup"><span data-stu-id="4f7af-112">For example, in the remote monitoring solution you can invoke a method to simulate rebooting a device.</span></span>

1. <span data-ttu-id="4f7af-113">Klik op het dashboard van de oplossing voor externe controle in het linkerdeelvenster op **Apparaten** om naar de **Lijst met apparaten** te navigeren.</span><span class="sxs-lookup"><span data-stu-id="4f7af-113">In the remote monitoring solution dashboard, click **Devices** in the left-hand panel to navigate to the **Devices list**.</span></span>
2. <span data-ttu-id="4f7af-114">Klik in de **Lijst met apparaten** op **Apparaat-id** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="4f7af-114">Click **Device ID** for your device in the **Devices list**.</span></span>
3. <span data-ttu-id="4f7af-115">Klik in het deelvenster **Apparaatdetails** op **Methoden**.</span><span class="sxs-lookup"><span data-stu-id="4f7af-115">In the **Device details** panel, click **Methods**.</span></span>
   
    ![Apparaatmethoden][13]
4. <span data-ttu-id="4f7af-117">Selecteer in de vervolgkeuzelijst **Methode** de methode **InitiateFirmwareUpdate** en voer in **FWPACKAGEURI** een dummy URL in.</span><span class="sxs-lookup"><span data-stu-id="4f7af-117">In the **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="4f7af-118">Klik op **Methode aanroepen** om de methode op het apparaat aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="4f7af-118">Click **Invoke Method** to call the method on the device.</span></span>
   
    ![Een apparaatmethode aanroepen][14]
   

5. <span data-ttu-id="4f7af-120">In de console waarin de apparaatcode wordt uitgevoerd, wordt een bericht weergegeven wanneer het apparaat de methode afhandelt.</span><span class="sxs-lookup"><span data-stu-id="4f7af-120">You see a message in the console running your device code when the device handles the method.</span></span> <span data-ttu-id="4f7af-121">De resultaten van de methode worden toegevoegd aan de geschiedenis in de portal van de oplossing:</span><span class="sxs-lookup"><span data-stu-id="4f7af-121">The results of the method are added to the history in the solution portal:</span></span>

    ![Geschiedenis van methoden weergeven][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="4f7af-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4f7af-123">Next steps</span></span>
<span data-ttu-id="4f7af-124">In het artikel [Customizing preconfigured solutions][lnk-customize] (Vooraf geconfigureerde oplossingen aanpassen) worden enkele manieren beschreven waarop u dit voorbeeld kunt uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="4f7af-124">The article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="4f7af-125">Mogelijke uitbreidingen zijn het gebruik van echte sensoren en de implementatie van aanvullende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="4f7af-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="4f7af-126">Zie [Permissions on the azureiotsuite.com site][lnk-permissions] (Machtigingen op de site azureiotsuite.com) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4f7af-126">You can learn more about the [permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md

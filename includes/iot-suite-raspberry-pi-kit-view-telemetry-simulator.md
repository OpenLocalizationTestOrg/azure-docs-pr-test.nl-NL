## <a name="view-the-telemetry"></a><span data-ttu-id="be31f-101">De telemetrie weergeven</span><span class="sxs-lookup"><span data-stu-id="be31f-101">View the telemetry</span></span>

<span data-ttu-id="be31f-102">De Pi frambozen is nu met het verzenden van telemetrie naar de oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="be31f-102">The Raspberry Pi is now sending telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="be31f-103">U kunt de telemetrie weergeven op het dashboard van oplossing.</span><span class="sxs-lookup"><span data-stu-id="be31f-103">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="be31f-104">U kunt ook berichten verzenden naar uw Pi frambozen vanuit het dashboard van oplossing.</span><span class="sxs-lookup"><span data-stu-id="be31f-104">You can also send messages to your Raspberry Pi from the solution dashboard.</span></span>

- <span data-ttu-id="be31f-105">Ga naar het dashboard van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="be31f-105">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="be31f-106">Selecteer het apparaat in de **apparaat naar de weergave** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="be31f-106">Select your device in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="be31f-107">De telemetrie van de Pi frambozen wordt weergegeven op het dashboard.</span><span class="sxs-lookup"><span data-stu-id="be31f-107">The telemetry from the Raspberry Pi displays on the dashboard.</span></span>

![Telemetrie weergegeven van de Pi frambozen][img-telemetry-display]

## <a name="act-on-the-device"></a><span data-ttu-id="be31f-109">Reageren op het apparaat</span><span class="sxs-lookup"><span data-stu-id="be31f-109">Act on the device</span></span>

<span data-ttu-id="be31f-110">U kunt vanuit het dashboard oplossing methoden aanroepen op uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="be31f-110">From the solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="be31f-111">Wanneer de Pi frambozen verbinding met de oplossing voor externe controle, stuurt informatie over de methoden die wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="be31f-111">When the Raspberry Pi connects to the remote monitoring solution, it sends information about the methods it supports.</span></span>

- <span data-ttu-id="be31f-112">Klik in het dashboard van de oplossing op **apparaten** bezoeken de **apparaten** pagina.</span><span class="sxs-lookup"><span data-stu-id="be31f-112">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="be31f-113">Selecteer uw Raspberry Pi in de **lijst met apparaten**.</span><span class="sxs-lookup"><span data-stu-id="be31f-113">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="be31f-114">Kies vervolgens **methoden**:</span><span class="sxs-lookup"><span data-stu-id="be31f-114">Then choose **Methods**:</span></span>

    ![Lijst met apparaten in het dashboard][img-list-devices]

- <span data-ttu-id="be31f-116">Op de **methode Invoke** pagina **LightBlink** in de **methode** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="be31f-116">On the **Invoke Method** page, choose **LightBlink** in the **Method** dropdown.</span></span>

- <span data-ttu-id="be31f-117">Kies **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="be31f-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="be31f-118">De simulator een bericht in de console op de Pi frambozen afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="be31f-118">The simulator prints a message in the console on the Raspberry Pi.</span></span> <span data-ttu-id="be31f-119">De app op de Pi frambozen verzendt een bevestiging terug naar het dashboard van oplossing:</span><span class="sxs-lookup"><span data-stu-id="be31f-119">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard:</span></span>

    ![Overzicht van de methode weergeven][img-method-history]

- <span data-ttu-id="be31f-121">Kunt u de LED in- en uitschakelen met behulp van de **ChangeLightStatus** methode met een **LightStatusValue** ingesteld op **1** voor op of **0** voor uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="be31f-121">You can switch the LED on and off using the **ChangeLightStatus** method with a **LightStatusValue** set to **1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="be31f-122">Als u de oplossing voor externe controle uitgevoerd in uw Azure-account laat, wordt u gefactureerd voor de tijd die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="be31f-122">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="be31f-123">Zie voor meer informatie over het verbruik verminderen terwijl de oplossing voor externe controle wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="be31f-123">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="be31f-124">De vooraf geconfigureerde oplossing verwijderen uit uw Azure-account wanneer u klaar bent met het gebruik van maken.</span><span class="sxs-lookup"><span data-stu-id="be31f-124">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
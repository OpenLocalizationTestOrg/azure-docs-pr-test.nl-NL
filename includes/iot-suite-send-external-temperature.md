## <a name="configure-the-nodejs-simulated-device"></a><span data-ttu-id="e28db-101">Het gesimuleerde apparaat Node.js configureren</span><span class="sxs-lookup"><span data-stu-id="e28db-101">Configure the Node.js simulated device</span></span>
1. <span data-ttu-id="e28db-102">Klik op het dashboard voor externe controle **+ een apparaat toevoegt** en voeg vervolgens een *aangepast apparaat*.</span><span class="sxs-lookup"><span data-stu-id="e28db-102">On the remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="e28db-103">Noteer de IoT-Hub hostnaam, apparaat-id en apparaatsleutel.</span><span class="sxs-lookup"><span data-stu-id="e28db-103">Make a note of the IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="e28db-104">U moet deze verderop in deze zelfstudie wanneer u de clienttoepassing remote_monitoring.js-apparaat voorbereiden.</span><span class="sxs-lookup"><span data-stu-id="e28db-104">You need them later in this tutorial when you prepare the remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="e28db-105">Zorg dat Node.js-versie 0.12.x of hoger is geïnstalleerd op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="e28db-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="e28db-106">Voer `node --version` achter de opdrachtprompt of in een shell controleren de versie.</span><span class="sxs-lookup"><span data-stu-id="e28db-106">Run `node --version` at a command prompt or in a shell to check the version.</span></span> <span data-ttu-id="e28db-107">Zie voor meer informatie over het gebruik van een Pakketbeheer Node.js installeren op Linux [Node.js installeren via Pakketbeheer][node-linux].</span><span class="sxs-lookup"><span data-stu-id="e28db-107">For information about using a package manager to install Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="e28db-108">Wanneer u Node.js hebt geïnstalleerd, kloon de nieuwste versie van de [azure-iot-sdk-knooppunt] [ lnk-github-repo] opslagplaats op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="e28db-108">When you have installed Node.js, clone the latest version of the [azure-iot-sdk-node][lnk-github-repo] repository to your development machine.</span></span> <span data-ttu-id="e28db-109">Gebruik altijd de **master** vertakking voor de nieuwste versie van de bibliotheken en voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="e28db-109">Always use the **master** branch for the latest version of the libraries and samples.</span></span>
4. <span data-ttu-id="e28db-110">In uw lokale exemplaar van de [azure-iot-sdk-knooppunt] [ lnk-github-repo] -opslagplaats, de volgende twee bestanden kopiëren van de apparaat-knooppunt-voorbeelden map naar een lege map op uw ontwikkelcomputer:</span><span class="sxs-lookup"><span data-stu-id="e28db-110">From your local copy of the [azure-iot-sdk-node][lnk-github-repo] repository, copy the following two files from the node/device/samples folder to an empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="e28db-111">Packages.JSON</span><span class="sxs-lookup"><span data-stu-id="e28db-111">packages.json</span></span>
   * <span data-ttu-id="e28db-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="e28db-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="e28db-113">Open het bestand remote_monitoring.js en zoekt u naar de definitie van de volgende variabele:</span><span class="sxs-lookup"><span data-stu-id="e28db-113">Open the remote_monitoring.js file and look for the following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="e28db-114">Vervang **[IoT Hub apparaat-verbindingsreeks]** met de verbindingsreeks van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="e28db-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="e28db-115">Gebruik de waarden voor uw IoT Hub-hostnaam, het apparaat-id en de apparaatsleutel die u een genoteerd in stap 1 hebt.</span><span class="sxs-lookup"><span data-stu-id="e28db-115">Use the values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="e28db-116">Een apparaat-verbindingsreeks heeft de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="e28db-116">A device connection string has the following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="e28db-117">Als uw IoT Hub-hostnaam **contoso** en uw apparaat-id is **mydevice**, de verbindingsreeks eruit ziet het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="e28db-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like the following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Sla het bestand op. <span data-ttu-id="e28db-119">Voer de volgende opdrachten in een shell of opdrachtprompt in de map met deze bestanden voor het installeren van de vereiste pakketten en voer vervolgens de voorbeeldtoepassing:</span><span class="sxs-lookup"><span data-stu-id="e28db-119">Run the following commands in a shell or command prompt in the folder that contains these files to install the necessary packages and then run the sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="e28db-120">Houd rekening met dynamische telemetrie in actie</span><span class="sxs-lookup"><span data-stu-id="e28db-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="e28db-121">Het dashboard toont de temperatuur en vochtigheid telemetrie van de bestaande gesimuleerde apparaten:</span><span class="sxs-lookup"><span data-stu-id="e28db-121">The dashboard shows the temperature and humidity telemetry from the existing simulated devices:</span></span>

![Het standaarddashboard][image1]

<span data-ttu-id="e28db-123">Als u het Node.js gesimuleerde apparaat die u in de vorige sectie hebt uitgevoerd selecteert, ziet u temperatuur en vochtigheid externe temperatuur telemetrie:</span><span class="sxs-lookup"><span data-stu-id="e28db-123">If you select the Node.js simulated device you ran in the previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![Externe temperatuur toevoegen aan het dashboard][image2]

<span data-ttu-id="e28db-125">De oplossing voor externe controle automatisch het type van de telemetrie aanvullende externe temperatuur detecteert en voegt het toe aan de grafiek in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="e28db-125">The remote monitoring solution automatically detects the additional external temperature telemetry type and adds it to the chart on the dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png
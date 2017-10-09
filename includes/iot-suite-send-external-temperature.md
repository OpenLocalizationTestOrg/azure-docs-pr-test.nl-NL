## <a name="configure-hello-nodejs-simulated-device"></a><span data-ttu-id="41c4f-101">Hallo Node.js gesimuleerde apparaat configureren</span><span class="sxs-lookup"><span data-stu-id="41c4f-101">Configure hello Node.js simulated device</span></span>
1. <span data-ttu-id="41c4f-102">Klik op Hallo dashboard externe controle, **+ een apparaat toevoegt** en voeg vervolgens een *aangepast apparaat*.</span><span class="sxs-lookup"><span data-stu-id="41c4f-102">On hello remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="41c4f-103">Noteer Hallo IoT Hub hostnaam, apparaat-id en apparaatsleutel.</span><span class="sxs-lookup"><span data-stu-id="41c4f-103">Make a note of hello IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="41c4f-104">U moet deze verderop in deze zelfstudie als u Hallo remote_monitoring.js device-clienttoepassing voorbereiden.</span><span class="sxs-lookup"><span data-stu-id="41c4f-104">You need them later in this tutorial when you prepare hello remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="41c4f-105">Zorg dat Node.js-versie 0.12.x of hoger is geïnstalleerd op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="41c4f-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="41c4f-106">Voer `node --version` achter de opdrachtprompt of in een shell toocheck Hallo-versie.</span><span class="sxs-lookup"><span data-stu-id="41c4f-106">Run `node --version` at a command prompt or in a shell toocheck hello version.</span></span> <span data-ttu-id="41c4f-107">Zie voor meer informatie over het gebruik van een pakket manager tooinstall Node.js op Linux [Node.js installeren via Pakketbeheer][node-linux].</span><span class="sxs-lookup"><span data-stu-id="41c4f-107">For information about using a package manager tooinstall Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="41c4f-108">Wanneer u Node.js hebt geïnstalleerd, de meest recente versie Hallo Hallo klonen [azure-iot-sdk-knooppunt] [ lnk-github-repo] opslagplaats tooyour ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="41c4f-108">When you have installed Node.js, clone hello latest version of hello [azure-iot-sdk-node][lnk-github-repo] repository tooyour development machine.</span></span> <span data-ttu-id="41c4f-109">Gebruik altijd Hallo **master** vertakking voor de meest recente versie Hallo Hallo-bibliotheken en voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="41c4f-109">Always use hello **master** branch for hello latest version of hello libraries and samples.</span></span>
4. <span data-ttu-id="41c4f-110">In uw lokale exemplaar van Hallo [azure-iot-sdk-knooppunt] [ lnk-github-repo] opslagplaats, kopie Hallo volgende twee bestanden uit Hallo apparaat-knooppunt-voorbeelden tooan lege map op uw ontwikkelcomputer:</span><span class="sxs-lookup"><span data-stu-id="41c4f-110">From your local copy of hello [azure-iot-sdk-node][lnk-github-repo] repository, copy hello following two files from hello node/device/samples folder tooan empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="41c4f-111">Packages.JSON</span><span class="sxs-lookup"><span data-stu-id="41c4f-111">packages.json</span></span>
   * <span data-ttu-id="41c4f-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="41c4f-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="41c4f-113">Hallo remote_monitoring.js bestand openen en zoekt u Hallo variabeledefinitie volgt:</span><span class="sxs-lookup"><span data-stu-id="41c4f-113">Open hello remote_monitoring.js file and look for hello following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="41c4f-114">Vervang **[IoT Hub apparaat-verbindingsreeks]** met de verbindingsreeks van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="41c4f-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="41c4f-115">Hallo waarden gebruiken voor uw IoT-Hub hostnaam, het apparaat-id en de apparaatsleutel die u een genoteerd in stap 1 hebt.</span><span class="sxs-lookup"><span data-stu-id="41c4f-115">Use hello values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="41c4f-116">Een verbindingsreeks apparaat heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="41c4f-116">A device connection string has hello following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="41c4f-117">Als uw IoT Hub-hostnaam **contoso** en uw apparaat-id is **mydevice**, de verbindingsreeks ziet eruit als Hallo codefragment te volgen:</span><span class="sxs-lookup"><span data-stu-id="41c4f-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like hello following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Hallo-bestand opslaan. <span data-ttu-id="41c4f-119">Hallo volgende opdrachten in een shell of opdrachtprompt in Hallo-map met deze bestanden tooinstall hello-pakketten voor nodig zijn uitgevoerd en voer vervolgens de voorbeeldtoepassing Hallo:</span><span class="sxs-lookup"><span data-stu-id="41c4f-119">Run hello following commands in a shell or command prompt in hello folder that contains these files tooinstall hello necessary packages and then run hello sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="41c4f-120">Houd rekening met dynamische telemetrie in actie</span><span class="sxs-lookup"><span data-stu-id="41c4f-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="41c4f-121">Hallo-dashboard ziet Hallo temperatuur en vochtigheid telemetrie van Hallo bestaande gesimuleerde apparaten:</span><span class="sxs-lookup"><span data-stu-id="41c4f-121">hello dashboard shows hello temperature and humidity telemetry from hello existing simulated devices:</span></span>

![Hallo standaarddashboard][image1]

<span data-ttu-id="41c4f-123">Als u Hallo Node.js gesimuleerd apparaat die hebt uitgevoerd in de vorige sectie Hallo selecteert, ziet u temperatuur en vochtigheid externe temperatuur telemetrie:</span><span class="sxs-lookup"><span data-stu-id="41c4f-123">If you select hello Node.js simulated device you ran in hello previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![Externe temperatuur toohello dashboard toevoegen][image2]

<span data-ttu-id="41c4f-125">Hallo-oplossing voor externe controle Hallo aanvullende externe temperatuur telemetrie type detecteert automatisch en wordt toohello grafiek op Hallo dashboard toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="41c4f-125">hello remote monitoring solution automatically detects hello additional external temperature telemetry type and adds it toohello chart on hello dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png
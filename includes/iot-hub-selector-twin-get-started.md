> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9942-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="a9942-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [<span data-ttu-id="a9942-102">C#/node.js</span><span class="sxs-lookup"><span data-stu-id="a9942-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [<span data-ttu-id="a9942-103">C#</span><span class="sxs-lookup"><span data-stu-id="a9942-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [<span data-ttu-id="a9942-104">Java</span><span class="sxs-lookup"><span data-stu-id="a9942-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

<span data-ttu-id="a9942-105">Apparaatdubbels zijn JSON-documenten waarin statusinformatie van een apparaat (metagegevens, configuraties en voorwaarden) zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a9942-105">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="a9942-106">IoT Hub persistente een apparaat twin voor elk apparaat dat tooit verbindt.</span><span class="sxs-lookup"><span data-stu-id="a9942-106">IoT Hub persists a device twin for each device that connects tooit.</span></span>

<span data-ttu-id="a9942-107">Apparaat horende te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a9942-107">Use device twins to:</span></span>

* <span data-ttu-id="a9942-108">Opslaan van metagegevens van apparaten uit de back-end van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="a9942-108">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="a9942-109">Huidige statusinformatie zoals de beschikbare mogelijkheden en voorwaarden (bijvoorbeeld Hallo connectiviteit methode die wordt gebruikt) van uw app apparaat rapporteren.</span><span class="sxs-lookup"><span data-stu-id="a9942-109">Report current state information such as available capabilities and conditions (for example, hello connectivity method used) from your device app.</span></span>
* <span data-ttu-id="a9942-110">Hallo-status van langlopende werkstromen (zoals updates, firmware en configuratie) tussen een apparaat-app en een back-endserver voor apps worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="a9942-110">Synchronize hello state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="a9942-111">De metagegevens van apparaten, de configuratie of de status opvragen.</span><span class="sxs-lookup"><span data-stu-id="a9942-111">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> <span data-ttu-id="a9942-112">Apparaat horende zijn ontworpen voor synchronisatie en voor het uitvoeren van query's apparaatconfiguraties en voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="a9942-112">Device twins are designed for synchronization and for querying device configurations and conditions.</span></span> <span data-ttu-id="a9942-113">Meer informatie over op wanneer toouse apparaat horende vindt u in [apparaat horende begrijpen][lnk-twins].</span><span class="sxs-lookup"><span data-stu-id="a9942-113">More informations on when toouse device twins can be found in [Understand device twins][lnk-twins].</span></span>

<span data-ttu-id="a9942-114">Apparaat horende worden opgeslagen in een IoT-hub en bevatten:</span><span class="sxs-lookup"><span data-stu-id="a9942-114">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="a9942-115">*labels*, de metagegevens van de apparaten is alleen toegankelijk zijn voor Hallo back-end oplossing;</span><span class="sxs-lookup"><span data-stu-id="a9942-115">*tags*, device metadata accessible only by hello solution back end;</span></span>
* <span data-ttu-id="a9942-116">*Eigenschappen gewenst*, JSON-objecten die kunnen worden gewijzigd door Hallo oplossing back-end en opslagtijd met Hallo apparaattoepassing; en</span><span class="sxs-lookup"><span data-stu-id="a9942-116">*desired properties*, JSON objects modifiable by hello solution back end and observable by hello device app; and</span></span>
* <span data-ttu-id="a9942-117">*Eigenschappen gerapporteerd*, JSON-objecten kunnen worden gewijzigd door Hallo apparaattoepassing en gelezen door Hallo back-end oplossing.</span><span class="sxs-lookup"><span data-stu-id="a9942-117">*reported properties*, JSON objects modifiable by hello device app and readable by hello solution back end.</span></span> <span data-ttu-id="a9942-118">Labels en eigenschappen kunnen geen matrices bevatten, maar objecten kunnen worden genest.</span><span class="sxs-lookup"><span data-stu-id="a9942-118">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="a9942-119">Hallo back-end oplossing kan bovendien apparaat horende op basis van alle Hallo boven gegevens opvragen.</span><span class="sxs-lookup"><span data-stu-id="a9942-119">Additionally, hello solution back end can query device twins based on all hello above data.</span></span>
<span data-ttu-id="a9942-120">Raadpleeg te[horende apparaten begrijpen] [ lnk-twins] voor meer informatie over apparaat horende en toohello [IoT Hub-querytaal] [ lnk-query] verwijzing query's.</span><span class="sxs-lookup"><span data-stu-id="a9942-120">Refer too[Understand device twins][lnk-twins] for more information about device twins, and toohello [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> <span data-ttu-id="a9942-121">Op dit moment horende apparaten zijn alleen toegankelijk vanaf apparaten die verbinding tooIoT Hub maken met Hallo MQTT-protocol.</span><span class="sxs-lookup"><span data-stu-id="a9942-121">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="a9942-122">Raadpleeg toohello [MQTT ondersteuning] [ lnk-devguide-mqtt] artikel voor instructies over het tooconvert bestaande apparaat app toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="a9942-122">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>

<span data-ttu-id="a9942-123">In deze handleiding ontdekt u hoe u:</span><span class="sxs-lookup"><span data-stu-id="a9942-123">This tutorial shows you how to:</span></span>

* <span data-ttu-id="a9942-124">Maakt een back-end-app die wordt toegevoegd *labels* tooa apparaat twin en een gesimuleerde apparaattoepassing die rapporteert de connectiviteit van de channel-als een *gerapporteerd eigenschap* op Hallo apparaat twin.</span><span class="sxs-lookup"><span data-stu-id="a9942-124">Create a back-end app that adds *tags* tooa device twin, and a simulated device app that reports its connectivity channel as a *reported property* on hello device twin.</span></span>
* <span data-ttu-id="a9942-125">Query uitvoeren op apparaten van uw back-end-app met behulp van filters op Hallo-labels en eigenschappen eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a9942-125">Query devices from your back-end app using filters on hello tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md
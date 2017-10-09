> [!div class="op_single_selector"]
> * [<span data-ttu-id="0817e-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="0817e-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [<span data-ttu-id="0817e-102">C#/node.js</span><span class="sxs-lookup"><span data-stu-id="0817e-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [<span data-ttu-id="0817e-103">C#</span><span class="sxs-lookup"><span data-stu-id="0817e-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="0817e-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="0817e-104">Introduction</span></span>

<span data-ttu-id="0817e-105">In [aan de slag met IoT Hub apparaat horende][lnk-twin-tutorial], hebt u geleerd hoe tooset metagegevens voor de apparaten van uw oplossing terug eindigen met behulp van *labels*, voorwaarden apparaat vanuit een app apparaat rapporteren met behulp van *gerapporteerd eigenschappen*, en deze gegevens door middel van een SQL-achtige taal opvragen.</span><span class="sxs-lookup"><span data-stu-id="0817e-105">In [Get started with IoT Hub device twins][lnk-twin-tutorial], you learned how tooset device metadata from your solution back end using *tags*, report device conditions from a device app using *reported properties*, and query this information using a SQL-like language.</span></span>

<span data-ttu-id="0817e-106">In deze zelfstudie leert u hoe toouse Hallo Hallo apparaat twin *gewenst eigenschappen* samen met *gerapporteerd eigenschappen*, tooremotely apparaat-apps configureren.</span><span class="sxs-lookup"><span data-stu-id="0817e-106">In this tutorial, you will learn how toouse hello hello device twin's *desired properties* along with *reported properties*, tooremotely configure device apps.</span></span> <span data-ttu-id="0817e-107">Meer specifiek, deze zelfstudie laat zien hoe een apparaat-twin gerapporteerd en gewenste eigenschappen een configuratie met meerdere stappen van de apparaattoepassing van een inschakelen en bieden Hallo zichtbaarheid toohello back-end oplossing van Hallo status van deze bewerking op alle apparaten.</span><span class="sxs-lookup"><span data-stu-id="0817e-107">More specifically, this tutorial shows how a device twin's reported and desired properties enable a multi-step configuration of a device application, and provide hello visibility toohello solution back end of hello status of this operation across all devices.</span></span> <span data-ttu-id="0817e-108">U vindt meer informatie over het Hallo-rol van apparaatconfiguraties in [overzicht van Apparaatbeheer met IoT Hub][lnk-dm-overview].</span><span class="sxs-lookup"><span data-stu-id="0817e-108">You can find more information regarding hello role of device configurations in [Overview of device management with IoT Hub][lnk-dm-overview].</span></span>

<span data-ttu-id="0817e-109">Op een hoog niveau kunt apparaat horende Hallo oplossing voor back-end toospecify Hallo gewenste configuratie voor Hallo beheerde apparaten, door specifieke opdrachten te verzenden in plaats van.</span><span class="sxs-lookup"><span data-stu-id="0817e-109">At a high level, using device twins enables hello solution back end toospecify hello desired configuration for hello managed devices, instead of sending specific commands.</span></span> <span data-ttu-id="0817e-110">Dit apparaat Hallo verantwoordelijk instellen van de beste manier tooupdate Hallo configuratie ervan (zeer belangrijk in IoT-scenario's waarin specifieke apparaat voorwaarden invloed hebben op Hallo mogelijkheid tooimmediately uitvoeren door specifieke opdrachten), plaatst tijdens voortdurend reporting toohello back-end oplossing Hallo huidige status en potentiële fouten van Hallo updateproces kan controleren.</span><span class="sxs-lookup"><span data-stu-id="0817e-110">This puts hello device in charge of setting up hello best way tooupdate its configuration (very important in IoT scenarios where specific device conditions affect hello ability tooimmediately carry out specific commands), while continually reporting toohello solution back end hello current state and potential error conditions of hello update process.</span></span> <span data-ttu-id="0817e-111">Dit patroon is instrumentale toohello beheer van grote sets van apparaten, zoals Hallo oplossing voor back-end toohave volledig inzicht in de status van de configuratie van Hallo Hallo op alle apparaten kunnen.</span><span class="sxs-lookup"><span data-stu-id="0817e-111">This pattern is instrumental toohello management of large sets of devices, as it enables hello solution back end toohave full visibility of hello state of hello configuration process across all devices.</span></span>

> [!NOTE]
> <span data-ttu-id="0817e-112">In scenario's waarin apparaten worden beheerd op een nieuwe interactieve wijze (inschakelen voor een ventilator van een gebruiker beheerde app), kunt u overwegen [methoden directe][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="0817e-112">In scenarios where devices are controlled in a more interactive fashion (turn on a fan from a user-controlled app), consider using [direct methods][lnk-methods].</span></span>
> 
> 

<span data-ttu-id="0817e-113">In deze zelfstudie update Hallo oplossing voor back-end wijzigingen Hallo telemetrie configuratie van een doelapparaat en, als gevolg van die Hallo apparaattoepassing een proces met meerdere stappen tooapply een configuratie volgt (bijvoorbeeld software-module opnieuw moet worden gestart, waarvoor deze zelfstudie simuleert met een eenvoudige vertraging).</span><span class="sxs-lookup"><span data-stu-id="0817e-113">In this tutorial, hello solution back end changes hello telemetry configuration of a target device and, as a result of that, hello device app follows a multi-step process tooapply a configuration update (for example, requiring a software module restart, which this tutorial simulates with a simple delay).</span></span>

<span data-ttu-id="0817e-114">Hallo back-end oplossing slaat Hallo configuratie in de gewenste eigenschappen in de volgende manieren Hallo Hallo apparaat twin:</span><span class="sxs-lookup"><span data-stu-id="0817e-114">hello solution back end stores hello configuration in hello device twin's desired properties in hello following way:</span></span>

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> <span data-ttu-id="0817e-115">Omdat configuraties kunnen complexe objecten, worden ze meestal toegewezen unieke id's (hashes of [GUID's][lnk-guid]) toosimplify hun vergelijkingen.</span><span class="sxs-lookup"><span data-stu-id="0817e-115">Since configurations can be complex objects, they are usually assigned unique ids (hashes or [GUIDs][lnk-guid]) toosimplify their comparisons.</span></span>
> 
> 

<span data-ttu-id="0817e-116">Hallo apparaattoepassing rapporteert de huidige configuratie gewenst Hallo eigenschap spiegelen **telemetryConfig** Hallo gerapporteerd eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="0817e-116">hello device app reports its current configuration mirroring hello desired property **telemetryConfig** in hello reported properties:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

<span data-ttu-id="0817e-117">Houd er rekening mee hoe Hallo gerapporteerd **telemetryConfig** heeft een extra eigenschap **status**, tooreport Hallo status van de update configuratieproces Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0817e-117">Note how hello reported **telemetryConfig** has an additional property **status**, used tooreport hello state of hello configuration update process.</span></span>

<span data-ttu-id="0817e-118">Wanneer een nieuwe gewenste configuratie wordt ontvangen, rapporten Hallo apparaattoepassing een in behandeling configuratie door Hallo gegevens te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="0817e-118">When a new desired configuration is received, hello device app reports a pending configuration by changing hello information:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

<span data-ttu-id="0817e-119">Klik vervolgens op een later tijdstip rapporteert Hallo apparaattoepassing Hallo slagen of mislukken van deze bewerking door Hallo boven eigenschap bij te werken.</span><span class="sxs-lookup"><span data-stu-id="0817e-119">Then, at some later time, hello device app will report hello success or failure of this operation by updating hello above property.</span></span>
<span data-ttu-id="0817e-120">Houd er rekening mee hoe Hallo back-end oplossing kunnen op elk gewenst moment, tooquery Hallo status van de configuratieproces Hallo op alle Hallo-apparaten.</span><span class="sxs-lookup"><span data-stu-id="0817e-120">Note how hello solution back end is able, at any time, tooquery hello status of hello configuration process across all hello devices.</span></span>

<span data-ttu-id="0817e-121">In deze handleiding ontdekt u hoe u:</span><span class="sxs-lookup"><span data-stu-id="0817e-121">This tutorial shows you how to:</span></span>

* <span data-ttu-id="0817e-122">Maakt een gesimuleerd apparaat-app die configuratie-updates ontvangt van Hallo back-end oplossing en rapporten van meerdere updates als *eigenschappen gerapporteerd* op Hallo configuratie proces niet bijwerken.</span><span class="sxs-lookup"><span data-stu-id="0817e-122">Create a simulated device app that receives configuration updates from hello solution back end, and reports multiple updates as *reported properties* on hello configuration update process.</span></span>
* <span data-ttu-id="0817e-123">Maakt een back-end-app dat updates Hallo gewenste configuratie van een apparaat, en vervolgens query's Hallo update configuratieproces.</span><span class="sxs-lookup"><span data-stu-id="0817e-123">Create a back-end app that updates hello desired configuration of a device, and then queries hello configuration update process.</span></span>

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

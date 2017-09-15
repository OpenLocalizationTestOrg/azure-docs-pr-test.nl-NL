> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb775-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="bb775-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [<span data-ttu-id="bb775-102">C#/node.js</span><span class="sxs-lookup"><span data-stu-id="bb775-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [<span data-ttu-id="bb775-103">C#</span><span class="sxs-lookup"><span data-stu-id="bb775-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="bb775-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="bb775-104">Introduction</span></span>

<span data-ttu-id="bb775-105">In [aan de slag met IoT Hub apparaat horende][lnk-twin-tutorial], hebt u geleerd hoe u de metagegevens van apparaten instellen van uw oplossing voor back-end met *labels*, voorwaarden apparaat vanuit een app apparaat rapporteren met behulp van *gerapporteerd eigenschappen*, en deze gegevens door middel van een SQL-achtige taal opvragen.</span><span class="sxs-lookup"><span data-stu-id="bb775-105">In [Get started with IoT Hub device twins][lnk-twin-tutorial], you learned how to set device metadata from your solution back end using *tags*, report device conditions from a device app using *reported properties*, and query this information using a SQL-like language.</span></span>

<span data-ttu-id="bb775-106">In deze zelfstudie leert u hoe u de de apparaat-twin *gewenst eigenschappen* samen met *gerapporteerd eigenschappen*, apparaat-apps op afstand te configureren.</span><span class="sxs-lookup"><span data-stu-id="bb775-106">In this tutorial, you will learn how to use the the device twin's *desired properties* along with *reported properties*, to remotely configure device apps.</span></span> <span data-ttu-id="bb775-107">Meer specifiek, deze zelfstudie laat zien hoe een apparaat-twin gerapporteerd en gewenste eigenschappen een configuratie met meerdere stappen van de apparaattoepassing van een inschakelen en de zichtbaarheid van de oplossing voor back-end van de status van deze bewerking op alle apparaten opgeven.</span><span class="sxs-lookup"><span data-stu-id="bb775-107">More specifically, this tutorial shows how a device twin's reported and desired properties enable a multi-step configuration of a device application, and provide the visibility to the solution back end of the status of this operation across all devices.</span></span> <span data-ttu-id="bb775-108">U vindt meer informatie over de rol van apparaatconfiguraties in [overzicht van Apparaatbeheer met IoT Hub][lnk-dm-overview].</span><span class="sxs-lookup"><span data-stu-id="bb775-108">You can find more information regarding the role of device configurations in [Overview of device management with IoT Hub][lnk-dm-overview].</span></span>

<span data-ttu-id="bb775-109">Op een hoog niveau kunt horende apparaten het back-end oplossing om op te geven van de gewenste configuratie voor de beheerde apparaten, in plaats van door specifieke opdrachten te sturen.</span><span class="sxs-lookup"><span data-stu-id="bb775-109">At a high level, using device twins enables the solution back end to specify the desired configuration for the managed devices, instead of sending specific commands.</span></span> <span data-ttu-id="bb775-110">Hiermee wordt het apparaat voor het instellen van de beste manier om het bijwerken van de configuratie ervan (zeer belangrijk in IoT-scenario's waarin specifieke apparaat voorwaarden invloed hebben op het onmiddellijk uit te voeren door specifieke opdrachten), geplaatst tijdens voortdurend rapporteren aan de achterzijde van de oplossing Beëindig de huidige status en potentiële fouten van het updateproces.</span><span class="sxs-lookup"><span data-stu-id="bb775-110">This puts the device in charge of setting up the best way to update its configuration (very important in IoT scenarios where specific device conditions affect the ability to immediately carry out specific commands), while continually reporting to the solution back end the current state and potential error conditions of the update process.</span></span> <span data-ttu-id="bb775-111">Dit patroon is noodzakelijk hulpmiddel voor het beheer van grote sets van apparaten, zoals kunnen de back-end oplossing volledig inzicht in de status van het configuratieproces hebben op alle apparaten.</span><span class="sxs-lookup"><span data-stu-id="bb775-111">This pattern is instrumental to the management of large sets of devices, as it enables the solution back end to have full visibility of the state of the configuration process across all devices.</span></span>

> [!NOTE]
> <span data-ttu-id="bb775-112">In scenario's waarin apparaten worden beheerd op een nieuwe interactieve wijze (inschakelen voor een ventilator van een gebruiker beheerde app), kunt u overwegen [methoden directe][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="bb775-112">In scenarios where devices are controlled in a more interactive fashion (turn on a fan from a user-controlled app), consider using [direct methods][lnk-methods].</span></span>
> 
> 

<span data-ttu-id="bb775-113">In deze zelfstudie, verandert de back-end oplossing de telemetrie-configuratie van een doelapparaat en dat, als gevolg hiervan volgt de apparaattoepassing een proces met meerdere stappen voor het toepassen van een configuratie-update (bijvoorbeeld vereisen van een software-module opnieuw wordt opgestart, waarvoor deze zelfstudie simuleert met een eenvoudige vertraging).</span><span class="sxs-lookup"><span data-stu-id="bb775-113">In this tutorial, the solution back end changes the telemetry configuration of a target device and, as a result of that, the device app follows a multi-step process to apply a configuration update (for example, requiring a software module restart, which this tutorial simulates with a simple delay).</span></span>

<span data-ttu-id="bb775-114">De back-end oplossing slaat de configuratie in de apparaat-twin gewenste eigenschappen in de volgende manier:</span><span class="sxs-lookup"><span data-stu-id="bb775-114">The solution back end stores the configuration in the device twin's desired properties in the following way:</span></span>

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of the configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> <span data-ttu-id="bb775-115">Omdat configuraties kunnen complexe objecten, worden ze meestal toegewezen unieke id's (hashes of [GUID's][lnk-guid]) voor het vereenvoudigen van hun vergelijkingen.</span><span class="sxs-lookup"><span data-stu-id="bb775-115">Since configurations can be complex objects, they are usually assigned unique ids (hashes or [GUIDs][lnk-guid]) to simplify their comparisons.</span></span>
> 
> 

<span data-ttu-id="bb775-116">De app apparaat rapporteert de huidige configuratie voor het spiegelen van de gewenste eigenschap **telemetryConfig** in de gerapporteerde eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="bb775-116">The device app reports its current configuration mirroring the desired property **telemetryConfig** in the reported properties:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of the current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

<span data-ttu-id="bb775-117">Opmerking hoe de gerapporteerde **telemetryConfig** heeft een extra eigenschap **status**die worden gebruikt voor het rapporteren van de status van het configuratieproces van de update.</span><span class="sxs-lookup"><span data-stu-id="bb775-117">Note how the reported **telemetryConfig** has an additional property **status**, used to report the state of the configuration update process.</span></span>

<span data-ttu-id="bb775-118">Wanneer een nieuwe gewenste configuratie wordt ontvangen, rapporteert de apparaattoepassing een in behandeling configuratie door de gegevens te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="bb775-118">When a new desired configuration is received, the device app reports a pending configuration by changing the information:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of the current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of the pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

<span data-ttu-id="bb775-119">Klik vervolgens op een later tijdstip rapporteert de apparaattoepassing het slagen of mislukken van deze bewerking door het bijwerken van de bovenstaande eigenschap.</span><span class="sxs-lookup"><span data-stu-id="bb775-119">Then, at some later time, the device app will report the success or failure of this operation by updating the above property.</span></span>
<span data-ttu-id="bb775-120">Houd er rekening mee hoe de back-end oplossing kunnen op elk gewenst moment de status van de configuratie niet opvragen op alle apparaten.</span><span class="sxs-lookup"><span data-stu-id="bb775-120">Note how the solution back end is able, at any time, to query the status of the configuration process across all the devices.</span></span>

<span data-ttu-id="bb775-121">In deze handleiding ontdekt u hoe u:</span><span class="sxs-lookup"><span data-stu-id="bb775-121">This tutorial shows you how to:</span></span>

* <span data-ttu-id="bb775-122">Maakt een gesimuleerd apparaat-app die configuratie-updates ontvangt van de back-end van de oplossing en rapporten van meerdere updates als *eigenschappen gerapporteerd* proces van de configuratie niet bijwerken.</span><span class="sxs-lookup"><span data-stu-id="bb775-122">Create a simulated device app that receives configuration updates from the solution back end, and reports multiple updates as *reported properties* on the configuration update process.</span></span>
* <span data-ttu-id="bb775-123">Maak een back-end-app die werkt u de gewenste configuratie van een apparaat en het configuratieproces van de update vervolgens een query.</span><span class="sxs-lookup"><span data-stu-id="bb775-123">Create a back-end app that updates the desired configuration of a device, and then queries the configuration update process.</span></span>

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

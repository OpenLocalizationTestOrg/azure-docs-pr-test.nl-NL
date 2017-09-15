> [!div class="op_single_selector"]
> * [<span data-ttu-id="d2219-101">Linux</span><span class="sxs-lookup"><span data-stu-id="d2219-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="d2219-102">Windows</span><span class="sxs-lookup"><span data-stu-id="d2219-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="d2219-103">Dit artikel bevat een gedetailleerd overzicht van de [Hallo wereld-voorbeeldcode][lnk-helloworld-sample] om de fundamentele onderdelen van de architectuur van [Azure IoT Edge][lnk-iot-edge] te illustreren.</span><span class="sxs-lookup"><span data-stu-id="d2219-103">This article provides a detailed walkthrough of the [Hello World sample code][lnk-helloworld-sample] to illustrate the fundamental components of the [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="d2219-104">In het voorbeeld wordt Azure IoT Edge gebruikt om een eenvoudige gateway te maken die om de vijf seconden een 'Hallo wereld'-bericht vastlegt in een bestand.</span><span class="sxs-lookup"><span data-stu-id="d2219-104">The sample uses the Azure IoT Edge to build a simple gateway that logs a "hello world" message to a file every five seconds.</span></span>

<span data-ttu-id="d2219-105">Dit overzicht omvat:</span><span class="sxs-lookup"><span data-stu-id="d2219-105">This walkthrough covers:</span></span>

* <span data-ttu-id="d2219-106">**Hallo wereld voorbeeldarchitectuur**: hierin wordt beschreven hoe [Azure IoT rand architectuur concepten] [ lnk-edge-concepts] van toepassing op het Hallo wereld-voorbeeld en hoe de onderdelen in elkaar passen.</span><span class="sxs-lookup"><span data-stu-id="d2219-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply to the Hello World sample and how the components fit together.</span></span>
* <span data-ttu-id="d2219-107">**Het voorbeeld maken**: de stappen die nodig zijn om het voorbeeld te maken.</span><span class="sxs-lookup"><span data-stu-id="d2219-107">**How to build the sample**: The steps required to build the sample.</span></span>
* <span data-ttu-id="d2219-108">**Het voorbeeld uitvoeren**: de stappen die nodig zijn om het voorbeeld uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="d2219-108">**How to run the sample**: The steps required to run the sample.</span></span> 
* <span data-ttu-id="d2219-109">**Typische uitvoer**: een voorbeeld van de uitvoer die u kunt verwachten wanneer u het voorbeeld uitvoert.</span><span class="sxs-lookup"><span data-stu-id="d2219-109">**Typical output**: An example of the output to expect when you run the sample.</span></span>
* <span data-ttu-id="d2219-110">**Codefragmenten**: een verzameling van codefragmenten om weer te geven hoe het Hallo wereld-voorbeeld belangrijke onderdelen van de rand van de IoT gateway implementeert.</span><span class="sxs-lookup"><span data-stu-id="d2219-110">**Code snippets**: A collection of code snippets to show how the Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="d2219-111">Architectuur van het 'Hallo wereld'-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d2219-111">Hello World sample architecture</span></span>
<span data-ttu-id="d2219-112">Het 'Hallo wereld'-voorbeeld illustreert de concepten die in de vorige sectie zijn beschreven.</span><span class="sxs-lookup"><span data-stu-id="d2219-112">The Hello World sample illustrates the concepts described in the previous section.</span></span> <span data-ttu-id="d2219-113">Het Hallo wereld-voorbeeld implementeert een IoT-Edge-gateway met een pijplijn die bestaat uit twee IoT Edge-modules:</span><span class="sxs-lookup"><span data-stu-id="d2219-113">The Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="d2219-114">De *Hallo wereld*-module maakt om de vijf seconden een bericht en geeft dit door aan de logboekregistratiemodule.</span><span class="sxs-lookup"><span data-stu-id="d2219-114">The *hello world* module creates a message every five seconds and passes it to the logger module.</span></span>
* <span data-ttu-id="d2219-115">De *logboekregistratie*module schrijft de ontvangen berichten naar een bestand.</span><span class="sxs-lookup"><span data-stu-id="d2219-115">The *logger* module writes the messages it receives to a file.</span></span>

![Architectuur van 'Hallo wereld'-voorbeeld gebouwd met Azure IoT Edge][4]

<span data-ttu-id="d2219-117">Zoals in de vorige sectie is beschreven, geeft de module 'Hallo wereld' niet elke vijf seconden berichten rechtstreeks aan de logboekregistratiemodule door.</span><span class="sxs-lookup"><span data-stu-id="d2219-117">As described in the previous section, the Hello World module does not pass messages directly to the logger module every five seconds.</span></span> <span data-ttu-id="d2219-118">In plaats daarvan wordt het bericht elke vijf seconden naar de broker gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="d2219-118">Instead, it publishes a message to the broker every five seconds.</span></span>

<span data-ttu-id="d2219-119">De loggermodule ontvangt het bericht van de broker en reageert erop door de inhoud van het bericht naar een bestand te schrijven.</span><span class="sxs-lookup"><span data-stu-id="d2219-119">The logger module receives the message from the broker and acts upon it, writing the contents of the message to a file.</span></span>

<span data-ttu-id="d2219-120">De loggermodule verwerkt alleen berichten van de broker en publiceert nooit nieuwe berichten naar de broker.</span><span class="sxs-lookup"><span data-stu-id="d2219-120">The logger module only consumes messages from the broker, it never publishes new messages to the broker.</span></span>

![Hoe de broker berichten routeert tussen modules in Azure IoT Edge][5]

<span data-ttu-id="d2219-122">In de bovenstaande afbeelding ziet u de architectuur van het 'Hello World'-voorbeeld en de relatieve paden naar de bronbestanden die verschillende delen van het voorbeeld implementeren in de [opslagplaats][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="d2219-122">The figure above shows the architecture of the Hello World sample and the relative paths to the source files that implement different portions of the sample in the [repository][lnk-iot-edge].</span></span> <span data-ttu-id="d2219-123">Verken zelf de code of gebruik de codefragmenten hieronder als richtlijn.</span><span class="sxs-lookup"><span data-stu-id="d2219-123">Explore the code on your own, or use the code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md
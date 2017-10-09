> [!div class="op_single_selector"]
> * [<span data-ttu-id="9e36e-101">Linux</span><span class="sxs-lookup"><span data-stu-id="9e36e-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="9e36e-102">Windows</span><span class="sxs-lookup"><span data-stu-id="9e36e-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="9e36e-103">Dit artikel bevat een gedetailleerd overzicht van Hallo [Hallo wereld voorbeeldcode] [ lnk-helloworld-sample] tooillustrate Hallo fundamentele onderdelen van Hallo [Azure IoT rand] [ lnk-iot-edge] architectuur.</span><span class="sxs-lookup"><span data-stu-id="9e36e-103">This article provides a detailed walkthrough of hello [Hello World sample code][lnk-helloworld-sample] tooillustrate hello fundamental components of hello [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="9e36e-104">Hallo voorbeeld maakt gebruik van hello Azure IoT rand toobuild een eenvoudige gateway die u een "Hallo wereld" tooa berichtbestand elke vijf seconden registreert.</span><span class="sxs-lookup"><span data-stu-id="9e36e-104">hello sample uses hello Azure IoT Edge toobuild a simple gateway that logs a "hello world" message tooa file every five seconds.</span></span>

<span data-ttu-id="9e36e-105">Dit overzicht omvat:</span><span class="sxs-lookup"><span data-stu-id="9e36e-105">This walkthrough covers:</span></span>

* <span data-ttu-id="9e36e-106">**Hallo wereld voorbeeldarchitectuur**: hierin wordt beschreven hoe [Azure IoT rand architectuur concepten] [ lnk-edge-concepts] toohello Hallo wereld-voorbeeld en hoe Hallo-onderdelen in elkaar passen toepassen.</span><span class="sxs-lookup"><span data-stu-id="9e36e-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply toohello Hello World sample and how hello components fit together.</span></span>
* <span data-ttu-id="9e36e-107">**Hoe toobuild voorbeeld Hallo**: Hallo stappen vereist toobuild Hallo voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="9e36e-107">**How toobuild hello sample**: hello steps required toobuild hello sample.</span></span>
* <span data-ttu-id="9e36e-108">**Hoe toorun voorbeeld Hallo**: Hallo stappen vereist toorun Hallo voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="9e36e-108">**How toorun hello sample**: hello steps required toorun hello sample.</span></span> 
* <span data-ttu-id="9e36e-109">**Typische uitvoer**: een voorbeeld van Hallo tooexpect uitvoer wanneer u Hallo voorbeeld uitvoert.</span><span class="sxs-lookup"><span data-stu-id="9e36e-109">**Typical output**: An example of hello output tooexpect when you run hello sample.</span></span>
* <span data-ttu-id="9e36e-110">**Codefragmenten**: een verzameling van code codefragmenten tooshow hoe Hallo Hallo wereld-voorbeeld implementeert sleutel rand IoT gateway-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="9e36e-110">**Code snippets**: A collection of code snippets tooshow how hello Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="9e36e-111">Architectuur van het 'Hallo wereld'-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="9e36e-111">Hello World sample architecture</span></span>
<span data-ttu-id="9e36e-112">Hallo Hallo wereld-voorbeeld illustreert Hallo concepten beschreven in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="9e36e-112">hello Hello World sample illustrates hello concepts described in hello previous section.</span></span> <span data-ttu-id="9e36e-113">Hallo Hallo wereld-voorbeeld implementeert een IoT-Edge-gateway met een pijplijn die bestaat uit twee IoT Edge-modules:</span><span class="sxs-lookup"><span data-stu-id="9e36e-113">hello Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="9e36e-114">Hallo *Hallo wereld* module elke vijf seconden een bericht wordt gemaakt en wordt doorgegeven toohello berichtenlogboek module.</span><span class="sxs-lookup"><span data-stu-id="9e36e-114">hello *hello world* module creates a message every five seconds and passes it toohello logger module.</span></span>
* <span data-ttu-id="9e36e-115">Hallo *berichtenlogboek* module schrijfbewerkingen Hallo-berichten ontvangen tooa-bestand.</span><span class="sxs-lookup"><span data-stu-id="9e36e-115">hello *logger* module writes hello messages it receives tooa file.</span></span>

![Architectuur van 'Hallo wereld'-voorbeeld gebouwd met Azure IoT Edge][4]

<span data-ttu-id="9e36e-117">Zoals beschreven in de vorige sectie hello, Hallo Hallo wereld module niet geeft-berichten rechtstreeks toohello berichtenlogboek module elke vijf seconden.</span><span class="sxs-lookup"><span data-stu-id="9e36e-117">As described in hello previous section, hello Hello World module does not pass messages directly toohello logger module every five seconds.</span></span> <span data-ttu-id="9e36e-118">Het publiceert in plaats daarvan elke vijf seconden een bericht toohello broker.</span><span class="sxs-lookup"><span data-stu-id="9e36e-118">Instead, it publishes a message toohello broker every five seconds.</span></span>

<span data-ttu-id="9e36e-119">Hallo berichtenlogboek module Hallo-bericht ontvangt van Hallo broker en fungeert daarvan Hallo inhoud van Hallo-bericht tooa bestand schrijven.</span><span class="sxs-lookup"><span data-stu-id="9e36e-119">hello logger module receives hello message from hello broker and acts upon it, writing hello contents of hello message tooa file.</span></span>

<span data-ttu-id="9e36e-120">Hallo berichtenlogboek module alleen berichten van Hallo broker verbruikt, nieuwe berichten toohello broker nooit wordt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="9e36e-120">hello logger module only consumes messages from hello broker, it never publishes new messages toohello broker.</span></span>

![Hoe Hallo broker routeert berichten tussen de modules in Azure IoT rand][5]

<span data-ttu-id="9e36e-122">Hallo bovenstaande afbeelding ziet u Hallo-architectuur van Hallo Hallo wereld-voorbeeld en relatieve paden Hallo toohello bronbestanden die andere gedeelten van Hallo voorbeeld in Hallo implementeren [opslagplaats][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="9e36e-122">hello figure above shows hello architecture of hello Hello World sample and hello relative paths toohello source files that implement different portions of hello sample in hello [repository][lnk-iot-edge].</span></span> <span data-ttu-id="9e36e-123">Verken Hallo code in uw eigen of Hallo codefragmenten hieronder als richtlijn gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9e36e-123">Explore hello code on your own, or use hello code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md
## <a name="typical-output"></a><span data-ttu-id="f3420-101">Typische uitvoer</span><span class="sxs-lookup"><span data-stu-id="f3420-101">Typical output</span></span>

<span data-ttu-id="f3420-102">Hallo volgende voorbeeld ziet u Hallo uitvoer toohello logboekbestand geschreven door Hallo Hallo wereld-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f3420-102">hello following example shows hello output written toohello log file by hello Hello World sample.</span></span> <span data-ttu-id="f3420-103">Hallo-uitvoer is ingedeeld voor de leesbaarheid:</span><span class="sxs-lookup"><span data-stu-id="f3420-103">hello output is formatted for legibility:</span></span>

```json
[{
    "time": "Mon Apr 11 13:48:07 2016",
    "content": "Log started"
}, {
    "time": "Mon Apr 11 13:48:48 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:48:55 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:01 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:04 2016",
    "content": "Log stopped"
}]
```

## <a name="code-snippets"></a><span data-ttu-id="f3420-104">Codefragmenten</span><span class="sxs-lookup"><span data-stu-id="f3420-104">Code snippets</span></span>

<span data-ttu-id="f3420-105">In deze sectie worden enkele belangrijke secties Hallo-code in Hallo Hallo\_wereld-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f3420-105">This section discusses some key sections of hello code in hello hello\_world sample.</span></span>

### <a name="iot-edge-gateway-creation"></a><span data-ttu-id="f3420-106">Rand IoT gateway maken</span><span class="sxs-lookup"><span data-stu-id="f3420-106">IoT Edge gateway creation</span></span>

<span data-ttu-id="f3420-107">U moet implementeren een *gateway proces*.</span><span class="sxs-lookup"><span data-stu-id="f3420-107">You must implement a *gateway process*.</span></span> <span data-ttu-id="f3420-108">Dit programma Hallo interne infrastructuur (Hallo broker) maakt, wordt geladen Hallo IoT rand modules en configureert u Hallo gateway proces.</span><span class="sxs-lookup"><span data-stu-id="f3420-108">This program creates hello internal infrastructure (hello broker), loads hello IoT Edge modules, and configures hello gateway process.</span></span> <span data-ttu-id="f3420-109">IoT-Edge biedt Hallo **Gateway\_maken\_van\_JSON** werken tooenable toobootstrap een gateway vanuit een JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="f3420-109">IoT Edge provides hello **Gateway\_Create\_From\_JSON** function tooenable you toobootstrap a gateway from a JSON file.</span></span> <span data-ttu-id="f3420-110">Hallo toouse **Gateway\_maken\_van\_JSON** werkt, Hallo pad tooa JSON-bestand waarmee Hallo IoT rand modules tooload doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="f3420-110">toouse hello **Gateway\_Create\_From\_JSON** function, pass it hello path tooa JSON file that specifies hello IoT Edge modules tooload.</span></span>

<span data-ttu-id="f3420-111">U vindt Hallo code Hallo gateway proces op Hallo *Hallo wereld* voorbeeld in Hallo [main.c] [ lnk-main-c] bestand.</span><span class="sxs-lookup"><span data-stu-id="f3420-111">You can find hello code for hello gateway process in hello *Hello World* sample in hello [main.c][lnk-main-c] file.</span></span> <span data-ttu-id="f3420-112">Voor de leesbaarheid, hello volgende fragment toont een verkorte versie van Hallo gateway procescode.</span><span class="sxs-lookup"><span data-stu-id="f3420-112">For legibility, hello following snippet shows an abbreviated version of hello gateway process code.</span></span> <span data-ttu-id="f3420-113">Dit voorbeeldprogramma maakt u een gateway en vervolgens wordt gewacht op Hallo gebruiker toopress hello **ENTER** sleutel voordat deze omlaag Hallo-gateway breekt.</span><span class="sxs-lookup"><span data-stu-id="f3420-113">This example program creates a gateway and then waits for hello user toopress hello **ENTER** key before it tears down hello gateway.</span></span>

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed toocreate hello gateway from JSON\n");
    }
    else
    {
        printf("gateway successfully created from JSON\n");
        printf("gateway shall run until ENTER is pressed\n");
        (void)getchar();
        Gateway_LL_Destroy(gateway);
    }
    return 0;
}
```

<span data-ttu-id="f3420-114">Hallo JSON-instellingen-bestand bevat een lijst van IoT rand modules tooload en Hallo koppelingen tussen Hallo-modules.</span><span class="sxs-lookup"><span data-stu-id="f3420-114">hello JSON settings file contains a list of IoT Edge modules tooload and hello links between hello modules.</span></span> <span data-ttu-id="f3420-115">Elke IoT rand module moet a: opgeven</span><span class="sxs-lookup"><span data-stu-id="f3420-115">Each IoT Edge module must specify a:</span></span>

* <span data-ttu-id="f3420-116">**naam**: een unieke naam voor het Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="f3420-116">**name**: a unique name for hello module.</span></span>
* <span data-ttu-id="f3420-117">**laadprogramma**: een loader die weet hoe tooload Hallo module gewenst.</span><span class="sxs-lookup"><span data-stu-id="f3420-117">**loader**: a loader that knows how tooload hello desired module.</span></span> <span data-ttu-id="f3420-118">Laadprogramma's zijn een uitbreidingspunt voor het laden van verschillende soorten modules.</span><span class="sxs-lookup"><span data-stu-id="f3420-118">Loaders are an extension point for loading different types of modules.</span></span> <span data-ttu-id="f3420-119">IoT-Edge biedt laadprogramma's voor gebruik met modules die zijn geschreven in systeemeigen C, Node.js, Java en .NET.</span><span class="sxs-lookup"><span data-stu-id="f3420-119">IoT Edge provides loaders for use with modules written in native C, Node.js, Java, and .NET.</span></span> <span data-ttu-id="f3420-120">Hallo Hallo wereld-voorbeeld gebruikt alleen Hallo systeemeigen C loader omdat alle Hallo-modules in dit voorbeeld dynamische tapewisselaars die zijn geschreven in c zijn Voor meer informatie over het toouse IoT rand modules geschreven in verschillende talen, Zie Hallo [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), of [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="f3420-120">hello Hello World sample only uses hello native C loader because all hello modules in this sample are dynamic libraries written in C. For more information about how toouse IoT Edge modules written in different languages, see hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), or [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) samples.</span></span>
    * <span data-ttu-id="f3420-121">**naam**: Hallo-naam van Hallo loader tooload Hallo module gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f3420-121">**name**: hello name of hello loader used tooload hello module.</span></span>
    * <span data-ttu-id="f3420-122">**entrypoint**: Hallo pad toohello bibliotheek met Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="f3420-122">**entrypoint**: hello path toohello library containing hello module.</span></span> <span data-ttu-id="f3420-123">Voor Linux is deze bibliotheek een SO-bestand, voor Windows een DLL-bestand.</span><span class="sxs-lookup"><span data-stu-id="f3420-123">On Linux this library is a .so file, on Windows this library is a .dll file.</span></span> <span data-ttu-id="f3420-124">Hallo-ingangspunt is specifiek toohello type loader wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f3420-124">hello entry point is specific toohello type of loader being used.</span></span> <span data-ttu-id="f3420-125">Hallo Node.js loader invoerpunt is een bestand .js.</span><span class="sxs-lookup"><span data-stu-id="f3420-125">hello Node.js loader entry point is a .js file.</span></span> <span data-ttu-id="f3420-126">Hallo Java loader invoerpunt is een klassepad en naam van een klasse.</span><span class="sxs-lookup"><span data-stu-id="f3420-126">hello Java loader entry point is a classpath and a class name.</span></span> <span data-ttu-id="f3420-127">Hallo .NET loader invoerpunt is een assembly-naam en de naam van een klasse.</span><span class="sxs-lookup"><span data-stu-id="f3420-127">hello .NET loader entry point is an assembly name and a class name.</span></span>

* <span data-ttu-id="f3420-128">**argumenten**: configuratie informatie Hallo module moet.</span><span class="sxs-lookup"><span data-stu-id="f3420-128">**args**: any configuration information hello module needs.</span></span>

<span data-ttu-id="f3420-129">Hallo volgende code toont Hallo JSON gebruikt toodeclare alle Hallo IoT Edge-modules voor Hallo Hallo wereld-voorbeeld op Linux.</span><span class="sxs-lookup"><span data-stu-id="f3420-129">hello following code shows hello JSON used toodeclare all hello IoT Edge modules for hello Hello World sample on Linux.</span></span> <span data-ttu-id="f3420-130">Of een module geen argumenten vereist, is afhankelijk van Hallo ontwerp van Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="f3420-130">Whether a module requires any arguments depends on hello design of hello module.</span></span> <span data-ttu-id="f3420-131">In dit voorbeeld Hallo berichtenlogboek module vereist een argument dat is Hallo pad toohello uitvoerbestand en Hallo Hallo\_wereld-module heeft geen argumenten.</span><span class="sxs-lookup"><span data-stu-id="f3420-131">In this example, hello logger module takes an argument that is hello path toohello output file and hello hello\_world module has no arguments.</span></span>

```json
"modules" :
[
    {
        "name" : "logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/logger/liblogger.so"
        }
        },
        "args" : {"filename":"log.txt"}
    },
    {
        "name" : "hello_world",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/hello_world/libhello_world.so"
        }
        },
        "args" : null
    }
]
```

<span data-ttu-id="f3420-132">Hallo JSON-bestand bevat ook Hallo koppelingen tussen Hallo-modules die zijn doorgegeven toohello broker.</span><span class="sxs-lookup"><span data-stu-id="f3420-132">hello JSON file also contains hello links between hello modules that are passed toohello broker.</span></span> <span data-ttu-id="f3420-133">Een koppeling heeft twee eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="f3420-133">A link has two properties:</span></span>

* <span data-ttu-id="f3420-134">**bron**: de naam van een module van Hallo `modules` sectie of `\*`.</span><span class="sxs-lookup"><span data-stu-id="f3420-134">**source**: a module name from hello `modules` section, or `\*`.</span></span>
* <span data-ttu-id="f3420-135">**sink**: de naam van een module van Hallo `modules` sectie.</span><span class="sxs-lookup"><span data-stu-id="f3420-135">**sink**: a module name from hello `modules` section.</span></span>

<span data-ttu-id="f3420-136">Elke koppeling definieert de route en richting van een bericht.</span><span class="sxs-lookup"><span data-stu-id="f3420-136">Each link defines a message route and direction.</span></span> <span data-ttu-id="f3420-137">Berichten van Hallo **bron** module geleverd toohello **sink** module.</span><span class="sxs-lookup"><span data-stu-id="f3420-137">Messages from hello **source** module are delivered toohello **sink** module.</span></span> <span data-ttu-id="f3420-138">U kunt instellen Hallo **bron** module te`\*`, waarmee wordt aangegeven dat Hallo **sink** module berichten ontvangt van elke module.</span><span class="sxs-lookup"><span data-stu-id="f3420-138">You can set hello **source** module too`\*`, which indicates that hello **sink** module receives messages from any module.</span></span>

<span data-ttu-id="f3420-139">Hallo volgende code toont Hallo JSON gebruikt tooconfigure koppelingen tussen Hallo-modules die worden gebruikt in Hallo Hallo\_wereld-voorbeeld op Linux.</span><span class="sxs-lookup"><span data-stu-id="f3420-139">hello following code shows hello JSON used tooconfigure links between hello modules used in hello hello\_world sample on Linux.</span></span> <span data-ttu-id="f3420-140">Elk bericht wordt geproduceerd door Hallo `hello_world` module wordt gebruikt door Hallo `logger` module.</span><span class="sxs-lookup"><span data-stu-id="f3420-140">Every message produced by hello `hello_world` module is consumed by hello `logger` module.</span></span>

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a><span data-ttu-id="f3420-141">Publiceren van berichten door de module hello\_world</span><span class="sxs-lookup"><span data-stu-id="f3420-141">Hello\_world module message publishing</span></span>

<span data-ttu-id="f3420-142">U vindt Hallo-code die wordt gebruikt door Hallo Hallo\_world module toopublish berichten in Hallo ['hello_world.c'] [ lnk-helloworld-c] bestand.</span><span class="sxs-lookup"><span data-stu-id="f3420-142">You can find hello code used by hello hello\_world module toopublish messages in hello ['hello_world.c'][lnk-helloworld-c] file.</span></span> <span data-ttu-id="f3420-143">Hallo volgende fragment toont een gewijzigde versie van Hallo code met opmerkingen toegevoegd en sommige foutafhandeling code voor de leesbaarheid verwijderd:</span><span class="sxs-lookup"><span data-stu-id="f3420-143">hello following snippet shows an amended version of hello code with comments added and some error handling code removed for legibility:</span></span>

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" tooa set of message properties that
    // will be appended toohello message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set hello content for hello message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set hello properties for hello message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on hello msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of hello thread*/
        }
        else
        {
            // publish hello message toohello broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a><span data-ttu-id="f3420-144">Berichtverwerking door de module hello\_world</span><span class="sxs-lookup"><span data-stu-id="f3420-144">Hello\_world module message processing</span></span>

<span data-ttu-id="f3420-145">Hallo Hallo\_world module verwerkt nooit berichten dat andere modules IoT rand toohello broker publiceren.</span><span class="sxs-lookup"><span data-stu-id="f3420-145">hello hello\_world module never processes messages that other IoT Edge modules publish toohello broker.</span></span> <span data-ttu-id="f3420-146">Implementatie van Hallo-bericht retouraanroep in Hallo Hallo daarom Hallo\_wereld-module is geen functie.</span><span class="sxs-lookup"><span data-stu-id="f3420-146">Therefore, hello implementation of hello message callback in hello hello\_world module is a no-op function.</span></span>

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a><span data-ttu-id="f3420-147">Loggermodule berichtpublicatie en -verwerking</span><span class="sxs-lookup"><span data-stu-id="f3420-147">Logger module message publishing and processing</span></span>

<span data-ttu-id="f3420-148">Hallo berichtenlogboek module berichten ontvangt van Hallo broker en schrijft ze tooa-bestand.</span><span class="sxs-lookup"><span data-stu-id="f3420-148">hello logger module receives messages from hello broker and writes them tooa file.</span></span> <span data-ttu-id="f3420-149">Deze module publiceert nooit berichten.</span><span class="sxs-lookup"><span data-stu-id="f3420-149">It never publishes any messages.</span></span> <span data-ttu-id="f3420-150">Daarom Hallo-code van Hallo berichtenlogboek module wordt nooit aangeroepen door Hallo **Broker_Publish** functie.</span><span class="sxs-lookup"><span data-stu-id="f3420-150">Therefore, hello code of hello logger module never calls hello **Broker_Publish** function.</span></span>

<span data-ttu-id="f3420-151">Hallo **Logger_Receive** functie in Hallo [logger.c] [ lnk-logger-c] bestand is Hallo callback Hallo broker toodeliver berichten toohello berichtenlogboek module wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f3420-151">hello **Logger_Receive** function in hello [logger.c][lnk-logger-c] file is hello callback hello broker invokes toodeliver messages toohello logger module.</span></span> <span data-ttu-id="f3420-152">Hallo volgende fragment toont een gewijzigde versie met opmerkingen toegevoegd en sommige foutafhandeling code voor de leesbaarheid verwijderd:</span><span class="sxs-lookup"><span data-stu-id="f3420-152">hello following snippet shows an amended version with comments added and some error handling code removed for legibility:</span></span>

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get hello message properties from hello message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert hello collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode hello message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start hello construction of hello final string toobe logged by adding
    // hello timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add hello message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add hello content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write hello formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a><span data-ttu-id="f3420-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f3420-153">Next steps</span></span>

<span data-ttu-id="f3420-154">In dit artikel hebt u een eenvoudige rand IoT gateway die berichten tooa logboekbestand uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f3420-154">In this article, you ran a simple IoT Edge gateway that writes messages tooa log file.</span></span> <span data-ttu-id="f3420-155">toorun een voorbeeldtoepassing die u berichten tooIoT Hub verzendt, Zie [rand van de IoT-apparaat-naar-cloud-berichten verzenden met een gesimuleerd apparaat met Linux] [ lnk-gateway-simulated-linux] of [rand van de IoT-apparaat-naar-cloud-berichten verzenden met een gesimuleerde apparaat met Windows][lnk-gateway-simulated-windows].</span><span class="sxs-lookup"><span data-stu-id="f3420-155">toorun a sample that sends messages tooIoT Hub, see [IoT Edge – send device-to-cloud messages with a simulated device using Linux][lnk-gateway-simulated-linux] or [IoT Edge – send device-to-cloud messages with a simulated device using Windows][lnk-gateway-simulated-windows].</span></span>


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md
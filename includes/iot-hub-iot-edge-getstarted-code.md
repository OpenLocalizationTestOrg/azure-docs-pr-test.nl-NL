## <a name="typical-output"></a><span data-ttu-id="4a023-101">Typische uitvoer</span><span class="sxs-lookup"><span data-stu-id="4a023-101">Typical output</span></span>

<span data-ttu-id="4a023-102">Het volgende voorbeeld ziet u de uitvoer naar het logboekbestand geschreven door de Hallo wereld-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4a023-102">The following example shows the output written to the log file by the Hello World sample.</span></span> <span data-ttu-id="4a023-103">De uitvoer is voor de leesbaarheid voorzien van opmaak:</span><span class="sxs-lookup"><span data-stu-id="4a023-103">The output is formatted for legibility:</span></span>

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

## <a name="code-snippets"></a><span data-ttu-id="4a023-104">Codefragmenten</span><span class="sxs-lookup"><span data-stu-id="4a023-104">Code snippets</span></span>

<span data-ttu-id="4a023-105">In deze sectie worden enkele belangrijke onderdelen van de code in het voorbeeldprogramma Hello\_World behandeld.</span><span class="sxs-lookup"><span data-stu-id="4a023-105">This section discusses some key sections of the code in the hello\_world sample.</span></span>

### <a name="iot-edge-gateway-creation"></a><span data-ttu-id="4a023-106">Rand IoT gateway maken</span><span class="sxs-lookup"><span data-stu-id="4a023-106">IoT Edge gateway creation</span></span>

<span data-ttu-id="4a023-107">U moet implementeren een *gateway proces*.</span><span class="sxs-lookup"><span data-stu-id="4a023-107">You must implement a *gateway process*.</span></span> <span data-ttu-id="4a023-108">Dit programma maakt de interne infrastructuur (broker), wordt de rand van de IoT-modules geladen en het proces gateway configureert.</span><span class="sxs-lookup"><span data-stu-id="4a023-108">This program creates the internal infrastructure (the broker), loads the IoT Edge modules, and configures the gateway process.</span></span> <span data-ttu-id="4a023-109">IoT Edge biedt de functie **Gateway\_Create\_From\_JSON**, waarmee u een gateway vanuit een JSON-bestand kunt opstarten.</span><span class="sxs-lookup"><span data-stu-id="4a023-109">IoT Edge provides the **Gateway\_Create\_From\_JSON** function to enable you to bootstrap a gateway from a JSON file.</span></span> <span data-ttu-id="4a023-110">Gebruik de **Gateway\_maken\_van\_JSON** werkt, het pad naar een JSON-bestand dat Hiermee geeft u aan de rand van de IoT-modules laden doorgeven.</span><span class="sxs-lookup"><span data-stu-id="4a023-110">To use the **Gateway\_Create\_From\_JSON** function, pass it the path to a JSON file that specifies the IoT Edge modules to load.</span></span>

<span data-ttu-id="4a023-111">U vindt de code voor het gateway-proces in de *Hallo wereld* voorbeeld in de [main.c] [ lnk-main-c] bestand.</span><span class="sxs-lookup"><span data-stu-id="4a023-111">You can find the code for the gateway process in the *Hello World* sample in the [main.c][lnk-main-c] file.</span></span> <span data-ttu-id="4a023-112">Voor een betere leesbaarheid bevat het fragment hieronder een verkorte versie van de code voor het verwerken van de gateway.</span><span class="sxs-lookup"><span data-stu-id="4a023-112">For legibility, the following snippet shows an abbreviated version of the gateway process code.</span></span> <span data-ttu-id="4a023-113">Het voorbeeldprogramma maakt een gateway en wacht dan tot de gebruiker op **Enter** drukt om de gateway weer te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4a023-113">This example program creates a gateway and then waits for the user to press the **ENTER** key before it tears down the gateway.</span></span>

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed to create the gateway from JSON\n");
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

<span data-ttu-id="4a023-114">De instellingen voor JSON-bestand bevat een lijst van de rand van de IoT-modules laden en de koppelingen tussen de modules.</span><span class="sxs-lookup"><span data-stu-id="4a023-114">The JSON settings file contains a list of IoT Edge modules to load and the links between the modules.</span></span> <span data-ttu-id="4a023-115">Elke IoT rand module moet a: opgeven</span><span class="sxs-lookup"><span data-stu-id="4a023-115">Each IoT Edge module must specify a:</span></span>

* <span data-ttu-id="4a023-116">**name**: een unieke naam voor de module.</span><span class="sxs-lookup"><span data-stu-id="4a023-116">**name**: a unique name for the module.</span></span>
* <span data-ttu-id="4a023-117">**loader**: een laadprogramma dat de gewenste module kan laden.</span><span class="sxs-lookup"><span data-stu-id="4a023-117">**loader**: a loader that knows how to load the desired module.</span></span> <span data-ttu-id="4a023-118">Laadprogramma's zijn een uitbreidingspunt voor het laden van verschillende soorten modules.</span><span class="sxs-lookup"><span data-stu-id="4a023-118">Loaders are an extension point for loading different types of modules.</span></span> <span data-ttu-id="4a023-119">IoT-Edge biedt laadprogramma's voor gebruik met modules die zijn geschreven in systeemeigen C, Node.js, Java en .NET.</span><span class="sxs-lookup"><span data-stu-id="4a023-119">IoT Edge provides loaders for use with modules written in native C, Node.js, Java, and .NET.</span></span> <span data-ttu-id="4a023-120">Het Hallo wereld-voorbeeld gebruikt alleen de lader van de systeemeigen C omdat alle modules in dit voorbeeld dynamische tapewisselaars die zijn geschreven in c zijn Zie voor meer informatie over het gebruik van de rand van de IoT-modules die zijn geschreven in verschillende talen de [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), of [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="4a023-120">The Hello World sample only uses the native C loader because all the modules in this sample are dynamic libraries written in C. For more information about how to use IoT Edge modules written in different languages, see the [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), or [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) samples.</span></span>
    * <span data-ttu-id="4a023-121">**naam**: de naam van het laadprogramma gebruikt voor het laden van de module.</span><span class="sxs-lookup"><span data-stu-id="4a023-121">**name**: the name of the loader used to load the module.</span></span>
    * <span data-ttu-id="4a023-122">**entrypoint**: het pad naar de bibliotheek met de module.</span><span class="sxs-lookup"><span data-stu-id="4a023-122">**entrypoint**: the path to the library containing the module.</span></span> <span data-ttu-id="4a023-123">Voor Linux is deze bibliotheek een SO-bestand, voor Windows een DLL-bestand.</span><span class="sxs-lookup"><span data-stu-id="4a023-123">On Linux this library is a .so file, on Windows this library is a .dll file.</span></span> <span data-ttu-id="4a023-124">Het toegangspunt is specifiek voor het type laadprogramma dat wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4a023-124">The entry point is specific to the type of loader being used.</span></span> <span data-ttu-id="4a023-125">Het toegangspunt voor Node.js-laadprogramma is een bestand .js.</span><span class="sxs-lookup"><span data-stu-id="4a023-125">The Node.js loader entry point is a .js file.</span></span> <span data-ttu-id="4a023-126">Het toegangspunt voor Java-laadprogramma is een klassepad en de naam van een klasse.</span><span class="sxs-lookup"><span data-stu-id="4a023-126">The Java loader entry point is a classpath and a class name.</span></span> <span data-ttu-id="4a023-127">Het toegangspunt voor .NET-laadprogramma is een assembly-naam en de naam van een klasse.</span><span class="sxs-lookup"><span data-stu-id="4a023-127">The .NET loader entry point is an assembly name and a class name.</span></span>

* <span data-ttu-id="4a023-128">**args**: alle configuratie-informatie die de module nodig heeft.</span><span class="sxs-lookup"><span data-stu-id="4a023-128">**args**: any configuration information the module needs.</span></span>

<span data-ttu-id="4a023-129">De volgende code toont de JSON die wordt gebruikt voor alle IoT-rand modules voor het Hallo wereld-voorbeeld declareren op Linux.</span><span class="sxs-lookup"><span data-stu-id="4a023-129">The following code shows the JSON used to declare all the IoT Edge modules for the Hello World sample on Linux.</span></span> <span data-ttu-id="4a023-130">Of een module argumenten nodig heeft, is afhankelijk van het ontwerp van de module.</span><span class="sxs-lookup"><span data-stu-id="4a023-130">Whether a module requires any arguments depends on the design of the module.</span></span> <span data-ttu-id="4a023-131">In dit voorbeeld wordt aan de loggermodule een argument doorgegeven dat bestaat uit het pad naar het uitvoerbestand. De module hello\_world heeft geen argumenten.</span><span class="sxs-lookup"><span data-stu-id="4a023-131">In this example, the logger module takes an argument that is the path to the output file and the hello\_world module has no arguments.</span></span>

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

<span data-ttu-id="4a023-132">Het JSON-bestand bevat ook de koppelingen tussen de modules die worden doorgegeven aan de broker.</span><span class="sxs-lookup"><span data-stu-id="4a023-132">The JSON file also contains the links between the modules that are passed to the broker.</span></span> <span data-ttu-id="4a023-133">Een koppeling heeft twee eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="4a023-133">A link has two properties:</span></span>

* <span data-ttu-id="4a023-134">**bron**: de naam van een module van de `modules` sectie of `\*`.</span><span class="sxs-lookup"><span data-stu-id="4a023-134">**source**: a module name from the `modules` section, or `\*`.</span></span>
* <span data-ttu-id="4a023-135">**sink**: de naam van een module van het gedeelte `modules`.</span><span class="sxs-lookup"><span data-stu-id="4a023-135">**sink**: a module name from the `modules` section.</span></span>

<span data-ttu-id="4a023-136">Elke koppeling definieert de route en richting van een bericht.</span><span class="sxs-lookup"><span data-stu-id="4a023-136">Each link defines a message route and direction.</span></span> <span data-ttu-id="4a023-137">Berichten van de **bron** module geleverd worden aan de **sink** module.</span><span class="sxs-lookup"><span data-stu-id="4a023-137">Messages from the **source** module are delivered to the **sink** module.</span></span> <span data-ttu-id="4a023-138">U kunt instellen de **bron** module die u wilt `\*`, wat aangeeft dat de **sink** module berichten ontvangt van elke module.</span><span class="sxs-lookup"><span data-stu-id="4a023-138">You can set the **source** module to `\*`, which indicates that the **sink** module receives messages from any module.</span></span>

<span data-ttu-id="4a023-139">De volgende code toont de JSON die wordt gebruikt om koppelingen te configureren tussen de modules die worden gebruikt in het voorbeeld hello\_world op Linux.</span><span class="sxs-lookup"><span data-stu-id="4a023-139">The following code shows the JSON used to configure links between the modules used in the hello\_world sample on Linux.</span></span> <span data-ttu-id="4a023-140">Elk bericht dat wordt gemaakt door de module `hello_world`, wordt gebruikt door de module `logger`.</span><span class="sxs-lookup"><span data-stu-id="4a023-140">Every message produced by the `hello_world` module is consumed by the `logger` module.</span></span>

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a><span data-ttu-id="4a023-141">Publiceren van berichten door de module hello\_world</span><span class="sxs-lookup"><span data-stu-id="4a023-141">Hello\_world module message publishing</span></span>

<span data-ttu-id="4a023-142">U vindt de code die door de module hello\_world wordt gebruikt om berichten te publiceren, in het bestand [hello_world.c][lnk-helloworld-c].</span><span class="sxs-lookup"><span data-stu-id="4a023-142">You can find the code used by the hello\_world module to publish messages in the ['hello_world.c'][lnk-helloworld-c] file.</span></span> <span data-ttu-id="4a023-143">Voor een betere leesbaarheid bevat het volgende fragment een gewijzigde versie van de code, waarbij opmerkingen zijn toegevoegd en code voor foutafhandeling is weggelaten:</span><span class="sxs-lookup"><span data-stu-id="4a023-143">The following snippet shows an amended version of the code with comments added and some error handling code removed for legibility:</span></span>

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" to a set of message properties that
    // will be appended to the message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set the content for the message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set the properties for the message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on the msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of the thread*/
        }
        else
        {
            // publish the message to the broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a><span data-ttu-id="4a023-144">Berichtverwerking door de module hello\_world</span><span class="sxs-lookup"><span data-stu-id="4a023-144">Hello\_world module message processing</span></span>

<span data-ttu-id="4a023-145">De Hallo\_world module nooit berichten verwerkt die andere modules IoT rand naar de broker publiceren.</span><span class="sxs-lookup"><span data-stu-id="4a023-145">The hello\_world module never processes messages that other IoT Edge modules publish to the broker.</span></span> <span data-ttu-id="4a023-146">Om die reden is de implementatie van de bericht-callback in de module hello\_world een no-op-functie.</span><span class="sxs-lookup"><span data-stu-id="4a023-146">Therefore, the implementation of the message callback in the hello\_world module is a no-op function.</span></span>

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a><span data-ttu-id="4a023-147">Loggermodule berichtpublicatie en -verwerking</span><span class="sxs-lookup"><span data-stu-id="4a023-147">Logger module message publishing and processing</span></span>

<span data-ttu-id="4a023-148">De loggermodule ontvangt berichten van de broker en schrijft deze weg naar een bestand.</span><span class="sxs-lookup"><span data-stu-id="4a023-148">The logger module receives messages from the broker and writes them to a file.</span></span> <span data-ttu-id="4a023-149">Deze module publiceert nooit berichten.</span><span class="sxs-lookup"><span data-stu-id="4a023-149">It never publishes any messages.</span></span> <span data-ttu-id="4a023-150">Daarom roept de code van de loggermodule nooit de functie **Broker_Publish** aan.</span><span class="sxs-lookup"><span data-stu-id="4a023-150">Therefore, the code of the logger module never calls the **Broker_Publish** function.</span></span>

<span data-ttu-id="4a023-151">De **Logger_Receive** werken in de [logger.c] [ lnk-logger-c] bestand is de callback van de broker wordt aangeroepen voor het leveren van berichten naar de module berichtenlogboek.</span><span class="sxs-lookup"><span data-stu-id="4a023-151">The **Logger_Receive** function in the [logger.c][lnk-logger-c] file is the callback the broker invokes to deliver messages to the logger module.</span></span> <span data-ttu-id="4a023-152">Voor een betere leesbaarheid bevat het volgende fragment een gewijzigde versie, waarbij opmerkingen zijn toegevoegd en code voor foutafhandeling is weggelaten:</span><span class="sxs-lookup"><span data-stu-id="4a023-152">The following snippet shows an amended version with comments added and some error handling code removed for legibility:</span></span>

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get the message properties from the message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert the collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode the message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start the construction of the final string to be logged by adding
    // the timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add the message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add the content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write the formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a><span data-ttu-id="4a023-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4a023-153">Next steps</span></span>

<span data-ttu-id="4a023-154">In dit artikel hebt u een eenvoudige rand IoT gateway die berichten naar een logboekbestand schrijft uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4a023-154">In this article, you ran a simple IoT Edge gateway that writes messages to a log file.</span></span> <span data-ttu-id="4a023-155">Zie het uitvoeren van een steekproef die berichten naar IoT Hub verzendt [rand van de IoT-apparaat-naar-cloud-berichten verzenden met een gesimuleerd apparaat met Linux] [ lnk-gateway-simulated-linux] of [rand van de IoT-apparaat-naar-cloud-berichten verzenden met een gesimuleerde apparaat met Windows][lnk-gateway-simulated-windows].</span><span class="sxs-lookup"><span data-stu-id="4a023-155">To run a sample that sends messages to IoT Hub, see [IoT Edge – send device-to-cloud messages with a simulated device using Linux][lnk-gateway-simulated-linux] or [IoT Edge – send device-to-cloud messages with a simulated device using Windows][lnk-gateway-simulated-windows].</span></span>


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md
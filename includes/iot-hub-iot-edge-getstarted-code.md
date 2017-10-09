## <a name="typical-output"></a>Typische uitvoer

Hallo volgende voorbeeld ziet u Hallo uitvoer toohello logboekbestand geschreven door Hallo Hallo wereld-voorbeeld. Hallo-uitvoer is ingedeeld voor de leesbaarheid:

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

## <a name="code-snippets"></a>Codefragmenten

In deze sectie worden enkele belangrijke secties Hallo-code in Hallo Hallo\_wereld-voorbeeld.

### <a name="iot-edge-gateway-creation"></a>Rand IoT gateway maken

U moet implementeren een *gateway proces*. Dit programma Hallo interne infrastructuur (Hallo broker) maakt, wordt geladen Hallo IoT rand modules en configureert u Hallo gateway proces. IoT-Edge biedt Hallo **Gateway\_maken\_van\_JSON** werken tooenable toobootstrap een gateway vanuit een JSON-bestand. Hallo toouse **Gateway\_maken\_van\_JSON** werkt, Hallo pad tooa JSON-bestand waarmee Hallo IoT rand modules tooload doorgegeven.

U vindt Hallo code Hallo gateway proces op Hallo *Hallo wereld* voorbeeld in Hallo [main.c] [ lnk-main-c] bestand. Voor de leesbaarheid, hello volgende fragment toont een verkorte versie van Hallo gateway procescode. Dit voorbeeldprogramma maakt u een gateway en vervolgens wordt gewacht op Hallo gebruiker toopress hello **ENTER** sleutel voordat deze omlaag Hallo-gateway breekt.

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

Hallo JSON-instellingen-bestand bevat een lijst van IoT rand modules tooload en Hallo koppelingen tussen Hallo-modules. Elke IoT rand module moet a: opgeven

* **naam**: een unieke naam voor het Hallo-module.
* **laadprogramma**: een loader die weet hoe tooload Hallo module gewenst. Laadprogramma's zijn een uitbreidingspunt voor het laden van verschillende soorten modules. IoT-Edge biedt laadprogramma's voor gebruik met modules die zijn geschreven in systeemeigen C, Node.js, Java en .NET. Hallo Hallo wereld-voorbeeld gebruikt alleen Hallo systeemeigen C loader omdat alle Hallo-modules in dit voorbeeld dynamische tapewisselaars die zijn geschreven in c zijn Voor meer informatie over het toouse IoT rand modules geschreven in verschillende talen, Zie Hallo [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), of [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) voorbeelden.
    * **naam**: Hallo-naam van Hallo loader tooload Hallo module gebruikt.
    * **entrypoint**: Hallo pad toohello bibliotheek met Hallo-module. Voor Linux is deze bibliotheek een SO-bestand, voor Windows een DLL-bestand. Hallo-ingangspunt is specifiek toohello type loader wordt gebruikt. Hallo Node.js loader invoerpunt is een bestand .js. Hallo Java loader invoerpunt is een klassepad en naam van een klasse. Hallo .NET loader invoerpunt is een assembly-naam en de naam van een klasse.

* **argumenten**: configuratie informatie Hallo module moet.

Hallo volgende code toont Hallo JSON gebruikt toodeclare alle Hallo IoT Edge-modules voor Hallo Hallo wereld-voorbeeld op Linux. Of een module geen argumenten vereist, is afhankelijk van Hallo ontwerp van Hallo-module. In dit voorbeeld Hallo berichtenlogboek module vereist een argument dat is Hallo pad toohello uitvoerbestand en Hallo Hallo\_wereld-module heeft geen argumenten.

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

Hallo JSON-bestand bevat ook Hallo koppelingen tussen Hallo-modules die zijn doorgegeven toohello broker. Een koppeling heeft twee eigenschappen:

* **bron**: de naam van een module van Hallo `modules` sectie of `\*`.
* **sink**: de naam van een module van Hallo `modules` sectie.

Elke koppeling definieert de route en richting van een bericht. Berichten van Hallo **bron** module geleverd toohello **sink** module. U kunt instellen Hallo **bron** module te`\*`, waarmee wordt aangegeven dat Hallo **sink** module berichten ontvangt van elke module.

Hallo volgende code toont Hallo JSON gebruikt tooconfigure koppelingen tussen Hallo-modules die worden gebruikt in Hallo Hallo\_wereld-voorbeeld op Linux. Elk bericht wordt geproduceerd door Hallo `hello_world` module wordt gebruikt door Hallo `logger` module.

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a>Publiceren van berichten door de module hello\_world

U vindt Hallo-code die wordt gebruikt door Hallo Hallo\_world module toopublish berichten in Hallo ['hello_world.c'] [ lnk-helloworld-c] bestand. Hallo volgende fragment toont een gewijzigde versie van Hallo code met opmerkingen toegevoegd en sommige foutafhandeling code voor de leesbaarheid verwijderd:

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

### <a name="helloworld-module-message-processing"></a>Berichtverwerking door de module hello\_world

Hallo Hallo\_world module verwerkt nooit berichten dat andere modules IoT rand toohello broker publiceren. Implementatie van Hallo-bericht retouraanroep in Hallo Hallo daarom Hallo\_wereld-module is geen functie.

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a>Loggermodule berichtpublicatie en -verwerking

Hallo berichtenlogboek module berichten ontvangt van Hallo broker en schrijft ze tooa-bestand. Deze module publiceert nooit berichten. Daarom Hallo-code van Hallo berichtenlogboek module wordt nooit aangeroepen door Hallo **Broker_Publish** functie.

Hallo **Logger_Receive** functie in Hallo [logger.c] [ lnk-logger-c] bestand is Hallo callback Hallo broker toodeliver berichten toohello berichtenlogboek module wordt aangeroepen. Hallo volgende fragment toont een gewijzigde versie met opmerkingen toegevoegd en sommige foutafhandeling code voor de leesbaarheid verwijderd:

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

## <a name="next-steps"></a>Volgende stappen

In dit artikel hebt u een eenvoudige rand IoT gateway die berichten tooa logboekbestand uitgevoerd. toorun een voorbeeldtoepassing die u berichten tooIoT Hub verzendt, Zie [rand van de IoT-apparaat-naar-cloud-berichten verzenden met een gesimuleerd apparaat met Linux] [ lnk-gateway-simulated-linux] of [rand van de IoT-apparaat-naar-cloud-berichten verzenden met een gesimuleerde apparaat met Windows][lnk-gateway-simulated-windows].


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md
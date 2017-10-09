---
title: aaaAzure IoT-apparaat SDK voor C - serialisatiefunctie | Microsoft Docs
description: Hoe toouse Hallo Serializer-bibliotheek op Hallo van het apparaat van Azure IoT SDK voor C toocreate apparaat-apps die communiceren met een IoT-hub.
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: defbed34-de73-429c-8592-cd863a38e4dd
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: c5776e9b50ffea71df96cb2d342ea2fc045f5a0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a>Azure IoT-apparaat SDK voor C: meer informatie over de serialisatiefunctie
Hallo [eerst artikel](iot-hub-device-sdk-c-intro.md) in deze reeks geïntroduceerd Hallo **Azure IoT-device SDK voor C**. het volgende artikel Hallo opgegeven een gedetailleerdere beschrijving van Hallo [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md). In dit artikel is dekking Hallo SDK voltooid door een gedetailleerdere beschrijving van de resterende onderdeel Hallo: Hallo **serialisatiefunctie** bibliotheek.

Hallo inleidende artikel wordt beschreven hoe toouse hello **serialisatiefunctie** bibliotheek toosend gebeurtenissen tooand ontvangen berichten uit IoT Hub. In dit artikel we die discussie uitbreiden door te geven van een uitgebreidere uitleg van de werking toomodel uw gegevens met Hallo **serialisatiefunctie** macrotaal. Hallo artikel bevat ook meer informatie over hoe Hallo bibliotheek berichten serialiseert (en in sommige gevallen hoe u kunt bepalen Hallo serialisatie gedrag). We beschrijven ook bepaalde parameters die kunt u wijzigen om te bepalen Hallo grootte van Hallo modellen die u maakt.

Ten slotte revisits Hallo artikel sommige onderwerpen in de vorige artikelen zoals bericht en de verwerking van de eigenschap. Als we vinden uit deze werken in dezelfde manier met Hallo Hallo **serialisatiefunctie** bibliotheek als met de Hallo **IoTHubClient** bibliotheek.

Alles dat wordt beschreven in dit artikel is gebaseerd op Hallo **serialisatiefunctie** SDK-voorbeelden. Als u toofollow langs wilt, raadpleegt u Hallo **simplesample\_amqp** en **simplesample\_http** toepassingen die zijn opgenomen in hello Azure IoT-device SDK voor C.

U vindt Hallo [ **Azure IoT-device SDK voor C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub-opslagplaats en de weergave details van Hallo API in Hallo [C-API-referentiemateriaal](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-modeling-language"></a>Hallo modelleertaal
Hallo [inleidende artikel](iot-hub-device-sdk-c-intro.md) in deze reeks geïntroduceerd Hallo **Azure IoT-device SDK voor C** modelleertaal via Hallo voorbeeld in Hallo **simplesample\_amqp**  toepassing:

```
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(double, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

Zoals u ziet, is Hallo modelleertaal gebaseerd op C macro's. De definitie van de met beginnen altijd **BEGIN\_NAAMRUIMTE** en altijd eindigen met **END\_NAAMRUIMTE**. Hallo naamruimte voor uw bedrijf of, net zoals in dit voorbeeld Hallo-project dat u met werkt een algemene tooname is.

Wat komt binnen Hallo naamruimte model definities zijn. In dit geval is er één model voor een anemometer. Nogmaals Hallo model kan worden benoemd alles, maar doorgaans dit heet Hallo-apparaat of type gegevens dat u wilt tooexchange met IoT Hub.  

Modellen een definitie bevatten van Hallo gebeurtenissen kunt u inkomend tooIoT Hub (Hallo *gegevens*) en het Hallo-berichten uit IoT Hub kunt u ontvangen (Hallo *acties*). Als u in het Hallo-voorbeeld zien kunt, hebben gebeurtenissen een type en een naam; acties hebben een naam en optionele parameters (elk met een type).

Wat wordt niet gedemonstreerd in dit voorbeeld zijn extra gegevenstypen die worden ondersteund door Hallo SDK. Aan bod om het dialoogvenster.

> [!NOTE]
> IoT Hub verwijst toohello gegevens een apparaat tooit als verzendt *gebeurtenissen*, terwijl Hallo modelleertaal tooit als verwijst *gegevens* (gedefinieerd met behulp van **WITH_DATA**). Evenzo IoT Hub toohello gegevens verzenden van toodevices als verwijst *berichten*, terwijl Hallo modelleertaal tooit als verwijst *acties* (gedefinieerd met behulp van **WITH_ACTION**). Let erop dat deze voorwaarden door elkaar kunnen worden gebruikt in dit artikel.
> 
> 

### <a name="supported-data-types"></a>Ondersteunde gegevenstypen
Hallo volgende gegevenstypen worden ondersteund in modellen die zijn gemaakt met de Hallo **serialisatiefunctie** bibliotheek:

| Type | Beschrijving |
| --- | --- |
| dubbele |dubbele precisiegetal met drijvende komma |
| int |32-bits geheel getal |
| Float |drijvende-kommagetal met enkele precisie |
| lang |lang geheel getal |
| int8\_t |8-bits geheel getal |
| Int16\_t |16-bits geheel getal |
| Int32\_t |32-bits geheel getal |
| Int64\_t |64-bits geheel getal |
| BOOL |Booleaanse waarde |
| ASCII\_char\_ptr |ASCII-tekenreeks |
| EDM\_DATUM\_TIJD\_OFFSET |datum tijdverschil |
| EDM\_GUID |GUID |
| EDM\_BINAIRE |Binaire |
| DECLAREREN\_STRUCT |complex gegevenstype |

Laten we beginnen met de laatste gegevenstype Hallo. Hallo **DECLARE\_STRUCT** kunt u toodefine complexe gegevenstypen, dat wil zeggen groepen Hallo andere primitieve typen. Deze groeperingen kunnen we toodefine een model dat er als volgt uit:

```
DECLARE_STRUCT(TestType,
double, aDouble,
int, aInt,
float, aFloat,
long, aLong,
int8_t, aInt8,
uint8_t, auInt8,
int16_t, aInt16,
int32_t, aInt32,
int64_t, aInt64,
bool, aBool,
ascii_char_ptr, aAsciiCharPtr,
EDM_DATE_TIME_OFFSET, aDateTimeOffset,
EDM_GUID, aGuid,
EDM_BINARY, aBinary
);

DECLARE_MODEL(TestModel,
WITH_DATA(TestType, Test)
);
```

Het model bevat een één-gebeurtenis van het type **TestType**. **TestType** is een complex type met verschillende leden die gezamenlijk Hallo primitieve typen ondersteund door Hallo aantonen **serialisatiefunctie** modelleertaal.

We kunnen code toosend gegevens tooIoT Hub die wordt weergegeven als volgt schrijven met een model als volgt:

```
TestModel* testModel = CREATE_MODEL_INSTANCE(MyThermostat, TestModel);

testModel->Test.aDouble = 1.1;
testModel->Test.aInt = 2;
testModel->Test.aFloat = 3.0f;
testModel->Test.aLong = 4;
testModel->Test.aInt8 = 5;
testModel->Test.auInt8 = 6;
testModel->Test.aInt16 = 7;
testModel->Test.aInt32 = 8;
testModel->Test.aInt64 = 9;
testModel->Test.aBool = true;
testModel->Test.aAsciiCharPtr = "ascii string 1";

time_t now;
time(&now);
testModel->Test.aDateTimeOffset = GetDateTimeOffset(now);

EDM_GUID guid = { { 0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0A, 0x0B, 0x0C, 0x0D, 0x0E, 0x0F } };
testModel->Test.aGuid = guid;

unsigned char binaryArray[3] = { 0x01, 0x02, 0x03 };
EDM_BINARY binaryData = { sizeof(binaryArray), &binaryArray };
testModel->Test.aBinary = binaryData;

SendAsync(iotHubClientHandle, (const void*)&(testModel->Test));
```

In principe we waarde tooevery lid zijn van Hallo toewijst **Test** structuur en vervolgens aan te roepen **SendAsync** toosend hello **Test** gegevens gebeurtenis toohello cloud. **SendAsync** is een Help-functie waarmee een tooIoT in één event Hub worden verzonden:

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate hello string
        char* destinationAsString = (char*)malloc(destinationSize + 1);
        if (destinationAsString != NULL)
        {
            memcpy(destinationAsString, destination, destinationSize);
            destinationAsString[destinationSize] = '\0';
            IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromString(destinationAsString);
            if (messageHandle != NULL)
            {
                IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)0);

                IoTHubMessage_Destroy(messageHandle);
            }
            free(destinationAsString);
        }
        free(destination);
    }
}
```

Deze functie serialiseert Hallo bepaalde gegevensgebeurtenis en verzendt het tooIoT Hub met **IoTHubClient\_SendEventAsync**. Dit is dezelfde code die wordt besproken in de vorige artikelen hello (**SendAsync** Hallo logica ingekapseld in een handige functie).

Een andere hulpfunctie gebruikt in de vorige code Hallo is **GetDateTimeOffset**. Deze functie transformeert Hallo gelegenheid naar een waarde van het type **EDM\_datum\_tijd\_OFFSET**:

```
EDM_DATE_TIME_OFFSET GetDateTimeOffset(time_t time)
{
    struct tm newTime;
    gmtime_s(&newTime, &time);
    EDM_DATE_TIME_OFFSET dateTimeOffset;
    dateTimeOffset.dateTime = newTime;
    dateTimeOffset.fractionalSecond = 0;
    dateTimeOffset.hasFractionalSecond = 0;
    dateTimeOffset.hasTimeZone = 0;
    dateTimeOffset.timeZoneHour = 0;
    dateTimeOffset.timeZoneMinute = 0;
    return dateTimeOffset;
}
```

Als u deze code uitvoert, wordt na bericht Hallo tooIoT Hub verzonden:

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

Houd er rekening mee dat Hallo serialisatie JSON die gegenereerd door Hallo Hallo-indeling is is **serialisatiefunctie** bibliotheek. Opmerking dat elk lid van Hallo geserialiseerd JSON-object overeenkomt met leden van Hallo Hallo **TestType** die is gedefinieerd in het model. Hallo ook exact overeenkomen met de waarden in Hallo code gebruikt. Bedenk wel dat de binaire gegevens Hallo base64-gecodeerd is: 'AQID' is Hallo base64-codering van {0x01, 0x02, 0x03}.

In dit voorbeeld demonstreert Hallo voordeel van het gebruik van Hallo **serialisatiefunctie** bibliotheek--Hierdoor kunnen wij toosend JSON toohello cloud zonder tooexplicitly omgaan met serialisatie in onze toepassing. Alle hebben we tooworry over configureert Hallo waarden Hallo data-gebeurtenissen in het model en vervolgens het aanroepen van eenvoudige API's toosend die gebeurtenissen toohello cloud.

Met deze informatie kunt definiëren we modellen die Hallo bereik van de ondersteunde gegevenstypen, met inbegrip van complexe typen (we kan zelfs complexe typen binnen andere complexe typen bevatten) bevatten. Echter hij geserialiseerd JSON die zijn gegenereerd door Hallo in bovenstaand voorbeeld wordt een belangrijk punt. *Hoe* we verzenden van gegevens met Hallo **serialisatiefunctie** bibliotheek bepaalt precies hoe Hallo JSON is samengesteld. Dat bepaald punt wat aan bod naast is.

## <a name="more-about-serialization"></a>Meer informatie over de serialisatie
de vorige sectie Hallo markeert een voorbeeld van uitvoer hello wordt gegenereerd door Hallo **serialisatiefunctie** bibliotheek. In deze sectie wordt uitgelegd hoe Hallo bibliotheek gegevens serialiseert en hoe u dit gedrag van Hallo serialisatie API's kunt bepalen.

In de volgorde tooadvance Hallo bespreking van de serialisatie werkt we met een nieuw model op basis van een thermostaat. Eerst laten we bieden sommige achtergrond op Hallo scenario we tooaddress proberen.

We willen toomodel een thermostaat die temperatuur en vochtigheid meet. Elk gegevensitem gaat toobe tooIoT Hub anders wordt verzonden. Standaard Hallo thermostaat ingresses een gebeurtenis temperatuur elke 2 minuten; een gebeurtenis vochtigheid is ingressed om de 15 minuten. Wanneer beide gebeurtenissen ingressed is, moet deze een tijdstempel dat laat Hallo die Hallo bijbehorende temperatuur zien of vochtigheid werd gemeten.

Dit scenario wordt opgegeven, moet ziet u twee verschillende manieren toomodel Hallo gegevens en Hallo effect dat modellering heeft op Hallo geserialiseerd uitvoer wordt uitgelegd.

### <a name="model-1"></a>Model 1
Hier volgt Hallo eerste versie van een model dat ondersteunt het voorgaande scenario Hallo:

```
BEGIN_NAMESPACE(Contoso);

DECLARE_STRUCT(TemperatureEvent,
int, Temperature,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_STRUCT(HumidityEvent,
int, Humidity,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureEvent, Temperature),
WITH_DATA(HumidityEvent, Humidity)
);

END_NAMESPACE(Contoso);
```

Opmerking Hallo model bevat twee Gegevensgebeurtenissen: **temperatuur** en **vochtigheid**. In tegenstelling tot eerdere voorbeelden Hallo-type van elke gebeurtenis is een structuur gedefinieerd met behulp van **DECLARE\_STRUCT**. **TemperatureEvent** bevat een temperatuurmeting en een tijdstempel; **HumidityEvent** een meting vochtigheid en een tijdstempel bevat. Dit model biedt ons een natuurlijke manier toomodel Hallo-gegevens voor Hallo scenario die hierboven worden beschreven. Wanneer er een gebeurtenis toohello cloud verzendt, sturen ofwel we een temperatuur/tijdstempel of een combinatie van vochtigheid/tijdstempel.

We kunnen een temperatuur gebeurtenis toohello cloud met code zoals Hallo volgende sturen:

```
time_t now;
time(&now);
thermostat->Temperature.Temperature = 75;
thermostat->Temperature.Time = GetDateTimeOffset(now);

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

We je vastgelegde waarden gebruiken voor de temperatuur en vochtigheid in de voorbeeldcode hello, maar Stel dat we daadwerkelijk deze waarden ophaalt door middel van steekproeven Hallo bijbehorende sensoren op Hallo thermostaat.

Hallo bovenstaande code maakt gebruik van Hallo **GetDateTimeOffset** helper die eerder is geïntroduceerd. Om redenen die wissen hoger fungeren zal, scheidt u deze code expliciet Hallo taak serialiseren en Hallo gebeurtenis wordt verzonden. de vorige code Hallo serialiseert Hallo temperatuur gebeurtenis in een buffer. Vervolgens **sendMessage** is een Help-functie (opgenomen in **simplesample\_amqp**) dat verzendt Hallo tooIoT event Hub:

```
static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle != NULL)
    {
        IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId);

        IoTHubMessage_Destroy(messageHandle);
    }
    free((void*)buffer);
}
```

Deze code is een subset van Hallo **SendAsync** helper beschreven in de vorige sectie hello, zodat we won't gaan eroverheen opnieuw hier.

Wanneer we Hallo vorige code toosend Hallo temperatuur gebeurtenis uitvoert, wordt deze geserialiseerde vorm van Hallo gebeurtenis tooIoT Hub verzonden:

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

We bij het verzenden van een temperatuur van type **TemperatureEvent** en die struct bevat een **temperatuur** en **tijd** lid. Dit is rechtstreeks weerspiegeld in Hallo geserialiseerd gegevens.

Op deze manier kunnen we een gebeurtenis vochtigheid met deze code verzenden:

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Hallo geserialiseerd formulier dat tooIoT Hub heeft verzonden, wordt als volgt weergegeven:

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Dit is opnieuw, zoals verwacht.

Met dit model, kunt u voorstellen dat hoe meer gebeurtenissen kunnen eenvoudig worden toegevoegd. U meer structuren met definiëren **DECLARE\_STRUCT**, en de bijbehorende gebeurtenis Hallo opnemen in het Hallo-model gebruiken **WITH\_gegevens**.

Nu gaan we Hallo model wijzigen zodat het Hallo bevat dezelfde gegevens, maar met een andere structuur.

### <a name="model-2"></a>Model 2
Houd rekening met deze alternatieve model toohello een hierboven:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

In dit geval wordt geëlimineerd Hallo **DECLARE\_STRUCT** macro's en eenvoudig hello gegevensitems van ons scenario met eenvoudige typen van Hallo modelleertaal definieert.

Alleen voor Hallo moment Hallo we negeren **tijd** gebeurtenis. Met deze Reserveer hier is Hallo code tooingress **temperatuur**:

```
time_t now;
time(&now);
thermostat->Temperature = 75;

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Deze code verzendt Hallo volgende geserialiseerd tooIoT event Hub:

```
{"Temperature":75}
```

En Hallo-code voor het verzenden van Hallo vochtigheid gebeurtenis ziet er als volgt:

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Deze code verzendt deze tooIoT Hub:

```
{"Humidity":45}
```

Tot nu toe zijn er nog geen verrassingen. Nu gaan we wijzigen hoe we Hallo SERIALISEREN macro gebruiken.

Hallo **SERIALISEREN** macro kunnen meerdere Gegevensgebeurtenissen als argumenten. Hierdoor kunnen ons tooserialize hello **temperatuur** en **vochtigheid** gebeurtenis samen en verzend tooIoT Hub in één aanroep:

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Geschat mogelijk dat Hallo-resultaat van deze code is dat twee gebeurtenissen tooIoT Hub worden verzonden:

[

{{'Temperatuur': 75},

{{'Vochtigheid': 45}

]

Met andere woorden, u verwacht dat deze code dezelfde is Hallo als het verzenden van **temperatuur** en **vochtigheid** afzonderlijk. Is alleen een toopass gemak beide gebeurtenissen te**SERIALISEREN** in Hallo dezelfde aanroep. Dat is echter niet Hallo geval. In plaats daarvan verzendt Hallo bovenstaande code deze gegevens met één gebeurtenis tooIoT Hub:

{{'Temperatuur': 75, 'vochtigheid': 45}

Dit kan het lijken vreemd omdat het model definieert **temperatuur** en **vochtigheid** als twee *afzonderlijke* gebeurtenissen:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Meer toohello-punt niet we deze gebeurtenissen model waar **temperatuur** en **vochtigheid** zijn in Hallo dezelfde structuur:

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

Als we dit model gebruikt, zou worden eenvoudiger toounderstand hoe **temperatuur** en **vochtigheid** zou worden verzonden in Hallo dezelfde bericht geserialiseerd. Echter niet altijd duidelijk waarom het op die manier werkt wanneer u beide Gegevensgebeurtenissen te doorgeeft**SERIALISEREN** met model 2.

Dit gedrag is eenvoudiger toounderstand als u Hallo veronderstellingen die Hallo weet **serialisatiefunctie** bibliotheek aan te brengen. toomake beeld krijgt van dit gaan we back tooour model:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Dit model in objectgeoriënteerde voorwaarden zien. In dit geval wordt een fysiek apparaat (thermostaat) bent modelleren en dat het apparaat bevat kenmerken, zoals **temperatuur** en **vochtigheid**.

We kunnen Hallo volledige status van het model met code zoals Hallo volgende sturen:

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Ervan uitgaande dat Hallo waarden van temperatuur en vochtigheid van tijd worden ingesteld, zou er een gebeurtenis als deze verzonden tooIoT Hub zien:

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Soms wilt u misschien alleen toosend *sommige* eigenschappen van Hallo model toohello cloud (dit is vooral van toepassing als uw model een groot aantal Gegevensgebeurtenissen bevat). Het is nuttig toosend slechts een subset van van Gegevensgebeurtenissen, zoals in het vorige voorbeeld:

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Hiermee wordt precies Hallo gegenereerd dezelfde gebeurtenis geserialiseerd als we hebt gedefinieerd een **TemperatureEvent** met een **temperatuur** en **tijd** lid, net zoals we met model 1. In dit geval zijn kunnen toogenerate exact hello dezelfde geserialiseerd gebeurtenis met behulp van een ander model (model 2), omdat we aangeroepen **SERIALISEREN** op een andere manier.

Hallo belangrijk is dat als u meerdere Gegevensgebeurtenissen te doorgeeft**SERIALISEREN,** en vervolgens wordt ervan uitgegaan dat elke gebeurtenis is een eigenschap in een JSON-object.

Hallo beste aanpak is afhankelijk van u en hoe u nadenken over uw model. Als u 'gebeurtenissen' toohello cloud verzendt en elke gebeurtenis een gedefinieerde set eigenschappen bevat, maakt de eerste benadering Hallo veel zin. In dat geval gebruikt u **DECLARE\_STRUCT** toodefine Hallo structuur van elke gebeurtenis en plaatst deze in uw model Hello **WITH\_gegevens** macro. U verzendt vervolgens elke gebeurtenis zoals we hebben gedaan in Hallo eerste voorbeeld hierboven. In deze benadering u zou alleen doorgeven een één-gebeurtenis te**SERIALISATIEFUNCTIE**.

Als u over uw model op een wijze objectgeoriënteerde nadenkt, vervolgens de tweede oplossing Hallo mogelijk aan de behoeften van u. In dit geval Hallo-elementen gedefinieerd met behulp van **WITH\_gegevens** Hallo 'Eigenschappen' van het object zijn. U kunt de subset van gebeurtenissen te doorgeven**SERIALISEREN** dat u, afhankelijk van hoeveel van uw 'van het object' status gewenste toosend toohello cloud.

Clusterservice aanpak is goed of fout. NET worden weten hoe Hallo **serialisatiefunctie** bibliotheek werkt en kies Hallo modellering benadering die het beste past bij uw behoeften.

## <a name="message-handling"></a>Afhandeling van berichten
Tot nu toe in dit artikel is alleen verzenden gebeurtenissen tooIoT Hub besproken en nog niet opgelost ontvangen van berichten. Hallo reden voor deze bewerking is die wat er moet tooknow over het ontvangen van berichten grotendeels behandeld is in een [eerder artikel](iot-hub-device-sdk-c-intro.md). Intrekken van dat artikel berichten worden verwerkt door de callback-functie van een bericht te registreren:

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

U schrijft vervolgens Hallo callbackfunctie die wordt aangeroepen wanneer een bericht wordt ontvangen:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = EXECUTE_COMMAND_ERROR;
        }
        else
        {
            memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

Deze implementatie van **IoTHubMessage** aanroepen Hallo bepaalde functie voor elke actie in het model. Bijvoorbeeld, als het model is gedefinieerd met deze actie:

```
WITH_ACTION(SetAirResistance, int, Position)
```

U moet een functie met deze handtekening definiëren:

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

**SetAirResistance** wordt aangeroepen wanneer dat bericht tooyour apparaat wordt verzonden.

We nog niet uitgelegd is welke versie Hallo geserialiseerd van bericht lijkt erop nog. Met andere woorden, als u wilt dat toosend een **SetAirResistance** bericht tooyour apparaat, hoe ziet dit eruit?

Als u een bericht tooa apparaat verzendt, zou u dit doen via hello Azure IoT service SDK. Moet u toch tooknow wat een bepaalde actie toosend tooinvoke string. Hallo algemene indeling voor het verzenden van een bericht wordt weergegeven als volgt:

```
{"Name" : "", "Parameters" : "" }
```

U verzendt een geserialiseerde JSON-object met twee eigenschappen: **naam** Hallo-naam van Hallo actie (bericht) en **Parameters** bevat Hallo parameters van deze actie.

Bijvoorbeeld: tooinvoke **SetAirResistance** kunt u dit bericht tooa apparaat verzenden:

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

Hallo actie exact overeenkomt met een actie die is gedefinieerd in het model. Hallo parameternamen moeten ook overeenkomen met. Let ook op hoofdletters en kleine letters. **Naam** en **Parameters** zijn altijd hoofdletters. Zorg ervoor dat toomatch Hallo-aanvraag van de naam van de actie en de parameters in het model. In dit voorbeeld is actienaam Hallo 'SetAirResistance' en niet 'setairresistance'.

twee andere acties Hallo **TurnFanOn** en **TurnFanOff** kan worden aangeroepen door deze berichten tooa apparaat verzenden:

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

Deze sectie beschreven alles wat u moet tooknow wanneer gebeurtenissen verzenden en ontvangen van berichten met Hallo **serialisatiefunctie** bibliotheek. Voordat u doorgaat, gaan we betrekking op bepaalde parameters kunt u configureren die bepalen hoe groot is voor het model.

## <a name="macro-configuration"></a>Macro-configuratie
Als u Hallo **serialisatiefunctie** bibliotheek een belangrijk onderdeel van Hallo SDK toobe op de hoogte van is gevonden in de bibliotheek voor het hello azure-c-gedeeld-hulpprogramma.
Als u hebt gekloond hello Azure-iot-sdk-c-opslagplaats vanuit GitHub Hallo--recursieve wordt gebruikt, ziet u deze gedeelde hulpprogrammabibliotheek:

```
.\\c-utility
```

Als u geen Hallo-bibliotheek hebt gekloond, kun je [hier](https://github.com/Azure/azure-c-shared-utility).

Hallo hulpprogramma gedeelde bibliotheek vindt u Hallo volgende map:

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

Deze map bevat een Visual Studio-oplossing aangeroepen **macro\_utils\_h\_generator.sln**:

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

Hallo-programma in deze oplossing genereert Hallo **macro\_utils.h** bestand. Er is een standaardmacro\_utils.h bestand Hello SDK is opgenomen. Deze oplossing kunt u toomodify sommige parameters en vervolgens opnieuw maken Hallo header-bestand op basis van deze parameters.

Hallo twee belangrijke parameters toobe met bezighoudt zijn **nArithmetic** en **nMacroParameters** die zijn gedefinieerd in deze twee regels gevonden in de macro\_utils.tt:

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

Deze waarden zijn Hallo standaardparameters Hello SDK is opgenomen. Elke parameter heeft Hallo betekenis te volgen:

* nMacroParameters – bepaalt hoeveel parameters die u kunt hebben in een DECLARE\_macrodefinitie MODEL.
* nArithmetic – besturingselementen Hallo totale aantal leden in een model is toegestaan.

Hallo reden die deze parameters belangrijk zijn is omdat ze bepalen hoe groot uw model kan worden. Neem bijvoorbeeld een modeldefinitie voor dit:

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

Zoals eerder vermeld **DECLARE\_MODEL** is slechts een C macro. namen van Hallo model en Hallo Hallo **WITH\_gegevens** instructie (nog een andere macro) zijn parameters van **DECLARE\_MODEL**. **nMacroParameters** definieert hoeveel parameters kunnen worden opgenomen in **DECLARE\_MODEL**. Hiermee definieert effectief, hoeveel gegevens gebeurtenis en actie declaraties u kunt hebben. Als zodanig met Hallo standaardlimiet van 124 betekent dit dat u een model met een combinatie van ongeveer 60 acties en Gegevensgebeurtenissen kunt definiëren. Als u deze limiet tooexceed probeert, ontvangt u compilatiefouten waarmee soortgelijke toothis gezocht:

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

Hallo **nArithmetic** parameter meer over Hallo interne werking van Hallo macrotaal dan uw toepassing is.  Het totale aantal leden die u in uw model hebben kunt Hallo bepaalt inclusief **DECLARE_STRUCT** macro's. Als u beginnen te zien compilatiefouten zoals dit en probeer u moet verhogen **nArithmetic**:

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

Als u deze parameters toochange wilt, wijzigt u de waarden Hallo in Hallo macro\_utils.tt-bestand, recompile Hallo macro\_utils\_h\_generator.sln oplossing en Voer Hallo gecompileerd programma. Als u dit doet, een nieuwe macro\_utils.h bestand is gegenereerd en worden in Hallo.\\ algemene\\inc directory.

In volgorde toouse Hallo nieuwe versie van de macro\_utils.h, verwijder Hallo **serialisatiefunctie** NuGet-pakket van uw oplossing en in plaats daarvan bevatten Hallo **serialisatiefunctie** Visual Studio-project. Hierdoor wordt uw code toocompile tegen de broncode Hallo Hallo serializer-bibliotheek. Dit omvat Hallo bijgewerkt macro\_utils.h. Als u dat wilt toodo voor **simplesample\_amqp**, begin met het verwijderen van Hallo NuGet-pakket voor Hallo serialisatiefunctie bibliotheek uit Hallo-oplossing:

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

Voeg dit project tooyour Visual Studio-oplossing:

> . \\c\\serialisatiefunctie\\bouwen\\windows\\serializer.vcxproj
> 
> 

Wanneer u bent klaar, ziet uw oplossing als volgt:

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

Nu macro wanneer u compileert uw oplossing hello bijgewerkt\_utils.h is opgenomen in uw binary.

Houd er rekening mee dat deze waarden hoog genoeg verhogen compiler overschrijden kunt. toothis aanwijst, hello **nMacroParameters** Hallo belangrijkste parameter met welke toobe betrokken is. Hallo C99 spec geeft aan dat een minimum van 127 parameters zijn toegestaan in een macrodefinitie van de. Hallo Microsoft compiler Hallo spec precies volgt (en kent een limiet van 127), zodat u niet kunt tooincrease **nMacroParameters** tot meer dan Hallo standaardwaarde. Andere compilers kunt u mogelijk toodo dus (bijvoorbeeld Hallo GNU compiler een hogere limiet ondersteunt).

Tot nu toe hebben we behandeld bijna alles wat u tooknow moet over hoe toowrite code Hello **serialisatiefunctie** bibliotheek. Vóór de sluiting, bezoekt u gaan we een aantal onderwerpen uit eerdere artikelen die u vraagt zich misschien af over.

## <a name="hello-lower-level-apis"></a>Hallo lager niveau API's
Hallo-voorbeeldtoepassing waarop dit artikel gericht is **simplesample\_amqp**. Dit voorbeeld gebruikt Hallo een hoger niveau (Hallo niet-' LLE ") API's toosend gebeurtenissen en ontvangen van berichten. Als u deze API's gebruikt, wordt een achtergrond-thread wordt uitgevoerd die zorgt voor zowel het verzenden van gebeurtenissen en ontvangen van berichten. Echter, u kunt gebruiken Hallo lager niveau (ES) API's tooeliminate deze achtergrondthread en besturen expliciete wanneer u gebeurtenissen verzenden of ontvangen van berichten van Hallo cloud.

Zoals beschreven in een [vorige artikel](iot-hub-device-sdk-c-iothubclient.md), er is een reeks functies die uit het Hallo bestaat-API's een hoger niveau:

* IoTHubClient\_CreateFromConnectionString
* IoTHubClient\_SendEventAsync
* IoTHubClient\_SetMessageCallback
* IoTHubClient\_vernietigen

Deze API's worden uitgelegd **simplesample\_amqp**.

Er is ook een vergelijkbare reeks API's van lager niveau.

* IoTHubClient\_LLE\_CreateFromConnectionString
* IoTHubClient\_LLE\_SendEventAsync
* IoTHubClient\_LLE\_SetMessageCallback
* IoTHubClient\_LLE\_vernietigen

Opmerking dat Hallo lager niveau API's werk exact Hallo dezelfde manier zoals beschreven in de vorige artikelen Hallo. U kunt Hallo eerste set API's gebruiken als u wilt dat een achtergrond-thread toohandle gebeurtenissen verzenden en ontvangen van berichten. U Hallo tweede reeks API's gebruiken als u wilt dat expliciete controle over wanneer u gegevens verzenden en ontvangen van IoT Hub. Een reeks API's werken net zo goed met Hallo **serialisatiefunctie** bibliotheek.

Voor een voorbeeld van hoe hello lager niveau API's worden gebruikt met Hallo **serialisatiefunctie** bibliotheek, Zie Hallo **simplesample\_http** toepassing.

## <a name="additional-topics"></a>Extra onderwerpen
Enkele andere onderwerpen opgemerkt zijn opnieuw eigendom verwerken, met behulp van alternatieve inloggegevens en configuratieopties. Dit zijn alle onderwerpen in een [vorige artikel](iot-hub-device-sdk-c-iothubclient.md). Hallo belangrijkste is dat al deze functies in Hallo dezelfde werken manier Hello **serialisatiefunctie** bibliotheek als met de Hallo **IoTHubClient** bibliotheek. Bijvoorbeeld, als u tooattach eigenschappen tooan gebeurtenis uit het model wilt, u **IoTHubMessage\_eigenschappen** en **kaart**\_**AddorUpdate**, Hallo op dezelfde manier zoals eerder beschreven:

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Of Hallo gebeurtenis is gegenereerd op basis van Hallo **serialisatiefunctie** bibliotheek of gemaakt handmatig met Hallo **IoTHubClient** bibliotheek maakt niet uit.

Alternatieve voor Hallo apparaat referenties, met behulp van **IoTHubClient\_LLE\_maken** net zo goed werkt als **IoTHubClient\_CreateFromConnectionString** voor toewijzen van een **IOTHUB\_CLIENT\_verwerken**.

Ten slotte, als u Hallo **serialisatiefunctie** bibliotheek, kunt u configuratieopties met instellen **IoTHubClient\_LLE\_SetOption** net zoals u deed bij gebruik van Hallo **IoTHubClient** bibliotheek.

Een functie die de unieke toohello **serialisatiefunctie** bibliotheek Hallo initialisatie API's zijn. Voordat u met Hallo bibliotheek werken beginnen kunt, moet u aanroepen **serialisatiefunctie\_init**:

```
serializer_init(NULL);
```

Dit wordt gedaan vlak voordat u aanroepen **IoTHubClient\_CreateFromConnectionString**.

Op dezelfde manier als u klaar bent met Hallo bibliotheek werken, de laatste aanroep Hallo u maakt is te**serialisatiefunctie\_deinit**:

```
serializer_deinit();
```

Anders wordt alle andere functies die hierboven worden genoemd Hallo werk Hallo dezelfde in Hallo **serialisatiefunctie** bibliotheek als in Hallo **IoTHubClient** bibliotheek. Zie voor meer informatie over deze onderwerpen Hallo [vorige artikel](iot-hub-device-sdk-c-iothubclient.md) in deze reeks.

## <a name="next-steps"></a>Volgende stappen
Dit artikel wordt beschreven in detail Hallo unieke aspecten van Hallo **serialisatiefunctie** bibliotheek opgenomen in Hallo **Azure IoT-device SDK voor C**. Met geleverde Hallo informatie moet u goed begrijpt hoe toouse toosend gebeurtenissen modellen hebben en ontvangen van berichten uit IoT Hub.

Hiermee ook Hallo driedelige reeks in hoe toodevelop toepassingen met Hallo is **Azure IoT-device SDK voor C**. Dit moet worden voldoende informatie toonot alleen get die u gestart, maar bieden u een grondig begrip over de werking van Hallo API's. Voor meer informatie, moet u er een paar voorbeelden zijn in Hallo die SDK niet ingegaan. Anders Hallo [SDK-documentatie](https://github.com/Azure/azure-iot-sdk-c) is een goede bron voor meer informatie.

toolearn meer informatie over het ontwikkelen voor IoT Hub, Zie Hallo [Azure IoT SDK's][lnk-sdks].

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Een apparaat simuleren met Azure IoT rand][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

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
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="81d82-103">Azure IoT-apparaat SDK voor C: meer informatie over de serialisatiefunctie</span><span class="sxs-lookup"><span data-stu-id="81d82-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="81d82-104">Hallo [eerst artikel](iot-hub-device-sdk-c-intro.md) in deze reeks geïntroduceerd Hallo **Azure IoT-device SDK voor C**. het volgende artikel Hallo opgegeven een gedetailleerdere beschrijving van Hallo [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="81d82-104">hello [first article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C**. hello next article provided a more detailed description of hello [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="81d82-105">In dit artikel is dekking Hallo SDK voltooid door een gedetailleerdere beschrijving van de resterende onderdeel Hallo: Hallo **serialisatiefunctie** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="81d82-105">This article completes coverage of hello SDK by providing a more detailed description of hello remaining component: hello **serializer** library.</span></span>

<span data-ttu-id="81d82-106">Hallo inleidende artikel wordt beschreven hoe toouse hello **serialisatiefunctie** bibliotheek toosend gebeurtenissen tooand ontvangen berichten uit IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="81d82-106">hello introductory article described how toouse hello **serializer** library toosend events tooand receive messages from IoT Hub.</span></span> <span data-ttu-id="81d82-107">In dit artikel we die discussie uitbreiden door te geven van een uitgebreidere uitleg van de werking toomodel uw gegevens met Hallo **serialisatiefunctie** macrotaal.</span><span class="sxs-lookup"><span data-stu-id="81d82-107">In this article, we extend that discussion by providing a more complete explanation of how toomodel your data with hello **serializer** macro language.</span></span> <span data-ttu-id="81d82-108">Hallo artikel bevat ook meer informatie over hoe Hallo bibliotheek berichten serialiseert (en in sommige gevallen hoe u kunt bepalen Hallo serialisatie gedrag).</span><span class="sxs-lookup"><span data-stu-id="81d82-108">hello article also includes more detail about how hello library serializes messages (and in some cases how you can control hello serialization behavior).</span></span> <span data-ttu-id="81d82-109">We beschrijven ook bepaalde parameters die kunt u wijzigen om te bepalen Hallo grootte van Hallo modellen die u maakt.</span><span class="sxs-lookup"><span data-stu-id="81d82-109">We'll also describe some parameters you can modify that determine hello size of hello models you create.</span></span>

<span data-ttu-id="81d82-110">Ten slotte revisits Hallo artikel sommige onderwerpen in de vorige artikelen zoals bericht en de verwerking van de eigenschap.</span><span class="sxs-lookup"><span data-stu-id="81d82-110">Finally, hello article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="81d82-111">Als we vinden uit deze werken in dezelfde manier met Hallo Hallo **serialisatiefunctie** bibliotheek als met de Hallo **IoTHubClient** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="81d82-111">As we'll find out, those features work in hello same way using hello **serializer** library as they do with hello **IoTHubClient** library.</span></span>

<span data-ttu-id="81d82-112">Alles dat wordt beschreven in dit artikel is gebaseerd op Hallo **serialisatiefunctie** SDK-voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="81d82-112">Everything described in this article is based on hello **serializer** SDK samples.</span></span> <span data-ttu-id="81d82-113">Als u toofollow langs wilt, raadpleegt u Hallo **simplesample\_amqp** en **simplesample\_http** toepassingen die zijn opgenomen in hello Azure IoT-device SDK voor C.</span><span class="sxs-lookup"><span data-stu-id="81d82-113">If you want toofollow along, see hello **simplesample\_amqp** and **simplesample\_http** applications included in hello Azure IoT device SDK for C.</span></span>

<span data-ttu-id="81d82-114">U vindt Hallo [ **Azure IoT-device SDK voor C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub-opslagplaats en de weergave details van Hallo API in Hallo [C-API-referentiemateriaal](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="81d82-114">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="hello-modeling-language"></a><span data-ttu-id="81d82-115">Hallo modelleertaal</span><span class="sxs-lookup"><span data-stu-id="81d82-115">hello modeling language</span></span>
<span data-ttu-id="81d82-116">Hallo [inleidende artikel](iot-hub-device-sdk-c-intro.md) in deze reeks geïntroduceerd Hallo **Azure IoT-device SDK voor C** modelleertaal via Hallo voorbeeld in Hallo **simplesample\_amqp**  toepassing:</span><span class="sxs-lookup"><span data-stu-id="81d82-116">hello [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C** modeling language through hello example provided in hello **simplesample\_amqp** application:</span></span>

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

<span data-ttu-id="81d82-117">Zoals u ziet, is Hallo modelleertaal gebaseerd op C macro's.</span><span class="sxs-lookup"><span data-stu-id="81d82-117">As you can see, hello modeling language is based on C macros.</span></span> <span data-ttu-id="81d82-118">De definitie van de met beginnen altijd **BEGIN\_NAAMRUIMTE** en altijd eindigen met **END\_NAAMRUIMTE**.</span><span class="sxs-lookup"><span data-stu-id="81d82-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="81d82-119">Hallo naamruimte voor uw bedrijf of, net zoals in dit voorbeeld Hallo-project dat u met werkt een algemene tooname is.</span><span class="sxs-lookup"><span data-stu-id="81d82-119">It's common tooname hello namespace for your company or, as in this example, hello project that you're working on.</span></span>

<span data-ttu-id="81d82-120">Wat komt binnen Hallo naamruimte model definities zijn.</span><span class="sxs-lookup"><span data-stu-id="81d82-120">What goes inside hello namespace are model definitions.</span></span> <span data-ttu-id="81d82-121">In dit geval is er één model voor een anemometer.</span><span class="sxs-lookup"><span data-stu-id="81d82-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="81d82-122">Nogmaals Hallo model kan worden benoemd alles, maar doorgaans dit heet Hallo-apparaat of type gegevens dat u wilt tooexchange met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="81d82-122">Once again, hello model can be named anything, but typically this is named for hello device or type of data you want tooexchange with IoT Hub.</span></span>  

<span data-ttu-id="81d82-123">Modellen een definitie bevatten van Hallo gebeurtenissen kunt u inkomend tooIoT Hub (Hallo *gegevens*) en het Hallo-berichten uit IoT Hub kunt u ontvangen (Hallo *acties*).</span><span class="sxs-lookup"><span data-stu-id="81d82-123">Models contain a definition of hello events you can ingress tooIoT Hub (hello *data*) as well as hello messages you can receive from IoT Hub (hello *actions*).</span></span> <span data-ttu-id="81d82-124">Als u in het Hallo-voorbeeld zien kunt, hebben gebeurtenissen een type en een naam; acties hebben een naam en optionele parameters (elk met een type).</span><span class="sxs-lookup"><span data-stu-id="81d82-124">As you can see from hello example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="81d82-125">Wat wordt niet gedemonstreerd in dit voorbeeld zijn extra gegevenstypen die worden ondersteund door Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="81d82-125">What’s not demonstrated in this sample are additional data types that are supported by hello SDK.</span></span> <span data-ttu-id="81d82-126">Aan bod om het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="81d82-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="81d82-127">IoT Hub verwijst toohello gegevens een apparaat tooit als verzendt *gebeurtenissen*, terwijl Hallo modelleertaal tooit als verwijst *gegevens* (gedefinieerd met behulp van **WITH_DATA**).</span><span class="sxs-lookup"><span data-stu-id="81d82-127">IoT Hub refers toohello data a device sends tooit as *events*, while hello modeling language refers tooit as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="81d82-128">Evenzo IoT Hub toohello gegevens verzenden van toodevices als verwijst *berichten*, terwijl Hallo modelleertaal tooit als verwijst *acties* (gedefinieerd met behulp van **WITH_ACTION**).</span><span class="sxs-lookup"><span data-stu-id="81d82-128">Likewise, IoT Hub refers toohello data you send toodevices as *messages*, while hello modeling language refers tooit as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="81d82-129">Let erop dat deze voorwaarden door elkaar kunnen worden gebruikt in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="81d82-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="81d82-130">Ondersteunde gegevenstypen</span><span class="sxs-lookup"><span data-stu-id="81d82-130">Supported data types</span></span>
<span data-ttu-id="81d82-131">Hallo volgende gegevenstypen worden ondersteund in modellen die zijn gemaakt met de Hallo **serialisatiefunctie** bibliotheek:</span><span class="sxs-lookup"><span data-stu-id="81d82-131">hello following data types are supported in models created with hello **serializer** library:</span></span>

| <span data-ttu-id="81d82-132">Type</span><span class="sxs-lookup"><span data-stu-id="81d82-132">Type</span></span> | <span data-ttu-id="81d82-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="81d82-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="81d82-134">dubbele</span><span class="sxs-lookup"><span data-stu-id="81d82-134">double</span></span> |<span data-ttu-id="81d82-135">dubbele precisiegetal met drijvende komma</span><span class="sxs-lookup"><span data-stu-id="81d82-135">double precision floating point number</span></span> |
| <span data-ttu-id="81d82-136">int</span><span class="sxs-lookup"><span data-stu-id="81d82-136">int</span></span> |<span data-ttu-id="81d82-137">32-bits geheel getal</span><span class="sxs-lookup"><span data-stu-id="81d82-137">32 bit integer</span></span> |
| <span data-ttu-id="81d82-138">Float</span><span class="sxs-lookup"><span data-stu-id="81d82-138">float</span></span> |<span data-ttu-id="81d82-139">drijvende-kommagetal met enkele precisie</span><span class="sxs-lookup"><span data-stu-id="81d82-139">single precision floating point number</span></span> |
| <span data-ttu-id="81d82-140">lang</span><span class="sxs-lookup"><span data-stu-id="81d82-140">long</span></span> |<span data-ttu-id="81d82-141">lang geheel getal</span><span class="sxs-lookup"><span data-stu-id="81d82-141">long integer</span></span> |
| <span data-ttu-id="81d82-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="81d82-142">int8\_t</span></span> |<span data-ttu-id="81d82-143">8-bits geheel getal</span><span class="sxs-lookup"><span data-stu-id="81d82-143">8 bit integer</span></span> |
| <span data-ttu-id="81d82-144">Int16\_t</span><span class="sxs-lookup"><span data-stu-id="81d82-144">int16\_t</span></span> |<span data-ttu-id="81d82-145">16-bits geheel getal</span><span class="sxs-lookup"><span data-stu-id="81d82-145">16 bit integer</span></span> |
| <span data-ttu-id="81d82-146">Int32\_t</span><span class="sxs-lookup"><span data-stu-id="81d82-146">int32\_t</span></span> |<span data-ttu-id="81d82-147">32-bits geheel getal</span><span class="sxs-lookup"><span data-stu-id="81d82-147">32 bit integer</span></span> |
| <span data-ttu-id="81d82-148">Int64\_t</span><span class="sxs-lookup"><span data-stu-id="81d82-148">int64\_t</span></span> |<span data-ttu-id="81d82-149">64-bits geheel getal</span><span class="sxs-lookup"><span data-stu-id="81d82-149">64 bit integer</span></span> |
| <span data-ttu-id="81d82-150">BOOL</span><span class="sxs-lookup"><span data-stu-id="81d82-150">bool</span></span> |<span data-ttu-id="81d82-151">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="81d82-151">boolean</span></span> |
| <span data-ttu-id="81d82-152">ASCII\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="81d82-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="81d82-153">ASCII-tekenreeks</span><span class="sxs-lookup"><span data-stu-id="81d82-153">ASCII string</span></span> |
| <span data-ttu-id="81d82-154">EDM\_DATUM\_TIJD\_OFFSET</span><span class="sxs-lookup"><span data-stu-id="81d82-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="81d82-155">datum tijdverschil</span><span class="sxs-lookup"><span data-stu-id="81d82-155">date time offset</span></span> |
| <span data-ttu-id="81d82-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="81d82-156">EDM\_GUID</span></span> |<span data-ttu-id="81d82-157">GUID</span><span class="sxs-lookup"><span data-stu-id="81d82-157">GUID</span></span> |
| <span data-ttu-id="81d82-158">EDM\_BINAIRE</span><span class="sxs-lookup"><span data-stu-id="81d82-158">EDM\_BINARY</span></span> |<span data-ttu-id="81d82-159">Binaire</span><span class="sxs-lookup"><span data-stu-id="81d82-159">binary</span></span> |
| <span data-ttu-id="81d82-160">DECLAREREN\_STRUCT</span><span class="sxs-lookup"><span data-stu-id="81d82-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="81d82-161">complex gegevenstype</span><span class="sxs-lookup"><span data-stu-id="81d82-161">complex data type</span></span> |

<span data-ttu-id="81d82-162">Laten we beginnen met de laatste gegevenstype Hallo.</span><span class="sxs-lookup"><span data-stu-id="81d82-162">Let’s start with hello last data type.</span></span> <span data-ttu-id="81d82-163">Hallo **DECLARE\_STRUCT** kunt u toodefine complexe gegevenstypen, dat wil zeggen groepen Hallo andere primitieve typen.</span><span class="sxs-lookup"><span data-stu-id="81d82-163">hello **DECLARE\_STRUCT** allows you toodefine complex data types, which are groupings of hello other primitive types.</span></span> <span data-ttu-id="81d82-164">Deze groeperingen kunnen we toodefine een model dat er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="81d82-164">These groupings allow us toodefine a model that looks like this:</span></span>

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

<span data-ttu-id="81d82-165">Het model bevat een één-gebeurtenis van het type **TestType**.</span><span class="sxs-lookup"><span data-stu-id="81d82-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="81d82-166">**TestType** is een complex type met verschillende leden die gezamenlijk Hallo primitieve typen ondersteund door Hallo aantonen **serialisatiefunctie** modelleertaal.</span><span class="sxs-lookup"><span data-stu-id="81d82-166">**TestType** is a complex type that includes several members, which collectively demonstrate hello primitive types supported by hello **serializer** modeling language.</span></span>

<span data-ttu-id="81d82-167">We kunnen code toosend gegevens tooIoT Hub die wordt weergegeven als volgt schrijven met een model als volgt:</span><span class="sxs-lookup"><span data-stu-id="81d82-167">With a model like this, we can write code toosend data tooIoT Hub that appears as follows:</span></span>

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

<span data-ttu-id="81d82-168">In principe we waarde tooevery lid zijn van Hallo toewijst **Test** structuur en vervolgens aan te roepen **SendAsync** toosend hello **Test** gegevens gebeurtenis toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="81d82-168">Basically, we’re assigning a value tooevery member of hello **Test** structure and then calling **SendAsync** toosend hello **Test** data event toohello cloud.</span></span> <span data-ttu-id="81d82-169">**SendAsync** is een Help-functie waarmee een tooIoT in één event Hub worden verzonden:</span><span class="sxs-lookup"><span data-stu-id="81d82-169">**SendAsync** is a helper function that sends a single data event tooIoT Hub:</span></span>

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

<span data-ttu-id="81d82-170">Deze functie serialiseert Hallo bepaalde gegevensgebeurtenis en verzendt het tooIoT Hub met **IoTHubClient\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="81d82-170">This function serializes hello given data event and sends it tooIoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="81d82-171">Dit is dezelfde code die wordt besproken in de vorige artikelen hello (**SendAsync** Hallo logica ingekapseld in een handige functie).</span><span class="sxs-lookup"><span data-stu-id="81d82-171">This is hello same code discussed in previous articles (**SendAsync** encapsulates hello logic into a convenient function).</span></span>

<span data-ttu-id="81d82-172">Een andere hulpfunctie gebruikt in de vorige code Hallo is **GetDateTimeOffset**.</span><span class="sxs-lookup"><span data-stu-id="81d82-172">One other helper function used in hello previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="81d82-173">Deze functie transformeert Hallo gelegenheid naar een waarde van het type **EDM\_datum\_tijd\_OFFSET**:</span><span class="sxs-lookup"><span data-stu-id="81d82-173">This function transforms hello given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

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

<span data-ttu-id="81d82-174">Als u deze code uitvoert, wordt na bericht Hallo tooIoT Hub verzonden:</span><span class="sxs-lookup"><span data-stu-id="81d82-174">If you run this code, hello following message is sent tooIoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="81d82-175">Houd er rekening mee dat Hallo serialisatie JSON die gegenereerd door Hallo Hallo-indeling is is **serialisatiefunctie** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="81d82-175">Note that hello serialization is JSON, which is hello format generated by hello **serializer** library.</span></span> <span data-ttu-id="81d82-176">Opmerking dat elk lid van Hallo geserialiseerd JSON-object overeenkomt met leden van Hallo Hallo **TestType** die is gedefinieerd in het model.</span><span class="sxs-lookup"><span data-stu-id="81d82-176">Also note that each member of hello serialized JSON object matches hello members of hello **TestType** that we defined in our model.</span></span> <span data-ttu-id="81d82-177">Hallo ook exact overeenkomen met de waarden in Hallo code gebruikt.</span><span class="sxs-lookup"><span data-stu-id="81d82-177">hello values also exactly match those used in hello code.</span></span> <span data-ttu-id="81d82-178">Bedenk wel dat de binaire gegevens Hallo base64-gecodeerd is: 'AQID' is Hallo base64-codering van {0x01, 0x02, 0x03}.</span><span class="sxs-lookup"><span data-stu-id="81d82-178">However, note that hello binary data is base64-encoded: "AQID" is hello base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="81d82-179">In dit voorbeeld demonstreert Hallo voordeel van het gebruik van Hallo **serialisatiefunctie** bibliotheek--Hierdoor kunnen wij toosend JSON toohello cloud zonder tooexplicitly omgaan met serialisatie in onze toepassing.</span><span class="sxs-lookup"><span data-stu-id="81d82-179">This example demonstrates hello advantage of using hello **serializer** library -- it enables us toosend JSON toohello cloud, without having tooexplicitly deal with serialization in our application.</span></span> <span data-ttu-id="81d82-180">Alle hebben we tooworry over configureert Hallo waarden Hallo data-gebeurtenissen in het model en vervolgens het aanroepen van eenvoudige API's toosend die gebeurtenissen toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="81d82-180">All we have tooworry about is setting hello values of hello data events in our model and then calling simple APIs toosend those events toohello cloud.</span></span>

<span data-ttu-id="81d82-181">Met deze informatie kunt definiëren we modellen die Hallo bereik van de ondersteunde gegevenstypen, met inbegrip van complexe typen (we kan zelfs complexe typen binnen andere complexe typen bevatten) bevatten.</span><span class="sxs-lookup"><span data-stu-id="81d82-181">With this information, we can define models that include hello range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="81d82-182">Echter hij geserialiseerd JSON die zijn gegenereerd door Hallo in bovenstaand voorbeeld wordt een belangrijk punt.</span><span class="sxs-lookup"><span data-stu-id="81d82-182">However, he serialized JSON generated by hello example above brings up an important point.</span></span> <span data-ttu-id="81d82-183">*Hoe* we verzenden van gegevens met Hallo **serialisatiefunctie** bibliotheek bepaalt precies hoe Hallo JSON is samengesteld.</span><span class="sxs-lookup"><span data-stu-id="81d82-183">*How* we send data with hello **serializer** library determines exactly how hello JSON is formed.</span></span> <span data-ttu-id="81d82-184">Dat bepaald punt wat aan bod naast is.</span><span class="sxs-lookup"><span data-stu-id="81d82-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="81d82-185">Meer informatie over de serialisatie</span><span class="sxs-lookup"><span data-stu-id="81d82-185">More about serialization</span></span>
<span data-ttu-id="81d82-186">de vorige sectie Hallo markeert een voorbeeld van uitvoer hello wordt gegenereerd door Hallo **serialisatiefunctie** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="81d82-186">hello previous section highlights an example of hello output generated by hello **serializer** library.</span></span> <span data-ttu-id="81d82-187">In deze sectie wordt uitgelegd hoe Hallo bibliotheek gegevens serialiseert en hoe u dit gedrag van Hallo serialisatie API's kunt bepalen.</span><span class="sxs-lookup"><span data-stu-id="81d82-187">In this section, we'll explain how hello library serializes data and how you can control that behavior using hello serialization APIs.</span></span>

<span data-ttu-id="81d82-188">In de volgorde tooadvance Hallo bespreking van de serialisatie werkt we met een nieuw model op basis van een thermostaat.</span><span class="sxs-lookup"><span data-stu-id="81d82-188">In order tooadvance hello discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="81d82-189">Eerst laten we bieden sommige achtergrond op Hallo scenario we tooaddress proberen.</span><span class="sxs-lookup"><span data-stu-id="81d82-189">First, let's provide some background on hello scenario we're trying tooaddress.</span></span>

<span data-ttu-id="81d82-190">We willen toomodel een thermostaat die temperatuur en vochtigheid meet.</span><span class="sxs-lookup"><span data-stu-id="81d82-190">We want toomodel a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="81d82-191">Elk gegevensitem gaat toobe tooIoT Hub anders wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="81d82-191">Each piece of data is going toobe sent tooIoT Hub differently.</span></span> <span data-ttu-id="81d82-192">Standaard Hallo thermostaat ingresses een gebeurtenis temperatuur elke 2 minuten; een gebeurtenis vochtigheid is ingressed om de 15 minuten.</span><span class="sxs-lookup"><span data-stu-id="81d82-192">By default, hello thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="81d82-193">Wanneer beide gebeurtenissen ingressed is, moet deze een tijdstempel dat laat Hallo die Hallo bijbehorende temperatuur zien of vochtigheid werd gemeten.</span><span class="sxs-lookup"><span data-stu-id="81d82-193">When either event is ingressed, it must include a timestamp that shows hello time that hello corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="81d82-194">Dit scenario wordt opgegeven, moet ziet u twee verschillende manieren toomodel Hallo gegevens en Hallo effect dat modellering heeft op Hallo geserialiseerd uitvoer wordt uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="81d82-194">Given this scenario, we'll demonstrate two different ways toomodel hello data, and we'll explain hello effect that modeling has on hello serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="81d82-195">Model 1</span><span class="sxs-lookup"><span data-stu-id="81d82-195">Model 1</span></span>
<span data-ttu-id="81d82-196">Hier volgt Hallo eerste versie van een model dat ondersteunt het voorgaande scenario Hallo:</span><span class="sxs-lookup"><span data-stu-id="81d82-196">Here's hello first version of a model that supports hello previous scenario:</span></span>

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

<span data-ttu-id="81d82-197">Opmerking Hallo model bevat twee Gegevensgebeurtenissen: **temperatuur** en **vochtigheid**.</span><span class="sxs-lookup"><span data-stu-id="81d82-197">Note that hello model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="81d82-198">In tegenstelling tot eerdere voorbeelden Hallo-type van elke gebeurtenis is een structuur gedefinieerd met behulp van **DECLARE\_STRUCT**.</span><span class="sxs-lookup"><span data-stu-id="81d82-198">Unlike previous examples, hello type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="81d82-199">**TemperatureEvent** bevat een temperatuurmeting en een tijdstempel; **HumidityEvent** een meting vochtigheid en een tijdstempel bevat.</span><span class="sxs-lookup"><span data-stu-id="81d82-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="81d82-200">Dit model biedt ons een natuurlijke manier toomodel Hallo-gegevens voor Hallo scenario die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="81d82-200">This model gives us a natural way toomodel hello data for hello scenario described above.</span></span> <span data-ttu-id="81d82-201">Wanneer er een gebeurtenis toohello cloud verzendt, sturen ofwel we een temperatuur/tijdstempel of een combinatie van vochtigheid/tijdstempel.</span><span class="sxs-lookup"><span data-stu-id="81d82-201">When we send an event toohello cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="81d82-202">We kunnen een temperatuur gebeurtenis toohello cloud met code zoals Hallo volgende sturen:</span><span class="sxs-lookup"><span data-stu-id="81d82-202">We can send a temperature event toohello cloud using code such as hello following:</span></span>

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

<span data-ttu-id="81d82-203">We je vastgelegde waarden gebruiken voor de temperatuur en vochtigheid in de voorbeeldcode hello, maar Stel dat we daadwerkelijk deze waarden ophaalt door middel van steekproeven Hallo bijbehorende sensoren op Hallo thermostaat.</span><span class="sxs-lookup"><span data-stu-id="81d82-203">We'll use hard-coded values for temperature and humidity in hello sample code, but imagine that we’re actually retrieving these values by sampling hello corresponding sensors on hello thermostat.</span></span>

<span data-ttu-id="81d82-204">Hallo bovenstaande code maakt gebruik van Hallo **GetDateTimeOffset** helper die eerder is geïntroduceerd.</span><span class="sxs-lookup"><span data-stu-id="81d82-204">hello code above uses hello **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="81d82-205">Om redenen die wissen hoger fungeren zal, scheidt u deze code expliciet Hallo taak serialiseren en Hallo gebeurtenis wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="81d82-205">For reasons that will become clear later, this code explicitly separates hello task of serializing and sending hello event.</span></span> <span data-ttu-id="81d82-206">de vorige code Hallo serialiseert Hallo temperatuur gebeurtenis in een buffer.</span><span class="sxs-lookup"><span data-stu-id="81d82-206">hello previous code serializes hello temperature event into a buffer.</span></span> <span data-ttu-id="81d82-207">Vervolgens **sendMessage** is een Help-functie (opgenomen in **simplesample\_amqp**) dat verzendt Hallo tooIoT event Hub:</span><span class="sxs-lookup"><span data-stu-id="81d82-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends hello event tooIoT Hub:</span></span>

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

<span data-ttu-id="81d82-208">Deze code is een subset van Hallo **SendAsync** helper beschreven in de vorige sectie hello, zodat we won't gaan eroverheen opnieuw hier.</span><span class="sxs-lookup"><span data-stu-id="81d82-208">This code is a subset of hello **SendAsync** helper described in hello previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="81d82-209">Wanneer we Hallo vorige code toosend Hallo temperatuur gebeurtenis uitvoert, wordt deze geserialiseerde vorm van Hallo gebeurtenis tooIoT Hub verzonden:</span><span class="sxs-lookup"><span data-stu-id="81d82-209">When we run hello previous code toosend hello Temperature event, this serialized form of hello event is sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="81d82-210">We bij het verzenden van een temperatuur van type **TemperatureEvent** en die struct bevat een **temperatuur** en **tijd** lid.</span><span class="sxs-lookup"><span data-stu-id="81d82-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="81d82-211">Dit is rechtstreeks weerspiegeld in Hallo geserialiseerd gegevens.</span><span class="sxs-lookup"><span data-stu-id="81d82-211">This is directly reflected in hello serialized data.</span></span>

<span data-ttu-id="81d82-212">Op deze manier kunnen we een gebeurtenis vochtigheid met deze code verzenden:</span><span class="sxs-lookup"><span data-stu-id="81d82-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="81d82-213">Hallo geserialiseerd formulier dat tooIoT Hub heeft verzonden, wordt als volgt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="81d82-213">hello serialized form that’s sent tooIoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="81d82-214">Dit is opnieuw, zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="81d82-214">Again, this is as expected.</span></span>

<span data-ttu-id="81d82-215">Met dit model, kunt u voorstellen dat hoe meer gebeurtenissen kunnen eenvoudig worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="81d82-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="81d82-216">U meer structuren met definiëren **DECLARE\_STRUCT**, en de bijbehorende gebeurtenis Hallo opnemen in het Hallo-model gebruiken **WITH\_gegevens**.</span><span class="sxs-lookup"><span data-stu-id="81d82-216">You define more structures using **DECLARE\_STRUCT**, and include hello corresponding event in hello model using **WITH\_DATA**.</span></span>

<span data-ttu-id="81d82-217">Nu gaan we Hallo model wijzigen zodat het Hallo bevat dezelfde gegevens, maar met een andere structuur.</span><span class="sxs-lookup"><span data-stu-id="81d82-217">Now, let’s modify hello model so that it includes hello same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="81d82-218">Model 2</span><span class="sxs-lookup"><span data-stu-id="81d82-218">Model 2</span></span>
<span data-ttu-id="81d82-219">Houd rekening met deze alternatieve model toohello een hierboven:</span><span class="sxs-lookup"><span data-stu-id="81d82-219">Consider this alternative model toohello one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="81d82-220">In dit geval wordt geëlimineerd Hallo **DECLARE\_STRUCT** macro's en eenvoudig hello gegevensitems van ons scenario met eenvoudige typen van Hallo modelleertaal definieert.</span><span class="sxs-lookup"><span data-stu-id="81d82-220">In this case we've eliminated hello **DECLARE\_STRUCT** macros and are simply defining hello data items from our scenario using simple types from hello modeling language.</span></span>

<span data-ttu-id="81d82-221">Alleen voor Hallo moment Hallo we negeren **tijd** gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="81d82-221">Just for hello moment let’s ignore hello **Time** event.</span></span> <span data-ttu-id="81d82-222">Met deze Reserveer hier is Hallo code tooingress **temperatuur**:</span><span class="sxs-lookup"><span data-stu-id="81d82-222">With that aside, here’s hello code tooingress **Temperature**:</span></span>

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

<span data-ttu-id="81d82-223">Deze code verzendt Hallo volgende geserialiseerd tooIoT event Hub:</span><span class="sxs-lookup"><span data-stu-id="81d82-223">This code sends hello following serialized event tooIoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="81d82-224">En Hallo-code voor het verzenden van Hallo vochtigheid gebeurtenis ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="81d82-224">And hello code for sending hello Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="81d82-225">Deze code verzendt deze tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="81d82-225">This code sends this tooIoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="81d82-226">Tot nu toe zijn er nog geen verrassingen.</span><span class="sxs-lookup"><span data-stu-id="81d82-226">So far there are still no surprises.</span></span> <span data-ttu-id="81d82-227">Nu gaan we wijzigen hoe we Hallo SERIALISEREN macro gebruiken.</span><span class="sxs-lookup"><span data-stu-id="81d82-227">Now let's change how we use hello SERIALIZE macro.</span></span>

<span data-ttu-id="81d82-228">Hallo **SERIALISEREN** macro kunnen meerdere Gegevensgebeurtenissen als argumenten.</span><span class="sxs-lookup"><span data-stu-id="81d82-228">hello **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="81d82-229">Hierdoor kunnen ons tooserialize hello **temperatuur** en **vochtigheid** gebeurtenis samen en verzend tooIoT Hub in één aanroep:</span><span class="sxs-lookup"><span data-stu-id="81d82-229">This enables us tooserialize hello **Temperature** and **Humidity** event together and send them tooIoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="81d82-230">Geschat mogelijk dat Hallo-resultaat van deze code is dat twee gebeurtenissen tooIoT Hub worden verzonden:</span><span class="sxs-lookup"><span data-stu-id="81d82-230">You might guess that hello result of this code is that two data events are sent tooIoT Hub:</span></span>

<span data-ttu-id="81d82-231">[</span><span class="sxs-lookup"><span data-stu-id="81d82-231">[</span></span>

<span data-ttu-id="81d82-232">{{'Temperatuur': 75},</span><span class="sxs-lookup"><span data-stu-id="81d82-232">{"Temperature":75},</span></span>

<span data-ttu-id="81d82-233">{{'Vochtigheid': 45}</span><span class="sxs-lookup"><span data-stu-id="81d82-233">{"Humidity":45}</span></span>

<span data-ttu-id="81d82-234">]</span><span class="sxs-lookup"><span data-stu-id="81d82-234">]</span></span>

<span data-ttu-id="81d82-235">Met andere woorden, u verwacht dat deze code dezelfde is Hallo als het verzenden van **temperatuur** en **vochtigheid** afzonderlijk.</span><span class="sxs-lookup"><span data-stu-id="81d82-235">In other words, you might expect that this code is hello same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="81d82-236">Is alleen een toopass gemak beide gebeurtenissen te**SERIALISEREN** in Hallo dezelfde aanroep.</span><span class="sxs-lookup"><span data-stu-id="81d82-236">It’s just a convenience toopass both events too**SERIALIZE** in hello same call.</span></span> <span data-ttu-id="81d82-237">Dat is echter niet Hallo geval.</span><span class="sxs-lookup"><span data-stu-id="81d82-237">However, that’s not hello case.</span></span> <span data-ttu-id="81d82-238">In plaats daarvan verzendt Hallo bovenstaande code deze gegevens met één gebeurtenis tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="81d82-238">Instead, hello code above sends this single data event tooIoT Hub:</span></span>

<span data-ttu-id="81d82-239">{{'Temperatuur': 75, 'vochtigheid': 45}</span><span class="sxs-lookup"><span data-stu-id="81d82-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="81d82-240">Dit kan het lijken vreemd omdat het model definieert **temperatuur** en **vochtigheid** als twee *afzonderlijke* gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="81d82-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="81d82-241">Meer toohello-punt niet we deze gebeurtenissen model waar **temperatuur** en **vochtigheid** zijn in Hallo dezelfde structuur:</span><span class="sxs-lookup"><span data-stu-id="81d82-241">More toohello point, we didn’t model these events where **Temperature** and **Humidity** are in hello same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="81d82-242">Als we dit model gebruikt, zou worden eenvoudiger toounderstand hoe **temperatuur** en **vochtigheid** zou worden verzonden in Hallo dezelfde bericht geserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="81d82-242">If we used this model, it would be easier toounderstand how **Temperature** and **Humidity** would be sent in hello same serialized message.</span></span> <span data-ttu-id="81d82-243">Echter niet altijd duidelijk waarom het op die manier werkt wanneer u beide Gegevensgebeurtenissen te doorgeeft**SERIALISEREN** met model 2.</span><span class="sxs-lookup"><span data-stu-id="81d82-243">However it may not be clear why it works that way when you pass both data events too**SERIALIZE** using model 2.</span></span>

<span data-ttu-id="81d82-244">Dit gedrag is eenvoudiger toounderstand als u Hallo veronderstellingen die Hallo weet **serialisatiefunctie** bibliotheek aan te brengen.</span><span class="sxs-lookup"><span data-stu-id="81d82-244">This behavior is easier toounderstand if you know hello assumptions that hello **serializer** library is making.</span></span> <span data-ttu-id="81d82-245">toomake beeld krijgt van dit gaan we back tooour model:</span><span class="sxs-lookup"><span data-stu-id="81d82-245">toomake sense of this let’s go back tooour model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="81d82-246">Dit model in objectgeoriënteerde voorwaarden zien.</span><span class="sxs-lookup"><span data-stu-id="81d82-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="81d82-247">In dit geval wordt een fysiek apparaat (thermostaat) bent modelleren en dat het apparaat bevat kenmerken, zoals **temperatuur** en **vochtigheid**.</span><span class="sxs-lookup"><span data-stu-id="81d82-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="81d82-248">We kunnen Hallo volledige status van het model met code zoals Hallo volgende sturen:</span><span class="sxs-lookup"><span data-stu-id="81d82-248">We can send hello entire state of our model with code such as hello following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="81d82-249">Ervan uitgaande dat Hallo waarden van temperatuur en vochtigheid van tijd worden ingesteld, zou er een gebeurtenis als deze verzonden tooIoT Hub zien:</span><span class="sxs-lookup"><span data-stu-id="81d82-249">Assuming hello values of Temperature, Humidity and Time are set, we would see an event like this sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="81d82-250">Soms wilt u misschien alleen toosend *sommige* eigenschappen van Hallo model toohello cloud (dit is vooral van toepassing als uw model een groot aantal Gegevensgebeurtenissen bevat).</span><span class="sxs-lookup"><span data-stu-id="81d82-250">Sometimes you may only want toosend *some* properties of hello model toohello cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="81d82-251">Het is nuttig toosend slechts een subset van van Gegevensgebeurtenissen, zoals in het vorige voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="81d82-251">It’s useful toosend only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="81d82-252">Hiermee wordt precies Hallo gegenereerd dezelfde gebeurtenis geserialiseerd als we hebt gedefinieerd een **TemperatureEvent** met een **temperatuur** en **tijd** lid, net zoals we met model 1.</span><span class="sxs-lookup"><span data-stu-id="81d82-252">This generates exactly hello same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="81d82-253">In dit geval zijn kunnen toogenerate exact hello dezelfde geserialiseerd gebeurtenis met behulp van een ander model (model 2), omdat we aangeroepen **SERIALISEREN** op een andere manier.</span><span class="sxs-lookup"><span data-stu-id="81d82-253">In this case we were able toogenerate exactly hello same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="81d82-254">Hallo belangrijk is dat als u meerdere Gegevensgebeurtenissen te doorgeeft**SERIALISEREN,** en vervolgens wordt ervan uitgegaan dat elke gebeurtenis is een eigenschap in een JSON-object.</span><span class="sxs-lookup"><span data-stu-id="81d82-254">hello important point is that if you pass multiple data events too**SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="81d82-255">Hallo beste aanpak is afhankelijk van u en hoe u nadenken over uw model.</span><span class="sxs-lookup"><span data-stu-id="81d82-255">hello best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="81d82-256">Als u 'gebeurtenissen' toohello cloud verzendt en elke gebeurtenis een gedefinieerde set eigenschappen bevat, maakt de eerste benadering Hallo veel zin.</span><span class="sxs-lookup"><span data-stu-id="81d82-256">If you’re sending "events" toohello cloud and each event contains a defined set of properties, then hello first approach makes a lot of sense.</span></span> <span data-ttu-id="81d82-257">In dat geval gebruikt u **DECLARE\_STRUCT** toodefine Hallo structuur van elke gebeurtenis en plaatst deze in uw model Hello **WITH\_gegevens** macro.</span><span class="sxs-lookup"><span data-stu-id="81d82-257">In that case you would use **DECLARE\_STRUCT** toodefine hello structure of each event and then include them in your model with hello **WITH\_DATA** macro.</span></span> <span data-ttu-id="81d82-258">U verzendt vervolgens elke gebeurtenis zoals we hebben gedaan in Hallo eerste voorbeeld hierboven.</span><span class="sxs-lookup"><span data-stu-id="81d82-258">Then you send each event as we did in hello first example above.</span></span> <span data-ttu-id="81d82-259">In deze benadering u zou alleen doorgeven een één-gebeurtenis te**SERIALISATIEFUNCTIE**.</span><span class="sxs-lookup"><span data-stu-id="81d82-259">In this approach you would only pass a single data event too**SERIALIZER**.</span></span>

<span data-ttu-id="81d82-260">Als u over uw model op een wijze objectgeoriënteerde nadenkt, vervolgens de tweede oplossing Hallo mogelijk aan de behoeften van u.</span><span class="sxs-lookup"><span data-stu-id="81d82-260">If you think about your model in an object-oriented fashion, then hello second approach may suit you.</span></span> <span data-ttu-id="81d82-261">In dit geval Hallo-elementen gedefinieerd met behulp van **WITH\_gegevens** Hallo 'Eigenschappen' van het object zijn.</span><span class="sxs-lookup"><span data-stu-id="81d82-261">In this case, hello elements defined using **WITH\_DATA** are hello "properties" of your object.</span></span> <span data-ttu-id="81d82-262">U kunt de subset van gebeurtenissen te doorgeven**SERIALISEREN** dat u, afhankelijk van hoeveel van uw 'van het object' status gewenste toosend toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="81d82-262">You pass whatever subset of events too**SERIALIZE** that you like, depending on how much of your "object’s" state you want toosend toohello cloud.</span></span>

<span data-ttu-id="81d82-263">Clusterservice aanpak is goed of fout.</span><span class="sxs-lookup"><span data-stu-id="81d82-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="81d82-264">NET worden weten hoe Hallo **serialisatiefunctie** bibliotheek werkt en kies Hallo modellering benadering die het beste past bij uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="81d82-264">Just be aware of how hello **serializer** library works, and pick hello modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="81d82-265">Afhandeling van berichten</span><span class="sxs-lookup"><span data-stu-id="81d82-265">Message handling</span></span>
<span data-ttu-id="81d82-266">Tot nu toe in dit artikel is alleen verzenden gebeurtenissen tooIoT Hub besproken en nog niet opgelost ontvangen van berichten.</span><span class="sxs-lookup"><span data-stu-id="81d82-266">So far this article has only discussed sending events tooIoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="81d82-267">Hallo reden voor deze bewerking is die wat er moet tooknow over het ontvangen van berichten grotendeels behandeld is in een [eerder artikel](iot-hub-device-sdk-c-intro.md).</span><span class="sxs-lookup"><span data-stu-id="81d82-267">hello reason for this is that what we need tooknow about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="81d82-268">Intrekken van dat artikel berichten worden verwerkt door de callback-functie van een bericht te registreren:</span><span class="sxs-lookup"><span data-stu-id="81d82-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="81d82-269">U schrijft vervolgens Hallo callbackfunctie die wordt aangeroepen wanneer een bericht wordt ontvangen:</span><span class="sxs-lookup"><span data-stu-id="81d82-269">You then write hello callback function that’s invoked when a message is received:</span></span>

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

<span data-ttu-id="81d82-270">Deze implementatie van **IoTHubMessage** aanroepen Hallo bepaalde functie voor elke actie in het model.</span><span class="sxs-lookup"><span data-stu-id="81d82-270">This implementation of **IoTHubMessage** calls hello specific function for each action in your model.</span></span> <span data-ttu-id="81d82-271">Bijvoorbeeld, als het model is gedefinieerd met deze actie:</span><span class="sxs-lookup"><span data-stu-id="81d82-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="81d82-272">U moet een functie met deze handtekening definiëren:</span><span class="sxs-lookup"><span data-stu-id="81d82-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="81d82-273">**SetAirResistance** wordt aangeroepen wanneer dat bericht tooyour apparaat wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="81d82-273">**SetAirResistance** is then called when that message is sent tooyour device.</span></span>

<span data-ttu-id="81d82-274">We nog niet uitgelegd is welke versie Hallo geserialiseerd van bericht lijkt erop nog.</span><span class="sxs-lookup"><span data-stu-id="81d82-274">What we haven't explained yet is what hello serialized version of message looks like.</span></span> <span data-ttu-id="81d82-275">Met andere woorden, als u wilt dat toosend een **SetAirResistance** bericht tooyour apparaat, hoe ziet dit eruit?</span><span class="sxs-lookup"><span data-stu-id="81d82-275">In other words, if you want toosend a **SetAirResistance** message tooyour device, what does that look like?</span></span>

<span data-ttu-id="81d82-276">Als u een bericht tooa apparaat verzendt, zou u dit doen via hello Azure IoT service SDK.</span><span class="sxs-lookup"><span data-stu-id="81d82-276">If you're sending a message tooa device, you would do so through hello Azure IoT service SDK.</span></span> <span data-ttu-id="81d82-277">Moet u toch tooknow wat een bepaalde actie toosend tooinvoke string.</span><span class="sxs-lookup"><span data-stu-id="81d82-277">You still need tooknow what string toosend tooinvoke a particular action.</span></span> <span data-ttu-id="81d82-278">Hallo algemene indeling voor het verzenden van een bericht wordt weergegeven als volgt:</span><span class="sxs-lookup"><span data-stu-id="81d82-278">hello general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="81d82-279">U verzendt een geserialiseerde JSON-object met twee eigenschappen: **naam** Hallo-naam van Hallo actie (bericht) en **Parameters** bevat Hallo parameters van deze actie.</span><span class="sxs-lookup"><span data-stu-id="81d82-279">You're sending a serialized JSON object with two properties: **Name** is hello name of hello action (message) and **Parameters** contains hello parameters of that action.</span></span>

<span data-ttu-id="81d82-280">Bijvoorbeeld: tooinvoke **SetAirResistance** kunt u dit bericht tooa apparaat verzenden:</span><span class="sxs-lookup"><span data-stu-id="81d82-280">For example, tooinvoke **SetAirResistance** you can send this message tooa device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="81d82-281">Hallo actie exact overeenkomt met een actie die is gedefinieerd in het model.</span><span class="sxs-lookup"><span data-stu-id="81d82-281">hello action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="81d82-282">Hallo parameternamen moeten ook overeenkomen met.</span><span class="sxs-lookup"><span data-stu-id="81d82-282">hello parameter names must match as well.</span></span> <span data-ttu-id="81d82-283">Let ook op hoofdletters en kleine letters.</span><span class="sxs-lookup"><span data-stu-id="81d82-283">Also note case sensitivity.</span></span> <span data-ttu-id="81d82-284">**Naam** en **Parameters** zijn altijd hoofdletters.</span><span class="sxs-lookup"><span data-stu-id="81d82-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="81d82-285">Zorg ervoor dat toomatch Hallo-aanvraag van de naam van de actie en de parameters in het model.</span><span class="sxs-lookup"><span data-stu-id="81d82-285">Make sure toomatch hello case of your action name and parameters in your model.</span></span> <span data-ttu-id="81d82-286">In dit voorbeeld is actienaam Hallo 'SetAirResistance' en niet 'setairresistance'.</span><span class="sxs-lookup"><span data-stu-id="81d82-286">In this example, hello action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="81d82-287">twee andere acties Hallo **TurnFanOn** en **TurnFanOff** kan worden aangeroepen door deze berichten tooa apparaat verzenden:</span><span class="sxs-lookup"><span data-stu-id="81d82-287">hello two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages tooa device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="81d82-288">Deze sectie beschreven alles wat u moet tooknow wanneer gebeurtenissen verzenden en ontvangen van berichten met Hallo **serialisatiefunctie** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="81d82-288">This section described everything you need tooknow when sending events and receiving messages with hello **serializer** library.</span></span> <span data-ttu-id="81d82-289">Voordat u doorgaat, gaan we betrekking op bepaalde parameters kunt u configureren die bepalen hoe groot is voor het model.</span><span class="sxs-lookup"><span data-stu-id="81d82-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="81d82-290">Macro-configuratie</span><span class="sxs-lookup"><span data-stu-id="81d82-290">Macro configuration</span></span>
<span data-ttu-id="81d82-291">Als u Hallo **serialisatiefunctie** bibliotheek een belangrijk onderdeel van Hallo SDK toobe op de hoogte van is gevonden in de bibliotheek voor het hello azure-c-gedeeld-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="81d82-291">If you’re using hello **Serializer** library an important part of hello SDK toobe aware of is found in hello azure-c-shared-utility library.</span></span>
<span data-ttu-id="81d82-292">Als u hebt gekloond hello Azure-iot-sdk-c-opslagplaats vanuit GitHub Hallo--recursieve wordt gebruikt, ziet u deze gedeelde hulpprogrammabibliotheek:</span><span class="sxs-lookup"><span data-stu-id="81d82-292">If you have cloned hello Azure-iot-sdk-c repository from GitHub using hello --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="81d82-293">Als u geen Hallo-bibliotheek hebt gekloond, kun je [hier](https://github.com/Azure/azure-c-shared-utility).</span><span class="sxs-lookup"><span data-stu-id="81d82-293">If you have not cloned hello library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="81d82-294">Hallo hulpprogramma gedeelde bibliotheek vindt u Hallo volgende map:</span><span class="sxs-lookup"><span data-stu-id="81d82-294">Within hello shared utility library, you will find hello following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="81d82-295">Deze map bevat een Visual Studio-oplossing aangeroepen **macro\_utils\_h\_generator.sln**:</span><span class="sxs-lookup"><span data-stu-id="81d82-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="81d82-296">Hallo-programma in deze oplossing genereert Hallo **macro\_utils.h** bestand.</span><span class="sxs-lookup"><span data-stu-id="81d82-296">hello program in this solution generates hello **macro\_utils.h** file.</span></span> <span data-ttu-id="81d82-297">Er is een standaardmacro\_utils.h bestand Hello SDK is opgenomen.</span><span class="sxs-lookup"><span data-stu-id="81d82-297">There’s a default macro\_utils.h file included with hello SDK.</span></span> <span data-ttu-id="81d82-298">Deze oplossing kunt u toomodify sommige parameters en vervolgens opnieuw maken Hallo header-bestand op basis van deze parameters.</span><span class="sxs-lookup"><span data-stu-id="81d82-298">This solution allows you toomodify some parameters and then recreate hello header file based on these parameters.</span></span>

<span data-ttu-id="81d82-299">Hallo twee belangrijke parameters toobe met bezighoudt zijn **nArithmetic** en **nMacroParameters** die zijn gedefinieerd in deze twee regels gevonden in de macro\_utils.tt:</span><span class="sxs-lookup"><span data-stu-id="81d82-299">hello two key parameters toobe concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="81d82-300">Deze waarden zijn Hallo standaardparameters Hello SDK is opgenomen.</span><span class="sxs-lookup"><span data-stu-id="81d82-300">These values are hello default parameters included with hello SDK.</span></span> <span data-ttu-id="81d82-301">Elke parameter heeft Hallo betekenis te volgen:</span><span class="sxs-lookup"><span data-stu-id="81d82-301">Each parameter has hello following meaning:</span></span>

* <span data-ttu-id="81d82-302">nMacroParameters – bepaalt hoeveel parameters die u kunt hebben in een DECLARE\_macrodefinitie MODEL.</span><span class="sxs-lookup"><span data-stu-id="81d82-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="81d82-303">nArithmetic – besturingselementen Hallo totale aantal leden in een model is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="81d82-303">nArithmetic – Controls hello total number of members allowed in a model.</span></span>

<span data-ttu-id="81d82-304">Hallo reden die deze parameters belangrijk zijn is omdat ze bepalen hoe groot uw model kan worden.</span><span class="sxs-lookup"><span data-stu-id="81d82-304">hello reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="81d82-305">Neem bijvoorbeeld een modeldefinitie voor dit:</span><span class="sxs-lookup"><span data-stu-id="81d82-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="81d82-306">Zoals eerder vermeld **DECLARE\_MODEL** is slechts een C macro.</span><span class="sxs-lookup"><span data-stu-id="81d82-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="81d82-307">namen van Hallo model en Hallo Hallo **WITH\_gegevens** instructie (nog een andere macro) zijn parameters van **DECLARE\_MODEL**.</span><span class="sxs-lookup"><span data-stu-id="81d82-307">hello names of hello model and hello **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="81d82-308">**nMacroParameters** definieert hoeveel parameters kunnen worden opgenomen in **DECLARE\_MODEL**.</span><span class="sxs-lookup"><span data-stu-id="81d82-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="81d82-309">Hiermee definieert effectief, hoeveel gegevens gebeurtenis en actie declaraties u kunt hebben.</span><span class="sxs-lookup"><span data-stu-id="81d82-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="81d82-310">Als zodanig met Hallo standaardlimiet van 124 betekent dit dat u een model met een combinatie van ongeveer 60 acties en Gegevensgebeurtenissen kunt definiëren.</span><span class="sxs-lookup"><span data-stu-id="81d82-310">As such, with hello default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="81d82-311">Als u deze limiet tooexceed probeert, ontvangt u compilatiefouten waarmee soortgelijke toothis gezocht:</span><span class="sxs-lookup"><span data-stu-id="81d82-311">If you try tooexceed this limit, you'll receive compiler errors that look similar toothis:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="81d82-312">Hallo **nArithmetic** parameter meer over Hallo interne werking van Hallo macrotaal dan uw toepassing is.</span><span class="sxs-lookup"><span data-stu-id="81d82-312">hello **nArithmetic** parameter is more about hello internal workings of hello macro language than your application.</span></span>  <span data-ttu-id="81d82-313">Het totale aantal leden die u in uw model hebben kunt Hallo bepaalt inclusief **DECLARE_STRUCT** macro's.</span><span class="sxs-lookup"><span data-stu-id="81d82-313">It controls hello total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="81d82-314">Als u beginnen te zien compilatiefouten zoals dit en probeer u moet verhogen **nArithmetic**:</span><span class="sxs-lookup"><span data-stu-id="81d82-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="81d82-315">Als u deze parameters toochange wilt, wijzigt u de waarden Hallo in Hallo macro\_utils.tt-bestand, recompile Hallo macro\_utils\_h\_generator.sln oplossing en Voer Hallo gecompileerd programma.</span><span class="sxs-lookup"><span data-stu-id="81d82-315">If you want toochange these parameters, modify hello values in hello macro\_utils.tt file, recompile hello macro\_utils\_h\_generator.sln solution, and run hello compiled program.</span></span> <span data-ttu-id="81d82-316">Als u dit doet, een nieuwe macro\_utils.h bestand is gegenereerd en worden in Hallo.\\ algemene\\inc directory.</span><span class="sxs-lookup"><span data-stu-id="81d82-316">When you do so, a new macro\_utils.h file is generated and placed in hello .\\common\\inc directory.</span></span>

<span data-ttu-id="81d82-317">In volgorde toouse Hallo nieuwe versie van de macro\_utils.h, verwijder Hallo **serialisatiefunctie** NuGet-pakket van uw oplossing en in plaats daarvan bevatten Hallo **serialisatiefunctie** Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="81d82-317">In order toouse hello new version of macro\_utils.h, remove hello **serializer** NuGet package from your solution and in its place include hello **serializer** Visual Studio project.</span></span> <span data-ttu-id="81d82-318">Hierdoor wordt uw code toocompile tegen de broncode Hallo Hallo serializer-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="81d82-318">This enables your code toocompile against hello source code of hello serializer library.</span></span> <span data-ttu-id="81d82-319">Dit omvat Hallo bijgewerkt macro\_utils.h.</span><span class="sxs-lookup"><span data-stu-id="81d82-319">This includes hello updated macro\_utils.h.</span></span> <span data-ttu-id="81d82-320">Als u dat wilt toodo voor **simplesample\_amqp**, begin met het verwijderen van Hallo NuGet-pakket voor Hallo serialisatiefunctie bibliotheek uit Hallo-oplossing:</span><span class="sxs-lookup"><span data-stu-id="81d82-320">If you want toodo this for **simplesample\_amqp**, start by removing hello NuGet package for hello serializer library from hello solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="81d82-321">Voeg dit project tooyour Visual Studio-oplossing:</span><span class="sxs-lookup"><span data-stu-id="81d82-321">Then add this project tooyour Visual Studio solution:</span></span>

> <span data-ttu-id="81d82-322">. \\c\\serialisatiefunctie\\bouwen\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="81d82-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="81d82-323">Wanneer u bent klaar, ziet uw oplossing als volgt:</span><span class="sxs-lookup"><span data-stu-id="81d82-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="81d82-324">Nu macro wanneer u compileert uw oplossing hello bijgewerkt\_utils.h is opgenomen in uw binary.</span><span class="sxs-lookup"><span data-stu-id="81d82-324">Now when you compile your solution, hello updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="81d82-325">Houd er rekening mee dat deze waarden hoog genoeg verhogen compiler overschrijden kunt.</span><span class="sxs-lookup"><span data-stu-id="81d82-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="81d82-326">toothis aanwijst, hello **nMacroParameters** Hallo belangrijkste parameter met welke toobe betrokken is.</span><span class="sxs-lookup"><span data-stu-id="81d82-326">toothis point, hello **nMacroParameters** is hello main parameter with which toobe concerned.</span></span> <span data-ttu-id="81d82-327">Hallo C99 spec geeft aan dat een minimum van 127 parameters zijn toegestaan in een macrodefinitie van de.</span><span class="sxs-lookup"><span data-stu-id="81d82-327">hello C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="81d82-328">Hallo Microsoft compiler Hallo spec precies volgt (en kent een limiet van 127), zodat u niet kunt tooincrease **nMacroParameters** tot meer dan Hallo standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="81d82-328">hello Microsoft compiler follows hello spec exactly (and has a limit of 127), so you won't be able tooincrease **nMacroParameters** beyond hello default.</span></span> <span data-ttu-id="81d82-329">Andere compilers kunt u mogelijk toodo dus (bijvoorbeeld Hallo GNU compiler een hogere limiet ondersteunt).</span><span class="sxs-lookup"><span data-stu-id="81d82-329">Other compilers might allow you toodo so (for example, hello GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="81d82-330">Tot nu toe hebben we behandeld bijna alles wat u tooknow moet over hoe toowrite code Hello **serialisatiefunctie** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="81d82-330">So far we've covered just about everything you need tooknow about how toowrite code with hello **serializer** library.</span></span> <span data-ttu-id="81d82-331">Vóór de sluiting, bezoekt u gaan we een aantal onderwerpen uit eerdere artikelen die u vraagt zich misschien af over.</span><span class="sxs-lookup"><span data-stu-id="81d82-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="hello-lower-level-apis"></a><span data-ttu-id="81d82-332">Hallo lager niveau API's</span><span class="sxs-lookup"><span data-stu-id="81d82-332">hello lower-level APIs</span></span>
<span data-ttu-id="81d82-333">Hallo-voorbeeldtoepassing waarop dit artikel gericht is **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="81d82-333">hello sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="81d82-334">Dit voorbeeld gebruikt Hallo een hoger niveau (Hallo niet-' LLE ") API's toosend gebeurtenissen en ontvangen van berichten.</span><span class="sxs-lookup"><span data-stu-id="81d82-334">This sample uses hello higher-level (hello non-"LL") APIs toosend events and receive messages.</span></span> <span data-ttu-id="81d82-335">Als u deze API's gebruikt, wordt een achtergrond-thread wordt uitgevoerd die zorgt voor zowel het verzenden van gebeurtenissen en ontvangen van berichten.</span><span class="sxs-lookup"><span data-stu-id="81d82-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="81d82-336">Echter, u kunt gebruiken Hallo lager niveau (ES) API's tooeliminate deze achtergrondthread en besturen expliciete wanneer u gebeurtenissen verzenden of ontvangen van berichten van Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="81d82-336">However, you can use hello lower-level (LL) APIs tooeliminate this background thread and take explicit control over when you send events or receive messages from hello cloud.</span></span>

<span data-ttu-id="81d82-337">Zoals beschreven in een [vorige artikel](iot-hub-device-sdk-c-iothubclient.md), er is een reeks functies die uit het Hallo bestaat-API's een hoger niveau:</span><span class="sxs-lookup"><span data-stu-id="81d82-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of hello higher-level APIs:</span></span>

* <span data-ttu-id="81d82-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="81d82-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="81d82-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="81d82-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="81d82-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="81d82-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="81d82-341">IoTHubClient\_vernietigen</span><span class="sxs-lookup"><span data-stu-id="81d82-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="81d82-342">Deze API's worden uitgelegd **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="81d82-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="81d82-343">Er is ook een vergelijkbare reeks API's van lager niveau.</span><span class="sxs-lookup"><span data-stu-id="81d82-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="81d82-344">IoTHubClient\_LLE\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="81d82-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="81d82-345">IoTHubClient\_LLE\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="81d82-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="81d82-346">IoTHubClient\_LLE\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="81d82-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="81d82-347">IoTHubClient\_LLE\_vernietigen</span><span class="sxs-lookup"><span data-stu-id="81d82-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="81d82-348">Opmerking dat Hallo lager niveau API's werk exact Hallo dezelfde manier zoals beschreven in de vorige artikelen Hallo.</span><span class="sxs-lookup"><span data-stu-id="81d82-348">Note that hello lower-level APIs work exactly hello same way as described in hello previous articles.</span></span> <span data-ttu-id="81d82-349">U kunt Hallo eerste set API's gebruiken als u wilt dat een achtergrond-thread toohandle gebeurtenissen verzenden en ontvangen van berichten.</span><span class="sxs-lookup"><span data-stu-id="81d82-349">You can use hello first set of APIs if you want a background thread toohandle sending events and receiving messages.</span></span> <span data-ttu-id="81d82-350">U Hallo tweede reeks API's gebruiken als u wilt dat expliciete controle over wanneer u gegevens verzenden en ontvangen van IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="81d82-350">You use hello second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="81d82-351">Een reeks API's werken net zo goed met Hallo **serialisatiefunctie** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="81d82-351">Either set of APIs work equally well with hello **serializer** library.</span></span>

<span data-ttu-id="81d82-352">Voor een voorbeeld van hoe hello lager niveau API's worden gebruikt met Hallo **serialisatiefunctie** bibliotheek, Zie Hallo **simplesample\_http** toepassing.</span><span class="sxs-lookup"><span data-stu-id="81d82-352">For an example of how hello lower-level APIs are used with hello **serializer** library, see hello **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="81d82-353">Extra onderwerpen</span><span class="sxs-lookup"><span data-stu-id="81d82-353">Additional topics</span></span>
<span data-ttu-id="81d82-354">Enkele andere onderwerpen opgemerkt zijn opnieuw eigendom verwerken, met behulp van alternatieve inloggegevens en configuratieopties.</span><span class="sxs-lookup"><span data-stu-id="81d82-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="81d82-355">Dit zijn alle onderwerpen in een [vorige artikel](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="81d82-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="81d82-356">Hallo belangrijkste is dat al deze functies in Hallo dezelfde werken manier Hello **serialisatiefunctie** bibliotheek als met de Hallo **IoTHubClient** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="81d82-356">hello main point is that all of these features work in hello same way with hello **serializer** library as they do with hello **IoTHubClient** library.</span></span> <span data-ttu-id="81d82-357">Bijvoorbeeld, als u tooattach eigenschappen tooan gebeurtenis uit het model wilt, u **IoTHubMessage\_eigenschappen** en **kaart**\_**AddorUpdate**, Hallo op dezelfde manier zoals eerder beschreven:</span><span class="sxs-lookup"><span data-stu-id="81d82-357">For example, if you want tooattach properties tooan event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, hello same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="81d82-358">Of Hallo gebeurtenis is gegenereerd op basis van Hallo **serialisatiefunctie** bibliotheek of gemaakt handmatig met Hallo **IoTHubClient** bibliotheek maakt niet uit.</span><span class="sxs-lookup"><span data-stu-id="81d82-358">Whether hello event was generated from hello **serializer** library or created manually using hello **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="81d82-359">Alternatieve voor Hallo apparaat referenties, met behulp van **IoTHubClient\_LLE\_maken** net zo goed werkt als **IoTHubClient\_CreateFromConnectionString** voor toewijzen van een **IOTHUB\_CLIENT\_verwerken**.</span><span class="sxs-lookup"><span data-stu-id="81d82-359">For hello alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="81d82-360">Ten slotte, als u Hallo **serialisatiefunctie** bibliotheek, kunt u configuratieopties met instellen **IoTHubClient\_LLE\_SetOption** net zoals u deed bij gebruik van Hallo **IoTHubClient** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="81d82-360">Finally, if you're using hello **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using hello **IoTHubClient** library.</span></span>

<span data-ttu-id="81d82-361">Een functie die de unieke toohello **serialisatiefunctie** bibliotheek Hallo initialisatie API's zijn.</span><span class="sxs-lookup"><span data-stu-id="81d82-361">A feature that is unique toohello **serializer** library are hello initialization APIs.</span></span> <span data-ttu-id="81d82-362">Voordat u met Hallo bibliotheek werken beginnen kunt, moet u aanroepen **serialisatiefunctie\_init**:</span><span class="sxs-lookup"><span data-stu-id="81d82-362">Before you can start working with hello library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="81d82-363">Dit wordt gedaan vlak voordat u aanroepen **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="81d82-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="81d82-364">Op dezelfde manier als u klaar bent met Hallo bibliotheek werken, de laatste aanroep Hallo u maakt is te**serialisatiefunctie\_deinit**:</span><span class="sxs-lookup"><span data-stu-id="81d82-364">Similarly, when you're done working with hello library, hello last call you’ll make is too**serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="81d82-365">Anders wordt alle andere functies die hierboven worden genoemd Hallo werk Hallo dezelfde in Hallo **serialisatiefunctie** bibliotheek als in Hallo **IoTHubClient** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="81d82-365">Otherwise, all of hello other features listed above work hello same in hello **serializer** library as they do in hello **IoTHubClient** library.</span></span> <span data-ttu-id="81d82-366">Zie voor meer informatie over deze onderwerpen Hallo [vorige artikel](iot-hub-device-sdk-c-iothubclient.md) in deze reeks.</span><span class="sxs-lookup"><span data-stu-id="81d82-366">For more information about any of these topics, see hello [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81d82-367">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="81d82-367">Next steps</span></span>
<span data-ttu-id="81d82-368">Dit artikel wordt beschreven in detail Hallo unieke aspecten van Hallo **serialisatiefunctie** bibliotheek opgenomen in Hallo **Azure IoT-device SDK voor C**. Met geleverde Hallo informatie moet u goed begrijpt hoe toouse toosend gebeurtenissen modellen hebben en ontvangen van berichten uit IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="81d82-368">This article describes in detail hello unique aspects of hello **serializer** library contained in hello **Azure IoT device SDK for C**. With hello information provided you should have a good understanding of how toouse models toosend events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="81d82-369">Hiermee ook Hallo driedelige reeks in hoe toodevelop toepassingen met Hallo is **Azure IoT-device SDK voor C**. Dit moet worden voldoende informatie toonot alleen get die u gestart, maar bieden u een grondig begrip over de werking van Hallo API's.</span><span class="sxs-lookup"><span data-stu-id="81d82-369">This also concludes hello three-part series on how toodevelop applications with hello **Azure IoT device SDK for C**. This should be enough information toonot only get you started but give you a thorough understanding of how hello APIs work.</span></span> <span data-ttu-id="81d82-370">Voor meer informatie, moet u er een paar voorbeelden zijn in Hallo die SDK niet ingegaan.</span><span class="sxs-lookup"><span data-stu-id="81d82-370">For additional information, there are a few samples in hello SDK not covered here.</span></span> <span data-ttu-id="81d82-371">Anders Hallo [SDK-documentatie](https://github.com/Azure/azure-iot-sdk-c) is een goede bron voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="81d82-371">Otherwise, hello [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="81d82-372">toolearn meer informatie over het ontwikkelen voor IoT Hub, Zie Hallo [Azure IoT SDK's][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="81d82-372">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="81d82-373">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="81d82-373">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="81d82-374">[Een apparaat simuleren met Azure IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="81d82-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

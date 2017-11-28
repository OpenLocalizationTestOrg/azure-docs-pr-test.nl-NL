---
title: dynamische telemetrie aaaUse | Microsoft Docs
description: Volg deze zelfstudie toolearn hoe dynamische telemetrie toouse met hello Azure IoT Suite remote monitoring vooraf geconfigureerde oplossing.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 06cb2a370b67b4950efdfa4c7d906ac92106f4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="8a367-103">Gebruik dynamische telemetrie Hello vooraf geconfigureerde oplossing voor externe controle</span><span class="sxs-lookup"><span data-stu-id="8a367-103">Use dynamic telemetry with hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="8a367-104">Dynamische telemetrie kunt u toovisualize alle telemetrie verzonden toohello vooraf geconfigureerde oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="8a367-104">Dynamic telemetry enables you toovisualize any telemetry sent toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="8a367-105">Hallo gesimuleerde apparaten die met Hallo vooraf geconfigureerde oplossing implementeren verzenden temperatuur en vochtigheid telemetrie die u op Hallo dashboard visualiseren kunt.</span><span class="sxs-lookup"><span data-stu-id="8a367-105">hello simulated devices that deploy with hello preconfigured solution send temperature and humidity telemetry, which you can visualize on hello dashboard.</span></span> <span data-ttu-id="8a367-106">Als u bestaande gesimuleerde apparaten wilt aanpassen, nieuwe gesimuleerde apparaten maken of fysieke apparaten toohello vooraf geconfigureerde oplossing kunt u andere waarden telemetrie zoals externe temperatuur hello, RPM of windsnelheid verzenden verbinden.</span><span class="sxs-lookup"><span data-stu-id="8a367-106">If you customize existing simulated devices, create new simulated devices, or connect physical devices toohello preconfigured solution you can send other telemetry values such as hello external temperature, RPM, or windspeed.</span></span> <span data-ttu-id="8a367-107">U kunt vervolgens visualiseren van deze extra telemetrie op Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="8a367-107">You can then visualize this additional telemetry on hello dashboard.</span></span>

<span data-ttu-id="8a367-108">Deze zelfstudie wordt een eenvoudige Node.js gesimuleerd apparaat kunt u eenvoudig tooexperiment met dynamische telemetrie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8a367-108">This tutorial uses a simple Node.js simulated device that you can easily modify tooexperiment with dynamic telemetry.</span></span>

<span data-ttu-id="8a367-109">toocomplete in deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="8a367-109">toocomplete this tutorial, you’ll need:</span></span>

* <span data-ttu-id="8a367-110">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8a367-110">An active Azure subscription.</span></span> <span data-ttu-id="8a367-111">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="8a367-111">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8a367-112">Zie [Gratis proefversie van Azure][lnk_free_trial] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8a367-112">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="8a367-113">[Node.js] [ lnk-node] versie 0.12.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="8a367-113">[Node.js][lnk-node] version 0.12.x or later.</span></span>

<span data-ttu-id="8a367-114">U kunt voltooien van deze zelfstudie op elk besturingssysteem, zoals Windows of Linux, waar u Node.js kunt installeren.</span><span class="sxs-lookup"><span data-stu-id="8a367-114">You can complete this tutorial on any operating system, such as Windows or Linux, where you can install Node.js.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a><span data-ttu-id="8a367-115">Een type telemetrie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8a367-115">Add a telemetry type</span></span>

<span data-ttu-id="8a367-116">de volgende stap Hallo is tooreplace Hallo telemetrie die worden gegenereerd door Hallo Node.js gesimuleerd apparaat met een nieuwe set met waarden:</span><span class="sxs-lookup"><span data-stu-id="8a367-116">hello next step is tooreplace hello telemetry generated by hello Node.js simulated device with a new set of values:</span></span>

1. <span data-ttu-id="8a367-117">Stop Hallo Node.js gesimuleerd apparaat door te typen **Ctrl + C** in uw opdrachtprompt of de shell.</span><span class="sxs-lookup"><span data-stu-id="8a367-117">Stop hello Node.js simulated device by typing **Ctrl+C** in your command prompt or shell.</span></span>
2. <span data-ttu-id="8a367-118">Hallo remote_monitoring.js bestand ziet u Hallo basisgegevens waarden voor Hallo bestaande temperatuur en vochtigheid externe temperatuur telemetrie.</span><span class="sxs-lookup"><span data-stu-id="8a367-118">In hello remote_monitoring.js file, you can see hello base data values for hello existing temperature, humidity, and external temperature telemetry.</span></span> <span data-ttu-id="8a367-119">Voeg een waarde basisgegevens voor **rpm** als volgt:</span><span class="sxs-lookup"><span data-stu-id="8a367-119">Add a base data value for **rpm** as follows:</span></span>

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. <span data-ttu-id="8a367-120">Hallo Node.js gesimuleerd apparaat maakt gebruik van Hallo **generateRandomIncrement** werken in Hallo remote_monitoring.js bestand tooadd een willekeurige verhoging toohello basisgegevens waarden.</span><span class="sxs-lookup"><span data-stu-id="8a367-120">hello Node.js simulated device uses hello **generateRandomIncrement** function in hello remote_monitoring.js file tooadd a random increment toohello base data values.</span></span> <span data-ttu-id="8a367-121">Hallo willekeurige **rpm** waarde door een regel code na Hallo bestaande randomizations toe te voegen als volgt:</span><span class="sxs-lookup"><span data-stu-id="8a367-121">Randomize hello **rpm** value by adding a line of code after hello existing randomizations as follows:</span></span>

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. <span data-ttu-id="8a367-122">Hallo nieuwe rpm waarde toohello JSON-nettolading Hallo apparaat verzendt tooIoT Hub toevoegen:</span><span class="sxs-lookup"><span data-stu-id="8a367-122">Add hello new rpm value toohello JSON payload hello device sends tooIoT Hub:</span></span>

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. <span data-ttu-id="8a367-123">Hallo Node.js gesimuleerd apparaat met behulp van de volgende opdracht Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8a367-123">Run hello Node.js simulated device using hello following command:</span></span>

    `node remote_monitoring.js`

6. <span data-ttu-id="8a367-124">Houd rekening met Hallo nieuw RPM telemetrie type dat wordt weergegeven in de grafiek Hallo in Hallo dashboard:</span><span class="sxs-lookup"><span data-stu-id="8a367-124">Observe hello new RPM telemetry type that displays on hello chart in hello dashboard:</span></span>

![RPM toohello dashboard toevoegen][image3]

> [!NOTE]
> <span data-ttu-id="8a367-126">U kunt toodisable moet en schakel vervolgens Hallo Node.js-apparaat op Hallo **apparaten** pagina in Hallo dashboard toosee Hallo wijziging onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="8a367-126">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="customize-hello-dashboard-display"></a><span data-ttu-id="8a367-127">Hallo-dashboard aanpassen</span><span class="sxs-lookup"><span data-stu-id="8a367-127">Customize hello dashboard display</span></span>

<span data-ttu-id="8a367-128">Hallo **apparaatgegevens** bericht metagegevens kunt opnemen over Hallo telemetrie Hallo apparaat tooIoT Hub kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="8a367-128">hello **Device-Info** message can include metadata about hello telemetry hello device can send tooIoT Hub.</span></span> <span data-ttu-id="8a367-129">Deze metagegevens kunt Hallo telemetrie typen Hallo apparaat verzendt opgeven.</span><span class="sxs-lookup"><span data-stu-id="8a367-129">This metadata can specify hello telemetry types hello device sends.</span></span> <span data-ttu-id="8a367-130">Hallo wijzigen **deviceMetaData** waarde in Hallo remote_monitoring.js bestand tooinclude een **telemetrie** definitie Hallo na **opdrachten** definitie.</span><span class="sxs-lookup"><span data-stu-id="8a367-130">Modify hello **deviceMetaData** value in hello remote_monitoring.js file tooinclude a **Telemetry** definition following hello **Commands** definition.</span></span> <span data-ttu-id="8a367-131">Hallo volgende codefragment toont Hallo **opdrachten** definition (ervoor tooadd worden een `,` na Hallo **opdrachten** definitie):</span><span class="sxs-lookup"><span data-stu-id="8a367-131">hello following code snippet shows hello **Commands** definition (be sure tooadd a `,` after hello **Commands** definition):</span></span>

```nodejs
'Commands': [{
  'Name': 'SetTemperature',
  'Parameters': [{
    'Name': 'Temperature',
    'Type': 'double'
  }]
},
{
  'Name': 'SetHumidity',
  'Parameters': [{
    'Name': 'Humidity',
    'Type': 'double'
  }]
}],
'Telemetry': [{
  'Name': 'Temperature',
  'Type': 'double'
},
{
  'Name': 'Humidity',
  'Type': 'double'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double'
}]
```

> [!NOTE]
> <span data-ttu-id="8a367-132">Hallo-oplossing voor externe controle maakt gebruik van de definitie van een niet-hoofdlettergevoelige overeenkomst toocompare Hallo metagegevens met gegevens in de telemetriestroom Hallo.</span><span class="sxs-lookup"><span data-stu-id="8a367-132">hello remote monitoring solution uses a case-insensitive match toocompare hello metadata definition with data in hello telemetry stream.</span></span>


<span data-ttu-id="8a367-133">Toevoegen van een **telemetrie** definitie zoals weergegeven in de voorgaande Hallo codefragment verandert niet Hallo gedrag van Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="8a367-133">Adding a **Telemetry** definition as shown in hello preceding code snippet does not change hello behavior of hello dashboard.</span></span> <span data-ttu-id="8a367-134">Hallo metagegevens kan echter ook bevatten een **DisplayName** kenmerk toocustomize Hallo weergave in Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="8a367-134">However, hello metadata can also include a **DisplayName** attribute toocustomize hello display in hello dashboard.</span></span> <span data-ttu-id="8a367-135">Update Hallo **telemetrie** definitie van metagegevens zoals weergegeven in het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="8a367-135">Update hello **Telemetry** metadata definition as shown in hello following snippet:</span></span>

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double',
  'DisplayName': 'Outdoor Temperature (C*)'
}
]
```

<span data-ttu-id="8a367-136">Hallo volgende schermafbeelding ziet u hoe de grafieklegenda Hallo op Hallo dashboard Hiermee wijzigt u deze wijziging:</span><span class="sxs-lookup"><span data-stu-id="8a367-136">hello following screenshot shows how this change modifies hello chart legend on hello dashboard:</span></span>

![De grafieklegenda Hallo aanpassen][image4]

> [!NOTE]
> <span data-ttu-id="8a367-138">U kunt toodisable moet en schakel vervolgens Hallo Node.js-apparaat op Hallo **apparaten** pagina in Hallo dashboard toosee Hallo wijziging onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="8a367-138">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="filter-hello-telemetry-types"></a><span data-ttu-id="8a367-139">Hallo telemetrie typen worden gefilterd</span><span class="sxs-lookup"><span data-stu-id="8a367-139">Filter hello telemetry types</span></span>

<span data-ttu-id="8a367-140">Hallo-grafiek op Hallo dashboard wordt standaard elke gegevensreeks in Hallo telemetriestroom.</span><span class="sxs-lookup"><span data-stu-id="8a367-140">By default, hello chart on hello dashboard shows every data series in hello telemetry stream.</span></span> <span data-ttu-id="8a367-141">U kunt Hallo **apparaatgegevens** metagegevens toosuppress Hallo weergave van specifieke telemetrie typen op Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="8a367-141">You can use hello **Device-Info** metadata toosuppress hello display of specific telemetry types on hello chart.</span></span> 

<span data-ttu-id="8a367-142">toomake hello grafiek weergeven alleen temperatuur en vochtigheid telemetrie, weglaten **ExternalTemperature** van Hallo **apparaatgegevens** **telemetrie** metagegevens als volgt:</span><span class="sxs-lookup"><span data-stu-id="8a367-142">toomake hello chart show only Temperature and Humidity telemetry, omit **ExternalTemperature** from hello **Device-Info** **Telemetry** metadata as follows:</span></span>

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
//{
//  'Name': 'ExternalTemperature',
//  'Type': 'double',
//  'DisplayName': 'Outdoor Temperature (C*)'
//}
]
```

<span data-ttu-id="8a367-143">Hallo **buiten temperatuur** niet meer weergegeven op het Hallo-grafiek:</span><span class="sxs-lookup"><span data-stu-id="8a367-143">hello **Outdoor Temperature** no longer displays on hello chart:</span></span>

![Filter Hallo telemetrie op Hallo-dashboard][image5]

<span data-ttu-id="8a367-145">Deze wijziging is alleen van invloed op Hallo grafiekweergave.</span><span class="sxs-lookup"><span data-stu-id="8a367-145">This change only affects hello chart display.</span></span> <span data-ttu-id="8a367-146">Hallo **ExternalTemperature** gegevenswaarden nog steeds worden opgeslagen en beschikbaar gesteld voor de verwerking van de back-end.</span><span class="sxs-lookup"><span data-stu-id="8a367-146">hello **ExternalTemperature** data values are still stored and made available for any backend processing.</span></span>

> [!NOTE]
> <span data-ttu-id="8a367-147">U kunt toodisable moet en schakel vervolgens Hallo Node.js-apparaat op Hallo **apparaten** pagina in Hallo dashboard toosee Hallo wijziging onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="8a367-147">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="handle-errors"></a><span data-ttu-id="8a367-148">Afhandelen van fouten</span><span class="sxs-lookup"><span data-stu-id="8a367-148">Handle errors</span></span>

<span data-ttu-id="8a367-149">Voor een toodisplay van de gegevensstroom in de grafiek hello, de **Type** in Hallo **apparaatgegevens** metagegevens moet overeenkomen met de Hallo-gegevenstype van Hallo telemetrie waarden.</span><span class="sxs-lookup"><span data-stu-id="8a367-149">For a data stream toodisplay on hello chart, its **Type** in hello **Device-Info** metadata must match hello data type of hello telemetry values.</span></span> <span data-ttu-id="8a367-150">Bijvoorbeeld, als hello metagegevens geeft aan dat Hallo **Type** van vochtigheid gegevens is **int** en een **dubbele** is gevonden in de telemetriestroom Hallo vervolgens Hallo vochtigheid telemetrie biedt niet weergegeven op het Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="8a367-150">For example, if hello metadata specifies that hello **Type** of humidity data is **int** and a **double** is found in hello telemetry stream then hello humidity telemetry does not display on hello chart.</span></span> <span data-ttu-id="8a367-151">Hallo echter **vochtigheid** waarden zijn nog steeds opgeslagen en beschikbaar gesteld voor de verwerking van de back-end.</span><span class="sxs-lookup"><span data-stu-id="8a367-151">However, hello **Humidity** values are still stored and made available for any back-end processing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a367-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8a367-152">Next steps</span></span>

<span data-ttu-id="8a367-153">Nu dat u hebt gezien hoe dynamische telemetrie toouse, voor meer informatie over hoe Hallo vooraf oplossingen geconfigureerde gebruiken apparaatgegevens: [apparaat informatie metagegevens in Hallo externe controle vooraf geconfigureerde oplossing] [ lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="8a367-153">Now that you've seen how toouse dynamic telemetry, you can learn more about how hello preconfigured solutions use device information: [Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org

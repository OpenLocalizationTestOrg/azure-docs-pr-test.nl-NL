---
title: aaaCustomizing vooraf geconfigureerde oplossingen | Microsoft Docs
description: Biedt richtlijnen voor hoe toocustomize hello Azure IoT Suite vooraf oplossingen geconfigureerde.
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="647d6-103">Een vooraf geconfigureerde oplossing aanpassen</span><span class="sxs-lookup"><span data-stu-id="647d6-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="647d6-104">Hallo vooraf geconfigureerde oplossingen Hello Azure IoT Suite demonstreren Hallo services binnen Hallo suite werken samen toodeliver een end-to-end-oplossing.</span><span class="sxs-lookup"><span data-stu-id="647d6-104">hello preconfigured solutions provided with hello Azure IoT Suite demonstrate hello services within hello suite working together toodeliver an end-to-end solution.</span></span> <span data-ttu-id="647d6-105">Vanaf deze beginpunt zijn er verschillende plaatsen waarin u kunt uitbreiden en aanpassen Hallo-oplossing voor specifieke scenario's.</span><span class="sxs-lookup"><span data-stu-id="647d6-105">From this starting point, there are various places in which you can extend and customize hello solution for specific scenarios.</span></span> <span data-ttu-id="647d6-106">Hallo volgende secties beschrijven deze common aanpassing punten.</span><span class="sxs-lookup"><span data-stu-id="647d6-106">hello following sections describe these common customization points.</span></span>

## <a name="find-hello-source-code"></a><span data-ttu-id="647d6-107">Hallo broncode vinden</span><span class="sxs-lookup"><span data-stu-id="647d6-107">Find hello source code</span></span>

<span data-ttu-id="647d6-108">de broncode Hallo voor Hallo vooraf geconfigureerde oplossingen is beschikbaar op GitHub in Hallo opslagplaatsen te volgen:</span><span class="sxs-lookup"><span data-stu-id="647d6-108">hello source code for hello preconfigured solutions is available on GitHub in hello following repositories:</span></span>

* <span data-ttu-id="647d6-109">Externe controle: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="647d6-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="647d6-110">Voorspeld onderhoud: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="647d6-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="647d6-111">Verbonden factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="647d6-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="647d6-112">de broncode Hallo voor Hallo vooraf geconfigureerde oplossingen wordt verstrekt toodemonstrate Hallo patterns and practice tooimplement Hallo end-to-end-functionaliteit van een IoT-oplossing met behulp van Azure IoT Suite gebruikt.</span><span class="sxs-lookup"><span data-stu-id="647d6-112">hello source code for hello preconfigured solutions is provided toodemonstrate hello patterns and practices used tooimplement hello end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="647d6-113">U vindt meer informatie over het toobuild en oplossingen in de GitHub-opslagplaatsen Hallo Hallo implementeren.</span><span class="sxs-lookup"><span data-stu-id="647d6-113">You can find more information about how toobuild and deploy hello solutions in hello GitHub repositories.</span></span>

## <a name="change-hello-preconfigured-rules"></a><span data-ttu-id="647d6-114">Hallo vooraf geconfigureerde regels wijzigen</span><span class="sxs-lookup"><span data-stu-id="647d6-114">Change hello preconfigured rules</span></span>

<span data-ttu-id="647d6-115">Hallo oplossing voor externe controle omvat drie [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) taken toohandle apparaatgegevens, Telemetrie en regellogica in Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="647d6-115">hello remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs toohandle device information, telemetry, and rules logic in hello solution.</span></span>

<span data-ttu-id="647d6-116">Hallo drie stream analytics-taken en hun syntaxis worden beschreven in de diepte in Hallo [externe controle oplossing walkthrough over vooraf geconfigureerde](iot-suite-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="647d6-116">hello three stream analytics jobs and their syntax are described in depth in hello [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="647d6-117">U kunt deze taken bewerken direct tooalter Hallo logica of Voeg logica specifieke tooyour scenario.</span><span class="sxs-lookup"><span data-stu-id="647d6-117">You can edit these jobs directly tooalter hello logic, or add logic specific tooyour scenario.</span></span> <span data-ttu-id="647d6-118">U vindt Hallo Stream Analytics-taken als volgt:</span><span class="sxs-lookup"><span data-stu-id="647d6-118">You can find hello Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="647d6-119">Ga te[Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="647d6-119">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="647d6-120">De resourcegroep toohello met dezelfde naam als uw IoT-oplossing Hallo navigeren.</span><span class="sxs-lookup"><span data-stu-id="647d6-120">Navigate toohello resource group with hello same name as your IoT solution.</span></span> 
3. <span data-ttu-id="647d6-121">Selecteer hello Azure Stream Analytics-taak gewenst toomodify.</span><span class="sxs-lookup"><span data-stu-id="647d6-121">Select hello Azure Stream Analytics job you'd like toomodify.</span></span> 
4. <span data-ttu-id="647d6-122">Hallo-taak stoppen als u selecteert **stoppen** in Hallo reeks opdrachten.</span><span class="sxs-lookup"><span data-stu-id="647d6-122">Stop hello job by selecting **Stop** in hello set of commands.</span></span> 
5. <span data-ttu-id="647d6-123">Hallo-in-, query- en uitgangen bewerken.</span><span class="sxs-lookup"><span data-stu-id="647d6-123">Edit hello inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="647d6-124">Een eenvoudige wijziging is toochange Hallo-query voor Hallo **regels** taak toouse een **' < '** in plaats van een **' > '**.</span><span class="sxs-lookup"><span data-stu-id="647d6-124">A simple modification is toochange hello query for hello **Rules** job toouse a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="647d6-125">nog steeds weergegeven in de oplossingsportal Hello **' > '** wanneer u een regel voor het bewerken, maar u ziet hoe Hallo gedrag vanwege toohello wijziging in de onderliggende taak hello wordt gespiegeld.</span><span class="sxs-lookup"><span data-stu-id="647d6-125">hello solution portal still shows **">"** when you edit a rule, but notice how hello behavior is flipped due toohello change in hello underlying job.</span></span>
6. <span data-ttu-id="647d6-126">Hallo taak starten</span><span class="sxs-lookup"><span data-stu-id="647d6-126">Start hello job</span></span>

> [!NOTE]
> <span data-ttu-id="647d6-127">Hallo-dashboard voor externe controle, is afhankelijk van wat u specifieke gegevens dus Hallo dashboard toofail wijzigen Hallo taken kan veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="647d6-127">hello remote monitoring dashboard depends on specific data, so altering hello jobs can cause hello dashboard toofail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="647d6-128">Uw eigen regels toevoegen</span><span class="sxs-lookup"><span data-stu-id="647d6-128">Add your own rules</span></span>

<span data-ttu-id="647d6-129">Bovendien toochanging Hallo vooraf geconfigureerde Azure Stream Analytics-taken, kunt u hello Azure portal tooadd nieuwe taken gebruiken of nieuwe query's tooexisting taken toevoegen.</span><span class="sxs-lookup"><span data-stu-id="647d6-129">In addition toochanging hello preconfigured Azure Stream Analytics jobs, you can use hello Azure portal tooadd new jobs or add new queries tooexisting jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="647d6-130">Apparaten aanpassen</span><span class="sxs-lookup"><span data-stu-id="647d6-130">Customize devices</span></span>

<span data-ttu-id="647d6-131">Een van de meest voorkomende extensie activiteiten Hallo werkt met apparaten specifieke tooyour scenario.</span><span class="sxs-lookup"><span data-stu-id="647d6-131">One of hello most common extension activities is working with devices specific tooyour scenario.</span></span> <span data-ttu-id="647d6-132">Er zijn verschillende methoden voor het werken met apparaten.</span><span class="sxs-lookup"><span data-stu-id="647d6-132">There are several methods for working with devices.</span></span> <span data-ttu-id="647d6-133">Deze methoden omvatten een gesimuleerd apparaat toomatch uw scenario wijzigen of met behulp van Hallo [IoT Device SDK] [ IoT Device SDK] tooconnect uw fysieke apparaat toohello oplossing.</span><span class="sxs-lookup"><span data-stu-id="647d6-133">These methods include altering a simulated device toomatch your scenario, or using hello [IoT Device SDK][IoT Device SDK] tooconnect your physical device toohello solution.</span></span>

<span data-ttu-id="647d6-134">Zie voor een stapsgewijze handleiding tooadding apparaten, Hallo [Iot Suite-verbinding maken met apparaten](iot-suite-connecting-devices.md) artikel en Hallo [van een remote monitoring C SDK voorbeeld](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span><span class="sxs-lookup"><span data-stu-id="647d6-134">For a step-by-step guide tooadding devices, see hello [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and hello [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="647d6-135">Dit voorbeeld is ontworpen toowork Hello vooraf geconfigureerde oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="647d6-135">This sample is designed toowork with hello remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="647d6-136">Uw eigen gesimuleerd apparaat kunt maken</span><span class="sxs-lookup"><span data-stu-id="647d6-136">Create your own simulated device</span></span>

<span data-ttu-id="647d6-137">Opgenomen in Hallo [voor externe controle oplossing broncode](https://github.com/Azure/azure-iot-remote-monitoring), is een .NET-simulator.</span><span class="sxs-lookup"><span data-stu-id="647d6-137">Included in hello [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="647d6-138">Deze simulator is Hallo een ingericht als onderdeel van het Hallo-oplossing en u kunt wijzigen toosend andere metagegevens telemetrie, reageren toodifferent opdrachten en -methoden.</span><span class="sxs-lookup"><span data-stu-id="647d6-138">This simulator is hello one provisioned as part of hello solution and you can alter it toosend different metadata, telemetry, and respond toodifferent commands and methods.</span></span>

<span data-ttu-id="647d6-139">de vooraf geconfigureerde simulator Hallo in Hallo vooraf geconfigureerde oplossing voor externe controle een koelervoorbeeld apparaat simuleert dat temperatuur en vochtigheid telemetrie verzendt.</span><span class="sxs-lookup"><span data-stu-id="647d6-139">hello preconfigured simulator in hello remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="647d6-140">U kunt wijzigen Hallo simulator in Hallo [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) wanneer u hebt de GitHub-opslagplaats Hallo forked project.</span><span class="sxs-lookup"><span data-stu-id="647d6-140">You can modify hello simulator in hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked hello GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="647d6-141">Beschikbare locaties voor de gesimuleerde apparaten</span><span class="sxs-lookup"><span data-stu-id="647d6-141">Available locations for simulated devices</span></span>

<span data-ttu-id="647d6-142">Er is een Hallo standaardset locaties in Seattle/Redmond, Washington, Verenigde Staten van Amerika.</span><span class="sxs-lookup"><span data-stu-id="647d6-142">hello default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="647d6-143">U kunt deze locaties in wijzigen [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="647d6-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a><span data-ttu-id="647d6-144">Een gewenste eigenschap update handler toohello simulator toevoegen</span><span class="sxs-lookup"><span data-stu-id="647d6-144">Add a desired property update handler toohello simulator</span></span>

<span data-ttu-id="647d6-145">U kunt een waarde voor een gewenste eigenschap voor een apparaat in de oplossingsportal Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="647d6-145">You can set a value for a desired property for a device in hello solution portal.</span></span> <span data-ttu-id="647d6-146">Het is Hallo verantwoordelijkheid van Hallo apparaat toohandle Hallo eigenschap wijzigingsaanvraag Hallo apparaat ophalen van eigenschapswaarde Hallo gewenst.</span><span class="sxs-lookup"><span data-stu-id="647d6-146">It is hello responsibility of hello device toohandle hello property change request when hello device retrieves hello desired property value.</span></span> <span data-ttu-id="647d6-147">tooadd ondersteuning voor een wijziging in de eigenschap waarde via een gewenste eigenschap, moet u een handler toohello simulator tooadd.</span><span class="sxs-lookup"><span data-stu-id="647d6-147">tooadd support for a property value change through a desired property, you need tooadd a handler toohello simulator.</span></span>

<span data-ttu-id="647d6-148">Hallo simulator bevat handlers voor Hallo **SetPointTemp** en **TelemetryInterval** eigenschappen die u bijwerken door het instellen van kunt de gewenste waarden in de oplossingsportal Hallo.</span><span class="sxs-lookup"><span data-stu-id="647d6-148">hello simulator contains handlers for hello **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in hello solution portal.</span></span>

<span data-ttu-id="647d6-149">Hallo volgende voorbeeld ziet u Hallo-handler voor Hallo **SetPointTemp** gewenst eigenschap in Hallo **CoolerDevice** klasse:</span><span class="sxs-lookup"><span data-stu-id="647d6-149">hello following example shows hello handler for hello **SetPointTemp** desired property in hello **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="647d6-150">Deze methode werkt Hallo telemetrie punt temperatuur- en vervolgens rapporten Hallo back tooIoT Hub wijzigen door een eigenschap gemeld.</span><span class="sxs-lookup"><span data-stu-id="647d6-150">This method updates hello telemetry point temperature and then reports hello change back tooIoT Hub by setting a reported property.</span></span>

<span data-ttu-id="647d6-151">U kunt uw eigen handlers voor uw eigen eigenschappen toevoegen door de volgende Hallo patroon in het voorgaande voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="647d6-151">You can add your own handlers for your own properties by following hello pattern in hello preceding example.</span></span>

<span data-ttu-id="647d6-152">U moet ook Hallo gewenste eigenschap toohello handler binden zoals weergegeven in het volgende voorbeeld uit Hallo Hallo **CoolerDevice** constructor:</span><span class="sxs-lookup"><span data-stu-id="647d6-152">You must also bind hello desired property toohello handler as shown in hello following example from hello **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="647d6-153">Houd er rekening mee dat **SetPointTempPropertyName** een constante is gedefinieerd als 'Config.SetPointTemp'.</span><span class="sxs-lookup"><span data-stu-id="647d6-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-toohello-simulator"></a><span data-ttu-id="647d6-154">Ondersteuning voor een nieuwe methode toohello simulator toevoegen</span><span class="sxs-lookup"><span data-stu-id="647d6-154">Add support for a new method toohello simulator</span></span>

<span data-ttu-id="647d6-155">U kunt aanpassen Hallo simulator tooadd ondersteuning voor een nieuwe [methode (directe methode)][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="647d6-155">You can customize hello simulator tooadd support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="647d6-156">Er zijn twee belangrijke stappen vereist:</span><span class="sxs-lookup"><span data-stu-id="647d6-156">There are two key steps required:</span></span>

- <span data-ttu-id="647d6-157">Hallo simulator verwittigt Hallo IoT-hub in Hallo vooraf geconfigureerde oplossing met details van Hallo-methode.</span><span class="sxs-lookup"><span data-stu-id="647d6-157">hello simulator must notify hello IoT hub in hello preconfigured solution with details of hello method.</span></span>
- <span data-ttu-id="647d6-158">Hallo simulator moet code toohandle Hallo methodeaanroep bevatten wanneer u het aanroepen van Hallo **Apparaatdetails** deelvenster in Hallo solution explorer of via een taak.</span><span class="sxs-lookup"><span data-stu-id="647d6-158">hello simulator must include code toohandle hello method call when you invoke it from hello **Device details** panel in hello solution explorer or through a job.</span></span>

<span data-ttu-id="647d6-159">Hallo externe controle vooraf geconfigureerde oplossing maakt gebruik van *gerapporteerd eigenschappen* toosend details van de ondersteunde methoden tooIoT hub.</span><span class="sxs-lookup"><span data-stu-id="647d6-159">hello remote monitoring preconfigured solution uses *reported properties* toosend details of supported methods tooIoT hub.</span></span> <span data-ttu-id="647d6-160">Hallo back-end oplossing houdt een lijst van alle Hallo methoden die worden ondersteund door elk apparaat samen met een geschiedenis van methode aanroepen.</span><span class="sxs-lookup"><span data-stu-id="647d6-160">hello solution back end maintains a list of all hello methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="647d6-161">U kunt deze informatie weergeven over apparaten en methoden aanroepen in de oplossingsportal Hallo.</span><span class="sxs-lookup"><span data-stu-id="647d6-161">You can view this information about devices and invoke methods in hello solution portal.</span></span>

<span data-ttu-id="647d6-162">Hallo toonotify IoT-hub of een apparaat een methode ondersteunt, Hallo apparaat moet toevoegen details van Hallo methode toohello **SupportedMethods** knooppunt in Hallo gerapporteerd eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="647d6-162">toonotify hello IoT hub that a device supports a method, hello device must add details of hello method toohello **SupportedMethods** node in hello reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="647d6-163">Hallo Methodehandtekening heeft Hallo volgende indeling: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="647d6-163">hello method signature has hello following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="647d6-164">Bijvoorbeeld: toospecify hello **InitiateFirmwareUpdate** methode verwacht een tekenreeksparameter met de naam **FwPackageURI**, Hallo methodehandtekening volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="647d6-164">For example, toospecify hello **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use hello following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="647d6-165">Zie voor een lijst van ondersteunde parametertypen Hallo **CommandTypes** klasse in Hallo infrastructuurproject.</span><span class="sxs-lookup"><span data-stu-id="647d6-165">For a list of supported parameter types, see hello **CommandTypes** class in hello Infrastructure project.</span></span>

<span data-ttu-id="647d6-166">toodelete een methode instellen Hallo methodehandtekening te`null` in Hallo gerapporteerd eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="647d6-166">toodelete a method, set hello method signature too`null` in hello reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="647d6-167">Hallo back-end oplossing werkt alleen informatie over ondersteunde methoden wanneer dit ontvangt een *apparaatgegevens* bericht van het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="647d6-167">hello solution back end only updates information about supported methods when it receives a *device information* message from hello device.</span></span>

<span data-ttu-id="647d6-168">Hallo volgende codevoorbeeld van Hallo **SampleDeviceFactory** klasse in Hallo gemeenschappelijke project toont hoe tooadd een methode toohello lijst van **SupportedMethods** Hallo eigenschappen is verzonden door Hallo gerapporteerd apparaat:</span><span class="sxs-lookup"><span data-stu-id="647d6-168">hello following code sample from hello **SampleDeviceFactory** class in hello Common project shows how tooadd a method toohello list of **SupportedMethods** in hello reported properties sent by hello device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="647d6-169">Dit codefragment voegt details van Hallo **InitiateFirmwareUpdate** methode, met inbegrip van tekst toodisplay in de oplossingsportal hello en details van Hallo methodeparameters vereist.</span><span class="sxs-lookup"><span data-stu-id="647d6-169">This code snippet adds details of hello **InitiateFirmwareUpdate** method including text toodisplay in hello solution portal and details of hello required method parameters.</span></span>

<span data-ttu-id="647d6-170">Hallo simulator verzendt gemelde eigenschappen, waaronder Hallo lijst van ondersteunde methoden tooIoT Hub wanneer Hallo simulator wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="647d6-170">hello simulator sends reported properties, including hello list of supported methods, tooIoT Hub when hello simulator starts.</span></span>

<span data-ttu-id="647d6-171">Voeg een handler toohello simulator code voor elke methode ondersteund.</span><span class="sxs-lookup"><span data-stu-id="647d6-171">Add a handler toohello simulator code for each method it supports.</span></span> <span data-ttu-id="647d6-172">U kunt bestaande handlers in Hallo Hallo zien **CoolerDevice** klasse in Hallo Simulator.WebJob project.</span><span class="sxs-lookup"><span data-stu-id="647d6-172">You can see hello existing handlers in hello **CoolerDevice** class in hello Simulator.WebJob project.</span></span> <span data-ttu-id="647d6-173">Hallo volgende voorbeeld ziet u Hallo-handler voor **InitiateFirmwareUpdate** methode:</span><span class="sxs-lookup"><span data-stu-id="647d6-173">hello following example shows hello handler for **InitiateFirmwareUpdate** method:</span></span>

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

<span data-ttu-id="647d6-174">Methode handler namen moeten beginnen met `On` gevolgd door Hallo-naam van het Hallo-methode.</span><span class="sxs-lookup"><span data-stu-id="647d6-174">Method handler names must start with `On` followed by hello name of hello method.</span></span> <span data-ttu-id="647d6-175">Hallo **methodRequest** parameter met de methodeaanroep Hallo van Hallo back-end oplossing doorgegeven parameters bevat.</span><span class="sxs-lookup"><span data-stu-id="647d6-175">hello **methodRequest** parameter contains any parameters passed with hello method invocation from hello solution back end.</span></span> <span data-ttu-id="647d6-176">Hallo retourwaarde moet van het type **taak&lt;MethodResponse&gt;**.</span><span class="sxs-lookup"><span data-stu-id="647d6-176">hello return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="647d6-177">Hallo **BuildMethodResponse** hulpprogramma methode kunt u de retourwaarde Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="647d6-177">hello **BuildMethodResponse** utility method helps you create hello return value.</span></span>

<span data-ttu-id="647d6-178">Binnen Hallo methode handler, kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="647d6-178">Inside hello method handler, you could:</span></span>

- <span data-ttu-id="647d6-179">Een asynchrone taak gestart.</span><span class="sxs-lookup"><span data-stu-id="647d6-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="647d6-180">Eigenschappen van de gewenste ophalen van Hallo *apparaat twin* in IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="647d6-180">Retrieve desired properties from hello *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="647d6-181">Bijwerken van één gemelde eigenschap Hallo met **SetReportedPropertyAsync** methode in Hallo **CoolerDevice** klasse.</span><span class="sxs-lookup"><span data-stu-id="647d6-181">Update a single reported property using hello **SetReportedPropertyAsync** method in hello **CoolerDevice** class.</span></span>
- <span data-ttu-id="647d6-182">De eigenschappen van meerdere gemelde bijwerken door het maken van een **TwinCollection** exemplaar en aanroepen Hallo **Transport.UpdateReportedPropertiesAsync** methode.</span><span class="sxs-lookup"><span data-stu-id="647d6-182">Update multiple reported properties by creating a **TwinCollection** instance and calling hello **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="647d6-183">Hallo voert voorgaande voorbeeld voor firmware-update Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="647d6-183">hello preceding firmware update example performs hello following steps:</span></span>

- <span data-ttu-id="647d6-184">Controles Hallo apparaat is een aanvraag kunnen tooaccept Hallo firmware-update.</span><span class="sxs-lookup"><span data-stu-id="647d6-184">Checks hello device is able tooaccept hello firmware update request.</span></span>
- <span data-ttu-id="647d6-185">Asynchroon Hallo firmware-update-bewerking initieert en herstelt u de Hallo telemetrie wanneer Hallo voltooid is.</span><span class="sxs-lookup"><span data-stu-id="647d6-185">Asynchronously initiates hello firmware update operation and resets hello telemetry when hello operation is complete.</span></span>
- <span data-ttu-id="647d6-186">Onmiddellijk retourneert 'FirmwareUpdate geaccepteerd' Hallo worden bericht tooindicate Hallo-aanvraag is geaccepteerd door Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="647d6-186">Immediately returns hello "FirmwareUpdate accepted" message tooindicate hello request was accepted by hello device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="647d6-187">Opbouwen en uw eigen (fysiek) apparaat gebruiken</span><span class="sxs-lookup"><span data-stu-id="647d6-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="647d6-188">Hallo [Azure IoT SDK's](https://github.com/Azure/azure-iot-sdks) bibliotheken voor het verbinden van verschillende typen apparaten (talen en besturingssystemen) in IoT-oplossingen bieden.</span><span class="sxs-lookup"><span data-stu-id="647d6-188">hello [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="647d6-189">Limieten van dashboard wijzigen</span><span class="sxs-lookup"><span data-stu-id="647d6-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="647d6-190">Aantal apparaten weergegeven in de vervolgkeuzelijst dashboard</span><span class="sxs-lookup"><span data-stu-id="647d6-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="647d6-191">Hallo standaardwaarde is 200.</span><span class="sxs-lookup"><span data-stu-id="647d6-191">hello default is 200.</span></span> <span data-ttu-id="647d6-192">U kunt dit nummer in wijzigen [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="647d6-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a><span data-ttu-id="647d6-193">Het aantal pincodes toodisplay in besturingselement Bing-kaart</span><span class="sxs-lookup"><span data-stu-id="647d6-193">Number of pins toodisplay in Bing Map control</span></span>

<span data-ttu-id="647d6-194">Hallo standaardwaarde is 200.</span><span class="sxs-lookup"><span data-stu-id="647d6-194">hello default is 200.</span></span> <span data-ttu-id="647d6-195">U kunt dit nummer in wijzigen [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="647d6-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="647d6-196">De periode van telemetrie-grafiek</span><span class="sxs-lookup"><span data-stu-id="647d6-196">Time period of telemetry graph</span></span>

<span data-ttu-id="647d6-197">Hallo standaardwaarde is 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="647d6-197">hello default is 10 minutes.</span></span> <span data-ttu-id="647d6-198">U kunt deze waarde in wijzigen [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="647d6-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="647d6-199">Toepassingsrollen handmatig instellen</span><span class="sxs-lookup"><span data-stu-id="647d6-199">Manually set up application roles</span></span>

<span data-ttu-id="647d6-200">Hallo volgende procedure wordt beschreven hoe tooadd **Admin** en **ReadOnly** toepassing rollen tooa vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="647d6-200">hello following procedure describes how tooadd **Admin** and **ReadOnly** application roles tooa preconfigured solution.</span></span> <span data-ttu-id="647d6-201">Houd er rekening mee dat vooraf geconfigureerde oplossingen al ingericht van Hallo azureiotsuite.com site Hallo **Admin** en **ReadOnly** rollen.</span><span class="sxs-lookup"><span data-stu-id="647d6-201">Note that preconfigured solutions provisioned from hello azureiotsuite.com site already include hello **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="647d6-202">Leden van Hallo **ReadOnly** rol Hallo dashboard en de lijst met apparaten Hallo kunt zien, maar zijn niet toegestaan tooadd apparaten, apparaatkenmerken wijzigen of de opdrachten voor verzenden.</span><span class="sxs-lookup"><span data-stu-id="647d6-202">Members of hello **ReadOnly** role can see hello dashboard and hello device list, but are not allowed tooadd devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="647d6-203">Leden van Hallo **Admin** rol hebben volledige toegang tooall Hallo functionaliteit in Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="647d6-203">Members of hello **Admin** role have full access tooall hello functionality in hello solution.</span></span>

1. <span data-ttu-id="647d6-204">Ga toohello [klassieke Azure-portal][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="647d6-204">Go toohello [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="647d6-205">Selecteer **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="647d6-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="647d6-206">Klik op de naam Hallo van Hallo AAD-tenant die u hebt gebruikt toen u uw oplossing hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="647d6-206">Click hello name of hello AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="647d6-207">Klik op **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="647d6-207">Click **Applications**.</span></span>
5. <span data-ttu-id="647d6-208">Klik op Hallo-naam van de toepassing hello die overeenkomt met de naam van uw vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="647d6-208">Click hello name of hello application that matches your preconfigured solution name.</span></span> <span data-ttu-id="647d6-209">Als u uw toepassing in de lijst Hallo niet ziet, selecteert u **toepassingen mijn bedrijf eigenaar is van** in Hallo **weergeven** vervolgkeuzelijst en klik op Hallo selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="647d6-209">If you don't see your application in hello list, select **Applications my company owns** in hello **Show** dropdown and click hello check mark.</span></span>
6. <span data-ttu-id="647d6-210">Klik onder aan de pagina Hallo Hallo op **beheren Manifest** en vervolgens **downloaden Manifest**.</span><span class="sxs-lookup"><span data-stu-id="647d6-210">At hello bottom of hello page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="647d6-211">Deze procedure downloadt een .json-bestand tooyour lokale machine.</span><span class="sxs-lookup"><span data-stu-id="647d6-211">This procedure downloads a .json file tooyour local machine.</span></span> <span data-ttu-id="647d6-212">Open dit bestand bewerken in een teksteditor van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="647d6-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="647d6-213">Op de derde regel Hallo van Hallo .json-bestand, kunt u het volgende zien:</span><span class="sxs-lookup"><span data-stu-id="647d6-213">On hello third line of hello .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="647d6-214">Deze regel vervangen door Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="647d6-214">Replace this line with hello following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="647d6-215">Sla Hallo bijgewerkte .json-bestand (u kunt Hallo bestaand bestand overschrijven).</span><span class="sxs-lookup"><span data-stu-id="647d6-215">Save hello updated .json file (you can overwrite hello existing file).</span></span>
10. <span data-ttu-id="647d6-216">Selecteer in de klassieke Azure-portal onderaan Hallo Hallo pagina Hallo **beheren Manifest** vervolgens **uploaden Manifest** tooupload hello .json-bestand die u in de vorige stap Hallo opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="647d6-216">In hello Azure classic portal, at hello bottom of hello page, select **Manage Manifest** then **Upload Manifest** tooupload hello .json file you saved in hello previous step.</span></span>
11. <span data-ttu-id="647d6-217">U hebt nu toegevoegd Hallo **Admin** en **ReadOnly** rollen tooyour toepassing.</span><span class="sxs-lookup"><span data-stu-id="647d6-217">You have now added hello **Admin** and **ReadOnly** roles tooyour application.</span></span>
12. <span data-ttu-id="647d6-218">Zie tooassign een van deze rollen tooa gebruiker in uw directory [machtigingen op Hallo azureiotsuite.com site][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="647d6-218">tooassign one of these roles tooa user in your directory, see [Permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="647d6-219">Feedback</span><span class="sxs-lookup"><span data-stu-id="647d6-219">Feedback</span></span>

<span data-ttu-id="647d6-220">Hebt u het gewenste toosee in dit document behandeld aanpassen?</span><span class="sxs-lookup"><span data-stu-id="647d6-220">Do you have a customization you'd like toosee covered in this document?</span></span> <span data-ttu-id="647d6-221">Suggesties voor functies te toevoegen[User Voice](https://feedback.azure.com/forums/321918-azure-iot), of de opmerking bij dit artikel.</span><span class="sxs-lookup"><span data-stu-id="647d6-221">Add feature suggestions too[User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="647d6-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="647d6-222">Next steps</span></span>

<span data-ttu-id="647d6-223">toolearn meer informatie over het Hallo-opties voor het aanpassen van Hallo vooraf geconfigureerde oplossingen, Zie:</span><span class="sxs-lookup"><span data-stu-id="647d6-223">toolearn more about hello options for customizing hello preconfigured solutions, see:</span></span>

* <span data-ttu-id="647d6-224">[Logische App tooyour Azure IoT Suite Remote Monitoring vooraf geconfigureerde oplossing verbinden][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="647d6-224">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="647d6-225">[Gebruik dynamische telemetrie Hello vooraf geconfigureerde oplossing voor externe controle][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="647d6-225">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="647d6-226">[Metagegevens van apparaten informatie in Hallo vooraf geconfigureerde oplossing voor externe controle][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="647d6-226">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="647d6-227">[Aanpassen hoe Hallo factory oplossing geeft gegevens van uw servers OPC UA verbonden][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="647d6-227">[Customize how hello connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md
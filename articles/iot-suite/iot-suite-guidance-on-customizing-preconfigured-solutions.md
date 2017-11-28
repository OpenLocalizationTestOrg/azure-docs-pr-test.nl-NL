---
title: Aanpassen van vooraf geconfigureerde oplossingen | Microsoft Docs
description: Biedt richtlijnen voor het aanpassen van de vooraf geconfigureerde Azure IoT Suite-oplossingen.
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
ms.openlocfilehash: bdf4cd89d5ad0392337dfe761108608d506adf18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="7beca-103">Een vooraf geconfigureerde oplossing aanpassen</span><span class="sxs-lookup"><span data-stu-id="7beca-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="7beca-104">De vooraf geconfigureerde oplossingen die zijn opgegeven met de Azure IoT Suite laten zien dat de services in de suite die samenwerken voor het leveren van een end-to-end-oplossing.</span><span class="sxs-lookup"><span data-stu-id="7beca-104">The preconfigured solutions provided with the Azure IoT Suite demonstrate the services within the suite working together to deliver an end-to-end solution.</span></span> <span data-ttu-id="7beca-105">Vanaf deze beginpunt zijn er verschillende plaatsen in die u kunt uitbreiden en aanpassen van de oplossing voor specifieke scenario's.</span><span class="sxs-lookup"><span data-stu-id="7beca-105">From this starting point, there are various places in which you can extend and customize the solution for specific scenarios.</span></span> <span data-ttu-id="7beca-106">De volgende secties worden deze common aanpassing punten.</span><span class="sxs-lookup"><span data-stu-id="7beca-106">The following sections describe these common customization points.</span></span>

## <a name="find-the-source-code"></a><span data-ttu-id="7beca-107">De broncode vinden</span><span class="sxs-lookup"><span data-stu-id="7beca-107">Find the source code</span></span>

<span data-ttu-id="7beca-108">De broncode voor de vooraf geconfigureerde oplossingen is beschikbaar op GitHub in de volgende opslagplaatsen:</span><span class="sxs-lookup"><span data-stu-id="7beca-108">The source code for the preconfigured solutions is available on GitHub in the following repositories:</span></span>

* <span data-ttu-id="7beca-109">Externe controle: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="7beca-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="7beca-110">Voorspeld onderhoud: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="7beca-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="7beca-111">Verbonden factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="7beca-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="7beca-112">De broncode voor de vooraf geconfigureerde oplossingen is voor het demonstreren van de patronen en procedures die worden gebruikt voor het implementeren van de functionaliteit van de end-to-end van een IoT-oplossing met behulp van Azure IoT Suite opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7beca-112">The source code for the preconfigured solutions is provided to demonstrate the patterns and practices used to implement the end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="7beca-113">U vindt meer informatie over het maken en implementeren van de oplossingen in de GitHub-opslagplaatsen.</span><span class="sxs-lookup"><span data-stu-id="7beca-113">You can find more information about how to build and deploy the solutions in the GitHub repositories.</span></span>

## <a name="change-the-preconfigured-rules"></a><span data-ttu-id="7beca-114">De vooraf geconfigureerde regels wijzigen</span><span class="sxs-lookup"><span data-stu-id="7beca-114">Change the preconfigured rules</span></span>

<span data-ttu-id="7beca-115">De oplossing voor externe controle omvat drie [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) taken voor het afhandelen van apparaatgegevens, Telemetrie en regellogica in de oplossing.</span><span class="sxs-lookup"><span data-stu-id="7beca-115">The remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs to handle device information, telemetry, and rules logic in the solution.</span></span>

<span data-ttu-id="7beca-116">De drie stream analytics-taken en hun syntaxis worden beschreven in de diepte in de [externe controle oplossing walkthrough over vooraf geconfigureerde](iot-suite-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="7beca-116">The three stream analytics jobs and their syntax are described in depth in the [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="7beca-117">U kunt deze taken om de logica alter rechtstreeks te bewerken of voeg specifieke logica toe aan uw scenario.</span><span class="sxs-lookup"><span data-stu-id="7beca-117">You can edit these jobs directly to alter the logic, or add logic specific to your scenario.</span></span> <span data-ttu-id="7beca-118">U vindt de Stream Analytics-taken als volgt:</span><span class="sxs-lookup"><span data-stu-id="7beca-118">You can find the Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="7beca-119">Ga naar [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7beca-119">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7beca-120">Navigeer naar de resourcegroep met dezelfde naam als uw IoT-oplossing.</span><span class="sxs-lookup"><span data-stu-id="7beca-120">Navigate to the resource group with the same name as your IoT solution.</span></span> 
3. <span data-ttu-id="7beca-121">Selecteer de Azure Stream Analytics-taak die u wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7beca-121">Select the Azure Stream Analytics job you'd like to modify.</span></span> 
4. <span data-ttu-id="7beca-122">De taak stoppen als u selecteert **stoppen** in de reeks opdrachten.</span><span class="sxs-lookup"><span data-stu-id="7beca-122">Stop the job by selecting **Stop** in the set of commands.</span></span> 
5. <span data-ttu-id="7beca-123">Bewerk de invoer-, query- en uitvoer.</span><span class="sxs-lookup"><span data-stu-id="7beca-123">Edit the inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="7beca-124">Een eenvoudige wijziging wordt gewijzigd van de query voor de **regels** taak voor het gebruik van een **' < '** in plaats van een **' > '**.</span><span class="sxs-lookup"><span data-stu-id="7beca-124">A simple modification is to change the query for the **Rules** job to use a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="7beca-125">Nog steeds weergegeven in de oplossingsportal **' > '** wanneer u een regel voor het bewerken, maar u ziet hoe het gedrag als gevolg van de wijziging in de onderliggende taak wordt gespiegeld.</span><span class="sxs-lookup"><span data-stu-id="7beca-125">The solution portal still shows **">"** when you edit a rule, but notice how the behavior is flipped due to the change in the underlying job.</span></span>
6. <span data-ttu-id="7beca-126">Start de taak</span><span class="sxs-lookup"><span data-stu-id="7beca-126">Start the job</span></span>

> [!NOTE]
> <span data-ttu-id="7beca-127">Het dashboard voor externe controle, is afhankelijk van wat u specifieke gegevens dus wijzigen van de taken leiden het dashboard tot kan mislukken.</span><span class="sxs-lookup"><span data-stu-id="7beca-127">The remote monitoring dashboard depends on specific data, so altering the jobs can cause the dashboard to fail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="7beca-128">Uw eigen regels toevoegen</span><span class="sxs-lookup"><span data-stu-id="7beca-128">Add your own rules</span></span>

<span data-ttu-id="7beca-129">Naast de vooraf geconfigureerde Azure Stream Analytics-taken te wijzigen, kunt u de Azure-portal nieuwe taken toevoegen of nieuwe query's toevoegen aan bestaande projecten.</span><span class="sxs-lookup"><span data-stu-id="7beca-129">In addition to changing the preconfigured Azure Stream Analytics jobs, you can use the Azure portal to add new jobs or add new queries to existing jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="7beca-130">Apparaten aanpassen</span><span class="sxs-lookup"><span data-stu-id="7beca-130">Customize devices</span></span>

<span data-ttu-id="7beca-131">Een van de meest voorkomende extensie activiteiten werkt samen met apparaten die specifiek zijn voor uw scenario.</span><span class="sxs-lookup"><span data-stu-id="7beca-131">One of the most common extension activities is working with devices specific to your scenario.</span></span> <span data-ttu-id="7beca-132">Er zijn verschillende methoden voor het werken met apparaten.</span><span class="sxs-lookup"><span data-stu-id="7beca-132">There are several methods for working with devices.</span></span> <span data-ttu-id="7beca-133">Deze methoden omvatten een gesimuleerd apparaat zodat deze overeenkomen met uw scenario te wijzigen of met behulp van de [IoT Device SDK] [ IoT Device SDK] uw fysieke apparaat aan de oplossing te sluiten.</span><span class="sxs-lookup"><span data-stu-id="7beca-133">These methods include altering a simulated device to match your scenario, or using the [IoT Device SDK][IoT Device SDK] to connect your physical device to the solution.</span></span>

<span data-ttu-id="7beca-134">Zie voor een stapsgewijze handleiding voor het toevoegen van apparaten, de [Iot Suite-verbinding maken met apparaten](iot-suite-connecting-devices.md) artikel en de [van een remote monitoring C SDK voorbeeld](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span><span class="sxs-lookup"><span data-stu-id="7beca-134">For a step-by-step guide to adding devices, see the [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and the [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="7beca-135">Dit voorbeeld is ontworpen voor gebruik met de vooraf geconfigureerde oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="7beca-135">This sample is designed to work with the remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="7beca-136">Uw eigen gesimuleerd apparaat kunt maken</span><span class="sxs-lookup"><span data-stu-id="7beca-136">Create your own simulated device</span></span>

<span data-ttu-id="7beca-137">Opgenomen in de [voor externe controle oplossing broncode](https://github.com/Azure/azure-iot-remote-monitoring), is een .NET-simulator.</span><span class="sxs-lookup"><span data-stu-id="7beca-137">Included in the [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="7beca-138">Deze simulator is ingericht als onderdeel van de oplossing en u kunt wijzigen en andere metagegevens, telemetrie verzenden en reageren op andere opdrachten en -methoden.</span><span class="sxs-lookup"><span data-stu-id="7beca-138">This simulator is the one provisioned as part of the solution and you can alter it to send different metadata, telemetry, and respond to different commands and methods.</span></span>

<span data-ttu-id="7beca-139">De vooraf geconfigureerde simulator in de vooraf geconfigureerde oplossing voor externe controle een koelervoorbeeld apparaat simuleert dat temperatuur en vochtigheid telemetrie verzendt.</span><span class="sxs-lookup"><span data-stu-id="7beca-139">The preconfigured simulator in the remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="7beca-140">U kunt de simulator in wijzigen de [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) wanneer u hebt de GitHub-opslagplaats forked project.</span><span class="sxs-lookup"><span data-stu-id="7beca-140">You can modify the simulator in the [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked the GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="7beca-141">Beschikbare locaties voor de gesimuleerde apparaten</span><span class="sxs-lookup"><span data-stu-id="7beca-141">Available locations for simulated devices</span></span>

<span data-ttu-id="7beca-142">Er is een reeks locaties in Seattle/Redmond, Washington, Verenigde Staten van Amerika.</span><span class="sxs-lookup"><span data-stu-id="7beca-142">The default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="7beca-143">U kunt deze locaties in wijzigen [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="7beca-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-to-the-simulator"></a><span data-ttu-id="7beca-144">Een updatehandler gewenste eigenschap toevoegen aan de simulator</span><span class="sxs-lookup"><span data-stu-id="7beca-144">Add a desired property update handler to the simulator</span></span>

<span data-ttu-id="7beca-145">U kunt een waarde voor een gewenste eigenschap voor een apparaat in de oplossingsportal instellen.</span><span class="sxs-lookup"><span data-stu-id="7beca-145">You can set a value for a desired property for a device in the solution portal.</span></span> <span data-ttu-id="7beca-146">Het is de verantwoordelijkheid van het apparaat voor het afhandelen van de eigenschap wijzigingsaanvraag wanneer het apparaat wordt de gewenste eigenschapswaarde opgehaald.</span><span class="sxs-lookup"><span data-stu-id="7beca-146">It is the responsibility of the device to handle the property change request when the device retrieves the desired property value.</span></span> <span data-ttu-id="7beca-147">U voegt ondersteuning voor een wijziging van de eigenschap waarde via een gewenste eigenschap, moet u een handler toevoegen aan de simulator.</span><span class="sxs-lookup"><span data-stu-id="7beca-147">To add support for a property value change through a desired property, you need to add a handler to the simulator.</span></span>

<span data-ttu-id="7beca-148">De simulator handlers bevat voor de **SetPointTemp** en **TelemetryInterval** eigenschappen die u bijwerken door het instellen van kunt de gewenste waarden in de portal van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="7beca-148">The simulator contains handlers for the **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in the solution portal.</span></span>

<span data-ttu-id="7beca-149">Het volgende voorbeeld ziet u de handler voor de **SetPointTemp** gewenst eigenschap in de **CoolerDevice** klasse:</span><span class="sxs-lookup"><span data-stu-id="7beca-149">The following example shows the handler for the **SetPointTemp** desired property in the **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="7beca-150">Deze methode werkt de telemetrie punt temperatuur en vervolgens meldt deze wijziging terug naar IoT Hub door een eigenschap gemeld.</span><span class="sxs-lookup"><span data-stu-id="7beca-150">This method updates the telemetry point temperature and then reports the change back to IoT Hub by setting a reported property.</span></span>

<span data-ttu-id="7beca-151">U kunt uw eigen handlers voor uw eigen eigenschappen toevoegen aan de hand van het patroon in het voorgaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7beca-151">You can add your own handlers for your own properties by following the pattern in the preceding example.</span></span>

<span data-ttu-id="7beca-152">U moet ook de gewenste eigenschap binden aan de handler zoals weergegeven in het volgende voorbeeld uit de **CoolerDevice** constructor:</span><span class="sxs-lookup"><span data-stu-id="7beca-152">You must also bind the desired property to the handler as shown in the following example from the **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="7beca-153">Houd er rekening mee dat **SetPointTempPropertyName** een constante is gedefinieerd als 'Config.SetPointTemp'.</span><span class="sxs-lookup"><span data-stu-id="7beca-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-to-the-simulator"></a><span data-ttu-id="7beca-154">Ondersteuning voor een nieuwe methode toevoegen aan de simulator</span><span class="sxs-lookup"><span data-stu-id="7beca-154">Add support for a new method to the simulator</span></span>

<span data-ttu-id="7beca-155">U kunt de simulator om ondersteuning voor een nieuwe [methode (directe methode)][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="7beca-155">You can customize the simulator to add support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="7beca-156">Er zijn twee belangrijke stappen vereist:</span><span class="sxs-lookup"><span data-stu-id="7beca-156">There are two key steps required:</span></span>

- <span data-ttu-id="7beca-157">De simulator verwittigt de IoT-hub in de vooraf geconfigureerde oplossing met details van de methode.</span><span class="sxs-lookup"><span data-stu-id="7beca-157">The simulator must notify the IoT hub in the preconfigured solution with details of the method.</span></span>
- <span data-ttu-id="7beca-158">De simulator vergezeld gaan van code voor het afhandelen van de methodeaanroep van wanneer u vanuit aanroept de **Apparaatdetails** deelvenster in solution explorer of via een taak.</span><span class="sxs-lookup"><span data-stu-id="7beca-158">The simulator must include code to handle the method call when you invoke it from the **Device details** panel in the solution explorer or through a job.</span></span>

<span data-ttu-id="7beca-159">Externe controle vooraf geconfigureerde oplossing maakt gebruik van *eigenschappen gerapporteerd* details van ondersteunde methoden naar IoT-hub te verzenden.</span><span class="sxs-lookup"><span data-stu-id="7beca-159">The remote monitoring preconfigured solution uses *reported properties* to send details of supported methods to IoT hub.</span></span> <span data-ttu-id="7beca-160">De back-end oplossing houdt een lijst van alle methoden die worden ondersteund door elk apparaat samen met een geschiedenis van methode aanroepen.</span><span class="sxs-lookup"><span data-stu-id="7beca-160">The solution back end maintains a list of all the methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="7beca-161">U kunt deze informatie weergeven over apparaten en methoden aanroepen in de portal van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="7beca-161">You can view this information about devices and invoke methods in the solution portal.</span></span>

<span data-ttu-id="7beca-162">Melding van de IoT-hub die een apparaat ondersteunt een methode, het apparaat moet details van de methode voor het toevoegen de **SupportedMethods** knooppunt in de gerapporteerde eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="7beca-162">To notify the IoT hub that a device supports a method, the device must add details of the method to the **SupportedMethods** node in the reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="7beca-163">De methodehandtekening heeft de volgende indeling: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="7beca-163">The method signature has the following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="7beca-164">Bijvoorbeeld, om op te geven de **InitiateFirmwareUpdate** methode verwacht een tekenreeksparameter met de naam **FwPackageURI**, gebruikt u de volgende methodehandtekening:</span><span class="sxs-lookup"><span data-stu-id="7beca-164">For example, to specify the **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use the following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="7beca-165">Zie voor een lijst van ondersteunde parametertypen de **CommandTypes** klasse in het project voor de infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="7beca-165">For a list of supported parameter types, see the **CommandTypes** class in the Infrastructure project.</span></span>

<span data-ttu-id="7beca-166">Stel voor het verwijderen van een methode in de methodehandtekening op `null` in de eigenschappen van gemeld.</span><span class="sxs-lookup"><span data-stu-id="7beca-166">To delete a method, set the method signature to `null` in the reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="7beca-167">De back-end oplossing informatie over ondersteunde methodes alleen bijgewerkt wanneer het ontvangt een *apparaatgegevens* bericht van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="7beca-167">The solution back end only updates information about supported methods when it receives a *device information* message from the device.</span></span>

<span data-ttu-id="7beca-168">Het volgende codevoorbeeld van de **SampleDeviceFactory** klasse in het algemene project ziet u hoe u een methode toevoegen aan de lijst met **SupportedMethods** in de gerapporteerde eigenschappen is verzonden door het apparaat:</span><span class="sxs-lookup"><span data-stu-id="7beca-168">The following code sample from the **SampleDeviceFactory** class in the Common project shows how to add a method to the list of **SupportedMethods** in the reported properties sent by the device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' to specifiy the URI of the firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="7beca-169">Dit codefragment voegt details van de **InitiateFirmwareUpdate** methode, met inbegrip van tekst moet worden weergegeven in de portal van de oplossing en de details van de vereiste methode-parameters.</span><span class="sxs-lookup"><span data-stu-id="7beca-169">This code snippet adds details of the **InitiateFirmwareUpdate** method including text to display in the solution portal and details of the required method parameters.</span></span>

<span data-ttu-id="7beca-170">De simulator verzendt gemelde eigenschappen, met inbegrip van de lijst met ondersteunde methoden, IoT-hub wanneer de simulator wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="7beca-170">The simulator sends reported properties, including the list of supported methods, to IoT Hub when the simulator starts.</span></span>

<span data-ttu-id="7beca-171">Een handler toevoegen aan de simulator code voor elke methode ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7beca-171">Add a handler to the simulator code for each method it supports.</span></span> <span data-ttu-id="7beca-172">Ziet u de bestaande handlers in de **CoolerDevice** klasse in het project Simulator.WebJob.</span><span class="sxs-lookup"><span data-stu-id="7beca-172">You can see the existing handlers in the **CoolerDevice** class in the Simulator.WebJob project.</span></span> <span data-ttu-id="7beca-173">Het volgende voorbeeld ziet u de handler voor **InitiateFirmwareUpdate** methode:</span><span class="sxs-lookup"><span data-stu-id="7beca-173">The following example shows the handler for **InitiateFirmwareUpdate** method:</span></span>

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

<span data-ttu-id="7beca-174">Methode handler namen moeten beginnen met `On` gevolgd door de naam van de methode.</span><span class="sxs-lookup"><span data-stu-id="7beca-174">Method handler names must start with `On` followed by the name of the method.</span></span> <span data-ttu-id="7beca-175">De **methodRequest** parameter met de aanroepen van de methode van de back-end oplossing doorgegeven parameters bevat.</span><span class="sxs-lookup"><span data-stu-id="7beca-175">The **methodRequest** parameter contains any parameters passed with the method invocation from the solution back end.</span></span> <span data-ttu-id="7beca-176">De retourwaarde moet van het type **taak&lt;MethodResponse&gt;**.</span><span class="sxs-lookup"><span data-stu-id="7beca-176">The return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="7beca-177">De **BuildMethodResponse** hulpprogramma methode kunt u de retourwaarde maken.</span><span class="sxs-lookup"><span data-stu-id="7beca-177">The **BuildMethodResponse** utility method helps you create the return value.</span></span>

<span data-ttu-id="7beca-178">Binnen de handler methode kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="7beca-178">Inside the method handler, you could:</span></span>

- <span data-ttu-id="7beca-179">Een asynchrone taak gestart.</span><span class="sxs-lookup"><span data-stu-id="7beca-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="7beca-180">Ophalen van de gewenste eigenschappen van de *apparaat twin* in IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="7beca-180">Retrieve desired properties from the *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="7beca-181">Bijwerken van een enkele gemelde eigenschap met de **SetReportedPropertyAsync** methode in de **CoolerDevice** klasse.</span><span class="sxs-lookup"><span data-stu-id="7beca-181">Update a single reported property using the **SetReportedPropertyAsync** method in the **CoolerDevice** class.</span></span>
- <span data-ttu-id="7beca-182">De eigenschappen van meerdere gemelde bijwerken door het maken van een **TwinCollection** exemplaar en het aanroepen van de **Transport.UpdateReportedPropertiesAsync** methode.</span><span class="sxs-lookup"><span data-stu-id="7beca-182">Update multiple reported properties by creating a **TwinCollection** instance and calling the **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="7beca-183">Het voorgaande voorbeeld van de firmware-update voert de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7beca-183">The preceding firmware update example performs the following steps:</span></span>

- <span data-ttu-id="7beca-184">Controleert dat het apparaat kan de aanvraag voor firmware-update accepteren.</span><span class="sxs-lookup"><span data-stu-id="7beca-184">Checks the device is able to accept the firmware update request.</span></span>
- <span data-ttu-id="7beca-185">Asynchroon initieert de updatebewerking firmware en de telemetrie weer ingesteld als de bewerking voltooid is.</span><span class="sxs-lookup"><span data-stu-id="7beca-185">Asynchronously initiates the firmware update operation and resets the telemetry when the operation is complete.</span></span>
- <span data-ttu-id="7beca-186">Retourneert onmiddellijk het bericht 'FirmwareUpdate geaccepteerd' om aan te geven van dat de aanvraag is geaccepteerd door het apparaat.</span><span class="sxs-lookup"><span data-stu-id="7beca-186">Immediately returns the "FirmwareUpdate accepted" message to indicate the request was accepted by the device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="7beca-187">Opbouwen en uw eigen (fysiek) apparaat gebruiken</span><span class="sxs-lookup"><span data-stu-id="7beca-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="7beca-188">De [Azure IoT SDK's](https://github.com/Azure/azure-iot-sdks) bibliotheken voor het verbinden van verschillende typen apparaten (talen en besturingssystemen) in IoT-oplossingen bieden.</span><span class="sxs-lookup"><span data-stu-id="7beca-188">The [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="7beca-189">Limieten van dashboard wijzigen</span><span class="sxs-lookup"><span data-stu-id="7beca-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="7beca-190">Aantal apparaten weergegeven in de vervolgkeuzelijst dashboard</span><span class="sxs-lookup"><span data-stu-id="7beca-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="7beca-191">De standaardwaarde is 200.</span><span class="sxs-lookup"><span data-stu-id="7beca-191">The default is 200.</span></span> <span data-ttu-id="7beca-192">U kunt dit nummer in wijzigen [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="7beca-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-to-display-in-bing-map-control"></a><span data-ttu-id="7beca-193">Het aantal pincodes dat wordt weergegeven in het kaartbesturingselement van Bing</span><span class="sxs-lookup"><span data-stu-id="7beca-193">Number of pins to display in Bing Map control</span></span>

<span data-ttu-id="7beca-194">De standaardwaarde is 200.</span><span class="sxs-lookup"><span data-stu-id="7beca-194">The default is 200.</span></span> <span data-ttu-id="7beca-195">U kunt dit nummer in wijzigen [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="7beca-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="7beca-196">De periode van telemetrie-grafiek</span><span class="sxs-lookup"><span data-stu-id="7beca-196">Time period of telemetry graph</span></span>

<span data-ttu-id="7beca-197">De standaardwaarde is 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="7beca-197">The default is 10 minutes.</span></span> <span data-ttu-id="7beca-198">U kunt deze waarde in wijzigen [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="7beca-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="7beca-199">Toepassingsrollen handmatig instellen</span><span class="sxs-lookup"><span data-stu-id="7beca-199">Manually set up application roles</span></span>

<span data-ttu-id="7beca-200">De volgende procedure beschrijft hoe u toevoegt **Admin** en **ReadOnly** toepassingsrollen een vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="7beca-200">The following procedure describes how to add **Admin** and **ReadOnly** application roles to a preconfigured solution.</span></span> <span data-ttu-id="7beca-201">Houd er rekening mee dat vooraf geconfigureerde oplossingen al vanaf de site azureiotsuite.com ingericht bevatten de **Admin** en **ReadOnly** rollen.</span><span class="sxs-lookup"><span data-stu-id="7beca-201">Note that preconfigured solutions provisioned from the azureiotsuite.com site already include the **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="7beca-202">Leden van de **ReadOnly** rol kunt het dashboard en de lijst met apparaten zien, maar zijn niet toegestaan voor apparaten toevoegen, wijzigen apparaatkenmerken of opdrachten verzenden.</span><span class="sxs-lookup"><span data-stu-id="7beca-202">Members of the **ReadOnly** role can see the dashboard and the device list, but are not allowed to add devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="7beca-203">Leden van de **Admin** rol hebben volledige toegang tot alle functies in de oplossing.</span><span class="sxs-lookup"><span data-stu-id="7beca-203">Members of the **Admin** role have full access to all the functionality in the solution.</span></span>

1. <span data-ttu-id="7beca-204">Ga naar de [klassieke Azure-portal][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="7beca-204">Go to the [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="7beca-205">Selecteer **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7beca-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="7beca-206">Klik op de naam van de AAD-tenant die u hebt gebruikt toen u uw oplossing hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="7beca-206">Click the name of the AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="7beca-207">Klik op **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7beca-207">Click **Applications**.</span></span>
5. <span data-ttu-id="7beca-208">Klik op de naam van de toepassing die overeenkomt met de naam van uw vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="7beca-208">Click the name of the application that matches your preconfigured solution name.</span></span> <span data-ttu-id="7beca-209">Als u uw toepassing in de lijst niet ziet, selecteert u **toepassingen mijn bedrijf eigenaar is van** in de **weergeven** vervolgkeuzelijst en klik op het vinkje.</span><span class="sxs-lookup"><span data-stu-id="7beca-209">If you don't see your application in the list, select **Applications my company owns** in the **Show** dropdown and click the check mark.</span></span>
6. <span data-ttu-id="7beca-210">Klik onder aan de pagina op **beheren Manifest** en vervolgens **downloaden Manifest**.</span><span class="sxs-lookup"><span data-stu-id="7beca-210">At the bottom of the page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="7beca-211">Deze procedure downloadt een .json-bestand naar uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="7beca-211">This procedure downloads a .json file to your local machine.</span></span> <span data-ttu-id="7beca-212">Open dit bestand bewerken in een teksteditor van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="7beca-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="7beca-213">Op de derde regel van het .json-bestand, kunt u het volgende zien:</span><span class="sxs-lookup"><span data-stu-id="7beca-213">On the third line of the .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="7beca-214">Deze regel wordt vervangen door de volgende code:</span><span class="sxs-lookup"><span data-stu-id="7beca-214">Replace this line with the following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access to the application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access to device information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="7beca-215">Sla het bijgewerkte .json-bestand (u kunt het bestaande bestand overschrijven).</span><span class="sxs-lookup"><span data-stu-id="7beca-215">Save the updated .json file (you can overwrite the existing file).</span></span>
10. <span data-ttu-id="7beca-216">Selecteer in de klassieke Azure-portal aan de onderkant van de pagina **beheren Manifest** vervolgens **uploaden Manifest** voor het uploaden van de .json-bestand dat u in de vorige stap hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7beca-216">In the Azure classic portal, at the bottom of the page, select **Manage Manifest** then **Upload Manifest** to upload the .json file you saved in the previous step.</span></span>
11. <span data-ttu-id="7beca-217">U hebt nu toegevoegd de **Admin** en **ReadOnly** functies aan uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7beca-217">You have now added the **Admin** and **ReadOnly** roles to your application.</span></span>
12. <span data-ttu-id="7beca-218">Zie voor een van deze rollen toewijzen aan een gebruiker in uw directory, [machtigingen op de site azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="7beca-218">To assign one of these roles to a user in your directory, see [Permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="7beca-219">Feedback</span><span class="sxs-lookup"><span data-stu-id="7beca-219">Feedback</span></span>

<span data-ttu-id="7beca-220">Hebt u een aanpassing u zou willen zien in dit document gedekte?</span><span class="sxs-lookup"><span data-stu-id="7beca-220">Do you have a customization you'd like to see covered in this document?</span></span> <span data-ttu-id="7beca-221">Functie suggesties toevoegen aan [User Voice](https://feedback.azure.com/forums/321918-azure-iot), of de opmerking bij dit artikel.</span><span class="sxs-lookup"><span data-stu-id="7beca-221">Add feature suggestions to [User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7beca-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7beca-222">Next steps</span></span>

<span data-ttu-id="7beca-223">Zie voor meer informatie over de opties voor het aanpassen van de vooraf geconfigureerde oplossingen:</span><span class="sxs-lookup"><span data-stu-id="7beca-223">To learn more about the options for customizing the preconfigured solutions, see:</span></span>

* <span data-ttu-id="7beca-224">[Logic App verbinden met uw Azure IoT Suite Remote Monitoring vooraf geconfigureerde oplossing][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="7beca-224">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="7beca-225">[Dynamische telemetrie gebruiken met de vooraf geconfigureerde oplossing voor externe controle][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="7beca-225">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="7beca-226">[Metagegevens van apparaten informatie in de vooraf geconfigureerde oplossing voor externe controle][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="7beca-226">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="7beca-227">[Aanpassen hoe de gegevens van uw OPC UA-servers worden weergegeven in de verbonden factory-oplossing][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="7beca-227">[Customize how the connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

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
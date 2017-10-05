---
title: Walkthrough over vooraf geconfigureerde oplossing voor externe controle | Microsoft Docs
description: Een beschrijving van de vooraf geconfigureerde oplossing voor externe controle IoT Azure en de bijbehorende architectuur.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: b28105f300723b542fa6d1aebc569439d5c73dc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a><span data-ttu-id="c2ef0-103">Walkthrough over vooraf geconfigureerde oplossing voor externe controle</span><span class="sxs-lookup"><span data-stu-id="c2ef0-103">Remote monitoring preconfigured solution walkthrough</span></span>

<span data-ttu-id="c2ef0-104">De [vooraf geconfigureerde oplossing][lnk-preconfigured-solutions] voor externe controle met IoT Suite is een implementatie van een end-to-endoplossing voor controle voor meerdere computers die op externe locaties worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-104">The IoT Suite remote monitoring [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end monitoring solution for multiple machines running in remote locations.</span></span> <span data-ttu-id="c2ef0-105">De oplossing combineert belangrijke Azure-services voor een algemene implementatie van het bedrijfsscenario.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-105">The solution combines key Azure services to provide a generic implementation of the business scenario.</span></span> <span data-ttu-id="c2ef0-106">U kunt de oplossing gebruiken als uitgangspunt voor uw eigen implementatie en u kunt deze [aanpassen][lnk-customize] aan uw eigen specifieke zakelijke vereisten.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-106">You can use the solution as a starting point for your own implementation and [customize][lnk-customize] it to meet your own specific business requirements.</span></span>

<span data-ttu-id="c2ef0-107">In dit artikel wordt stapsgewijs een aantal belangrijke elementen van externe controle beschreven, zodat u beter begrijpt hoe dit werkt.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-107">This article walks you through some of the key elements of the remote monitoring solution to enable you to understand how it works.</span></span> <span data-ttu-id="c2ef0-108">Deze kennis helpt u bij:</span><span class="sxs-lookup"><span data-stu-id="c2ef0-108">This knowledge helps you to:</span></span>

* <span data-ttu-id="c2ef0-109">Het oplossen van problemen met de oplossing.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-109">Troubleshoot issues in the solution.</span></span>
* <span data-ttu-id="c2ef0-110">Het plannen van een aanpassing van de oplossing zodat deze voldoet aan uw eigen specifieke vereisten.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-110">Plan how to customize to the solution to meet your own specific requirements.</span></span> 
* <span data-ttu-id="c2ef0-111">Het ontwerpen van uw eigen IoT-oplossing die gebruikmaakt van Azure-services.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-111">Design your own IoT solution that uses Azure services.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="c2ef0-112">Logische architectuur</span><span class="sxs-lookup"><span data-stu-id="c2ef0-112">Logical architecture</span></span>

<span data-ttu-id="c2ef0-113">Het volgende diagram geeft een overzicht van de logische onderdelen van de vooraf geconfigureerde oplossing:</span><span class="sxs-lookup"><span data-stu-id="c2ef0-113">The following diagram outlines the logical components of the preconfigured solution:</span></span>

![Logische architectuur](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a><span data-ttu-id="c2ef0-115">Gesimuleerde apparaten</span><span class="sxs-lookup"><span data-stu-id="c2ef0-115">Simulated devices</span></span>

<span data-ttu-id="c2ef0-116">In de vooraf geconfigureerde oplossing vertegenwoordigt het gesimuleerde apparaat een koelapparaat (zoals een airconditioner of een luchtververser in een gebouw).</span><span class="sxs-lookup"><span data-stu-id="c2ef0-116">In the preconfigured solution, the simulated device represents a cooling device (such as a building air conditioner or facility air handling unit).</span></span> <span data-ttu-id="c2ef0-117">Wanneer u de vooraf geconfigureerde oplossing implementeert, richt u ook automatisch vier gesimuleerde apparaten in waarop een [Azure-webtaak][lnk-webjobs] wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-117">When you deploy the preconfigured solution, you also automatically provision four simulated devices that run in an [Azure WebJob][lnk-webjobs].</span></span> <span data-ttu-id="c2ef0-118">Met de gesimuleerde apparaten kunt u eenvoudig het gedrag van de oplossing bekijken zonder dat u fysieke apparaten hoeft te implementeren.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-118">The simulated devices make it easy for you to explore the behavior of the solution without the need to deploy any physical devices.</span></span> <span data-ttu-id="c2ef0-119">Zie de zelfstudie [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] (Uw apparaat koppelen aan de vooraf geconfigureerde oplossing voor externe controle) als u een echt fysiek apparaat wilt implementeren.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-119">To deploy a real physical device, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

### <a name="device-to-cloud-messages"></a><span data-ttu-id="c2ef0-120">Apparaat-naar-cloud-berichten</span><span class="sxs-lookup"><span data-stu-id="c2ef0-120">Device-to-cloud messages</span></span>

<span data-ttu-id="c2ef0-121">Via elk gesimuleerd apparaat kunnen de volgende berichttypen worden verzonden naar IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="c2ef0-121">Each simulated device can send the following message types to IoT Hub:</span></span>

| <span data-ttu-id="c2ef0-122">Bericht</span><span class="sxs-lookup"><span data-stu-id="c2ef0-122">Message</span></span> | <span data-ttu-id="c2ef0-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c2ef0-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c2ef0-124">Opstarten</span><span class="sxs-lookup"><span data-stu-id="c2ef0-124">Startup</span></span> |<span data-ttu-id="c2ef0-125">Wanneer het apparaat start, wordt er een bericht over **apparaatgegevens** verzonden naar de back-end met hierin informatie over het apparaat.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-125">When the device starts, it sends a **device-info** message containing information about itself to the back end.</span></span> <span data-ttu-id="c2ef0-126">Deze gegevens omvatten de apparaat-id en een lijst met de opdrachten en methoden die door het apparaat worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-126">This data includes the device id and a list of the commands and methods the device supports.</span></span> |
| <span data-ttu-id="c2ef0-127">Aanwezigheid</span><span class="sxs-lookup"><span data-stu-id="c2ef0-127">Presence</span></span> |<span data-ttu-id="c2ef0-128">Via een apparaat wordt periodiek een bericht verzonden over **aanwezigheid** om te melden of het apparaat de aanwezigheid van een sensor bemerkt.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-128">A device periodically sends a **presence** message to report whether the device can sense the presence of a sensor.</span></span> |
| <span data-ttu-id="c2ef0-129">Telemetrie</span><span class="sxs-lookup"><span data-stu-id="c2ef0-129">Telemetry</span></span> |<span data-ttu-id="c2ef0-130">Via een apparaat wordt periodiek een bericht verzonden over **telemetrie** waarin gesimuleerde waarden voor de temperatuur en vochtigheid worden gemeld die zijn verzameld met de gesimuleerde sensoren van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-130">A device periodically sends a **telemetry** message that reports simulated values for the temperature and humidity collected from the device's simulated sensors.</span></span> |

> [!NOTE]
> <span data-ttu-id="c2ef0-131">De oplossing slaat de lijst met opdrachten die door het apparaat worden ondersteund, op in een Cosmos DB-database en niet in de apparaatdubbel.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-131">The solution stores the list of commands supported by the device in a Cosmos DB database and not in the device twin.</span></span>

### <a name="properties-and-device-twins"></a><span data-ttu-id="c2ef0-132">Eigenschappen en apparaatdubbels</span><span class="sxs-lookup"><span data-stu-id="c2ef0-132">Properties and device twins</span></span>

<span data-ttu-id="c2ef0-133">De gesimuleerde apparaten verzenden de volgende apparaateigenschappen als *gerapporteerde eigenschappen* naar de [dubbele][lnk-device-twins] in de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-133">The simulated devices send the following device properties to the [twin][lnk-device-twins] in the IoT hub as *reported properties*.</span></span> <span data-ttu-id="c2ef0-134">Het apparaat verzendt gerapporteerde eigenschappen bij het opstarten en als reactie op een opdracht of methode voor het **wijzigen van de apparaatstatus**.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-134">The device sends reported properties at startup and in response to a **Change Device State** command or method.</span></span>

| <span data-ttu-id="c2ef0-135">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c2ef0-135">Property</span></span> | <span data-ttu-id="c2ef0-136">Doel</span><span class="sxs-lookup"><span data-stu-id="c2ef0-136">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="c2ef0-137">Config.TelemetryInterval</span><span class="sxs-lookup"><span data-stu-id="c2ef0-137">Config.TelemetryInterval</span></span> | <span data-ttu-id="c2ef0-138">Frequentie (seconden) waarmee het apparaat telemetrie verzendt</span><span class="sxs-lookup"><span data-stu-id="c2ef0-138">Frequency (seconds) the device sends telemetry</span></span> |
| <span data-ttu-id="c2ef0-139">Config.TemperatureMeanValue</span><span class="sxs-lookup"><span data-stu-id="c2ef0-139">Config.TemperatureMeanValue</span></span> | <span data-ttu-id="c2ef0-140">Geeft de gemiddelde waarde voor de gesimuleerde temperatuurtelemetrie</span><span class="sxs-lookup"><span data-stu-id="c2ef0-140">Specifies the mean value for the simulated temperature telemetry</span></span> |
| <span data-ttu-id="c2ef0-141">Device.DeviceID</span><span class="sxs-lookup"><span data-stu-id="c2ef0-141">Device.DeviceID</span></span> |<span data-ttu-id="c2ef0-142">De id die wordt verstrekt of toegewezen wanneer een apparaat in de oplossing wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="c2ef0-142">Id that is either provided or assigned when a device is created in the solution</span></span> |
| <span data-ttu-id="c2ef0-143">Device.DeviceState</span><span class="sxs-lookup"><span data-stu-id="c2ef0-143">Device.DeviceState</span></span> | <span data-ttu-id="c2ef0-144">Status die door het apparaat wordt gemeld</span><span class="sxs-lookup"><span data-stu-id="c2ef0-144">State reported by the device</span></span> |
| <span data-ttu-id="c2ef0-145">Device.CreatedTime</span><span class="sxs-lookup"><span data-stu-id="c2ef0-145">Device.CreatedTime</span></span> |<span data-ttu-id="c2ef0-146">Tijd waarop het apparaat in de oplossing is gemaakt</span><span class="sxs-lookup"><span data-stu-id="c2ef0-146">Time the device was created in the solution</span></span> |
| <span data-ttu-id="c2ef0-147">Device.StartupTime</span><span class="sxs-lookup"><span data-stu-id="c2ef0-147">Device.StartupTime</span></span> |<span data-ttu-id="c2ef0-148">Het tijdstip waarop het apparaat is gestart</span><span class="sxs-lookup"><span data-stu-id="c2ef0-148">Time the device was started</span></span> |
| <span data-ttu-id="c2ef0-149">Device.LastDesiredPropertyChange</span><span class="sxs-lookup"><span data-stu-id="c2ef0-149">Device.LastDesiredPropertyChange</span></span> |<span data-ttu-id="c2ef0-150">Het versienummer van de laatst gewenste eigenschapswijziging</span><span class="sxs-lookup"><span data-stu-id="c2ef0-150">The version number of the last desired property change</span></span> |
| <span data-ttu-id="c2ef0-151">Device.Location.Latitude</span><span class="sxs-lookup"><span data-stu-id="c2ef0-151">Device.Location.Latitude</span></span> |<span data-ttu-id="c2ef0-152">Breedtegraad van locatie waar het apparaat zich bevindt</span><span class="sxs-lookup"><span data-stu-id="c2ef0-152">Latitude location of the device</span></span> |
| <span data-ttu-id="c2ef0-153">Device.Location.Longitude</span><span class="sxs-lookup"><span data-stu-id="c2ef0-153">Device.Location.Longitude</span></span> |<span data-ttu-id="c2ef0-154">Lengtegraad van locatie waar het apparaat zich bevindt</span><span class="sxs-lookup"><span data-stu-id="c2ef0-154">Longitude location of the device</span></span> |
| <span data-ttu-id="c2ef0-155">System.Manufacturer</span><span class="sxs-lookup"><span data-stu-id="c2ef0-155">System.Manufacturer</span></span> |<span data-ttu-id="c2ef0-156">Fabrikant van apparaat</span><span class="sxs-lookup"><span data-stu-id="c2ef0-156">Device manufacturer</span></span> |
| <span data-ttu-id="c2ef0-157">System.ModelNumber</span><span class="sxs-lookup"><span data-stu-id="c2ef0-157">System.ModelNumber</span></span> |<span data-ttu-id="c2ef0-158">Modelnummer van het apparaat</span><span class="sxs-lookup"><span data-stu-id="c2ef0-158">Model number of the device</span></span> |
| <span data-ttu-id="c2ef0-159">System.SerialNumber</span><span class="sxs-lookup"><span data-stu-id="c2ef0-159">System.SerialNumber</span></span> |<span data-ttu-id="c2ef0-160">Serienummer van het apparaat</span><span class="sxs-lookup"><span data-stu-id="c2ef0-160">Serial number of the device</span></span> |
| <span data-ttu-id="c2ef0-161">System.FirmwareVersion</span><span class="sxs-lookup"><span data-stu-id="c2ef0-161">System.FirmwareVersion</span></span> |<span data-ttu-id="c2ef0-162">Huidige versie van de firmware op het apparaat</span><span class="sxs-lookup"><span data-stu-id="c2ef0-162">Current version of firmware on the device</span></span> |
| <span data-ttu-id="c2ef0-163">System.Platform</span><span class="sxs-lookup"><span data-stu-id="c2ef0-163">System.Platform</span></span> |<span data-ttu-id="c2ef0-164">Platformarchitectuur van het apparaat</span><span class="sxs-lookup"><span data-stu-id="c2ef0-164">Platform architecture of the device</span></span> |
| <span data-ttu-id="c2ef0-165">System.Processor</span><span class="sxs-lookup"><span data-stu-id="c2ef0-165">System.Processor</span></span> |<span data-ttu-id="c2ef0-166">Processor waarop het apparaat wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="c2ef0-166">Processor running the device</span></span> |
| <span data-ttu-id="c2ef0-167">System.InstalledRAM</span><span class="sxs-lookup"><span data-stu-id="c2ef0-167">System.InstalledRAM</span></span> |<span data-ttu-id="c2ef0-168">Hoeveelheid RAM-geheugen dat op het apparaat is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="c2ef0-168">Amount of RAM installed on the device</span></span> |

<span data-ttu-id="c2ef0-169">De simulator voorziet deze eigenschappen in de gesimuleerde apparaten van voorbeeldwaarden.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-169">The simulator seeds these properties in simulated devices with sample values.</span></span> <span data-ttu-id="c2ef0-170">Telkens wanneer de simulator een gesimuleerd apparaat initialiseert, rapporteert het apparaat de vooraf gedefinieerde metagegevens als gerapporteerde eigenschappen aan IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-170">Each time the simulator initializes a simulated device, the device reports the pre-defined metadata to IoT Hub as reported properties.</span></span> <span data-ttu-id="c2ef0-171">Gerapporteerde eigenschappen kunnen alleen worden bijgewerkt door het apparaat.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-171">Reported properties can only be updated by the device.</span></span> <span data-ttu-id="c2ef0-172">Als u een gerapporteerde eigenschap wilt wijzigen, stelt u in de oplossingsportal een gewenste eigenschap in.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-172">To change a reported property, you set a desired property in solution portal.</span></span> <span data-ttu-id="c2ef0-173">Het is de verantwoordelijkheid van het apparaat om:</span><span class="sxs-lookup"><span data-stu-id="c2ef0-173">It is the responsibility of the device to:</span></span>

1. <span data-ttu-id="c2ef0-174">Regelmatig gewenste eigenschappen op te halen uit de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-174">Periodically retrieve desired properties from the IoT hub.</span></span>
2. <span data-ttu-id="c2ef0-175">Diens configuratie bij te werken met de gewenste eigenschapswaarde.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-175">Update its configuration with the desired property value.</span></span>
3. <span data-ttu-id="c2ef0-176">De nieuwe waarde weer als een gerapporteerde eigenschap terug te sturen naar de hub.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-176">Send the new value back to the hub as a reported property.</span></span>

<span data-ttu-id="c2ef0-177">Vanuit het dashboard van de oplossing kunt u *gewenste eigenschappen* gebruiken om eigenschappen op een apparaat in te stellen met behulp van de [apparaatdubbel][lnk-device-twins].</span><span class="sxs-lookup"><span data-stu-id="c2ef0-177">From the solution dashboard, you can use *desired properties* to set properties on a device by using the [device twin][lnk-device-twins].</span></span> <span data-ttu-id="c2ef0-178">Gewoonlijk haalt een apparaat de waarde van een gewenste eigenschap op uit de hub om diens interne status bij te werken en de wijziging weer als een gerapporteerde eigenschap terug te melden.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-178">Typically, a device reads a desired property value from the hub to update its internal state and report the change back as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="c2ef0-179">De code van het gesimuleerde apparaat gebruikt alleen de gewenste eigenschappen **Desired.Config.TemperatureMeanValue** en **Desired.Config.TelemetryInterval** om de gerapporteerde eigenschappen bij te werken die naar IoT Hub worden teruggestuurd.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-179">The simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties sent back to IoT Hub.</span></span> <span data-ttu-id="c2ef0-180">Alle andere aanvragen om gewenste eigenschappen te wijzigen worden in het gesimuleerde apparaat genegeerd.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-180">All other desired property change requests are ignored in the simulated device.</span></span>

### <a name="methods"></a><span data-ttu-id="c2ef0-181">Methoden</span><span class="sxs-lookup"><span data-stu-id="c2ef0-181">Methods</span></span>

<span data-ttu-id="c2ef0-182">De gesimuleerde apparaten kunnen de volgende methoden ([directe methoden][lnk-direct-methods]) afhandelen die via de IoT Hub vanuit oplossingsportal zijn geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="c2ef0-182">The simulated devices can handle the following methods ([direct methods][lnk-direct-methods]) invoked from the solution portal through the IoT hub:</span></span>

| <span data-ttu-id="c2ef0-183">Methode</span><span class="sxs-lookup"><span data-stu-id="c2ef0-183">Method</span></span> | <span data-ttu-id="c2ef0-184">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c2ef0-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c2ef0-185">InitiateFirmwareUpdate</span><span class="sxs-lookup"><span data-stu-id="c2ef0-185">InitiateFirmwareUpdate</span></span> |<span data-ttu-id="c2ef0-186">Geeft het apparaat de opdracht om een firmware-update uit te voeren</span><span class="sxs-lookup"><span data-stu-id="c2ef0-186">Instructs the device to perform a firmware update</span></span> |
| <span data-ttu-id="c2ef0-187">Opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="c2ef0-187">Reboot</span></span> |<span data-ttu-id="c2ef0-188">Geeft het apparaat de opdracht opnieuw op te starten</span><span class="sxs-lookup"><span data-stu-id="c2ef0-188">Instructs the device to reboot</span></span> |
| <span data-ttu-id="c2ef0-189">FactoryReset</span><span class="sxs-lookup"><span data-stu-id="c2ef0-189">FactoryReset</span></span> |<span data-ttu-id="c2ef0-190">Geeft het apparaat de opdracht om de fabrieksinstellingen terug te zetten</span><span class="sxs-lookup"><span data-stu-id="c2ef0-190">Instructs the device to perform a factory reset</span></span> |

<span data-ttu-id="c2ef0-191">Sommige methoden gebruiken gerapporteerde eigenschappen om te rapporteren over hun voortgang.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-191">Some methods use reported properties to report on progress.</span></span> <span data-ttu-id="c2ef0-192">Zo simuleert de methode **InitiateFirmwareUpdate** bijvoorbeeld een asynchrone uitvoering van de update op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-192">For example, the **InitiateFirmwareUpdate** method simulates running the update asynchronously on the device.</span></span> <span data-ttu-id="c2ef0-193">De methode keert onmiddellijk terug naar het apparaat terwijl de asynchrone taak met behulp van gerapporteerde eigenschappen statusupdates naar het dashboard van de oplossing blijft verzenden.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-193">The method returns immediately on the device, while the asynchronous task continues to send status updates back to the solution dashboard using reported properties.</span></span>

### <a name="commands"></a><span data-ttu-id="c2ef0-194">Opdrachten</span><span class="sxs-lookup"><span data-stu-id="c2ef0-194">Commands</span></span>

<span data-ttu-id="c2ef0-195">De gesimuleerde apparaten kunnen de volgende opdrachten (cloud-naar-apparaat-berichten) afhandelen die vanuit de oplossingsportal via de IoT Hub worden verzonden:</span><span class="sxs-lookup"><span data-stu-id="c2ef0-195">The simulated devices can handle the following commands (cloud-to-device messages) sent from the solution portal through the IoT hub:</span></span>

| <span data-ttu-id="c2ef0-196">Opdracht</span><span class="sxs-lookup"><span data-stu-id="c2ef0-196">Command</span></span> | <span data-ttu-id="c2ef0-197">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c2ef0-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c2ef0-198">PingDevice</span><span class="sxs-lookup"><span data-stu-id="c2ef0-198">PingDevice</span></span> |<span data-ttu-id="c2ef0-199">Hiermee wordt een *ping* verzonden naar het apparaat om te controleren of het actief is</span><span class="sxs-lookup"><span data-stu-id="c2ef0-199">Sends a *ping* to the device to check it is alive</span></span> |
| <span data-ttu-id="c2ef0-200">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="c2ef0-200">StartTelemetry</span></span> |<span data-ttu-id="c2ef0-201">Geeft het apparaat opdracht om te beginnen met het verzenden van telemetriegegevens</span><span class="sxs-lookup"><span data-stu-id="c2ef0-201">Starts the device sending telemetry</span></span> |
| <span data-ttu-id="c2ef0-202">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="c2ef0-202">StopTelemetry</span></span> |<span data-ttu-id="c2ef0-203">Geeft het apparaat opdracht om te stoppen met het verzenden van telemetriegegevens</span><span class="sxs-lookup"><span data-stu-id="c2ef0-203">Stops the device from sending telemetry</span></span> |
| <span data-ttu-id="c2ef0-204">ChangeSetPointTemp</span><span class="sxs-lookup"><span data-stu-id="c2ef0-204">ChangeSetPointTemp</span></span> |<span data-ttu-id="c2ef0-205">Hiermee wordt de waarde van het instelpunt gewijzigd waaromheen de willekeurige gegevens worden gegenereerd</span><span class="sxs-lookup"><span data-stu-id="c2ef0-205">Changes the set point value around which the random data is generated</span></span> |
| <span data-ttu-id="c2ef0-206">DiagnosticTelemetry</span><span class="sxs-lookup"><span data-stu-id="c2ef0-206">DiagnosticTelemetry</span></span> |<span data-ttu-id="c2ef0-207">Hiermee wordt de apparaatsimulator geactiveerd voor het verzenden van een extra telemetriewaarde (externalTemp)</span><span class="sxs-lookup"><span data-stu-id="c2ef0-207">Triggers the device simulator to send an additional telemetry value (externalTemp)</span></span> |
| <span data-ttu-id="c2ef0-208">ChangeDeviceState</span><span class="sxs-lookup"><span data-stu-id="c2ef0-208">ChangeDeviceState</span></span> |<span data-ttu-id="c2ef0-209">Hiermee wordt een eigenschap uitgebreide status voor het apparaat gewijzigd en wordt het bericht met apparaatgegevens verzonden vanaf het apparaat</span><span class="sxs-lookup"><span data-stu-id="c2ef0-209">Changes an extended state property for the device and sends the device info message from the device</span></span> |

> [!NOTE]
> <span data-ttu-id="c2ef0-210">Zie [Cloud-to-device communications guidance][lnk-c2d-guidance] (Richtlijnen voor communicatie tussen cloud en apparaat) voor een vergelijking van deze opdrachten (berichten van cloud naar apparaat) en methoden (directe methoden).</span><span class="sxs-lookup"><span data-stu-id="c2ef0-210">For a comparison of these commands (cloud-to-device messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

## <a name="iot-hub"></a><span data-ttu-id="c2ef0-211">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="c2ef0-211">IoT Hub</span></span>

<span data-ttu-id="c2ef0-212">De [IoT Hub][lnk-iothub] neemt gegevens op die vanaf de apparaten worden verzonden naar de cloud, en maakt ze beschikbaar voor de ASA-taken (Azure Stream Analytics).</span><span class="sxs-lookup"><span data-stu-id="c2ef0-212">The [IoT hub][lnk-iothub] ingests data sent from the devices into the cloud and makes it available to the Azure Stream Analytics (ASA) jobs.</span></span> <span data-ttu-id="c2ef0-213">Voor elke stream maakt de ASA-taak gebruik van een afzonderlijke IoT Hub-consumentengroep om de stroom berichten van de apparaten te lezen.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-213">Each stream ASA job uses a separate IoT Hub consumer group to read the stream of messages from your devices.</span></span>

<span data-ttu-id="c2ef0-214">De IoT Hub in de oplossing doet ook het volgende:</span><span class="sxs-lookup"><span data-stu-id="c2ef0-214">The IoT hub in the solution also:</span></span>

- <span data-ttu-id="c2ef0-215">Houdt een register van identiteiten bij waarin de id's en verificatiesleutels zijn opgeslagen van alle apparaten die verbinding mogen maken met de portal.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-215">Maintains an identity registry that stores the ids and authentication keys of all the devices permitted to connect to the portal.</span></span> <span data-ttu-id="c2ef0-216">U kunt apparaten in- en uitschakelen via het register van identiteiten.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-216">You can enable and disable devices through the identity registry.</span></span>
- <span data-ttu-id="c2ef0-217">Verstuurt namens de oplossingsportal opdrachten naar uw apparaten.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-217">Sends commands to your devices on behalf of the solution portal.</span></span>
- <span data-ttu-id="c2ef0-218">Roept namens de oplossingsportal methoden aan op uw apparaten.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-218">Invokes methods on your devices on behalf of the solution portal.</span></span>
- <span data-ttu-id="c2ef0-219">Onderhoudt apparaatdubbels voor alle geregistreerde apparaten.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-219">Maintains device twins for all registered devices.</span></span> <span data-ttu-id="c2ef0-220">Een apparaatdubbel slaat de eigenschapswaarden op die door een apparaat worden gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-220">A device twin stores the property values reported by a device.</span></span> <span data-ttu-id="c2ef0-221">Een apparaatdubbel slaat ook gewenste eigenschappen op die in de oplossingsportal zijn ingesteld, zodat het apparaat deze kan ophalen wanneer opnieuw verbinding wordt maakt.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-221">A device twin also stores desired properties, set in the solution portal, for the device to retrieve when it next connects.</span></span>
- <span data-ttu-id="c2ef0-222">Plant taken voor het instellen van eigenschappen voor meerdere apparaten of voor het aanroepen van methoden op meerdere apparaten.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-222">Schedules jobs to set properties for multiple devices or invoke methods on multiple devices.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="c2ef0-223">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c2ef0-223">Azure Stream Analytics</span></span>

<span data-ttu-id="c2ef0-224">Bij de oplossing voor externe controle worden via [ASA][lnk-asa]-apparaatberichten (Azure Stream Analytics) die zijn ontvangen via de IoT Hub, verzonden naar andere back-endonderdelen voor verwerking of opslag.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-224">In the remote monitoring solution, [Azure Stream Analytics][lnk-asa] (ASA) dispatches device messages received by the IoT hub to other back-end components for processing or storage.</span></span> <span data-ttu-id="c2ef0-225">Met verschillende ASA-taken worden specifieke functies uitgevoerd gebaseerd op de inhoud van de berichten.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-225">Different ASA jobs perform specific functions based on the content of the messages.</span></span>

<span data-ttu-id="c2ef0-226">**Taak 1: apparaatgegevens** filtert berichten met apparaatgegevens uit de binnenkomende berichtenstroom en stuurt deze naar een Event Hub-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-226">**Job 1: Device Info** filters device information messages from the incoming message stream and sends them to an Event Hub endpoint.</span></span> <span data-ttu-id="c2ef0-227">Via een apparaat worden berichten met apparaatgegevens verzonden bij het opstarten en als reactie op een opdracht **SendDeviceInfo**.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-227">A device sends device information messages at startup and in response to a **SendDeviceInfo** command.</span></span> <span data-ttu-id="c2ef0-228">Tijdens deze taak wordt gebruikgemaakt van de volgende querydefinitie om berichten over **apparaatgegevens** te identificeren:</span><span class="sxs-lookup"><span data-stu-id="c2ef0-228">This job uses the following query definition to identify **device-info** messages:</span></span>

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

<span data-ttu-id="c2ef0-229">Tijdens deze taak wordt de uitvoer verzonden naar een Event Hub voor verdere verwerking.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-229">This job sends its output to an Event Hub for further processing.</span></span>

<span data-ttu-id="c2ef0-230">**Taak 2: regels** evalueren de binnenkomende telemetriegegevens over temperatuur en vochtigheid aan de hand van de drempelwaarden voor elk apparaat.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-230">**Job 2: Rules** evaluates incoming temperature and humidity telemetry values against per-device thresholds.</span></span> <span data-ttu-id="c2ef0-231">Drempelwaarden kunnen worden ingesteld met de regeleditor die beschikbaar is in de oplossingsportal.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-231">Threshold values are set in the rules editor available in the solution portal.</span></span> <span data-ttu-id="c2ef0-232">Elk koppel apparaat/waarde wordt per tijdstempel opgeslagen in een blob die met Stream Analytics wordt gelezen als **referentiegegevens**.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-232">Each device/value pair is stored by timestamp in a blob which Stream Analytics reads in as **Reference Data**.</span></span> <span data-ttu-id="c2ef0-233">De taak vergelijkt elke niet-lege waarde met de ingestelde drempelwaarde voor het apparaat.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-233">The job compares any non-empty value against the set threshold for the device.</span></span> <span data-ttu-id="c2ef0-234">Als deze de voorwaarde > overschrijdt, bestaat de taakuitvoer uit een **waarschuwings**gebeurtenis die aangeeft dat de drempelwaarde is overschreden, en worden tevens de waarden voor het apparaat, de waarde en de tijdstempel gegeven.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-234">If it exceeds the '>' condition, the job outputs an **alarm** event that indicates that the threshold is exceeded and provides the device, value, and timestamp values.</span></span> <span data-ttu-id="c2ef0-235">Voor deze taak wordt gebruikgemaakt van de volgende querydefinitie om berichten over telemetrie te identificeren die een alarm moeten activeren:</span><span class="sxs-lookup"><span data-stu-id="c2ef0-235">This job uses the following query definition to identify telemetry messages that should trigger an alarm:</span></span>

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

<span data-ttu-id="c2ef0-236">Tijdens deze taak wordt de uitvoer verzonden naar een Event Hub voor verdere verwerking. Ook worden details van elke waarschuwing opgeslagen in de blobopslag, waar de informatie uit de waarschuwing kan worden gelezen in de oplossingsportal.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-236">The job sends its output to an Event Hub for further processing and saves details of each alert to blob storage from where the solution portal can read the alert information.</span></span>

<span data-ttu-id="c2ef0-237">**Taak 3: telemetrie** is op twee manieren actief op de binnenkomende stroom telemetriegegevens van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-237">**Job 3: Telemetry** operates on the incoming device telemetry stream in two ways.</span></span> <span data-ttu-id="c2ef0-238">Allereerst worden alle telemetrieberichten vanaf de apparaten naar een permanente blobopslag verzonden voor langdurige opslag.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-238">The first sends all telemetry messages from the devices to persistent blob storage for long-term storage.</span></span> <span data-ttu-id="c2ef0-239">Ten tweede worden elke vijf minuten de gemiddelde, minimale en maximale vochtigheidswaarden berekend. Deze gegevens worden verzonden naar de blobopslag.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-239">The second computes average, minimum, and maximum humidity values over a five-minute sliding window and sends this data to blob storage.</span></span> <span data-ttu-id="c2ef0-240">Met de oplossingsportal worden de telemetriegegevens uit de blobopslag gelezen om de grafieken te vullen.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-240">The solution portal reads the telemetry data from blob storage to populate the charts.</span></span> <span data-ttu-id="c2ef0-241">Tijdens deze taak wordt gebruikgemaakt van de volgende querydefinitie:</span><span class="sxs-lookup"><span data-stu-id="c2ef0-241">This job uses the following query definition:</span></span>

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a><span data-ttu-id="c2ef0-242">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c2ef0-242">Event Hubs</span></span>

<span data-ttu-id="c2ef0-243">De ASA-taken voor **apparaatgegevens** en **regels** voeren hun gegevens uit naar Event Hubs die zo kunnen worden doorgestuurd naar de **gebeurtenisprocessor** die actief is in de webtaak.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-243">The **device info** and **rules** ASA jobs output their data to Event Hubs to reliably forward on to the **Event Processor** running in the WebJob.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="c2ef0-244">Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="c2ef0-244">Azure storage</span></span>

<span data-ttu-id="c2ef0-245">De oplossing maakt gebruik van Azure Blob-opslag om alle ruwe en samengevatte telemetriegegevens op de apparaten in de oplossing te behouden.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-245">The solution uses Azure blob storage to persist all the raw and summarized telemetry data from the devices in the solution.</span></span> <span data-ttu-id="c2ef0-246">Met de portal worden de telemetriegegevens uit de blobopslag gelezen om de grafieken te vullen.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-246">The portal reads the telemetry data from blob storage to populate the charts.</span></span> <span data-ttu-id="c2ef0-247">Voor het weergeven van waarschuwingen leest de oplossingsportal de gegevens uit de blobopslag, waarin is vastgelegd wanneer telemetriewaarden de geconfigureerde drempelwaarden hebben overschreden.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-247">To display alerts, the solution portal reads the data from blob storage that records when telemetry values exceeded the configured threshold values.</span></span> <span data-ttu-id="c2ef0-248">In de oplossing wordt blobopslag ook gebruikt om de drempelwaarden vast te leggen die u in de oplossingsportal hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-248">The solution also uses blob storage to record the threshold values you set in the solution portal.</span></span>

## <a name="webjobs"></a><span data-ttu-id="c2ef0-249">Webtaken</span><span class="sxs-lookup"><span data-stu-id="c2ef0-249">WebJobs</span></span>

<span data-ttu-id="c2ef0-250">De webtaken in de oplossing hosten niet alleen de apparaatsimulatoren maar ook de **gebeurtenisprocessor** die wordt uitgevoerd in een Azure-webtaak die opdrachtantwoorden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-250">In addition to hosting the device simulators, the WebJobs in the solution also host the **Event Processor** running in an Azure WebJob that handles command responses.</span></span> <span data-ttu-id="c2ef0-251">Met behulp van berichten met reacties op opdrachten wordt de opdrachtgeschiedenis van het apparaat bijgewerkt (opgeslagen in de Cosmos DB-database).</span><span class="sxs-lookup"><span data-stu-id="c2ef0-251">It uses command response messages to update the device command history (stored in the Cosmos DB database).</span></span>

## <a name="cosmos-db"></a><span data-ttu-id="c2ef0-252">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c2ef0-252">Cosmos DB</span></span>

<span data-ttu-id="c2ef0-253">De oplossing maakt gebruik van een Cosmos DB-database om informatie op te slaan over de apparaten die zijn verbonden met de oplossing.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-253">The solution uses a Cosmos DB database to store information about the devices connected to the solution.</span></span> <span data-ttu-id="c2ef0-254">Deze informatie omvat de geschiedenis van opdrachten die vanuit de oplossingsportal naar apparaten zijn verzonden en van methoden die vanuit de oplossingsportal zijn aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-254">This information includes the history of commands sent to devices from the solution portal and of methods invoked from the solution portal.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="c2ef0-255">Oplossingsportal</span><span class="sxs-lookup"><span data-stu-id="c2ef0-255">Solution portal</span></span>

<span data-ttu-id="c2ef0-256">De oplossingsportal is een webtoepassing die als onderdeel van de vooraf geconfigureerde oplossing wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-256">The solution portal is a web app deployed as part of the preconfigured solution.</span></span> <span data-ttu-id="c2ef0-257">De belangrijkste pagina's in de oplossingsportal zijn het dashboard en de lijst met apparaten.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-257">The key pages in the solution portal are the dashboard and the device list.</span></span>

### <a name="dashboard"></a><span data-ttu-id="c2ef0-258">Dashboard</span><span class="sxs-lookup"><span data-stu-id="c2ef0-258">Dashboard</span></span>

<span data-ttu-id="c2ef0-259">Deze pagina in de webtoepassing maakt gebruik van Power BI javascript-besturingselementen (zie [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) om de telemetriegegevens van de apparaten te visualiseren.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-259">This page in the web app uses PowerBI javascript controls (See [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) to visualize the telemetry data from the devices.</span></span> <span data-ttu-id="c2ef0-260">De oplossing maakt gebruik van de ASA-telemetrietaak om de telemetriegegevens naar de blobopslag te schrijven.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-260">The solution uses the ASA telemetry job to write the telemetry data to blob storage.</span></span>

### <a name="device-list"></a><span data-ttu-id="c2ef0-261">Lijst met apparaten</span><span class="sxs-lookup"><span data-stu-id="c2ef0-261">Device list</span></span>

<span data-ttu-id="c2ef0-262">Op deze pagina van de oplossingsportal kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="c2ef0-262">From this page in the solution portal you can:</span></span>

* <span data-ttu-id="c2ef0-263">Nieuwe apparaten inrichten.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-263">Provision a new device.</span></span> <span data-ttu-id="c2ef0-264">Met deze actie wordt het unieke apparaat-id ingesteld en de verificatiesleutel gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-264">This action sets the unique device id and generates the authentication key.</span></span> <span data-ttu-id="c2ef0-265">Er wordt informatie over het apparaat geschreven naar het IoT Hub-identiteitsregister en de oplossingsspecifieke Cosmos DB-database.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-265">It writes information about the device to both the IoT Hub identity registry and the solution-specific Cosmos DB database.</span></span>
* <span data-ttu-id="c2ef0-266">Apparaateigenschappen beheren.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-266">Manage device properties.</span></span> <span data-ttu-id="c2ef0-267">Deze actie omvat het weergeven van bestaande eigenschappen en het bijwerken met nieuwe eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-267">This action includes viewing existing properties and updating with new properties.</span></span>
* <span data-ttu-id="c2ef0-268">Opdrachten naar een apparaat verzenden.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-268">Send commands to a device.</span></span>
* <span data-ttu-id="c2ef0-269">De opdrachtgeschiedenis voor een apparaat weergeven.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-269">View the command history for a device.</span></span>
* <span data-ttu-id="c2ef0-270">Apparaten in- en uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="c2ef0-270">Enable and disable devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2ef0-271">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c2ef0-271">Next steps</span></span>

<span data-ttu-id="c2ef0-272">De volgende TechNet-blogberichten bieden meer details over de vooraf geconfigureerde oplossing voor externe controle:</span><span class="sxs-lookup"><span data-stu-id="c2ef0-272">The following TechNet blog posts provide more detail about the remote monitoring preconfigured solution:</span></span>

* [<span data-ttu-id="c2ef0-273">IoT Suite - Under The Hood - Remote Monitoring (IoT Suite - achter de schermen - externe controle)</span><span class="sxs-lookup"><span data-stu-id="c2ef0-273">IoT Suite - Under The Hood - Remote Monitoring</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [<span data-ttu-id="c2ef0-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices (IoT Suite - externe controle - live- en gesimuleerde apparaten toevoegen)</span><span class="sxs-lookup"><span data-stu-id="c2ef0-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

<span data-ttu-id="c2ef0-275">U kunt verder aan de slag gaan met IoT Suite door de volgende artikelen te lezen:</span><span class="sxs-lookup"><span data-stu-id="c2ef0-275">You can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="c2ef0-276">[Uw apparaat koppelen aan de vooraf geconfigureerde oplossing voor externe bewaking][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="c2ef0-276">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="c2ef0-277">[Machtigingen op de site azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="c2ef0-277">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md

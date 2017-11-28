---
title: aaaRemote bewaking van de vooraf geconfigureerde oplossing overzicht | Microsoft Docs
description: Een beschrijving van hello Azure IoT vooraf geconfigureerde oplossing voor externe controle en de bijbehorende architectuur.
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
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a><span data-ttu-id="8b947-103">Walkthrough over vooraf geconfigureerde oplossing voor externe controle</span><span class="sxs-lookup"><span data-stu-id="8b947-103">Remote monitoring preconfigured solution walkthrough</span></span>

<span data-ttu-id="8b947-104">Hallo externe controle IoT Suite [vooraf geconfigureerde oplossing] [ lnk-preconfigured-solutions] is een implementatie van een end-to-end-bewakingsoplossing voor meerdere machines die worden uitgevoerd op externe locaties.</span><span class="sxs-lookup"><span data-stu-id="8b947-104">hello IoT Suite remote monitoring [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end monitoring solution for multiple machines running in remote locations.</span></span> <span data-ttu-id="8b947-105">Hallo oplossing combineert belangrijke Azure-services tooprovide een algemene implementatie van Hallo bedrijfsscenario.</span><span class="sxs-lookup"><span data-stu-id="8b947-105">hello solution combines key Azure services tooprovide a generic implementation of hello business scenario.</span></span> <span data-ttu-id="8b947-106">U kunt Hallo oplossing gebruiken als een beginpunt voor uw eigen implementatie en [aanpassen] [ lnk-customize] het toomeet uw eigen specifieke zakelijke vereisten.</span><span class="sxs-lookup"><span data-stu-id="8b947-106">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="8b947-107">In dit artikel worden enkele van de belangrijkste elementen van de Hallo van Hallo remote monitoring solution tooenable toounderstand u hoe het werkt.</span><span class="sxs-lookup"><span data-stu-id="8b947-107">This article walks you through some of hello key elements of hello remote monitoring solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="8b947-108">Deze kennis helpt u bij:</span><span class="sxs-lookup"><span data-stu-id="8b947-108">This knowledge helps you to:</span></span>

* <span data-ttu-id="8b947-109">Los problemen met het Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="8b947-109">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="8b947-110">Plannen hoe toocustomize toohello oplossing toomeet uw eigen specifieke vereisten.</span><span class="sxs-lookup"><span data-stu-id="8b947-110">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span> 
* <span data-ttu-id="8b947-111">Het ontwerpen van uw eigen IoT-oplossing die gebruikmaakt van Azure-services.</span><span class="sxs-lookup"><span data-stu-id="8b947-111">Design your own IoT solution that uses Azure services.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="8b947-112">Logische architectuur</span><span class="sxs-lookup"><span data-stu-id="8b947-112">Logical architecture</span></span>

<span data-ttu-id="8b947-113">Hallo volgende diagram geeft een overzicht van de logische onderdelen van de Hallo van Hallo vooraf geconfigureerde oplossing:</span><span class="sxs-lookup"><span data-stu-id="8b947-113">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Logische architectuur](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a><span data-ttu-id="8b947-115">Gesimuleerde apparaten</span><span class="sxs-lookup"><span data-stu-id="8b947-115">Simulated devices</span></span>

<span data-ttu-id="8b947-116">In Hallo vooraf geconfigureerde oplossing vertegenwoordigt Hallo gesimuleerde apparaat een koelapparaat (zoals een airconditioner of faciliteit lucht verwerking eenheid).</span><span class="sxs-lookup"><span data-stu-id="8b947-116">In hello preconfigured solution, hello simulated device represents a cooling device (such as a building air conditioner or facility air handling unit).</span></span> <span data-ttu-id="8b947-117">Wanneer u Hallo vooraf geconfigureerde oplossing implementeert, u ook automatisch inrichten vier gesimuleerde apparaten die worden uitgevoerd in een [Azure webtaak][lnk-webjobs].</span><span class="sxs-lookup"><span data-stu-id="8b947-117">When you deploy hello preconfigured solution, you also automatically provision four simulated devices that run in an [Azure WebJob][lnk-webjobs].</span></span> <span data-ttu-id="8b947-118">Hallo gesimuleerde apparaten eenvoudiger voor u tooexplore Hallo gedrag van Hallo oplossing zonder Hallo nodig toodeploy fysieke apparaten.</span><span class="sxs-lookup"><span data-stu-id="8b947-118">hello simulated devices make it easy for you tooexplore hello behavior of hello solution without hello need toodeploy any physical devices.</span></span> <span data-ttu-id="8b947-119">een echte fysiek apparaat toodeploy Zie Hallo [verbinding maken met uw vooraf geconfigureerde oplossing voor externe controle apparaat toohello] [ lnk-connect-rm] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="8b947-119">toodeploy a real physical device, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

### <a name="device-to-cloud-messages"></a><span data-ttu-id="8b947-120">Apparaat-naar-cloud-berichten</span><span class="sxs-lookup"><span data-stu-id="8b947-120">Device-to-cloud messages</span></span>

<span data-ttu-id="8b947-121">Elk gesimuleerd apparaat kunt verzenden Hallo-bericht typen tooIoT Hub te volgen:</span><span class="sxs-lookup"><span data-stu-id="8b947-121">Each simulated device can send hello following message types tooIoT Hub:</span></span>

| <span data-ttu-id="8b947-122">Bericht</span><span class="sxs-lookup"><span data-stu-id="8b947-122">Message</span></span> | <span data-ttu-id="8b947-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8b947-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8b947-124">Opstarten</span><span class="sxs-lookup"><span data-stu-id="8b947-124">Startup</span></span> |<span data-ttu-id="8b947-125">Wanneer het Hallo-apparaat wordt gestart, stuurt een **apparaatgegevens** -bericht met informatie over zichzelf toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="8b947-125">When hello device starts, it sends a **device-info** message containing information about itself toohello back end.</span></span> <span data-ttu-id="8b947-126">Deze gegevens omvatten Hallo apparaat-id en een lijst met opdrachten Hallo en methoden Hallo apparaat worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="8b947-126">This data includes hello device id and a list of hello commands and methods hello device supports.</span></span> |
| <span data-ttu-id="8b947-127">Aanwezigheid</span><span class="sxs-lookup"><span data-stu-id="8b947-127">Presence</span></span> |<span data-ttu-id="8b947-128">Een apparaat periodiek verzendt een **aanwezigheid** tooreport bericht of Hallo apparaat Hallo aanwezigheid van een sensor kunt detecteren.</span><span class="sxs-lookup"><span data-stu-id="8b947-128">A device periodically sends a **presence** message tooreport whether hello device can sense hello presence of a sensor.</span></span> |
| <span data-ttu-id="8b947-129">Telemetrie</span><span class="sxs-lookup"><span data-stu-id="8b947-129">Telemetry</span></span> |<span data-ttu-id="8b947-130">Een apparaat periodiek verzendt een **telemetrie** bericht die gesimuleerde waarden voor Hallo temperatuur en vochtigheid verzameld van Hallo apparaat rapporteert de sensoren gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="8b947-130">A device periodically sends a **telemetry** message that reports simulated values for hello temperature and humidity collected from hello device's simulated sensors.</span></span> |

> [!NOTE]
> <span data-ttu-id="8b947-131">Hallo oplossing slaat Hallo lijst met opdrachten die worden ondersteund door Hallo-apparaat in een Cosmos-DB-database en niet in Hallo apparaat twin.</span><span class="sxs-lookup"><span data-stu-id="8b947-131">hello solution stores hello list of commands supported by hello device in a Cosmos DB database and not in hello device twin.</span></span>

### <a name="properties-and-device-twins"></a><span data-ttu-id="8b947-132">Eigenschappen en apparaatdubbels</span><span class="sxs-lookup"><span data-stu-id="8b947-132">Properties and device twins</span></span>

<span data-ttu-id="8b947-133">Hallo gesimuleerde apparaten verzenden Hallo na apparaat eigenschappen toohello [twin] [ lnk-device-twins] in Hallo IoT-hub als *eigenschappen gerapporteerd*.</span><span class="sxs-lookup"><span data-stu-id="8b947-133">hello simulated devices send hello following device properties toohello [twin][lnk-device-twins] in hello IoT hub as *reported properties*.</span></span> <span data-ttu-id="8b947-134">Hallo apparaat verzendt gerapporteerd eigenschappen bij het opstarten en in reactie tooa **Changedevicestate** opdracht of methode.</span><span class="sxs-lookup"><span data-stu-id="8b947-134">hello device sends reported properties at startup and in response tooa **Change Device State** command or method.</span></span>

| <span data-ttu-id="8b947-135">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="8b947-135">Property</span></span> | <span data-ttu-id="8b947-136">Doel</span><span class="sxs-lookup"><span data-stu-id="8b947-136">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="8b947-137">Config.TelemetryInterval</span><span class="sxs-lookup"><span data-stu-id="8b947-137">Config.TelemetryInterval</span></span> | <span data-ttu-id="8b947-138">Frequentie (seconden) Hallo apparaat verzendt telemetrie</span><span class="sxs-lookup"><span data-stu-id="8b947-138">Frequency (seconds) hello device sends telemetry</span></span> |
| <span data-ttu-id="8b947-139">Config.TemperatureMeanValue</span><span class="sxs-lookup"><span data-stu-id="8b947-139">Config.TemperatureMeanValue</span></span> | <span data-ttu-id="8b947-140">Geeft de gemiddelde waarde Hallo voor Hallo gesimuleerde temperatuur telemetrie</span><span class="sxs-lookup"><span data-stu-id="8b947-140">Specifies hello mean value for hello simulated temperature telemetry</span></span> |
| <span data-ttu-id="8b947-141">Device.DeviceID</span><span class="sxs-lookup"><span data-stu-id="8b947-141">Device.DeviceID</span></span> |<span data-ttu-id="8b947-142">-ID die is opgegeven of is toegewezen als een apparaat is gemaakt in Hallo-oplossing</span><span class="sxs-lookup"><span data-stu-id="8b947-142">Id that is either provided or assigned when a device is created in hello solution</span></span> |
| <span data-ttu-id="8b947-143">Device.DeviceState</span><span class="sxs-lookup"><span data-stu-id="8b947-143">Device.DeviceState</span></span> | <span data-ttu-id="8b947-144">Is gerapporteerd door het Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="8b947-144">State reported by hello device</span></span> |
| <span data-ttu-id="8b947-145">Device.CreatedTime</span><span class="sxs-lookup"><span data-stu-id="8b947-145">Device.CreatedTime</span></span> |<span data-ttu-id="8b947-146">Tijd Hallo apparaat is gemaakt in het Hallo-oplossing</span><span class="sxs-lookup"><span data-stu-id="8b947-146">Time hello device was created in hello solution</span></span> |
| <span data-ttu-id="8b947-147">Device.StartupTime</span><span class="sxs-lookup"><span data-stu-id="8b947-147">Device.StartupTime</span></span> |<span data-ttu-id="8b947-148">Tijd Hallo apparaat is gestart</span><span class="sxs-lookup"><span data-stu-id="8b947-148">Time hello device was started</span></span> |
| <span data-ttu-id="8b947-149">Device.LastDesiredPropertyChange</span><span class="sxs-lookup"><span data-stu-id="8b947-149">Device.LastDesiredPropertyChange</span></span> |<span data-ttu-id="8b947-150">Hallo-versienummer van de laatste gewenste eigenschap Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="8b947-150">hello version number of hello last desired property change</span></span> |
| <span data-ttu-id="8b947-151">Device.Location.Latitude</span><span class="sxs-lookup"><span data-stu-id="8b947-151">Device.Location.Latitude</span></span> |<span data-ttu-id="8b947-152">Locatie van de breedte van Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="8b947-152">Latitude location of hello device</span></span> |
| <span data-ttu-id="8b947-153">Device.Location.Longitude</span><span class="sxs-lookup"><span data-stu-id="8b947-153">Device.Location.Longitude</span></span> |<span data-ttu-id="8b947-154">Locatie van de lengtegraad van Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="8b947-154">Longitude location of hello device</span></span> |
| <span data-ttu-id="8b947-155">System.Manufacturer</span><span class="sxs-lookup"><span data-stu-id="8b947-155">System.Manufacturer</span></span> |<span data-ttu-id="8b947-156">Fabrikant van apparaat</span><span class="sxs-lookup"><span data-stu-id="8b947-156">Device manufacturer</span></span> |
| <span data-ttu-id="8b947-157">System.ModelNumber</span><span class="sxs-lookup"><span data-stu-id="8b947-157">System.ModelNumber</span></span> |<span data-ttu-id="8b947-158">Modelnummer van het Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="8b947-158">Model number of hello device</span></span> |
| <span data-ttu-id="8b947-159">System.SerialNumber</span><span class="sxs-lookup"><span data-stu-id="8b947-159">System.SerialNumber</span></span> |<span data-ttu-id="8b947-160">Serienummer van Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="8b947-160">Serial number of hello device</span></span> |
| <span data-ttu-id="8b947-161">System.FirmwareVersion</span><span class="sxs-lookup"><span data-stu-id="8b947-161">System.FirmwareVersion</span></span> |<span data-ttu-id="8b947-162">Huidige versie van de firmware op Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="8b947-162">Current version of firmware on hello device</span></span> |
| <span data-ttu-id="8b947-163">System.Platform</span><span class="sxs-lookup"><span data-stu-id="8b947-163">System.Platform</span></span> |<span data-ttu-id="8b947-164">Platformarchitectuur van Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="8b947-164">Platform architecture of hello device</span></span> |
| <span data-ttu-id="8b947-165">System.Processor</span><span class="sxs-lookup"><span data-stu-id="8b947-165">System.Processor</span></span> |<span data-ttu-id="8b947-166">Processor actieve Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="8b947-166">Processor running hello device</span></span> |
| <span data-ttu-id="8b947-167">System.InstalledRAM</span><span class="sxs-lookup"><span data-stu-id="8b947-167">System.InstalledRAM</span></span> |<span data-ttu-id="8b947-168">Hoeveelheid RAM-geheugen op Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="8b947-168">Amount of RAM installed on hello device</span></span> |

<span data-ttu-id="8b947-169">Hallo simulator voorziet deze eigenschappen in de gesimuleerde apparaten van voorbeeldwaarden.</span><span class="sxs-lookup"><span data-stu-id="8b947-169">hello simulator seeds these properties in simulated devices with sample values.</span></span> <span data-ttu-id="8b947-170">Elke keer Hallo simulator een gesimuleerd apparaat, het Hallo-apparaat initialiseert rapporteert Hallo vooraf gedefinieerde metagegevens tooIoT Hub als gemelde eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="8b947-170">Each time hello simulator initializes a simulated device, hello device reports hello pre-defined metadata tooIoT Hub as reported properties.</span></span> <span data-ttu-id="8b947-171">Gerapporteerde eigenschappen kunnen alleen worden bijgewerkt door Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="8b947-171">Reported properties can only be updated by hello device.</span></span> <span data-ttu-id="8b947-172">een gerapporteerde eigenschap toochange, stelt u een gewenste eigenschap in de portal van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="8b947-172">toochange a reported property, you set a desired property in solution portal.</span></span> <span data-ttu-id="8b947-173">Hallo verantwoordelijkheid van Hallo van het apparaat is:</span><span class="sxs-lookup"><span data-stu-id="8b947-173">It is hello responsibility of hello device to:</span></span>

1. <span data-ttu-id="8b947-174">Periodiek de gewenste eigenschappen ophalen uit Hallo iothub.</span><span class="sxs-lookup"><span data-stu-id="8b947-174">Periodically retrieve desired properties from hello IoT hub.</span></span>
2. <span data-ttu-id="8b947-175">Werk de configuratie waarbij de eigenschapwaarde Hallo gewenst.</span><span class="sxs-lookup"><span data-stu-id="8b947-175">Update its configuration with hello desired property value.</span></span>
3. <span data-ttu-id="8b947-176">Hallo nieuwe waarde back toohello hub als een gerapporteerde eigenschap verzenden.</span><span class="sxs-lookup"><span data-stu-id="8b947-176">Send hello new value back toohello hub as a reported property.</span></span>

<span data-ttu-id="8b947-177">Vanuit het dashboard van de oplossing hello, kunt u met *gewenst eigenschappen* tooset eigenschappen op een apparaat met behulp van Hallo [apparaat twin][lnk-device-twins].</span><span class="sxs-lookup"><span data-stu-id="8b947-177">From hello solution dashboard, you can use *desired properties* tooset properties on a device by using hello [device twin][lnk-device-twins].</span></span> <span data-ttu-id="8b947-178">Normaal gesproken leest een apparaat een gewenste eigenschapswaarde van Hallo hub tooupdate die de interne status en het rapport Hallo weer als een eigenschap gemeld wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8b947-178">Typically, a device reads a desired property value from hello hub tooupdate its internal state and report hello change back as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="8b947-179">Hallo gesimuleerd apparaatcode gebruikt alleen Hallo **Desired.Config.TemperatureMeanValue** en **Desired.Config.TelemetryInterval** gewenste eigenschappen tooupdate Hallo eigenschappen teruggestuurd gerapporteerd tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8b947-179">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="8b947-180">Alle andere gewenste eigenschap wijzigingsaanvragen worden genegeerd in Hallo gesimuleerde apparaat.</span><span class="sxs-lookup"><span data-stu-id="8b947-180">All other desired property change requests are ignored in hello simulated device.</span></span>

### <a name="methods"></a><span data-ttu-id="8b947-181">Methoden</span><span class="sxs-lookup"><span data-stu-id="8b947-181">Methods</span></span>

<span data-ttu-id="8b947-182">Hallo gesimuleerde apparaten kunnen verwerken Hallo volgende methoden ([methoden directe][lnk-direct-methods]) aangeroepen vanuit de oplossingsportal Hallo via Hallo iothub:</span><span class="sxs-lookup"><span data-stu-id="8b947-182">hello simulated devices can handle hello following methods ([direct methods][lnk-direct-methods]) invoked from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="8b947-183">Methode</span><span class="sxs-lookup"><span data-stu-id="8b947-183">Method</span></span> | <span data-ttu-id="8b947-184">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8b947-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8b947-185">InitiateFirmwareUpdate</span><span class="sxs-lookup"><span data-stu-id="8b947-185">InitiateFirmwareUpdate</span></span> |<span data-ttu-id="8b947-186">Hiermee geeft u Hallo apparaat tooperform een firmware-update</span><span class="sxs-lookup"><span data-stu-id="8b947-186">Instructs hello device tooperform a firmware update</span></span> |
| <span data-ttu-id="8b947-187">Opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="8b947-187">Reboot</span></span> |<span data-ttu-id="8b947-188">Hiermee geeft u Hallo apparaat tooreboot</span><span class="sxs-lookup"><span data-stu-id="8b947-188">Instructs hello device tooreboot</span></span> |
| <span data-ttu-id="8b947-189">FactoryReset</span><span class="sxs-lookup"><span data-stu-id="8b947-189">FactoryReset</span></span> |<span data-ttu-id="8b947-190">Hiermee geeft u een van de fabrieksinstellingen van Hallo apparaat tooperform</span><span class="sxs-lookup"><span data-stu-id="8b947-190">Instructs hello device tooperform a factory reset</span></span> |

<span data-ttu-id="8b947-191">Bepaalde methoden voor het gebruik gemelde eigenschappen tooreport op uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8b947-191">Some methods use reported properties tooreport on progress.</span></span> <span data-ttu-id="8b947-192">Bijvoorbeeld, Hallo **InitiateFirmwareUpdate** methode actieve Hallo update asynchroon op Hallo apparaat simuleert.</span><span class="sxs-lookup"><span data-stu-id="8b947-192">For example, hello **InitiateFirmwareUpdate** method simulates running hello update asynchronously on hello device.</span></span> <span data-ttu-id="8b947-193">Hallo-methode retourneert onmiddellijk op Hallo-apparaat, terwijl de Hallo asynchrone taak nog steeds statusupdates terug toosend toohello oplossing dashboard gebruikt gerapporteerd eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="8b947-193">hello method returns immediately on hello device, while hello asynchronous task continues toosend status updates back toohello solution dashboard using reported properties.</span></span>

### <a name="commands"></a><span data-ttu-id="8b947-194">Opdrachten</span><span class="sxs-lookup"><span data-stu-id="8b947-194">Commands</span></span>

<span data-ttu-id="8b947-195">Hallo gesimuleerde apparaten kunnen verwerken Hallo opdrachten (cloud-naar-apparaat-berichten) verzonden vanaf de oplossingsportal Hallo via Hallo iothub te volgen:</span><span class="sxs-lookup"><span data-stu-id="8b947-195">hello simulated devices can handle hello following commands (cloud-to-device messages) sent from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="8b947-196">Opdracht</span><span class="sxs-lookup"><span data-stu-id="8b947-196">Command</span></span> | <span data-ttu-id="8b947-197">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8b947-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8b947-198">PingDevice</span><span class="sxs-lookup"><span data-stu-id="8b947-198">PingDevice</span></span> |<span data-ttu-id="8b947-199">Verzendt een *ping* toohello apparaat toocheck het actief is</span><span class="sxs-lookup"><span data-stu-id="8b947-199">Sends a *ping* toohello device toocheck it is alive</span></span> |
| <span data-ttu-id="8b947-200">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="8b947-200">StartTelemetry</span></span> |<span data-ttu-id="8b947-201">Start Hallo apparaat verzenden van telemetrie</span><span class="sxs-lookup"><span data-stu-id="8b947-201">Starts hello device sending telemetry</span></span> |
| <span data-ttu-id="8b947-202">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="8b947-202">StopTelemetry</span></span> |<span data-ttu-id="8b947-203">Stopt Hallo apparaat verzenden van telemetriegegevens</span><span class="sxs-lookup"><span data-stu-id="8b947-203">Stops hello device from sending telemetry</span></span> |
| <span data-ttu-id="8b947-204">ChangeSetPointTemp</span><span class="sxs-lookup"><span data-stu-id="8b947-204">ChangeSetPointTemp</span></span> |<span data-ttu-id="8b947-205">Wijzigingen Hallo set puntwaarde rond welke Hallo willekeurige gegevens worden gegenereerd</span><span class="sxs-lookup"><span data-stu-id="8b947-205">Changes hello set point value around which hello random data is generated</span></span> |
| <span data-ttu-id="8b947-206">DiagnosticTelemetry</span><span class="sxs-lookup"><span data-stu-id="8b947-206">DiagnosticTelemetry</span></span> |<span data-ttu-id="8b947-207">Triggers Hallo apparaat simulator toosend een extra telemetriewaarde (externalTemp)</span><span class="sxs-lookup"><span data-stu-id="8b947-207">Triggers hello device simulator toosend an additional telemetry value (externalTemp)</span></span> |
| <span data-ttu-id="8b947-208">ChangeDeviceState</span><span class="sxs-lookup"><span data-stu-id="8b947-208">ChangeDeviceState</span></span> |<span data-ttu-id="8b947-209">Een eigenschap uitgebreide status voor Hallo apparaat wijzigingen en Hallo bericht met apparaatgegevens vanaf Hallo apparaat verzenden</span><span class="sxs-lookup"><span data-stu-id="8b947-209">Changes an extended state property for hello device and sends hello device info message from hello device</span></span> |

> [!NOTE]
> <span data-ttu-id="8b947-210">Zie [Cloud-to-device communications guidance][lnk-c2d-guidance] (Richtlijnen voor communicatie tussen cloud en apparaat) voor een vergelijking van deze opdrachten (berichten van cloud naar apparaat) en methoden (directe methoden).</span><span class="sxs-lookup"><span data-stu-id="8b947-210">For a comparison of these commands (cloud-to-device messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

## <a name="iot-hub"></a><span data-ttu-id="8b947-211">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="8b947-211">IoT Hub</span></span>

<span data-ttu-id="8b947-212">Hallo [IoT-hub] [ lnk-iothub] opgenomen in de cloud Hallo Hallo apparaten verzonden gegevens en maakt het beschikbaar toohello Azure Stream Analytics (ASA)-taken.</span><span class="sxs-lookup"><span data-stu-id="8b947-212">hello [IoT hub][lnk-iothub] ingests data sent from hello devices into hello cloud and makes it available toohello Azure Stream Analytics (ASA) jobs.</span></span> <span data-ttu-id="8b947-213">Elke stream ASA-taak maakt gebruik van een afzonderlijke IoT Hub consumer groep tooread Hallo stroom van berichten van uw apparaten.</span><span class="sxs-lookup"><span data-stu-id="8b947-213">Each stream ASA job uses a separate IoT Hub consumer group tooread hello stream of messages from your devices.</span></span>

<span data-ttu-id="8b947-214">Hallo IoT-hub in Hallo oplossing ook:</span><span class="sxs-lookup"><span data-stu-id="8b947-214">hello IoT hub in hello solution also:</span></span>

- <span data-ttu-id="8b947-215">Onderhoudt een identity-registry die Hallo-id's en verificatiesleutels van alle Hallo apparaten toegestaan tooconnect toohello portal worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8b947-215">Maintains an identity registry that stores hello ids and authentication keys of all hello devices permitted tooconnect toohello portal.</span></span> <span data-ttu-id="8b947-216">U kunt inschakelen en uitschakelen van apparaten via Hallo id-register.</span><span class="sxs-lookup"><span data-stu-id="8b947-216">You can enable and disable devices through hello identity registry.</span></span>
- <span data-ttu-id="8b947-217">Opdrachten verzendt tooyour apparaten namens de oplossingsportal Hallo.</span><span class="sxs-lookup"><span data-stu-id="8b947-217">Sends commands tooyour devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="8b947-218">Methoden op uw apparaten aanroept namens de oplossingsportal Hallo.</span><span class="sxs-lookup"><span data-stu-id="8b947-218">Invokes methods on your devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="8b947-219">Onderhoudt apparaatdubbels voor alle geregistreerde apparaten.</span><span class="sxs-lookup"><span data-stu-id="8b947-219">Maintains device twins for all registered devices.</span></span> <span data-ttu-id="8b947-220">Een apparaat-twin slaat Hallo eigenschapswaarden gemeld door een apparaat.</span><span class="sxs-lookup"><span data-stu-id="8b947-220">A device twin stores hello property values reported by a device.</span></span> <span data-ttu-id="8b947-221">Een apparaat-twin slaat ook gewenste eigenschappen instellen in de oplossingsportal Hallo voor Hallo apparaat tooretrieve wanneer deze vervolgens verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="8b947-221">A device twin also stores desired properties, set in hello solution portal, for hello device tooretrieve when it next connects.</span></span>
- <span data-ttu-id="8b947-222">Planningen taken tooset eigenschappen voor meerdere apparaten of methoden op meerdere apparaten.</span><span class="sxs-lookup"><span data-stu-id="8b947-222">Schedules jobs tooset properties for multiple devices or invoke methods on multiple devices.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="8b947-223">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8b947-223">Azure Stream Analytics</span></span>

<span data-ttu-id="8b947-224">In de oplossing, voor externe controle Hallo [Azure Stream Analytics] [ lnk-asa] (ASA) verzendt de apparaat-berichten ontvangen door Hallo IoT hub tooother back-end-onderdelen voor de verwerking of opslag.</span><span class="sxs-lookup"><span data-stu-id="8b947-224">In hello remote monitoring solution, [Azure Stream Analytics][lnk-asa] (ASA) dispatches device messages received by hello IoT hub tooother back-end components for processing or storage.</span></span> <span data-ttu-id="8b947-225">Andere ASA-jobs uitvoeren specifieke functies op basis van inhoud van het Hallo-berichten Hallo.</span><span class="sxs-lookup"><span data-stu-id="8b947-225">Different ASA jobs perform specific functions based on hello content of hello messages.</span></span>

<span data-ttu-id="8b947-226">**Taak 1: Apparaatgegevens** filtert berichten met apparaatgegevens uit Hallo binnenkomende berichtenstroom en stuurt deze tooan Event Hub-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="8b947-226">**Job 1: Device Info** filters device information messages from hello incoming message stream and sends them tooan Event Hub endpoint.</span></span> <span data-ttu-id="8b947-227">Een apparaat verzendt berichten met apparaatgegevens bij het opstarten en in reactie tooa **SendDeviceInfo** opdracht.</span><span class="sxs-lookup"><span data-stu-id="8b947-227">A device sends device information messages at startup and in response tooa **SendDeviceInfo** command.</span></span> <span data-ttu-id="8b947-228">Deze taak wordt gebruikgemaakt van Hallo query definitie tooidentify na **apparaatgegevens** berichten:</span><span class="sxs-lookup"><span data-stu-id="8b947-228">This job uses hello following query definition tooidentify **device-info** messages:</span></span>

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

<span data-ttu-id="8b947-229">Deze taak wordt de uitvoer tooan Event Hub verzendt voor verdere verwerking.</span><span class="sxs-lookup"><span data-stu-id="8b947-229">This job sends its output tooan Event Hub for further processing.</span></span>

<span data-ttu-id="8b947-230">**Taak 2: regels** evalueren de binnenkomende telemetriegegevens over temperatuur en vochtigheid aan de hand van de drempelwaarden voor elk apparaat.</span><span class="sxs-lookup"><span data-stu-id="8b947-230">**Job 2: Rules** evaluates incoming temperature and humidity telemetry values against per-device thresholds.</span></span> <span data-ttu-id="8b947-231">Drempelwaarden zijn in Hallo regeleditor die beschikbaar zijn in de oplossingsportal Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8b947-231">Threshold values are set in hello rules editor available in hello solution portal.</span></span> <span data-ttu-id="8b947-232">Elk koppel apparaat/waarde wordt per tijdstempel opgeslagen in een blob die met Stream Analytics wordt gelezen als **referentiegegevens**.</span><span class="sxs-lookup"><span data-stu-id="8b947-232">Each device/value pair is stored by timestamp in a blob which Stream Analytics reads in as **Reference Data**.</span></span> <span data-ttu-id="8b947-233">Hallo taak vergelijkt elke niet-lege waarde tegen Hallo ingestelde drempelwaarde voor Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="8b947-233">hello job compares any non-empty value against hello set threshold for hello device.</span></span> <span data-ttu-id="8b947-234">Als deze groter is dan Hallo ' >' voorwaarde, Hallo taak voert een **alarm** gebeurtenis die dat Hallo drempelwaarde aangeeft wordt overschreden en biedt Hallo-apparaat, waarde en timestamp-waarden.</span><span class="sxs-lookup"><span data-stu-id="8b947-234">If it exceeds hello '>' condition, hello job outputs an **alarm** event that indicates that hello threshold is exceeded and provides hello device, value, and timestamp values.</span></span> <span data-ttu-id="8b947-235">Deze taak maakt gebruik van Hallo query definitie tooidentify telemetrieberichten die moeten worden geactiveerd door een waarschuwing te volgen:</span><span class="sxs-lookup"><span data-stu-id="8b947-235">This job uses hello following query definition tooidentify telemetry messages that should trigger an alarm:</span></span>

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

<span data-ttu-id="8b947-236">Hallo taak verzendt de uitvoer tooan Event Hub voor verdere verwerking en details van de opslag van elke waarschuwing tooblob opslaat uit waarbij de oplossingsportal Hallo Hallo waarschuwingsgegevens kan lezen.</span><span class="sxs-lookup"><span data-stu-id="8b947-236">hello job sends its output tooan Event Hub for further processing and saves details of each alert tooblob storage from where hello solution portal can read hello alert information.</span></span>

<span data-ttu-id="8b947-237">**Taak 3: Telemetrie** is van invloed op Hallo binnenkomende apparaat telemetriestroom op twee manieren.</span><span class="sxs-lookup"><span data-stu-id="8b947-237">**Job 3: Telemetry** operates on hello incoming device telemetry stream in two ways.</span></span> <span data-ttu-id="8b947-238">Hallo verzendt eerst alle telemetrieberichten van Hallo apparaten toopersistent blob-opslag voor langdurige opslag.</span><span class="sxs-lookup"><span data-stu-id="8b947-238">hello first sends all telemetry messages from hello devices toopersistent blob storage for long-term storage.</span></span> <span data-ttu-id="8b947-239">Hallo berekent een gemiddelde, de minimale en maximale vochtigheid gedurende een sliding window van vijf minuten en verzendt deze gegevens tooblob opslag tweede verbruik.</span><span class="sxs-lookup"><span data-stu-id="8b947-239">hello second computes average, minimum, and maximum humidity values over a five-minute sliding window and sends this data tooblob storage.</span></span> <span data-ttu-id="8b947-240">Hallo oplossingsportal leest Hallo telemetrische gegevens uit blob storage toopopulate Hallo grafieken.</span><span class="sxs-lookup"><span data-stu-id="8b947-240">hello solution portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="8b947-241">Deze taak maakt gebruik van Hallo volgende querydefinitie:</span><span class="sxs-lookup"><span data-stu-id="8b947-241">This job uses hello following query definition:</span></span>

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

## <a name="event-hubs"></a><span data-ttu-id="8b947-242">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8b947-242">Event Hubs</span></span>

<span data-ttu-id="8b947-243">Hallo **apparaatgegevens** en **regels** ASA-jobs uitvoer hun gegevens tooEvent Hubs tooreliably doorsturen op toohello **Gebeurtenisprocessor** in Hallo webtaak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8b947-243">hello **device info** and **rules** ASA jobs output their data tooEvent Hubs tooreliably forward on toohello **Event Processor** running in hello WebJob.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="8b947-244">Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="8b947-244">Azure storage</span></span>

<span data-ttu-id="8b947-245">Hallo-oplossing gebruikt Azure blob storage toopersist alle Hallo ruwe en het samengevatte telemetriegegevens van Hallo apparaten in Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="8b947-245">hello solution uses Azure blob storage toopersist all hello raw and summarized telemetry data from hello devices in hello solution.</span></span> <span data-ttu-id="8b947-246">Hallo portal leest Hallo telemetrische gegevens uit blob storage toopopulate Hallo grafieken.</span><span class="sxs-lookup"><span data-stu-id="8b947-246">hello portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="8b947-247">toodisplay waarschuwingen, oplossingsportal Hallo Hallo gegevens leest uit blob-opslag die records wanneer telemetrie waarden overschreden Hallo drempelwaarden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8b947-247">toodisplay alerts, hello solution portal reads hello data from blob storage that records when telemetry values exceeded hello configured threshold values.</span></span> <span data-ttu-id="8b947-248">Hallo-oplossing gebruikt ook blob storage toorecord Hallo drempelwaarden die u in de oplossingsportal Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="8b947-248">hello solution also uses blob storage toorecord hello threshold values you set in hello solution portal.</span></span>

## <a name="webjobs"></a><span data-ttu-id="8b947-249">Webtaken</span><span class="sxs-lookup"><span data-stu-id="8b947-249">WebJobs</span></span>

<span data-ttu-id="8b947-250">Bovendien toohosting Hallo apparaat simulatoren Hallo webtaken in Hallo oplossing ook host Hallo **Gebeurtenisprocessor** uitgevoerd in een Azure-webtaak die verantwoordelijk is voor reacties op opdrachten.</span><span class="sxs-lookup"><span data-stu-id="8b947-250">In addition toohosting hello device simulators, hello WebJobs in hello solution also host hello **Event Processor** running in an Azure WebJob that handles command responses.</span></span> <span data-ttu-id="8b947-251">Antwoord berichten tooupdate Hallo apparaat opdracht opdrachtgeschiedenis (opgeslagen in Hallo Cosmos DB database) wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8b947-251">It uses command response messages tooupdate hello device command history (stored in hello Cosmos DB database).</span></span>

## <a name="cosmos-db"></a><span data-ttu-id="8b947-252">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8b947-252">Cosmos DB</span></span>

<span data-ttu-id="8b947-253">Hallo-oplossing gebruikt een Cosmos-DB toostore databasegegevens over Hallo apparaten verbonden toohello oplossing.</span><span class="sxs-lookup"><span data-stu-id="8b947-253">hello solution uses a Cosmos DB database toostore information about hello devices connected toohello solution.</span></span> <span data-ttu-id="8b947-254">Deze informatie omvat Hallo geschiedenis van opdrachten toodevices verzonden vanaf de oplossingsportal hello en methoden die worden aangeroepen vanuit de portal van de oplossing Hallo.</span><span class="sxs-lookup"><span data-stu-id="8b947-254">This information includes hello history of commands sent toodevices from hello solution portal and of methods invoked from hello solution portal.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="8b947-255">Oplossingsportal</span><span class="sxs-lookup"><span data-stu-id="8b947-255">Solution portal</span></span>

<span data-ttu-id="8b947-256">Hallo oplossingsportal is een web-app geïmplementeerd als onderdeel van Hallo vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="8b947-256">hello solution portal is a web app deployed as part of hello preconfigured solution.</span></span> <span data-ttu-id="8b947-257">Hallo belangrijkste pagina's in de oplossingsportal Hallo zijn Hallo dashboard en de lijst met Hallo-apparaten.</span><span class="sxs-lookup"><span data-stu-id="8b947-257">hello key pages in hello solution portal are hello dashboard and hello device list.</span></span>

### <a name="dashboard"></a><span data-ttu-id="8b947-258">Dashboard</span><span class="sxs-lookup"><span data-stu-id="8b947-258">Dashboard</span></span>

<span data-ttu-id="8b947-259">Deze pagina in Hallo web-app maakt gebruik van PowerBI javascript-besturingselementen (Zie [PowerBI-visuals Reports](https://www.github.com/Microsoft/PowerBI-visuals)) toovisualize hello telemetriegegevens van Hallo-apparaten.</span><span class="sxs-lookup"><span data-stu-id="8b947-259">This page in hello web app uses PowerBI javascript controls (See [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) toovisualize hello telemetry data from hello devices.</span></span> <span data-ttu-id="8b947-260">Hallo-oplossing gebruikt Hallo ASA telemetrie taak toowrite Hallo telemetrie tooblob opslag van gegevens.</span><span class="sxs-lookup"><span data-stu-id="8b947-260">hello solution uses hello ASA telemetry job toowrite hello telemetry data tooblob storage.</span></span>

### <a name="device-list"></a><span data-ttu-id="8b947-261">Lijst met apparaten</span><span class="sxs-lookup"><span data-stu-id="8b947-261">Device list</span></span>

<span data-ttu-id="8b947-262">U kunt via deze pagina in de oplossingsportal Hallo:</span><span class="sxs-lookup"><span data-stu-id="8b947-262">From this page in hello solution portal you can:</span></span>

* <span data-ttu-id="8b947-263">Nieuwe apparaten inrichten.</span><span class="sxs-lookup"><span data-stu-id="8b947-263">Provision a new device.</span></span> <span data-ttu-id="8b947-264">Deze actie stelt Hallo unieke apparaat-id en verificatiesleutel Hallo genereert.</span><span class="sxs-lookup"><span data-stu-id="8b947-264">This action sets hello unique device id and generates hello authentication key.</span></span> <span data-ttu-id="8b947-265">Informatie over Hallo apparaat tooboth Hallo id-register IoT Hub en Hallo oplossings-specifieke Cosmos-DB-database geschreven.</span><span class="sxs-lookup"><span data-stu-id="8b947-265">It writes information about hello device tooboth hello IoT Hub identity registry and hello solution-specific Cosmos DB database.</span></span>
* <span data-ttu-id="8b947-266">Apparaateigenschappen beheren.</span><span class="sxs-lookup"><span data-stu-id="8b947-266">Manage device properties.</span></span> <span data-ttu-id="8b947-267">Deze actie omvat het weergeven van bestaande eigenschappen en het bijwerken met nieuwe eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="8b947-267">This action includes viewing existing properties and updating with new properties.</span></span>
* <span data-ttu-id="8b947-268">Opdrachten tooa apparaat verzenden.</span><span class="sxs-lookup"><span data-stu-id="8b947-268">Send commands tooa device.</span></span>
* <span data-ttu-id="8b947-269">Hallo opdrachtgeschiedenis voor een apparaat weergeven.</span><span class="sxs-lookup"><span data-stu-id="8b947-269">View hello command history for a device.</span></span>
* <span data-ttu-id="8b947-270">Apparaten in- en uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="8b947-270">Enable and disable devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b947-271">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8b947-271">Next steps</span></span>

<span data-ttu-id="8b947-272">Hallo bieden volgende TechNet-blogberichten meer informatie over vooraf geconfigureerde oplossing voor externe controle Hallo:</span><span class="sxs-lookup"><span data-stu-id="8b947-272">hello following TechNet blog posts provide more detail about hello remote monitoring preconfigured solution:</span></span>

* [<span data-ttu-id="8b947-273">IoT Suite - Under Hallo schermen - externe controle</span><span class="sxs-lookup"><span data-stu-id="8b947-273">IoT Suite - Under hello Hood - Remote Monitoring</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [<span data-ttu-id="8b947-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices (IoT Suite - externe controle - live- en gesimuleerde apparaten toevoegen)</span><span class="sxs-lookup"><span data-stu-id="8b947-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

<span data-ttu-id="8b947-275">U kunt blijven aan de slag met IoT Suite door te lezen Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8b947-275">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="8b947-276">[Verbinding maken met uw apparaat toohello vooraf geconfigureerde oplossing voor externe controle][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="8b947-276">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="8b947-277">[Machtigingen op Hallo azureiotsuite.com site][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="8b947-277">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

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

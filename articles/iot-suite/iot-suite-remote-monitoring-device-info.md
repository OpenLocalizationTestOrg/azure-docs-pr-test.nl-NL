---
title: Metagegevens van apparaten informatie in de oplossing voor externe controle | Microsoft Docs
description: Een beschrijving van de vooraf geconfigureerde oplossing voor externe controle IoT Azure en de bijbehorende architectuur.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: f8fd452806a0a0b98cf8e434c9bd55700083a6c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="device-information-metadata-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="8f513-103">Metagegevens van apparaten informatie in de vooraf geconfigureerde oplossing voor externe controle</span><span class="sxs-lookup"><span data-stu-id="8f513-103">Device information metadata in the remote monitoring preconfigured solution</span></span>

<span data-ttu-id="8f513-104">De Azure IoT Suite vooraf geconfigureerde oplossing voor externe controle demonstreert een benadering voor het beheren van metagegevens van apparaten.</span><span class="sxs-lookup"><span data-stu-id="8f513-104">The Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="8f513-105">In dit artikel bevat een overzicht van de aanpak van die deze oplossing nodig is om te begrijpen:</span><span class="sxs-lookup"><span data-stu-id="8f513-105">This article outlines the approach this solution takes to enable you to understand:</span></span>

* <span data-ttu-id="8f513-106">De metagegevens van welke apparaten de oplossing worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8f513-106">What device metadata the solution stores.</span></span>
* <span data-ttu-id="8f513-107">Hoe de oplossing de metagegevens van de apparaten beheert.</span><span class="sxs-lookup"><span data-stu-id="8f513-107">How the solution manages the device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="8f513-108">Context</span><span class="sxs-lookup"><span data-stu-id="8f513-108">Context</span></span>

<span data-ttu-id="8f513-109">Externe controle vooraf geconfigureerde oplossing maakt gebruik van [Azure IoT Hub] [ lnk-iot-hub] waarmee uw apparaten gegevens verzenden naar de cloud.</span><span class="sxs-lookup"><span data-stu-id="8f513-109">The remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] to enable your devices to send data to the cloud.</span></span> <span data-ttu-id="8f513-110">De oplossing bevat gegevens over de apparaten in drie verschillende locaties:</span><span class="sxs-lookup"><span data-stu-id="8f513-110">The solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="8f513-111">Locatie</span><span class="sxs-lookup"><span data-stu-id="8f513-111">Location</span></span> | <span data-ttu-id="8f513-112">Gegevens die zijn opgeslagen</span><span class="sxs-lookup"><span data-stu-id="8f513-112">Information stored</span></span> | <span data-ttu-id="8f513-113">Implementatie</span><span class="sxs-lookup"><span data-stu-id="8f513-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="8f513-114">ID-register</span><span class="sxs-lookup"><span data-stu-id="8f513-114">Identity registry</span></span> | <span data-ttu-id="8f513-115">Apparaat-id, verificatiesleutels, de status ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="8f513-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="8f513-116">Ingebouwd in IoT-Hub</span><span class="sxs-lookup"><span data-stu-id="8f513-116">Built in to IoT Hub</span></span> |
| <span data-ttu-id="8f513-117">Apparaat horende</span><span class="sxs-lookup"><span data-stu-id="8f513-117">Device twins</span></span> | <span data-ttu-id="8f513-118">Metagegevens: gemelde eigenschappen, gewenste eigenschappen, tags</span><span class="sxs-lookup"><span data-stu-id="8f513-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="8f513-119">Ingebouwd in IoT-Hub</span><span class="sxs-lookup"><span data-stu-id="8f513-119">Built in to IoT Hub</span></span> |
| <span data-ttu-id="8f513-120">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8f513-120">Cosmos DB</span></span> | <span data-ttu-id="8f513-121">Geschiedenis van de opdracht en methode</span><span class="sxs-lookup"><span data-stu-id="8f513-121">Command and method history</span></span> | <span data-ttu-id="8f513-122">Aangepaste voor oplossing</span><span class="sxs-lookup"><span data-stu-id="8f513-122">Custom for solution</span></span> |

<span data-ttu-id="8f513-123">IoT-Hub bevat een [register voor apparaat-id's] [ lnk-identity-registry] voor het beheren van toegang tot een IoT-hub en maakt gebruik van [apparaat horende] [ lnk-device-twin] voor het beheren van metagegevens van apparaten.</span><span class="sxs-lookup"><span data-stu-id="8f513-123">IoT Hub includes a [device identity registry][lnk-identity-registry] to manage access to an IoT hub and uses [device twins][lnk-device-twin] to manage device metadata.</span></span> <span data-ttu-id="8f513-124">Er is ook een externe controle oplossings-specifieke *apparaatregister* die worden opgeslagen geschiedenis van de opdracht en de methode.</span><span class="sxs-lookup"><span data-stu-id="8f513-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="8f513-125">Maakt gebruik van de oplossing voor externe controle een [Cosmos DB] [ lnk-docdb] database voor het implementeren van een aangepast archief voor de opdracht en methode geschiedenis.</span><span class="sxs-lookup"><span data-stu-id="8f513-125">The remote monitoring solution uses a [Cosmos DB][lnk-docdb] database to implement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="8f513-126">De vooraf geconfigureerde oplossing voor externe controle houdt het register voor apparaat-id's gesynchroniseerd met de informatie in de database van de Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="8f513-126">The remote monitoring preconfigured solution keeps the device identity registry in sync with the information in the Cosmos DB database.</span></span> <span data-ttu-id="8f513-127">Beide dezelfde apparaat-id gebruiken voor het aanduiden van elk apparaat dat is verbonden met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8f513-127">Both use the same device id to uniquely identify each device connected to your IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="8f513-128">Metagegevens van apparaten</span><span class="sxs-lookup"><span data-stu-id="8f513-128">Device metadata</span></span>

<span data-ttu-id="8f513-129">IoT Hub onderhoudt een [apparaat twin] [ lnk-device-twin] voor elke gesimuleerde en het fysieke apparaat is verbonden met een oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="8f513-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected to a remote monitoring solution.</span></span> <span data-ttu-id="8f513-130">De oplossing maakt gebruik van apparaat horende voor het beheren van de metagegevens gekoppeld aan apparaten.</span><span class="sxs-lookup"><span data-stu-id="8f513-130">The solution uses device twins to manage the metadata associated with devices.</span></span> <span data-ttu-id="8f513-131">Een apparaat-twin is een JSON-document bijgehouden door de IoT Hub en de oplossing maakt gebruik van de IoT Hub-API om te communiceren met horende apparaten.</span><span class="sxs-lookup"><span data-stu-id="8f513-131">A device twin is a JSON document maintained by IoT Hub, and the solution uses the IoT Hub API to interact with device twins.</span></span>

<span data-ttu-id="8f513-132">Een apparaat-twin drie soorten metagegevens worden opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="8f513-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="8f513-133">*Eigenschappen gerapporteerd* naar een IoT-hub worden verzonden door een apparaat.</span><span class="sxs-lookup"><span data-stu-id="8f513-133">*Reported properties* are sent to an IoT hub by a device.</span></span> <span data-ttu-id="8f513-134">In de oplossing voor externe controle gesimuleerde apparaten verzenden gemelde eigenschappen bij het opstarten en in reactie op **Changedevicestate** opdrachten en -methoden.</span><span class="sxs-lookup"><span data-stu-id="8f513-134">In the remote monitoring solution, simulated devices send reported properties at start-up and in response to **Change device state** commands and methods.</span></span> <span data-ttu-id="8f513-135">U kunt weergeven gemelde eigenschappen in de **lijst met apparaten** en **details apparaat** in de portal van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="8f513-135">You can view reported properties in the **Device list** and **Device details** in the solution portal.</span></span> <span data-ttu-id="8f513-136">Gerapporteerde eigenschappen zijn alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="8f513-136">Reported properties are read only.</span></span>
- <span data-ttu-id="8f513-137">*Eigenschappen gewenst* door apparaten worden opgehaald uit de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8f513-137">*Desired properties* are retrieved from the IoT hub by devices.</span></span> <span data-ttu-id="8f513-138">Het is de verantwoordelijkheid van het apparaat nodig configuratiewijziging op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="8f513-138">It is the responsibility of the device to make any necessary configuration change on the device.</span></span> <span data-ttu-id="8f513-139">Het is ook de verantwoordelijkheid van het apparaat voor het rapporteren van de wijziging terug naar de hub als een eigenschap gemeld.</span><span class="sxs-lookup"><span data-stu-id="8f513-139">It is also the responsibility of the device to report the change back to the hub as a reported property.</span></span> <span data-ttu-id="8f513-140">U kunt een waarde van de gewenste eigenschap via de portal van de oplossing instellen.</span><span class="sxs-lookup"><span data-stu-id="8f513-140">You can set a desired property value through the solution portal.</span></span>
- <span data-ttu-id="8f513-141">*Labels* bestaan alleen in de apparaat-twin en zijn nooit gesynchroniseerd met een apparaat.</span><span class="sxs-lookup"><span data-stu-id="8f513-141">*Tags* only exist in the device twin and are never synchronized with a device.</span></span> <span data-ttu-id="8f513-142">U kunt in de oplossingsportal labelwaarden en ze gebruiken bij het filteren van de lijst met apparaten.</span><span class="sxs-lookup"><span data-stu-id="8f513-142">You can set tag values in the solution portal and use them when you filter the list of devices.</span></span> <span data-ttu-id="8f513-143">De oplossing gebruikt ook een code voor het identificeren van het pictogram moet worden weergegeven voor een apparaat in de portal van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="8f513-143">The solution also uses a tag to identify the icon to display for a device in the solution portal.</span></span>

<span data-ttu-id="8f513-144">Voorbeeld gerapporteerd eigenschappen van de gesimuleerde apparaten zijn onder meer de fabrikant, modelnummer breedtegraad en lengtegraad.</span><span class="sxs-lookup"><span data-stu-id="8f513-144">Example reported properties from the simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="8f513-145">De lijst met ondersteunde methodes gesimuleerde apparaten ook geretourneerd als een eigenschap gemeld.</span><span class="sxs-lookup"><span data-stu-id="8f513-145">Simulated devices also return the list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="8f513-146">De code van het gesimuleerde apparaat gebruikt alleen de gewenste eigenschappen **Desired.Config.TemperatureMeanValue** en **Desired.Config.TelemetryInterval** om de gerapporteerde eigenschappen bij te werken die naar IoT Hub worden teruggestuurd.</span><span class="sxs-lookup"><span data-stu-id="8f513-146">The simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties sent back to IoT Hub.</span></span> <span data-ttu-id="8f513-147">Alle andere gewenste eigenschap wijzigingsaanvragen worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="8f513-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="8f513-148">Een apparaat informatie metagegevens JSON-document opgeslagen in de database apparaat register Cosmos DB heeft de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="8f513-148">A device information metadata JSON document stored in the device registry Cosmos DB database has the following structure:</span></span>

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> <span data-ttu-id="8f513-149">Gegevens van een apparaat kan ook betekenen metagegevens om te beschrijven de telemetrie die het apparaat naar IoT Hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="8f513-149">Device information can also include metadata to describe the telemetry the device sends to IoT Hub.</span></span> <span data-ttu-id="8f513-150">De oplossing voor externe controle gebruikt deze metagegevens telemetrie naar de weergave van het dashboard [dynamische telemetrie][lnk-dynamic-telemetry].</span><span class="sxs-lookup"><span data-stu-id="8f513-150">The remote monitoring solution uses this telemetry metadata to customize how the dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="8f513-151">Levenscyclus</span><span class="sxs-lookup"><span data-stu-id="8f513-151">Lifecycle</span></span>

<span data-ttu-id="8f513-152">Wanneer u eerst een apparaat in de portal van de oplossing maakt, maakt de oplossing een vermelding in de database van de Cosmos-database voor het opslaan van de geschiedenis van de opdracht en de methode.</span><span class="sxs-lookup"><span data-stu-id="8f513-152">When you first create a device in the solution portal, the solution creates an entry in the Cosmos DB database to store command and method history.</span></span> <span data-ttu-id="8f513-153">De oplossing maakt op dit moment ook een vermelding voor het apparaat in het identiteitenregister van apparaten, waardoor de sleutels die het apparaat gebruikt om te verifiëren met IoT Hub worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="8f513-153">At this point, the solution also creates an entry for the device in the device identity registry, which generates the keys the device uses to authenticate with IoT Hub.</span></span> <span data-ttu-id="8f513-154">Dit leidt ook tot een apparaat-twin.</span><span class="sxs-lookup"><span data-stu-id="8f513-154">It also creates a device twin.</span></span>

<span data-ttu-id="8f513-155">Wanneer een apparaat is eerst verbinding met de oplossing maakt, stuurt het gerapporteerde eigenschappen en een informatiebericht van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="8f513-155">When a device first connects to the solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="8f513-156">De gerapporteerde eigenschapswaarden worden automatisch opgeslagen in de apparaat-twin.</span><span class="sxs-lookup"><span data-stu-id="8f513-156">The reported property values are automatically saved in the device twin.</span></span> <span data-ttu-id="8f513-157">De gerapporteerde eigenschappen zijn de fabrikant, modelnummer, serienummer en een lijst van ondersteunde methoden.</span><span class="sxs-lookup"><span data-stu-id="8f513-157">The reported properties include the device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="8f513-158">Het apparaat informatie-bericht bevat de lijst met het apparaat inclusief informatie over alle parameters van de ondersteunt opdrachten.</span><span class="sxs-lookup"><span data-stu-id="8f513-158">The device information message includes the list of the commands the device supports including information about any command parameters.</span></span> <span data-ttu-id="8f513-159">Wanneer de oplossing voor dit bericht ontvangt, wordt de informatie van de apparaten in de database van de Cosmos-database bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="8f513-159">When the solution receives this message, it updates the device information in the Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-the-solution-portal"></a><span data-ttu-id="8f513-160">Apparaat-informatie in de oplossingsportal weergeven en bewerken</span><span class="sxs-lookup"><span data-stu-id="8f513-160">View and edit device information in the solution portal</span></span>

<span data-ttu-id="8f513-161">De lijst met apparaten in de oplossingsportal standaard als kolommen in de volgende eigenschappen van de apparaten weergegeven: **Status**, **DeviceId**, **fabrikant**, **modelnummer**, **serienummer**, **Firmware**, **Platform**, **Processor**, en **geïnstalleerd RAM-geheugen**.</span><span class="sxs-lookup"><span data-stu-id="8f513-161">The device list in the solution portal displays the following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="8f513-162">U kunt de kolommen aanpassen door te klikken op **kolom editor**.</span><span class="sxs-lookup"><span data-stu-id="8f513-162">You can customize the columns by clicking **Column editor**.</span></span> <span data-ttu-id="8f513-163">Eigenschappen voor het apparaat **breedtegraad** en **lengtegraad** station van de locatie in de Bing-kaart op het dashboard.</span><span class="sxs-lookup"><span data-stu-id="8f513-163">The device properties **Latitude** and **Longitude** drive the location in the Bing Map on the dashboard.</span></span>

![Editor voor kolom in de lijst met apparaten][img-device-list]

<span data-ttu-id="8f513-165">In de **Apparaatdetails** deelvenster in de oplossingsportal kunt u de eigenschappen van de gewenste en labels bewerken (gerapporteerd eigenschappen zijn alleen-lezen).</span><span class="sxs-lookup"><span data-stu-id="8f513-165">In the **Device Details** pane in the solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![Deelvenster Apparaatdetails][img-device-edit]

<span data-ttu-id="8f513-167">De oplossingsportal kunt u een apparaat verwijdert uit uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="8f513-167">You can use the solution portal to remove a device from your solution.</span></span> <span data-ttu-id="8f513-168">Wanneer u een apparaat verwijdert, wordt de oplossing voor de apparaatvermelding verwijdert uit het identiteitenregister en verwijdert vervolgens de apparaat-twin.</span><span class="sxs-lookup"><span data-stu-id="8f513-168">When you remove a device, the solution removes the device entry from identity registry and then deletes the device twin.</span></span> <span data-ttu-id="8f513-169">De oplossing ook verwijderd informatie met betrekking tot het apparaat uit de database van de Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="8f513-169">The solution also removes information related to the device from the Cosmos DB database.</span></span> <span data-ttu-id="8f513-170">Voordat u een apparaat verwijdert kunt, moet u deze uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="8f513-170">Before you can remove a device, you must disable it.</span></span>

![Apparaat verwijderen][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="8f513-172">Apparaat informatie berichtverwerking</span><span class="sxs-lookup"><span data-stu-id="8f513-172">Device information message processing</span></span>

<span data-ttu-id="8f513-173">Berichten met apparaatgegevens verzonden door een apparaat zijn telemetrieberichten.</span><span class="sxs-lookup"><span data-stu-id="8f513-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="8f513-174">Berichten met apparaatgegevens omvatten de opdrachten die een apparaat kan reageren, en eventuele opdrachtgeschiedenis.</span><span class="sxs-lookup"><span data-stu-id="8f513-174">Device information messages include the commands a device can respond to, and any command history.</span></span> <span data-ttu-id="8f513-175">IoT-Hub zelf heeft geen informatie over de metagegevens in het informatiebericht van een apparaat en het bericht verwerkt op dezelfde manier die alle apparaat-naar-cloud-berichten worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="8f513-175">IoT Hub itself has no knowledge of the metadata contained in a device information message and processes the message in the same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="8f513-176">In de oplossing voor externe controle een [Azure Stream Analytics] [ lnk-stream-analytics] (ASA)-taak de berichten uit IoT Hub kan lezen.</span><span class="sxs-lookup"><span data-stu-id="8f513-176">In the remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads the messages from IoT Hub.</span></span> <span data-ttu-id="8f513-177">De **DeviceInfo** stream analytics-taak filters voor berichten met **'ObjectType': 'DeviceInfo'** en stuurt ze de **EventProcessorHost** hostexemplaar dat wordt uitgevoerd in een web-taak.</span><span class="sxs-lookup"><span data-stu-id="8f513-177">The **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them to the **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="8f513-178">Logica in de **EventProcessorHost** exemplaar gebruikt de apparaat-id voor de Cosmos-DB-record vinden voor het specifieke apparaat en update voor de record.</span><span class="sxs-lookup"><span data-stu-id="8f513-178">Logic in the **EventProcessorHost** instance uses the device id to find the Cosmos DB record for the specific device and update the record.</span></span>

> [!NOTE]
> <span data-ttu-id="8f513-179">Een informatiebericht van het apparaat is een standaard apparaat-naar-cloud-bericht.</span><span class="sxs-lookup"><span data-stu-id="8f513-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="8f513-180">De oplossing wordt onderscheid gemaakt tussen berichten met apparaatgegevens en telemetrieberichten met behulp van de ASA-query's.</span><span class="sxs-lookup"><span data-stu-id="8f513-180">The solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f513-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8f513-181">Next steps</span></span>

<span data-ttu-id="8f513-182">Nu u klaar bent met het leren hoe u de vooraf geconfigureerde oplossingen kunt aanpassen, vindt u enkele van de andere functies en mogelijkheden van de vooraf geconfigureerde IoT Suite-oplossingen:</span><span class="sxs-lookup"><span data-stu-id="8f513-182">Now you've finished learning how you can customize the preconfigured solutions, you can explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="8f513-183">[Overzicht van voorspeld onderhoud vooraf geconfigureerde oplossing][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="8f513-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="8f513-184">[Veelgestelde vragen over IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="8f513-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="8f513-185">[Fundamentele IoT-beveiliging][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="8f513-185">[IoT security from the ground up][lnk-security-groundup]</span></span>

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md

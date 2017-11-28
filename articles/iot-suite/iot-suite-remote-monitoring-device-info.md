---
title: aaaDevice informatie metagegevens in Hallo oplossing voor externe controle | Microsoft Docs
description: Een beschrijving van hello Azure IoT vooraf geconfigureerde oplossing voor externe controle en de bijbehorende architectuur.
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
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="075be-103">Metagegevens van apparaten informatie in Hallo vooraf geconfigureerde oplossing voor externe controle</span><span class="sxs-lookup"><span data-stu-id="075be-103">Device information metadata in hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="075be-104">Hello Azure IoT Suite vooraf geconfigureerde oplossing voor externe controle demonstreert een benadering voor het beheren van metagegevens van apparaten.</span><span class="sxs-lookup"><span data-stu-id="075be-104">hello Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="075be-105">In dit artikel bevat een overzicht van Hallo benadering deze oplossing wordt tooenable u toounderstand:</span><span class="sxs-lookup"><span data-stu-id="075be-105">This article outlines hello approach this solution takes tooenable you toounderstand:</span></span>

* <span data-ttu-id="075be-106">Welke oplossing Hallo metagegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="075be-106">What device metadata hello solution stores.</span></span>
* <span data-ttu-id="075be-107">Hoe beheert Hallo oplossing Hallo Apparaatmetagegevens.</span><span class="sxs-lookup"><span data-stu-id="075be-107">How hello solution manages hello device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="075be-108">Context</span><span class="sxs-lookup"><span data-stu-id="075be-108">Context</span></span>

<span data-ttu-id="075be-109">Hallo externe controle vooraf geconfigureerde oplossing maakt gebruik van [Azure IoT Hub] [ lnk-iot-hub] tooenable uw apparaten toosend gegevens toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="075be-109">hello remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] tooenable your devices toosend data toohello cloud.</span></span> <span data-ttu-id="075be-110">Hallo oplossing bevat informatie over apparaten op drie verschillende locaties:</span><span class="sxs-lookup"><span data-stu-id="075be-110">hello solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="075be-111">Locatie</span><span class="sxs-lookup"><span data-stu-id="075be-111">Location</span></span> | <span data-ttu-id="075be-112">Gegevens die zijn opgeslagen</span><span class="sxs-lookup"><span data-stu-id="075be-112">Information stored</span></span> | <span data-ttu-id="075be-113">Implementatie</span><span class="sxs-lookup"><span data-stu-id="075be-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="075be-114">ID-register</span><span class="sxs-lookup"><span data-stu-id="075be-114">Identity registry</span></span> | <span data-ttu-id="075be-115">Apparaat-id, verificatiesleutels, de status ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="075be-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="075be-116">Ingebouwde tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="075be-116">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="075be-117">Apparaat horende</span><span class="sxs-lookup"><span data-stu-id="075be-117">Device twins</span></span> | <span data-ttu-id="075be-118">Metagegevens: gemelde eigenschappen, gewenste eigenschappen, tags</span><span class="sxs-lookup"><span data-stu-id="075be-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="075be-119">Ingebouwde tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="075be-119">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="075be-120">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="075be-120">Cosmos DB</span></span> | <span data-ttu-id="075be-121">Geschiedenis van de opdracht en methode</span><span class="sxs-lookup"><span data-stu-id="075be-121">Command and method history</span></span> | <span data-ttu-id="075be-122">Aangepaste voor oplossing</span><span class="sxs-lookup"><span data-stu-id="075be-122">Custom for solution</span></span> |

<span data-ttu-id="075be-123">IoT-Hub bevat een [register voor apparaat-id's] [ lnk-identity-registry] toomanage toegang tot tooan iothub en maakt gebruik van [apparaat horende] [ lnk-device-twin] toomanage Apparaatmetagegevens .</span><span class="sxs-lookup"><span data-stu-id="075be-123">IoT Hub includes a [device identity registry][lnk-identity-registry] toomanage access tooan IoT hub and uses [device twins][lnk-device-twin] toomanage device metadata.</span></span> <span data-ttu-id="075be-124">Er is ook een externe controle oplossings-specifieke *apparaatregister* die worden opgeslagen geschiedenis van de opdracht en de methode.</span><span class="sxs-lookup"><span data-stu-id="075be-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="075be-125">Hallo voor externe controle oplossing gebruikt een [Cosmos DB] [ lnk-docdb] database tooimplement een aangepast archief voor de opdracht en methode geschiedenis.</span><span class="sxs-lookup"><span data-stu-id="075be-125">hello remote monitoring solution uses a [Cosmos DB][lnk-docdb] database tooimplement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="075be-126">Hallo vooraf geconfigureerde oplossing voor externe controle houdt register Hallo apparaat-id's gesynchroniseerd met de Hallo informatie in Hallo Cosmos-DB-database.</span><span class="sxs-lookup"><span data-stu-id="075be-126">hello remote monitoring preconfigured solution keeps hello device identity registry in sync with hello information in hello Cosmos DB database.</span></span> <span data-ttu-id="075be-127">Beide gebruik van dezelfde apparaat-id toouniquely identificeren Hallo elk apparaat verbonden tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="075be-127">Both use hello same device id toouniquely identify each device connected tooyour IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="075be-128">Metagegevens van apparaten</span><span class="sxs-lookup"><span data-stu-id="075be-128">Device metadata</span></span>

<span data-ttu-id="075be-129">IoT Hub onderhoudt een [apparaat twin] [ lnk-device-twin] voor elk apparaat gesimuleerde en fysieke verbonden tooa oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="075be-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected tooa remote monitoring solution.</span></span> <span data-ttu-id="075be-130">Hallo-oplossing gebruikt horende toomanage Hallo metagegevens van apparaten die zijn gekoppeld aan apparaten.</span><span class="sxs-lookup"><span data-stu-id="075be-130">hello solution uses device twins toomanage hello metadata associated with devices.</span></span> <span data-ttu-id="075be-131">Een apparaat-twin is een JSON-document bijgehouden door de IoT Hub en Hallo oplossing maakt gebruik van Hallo IoT Hub API toointeract met horende apparaten.</span><span class="sxs-lookup"><span data-stu-id="075be-131">A device twin is a JSON document maintained by IoT Hub, and hello solution uses hello IoT Hub API toointeract with device twins.</span></span>

<span data-ttu-id="075be-132">Een apparaat-twin drie soorten metagegevens worden opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="075be-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="075be-133">*Eigenschappen gerapporteerd* tooan iothub worden verzonden door een apparaat.</span><span class="sxs-lookup"><span data-stu-id="075be-133">*Reported properties* are sent tooan IoT hub by a device.</span></span> <span data-ttu-id="075be-134">In de oplossing voor externe controle hello, gesimuleerde apparaten verzenden gemelde eigenschappen bij het opstarten en in reactie te**Changedevicestate** opdrachten en -methoden.</span><span class="sxs-lookup"><span data-stu-id="075be-134">In hello remote monitoring solution, simulated devices send reported properties at start-up and in response too**Change device state** commands and methods.</span></span> <span data-ttu-id="075be-135">U kunt gemelde eigenschappen weergeven in Hallo **lijst met apparaten** en **details apparaat** in de oplossingsportal Hallo.</span><span class="sxs-lookup"><span data-stu-id="075be-135">You can view reported properties in hello **Device list** and **Device details** in hello solution portal.</span></span> <span data-ttu-id="075be-136">Gerapporteerde eigenschappen zijn alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="075be-136">Reported properties are read only.</span></span>
- <span data-ttu-id="075be-137">*Eigenschappen gewenst* worden opgehaald uit de IoT-hub Hallo door apparaten.</span><span class="sxs-lookup"><span data-stu-id="075be-137">*Desired properties* are retrieved from hello IoT hub by devices.</span></span> <span data-ttu-id="075be-138">Het is de verantwoordelijkheid Hallo van Hallo apparaat toomake alle benodigde configuratie wijzigen op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="075be-138">It is hello responsibility of hello device toomake any necessary configuration change on hello device.</span></span> <span data-ttu-id="075be-139">Het is ook Hallo verantwoordelijkheid van Hallo apparaat tooreport Hallo wijziging back toohello hub als een eigenschap gemeld.</span><span class="sxs-lookup"><span data-stu-id="075be-139">It is also hello responsibility of hello device tooreport hello change back toohello hub as a reported property.</span></span> <span data-ttu-id="075be-140">U kunt een waarde van de gewenste eigenschap via de portal van de oplossing Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="075be-140">You can set a desired property value through hello solution portal.</span></span>
- <span data-ttu-id="075be-141">*Labels* alleen bestaan in Hallo apparaat twin en nooit worden gesynchroniseerd met een apparaat.</span><span class="sxs-lookup"><span data-stu-id="075be-141">*Tags* only exist in hello device twin and are never synchronized with a device.</span></span> <span data-ttu-id="075be-142">U kunt in de oplossingsportal Hallo labelwaarden en ze gebruiken bij het filteren van Hallo lijst met apparaten.</span><span class="sxs-lookup"><span data-stu-id="075be-142">You can set tag values in hello solution portal and use them when you filter hello list of devices.</span></span> <span data-ttu-id="075be-143">een label tooidentify Hallo pictogram toodisplay Hallo oplossing ook gebruikt voor een apparaat in de oplossingsportal Hallo.</span><span class="sxs-lookup"><span data-stu-id="075be-143">hello solution also uses a tag tooidentify hello icon toodisplay for a device in hello solution portal.</span></span>

<span data-ttu-id="075be-144">Voorbeeld gerapporteerd eigenschappen van Hallo gesimuleerde apparaten zijn onder meer de fabrikant, modelnummer breedtegraad en lengtegraad.</span><span class="sxs-lookup"><span data-stu-id="075be-144">Example reported properties from hello simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="075be-145">Hallo-lijst van ondersteunde methoden gesimuleerde apparaten ook geretourneerd als een gerapporteerde eigenschap.</span><span class="sxs-lookup"><span data-stu-id="075be-145">Simulated devices also return hello list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="075be-146">Hallo gesimuleerd apparaatcode gebruikt alleen Hallo **Desired.Config.TemperatureMeanValue** en **Desired.Config.TelemetryInterval** gewenste eigenschappen tooupdate Hallo eigenschappen teruggestuurd gerapporteerd tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="075be-146">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="075be-147">Alle andere gewenste eigenschap wijzigingsaanvragen worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="075be-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="075be-148">Een apparaat informatie metagegevens JSON-document opgeslagen in Hallo apparaat register Cosmos-DB-database heeft Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="075be-148">A device information metadata JSON document stored in hello device registry Cosmos DB database has hello following structure:</span></span>

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
> <span data-ttu-id="075be-149">Gegevens van een apparaat kan ook metagegevens toodescribe Hallo telemetrie Hallo apparaat verzendt tooIoT Hub bevatten.</span><span class="sxs-lookup"><span data-stu-id="075be-149">Device information can also include metadata toodescribe hello telemetry hello device sends tooIoT Hub.</span></span> <span data-ttu-id="075be-150">Hallo-oplossing voor externe controle maakt gebruik van deze telemetrie metagegevens toocustomize hoe Hallo dashboard toont de [dynamische telemetrie][lnk-dynamic-telemetry].</span><span class="sxs-lookup"><span data-stu-id="075be-150">hello remote monitoring solution uses this telemetry metadata toocustomize how hello dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="075be-151">Levenscyclus</span><span class="sxs-lookup"><span data-stu-id="075be-151">Lifecycle</span></span>

<span data-ttu-id="075be-152">Wanneer u eerst een apparaat in de oplossingsportal Hallo maakt, maakt Hallo oplossing een vermelding in Hallo Cosmos DB database toostore opdracht en de geschiedenis van de methode.</span><span class="sxs-lookup"><span data-stu-id="075be-152">When you first create a device in hello solution portal, hello solution creates an entry in hello Cosmos DB database toostore command and method history.</span></span> <span data-ttu-id="075be-153">Hallo-oplossing maakt een vermelding voor Hallo apparaat op dit moment ook in Hallo apparaat identiteitenregister, waardoor Hallo sleutels Hallo apparaat maakt gebruik van tooauthenticate met IoT Hub worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="075be-153">At this point, hello solution also creates an entry for hello device in hello device identity registry, which generates hello keys hello device uses tooauthenticate with IoT Hub.</span></span> <span data-ttu-id="075be-154">Dit leidt ook tot een apparaat-twin.</span><span class="sxs-lookup"><span data-stu-id="075be-154">It also creates a device twin.</span></span>

<span data-ttu-id="075be-155">Wanneer een apparaat toohello oplossing de eerst verbinding maakt, wordt gemeld eigenschappen en een informatiebericht van het apparaat verzonden.</span><span class="sxs-lookup"><span data-stu-id="075be-155">When a device first connects toohello solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="075be-156">Hallo gerapporteerd eigenschapswaarden worden automatisch opgeslagen in Hallo apparaat twin.</span><span class="sxs-lookup"><span data-stu-id="075be-156">hello reported property values are automatically saved in hello device twin.</span></span> <span data-ttu-id="075be-157">Hallo gerapporteerd eigenschappen zijn onder meer apparaatfabrikant hello, modelnummer, serienummer en een lijst van ondersteunde methoden.</span><span class="sxs-lookup"><span data-stu-id="075be-157">hello reported properties include hello device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="075be-158">Hallo-bericht van apparaat informatie bevat de lijst Hallo Hallo opdrachten Hallo apparaat inclusief informatie over eventuele opdrachtparameters ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="075be-158">hello device information message includes hello list of hello commands hello device supports including information about any command parameters.</span></span> <span data-ttu-id="075be-159">Wanneer Hallo oplossing dit bericht ontvangt, werkt het Hallo-apparaatgegevens in Hallo Cosmos-DB-database.</span><span class="sxs-lookup"><span data-stu-id="075be-159">When hello solution receives this message, it updates hello device information in hello Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a><span data-ttu-id="075be-160">Apparaat-informatie in de oplossingsportal Hallo weergeven en bewerken</span><span class="sxs-lookup"><span data-stu-id="075be-160">View and edit device information in hello solution portal</span></span>

<span data-ttu-id="075be-161">Hallo lijst met apparaten in de oplossingsportal Hallo geeft Hallo apparaateigenschappen volgen als kolommen in een standaard: **Status**, **DeviceId**, **fabrikant**, **Modelnummer**, **serienummer**, **Firmware**, **Platform**, **Processor**, en  **Geïnstalleerd RAM-geheugen**.</span><span class="sxs-lookup"><span data-stu-id="075be-161">hello device list in hello solution portal displays hello following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="075be-162">U kunt Hallo kolommen aanpassen door te klikken op **kolom editor**.</span><span class="sxs-lookup"><span data-stu-id="075be-162">You can customize hello columns by clicking **Column editor**.</span></span> <span data-ttu-id="075be-163">Apparaateigenschappen Hallo **breedtegraad** en **lengtegraad** station Hallo locatie in Hallo Bing-kaart op Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="075be-163">hello device properties **Latitude** and **Longitude** drive hello location in hello Bing Map on hello dashboard.</span></span>

![Editor voor kolom in de lijst met apparaten][img-device-list]

<span data-ttu-id="075be-165">In Hallo **Apparaatdetails** deelvenster in de oplossingsportal hello, kunt u gewenste eigenschappen en labels bewerken (gerapporteerd eigenschappen zijn alleen-lezen).</span><span class="sxs-lookup"><span data-stu-id="075be-165">In hello **Device Details** pane in hello solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![Deelvenster Apparaatdetails][img-device-edit]

<span data-ttu-id="075be-167">U kunt Hallo oplossing portal tooremove een apparaat gebruiken van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="075be-167">You can use hello solution portal tooremove a device from your solution.</span></span> <span data-ttu-id="075be-168">Wanneer u een apparaat verwijdert, wordt Hallo oplossing vermelding Hallo-apparaat verwijdert uit het identiteitenregister en verwijdert vervolgens Hallo apparaat twin.</span><span class="sxs-lookup"><span data-stu-id="075be-168">When you remove a device, hello solution removes hello device entry from identity registry and then deletes hello device twin.</span></span> <span data-ttu-id="075be-169">Hallo oplossing verwijdert informatie gerelateerde toohello apparaat ook uit Hallo Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="075be-169">hello solution also removes information related toohello device from hello Cosmos DB database.</span></span> <span data-ttu-id="075be-170">Voordat u een apparaat verwijdert kunt, moet u deze uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="075be-170">Before you can remove a device, you must disable it.</span></span>

![Apparaat verwijderen][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="075be-172">Apparaat informatie berichtverwerking</span><span class="sxs-lookup"><span data-stu-id="075be-172">Device information message processing</span></span>

<span data-ttu-id="075be-173">Berichten met apparaatgegevens verzonden door een apparaat zijn telemetrieberichten.</span><span class="sxs-lookup"><span data-stu-id="075be-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="075be-174">Berichten met apparaatgegevens omvatten een apparaat kan reageren op Hallo-opdrachten en eventuele opdrachtgeschiedenis.</span><span class="sxs-lookup"><span data-stu-id="075be-174">Device information messages include hello commands a device can respond to, and any command history.</span></span> <span data-ttu-id="075be-175">IoT-Hub zelf heeft geen informatie over Hallo metagegevens in het informatiebericht van een apparaat en processen Hallo-bericht in Hallo dezelfde manier als alle apparaat-naar-cloud-berichten worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="075be-175">IoT Hub itself has no knowledge of hello metadata contained in a device information message and processes hello message in hello same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="075be-176">In het Hallo-oplossing, voor externe controle een [Azure Stream Analytics] [ lnk-stream-analytics] (ASA) taak Hallo-berichten uit IoT Hub kan lezen.</span><span class="sxs-lookup"><span data-stu-id="075be-176">In hello remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads hello messages from IoT Hub.</span></span> <span data-ttu-id="075be-177">Hallo **DeviceInfo** stream analytics-taak filters voor berichten met **'ObjectType': 'DeviceInfo'** en stuurt ze toohello **EventProcessorHost** host exemplaar dat wordt uitgevoerd in een web-taak.</span><span class="sxs-lookup"><span data-stu-id="075be-177">hello **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them toohello **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="075be-178">Logica in Hallo **EventProcessorHost** instantie Hallo apparaat-id toofind hello Cosmos DB record voor Hallo specifieke apparaat- en update Hallo record gebruikt.</span><span class="sxs-lookup"><span data-stu-id="075be-178">Logic in hello **EventProcessorHost** instance uses hello device id toofind hello Cosmos DB record for hello specific device and update hello record.</span></span>

> [!NOTE]
> <span data-ttu-id="075be-179">Een informatiebericht van het apparaat is een standaard apparaat-naar-cloud-bericht.</span><span class="sxs-lookup"><span data-stu-id="075be-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="075be-180">Hallo-oplossing wordt onderscheid gemaakt tussen berichten met apparaatgegevens en telemetrieberichten met behulp van de ASA-query's.</span><span class="sxs-lookup"><span data-stu-id="075be-180">hello solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="075be-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="075be-181">Next steps</span></span>

<span data-ttu-id="075be-182">Nu u klaar bent met het leren hoe u Hallo vooraf geconfigureerde oplossingen kunt aanpassen, vindt u enkele Hallo andere functies en mogelijkheden van Hallo vooraf geconfigureerde IoT Suite-oplossingen:</span><span class="sxs-lookup"><span data-stu-id="075be-182">Now you've finished learning how you can customize hello preconfigured solutions, you can explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="075be-183">[Overzicht van voorspeld onderhoud vooraf geconfigureerde oplossing][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="075be-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="075be-184">[Veelgestelde vragen over IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="075be-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="075be-185">[Beveiliging van de IoT van Hallo gemalen][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="075be-185">[IoT security from hello ground up][lnk-security-groundup]</span></span>

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

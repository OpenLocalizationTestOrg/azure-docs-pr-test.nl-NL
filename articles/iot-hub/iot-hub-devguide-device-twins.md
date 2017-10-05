---
title: Azure IoT Hub apparaat horende begrijpen | Microsoft Docs
description: Handleiding voor ontwikkelaars - gebruik apparaat horende status en configuratie van gegevens tussen IoT Hub en uw apparaten synchroniseren
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b316aa419d558547f90a914a22fb29935076de21
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="2e0f3-103">Begrijpen en gebruiken van apparaat horende in IoT-Hub</span><span class="sxs-lookup"><span data-stu-id="2e0f3-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="2e0f3-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2e0f3-104">Overview</span></span>
<span data-ttu-id="2e0f3-105">*Apparaat horende* zijn JSON-documenten die apparaatgegevens van status (metagegevens, configuraties en voorwaarden) opslaan.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="2e0f3-106">IoT Hub gebruikt een apparaatdubbel voor elk apparaat dat u verbindt met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-106">IoT Hub persists a device twin for each device that you connect to IoT Hub.</span></span> <span data-ttu-id="2e0f3-107">Dit artikel wordt beschreven:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-107">This article describes:</span></span>

* <span data-ttu-id="2e0f3-108">De structuur van het apparaat twin: *labels*, *gewenste* en *gerapporteerd eigenschappen*, en</span><span class="sxs-lookup"><span data-stu-id="2e0f3-108">The structure of the device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="2e0f3-109">De bewerkingen die apparaat-apps en back-ends op het apparaat horende kunnen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-109">The operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="2e0f3-110">Apparaat horende zijn momenteel alleen toegankelijk vanaf apparaten die verbinding maken met behulp van het protocol MQTT IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-110">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="2e0f3-111">Raadpleeg de [MQTT ondersteuning] [ lnk-devguide-mqtt] artikel voor instructies over het converteren van bestaande apparaattoepassing MQTT gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-111">Refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

### <a name="when-to-use"></a><span data-ttu-id="2e0f3-112">Wanneer gebruikt u dit?</span><span class="sxs-lookup"><span data-stu-id="2e0f3-112">When to use</span></span>
<span data-ttu-id="2e0f3-113">Apparaat horende te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-113">Use device twins to:</span></span>

* <span data-ttu-id="2e0f3-114">Apparaatspecifieke metagegevens niet opslaan in de cloud.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-114">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="2e0f3-115">Bijvoorbeeld, de implementatielocatie van een snoep-machine.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-115">For example, the deployment location of a vending machine.</span></span>
* <span data-ttu-id="2e0f3-116">Huidige status rapportgegevens zoals beschikbaar mogelijkheden en de voorwaarden van de app op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="2e0f3-117">Bijvoorbeeld, een apparaat is verbonden met uw IoT-hub over mobiel of Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-117">For example, a device is connected to your IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="2e0f3-118">De status van langlopende werkstromen tussen apparaattoepassing en back-endserver voor apps worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-118">Synchronize the state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="2e0f3-119">Wanneer de oplossing voor back-end geeft u de nieuwe firmwareversie voor het installeren en de apparaattoepassing rapporteert de verschillende stadia van het updateproces.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-119">For example, when the solution back end specifies the new firmware version to install, and the device app reports the various stages of the update process.</span></span>
* <span data-ttu-id="2e0f3-120">De metagegevens van apparaten, de configuratie of de status opvragen.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="2e0f3-121">Raadpleeg [apparaat-naar-cloud communicatie richtlijnen] [ lnk-d2c-guidance] voor instructies over het gebruik van de gerapporteerde eigenschappen, apparaat-naar-cloud-berichten of bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-121">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="2e0f3-122">Raadpleeg [Cloud-naar-apparaat communicatie richtlijnen] [ lnk-c2d-guidance] voor hulp bij het gebruik van eigenschappen van de gewenste rechtstreekse methoden of cloud-naar-apparaat-berichten.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-122">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="2e0f3-123">Apparaat horende</span><span class="sxs-lookup"><span data-stu-id="2e0f3-123">Device twins</span></span>
<span data-ttu-id="2e0f3-124">Apparaat horende apparaatgerelateerde gegevens opslaan die:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="2e0f3-125">Apparaat- en back-ends kunnen gebruiken om apparaat-voorwaarden en configuratie te synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-125">Device and back ends can use to synchronize device conditions and configuration.</span></span>
* <span data-ttu-id="2e0f3-126">De back-end oplossing kunt gebruiken voor query- en doel langlopende bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-126">The solution back end can use to query and target long-running operations.</span></span>

<span data-ttu-id="2e0f3-127">De levenscyclus van een apparaat-twin is gekoppeld aan de bijbehorende [apparaat-id][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="2e0f3-127">The lifecycle of a device twin is linked to the corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="2e0f3-128">Apparaat horende worden impliciet gemaakt en verwijderd wanneer een nieuw apparaat-id is gemaakt of verwijderd uit IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="2e0f3-129">Een apparaat-twin is een JSON-document met:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="2e0f3-130">**Labels**.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-130">**Tags**.</span></span> <span data-ttu-id="2e0f3-131">Een gedeelte van de JSON-document dat de back-end oplossing kunt lezen en schrijven naar.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-131">A section of the JSON document that the solution back end can read from and write to.</span></span> <span data-ttu-id="2e0f3-132">Labels zijn niet zichtbaar voor apparaat-apps.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-132">Tags are not visible to device apps.</span></span>
* <span data-ttu-id="2e0f3-133">**Eigenschappen van de gewenste**.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-133">**Desired properties**.</span></span> <span data-ttu-id="2e0f3-134">Gebruikt samen met de eigenschappen van de gerapporteerde synchroniseren apparaatconfiguratie of voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-134">Used along with reported properties to synchronize device configuration or conditions.</span></span> <span data-ttu-id="2e0f3-135">Gewenste eigenschappen kunnen alleen worden ingesteld door de oplossing terug einde en kunnen worden gelezen door de app voor het apparaat.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-135">Desired properties can only be set by the solution back end and can be read by the device app.</span></span> <span data-ttu-id="2e0f3-136">De apparaat-app kan ook worden gewaarschuwd in realtime van wijzigingen in de gewenste eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-136">The device app can also be notified in real time of changes in the desired properties.</span></span>
* <span data-ttu-id="2e0f3-137">**Eigenschappen gerapporteerd**.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-137">**Reported properties**.</span></span> <span data-ttu-id="2e0f3-138">Gebruikt samen met de gewenste eigenschappen voor het synchroniseren van apparaatconfiguratie of voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-138">Used along with desired properties to synchronize device configuration or conditions.</span></span> <span data-ttu-id="2e0f3-139">Eigenschappen van de gerapporteerde kunnen kan alleen worden ingesteld door de apparaat-app en worden gelezen en opgevraagd met de back-end oplossing.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-139">Reported properties can only be set by the device app and can be read and queried by the solution back end.</span></span>

<span data-ttu-id="2e0f3-140">De hoofdmap van het apparaat twin JSON-document bevat tevens de alleen-lezen eigenschappen van de bijbehorende apparaat-id opgeslagen in de [identiteitsregister][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="2e0f3-140">Additionally, the root of the device twin JSON document contains the read-only properties from the corresponding device identity stored in the [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="2e0f3-141">Het volgende voorbeeld ziet u een apparaat twin JSON-document:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-141">The following example shows a device twin JSON document:</span></span>

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

<span data-ttu-id="2e0f3-142">In het hoofdobject Systeemeigenschappen en containerobjecten voor `tags` en beide `reported` en `desired` eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-142">In the root object, are the system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="2e0f3-143">De `properties` container bevat sommige alleen-lezen-elementen (`$metadata`, `$etag`, en `$version`) dat wordt beschreven in de [twin Apparaatmetagegevens] [ lnk-twin-metadata] en [ Optimistische gelijktijdigheid] [ lnk-concurrency] secties.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-143">The `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in the [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="2e0f3-144">Voorbeeld van de gerapporteerde eigenschap</span><span class="sxs-lookup"><span data-stu-id="2e0f3-144">Reported property example</span></span>
<span data-ttu-id="2e0f3-145">In het vorige voorbeeld de apparaat-twin bevat een `batteryLevel` eigenschap die is gerapporteerd door de app voor het apparaat.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-145">In the previous example, the device twin contains a `batteryLevel` property that is reported by the device app.</span></span> <span data-ttu-id="2e0f3-146">Deze eigenschap kan doorzoeken en op apparaten die zijn gebaseerd op het niveau van de laatste gemelde batterij werkt.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-146">This property makes it possible to query and operate on devices based on the last reported battery level.</span></span> <span data-ttu-id="2e0f3-147">Andere voorbeelden zijn de apparaat-app apparaat rapportagemogelijkheden of opties voor netwerkconnectiviteit.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-147">Other examples include the device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="2e0f3-148">Eigenschappen van de gerapporteerde vereenvoudigen scenario's waarin de back-end van de oplossing is geïnteresseerd in de laatst bekende waarde van een eigenschap.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-148">Reported properties simplify scenarios where the solution back end is interested in the last known value of a property.</span></span> <span data-ttu-id="2e0f3-149">Gebruik [apparaat-naar-cloudberichten] [ lnk-d2c] als de back-end van de oplossing moet verwerken van telemetriegegevens in de vorm van reeksen voorzien van een tijdstempel gebeurtenissen, zoals een tijdreeks.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-149">Use [device-to-cloud messages][lnk-d2c] if the solution back end needs to process device telemetry in the form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="2e0f3-150">Voorbeeld van de gewenste eigenschap</span><span class="sxs-lookup"><span data-stu-id="2e0f3-150">Desired property example</span></span>
<span data-ttu-id="2e0f3-151">In het vorige voorbeeld de `telemetryConfig` apparaat twin gewenst en gemelde eigenschappen worden gebruikt door de back-end van de oplossing en de apparaat-app voor het synchroniseren van de telemetrie-configuratie voor dit apparaat.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-151">In the previous example, the `telemetryConfig` device twin desired and reported properties are used by the solution back end and the device app to synchronize the telemetry configuration for this device.</span></span> <span data-ttu-id="2e0f3-152">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-152">For example:</span></span>

1. <span data-ttu-id="2e0f3-153">De back-end oplossing stelt de gewenste eigenschap met de waarde van de gewenste configuratie.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-153">The solution back end sets the desired property with the desired configuration value.</span></span> <span data-ttu-id="2e0f3-154">Dit is het gedeelte van het document met de gewenste eigenschap is ingesteld:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-154">Here is the portion of the document with the desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="2e0f3-155">De apparaat-app ontvangt een melding van de wijziging onmiddellijk als verbonden of op de eerste opnieuw verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-155">The device app is notified of the change immediately if connected, or at the first reconnect.</span></span> <span data-ttu-id="2e0f3-156">De apparaat-app vervolgens verslag uitbrengt de bijgewerkte configuratie (of een fout voorwaarde met behulp van de `status` eigenschap).</span><span class="sxs-lookup"><span data-stu-id="2e0f3-156">The device app then reports the updated configuration (or an error condition using the `status` property).</span></span> <span data-ttu-id="2e0f3-157">Dit is het gedeelte van de gerapporteerde eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-157">Here is the portion of the reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="2e0f3-158">De back-end oplossing kunt volgen de resultaten van de configuratie-bewerking op veel apparaten door [opvragen] [ lnk-query] horende apparaten.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-158">The solution back end can track the results of the configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="2e0f3-159">De voorgaande codefragmenten zijn voorbeelden, geoptimaliseerd voor de leesbaarheid van een manier voor het coderen van de configuratie van een apparaat en de status ervan.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-159">The preceding snippets are examples, optimized for readability, of one way to encode a device configuration and its status.</span></span> <span data-ttu-id="2e0f3-160">IoT Hub legt een specifieke schema voor de apparaat-twin gewenst en eigenschappen in de horende apparaten gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-160">IoT Hub does not impose a specific schema for the device twin desired and reported properties in the device twins.</span></span>
> 
> 

<span data-ttu-id="2e0f3-161">U kunt horende langlopende bewerkingen zoals firmware-updates te synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-161">You can use twins to synchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="2e0f3-162">Zie voor meer informatie over het gebruik van eigenschappen om te synchroniseren en een langdurige bewerking bijhouden op apparaten [gebruik gewenst eigenschappen voor het configureren van apparaten][lnk-twin-properties].</span><span class="sxs-lookup"><span data-stu-id="2e0f3-162">For more information on how to use properties to synchronize and track a long running operation across devices, see [Use desired properties to configure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="2e0f3-163">Back-end-bewerkingen</span><span class="sxs-lookup"><span data-stu-id="2e0f3-163">Back-end operations</span></span>
<span data-ttu-id="2e0f3-164">De back-end van de oplossing is van invloed op het apparaat twin met behulp van de volgende atomische bewerkingen, die toegankelijk is via HTTP:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-164">The solution back end operates on the device twin using the following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="2e0f3-165">**Apparaat-twin ophalen met id**. Deze bewerking retourneert het apparaat twin document, inclusief tags en gewenst, gerapporteerd, en Systeemeigenschappen.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-165">**Retrieve device twin by id**. This operation returns the device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="2e0f3-166">**Gedeeltelijk bijwerken apparaat twin**.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-166">**Partially update device twin**.</span></span> <span data-ttu-id="2e0f3-167">Deze bewerking kunt de back-end oplossing gedeeltelijk de codes of de gewenste eigenschappen in een twin apparaat bijwerken.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-167">This operation enables the solution back end to partially update the tags or desired properties in a device twin.</span></span> <span data-ttu-id="2e0f3-168">De gedeeltelijke update wordt uitgedrukt als een JSON-document dat wordt toegevoegd of updates van een eigenschap.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-168">The partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="2e0f3-169">Eigenschappen ingesteld op `null` worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-169">Properties set to `null` are removed.</span></span> <span data-ttu-id="2e0f3-170">Het volgende voorbeeld wordt een nieuwe gewenste eigenschap met de waarde `{"newProperty": "newValue"}`, overschrijft de bestaande waarde van `existingProperty` met `"otherNewValue"`, en verwijdert u `otherOldProperty`.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-170">The following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites the existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="2e0f3-171">Er zijn geen andere wijzigingen zijn aangebracht aan de bestaande gewenste eigenschappen of labels:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-171">No other changes are made to existing desired properties or tags:</span></span>
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. <span data-ttu-id="2e0f3-172">**Gewenste eigenschappen vervangen**.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-172">**Replace desired properties**.</span></span> <span data-ttu-id="2e0f3-173">Deze bewerking kunt u de back-end oplossing voor het volledig overschrijven alle bestaande gewenste eigenschappen en vervangen door een nieuwe JSON-document voor `properties/desired`.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-173">This operation enables the solution back end to completely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="2e0f3-174">**Vervang labels**.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-174">**Replace tags**.</span></span> <span data-ttu-id="2e0f3-175">Deze bewerking kunt u de back-end oplossing voor het volledig overschrijven alle bestaande tags en vervangen door een nieuwe JSON-document voor `tags`.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-175">This operation enables the solution back end to completely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="2e0f3-176">**Dubbele meldingen ontvangen**.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-176">**Receive twin notifications**.</span></span> <span data-ttu-id="2e0f3-177">Deze bewerking kunt de back-end oplossing wilt worden gewaarschuwd als de twin is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-177">This operation allows the solution back end to be notified when the twin is modified.</span></span> <span data-ttu-id="2e0f3-178">Om dit te doen, moet uw IoT-oplossing het maken van een route en stelt u de gegevensbron op *twinChangeEvents*.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-178">To do so, your IoT solution needs to create a route and to set the Data Source equal to *twinChangeEvents*.</span></span> <span data-ttu-id="2e0f3-179">Standaard geen twin meldingen worden verzonden, dat wil zeggen, geen dergelijke routes vooraf bestaan.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="2e0f3-180">Als de wijzigingssnelheid te hoog is, of om andere redenen, zoals interne fouten, kan de IoT-Hub slechts één melding waarin alle wijzigingen verzenden.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-180">If the rate of change is too high, or for other reasons, such as internal failures, the IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="2e0f3-181">Dus als uw toepassing moet betrouwbare voor controle en logboekregistratie van alle tussenliggende statussen, nog steeds aanbevolen wordt dat u D2C berichten.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="2e0f3-182">Het meldingsbericht twin bevat eigenschappen en hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-182">The twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="2e0f3-183">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="2e0f3-183">Properties</span></span>

    | <span data-ttu-id="2e0f3-184">Naam</span><span class="sxs-lookup"><span data-stu-id="2e0f3-184">Name</span></span> | <span data-ttu-id="2e0f3-185">Waarde</span><span class="sxs-lookup"><span data-stu-id="2e0f3-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="2e0f3-186">$content-type</span><span class="sxs-lookup"><span data-stu-id="2e0f3-186">$content-type</span></span> | <span data-ttu-id="2e0f3-187">application/json</span><span class="sxs-lookup"><span data-stu-id="2e0f3-187">application/json</span></span> |
    <span data-ttu-id="2e0f3-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="2e0f3-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="2e0f3-189">Tijd waarop de melding is verzonden</span><span class="sxs-lookup"><span data-stu-id="2e0f3-189">Time when the notification was sent</span></span> |
    <span data-ttu-id="2e0f3-190">$iothub-bericht-bron</span><span class="sxs-lookup"><span data-stu-id="2e0f3-190">$iothub-message-source</span></span> | <span data-ttu-id="2e0f3-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="2e0f3-191">twinChangeEvents</span></span> |
    <span data-ttu-id="2e0f3-192">$content-codering</span><span class="sxs-lookup"><span data-stu-id="2e0f3-192">$content-encoding</span></span> | <span data-ttu-id="2e0f3-193">UTF-8</span><span class="sxs-lookup"><span data-stu-id="2e0f3-193">utf-8</span></span> |
    <span data-ttu-id="2e0f3-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="2e0f3-194">deviceId</span></span> | <span data-ttu-id="2e0f3-195">Id van het apparaat</span><span class="sxs-lookup"><span data-stu-id="2e0f3-195">Id of the device</span></span> |
    <span data-ttu-id="2e0f3-196">hubName</span><span class="sxs-lookup"><span data-stu-id="2e0f3-196">hubName</span></span> | <span data-ttu-id="2e0f3-197">Naam van de IoT-Hub</span><span class="sxs-lookup"><span data-stu-id="2e0f3-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="2e0f3-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="2e0f3-198">operationTimestamp</span></span> | <span data-ttu-id="2e0f3-199">[ISO8601] tijdstempel van bewerking</span><span class="sxs-lookup"><span data-stu-id="2e0f3-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="2e0f3-200">bericht-iothub-schema</span><span class="sxs-lookup"><span data-stu-id="2e0f3-200">iothub-message-schema</span></span> | <span data-ttu-id="2e0f3-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="2e0f3-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="2e0f3-202">opType</span><span class="sxs-lookup"><span data-stu-id="2e0f3-202">opType</span></span> | <span data-ttu-id="2e0f3-203">'replaceTwin' of 'updateTwin'</span><span class="sxs-lookup"><span data-stu-id="2e0f3-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="2e0f3-204">Bericht Systeemeigenschappen worden voorafgegaan door de `'$'` symbool.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-204">Message system properties are prefixed with the `'$'` symbol.</span></span>

    - <span data-ttu-id="2e0f3-205">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="2e0f3-205">Body</span></span>
        
    <span data-ttu-id="2e0f3-206">Deze sectie bevat alle twin wijzigingen in een JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-206">This section includes all the twin changes in a JSON format.</span></span> <span data-ttu-id="2e0f3-207">Met het verschil dat deze alle twin secties kan bevatten, wordt dezelfde indeling als een patch: labels, properties.reported properties.desired en dat deze de elementen '$metadata bevat'.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-207">It uses the same format as a patch, with the difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains the “$metadata” elements.</span></span> <span data-ttu-id="2e0f3-208">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-208">For example,</span></span>
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

<span data-ttu-id="2e0f3-209">Ondersteuning voor alle voorgaande bewerkingen [optimistische gelijktijdigheid] [ lnk-concurrency] en vereisen de **ServiceConnect** toestemming hebben, zoals gedefinieerd in de [beveiliging] [ lnk-security] artikel.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-209">All the preceding operations support [Optimistic concurrency][lnk-concurrency] and require the **ServiceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="2e0f3-210">Naast deze bewerkingen kan de back-end oplossing:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-210">In addition to these operations, the solution back end can:</span></span>

* <span data-ttu-id="2e0f3-211">De apparaat-horende met behulp van de SQL-achtige query [IoT Hub-querytaal][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="2e0f3-211">Query the device twins using the SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="2e0f3-212">Bewerkingen uitvoeren op grote gegevenssets apparaat horende met [taken][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="2e0f3-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="2e0f3-213">Apparaatbewerkingen</span><span class="sxs-lookup"><span data-stu-id="2e0f3-213">Device operations</span></span>
<span data-ttu-id="2e0f3-214">De app voor het apparaat is van invloed op het apparaat twin met behulp van de volgende atomische bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-214">The device app operates on the device twin using the following atomic operations:</span></span>

1. <span data-ttu-id="2e0f3-215">**Ophalen van apparaat twin**.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-215">**Retrieve device twin**.</span></span> <span data-ttu-id="2e0f3-216">Deze bewerking wordt het apparaat twin-document (inclusief tags en gewenste, gerapporteerd en Systeemeigenschappen) voor de momenteel verbonden apparaat.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-216">This operation returns the device twin document (including tags and desired, reported and system properties) for the currently connected device.</span></span>
2. <span data-ttu-id="2e0f3-217">**De eigenschappen van de gerapporteerde gedeeltelijk bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-217">**Partially update reported properties**.</span></span> <span data-ttu-id="2e0f3-218">Deze bewerking kunt het gedeeltelijke bijwerken van de gerapporteerde eigenschappen van de momenteel verbonden apparaat.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-218">This operation enables the partial update of the reported properties of the currently connected device.</span></span> <span data-ttu-id="2e0f3-219">Deze bewerking wordt de dezelfde JSON-update-indeling dat de oplossing voor back-end gebruikt voor een gedeeltelijke update van de gewenste eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-219">This operation uses the same JSON update format that the solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="2e0f3-220">**Houd rekening met de eigenschappen van de gewenste**.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-220">**Observe desired properties**.</span></span> <span data-ttu-id="2e0f3-221">De momenteel verbonden apparaat kunt van updates voor de gewenste eigenschappen informeren wanneer ze zich voordoen.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-221">The currently connected device can choose to be notified of updates to the desired properties when they happen.</span></span> <span data-ttu-id="2e0f3-222">Het apparaat ontvangt de dezelfde vorm van update (gedeeltelijke of volledige vervanging) uitgevoerd door de back-end oplossing.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-222">The device receives the same form of update (partial or full replacement) executed by the solution back end.</span></span>

<span data-ttu-id="2e0f3-223">De voorgaande bewerkingen vereist de **DeviceConnect** toestemming hebben, zoals gedefinieerd in de [beveiliging] [ lnk-security] artikel.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-223">All the preceding operations require the **DeviceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="2e0f3-224">De [apparaat Azure IoT SDK's] [ lnk-sdks] gemakkelijk te gebruiken van de voorgaande bewerkingen uit veel talen en platforms.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-224">The [Azure IoT device SDKs][lnk-sdks] make it easy to use the preceding operations from many languages and platforms.</span></span> <span data-ttu-id="2e0f3-225">Meer informatie over de details van IoT Hub primitieven voor synchronisatie van de gewenste eigenschappen vindt u in [apparaat opnieuw verbinden stroom][lnk-reconnection].</span><span class="sxs-lookup"><span data-stu-id="2e0f3-225">More information on the details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="2e0f3-226">Apparaat horende zijn momenteel alleen toegankelijk vanaf apparaten die verbinding maken met behulp van het protocol MQTT IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-226">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="2e0f3-227">De onderwerpen waarnaar wordt verwezen:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-227">Reference topics:</span></span>
<span data-ttu-id="2e0f3-228">De volgende onderwerpen met naslaginformatie bieden u meer informatie over het beheren van toegang tot uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-228">The following reference topics provide you with more information about controlling access to your IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="2e0f3-229">Labels en eigenschappen indeling</span><span class="sxs-lookup"><span data-stu-id="2e0f3-229">Tags and properties format</span></span>
<span data-ttu-id="2e0f3-230">Labels, gewenste en gerapporteerde eigenschappen zijn JSON-objecten met de volgende beperkingen:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-230">Tags, desired, and reported properties are JSON objects with the following restrictions:</span></span>

* <span data-ttu-id="2e0f3-231">Alle sleutels in JSON-objecten zijn hoofdlettergevoelig 64 bytes UTF-8, UNICODE-tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="2e0f3-232">Toegestane tekens Unicode-tekens (segmenten C0 en C1), uitsluiten en `'.'`, `' '`, en `'$'`.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="2e0f3-233">Alle waarden in de JSON-objecten van de volgende JSON-typen kunnen zijn: boolean, getal, string, object.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-233">All values in JSON objects can be of the following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="2e0f3-234">Matrices zijn niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="2e0f3-235">Alle JSON-objecten in tags, gewenste en gerapporteerde eigenschappen kunnen een maximale diepte van 5 hebben.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="2e0f3-236">De volgende object is bijvoorbeeld geldig:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-236">For instance, the following object is valid:</span></span>

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* <span data-ttu-id="2e0f3-237">Alle tekenreekswaarden mag hoogstens 512 bytes lang.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="2e0f3-238">De grootte van de apparaat-twin</span><span class="sxs-lookup"><span data-stu-id="2e0f3-238">Device twin size</span></span>
<span data-ttu-id="2e0f3-239">IoT Hub worden afgedwongen voor een beperking van 8KB grootte van de waarden van `tags`, `properties/desired`, en `properties/reported`, met uitzondering van alleen-lezen-elementen.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-239">IoT Hub enforces an 8KB size limitation on the values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="2e0f3-240">De grootte wordt berekend door het tellen van alle tekens, met uitzondering van UNICODE-tekens (segmenten C0 en C1) en ruimte beheren `' '` wanneer deze buiten een tekenreeksconstante wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-240">The size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="2e0f3-241">IoT Hub worden alle bewerkingen die u wilt de grootte van deze documenten boven de limiet verhogen geweigerd met een fout.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-241">IoT Hub rejects with an error all operations that would increase the size of those documents above the limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="2e0f3-242">Metagegevens van apparaten twin</span><span class="sxs-lookup"><span data-stu-id="2e0f3-242">Device twin metadata</span></span>
<span data-ttu-id="2e0f3-243">IoT Hub onderhoudt het tijdstempel van de laatste update voor elk JSON-object in de apparaat-twin gewenst en eigenschappen gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-243">IoT Hub maintains the timestamp of the last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="2e0f3-244">De tijdstempels in UTC en gecodeerd in de [ISO8601] indeling `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-244">The timestamps are in UTC and encoded in the [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="2e0f3-245">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-245">For example:</span></span>

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

<span data-ttu-id="2e0f3-246">Deze informatie wordt opgeslagen op elk niveau (niet alleen de knooppunten van de JSON-structuur)-updates die objectsleutels verwijderen moet worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-246">This information is kept at every level (not just the leaves of the JSON structure) to preserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="2e0f3-247">Optimistische gelijktijdigheid</span><span class="sxs-lookup"><span data-stu-id="2e0f3-247">Optimistic concurrency</span></span>
<span data-ttu-id="2e0f3-248">Labels, gewenst en eigenschappen van alle ondersteuning optimistische gelijktijdigheid gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="2e0f3-249">Labels hebben een ETag conform [RFC7232], die staat voor de JSON-weergave van de tag.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-249">Tags have an ETag, as per [RFC7232], that represents the tag's JSON representation.</span></span> <span data-ttu-id="2e0f3-250">U kunt ETags in voorwaardelijke bijwerkbewerkingen van de back-end oplossing gebruiken om consistentie te garanderen.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-250">You can use ETags in conditional update operations from the solution back end to ensure consistency.</span></span>

<span data-ttu-id="2e0f3-251">Apparaat twin gewenst en gerapporteerde eigenschappen zijn niet ETags, maar hebben een `$version` is gegarandeerd incrementele waarde.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed to be incremental.</span></span> <span data-ttu-id="2e0f3-252">Op dezelfde manier naar een ETag, de versie kan worden gebruikt door de partij bijwerken om af te dwingen van de consistentie van updates.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-252">Similarly to an ETag, the version can be used by the updating party to enforce consistency of updates.</span></span> <span data-ttu-id="2e0f3-253">Bijvoorbeeld, een apparaat-app voor een eigenschap gemeld of de back-end oplossing voor een gewenste eigenschap.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-253">For example, a device app for a reported property or the solution back end for a desired property.</span></span>

<span data-ttu-id="2e0f3-254">Versies zijn ook handig wanneer een observing agent (zoals de apparaat-app de gewenste eigenschappen observeren) op elkaar races tussen het resultaat van een bewerking ophalen en een melding van updates afstemmen moet.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-254">Versions are also useful when an observing agent (such as the device app observing the desired properties) must reconcile races between the result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="2e0f3-255">De sectie [apparaat opnieuw verbinden stroom] [ lnk-reconnection] vindt u meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-255">The section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="2e0f3-256">Opnieuw verbinden stroom van apparaat</span><span class="sxs-lookup"><span data-stu-id="2e0f3-256">Device reconnection flow</span></span>
<span data-ttu-id="2e0f3-257">IoT Hub behoudt updatemeldingen gewenste eigenschappen voor niet-verbonden apparaten niet.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="2e0f3-258">Betekent dit dat het document volledige gewenste eigenschappen naast abonneren op updatemeldingen moet worden opgehaald door een apparaat dat verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-258">It follows that a device that is connecting must retrieve the full desired properties document, in addition to subscribing for update notifications.</span></span> <span data-ttu-id="2e0f3-259">Gezien de mogelijkheid van races tussen updatemeldingen en volledige ophalen, ervoor de volgende stroom wordt gezorgd</span><span class="sxs-lookup"><span data-stu-id="2e0f3-259">Given the possibility of races between update notifications and full retrieval, the following flow must be ensured:</span></span>

1. <span data-ttu-id="2e0f3-260">App voor het apparaat verbindt met een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-260">Device app connects to an IoT hub.</span></span>
2. <span data-ttu-id="2e0f3-261">App voor het apparaat is lid voor de gewenste eigenschappen updatemeldingen.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="2e0f3-262">Apparaattoepassing haalt het volledige document van de gewenste eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-262">Device app retrieves the full document for desired properties.</span></span>

<span data-ttu-id="2e0f3-263">De apparaat-app kunt negeren alle meldingen met `$version` of minder zijn dan de versie van het volledige document opgehaald.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-263">The device app can ignore all notifications with `$version` less or equal than the version of the full retrieved document.</span></span> <span data-ttu-id="2e0f3-264">Deze aanpak is mogelijk omdat IoT Hub wordt gegarandeerd dat versies altijd verhogen.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="2e0f3-265">Deze logica wordt al geïmplementeerd de [apparaat Azure IoT SDK's][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="2e0f3-265">This logic is already implemented in the [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="2e0f3-266">Deze beschrijving is handig als de app voor het apparaat een apparaat met Azure IoT SDK's gebruiken kan en de protocollen MQTT-interface moet rechtstreeks programma.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-266">This description is useful only if the device app cannot use any of Azure IoT device SDKs and must program the MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="2e0f3-267">Aanvullende referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="2e0f3-267">Additional reference material</span></span>
<span data-ttu-id="2e0f3-268">Er zijn andere onderwerpen waarnaar wordt verwezen in de IoT Hub developer guide:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-268">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="2e0f3-269">De [IoT-hubeindpunten] [ lnk-endpoints] artikel beschrijft de verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-269">The [IoT Hub endpoints][lnk-endpoints] article describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="2e0f3-270">De [bandbreedtebeperking en quota's] [ lnk-quotas] artikel beschrijft de quota die betrekking hebben op de IoT Hub-service en het gedrag bandbreedteregeling kunt verwachten wanneer u de service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-270">The [Throttling and quotas][lnk-quotas] article describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="2e0f3-271">De [apparaat en de service Azure IoT-SDK's] [ lnk-sdks] artikel bevat een overzicht van de verschillende SDK's kunt u bij het ontwikkelen van apps voor het apparaat en de service die communiceren met IoT Hub-taal.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-271">The [Azure IoT device and service SDKs][lnk-sdks] article lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="2e0f3-272">De [querytaal IoT Hub voor apparaat horende, taken en berichtroutering] [ lnk-query] artikel beschrijft de IoT Hub-querytaal kunt u gegevens ophalen uit IoT Hub over uw apparaat horende en taken.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-272">The [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="2e0f3-273">De [IoT Hub MQTT ondersteuning] [ lnk-devguide-mqtt] artikel vindt u meer informatie over ondersteuning voor het protocol MQTT IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-273">The [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e0f3-274">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e0f3-274">Next steps</span></span>
<span data-ttu-id="2e0f3-275">Nu hebt u geleerd over horende apparaat, hebt u mogelijk geïnteresseerd in de volgende onderwerpen van IoT Hub developer guide:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-275">Now you have learned about device twins, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="2e0f3-276">[Een directe methode aangeroepen voor een apparaat][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="2e0f3-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="2e0f3-277">[Taken plannen op meerdere apparaten][lnk-jobs]</span><span class="sxs-lookup"><span data-stu-id="2e0f3-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="2e0f3-278">Als u wilt uitproberen enkele concepten die in dit artikel wordt beschreven, kunt u mogelijk geïnteresseerd in de volgende zelfstudies met IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-278">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="2e0f3-279">[Het gebruik van de apparaat-twin][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="2e0f3-279">[How to use the device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="2e0f3-280">[Het gebruik van twin apparaateigenschappen][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="2e0f3-280">[How to use device twin properties][lnk-twin-properties]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png

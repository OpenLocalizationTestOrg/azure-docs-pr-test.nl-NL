---
title: aaaUnderstand Azure IoT Hub apparaat horende | Microsoft Docs
description: Handleiding voor ontwikkelaars - apparaat gebruiken horende toosynchronize status en de configuratie van gegevens tussen IoT Hub en uw apparaten
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
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="a51d2-103">Begrijpen en gebruiken van apparaat horende in IoT-Hub</span><span class="sxs-lookup"><span data-stu-id="a51d2-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="a51d2-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="a51d2-104">Overview</span></span>
<span data-ttu-id="a51d2-105">*Apparaat horende* zijn JSON-documenten die apparaatgegevens van status (metagegevens, configuraties en voorwaarden) opslaan.</span><span class="sxs-lookup"><span data-stu-id="a51d2-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="a51d2-106">IoT Hub persistente een apparaat twin voor elk apparaat dat u verbinding tooIoT Hub maakt.</span><span class="sxs-lookup"><span data-stu-id="a51d2-106">IoT Hub persists a device twin for each device that you connect tooIoT Hub.</span></span> <span data-ttu-id="a51d2-107">Dit artikel wordt beschreven:</span><span class="sxs-lookup"><span data-stu-id="a51d2-107">This article describes:</span></span>

* <span data-ttu-id="a51d2-108">structuur van Hallo apparaat twin Hallo: *labels*, *gewenste* en *gerapporteerd eigenschappen*, en</span><span class="sxs-lookup"><span data-stu-id="a51d2-108">hello structure of hello device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="a51d2-109">Hallo-bewerkingen die apparaat-apps en back-ends voor horende apparaten kunnen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a51d2-109">hello operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="a51d2-110">Apparaat horende zijn momenteel alleen toegankelijk vanaf apparaten die verbinding tooIoT Hub maken met Hallo MQTT-protocol.</span><span class="sxs-lookup"><span data-stu-id="a51d2-110">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="a51d2-111">Raadpleeg toohello [MQTT ondersteuning] [ lnk-devguide-mqtt] artikel voor instructies over het tooconvert bestaande apparaat app toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="a51d2-111">Refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

### <a name="when-toouse"></a><span data-ttu-id="a51d2-112">Wanneer toouse</span><span class="sxs-lookup"><span data-stu-id="a51d2-112">When toouse</span></span>
<span data-ttu-id="a51d2-113">Apparaat horende te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a51d2-113">Use device twins to:</span></span>

* <span data-ttu-id="a51d2-114">Apparaatspecifieke metagegevens opslaan in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="a51d2-114">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="a51d2-115">Bijvoorbeeld, de implementatielocatie van de van een machine snoep Hallo.</span><span class="sxs-lookup"><span data-stu-id="a51d2-115">For example, hello deployment location of a vending machine.</span></span>
* <span data-ttu-id="a51d2-116">Huidige status rapportgegevens zoals beschikbaar mogelijkheden en de voorwaarden van de app op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="a51d2-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="a51d2-117">Bijvoorbeeld, een apparaat is verbonden tooyour IoT-hub over mobiel of Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="a51d2-117">For example, a device is connected tooyour IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="a51d2-118">Hallo-status van langlopende werkstromen tussen apparaattoepassing en back-endserver voor apps worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="a51d2-118">Synchronize hello state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="a51d2-119">Wanneer een back-Hallo oplossing einde geeft aan nieuwe firmware versie tooinstall Hallo en Hallo apparaat app rapporten verschillende fasen van het updateproces Hallo Hallo is.</span><span class="sxs-lookup"><span data-stu-id="a51d2-119">For example, when hello solution back end specifies hello new firmware version tooinstall, and hello device app reports hello various stages of hello update process.</span></span>
* <span data-ttu-id="a51d2-120">De metagegevens van apparaten, de configuratie of de status opvragen.</span><span class="sxs-lookup"><span data-stu-id="a51d2-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="a51d2-121">Raadpleeg te[apparaat-naar-cloud communicatie richtlijnen] [ lnk-d2c-guidance] voor instructies over het gebruik van de gerapporteerde eigenschappen, apparaat-naar-cloud-berichten of bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="a51d2-121">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="a51d2-122">Raadpleeg te[Cloud-naar-apparaat communicatie richtlijnen] [ lnk-c2d-guidance] voor hulp bij het gebruik van eigenschappen van de gewenste rechtstreekse methoden of cloud-naar-apparaat-berichten.</span><span class="sxs-lookup"><span data-stu-id="a51d2-122">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="a51d2-123">Apparaat horende</span><span class="sxs-lookup"><span data-stu-id="a51d2-123">Device twins</span></span>
<span data-ttu-id="a51d2-124">Apparaat horende apparaatgerelateerde gegevens opslaan die:</span><span class="sxs-lookup"><span data-stu-id="a51d2-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="a51d2-125">Apparaat- en back-ends kunnen toosynchronize apparaat voorwaarden en configuratie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a51d2-125">Device and back ends can use toosynchronize device conditions and configuration.</span></span>
* <span data-ttu-id="a51d2-126">Hallo back-end oplossing kunt tooquery gebruiken en langlopende bewerkingen zijn gericht.</span><span class="sxs-lookup"><span data-stu-id="a51d2-126">hello solution back end can use tooquery and target long-running operations.</span></span>

<span data-ttu-id="a51d2-127">Hallo levenscyclus van een apparaat-twin is gekoppeld toohello overeenkomt [apparaat-id][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="a51d2-127">hello lifecycle of a device twin is linked toohello corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="a51d2-128">Apparaat horende worden impliciet gemaakt en verwijderd wanneer een nieuw apparaat-id is gemaakt of verwijderd uit IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a51d2-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="a51d2-129">Een apparaat-twin is een JSON-document met:</span><span class="sxs-lookup"><span data-stu-id="a51d2-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="a51d2-130">**Labels**.</span><span class="sxs-lookup"><span data-stu-id="a51d2-130">**Tags**.</span></span> <span data-ttu-id="a51d2-131">Een gedeelte van Hallo JSON-document dat back-end oplossing Hallo kunt lezen van en schrijven naar.</span><span class="sxs-lookup"><span data-stu-id="a51d2-131">A section of hello JSON document that hello solution back end can read from and write to.</span></span> <span data-ttu-id="a51d2-132">Labels zijn niet zichtbaar toodevice apps.</span><span class="sxs-lookup"><span data-stu-id="a51d2-132">Tags are not visible toodevice apps.</span></span>
* <span data-ttu-id="a51d2-133">**Eigenschappen van de gewenste**.</span><span class="sxs-lookup"><span data-stu-id="a51d2-133">**Desired properties**.</span></span> <span data-ttu-id="a51d2-134">Gebruikt samen met de eigenschappen van de gerapporteerde toosynchronize apparaatconfiguratie of voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="a51d2-134">Used along with reported properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="a51d2-135">Gewenste eigenschappen kunnen alleen worden ingesteld door Hallo oplossing terug einde en kunnen worden gelezen door Hallo apparaattoepassing.</span><span class="sxs-lookup"><span data-stu-id="a51d2-135">Desired properties can only be set by hello solution back end and can be read by hello device app.</span></span> <span data-ttu-id="a51d2-136">Hallo apparaattoepassing kan ook worden gewaarschuwd in realtime van wijzigingen in de eigenschappen van Hallo gewenst.</span><span class="sxs-lookup"><span data-stu-id="a51d2-136">hello device app can also be notified in real time of changes in hello desired properties.</span></span>
* <span data-ttu-id="a51d2-137">**Eigenschappen gerapporteerd**.</span><span class="sxs-lookup"><span data-stu-id="a51d2-137">**Reported properties**.</span></span> <span data-ttu-id="a51d2-138">Gebruikt samen met de gewenste eigenschappen toosynchronize apparaatconfiguratie of voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="a51d2-138">Used along with desired properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="a51d2-139">Eigenschappen van de gerapporteerde kunnen Hallo apparaattoepassing kan alleen worden ingesteld en worden gelezen en opgevraagd door Hallo back-end oplossing.</span><span class="sxs-lookup"><span data-stu-id="a51d2-139">Reported properties can only be set by hello device app and can be read and queried by hello solution back end.</span></span>

<span data-ttu-id="a51d2-140">Hallo-hoofdmap van Hallo apparaat twin JSON-document bevat tevens Hallo alleen-lezen eigenschappen van Hallo bijbehorende apparaat-id opgeslagen in Hallo [identiteitsregister][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="a51d2-140">Additionally, hello root of hello device twin JSON document contains hello read-only properties from hello corresponding device identity stored in hello [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="a51d2-141">Hallo volgende voorbeeld ziet u een apparaat twin JSON-document:</span><span class="sxs-lookup"><span data-stu-id="a51d2-141">hello following example shows a device twin JSON document:</span></span>

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

<span data-ttu-id="a51d2-142">In het hoofdobject hello, Hallo Systeemeigenschappen en containerobjecten voor `tags` en beide `reported` en `desired` eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="a51d2-142">In hello root object, are hello system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="a51d2-143">Hallo `properties` container bevat sommige alleen-lezen-elementen (`$metadata`, `$etag`, en `$version`) dat wordt beschreven in Hallo [twin Apparaatmetagegevens] [ lnk-twin-metadata] en [ Optimistische gelijktijdigheid] [ lnk-concurrency] secties.</span><span class="sxs-lookup"><span data-stu-id="a51d2-143">hello `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in hello [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="a51d2-144">Voorbeeld van de gerapporteerde eigenschap</span><span class="sxs-lookup"><span data-stu-id="a51d2-144">Reported property example</span></span>
<span data-ttu-id="a51d2-145">In het vorige voorbeeld Hallo Hallo apparaat twin bevat een `batteryLevel` eigenschap die is gerapporteerd door Hallo apparaattoepassing.</span><span class="sxs-lookup"><span data-stu-id="a51d2-145">In hello previous example, hello device twin contains a `batteryLevel` property that is reported by hello device app.</span></span> <span data-ttu-id="a51d2-146">Deze eigenschap maakt het mogelijk tooquery en werkt op apparaten die zijn gebaseerd op Hallo laatste gemelde accuniveau.</span><span class="sxs-lookup"><span data-stu-id="a51d2-146">This property makes it possible tooquery and operate on devices based on hello last reported battery level.</span></span> <span data-ttu-id="a51d2-147">Andere voorbeelden zijn Hallo apparaat app apparaat rapportagemogelijkheden of opties voor netwerkconnectiviteit.</span><span class="sxs-lookup"><span data-stu-id="a51d2-147">Other examples include hello device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="a51d2-148">Eigenschappen van de gerapporteerde vereenvoudigen scenario's waarbij Hallo back-end oplossing is geïnteresseerd in de laatste bekende waarde van een eigenschap Hallo.</span><span class="sxs-lookup"><span data-stu-id="a51d2-148">Reported properties simplify scenarios where hello solution back end is interested in hello last known value of a property.</span></span> <span data-ttu-id="a51d2-149">Gebruik [apparaat-naar-cloudberichten] [ lnk-d2c] als Hallo back-end oplossing tooprocess apparaattelemetrie in de vorm Hallo van reeksen voorzien van een tijdstempel gebeurtenissen, zoals een tijdreeks moet.</span><span class="sxs-lookup"><span data-stu-id="a51d2-149">Use [device-to-cloud messages][lnk-d2c] if hello solution back end needs tooprocess device telemetry in hello form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="a51d2-150">Voorbeeld van de gewenste eigenschap</span><span class="sxs-lookup"><span data-stu-id="a51d2-150">Desired property example</span></span>
<span data-ttu-id="a51d2-151">In het vorige voorbeeld Hallo Hallo `telemetryConfig` apparaat twin gewenst en gerapporteerde eigenschappen worden gebruikt door Hallo back-end oplossing en Hallo app toosynchronize Hallo telemetrie apparaatconfiguratie voor dit apparaat.</span><span class="sxs-lookup"><span data-stu-id="a51d2-151">In hello previous example, hello `telemetryConfig` device twin desired and reported properties are used by hello solution back end and hello device app toosynchronize hello telemetry configuration for this device.</span></span> <span data-ttu-id="a51d2-152">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a51d2-152">For example:</span></span>

1. <span data-ttu-id="a51d2-153">Hallo back-end oplossing Hallo gewenst eigenschap met de Hallo desired configuratiewaarde ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a51d2-153">hello solution back end sets hello desired property with hello desired configuration value.</span></span> <span data-ttu-id="a51d2-154">Hier volgt Hallo-gedeelte van Hallo-document met Hallo gewenst eigenschap is ingesteld:</span><span class="sxs-lookup"><span data-stu-id="a51d2-154">Here is hello portion of hello document with hello desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="a51d2-155">Hallo apparaattoepassing ontvangt een melding van Hallo wijziging onmiddellijk als op Hallo eerst verbinding of geen verbinding.</span><span class="sxs-lookup"><span data-stu-id="a51d2-155">hello device app is notified of hello change immediately if connected, or at hello first reconnect.</span></span> <span data-ttu-id="a51d2-156">Hallo apparaattoepassing vervolgens verslag uitbrengt Hallo bijgewerkt configuration (of een foutconditie Hallo met `status` eigenschap).</span><span class="sxs-lookup"><span data-stu-id="a51d2-156">hello device app then reports hello updated configuration (or an error condition using hello `status` property).</span></span> <span data-ttu-id="a51d2-157">Hier volgt Hallo gedeelte Hallo gerapporteerd eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="a51d2-157">Here is hello portion of hello reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="a51d2-158">Hallo back-end oplossing kunt bijhouden Hallo resultaten van de bewerking van de configuratie van Hallo op veel apparaten door [opvragen] [ lnk-query] horende apparaten.</span><span class="sxs-lookup"><span data-stu-id="a51d2-158">hello solution back end can track hello results of hello configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="a51d2-159">Hallo voorgaande codefragmenten zijn voorbeelden, geoptimaliseerd voor de leesbaarheid van eenrichtingssessie tooencode de configuratie van een apparaat en de status ervan.</span><span class="sxs-lookup"><span data-stu-id="a51d2-159">hello preceding snippets are examples, optimized for readability, of one way tooencode a device configuration and its status.</span></span> <span data-ttu-id="a51d2-160">IoT Hub afdwingen voor Hallo apparaat twin gewenst en eigenschappen in Hallo apparaat horende gerapporteerd niet met een specifiek schema.</span><span class="sxs-lookup"><span data-stu-id="a51d2-160">IoT Hub does not impose a specific schema for hello device twin desired and reported properties in hello device twins.</span></span>
> 
> 

<span data-ttu-id="a51d2-161">U kunt horende toosynchronize langlopende bewerkingen zoals firmware-updates.</span><span class="sxs-lookup"><span data-stu-id="a51d2-161">You can use twins toosynchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="a51d2-162">Voor meer informatie over hoe toouse eigenschappen toosynchronize en bijhouden een langdurige bewerking op apparaten, Zie [gebruik gewenst eigenschappen tooconfigure apparaten][lnk-twin-properties].</span><span class="sxs-lookup"><span data-stu-id="a51d2-162">For more information on how toouse properties toosynchronize and track a long running operation across devices, see [Use desired properties tooconfigure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="a51d2-163">Back-end-bewerkingen</span><span class="sxs-lookup"><span data-stu-id="a51d2-163">Back-end operations</span></span>
<span data-ttu-id="a51d2-164">Hallo back-end oplossing is van invloed op Hallo apparaat twin Hallo volgt atomic bewerkingen, die toegankelijk is via HTTP met:</span><span class="sxs-lookup"><span data-stu-id="a51d2-164">hello solution back end operates on hello device twin using hello following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="a51d2-165">**Apparaat-twin ophalen met id**. Deze bewerking retourneert Hallo apparaat twin document, inclusief tags en gewenst, gerapporteerd, en Systeemeigenschappen.</span><span class="sxs-lookup"><span data-stu-id="a51d2-165">**Retrieve device twin by id**. This operation returns hello device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="a51d2-166">**Gedeeltelijk bijwerken apparaat twin**.</span><span class="sxs-lookup"><span data-stu-id="a51d2-166">**Partially update device twin**.</span></span> <span data-ttu-id="a51d2-167">Deze bewerking kan Hallo oplossing voor back-end toopartially update Hallo tags of gewenste eigenschappen in een twin apparaat.</span><span class="sxs-lookup"><span data-stu-id="a51d2-167">This operation enables hello solution back end toopartially update hello tags or desired properties in a device twin.</span></span> <span data-ttu-id="a51d2-168">Hallo gedeeltelijke update wordt uitgedrukt als een JSON-document dat wordt toegevoegd of updates van een eigenschap.</span><span class="sxs-lookup"><span data-stu-id="a51d2-168">hello partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="a51d2-169">Eigenschappen instellen te`null` worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a51d2-169">Properties set too`null` are removed.</span></span> <span data-ttu-id="a51d2-170">Hallo volgende voorbeeld wordt een nieuwe gewenste eigenschap met de waarde `{"newProperty": "newValue"}`, overschrijft de bestaande waarde Hallo van `existingProperty` met `"otherNewValue"`, en verwijdert u `otherOldProperty`.</span><span class="sxs-lookup"><span data-stu-id="a51d2-170">hello following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites hello existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="a51d2-171">Er worden geen andere wijzigingen aangebracht tooexisting gewenst eigenschappen of labels:</span><span class="sxs-lookup"><span data-stu-id="a51d2-171">No other changes are made tooexisting desired properties or tags:</span></span>
   
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
3. <span data-ttu-id="a51d2-172">**Gewenste eigenschappen vervangen**.</span><span class="sxs-lookup"><span data-stu-id="a51d2-172">**Replace desired properties**.</span></span> <span data-ttu-id="a51d2-173">Deze bewerking kunt Hallo oplossing voor back-end toocompletely overschrijven alle bestaande gewenste eigenschappen en vervangen door een nieuwe JSON-document voor `properties/desired`.</span><span class="sxs-lookup"><span data-stu-id="a51d2-173">This operation enables hello solution back end toocompletely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="a51d2-174">**Vervang labels**.</span><span class="sxs-lookup"><span data-stu-id="a51d2-174">**Replace tags**.</span></span> <span data-ttu-id="a51d2-175">Deze bewerking kunt Hallo oplossing voor back-end toocompletely overschrijven alle bestaande codes en vervangen door een nieuwe JSON-document voor `tags`.</span><span class="sxs-lookup"><span data-stu-id="a51d2-175">This operation enables hello solution back end toocompletely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="a51d2-176">**Dubbele meldingen ontvangen**.</span><span class="sxs-lookup"><span data-stu-id="a51d2-176">**Receive twin notifications**.</span></span> <span data-ttu-id="a51d2-177">Deze bewerking kunt Hallo oplossing voor back-end toobe gewaarschuwd als Hallo twin is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="a51d2-177">This operation allows hello solution back end toobe notified when hello twin is modified.</span></span> <span data-ttu-id="a51d2-178">toodo, uw IoT-oplossing moet een route toocreate en tooset Hallo gegevensbron gelijk te*twinChangeEvents*.</span><span class="sxs-lookup"><span data-stu-id="a51d2-178">toodo so, your IoT solution needs toocreate a route and tooset hello Data Source equal too*twinChangeEvents*.</span></span> <span data-ttu-id="a51d2-179">Standaard geen twin meldingen worden verzonden, dat wil zeggen, geen dergelijke routes vooraf bestaan.</span><span class="sxs-lookup"><span data-stu-id="a51d2-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="a51d2-180">Als wijzigingsratio Hallo te hoog is of om andere redenen, zoals interne fouten Hallo IoT Hub slechts één melding waarin alle wijzigingen kan verzenden.</span><span class="sxs-lookup"><span data-stu-id="a51d2-180">If hello rate of change is too high, or for other reasons, such as internal failures, hello IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="a51d2-181">Dus als uw toepassing moet betrouwbare voor controle en logboekregistratie van alle tussenliggende statussen, nog steeds aanbevolen wordt dat u D2C berichten.</span><span class="sxs-lookup"><span data-stu-id="a51d2-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="a51d2-182">Hallo twin Meldingsbericht bevat eigenschappen en hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="a51d2-182">hello twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="a51d2-183">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="a51d2-183">Properties</span></span>

    | <span data-ttu-id="a51d2-184">Naam</span><span class="sxs-lookup"><span data-stu-id="a51d2-184">Name</span></span> | <span data-ttu-id="a51d2-185">Waarde</span><span class="sxs-lookup"><span data-stu-id="a51d2-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="a51d2-186">$content-type</span><span class="sxs-lookup"><span data-stu-id="a51d2-186">$content-type</span></span> | <span data-ttu-id="a51d2-187">application/json</span><span class="sxs-lookup"><span data-stu-id="a51d2-187">application/json</span></span> |
    <span data-ttu-id="a51d2-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="a51d2-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="a51d2-189">Tijd waarop het Hallo-bericht is verzonden</span><span class="sxs-lookup"><span data-stu-id="a51d2-189">Time when hello notification was sent</span></span> |
    <span data-ttu-id="a51d2-190">$iothub-bericht-bron</span><span class="sxs-lookup"><span data-stu-id="a51d2-190">$iothub-message-source</span></span> | <span data-ttu-id="a51d2-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="a51d2-191">twinChangeEvents</span></span> |
    <span data-ttu-id="a51d2-192">$content-codering</span><span class="sxs-lookup"><span data-stu-id="a51d2-192">$content-encoding</span></span> | <span data-ttu-id="a51d2-193">UTF-8</span><span class="sxs-lookup"><span data-stu-id="a51d2-193">utf-8</span></span> |
    <span data-ttu-id="a51d2-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="a51d2-194">deviceId</span></span> | <span data-ttu-id="a51d2-195">Hallo-apparaat-id</span><span class="sxs-lookup"><span data-stu-id="a51d2-195">Id of hello device</span></span> |
    <span data-ttu-id="a51d2-196">hubName</span><span class="sxs-lookup"><span data-stu-id="a51d2-196">hubName</span></span> | <span data-ttu-id="a51d2-197">Naam van de IoT-Hub</span><span class="sxs-lookup"><span data-stu-id="a51d2-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="a51d2-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="a51d2-198">operationTimestamp</span></span> | <span data-ttu-id="a51d2-199">[ISO8601] tijdstempel van bewerking</span><span class="sxs-lookup"><span data-stu-id="a51d2-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="a51d2-200">bericht-iothub-schema</span><span class="sxs-lookup"><span data-stu-id="a51d2-200">iothub-message-schema</span></span> | <span data-ttu-id="a51d2-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="a51d2-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="a51d2-202">opType</span><span class="sxs-lookup"><span data-stu-id="a51d2-202">opType</span></span> | <span data-ttu-id="a51d2-203">'replaceTwin' of 'updateTwin'</span><span class="sxs-lookup"><span data-stu-id="a51d2-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="a51d2-204">Bericht Systeemeigenschappen worden voorafgegaan door Hallo `'$'` symbool.</span><span class="sxs-lookup"><span data-stu-id="a51d2-204">Message system properties are prefixed with hello `'$'` symbol.</span></span>

    - <span data-ttu-id="a51d2-205">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="a51d2-205">Body</span></span>
        
    <span data-ttu-id="a51d2-206">Deze sectie bevat alle Hallo twin wijzigingen in een JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="a51d2-206">This section includes all hello twin changes in a JSON format.</span></span> <span data-ttu-id="a51d2-207">Hallo verschil dat deze alle twin secties kan bevatten, wordt Hallo dezelfde notatie als een patch: labels, properties.reported properties.desired en dat het Hallo '$metadata' elementen bevat.</span><span class="sxs-lookup"><span data-stu-id="a51d2-207">It uses hello same format as a patch, with hello difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains hello “$metadata” elements.</span></span> <span data-ttu-id="a51d2-208">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a51d2-208">For example,</span></span>
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

<span data-ttu-id="a51d2-209">Alle voorgaande operations ondersteuning Hallo [optimistische gelijktijdigheid] [ lnk-concurrency] en vereisen Hallo **ServiceConnect** toestemming hebben, zoals gedefinieerd in Hallo [beveiliging ] [ lnk-security] artikel.</span><span class="sxs-lookup"><span data-stu-id="a51d2-209">All hello preceding operations support [Optimistic concurrency][lnk-concurrency] and require hello **ServiceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="a51d2-210">Bovendien toothese bewerkingen, Hallo oplossing een back-end kan:</span><span class="sxs-lookup"><span data-stu-id="a51d2-210">In addition toothese operations, hello solution back end can:</span></span>

* <span data-ttu-id="a51d2-211">Query uitvoeren op Hallo apparaat horende Hallo met SQL-achtige [IoT Hub-querytaal][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="a51d2-211">Query hello device twins using hello SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="a51d2-212">Bewerkingen uitvoeren op grote gegevenssets apparaat horende met [taken][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="a51d2-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="a51d2-213">Apparaatbewerkingen</span><span class="sxs-lookup"><span data-stu-id="a51d2-213">Device operations</span></span>
<span data-ttu-id="a51d2-214">Hallo apparaattoepassing is van invloed op Hallo apparaat twin met Hallo atomische bewerkingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a51d2-214">hello device app operates on hello device twin using hello following atomic operations:</span></span>

1. <span data-ttu-id="a51d2-215">**Ophalen van apparaat twin**.</span><span class="sxs-lookup"><span data-stu-id="a51d2-215">**Retrieve device twin**.</span></span> <span data-ttu-id="a51d2-216">Deze bewerking retourneert Hallo apparaat twin document (inclusief tags en gewenste, gerapporteerd en Systeemeigenschappen) voor Hallo momenteel apparaat verbonden.</span><span class="sxs-lookup"><span data-stu-id="a51d2-216">This operation returns hello device twin document (including tags and desired, reported and system properties) for hello currently connected device.</span></span>
2. <span data-ttu-id="a51d2-217">**De eigenschappen van de gerapporteerde gedeeltelijk bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="a51d2-217">**Partially update reported properties**.</span></span> <span data-ttu-id="a51d2-218">Deze bewerking kunt Hallo gedeeltelijke update Hallo eigenschappen van de momenteel verbonden apparaat Hallo gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="a51d2-218">This operation enables hello partial update of hello reported properties of hello currently connected device.</span></span> <span data-ttu-id="a51d2-219">Deze bewerking gebruikt Hallo bijwerken van dezelfde JSON-indeling die Hallo oplossing back-end gebruikt voor een gedeeltelijke update van de gewenste eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="a51d2-219">This operation uses hello same JSON update format that hello solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="a51d2-220">**Houd rekening met de eigenschappen van de gewenste**.</span><span class="sxs-lookup"><span data-stu-id="a51d2-220">**Observe desired properties**.</span></span> <span data-ttu-id="a51d2-221">Hallo momenteel aangesloten apparaat kunt toobe updates toohello gewenst eigenschappen van een melding krijgen wanneer ze zich voordoen.</span><span class="sxs-lookup"><span data-stu-id="a51d2-221">hello currently connected device can choose toobe notified of updates toohello desired properties when they happen.</span></span> <span data-ttu-id="a51d2-222">Hallo apparaat ontvangt Hallo hetzelfde formulier van update (gedeeltelijke of volledige vervanging) wordt uitgevoerd door Hallo back-end oplossing.</span><span class="sxs-lookup"><span data-stu-id="a51d2-222">hello device receives hello same form of update (partial or full replacement) executed by hello solution back end.</span></span>

<span data-ttu-id="a51d2-223">Alle voorgaande bewerkingen Hallo Hallo vereisen **DeviceConnect** toestemming hebben, zoals gedefinieerd in Hallo [beveiliging] [ lnk-security] artikel.</span><span class="sxs-lookup"><span data-stu-id="a51d2-223">All hello preceding operations require hello **DeviceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="a51d2-224">Hallo [apparaat Azure IoT SDK's] [ lnk-sdks] maken het gemakkelijk toouse Hallo voorafgaand aan de bewerkingen van veel talen en platforms.</span><span class="sxs-lookup"><span data-stu-id="a51d2-224">hello [Azure IoT device SDKs][lnk-sdks] make it easy toouse hello preceding operations from many languages and platforms.</span></span> <span data-ttu-id="a51d2-225">Meer informatie over het Hallo-details van IoT Hub primitieven voor synchronisatie van de gewenste eigenschappen vindt u in [apparaat opnieuw verbinden stroom][lnk-reconnection].</span><span class="sxs-lookup"><span data-stu-id="a51d2-225">More information on hello details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="a51d2-226">Apparaat horende zijn momenteel alleen toegankelijk vanaf apparaten die verbinding tooIoT Hub maken met Hallo MQTT-protocol.</span><span class="sxs-lookup"><span data-stu-id="a51d2-226">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="a51d2-227">De onderwerpen waarnaar wordt verwezen:</span><span class="sxs-lookup"><span data-stu-id="a51d2-227">Reference topics:</span></span>
<span data-ttu-id="a51d2-228">Hallo bieden volgende naslagonderwerpen u meer informatie over het beheren van toegang tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="a51d2-228">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="a51d2-229">Labels en eigenschappen indeling</span><span class="sxs-lookup"><span data-stu-id="a51d2-229">Tags and properties format</span></span>
<span data-ttu-id="a51d2-230">Labels, gewenste en gerapporteerde eigenschappen zijn JSON-objecten met Hallo volgende beperkingen:</span><span class="sxs-lookup"><span data-stu-id="a51d2-230">Tags, desired, and reported properties are JSON objects with hello following restrictions:</span></span>

* <span data-ttu-id="a51d2-231">Alle sleutels in JSON-objecten zijn hoofdlettergevoelig 64 bytes UTF-8, UNICODE-tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="a51d2-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="a51d2-232">Toegestane tekens Unicode-tekens (segmenten C0 en C1), uitsluiten en `'.'`, `' '`, en `'$'`.</span><span class="sxs-lookup"><span data-stu-id="a51d2-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="a51d2-233">Alle waarden in de JSON-objecten van de volgende JSON-typen Hallo kunnen zijn: boolean, getal, string, object.</span><span class="sxs-lookup"><span data-stu-id="a51d2-233">All values in JSON objects can be of hello following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="a51d2-234">Matrices zijn niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="a51d2-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="a51d2-235">Alle JSON-objecten in tags, gewenste en gerapporteerde eigenschappen kunnen een maximale diepte van 5 hebben.</span><span class="sxs-lookup"><span data-stu-id="a51d2-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="a51d2-236">Bijvoorbeeld: Hallo na-object is ongeldig:</span><span class="sxs-lookup"><span data-stu-id="a51d2-236">For instance, hello following object is valid:</span></span>

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

* <span data-ttu-id="a51d2-237">Alle tekenreekswaarden mag hoogstens 512 bytes lang.</span><span class="sxs-lookup"><span data-stu-id="a51d2-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="a51d2-238">De grootte van de apparaat-twin</span><span class="sxs-lookup"><span data-stu-id="a51d2-238">Device twin size</span></span>
<span data-ttu-id="a51d2-239">IoT Hub worden afgedwongen voor een beperking van de grootte van 8KB op Hallo van waarden van `tags`, `properties/desired`, en `properties/reported`, met uitzondering van alleen-lezen-elementen.</span><span class="sxs-lookup"><span data-stu-id="a51d2-239">IoT Hub enforces an 8KB size limitation on hello values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="a51d2-240">Hallo grootte wordt berekend door het tellen van alle tekens, met uitzondering van UNICODE-tekens (segmenten C0 en C1) en ruimte beheren `' '` wanneer deze buiten een tekenreeksconstante wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a51d2-240">hello size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="a51d2-241">IoT Hub worden alle bewerkingen die Hallo van deze documenten boven hello vergroot zou geweigerd met een fout.</span><span class="sxs-lookup"><span data-stu-id="a51d2-241">IoT Hub rejects with an error all operations that would increase hello size of those documents above hello limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="a51d2-242">Metagegevens van apparaten twin</span><span class="sxs-lookup"><span data-stu-id="a51d2-242">Device twin metadata</span></span>
<span data-ttu-id="a51d2-243">IoT Hub onderhoudt Hallo tijdstempel van de laatste update Hallo voor elk JSON-object in de apparaat-twin gewenst en eigenschappen gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="a51d2-243">IoT Hub maintains hello timestamp of hello last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="a51d2-244">Hallo tijdstempels in UTC en gecodeerd in Hallo [ISO8601] indeling `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span><span class="sxs-lookup"><span data-stu-id="a51d2-244">hello timestamps are in UTC and encoded in hello [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="a51d2-245">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a51d2-245">For example:</span></span>

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

<span data-ttu-id="a51d2-246">Deze informatie wordt opgeslagen op elk niveau (niet alleen Hallo leaves Hallo JSON-structuur) toopreserve updates objectsleutels te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a51d2-246">This information is kept at every level (not just hello leaves of hello JSON structure) toopreserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="a51d2-247">Optimistische gelijktijdigheid</span><span class="sxs-lookup"><span data-stu-id="a51d2-247">Optimistic concurrency</span></span>
<span data-ttu-id="a51d2-248">Labels, gewenst en eigenschappen van alle ondersteuning optimistische gelijktijdigheid gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="a51d2-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="a51d2-249">Labels hebben een ETag conform [RFC7232], die staat voor de JSON-weergave Hallo-tag.</span><span class="sxs-lookup"><span data-stu-id="a51d2-249">Tags have an ETag, as per [RFC7232], that represents hello tag's JSON representation.</span></span> <span data-ttu-id="a51d2-250">U kunt ETags gebruiken in voorwaardelijke bijwerkbewerkingen van Hallo oplossing voor back-end tooensure consistentie.</span><span class="sxs-lookup"><span data-stu-id="a51d2-250">You can use ETags in conditional update operations from hello solution back end tooensure consistency.</span></span>

<span data-ttu-id="a51d2-251">Apparaat-twin gewenst en gerapporteerde eigenschappen zijn niet ETags, maar hebben een `$version` waarde die kan worden gegarandeerd toobe incrementele.</span><span class="sxs-lookup"><span data-stu-id="a51d2-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed toobe incremental.</span></span> <span data-ttu-id="a51d2-252">Tooan ETag, Hallo versie kan ook worden gebruikt door Hallo bijwerken van derden tooenforce consistentie van updates.</span><span class="sxs-lookup"><span data-stu-id="a51d2-252">Similarly tooan ETag, hello version can be used by hello updating party tooenforce consistency of updates.</span></span> <span data-ttu-id="a51d2-253">Bijvoorbeeld, een apparaat-app voor een gerapporteerde eigenschap of Hallo back-end oplossing voor een gewenste eigenschap.</span><span class="sxs-lookup"><span data-stu-id="a51d2-253">For example, a device app for a reported property or hello solution back end for a desired property.</span></span>

<span data-ttu-id="a51d2-254">Versies zijn ook handig wanneer een observing agent (zoals Hallo apparaattoepassing Hallo gewenst eigenschappen observeren) op elkaar races tussen Hallo resultaat van een bewerking ophalen en een melding van updates afstemmen moet.</span><span class="sxs-lookup"><span data-stu-id="a51d2-254">Versions are also useful when an observing agent (such as hello device app observing hello desired properties) must reconcile races between hello result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="a51d2-255">sectie Hallo [apparaat opnieuw verbinden stroom] [ lnk-reconnection] vindt u meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a51d2-255">hello section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="a51d2-256">Opnieuw verbinden stroom van apparaat</span><span class="sxs-lookup"><span data-stu-id="a51d2-256">Device reconnection flow</span></span>
<span data-ttu-id="a51d2-257">IoT Hub behoudt updatemeldingen gewenste eigenschappen voor niet-verbonden apparaten niet.</span><span class="sxs-lookup"><span data-stu-id="a51d2-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="a51d2-258">Hieruit volgt dat een apparaat dat verbinding maakt Hallo volledige gewenste eigenschappendocument in toevoeging toosubscribing voor updatemeldingen moet ophalen.</span><span class="sxs-lookup"><span data-stu-id="a51d2-258">It follows that a device that is connecting must retrieve hello full desired properties document, in addition toosubscribing for update notifications.</span></span> <span data-ttu-id="a51d2-259">Hallo races tussen updatemeldingen en volledige ophalen van de mogelijkheid gegeven, ervoor Hallo volgende stroom wordt gezorgd</span><span class="sxs-lookup"><span data-stu-id="a51d2-259">Given hello possibility of races between update notifications and full retrieval, hello following flow must be ensured:</span></span>

1. <span data-ttu-id="a51d2-260">App voor het apparaat verbindt tooan IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="a51d2-260">Device app connects tooan IoT hub.</span></span>
2. <span data-ttu-id="a51d2-261">App voor het apparaat is lid voor de gewenste eigenschappen updatemeldingen.</span><span class="sxs-lookup"><span data-stu-id="a51d2-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="a51d2-262">Apparaattoepassing haalt Hallo volledige document voor gewenste eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="a51d2-262">Device app retrieves hello full document for desired properties.</span></span>

<span data-ttu-id="a51d2-263">Hallo apparaattoepassing kunt negeren alle meldingen met `$version` of minder zijn dan de versie van volledige opgehaalde document Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="a51d2-263">hello device app can ignore all notifications with `$version` less or equal than hello version of hello full retrieved document.</span></span> <span data-ttu-id="a51d2-264">Deze aanpak is mogelijk omdat IoT Hub wordt gegarandeerd dat versies altijd verhogen.</span><span class="sxs-lookup"><span data-stu-id="a51d2-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="a51d2-265">Deze logica wordt al geïmplementeerd in Hallo [apparaat Azure IoT SDK's][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="a51d2-265">This logic is already implemented in hello [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="a51d2-266">Deze beschrijving is handig als Hallo apparaattoepassing een apparaat met Azure IoT SDK's gebruiken kan en Hallo MQTT interface moet rechtstreeks programma.</span><span class="sxs-lookup"><span data-stu-id="a51d2-266">This description is useful only if hello device app cannot use any of Azure IoT device SDKs and must program hello MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="a51d2-267">Aanvullende referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="a51d2-267">Additional reference material</span></span>
<span data-ttu-id="a51d2-268">Er zijn andere onderwerpen met naslaginformatie in Hallo Ontwikkelaarshandleiding voor IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="a51d2-268">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="a51d2-269">Hallo [IoT-hubeindpunten] [ lnk-endpoints] beschreven Hallo verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.</span><span class="sxs-lookup"><span data-stu-id="a51d2-269">hello [IoT Hub endpoints][lnk-endpoints] article describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="a51d2-270">Hallo [bandbreedtebeperking en quota's] [ lnk-quotas] Hallo quota's die van toepassing toohello service IoT Hub en bandbreedteregeling gedrag tooexpect Hallo wanneer u Hallo-service wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="a51d2-270">hello [Throttling and quotas][lnk-quotas] article describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="a51d2-271">Hallo [apparaat en de service Azure IoT-SDK's] [ lnk-sdks] artikel lijsten Hallo verschillende taal SDK's kunt u bij het ontwikkelen van apps voor het apparaat en de service die communiceren met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a51d2-271">hello [Azure IoT device and service SDKs][lnk-sdks] article lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="a51d2-272">Hallo [querytaal IoT Hub voor apparaat horende, taken en berichtroutering] [ lnk-query] beschreven Hallo querytaal IoT-Hub kunt u informatie van de tooretrieve uit IoT Hub over uw apparaat horende en taken .</span><span class="sxs-lookup"><span data-stu-id="a51d2-272">hello [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="a51d2-273">Hallo [IoT Hub MQTT ondersteuning] [ lnk-devguide-mqtt] artikel vindt u meer informatie over ondersteuning voor Hallo MQTT protocol IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a51d2-273">hello [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a51d2-274">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a51d2-274">Next steps</span></span>
<span data-ttu-id="a51d2-275">Nu u over horende apparaten hebt geleerd, kunt u mogelijk geïnteresseerd in de volgende onderwerpen voor IoT Hub developer guide Hallo:</span><span class="sxs-lookup"><span data-stu-id="a51d2-275">Now you have learned about device twins, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="a51d2-276">[Een directe methode aangeroepen voor een apparaat][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="a51d2-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="a51d2-277">[Taken plannen op meerdere apparaten][lnk-jobs]</span><span class="sxs-lookup"><span data-stu-id="a51d2-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="a51d2-278">Als u tootry sommige Hallo concepten die in dit artikel wordt beschreven wilt, kunt u mogelijk geïnteresseerd in Hallo IoT Hub zelfstudies te volgen:</span><span class="sxs-lookup"><span data-stu-id="a51d2-278">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="a51d2-279">[Hoe toouse Hallo apparaat twin][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="a51d2-279">[How toouse hello device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="a51d2-280">[Hoe toouse apparaat eigenschappen twin][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="a51d2-280">[How toouse device twin properties][lnk-twin-properties]</span></span>

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

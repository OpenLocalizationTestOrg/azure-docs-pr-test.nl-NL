---
title: aaaDeveloper-handleiding voor Azure IoT Hub | Microsoft Docs
description: Hello Azure IoT Hub developer guide bevat discussies van eindpunten, beveiliging, identiteitsregister hello, Apparaatbeheer, direct methoden, apparaat horende, bestandsuploads, taken, Hallo querytaal IoT Hub en messaging.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: d534ff9d-2de5-4995-bb2d-84a02693cb2e
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 2d3f18399e4cef6f9c4850a5caeb170a2d091a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-developer-guide"></a><span data-ttu-id="c76b0-103">Azure IoT Hub developer guide</span><span class="sxs-lookup"><span data-stu-id="c76b0-103">Azure IoT Hub developer guide</span></span>

<span data-ttu-id="c76b0-104">Azure IoT Hub is een volledig beheerde service waarmee stabiele en veilige tweerichtingscommunicatie tussen miljoenen apparaten inschakelen en een back-end oplossing.</span><span class="sxs-lookup"><span data-stu-id="c76b0-104">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span>

<span data-ttu-id="c76b0-105">Azure IoT Hub beschikt u over:</span><span class="sxs-lookup"><span data-stu-id="c76b0-105">Azure IoT Hub provides you with:</span></span>

* <span data-ttu-id="c76b0-106">Veilige communicatie met behulp van per apparaat beveiligingsreferenties en toegangscontrole.</span><span class="sxs-lookup"><span data-stu-id="c76b0-106">Secure communications by using per-device security credentials and access control.</span></span>
* <span data-ttu-id="c76b0-107">Opties voor meerdere apparaat-naar-cloud- en cloud-naar-apparaat hyperschaal communicatie.</span><span class="sxs-lookup"><span data-stu-id="c76b0-107">Multiple device-to-cloud and cloud-to-device hyper-scale communication options.</span></span>
* <span data-ttu-id="c76b0-108">Waarop opslag van informatie over de status per apparaat en de metagegevens.</span><span class="sxs-lookup"><span data-stu-id="c76b0-108">Queryable storage of per-device state information and meta-data.</span></span>
* <span data-ttu-id="c76b0-109">Eenvoudig apparaten connectiviteit met de apparaatbibliotheken voor Hallo meest populaire talen en platforms.</span><span class="sxs-lookup"><span data-stu-id="c76b0-109">Easy device connectivity with device libraries for hello most popular languages and platforms.</span></span>

<span data-ttu-id="c76b0-110">Deze IoT Hub developer guide bevat Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c76b0-110">This IoT Hub developer guide includes hello following articles:</span></span>

* <span data-ttu-id="c76b0-111">[Apparaat-naar-cloud communicatie richtlijnen] [ lnk-d2c-guidance] kunt u tussen apparaat-naar-cloud-berichten van apparaat twin gemelde eigenschappen en uploaden bestand kiezen.</span><span class="sxs-lookup"><span data-stu-id="c76b0-111">[Device-to-cloud communication guidance][lnk-d2c-guidance] helps you choose between device-to-cloud messages, device twin's reported properties, and file upload.</span></span>
* <span data-ttu-id="c76b0-112">[Cloud-naar-apparaat communicatie richtlijnen] [ lnk-c2d-guidance] kunt u tussen rechtstreekse methoden van apparaat twin gewenste eigenschappen en cloud-naar-apparaat-berichten kiezen.</span><span class="sxs-lookup"><span data-stu-id="c76b0-112">[Cloud-to-device communication guidance][lnk-c2d-guidance] helps you choose between direct methods, device twin's desired properties, and cloud-to-device messages.</span></span>
* <span data-ttu-id="c76b0-113">[Apparaat-naar-cloud- en cloud-naar-apparaat met IoT Hub berichten] [ devguide-messaging] Hallo messaging worden functies beschreven (apparaat-naar-cloud en cloud-naar-apparaat) die IoT-Hub toont.</span><span class="sxs-lookup"><span data-stu-id="c76b0-113">[Device-to-cloud and cloud-to-device messaging with IoT Hub][devguide-messaging] describes hello messaging features (device-to-cloud and cloud-to-device) that IoT Hub exposes.</span></span>
  * <span data-ttu-id="c76b0-114">[Verzenden van apparaat-naar-cloudberichten tooIoT Hub][devguide-messages-d2c].</span><span class="sxs-lookup"><span data-stu-id="c76b0-114">[Send device-to-cloud messages tooIoT Hub][devguide-messages-d2c].</span></span>
  * <span data-ttu-id="c76b0-115">[Apparaat-naar-cloud-berichten lezen uit Hallo ingebouwd eindpunt][devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="c76b0-115">[Read device-to-cloud messages from hello built-in endpoint][devguide-builtin].</span></span>
  * <span data-ttu-id="c76b0-116">[Gebruik aangepaste eindpunten en routeringsregels voor apparaat-naar-cloudberichten][devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="c76b0-116">[Use custom endpoints and routing rules for device-to-cloud messages][devguide-custom].</span></span>
  * <span data-ttu-id="c76b0-117">[Verzenden van cloud naar apparaat-berichten uit IoT Hub][devguide-messages-c2d].</span><span class="sxs-lookup"><span data-stu-id="c76b0-117">[Send cloud-to-device messages from IoT Hub][devguide-messages-c2d].</span></span>
  * <span data-ttu-id="c76b0-118">[Maken en IoT Hub berichten lezen][devguide-format].</span><span class="sxs-lookup"><span data-stu-id="c76b0-118">[Create and read IoT Hub messages][devguide-format].</span></span>
* <span data-ttu-id="c76b0-119">[Uploaden van bestanden van een apparaat] [ devguide-upload] wordt beschreven hoe u de bestanden van een apparaat kunt uploaden.</span><span class="sxs-lookup"><span data-stu-id="c76b0-119">[Upload files from a device][devguide-upload] describes how you can upload files from a device.</span></span> <span data-ttu-id="c76b0-120">Hallo artikel bevat ook informatie over onderwerpen zoals Hallo meldingen Hallo uploadproces kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="c76b0-120">hello article also includes information about topics such as hello notifications hello upload process can send.</span></span>
* <span data-ttu-id="c76b0-121">[Apparaat-id's van IoT-Hub beheren] [ devguide-identities] wordt beschreven welke gegevens elk IoT-hub register identiteitsopslag en hoe u toegang tot en wijzigt.</span><span class="sxs-lookup"><span data-stu-id="c76b0-121">[Manage device identities in IoT Hub][devguide-identities] describes what information each IoT hub's identity registry stores, and how you can access and modify it.</span></span>
* <span data-ttu-id="c76b0-122">[Beheren van toegang tooIoT Hub] [ devguide-security] wordt Hallo security model gebruikt toogrant toegang tooIoT Hub functionaliteit beschreven voor apparaten en cloud-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="c76b0-122">[Control access tooIoT Hub][devguide-security] describes hello security model used toogrant access tooIoT Hub functionality for both devices and cloud components.</span></span> <span data-ttu-id="c76b0-123">Hallo artikel bevat informatie over het gebruik van tokens en X.509-certificaten en details van Hallo machtigingen u verleent.</span><span class="sxs-lookup"><span data-stu-id="c76b0-123">hello article includes information about using tokens and X.509 certificates, and details of hello permissions you can grant.</span></span>
* <span data-ttu-id="c76b0-124">[Gebruik Apparaatstatus horende toosynchronize en configuraties] [ devguide-device-twins] beschrijft Hallo *apparaat twin* concept en Hallo functionaliteit, zoals het synchroniseren van een apparaat met het apparaat worden getoond Twin.</span><span class="sxs-lookup"><span data-stu-id="c76b0-124">[Use device twins toosynchronize state and configurations][devguide-device-twins] describes hello *device twin* concept and hello functionality it exposes such as synchronizing a device with its device twin.</span></span> <span data-ttu-id="c76b0-125">Hallo artikel bevat informatie over het Hallo-gegevens die zijn opgeslagen in een twin apparaat.</span><span class="sxs-lookup"><span data-stu-id="c76b0-125">hello article includes information about hello data stored in a device twin.</span></span>
* <span data-ttu-id="c76b0-126">[Een directe methode aangeroepen voor een apparaat] [ devguide-directmethods] beschrijft Hallo levenscyclus van een directe methode, informatie over hoe tooinvoke methoden op een apparaat vanuit uw back-end-app en ingang Hallo methode op uw apparaat directe.</span><span class="sxs-lookup"><span data-stu-id="c76b0-126">[Invoke a direct method on a device][devguide-directmethods] describes hello lifecycle of a direct method, information about how tooinvoke methods on a device from your back-end app and handle hello direct method on your device.</span></span>
* <span data-ttu-id="c76b0-127">[Plannen van taken op meerdere apparaten] [ devguide-jobs] wordt beschreven hoe u taken op meerdere apparaten kunt plannen.</span><span class="sxs-lookup"><span data-stu-id="c76b0-127">[Schedule jobs on multiple devices][devguide-jobs] describes how you can schedule jobs on multiple devices.</span></span> <span data-ttu-id="c76b0-128">Hallo artikel wordt beschreven hoe toosubmit taken die taken uitvoeren als een directe methode, het bijwerken van een apparaat met een apparaat-twin uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c76b0-128">hello article describes how toosubmit jobs that perform tasks as executing a direct method, updating a device using a device twin.</span></span> <span data-ttu-id="c76b0-129">Ook wordt beschreven hoe tooquery Hallo status van een taak.</span><span class="sxs-lookup"><span data-stu-id="c76b0-129">It also describes how tooquery hello status of a job.</span></span>
* <span data-ttu-id="c76b0-130">[Verwijzen naar: Kies een communicatieprotocol] [ devguide-protocol] beschrijft Hallo communicatieprotocollen dat IoT Hub voor apparaatcommunicatie ondersteunt en lijsten Hallo poorten die geopend worden moeten.</span><span class="sxs-lookup"><span data-stu-id="c76b0-130">[Reference - choose a communication protocol][devguide-protocol] describes hello communication protocols that IoT Hub supports for device communication and lists hello ports that should be open.</span></span>
* <span data-ttu-id="c76b0-131">[Referentie - IoT-hubeindpunten] [ devguide-endpoints] beschrijft Hallo verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.</span><span class="sxs-lookup"><span data-stu-id="c76b0-131">[Reference - IoT Hub endpoints][devguide-endpoints] describes hello various endpoints that each IoT hub exposes for runtime and management operations.</span></span> <span data-ttu-id="c76b0-132">Hallo tevens wordt beschreven hoe u kunt extra eindpunten maken in uw IoT-hub en hoe toouse een veld gateway tooenable apparaten connectiviteit tooyour IoT Hub-eindpunten in scenario's voor niet-standaard.</span><span class="sxs-lookup"><span data-stu-id="c76b0-132">hello article also describes how you can create additional endpoints in your IoT hub, and how toouse a field gateway tooenable devices connectivity tooyour IoT Hub endpoints in non-standard scenarios.</span></span>
* <span data-ttu-id="c76b0-133">[Referentie - querytaal IoT Hub voor apparaat horende, taken en berichtroutering] [ devguide-query] die IoT Hub-querytaal waarmee u tooretrieve gegevens van uw hub over uw apparaat horende en taken worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="c76b0-133">[Reference - IoT Hub query language for device twins, jobs, and message routing][devguide-query] describes that IoT Hub query language that enables you tooretrieve information from your hub about your device twins and jobs.</span></span>
* <span data-ttu-id="c76b0-134">[Referentie - quota's en beperking] [ devguide-quotas] bevat een overzicht van Hallo quota die zijn ingesteld in Hallo service IoT Hub en Hallo beperking gedrag die u kunt toosee verwachten wanneer u een quotum overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="c76b0-134">[Reference - quotas and throttling][devguide-quotas] summarizes hello quotas set in hello IoT Hub service and hello throttling behavior you can expect toosee when you exceed a quota.</span></span>
* <span data-ttu-id="c76b0-135">[Verwijzen naar - prijzen] [ devguide-pricing] biedt algemene informatie over de verschillende SKU's en prijzen voor IoT Hub en meer informatie over hoe verschillende functies van de IoT Hub worden gemeten als Hallo door de IoT Hub berichten.</span><span class="sxs-lookup"><span data-stu-id="c76b0-135">[Reference - pricing][devguide-pricing] provides general information on different SKUs and pricing for IoT Hub and details on how hello various IoT Hub functionalities are metered as messages by IoT Hub.</span></span>
* <span data-ttu-id="c76b0-136">[Referentie - apparaat en de service SDK's] [ devguide-sdks] lijsten hello Azure IoT SDK's kunt u toodevelop apparaat en de service-apps die met uw IoT-hub communiceren.</span><span class="sxs-lookup"><span data-stu-id="c76b0-136">[Reference - Device and service SDKs][devguide-sdks] lists hello Azure IoT SDKs you can use toodevelop both device and service apps that interact with your IoT hub.</span></span> <span data-ttu-id="c76b0-137">Hallo artikel bevat koppelingen tooonline API-documentatie.</span><span class="sxs-lookup"><span data-stu-id="c76b0-137">hello article includes links tooonline API documentation.</span></span>
* <span data-ttu-id="c76b0-138">[Referentie - ondersteuning voor IoT Hub MQTT] [ devguide-mqtt] bevat gedetailleerde informatie over hoe IoT Hub Hallo MQTT protocol ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="c76b0-138">[Reference - IoT Hub MQTT support][devguide-mqtt] provides detailed information about how IoT Hub supports hello MQTT protocol.</span></span> <span data-ttu-id="c76b0-139">Hallo artikel beschrijft Hallo-ondersteuning voor Hallo MQTT protocol ingebouwde toohello Azure IoT SDK's en bevat informatie over het gebruik van Hallo MQTT protocol rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="c76b0-139">hello article describes hello support for hello MQTT protocol built-in toohello Azure IoT SDKs and provides information about using hello MQTT protocol directly.</span></span>
* <span data-ttu-id="c76b0-140">[Verklarende woordenlijst] [ devguide-glossary] een lijst met algemene IoT-Hub-termen.</span><span class="sxs-lookup"><span data-stu-id="c76b0-140">[Glossary][devguide-glossary] a list of common IoT Hub-related terms.</span></span>

[devguide-messaging]: iot-hub-devguide-messaging.md
[devguide-upload]: iot-hub-devguide-file-upload.md
[devguide-identities]: iot-hub-devguide-identity-registry.md
[devguide-security]: iot-hub-devguide-security.md
[devguide-device-twins]: iot-hub-devguide-device-twins.md
[devguide-directmethods]: iot-hub-devguide-direct-methods.md
[devguide-jobs]: iot-hub-devguide-jobs.md
[devguide-endpoints]: iot-hub-devguide-endpoints.md
[devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[devguide-query]: iot-hub-devguide-query-language.md
[devguide-sdks]: iot-hub-devguide-sdks.md
[devguide-mqtt]: iot-hub-mqtt-support.md
[devguide-glossary]: iot-hub-devguide-glossary.md
[devguide-pricing]: iot-hub-devguide-pricing.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[devguide-messages-d2c]: iot-hub-devguide-messages-d2c.md
[devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[devguide-custom]: iot-hub-devguide-messages-read-custom.md
[devguide-messages-c2d]: iot-hub-devguide-messages-c2d.md
[devguide-format]: iot-hub-devguide-messages-construct.md
[devguide-protocol]: iot-hub-devguide-protocols.md

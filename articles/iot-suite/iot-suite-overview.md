---
title: overzicht van Azure IoT Suite aaaMicrosoft | Microsoft Docs
description: Overzicht van hoe Azure IoT Suite biedt internet der dingen vooraf geconfigureerde oplossingen toocollect, analyseren en opslaan van gegevens, bieden van visualisaties en integreren met andere systemen.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a><span data-ttu-id="38924-103">Overview of Azure IoT Suite (Engelstalig)</span><span class="sxs-lookup"><span data-stu-id="38924-103">Overview of Azure IoT Suite</span></span>

<span data-ttu-id="38924-104">Hello Azure internet der dingen (IoT)-services bieden een breed scala aan mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="38924-104">hello Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="38924-105">Met deze hoogwaardige services kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="38924-105">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="38924-106">Gegevens van apparaten verzamelen</span><span class="sxs-lookup"><span data-stu-id="38924-106">Collect data from devices</span></span>
* <span data-ttu-id="38924-107">Gegevensstromen in beweging analyseren</span><span class="sxs-lookup"><span data-stu-id="38924-107">Analyze data streams in-motion</span></span>
* <span data-ttu-id="38924-108">Grote gegevenssets opslaan en er query’s op uitvoeren</span><span class="sxs-lookup"><span data-stu-id="38924-108">Store and query large data sets</span></span>
* <span data-ttu-id="38924-109">Gegevens in realtime en historische gegevens visualiseren</span><span class="sxs-lookup"><span data-stu-id="38924-109">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="38924-110">Integraties met back-officesystemen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="38924-110">Integrate with back-office systems</span></span>
* <span data-ttu-id="38924-111">Uw apparaten beheren</span><span class="sxs-lookup"><span data-stu-id="38924-111">Manage your devices</span></span>

<span data-ttu-id="38924-112">toodeliver deze mogelijkheden kunnen Azure IoT Suite-pakketten meerdere Azure-services met aangepaste extensies als *vooraf geconfigureerde oplossingen*.</span><span class="sxs-lookup"><span data-stu-id="38924-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span></span> <span data-ttu-id="38924-113">Deze vooraf geconfigureerde oplossingen zijn basisimplementaties van algemene patronen van IoT-oplossing waarmee tooreduce Hallo u tijd toodeliver uw IoT-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="38924-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="38924-114">Met behulp van Hallo [IoT-SDK's][lnk-sdks], u kunt aanpassen en uitbreiden van deze oplossingen toomeet uw eigen vereisten.</span><span class="sxs-lookup"><span data-stu-id="38924-114">Using hello [IoT software development kits][lnk-sdks], you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="38924-115">U kunt deze oplossingen gebruiken als voorbeelden of sjablonen als u nieuwe IoT-oplossingen ontwikkelt.</span><span class="sxs-lookup"><span data-stu-id="38924-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="38924-116">Hallo biedt volgende video een inleiding tooAzure IoT Suite:</span><span class="sxs-lookup"><span data-stu-id="38924-116">hello following video provides an introduction tooAzure IoT Suite:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a><span data-ttu-id="38924-117">Azure IoT-services in Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="38924-117">Azure IoT services in Azure IoT Suite</span></span>
<span data-ttu-id="38924-118">Hallo vooraf geconfigureerde oplossingen gebruiken doorgaans Hallo volgende services:</span><span class="sxs-lookup"><span data-stu-id="38924-118">hello preconfigured solutions typically use hello following services:</span></span>

* <span data-ttu-id="38924-119">Core tooAzure IoT Suite is Hallo [Azure IoT Hub] [ lnk-iot-hub] service.</span><span class="sxs-lookup"><span data-stu-id="38924-119">Core tooAzure IoT Suite is hello [Azure IoT Hub][lnk-iot-hub] service.</span></span> <span data-ttu-id="38924-120">Deze service bevat Hallo apparaat-naar-cloud en de mogelijkheden voor cloud-naar-apparaat messaging en besluiten als gateway toohello Hallo cloud Hallo andere belangrijke IoT Suite-services.</span><span class="sxs-lookup"><span data-stu-id="38924-120">This service provides hello device-to-cloud and cloud-to-device messaging capabilities and acts as hello gateway toohello cloud and hello other key IoT Suite services.</span></span> <span data-ttu-id="38924-121">Hallo-service kunt u berichten van uw apparaten op schaal tooreceive en opdrachten tooyour apparaten verzenden.</span><span class="sxs-lookup"><span data-stu-id="38924-121">hello service enables you tooreceive messages from your devices at scale, and send commands tooyour devices.</span></span> <span data-ttu-id="38924-122">Hallo-service kunt u ook te[beheren van uw apparaten][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="38924-122">hello service also enables you too[manage your devices][lnk-device-management].</span></span> <span data-ttu-id="38924-123">U kunt bijvoorbeeld configureren, opnieuw starten of u de fabrieksinstellingen op een of meer apparaten verbonden toohello hub.</span><span class="sxs-lookup"><span data-stu-id="38924-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected toohello hub.</span></span>
* <span data-ttu-id="38924-124">[Azure Stream Analytics][lnk-asa] biedt de mogelijkheid om gegevens in beweging te analyseren.</span><span class="sxs-lookup"><span data-stu-id="38924-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span></span> <span data-ttu-id="38924-125">IoT Suite maakt gebruik van deze service tooprocess binnenkomende telemetriegegevens, uitvoeren van aggregatiebewerkingen en detecteren van gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="38924-125">IoT Suite uses this service tooprocess incoming telemetry, perform aggregation, and detect events.</span></span> <span data-ttu-id="38924-126">Hallo vooraf geconfigureerde oplossingen gebruiken ook stream analytics tooprocess informatieve berichten met gegevens zoals metagegevens of opdracht reacties van apparaten.</span><span class="sxs-lookup"><span data-stu-id="38924-126">hello preconfigured solutions also use stream analytics tooprocess informational messages that contain data such as metadata or command responses from devices.</span></span> <span data-ttu-id="38924-127">Hallo oplossingen gebruik Stream Analytics tooprocess Hallo-berichten van uw apparaten en deze berichten tooother services leveren.</span><span class="sxs-lookup"><span data-stu-id="38924-127">hello solutions use Stream Analytics tooprocess hello messages from your devices and deliver those messages tooother services.</span></span>
* <span data-ttu-id="38924-128">[Azure Storage] [ lnk-azure-storage] en [Azure Cosmos DB] [ lnk-document-db] Hallo gegevens opslagmogelijkheden bevatten.</span><span class="sxs-lookup"><span data-stu-id="38924-128">[Azure Storage][lnk-azure-storage] and [Azure Cosmos DB][lnk-document-db] provide hello data storage capabilities.</span></span> <span data-ttu-id="38924-129">Hallo vooraf geconfigureerde oplossingen gebruiken blob storage toostore Telemetrie en toomake deze beschikbaar voor analyse.</span><span class="sxs-lookup"><span data-stu-id="38924-129">hello preconfigured solutions use blob storage toostore telemetry and toomake it available for analysis.</span></span> <span data-ttu-id="38924-130">Hallo oplossingen gebruik van metagegevens van de Cosmos-DB toostore apparaten en schakel mogelijkheden voor Apparaatbeheer Hallo van Hallo-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="38924-130">hello solutions use Cosmos DB toostore device metadata and enable hello device management capabilities of hello solutions.</span></span>
* <span data-ttu-id="38924-131">[Azure Web Apps] [ lnk-web-apps] en [Microsoft Power BI] [ lnk-power-bi] Hallo gegevensvisualisatie mogelijkheden bieden.</span><span class="sxs-lookup"><span data-stu-id="38924-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide hello data visualization capabilities.</span></span> <span data-ttu-id="38924-132">Hallo flexibiliteit van Power BI kunt u tooquickly bouwen uw eigen interactieve dashboards die gebruikmaken van IoT Suite-gegevens.</span><span class="sxs-lookup"><span data-stu-id="38924-132">hello flexibility of Power BI enables you tooquickly build your own interactive dashboards that use IoT Suite data.</span></span>

<span data-ttu-id="38924-133">Zie voor een overzicht van Hallo-architectuur van een typische IoT-oplossing [Microsoft Azure en Internet der dingen (IoT) Hallo][iot-suite-what-is-azure-iot].</span><span class="sxs-lookup"><span data-stu-id="38924-133">For an overview of hello architecture of a typical IoT solution, see [Microsoft Azure and hello Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span></span>

## <a name="preconfigured-solutions"></a><span data-ttu-id="38924-134">Vooraf geconfigureerde oplossingen</span><span class="sxs-lookup"><span data-stu-id="38924-134">Preconfigured solutions</span></span>

<span data-ttu-id="38924-135">IoT Suite bevat vooraf geconfigureerde oplossingen die u tooquickly aan de slag met inschakelen en tooexplore Hallo algemene IoT-scenario's, zoals:</span><span class="sxs-lookup"><span data-stu-id="38924-135">IoT Suite includes preconfigured solutions that enable you tooquickly get started with and tooexplore hello common IoT scenarios, such as:</span></span>

* <span data-ttu-id="38924-136">Externe bewaking</span><span class="sxs-lookup"><span data-stu-id="38924-136">Remote monitoring</span></span>
* <span data-ttu-id="38924-137">Voorspellend onderhoud</span><span class="sxs-lookup"><span data-stu-id="38924-137">Predictive maintenance</span></span>
* <span data-ttu-id="38924-138">Verbonden factory</span><span class="sxs-lookup"><span data-stu-id="38924-138">Connected factory</span></span>

<span data-ttu-id="38924-139">U kunt deze oplossingen tooyour Azure-abonnement implementeren en voer vervolgens een volledige, end-to-end-IoT-scenario.</span><span class="sxs-lookup"><span data-stu-id="38924-139">You can deploy these solutions tooyour Azure subscription and then run a complete, end-to-end IoT scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38924-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="38924-140">Next steps</span></span>

<span data-ttu-id="38924-141">Nu dat u een overzicht van wat IoT Suite kan doen en wat zijn de belangrijkste componenten hebt, kunt u meer informatie over Hallo vooraf geconfigureerde oplossingen in IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="38924-141">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about hello preconfigured solutions in IoT Suite.</span></span> <span data-ttu-id="38924-142">Zie voor meer informatie [wat hello Azure IoT zijn vooraf geconfigureerde oplossingen?][lnk-what-are-preconfig]</span><span class="sxs-lookup"><span data-stu-id="38924-142">For more information, see [What are hello Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span></span>

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md

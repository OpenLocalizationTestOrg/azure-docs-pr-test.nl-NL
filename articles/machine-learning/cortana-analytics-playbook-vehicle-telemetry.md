---
title: aaaPredict vehicle gezondheid en die zorg draagt gewoonten - Azure | Microsoft Docs
description: Hallo-mogelijkheden van Cortana Intelligence toogain real-time en voorspellende inzicht op vehicle health gebruiken en gewoonten besturen.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="33eee-103">Draaiboek met oplossingen voor voertuigtelemetrieanalyse</span><span class="sxs-lookup"><span data-stu-id="33eee-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="33eee-104">Dit **menu** toohello hoofdstukken in deze playbook koppelingen.</span><span class="sxs-lookup"><span data-stu-id="33eee-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="33eee-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="33eee-105">Overview</span></span>
<span data-ttu-id="33eee-106">Super computers worden buiten Hallo testomgeving hebt verplaatst en nu in onze garage!</span><span class="sxs-lookup"><span data-stu-id="33eee-106">Super computers have moved out of hello lab and are now parked in our garage!</span></span> <span data-ttu-id="33eee-107">Deze geavanceerde auto's bevatten een groot aantal sensoren, zodat ze Hallo mogelijkheid tootrack en bewaken van miljoenen gebeurtenissen per seconde.</span><span class="sxs-lookup"><span data-stu-id="33eee-107">These cutting-edge automobiles contain a myriad of sensors, giving them hello ability tootrack and monitor millions of events every second.</span></span> <span data-ttu-id="33eee-108">We verwachten dat door 2020, de meeste van deze auto's wordt zijn verbonden toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="33eee-108">We expect that by 2020, most of these cars will have been connected toohello Internet.</span></span> <span data-ttu-id="33eee-109">Stel dat u toegang te krijgen tot deze schat aan gegevens tooprovide groter veiligheid, betrouwbaarheid en een beter aangedreven ervaring!</span><span class="sxs-lookup"><span data-stu-id="33eee-109">Imagine tapping into this wealth of data tooprovide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="33eee-110">Microsoft heeft gesteld dat dit een situatie met Cortana Intelligence aan het einde.</span><span class="sxs-lookup"><span data-stu-id="33eee-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="33eee-111">Microsoft Cortana Intelligence is een volledig beheerde big data en advanced analytics suite waarmee u tootransform uw gegevens in intelligent actie.</span><span class="sxs-lookup"><span data-stu-id="33eee-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you tootransform your data into intelligent action.</span></span> <span data-ttu-id="33eee-112">We willen toointroduce toohello Cortana Intelligence Vehicle telemetrie Analytics oplossingssjabloon.</span><span class="sxs-lookup"><span data-stu-id="33eee-112">We want toointroduce you toohello Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="33eee-113">Deze oplossing wordt gedemonstreerd hoe auto dealerbedrijven, auto fabrikanten en ondernemingen Hallo-mogelijkheden van Cortana Intelligence toogain realtime gebruiken kunnen en gewoonten voorspellende insights op de drager gezondheid en groot.</span><span class="sxs-lookup"><span data-stu-id="33eee-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="33eee-114">Hallo-oplossing is geïmplementeerd als een [lambda architectuur patroon](https://en.wikipedia.org/wiki/Lambda_architecture) met Hallo mogelijkheden van Hallo Cortana Intelligence platform voor realtime en batchverwerking.</span><span class="sxs-lookup"><span data-stu-id="33eee-114">hello solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing hello full potential of hello Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="33eee-115">Hallo-oplossing:</span><span class="sxs-lookup"><span data-stu-id="33eee-115">hello solution:</span></span> 

* <span data-ttu-id="33eee-116">biedt een simulator Vehicle telematica</span><span class="sxs-lookup"><span data-stu-id="33eee-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="33eee-117">maakt gebruik van Event Hubs voor het opnemen van miljoenen gesimuleerde vehicle telemetrische gebeurtenissen in Azure</span><span class="sxs-lookup"><span data-stu-id="33eee-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="33eee-118">maakt gebruik van Stream Analytics toogain realtime-inzichten op vehicle health</span><span class="sxs-lookup"><span data-stu-id="33eee-118">uses Stream Analytics toogain real-time insights on vehicle health</span></span>
* <span data-ttu-id="33eee-119">persistente gegevens Hallo in langdurige opslag voor uitgebreidere batch analyses.</span><span class="sxs-lookup"><span data-stu-id="33eee-119">persists hello data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="33eee-120">maakt gebruik van Machine Learning voor afwijkingsdetectie in realtime en batch-verwerking toogain voorspellende insights.</span><span class="sxs-lookup"><span data-stu-id="33eee-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="33eee-121">maakt gebruik van HDInsight tootransform gegevens op schaal en Data Factory toohandle orchestration, planning, bronbeheer en bewaking van de pipeline voor Hallo batch verwerkt</span><span class="sxs-lookup"><span data-stu-id="33eee-121">leverages HDInsight tootransform data at scale and Data Factory toohandle orchestration, scheduling, resource management, and monitoring of hello batch processing pipeline</span></span> 
* <span data-ttu-id="33eee-122">een uitgebreide dashboard van deze oplossing biedt voor realtime-gegevens en predictive analytics visualisaties met Power BI</span><span class="sxs-lookup"><span data-stu-id="33eee-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="33eee-123">Architectuur</span><span class="sxs-lookup"><span data-stu-id="33eee-123">Architecture</span></span>
<span data-ttu-id="33eee-124">![Architectuurdiagram van de oplossing](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*afbeelding 1 – architectuur Vehicle telemetrie Analytics-oplossing*</span><span class="sxs-lookup"><span data-stu-id="33eee-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="33eee-125">Deze oplossing omvat Hallo volgende **Cortana Intelligence-onderdelen** en gepresenteerd hun end tooend integratie:</span><span class="sxs-lookup"><span data-stu-id="33eee-125">This solution includes hello following **Cortana Intelligence components** and showcases their end tooend integration:</span></span>

* <span data-ttu-id="33eee-126">**Event Hubs** voor het opnemen van miljoenen vehicle telemetrische gebeurtenissen in Azure.</span><span class="sxs-lookup"><span data-stu-id="33eee-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="33eee-127">**Stream Analytics** voor realtime-inzichten op vehicle gezondheid en dat de gegevens zich blijft voordoen in langdurige opslag voor uitgebreidere batch analyses.</span><span class="sxs-lookup"><span data-stu-id="33eee-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="33eee-128">**Machine Learning** voor afwijkingsdetectie in realtime en batchverwerking toogain voorspellende insights.</span><span class="sxs-lookup"><span data-stu-id="33eee-128">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="33eee-129">**HDInsight** gegevens over tootransform op grote schaal is</span><span class="sxs-lookup"><span data-stu-id="33eee-129">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="33eee-130">**Data Factory** verwerkt orchestration, planning, bronbeheer en controle van de pipeline voor Hallo batch verwerkt.</span><span class="sxs-lookup"><span data-stu-id="33eee-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>
* <span data-ttu-id="33eee-131">**Power BI** biedt deze oplossing een uitgebreide dashboard voor realtime-gegevens en visualisaties predictive analytics.</span><span class="sxs-lookup"><span data-stu-id="33eee-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="33eee-132">Deze oplossing gebruikt twee verschillende **gegevensbronnen**:</span><span class="sxs-lookup"><span data-stu-id="33eee-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="33eee-133">**Vehicle signalen en diagnostische gegevens in de simulatie**: een vehicle telematica simulator verzendt de diagnostische gegevens en signalen die overeenkomen met toohello status van Hallo vehicle en Hallo besturen patroon op een bepaald tijdstip.</span><span class="sxs-lookup"><span data-stu-id="33eee-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond toohello state of hello vehicle and hello driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="33eee-134">**Vehicle catalogus**: een verwijzingsgegevensset met een Chassisnummer toomodel-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="33eee-134">**Vehicle catalog**: A reference dataset containing a VIN toomodel mapping.</span></span>


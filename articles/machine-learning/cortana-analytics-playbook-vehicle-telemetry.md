---
title: Vehicle health voorspellen en die zorg draagt gewoonten - Azure | Microsoft Docs
description: De mogelijkheden van Cortana Intelligence gebruiken om inzicht in real-time en voorspeld op vehicle status en verkeer te krijgen gewoonten.
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
ms.openlocfilehash: d202d314c61416cf306f760f93e0a4a88a1ab42b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="d0f5a-103">Draaiboek met oplossingen voor voertuigtelemetrieanalyse</span><span class="sxs-lookup"><span data-stu-id="d0f5a-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="d0f5a-104">Dit **menu** koppelingen naar de hoofdstukken in deze playbook.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="d0f5a-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d0f5a-105">Overview</span></span>
<span data-ttu-id="d0f5a-106">Super computers worden buiten de testomgeving hebt verplaatst en nu in onze garage!</span><span class="sxs-lookup"><span data-stu-id="d0f5a-106">Super computers have moved out of the lab and are now parked in our garage!</span></span> <span data-ttu-id="d0f5a-107">Deze geavanceerde auto's bevatten een groot aantal sensoren, waardoor ze in staat te volgen en controleren van miljoenen gebeurtenissen per seconde.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-107">These cutting-edge automobiles contain a myriad of sensors, giving them the ability to track and monitor millions of events every second.</span></span> <span data-ttu-id="d0f5a-108">We verwachten dat door 2020, de meeste van deze auto's wordt hebt is verbonden met Internet.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-108">We expect that by 2020, most of these cars will have been connected to the Internet.</span></span> <span data-ttu-id="d0f5a-109">Stel dat u toegang te krijgen tot deze schat aan gegevens voor meer veiligheid, betrouwbaarheid en een beter aangedreven ervaring!</span><span class="sxs-lookup"><span data-stu-id="d0f5a-109">Imagine tapping into this wealth of data to provide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="d0f5a-110">Microsoft heeft gesteld dat dit een situatie met Cortana Intelligence aan het einde.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="d0f5a-111">Microsoft Cortana Intelligence is een volledig beheerde big data en geavanceerde analyses suite waarmee u uw gegevens transformeren naar intelligent actie.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you to transform your data into intelligent action.</span></span> <span data-ttu-id="d0f5a-112">We willen u kennis met de sjabloon Cortana Intelligence Vehicle telemetrie Analytics-oplossing.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-112">We want to introduce you to the Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="d0f5a-113">Deze oplossing wordt gedemonstreerd hoe auto dealerbedrijven, auto fabrikanten en ondernemingen de mogelijkheden van Cortana Intelligence gebruiken kunnen om te krijgen realtime en gewoonten voorspellende insights op de drager gezondheid en groot.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="d0f5a-114">De oplossing is geïmplementeerd als een [lambda architectuur patroon](https://en.wikipedia.org/wiki/Lambda_architecture) met de volledige potentiële van de Cortana Intelligence-platform voor realtime en batchverwerking.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-114">The solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing the full potential of the Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="d0f5a-115">De oplossing:</span><span class="sxs-lookup"><span data-stu-id="d0f5a-115">The solution:</span></span> 

* <span data-ttu-id="d0f5a-116">biedt een simulator Vehicle telematica</span><span class="sxs-lookup"><span data-stu-id="d0f5a-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="d0f5a-117">maakt gebruik van Event Hubs voor het opnemen van miljoenen gesimuleerde vehicle telemetrische gebeurtenissen in Azure</span><span class="sxs-lookup"><span data-stu-id="d0f5a-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="d0f5a-118">Stream Analytics gebruikt om te verkrijgen van realtime-inzichten op vehicle health</span><span class="sxs-lookup"><span data-stu-id="d0f5a-118">uses Stream Analytics to gain real-time insights on vehicle health</span></span>
* <span data-ttu-id="d0f5a-119">de gegevens persistente in langdurige opslag voor uitgebreidere batch analytics.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-119">persists the data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="d0f5a-120">maakt gebruik van Machine Learning voor afwijkingsdetectie in realtime en batchverwerking om voorspellende inzicht krijgen.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="d0f5a-121">maakt gebruik van HDInsight voor het transformeren van gegevens op grote schaal en Data Factory om af te handelen orchestration, planning, bronbeheer en bewaking van de pipeline batch verwerkt</span><span class="sxs-lookup"><span data-stu-id="d0f5a-121">leverages HDInsight to transform data at scale and Data Factory to handle orchestration, scheduling, resource management, and monitoring of the batch processing pipeline</span></span> 
* <span data-ttu-id="d0f5a-122">een uitgebreide dashboard van deze oplossing biedt voor realtime-gegevens en predictive analytics visualisaties met Power BI</span><span class="sxs-lookup"><span data-stu-id="d0f5a-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="d0f5a-123">Architectuur</span><span class="sxs-lookup"><span data-stu-id="d0f5a-123">Architecture</span></span>
<span data-ttu-id="d0f5a-124">![Architectuurdiagram van de oplossing](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*afbeelding 1 – architectuur Vehicle telemetrie Analytics-oplossing*</span><span class="sxs-lookup"><span data-stu-id="d0f5a-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="d0f5a-125">Deze oplossing omvat het volgende **Cortana Intelligence-onderdelen** en gepresenteerd hun end-to-end-integratie:</span><span class="sxs-lookup"><span data-stu-id="d0f5a-125">This solution includes the following **Cortana Intelligence components** and showcases their end to end integration:</span></span>

* <span data-ttu-id="d0f5a-126">**Event Hubs** voor het opnemen van miljoenen vehicle telemetrische gebeurtenissen in Azure.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="d0f5a-127">**Stream Analytics** voor realtime-inzichten op vehicle gezondheid en dat de gegevens zich blijft voordoen in langdurige opslag voor uitgebreidere batch analyses.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="d0f5a-128">**Machine Learning** voor afwijkingsdetectie in realtime en batchverwerking om voorspellende inzicht te krijgen.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-128">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="d0f5a-129">**HDInsight** wordt gebruikt voor het transformeren van gegevens op grote schaal</span><span class="sxs-lookup"><span data-stu-id="d0f5a-129">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="d0f5a-130">**Data Factory** orchestration, planning, bronbeheer en controle van de pijplijn batchverwerking verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>
* <span data-ttu-id="d0f5a-131">**Power BI** biedt deze oplossing een uitgebreide dashboard voor realtime-gegevens en visualisaties predictive analytics.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="d0f5a-132">Deze oplossing gebruikt twee verschillende **gegevensbronnen**:</span><span class="sxs-lookup"><span data-stu-id="d0f5a-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="d0f5a-133">**Vehicle signalen en diagnostische gegevens in de simulatie**: een vehicle telematica simulator verzendt de diagnostische gegevens en signalen die overeenkomen met de status van de drager en het aangedreven patroon op een bepaald tijdstip.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond to the state of the vehicle and the driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="d0f5a-134">**Vehicle catalogus**: een verwijzingsgegevensset met een Chassisnummer toewijzing van het model.</span><span class="sxs-lookup"><span data-stu-id="d0f5a-134">**Vehicle catalog**: A reference dataset containing a VIN to model mapping.</span></span>


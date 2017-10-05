---
title: Voorspeld onderhoud vooraf geconfigureerde oplossing | Microsoft Docs
description: Een beschrijving van de vooraf geconfigureerde oplossing van Azure IoT Suite voor voorspeld onderhoud.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 8bad198488c4940a83eb32ec02122a91d47ca86c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="aac7a-103">Overzicht van de vooraf geconfigureerde oplossing voor voorspeld onderhoud</span><span class="sxs-lookup"><span data-stu-id="aac7a-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="aac7a-104">De [vooraf geconfigureerde oplossing][lnk_preconfigured_solutions] voor *voorspellend onderhoud* is een van de vooraf geconfigureerde oplossingen van [Microsoft Azure IoT Suite][lnk_iot_suite].</span><span class="sxs-lookup"><span data-stu-id="aac7a-104">The *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of the [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="aac7a-105">Deze oplossing integreert het in realtime verzamelen van telemetriegegevens met een voorspellend model dat is gemaakt met behulp van [Azure Machine Learning][lnk-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="aac7a-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="aac7a-106">Met Azure IoT Suite kunt u snel en eenvoudig verbinding maken met assets en deze controleren, en telemetriegegevens in realtime analyseren in dashboards en visualisaties.</span><span class="sxs-lookup"><span data-stu-id="aac7a-106">With Azure IoT Suite, you can quickly and easily connect to and monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="aac7a-107">De oplossing voor predictief onderhoud bevat dashboards en visualisaties om u nieuwe bedrijfsinformatie te bieden waardoor u efficiënter kunt werken en meer inkomsten kunt genereren.</span><span class="sxs-lookup"><span data-stu-id="aac7a-107">In the predictive maintenance solution, the dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="the-scenario"></a><span data-ttu-id="aac7a-108">Het scenario</span><span class="sxs-lookup"><span data-stu-id="aac7a-108">The Scenario</span></span>

<span data-ttu-id="aac7a-109">Fabrikam is een regionale luchtvaartmaatschappij die zich toelegt op het leveren van een uitstekende klantervaring tegen concurrerende prijzen.</span><span class="sxs-lookup"><span data-stu-id="aac7a-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="aac7a-110">Een oorzaak van vertragingen zijn onderhoudsproblemen, waarbij het onderhoud van vliegtuigmotoren een bijzondere uitdaging vormt.</span><span class="sxs-lookup"><span data-stu-id="aac7a-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="aac7a-111">Motorproblemen tijdens de vlucht moeten koste wat kost worden voorkomen. Fabrikam inspecteert om die reden regelmatig de motoren en volgt een planning voor het plegen van onderhoud.</span><span class="sxs-lookup"><span data-stu-id="aac7a-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according to a plan.</span></span> <span data-ttu-id="aac7a-112">Vliegtuigmotoren slijten echter niet allemaal even snel.</span><span class="sxs-lookup"><span data-stu-id="aac7a-112">However, aircraft engines don’t always wear the same.</span></span> <span data-ttu-id="aac7a-113">Soms wordt er onnodig onderhoud uitgevoerd op motoren.</span><span class="sxs-lookup"><span data-stu-id="aac7a-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="aac7a-114">En wat belangrijker is, er doen zich soms problemen voor die ervoor zorgen dat een vliegtuig aan de grond moet blijven totdat het onderhoud is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="aac7a-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="aac7a-115">Deze problemen kunnen erg kostbaar zijn, in het bijzonder als een vliegtuig zich op een locatie bevindt waar de juiste technici of onderdelen niet beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="aac7a-115">If an aircraft is at a location where the right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="aac7a-116">De motoren van de vliegtuigen van Fabrikam zijn uitgerust met sensoren die de toestand van de motor tijdens de vlucht in de gaten houden.</span><span class="sxs-lookup"><span data-stu-id="aac7a-116">The engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="aac7a-117">Fabrikam maakt gebruik van de oplossing voor predictief onderhoud voor het verzamelen van de sensorgegevens die tijdens de vlucht worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="aac7a-117">Fabrikam uses the predictive maintenance solution to collect the sensor data collected during the flight.</span></span> <span data-ttu-id="aac7a-118">Na jarenlang operationele gegevens van engines te hebben verzameld, hebben de gegevensanalisten van Fabrikam een model samengesteld waarmee ze de nog resterende bruikbare levensduur van een vliegtuigmotor kunnen voorspellen.</span><span class="sxs-lookup"><span data-stu-id="aac7a-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way to predict the Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="aac7a-119">Het model gebruikt een correlatie tussen gegevens van vier van de motorsensoren en de slijtage van de motor die uiteindelijk tot problemen leidt.</span><span class="sxs-lookup"><span data-stu-id="aac7a-119">The model uses a correlation between data from four of the engine sensors and engine wear that leads to eventual failure.</span></span> <span data-ttu-id="aac7a-120">Hoewel Fabrikam doorgaat met het uitvoeren van regelmatige inspecties om de veiligheid te garanderen, kan het bedrijf nu de modellen gebruiken om na elke vlucht de resterende bruikbare levensduur van elke motor te berekenen.</span><span class="sxs-lookup"><span data-stu-id="aac7a-120">While Fabrikam continues to perform regular inspections to ensure safety, it can now use the models to compute the RUL for each engine after every flight.</span></span> <span data-ttu-id="aac7a-121">Het model gebruikt de telemetrie die tijdens de vlucht vanuit de machines is verzameld.</span><span class="sxs-lookup"><span data-stu-id="aac7a-121">The model uses the telemetry collected from the engines during the flight.</span></span> <span data-ttu-id="aac7a-122">Fabrikam is nu in staat om toekomstige probleempunten te voorspellen en om van tevoren onderhoud en reparatiewerkzaamheden te plannen.</span><span class="sxs-lookup"><span data-stu-id="aac7a-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="aac7a-123">Het model van de oplossing maakt gebruik van de reële slijtagegegevens van de motor.</span><span class="sxs-lookup"><span data-stu-id="aac7a-123">The solution model uses actual engine wear data.</span></span>

<span data-ttu-id="aac7a-124">Door het punt te voorspellen waarop onderhoud vereist is, kan Fabrikam zijn activiteiten zo optimaliseren dat de kosten worden verminderd.</span><span class="sxs-lookup"><span data-stu-id="aac7a-124">By predicting the point when maintenance is required, Fabrikam can optimize its operations to reduce costs.</span></span>

<span data-ttu-id="aac7a-125">Onderhoudscoördinatoren werken met planners:</span><span class="sxs-lookup"><span data-stu-id="aac7a-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="aac7a-126">Om onderhoud zo te plannen dat dit samenvalt met een moment waarop een vliegtuig op een bepaalde locatie aan de grond staat.</span><span class="sxs-lookup"><span data-stu-id="aac7a-126">Plan maintenance to coincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="aac7a-127">Om ervoor te zorgen dat er voldoende tijd is om het vliegtuig buiten bedrijf te stellen zonder het vliegschema te verstoren.</span><span class="sxs-lookup"><span data-stu-id="aac7a-127">Ensure sufficient time is available for the aircraft to be out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="aac7a-128">Om technici zo in te plannen dat het onderhoud van het vliegtuig efficiënt en wordt uitgevoerd zonder dat er vertragingen ontstaan.</span><span class="sxs-lookup"><span data-stu-id="aac7a-128">To schedule technicians to ensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="aac7a-129">Magazijnbeheerders ontvangen de onderhoudsplannen zodat zij hun bestelproces en hun voorraad met reserveonderdelen kunnen optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="aac7a-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="aac7a-130">Door deze activiteiten is Fabrikam in staat om de tijd die vliegtuigen aan de grond staan te minimaliseren, de operationele kosten te verlagen en kan het bedrijf de veiligheid van de passagiers en bemanning garanderen.</span><span class="sxs-lookup"><span data-stu-id="aac7a-130">These activities enable Fabrikam to minimize aircraft ground time and reduce operating costs while ensuring the safety of passengers and crew.</span></span>

<span data-ttu-id="aac7a-131">Als u beter wilt begrijpen welke mogelijkheden [Azure IoT Suite][lnk_iot_suite] biedt die klanten nodig hebben om het potentieel van voorspellend onderhoud te realiseren, bekijkt u deze [infographic][lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="aac7a-131">To understand how [Azure IoT Suite][lnk_iot_suite] provides the capabilities customers need to realize the potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-the-predictive-maintenance-solution-is-built"></a><span data-ttu-id="aac7a-132">Hoe de oplossing voor voorspeld onderhoud is gebouwd</span><span class="sxs-lookup"><span data-stu-id="aac7a-132">How the predictive maintenance solution is built</span></span>

<span data-ttu-id="aac7a-133">De oplossing gebruikt een bestaand Azure Machine Learning-model dat als sjabloon beschikbaar is om te laten zien hoe deze mogelijkheden werken op basis van telemetriegegevens die zijn verzameld via IoT Suite-services.</span><span class="sxs-lookup"><span data-stu-id="aac7a-133">The solution uses an existing Azure Machine Learning model available as a template to show these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="aac7a-134">Microsoft heeft een [regressiemodel][lnk_regression_model] van een vliegtuigmotor ontwikkeld op basis van algemeen beschikbare gegevens<sup>\[1\]</sup>, evenals richtlijnen met stappen voor het gebruik van het model.</span><span class="sxs-lookup"><span data-stu-id="aac7a-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how to use the model.</span></span>

<span data-ttu-id="aac7a-135">De Azure IoT-oplossing voor predictief onderhoud maakt gebruik van het regressiemodel dat op basis van deze sjabloon is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aac7a-135">The Azure IoT predictive maintenance solution uses the regression model created from this template.</span></span> <span data-ttu-id="aac7a-136">Het model is geïmplementeerd in uw Azure-abonnement en is toegankelijk via een automatisch gegenereerde API.</span><span class="sxs-lookup"><span data-stu-id="aac7a-136">The model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="aac7a-137">De oplossing omvat een subset met de testgegevens voor 4 (van in totaal 100) motoren en de 4 (van in totaal 21) gegevensstromen van sensoren.</span><span class="sxs-lookup"><span data-stu-id="aac7a-137">The solution includes a subset of the testing data representing 4 (of 100 total) engines and the 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="aac7a-138">Deze gegevens leveren een accuraat resultaat op van het getrainde model.</span><span class="sxs-lookup"><span data-stu-id="aac7a-138">This data is sufficient to provide an accurate result from the trained model.</span></span>

<span data-ttu-id="aac7a-139">*\[1\] A. Saxena en K. Goebel (2008). 'Turbofan Engine Degradation Simulation Data Set', NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span><span class="sxs-lookup"><span data-stu-id="aac7a-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="aac7a-140">Aan de slag met voorspellend onderhoud</span><span class="sxs-lookup"><span data-stu-id="aac7a-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="aac7a-141">In deze zelfstudie ziet u hoe u de oplossing voor voorspellend onderhoud inricht.</span><span class="sxs-lookup"><span data-stu-id="aac7a-141">This tutorial shows you how to provision the predictive maintenance solution.</span></span> <span data-ttu-id="aac7a-142">U maakt u kennis met de basisfuncties van de oplossing voor voorspellend onderhoud.</span><span class="sxs-lookup"><span data-stu-id="aac7a-142">It also walks you through the basic features of the predictive maintenance solution.</span></span> <span data-ttu-id="aac7a-143">U krijgt toegang tot deze functies via het oplossingsdashboard dat samen met de vooraf geconfigureerde oplossing het volgende implementeert.</span><span class="sxs-lookup"><span data-stu-id="aac7a-143">You can access many of these features through the solution dashboard that deploys along with the preconfigured solution.</span></span>

<span data-ttu-id="aac7a-144">U hebt een actief Azure-abonnement nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="aac7a-144">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="aac7a-145">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="aac7a-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="aac7a-146">Zie [Gratis proefversie van Azure][lnk_free_trial] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="aac7a-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="aac7a-147">Meld u aan bij [azureiotsuite.com][lnk-azureiotsuite] met de referenties van uw Azure-account en klik op **+** om een oplossing te maken.</span><span class="sxs-lookup"><span data-stu-id="aac7a-147">Log on to [azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** to create a solution.</span></span>
1. <span data-ttu-id="aac7a-148">Klik in de tegel **Voorspellend onderhoud** op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="aac7a-148">Click **Select** the **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="aac7a-149">Voer een **Naam van oplossing** in voor uw vooraf geconfigureerde oplossing voor voorspellend onderhoud.</span><span class="sxs-lookup"><span data-stu-id="aac7a-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="aac7a-150">Selecteer de **regio** die en het **abonnement** dat u wilt gebruiken voor het inrichten van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="aac7a-150">Select the **Region** and **Subscription** you want to use to provision the solution.</span></span>
1. <span data-ttu-id="aac7a-151">Klik op **Oplossing maken** om het inrichtingsproces te starten.</span><span class="sxs-lookup"><span data-stu-id="aac7a-151">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="aac7a-152">Doorgaans duurt het enkele minuten om dit proces uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="aac7a-152">This process typically takes several minutes to run.</span></span>

### <a name="wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="aac7a-153">Wacht tot het inrichtingsproces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="aac7a-153">Wait for the provisioning process to complete</span></span>

1. <span data-ttu-id="aac7a-154">Klik op de tegel voor uw oplossing met de status **Inrichten**.</span><span class="sxs-lookup"><span data-stu-id="aac7a-154">Click the tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="aac7a-155">Tijdens de implementatie van Azure-services in uw Azure-abonnement verschijnen verschillende **inrichtingstatuswaarden**.</span><span class="sxs-lookup"><span data-stu-id="aac7a-155">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="aac7a-156">Nadat het inrichten is voltooid, verandert de status in **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="aac7a-156">Once provisioning completes, the status changes to **Ready**.</span></span>
1. <span data-ttu-id="aac7a-157">Klik op de tegel om de details van uw oplossing in het rechterdeelvenster weer te geven.</span><span class="sxs-lookup"><span data-stu-id="aac7a-157">Click the tile to see the details of your solution in the right-hand pane.</span></span> <span data-ttu-id="aac7a-158">In dit deelvenster kunt u het oplossingsdashboard starten en toegang krijgen tot de Machine Learning-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="aac7a-158">From this pane, you can launch the solution dashboard and access the Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="aac7a-159">Als er problemen zijn met de implementatie van de vooraf geconfigureerde oplossing, leest u [Machtigingen op azureiotsuite.com][lnk-permissions] en de [veelgestelde vragen][lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="aac7a-159">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [FAQ][lnk-faq].</span></span> <span data-ttu-id="aac7a-160">Als de problemen zich blijven voordoen, maakt u een serviceticket aan in de [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="aac7a-160">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>

<span data-ttu-id="aac7a-161">Zijn er voor uw oplossing bepaalde details niet vermeld, die u wel verwacht had te zien?</span><span class="sxs-lookup"><span data-stu-id="aac7a-161">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="aac7a-162">Geef ons suggesties voor functies op [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="aac7a-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-the-solution"></a><span data-ttu-id="aac7a-163">De oplossing bekijken</span><span class="sxs-lookup"><span data-stu-id="aac7a-163">View the solution</span></span>

<span data-ttu-id="aac7a-164">Deze sectie helpt u bij de gebruikersinterface van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="aac7a-164">This section guides you through the solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="aac7a-165">Dashboard voorspeld onderhoud</span><span class="sxs-lookup"><span data-stu-id="aac7a-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="aac7a-166">Voor deze pagina in de webtoepassing wordt gebruikgemaakt van PowerBI JavaScript-besturingselementen (zie de [PowerBI-opslagplaats voor visualisaties][lnk-powerbi]) voor het visualiseren van:</span><span class="sxs-lookup"><span data-stu-id="aac7a-166">This page in the web application uses PowerBI JavaScript controls (see the [PowerBI-visuals repository][lnk-powerbi]) to visualize:</span></span>

* <span data-ttu-id="aac7a-167">De uitvoergegevens van de Stream Analytics-jobs in Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="aac7a-167">The output data from the Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="aac7a-168">De resterende levensduur en aantal cycli per vliegtuigmotor.</span><span class="sxs-lookup"><span data-stu-id="aac7a-168">The RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-the-behavior-of-the-cloud-solution"></a><span data-ttu-id="aac7a-169">Het gedrag van de cloudoplossing observeren</span><span class="sxs-lookup"><span data-stu-id="aac7a-169">Observing the behavior of the cloud solution</span></span>

<span data-ttu-id="aac7a-170">Navigeer in Azure Portal naar de resourcegroep met de naam van de oplossing die u hebt gekozen om de ingerichte resources weer te geven.</span><span class="sxs-lookup"><span data-stu-id="aac7a-170">In the Azure portal, navigate to the resource group with the solution name you chose to view your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="aac7a-171">Wanneer u de vooraf geconfigureerde oplossing inricht, krijgt u een e-mailbericht met een koppeling naar de Machine Learning-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="aac7a-171">When you provision the preconfigured solution, you receive an email with a link to the Machine Learning workspace.</span></span> <span data-ttu-id="aac7a-172">U kunt ook naar de Machine Learning-werkruimte navigeren vanaf de [azureiotsuite.com][lnk-azureiotsuite]-pagina voor de ingerichte oplossing.</span><span class="sxs-lookup"><span data-stu-id="aac7a-172">You can also navigate to the Machine Learning workspace from the [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="aac7a-173">Op deze pagina is een tegel beschikbaar wanneer de oplossing de status **Gereed** heeft.</span><span class="sxs-lookup"><span data-stu-id="aac7a-173">A tile is available on this page when the solution is in the **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="aac7a-174">In de oplossingsportal kunt u zien dat het voorbeeld is ingericht met vier gesimuleerde apparaten die twee vliegtuigen met twee motoren per vliegtuig vertegenwoordigen, elk met vier sensoren.</span><span class="sxs-lookup"><span data-stu-id="aac7a-174">In the solution portal, you can see that the sample is provisioned with four simulated devices to represent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="aac7a-175">Wanneer u voor het eerst naar de oplossingsportal navigeert, wordt de simulatie gestopt.</span><span class="sxs-lookup"><span data-stu-id="aac7a-175">When you first navigate to the solution portal, the simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="aac7a-176">Klik op **Simulatie starten** om te beginnen met de simulatie.</span><span class="sxs-lookup"><span data-stu-id="aac7a-176">Click **Start simulation** to begin the simulation.</span></span> <span data-ttu-id="aac7a-177">Het dashboard wordt ingevuld met de sensorgeschiedenis, de resterende levensduur, de cycli en de geschiedenis van de resterende levensduur.</span><span class="sxs-lookup"><span data-stu-id="aac7a-177">The sensor history, RUL, Cycles, and RUL history populate the dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="aac7a-178">Wanneer de resterende levensduur minder dan 160 is (een willekeurige drempelwaarde gekozen ter illustratie), verschijnt in de oplossingsportal een waarschuwingssymbool naast de weergegeven resterende levensduur.</span><span class="sxs-lookup"><span data-stu-id="aac7a-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), the solution portal displays a warning symbol next to the RUL display.</span></span> <span data-ttu-id="aac7a-179">De oplossingsportal geeft ook de vliegtuigmotor geel gemarkeerd weer.</span><span class="sxs-lookup"><span data-stu-id="aac7a-179">The solution portal also highlights the aircraft engine in yellow.</span></span> <span data-ttu-id="aac7a-180">Zoals u merkt, vertonen de waarden van de resterende levensduur een algemene neerwaartse trend, maar stijgen en dalen die waarden vaak.</span><span class="sxs-lookup"><span data-stu-id="aac7a-180">Notice how the RUL values have a general downward trend overall, but tend to bounce up and down.</span></span> <span data-ttu-id="aac7a-181">Dit gedrag wordt veroorzaakt door de verschillende lengten van de cycli en de nauwkeurigheid van het model.</span><span class="sxs-lookup"><span data-stu-id="aac7a-181">This behavior results from the varying cycle lengths and the model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="aac7a-182">Het duurt ongeveer 35 minuten voordat de volledige simulatie 148 cycli heeft voltooid.</span><span class="sxs-lookup"><span data-stu-id="aac7a-182">The full simulation takes around 35 minutes to complete 148 cycles.</span></span> <span data-ttu-id="aac7a-183">Na ongeveer 5 minuten wordt voor het eerst de drempelwaarde van 160 voor de resterende levensduur bereikt. De drempelwaarde voor beide motoren wordt na ongeveer 8 minuten bereikt.</span><span class="sxs-lookup"><span data-stu-id="aac7a-183">The 160 RUL threshold is met for the first time at around 5 minutes and both engines hit the threshold at around 8 minutes.</span></span>

<span data-ttu-id="aac7a-184">De simulatie wordt uitgevoerd voor de volledige gegevensset voor 148 cycli en bepaalt dan het eindresultaat voor de resterende levensduur en het aantal cycli.</span><span class="sxs-lookup"><span data-stu-id="aac7a-184">The simulation runs through the complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="aac7a-185">U kunt de simulatie op elk punt stoppen, maar wanneer u op **Simulatie starten** klikt, wordt de simulatie opnieuw vanaf het begin van de gegevensset uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="aac7a-185">You can stop the simulation at any point, but clicking **Start Simulation** replays the simulation from the start of the dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aac7a-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aac7a-186">Next steps</span></span>

<span data-ttu-id="aac7a-187">Meer informatie hoe Azure IoT werkt in scenario's voor voorspellend onderhoud vindt u in [Capture value from the Internet of Things][lnk_capture_value] (Waarde toevoegen via het Internet of Things).</span><span class="sxs-lookup"><span data-stu-id="aac7a-187">To learn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from the Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="aac7a-188">Volg een [walkthrough][lnk-predictive-walkthrough] over de oplossing voor predictief onderhoud.</span><span class="sxs-lookup"><span data-stu-id="aac7a-188">Take a [walkthrough][lnk-predictive-walkthrough] of the predictive maintenance solution.</span></span>

<span data-ttu-id="aac7a-189">U kunt ook enkele van de andere functies en mogelijkheden van de vooraf geconfigureerde IoT Suite-oplossingen verkennen:</span><span class="sxs-lookup"><span data-stu-id="aac7a-189">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="aac7a-190">[Veelgestelde vragen over IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="aac7a-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="aac7a-191">[Fundamentele IoT-beveiliging][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="aac7a-191">[IoT security from the ground up][lnk-security-groundup]</span></span>

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/
---
title: aaaPredictive onderhoud vooraf geconfigureerde oplossing | Microsoft Docs
description: Een beschrijving van hello Azure IoT Suite voorspeld onderhoud vooraf geconfigureerde oplossing.
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
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="40083-103">Overzicht van de vooraf geconfigureerde oplossing voor voorspeld onderhoud</span><span class="sxs-lookup"><span data-stu-id="40083-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="40083-104">Hallo *voorspeld onderhoud* [vooraf geconfigureerde oplossing] [ lnk_preconfigured_solutions] is een Hallo [Microsoft Azure IoT Suite] [ lnk_iot_suite] vooraf geconfigureerde oplossingen.</span><span class="sxs-lookup"><span data-stu-id="40083-104">hello *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of hello [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="40083-105">Deze oplossing integreert het in realtime verzamelen van telemetriegegevens met een voorspellend model dat is gemaakt met behulp van [Azure Machine Learning][lnk-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="40083-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="40083-106">Met Azure IoT Suite u snel en eenvoudig verbinding kunt tooand monitor activa, en analyseren van telemetrie in realtime in dashboards en visualisaties.</span><span class="sxs-lookup"><span data-stu-id="40083-106">With Azure IoT Suite, you can quickly and easily connect tooand monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="40083-107">In de oplossing voor voorspeld onderhoud hello bieden Hallo dashboards en visualisaties u nieuwe bedrijfsinformatie die kan efficiënter en meer inkomsten kunnen genereren.</span><span class="sxs-lookup"><span data-stu-id="40083-107">In hello predictive maintenance solution, hello dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="hello-scenario"></a><span data-ttu-id="40083-108">Hallo Scenario</span><span class="sxs-lookup"><span data-stu-id="40083-108">hello Scenario</span></span>

<span data-ttu-id="40083-109">Fabrikam is een regionale luchtvaartmaatschappij die zich toelegt op het leveren van een uitstekende klantervaring tegen concurrerende prijzen.</span><span class="sxs-lookup"><span data-stu-id="40083-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="40083-110">Een oorzaak van vertragingen zijn onderhoudsproblemen, waarbij het onderhoud van vliegtuigmotoren een bijzondere uitdaging vormt.</span><span class="sxs-lookup"><span data-stu-id="40083-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="40083-111">Fabrikam moet voorkomen motoren ontstaan tijdens de vlucht ten koste wat kost dus regelmatig de motoren inspecteert en gepland onderhoud op basis van tooa plan.</span><span class="sxs-lookup"><span data-stu-id="40083-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according tooa plan.</span></span> <span data-ttu-id="40083-112">Vliegtuig engines niet slijten Hallo echter hetzelfde.</span><span class="sxs-lookup"><span data-stu-id="40083-112">However, aircraft engines don’t always wear hello same.</span></span> <span data-ttu-id="40083-113">Soms wordt er onnodig onderhoud uitgevoerd op motoren.</span><span class="sxs-lookup"><span data-stu-id="40083-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="40083-114">En wat belangrijker is, er doen zich soms problemen voor die ervoor zorgen dat een vliegtuig aan de grond moet blijven totdat het onderhoud is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="40083-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="40083-115">Als een vliegtuig zich op een locatie kunnen waar Hallo juiste technici of onderdelen zijn niet beschikbaar, deze problemen bijzonder kostbaar.</span><span class="sxs-lookup"><span data-stu-id="40083-115">If an aircraft is at a location where hello right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="40083-116">Hallo-engines van de vliegtuigen van Fabrikam zijn uitgerust met sensoren die motor tijdens de vlucht bewaken.</span><span class="sxs-lookup"><span data-stu-id="40083-116">hello engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="40083-117">Fabrikam gebruikt Hallo voorspeld onderhoud oplossing toocollect Hallo sensorgegevens die zijn verzameld tijdens de vlucht Hallo.</span><span class="sxs-lookup"><span data-stu-id="40083-117">Fabrikam uses hello predictive maintenance solution toocollect hello sensor data collected during hello flight.</span></span> <span data-ttu-id="40083-118">Na jarenlang van operationele-engine en gegevens hebt verzameld van Fabrikam een manier toopredict Hallo resterende levensduur (resterende Levensduur) van een vliegtuigmotor gemodelleerd.</span><span class="sxs-lookup"><span data-stu-id="40083-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way toopredict hello Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="40083-119">Hallo-model maakt gebruik van een correlatie tussen gegevens van vier hello motorsensoren en de slijtage engine die tooeventual fout leidt.</span><span class="sxs-lookup"><span data-stu-id="40083-119">hello model uses a correlation between data from four of hello engine sensors and engine wear that leads tooeventual failure.</span></span> <span data-ttu-id="40083-120">Terwijl Fabrikam tooperform regelmatige inspecties tooensure veiligheid doorgaat, kan nu gebruikmaken van Hallo modellen toocompute Hallo resterende Levensduur van elke motor na elke vlucht.</span><span class="sxs-lookup"><span data-stu-id="40083-120">While Fabrikam continues tooperform regular inspections tooensure safety, it can now use hello models toocompute hello RUL for each engine after every flight.</span></span> <span data-ttu-id="40083-121">Hallo model Hallo verzamelen van telemetriegegevens van Hallo-engines tijdens de vlucht Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="40083-121">hello model uses hello telemetry collected from hello engines during hello flight.</span></span> <span data-ttu-id="40083-122">Fabrikam is nu in staat om toekomstige probleempunten te voorspellen en om van tevoren onderhoud en reparatiewerkzaamheden te plannen.</span><span class="sxs-lookup"><span data-stu-id="40083-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="40083-123">Hallo oplossing model reële slijtagegegevens gebruikt.</span><span class="sxs-lookup"><span data-stu-id="40083-123">hello solution model uses actual engine wear data.</span></span>

<span data-ttu-id="40083-124">Door het Hallo-punt voorspellen waarop onderhoud vereist, kan Fabrikam zijn bewerkingen tooreduce kosten optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="40083-124">By predicting hello point when maintenance is required, Fabrikam can optimize its operations tooreduce costs.</span></span>

<span data-ttu-id="40083-125">Onderhoudscoördinatoren werken met planners:</span><span class="sxs-lookup"><span data-stu-id="40083-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="40083-126">Plan onderhoud toocoincide een vliegtuig stoppen op een bepaalde locatie.</span><span class="sxs-lookup"><span data-stu-id="40083-126">Plan maintenance toocoincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="40083-127">Zorg ervoor dat voldoende tijd is beschikbaar voor Hallo vliegtuig toobe buiten de service zonder onderbreking van de planning.</span><span class="sxs-lookup"><span data-stu-id="40083-127">Ensure sufficient time is available for hello aircraft toobe out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="40083-128">tooschedule technici tooensure vliegtuig efficiënt worden verwerkt zonder wachttijd.</span><span class="sxs-lookup"><span data-stu-id="40083-128">tooschedule technicians tooensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="40083-129">Magazijnbeheerders ontvangen de onderhoudsplannen zodat zij hun bestelproces en hun voorraad met reserveonderdelen kunnen optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="40083-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="40083-130">Deze activiteiten Fabrikam toominimize vliegtuig compleet tijd inschakelen en de operationele kosten verlagen terwijl de veiligheid van passagiers en bemanning Hallo.</span><span class="sxs-lookup"><span data-stu-id="40083-130">These activities enable Fabrikam toominimize aircraft ground time and reduce operating costs while ensuring hello safety of passengers and crew.</span></span>

<span data-ttu-id="40083-131">toounderstand hoe [Azure IoT Suite] [ lnk_iot_suite] biedt Hallo mogelijkheden klanten nodig toorealize Hallo potentieel van voorspeld onderhoud controleert dit [infographic] [lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="40083-131">toounderstand how [Azure IoT Suite][lnk_iot_suite] provides hello capabilities customers need toorealize hello potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-hello-predictive-maintenance-solution-is-built"></a><span data-ttu-id="40083-132">Hoe Hallo-oplossing voor voorspeld onderhoud is gebouwd</span><span class="sxs-lookup"><span data-stu-id="40083-132">How hello predictive maintenance solution is built</span></span>

<span data-ttu-id="40083-133">Hallo oplossing maakt gebruik van een bestaand Azure Machine Learning-model beschikbaar als een sjabloon tooshow deze mogelijkheden werken op basis van telemetriegegevens die zijn verzameld via IoT Suite-services.</span><span class="sxs-lookup"><span data-stu-id="40083-133">hello solution uses an existing Azure Machine Learning model available as a template tooshow these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="40083-134">Microsoft heeft ontwikkeld een [regressiemodel] [ lnk_regression_model] van een vliegtuigmotor op basis van openbaar beschikbare gegevens<sup>\[1\]</sup>, en stapsgewijze hulp bij hoe toouse Hallo model.</span><span class="sxs-lookup"><span data-stu-id="40083-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how toouse hello model.</span></span>

<span data-ttu-id="40083-135">Hallo-regressiemodel dat is gemaakt met deze sjabloon maakt gebruik van Hello Azure IoT-oplossing voor voorspeld onderhoud.</span><span class="sxs-lookup"><span data-stu-id="40083-135">hello Azure IoT predictive maintenance solution uses hello regression model created from this template.</span></span> <span data-ttu-id="40083-136">Hallo-model is geïmplementeerd in uw Azure-abonnement en toegankelijk zijn via een automatisch gegenereerde API.</span><span class="sxs-lookup"><span data-stu-id="40083-136">hello model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="40083-137">Hallo-oplossing omvat een subset van Hallo testen van gegevens voor 4 (van in totaal 100) motoren en Hallo 4 (van in totaal 21) gegevensstromen.</span><span class="sxs-lookup"><span data-stu-id="40083-137">hello solution includes a subset of hello testing data representing 4 (of 100 total) engines and hello 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="40083-138">Deze gegevens zijn voldoende tooprovide een accuraat resultaat opleveren van Hallo getrainde model.</span><span class="sxs-lookup"><span data-stu-id="40083-138">This data is sufficient tooprovide an accurate result from hello trained model.</span></span>

<span data-ttu-id="40083-139">*\[1\] A. Saxena en K. Goebel (2008). 'Turbofan Engine Degradation Simulation Data Set', NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span><span class="sxs-lookup"><span data-stu-id="40083-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="40083-140">Aan de slag met voorspellend onderhoud</span><span class="sxs-lookup"><span data-stu-id="40083-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="40083-141">Deze zelfstudie leert u hoe tooprovision Hallo oplossing voor voorspeld onderhoud.</span><span class="sxs-lookup"><span data-stu-id="40083-141">This tutorial shows you how tooprovision hello predictive maintenance solution.</span></span> <span data-ttu-id="40083-142">Ook wordt u begeleid Hallo basisfuncties van Hallo-oplossing voor voorspeld onderhoud.</span><span class="sxs-lookup"><span data-stu-id="40083-142">It also walks you through hello basic features of hello predictive maintenance solution.</span></span> <span data-ttu-id="40083-143">Veel van deze functies kunt u openen via het dashboard van de oplossing Hallo die samen met de Hallo vooraf geconfigureerde oplossing implementeert.</span><span class="sxs-lookup"><span data-stu-id="40083-143">You can access many of these features through hello solution dashboard that deploys along with hello preconfigured solution.</span></span>

<span data-ttu-id="40083-144">toocomplete in deze zelfstudie, moet u een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="40083-144">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="40083-145">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="40083-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="40083-146">Zie [Gratis proefversie van Azure][lnk_free_trial] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="40083-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="40083-147">Meld u aan te[azureiotsuite.com] [ lnk-azureiotsuite] met behulp van uw Azure accountreferenties en klikt u op  **+**  toocreate een oplossing.</span><span class="sxs-lookup"><span data-stu-id="40083-147">Log on too[azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** toocreate a solution.</span></span>
1. <span data-ttu-id="40083-148">Klik op **Selecteer** hello **voorspeld onderhoud** tegel.</span><span class="sxs-lookup"><span data-stu-id="40083-148">Click **Select** hello **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="40083-149">Voer een **Naam van oplossing** in voor uw vooraf geconfigureerde oplossing voor voorspellend onderhoud.</span><span class="sxs-lookup"><span data-stu-id="40083-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="40083-150">Selecteer Hallo **regio** en **abonnement** toouse tooprovision Hallo oplossing.</span><span class="sxs-lookup"><span data-stu-id="40083-150">Select hello **Region** and **Subscription** you want toouse tooprovision hello solution.</span></span>
1. <span data-ttu-id="40083-151">Klik op **oplossing maken** toobegin Hallo inrichtingsproces.</span><span class="sxs-lookup"><span data-stu-id="40083-151">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="40083-152">Dit proces duurt gewoonlijk enkele minuten toorun.</span><span class="sxs-lookup"><span data-stu-id="40083-152">This process typically takes several minutes toorun.</span></span>

### <a name="wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="40083-153">Wachten op Hallo proces toocomplete inrichten</span><span class="sxs-lookup"><span data-stu-id="40083-153">Wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="40083-154">Klik op de tegel Hallo voor uw oplossing met **inrichten** status.</span><span class="sxs-lookup"><span data-stu-id="40083-154">Click hello tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="40083-155">Kennisgeving Hallo **Inrichtingstatuswaarden** wanneer Azure-services worden geïmplementeerd in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="40083-155">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="40083-156">Nadat het inrichten is voltooid, Hallo u statuswijzigingen te**gereed**.</span><span class="sxs-lookup"><span data-stu-id="40083-156">Once provisioning completes, hello status changes too**Ready**.</span></span>
1. <span data-ttu-id="40083-157">Klik op Hallo tegel toosee Hallo details van uw oplossing in het rechterdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="40083-157">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span> <span data-ttu-id="40083-158">U kunt dit deelvenster Hallo oplossing dashboard en toegang Hallo Machine Learning-werkruimte starten.</span><span class="sxs-lookup"><span data-stu-id="40083-158">From this pane, you can launch hello solution dashboard and access hello Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="40083-159">Als u problemen Hallo vooraf geconfigureerde oplossing implementeren, controleren [machtigingen op Hallo azureiotsuite.com site] [ lnk-permissions] en Hallo [Veelgestelde vragen over] [ lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="40083-159">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [FAQ][lnk-faq].</span></span> <span data-ttu-id="40083-160">Als Hallo problemen zich blijven voordoen, maakt u een serviceticket op Hallo [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="40083-160">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="40083-161">Zijn er details u mag verwachten toosee die voor uw oplossing niet vermeld?</span><span class="sxs-lookup"><span data-stu-id="40083-161">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="40083-162">Geef ons suggesties voor functies op [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="40083-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-hello-solution"></a><span data-ttu-id="40083-163">Hallo-oplossing weergeven</span><span class="sxs-lookup"><span data-stu-id="40083-163">View hello solution</span></span>

<span data-ttu-id="40083-164">Deze sectie helpt u bij Hallo oplossing gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="40083-164">This section guides you through hello solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="40083-165">Dashboard voorspeld onderhoud</span><span class="sxs-lookup"><span data-stu-id="40083-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="40083-166">Deze pagina in Hallo-webtoepassing maakt gebruik van PowerBI JavaScript-besturingselementen (Zie Hallo [PowerBI-visuals repository][lnk-powerbi]) toovisualize:</span><span class="sxs-lookup"><span data-stu-id="40083-166">This page in hello web application uses PowerBI JavaScript controls (see hello [PowerBI-visuals repository][lnk-powerbi]) toovisualize:</span></span>

* <span data-ttu-id="40083-167">Hallo uitvoergegevens van Hallo Stream Analytics-taken in de blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="40083-167">hello output data from hello Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="40083-168">Hallo resterende Levensduur en aantal cycli per vliegtuigmotor.</span><span class="sxs-lookup"><span data-stu-id="40083-168">hello RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a><span data-ttu-id="40083-169">Hallo-gedrag van Hallo cloudoplossing observeren</span><span class="sxs-lookup"><span data-stu-id="40083-169">Observing hello behavior of hello cloud solution</span></span>

<span data-ttu-id="40083-170">In Azure-portal hello, navigeert u toohello resourcegroep met de naam van de oplossing Hallo u hebt gekozen tooview uw ingerichte resources.</span><span class="sxs-lookup"><span data-stu-id="40083-170">In hello Azure portal, navigate toohello resource group with hello solution name you chose tooview your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="40083-171">Wanneer u Hallo vooraf geconfigureerde oplossing inricht, krijgt u een e-mail met een koppeling toohello Machine Learning-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="40083-171">When you provision hello preconfigured solution, you receive an email with a link toohello Machine Learning workspace.</span></span> <span data-ttu-id="40083-172">U kunt ook toohello Machine Learning-werkruimte van Hallo navigeren [azureiotsuite.com] [ lnk-azureiotsuite] pagina voor de ingerichte oplossing.</span><span class="sxs-lookup"><span data-stu-id="40083-172">You can also navigate toohello Machine Learning workspace from hello [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="40083-173">Een tegel is beschikbaar op deze pagina wanneer Hallo oplossing Hallo wordt **gereed** status.</span><span class="sxs-lookup"><span data-stu-id="40083-173">A tile is available on this page when hello solution is in hello **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="40083-174">In de oplossingsportal hello ziet u dat Hallo-voorbeeld is ingericht met vier gesimuleerde apparaten toorepresent twee vliegtuig met twee motoren per vliegtuig, elk met vier sensoren.</span><span class="sxs-lookup"><span data-stu-id="40083-174">In hello solution portal, you can see that hello sample is provisioned with four simulated devices toorepresent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="40083-175">Wanneer u eerst toohello oplossingsportal navigeert, wordt Hallo simulatie gestopt.</span><span class="sxs-lookup"><span data-stu-id="40083-175">When you first navigate toohello solution portal, hello simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="40083-176">Klik op **simulatie starten** toobegin Hallo simulatie.</span><span class="sxs-lookup"><span data-stu-id="40083-176">Click **Start simulation** toobegin hello simulation.</span></span> <span data-ttu-id="40083-177">Hallo sensor geschiedenis, resterende Levensduur, cycli en de resterende Levensduur geschiedenis vullen Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="40083-177">hello sensor history, RUL, Cycles, and RUL history populate hello dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="40083-178">Wanneer de resterende Levensduur minder dan 160 is (een willekeurige drempel gekozen ter illustratie), wordt een waarschuwing symbool volgende toohello weergegeven resterende Levensduur in Hallo oplossingsportal weergegeven.</span><span class="sxs-lookup"><span data-stu-id="40083-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), hello solution portal displays a warning symbol next toohello RUL display.</span></span> <span data-ttu-id="40083-179">Hallo oplossingsportal ook Hallo vliegtuigmotor geel gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="40083-179">hello solution portal also highlights hello aircraft engine in yellow.</span></span> <span data-ttu-id="40083-180">U ziet hoe Hallo resterende Levensduur waarden hebben voor een algemene neerwaartse trend, maar vaak toobounce omhoog en omlaag.</span><span class="sxs-lookup"><span data-stu-id="40083-180">Notice how hello RUL values have a general downward trend overall, but tend toobounce up and down.</span></span> <span data-ttu-id="40083-181">Dit probleem wordt veroorzaakt door verschillende lengten Hallo en Hallo model nauwkeurig.</span><span class="sxs-lookup"><span data-stu-id="40083-181">This behavior results from hello varying cycle lengths and hello model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="40083-182">de volledige simulatie Hallo duurt ongeveer 35 minuten toocomplete 148 cycli.</span><span class="sxs-lookup"><span data-stu-id="40083-182">hello full simulation takes around 35 minutes toocomplete 148 cycles.</span></span> <span data-ttu-id="40083-183">Hallo 160 resterende Levensduur drempelwaarde wordt voldaan voor Hallo eerst na ongeveer 5 minuten en beide motoren Hallo drempelwaarde na ongeveer 8 minuten bereikt.</span><span class="sxs-lookup"><span data-stu-id="40083-183">hello 160 RUL threshold is met for hello first time at around 5 minutes and both engines hit hello threshold at around 8 minutes.</span></span>

<span data-ttu-id="40083-184">Hallo simulatie wordt uitgevoerd via Hallo volledige gegevensset voor 148 cycli en bepaalt dan het eindresultaat van laatste resterende Levensduur en waarden.</span><span class="sxs-lookup"><span data-stu-id="40083-184">hello simulation runs through hello complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="40083-185">U kunt stoppen Hallo simulatie op elk punt, maar te klikken op **simulatie starten** replays Hallo simulatie van Hallo begin van Hallo gegevensset.</span><span class="sxs-lookup"><span data-stu-id="40083-185">You can stop hello simulation at any point, but clicking **Start Simulation** replays hello simulation from hello start of hello dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40083-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="40083-186">Next steps</span></span>

<span data-ttu-id="40083-187">meer informatie over hoe Azure IoT maakt voor voorspeld onderhoud-scenario's, lezen toolearn [vastleggen van de waarde van het Internet der dingen Hallo][lnk_capture_value].</span><span class="sxs-lookup"><span data-stu-id="40083-187">toolearn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from hello Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="40083-188">Duren voordat een [scenario] [ lnk-predictive-walkthrough] van Hallo-oplossing voor voorspeld onderhoud.</span><span class="sxs-lookup"><span data-stu-id="40083-188">Take a [walkthrough][lnk-predictive-walkthrough] of hello predictive maintenance solution.</span></span>

<span data-ttu-id="40083-189">U kunt ook verkennen van Hallo andere functies en mogelijkheden van Hallo vooraf geconfigureerde IoT Suite-oplossingen:</span><span class="sxs-lookup"><span data-stu-id="40083-189">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="40083-190">[Veelgestelde vragen over IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="40083-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="40083-191">[Beveiliging van de IoT van Hallo gemalen][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="40083-191">[IoT security from hello ground up][lnk-security-groundup]</span></span>

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
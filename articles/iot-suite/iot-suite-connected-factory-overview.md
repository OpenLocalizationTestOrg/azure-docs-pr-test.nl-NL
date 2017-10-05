---
title: Overzicht van verbonden factory's in Azure IoT Suite | Microsoft Docs
description: Een beschrijving van de vooraf geconfigureerde oplossing voor verbonden factory's van Azure IoT Suite.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: d502c8e2e2715899279f6ebcf7ed89c19a1bb9a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-connected-factory-preconfigured-solution"></a><span data-ttu-id="f6794-103">Aan de slag met de vooraf geconfigureerde oplossing voor verbonden factory's</span><span class="sxs-lookup"><span data-stu-id="f6794-103">Get started with the connected factory preconfigured solution</span></span>

<span data-ttu-id="f6794-104">[Vooraf geconfigureerde oplossingen][lnk-preconfigured-solutions] voor Azure IoT Suite zijn voorzien van meerdere Azure IoT-services om totaaloplossingen te leveren voor het implementeren van algemene IoT-bedrijfsscenario's.</span><span class="sxs-lookup"><span data-stu-id="f6794-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="f6794-105">De vooraf geconfigureerde oplossing voor *verbonden factory's* maakt verbinding met en controleert uw industriële apparaten.</span><span class="sxs-lookup"><span data-stu-id="f6794-105">The *connected factory* preconfigured solution connects to and monitors your industrial devices.</span></span> <span data-ttu-id="f6794-106">U kunt de oplossing gebruiken om de gegevensstroom van uw apparaten te analyseren en operationele productiviteit en winstgevendheid te bevorderen.</span><span class="sxs-lookup"><span data-stu-id="f6794-106">You can use the solution to analyze the stream of data from your devices and to drive operational productivity and profitability.</span></span>

<span data-ttu-id="f6794-107">In deze zelfstudie leert u hoe u de vooraf geconfigureerde oplossing voor verbonden factory's inricht.</span><span class="sxs-lookup"><span data-stu-id="f6794-107">This tutorial shows you how to provision the connected factory preconfigured solution.</span></span> <span data-ttu-id="f6794-108">Hierbij maakt u ook kennis met de basisfuncties van de vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="f6794-108">It also walks you through the basic features of the preconfigured solution.</span></span> <span data-ttu-id="f6794-109">U hebt toegang tot veel van deze functies via het *oplossingsdashboard* dat als onderdeel van de vooraf geconfigureerde oplossing wordt geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="f6794-109">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span></span>

![dashboard van de vooraf geconfigureerde oplossing voor verbonden factory's][img-cf-home]

<span data-ttu-id="f6794-111">U hebt een actief Azure-abonnement nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="f6794-111">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="f6794-112">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="f6794-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f6794-113">Zie [Gratis proefversie van Azure][lnk_free_trial] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f6794-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-the-solution"></a><span data-ttu-id="f6794-114">De oplossing inrichten</span><span class="sxs-lookup"><span data-stu-id="f6794-114">Provision the solution</span></span>

1. <span data-ttu-id="f6794-115">Meld u aan bij azureiotsuite.com met de referenties van uw Azure-account en klik op **+** om een oplossing te maken.</span><span class="sxs-lookup"><span data-stu-id="f6794-115">Log on to azureiotsuite.com using your Azure account credentials, and click "**+**" to create a solution.</span></span>
2. <span data-ttu-id="f6794-116">Klik op de tegel **Verbonden factory** op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="f6794-116">Click **Select** on the **Connected factory** tile.</span></span>
3. <span data-ttu-id="f6794-117">Voer een **oplossingsnaam** in voor uw verbonden vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="f6794-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="f6794-118">Selecteer het **abonnement** dat en de **regio** die u wilt gebruiken voor het inrichten van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="f6794-118">Select the **Subscription** and **Region** you want to use to provision the solution.</span></span>
5. <span data-ttu-id="f6794-119">Klik op **Oplossing maken** om het inrichtingsproces te starten.</span><span class="sxs-lookup"><span data-stu-id="f6794-119">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="f6794-120">Doorgaans duurt het enkele minuten om dit proces uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="f6794-120">This process typically takes several minutes to run.</span></span>

### <a name="while-you-wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="f6794-121">Doe het volgende terwijl u wacht tot het inrichtingsproces is voltooid</span><span class="sxs-lookup"><span data-stu-id="f6794-121">While you wait for the provisioning process to complete</span></span>

1. <span data-ttu-id="f6794-122">Klik op de tegel voor uw oplossing met de status **Inrichten**.</span><span class="sxs-lookup"><span data-stu-id="f6794-122">Click the tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="f6794-123">Tijdens de implementatie van Azure-services in uw Azure-abonnement verschijnen verschillende **inrichtingstatuswaarden**.</span><span class="sxs-lookup"><span data-stu-id="f6794-123">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="f6794-124">Nadat het inrichten is voltooid, verandert de status in **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="f6794-124">Once provisioning completes, the status changes to **Ready**.</span></span>
4. <span data-ttu-id="f6794-125">Klik op de tegel om de details van uw oplossing in het rechterdeelvenster weer te geven.</span><span class="sxs-lookup"><span data-stu-id="f6794-125">Click the tile to see the details of your solution in the right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="f6794-126">Als er problemen zijn met de implementatie van de vooraf geconfigureerde oplossing, leest u [Machtigingen op azureiotsuite.com][lnk-permissions] en de [veelgestelde vragen over Connected Factory](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="f6794-126">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="f6794-127">Als de problemen zich blijven voordoen, maakt u een serviceticket aan in de [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="f6794-127">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>

<span data-ttu-id="f6794-128">Zijn er voor uw oplossing bepaalde details niet vermeld, die u wel verwacht had te zien?</span><span class="sxs-lookup"><span data-stu-id="f6794-128">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="f6794-129">Geef ons suggesties voor functies op [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="f6794-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="f6794-130">Overzicht van scenario's</span><span class="sxs-lookup"><span data-stu-id="f6794-130">Scenario overview</span></span>

<span data-ttu-id="f6794-131">Wanneer u de vooraf geconfigureerde oplossing voor verbonden factory's implementeert, wordt deze vooraf ingevuld met de resources waarmee u een algemeen industrieel scenario kunt doorlopen.</span><span class="sxs-lookup"><span data-stu-id="f6794-131">When you deploy the connected factory preconfigured solution, it is prepopulated with resources that enable you to step through a common industrial scenario.</span></span> <span data-ttu-id="f6794-132">In dit scenario rapporteren verschillende factory's die zijn verbonden met de oplossing, de gegevenswaarden die vereist zijn voor het berekenen van de algemene apparatuurefficiëntie (overall equipment efficiency, OEE) en de key performance indicators (KPI's).</span><span class="sxs-lookup"><span data-stu-id="f6794-132">In this scenario, several factories connected to the solution report the data values required to compute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="f6794-133">De volgende gedeelten laten u zien hoe u:</span><span class="sxs-lookup"><span data-stu-id="f6794-133">The following sections show you how to:</span></span>

* <span data-ttu-id="f6794-134">de factory, de productielijnen, de OEE van stations en de KPI-waarden controleert;</span><span class="sxs-lookup"><span data-stu-id="f6794-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="f6794-135">de telemetriegegevens analyseert die van deze apparaten worden gegenereerd, met behulp van Time Series Insights in Azure;</span><span class="sxs-lookup"><span data-stu-id="f6794-135">Analyze the telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="f6794-136">op waarschuwingen reageert om problemen op te lossen.</span><span class="sxs-lookup"><span data-stu-id="f6794-136">Act on alerts to fix issues</span></span>

<span data-ttu-id="f6794-137">Een belangrijke functie van dit scenario is dat u al deze acties extern kunt uitvoeren vanuit het dashboard van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="f6794-137">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span></span> <span data-ttu-id="f6794-138">U hebt geen fysieke toegang tot de apparaten nodig.</span><span class="sxs-lookup"><span data-stu-id="f6794-138">You do not need physical access to the devices.</span></span>

## <a name="view-the-solution-dashboard"></a><span data-ttu-id="f6794-139">Het oplossingsdashboard bekijken</span><span class="sxs-lookup"><span data-stu-id="f6794-139">View the solution dashboard</span></span>

<span data-ttu-id="f6794-140">Vanaf het dashboard van de oplossing kunt u de geïmplementeerde oplossing beheren.</span><span class="sxs-lookup"><span data-stu-id="f6794-140">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="f6794-141">Het is een hiërarchische weergave van een overkoepelende factoryconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="f6794-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="f6794-142">U kunt bijvoorbeeld de OEE en KPI's weergeven, nieuwe knooppunten voor telemetrie publiceren en waarschuwingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f6794-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="f6794-143">Wanneer het inrichten is voltooid en op de tegel voor uw vooraf geconfigureerde oplossing de status **Gereed** wordt weergegeven, kiest u **Starten** om uw portal voor de oplossing voor verbonden factory's te openen op een nieuw tabblad.</span><span class="sxs-lookup"><span data-stu-id="f6794-143">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your connected factory solution portal in a new tab.</span></span>

    ![De vooraf geconfigureerde oplossing starten][img-launch-solution]

1. <span data-ttu-id="f6794-145">Standaard ziet u in de oplossingsportal het *dashboard*.</span><span class="sxs-lookup"><span data-stu-id="f6794-145">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="f6794-146">U kunt naar andere gebieden van de portal navigeren met het menu aan de linkerkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="f6794-146">To navigate to other areas of the portal, use the menu on the left-hand side of the page.</span></span>

    ![Dashboard van de vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-menu]

<span data-ttu-id="f6794-148">Het dashboard bevat de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="f6794-148">The dashboard displays the following information:</span></span>

* <span data-ttu-id="f6794-149">Een paneel met een **factorylijst** waarin de status, locatie en huidige productieconfiguratie in de oplossing worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f6794-149">A **Factory list** panel that shows the status, location, and current production configuration in the solution.</span></span> <span data-ttu-id="f6794-150">Wanneer u de oplossing voor het eerst uitvoert, zijn er een paar gesimuleerde apparaten.</span><span class="sxs-lookup"><span data-stu-id="f6794-150">When you first run the solution, there are a number of simulated devices.</span></span> <span data-ttu-id="f6794-151">De simulatie van de productielijn bestaat uit drie echte OPC UA-servers per productielijn die gesimuleerde taken uitvoeren en gegevens delen.</span><span class="sxs-lookup"><span data-stu-id="f6794-151">The production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="f6794-152">Zie de [veelgestelde vragen over Connected Factory](iot-suite-faq-cf.md) voor meer informatie over OPC UA.</span><span class="sxs-lookup"><span data-stu-id="f6794-152">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="f6794-153">Een **kaart** die de locatie aangeeft van elk apparaat dat met de oplossing is verbonden.</span><span class="sxs-lookup"><span data-stu-id="f6794-153">A **map** that displays the location of each device connected to the solution.</span></span> <span data-ttu-id="f6794-154">De oplossing kan de Bing Kaarten-API gebruiken om informatie op de kaart tekenen.</span><span class="sxs-lookup"><span data-stu-id="f6794-154">The solution can use the Bing Maps API to plot information on the map.</span></span> <span data-ttu-id="f6794-155">Als de Bing Kaarten Enterprise-API is ingeschakeld voor uw abonnement, wordt deze functie automatisch gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f6794-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="f6794-156">Als dit niet het geval is, leest u de [veelgestelde vragen][lnk-faq] voor meer informatie over hoe u de kaart dynamisch kunt maken.</span><span class="sxs-lookup"><span data-stu-id="f6794-156">If not, see the [FAQ][lnk-faq] to learn how to make the map dynamic.</span></span>
* <span data-ttu-id="f6794-157">Een paneel **Waarschuwingen** dat waarschuwingen weergeeft die worden gegenereerd wanneer een telemetrie- of OEE-/KPI-waarde een bepaalde drempelwaarde overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="f6794-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="f6794-158">Een paneel **Overall Equipment Efficiency** dat de OEE-waarden weergeeft voor de hele onderneming of voor de factory, de productielijn of het station die/dat u bekijkt.</span><span class="sxs-lookup"><span data-stu-id="f6794-158">An **Overall Equipment Efficiency** panel that shows the OEE values for the whole enterprise, or the factory/production line/station you are viewing.</span></span> <span data-ttu-id="f6794-159">Deze waarde wordt geaggregeerd van de stationsweergave naar het ondernemingsniveau.</span><span class="sxs-lookup"><span data-stu-id="f6794-159">This value is aggregated from the station view to the enterprise level.</span></span> <span data-ttu-id="f6794-160">De OEE-gegevens en de bijbehorende elementen kunnen nader worden geanalyseerd.</span><span class="sxs-lookup"><span data-stu-id="f6794-160">The OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="f6794-161">Een paneel **Key Performance Indicators** dat het aantal geproduceerde eenheden weergeeft en de energie die wordt verbruikt door de hele onderneming of door de factory, de productielijn of het station die/dat u bekijkt.</span><span class="sxs-lookup"><span data-stu-id="f6794-161">**Key Performance Indicators** panel that displays the number of units produced and energy used by the whole enterprise or the factory/production line/station you are viewing.</span></span> <span data-ttu-id="f6794-162">Deze waarden worden geaggregeerd van de stationsweergave naar het ondernemingsniveau.</span><span class="sxs-lookup"><span data-stu-id="f6794-162">These values are aggregated from a station view to the enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="f6794-163">Factory's weergeven</span><span class="sxs-lookup"><span data-stu-id="f6794-163">View factories</span></span>

<span data-ttu-id="f6794-164">Het paneel *Factory's* geeft de geografische locatie van alle factory's in de oplossing weer, samen met hun status en de huidige productieconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="f6794-164">The *Factories* panel shows you the geographical location of all the factories in the solution, their status, and current production configuration.</span></span> <span data-ttu-id="f6794-165">U kunt in de lijst met locaties naar de andere niveaus in de oplossingshiërarchie navigeren.</span><span class="sxs-lookup"><span data-stu-id="f6794-165">From the locations list, you can navigate to the other levels in the solution hierarchy.</span></span> <span data-ttu-id="f6794-166">De rijen in de lijst zijn hyperlinks die gekoppeld zijn aan details van de productielijnen op die locatie.</span><span class="sxs-lookup"><span data-stu-id="f6794-166">The rows in the list are hyperlinks that link details of the production lines at that location.</span></span> <span data-ttu-id="f6794-167">U kunt vervolgens inzoomen op de details van de productielijn en de weergave op stationsniveau.</span><span class="sxs-lookup"><span data-stu-id="f6794-167">It is then possible to drill into the production line details and down to the station level view.</span></span> <span data-ttu-id="f6794-168">U kunt ook een filter toepassen op de lijst.</span><span class="sxs-lookup"><span data-stu-id="f6794-168">You can also apply a filter to the list.</span></span>

![Factory's van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-factories] 

1. <span data-ttu-id="f6794-170">Het **paneel Factory's** bevat de lijst met factory's voor deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="f6794-170">The **Factory panel** shows the factory list for this solution.</span></span>

2. <span data-ttu-id="f6794-171">De factorylijst geeft aanvankelijk aan dat bij het inrichtingsproces zes factory's zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f6794-171">The factory list initially shows six factories created by the provisioning process.</span></span> <span data-ttu-id="f6794-172">U kunt extra gesimuleerde en fysieke apparaten aan de oplossing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f6794-172">You can add additional simulated and physical devices to the solution.</span></span>

3. <span data-ttu-id="f6794-173">Als u de details van een factory wil bekijken, klikt u op de rij in de factorylijst.</span><span class="sxs-lookup"><span data-stu-id="f6794-173">To view the details of a factory, click the row in the factory list.</span></span>

4. <span data-ttu-id="f6794-174">Als u de details van een productielijn wil bekijken, klikt u op de rij in de lijst.</span><span class="sxs-lookup"><span data-stu-id="f6794-174">To view the details of a production line, click the row in the list.</span></span>

5. <span data-ttu-id="f6794-175">Als u de gepubliceerde OPC UA-knooppunten van een station in de productielijn wilt weergeven, klikt u op de rij in de lijst.</span><span class="sxs-lookup"><span data-stu-id="f6794-175">To view the published OPC UA nodes of a station on the production line, click the row in the list.</span></span>

6. <span data-ttu-id="f6794-176">Als u details voor een bepaald knooppunt in het station wilt bekijken, klikt u op de rij in de lijst.</span><span class="sxs-lookup"><span data-stu-id="f6794-176">To view details on a specific node in the station, click the row in the list.</span></span> <span data-ttu-id="f6794-177">Met deze actie wordt het contextpaneel met Time Series Insights-visualisaties gestart.</span><span class="sxs-lookup"><span data-stu-id="f6794-177">This action launches the context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="f6794-178">Klik op de grafieken voor verdere analyse in de Time Series Insights-verkenner.</span><span class="sxs-lookup"><span data-stu-id="f6794-178">Click these graphs to do further analysis in the Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="f6794-179">Kaart weergeven</span><span class="sxs-lookup"><span data-stu-id="f6794-179">View map</span></span>

<span data-ttu-id="f6794-180">Als u met uw abonnement toegang hebt tot de Bing Kaarten-API, wordt op de kaart *Factory's* de geografische locatie en de status van alle factory's in de oplossing weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f6794-180">If your subscription has access to the Bing Maps API, the *Factories* map shows you the geographical location and status of all the factories in the solution.</span></span> <span data-ttu-id="f6794-181">Klik op de locaties op de kaart om in te zoomen op de locatiedetails.</span><span class="sxs-lookup"><span data-stu-id="f6794-181">To drill into the location details, click the locations displayed on the map.</span></span>

![Kaart van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="f6794-183">Waarschuwingen weergeven</span><span class="sxs-lookup"><span data-stu-id="f6794-183">View alerts</span></span>

<span data-ttu-id="f6794-184">Het paneel **Waarschuwing** geeft de waarschuwingen weer die worden gegenereerd wanneer een gemelde waarde of een berekende OEE-/KPI-waarde de geconfigureerde drempelwaarde overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="f6794-184">The **Alert** panel shows you alerts generated due to a reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="f6794-185">Dit paneel geeft waarschuwingen weer van elk niveau van de hiërarchie, van de weergave op stationsniveau tot de overkoepelende weergave.</span><span class="sxs-lookup"><span data-stu-id="f6794-185">This panel displays alerts at each level of the hierarchy, from the station level view to the global view.</span></span> <span data-ttu-id="f6794-186">De waarschuwingen bevatten een beschrijving van de waarschuwing, de datum, de tijd, de locatie en het aantal instanties.</span><span class="sxs-lookup"><span data-stu-id="f6794-186">The alerts contain a description of the alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="f6794-187">Aan de hand van de Time Series Insights-gegevens krijgt u inzicht in de gegevens die de waarschuwing hebben veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="f6794-187">You can gain insights in to the data that caused the alert using the Time Series Insights data.</span></span> <span data-ttu-id="f6794-188">Waar van toepassing worden de Time Series Insights-gegevens weergegeven in de waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="f6794-188">The Time Series Insights data is visualized in the alerts where applicable.</span></span> <span data-ttu-id="f6794-189">Als u beheerder bent, kunt u standaardacties uitvoeren voor de waarschuwingen, zoals:</span><span class="sxs-lookup"><span data-stu-id="f6794-189">If you are an Administrator, you can take default actions on the alerts such as:</span></span>

* <span data-ttu-id="f6794-190">De waarschuwing sluiten.</span><span class="sxs-lookup"><span data-stu-id="f6794-190">Close the alert.</span></span>
* <span data-ttu-id="f6794-191">De waarschuwing accepteren.</span><span class="sxs-lookup"><span data-stu-id="f6794-191">Acknowledge the alert.</span></span>

<span data-ttu-id="f6794-192">Eventueel kunt u complexere acties uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f6794-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="f6794-193">Voor het OPC UA-drukknooppunt van de assembly kunt u bijvoorbeeld het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="f6794-193">For example, for the Pressure OPC UA Node of the Assembly you could:</span></span>

* <span data-ttu-id="f6794-194">Ondersteunende informatie weergeven op een webpagina in een nieuw browservenster.</span><span class="sxs-lookup"><span data-stu-id="f6794-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="f6794-195">De oorzaak van de waarschuwing oplossen door een OPC UA-methode op het apparaat aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="f6794-195">Mitigate the cause of the alert by calling an OPC UA method on the device.</span></span>
* <span data-ttu-id="f6794-196">De beschikbaarheid van de standaardacties onderdrukken.</span><span class="sxs-lookup"><span data-stu-id="f6794-196">Suppress the availability of the default actions.</span></span>

    ![Waarschuwingen van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="f6794-198">Deze waarschuwingen worden gegenereerd door regels die zijn opgegeven in een configuratiebestand in de vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="f6794-198">These alerts are generated by rules that are specified in a configuration file in the preconfigured solution.</span></span> <span data-ttu-id="f6794-199">Deze regels kunnen waarschuwingen genereren wanneer de OEE- of KPI-gegevens of de waarden van het OPC UA-knooppunt de geconfigureerde drempelwaarde overschrijden.</span><span class="sxs-lookup"><span data-stu-id="f6794-199">These rules can generate alerts when the OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="f6794-200">Het **paneel Waarschuwingen** geeft de waarschuwingen weer die in deze oplossing worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="f6794-200">The **Alerts panel** shows the alerts generated in this solution.</span></span>

2. <span data-ttu-id="f6794-201">Klik op de waarschuwing in het paneel Waarschuwingen om de details van een waarschuwing weer te geven.</span><span class="sxs-lookup"><span data-stu-id="f6794-201">To view the details of an alert, click the alert in the alerts panel.</span></span>

3. <span data-ttu-id="f6794-202">Klik op de grafiek in het paneel Waarschuwingen om de Time Series Insights-verkenner te openen en de waarschuwingsgegevens verder te analyseren.</span><span class="sxs-lookup"><span data-stu-id="f6794-202">To further analyze the alert data, click the graph in the alert panel to open the Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="f6794-203">In het paneel Waarschuwingen zijn verschillende acties voor de waarschuwing beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="f6794-203">To address the alert, several actions are available in the alert panel.</span></span> <span data-ttu-id="f6794-204">Kies de gewenste optie en klik op de knop voor het uitvoeren van de actie.</span><span class="sxs-lookup"><span data-stu-id="f6794-204">Choose the appropriate option for you and click the execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="f6794-205">Algemene apparatuurefficiëntie weergeven</span><span class="sxs-lookup"><span data-stu-id="f6794-205">View overall equipment efficiency</span></span>

<span data-ttu-id="f6794-206">De OEE bepaalt de efficiëntie van het productieproces met behulp van operationele parameters gerelateerd aan cruciale productie.</span><span class="sxs-lookup"><span data-stu-id="f6794-206">OEE rates the efficiency of the manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="f6794-207">OEE is een standaardmeeteenheid binnen de industrie die wordt berekend door de beschikbaarheidswaarde te vermenigvuldigen met de prestatiewaarde en de kwaliteitswaarde: OEE = beschikbaarheid x prestaties x kwaliteit.</span><span class="sxs-lookup"><span data-stu-id="f6794-207">OEE is an industry standard measure calculated by multiplying the availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![OEE van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-oee]

1. <span data-ttu-id="f6794-209">Als u de OEE voor een bepaald niveau in de hiërarchie wilt bekijken, gaat u naar de weergave die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="f6794-209">To view OEE for any level in the hierarchy, navigate to the specific view you require.</span></span> <span data-ttu-id="f6794-210">De OEE voor deze weergave wordt in het paneel weergegeven samen met de elementen die onderdeel uitmaken van het OEE-percentage.</span><span class="sxs-lookup"><span data-stu-id="f6794-210">The OEE for that view displays in the panel along with each of the elements that make up the OEE percentage.</span></span>

2. <span data-ttu-id="f6794-211">Voor een nadere analyse van de OEE voor een willekeurig niveau in de hiërarchiegegevens klikt u op het OEE-percentage, het beschikbaarheidspercentage, het prestatiepercentage of het kwaliteitspercentage.</span><span class="sxs-lookup"><span data-stu-id="f6794-211">To further analyze the OEE for any level in the hierarchy data, click either the OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="f6794-212">Er wordt een contextpaneel weergegeven met Time Series Insights-visualisaties die gegevens van het afgelopen uur, de afgelopen 24 uur en de afgelopen 7 dagen tonen.</span><span class="sxs-lookup"><span data-stu-id="f6794-212">A context panel appears with Time Series Insights powered visualizations that shows data from the last hour, last 24 hours, and last 7 days.</span></span>

    ![TSI-visualisatie van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-tsi-visualization]

3. <span data-ttu-id="f6794-214">Klik op de grafiek in het paneel Waarschuwingen om de waarschuwingsgegevens verder te analyseren.</span><span class="sxs-lookup"><span data-stu-id="f6794-214">To further analyze the alert data, click the graph in the alert panel.</span></span> <span data-ttu-id="f6794-215">Met deze actie wordt de Time Series Insights-verkenner geopend.</span><span class="sxs-lookup"><span data-stu-id="f6794-215">This action opens the Time Series Insights explorer environment.</span></span>

    ![TSI-verkenner van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="f6794-217">Key performance indicators weergeven</span><span class="sxs-lookup"><span data-stu-id="f6794-217">View Key Performance Indicators</span></span>

<span data-ttu-id="f6794-218">De oplossing biedt twee key performance indicators: *eenheden per uur* en *energieverbruik in kWh*.</span><span class="sxs-lookup"><span data-stu-id="f6794-218">The solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![KPI van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-kpi]

1. <span data-ttu-id="f6794-220">Als u het aantal eenheden per uur of het energieverbruik voor een bepaald niveau in de hiërarchie wilt bekijken, gaat u naar de weergave die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="f6794-220">To view units per hour or energy used for any level in the hierarchy, navigate to the specific view you require.</span></span> <span data-ttu-id="f6794-221">Het aantal eenheden per uur en het energieverbruik worden in het paneel weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f6794-221">The units per hour and energy used display in the panel.</span></span>

2. <span data-ttu-id="f6794-222">Als u het aantal eenheden per uur of het energieverbruik verder wilt analyseren voor een willekeurig niveau in de hiërarchie, klikt u op de meter in het paneel **Key Performance Indicators**.</span><span class="sxs-lookup"><span data-stu-id="f6794-222">To analyze units per hour or energy used for any level in the hierarchy further, click the gauge in the **Key Performance Indicators** panel.</span></span> <span data-ttu-id="f6794-223">Er wordt een contextpaneel weergegeven met Time Series Insights-visualisaties waarmee u gegevens van het afgelopen uur, de afgelopen 24 uur en de afgelopen 7 dagen kunt bekijken.</span><span class="sxs-lookup"><span data-stu-id="f6794-223">A context panel appears with Time Series Insights powered visualizations enabling you to view data from the last hour, the last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="f6794-224">Samenvatting van scenario</span><span class="sxs-lookup"><span data-stu-id="f6794-224">Scenario review</span></span>

<span data-ttu-id="f6794-225">In dit scenario hebt u de OEE- en KPI-waarden van uw factory's gecontroleerd in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="f6794-225">In this scenario, you monitored your factories OEE and KPIs values, in the dashboard.</span></span> <span data-ttu-id="f6794-226">Vervolgens hebt u Time Series Insights gebruikt om meer informatie te krijgen voor het verder inzoomen op de telemetriegegevens voor OEE en KPI's om te helpen bij het detecteren van afwijkingen.</span><span class="sxs-lookup"><span data-stu-id="f6794-226">You then used Time Series Insights to provide more information to help drill further into the telemetry data for OEE and KPIs to help with detecting anomalies.</span></span> <span data-ttu-id="f6794-227">U hebt ook het paneel Waarschuwingen gebruikt om problemen met uw factory's te bekijken en de beschikbare acties gebruikt om de waarschuwing te verhelpen.</span><span class="sxs-lookup"><span data-stu-id="f6794-227">You also used the alert panel to view issues with your factories and you used the actions available to you to resolve the alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="f6794-228">Andere functies</span><span class="sxs-lookup"><span data-stu-id="f6794-228">Other features</span></span>

<span data-ttu-id="f6794-229">De volgende gedeelten beschrijven een aantal extra functies van de oplossing voor verbonden factory's die niet aan bod zijn gekomen in het voorgaande scenario.</span><span class="sxs-lookup"><span data-stu-id="f6794-229">The following sections describe some additional features of the connected factory solution that are not described in the previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="f6794-230">Filters toepassen</span><span class="sxs-lookup"><span data-stu-id="f6794-230">Apply filters</span></span>

1. <span data-ttu-id="f6794-231">Klik op de **dubbele punthaak** om een lijst met beschikbare filters weer te geven in het paneel met factorylocaties of het paneel Waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="f6794-231">Click the **chevron** to display a list of available filters in either the factory locations panel or the alerts panel.</span></span>

2. <span data-ttu-id="f6794-232">Het paneel Filters wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f6794-232">The filters panel is displayed for you.</span></span> 

    ![Filters van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-alert-filter]

3. <span data-ttu-id="f6794-234">Kies het filter dat u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="f6794-234">Choose the filter that you require.</span></span> <span data-ttu-id="f6794-235">U kunt ook vrije tekst typen in de filtervelden.</span><span class="sxs-lookup"><span data-stu-id="f6794-235">It is also possible to type free text into the filter fields.</span></span>

4. <span data-ttu-id="f6794-236">Het filter wordt vervolgens toegepast.</span><span class="sxs-lookup"><span data-stu-id="f6794-236">The filter is then applied for you.</span></span> <span data-ttu-id="f6794-237">U ziet de filterstatus ook in het dashboard en wel in de vorm van een trechter die wordt weergegeven in de tabellen met factory's en waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="f6794-237">The filter state is also shown in the dashboard via a funnel that displays in the factories and alerts tables.</span></span>

    ![Filters van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="f6794-239">Een actief filter heeft geen invloed op de weergegeven OEE- en KPI-waarden; het filtert alleen de inhoud van de lijst.</span><span class="sxs-lookup"><span data-stu-id="f6794-239">An active filter does not affect the displayed OEE and KPI values, it only filters the list contents.</span></span>

5. <span data-ttu-id="f6794-240">Als u een filter wilt wissen, klikt u op de trechter en vervolgens op Filter in het filtercontextpaneel.</span><span class="sxs-lookup"><span data-stu-id="f6794-240">To clear a filter, click the funnel and click filter in the filter context panel.</span></span> <span data-ttu-id="f6794-241">De tekst **Alle** wordt weergegeven in de tabellen met factory's en waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="f6794-241">The text **All** is displayed in the factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="f6794-242">Door een OPC UA-server bladeren</span><span class="sxs-lookup"><span data-stu-id="f6794-242">Browse an OPC UA server</span></span>

<span data-ttu-id="f6794-243">Wanneer u de vooraf geconfigureerde oplossing implementeert, worden er automatisch gesimuleerde OPC UA-servers ingericht die u met de oplossingsbrowser kunt doorbladeren.</span><span class="sxs-lookup"><span data-stu-id="f6794-243">When you deploy the preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via the solution browser.</span></span> <span data-ttu-id="f6794-244">Deze servers zijn *gesimuleerde OPC UA-servers*.</span><span class="sxs-lookup"><span data-stu-id="f6794-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="f6794-245">Gesimuleerde servers maken het voor u gemakkelijk om te experimenteren met een vooraf geconfigureerde oplossing zonder dat u echte, fysieke servers hoeft te implementeren.</span><span class="sxs-lookup"><span data-stu-id="f6794-245">Simulated servers make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical servers.</span></span> <span data-ttu-id="f6794-246">Raadpleeg de zelfstudie [Connect your OPC UA device to the connected factory preconfigured solution][lnk-connect-cf] (Uw OPC UA-apparaat koppelen aan de vooraf geconfigureerde oplossing voor verbonden factory's) als u een echte OPC UA-server aan de oplossing wilt koppelen.</span><span class="sxs-lookup"><span data-stu-id="f6794-246">If you do want to connect a real OPC UA server to the solution, see the [Connect your OPC UA device to the connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="f6794-247">Klik op het **factorypictogram** in de navigatiebalk van het dashboard.</span><span class="sxs-lookup"><span data-stu-id="f6794-247">Click the **factory icon** in the dashboard navigation bar.</span></span>

    ![Serverbrowser van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-server-browser]

2. <span data-ttu-id="f6794-249">Kies een van de servers uit de vooraf geconfigureerde lijst.</span><span class="sxs-lookup"><span data-stu-id="f6794-249">Choose one of the servers from the preconfigured list.</span></span> <span data-ttu-id="f6794-250">Deze lijst bevat de servers die in de vooraf geconfigureerde oplossing zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f6794-250">This list shows the servers that are deployed for you in the preconfigured solution.</span></span>

    ![Serverselectie van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-server-choice]

3. <span data-ttu-id="f6794-252">Klik op **Verbinden**. Er wordt een beveiligingsdialoogvenster weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f6794-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="f6794-253">Tijdens de simulatie is het veilig om op **Doorgaan** te klikken</span><span class="sxs-lookup"><span data-stu-id="f6794-253">For the simulation, it is safe to click **Proceed**</span></span>

4. <span data-ttu-id="f6794-254">Klik op een van de knooppunten in de serverstructuur om deze uit te vouwen.</span><span class="sxs-lookup"><span data-stu-id="f6794-254">To expand any of the nodes in the server tree, click it.</span></span> <span data-ttu-id="f6794-255">Naast knooppunten die telemetrie publiceren, staat een vinkje.</span><span class="sxs-lookup"><span data-stu-id="f6794-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![Serverstructuur van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-server-tree]

5. <span data-ttu-id="f6794-257">Klik met de rechtermuisknop op een item om het knooppunt te lezen, te schrijven, te publiceren of aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="f6794-257">Right-click an item to read, write, publish, or call that node.</span></span> <span data-ttu-id="f6794-258">Welke acties er beschikbaar zijn, is afhankelijk van uw machtigingen en de kenmerken van het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="f6794-258">The actions available to you depend on your permissions and the attributes of the node.</span></span> <span data-ttu-id="f6794-259">Met de optie voor lezen wordt een contextpaneel weergegeven met de waarde van dat knooppunt.</span><span class="sxs-lookup"><span data-stu-id="f6794-259">The read option to displays a context panel showing the value of the specific node.</span></span> <span data-ttu-id="f6794-260">Met de optie voor schrijven wordt een contextpaneel weergegeven waarin u een nieuwe waarde kunt invoeren.</span><span class="sxs-lookup"><span data-stu-id="f6794-260">The write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="f6794-261">Met de optie voor aanroepen wordt een knooppunt weergegeven waarin u de parameters voor het aanroepen kunt invoeren.</span><span class="sxs-lookup"><span data-stu-id="f6794-261">The call option displays a node where you can enter the parameters for the call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="f6794-262">Een knooppunt publiceren</span><span class="sxs-lookup"><span data-stu-id="f6794-262">Publish a node</span></span>

<span data-ttu-id="f6794-263">Wanneer u door een *gesimuleerde OPC UA-server* bladert, kunt u ook nieuwe knooppunten publiceren.</span><span class="sxs-lookup"><span data-stu-id="f6794-263">When you browse a *simulated OPC UA server*, you can also choose to publish new nodes.</span></span> <span data-ttu-id="f6794-264">Vervolgens kunt u de telemetrie van deze knooppunten in de oplossing analyseren.</span><span class="sxs-lookup"><span data-stu-id="f6794-264">You can analyze the telemetry from these nodes in the solution.</span></span> <span data-ttu-id="f6794-265">De *gesimuleerde OPC UA-servers* maken het gemakkelijk om te experimenteren met een vooraf geconfigureerde oplossing zonder dat u echte, fysieke apparaten hoeft te implementeren.</span><span class="sxs-lookup"><span data-stu-id="f6794-265">These *simulated OPC UA servers* make it easy to experiment with the preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="f6794-266">Blader naar een knooppunt in de browserstructuur van de OPC UA-server die u wilt publiceren.</span><span class="sxs-lookup"><span data-stu-id="f6794-266">Browse to a node in the OPC UA server browser tree that you wish to publish.</span></span>

2. <span data-ttu-id="f6794-267">Klik met de rechtermuisknop op het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="f6794-267">Right-click the node.</span></span>

3. <span data-ttu-id="f6794-268">Kies **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="f6794-268">Choose **Publish**.</span></span>

    ![Verbonden factory publiceert knooppunt][cf-img-publish-node]

4. <span data-ttu-id="f6794-270">Er word een contextpaneel weergegeven waarin staat dat het publiceren is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f6794-270">A context panel appears which tells you that the publish has succeeded.</span></span> <span data-ttu-id="f6794-271">Het knooppunt wordt weergegeven met een vinkje in de weergave op stationsniveau.</span><span class="sxs-lookup"><span data-stu-id="f6794-271">The node appears in the station level view with a check mark beside it.</span></span>

    ![Succesvolle publicatie van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="f6794-273">Opdracht en controle</span><span class="sxs-lookup"><span data-stu-id="f6794-273">Command and control</span></span>

<span data-ttu-id="f6794-274">Met de verbonden factory kunt u uw industriële apparaten rechtstreeks vanuit de cloud beheren en bedienen.</span><span class="sxs-lookup"><span data-stu-id="f6794-274">The connected factory allows you command and control your industry devices directly from the cloud.</span></span> <span data-ttu-id="f6794-275">U kunt deze functie gebruiken om te reageren op waarschuwingen die door het apparaat worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="f6794-275">You can use this feature to respond to alerts generated by the device.</span></span> <span data-ttu-id="f6794-276">U kunt bijvoorbeeld vanuit de cloud een opdracht naar het apparaat verzenden.</span><span class="sxs-lookup"><span data-stu-id="f6794-276">For example, you could send a command to the device from the cloud.</span></span> <span data-ttu-id="f6794-277">U vindt de beschikbare opdrachten in het knooppunt **StationCommands** in de browserstructuur van de OPC UA-servers.</span><span class="sxs-lookup"><span data-stu-id="f6794-277">You can find the available commands in the **StationCommands** node in the OPC UA servers browser tree.</span></span> <span data-ttu-id="f6794-278">In dit scenario opent u een overdrukventiel op de verzamelplaats van een productielijn in München.</span><span class="sxs-lookup"><span data-stu-id="f6794-278">In this scenario, you open a pressure release valve on the assembly station of a production line in Munich.</span></span> <span data-ttu-id="f6794-279">U moet de rol van **beheerder** hebben voor de implementatie van de vooraf geconfigureerde oplossing om de opdracht- en bedieningsfuncties te kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f6794-279">To use the command and control functionality, you must be in the **Administrator** role for the preconfigured solution deployment.</span></span>

1. <span data-ttu-id="f6794-280">Blader naar het knooppunt **StationCommands** in de browserstructuur van de OPC UA-server.</span><span class="sxs-lookup"><span data-stu-id="f6794-280">Browse to the **StationCommands** node in the OPC UA server browser tree.</span></span>

2. <span data-ttu-id="f6794-281">Kies de opdracht die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f6794-281">Choose the command that you wish use.</span></span>

3. <span data-ttu-id="f6794-282">Klik met de rechtermuisknop op het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="f6794-282">Right-click the node.</span></span>

4. <span data-ttu-id="f6794-283">Kies **Aanroepen**.</span><span class="sxs-lookup"><span data-stu-id="f6794-283">Choose **Call**.</span></span>

    ![Aanroepopdracht van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-call-command]

5. <span data-ttu-id="f6794-285">Er wordt een contextpaneel weergegeven waarin staat welke methode u gaat aanroepen en, indien van toepassing, details van de parameter.</span><span class="sxs-lookup"><span data-stu-id="f6794-285">A context panel appears informing you which method you are about to call and any parameter details is applicable.</span></span>

6. <span data-ttu-id="f6794-286">Kies **Aanroepen**.</span><span class="sxs-lookup"><span data-stu-id="f6794-286">Choose **Call**.</span></span>

    ![Aanroepcontext van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-call-context]

7. <span data-ttu-id="f6794-288">Het contextpaneel wordt bijgewerkt met de melding dat het aanroepen van de methode is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f6794-288">The context panel is updated to inform you that the method call succeeded.</span></span> <span data-ttu-id="f6794-289">U kunt controleren of de oproep is voltooid door de waarde van het drukknooppunt te lezen, die na de aanroep is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f6794-289">You can verify the call succeeded by reading the value of the pressure node that updated as a result of the call.</span></span>

    ![Aanroepen voltooid van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-call-success]


## <a name="behind-the-scenes"></a><span data-ttu-id="f6794-291">Achter de schermen</span><span class="sxs-lookup"><span data-stu-id="f6794-291">Behind the scenes</span></span>

<span data-ttu-id="f6794-292">Wanneer u een vooraf geconfigureerde oplossing implementeert, maakt het implementatieproces meerdere resources in het door u geselecteerde Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f6794-292">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span></span> <span data-ttu-id="f6794-293">U kunt deze resources weergeven in Azure [Portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="f6794-293">You can view these resources in the Azure [portal][lnk-portal].</span></span> <span data-ttu-id="f6794-294">Het implementatieproces maakt een **resourcegroep** met een naam die is gebaseerd op de naam die u voor uw vooraf geconfigureerde oplossing hebt gekozen:</span><span class="sxs-lookup"><span data-stu-id="f6794-294">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span></span>

![Vooraf geconfigureerde oplossing in Azure Portal][img-cf-portal]

<span data-ttu-id="f6794-296">U kunt de instellingen van elke resource weergeven door deze te selecteren in de lijst met resources in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f6794-296">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span></span>

<span data-ttu-id="f6794-297">U kunt ook de broncode voor de vooraf geconfigureerde oplossing weergeven.</span><span class="sxs-lookup"><span data-stu-id="f6794-297">You can also view the source code for the preconfigured solution.</span></span> <span data-ttu-id="f6794-298">De broncode van de vooraf geconfigureerde oplossing voor verbonden factory's bevindt zich in de GitHub-opslagplaats [azure-iot-connected-factory][lnk-cfgithub]:</span><span class="sxs-lookup"><span data-stu-id="f6794-298">The connected factory preconfigured solution source code is in the [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="f6794-299">Wanneer u klaar bent, kunt u de vooraf geconfigureerde oplossing verwijderen uit uw Azure-abonnement op de site [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="f6794-299">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="f6794-300">Met de site kunt u gemakkelijk resources verwijderen die werden aangevoerd toen u de vooraf geconfigureerde oplossing hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f6794-300">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="f6794-301">Verwijder de oplossing op de site [azureiotsuite.com][lnk-azureiotsuite]. Zo zorgt u ervoor dat alles met betrekking tot de vooraf geconfigureerde oplossing wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f6794-301">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="f6794-302">Verwijder de resourcegroep niet in de portal.</span><span class="sxs-lookup"><span data-stu-id="f6794-302">Do not delete the resource group in the portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6794-303">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f6794-303">Next Steps</span></span>

<span data-ttu-id="f6794-304">Nu u een werkende vooraf geconfigureerde oplossing hebt geïmplementeerd, kunt u doorgaan met IoT Suite door de volgende artikels te lezen:</span><span class="sxs-lookup"><span data-stu-id="f6794-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="f6794-305">[Overzicht van de vooraf geconfigureerde oplossing voor verbonden factory's][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="f6794-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="f6794-306">[Uw apparaat koppelen aan de vooraf geconfigureerde oplossing voor verbonden factory's][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="f6794-306">[Connect your device to the Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="f6794-307">[Machtigingen op de site azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="f6794-307">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md
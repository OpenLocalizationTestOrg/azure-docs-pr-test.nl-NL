---
title: aaaAzure IoT Suite verbonden factory overzicht | Microsoft Docs
description: Een beschrijving van hello Azure IoT Suite verbonden factory vooraf geconfigureerde oplossing.
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
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a><span data-ttu-id="1f415-103">Aan de slag met Hallo verbonden factory vooraf geconfigureerde oplossing</span><span class="sxs-lookup"><span data-stu-id="1f415-103">Get started with hello connected factory preconfigured solution</span></span>

<span data-ttu-id="1f415-104">Azure IoT Suite [vooraf geconfigureerde oplossingen] [ lnk-preconfigured-solutions] combineren meerdere Azure IoT services toodeliver end-to-end-oplossingen die algemene IoT-bedrijfsscenario's implementeren.</span><span class="sxs-lookup"><span data-stu-id="1f415-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="1f415-105">Hallo *verbonden factory* tooand monitors uw industriële apparaten vooraf geconfigureerde oplossing verbonden.</span><span class="sxs-lookup"><span data-stu-id="1f415-105">hello *connected factory* preconfigured solution connects tooand monitors your industrial devices.</span></span> <span data-ttu-id="1f415-106">U kunt Hallo oplossing tooanalyze Hallo stroom van gegevens van uw apparaten en toodrive operationele productiviteit en winstgevendheid.</span><span class="sxs-lookup"><span data-stu-id="1f415-106">You can use hello solution tooanalyze hello stream of data from your devices and toodrive operational productivity and profitability.</span></span>

<span data-ttu-id="1f415-107">Deze zelfstudie laat zien hoe tooprovision Hallo factory verbonden vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="1f415-107">This tutorial shows you how tooprovision hello connected factory preconfigured solution.</span></span> <span data-ttu-id="1f415-108">Ook wordt u begeleid Hallo basisfuncties van Hallo vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="1f415-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="1f415-109">U veel van deze functies kunt openen vanaf Hallo oplossing *dashboard* die als onderdeel van Hallo vooraf geconfigureerde oplossing implementeert:</span><span class="sxs-lookup"><span data-stu-id="1f415-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![dashboard van de vooraf geconfigureerde oplossing voor verbonden factory's][img-cf-home]

<span data-ttu-id="1f415-111">toocomplete in deze zelfstudie, moet u een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1f415-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="1f415-112">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="1f415-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1f415-113">Zie [Gratis proefversie van Azure][lnk_free_trial] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1f415-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-hello-solution"></a><span data-ttu-id="1f415-114">Hallo-oplossing inrichten</span><span class="sxs-lookup"><span data-stu-id="1f415-114">Provision hello solution</span></span>

1. <span data-ttu-id="1f415-115">Meld u aan tooazureiotsuite.com met behulp van de referenties van uw Azure-account en klik op '**+**' toocreate een oplossing.</span><span class="sxs-lookup"><span data-stu-id="1f415-115">Log on tooazureiotsuite.com using your Azure account credentials, and click "**+**" toocreate a solution.</span></span>
2. <span data-ttu-id="1f415-116">Klik op **Selecteer** op Hallo **verbonden factory** tegel.</span><span class="sxs-lookup"><span data-stu-id="1f415-116">Click **Select** on hello **Connected factory** tile.</span></span>
3. <span data-ttu-id="1f415-117">Voer een **oplossingsnaam** in voor uw verbonden vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="1f415-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="1f415-118">Selecteer Hallo **abonnement** en **regio** toouse tooprovision Hallo oplossing.</span><span class="sxs-lookup"><span data-stu-id="1f415-118">Select hello **Subscription** and **Region** you want toouse tooprovision hello solution.</span></span>
5. <span data-ttu-id="1f415-119">Klik op **oplossing maken** toobegin Hallo inrichtingsproces.</span><span class="sxs-lookup"><span data-stu-id="1f415-119">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="1f415-120">Dit proces duurt gewoonlijk enkele minuten toorun.</span><span class="sxs-lookup"><span data-stu-id="1f415-120">This process typically takes several minutes toorun.</span></span>

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="1f415-121">Terwijl u wacht op Hallo proces toocomplete inrichten</span><span class="sxs-lookup"><span data-stu-id="1f415-121">While you wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="1f415-122">Klik op de tegel Hallo voor uw oplossing met **inrichten** status.</span><span class="sxs-lookup"><span data-stu-id="1f415-122">Click hello tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="1f415-123">Kennisgeving Hallo **Inrichtingstatuswaarden** wanneer Azure-services worden geïmplementeerd in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1f415-123">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="1f415-124">Nadat het inrichten is voltooid, Hallo u statuswijzigingen te**gereed**.</span><span class="sxs-lookup"><span data-stu-id="1f415-124">Once provisioning completes, hello status changes too**Ready**.</span></span>
4. <span data-ttu-id="1f415-125">Klik op Hallo tegel toosee Hallo details van uw oplossing in het rechterdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f415-125">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="1f415-126">Als u problemen Hallo vooraf geconfigureerde oplossing implementeren, controleren [machtigingen op Hallo azureiotsuite.com site] [ lnk-permissions] en Hallo [verbonden factory Veelgestelde vragen over](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="1f415-126">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="1f415-127">Als Hallo problemen zich blijven voordoen, maakt u een serviceticket op Hallo [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="1f415-127">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="1f415-128">Zijn er details u mag verwachten toosee die voor uw oplossing niet vermeld?</span><span class="sxs-lookup"><span data-stu-id="1f415-128">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="1f415-129">Geef ons suggesties voor functies op [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="1f415-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="1f415-130">Overzicht van scenario's</span><span class="sxs-lookup"><span data-stu-id="1f415-130">Scenario overview</span></span>

<span data-ttu-id="1f415-131">Bij het implementeren van Hallo verbonden factory vooraf geconfigureerde oplossing, het is vooraf ingevuld met de resources die u in staat toostep via een gemeenschappelijke industriële scenario stellen.</span><span class="sxs-lookup"><span data-stu-id="1f415-131">When you deploy hello connected factory preconfigured solution, it is prepopulated with resources that enable you toostep through a common industrial scenario.</span></span> <span data-ttu-id="1f415-132">In dit scenario verschillende fabrieken toohello oplossing rapport Hallo gegevenswaarden vereist toocompute verbonden algehele apparatuur efficiëntie (OEE) en prestatie-indicatoren (KPI's).</span><span class="sxs-lookup"><span data-stu-id="1f415-132">In this scenario, several factories connected toohello solution report hello data values required toocompute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="1f415-133">Hallo volgende secties ziet u hoe aan:</span><span class="sxs-lookup"><span data-stu-id="1f415-133">hello following sections show you how to:</span></span>

* <span data-ttu-id="1f415-134">de factory, de productielijnen, de OEE van stations en de KPI-waarden controleert;</span><span class="sxs-lookup"><span data-stu-id="1f415-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="1f415-135">Hallo telemetrische gegevens gegenereerd op basis van deze apparaten met behulp van Azure Time Series Insights analyseren</span><span class="sxs-lookup"><span data-stu-id="1f415-135">Analyze hello telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="1f415-136">Reageren op waarschuwingen toofix problemen</span><span class="sxs-lookup"><span data-stu-id="1f415-136">Act on alerts toofix issues</span></span>

<span data-ttu-id="1f415-137">Een belangrijke functie van dit scenario is dat u al deze acties extern vanuit Hallo oplossing dashboard uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="1f415-137">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="1f415-138">U hoeft geen fysieke toegang toohello apparaten.</span><span class="sxs-lookup"><span data-stu-id="1f415-138">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="1f415-139">Dashboard van oplossing Hallo weergeven</span><span class="sxs-lookup"><span data-stu-id="1f415-139">View hello solution dashboard</span></span>

<span data-ttu-id="1f415-140">Hallo oplossing dashboard kunt u toomanage Hallo geïmplementeerd oplossing.</span><span class="sxs-lookup"><span data-stu-id="1f415-140">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="1f415-141">Het is een hiërarchische weergave van een overkoepelende factoryconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="1f415-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="1f415-142">U kunt bijvoorbeeld de OEE en KPI's weergeven, nieuwe knooppunten voor telemetrie publiceren en waarschuwingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1f415-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="1f415-143">Wanneer Hallo inrichten is voltooid en Hallo tegel voor uw vooraf geconfigureerde oplossing geeft **gereed**, kies **starten** tooopen uw oplossingsportal verbonden factory in een nieuw tabblad.</span><span class="sxs-lookup"><span data-stu-id="1f415-143">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your connected factory solution portal in a new tab.</span></span>

    ![Hallo vooraf geconfigureerde oplossing starten][img-launch-solution]

1. <span data-ttu-id="1f415-145">Standaard ziet u de oplossingsportal Hallo Hallo *dashboard*.</span><span class="sxs-lookup"><span data-stu-id="1f415-145">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="1f415-146">toonavigate tooother gebieden van Hallo portal gebruik Hallo menu aan de linkerkant Hallo van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="1f415-146">toonavigate tooother areas of hello portal, use hello menu on hello left-hand side of hello page.</span></span>

    ![Dashboard van de vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-menu]

<span data-ttu-id="1f415-148">Hallo dashboard toont de Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="1f415-148">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="1f415-149">Een **Factory lijst** Configuratiescherm waarin Hallo status, de locatie en de huidige productconfiguratie in Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="1f415-149">A **Factory list** panel that shows hello status, location, and current production configuration in hello solution.</span></span> <span data-ttu-id="1f415-150">Wanneer u Hallo oplossing voor het eerst uitvoert, moet u er een aantal gesimuleerde apparaten zijn.</span><span class="sxs-lookup"><span data-stu-id="1f415-150">When you first run hello solution, there are a number of simulated devices.</span></span> <span data-ttu-id="1f415-151">Hallo productie regel simulatie bestaat uit drie echte OPC UA servers per regel productie die gesimuleerde taken uitvoeren en gegevens delen.</span><span class="sxs-lookup"><span data-stu-id="1f415-151">hello production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="1f415-152">Zie voor meer informatie over OPC UA Hallo [verbonden factory Veelgestelde vragen over](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="1f415-152">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="1f415-153">Een **kaart** dat Hiermee Hallo locatie van elk apparaat toohello oplossing verbonden.</span><span class="sxs-lookup"><span data-stu-id="1f415-153">A **map** that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="1f415-154">Hallo-oplossing kunt Hallo Bing kaarten-API tooplot informatie gebruiken op Hallo-kaart.</span><span class="sxs-lookup"><span data-stu-id="1f415-154">hello solution can use hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="1f415-155">Als de Bing Kaarten Enterprise-API is ingeschakeld voor uw abonnement, wordt deze functie automatisch gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1f415-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="1f415-156">Als dit niet het geval is, Zie Hallo [Veelgestelde vragen over] [ lnk-faq] toolearn hoe toomake kaart dynamische Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f415-156">If not, see hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="1f415-157">Een paneel **Waarschuwingen** dat waarschuwingen weergeeft die worden gegenereerd wanneer een telemetrie- of OEE-/KPI-waarde een bepaalde drempelwaarde overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="1f415-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="1f415-158">Een **algehele apparatuur efficiëntie** Configuratiescherm die toont Hallo OEE waarden voor de hele onderneming Hallo of Hallo productie-factory regel/station u bekijkt.</span><span class="sxs-lookup"><span data-stu-id="1f415-158">An **Overall Equipment Efficiency** panel that shows hello OEE values for hello whole enterprise, or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="1f415-159">Deze waarde wordt geaggregeerd van Hallo station weergave toohello enterprise niveau.</span><span class="sxs-lookup"><span data-stu-id="1f415-159">This value is aggregated from hello station view toohello enterprise level.</span></span> <span data-ttu-id="1f415-160">Hallo OEE afbeelding en de bijbehorende samenstellende elementen kunnen verder worden geanalyseerd.</span><span class="sxs-lookup"><span data-stu-id="1f415-160">hello OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="1f415-161">**Key Performance Indicators** bekijkt hello aantal geproduceerde eenheden en energie gebruikt door de hele onderneming Hallo of Hallo productie-factory regel/station u paneel.</span><span class="sxs-lookup"><span data-stu-id="1f415-161">**Key Performance Indicators** panel that displays hello number of units produced and energy used by hello whole enterprise or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="1f415-162">Deze waarden worden van een station weergave toohello enterprise-niveau samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="1f415-162">These values are aggregated from a station view toohello enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="1f415-163">Factory's weergeven</span><span class="sxs-lookup"><span data-stu-id="1f415-163">View factories</span></span>

<span data-ttu-id="1f415-164">Hallo *fabrieken* toont Hallo van geografische locatie van alle Hallo fabrieken in Hallo-oplossing, hun status en de huidige productconfiguratie van het deelvenster.</span><span class="sxs-lookup"><span data-stu-id="1f415-164">hello *Factories* panel shows you hello geographical location of all hello factories in hello solution, their status, and current production configuration.</span></span> <span data-ttu-id="1f415-165">Uit Hallo locaties lijst, kunt u toohello andere niveaus in Hallo oplossing hiërarchie navigeren.</span><span class="sxs-lookup"><span data-stu-id="1f415-165">From hello locations list, you can navigate toohello other levels in hello solution hierarchy.</span></span> <span data-ttu-id="1f415-166">Hallo rijen in de lijst Hallo zijn hyperlinks die een koppeling details van Hallo productie regels op die locatie.</span><span class="sxs-lookup"><span data-stu-id="1f415-166">hello rows in hello list are hyperlinks that link details of hello production lines at that location.</span></span> <span data-ttu-id="1f415-167">Is deze mogelijk toodrill in productie-regeldetails Hallo en omlaag weergave toohello station niveau.</span><span class="sxs-lookup"><span data-stu-id="1f415-167">It is then possible toodrill into hello production line details and down toohello station level view.</span></span> <span data-ttu-id="1f415-168">U kunt ook een filterlijst toohello toepassen.</span><span class="sxs-lookup"><span data-stu-id="1f415-168">You can also apply a filter toohello list.</span></span>

![Factory's van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-factories] 

1. <span data-ttu-id="1f415-170">Hallo **Factory Configuratiescherm** toont Hallo lijst van de fabriek voor deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="1f415-170">hello **Factory panel** shows hello factory list for this solution.</span></span>

2. <span data-ttu-id="1f415-171">Hallo factory lijst geeft in eerste instantie zes factory's die zijn gemaakt door Hallo inrichtingsproces.</span><span class="sxs-lookup"><span data-stu-id="1f415-171">hello factory list initially shows six factories created by hello provisioning process.</span></span> <span data-ttu-id="1f415-172">U kunt extra gesimuleerde en fysieke apparaten toohello oplossing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1f415-172">You can add additional simulated and physical devices toohello solution.</span></span>

3. <span data-ttu-id="1f415-173">tooview hello details van een fabriek, klikt u op Hallo rij in Hallo factory lijst.</span><span class="sxs-lookup"><span data-stu-id="1f415-173">tooview hello details of a factory, click hello row in hello factory list.</span></span>

4. <span data-ttu-id="1f415-174">tooview hello details van een regel voor productie, klikt u op Hallo rij in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f415-174">tooview hello details of a production line, click hello row in hello list.</span></span>

5. <span data-ttu-id="1f415-175">tooview hello OPC UA-knooppunten van een station op Hallo productie regel gepubliceerd, klikt u op Hallo rij in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f415-175">tooview hello published OPC UA nodes of a station on hello production line, click hello row in hello list.</span></span>

6. <span data-ttu-id="1f415-176">tooview op een specifiek knooppunt in het Hallo-station, klikt u op Hallo rij in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f415-176">tooview details on a specific node in hello station, click hello row in hello list.</span></span> <span data-ttu-id="1f415-177">Deze actie wordt gestart Hallo context Configuratiescherm met Time Series Insights visualisaties.</span><span class="sxs-lookup"><span data-stu-id="1f415-177">This action launches hello context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="1f415-178">Klik op deze grafieken toodo verdere analyse in Hallo Time Series Insights explorer-omgeving.</span><span class="sxs-lookup"><span data-stu-id="1f415-178">Click these graphs toodo further analysis in hello Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="1f415-179">Kaart weergeven</span><span class="sxs-lookup"><span data-stu-id="1f415-179">View map</span></span>

<span data-ttu-id="1f415-180">Als uw abonnement toegang toohello Bing kaarten-API heeft, Hallo *fabrieken* kaart toont u Hallo geografische locatie en status van alle Hallo fabrieken in Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="1f415-180">If your subscription has access toohello Bing Maps API, hello *Factories* map shows you hello geographical location and status of all hello factories in hello solution.</span></span> <span data-ttu-id="1f415-181">toodrill op Hallo locatiegegevens, klikt u op Hallo locaties op Hallo kaart weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1f415-181">toodrill into hello location details, click hello locations displayed on hello map.</span></span>

![Kaart van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="1f415-183">Waarschuwingen weergeven</span><span class="sxs-lookup"><span data-stu-id="1f415-183">View alerts</span></span>

<span data-ttu-id="1f415-184">Hallo **waarschuwing** deelvenster ziet u de waarschuwingen die worden gegenereerd vanwege tooa gerapporteerd waarde of een berekende OEE/KPI-waarde van meer dan de geconfigureerde drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="1f415-184">hello **Alert** panel shows you alerts generated due tooa reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="1f415-185">Dit deelvenster geeft waarschuwingen weer op elk niveau van de hiërarchie hello, van Hallo station weergave niveau toohello globale weergave.</span><span class="sxs-lookup"><span data-stu-id="1f415-185">This panel displays alerts at each level of hello hierarchy, from hello station level view toohello global view.</span></span> <span data-ttu-id="1f415-186">Hallo-berichten bevatten een beschrijving van waarschuwing hello, datum, tijd, locatie en het aantal exemplaren.</span><span class="sxs-lookup"><span data-stu-id="1f415-186">hello alerts contain a description of hello alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="1f415-187">Kan krijgt u inzicht in toohello gegevens die met behulp van Hallo Time Series-inzichtgegevens Hallo-waarschuwing heeft veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="1f415-187">You can gain insights in toohello data that caused hello alert using hello Time Series Insights data.</span></span> <span data-ttu-id="1f415-188">Hallo Time Series Insights gegevens worden weergegeven in Hallo waarschuwingen, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="1f415-188">hello Time Series Insights data is visualized in hello alerts where applicable.</span></span> <span data-ttu-id="1f415-189">Als u een beheerder bent, kunt u de standaardacties uitvoeren op Hallo van waarschuwingen, zoals:</span><span class="sxs-lookup"><span data-stu-id="1f415-189">If you are an Administrator, you can take default actions on hello alerts such as:</span></span>

* <span data-ttu-id="1f415-190">Waarschuwing sluiten Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f415-190">Close hello alert.</span></span>
* <span data-ttu-id="1f415-191">Begrijp Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="1f415-191">Acknowledge hello alert.</span></span>

<span data-ttu-id="1f415-192">Eventueel kunt u complexere acties uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1f415-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="1f415-193">Voor Hallo druk OPC UA knooppunt Hallo Assembly kan u bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1f415-193">For example, for hello Pressure OPC UA Node of hello Assembly you could:</span></span>

* <span data-ttu-id="1f415-194">Ondersteunende informatie weergeven op een webpagina in een nieuw browservenster.</span><span class="sxs-lookup"><span data-stu-id="1f415-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="1f415-195">Hallo oorzaak van de waarschuwing Hallo beperken door het aanroepen van een methode OPC UA op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="1f415-195">Mitigate hello cause of hello alert by calling an OPC UA method on hello device.</span></span>
* <span data-ttu-id="1f415-196">Hallo-beschikbaarheid van Hallo standaardacties onderdrukken.</span><span class="sxs-lookup"><span data-stu-id="1f415-196">Suppress hello availability of hello default actions.</span></span>

    ![Waarschuwingen van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="1f415-198">Deze waarschuwingen worden gegenereerd door regels die zijn opgegeven in een configuratiebestand in Hallo vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="1f415-198">These alerts are generated by rules that are specified in a configuration file in hello preconfigured solution.</span></span> <span data-ttu-id="1f415-199">Deze regels kunnen waarschuwingen genereren wanneer Hallo OEE of KPI cijfers of OPC UA knooppunt waarden de geconfigureerde drempelwaarde overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="1f415-199">These rules can generate alerts when hello OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="1f415-200">Hallo **waarschuwingen Configuratiescherm** toont Hallo waarschuwingen gegenereerd in deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="1f415-200">hello **Alerts panel** shows hello alerts generated in this solution.</span></span>

2. <span data-ttu-id="1f415-201">tooview hello details van een waarschuwing, klik op Hallo-waarschuwing in Hallo waarschuwingen Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="1f415-201">tooview hello details of an alert, click hello alert in hello alerts panel.</span></span>

3. <span data-ttu-id="1f415-202">toofurther hello waarschuwingsgegevens analyseren, klikt u op Hallo grafiek in Hallo waarschuwing Configuratiescherm tooopen Hallo Time Series Insights explorer-omgeving.</span><span class="sxs-lookup"><span data-stu-id="1f415-202">toofurther analyze hello alert data, click hello graph in hello alert panel tooopen hello Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="1f415-203">tooaddress Hallo waarschuwing, verschillende acties zijn beschikbaar in de waarschuwing deelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f415-203">tooaddress hello alert, several actions are available in hello alert panel.</span></span> <span data-ttu-id="1f415-204">Kies de gewenste optie Hallo voor u en klikt u op Hallo opdrachtknop actie uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1f415-204">Choose hello appropriate option for you and click hello execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="1f415-205">Algemene apparatuurefficiëntie weergeven</span><span class="sxs-lookup"><span data-stu-id="1f415-205">View overall equipment efficiency</span></span>

<span data-ttu-id="1f415-206">OEE tarieven Hallo efficiëntie Hallo fabricageproces met behulp van een sleutel operationele gerelateerd aan de productie-parameters.</span><span class="sxs-lookup"><span data-stu-id="1f415-206">OEE rates hello efficiency of hello manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="1f415-207">OEE is een industrie standaardeenheid berekend door vermenigvuldiging tarief hello, frequentie van de prestaties en kwaliteit snelheid: OEE = beschikbaarheid x prestaties x kwaliteit.</span><span class="sxs-lookup"><span data-stu-id="1f415-207">OEE is an industry standard measure calculated by multiplying hello availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![OEE van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-oee]

1. <span data-ttu-id="1f415-209">tooview OEE voor elk niveau in de hiërarchie hello, navigeer toohello specifieke weergave die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="1f415-209">tooview OEE for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="1f415-210">Hallo OEE voor deze weergave wordt weergegeven in Configuratiescherm samen met elk van de Hallo elementen waaruit percentage OEE Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f415-210">hello OEE for that view displays in hello panel along with each of hello elements that make up hello OEE percentage.</span></span>

2. <span data-ttu-id="1f415-211">toofurther hello OEE voor elk niveau in Hallo hiërarchiegegevens analyseren, klikt u op Hallo OEE, beschikbaarheid, prestaties of kwaliteit percentage.</span><span class="sxs-lookup"><span data-stu-id="1f415-211">toofurther analyze hello OEE for any level in hello hierarchy data, click either hello OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="1f415-212">Een context paneel wordt weergegeven met Time Series Insights voeding visualisaties waarin gegevens uit Hallo laatste uur, de afgelopen 24 uur en de afgelopen 7 dagen.</span><span class="sxs-lookup"><span data-stu-id="1f415-212">A context panel appears with Time Series Insights powered visualizations that shows data from hello last hour, last 24 hours, and last 7 days.</span></span>

    ![TSI-visualisatie van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-tsi-visualization]

3. <span data-ttu-id="1f415-214">toofurther hello waarschuwingsgegevens analyseren, klikt u op Hallo grafiek in Hallo waarschuwing Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="1f415-214">toofurther analyze hello alert data, click hello graph in hello alert panel.</span></span> <span data-ttu-id="1f415-215">Deze actie wordt geopend Hallo Time Series Insights explorer-omgeving.</span><span class="sxs-lookup"><span data-stu-id="1f415-215">This action opens hello Time Series Insights explorer environment.</span></span>

    ![TSI-verkenner van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="1f415-217">Key performance indicators weergeven</span><span class="sxs-lookup"><span data-stu-id="1f415-217">View Key Performance Indicators</span></span>

<span data-ttu-id="1f415-218">Hallo-oplossing biedt twee prestatie-indicatoren *eenheden per uur* en *energieverbruik in kWh*.</span><span class="sxs-lookup"><span data-stu-id="1f415-218">hello solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![KPI van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-kpi]

1. <span data-ttu-id="1f415-220">tooview eenheden per uur of energie gebruikt voor elk niveau in de hiërarchie hello, navigeer toohello specifieke weergave die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="1f415-220">tooview units per hour or energy used for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="1f415-221">Hallo-eenheden per uur en energie weergeven in Hallo Configuratiescherm gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1f415-221">hello units per hour and energy used display in hello panel.</span></span>

2. <span data-ttu-id="1f415-222">tooanalyze eenheden per uur of energie gebruikt voor elk niveau in Hallo hiërarchie verdere, klikt u op Hallo meter in Hallo **Key Performance Indicators** Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="1f415-222">tooanalyze units per hour or energy used for any level in hello hierarchy further, click hello gauge in hello **Key Performance Indicators** panel.</span></span> <span data-ttu-id="1f415-223">Een paneel context weergegeven met Time Series Insights ingeschakeld visualisaties zodat u tooview gegevens van Hallo afgelopen uur Hallo afgelopen 24 uur en de afgelopen 7 dagen.</span><span class="sxs-lookup"><span data-stu-id="1f415-223">A context panel appears with Time Series Insights powered visualizations enabling you tooview data from hello last hour, hello last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="1f415-224">Samenvatting van scenario</span><span class="sxs-lookup"><span data-stu-id="1f415-224">Scenario review</span></span>

<span data-ttu-id="1f415-225">In dit scenario moet u uw fabrieken OEE en KPI's waarden, Hallo dashboard bewaakt.</span><span class="sxs-lookup"><span data-stu-id="1f415-225">In this scenario, you monitored your factories OEE and KPIs values, in hello dashboard.</span></span> <span data-ttu-id="1f415-226">U vervolgens gebruikt Time Series Insights tooprovide meer informatie toohelp lager niveau verder Hallo telemetriegegevens voor OEE en KPI's toohelp met afwijkingen detecteren.</span><span class="sxs-lookup"><span data-stu-id="1f415-226">You then used Time Series Insights tooprovide more information toohelp drill further into hello telemetry data for OEE and KPIs toohelp with detecting anomalies.</span></span> <span data-ttu-id="1f415-227">U gebruikt ook Hallo waarschuwing Configuratiescherm tooview problemen met uw fabrieken en u Hallo acties beschikbaar tooyou tooresolve Hallo waarschuwing gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1f415-227">You also used hello alert panel tooview issues with your factories and you used hello actions available tooyou tooresolve hello alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="1f415-228">Andere functies</span><span class="sxs-lookup"><span data-stu-id="1f415-228">Other features</span></span>

<span data-ttu-id="1f415-229">Hallo volgende secties worden enkele aanvullende functies van Hallo verbonden factory-oplossing die niet zijn beschreven in het voorgaande scenario Hallo beschreven.</span><span class="sxs-lookup"><span data-stu-id="1f415-229">hello following sections describe some additional features of hello connected factory solution that are not described in hello previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="1f415-230">Filters toepassen</span><span class="sxs-lookup"><span data-stu-id="1f415-230">Apply filters</span></span>

1. <span data-ttu-id="1f415-231">Klik op Hallo **punthaak** toodisplay een lijst met beschikbare filters in ofwel Hallo factory locaties deelvenster of Hallo waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="1f415-231">Click hello **chevron** toodisplay a list of available filters in either hello factory locations panel or hello alerts panel.</span></span>

2. <span data-ttu-id="1f415-232">Hallo filters deelvenster wordt weergegeven voor u.</span><span class="sxs-lookup"><span data-stu-id="1f415-232">hello filters panel is displayed for you.</span></span> 

    ![Filters van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-alert-filter]

3. <span data-ttu-id="1f415-234">Kies Hallo filter die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="1f415-234">Choose hello filter that you require.</span></span> <span data-ttu-id="1f415-235">Het is ook mogelijk tootype vrije tekst in Hallo filtervelden.</span><span class="sxs-lookup"><span data-stu-id="1f415-235">It is also possible tootype free text into hello filter fields.</span></span>

4. <span data-ttu-id="1f415-236">Hallo-filter wordt vervolgens toegepast voor u.</span><span class="sxs-lookup"><span data-stu-id="1f415-236">hello filter is then applied for you.</span></span> <span data-ttu-id="1f415-237">Hallo-filterstatus wordt ook weergegeven in het dashboard Hallo via een trechter die wordt weergegeven in Hallo fabrieken en waarschuwt tabellen.</span><span class="sxs-lookup"><span data-stu-id="1f415-237">hello filter state is also shown in hello dashboard via a funnel that displays in hello factories and alerts tables.</span></span>

    ![Filters van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="1f415-239">Een actieve filter heeft geen invloed op de waarden van Hallo weergegeven OEE en KPI's, het Hallo lijstinhoud alleen wordt gefilterd.</span><span class="sxs-lookup"><span data-stu-id="1f415-239">An active filter does not affect hello displayed OEE and KPI values, it only filters hello list contents.</span></span>

5. <span data-ttu-id="1f415-240">een filter tooclear Hallo trechter en klik op filter in het deelvenster Hallo filter-context.</span><span class="sxs-lookup"><span data-stu-id="1f415-240">tooclear a filter, click hello funnel and click filter in hello filter context panel.</span></span> <span data-ttu-id="1f415-241">tekst Hello **alle** wordt weergegeven in Hallo fabrieken en waarschuwingen tabellen.</span><span class="sxs-lookup"><span data-stu-id="1f415-241">hello text **All** is displayed in hello factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="1f415-242">Door een OPC UA-server bladeren</span><span class="sxs-lookup"><span data-stu-id="1f415-242">Browse an OPC UA server</span></span>

<span data-ttu-id="1f415-243">Wanneer u Hallo vooraf geconfigureerde oplossing implementeert, worden automatisch gesimuleerde OPC UA-servers die u via Hallo oplossing browser bladeren kunt inrichten.</span><span class="sxs-lookup"><span data-stu-id="1f415-243">When you deploy hello preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via hello solution browser.</span></span> <span data-ttu-id="1f415-244">Deze servers zijn *gesimuleerde OPC UA-servers*.</span><span class="sxs-lookup"><span data-stu-id="1f415-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="1f415-245">Gesimuleerde servers maakt het eenvoudig voor u tooexperiment met Hallo vooraf geconfigureerde oplossing zonder Hallo nodig toodeploy echte servers.</span><span class="sxs-lookup"><span data-stu-id="1f415-245">Simulated servers make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical servers.</span></span> <span data-ttu-id="1f415-246">Als u dat een echte OPC UA toohello serveroplossing tooconnect wilt, raadpleegt u Hallo [uw OPC UA apparaat toohello verbonden factory vooraf geconfigureerde oplossing verbinden] [ lnk-connect-cf] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="1f415-246">If you do want tooconnect a real OPC UA server toohello solution, see hello [Connect your OPC UA device toohello connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="1f415-247">Klik op Hallo **factory pictogram** in de navigatiebalk Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="1f415-247">Click hello **factory icon** in hello dashboard navigation bar.</span></span>

    ![Serverbrowser van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-server-browser]

2. <span data-ttu-id="1f415-249">Kies een van de servers Hallo uit Hallo vooraf geconfigureerde lijst.</span><span class="sxs-lookup"><span data-stu-id="1f415-249">Choose one of hello servers from hello preconfigured list.</span></span> <span data-ttu-id="1f415-250">Deze lijst bevat Hallo-servers die in Hallo vooraf geconfigureerde oplossing voor u zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="1f415-250">This list shows hello servers that are deployed for you in hello preconfigured solution.</span></span>

    ![Serverselectie van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-server-choice]

3. <span data-ttu-id="1f415-252">Klik op **Verbinden**. Er wordt een beveiligingsdialoogvenster weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1f415-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="1f415-253">Voor de simulatie hello, is het veilig tooclick **doorgaan**</span><span class="sxs-lookup"><span data-stu-id="1f415-253">For hello simulation, it is safe tooclick **Proceed**</span></span>

4. <span data-ttu-id="1f415-254">tooexpand hello knooppunten in de serverstructuur hello, klikt u op.</span><span class="sxs-lookup"><span data-stu-id="1f415-254">tooexpand any of hello nodes in hello server tree, click it.</span></span> <span data-ttu-id="1f415-255">Naast knooppunten die telemetrie publiceren, staat een vinkje.</span><span class="sxs-lookup"><span data-stu-id="1f415-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![Serverstructuur van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-server-tree]

5. <span data-ttu-id="1f415-257">Met de rechtermuisknop op een item tooread, schrijven, publiceren of aanroepen van dat knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1f415-257">Right-click an item tooread, write, publish, or call that node.</span></span> <span data-ttu-id="1f415-258">Hallo acties beschikbaar tooyou, is afhankelijk van uw machtigingen en kenmerken van knooppunt Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f415-258">hello actions available tooyou depend on your permissions and hello attributes of hello node.</span></span> <span data-ttu-id="1f415-259">Hallo lezen optie toodisplays een context paneel Hallo-waarde van een specifiek knooppunt Hallo weergeeft.</span><span class="sxs-lookup"><span data-stu-id="1f415-259">hello read option toodisplays a context panel showing hello value of hello specific node.</span></span> <span data-ttu-id="1f415-260">Hallo schrijven optie geeft een context paneel waarin u een nieuwe waarde kunt invoeren.</span><span class="sxs-lookup"><span data-stu-id="1f415-260">hello write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="1f415-261">Hallo aanroep optie bevat een knooppunt waarin u Hallo parameters voor Hallo-aanroep invoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="1f415-261">hello call option displays a node where you can enter hello parameters for hello call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="1f415-262">Een knooppunt publiceren</span><span class="sxs-lookup"><span data-stu-id="1f415-262">Publish a node</span></span>

<span data-ttu-id="1f415-263">Wanneer u bladert een *gesimuleerde OPC UA-server*, u kunt ook toopublish nieuwe knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1f415-263">When you browse a *simulated OPC UA server*, you can also choose toopublish new nodes.</span></span> <span data-ttu-id="1f415-264">U kunt analyseren Hallo telemetrie van deze knooppunten in het Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="1f415-264">You can analyze hello telemetry from these nodes in hello solution.</span></span> <span data-ttu-id="1f415-265">Deze *OPC UA-servers in de simulatie* eenvoudig tooexperiment met Hallo vooraf geconfigureerde oplossing maken zonder het echte apparaten implementeren.</span><span class="sxs-lookup"><span data-stu-id="1f415-265">These *simulated OPC UA servers* make it easy tooexperiment with hello preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="1f415-266">Blader tooa knooppunt in Hallo OPC UA browser serverstructuur gewenste toopublish.</span><span class="sxs-lookup"><span data-stu-id="1f415-266">Browse tooa node in hello OPC UA server browser tree that you wish toopublish.</span></span>

2. <span data-ttu-id="1f415-267">Met de rechtermuisknop op Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1f415-267">Right-click hello node.</span></span>

3. <span data-ttu-id="1f415-268">Kies **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="1f415-268">Choose **Publish**.</span></span>

    ![Verbonden factory publiceert knooppunt][cf-img-publish-node]

4. <span data-ttu-id="1f415-270">Een paneel context wordt weergegeven dat aangeeft dat Hallo publiceren is voltooid.</span><span class="sxs-lookup"><span data-stu-id="1f415-270">A context panel appears which tells you that hello publish has succeeded.</span></span> <span data-ttu-id="1f415-271">Hallo-knooppunt wordt weergegeven in Hallo station weergave van niveau met een vinkje.</span><span class="sxs-lookup"><span data-stu-id="1f415-271">hello node appears in hello station level view with a check mark beside it.</span></span>

    ![Succesvolle publicatie van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="1f415-273">Opdracht en controle</span><span class="sxs-lookup"><span data-stu-id="1f415-273">Command and control</span></span>

<span data-ttu-id="1f415-274">Hallo verbonden factory kunt u de opdracht en beheren van uw apparaten bedrijfstak rechtstreeks vanuit de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f415-274">hello connected factory allows you command and control your industry devices directly from hello cloud.</span></span> <span data-ttu-id="1f415-275">U kunt deze functie toorespond tooalerts gegenereerd door Hallo-apparaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1f415-275">You can use this feature toorespond tooalerts generated by hello device.</span></span> <span data-ttu-id="1f415-276">U kan bijvoorbeeld een opdracht toohello apparaat verzenden vanuit Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="1f415-276">For example, you could send a command toohello device from hello cloud.</span></span> <span data-ttu-id="1f415-277">U vindt Hallo beschikbare opdrachten in Hallo **StationCommands** knooppunt in Hallo OPC UA servers browser structuur.</span><span class="sxs-lookup"><span data-stu-id="1f415-277">You can find hello available commands in hello **StationCommands** node in hello OPC UA servers browser tree.</span></span> <span data-ttu-id="1f415-278">In dit scenario moet u een zware belasting release klep op Hallo assembly station van een regel productie in München openen.</span><span class="sxs-lookup"><span data-stu-id="1f415-278">In this scenario, you open a pressure release valve on hello assembly station of a production line in Munich.</span></span> <span data-ttu-id="1f415-279">toouse hello opdracht en controle functionaliteit, moet u in Hallo **beheerder** rol voor Hallo vooraf geconfigureerde oplossing voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="1f415-279">toouse hello command and control functionality, you must be in hello **Administrator** role for hello preconfigured solution deployment.</span></span>

1. <span data-ttu-id="1f415-280">Blader toohello **StationCommands** knooppunt in Hallo OPC UA-server browser-structuur.</span><span class="sxs-lookup"><span data-stu-id="1f415-280">Browse toohello **StationCommands** node in hello OPC UA server browser tree.</span></span>

2. <span data-ttu-id="1f415-281">Hallo kiest dat u gebruiken wilt.</span><span class="sxs-lookup"><span data-stu-id="1f415-281">Choose hello command that you wish use.</span></span>

3. <span data-ttu-id="1f415-282">Met de rechtermuisknop op Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1f415-282">Right-click hello node.</span></span>

4. <span data-ttu-id="1f415-283">Kies **Aanroepen**.</span><span class="sxs-lookup"><span data-stu-id="1f415-283">Choose **Call**.</span></span>

    ![Aanroepopdracht van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-call-command]

5. <span data-ttu-id="1f415-285">Een context paneel wordt weergegeven waarin wordt gemeld welke methode u gaat toocall en eventuele details van de parameter is van toepassing.</span><span class="sxs-lookup"><span data-stu-id="1f415-285">A context panel appears informing you which method you are about toocall and any parameter details is applicable.</span></span>

6. <span data-ttu-id="1f415-286">Kies **Aanroepen**.</span><span class="sxs-lookup"><span data-stu-id="1f415-286">Choose **Call**.</span></span>

    ![Aanroepcontext van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-call-context]

7. <span data-ttu-id="1f415-288">Hallo context deelvenster is bijgewerkte tooinform dat Hallo methodeaanroep is voltooid.</span><span class="sxs-lookup"><span data-stu-id="1f415-288">hello context panel is updated tooinform you that hello method call succeeded.</span></span> <span data-ttu-id="1f415-289">U kunt controleren of Hallo-aanroep is voltooid door te lezen Hallo-waarde van Hallo zware belasting op het knooppunt dat als gevolg van het Hallo-aanroep bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="1f415-289">You can verify hello call succeeded by reading hello value of hello pressure node that updated as a result of hello call.</span></span>

    ![Aanroepen voltooid van vooraf geconfigureerde oplossing voor verbonden factory's][cf-img-call-success]


## <a name="behind-hello-scenes"></a><span data-ttu-id="1f415-291">Achter de schermen Hallo</span><span class="sxs-lookup"><span data-stu-id="1f415-291">Behind hello scenes</span></span>

<span data-ttu-id="1f415-292">Wanneer u een vooraf geconfigureerde oplossing implementeert, maakt Hallo implementatieproces meerdere resources in hello Azure-abonnement u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="1f415-292">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="1f415-293">U kunt deze resources weergeven in hello Azure [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="1f415-293">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="1f415-294">Hallo-implementatieproces maakt een **resourcegroep** met een naam op basis van Hallo-naam die u voor uw vooraf geconfigureerde oplossing kiest:</span><span class="sxs-lookup"><span data-stu-id="1f415-294">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Vooraf geconfigureerde oplossing in hello Azure-portal][img-cf-portal]

<span data-ttu-id="1f415-296">U kunt instellingen Hallo van elke resource weergeven door deze te selecteren in lijst van resources in de resourcegroep Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f415-296">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="1f415-297">U kunt ook de broncode Hallo voor Hallo vooraf geconfigureerde oplossing weergeven.</span><span class="sxs-lookup"><span data-stu-id="1f415-297">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="1f415-298">Hallo verbonden factory vooraf geconfigureerde oplossing broncode is in Hallo [azure-iot-verbonden-factory] [ lnk-cfgithub] GitHub-opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="1f415-298">hello connected factory preconfigured solution source code is in hello [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="1f415-299">Wanneer u klaar bent, kunt u Hallo vooraf geconfigureerde oplossing verwijderen uit uw Azure-abonnement op Hallo [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="1f415-299">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="1f415-300">Deze site kunt u alle resources die zijn ingericht toen u Hallo vooraf geconfigureerde oplossing maakte Hallo tooeasily-verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1f415-300">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="1f415-301">tooensure u Alles verwijderen gerelateerde toohello vooraf geconfigureerde oplossing, te verwijderen op Hallo [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="1f415-301">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="1f415-302">Hallo-resourcegroep in Hallo portal niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1f415-302">Do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f415-303">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1f415-303">Next Steps</span></span>

<span data-ttu-id="1f415-304">Nu dat u een werkende vooraf geconfigureerde oplossing hebt geïmplementeerd, kunt u blijven aan de slag met IoT Suite door te lezen Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1f415-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="1f415-305">[Overzicht van de vooraf geconfigureerde oplossing voor verbonden factory's][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="1f415-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="1f415-306">[Uw apparaat toohello verbonden factory vooraf geconfigureerde oplossing verbinden][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="1f415-306">[Connect your device toohello Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="1f415-307">[Machtigingen op Hallo azureiotsuite.com site][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="1f415-307">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

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
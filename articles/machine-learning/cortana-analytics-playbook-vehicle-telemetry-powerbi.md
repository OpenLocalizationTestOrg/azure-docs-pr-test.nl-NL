---
title: aaaPower BI-Dashboard van de status van de drager en groot gewoonten - Azure | Microsoft Docs
description: Hallo-mogelijkheden van Cortana Intelligence toogain real-time en voorspellende inzicht op vehicle health gebruiken en gewoonten besturen.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="d87a7-103">Vehicle telemetrie analytics-oplossing sjabloon Power BI-Dashboard installatie-instructies</span><span class="sxs-lookup"><span data-stu-id="d87a7-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="d87a7-104">Dit **menu** toohello hoofdstukken in deze playbook koppelingen.</span><span class="sxs-lookup"><span data-stu-id="d87a7-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="d87a7-105">Hallo Vehicle telemetrie Analytics-oplossing gepresenteerd hoe auto dealerbedrijven, auto fabrikanten en ondernemingen van Hallo-mogelijkheden van Cortana Intelligence toogain real-time en voorspellende insights op de drager gezondheid en groot gebruikmaken kunnen verbeteringen in Hallo gebied toodrive van klant gewoonten ervaren R & D- en marketingcampagnes.</span><span class="sxs-lookup"><span data-stu-id="d87a7-105">hello Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits toodrive improvements in hello area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="d87a7-106">Dit document bevat stapsgewijze instructies over hoe u Hallo Power BI-rapporten en dashboards configureren kunt zodra Hallo-oplossing is geïmplementeerd in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="d87a7-106">This document contains step by step instructions on how you can configure hello Power BI reports and dashboard once hello solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d87a7-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d87a7-107">Prerequisites</span></span>
1. <span data-ttu-id="d87a7-108">Hallo implementeren [telemetrie Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) oplossing</span><span class="sxs-lookup"><span data-stu-id="d87a7-108">Deploy hello [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="d87a7-109">Installeren van Microsoft Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="d87a7-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="d87a7-110">Een [Azure-abonnement](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d87a7-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="d87a7-111">Als u geen Azure-abonnement hebt, aan de slag met de gratis Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="d87a7-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="d87a7-112">Microsoft Power BI-account</span><span class="sxs-lookup"><span data-stu-id="d87a7-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="d87a7-113">Cortana Intelligence Suite-onderdelen</span><span class="sxs-lookup"><span data-stu-id="d87a7-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="d87a7-114">Hallo na Cortana Intelligence-services worden als onderdeel van Hallo Vehicle telemetrie Analytics oplossingssjabloon geïmplementeerd in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="d87a7-114">As part of hello Vehicle Telemetry Analytics solution template, hello following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="d87a7-115">**Event Hub** voor het opnemen van miljoenen vehicle telemetrische gebeurtenissen in Azure.</span><span class="sxs-lookup"><span data-stu-id="d87a7-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="d87a7-116">**Stream Analytics** voor realtime-inzichten op vehicle gezondheid en dat de gegevens zich blijft voordoen in langdurige opslag voor uitgebreidere batch analyses.</span><span class="sxs-lookup"><span data-stu-id="d87a7-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="d87a7-117">**Machine Learning** voor afwijkingsdetectie in realtime en batchverwerking toogain voorspellende insights.</span><span class="sxs-lookup"><span data-stu-id="d87a7-117">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="d87a7-118">**HDInsight** gegevens over tootransform op grote schaal is</span><span class="sxs-lookup"><span data-stu-id="d87a7-118">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="d87a7-119">**Data Factory** verwerkt orchestration, planning, bronbeheer en controle van de pipeline voor Hallo batch verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d87a7-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>

<span data-ttu-id="d87a7-120">**Power BI** biedt deze oplossing een uitgebreide dashboard voor realtime-gegevens en visualisaties predictive analytics.</span><span class="sxs-lookup"><span data-stu-id="d87a7-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="d87a7-121">Hallo-oplossing maakt gebruik van twee verschillende gegevensbronnen: **gesimuleerde vehicle signalen en diagnostische gegevensset** en **vehicle catalogus**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-121">hello solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="d87a7-122">Er is een vehicle telematica simulator opgenomen als onderdeel van deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="d87a7-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="d87a7-123">Deze diagnostische gegevens verzendt en signalen bijbehorende toohello status van Hallo vehicle en groot patroon op een bepaald tijdstip.</span><span class="sxs-lookup"><span data-stu-id="d87a7-123">It emits diagnostic information and signals corresponding toohello state of hello vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="d87a7-124">Hallo Vehicle Catalog is een verwijzing gegevensset met VIN toomodel toewijzing</span><span class="sxs-lookup"><span data-stu-id="d87a7-124">hello Vehicle Catalog is a reference dataset containing VIN toomodel mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="d87a7-125">Voorbereiding van Power BI-Dashboard</span><span class="sxs-lookup"><span data-stu-id="d87a7-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="d87a7-126">Realtime Power BI-Dashboard instellen</span><span class="sxs-lookup"><span data-stu-id="d87a7-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="d87a7-127">**Hallo realtime dashboardtoepassing starten** nadat Hallo-implementatie is voltooid, moet u Hallo handmatige bewerking instructies volgen</span><span class="sxs-lookup"><span data-stu-id="d87a7-127">**Start hello real-time dashboard application** Once hello deployment is completed, you should follow hello Manual Operation Instructions</span></span>

* <span data-ttu-id="d87a7-128">Realtime dashboardtoepassing RealtimeDashboardApp.zip downloaden en uitpakken van het.</span><span class="sxs-lookup"><span data-stu-id="d87a7-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="d87a7-129">Open in de uitgepakte map hello, app configuratiebestand 'RealtimeDashboardApp.exe.config' vervangen appSettings voor verbindingen met de service Eventhub, Blob Storage en ML met Hallo waarden in Hallo handmatige bewerking instructies en sla uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="d87a7-129">In hello unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with hello values in hello Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="d87a7-130">Toepassing RealtimeDashboardApp.exe uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d87a7-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="d87a7-131">Een aanmeldingsvenster wordt pop-, geldige referenties van uw Power BI en klikt u op Hallo **accepteren** knop.</span><span class="sxs-lookup"><span data-stu-id="d87a7-131">A login window will pop up, provide your valid PowerBI credentials and click hello **Accept** button.</span></span> <span data-ttu-id="d87a7-132">Hallo app start vervolgens toorun.</span><span class="sxs-lookup"><span data-stu-id="d87a7-132">Then hello app will start toorun.</span></span>

   ![Aanmelden tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Machtigingen voor Power BI-Dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="d87a7-135">Aanmelding tooPowerBI website, en realtime dashboard maken.</span><span class="sxs-lookup"><span data-stu-id="d87a7-135">Login tooPowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="d87a7-136">Nu u bent klaar tooconfigure Hallo Power BI-dashboard met visualisaties uitgebreide toogain realtime en gewoonten voorspellende insights op de drager gezondheid en groot.</span><span class="sxs-lookup"><span data-stu-id="d87a7-136">Now, you are ready tooconfigure hello Power BI dashboard with rich visualizations toogain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="d87a7-137">Het duurt ongeveer 45 minuten tooan uur toocreate alle hello-rapporten en Hallo dashboard configureren.</span><span class="sxs-lookup"><span data-stu-id="d87a7-137">It takes about 45 minutes tooan hour toocreate all hello reports and configure hello dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="d87a7-138">Power BI-rapporten configureren</span><span class="sxs-lookup"><span data-stu-id="d87a7-138">Configure Power BI reports</span></span>
<span data-ttu-id="d87a7-139">over toocomplete 30 tot 45 minuten duren voordat het Hallo realtime rapporten en Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="d87a7-139">hello real-time reports and hello dashboard take about 30-45 minutes toocomplete.</span></span> <span data-ttu-id="d87a7-140">Te bladeren[http://powerbi.com](http://powerbi.com) en meld u aan.</span><span class="sxs-lookup"><span data-stu-id="d87a7-140">Browse too[http://powerbi.com](http://powerbi.com) and login.</span></span>

![Aanmelden tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="d87a7-142">Een nieuwe gegevensset wordt gegenereerd in Power BI.</span><span class="sxs-lookup"><span data-stu-id="d87a7-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="d87a7-143">Klik op Hallo **ConnectedCarsRealtime** gegevensset.</span><span class="sxs-lookup"><span data-stu-id="d87a7-143">Click hello **ConnectedCarsRealtime** dataset.</span></span>

![Geselecteerd verbonden realtime gegevensset voor auto 's](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="d87a7-145">Opslaan Hallo leeg rapport met **Ctrl + s**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-145">Save hello blank report using **Ctrl + s**.</span></span>

![Leeg rapport opslaan](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="d87a7-147">Geef de naam van rapport *Vehicle telemetrie Analytics realtime - rapporten*.</span><span class="sxs-lookup"><span data-stu-id="d87a7-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![Geef de naam van rapport](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="d87a7-149">Realtime-rapporten</span><span class="sxs-lookup"><span data-stu-id="d87a7-149">Real-time reports</span></span>
<span data-ttu-id="d87a7-150">Er zijn drie realtime rapporten in deze oplossing:</span><span class="sxs-lookup"><span data-stu-id="d87a7-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="d87a7-151">Voertuigen in bewerking</span><span class="sxs-lookup"><span data-stu-id="d87a7-151">Vehicles in operation</span></span>
2. <span data-ttu-id="d87a7-152">Voertuigen onderhoud vereisen</span><span class="sxs-lookup"><span data-stu-id="d87a7-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="d87a7-153">Voertuigen Health statistieken</span><span class="sxs-lookup"><span data-stu-id="d87a7-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="d87a7-154">U kunt kiezen tooconfigure alle Hallo drie realtime rapporten of gestopt na elke fase en doorgaan toohello volgende sectie van het Hallo batch rapporten configureren.</span><span class="sxs-lookup"><span data-stu-id="d87a7-154">You can choose tooconfigure all hello three real-time reports or stop after any stage and proceed toohello next section of configuring hello batch reports.</span></span> <span data-ttu-id="d87a7-155">We raden u alle toocreate Hallo drie rapporten toovisualize Hallo volledige insights van realtime pad Hallo Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="d87a7-155">We recommend you toocreate all hello three reports toovisualize hello full insights of hello real-time path of hello solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="d87a7-156">1. Voertuigen in bewerking</span><span class="sxs-lookup"><span data-stu-id="d87a7-156">1. Vehicles in operation</span></span>
<span data-ttu-id="d87a7-157">Dubbelklik op **pagina 1** en te hernoemen 'Voertuigen in bewerking'</span><span class="sxs-lookup"><span data-stu-id="d87a7-157">Double-click **Page 1** and rename it too“Vehicles in operation”</span></span>  
    <span data-ttu-id="d87a7-158">![Auto - verbonden voertuigen in bewerking](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="d87a7-159">Selecteer **vin** veld **velden** en visualisatie kiezen als **'Kaart'**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="d87a7-160">Kaart visualisatie wordt gemaakt, zoals weergegeven in afbeelding.</span><span class="sxs-lookup"><span data-stu-id="d87a7-160">Card visualization is created as shown in figure.</span></span>  
    ![Verbonden auto - Selecteer vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="d87a7-162">Klik op Hallo leeg gebied tooadd nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="d87a7-162">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="d87a7-163">Selecteer **stad** en **vin** van velden.</span><span class="sxs-lookup"><span data-stu-id="d87a7-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="d87a7-164">Visualisatie ook wijzigen**'Kaart'**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-164">Change visualization too**“Map”**.</span></span> <span data-ttu-id="d87a7-165">Sleep **vin** in waardengebied.</span><span class="sxs-lookup"><span data-stu-id="d87a7-165">Drag **vin** in values area.</span></span> <span data-ttu-id="d87a7-166">Sleep **stad** van velden te**legenda** gebied.</span><span class="sxs-lookup"><span data-stu-id="d87a7-166">Drag **city** from fields too**Legend** area.</span></span>   
    <span data-ttu-id="d87a7-167">![Auto - kaart visualisatie verbonden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="d87a7-168">Selecteer **indeling** rubriek van **visualisaties**, klikt u op **titel** en wijzig Hallo **tekst** te**'voertuigen in de bewerking op stad'**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-168">Select **format** section from **Visualizations**, click **Title** and change hello **Text** too**“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="d87a7-169">![Auto - verbonden voertuigen in bewerking per plaats](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="d87a7-170">Laatste visualisatie lijkt zoals weergegeven in afbeelding.</span><span class="sxs-lookup"><span data-stu-id="d87a7-170">Final visualization looks as shown in figure.</span></span>    
    ![Verbonden auto - laatste visualisatie](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="d87a7-172">Klik op Hallo leeg gebied tooadd nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="d87a7-172">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="d87a7-173">Selecteer **stad** en **vin**, visualisatie type te wijzigen**kolomdiagram geclusterde**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-173">Select **City** and **vin**, change visualization type too**Clustered Column Chart**.</span></span> <span data-ttu-id="d87a7-174">Zorg ervoor dat **stad** veld **as gebied** en **vin** in **waarde gebied**</span><span class="sxs-lookup"><span data-stu-id="d87a7-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="d87a7-175">De grafiek sorteren door **'Aantal van vin'**</span><span class="sxs-lookup"><span data-stu-id="d87a7-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="d87a7-176">![Verbonden auto - telling van vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="d87a7-177">Diagram wijzigen **titel** te**'Voertuigen in bewerking per plaats'**</span><span class="sxs-lookup"><span data-stu-id="d87a7-177">Change chart **Title** too**“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="d87a7-178">Klik op Hallo **indeling** sectie en selecteer vervolgens **gegevens kleuren**, klikt u op Hallo **'Op'** te**Alles weergeven**</span><span class="sxs-lookup"><span data-stu-id="d87a7-178">Click hello **Format** section, then select **Data Colors**,  Click hello **“On”** too**Show All**</span></span>  
    <span data-ttu-id="d87a7-179">![Verbonden auto - weergeven alle gegevens kleuren](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="d87a7-180">Hallo kleur van afzonderlijke stad wijzigen door op het Kleurenpictogram te klikken.</span><span class="sxs-lookup"><span data-stu-id="d87a7-180">Change hello color of individual city by clicking on color icon.</span></span>  
    ![Verbonden auto - kleuren wijzigen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="d87a7-182">Klik op Hallo leeg gebied tooadd nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="d87a7-182">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="d87a7-183">Selecteer **kolomdiagram geclusterde** visualisatie van visualisaties, Sleep **stad** veld **as** gebied **Model** in **Legenda** gebied en **vin** in **waarde** gebied.</span><span class="sxs-lookup"><span data-stu-id="d87a7-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="d87a7-184">![Verbonden auto - gegroepeerd kolomdiagram](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="d87a7-185">![Verbonden auto - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="d87a7-186">Alle visualisaties op deze pagina rangschikken zoals weergegeven in afbeelding.</span><span class="sxs-lookup"><span data-stu-id="d87a7-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Verbonden auto - visualisaties](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="d87a7-188">Hallo 'Voertuigen in bewerking' realtime rapport hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d87a7-188">You have successfully configured hello “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="d87a7-189">U kunt doorgaan toocreate Hallo volgende realtime rapport of hier stoppen en Hallo dashboard configureren.</span><span class="sxs-lookup"><span data-stu-id="d87a7-189">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="d87a7-190">2. Voertuigen onderhoud vereisen</span><span class="sxs-lookup"><span data-stu-id="d87a7-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="d87a7-191">Klik op ![toevoegen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd een nieuw rapport te wijzigen**'Voertuigen vereisen onderhoud'**</span><span class="sxs-lookup"><span data-stu-id="d87a7-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd a new report, rename it too**“Vehicles Requiring Maintenance”**</span></span>

![Verbonden auto - voertuigen onderhoud vereisen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="d87a7-193">Selecteer **vin** veld en visualisatie type te wijzigen**kaart**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-193">Select **vin** field and change visualization type too**Card**.</span></span>  
    <span data-ttu-id="d87a7-194">![Verbonden auto - visualisatie Vin-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="d87a7-195">We hebben een veld met de naam 'MaintenanceLabel' In hello gegevensset.</span><span class="sxs-lookup"><span data-stu-id="d87a7-195">We have a field named “MaintenanceLabel” In hello dataset.</span></span> <span data-ttu-id="d87a7-196">Dit veld kan een waarde van '0' of '1' hebben."</span><span class="sxs-lookup"><span data-stu-id="d87a7-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="d87a7-197">Het is ingesteld door hello Azure Machine Learning-model ingericht als onderdeel van de oplossing en geïntegreerd met realtime Hallo-pad.</span><span class="sxs-lookup"><span data-stu-id="d87a7-197">It is set by hello Azure Machine Learning model provisioned as part of solution and integrated with hello real-time path.</span></span> <span data-ttu-id="d87a7-198">Hallo-waarde '1' geeft dat een medium vereist onderhoud.</span><span class="sxs-lookup"><span data-stu-id="d87a7-198">hello value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="d87a7-199">tooadd een **paginaniveau** filter voor het weergeven van voertuigen gegevens, die onderhoud vereisen:</span><span class="sxs-lookup"><span data-stu-id="d87a7-199">tooadd a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="d87a7-200">Sleep Hallo **'MaintenanceLabel'** veld in **niveau paginafilters**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-200">Drag hello **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="d87a7-201">![Verbonden auto - Filters paginaniveau](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="d87a7-202">Klik op **Basic filteren** menu aan de onderkant van het niveau van MaintenanceLabel paginafilter aanwezig.</span><span class="sxs-lookup"><span data-stu-id="d87a7-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="d87a7-203">![Verbonden auto - Basic filteren](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="d87a7-204">Stel de filterwaarde te**'1'**  </span><span class="sxs-lookup"><span data-stu-id="d87a7-204">Set its filter value too**“1”**  </span></span>  
   <span data-ttu-id="d87a7-205">![Verbonden auto - filterwaarde](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="d87a7-206">Klik op Hallo leeg gebied tooadd nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="d87a7-206">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="d87a7-207">Selecteer **kolomdiagram geclusterde** van visualisaties</span><span class="sxs-lookup"><span data-stu-id="d87a7-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="d87a7-208">![Verbonden auto - visualisatie Vind-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="d87a7-209">![Verbonden auto - gegroepeerd kolomdiagram](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="d87a7-210">Sleep veld **Model** in **as** gebied **Vin** te**waarde** gebied.</span><span class="sxs-lookup"><span data-stu-id="d87a7-210">Drag field **Model** into **Axis** area, **Vin** too**Value** area.</span></span> <span data-ttu-id="d87a7-211">Sorteer visualisatie door **aantal vin**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="d87a7-212">Diagram wijzigen **titel** te**"Voertuigen onderhoud vereisen door model"**</span><span class="sxs-lookup"><span data-stu-id="d87a7-212">Change chart **Title** too**“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="d87a7-213">Sleep **vin** velden in **kleurverzadiging** aanwezig zijn bij **velden** ![velden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) sectie van **visualisatie**tabblad</span><span class="sxs-lookup"><span data-stu-id="d87a7-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="d87a7-214">![Verbonden auto - kleurverzadiging](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="d87a7-215">Wijziging **gegevens kleuren** in visualisaties van **indeling** sectie</span><span class="sxs-lookup"><span data-stu-id="d87a7-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="d87a7-216">Minimale kleur te wijzigen: **F2C812**</span><span class="sxs-lookup"><span data-stu-id="d87a7-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="d87a7-217">Maximale kleur te wijzigen: **FF6300**</span><span class="sxs-lookup"><span data-stu-id="d87a7-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="d87a7-218">![Auto - wijzigingen in de kleuren verbonden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="d87a7-219">![Verbonden auto - nieuwe visualisatie kleuren](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="d87a7-220">Klik op Hallo leeg gebied tooadd nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="d87a7-220">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="d87a7-221">Selecteer **gegroepeerd kolomdiagram** visualisaties, Sleep **vin** veld in **waarde** gebied slepen **stad** veld in **As** gebied.</span><span class="sxs-lookup"><span data-stu-id="d87a7-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="d87a7-222">De grafiek sorteren door **'Aantal van vin'**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="d87a7-223">Diagram wijzigen **titel** te**'Voertuigen vereisen onderhoud per plaats'** </span><span class="sxs-lookup"><span data-stu-id="d87a7-223">Change chart **Title** too**“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="d87a7-224">![Verbonden auto - voertuigen onderhoud per plaats vereisen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="d87a7-225">Klik op Hallo leeg gebied tooadd nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="d87a7-225">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="d87a7-226">Selecteer **met meerdere rijen kaart** visualisatie van visualisaties, Sleep **Model** en **vin** in Hallo **velden** gebied.</span><span class="sxs-lookup"><span data-stu-id="d87a7-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into hello **Fields** area.</span></span>  
<span data-ttu-id="d87a7-227">![Verbonden auto - meerdere rij-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="d87a7-228">Alle Hallo visualisatie herschikken, Hallo laatste rapport ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="d87a7-228">Rearranging all of hello visualization, hello final report looks as follows:</span></span>  
![Verbonden auto - meerdere rij-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="d87a7-230">Hallo 'Voertuigen vereisen onderhoud' realtime rapport hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d87a7-230">You have successfully configured hello “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="d87a7-231">U kunt doorgaan toocreate Hallo volgende realtime rapport of hier stoppen en Hallo dashboard configureren.</span><span class="sxs-lookup"><span data-stu-id="d87a7-231">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="d87a7-232">3. Voertuigen Health statistieken</span><span class="sxs-lookup"><span data-stu-id="d87a7-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="d87a7-233">Klik op ![toevoegen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd nieuwe rapporteren, te wijzigen**'Voertuigen Health statistieken'**</span><span class="sxs-lookup"><span data-stu-id="d87a7-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd new report, rename it too**“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="d87a7-234">Selecteer **meter** visualisatie van visualisaties, sleept u Hallo **snelheid** veld in **waarde, minimumwaarde, maximumwaarde** gebieden.</span><span class="sxs-lookup"><span data-stu-id="d87a7-234">Select **Gauge** visualization from visualizations, then drag hello **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="d87a7-235">![Verbonden auto - meerdere rij-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="d87a7-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="d87a7-236">Hallo standaard aggregatie van wijzigen **snelheid** in **waarde gebied** te**gemiddelde**</span><span class="sxs-lookup"><span data-stu-id="d87a7-236">Change hello default aggregation of **speed** in **Value area** too**Average**</span></span> 

<span data-ttu-id="d87a7-237">Hallo standaard aggregatie van wijzigen **snelheid** in **Minimum gebied** te**Minimum**</span><span class="sxs-lookup"><span data-stu-id="d87a7-237">Change hello default aggregation of **speed** in **Minimum area** too**Minimum**</span></span>

<span data-ttu-id="d87a7-238">Hallo standaard aggregatie van wijzigen **snelheid** in **Maximum gebied** te**maximale**</span><span class="sxs-lookup"><span data-stu-id="d87a7-238">Change hello default aggregation of **speed** in **Maximum area** too**Maximum**</span></span>

![Verbonden auto - meerdere rij-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="d87a7-240">Wijzig de naam van Hallo **meter titel** te**'Gemiddelde snelheid'**</span><span class="sxs-lookup"><span data-stu-id="d87a7-240">Rename hello **Gauge Title** too**“Average speed”**</span></span> 

![Verbonden auto - meter](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="d87a7-242">Klik op Hallo leeg gebied tooadd nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="d87a7-242">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="d87a7-243">Op dezelfde manier toevoegen een **meter** voor **engine olie gemiddelde**, **gemiddelde brandstof**, en **gemiddelde temperatuur aangeven engine**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="d87a7-244">Hallo standaard aggregatie van velden in elke meter conform bovenstaande stappen in wijzigen **'Gemiddelde snelheid'** meter.</span><span class="sxs-lookup"><span data-stu-id="d87a7-244">Change hello default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Verbonden auto - meters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="d87a7-246">Klik op Hallo leeg gebied tooadd nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="d87a7-246">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="d87a7-247">Selecteer **lijndiagram en gegroepeerd kolomdiagram** van visualisaties, sleept u **stad** veld in **gedeeld as**, sleept u **snelheid**, **velden tirepressure en engineoil** in **kolomwaarden** gebied te wijzigen van hun samenvoegingstype**gemiddelde**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type too**Average**.</span></span> 

<span data-ttu-id="d87a7-248">Sleep Hallo **engineTemperature** veld in **regelwaarden** gebied Hallo samenvoegingstype ook wijzigen**gemiddelde**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-248">Drag hello **engineTemperature** field into **Line Values** area, change hello  aggregation type too**Average**.</span></span> 

![Verbonden auto - visualisaties velden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="d87a7-250">Diagram van wijzigen Hallo **titel** te**'Gemiddelde snelheid, band druk, engine olie en temperatuur motor'**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-250">Change hello chart **Title** too**“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Verbonden auto - visualisaties velden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="d87a7-252">Klik op Hallo leeg gebied tooadd nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="d87a7-252">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="d87a7-253">Selecteer **Treemap** visualisatie van visualisaties, sleept u Hallo **Model** veld in Hallo **groep** gebied en sleep Hallo veld  **MaintenanceProbability** in Hallo **waarden** gebied.</span><span class="sxs-lookup"><span data-stu-id="d87a7-253">Select **Treemap** visualization from visualizations, drag hello **Model** field into hello **Group** area, and drag hello field **MaintenanceProbability** into hello **Values** area.</span></span>

<span data-ttu-id="d87a7-254">Diagram van wijzigen Hallo **titel** te**'Vehicle modellen vereisen onderhoud'**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-254">Change hello chart **Title** too**“Vehicle models requiring maintenance”**.</span></span>

![Verbonden auto - grafiektitel wijzigen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="d87a7-256">Klik op Hallo leeg gebied tooadd nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="d87a7-256">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="d87a7-257">Selecteer **100% gestapeld staafdiagram** visualisatie, sleep Hallo **stad** veld in Hallo **as** gebied en sleep Hallo **MaintenanceProbability**, **RecallProbability** velden in Hallo **waarde** gebied.</span><span class="sxs-lookup"><span data-stu-id="d87a7-257">Select **100% Stacked Bar Chart** from visualization, drag hello **city** field into hello **Axis** area, and drag hello **MaintenanceProbability**, **RecallProbability** fields into hello **Value** area.</span></span>

![Verbonden auto - toevoegen nieuwe visualisatie](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="d87a7-259">Klik op **indeling**, selecteer **gegevens kleuren**, en set Hallo **MaintenanceProbability** toohello kleurwaarde **'F2C80F'**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-259">Click **Format**, select **Data Colors**, and set hello **MaintenanceProbability** color toohello value **“F2C80F”**.</span></span>

<span data-ttu-id="d87a7-260">Wijziging Hallo **titel** Hallo grafiek te**'Waarschijnlijkheid van Vehicle onderhoud & intrekken per plaats'**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-260">Change hello **Title** of hello chart too**“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Verbonden auto - toevoegen nieuwe visualisatie](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="d87a7-262">Klik op Hallo leeg gebied tooadd nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="d87a7-262">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="d87a7-263">Selecteer **vlakdiagram** visualisatie van visualisaties Sleep Hallo **Model** veld in Hallo **as** gebied en sleep Hallo **engineOil, tirepressure, snelheid en MaintenanceProbability** velden in Hallo **waarden** gebied.</span><span class="sxs-lookup"><span data-stu-id="d87a7-263">Select **Area Chart** from visualization from visualizations, drag hello **Model** field into hello **Axis** area, and drag hello **engineOil, tirepressure, speed and MaintenanceProbability** fields into hello **Values** area.</span></span> <span data-ttu-id="d87a7-264">Hun samenvoegingstype ook wijzigen**'Gemiddeld'**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-264">Change their aggregation type too**“Average”**.</span></span> 

![Verbonden auto - aggregatie wijzigingstype](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="d87a7-266">Titel van de grafiek Hallo Hallo ook wijzigen**"Gemiddelde engine olie, druk, snelheid en het onderhoud kans genoeg door model"**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-266">Change hello title of hello chart too**“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Verbonden auto - grafiektitel wijzigen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="d87a7-268">Klik op Hallo leeg gebied tooadd nieuwe visualisatie:</span><span class="sxs-lookup"><span data-stu-id="d87a7-268">Click hello blank area tooadd new visualization:</span></span>

1. <span data-ttu-id="d87a7-269">Selecteer **grafiek spreidingsdiagrammen** visualisatie van visualisaties.</span><span class="sxs-lookup"><span data-stu-id="d87a7-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="d87a7-270">Sleep Hallo **Model** veld in Hallo **Details** en **legenda** gebied.</span><span class="sxs-lookup"><span data-stu-id="d87a7-270">Drag hello **Model** field into hello **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="d87a7-271">Sleep Hallo **brandstof** veld in Hallo **x-as** gebied Hallo aggregatie ook wijzigen**gemiddelde**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-271">Drag hello **fuel** field into hello **X-Axis** area, change hello aggregation too**Average**.</span></span>
4. <span data-ttu-id="d87a7-272">Sleep **engineTemparature** in **y-as gebied**, Hallo aggregatie ook wijzigen**gemiddelde**</span><span class="sxs-lookup"><span data-stu-id="d87a7-272">Drag **engineTemparature** into **Y-Axis area**, change hello aggregation too**Average**</span></span>
5. <span data-ttu-id="d87a7-273">Sleep Hallo **vin** veld in Hallo **grootte** gebied.</span><span class="sxs-lookup"><span data-stu-id="d87a7-273">Drag hello **vin** field into hello **Size** area.</span></span>

![Verbonden auto - toevoegen nieuwe visualisatie](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="d87a7-275">Diagram van wijzigen Hallo **titel** te**"Gemiddelden van brandstof, Engine temperatuur door Model"**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-275">Change hello chart **Title** too**“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Verbonden auto - grafiektitel wijzigen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="d87a7-277">Hallo laatste rapport eruit zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d87a7-277">hello final report will look like as shown below.</span></span>

![Auto-Final rapport verbonden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a><span data-ttu-id="d87a7-279">Pincode visualisaties van Hallo rapporten toohello realtime dashboard</span><span class="sxs-lookup"><span data-stu-id="d87a7-279">Pin visualizations from hello reports toohello real-time dashboard</span></span>
<span data-ttu-id="d87a7-280">Een lege dashboard door te klikken op Hallo plus pictogram volgende tooDashboards maken.</span><span class="sxs-lookup"><span data-stu-id="d87a7-280">Create a blank dashboard by clicking on hello plus icon next tooDashboards.</span></span> <span data-ttu-id="d87a7-281">U kunt andere naam 'Vehicle telemetrie Analytics Dashboard'</span><span class="sxs-lookup"><span data-stu-id="d87a7-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Verbonden auto-Dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="d87a7-283">Pincode Hallo visualisatie van Hallo hierboven rapporten toohello dashboard.</span><span class="sxs-lookup"><span data-stu-id="d87a7-283">Pin hello visualization from hello above reports toohello dashboard.</span></span> 

![Verbonden auto-Dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="d87a7-285">Hallo-dashboard ziet er als volgt wanneer alle Hallo drie rapporten worden gemaakt en Hallo overeenkomt visualisaties vastgemaakt toohello dashboard zijn.</span><span class="sxs-lookup"><span data-stu-id="d87a7-285">hello dashboard should look as follows when all hello three reports are created and hello corresponding visualizations are pinned toohello dashboard.</span></span> <span data-ttu-id="d87a7-286">Als u niet alle Hallo rapporten hebt gemaakt, kan uw dashboard anders zijn.</span><span class="sxs-lookup"><span data-stu-id="d87a7-286">If you have not created all hello reports, your dashboard could look different.</span></span> 

![Verbonden auto-Dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="d87a7-288">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="d87a7-288">Congratulations!</span></span> <span data-ttu-id="d87a7-289">Hallo realtime dashboard hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d87a7-289">You have successfully created hello real-time dashboard.</span></span> <span data-ttu-id="d87a7-290">Als u tooexecute CarEventGenerator.exe en RealtimeDashboardApp.exe doorgaat, ziet u live updates op Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="d87a7-290">As you continue tooexecute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on hello dashboard.</span></span> <span data-ttu-id="d87a7-291">Het duurt ongeveer 10 too15 minuten toocomplete Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="d87a7-291">It should take about 10 too15 minutes toocomplete hello following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="d87a7-292">Power BI batch-verwerking dashboard instellen</span><span class="sxs-lookup"><span data-stu-id="d87a7-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="d87a7-293">Het duurt ongeveer twee uur (van Hallo voltooiing van implementatie Hallo) voor Hallo end tooend batch verwerken van de uitvoering van de pipeline-toofinish en een jaar aan gegenereerde gegevens verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d87a7-293">It takes about two hours (from hello successful completion of hello deployment) for hello end tooend batch processing pipeline toofinish execution and process a year worth of generated data.</span></span> <span data-ttu-id="d87a7-294">Wacht dus Hallo toofinish voordat u doorgaat met de volgende stappen Hallo verwerken.</span><span class="sxs-lookup"><span data-stu-id="d87a7-294">So wait for hello processing toofinish before proceeding with hello next steps.</span></span> 
> 
> 

<span data-ttu-id="d87a7-295">**Hallo Power BI designer-bestand downloaden**</span><span class="sxs-lookup"><span data-stu-id="d87a7-295">**Download hello Power BI designer file**</span></span>

* <span data-ttu-id="d87a7-296">Een vooraf geconfigureerde Power BI designer-bestand is opgenomen als onderdeel van Hallo implementatie handmatig bewerking instructies</span><span class="sxs-lookup"><span data-stu-id="d87a7-296">A pre-configured Power BI designer file is included as part of hello deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="d87a7-297">Zoek naar 2.</span><span class="sxs-lookup"><span data-stu-id="d87a7-297">Look for 2.</span></span> <span data-ttu-id="d87a7-298">Het installatieprogramma Power BI batch verwerking dashboard kunt u Hallo Power BI-sjabloon voor batchverwerking dashboard hier aangeroepen downloaden **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-298">Setup PowerBI batch processing dashboard You can download hello PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="d87a7-299">Lokaal opslaan</span><span class="sxs-lookup"><span data-stu-id="d87a7-299">Save locally</span></span>

<span data-ttu-id="d87a7-300">**Power BI-rapporten configureren**</span><span class="sxs-lookup"><span data-stu-id="d87a7-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="d87a7-301">Open Hallo designer bestand '**ConnectedCarsPbiReport.pbix**' met behulp van Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="d87a7-301">Open hello designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="d87a7-302">Als u al hebt, Installeer geen Power BI Desktop van Hallo [Power BI Desktop installeren](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="d87a7-302">If you do not already have, install hello Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="d87a7-303">Klik op Hallo **query's bewerken**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-303">Click hello **Edit Queries**.</span></span>

![Power BI query bewerken](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="d87a7-305">Dubbelklik op Hallo **bron**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-305">Double-click hello **Source**.</span></span>

![Set Power BI-bron](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="d87a7-307">Server-verbindingsreeks bijwerken met hello Azure SQL-server die als onderdeel van Hallo-implementatie hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="d87a7-307">Update Server connection string with hello Azure SQL server that got provisioned as part of hello deployment.</span></span>  <span data-ttu-id="d87a7-308">Zoeken in Hallo handmatige bewerking instructies onder</span><span class="sxs-lookup"><span data-stu-id="d87a7-308">Look in hello Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="d87a7-309">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d87a7-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="d87a7-310">Server: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="d87a7-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="d87a7-311">Database: connectedcar</span><span class="sxs-lookup"><span data-stu-id="d87a7-311">Database: connectedcar</span></span>
    * <span data-ttu-id="d87a7-312">Gebruikersnaam: gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="d87a7-312">Username: username</span></span>
    * <span data-ttu-id="d87a7-313">Wachtwoord: U kunt het wachtwoord van uw SQL-server beheren vanuit Azure-portal</span><span class="sxs-lookup"><span data-stu-id="d87a7-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="d87a7-314">Laat **Database** als *connectedcar*.</span><span class="sxs-lookup"><span data-stu-id="d87a7-314">Leave **Database** as *connectedcar*.</span></span>

![Stel de database in Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="d87a7-316">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-316">Click **OK**.</span></span>
* <span data-ttu-id="d87a7-317">U ziet **Windows-referentie** tabblad standaard geselecteerd, ook wijzigen**Database referenties** door te klikken op **Database** tabblad rechts.</span><span class="sxs-lookup"><span data-stu-id="d87a7-317">You will see **Windows credential** tab selected by default, change it too**Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="d87a7-318">Hallo bieden **gebruikersnaam** en **wachtwoord** van uw Azure SQL Database die is opgegeven tijdens de installatie van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="d87a7-318">Provide hello **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![Geef databasereferenties op](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="d87a7-320">Klik op **verbinding maken**</span><span class="sxs-lookup"><span data-stu-id="d87a7-320">Click **Connect**</span></span>
* <span data-ttu-id="d87a7-321">Hallo bovenstaande stappen herhalen voor elk Hallo drie resterende query's aanwezig zijn bij het rechter deelvenster en werk vervolgens details verbinding Hallo van gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="d87a7-321">Repeat hello above steps for each of hello three remaining queries present at right pane, and then update hello data source connection details.</span></span>
* <span data-ttu-id="d87a7-322">Klik op **sluiten en te laden**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-322">Click **Close and Load**.</span></span> <span data-ttu-id="d87a7-323">Power BI Desktop-bestand gegevenssets zijn verbonden tooSQL Azure databasetabellen.</span><span class="sxs-lookup"><span data-stu-id="d87a7-323">Power BI Desktop file datasets are connected tooSQL Azure Database tables.</span></span>
* <span data-ttu-id="d87a7-324">**Sluit** Power BI Desktop-bestand.</span><span class="sxs-lookup"><span data-stu-id="d87a7-324">**Close** Power BI Desktop file.</span></span>

![Sluit Power BI desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="d87a7-326">Klik op **opslaan** knop toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="d87a7-326">Click **Save** button toosave hello changes.</span></span> 

<span data-ttu-id="d87a7-327">U hebt nu alle Hallo rapporten toohello batch verwerken van het pad in Hallo oplossing overeenkomt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d87a7-327">You have now configured all hello reports corresponding toohello batch processing path in hello solution.</span></span> 

## <a name="upload-toopowerbicom"></a><span data-ttu-id="d87a7-328">Te uploaden*powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="d87a7-328">Upload too*powerbi.com*</span></span>
1. <span data-ttu-id="d87a7-329">Navigeer toohello Power BI-webportal op http://powerbi.com en meld u aan.</span><span class="sxs-lookup"><span data-stu-id="d87a7-329">Navigate toohello Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="d87a7-330">Klik op **gegevens ophalen**</span><span class="sxs-lookup"><span data-stu-id="d87a7-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="d87a7-331">Hallo Power BI Desktop-bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="d87a7-331">Upload hello Power BI Desktop File.</span></span>  
4. <span data-ttu-id="d87a7-332">tooupload, klikt u op **gegevens ophalen -> bestanden ophalen -> lokaal bestand**</span><span class="sxs-lookup"><span data-stu-id="d87a7-332">tooupload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="d87a7-333">Navigeer toohello **'**ConnectedCarsPbiReport.pbix**'**</span><span class="sxs-lookup"><span data-stu-id="d87a7-333">Navigate toohello **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="d87a7-334">Zodra het Hallo-bestand is geüpload, zult u waarin navigeren back tooyour Power BI-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="d87a7-334">Once hello file is uploaded, you will be navigated back tooyour Power BI work space.</span></span>  

<span data-ttu-id="d87a7-335">Een gegevensset, rapport en een lege dashboard wordt voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d87a7-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="d87a7-336">Pincode grafieken tooa nieuwe dashboard aangeroepen **Dashboard met analytische telemetrie Vehicle** in **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="d87a7-336">Pin charts tooa new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="d87a7-337">Klik op de lege dashboard Hallo die eerder is gemaakt en navigeer vervolgens toohello **rapporten** sectie Klik Hallo geüpload nieuw rapport.</span><span class="sxs-lookup"><span data-stu-id="d87a7-337">Click hello blank dashboard created above and then navigate toohello **Reports** section click hello newly uploaded report.</span></span>  

![Vehicle telemetrie Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="d87a7-339">**Opmerking Hallo rapport heeft zes pagina's:**</span><span class="sxs-lookup"><span data-stu-id="d87a7-339">**Note hello report has six pages:**</span></span>  
<span data-ttu-id="d87a7-340">Pagina 1: Vehicle dichtheid</span><span class="sxs-lookup"><span data-stu-id="d87a7-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="d87a7-341">Pagina 2: Realtime vehicle health</span><span class="sxs-lookup"><span data-stu-id="d87a7-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="d87a7-342">Pagina 3: Aangestuurd agressief voertuigen</span><span class="sxs-lookup"><span data-stu-id="d87a7-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="d87a7-343">Pagina 4: Teruggehaald voertuigen</span><span class="sxs-lookup"><span data-stu-id="d87a7-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="d87a7-344">Pagina 5: Brandstof efficiënt aangedreven voertuigen</span><span class="sxs-lookup"><span data-stu-id="d87a7-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="d87a7-345">Pagina 6: Contoso-Logo</span><span class="sxs-lookup"><span data-stu-id="d87a7-345">Page 6: Contoso Logo</span></span>  

![Verbonden auto's Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="d87a7-347">**Vanaf 3 pagina**, vastmaken Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="d87a7-347">**From Page 3**, pin hello following:</span></span>  

1. <span data-ttu-id="d87a7-348">Telling van VIN</span><span class="sxs-lookup"><span data-stu-id="d87a7-348">Count of VIN</span></span>  
   ![Verbonden auto's Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="d87a7-350">Agressief voertuigen aangedreven door model – waterval grafiek</span><span class="sxs-lookup"><span data-stu-id="d87a7-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![Vehicle telemetrie - pincode grafieken 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="d87a7-352">**Van pagina 5**, vastmaken Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="d87a7-352">**From Page 5**, pin hello following:</span></span> 

1. <span data-ttu-id="d87a7-353">Telling van vin</span><span class="sxs-lookup"><span data-stu-id="d87a7-353">Count of vin</span></span>    
   ![Vehicle telemetrie - grafieken van de pincode 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="d87a7-355">Efficiënte voertuigen brandstof door model: gegroepeerd kolomdiagram</span><span class="sxs-lookup"><span data-stu-id="d87a7-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![Vehicle telemetrie - pincode grafieken 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="d87a7-357">**Van pagina 4**, vastmaken Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="d87a7-357">**From Page 4**, pin hello following:</span></span>  

1. <span data-ttu-id="d87a7-358">Telling van vin</span><span class="sxs-lookup"><span data-stu-id="d87a7-358">Count of vin</span></span>  
   ![Vehicle telemetrie - pincode grafieken 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="d87a7-360">Ingetrokken voertuigen per plaats, model: Treemap</span><span class="sxs-lookup"><span data-stu-id="d87a7-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![Vehicle telemetrie - pincode grafieken 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="d87a7-362">**Pagina 6**, vastmaken Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="d87a7-362">**From Page 6**, pin hello following:</span></span>  

1. <span data-ttu-id="d87a7-363">Contoso motoren-logo</span><span class="sxs-lookup"><span data-stu-id="d87a7-363">Contoso Motors logo</span></span>  
   ![Vehicle telemetrie - pincode grafieken 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="d87a7-365">**Hallo dashboard ordenen**</span><span class="sxs-lookup"><span data-stu-id="d87a7-365">**Organize hello dashboard**</span></span>  

1. <span data-ttu-id="d87a7-366">Navigeer toohello dashboard</span><span class="sxs-lookup"><span data-stu-id="d87a7-366">Navigate toohello dashboard</span></span>
2. <span data-ttu-id="d87a7-367">Beweeg de muisaanwijzer over elke grafiek en wijzig de naam op basis van het Hallo naming opgegeven in Hallo voltooid dashboard in onderstaande afbeelding.</span><span class="sxs-lookup"><span data-stu-id="d87a7-367">Hover over each chart and rename it based on hello naming provided in hello complete dashboard image below.</span></span> <span data-ttu-id="d87a7-368">Hallo grafieken rond toolook zoals Hallo dashboard hieronder ook verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="d87a7-368">Also move hello charts around toolook like hello dashboard below.</span></span>  
   ![Vehicle telemetrie - Dashboard 2 ordenen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Vehicle telemetrie Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="d87a7-371">Als u alle Hallo rapporten, zoals vermeld in dit document hebt gemaakt, moet hello laatste voltooide dashboard eruitzien als Hallo volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="d87a7-371">If you have created all hello reports as mentioned in this document, hello final completed dashboard should look like hello following figure.</span></span> 

![Vehicle telemetrie - Dashboard 2 ordenen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="d87a7-373">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="d87a7-373">Congratulations!</span></span> <span data-ttu-id="d87a7-374">U Hallo rapporten hebt gemaakt en Hallo dashboard toogain realtime, voorspellende en gewoonten batch insights op de drager gezondheid en groot.</span><span class="sxs-lookup"><span data-stu-id="d87a7-374">You have successfully created hello reports and hello dashboard toogain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  

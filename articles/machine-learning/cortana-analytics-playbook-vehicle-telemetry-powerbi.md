---
title: Power BI-Dashboard vehicle status en die zorg draagt gewoonten - Azure | Microsoft Docs
description: De mogelijkheden van Cortana Intelligence gebruiken om inzicht in real-time en voorspeld op vehicle status en verkeer te krijgen gewoonten.
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
ms.openlocfilehash: f880aceb1657ffdfe909b73f175b9673d9ab02cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="83208-103">Vehicle telemetrie analytics-oplossing sjabloon Power BI-Dashboard installatie-instructies</span><span class="sxs-lookup"><span data-stu-id="83208-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="83208-104">Dit **menu** koppelingen naar de hoofdstukken in deze playbook.</span><span class="sxs-lookup"><span data-stu-id="83208-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="83208-105">De drager telemetrie Analytics-oplossing gepresenteerd hoe auto dealerbedrijven, auto fabrikanten en ondernemingen van de mogelijkheden van Cortana Intelligence gebruikmaken kunnen krijgen realtime en gewoonten voorspellende insights op de drager gezondheid en verkeer naar station verbeteringen aangebracht in het gebied van de klant ervaren R & D- en marketingcampagnes.</span><span class="sxs-lookup"><span data-stu-id="83208-105">The Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits to drive improvements in the area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="83208-106">Dit document bevat stapsgewijze instructies over hoe u de Power BI-rapporten en het dashboard configureren kunt zodra de oplossing is geïmplementeerd in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="83208-106">This document contains step by step instructions on how you can configure the Power BI reports and dashboard once the solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="83208-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="83208-107">Prerequisites</span></span>
1. <span data-ttu-id="83208-108">Implementeer de [telemetrie Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) oplossing</span><span class="sxs-lookup"><span data-stu-id="83208-108">Deploy the [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="83208-109">Installeren van Microsoft Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="83208-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="83208-110">Een [Azure-abonnement](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83208-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="83208-111">Als u geen Azure-abonnement hebt, aan de slag met de gratis Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="83208-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="83208-112">Microsoft Power BI-account</span><span class="sxs-lookup"><span data-stu-id="83208-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="83208-113">Cortana Intelligence Suite-onderdelen</span><span class="sxs-lookup"><span data-stu-id="83208-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="83208-114">Als onderdeel van de sjabloon Vehicle telemetrie Analytics-oplossing, worden de volgende Cortana Intelligence-services geïmplementeerd in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="83208-114">As part of the Vehicle Telemetry Analytics solution template, the following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="83208-115">**Event Hub** voor het opnemen van miljoenen vehicle telemetrische gebeurtenissen in Azure.</span><span class="sxs-lookup"><span data-stu-id="83208-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="83208-116">**Stream Analytics** voor realtime-inzichten op vehicle gezondheid en dat de gegevens zich blijft voordoen in langdurige opslag voor uitgebreidere batch analyses.</span><span class="sxs-lookup"><span data-stu-id="83208-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="83208-117">**Machine Learning** voor afwijkingsdetectie in realtime en batchverwerking om voorspellende inzicht te krijgen.</span><span class="sxs-lookup"><span data-stu-id="83208-117">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="83208-118">**HDInsight** wordt gebruikt voor het transformeren van gegevens op grote schaal</span><span class="sxs-lookup"><span data-stu-id="83208-118">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="83208-119">**Data Factory** orchestration, planning, bronbeheer en controle van de pijplijn batchverwerking verwerkt.</span><span class="sxs-lookup"><span data-stu-id="83208-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>

<span data-ttu-id="83208-120">**Power BI** biedt deze oplossing een uitgebreide dashboard voor realtime-gegevens en visualisaties predictive analytics.</span><span class="sxs-lookup"><span data-stu-id="83208-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="83208-121">De oplossing maakt gebruik van twee verschillende gegevensbronnen: **gesimuleerde vehicle signalen en diagnostische gegevensset** en **vehicle catalogus**.</span><span class="sxs-lookup"><span data-stu-id="83208-121">The solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="83208-122">Er is een vehicle telematica simulator opgenomen als onderdeel van deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="83208-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="83208-123">Deze diagnostische gegevens verzendt en signalen overeenkomt met de status van de drager als patroon groot op een bepaald tijdstip.</span><span class="sxs-lookup"><span data-stu-id="83208-123">It emits diagnostic information and signals corresponding to the state of the vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="83208-124">De catalogus drager is een verwijzing gegevensset met Chassisnummer model toewijzen aan</span><span class="sxs-lookup"><span data-stu-id="83208-124">The Vehicle Catalog is a reference dataset containing VIN to model mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="83208-125">Voorbereiding van Power BI-Dashboard</span><span class="sxs-lookup"><span data-stu-id="83208-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="83208-126">Realtime Power BI-Dashboard instellen</span><span class="sxs-lookup"><span data-stu-id="83208-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="83208-127">**Start de dashboardtoepassing realtime** zodra de implementatie is voltooid, moet u Volg de instructies van de bewerking handmatig</span><span class="sxs-lookup"><span data-stu-id="83208-127">**Start the real-time dashboard application** Once the deployment is completed, you should follow the Manual Operation Instructions</span></span>

* <span data-ttu-id="83208-128">Realtime dashboardtoepassing RealtimeDashboardApp.zip downloaden en uitpakken van het.</span><span class="sxs-lookup"><span data-stu-id="83208-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="83208-129">Open de app-configuratiebestand RealtimeDashboardApp.exe.config, vervangen appSettings voor Eventhub, Blob Storage en ML service-verbindingen met de waarden in de instructies van de bewerking handmatig en sla de wijzigingen in de uitgepakte map.</span><span class="sxs-lookup"><span data-stu-id="83208-129">In the unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with the values in the Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="83208-130">Toepassing RealtimeDashboardApp.exe uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="83208-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="83208-131">Een aanmeldingsvenster wordt pop-, geldige referenties van uw Power BI en klik op de **accepteren** knop.</span><span class="sxs-lookup"><span data-stu-id="83208-131">A login window will pop up, provide your valid PowerBI credentials and click the **Accept** button.</span></span> <span data-ttu-id="83208-132">De app wordt vervolgens gestart om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="83208-132">Then the app will start to run.</span></span>

   ![Aanmelden bij Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Machtigingen voor Power BI-Dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="83208-135">Meld u aan bij Power BI-website en realtime dashboard maken.</span><span class="sxs-lookup"><span data-stu-id="83208-135">Login to PowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="83208-136">Nu bent u klaar voor het configureren van de Power BI-dashboard met uitgebreide visualisaties krijgen realtime en gewoonten voorspellende insights op de drager gezondheid en groot.</span><span class="sxs-lookup"><span data-stu-id="83208-136">Now, you are ready to configure the Power BI dashboard with rich visualizations to gain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="83208-137">Het duurt ongeveer 45 minuten tot een uur alle rapporten maken en configureren van het dashboard.</span><span class="sxs-lookup"><span data-stu-id="83208-137">It takes about 45 minutes to an hour to create all the reports and configure the dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="83208-138">Power BI-rapporten configureren</span><span class="sxs-lookup"><span data-stu-id="83208-138">Configure Power BI reports</span></span>
<span data-ttu-id="83208-139">De realtime-rapporten en het dashboard rekening houden met ongeveer 30 tot 45 minuten om te voltooien.</span><span class="sxs-lookup"><span data-stu-id="83208-139">The real-time reports and the dashboard take about 30-45 minutes to complete.</span></span> <span data-ttu-id="83208-140">Blader naar [http://powerbi.com](http://powerbi.com) en meld u aan.</span><span class="sxs-lookup"><span data-stu-id="83208-140">Browse to [http://powerbi.com](http://powerbi.com) and login.</span></span>

![Aanmelden bij Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="83208-142">Een nieuwe gegevensset wordt gegenereerd in Power BI.</span><span class="sxs-lookup"><span data-stu-id="83208-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="83208-143">Klik op de **ConnectedCarsRealtime** gegevensset.</span><span class="sxs-lookup"><span data-stu-id="83208-143">Click the **ConnectedCarsRealtime** dataset.</span></span>

![Geselecteerd verbonden realtime gegevensset voor auto 's](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="83208-145">Sla de leeg rapport via **Ctrl + s**.</span><span class="sxs-lookup"><span data-stu-id="83208-145">Save the blank report using **Ctrl + s**.</span></span>

![Leeg rapport opslaan](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="83208-147">Geef de naam van rapport *Vehicle telemetrie Analytics realtime - rapporten*.</span><span class="sxs-lookup"><span data-stu-id="83208-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![Geef de naam van rapport](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="83208-149">Realtime-rapporten</span><span class="sxs-lookup"><span data-stu-id="83208-149">Real-time reports</span></span>
<span data-ttu-id="83208-150">Er zijn drie realtime rapporten in deze oplossing:</span><span class="sxs-lookup"><span data-stu-id="83208-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="83208-151">Voertuigen in bewerking</span><span class="sxs-lookup"><span data-stu-id="83208-151">Vehicles in operation</span></span>
2. <span data-ttu-id="83208-152">Voertuigen onderhoud vereisen</span><span class="sxs-lookup"><span data-stu-id="83208-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="83208-153">Voertuigen Health statistieken</span><span class="sxs-lookup"><span data-stu-id="83208-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="83208-154">U kunt de drie realtime rapporten configureren of stoppen nadat elke fase en gaat u verder met de volgende sectie van de configuratie van de batch-rapporten.</span><span class="sxs-lookup"><span data-stu-id="83208-154">You can choose to configure all the three real-time reports or stop after any stage and proceed to the next section of configuring the batch reports.</span></span> <span data-ttu-id="83208-155">We raden u aan te maken van de drie rapporten voor het visualiseren van de volledige inzichten van het real-time pad van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="83208-155">We recommend you to create all the three reports to visualize the full insights of the real-time path of the solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="83208-156">1. Voertuigen in bewerking</span><span class="sxs-lookup"><span data-stu-id="83208-156">1. Vehicles in operation</span></span>
<span data-ttu-id="83208-157">Dubbelklik op **pagina 1** en wijzig de naam 'Voertuigen in bewerking'</span><span class="sxs-lookup"><span data-stu-id="83208-157">Double-click **Page 1** and rename it to “Vehicles in operation”</span></span>  
    <span data-ttu-id="83208-158">![Auto - verbonden voertuigen in bewerking](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="83208-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="83208-159">Selecteer **vin** veld **velden** en visualisatie kiezen als **'Kaart'**.</span><span class="sxs-lookup"><span data-stu-id="83208-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="83208-160">Kaart visualisatie wordt gemaakt, zoals weergegeven in afbeelding.</span><span class="sxs-lookup"><span data-stu-id="83208-160">Card visualization is created as shown in figure.</span></span>  
    ![Verbonden auto - Selecteer vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="83208-162">Klik op het lege gebied om toe te voegen nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="83208-162">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="83208-163">Selecteer **stad** en **vin** van velden.</span><span class="sxs-lookup"><span data-stu-id="83208-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="83208-164">Visualisatie te wijzigen **'Kaart'**.</span><span class="sxs-lookup"><span data-stu-id="83208-164">Change visualization to **“Map”**.</span></span> <span data-ttu-id="83208-165">Sleep **vin** in waardengebied.</span><span class="sxs-lookup"><span data-stu-id="83208-165">Drag **vin** in values area.</span></span> <span data-ttu-id="83208-166">Sleep **stad** van velden in om **legenda** gebied.</span><span class="sxs-lookup"><span data-stu-id="83208-166">Drag **city** from fields to **Legend** area.</span></span>   
    <span data-ttu-id="83208-167">![Auto - kaart visualisatie verbonden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="83208-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="83208-168">Selecteer **indeling** rubriek van **visualisaties**, klikt u op **titel** en wijzig de **tekst** naar **'voertuigen in bewerking per plaats'**.</span><span class="sxs-lookup"><span data-stu-id="83208-168">Select **format** section from **Visualizations**, click **Title** and change the **Text** to **“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="83208-169">![Auto - verbonden voertuigen in bewerking per plaats](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="83208-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="83208-170">Laatste visualisatie lijkt zoals weergegeven in afbeelding.</span><span class="sxs-lookup"><span data-stu-id="83208-170">Final visualization looks as shown in figure.</span></span>    
    ![Verbonden auto - laatste visualisatie](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="83208-172">Klik op het lege gebied om toe te voegen nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="83208-172">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="83208-173">Selecteer **stad** en **vin**, wijzigt in visualisatie **kolomdiagram geclusterde**.</span><span class="sxs-lookup"><span data-stu-id="83208-173">Select **City** and **vin**, change visualization type to **Clustered Column Chart**.</span></span> <span data-ttu-id="83208-174">Zorg ervoor dat **stad** veld **as gebied** en **vin** in **waarde gebied**</span><span class="sxs-lookup"><span data-stu-id="83208-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="83208-175">De grafiek sorteren door **'Aantal van vin'**</span><span class="sxs-lookup"><span data-stu-id="83208-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="83208-176">![Verbonden auto - telling van vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="83208-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="83208-177">Diagram wijzigen **titel** naar **'Voertuigen in bewerking per plaats'**</span><span class="sxs-lookup"><span data-stu-id="83208-177">Change chart **Title** to **“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="83208-178">Klik op de **indeling** sectie en selecteer vervolgens **gegevens kleuren**, klikt u op de **'Op'** naar **Alles weergeven**</span><span class="sxs-lookup"><span data-stu-id="83208-178">Click the **Format** section, then select **Data Colors**,  Click the **“On”** to **Show All**</span></span>  
    <span data-ttu-id="83208-179">![Verbonden auto - weergeven alle gegevens kleuren](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="83208-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="83208-180">De kleur van afzonderlijke plaats door te klikken op het Kleurenpictogram wijzigen.</span><span class="sxs-lookup"><span data-stu-id="83208-180">Change the color of individual city by clicking on color icon.</span></span>  
    ![Verbonden auto - kleuren wijzigen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="83208-182">Klik op het lege gebied om toe te voegen nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="83208-182">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="83208-183">Selecteer **kolomdiagram geclusterde** visualisatie van visualisaties, Sleep **stad** veld **as** gebied **Model** in **Legenda** gebied en **vin** in **waarde** gebied.</span><span class="sxs-lookup"><span data-stu-id="83208-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="83208-184">![Verbonden auto - gegroepeerd kolomdiagram](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="83208-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="83208-185">![Verbonden auto - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="83208-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="83208-186">Alle visualisaties op deze pagina rangschikken zoals weergegeven in afbeelding.</span><span class="sxs-lookup"><span data-stu-id="83208-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Verbonden auto - visualisaties](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="83208-188">U hebt het real-time rapport 'Voertuigen in bewerking' geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="83208-188">You have successfully configured the “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="83208-189">U kunt doorgaan met het volgende realtime rapport gemaakt of hier stoppen en het configureren van het dashboard.</span><span class="sxs-lookup"><span data-stu-id="83208-189">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="83208-190">2. Voertuigen onderhoud vereisen</span><span class="sxs-lookup"><span data-stu-id="83208-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="83208-191">Klik op ![toevoegen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) om een nieuw rapport toevoegt, wijzigt u de naam **'Voertuigen vereisen onderhoud'**</span><span class="sxs-lookup"><span data-stu-id="83208-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add a new report, rename it to **“Vehicles Requiring Maintenance”**</span></span>

![Verbonden auto - voertuigen onderhoud vereisen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="83208-193">Selecteer **vin** veld en wijzigt in visualisatie **kaart**.</span><span class="sxs-lookup"><span data-stu-id="83208-193">Select **vin** field and change visualization type to **Card**.</span></span>  
    <span data-ttu-id="83208-194">![Verbonden auto - visualisatie Vin-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="83208-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="83208-195">We hebben een veld met de naam 'MaintenanceLabel' In de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="83208-195">We have a field named “MaintenanceLabel” In the dataset.</span></span> <span data-ttu-id="83208-196">Dit veld kan een waarde van '0' of '1' hebben."</span><span class="sxs-lookup"><span data-stu-id="83208-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="83208-197">Deze waarde is ingesteld door het Azure Machine Learning-model ingericht als onderdeel van de oplossing en geïntegreerd met het real-time pad.</span><span class="sxs-lookup"><span data-stu-id="83208-197">It is set by the Azure Machine Learning model provisioned as part of solution and integrated with the real-time path.</span></span> <span data-ttu-id="83208-198">De waarde '1' geeft dat een medium vereist onderhoud.</span><span class="sxs-lookup"><span data-stu-id="83208-198">The value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="83208-199">Om toe te voegen een **paginaniveau** filter voor het weergeven van voertuigen gegevens, die onderhoud vereisen:</span><span class="sxs-lookup"><span data-stu-id="83208-199">To add a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="83208-200">Sleep de **'MaintenanceLabel'** veld in **niveau paginafilters**.</span><span class="sxs-lookup"><span data-stu-id="83208-200">Drag the **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="83208-201">![Verbonden auto - Filters paginaniveau](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="83208-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="83208-202">Klik op **Basic filteren** menu aan de onderkant van het niveau van MaintenanceLabel paginafilter aanwezig.</span><span class="sxs-lookup"><span data-stu-id="83208-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="83208-203">![Verbonden auto - Basic filteren](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="83208-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="83208-204">Stel de filterwaarde op **'1'**  </span><span class="sxs-lookup"><span data-stu-id="83208-204">Set its filter value to **“1”**  </span></span>  
   <span data-ttu-id="83208-205">![Verbonden auto - filterwaarde](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="83208-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="83208-206">Klik op het lege gebied om toe te voegen nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="83208-206">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="83208-207">Selecteer **kolomdiagram geclusterde** van visualisaties</span><span class="sxs-lookup"><span data-stu-id="83208-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="83208-208">![Verbonden auto - visualisatie Vind-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="83208-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="83208-209">![Verbonden auto - gegroepeerd kolomdiagram](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="83208-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="83208-210">Sleep veld **Model** in **as** gebied **Vin** naar **waarde** gebied.</span><span class="sxs-lookup"><span data-stu-id="83208-210">Drag field **Model** into **Axis** area, **Vin** to **Value** area.</span></span> <span data-ttu-id="83208-211">Sorteer visualisatie door **aantal vin**.</span><span class="sxs-lookup"><span data-stu-id="83208-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="83208-212">Diagram wijzigen **titel** naar **"Voertuigen onderhoud vereisen door model"**</span><span class="sxs-lookup"><span data-stu-id="83208-212">Change chart **Title** to **“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="83208-213">Sleep **vin** velden in **kleurverzadiging** aanwezig zijn bij **velden** ![velden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) sectie van **visualisatie**tabblad</span><span class="sxs-lookup"><span data-stu-id="83208-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="83208-214">![Verbonden auto - kleurverzadiging](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="83208-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="83208-215">Wijziging **gegevens kleuren** in visualisaties van **indeling** sectie</span><span class="sxs-lookup"><span data-stu-id="83208-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="83208-216">Minimale kleur te wijzigen: **F2C812**</span><span class="sxs-lookup"><span data-stu-id="83208-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="83208-217">Maximale kleur te wijzigen: **FF6300**</span><span class="sxs-lookup"><span data-stu-id="83208-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="83208-218">![Auto - wijzigingen in de kleuren verbonden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="83208-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="83208-219">![Verbonden auto - nieuwe visualisatie kleuren](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="83208-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="83208-220">Klik op het lege gebied om toe te voegen nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="83208-220">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="83208-221">Selecteer **gegroepeerd kolomdiagram** visualisaties, Sleep **vin** veld in **waarde** gebied slepen **stad** veld in **As** gebied.</span><span class="sxs-lookup"><span data-stu-id="83208-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="83208-222">De grafiek sorteren door **'Aantal van vin'**.</span><span class="sxs-lookup"><span data-stu-id="83208-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="83208-223">Diagram wijzigen **titel** naar **'Voertuigen vereisen onderhoud per plaats'** </span><span class="sxs-lookup"><span data-stu-id="83208-223">Change chart **Title** to **“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="83208-224">![Verbonden auto - voertuigen onderhoud per plaats vereisen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="83208-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="83208-225">Klik op het lege gebied om toe te voegen nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="83208-225">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="83208-226">Selecteer **met meerdere rijen kaart** visualisatie van visualisaties, Sleep **Model** en **vin** in de **velden** gebied.</span><span class="sxs-lookup"><span data-stu-id="83208-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into the **Fields** area.</span></span>  
<span data-ttu-id="83208-227">![Verbonden auto - meerdere rij-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="83208-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="83208-228">Herschikken alle van de visualisatie, het laatste rapport ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="83208-228">Rearranging all of the visualization, the final report looks as follows:</span></span>  
![Verbonden auto - meerdere rij-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="83208-230">U hebt het real-time rapport 'Voertuigen vereisen onderhoud' geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="83208-230">You have successfully configured the “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="83208-231">U kunt doorgaan met het volgende realtime rapport gemaakt of hier stoppen en het configureren van het dashboard.</span><span class="sxs-lookup"><span data-stu-id="83208-231">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="83208-232">3. Voertuigen Health statistieken</span><span class="sxs-lookup"><span data-stu-id="83208-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="83208-233">Klik op ![toevoegen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) voor het nieuwe rapport toevoegt, wijzigt u de naam **'Voertuigen Health statistieken'**</span><span class="sxs-lookup"><span data-stu-id="83208-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add new report, rename it to **“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="83208-234">Selecteer **meter** visualisatie van visualisaties, Sleep de **snelheid** veld in **waarde, minimumwaarde, maximumwaarde** gebieden.</span><span class="sxs-lookup"><span data-stu-id="83208-234">Select **Gauge** visualization from visualizations, then drag the **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="83208-235">![Verbonden auto - meerdere rij-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="83208-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="83208-236">Wijzigen van de standaard-aggregatie van **snelheid** in **waarde gebied** naar **gemiddelde**</span><span class="sxs-lookup"><span data-stu-id="83208-236">Change the default aggregation of **speed** in **Value area** to **Average**</span></span> 

<span data-ttu-id="83208-237">Wijzigen van de standaard-aggregatie van **snelheid** in **Minimum gebied** naar **Minimum**</span><span class="sxs-lookup"><span data-stu-id="83208-237">Change the default aggregation of **speed** in **Minimum area** to **Minimum**</span></span>

<span data-ttu-id="83208-238">Wijzigen van de standaard-aggregatie van **snelheid** in **Maximum gebied** naar **maximale**</span><span class="sxs-lookup"><span data-stu-id="83208-238">Change the default aggregation of **speed** in **Maximum area** to **Maximum**</span></span>

![Verbonden auto - meerdere rij-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="83208-240">Wijzig de naam van de **meter titel** naar **'Gemiddelde snelheid'**</span><span class="sxs-lookup"><span data-stu-id="83208-240">Rename the **Gauge Title** to **“Average speed”**</span></span> 

![Verbonden auto - meter](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="83208-242">Klik op het lege gebied om toe te voegen nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="83208-242">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="83208-243">Op dezelfde manier toevoegen een **meter** voor **engine olie gemiddelde**, **gemiddelde brandstof**, en **gemiddelde temperatuur aangeven engine**.</span><span class="sxs-lookup"><span data-stu-id="83208-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="83208-244">Wijzigen van de standaard-aggregatie van velden in elke meter conform bovenstaande stappen in **'Gemiddelde snelheid'** meter.</span><span class="sxs-lookup"><span data-stu-id="83208-244">Change the default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Verbonden auto - meters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="83208-246">Klik op het lege gebied om toe te voegen nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="83208-246">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="83208-247">Selecteer **lijndiagram en gegroepeerd kolomdiagram** van visualisaties, sleept u **stad** veld in **gedeeld as**, sleept u **snelheid**, **velden tirepressure en engineoil** in **kolomwaarden** gebied wijzigt in hun aggregatie **gemiddelde**.</span><span class="sxs-lookup"><span data-stu-id="83208-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type to **Average**.</span></span> 

<span data-ttu-id="83208-248">Sleep de **engineTemperature** veld in **regelwaarden** gebied wijzigt in de aggregatie **gemiddelde**.</span><span class="sxs-lookup"><span data-stu-id="83208-248">Drag the **engineTemperature** field into **Line Values** area, change the  aggregation type to **Average**.</span></span> 

![Verbonden auto - visualisaties velden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="83208-250">Wijzigen van de grafiek **titel** naar **'Gemiddelde snelheid, band druk, engine olie en temperatuur motor'**.</span><span class="sxs-lookup"><span data-stu-id="83208-250">Change the chart **Title** to **“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Verbonden auto - visualisaties velden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="83208-252">Klik op het lege gebied om toe te voegen nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="83208-252">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="83208-253">Selecteer **Treemap** visualisatie van visualisaties, sleept u de **Model** veld in de **groep** gebied en sleep het veld **MaintenanceProbability** in de **waarden** gebied.</span><span class="sxs-lookup"><span data-stu-id="83208-253">Select **Treemap** visualization from visualizations, drag the **Model** field into the **Group** area, and drag the field **MaintenanceProbability** into the **Values** area.</span></span>

<span data-ttu-id="83208-254">Wijzigen van de grafiek **titel** naar **'Vehicle modellen vereisen onderhoud'**.</span><span class="sxs-lookup"><span data-stu-id="83208-254">Change the chart **Title** to **“Vehicle models requiring maintenance”**.</span></span>

![Verbonden auto - grafiektitel wijzigen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="83208-256">Klik op het lege gebied om toe te voegen nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="83208-256">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="83208-257">Selecteer **100% gestapeld staafdiagram** visualisatie, Sleep de **stad** veld in de **as** gebied en sleep de **MaintenanceProbability**, **RecallProbability** velden in de **waarde** gebied.</span><span class="sxs-lookup"><span data-stu-id="83208-257">Select **100% Stacked Bar Chart** from visualization, drag the **city** field into the **Axis** area, and drag the **MaintenanceProbability**, **RecallProbability** fields into the **Value** area.</span></span>

![Verbonden auto - toevoegen nieuwe visualisatie](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="83208-259">Klik op **indeling**, selecteer **gegevens kleuren**, en stel de **MaintenanceProbability** kleur aan de waarde **'F2C80F'**.</span><span class="sxs-lookup"><span data-stu-id="83208-259">Click **Format**, select **Data Colors**, and set the **MaintenanceProbability** color to the value **“F2C80F”**.</span></span>

<span data-ttu-id="83208-260">Wijzig de **titel** van de grafiek **'Waarschijnlijkheid van Vehicle onderhoud & intrekken per plaats'**.</span><span class="sxs-lookup"><span data-stu-id="83208-260">Change the **Title** of the chart to **“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Verbonden auto - toevoegen nieuwe visualisatie](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="83208-262">Klik op het lege gebied om toe te voegen nieuwe visualisatie.</span><span class="sxs-lookup"><span data-stu-id="83208-262">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="83208-263">Selecteer **vlakdiagram** visualisatie van visualisaties Sleep de **Model** veld in de **as** gebied en sleep de **engineOil, tirepressure, de snelheid en MaintenanceProbability** velden in de **waarden** gebied.</span><span class="sxs-lookup"><span data-stu-id="83208-263">Select **Area Chart** from visualization from visualizations, drag the **Model** field into the **Axis** area, and drag the **engineOil, tirepressure, speed and MaintenanceProbability** fields into the **Values** area.</span></span> <span data-ttu-id="83208-264">Wijzigen van hun samenvoegingstype naar **'Gemiddeld'**.</span><span class="sxs-lookup"><span data-stu-id="83208-264">Change their aggregation type to **“Average”**.</span></span> 

![Verbonden auto - aggregatie wijzigingstype](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="83208-266">Wijzig de titel van de grafiek **"Gemiddelde engine olie, druk, snelheid en het onderhoud kans genoeg door model"**.</span><span class="sxs-lookup"><span data-stu-id="83208-266">Change the title of the chart to **“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Verbonden auto - grafiektitel wijzigen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="83208-268">Klik op het lege gebied om toe te voegen nieuwe visualisatie:</span><span class="sxs-lookup"><span data-stu-id="83208-268">Click the blank area to add new visualization:</span></span>

1. <span data-ttu-id="83208-269">Selecteer **grafiek spreidingsdiagrammen** visualisatie van visualisaties.</span><span class="sxs-lookup"><span data-stu-id="83208-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="83208-270">Sleep de **Model** veld in de **Details** en **legenda** gebied.</span><span class="sxs-lookup"><span data-stu-id="83208-270">Drag the **Model** field into the **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="83208-271">Sleep de **brandstof** veld in de **x-as** gebied wijzigen van de aggregatie op **gemiddelde**.</span><span class="sxs-lookup"><span data-stu-id="83208-271">Drag the **fuel** field into the **X-Axis** area, change the aggregation to **Average**.</span></span>
4. <span data-ttu-id="83208-272">Sleep **engineTemparature** in **y-as gebied**, wijzig de aggregatie op **gemiddelde**</span><span class="sxs-lookup"><span data-stu-id="83208-272">Drag **engineTemparature** into **Y-Axis area**, change the aggregation to **Average**</span></span>
5. <span data-ttu-id="83208-273">Sleep de **vin** veld in de **grootte** gebied.</span><span class="sxs-lookup"><span data-stu-id="83208-273">Drag the **vin** field into the **Size** area.</span></span>

![Verbonden auto - toevoegen nieuwe visualisatie](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="83208-275">Wijzigen van de grafiek **titel** naar **"Gemiddelden van brandstof, Engine temperatuur door Model"**.</span><span class="sxs-lookup"><span data-stu-id="83208-275">Change the chart **Title** to **“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Verbonden auto - grafiektitel wijzigen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="83208-277">Het laatste rapport eruit als zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="83208-277">The final report will look like as shown below.</span></span>

![Auto-Final rapport verbonden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-the-reports-to-the-real-time-dashboard"></a><span data-ttu-id="83208-279">Pincode visualisaties van de rapporten naar het real-time dashboard</span><span class="sxs-lookup"><span data-stu-id="83208-279">Pin visualizations from the reports to the real-time dashboard</span></span>
<span data-ttu-id="83208-280">Een lege dashboard door te klikken op het plusteken naast Dashboards maken.</span><span class="sxs-lookup"><span data-stu-id="83208-280">Create a blank dashboard by clicking on the plus icon next to Dashboards.</span></span> <span data-ttu-id="83208-281">U kunt andere naam 'Vehicle telemetrie Analytics Dashboard'</span><span class="sxs-lookup"><span data-stu-id="83208-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Verbonden auto-Dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="83208-283">De visualisatie uit de bovenstaande rapporten naar het dashboard vastmaken.</span><span class="sxs-lookup"><span data-stu-id="83208-283">Pin the visualization from the above reports to the dashboard.</span></span> 

![Verbonden auto-Dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="83208-285">Het dashboard ziet er als volgt wanneer de drie rapporten zijn gemaakt en de bijbehorende visualisaties worden vastgemaakt aan het dashboard.</span><span class="sxs-lookup"><span data-stu-id="83208-285">The dashboard should look as follows when all the three reports are created and the corresponding visualizations are pinned to the dashboard.</span></span> <span data-ttu-id="83208-286">Als u niet alle rapporten hebt gemaakt, kan uw dashboard anders zijn.</span><span class="sxs-lookup"><span data-stu-id="83208-286">If you have not created all the reports, your dashboard could look different.</span></span> 

![Verbonden auto-Dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="83208-288">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="83208-288">Congratulations!</span></span> <span data-ttu-id="83208-289">U hebt het real-time dashboard gemaakt.</span><span class="sxs-lookup"><span data-stu-id="83208-289">You have successfully created the real-time dashboard.</span></span> <span data-ttu-id="83208-290">Als u doorgaat CarEventGenerator.exe en RealtimeDashboardApp.exe uit te voeren, ziet u live updates op het dashboard.</span><span class="sxs-lookup"><span data-stu-id="83208-290">As you continue to execute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on the dashboard.</span></span> <span data-ttu-id="83208-291">Het moet ongeveer 10 tot 15 minuten duren voordat de volgende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="83208-291">It should take about 10 to 15 minutes to complete the following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="83208-292">Power BI batch-verwerking dashboard instellen</span><span class="sxs-lookup"><span data-stu-id="83208-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="83208-293">Het duurt ongeveer twee uur (van de voltooiing van de implementatie) voor de pijplijn complete batchverwerking uitvoering is voltooid en een jaar waard van gegenereerde gegevens verwerkt.</span><span class="sxs-lookup"><span data-stu-id="83208-293">It takes about two hours (from the successful completion of the deployment) for the end to end batch processing pipeline to finish execution and process a year worth of generated data.</span></span> <span data-ttu-id="83208-294">Dus wacht u totdat de verwerking te voltooien voordat u doorgaat met de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="83208-294">So wait for the processing to finish before proceeding with the next steps.</span></span> 
> 
> 

<span data-ttu-id="83208-295">**Download het Power BI designer**</span><span class="sxs-lookup"><span data-stu-id="83208-295">**Download the Power BI designer file**</span></span>

* <span data-ttu-id="83208-296">Een vooraf geconfigureerde Power BI designer-bestand is opgenomen als onderdeel van de implementatie handmatig bewerking instructies</span><span class="sxs-lookup"><span data-stu-id="83208-296">A pre-configured Power BI designer file is included as part of the deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="83208-297">Zoek naar 2.</span><span class="sxs-lookup"><span data-stu-id="83208-297">Look for 2.</span></span> <span data-ttu-id="83208-298">Het installatieprogramma Power BI batch verwerking dashboard kunt u de Power BI-sjabloon voor batchverwerking dashboard hier aangeroepen downloaden **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="83208-298">Setup PowerBI batch processing dashboard You can download the PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="83208-299">Lokaal opslaan</span><span class="sxs-lookup"><span data-stu-id="83208-299">Save locally</span></span>

<span data-ttu-id="83208-300">**Power BI-rapporten configureren**</span><span class="sxs-lookup"><span data-stu-id="83208-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="83208-301">Open het bestand designer '**ConnectedCarsPbiReport.pbix**' met behulp van Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="83208-301">Open the designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="83208-302">Als u nog geen, installeert u Power BI Desktop van [Power BI Desktop installeren](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="83208-302">If you do not already have, install the Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="83208-303">Klik op de **query's bewerken**.</span><span class="sxs-lookup"><span data-stu-id="83208-303">Click the **Edit Queries**.</span></span>

![Power BI query bewerken](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="83208-305">Dubbelklik op de **bron**.</span><span class="sxs-lookup"><span data-stu-id="83208-305">Double-click the **Source**.</span></span>

![Set Power BI-bron](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="83208-307">Server-verbindingsreeks bijwerken met de Azure SQL-server die als onderdeel van de implementatie is ingericht.</span><span class="sxs-lookup"><span data-stu-id="83208-307">Update Server connection string with the Azure SQL server that got provisioned as part of the deployment.</span></span>  <span data-ttu-id="83208-308">Zoeken in de handmatige bewerking instructies onder</span><span class="sxs-lookup"><span data-stu-id="83208-308">Look in the Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="83208-309">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="83208-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="83208-310">Server: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="83208-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="83208-311">Database: connectedcar</span><span class="sxs-lookup"><span data-stu-id="83208-311">Database: connectedcar</span></span>
    * <span data-ttu-id="83208-312">Gebruikersnaam: gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="83208-312">Username: username</span></span>
    * <span data-ttu-id="83208-313">Wachtwoord: U kunt het wachtwoord van uw SQL-server beheren vanuit Azure-portal</span><span class="sxs-lookup"><span data-stu-id="83208-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="83208-314">Laat **Database** als *connectedcar*.</span><span class="sxs-lookup"><span data-stu-id="83208-314">Leave **Database** as *connectedcar*.</span></span>

![Stel de database in Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="83208-316">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="83208-316">Click **OK**.</span></span>
* <span data-ttu-id="83208-317">U ziet **Windows-referentie** tabblad standaard geselecteerd, wijzigen in **Database referenties** door te klikken op **Database** tabblad rechts.</span><span class="sxs-lookup"><span data-stu-id="83208-317">You will see **Windows credential** tab selected by default, change it to **Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="83208-318">Geef de **gebruikersnaam** en **wachtwoord** van uw Azure SQL Database die is opgegeven tijdens de installatie van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="83208-318">Provide the **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![Geef databasereferenties op](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="83208-320">Klik op **verbinding maken**</span><span class="sxs-lookup"><span data-stu-id="83208-320">Click **Connect**</span></span>
* <span data-ttu-id="83208-321">Herhaal de bovenstaande stappen voor elk van de drie resterende query's aanwezig zijn bij het rechter deelvenster en werk vervolgens de details van gegevensbron verbinding.</span><span class="sxs-lookup"><span data-stu-id="83208-321">Repeat the above steps for each of the three remaining queries present at right pane, and then update the data source connection details.</span></span>
* <span data-ttu-id="83208-322">Klik op **sluiten en te laden**.</span><span class="sxs-lookup"><span data-stu-id="83208-322">Click **Close and Load**.</span></span> <span data-ttu-id="83208-323">Power BI Desktop-bestand gegevenssets zijn verbonden met SQL Azure Database-tabellen.</span><span class="sxs-lookup"><span data-stu-id="83208-323">Power BI Desktop file datasets are connected to SQL Azure Database tables.</span></span>
* <span data-ttu-id="83208-324">**Sluit** Power BI Desktop-bestand.</span><span class="sxs-lookup"><span data-stu-id="83208-324">**Close** Power BI Desktop file.</span></span>

![Sluit Power BI desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="83208-326">Klik op **opslaan** knop de wijzigingen wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="83208-326">Click **Save** button to save the changes.</span></span> 

<span data-ttu-id="83208-327">U hebt nu alle rapporten die overeenkomt met het pad voor het verwerken van batch in de oplossing hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="83208-327">You have now configured all the reports corresponding to the batch processing path in the solution.</span></span> 

## <a name="upload-to-powerbicom"></a><span data-ttu-id="83208-328">Uploaden naar *powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="83208-328">Upload to *powerbi.com*</span></span>
1. <span data-ttu-id="83208-329">Navigeer naar de Power BI-webportal op http://powerbi.com en meld u aan.</span><span class="sxs-lookup"><span data-stu-id="83208-329">Navigate to the Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="83208-330">Klik op **gegevens ophalen**</span><span class="sxs-lookup"><span data-stu-id="83208-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="83208-331">De Power BI Desktop-bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="83208-331">Upload the Power BI Desktop File.</span></span>  
4. <span data-ttu-id="83208-332">Als u wilt uploaden, klikt u op **gegevens ophalen -> bestanden ophalen -> lokaal bestand**</span><span class="sxs-lookup"><span data-stu-id="83208-332">To upload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="83208-333">Navigeer naar de **'**ConnectedCarsPbiReport.pbix**'**</span><span class="sxs-lookup"><span data-stu-id="83208-333">Navigate to the **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="83208-334">Zodra het bestand is geüpload, wordt u gaat terug naar uw Power BI-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="83208-334">Once the file is uploaded, you will be navigated back to your Power BI work space.</span></span>  

<span data-ttu-id="83208-335">Een gegevensset, rapport en een lege dashboard wordt voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="83208-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="83208-336">Pincode-grafieken vast aan een nieuw dashboard aangeroepen **Dashboard met analytische telemetrie Vehicle** in **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="83208-336">Pin charts to a new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="83208-337">Klik op de lege dashboard die eerder is gemaakt en navigeer vervolgens naar de **rapporten** sectie op het rapport dat recent geüploade.</span><span class="sxs-lookup"><span data-stu-id="83208-337">Click the blank dashboard created above and then navigate to the **Reports** section click the newly uploaded report.</span></span>  

![Vehicle telemetrie Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="83208-339">**Houd rekening met dat het rapport heeft zes pagina's:**</span><span class="sxs-lookup"><span data-stu-id="83208-339">**Note the report has six pages:**</span></span>  
<span data-ttu-id="83208-340">Pagina 1: Vehicle dichtheid</span><span class="sxs-lookup"><span data-stu-id="83208-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="83208-341">Pagina 2: Realtime vehicle health</span><span class="sxs-lookup"><span data-stu-id="83208-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="83208-342">Pagina 3: Aangestuurd agressief voertuigen</span><span class="sxs-lookup"><span data-stu-id="83208-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="83208-343">Pagina 4: Teruggehaald voertuigen</span><span class="sxs-lookup"><span data-stu-id="83208-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="83208-344">Pagina 5: Brandstof efficiënt aangedreven voertuigen</span><span class="sxs-lookup"><span data-stu-id="83208-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="83208-345">Pagina 6: Contoso-Logo</span><span class="sxs-lookup"><span data-stu-id="83208-345">Page 6: Contoso Logo</span></span>  

![Verbonden auto's Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="83208-347">**Vanaf 3 pagina**, pincode van de volgende:</span><span class="sxs-lookup"><span data-stu-id="83208-347">**From Page 3**, pin the following:</span></span>  

1. <span data-ttu-id="83208-348">Telling van VIN</span><span class="sxs-lookup"><span data-stu-id="83208-348">Count of VIN</span></span>  
   ![Verbonden auto's Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="83208-350">Agressief voertuigen aangedreven door model – waterval grafiek</span><span class="sxs-lookup"><span data-stu-id="83208-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![Vehicle telemetrie - pincode grafieken 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="83208-352">**Van pagina 5**, pincode van de volgende:</span><span class="sxs-lookup"><span data-stu-id="83208-352">**From Page 5**, pin the following:</span></span> 

1. <span data-ttu-id="83208-353">Telling van vin</span><span class="sxs-lookup"><span data-stu-id="83208-353">Count of vin</span></span>    
   ![Vehicle telemetrie - grafieken van de pincode 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="83208-355">Efficiënte voertuigen brandstof door model: gegroepeerd kolomdiagram</span><span class="sxs-lookup"><span data-stu-id="83208-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![Vehicle telemetrie - pincode grafieken 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="83208-357">**Van pagina 4**, pincode van de volgende:</span><span class="sxs-lookup"><span data-stu-id="83208-357">**From Page 4**, pin the following:</span></span>  

1. <span data-ttu-id="83208-358">Telling van vin</span><span class="sxs-lookup"><span data-stu-id="83208-358">Count of vin</span></span>  
   ![Vehicle telemetrie - pincode grafieken 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="83208-360">Ingetrokken voertuigen per plaats, model: Treemap</span><span class="sxs-lookup"><span data-stu-id="83208-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![Vehicle telemetrie - pincode grafieken 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="83208-362">**Pagina 6**, pincode van de volgende:</span><span class="sxs-lookup"><span data-stu-id="83208-362">**From Page 6**, pin the following:</span></span>  

1. <span data-ttu-id="83208-363">Contoso motoren-logo</span><span class="sxs-lookup"><span data-stu-id="83208-363">Contoso Motors logo</span></span>  
   ![Vehicle telemetrie - pincode grafieken 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="83208-365">**Het dashboard te delen**</span><span class="sxs-lookup"><span data-stu-id="83208-365">**Organize the dashboard**</span></span>  

1. <span data-ttu-id="83208-366">Ga naar het dashboard</span><span class="sxs-lookup"><span data-stu-id="83208-366">Navigate to the dashboard</span></span>
2. <span data-ttu-id="83208-367">Beweeg de muisaanwijzer over elke grafiek en wijzig de naam van dit op basis van de naamgeving opgegeven in de onderstaande afbeelding van volledige dashboard.</span><span class="sxs-lookup"><span data-stu-id="83208-367">Hover over each chart and rename it based on the naming provided in the complete dashboard image below.</span></span> <span data-ttu-id="83208-368">De grafieken rond ook verplaatsen eruitzien zoals bij het onderstaande dashboard.</span><span class="sxs-lookup"><span data-stu-id="83208-368">Also move the charts around to look like the dashboard below.</span></span>  
   ![Vehicle telemetrie - Dashboard 2 ordenen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Vehicle telemetrie Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="83208-371">Als u kunt de rapporten hebt gemaakt, zoals vermeld in dit document, is de laatste voltooide dashboard moet eruitzien als in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="83208-371">If you have created all the reports as mentioned in this document, the final completed dashboard should look like the following figure.</span></span> 

![Vehicle telemetrie - Dashboard 2 ordenen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="83208-373">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="83208-373">Congratulations!</span></span> <span data-ttu-id="83208-374">U hebt gemaakt met de rapporten en het dashboard te krijgen van realtime, voorspellende batch-inzichten op vehicle status en groot gewoonten.</span><span class="sxs-lookup"><span data-stu-id="83208-374">You have successfully created the reports and the dashboard to gain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  

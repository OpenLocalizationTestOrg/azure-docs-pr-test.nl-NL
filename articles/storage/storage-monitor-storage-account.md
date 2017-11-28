---
title: Een Azure Storage-account controleren | Microsoft Docs
description: Informatie over het bewaken van een opslagaccount in Azure met behulp van de Azure-portal.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: b49e06da0019a50cc8e50c4da47e42c03b44bcc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-storage-account-in-the-azure-portal"></a><span data-ttu-id="42f13-103">Een opslagaccount in de Azure portal controleren</span><span class="sxs-lookup"><span data-stu-id="42f13-103">Monitor a storage account in the Azure portal</span></span>

<span data-ttu-id="42f13-104">[Azure Storage Analytics](storage-analytics.md) voorziet in maatstaven voor alle storage-services en logboeken voor blobs, wachtrijen en tabellen.</span><span class="sxs-lookup"><span data-stu-id="42f13-104">[Azure Storage Analytics](storage-analytics.md) provides metrics for all storage services, and logs for blobs, queues, and tables.</span></span> <span data-ttu-id="42f13-105">U kunt de [Azure-portal](https://portal.azure.com) configureren welke metrische gegevens en de logboeken worden geregistreerd voor uw account en grafieken die visuele weergaven van de metrische gegevens bieden configureren.</span><span class="sxs-lookup"><span data-stu-id="42f13-105">You can use the [Azure portal](https://portal.azure.com) to configure which metrics and logs are recorded for your account, and configure charts that provide visual representations of your metrics data.</span></span>

> [!NOTE]
> <span data-ttu-id="42f13-106">Er worden kosten in verband met het onderzoeken van controlegegevens in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="42f13-106">There are costs associated with examining monitoring data in the Azure portal.</span></span> <span data-ttu-id="42f13-107">Zie voor meer informatie [Storage Analytics en facturering](/rest/api/storageservices/Storage-Analytics-and-Billing).</span><span class="sxs-lookup"><span data-stu-id="42f13-107">For more information, see [Storage Analytics and Billing](/rest/api/storageservices/Storage-Analytics-and-Billing).</span></span>
>
> <span data-ttu-id="42f13-108">Azure File storage momenteel ondersteunt Opslaganalyse metrische gegevens, maar logboekregistratie nog niet ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="42f13-108">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>
> <span data-ttu-id="42f13-109">Storage-accounts met een replicatietype van de Zone-redundante opslag (ZRS) momenteel beschikt niet over de metrische gegevens of mogelijkheden voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="42f13-109">Storage accounts with a replication type of Zone-Redundant Storage (ZRS) currently do not have the metrics or logging capability enabled.</span></span>
> 
> <span data-ttu-id="42f13-110">Zie voor een gedetailleerde uitleg over het gebruik van Storage Analytics en andere hulpprogramma's om te bepalen, onderzoeken en oplossen van problemen met Azure Storage met [Monitor, vaststellen en oplossen van Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="42f13-110">For an in-depth guide on using Storage Analytics and other tools to identify, diagnose, and troubleshoot Azure Storage-related issues, see [Monitor, diagnose, and troubleshoot Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span></span>
>

## <a name="configure-monitoring-for-a-storage-account"></a><span data-ttu-id="42f13-111">Bewaking configureren voor een opslagaccount</span><span class="sxs-lookup"><span data-stu-id="42f13-111">Configure monitoring for a storage account</span></span>

1. <span data-ttu-id="42f13-112">In de [Azure-portal](https://portal.azure.com), selecteer **opslagaccounts**, klikt u vervolgens de opslagaccountnaam om de account-dashboard te openen.</span><span class="sxs-lookup"><span data-stu-id="42f13-112">In the [Azure portal](https://portal.azure.com), select **Storage accounts**, then the storage account name to open the account dashboard.</span></span>
1. <span data-ttu-id="42f13-113">Selecteer **Diagnostics** in de **bewaking** sectie van de blade menu.</span><span class="sxs-lookup"><span data-stu-id="42f13-113">Select **Diagnostics** in the **MONITORING** section of the menu blade.</span></span>

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. <span data-ttu-id="42f13-115">Selecteer de **type** van metrische gegevens voor elke **service** u wilt bewaken, en de **bewaarbeleid** voor de gegevens.</span><span class="sxs-lookup"><span data-stu-id="42f13-115">Select the **type** of metrics data for each **service** you wish to monitor, and the **retention policy** for the data.</span></span> <span data-ttu-id="42f13-116">U kunt ook uitschakelen door in te stellen bewaking **Status** naar **uit**.</span><span class="sxs-lookup"><span data-stu-id="42f13-116">You can also disable monitoring by setting **Status** to **Off**.</span></span>

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   <span data-ttu-id="42f13-118">Er zijn twee soorten metrische gegevens die kunt u inschakelen voor elke service, die beide zijn standaard ingeschakeld voor nieuwe storage-accounts:</span><span class="sxs-lookup"><span data-stu-id="42f13-118">There are two types of metrics you can enable for each service, both of which are enabled by default for new storage accounts:</span></span>

   * <span data-ttu-id="42f13-119">**Cumulatieve**: metrische gegevens zoals inkomend en uitgaand, beschikbaarheid, latentie en geslaagd percentages verzamelt.</span><span class="sxs-lookup"><span data-stu-id="42f13-119">**Aggregate**: Collects metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="42f13-120">Deze metrische gegevens worden voor de blob, queue, table en Bestandsservices samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="42f13-120">These metrics are aggregated for the blob, queue, table, and file services.</span></span>
   * <span data-ttu-id="42f13-121">**Per API**: naast de cumulatieve metrische gegevens, verzamelt u dezelfde set van metrische gegevens voor elke opslagbewerking in de API van Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="42f13-121">**Per API**: In addition to the aggregate metrics, collects the same set of metrics for each storage operation in the Azure Storage service API.</span></span>

   <span data-ttu-id="42f13-122">Om in te stellen het bewaarbeleid voor gegevens, gaan de **bewaartermijn (dagen)** schuifregelaar of Voer het aantal dagen aan gegevens te behouden tussen 1 en 365.</span><span class="sxs-lookup"><span data-stu-id="42f13-122">To set the data retention policy, move the **Retention (days)** slider or enter the number of days of data to retain, from 1 to 365.</span></span> <span data-ttu-id="42f13-123">De standaardwaarde voor nieuwe opslagaccounts is zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="42f13-123">The default for new storage accounts is seven days.</span></span> <span data-ttu-id="42f13-124">Als u niet een bewaarbeleid instellen wilt, voert u nul.</span><span class="sxs-lookup"><span data-stu-id="42f13-124">If you do not want to set a retention policy, enter zero.</span></span> <span data-ttu-id="42f13-125">Als er geen bewaarbeleid, is het tot u de bewakingsgegevens verwijderen.</span><span class="sxs-lookup"><span data-stu-id="42f13-125">If there is no retention policy, it is up to you to delete the monitoring data.</span></span>

   > [!WARNING]
   > <span data-ttu-id="42f13-126">U in rekening worden gebracht wanneer u metrische gegevens voor het handmatig verwijderen.</span><span class="sxs-lookup"><span data-stu-id="42f13-126">You are charged when you manually delete metrics data.</span></span> <span data-ttu-id="42f13-127">Verouderde analytische gegevens (gegevens die ouder zijn dan het bewaarbeleid) is verwijderd door het systeem zonder kosten.</span><span class="sxs-lookup"><span data-stu-id="42f13-127">Stale analytics data (data older than your retention policy) is deleted by the system at no cost.</span></span> <span data-ttu-id="42f13-128">Het is raadzaam om een bewaarbeleid voor afhankelijk van hoe lang u wilt behouden storage analytics-gegevens voor uw account instellen.</span><span class="sxs-lookup"><span data-stu-id="42f13-128">We recommend setting a retention policy based on how long you want to retain storage analytics data for your account.</span></span> <span data-ttu-id="42f13-129">Zie [welke kosten komen er gemaakt bij het inschakelen van metrische gegevens storage?](storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="42f13-129">See [What charges do you incur when you enable storage metrics?](storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) for more information.</span></span>
   >

1. <span data-ttu-id="42f13-130">Wanneer u klaar bent met de configuratie van de bewaking, selecteert u **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="42f13-130">When you finish the monitoring configuration, select **Save**.</span></span>

<span data-ttu-id="42f13-131">Een standaardset metrische gegevens wordt weergegeven in de grafieken op de blade opslagaccount, evenals de blades afzonderlijke service (blob, queue, table en -bestand).</span><span class="sxs-lookup"><span data-stu-id="42f13-131">A default set of metrics is displayed in charts on the storage account blade, as well as the individual service blades (blob, queue, table, and file).</span></span> <span data-ttu-id="42f13-132">Nadat u metrische gegevens voor een service hebt ingeschakeld, kan deze gegevens worden weergegeven in de grafieken een uur duren.</span><span class="sxs-lookup"><span data-stu-id="42f13-132">Once you've enabled metrics for a service, it may take up to an hour for data to appear in its charts.</span></span> <span data-ttu-id="42f13-133">U kunt selecteren **bewerken** op een metrische grafiek voor [configureren welke metrische gegevens](#how-to-customize-metrics-charts) worden weergegeven in de grafiek.</span><span class="sxs-lookup"><span data-stu-id="42f13-133">You can select **Edit** on any metric chart to [configure which metrics](#how-to-customize-metrics-charts) are displayed in the chart.</span></span>

<span data-ttu-id="42f13-134">U kunt metrische gegevens verzamelen en logboekregistratie uitschakelen door in te stellen **Status** naar **uit**.</span><span class="sxs-lookup"><span data-stu-id="42f13-134">You can disable metrics collection and logging by setting **Status** to **Off**.</span></span>

> [!NOTE]
> <span data-ttu-id="42f13-135">Azure Storage maakt gebruik van [tabel opslag](storage-introduction.md#table-storage) voor het opslaan van de metrische gegevens voor uw opslagaccount en slaat de metrische gegevens in de tabellen in uw account.</span><span class="sxs-lookup"><span data-stu-id="42f13-135">Azure Storage uses [table storage](storage-introduction.md#table-storage) to store the metrics for your storage account, and stores the metrics in tables in your account.</span></span> <span data-ttu-id="42f13-136">Zie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="42f13-136">For more information, see.</span></span> <span data-ttu-id="42f13-137">[Hoe metrische gegevens worden opgeslagen](storage-analytics.md#how-metrics-are-stored).</span><span class="sxs-lookup"><span data-stu-id="42f13-137">[How metrics are stored](storage-analytics.md#how-metrics-are-stored).</span></span>
>

## <a name="customize-metrics-charts"></a><span data-ttu-id="42f13-138">Metrische gegevens grafieken aanpassen</span><span class="sxs-lookup"><span data-stu-id="42f13-138">Customize metrics charts</span></span>

<span data-ttu-id="42f13-139">Gebruik de volgende procedure om te kiezen welke opslag metrische gegevens om weer te geven in een grafiek metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="42f13-139">Use the following procedure to choose which storage metrics to view in a metrics chart.</span></span> 

1. <span data-ttu-id="42f13-140">Start een metrische grafiek opslag in de Azure-portal weergegeven.</span><span class="sxs-lookup"><span data-stu-id="42f13-140">Start by displaying a storage metric chart in the Azure portal.</span></span> <span data-ttu-id="42f13-141">U kunt grafieken vinden op de **blade opslagaccount** en in de **metrische gegevens** blade voor een afzonderlijke service (blob, queue, table, bestand).</span><span class="sxs-lookup"><span data-stu-id="42f13-141">You can find charts on the **storage account blade** and in the **Metrics** blade for an individual service (blob, queue, table, file).</span></span>

   <span data-ttu-id="42f13-142">In dit voorbeeld werken we met het volgende diagram dat wordt weergegeven op de **blade opslagaccount**:</span><span class="sxs-lookup"><span data-stu-id="42f13-142">In this example, we work with the following chart that appears on the **storage account blade**:</span></span>

   ![Grafiekselectie in Azure-portal](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. <span data-ttu-id="42f13-144">Klik vervolgens op een willekeurige plaats in de grafiek openen de **metriek** blade.</span><span class="sxs-lookup"><span data-stu-id="42f13-144">Next, click anywhere within the chart to open the **Metric** blade.</span></span> <span data-ttu-id="42f13-145">Selecteer **grafiek bewerken** openen de **grafiek bewerken** blade.</span><span class="sxs-lookup"><span data-stu-id="42f13-145">Select **Edit chart** to open the **Edit Chart** blade.</span></span>

   ![Knop grafiek op de blade grafiek bewerken](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. <span data-ttu-id="42f13-147">Op de **grafiek bewerken** blade, selecteer de **tijdsbereik** van de metrische gegevens om weer te geven in de grafiek en de **service** (blob, queue, tabel, bestand) waarvan metrische gegevens die u wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="42f13-147">On the **Edit Chart** blade, select the **Time Range** of the metrics to display in the chart, and the **service** (blob, queue, table, file) whose metrics you wish to display.</span></span> <span data-ttu-id="42f13-148">Er is hier voor gekozen om de afgelopen week metrische gegevens voor de blob-service weer te geven:</span><span class="sxs-lookup"><span data-stu-id="42f13-148">Here we've selected to display the past week's metrics for the blob service:</span></span>

   ![Bereik en service tijdzone in de blade grafiek bewerken](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. <span data-ttu-id="42f13-150">Selecteer de afzonderlijke **metrische gegevens** moest u zoals weergegeven in de grafiek, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="42f13-150">Select the individual **metrics** you'd like displayed in the chart, then click **OK**.</span></span> <span data-ttu-id="42f13-151">Bijvoorbeeld, hier we hebt gekozen om weer te geven de *ContainerCount* en *ObjectCount* metrische gegevens:</span><span class="sxs-lookup"><span data-stu-id="42f13-151">For example, here we've chosen to display the *ContainerCount* and *ObjectCount* metrics:</span></span>

   ![Afzonderlijke metrische selectie in de blade grafiek bewerken](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

<span data-ttu-id="42f13-153">De grafiekinstellingen van uw hebben geen invloed op de verzameling, aggregatie of opslag van gegevens in het opslagaccount, alleen de weergave van metrische gegevens van bewaking.</span><span class="sxs-lookup"><span data-stu-id="42f13-153">Your chart settings do not affect the collection, aggregation, or storage of monitoring data in the storage account, only the viewing of metrics data.</span></span>

### <a name="metrics-availability-in-charts"></a><span data-ttu-id="42f13-154">Beschikbaarheid van de metrische gegevens in grafieken</span><span class="sxs-lookup"><span data-stu-id="42f13-154">Metrics availability in charts</span></span>

<span data-ttu-id="42f13-155">De lijst met beschikbare metrische gegevens wijzigingen op basis van welke service die u hebt gekozen in de vervolgkeuzelijst en het eenheidstype van de grafiek die u wilt bewerken.</span><span class="sxs-lookup"><span data-stu-id="42f13-155">The list of available metrics changes based on which service you've chosen in the drop-down, and the unit type of the chart you're editing.</span></span> <span data-ttu-id="42f13-156">Bijvoorbeeld, kunt u percentage metrische gegevens zoals *PercentNetworkError* en *PercentThrottlingError* alleen als u een diagram waarin eenheden percentage bewerkt:</span><span class="sxs-lookup"><span data-stu-id="42f13-156">For example, you can select percentage metrics like *PercentNetworkError* and *PercentThrottlingError* only if you're editing a chart that displays units in percentage:</span></span>

![Aanvraag voor fout percentage grafiek in de Azure-portal](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a><span data-ttu-id="42f13-158">Omzetting van de metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="42f13-158">Metrics resolution</span></span>

<span data-ttu-id="42f13-159">De metrische gegevens die u hebt geselecteerd in de Diagnostics bepaalt de resolutie van de metrische gegevens die beschikbaar voor uw account zijn:</span><span class="sxs-lookup"><span data-stu-id="42f13-159">The metrics you selected in Diagnostics determines the resolution of the metrics that are available for your account:</span></span>

* <span data-ttu-id="42f13-160">**Cumulatieve** voorziet in maatstaven zoals inkomend en uitgaand, beschikbaarheid, latentie en geslaagd percentages voor bewaking.</span><span class="sxs-lookup"><span data-stu-id="42f13-160">**Aggregate** monitoring provides metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="42f13-161">Deze metrische gegevens worden van de blob, table, bestand en wachtrijservices samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="42f13-161">These metrics are aggregated from the blob, table, file, and queue services.</span></span>
* <span data-ttu-id="42f13-162">**Per API** biedt betere oplossing met metrische gegevens beschikbaar voor afzonderlijke opslagbewerkingen, naast de serviceniveau-statistische functies.</span><span class="sxs-lookup"><span data-stu-id="42f13-162">**Per API** provides finer resolution, with metrics available for individual storage operations, in addition to the service-level aggregates.</span></span>

## <a name="configure-metrics-alerts"></a><span data-ttu-id="42f13-163">Metrische gegevens waarschuwingen configureren</span><span class="sxs-lookup"><span data-stu-id="42f13-163">Configure metrics alerts</span></span>

<span data-ttu-id="42f13-164">U kunt waarschuwingen om u te waarschuwen wanneer drempels hebt bereikt voor metrische gegevens van storage resource maken.</span><span class="sxs-lookup"><span data-stu-id="42f13-164">You can create alerts to notify you when thresholds have been reached for storage resource metrics.</span></span>

1. <span data-ttu-id="42f13-165">Openen de **waarschuwingsregels blade**, schuif omlaag naar de **bewaking** sectie van de **Menu blade** en selecteer **waarschuwing regels**.</span><span class="sxs-lookup"><span data-stu-id="42f13-165">To open the **Alert rules blade**, scroll down to the **MONITORING** section of the **Menu blade** and select **Alert rules**.</span></span>
1. <span data-ttu-id="42f13-166">Selecteer **waarschuwing toevoegen** openen de **een waarschuwingsregel toevoegen** blade</span><span class="sxs-lookup"><span data-stu-id="42f13-166">Select **Add alert** to open the **Add an alert rule** blade</span></span>
1. <span data-ttu-id="42f13-167">Selecteer een **Resource** (blob, bestand, in de wachtrij, tabel) in de vervolgkeuzelijst en voer een **naam** en **beschrijving** voor uw nieuwe waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="42f13-167">Select a **Resource** (blob, file, queue, table) from the drop-down, and enter a **Name** and **Description** for your new alert rule.</span></span>
1. <span data-ttu-id="42f13-168">Selecteer de **metriek** voor die u wilt een waarschuwing, wordt een waarschuwing toevoegen **voorwaarde**, en een **drempelwaarde**.</span><span class="sxs-lookup"><span data-stu-id="42f13-168">Select the **Metric** for which you'd like to add an alert, an alert **Condition**, and a **Threshold**.</span></span> <span data-ttu-id="42f13-169">De eenheid drempelwaarde Typ wijzigingen, afhankelijk van de metrische gegevens die u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="42f13-169">The threshold unit type changes depending on the metric you've chosen.</span></span> <span data-ttu-id="42f13-170">'Aantal' is bijvoorbeeld het eenheidstype voor *ContainerCount*, terwijl de eenheid voor de *PercentNetworkError* meetwaarde is een percentage.</span><span class="sxs-lookup"><span data-stu-id="42f13-170">For example, "count" is the unit type for *ContainerCount*, while the unit for the *PercentNetworkError* metric is a percentage.</span></span>
1. <span data-ttu-id="42f13-171">Selecteer de **periode**.</span><span class="sxs-lookup"><span data-stu-id="42f13-171">Select the **Period**.</span></span> <span data-ttu-id="42f13-172">Metrische gegevens die bereikt of overschrijdt de drempelwaarde binnen een periode geeft een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="42f13-172">Metrics that reach or exceed the Threshold within the period trigger an alert.</span></span>
1. <span data-ttu-id="42f13-173">(Optioneel) Configureer **e** en **Webhook** meldingen.</span><span class="sxs-lookup"><span data-stu-id="42f13-173">(Optional) Configure **Email** and **Webhook** notifications.</span></span> <span data-ttu-id="42f13-174">Zie voor meer informatie over webhooks [een webhook configureren op een Azure metrische waarschuwing](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="42f13-174">For more information on webhooks, see [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="42f13-175">Als u geen e-mailadres of webhook meldingen configureert, wordt alleen in de Azure portal waarschuwingen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="42f13-175">If you do not configure email or webhook notifications, alerts will appear only in the Azure portal.</span></span>

![Blade 'Een waarschuwingsregel toevoegen' in de Azure portal](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-to-the-portal-dashboard"></a><span data-ttu-id="42f13-177">Metrische gegevens grafieken toevoegen aan het portaldashboard</span><span class="sxs-lookup"><span data-stu-id="42f13-177">Add metrics charts to the portal dashboard</span></span>

<span data-ttu-id="42f13-178">U kunt grafieken van Azure Storage metrische gegevens voor een van uw storage-accounts toevoegen aan uw portal-dashboard.</span><span class="sxs-lookup"><span data-stu-id="42f13-178">You can add Azure Storage metrics charts for any of your storage accounts to your portal dashboard.</span></span>

1. <span data-ttu-id="42f13-179">Selecteer Klik **bewerken dashboard** tijdens het bekijken van het dashboard in de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="42f13-179">Select click **Edit dashboard** while viewing your dashboard in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="42f13-180">In de **tegel galerie**, selecteer **zoeken door tegels** > **Type**.</span><span class="sxs-lookup"><span data-stu-id="42f13-180">In the **Tile Gallery**, select **Find tiles by** > **Type**.</span></span>
1. <span data-ttu-id="42f13-181">Selecteer **Type** > **opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="42f13-181">Select **Type** > **Storage accounts**.</span></span>
1. <span data-ttu-id="42f13-182">In **Resources**, selecteer het opslagaccount waarvan metrische gegevens die u wilt toevoegen aan het dashboard.</span><span class="sxs-lookup"><span data-stu-id="42f13-182">In **Resources**, select the storage account whose metrics you wish to add to the dashboard.</span></span>
1. <span data-ttu-id="42f13-183">Selecteer **categorieën** > **bewaking**.</span><span class="sxs-lookup"><span data-stu-id="42f13-183">Select **Categories** > **Monitoring**.</span></span>
1. <span data-ttu-id="42f13-184">Slepen en neerzetten van de grafiek tegel op uw dashboard voor de metrische gegevens die u wilt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="42f13-184">Drag-and-drop the chart tile onto your dashboard for the metric you'd like displayed.</span></span> <span data-ttu-id="42f13-185">Herhaal van alle metrische gegevens die u wilt weergegeven op het dashboard.</span><span class="sxs-lookup"><span data-stu-id="42f13-185">Repeat for all metrics you'd like displayed on the dashboard.</span></span> <span data-ttu-id="42f13-186">De grafiek 'Blobs - totale aanvragen' is gemarkeerd als voorbeeld in de volgende afbeelding, maar alle grafieken zijn beschikbaar voor plaatsing op uw dashboard.</span><span class="sxs-lookup"><span data-stu-id="42f13-186">In the following image, the "Blobs - Total requests" chart is highlighted as an example, but all the charts are available for placement on your dashboard.</span></span>

   ![Tegel galerie in Azure-portal](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. <span data-ttu-id="42f13-188">Selecteer **gedaan aanpassen** boven aan het dashboard wanneer u grafieken toe te voegen bent klaar.</span><span class="sxs-lookup"><span data-stu-id="42f13-188">Select **Done customizing** near the top of the dashboard when you're done adding charts.</span></span>

<span data-ttu-id="42f13-189">Zodra u grafieken hebt toegevoegd aan uw dashboard, kunt u verder deze aanpassen zoals beschreven in [grafieken van de metrische gegevens aanpassen](#how-to-customize-metrics-charts).</span><span class="sxs-lookup"><span data-stu-id="42f13-189">Once you've added charts to your dashboard, you can further customize them as described in [Customize metrics charts](#how-to-customize-metrics-charts).</span></span>

## <a name="configure-logging"></a><span data-ttu-id="42f13-190">Logboekregistratie configureren</span><span class="sxs-lookup"><span data-stu-id="42f13-190">Configure logging</span></span>

<span data-ttu-id="42f13-191">U kunt opgeven dat Azure Storage Sla de logboeken van de diagnostische gegevens voor lezen, schrijven en aanvragen voor de blob, table en queue-services verwijderen.</span><span class="sxs-lookup"><span data-stu-id="42f13-191">You can instruct Azure Storage to save diagnostics logs for read, write, and delete requests for the blob, table, and queue services.</span></span> <span data-ttu-id="42f13-192">Het bewaarbeleid voor gegevens u geldt ook voor deze logboeken.</span><span class="sxs-lookup"><span data-stu-id="42f13-192">The data retention policy you set also applies to these logs.</span></span>

> [!NOTE]
> <span data-ttu-id="42f13-193">Azure File storage momenteel ondersteunt Opslaganalyse metrische gegevens, maar logboekregistratie nog niet ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="42f13-193">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>

1. <span data-ttu-id="42f13-194">In de [Azure-portal](https://portal.azure.com), selecteer **opslagaccounts**, klikt u vervolgens de naam van het storage-account openen van de blade opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="42f13-194">In the [Azure portal](https://portal.azure.com), select **Storage accounts**, then the name of the storage account to open the storage account blade.</span></span>
1. <span data-ttu-id="42f13-195">Selecteer **Diagnostics** in de **bewaking** sectie van de blade menu.</span><span class="sxs-lookup"><span data-stu-id="42f13-195">Select **Diagnostics** in the **MONITORING** section of the menu blade.</span></span>

    ![Diagnostische gegevens menu-item onder controle in de Azure portal.](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. <span data-ttu-id="42f13-197">Zorg ervoor dat **Status** is ingesteld op **op**, en selecteer de **services** voor die u wilt inschakelen van logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="42f13-197">Ensure **Status** is set to **On**, and select the **services** for which you'd like to enable logging.</span></span>

    ![Logboekregistratie in de Azure portal configureren.](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. <span data-ttu-id="42f13-199">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="42f13-199">Click **Save**.</span></span>

<span data-ttu-id="42f13-200">De logboeken met diagnostische gegevens worden opgeslagen in een blob-container met de naam $logs in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="42f13-200">The diagnostics logs are saved in a blob container named $logs in your storage account.</span></span> <span data-ttu-id="42f13-201">U kunt de logboekgegevens met een Opslagverkenner zoals weergeven de [Microsoft Opslagverkenner](http://storageexplorer.com), of programmatisch met behulp van de storage-clientbibliotheek of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="42f13-201">You can view the log data using a storage explorer like the [Microsoft Storage Explorer](http://storageexplorer.com), or programmatically using the storage client library or PowerShell.</span></span>

<span data-ttu-id="42f13-202">Zie voor meer informatie over het openen van de container $logs [opslag vastleggen inschakelen en toegang tot logboekgegevens](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).</span><span class="sxs-lookup"><span data-stu-id="42f13-202">For information about accessing the $logs container, see [Enabling Storage Logging and Accessing Log Data](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).</span></span>

## <a name="next-steps"></a><span data-ttu-id="42f13-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="42f13-203">Next steps</span></span>

* <span data-ttu-id="42f13-204">Meer informatie vinden over [metrische gegevens en de registratie en facturering](storage-analytics.md) voor Storage Analytics.</span><span class="sxs-lookup"><span data-stu-id="42f13-204">Find more details about [metrics, logging, and billing](storage-analytics.md) for Storage Analytics.</span></span>
* <span data-ttu-id="42f13-205">[Inschakelen van Azure Storage metrische gegevens en bekijk metrische gegevens](storage-enable-and-view-metrics.md) met behulp van PowerShell en programmatisch met C#.</span><span class="sxs-lookup"><span data-stu-id="42f13-205">[Enable Azure Storage metrics and view metrics data](storage-enable-and-view-metrics.md) by using PowerShell and programmatically with C#.</span></span>

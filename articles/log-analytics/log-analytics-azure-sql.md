---
title: Azure SQL Analytics-oplossing in Log Analytics | Microsoft Docs
description: De Azure SQL Analytics-oplossing kunt u uw Azure SQL-databases beheren.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: cab45cc6dd621eb4a95ef5f1842ec38c25e980b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a><span data-ttu-id="63675-103">Azure SQL Database met behulp van Azure SQL Analytics (Preview) in logboekanalyse bewaken</span><span class="sxs-lookup"><span data-stu-id="63675-103">Monitor Azure SQL Database using Azure SQL Analytics (Preview) in Log Analytics</span></span>

![Azure SQL Analytics symbool](./media/log-analytics-azure-sql/azure-sql-symbol.png)

<span data-ttu-id="63675-105">De Azure SQL Analytics-oplossing in Azure-logboekanalyse verzamelt en visualiseren van belangrijke maatstaven voor prestaties van SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="63675-105">The Azure SQL Analytics solution in Azure Log Analytics collects and visualizes important SQL Azure performance metrics.</span></span> <span data-ttu-id="63675-106">Met behulp van de metrische gegevens die u verzamelt van de oplossing, kunt u aangepaste regels voor bewaking en waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="63675-106">By using the metrics that you collect with the solution, you can create custom monitoring rules and alerts.</span></span> <span data-ttu-id="63675-107">U kunt Azure SQL Database bewaken en elastische pool metrische gegevens op meerdere Azure-abonnementen en elastische pools en ze visualiseren.</span><span class="sxs-lookup"><span data-stu-id="63675-107">And, you can monitor Azure SQL Database and elastic pool metrics across multiple Azure subscriptions and elastic pools and visualize them.</span></span> <span data-ttu-id="63675-108">De oplossing helpt u problemen bij elke laag van uw toepassing stack kunt identificeren.</span><span class="sxs-lookup"><span data-stu-id="63675-108">The solution also helps you to identify issues at each layer of your application stack.</span></span>  <span data-ttu-id="63675-109">Hierbij [diagnostische Azure metrische gegevens](log-analytics-azure-storage.md) samen met logboekanalyse weergaven om gegevens over uw Azure SQL-databases en elastische pools in een enkel Log Analytics-werkruimte te presenteren.</span><span class="sxs-lookup"><span data-stu-id="63675-109">It uses [Azure Diagnostic metrics](log-analytics-azure-storage.md) together with Log Analytics views to present data about all your Azure SQL databases and elastic pools in a single Log Analytics workspace.</span></span>

<span data-ttu-id="63675-110">Deze preview-oplossing ondersteunt momenteel maximaal 150.000 Azure SQL-Databases en 5000 SQL elastische Pools per werkruimte.</span><span class="sxs-lookup"><span data-stu-id="63675-110">Currently, this preview solution supports up to 150,000 Azure SQL Databases and 5,000 SQL Elastic Pools per workspace.</span></span>

<span data-ttu-id="63675-111">De Azure SQL Analytics-oplossing, net zoals andere beschikbaar voor logboekanalyse, kunt u controleren en meldingen ontvangen over de status van uw Azure-resources: in dit geval, Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="63675-111">The Azure SQL Analytics solution, like others available for Log Analytics, helps you monitor and receive notifications about the health of your Azure resources—in this case, Azure SQL Database.</span></span> <span data-ttu-id="63675-112">Microsoft Azure SQL Database is een schaalbare relationele database-service die bekende SQL-Server-achtige mogelijkheden voor toepassingen die worden uitgevoerd in de Azure-cloud biedt.</span><span class="sxs-lookup"><span data-stu-id="63675-112">Microsoft Azure SQL Database is a scalable relational database service that provides familiar SQL-Server-like capabilities to applications running in the Azure cloud.</span></span> <span data-ttu-id="63675-113">Log Analytics, helpt u bij het verzamelen, correleren en gestructureerde en ongestructureerde gegevens visualiseren.</span><span class="sxs-lookup"><span data-stu-id="63675-113">Log Analytics helps you to collect, correlate, and visualize structured and unstructured data.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="63675-114">Verbonden bronnen</span><span class="sxs-lookup"><span data-stu-id="63675-114">Connected sources</span></span>

<span data-ttu-id="63675-115">De Azure SQL Analytics-oplossing gebruikt niet agents verbinding maken met de Log Analytics-service.</span><span class="sxs-lookup"><span data-stu-id="63675-115">The Azure SQL Analytics solution doesn't use agents to connect to the Log Analytics service.</span></span>

<span data-ttu-id="63675-116">De volgende tabel beschrijft de verbonden bronnen die worden ondersteund door deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="63675-116">The following table describes the connected sources that are supported by this solution.</span></span>

| <span data-ttu-id="63675-117">Verbonden bron</span><span class="sxs-lookup"><span data-stu-id="63675-117">Connected Source</span></span> | <span data-ttu-id="63675-118">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="63675-118">Support</span></span> | <span data-ttu-id="63675-119">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="63675-119">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="63675-120">Windows-agents</span><span class="sxs-lookup"><span data-stu-id="63675-120">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="63675-121">Nee</span><span class="sxs-lookup"><span data-stu-id="63675-121">No</span></span> | <span data-ttu-id="63675-122">Directe Windows-agents worden niet gebruikt door de oplossing.</span><span class="sxs-lookup"><span data-stu-id="63675-122">Direct Windows agents are not used by the solution.</span></span> |
| [<span data-ttu-id="63675-123">Linux-agents</span><span class="sxs-lookup"><span data-stu-id="63675-123">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="63675-124">Nee</span><span class="sxs-lookup"><span data-stu-id="63675-124">No</span></span> | <span data-ttu-id="63675-125">Directe Linux-agents worden niet gebruikt door de oplossing.</span><span class="sxs-lookup"><span data-stu-id="63675-125">Direct Linux agents are not used by the solution.</span></span> |
| [<span data-ttu-id="63675-126">SCOM-beheergroep</span><span class="sxs-lookup"><span data-stu-id="63675-126">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="63675-127">Nee</span><span class="sxs-lookup"><span data-stu-id="63675-127">No</span></span> | <span data-ttu-id="63675-128">Een rechtstreekse verbinding tussen de SCOM-agents met logboekanalyse wordt niet gebruikt door de oplossing.</span><span class="sxs-lookup"><span data-stu-id="63675-128">A direct connection from the SCOM agent to Log Analytics is not used by the solution.</span></span> |
| [<span data-ttu-id="63675-129">Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="63675-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="63675-130">Nee</span><span class="sxs-lookup"><span data-stu-id="63675-130">No</span></span> | <span data-ttu-id="63675-131">Log Analytics biedt de gegevens niet lezen uit een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="63675-131">Log Analytics does not read the data from a storage account.</span></span> |
| [<span data-ttu-id="63675-132">Azure diagnostics</span><span class="sxs-lookup"><span data-stu-id="63675-132">Azure diagnostics</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="63675-133">Ja</span><span class="sxs-lookup"><span data-stu-id="63675-133">Yes</span></span> | <span data-ttu-id="63675-134">Azure metrische gegevens worden verzonden met logboekanalyse rechtstreeks door Azure.</span><span class="sxs-lookup"><span data-stu-id="63675-134">Azure metric data is sent to Log Analytics directly by Azure.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="63675-135">Vereisten</span><span class="sxs-lookup"><span data-stu-id="63675-135">Prerequisites</span></span>

- <span data-ttu-id="63675-136">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="63675-136">An Azure Subscription.</span></span> <span data-ttu-id="63675-137">Als u niet hebt, kunt u één voor [gratis](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="63675-137">If you don't have one, you can create one for [free](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="63675-138">Een werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="63675-138">A Log Analytics workspace.</span></span> <span data-ttu-id="63675-139">U kunt een bestaande of kunt u [Maak een nieuwe](log-analytics-get-started.md) voordat u begint met behulp van deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="63675-139">You can use an existing one, or you can [create a new one](log-analytics-get-started.md) before you start using this solution.</span></span>
- <span data-ttu-id="63675-140">Azure Diagnostics inschakelen voor uw Azure SQL-databases en elastische pools en [configureren zodat ze hun gegevens verzenden naar logboekanalyse](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="63675-140">Enable Azure Diagnostics for your Azure SQL databases and elastic pools and [configure them to send their data to Log Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span>

## <a name="configuration"></a><span data-ttu-id="63675-141">Configuratie</span><span class="sxs-lookup"><span data-stu-id="63675-141">Configuration</span></span>

<span data-ttu-id="63675-142">Voer de volgende stappen uit om toe te voegen van de Azure SQL Analytics-oplossing naar de werkruimte.</span><span class="sxs-lookup"><span data-stu-id="63675-142">Perform the following steps to add the Azure SQL Analytics solution to your workspace.</span></span>

1. <span data-ttu-id="63675-143">De Azure SQL Analytics-oplossing toevoegen aan uw werkruimte van [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) of met behulp van de procedure beschreven in [toevoegen Log Analytics-oplossingen van de galerie met oplossingen](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="63675-143">Add the Azure SQL Analytics solution to your workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="63675-144">Klik in de Azure-portal op **nieuw** (het symbool +), selecteer vervolgens in de lijst met resources **bewaking + Management**.</span><span class="sxs-lookup"><span data-stu-id="63675-144">In the Azure portal, click **New** (the + symbol), then in the list of resources, select **Monitoring + Management**.</span></span>  
    <span data-ttu-id="63675-145">![Controle en beheer](./media/log-analytics-azure-sql/monitoring-management.png)</span><span class="sxs-lookup"><span data-stu-id="63675-145">![Monitoring + Management](./media/log-analytics-azure-sql/monitoring-management.png)</span></span>
3. <span data-ttu-id="63675-146">In de **bewaking + Management** Klik **alle**.</span><span class="sxs-lookup"><span data-stu-id="63675-146">In the **Monitoring + Management** list click **See all**.</span></span>
4. <span data-ttu-id="63675-147">In de **aanbevolen** lijst, klikt u op **meer** , en klik vervolgens in de nieuwe lijst vinden **Azure SQL Analytics (Preview)** en selecteert u vervolgens.</span><span class="sxs-lookup"><span data-stu-id="63675-147">In the **Recommended** list, click **More** , and then in the new list, find **Azure SQL Analytics (Preview)** and then select it.</span></span>  
    <span data-ttu-id="63675-148">![Azure SQL Analytics-oplossing](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span><span class="sxs-lookup"><span data-stu-id="63675-148">![Azure SQL Analytics solution](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span></span>
5. <span data-ttu-id="63675-149">In de **Azure SQL Analytics (Preview)** blade, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="63675-149">In the **Azure SQL Analytics (Preview)** blade, click **Create**.</span></span>  
    <span data-ttu-id="63675-150">![Maken](./media/log-analytics-azure-sql/portal-create.png)</span><span class="sxs-lookup"><span data-stu-id="63675-150">![Create](./media/log-analytics-azure-sql/portal-create.png)</span></span>
6. <span data-ttu-id="63675-151">In de **nieuwe oplossing maken** blade, selecteer de werkruimte die u wilt toevoegen, de oplossing en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="63675-151">In the **Create new solution** blade, select the workspace that you want to add the solution to and then click **Create**.</span></span>  
    <span data-ttu-id="63675-152">![toevoegen aan werkruimte](./media/log-analytics-azure-sql/add-to-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="63675-152">![add to workspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span></span>


### <a name="to-configure-multiple-azure-subscriptions"></a><span data-ttu-id="63675-153">Voor het configureren van meerdere Azure-abonnementen</span><span class="sxs-lookup"><span data-stu-id="63675-153">To configure multiple Azure subscriptions</span></span>

<span data-ttu-id="63675-154">Gebruik de PowerShell-script uit ter ondersteuning van meerdere abonnementen [inschakelen Azure resource metrische gegevens logboekregistratie met behulp van PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="63675-154">To support multiple subscriptions, use the PowerShell script from [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span> <span data-ttu-id="63675-155">Geef de werkruimte-ID als parameter bij het uitvoeren van het script voor het verzenden van diagnostische gegevens van resources in een Azure-abonnement met een werkruimte in een andere Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="63675-155">Provide the workspace resource ID as a parameter when executing the script to send diagnostic data from resources in one Azure subscription to a workspace in another Azure subscription.</span></span>

<span data-ttu-id="63675-156">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="63675-156">**Example**</span></span>

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-the-solution"></a><span data-ttu-id="63675-157">De oplossing gebruiken</span><span class="sxs-lookup"><span data-stu-id="63675-157">Using the solution</span></span>

<span data-ttu-id="63675-158">Wanneer u de oplossing voor uw werkruimte toevoegt, is de tegel Azure SQL Analytics toegevoegd aan uw werkruimte en wordt deze weergegeven in het overzicht.</span><span class="sxs-lookup"><span data-stu-id="63675-158">When you add the solution to your workspace, the Azure SQL Analytics tile is added to your workspace, and it appears in Overview.</span></span> <span data-ttu-id="63675-159">De tegel toont het aantal Azure SQL-databases en elastische pools SQL Azure die de oplossing is verbonden met.</span><span class="sxs-lookup"><span data-stu-id="63675-159">The tile shows the number of Azure SQL databases and Azure SQL elastic pools that the solution is connected to.</span></span>

![Azure SQL-Analytics tegel](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a><span data-ttu-id="63675-161">Azure SQL analytische gegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="63675-161">Viewing Azure SQL Analytics data</span></span>

<span data-ttu-id="63675-162">Klik op de **Azure SQL Analytics** tegel om de Azure SQL Analytics dashboard te openen.</span><span class="sxs-lookup"><span data-stu-id="63675-162">Click on the **Azure SQL Analytics** tile to open the Azure SQL Analytics dashboard.</span></span> <span data-ttu-id="63675-163">Het dashboard bevat de blades zoals hieronder gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="63675-163">The dashboard includes the blades defined below.</span></span> <span data-ttu-id="63675-164">Elke blade bevat maximaal 15 bronnen (abonnement, server elastische pool en database).</span><span class="sxs-lookup"><span data-stu-id="63675-164">Each blade lists up to 15 resources (subscription, server, elastic pool, and database).</span></span> <span data-ttu-id="63675-165">Klik op de bronnen om het dashboard voor die specifieke bron te openen.</span><span class="sxs-lookup"><span data-stu-id="63675-165">Click any of the resources to open the dashboard for that specific resource.</span></span> <span data-ttu-id="63675-166">Elastische Pool of Database bevat de grafieken met metrische gegevens voor een geselecteerde bron.</span><span class="sxs-lookup"><span data-stu-id="63675-166">Elastic Pool or Database contains the charts with metrics for a selected resource.</span></span> <span data-ttu-id="63675-167">Klik op een grafiek om te openen van het dialoogvenster logboek zoeken.</span><span class="sxs-lookup"><span data-stu-id="63675-167">Click a chart to open the Log Search dialog.</span></span>

| <span data-ttu-id="63675-168">Blade</span><span class="sxs-lookup"><span data-stu-id="63675-168">Blade</span></span> | <span data-ttu-id="63675-169">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="63675-169">Description</span></span> |
|---|---|
| <span data-ttu-id="63675-170">Abonnementen</span><span class="sxs-lookup"><span data-stu-id="63675-170">Subscriptions</span></span> | <span data-ttu-id="63675-171">Lijst met abonnementen met het aantal gekoppelde servers, -adresgroepen en -databases.</span><span class="sxs-lookup"><span data-stu-id="63675-171">List of subscriptions with number of connected servers, pools, and databases.</span></span> |
| <span data-ttu-id="63675-172">Servers</span><span class="sxs-lookup"><span data-stu-id="63675-172">Servers</span></span> | <span data-ttu-id="63675-173">Lijst met servers met een aantal van de verbonden groepen en databases.</span><span class="sxs-lookup"><span data-stu-id="63675-173">List of servers with number of connected pools and databases.</span></span> |
| <span data-ttu-id="63675-174">Elastische pools</span><span class="sxs-lookup"><span data-stu-id="63675-174">Elastic Pools</span></span> | <span data-ttu-id="63675-175">Lijst met verbonden elastische pools met maximale GB en eDTU in de gecontroleerde periode.</span><span class="sxs-lookup"><span data-stu-id="63675-175">List of connected elastic pools with maximum GB and eDTU in the observed period.</span></span> |
|<span data-ttu-id="63675-176">Databases</span><span class="sxs-lookup"><span data-stu-id="63675-176">Databases</span></span> | <span data-ttu-id="63675-177">Lijst met verbonden databases met een maximale GB en DTU in de gecontroleerde periode.</span><span class="sxs-lookup"><span data-stu-id="63675-177">List of connected databases with maximum GB and DTU in the observed period.</span></span>|


### <a name="analyze-data-and-create-alerts"></a><span data-ttu-id="63675-178">Gegevens analyseren en waarschuwingen maken</span><span class="sxs-lookup"><span data-stu-id="63675-178">Analyze data and create alerts</span></span>

<span data-ttu-id="63675-179">U kunt eenvoudig waarschuwingen maken met de gegevens die afkomstig zijn van Azure SQL Database-resources.</span><span class="sxs-lookup"><span data-stu-id="63675-179">You can easily create alerts with the data coming from Azure SQL Database resources.</span></span> <span data-ttu-id="63675-180">Hier volgen enkele nuttige [logboek zoeken](log-analytics-log-searches.md) query's die u voor waarschuwingen gebruiken kunt:</span><span class="sxs-lookup"><span data-stu-id="63675-180">Here are a couple of useful [log search](log-analytics-log-searches.md) queries that you can use for alerting:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


<span data-ttu-id="63675-181">*Hoge DTU voor Azure SQL Database*</span><span class="sxs-lookup"><span data-stu-id="63675-181">*High DTU on Azure SQL Database*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="63675-182">*Hoge DTU op elastische Pool in Azure SQL Database*</span><span class="sxs-lookup"><span data-stu-id="63675-182">*High DTU on Azure SQL Database Elastic Pool*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="63675-183">U kunt deze waarschuwing-query's gebruiken om te attenderen op specifieke drempelwaarden voor Azure SQL Database en elastische pools.</span><span class="sxs-lookup"><span data-stu-id="63675-183">You can use these alert-based queries to alert on specific thresholds for both Azure SQL Database and elastic pools.</span></span> <span data-ttu-id="63675-184">Voor het configureren van een waarschuwing voor de OMS-werkruimte:</span><span class="sxs-lookup"><span data-stu-id="63675-184">To configure an alert for your OMS workspace:</span></span>

#### <a name="to-configure-an-alert-for-your-workspace"></a><span data-ttu-id="63675-185">Een waarschuwing voor uw werkruimte configureren</span><span class="sxs-lookup"><span data-stu-id="63675-185">To configure an alert for your workspace</span></span>

1. <span data-ttu-id="63675-186">Ga naar de [OMS-portal](http://mms.microsoft.com/) en meld u aan.</span><span class="sxs-lookup"><span data-stu-id="63675-186">Go to the [OMS portal](http://mms.microsoft.com/) and sign in.</span></span>
2. <span data-ttu-id="63675-187">Open de werkruimte die u hebt geconfigureerd voor de oplossing.</span><span class="sxs-lookup"><span data-stu-id="63675-187">Open the workspace that you have configured for the solution.</span></span>
3. <span data-ttu-id="63675-188">Klik op de pagina overzicht de **Azure SQL Analytics (Preview)** tegel.</span><span class="sxs-lookup"><span data-stu-id="63675-188">On the Overview page, click the **Azure SQL Analytics (Preview)** tile.</span></span>
4. <span data-ttu-id="63675-189">Voer een van de voorbeelden van query's.</span><span class="sxs-lookup"><span data-stu-id="63675-189">Run one of the example queries.</span></span>
5. <span data-ttu-id="63675-190">In logboek zoekopdracht, klikt u op **waarschuwing**.</span><span class="sxs-lookup"><span data-stu-id="63675-190">In Log Search, click **Alert**.</span></span>  
<span data-ttu-id="63675-191">![waarschuwing in de zoekopdracht maken](./media/log-analytics-azure-sql/create-alert01.png)</span><span class="sxs-lookup"><span data-stu-id="63675-191">![create alert in search](./media/log-analytics-azure-sql/create-alert01.png)</span></span>
6. <span data-ttu-id="63675-192">Op de **waarschuwingsregel toevoegen** pagina, configureert de toepasselijke eigenschappen en de specifieke drempelwaarden die u wilt en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="63675-192">On the **Add Alert Rule** page, configure the appropriate properties and the specific thresholds that you want and then click **Save**.</span></span>  
<span data-ttu-id="63675-193">![toevoegen van waarschuwingsregel](./media/log-analytics-azure-sql/create-alert02.png)</span><span class="sxs-lookup"><span data-stu-id="63675-193">![add alert rule](./media/log-analytics-azure-sql/create-alert02.png)</span></span>

### <a name="act-on-azure-sql-analytics-data"></a><span data-ttu-id="63675-194">Reageren op Azure SQL analytische gegevens</span><span class="sxs-lookup"><span data-stu-id="63675-194">Act on Azure SQL Analytics data</span></span>

<span data-ttu-id="63675-195">Een van de handigste query's die u kunt uitvoeren is bijvoorbeeld het DTU-gebruik voor alle Azure SQL elastische Pools van alle Azure-abonnement met elkaar vergelijken.</span><span class="sxs-lookup"><span data-stu-id="63675-195">As an example, one of the most useful queries that you can perform is to compare the DTU utilization for all Azure SQL Elastic Pools across all your Azure subscriptions.</span></span> <span data-ttu-id="63675-196">Doorvoer DTU (database Unit) biedt een manier om te beschrijven de relatieve capaciteit van een prestatieniveau van Basic, Standard en Premium-databases en pools.</span><span class="sxs-lookup"><span data-stu-id="63675-196">Database Throughput Unit (DTU) provides a way to describe the relative capacity of a performance level of Basic, Standard, and Premium databases and pools.</span></span> <span data-ttu-id="63675-197">Dtu's zijn gebaseerd op een gecombineerde meting van CPU, geheugen, leest en schrijft.</span><span class="sxs-lookup"><span data-stu-id="63675-197">DTUs are based on a blended measure of CPU, memory, reads, and writes.</span></span> <span data-ttu-id="63675-198">Als het aantal dtu's verhoogt, verhoogt de macht die worden aangeboden door het prestatieniveau.</span><span class="sxs-lookup"><span data-stu-id="63675-198">As DTUs increase, the power offered by the performance level increases.</span></span> <span data-ttu-id="63675-199">Bijvoorbeeld, heeft een prestatieniveau met 5 dtu's vijf keer krachtiger dan een prestatieniveau met 1 DTU.</span><span class="sxs-lookup"><span data-stu-id="63675-199">For example, a performance level with 5 DTUs has five times more power than a performance level with 1 DTU.</span></span> <span data-ttu-id="63675-200">Maximale DTU-quotum geldt voor elke server en de elastische groep.</span><span class="sxs-lookup"><span data-stu-id="63675-200">A maximum DTU quota applies to each server and elastic pool.</span></span>

<span data-ttu-id="63675-201">Door de volgende logboek-zoekopdracht wordt uitgevoerd, kunt u eenvoudig zien als u bepaalde zijn of over het gebruik van uw SQL Azure elastische pools.</span><span class="sxs-lookup"><span data-stu-id="63675-201">By running the following Log Search query, you can easily tell if you are underutilizing or over utilizing your SQL Azure elastic pools.</span></span>

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> <span data-ttu-id="63675-202">Als uw werkruimte is bijgewerkt naar de [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), en vervolgens de bovenstaande query zou Wijzig in het volgende.</span><span class="sxs-lookup"><span data-stu-id="63675-202">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

<span data-ttu-id="63675-203">In het volgende voorbeeld ziet u dat een elastische groep een hoog gebruik in de buurt van 100 heeft % DTU weinig gebruik zijn.</span><span class="sxs-lookup"><span data-stu-id="63675-203">In the following example, you can see that one elastic pool has a high usage near 100% DTU while others have very little usage.</span></span> <span data-ttu-id="63675-204">U kunt verder onderzoeken om op te lossen potentiële recente wijzigingen in uw omgeving met Logboeken van de Azure-activiteit.</span><span class="sxs-lookup"><span data-stu-id="63675-204">You can investigate further to troubleshoot potential recent changes in your environment using Azure Activity logs.</span></span>

![Zoekresultaten voor logboek - hoog gebruik](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a><span data-ttu-id="63675-206">Zie ook</span><span class="sxs-lookup"><span data-stu-id="63675-206">See also</span></span>

- <span data-ttu-id="63675-207">Gebruik [logboek zoekopdrachten](log-analytics-log-searches.md) in Log Analytics om gedetailleerde Azure SQL-gegevens te bekijken.</span><span class="sxs-lookup"><span data-stu-id="63675-207">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics to view detailed Azure SQL data.</span></span>
- <span data-ttu-id="63675-208">[Maak uw eigen dashboards](log-analytics-dashboards.md) Azure SQL-gegevens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="63675-208">[Create your own dashboards](log-analytics-dashboards.md) showing Azure SQL data.</span></span>
- <span data-ttu-id="63675-209">[Waarschuwingen maken](log-analytics-alerts.md) wanneer specifieke Azure SQL-gebeurtenissen plaatsvinden.</span><span class="sxs-lookup"><span data-stu-id="63675-209">[Create alerts](log-analytics-alerts.md) when specific Azure SQL events occur.</span></span>

---
title: aaaAzure SQL Analytics-oplossing in Log Analytics | Microsoft Docs
description: Hello Azure SQL Analytics-oplossing kunt u uw Azure SQL-databases beheren.
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
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a><span data-ttu-id="0b487-103">Azure SQL Database met behulp van Azure SQL Analytics (Preview) in logboekanalyse bewaken</span><span class="sxs-lookup"><span data-stu-id="0b487-103">Monitor Azure SQL Database using Azure SQL Analytics (Preview) in Log Analytics</span></span>

![Azure SQL Analytics symbool](./media/log-analytics-azure-sql/azure-sql-symbol.png)

<span data-ttu-id="0b487-105">Hello Azure SQL Analytics-oplossing in Azure-logboekanalyse verzamelt en visualiseren van belangrijke maatstaven voor prestaties van SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0b487-105">hello Azure SQL Analytics solution in Azure Log Analytics collects and visualizes important SQL Azure performance metrics.</span></span> <span data-ttu-id="0b487-106">Hallo metrische gegevens die u verzamelt met Hallo oplossing gebruikt, kunt u aangepaste regels voor bewaking en waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="0b487-106">By using hello metrics that you collect with hello solution, you can create custom monitoring rules and alerts.</span></span> <span data-ttu-id="0b487-107">U kunt Azure SQL Database bewaken en elastische pool metrische gegevens op meerdere Azure-abonnementen en elastische pools en ze visualiseren.</span><span class="sxs-lookup"><span data-stu-id="0b487-107">And, you can monitor Azure SQL Database and elastic pool metrics across multiple Azure subscriptions and elastic pools and visualize them.</span></span> <span data-ttu-id="0b487-108">Hallo-oplossing kunt u ook tooidentify problemen bij elke laag van de stack van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="0b487-108">hello solution also helps you tooidentify issues at each layer of your application stack.</span></span>  <span data-ttu-id="0b487-109">Hierbij [diagnostische Azure metrische gegevens](log-analytics-azure-storage.md) samen met logboekanalyse toopresent gegevens over uw Azure SQL-databases en elastische pools-weergaven in een enkel werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="0b487-109">It uses [Azure Diagnostic metrics](log-analytics-azure-storage.md) together with Log Analytics views toopresent data about all your Azure SQL databases and elastic pools in a single Log Analytics workspace.</span></span>

<span data-ttu-id="0b487-110">Deze preview-oplossing ondersteunt momenteel tot too150, 000 Azure SQL-Databases en 5000 SQL elastische Pools per werkruimte.</span><span class="sxs-lookup"><span data-stu-id="0b487-110">Currently, this preview solution supports up too150,000 Azure SQL Databases and 5,000 SQL Elastic Pools per workspace.</span></span>

<span data-ttu-id="0b487-111">Hello Azure SQL Analytics-oplossing, net zoals andere beschikbaar voor logboekanalyse, kunt u controleren en meldingen ontvangen over Hallo status van uw Azure-resources: in dit geval, Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0b487-111">hello Azure SQL Analytics solution, like others available for Log Analytics, helps you monitor and receive notifications about hello health of your Azure resources—in this case, Azure SQL Database.</span></span> <span data-ttu-id="0b487-112">Microsoft Azure SQL Database is een schaalbare relationele database-service waarmee bekende SQL-Server-achtige mogelijkheden tooapplications uitgevoerd in hello Azure-cloud.</span><span class="sxs-lookup"><span data-stu-id="0b487-112">Microsoft Azure SQL Database is a scalable relational database service that provides familiar SQL-Server-like capabilities tooapplications running in hello Azure cloud.</span></span> <span data-ttu-id="0b487-113">Log Analytics kunt u toocollect, correleren en gestructureerde en ongestructureerde gegevens visualiseren.</span><span class="sxs-lookup"><span data-stu-id="0b487-113">Log Analytics helps you toocollect, correlate, and visualize structured and unstructured data.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="0b487-114">Verbonden bronnen</span><span class="sxs-lookup"><span data-stu-id="0b487-114">Connected sources</span></span>

<span data-ttu-id="0b487-115">Hello Azure SQL Analytics-oplossing gebruik geen maakt van agents tooconnect toohello Log Analytics-service.</span><span class="sxs-lookup"><span data-stu-id="0b487-115">hello Azure SQL Analytics solution doesn't use agents tooconnect toohello Log Analytics service.</span></span>

<span data-ttu-id="0b487-116">Hallo volgende tabel beschrijft Hallo verbonden gegevensbronnen die worden ondersteund door deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="0b487-116">hello following table describes hello connected sources that are supported by this solution.</span></span>

| <span data-ttu-id="0b487-117">Verbonden bron</span><span class="sxs-lookup"><span data-stu-id="0b487-117">Connected Source</span></span> | <span data-ttu-id="0b487-118">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="0b487-118">Support</span></span> | <span data-ttu-id="0b487-119">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0b487-119">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="0b487-120">Windows-agents</span><span class="sxs-lookup"><span data-stu-id="0b487-120">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="0b487-121">Nee</span><span class="sxs-lookup"><span data-stu-id="0b487-121">No</span></span> | <span data-ttu-id="0b487-122">Directe Windows-agents worden niet gebruikt door Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="0b487-122">Direct Windows agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="0b487-123">Linux-agents</span><span class="sxs-lookup"><span data-stu-id="0b487-123">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="0b487-124">Nee</span><span class="sxs-lookup"><span data-stu-id="0b487-124">No</span></span> | <span data-ttu-id="0b487-125">Directe Linux-agents worden niet gebruikt door Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="0b487-125">Direct Linux agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="0b487-126">SCOM-beheergroep</span><span class="sxs-lookup"><span data-stu-id="0b487-126">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="0b487-127">Nee</span><span class="sxs-lookup"><span data-stu-id="0b487-127">No</span></span> | <span data-ttu-id="0b487-128">Een rechtstreekse verbinding tussen Hallo SCOM agent tooLog Analytics wordt niet gebruikt door Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="0b487-128">A direct connection from hello SCOM agent tooLog Analytics is not used by hello solution.</span></span> |
| [<span data-ttu-id="0b487-129">Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="0b487-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="0b487-130">Nee</span><span class="sxs-lookup"><span data-stu-id="0b487-130">No</span></span> | <span data-ttu-id="0b487-131">Log Analytics biedt Hallo gegevens niet lezen uit een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="0b487-131">Log Analytics does not read hello data from a storage account.</span></span> |
| [<span data-ttu-id="0b487-132">Azure diagnostics</span><span class="sxs-lookup"><span data-stu-id="0b487-132">Azure diagnostics</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="0b487-133">Ja</span><span class="sxs-lookup"><span data-stu-id="0b487-133">Yes</span></span> | <span data-ttu-id="0b487-134">Azure metrische gegevens verzonden tooLog Analytics rechtstreeks door Azure.</span><span class="sxs-lookup"><span data-stu-id="0b487-134">Azure metric data is sent tooLog Analytics directly by Azure.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="0b487-135">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0b487-135">Prerequisites</span></span>

- <span data-ttu-id="0b487-136">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0b487-136">An Azure Subscription.</span></span> <span data-ttu-id="0b487-137">Als u niet hebt, kunt u één voor [gratis](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="0b487-137">If you don't have one, you can create one for [free](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="0b487-138">Een werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="0b487-138">A Log Analytics workspace.</span></span> <span data-ttu-id="0b487-139">U kunt een bestaande of kunt u [Maak een nieuwe](log-analytics-get-started.md) voordat u begint met behulp van deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="0b487-139">You can use an existing one, or you can [create a new one](log-analytics-get-started.md) before you start using this solution.</span></span>
- <span data-ttu-id="0b487-140">Azure Diagnostics inschakelen voor uw Azure SQL-databases en elastische pools en [configureren zodat deze toosend hun gegevens tooLog Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="0b487-140">Enable Azure Diagnostics for your Azure SQL databases and elastic pools and [configure them toosend their data tooLog Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span>

## <a name="configuration"></a><span data-ttu-id="0b487-141">Configuratie</span><span class="sxs-lookup"><span data-stu-id="0b487-141">Configuration</span></span>

<span data-ttu-id="0b487-142">Volgende stappen tooadd hello Azure SQL Analytics-oplossing tooyour werkruimte Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0b487-142">Perform hello following steps tooadd hello Azure SQL Analytics solution tooyour workspace.</span></span>

1. <span data-ttu-id="0b487-143">Hello Azure SQL Analytics-oplossing tooyour werkruimte van toevoegen [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) of met behulp van Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="0b487-143">Add hello Azure SQL Analytics solution tooyour workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="0b487-144">In hello Azure-portal, klikt u op **nieuw** (Hallo + symbool), selecteer vervolgens in lijst met resources Hallo **bewaking + Management**.</span><span class="sxs-lookup"><span data-stu-id="0b487-144">In hello Azure portal, click **New** (hello + symbol), then in hello list of resources, select **Monitoring + Management**.</span></span>  
    <span data-ttu-id="0b487-145">![Controle en beheer](./media/log-analytics-azure-sql/monitoring-management.png)</span><span class="sxs-lookup"><span data-stu-id="0b487-145">![Monitoring + Management](./media/log-analytics-azure-sql/monitoring-management.png)</span></span>
3. <span data-ttu-id="0b487-146">In Hallo **bewaking + Management** Klik **alle**.</span><span class="sxs-lookup"><span data-stu-id="0b487-146">In hello **Monitoring + Management** list click **See all**.</span></span>
4. <span data-ttu-id="0b487-147">In Hallo **aanbevolen** lijst, klikt u op **meer** , en zoekt u in de nieuwe lijst Hallo **Azure SQL Analytics (Preview)** en selecteert u vervolgens.</span><span class="sxs-lookup"><span data-stu-id="0b487-147">In hello **Recommended** list, click **More** , and then in hello new list, find **Azure SQL Analytics (Preview)** and then select it.</span></span>  
    <span data-ttu-id="0b487-148">![Azure SQL Analytics-oplossing](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span><span class="sxs-lookup"><span data-stu-id="0b487-148">![Azure SQL Analytics solution](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span></span>
5. <span data-ttu-id="0b487-149">In Hallo **Azure SQL Analytics (Preview)** blade, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="0b487-149">In hello **Azure SQL Analytics (Preview)** blade, click **Create**.</span></span>  
    <span data-ttu-id="0b487-150">![Maken](./media/log-analytics-azure-sql/portal-create.png)</span><span class="sxs-lookup"><span data-stu-id="0b487-150">![Create](./media/log-analytics-azure-sql/portal-create.png)</span></span>
6. <span data-ttu-id="0b487-151">In Hallo **nieuwe oplossing maken** blade, selecteer Hallo werkruimte dat u wilt dat tooadd Hallo oplossing tooand en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="0b487-151">In hello **Create new solution** blade, select hello workspace that you want tooadd hello solution tooand then click **Create**.</span></span>  
    <span data-ttu-id="0b487-152">![tooworkspace toevoegen](./media/log-analytics-azure-sql/add-to-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="0b487-152">![add tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span></span>


### <a name="tooconfigure-multiple-azure-subscriptions"></a><span data-ttu-id="0b487-153">tooconfigure meerdere Azure-abonnementen</span><span class="sxs-lookup"><span data-stu-id="0b487-153">tooconfigure multiple Azure subscriptions</span></span>

<span data-ttu-id="0b487-154">toosupport meerdere abonnementen gebruiken Hallo PowerShell-script uit [inschakelen Azure resource metrische gegevens logboekregistratie met behulp van PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="0b487-154">toosupport multiple subscriptions, use hello PowerShell script from [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span> <span data-ttu-id="0b487-155">Hallo werkruimte resource-ID opgeven als parameter bij het uitvoeren van Hallo script toosend diagnostische gegevens van resources in één Azure-abonnement tooa werkruimte in een andere Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0b487-155">Provide hello workspace resource ID as a parameter when executing hello script toosend diagnostic data from resources in one Azure subscription tooa workspace in another Azure subscription.</span></span>

<span data-ttu-id="0b487-156">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="0b487-156">**Example**</span></span>

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a><span data-ttu-id="0b487-157">Met behulp van Hallo-oplossing</span><span class="sxs-lookup"><span data-stu-id="0b487-157">Using hello solution</span></span>

<span data-ttu-id="0b487-158">Wanneer u Hallo oplossing tooyour werkruimte toevoegt, hello Azure SQL Analytics tegel tooyour werkruimte is toegevoegd en wordt deze weergegeven in het overzicht.</span><span class="sxs-lookup"><span data-stu-id="0b487-158">When you add hello solution tooyour workspace, hello Azure SQL Analytics tile is added tooyour workspace, and it appears in Overview.</span></span> <span data-ttu-id="0b487-159">Hallo-tegel toont Hallo aantal Azure SQL-databases en elastische pools Azure SQL die Hallo-oplossing is verbonden met.</span><span class="sxs-lookup"><span data-stu-id="0b487-159">hello tile shows hello number of Azure SQL databases and Azure SQL elastic pools that hello solution is connected to.</span></span>

![Azure SQL-Analytics tegel](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a><span data-ttu-id="0b487-161">Azure SQL analytische gegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="0b487-161">Viewing Azure SQL Analytics data</span></span>

<span data-ttu-id="0b487-162">Klik op Hallo **Azure SQL Analytics** tegel tooopen hello Azure SQL Analytics dashboard.</span><span class="sxs-lookup"><span data-stu-id="0b487-162">Click on hello **Azure SQL Analytics** tile tooopen hello Azure SQL Analytics dashboard.</span></span> <span data-ttu-id="0b487-163">Hallo dashboard bevat Hallo blades zoals hieronder gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="0b487-163">hello dashboard includes hello blades defined below.</span></span> <span data-ttu-id="0b487-164">Elke blade bevat too15 resources (abonnement, server elastische pool en database).</span><span class="sxs-lookup"><span data-stu-id="0b487-164">Each blade lists up too15 resources (subscription, server, elastic pool, and database).</span></span> <span data-ttu-id="0b487-165">Klik op een Hallo resources tooopen Hallo dashboard voor die specifieke bron.</span><span class="sxs-lookup"><span data-stu-id="0b487-165">Click any of hello resources tooopen hello dashboard for that specific resource.</span></span> <span data-ttu-id="0b487-166">Elastische Pool of Database bevat Hallo grafieken met metrische gegevens voor een geselecteerde bron.</span><span class="sxs-lookup"><span data-stu-id="0b487-166">Elastic Pool or Database contains hello charts with metrics for a selected resource.</span></span> <span data-ttu-id="0b487-167">Klik op een grafiek tooopen Hallo logboek zoeken dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0b487-167">Click a chart tooopen hello Log Search dialog.</span></span>

| <span data-ttu-id="0b487-168">Blade</span><span class="sxs-lookup"><span data-stu-id="0b487-168">Blade</span></span> | <span data-ttu-id="0b487-169">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0b487-169">Description</span></span> |
|---|---|
| <span data-ttu-id="0b487-170">Abonnementen</span><span class="sxs-lookup"><span data-stu-id="0b487-170">Subscriptions</span></span> | <span data-ttu-id="0b487-171">Lijst met abonnementen met het aantal gekoppelde servers, -adresgroepen en -databases.</span><span class="sxs-lookup"><span data-stu-id="0b487-171">List of subscriptions with number of connected servers, pools, and databases.</span></span> |
| <span data-ttu-id="0b487-172">Servers</span><span class="sxs-lookup"><span data-stu-id="0b487-172">Servers</span></span> | <span data-ttu-id="0b487-173">Lijst met servers met een aantal van de verbonden groepen en databases.</span><span class="sxs-lookup"><span data-stu-id="0b487-173">List of servers with number of connected pools and databases.</span></span> |
| <span data-ttu-id="0b487-174">Elastische pools</span><span class="sxs-lookup"><span data-stu-id="0b487-174">Elastic Pools</span></span> | <span data-ttu-id="0b487-175">Lijst met verbonden elastische pools met maximale GB en eDTU in Hallo waargenomen periode.</span><span class="sxs-lookup"><span data-stu-id="0b487-175">List of connected elastic pools with maximum GB and eDTU in hello observed period.</span></span> |
|<span data-ttu-id="0b487-176">Databases</span><span class="sxs-lookup"><span data-stu-id="0b487-176">Databases</span></span> | <span data-ttu-id="0b487-177">Lijst van de gekoppelde databases met maximale GB en DTU op Hallo waargenomen periode.</span><span class="sxs-lookup"><span data-stu-id="0b487-177">List of connected databases with maximum GB and DTU in hello observed period.</span></span>|


### <a name="analyze-data-and-create-alerts"></a><span data-ttu-id="0b487-178">Gegevens analyseren en waarschuwingen maken</span><span class="sxs-lookup"><span data-stu-id="0b487-178">Analyze data and create alerts</span></span>

<span data-ttu-id="0b487-179">U kunt eenvoudig waarschuwingen maken met de Hallo-gegevens die afkomstig zijn uit Azure SQL Database-resources.</span><span class="sxs-lookup"><span data-stu-id="0b487-179">You can easily create alerts with hello data coming from Azure SQL Database resources.</span></span> <span data-ttu-id="0b487-180">Hier volgen enkele nuttige [logboek zoeken](log-analytics-log-searches.md) query's die u voor waarschuwingen gebruiken kunt:</span><span class="sxs-lookup"><span data-stu-id="0b487-180">Here are a couple of useful [log search](log-analytics-log-searches.md) queries that you can use for alerting:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


<span data-ttu-id="0b487-181">*Hoge DTU voor Azure SQL Database*</span><span class="sxs-lookup"><span data-stu-id="0b487-181">*High DTU on Azure SQL Database*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="0b487-182">*Hoge DTU op elastische Pool in Azure SQL Database*</span><span class="sxs-lookup"><span data-stu-id="0b487-182">*High DTU on Azure SQL Database Elastic Pool*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="0b487-183">U kunt deze tooalert waarschuwing-query's op specifieke drempelwaarden voor Azure SQL Database en elastische pools.</span><span class="sxs-lookup"><span data-stu-id="0b487-183">You can use these alert-based queries tooalert on specific thresholds for both Azure SQL Database and elastic pools.</span></span> <span data-ttu-id="0b487-184">tooconfigure een waarschuwing voor de OMS-werkruimte:</span><span class="sxs-lookup"><span data-stu-id="0b487-184">tooconfigure an alert for your OMS workspace:</span></span>

#### <a name="tooconfigure-an-alert-for-your-workspace"></a><span data-ttu-id="0b487-185">een waarschuwing voor uw werkruimte tooconfigure</span><span class="sxs-lookup"><span data-stu-id="0b487-185">tooconfigure an alert for your workspace</span></span>

1. <span data-ttu-id="0b487-186">Ga toohello [OMS-portal](http://mms.microsoft.com/) en meld u aan.</span><span class="sxs-lookup"><span data-stu-id="0b487-186">Go toohello [OMS portal](http://mms.microsoft.com/) and sign in.</span></span>
2. <span data-ttu-id="0b487-187">Hallo-werkruimte die u hebt geconfigureerd voor Hallo oplossing worden geopend.</span><span class="sxs-lookup"><span data-stu-id="0b487-187">Open hello workspace that you have configured for hello solution.</span></span>
3. <span data-ttu-id="0b487-188">Klik op de overzichtspagina Hallo Hallo **Azure SQL Analytics (Preview)** tegel.</span><span class="sxs-lookup"><span data-stu-id="0b487-188">On hello Overview page, click hello **Azure SQL Analytics (Preview)** tile.</span></span>
4. <span data-ttu-id="0b487-189">Voer een van de Hallo voorbeelden van query's.</span><span class="sxs-lookup"><span data-stu-id="0b487-189">Run one of hello example queries.</span></span>
5. <span data-ttu-id="0b487-190">In logboek zoekopdracht, klikt u op **waarschuwing**.</span><span class="sxs-lookup"><span data-stu-id="0b487-190">In Log Search, click **Alert**.</span></span>  
<span data-ttu-id="0b487-191">![waarschuwing in de zoekopdracht maken](./media/log-analytics-azure-sql/create-alert01.png)</span><span class="sxs-lookup"><span data-stu-id="0b487-191">![create alert in search](./media/log-analytics-azure-sql/create-alert01.png)</span></span>
6. <span data-ttu-id="0b487-192">Op Hallo **waarschuwingsregel toevoegen** pagina, Hallo toepasselijke eigenschappen configureren en specifieke drempelwaarden die u wilt en klik vervolgens op Hallo **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0b487-192">On hello **Add Alert Rule** page, configure hello appropriate properties and hello specific thresholds that you want and then click **Save**.</span></span>  
<span data-ttu-id="0b487-193">![toevoegen van waarschuwingsregel](./media/log-analytics-azure-sql/create-alert02.png)</span><span class="sxs-lookup"><span data-stu-id="0b487-193">![add alert rule](./media/log-analytics-azure-sql/create-alert02.png)</span></span>

### <a name="act-on-azure-sql-analytics-data"></a><span data-ttu-id="0b487-194">Reageren op Azure SQL analytische gegevens</span><span class="sxs-lookup"><span data-stu-id="0b487-194">Act on Azure SQL Analytics data</span></span>

<span data-ttu-id="0b487-195">Als u bijvoorbeeld is een van Hallo nuttigst-query's die u kunt uitvoeren toocompare hello DTU-gebruik voor alle Azure SQL elastische Pools voor uw Azure abonnementen.</span><span class="sxs-lookup"><span data-stu-id="0b487-195">As an example, one of hello most useful queries that you can perform is toocompare hello DTU utilization for all Azure SQL Elastic Pools across all your Azure subscriptions.</span></span> <span data-ttu-id="0b487-196">Doorvoer DTU (database Unit) biedt een manier toodescribe Hallo relatieve capaciteit van een prestatieniveau van Basic, Standard en Premium-databases en pools.</span><span class="sxs-lookup"><span data-stu-id="0b487-196">Database Throughput Unit (DTU) provides a way toodescribe hello relative capacity of a performance level of Basic, Standard, and Premium databases and pools.</span></span> <span data-ttu-id="0b487-197">Dtu's zijn gebaseerd op een gecombineerde meting van CPU, geheugen, leest en schrijft.</span><span class="sxs-lookup"><span data-stu-id="0b487-197">DTUs are based on a blended measure of CPU, memory, reads, and writes.</span></span> <span data-ttu-id="0b487-198">Als het aantal dtu's verhogen Hallo power die worden aangeboden door Hallo prestaties wordt verhoogd.</span><span class="sxs-lookup"><span data-stu-id="0b487-198">As DTUs increase, hello power offered by hello performance level increases.</span></span> <span data-ttu-id="0b487-199">Bijvoorbeeld, heeft een prestatieniveau met 5 dtu's vijf keer krachtiger dan een prestatieniveau met 1 DTU.</span><span class="sxs-lookup"><span data-stu-id="0b487-199">For example, a performance level with 5 DTUs has five times more power than a performance level with 1 DTU.</span></span> <span data-ttu-id="0b487-200">Maximale DTU-quotum geldt tooeach server en de elastische pool.</span><span class="sxs-lookup"><span data-stu-id="0b487-200">A maximum DTU quota applies tooeach server and elastic pool.</span></span>

<span data-ttu-id="0b487-201">Hallo na logboek zoekopdracht uitvoert, kunt u eenvoudig zien als u bepaalde of meer dan het gebruik van uw SQL Azure elastische pools.</span><span class="sxs-lookup"><span data-stu-id="0b487-201">By running hello following Log Search query, you can easily tell if you are underutilizing or over utilizing your SQL Azure elastic pools.</span></span>

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> <span data-ttu-id="0b487-202">Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), Hallo hierboven query zou Wijzig toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="0b487-202">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

<span data-ttu-id="0b487-203">In de Hallo voorbeeld te volgen, kunt u zien dat een elastische groep een hoog gebruik in de buurt van 100 heeft % DTU weinig gebruik zijn.</span><span class="sxs-lookup"><span data-stu-id="0b487-203">In hello following example, you can see that one elastic pool has a high usage near 100% DTU while others have very little usage.</span></span> <span data-ttu-id="0b487-204">Verdere tootroubleshoot potentiële recente wijzigingen kunt u onderzoeken in uw omgeving met Logboeken van de Azure-activiteit.</span><span class="sxs-lookup"><span data-stu-id="0b487-204">You can investigate further tootroubleshoot potential recent changes in your environment using Azure Activity logs.</span></span>

![Zoekresultaten voor logboek - hoog gebruik](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a><span data-ttu-id="0b487-206">Zie ook</span><span class="sxs-lookup"><span data-stu-id="0b487-206">See also</span></span>

- <span data-ttu-id="0b487-207">Gebruik [logboek zoekopdrachten](log-analytics-log-searches.md) in logboekanalyse tooview gedetailleerde Azure SQL-gegevens.</span><span class="sxs-lookup"><span data-stu-id="0b487-207">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics tooview detailed Azure SQL data.</span></span>
- <span data-ttu-id="0b487-208">[Maak uw eigen dashboards](log-analytics-dashboards.md) Azure SQL-gegevens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0b487-208">[Create your own dashboards](log-analytics-dashboards.md) showing Azure SQL data.</span></span>
- <span data-ttu-id="0b487-209">[Waarschuwingen maken](log-analytics-alerts.md) wanneer specifieke Azure SQL-gebeurtenissen plaatsvinden.</span><span class="sxs-lookup"><span data-stu-id="0b487-209">[Create alerts](log-analytics-alerts.md) when specific Azure SQL events occur.</span></span>

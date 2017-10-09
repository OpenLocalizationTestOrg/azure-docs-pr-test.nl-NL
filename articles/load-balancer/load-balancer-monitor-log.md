---
title: aaaMonitor bewerkingen, gebeurtenissen en prestatiemeteritems voor de Load Balancer | Microsoft Docs
description: Meer informatie over hoe tooenable waarschuwing gebeurtenissen en registratie van de health-status voor Azure Load Balancer-test
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="fe122-103">Logboekanalyse voor Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="fe122-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="fe122-104">U kunt verschillende typen Logboeken gebruiken in Azure toomanage en netwerktaakverdelers oplossen.</span><span class="sxs-lookup"><span data-stu-id="fe122-104">You can use different types of logs in Azure toomanage and troubleshoot load balancers.</span></span> <span data-ttu-id="fe122-105">Sommige van deze logboeken zijn toegankelijk via Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="fe122-105">Some of these logs can be accessed through hello portal.</span></span> <span data-ttu-id="fe122-106">Alle logboeken kunnen worden opgehaald uit Azure blob-opslag en worden bekeken in verschillende hulpprogramma's zoals Excel en Power BI.</span><span class="sxs-lookup"><span data-stu-id="fe122-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="fe122-107">U kunt meer informatie over Hallo verschillende typen logboeken in Hallo onderstaande lijst.</span><span class="sxs-lookup"><span data-stu-id="fe122-107">You can learn more about hello different types of logs from hello list below.</span></span>

* <span data-ttu-id="fe122-108">**Controlelogboeken:** kunt u [Azure controlelogboeken](../monitoring-and-diagnostics/insights-debugging-with-events.md) (voorheen bekend als operationele Logboeken) tooview alle bewerkingen worden verzonden tooyour Azure-abonnementen en hun status.</span><span class="sxs-lookup"><span data-stu-id="fe122-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) tooview all operations being submitted tooyour Azure subscription(s), and their status.</span></span> <span data-ttu-id="fe122-109">Controlelogboeken zijn standaard ingeschakeld en kunnen worden bekeken in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fe122-109">Audit logs are enabled by default, and can be viewed in hello Azure portal.</span></span>
* <span data-ttu-id="fe122-110">**Waarschuwing van gebeurtenislogboeken:** kunt u dit logboek tooview waarschuwingen rasied door Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="fe122-110">**Alert event logs:** You can use this log tooview alerts rasied by hello load balancer.</span></span> <span data-ttu-id="fe122-111">Hallo-status voor Hallo load balancer worden verzameld om de vijf minuten.</span><span class="sxs-lookup"><span data-stu-id="fe122-111">hello status for hello load balancer is collected every five minutes.</span></span> <span data-ttu-id="fe122-112">Dit logboek wordt alleen geschreven als een load balancer waarschuwing gebeurtenis treedt op.</span><span class="sxs-lookup"><span data-stu-id="fe122-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="fe122-113">**Health test Logboeken:** kunt u dit logboek tooview problemen die door uw health test, zoals het aantal exemplaren in uw back-end-pool die aanvragen vanwege health test problemen niet van Hallo load balancer ontvangen Hallo gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="fe122-113">**Health probe logs:** You can use this log tooview problems detected by your health probe, such as hello number of instances in your backend-pool that are not receiving requests from hello load balancer because of health probe failures.</span></span> <span data-ttu-id="fe122-114">Dit logboek wordt geschreven toowhen Hallo health test status is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="fe122-114">This log is written toowhen there is a change in hello health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe122-115">Meld u analytics momenteel werkt alleen voor Internet gerichte load balancers.</span><span class="sxs-lookup"><span data-stu-id="fe122-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="fe122-116">Logboeken zijn alleen beschikbaar voor resources geïmplementeerd in Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="fe122-116">Logs are only available for resources deployed in hello Resource Manager deployment model.</span></span> <span data-ttu-id="fe122-117">U kunt Logboeken niet gebruiken voor bronnen in het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="fe122-117">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="fe122-118">Zie voor meer informatie over de implementatiemodellen Hallo [Understanding Resource Manager-implementatie en klassieke implementatie](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fe122-118">For more information about hello deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="fe122-119">Logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="fe122-119">Enable logging</span></span>

<span data-ttu-id="fe122-120">Logboekregistratie is automatisch ingeschakeld voor elke Resource Manager-resource.</span><span class="sxs-lookup"><span data-stu-id="fe122-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="fe122-121">U moet tooenable gebeurtenis en health test logboekregistratie toostart Hallo gegevens beschikbaar zijn via deze logboeken worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="fe122-121">You need tooenable event and health probe logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="fe122-122">Volgende stappen tooenable logboekregistratie hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fe122-122">Use hello following steps tooenable logging.</span></span>

<span data-ttu-id="fe122-123">Aanmelden toohello [Azure-portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fe122-123">Sign-in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="fe122-124">Als u een load balancer, nog niet hebt [maken van een load balancer](load-balancer-get-started-internet-arm-ps.md) voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="fe122-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="fe122-125">Klik in de portal Hallo op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="fe122-125">In hello portal, click **Browse**.</span></span>
2. <span data-ttu-id="fe122-126">Selecteer **Taakverdelers**.</span><span class="sxs-lookup"><span data-stu-id="fe122-126">Select **Load Balancers**.</span></span>

    ![Portal - load balancer](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="fe122-128">Selecteer een bestaande load balancer >> **alle instellingen**.</span><span class="sxs-lookup"><span data-stu-id="fe122-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="fe122-129">Aan de rechterkant Hallo van Hallo dialoogvenster onder de naam van de Hallo Hallo load balancer, schuif te**bewaking**, klikt u op **Diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="fe122-129">On hello right side of hello dialog under hello name of hello load balancer, scroll too**Monitoring**, click **Diagnostics**.</span></span>

    ![Portal - instellingen van een load balancer](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="fe122-131">In Hallo **Diagnostics** deelvenster onder **Status**, selecteer **op**.</span><span class="sxs-lookup"><span data-stu-id="fe122-131">In hello **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="fe122-132">Klik op **Opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="fe122-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="fe122-133">Onder **LOGBOEKEN**, selecteer een bestaand opslagaccount of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="fe122-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="fe122-134">Hallo schuifregelaar toodetermine hoeveel dagen aan gebeurtenisgegevens wordt opgeslagen in de gebeurtenislogboeken Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fe122-134">Use hello slider toodetermine how many days worth of event data will be stored in hello event logs.</span></span> 
8. <span data-ttu-id="fe122-135">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fe122-135">Click **Save**.</span></span>

    ![Portal - logboeken met diagnostische gegevens](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="fe122-137">Controlelogboeken vereisen een afzonderlijke opslagaccount niet.</span><span class="sxs-lookup"><span data-stu-id="fe122-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="fe122-138">Hallo gebruik van opslag voor de gebeurtenis en health test logboekregistratie wordt service worden kosten in rekening.</span><span class="sxs-lookup"><span data-stu-id="fe122-138">hello use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="fe122-139">Controlelogboek</span><span class="sxs-lookup"><span data-stu-id="fe122-139">Audit log</span></span>

<span data-ttu-id="fe122-140">Hallo-controlelogboek wordt standaard gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="fe122-140">hello audit log is generated by default.</span></span> <span data-ttu-id="fe122-141">Hallo-logboeken worden bewaard gedurende 90 dagen in Azure gebeurtenislogboeken store.</span><span class="sxs-lookup"><span data-stu-id="fe122-141">hello logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="fe122-142">Meer informatie over deze logboeken door te lezen Hallo [gebeurtenissen bekijken en controlelogboeken](../monitoring-and-diagnostics/insights-debugging-with-events.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="fe122-142">Learn more about these logs by reading hello [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="fe122-143">Waarschuwing gebeurtenislogboek</span><span class="sxs-lookup"><span data-stu-id="fe122-143">Alert event log</span></span>

<span data-ttu-id="fe122-144">Dit logboek wordt alleen gegenereerd als u het hebt ingeschakeld op een per load balancer basis.</span><span class="sxs-lookup"><span data-stu-id="fe122-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="fe122-145">Hallo-gebeurtenissen worden vastgelegd in JSON-indeling en opgeslagen in Hallo storage-account opgegeven wanneer u Hallo-logboekregistratie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="fe122-145">hello events are logged in JSON format and stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="fe122-146">Hallo Hieronder volgt een voorbeeld van een gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="fe122-146">hello following is an example of an event.</span></span>

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

<span data-ttu-id="fe122-147">Hallo JSON-uitvoer toont Hallo *eventname* eigenschap die wordt beschreven Hallo reden voor Hallo load balancer een waarschuwing gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fe122-147">hello JSON output shows hello *eventname* property which will describe hello reason for hello load balancer created an alert.</span></span> <span data-ttu-id="fe122-148">In dit geval is Hallo waarschuwing gegenereerd vervallen tooTCP poort uitputting veroorzaakt door de bron-IP NAT beperkt (snat omzetten).</span><span class="sxs-lookup"><span data-stu-id="fe122-148">In this case, hello alert generated was due tooTCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="fe122-149">Health test-logboek</span><span class="sxs-lookup"><span data-stu-id="fe122-149">Health probe log</span></span>

<span data-ttu-id="fe122-150">Dit logboek wordt alleen gegenereerd als u het hebt ingeschakeld op een per per load balancer als gedetailleerde hierboven.</span><span class="sxs-lookup"><span data-stu-id="fe122-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="fe122-151">Hallo-gegevens worden opgeslagen in Hallo storage-account opgegeven wanneer u Hallo-logboekregistratie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="fe122-151">hello data is stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="fe122-152">Een container met de naam 'insights-logboeken-loadbalancerprobehealthstatus' wordt gemaakt en Hallo volgt gegevens vastgelegd:</span><span class="sxs-lookup"><span data-stu-id="fe122-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and hello following data is logged:</span></span>

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

<span data-ttu-id="fe122-153">Hallo JSON-uitvoer geeft in Hallo eigenschappen veld Hallo basisinformatie voor Hallo test gezondheidsstatus.</span><span class="sxs-lookup"><span data-stu-id="fe122-153">hello JSON output shows in hello properties field hello basic information for hello probe health status.</span></span> <span data-ttu-id="fe122-154">Hallo *dipDownCount* eigenschap toont Hallo kunt u het totale aantal exemplaren op Hallo back-end die netwerkverkeer vanwege toofailed test antwoorden niet ontvangen.</span><span class="sxs-lookup"><span data-stu-id="fe122-154">hello *dipDownCount* property shows hello total number of instances on hello back-end which are not receiving network traffic due toofailed probe responses.</span></span>

## <a name="view-and-analyze-hello-audit-log"></a><span data-ttu-id="fe122-155">Weergeven en analyseren van het controlelogboek Hallo</span><span class="sxs-lookup"><span data-stu-id="fe122-155">View and analyze hello audit log</span></span>

<span data-ttu-id="fe122-156">U kunt weergeven en analyseren van audit logboekgegevens met behulp van een Hallo volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="fe122-156">You can view and analyze audit log data using any of hello following methods:</span></span>

* <span data-ttu-id="fe122-157">**Azure-hulpprogramma's:** gegevens ophalen uit controlelogboeken Hallo via Azure PowerShell, hello Azure opdrachtregelinterface (CLI), hello Azure REST-API of hello Azure preview-portal.</span><span class="sxs-lookup"><span data-stu-id="fe122-157">**Azure tools:** Retrieve information from hello audit logs through Azure PowerShell, hello Azure Command Line Interface (CLI), hello Azure REST API, or hello Azure preview portal.</span></span> <span data-ttu-id="fe122-158">Stapsgewijze instructies voor elke methode zijn aangegeven in Hallo [bewerkingen met Resource Manager controleren](../azure-resource-manager/resource-group-audit.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="fe122-158">Step-by-step instructions for each method are detailed in hello [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="fe122-159">**Power BI:** als u nog geen een [Power BI](https://powerbi.microsoft.com/pricing) account, kunt u proberen deze gratis.</span><span class="sxs-lookup"><span data-stu-id="fe122-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="fe122-160">Met behulp van Hallo [Azure controlelogboeken inhoud pack voor Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), kunt u uw gegevens met vooraf geconfigureerde dashboards analyseren, of u weergaven toosuit uw vereisten kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="fe122-160">Using hello [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views toosuit your requirements.</span></span>

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a><span data-ttu-id="fe122-161">Weergeven en analyseren Hallo health test en gebeurtenislogboek</span><span class="sxs-lookup"><span data-stu-id="fe122-161">View and analyze hello health probe and event log</span></span>

<span data-ttu-id="fe122-162">U moet tooconnect tooyour storage-account en Hallo JSON logboekvermeldingen voor gebeurtenis en health test-logboeken ophalen.</span><span class="sxs-lookup"><span data-stu-id="fe122-162">You need tooconnect tooyour storage account and retrieve hello JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="fe122-163">Zodra u Hallo JSON-bestanden hebt gedownload, kunt u deze converteren tooCSV en weergeven in Excel, Power BI of een ander gegevensvisualisatie-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="fe122-163">Once you download hello JSON files, you can convert them tooCSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="fe122-164">Als u bekend met Visual Studio en de basisconcepten bent van het wijzigen van waarden voor de constanten en variabelen in C#, kunt u Hallo [Meld converter extra](https://github.com/Azure-Samples/networking-dotnet-log-converter) beschikbaar is via GitHub.</span><span class="sxs-lookup"><span data-stu-id="fe122-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fe122-165">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="fe122-165">Additional resources</span></span>

* <span data-ttu-id="fe122-166">[Uw Azure controlelogboeken met Power BI visualiseren](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blogbericht.</span><span class="sxs-lookup"><span data-stu-id="fe122-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="fe122-167">[Weergeven en analyseren van Azure controlelogboeken in Power BI en meer](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blogbericht.</span><span class="sxs-lookup"><span data-stu-id="fe122-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe122-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fe122-168">Next steps</span></span>

[<span data-ttu-id="fe122-169">Load Balancer-testen</span><span class="sxs-lookup"><span data-stu-id="fe122-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)

---
title: Bewaken van bewerkingen, gebeurtenissen en prestatiemeteritems voor de Load Balancer | Microsoft Docs
description: Informatie over het inschakelen van waarschuwingsgebeurtenissen en registratie van de health-status voor Azure Load Balancer-test
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
ms.openlocfilehash: 638ecd5e02889bd8cb6e7429dfcec335feaac4a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="31272-103">Logboekanalyse voor Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="31272-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="31272-104">U kunt verschillende typen logboeken in Azure beheren en problemen oplossen netwerktaakverdelers.</span><span class="sxs-lookup"><span data-stu-id="31272-104">You can use different types of logs in Azure to manage and troubleshoot load balancers.</span></span> <span data-ttu-id="31272-105">Sommige van deze logboeken zijn toegankelijk via de portal.</span><span class="sxs-lookup"><span data-stu-id="31272-105">Some of these logs can be accessed through the portal.</span></span> <span data-ttu-id="31272-106">Alle logboeken kunnen worden opgehaald uit Azure blob-opslag en worden bekeken in verschillende hulpprogramma's zoals Excel en Power BI.</span><span class="sxs-lookup"><span data-stu-id="31272-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="31272-107">U kunt meer informatie over de verschillende typen logboeken in de onderstaande lijst.</span><span class="sxs-lookup"><span data-stu-id="31272-107">You can learn more about the different types of logs from the list below.</span></span>

* <span data-ttu-id="31272-108">**Controlelogboeken:** kunt u [Azure controlelogboeken](../monitoring-and-diagnostics/insights-debugging-with-events.md) (voorheen bekend als operationele Logboeken) om alle bewerkingen die worden verzonden naar uw Azure-abonnementen en hun status weer te geven.</span><span class="sxs-lookup"><span data-stu-id="31272-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) to view all operations being submitted to your Azure subscription(s), and their status.</span></span> <span data-ttu-id="31272-109">Controlelogboeken zijn standaard ingeschakeld en kunnen worden weergegeven in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="31272-109">Audit logs are enabled by default, and can be viewed in the Azure portal.</span></span>
* <span data-ttu-id="31272-110">**Waarschuwing van gebeurtenislogboeken:** kunt u dit logboek rasied waarschuwingen weergeven met de load balancer.</span><span class="sxs-lookup"><span data-stu-id="31272-110">**Alert event logs:** You can use this log to view alerts rasied by the load balancer.</span></span> <span data-ttu-id="31272-111">De status voor de load balancer worden verzameld om de vijf minuten.</span><span class="sxs-lookup"><span data-stu-id="31272-111">The status for the load balancer is collected every five minutes.</span></span> <span data-ttu-id="31272-112">Dit logboek wordt alleen geschreven als een load balancer waarschuwing gebeurtenis treedt op.</span><span class="sxs-lookup"><span data-stu-id="31272-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="31272-113">**Health test Logboeken:** kunt u dit logboek bekijken door uw health test, zoals het aantal exemplaren in uw back-end-pool die aanvragen vanwege health test problemen niet van de load balancer ontvangen gedetecteerde problemen.</span><span class="sxs-lookup"><span data-stu-id="31272-113">**Health probe logs:** You can use this log to view problems detected by your health probe, such as the number of instances in your backend-pool that are not receiving requests from the load balancer because of health probe failures.</span></span> <span data-ttu-id="31272-114">Dit logboek wordt geschreven naar wanneer er een wijziging in de status van de test.</span><span class="sxs-lookup"><span data-stu-id="31272-114">This log is written to when there is a change in the health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31272-115">Meld u analytics momenteel werkt alleen voor Internet gerichte load balancers.</span><span class="sxs-lookup"><span data-stu-id="31272-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="31272-116">Logboeken zijn alleen beschikbaar voor resources die zijn geïmplementeerd in het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="31272-116">Logs are only available for resources deployed in the Resource Manager deployment model.</span></span> <span data-ttu-id="31272-117">U kunt Logboeken niet gebruiken voor resources in het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="31272-117">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="31272-118">Zie voor meer informatie over de implementatiemodellen [Understanding Resource Manager-implementatie en klassieke implementatie](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="31272-118">For more information about the deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="31272-119">Logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="31272-119">Enable logging</span></span>

<span data-ttu-id="31272-120">Logboekregistratie is automatisch ingeschakeld voor elke Resource Manager-resource.</span><span class="sxs-lookup"><span data-stu-id="31272-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="31272-121">U moet inschakelen gebeurtenis en health test logboekregistratie voor het starten van de gegevens beschikbaar zijn via deze logboeken worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="31272-121">You need to enable event and health probe logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="31272-122">Gebruik de volgende stappen logboekregistratie in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="31272-122">Use the following steps to enable logging.</span></span>

<span data-ttu-id="31272-123">Aanmelden bij de [Azure-portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31272-123">Sign-in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="31272-124">Als u een load balancer, nog niet hebt [maken van een load balancer](load-balancer-get-started-internet-arm-ps.md) voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="31272-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="31272-125">Klik in de portal op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="31272-125">In the portal, click **Browse**.</span></span>
2. <span data-ttu-id="31272-126">Selecteer **Taakverdelers**.</span><span class="sxs-lookup"><span data-stu-id="31272-126">Select **Load Balancers**.</span></span>

    ![Portal - load balancer](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="31272-128">Selecteer een bestaande load balancer >> **alle instellingen**.</span><span class="sxs-lookup"><span data-stu-id="31272-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="31272-129">Aan de rechterkant van het dialoogvenster onder de naam van de load balancer, schuif naar **bewaking**, klikt u op **Diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="31272-129">On the right side of the dialog under the name of the load balancer, scroll to **Monitoring**, click **Diagnostics**.</span></span>

    ![Portal - instellingen van een load balancer](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="31272-131">In de **Diagnostics** deelvenster onder **Status**, selecteer **op**.</span><span class="sxs-lookup"><span data-stu-id="31272-131">In the **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="31272-132">Klik op **Opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="31272-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="31272-133">Onder **LOGBOEKEN**, selecteer een bestaand opslagaccount of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="31272-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="31272-134">Gebruik de schuifregelaar om te bepalen hoeveel dagen gebeurtenisgegevens worden opgeslagen in de gebeurtenislogboeken.</span><span class="sxs-lookup"><span data-stu-id="31272-134">Use the slider to determine how many days worth of event data will be stored in the event logs.</span></span> 
8. <span data-ttu-id="31272-135">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="31272-135">Click **Save**.</span></span>

    ![Portal - logboeken met diagnostische gegevens](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="31272-137">Controlelogboeken vereisen een afzonderlijke opslagaccount niet.</span><span class="sxs-lookup"><span data-stu-id="31272-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="31272-138">Het gebruik van opslag voor de gebeurtenis en health test logboekregistratie wordt service worden kosten in rekening.</span><span class="sxs-lookup"><span data-stu-id="31272-138">The use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="31272-139">Controlelogboek</span><span class="sxs-lookup"><span data-stu-id="31272-139">Audit log</span></span>

<span data-ttu-id="31272-140">Het controlelogboek wordt standaard gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="31272-140">The audit log is generated by default.</span></span> <span data-ttu-id="31272-141">De logboeken worden bewaard gedurende 90 dagen in de Azure gebeurtenislogboeken store.</span><span class="sxs-lookup"><span data-stu-id="31272-141">The logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="31272-142">Meer informatie over deze logboeken door te lezen de [gebeurtenissen bekijken en controlelogboeken](../monitoring-and-diagnostics/insights-debugging-with-events.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="31272-142">Learn more about these logs by reading the [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="31272-143">Waarschuwing gebeurtenislogboek</span><span class="sxs-lookup"><span data-stu-id="31272-143">Alert event log</span></span>

<span data-ttu-id="31272-144">Dit logboek wordt alleen gegenereerd als u het hebt ingeschakeld op een per load balancer basis.</span><span class="sxs-lookup"><span data-stu-id="31272-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="31272-145">De gebeurtenissen worden vastgelegd in JSON-indeling en opgeslagen in het opslagaccount dat u hebt opgegeven als u de logboekregistratie ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="31272-145">The events are logged in JSON format and stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="31272-146">Hier volgt een voorbeeld van een gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="31272-146">The following is an example of an event.</span></span>

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

<span data-ttu-id="31272-147">De JSON-uitvoer bevat de *eventname* -eigenschap hebben die de reden voor de load balancer beschrijft een waarschuwing gemaakt.</span><span class="sxs-lookup"><span data-stu-id="31272-147">The JSON output shows the *eventname* property which will describe the reason for the load balancer created an alert.</span></span> <span data-ttu-id="31272-148">In dit geval is de waarschuwing gegenereerd als gevolg van uitputting van de TCP-poort is veroorzaakt door de bron-IP NAT limieten (snat omzetten).</span><span class="sxs-lookup"><span data-stu-id="31272-148">In this case, the alert generated was due to TCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="31272-149">Health test-logboek</span><span class="sxs-lookup"><span data-stu-id="31272-149">Health probe log</span></span>

<span data-ttu-id="31272-150">Dit logboek wordt alleen gegenereerd als u het hebt ingeschakeld op een per per load balancer als gedetailleerde hierboven.</span><span class="sxs-lookup"><span data-stu-id="31272-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="31272-151">De gegevens worden opgeslagen in het opslagaccount dat u hebt opgegeven als u de logboekregistratie ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="31272-151">The data is stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="31272-152">Een container met de naam 'insights-logboeken-loadbalancerprobehealthstatus' wordt gemaakt en de volgende gegevens worden geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="31272-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and the following data is logged:</span></span>

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

<span data-ttu-id="31272-153">De JSON-uitvoer ziet in het eigenschappenveld de basisgegevens voor de status van de test.</span><span class="sxs-lookup"><span data-stu-id="31272-153">The JSON output shows in the properties field the basic information for the probe health status.</span></span> <span data-ttu-id="31272-154">De *dipDownCount* eigenschap geeft het totale aantal exemplaren op de back-end die netwerkverkeer vanwege mislukte test antwoorden niet ontvangen.</span><span class="sxs-lookup"><span data-stu-id="31272-154">The *dipDownCount* property shows the total number of instances on the back-end which are not receiving network traffic due to failed probe responses.</span></span>

## <a name="view-and-analyze-the-audit-log"></a><span data-ttu-id="31272-155">Weergeven en analyseren van het controlelogboek</span><span class="sxs-lookup"><span data-stu-id="31272-155">View and analyze the audit log</span></span>

<span data-ttu-id="31272-156">U kunt weergeven en analyseren van audit logboekgegevens met behulp van een van de volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="31272-156">You can view and analyze audit log data using any of the following methods:</span></span>

* <span data-ttu-id="31272-157">**Azure-hulpprogramma's:** gegevens ophalen uit de controlelogboeken via Azure PowerShell, de Azure-opdrachtregelinterface (CLI), de REST-API van Azure of de Azure preview portal.</span><span class="sxs-lookup"><span data-stu-id="31272-157">**Azure tools:** Retrieve information from the audit logs through Azure PowerShell, the Azure Command Line Interface (CLI), the Azure REST API, or the Azure preview portal.</span></span> <span data-ttu-id="31272-158">Stapsgewijze instructies voor elke methode zijn aangegeven in de [bewerkingen met Resource Manager controleren](../azure-resource-manager/resource-group-audit.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="31272-158">Step-by-step instructions for each method are detailed in the [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="31272-159">**Power BI:** als u nog geen een [Power BI](https://powerbi.microsoft.com/pricing) account, kunt u proberen deze gratis.</span><span class="sxs-lookup"><span data-stu-id="31272-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="31272-160">Met behulp van de [Azure controlelogboeken inhoud pack voor Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), kunt u uw gegevens met vooraf geconfigureerde dashboards analyseren, of u weergaven aanpassen aan uw vereisten kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="31272-160">Using the [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views to suit your requirements.</span></span>

## <a name="view-and-analyze-the-health-probe-and-event-log"></a><span data-ttu-id="31272-161">Weergeven en analyseren van de gebeurtenislogboeken en health test</span><span class="sxs-lookup"><span data-stu-id="31272-161">View and analyze the health probe and event log</span></span>

<span data-ttu-id="31272-162">U moet verbinding maken met uw opslagaccount en ophalen van de JSON-logboekvermeldingen voor gebeurtenis en health test-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="31272-162">You need to connect to your storage account and retrieve the JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="31272-163">Zodra u de JSON-bestanden hebt gedownload, kunt u ze kunt converteren naar CSV en de weergave in Excel, Power BI of een ander gegevensvisualisatie-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="31272-163">Once you download the JSON files, you can convert them to CSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="31272-164">Als u bekend met Visual Studio en de basisconcepten bent van het wijzigen van waarden voor de constanten en variabelen in C#, kunt u de [Meld converter extra](https://github.com/Azure-Samples/networking-dotnet-log-converter) beschikbaar is via GitHub.</span><span class="sxs-lookup"><span data-stu-id="31272-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="31272-165">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="31272-165">Additional resources</span></span>

* <span data-ttu-id="31272-166">[Uw Azure controlelogboeken met Power BI visualiseren](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blogbericht.</span><span class="sxs-lookup"><span data-stu-id="31272-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="31272-167">[Weergeven en analyseren van Azure controlelogboeken in Power BI en meer](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blogbericht.</span><span class="sxs-lookup"><span data-stu-id="31272-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31272-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="31272-168">Next steps</span></span>

[<span data-ttu-id="31272-169">Load Balancer-testen</span><span class="sxs-lookup"><span data-stu-id="31272-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)

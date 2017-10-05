---
title: Toegangslogboeken, Prestatielogboeken, back-end-status en metrische gegevens voor Application Gateway bewaken | Microsoft Docs
description: Meer informatie over het inschakelen en beheren van toegang en Prestatielogboeken voor Application Gateway
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 12c252340b82aba5ee69b12db83353750782e7c5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="20382-103">Back-end-status, diagnostische logboeken en metrische gegevens voor Application Gateway</span><span class="sxs-lookup"><span data-stu-id="20382-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="20382-104">U kunt met behulp van Azure Application Gateway resources bewaken in de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="20382-104">By using Azure Application Gateway, you can monitor resources in the following ways:</span></span>

* <span data-ttu-id="20382-105">[Status van de back-end](#back-end-health): Application Gateway biedt de mogelijkheid voor het bewaken van de status van de servers in de back-end-adresgroepen via de Azure-portal en via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20382-105">[Back-end health](#back-end-health): Application Gateway provides the capability to monitor the health of the servers in the back-end pools through the Azure portal and through PowerShell.</span></span> <span data-ttu-id="20382-106">U kunt ook de status van de back-end-adresgroepen via de prestaties van diagnostische logboeken vinden.</span><span class="sxs-lookup"><span data-stu-id="20382-106">You can also find the health of the back-end pools through the performance diagnostic logs.</span></span>

* <span data-ttu-id="20382-107">[Logboeken](#diagnostic-logs): Logboeken toestaan voor prestaties, toegang en andere gegevens worden opgeslagen of gebruikt van een resource voor controledoeleinden.</span><span class="sxs-lookup"><span data-stu-id="20382-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data to be saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="20382-108">[Metrische gegevens](#metrics): Application Gateway is momenteel een waarde.</span><span class="sxs-lookup"><span data-stu-id="20382-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="20382-109">Met deze metriek wordt de doorvoer van de toepassingsgateway in bytes per seconde.</span><span class="sxs-lookup"><span data-stu-id="20382-109">This metric measures the throughput of the application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="20382-110">Back-end-status</span><span class="sxs-lookup"><span data-stu-id="20382-110">Back-end health</span></span>

<span data-ttu-id="20382-111">Toepassingsgateway biedt de mogelijkheid voor het bewaken van de status van afzonderlijke onderdelen van de back-end-adresgroepen via de portal, PowerShell en de opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="20382-111">Application Gateway provides the capability to monitor the health of individual members of the back-end pools through the portal, PowerShell, and the command-line interface (CLI).</span></span> <span data-ttu-id="20382-112">U kunt ook een geaggregeerde status vinden samenvatting van back-end-groepen via de diagnostische logboeken van de prestaties.</span><span class="sxs-lookup"><span data-stu-id="20382-112">You can also find an aggregated health summary of back-end pools through the performance diagnostic logs.</span></span> 

<span data-ttu-id="20382-113">Het back-end-statusrapport weerspiegelt de uitvoer van de statuscontrole van de Application Gateway naar de back-end-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="20382-113">The back-end health report reflects the output of the Application Gateway health probe to the back-end instances.</span></span> <span data-ttu-id="20382-114">Bij het zoeken is voltooid en de back-end kan verkeer ontvangen, als in orde wordt beschouwd.</span><span class="sxs-lookup"><span data-stu-id="20382-114">When probing is successful and the back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="20382-115">Anders wordt deze orde beschouwd.</span><span class="sxs-lookup"><span data-stu-id="20382-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20382-116">Als er een netwerkbeveiligingsgroep (NSG) op een Application Gateway-subnet, opent u poortbereiken 65503 65534 op het subnet voor Application Gateway voor binnenkomend verkeer.</span><span class="sxs-lookup"><span data-stu-id="20382-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on the Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="20382-117">Deze poorten zijn vereist voor de back-end-status API om te werken.</span><span class="sxs-lookup"><span data-stu-id="20382-117">These ports are required for the back-end health API to work.</span></span>


### <a name="view-back-end-health-through-the-portal"></a><span data-ttu-id="20382-118">Status van de back-end via de portal weergeven</span><span class="sxs-lookup"><span data-stu-id="20382-118">View back-end health through the portal</span></span>

<span data-ttu-id="20382-119">In de portal wordt automatisch back-end health verstrekt.</span><span class="sxs-lookup"><span data-stu-id="20382-119">In the portal, back-end health is provided automatically.</span></span> <span data-ttu-id="20382-120">Selecteer in een bestaande toepassingsgateway **bewaking** > **back-end health**.</span><span class="sxs-lookup"><span data-stu-id="20382-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="20382-121">Elk lid in de back-end-pool wordt vermeld op deze pagina (of het is een NIC, IP of FQDN).</span><span class="sxs-lookup"><span data-stu-id="20382-121">Each member in the back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="20382-122">De naam van de back-endpool, poort, HTTP-instellingen voor de naam van back-end en gezondheidsstatus worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="20382-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="20382-123">Geldige waarden voor gezondheidsstatus zijn **goed**, **niet in orde**, en **onbekende**.</span><span class="sxs-lookup"><span data-stu-id="20382-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="20382-124">Als er een back-end-gezondheidsstatus van **onbekende**, zorg ervoor dat de toegang tot de back-end niet wordt geblokkeerd door een regel voor het NSG, een door de gebruiker opgegeven routes (UDR) of een aangepaste DNS-server in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="20382-124">If you see a back-end health status of **Unknown**, ensure that access to the back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in the virtual network.</span></span>

![Back-end-status][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="20382-126">Status van de back-end via PowerShell weergeven</span><span class="sxs-lookup"><span data-stu-id="20382-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="20382-127">De volgende PowerShell-code laat zien hoe de gezondheid van de back-end weergeven met behulp van de `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="20382-127">The following PowerShell code shows how to view back-end health by using the `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="20382-128">Status van de back-end via Azure CLI 2.0 weergeven</span><span class="sxs-lookup"><span data-stu-id="20382-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="20382-129">Resultaten</span><span class="sxs-lookup"><span data-stu-id="20382-129">Results</span></span>

<span data-ttu-id="20382-130">Het volgende fragment toont een voorbeeld van het antwoord:</span><span class="sxs-lookup"><span data-stu-id="20382-130">The following snippet shows an example of the response:</span></span>

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <span data-ttu-id="20382-131"><a name="diagnostic-logging"></a>Diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="20382-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="20382-132">U kunt verschillende typen logboeken in Azure beheren en problemen oplossen Toepassingsgateways.</span><span class="sxs-lookup"><span data-stu-id="20382-132">You can use different types of logs in Azure to manage and troubleshoot application gateways.</span></span> <span data-ttu-id="20382-133">U kunt sommige van deze logboeken openen via de portal.</span><span class="sxs-lookup"><span data-stu-id="20382-133">You can access some of these logs through the portal.</span></span> <span data-ttu-id="20382-134">Alle logboeken kunnen worden opgehaald uit Azure Blob storage en weergegeven in de verschillende hulpprogramma's, zoals [logboekanalyse](../log-analytics/log-analytics-azure-networking-analytics.md), Excel en Power BI.</span><span class="sxs-lookup"><span data-stu-id="20382-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="20382-135">U kunt meer informatie over de verschillende typen logboeken in de volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="20382-135">You can learn more about the different types of logs from the following list:</span></span>

* <span data-ttu-id="20382-136">**Activiteitenlogboek**: U kunt [Azure activiteitenlogboeken](../monitoring-and-diagnostics/insights-debugging-with-events.md) (voorheen bekend als operationele logboeken en controlelogboeken) om alle bewerkingen die worden verzonden naar uw Azure-abonnement en hun status weer te geven.</span><span class="sxs-lookup"><span data-stu-id="20382-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) to view all operations that are submitted to your Azure subscription, and their status.</span></span> <span data-ttu-id="20382-137">Logboekvermeldingen activiteit worden standaard verzameld en u kunt ze weergeven in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="20382-137">Activity log entries are collected by default, and you can view them in the Azure portal.</span></span>
* <span data-ttu-id="20382-138">**Toegangslogboek**: U kunt dit logboek Application Gateway toegangspatronen weergeven en analyseren van informatie, waaronder de aanroeper IP, aangevraagde URL antwoord latentie, retourcode en bytes in en uit. Een toegangslogboek verzameld om de 300 seconden.</span><span class="sxs-lookup"><span data-stu-id="20382-138">**Access log**: You can use this log to view Application Gateway access patterns and analyze important information, including the caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="20382-139">Dit logboek bevat één record per exemplaar van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="20382-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="20382-140">Het exemplaar Application Gateway kan worden geïdentificeerd door de exemplaar-id-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="20382-140">The Application Gateway instance can be identified by the instanceId property.</span></span>
* <span data-ttu-id="20382-141">**Prestatielogboek**: U kunt dit logboek gebruiken om weer te geven hoe Application Gateway-exemplaren uitvoert.</span><span class="sxs-lookup"><span data-stu-id="20382-141">**Performance log**: You can use this log to view how Application Gateway instances are performing.</span></span> <span data-ttu-id="20382-142">Dit logboek bevat informatie over de prestaties voor elk exemplaar, met inbegrip van totaal aantal aanvragen die worden geleverd, doorvoer in bytes, totaal aantal aanvragen dat wordt geleverd, aantal mislukte aanvragen en in orde en slecht backend-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="20382-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="20382-143">Een prestatielogboek worden verzameld om de 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="20382-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="20382-144">**Firewall-logboek**: U kunt dit logboek gebruiken om de aanvragen die zijn geregistreerd via de modus voor detectie of ter voorkoming van een toepassingsgateway die is geconfigureerd met de web application firewall weer te geven.</span><span class="sxs-lookup"><span data-stu-id="20382-144">**Firewall log**: You can use this log to view the requests that are logged through either detection or prevention mode of an application gateway that is configured with the web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="20382-145">Logboeken zijn alleen beschikbaar voor resources geïmplementeerd in het Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="20382-145">Logs are available only for resources deployed in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="20382-146">U kunt Logboeken niet gebruiken voor resources in het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="20382-146">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="20382-147">Zie voor een beter begrip van de twee modellen, de [Understanding Resource Manager-implementatie en klassieke implementatie](../azure-resource-manager/resource-manager-deployment-model.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="20382-147">For a better understanding of the two models, see the [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="20382-148">Hebt u drie opties voor het opslaan van uw logboeken:</span><span class="sxs-lookup"><span data-stu-id="20382-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="20382-149">**Storage-account**: Storage-accounts beste kunnen worden gebruikt voor Logboeken wanneer logboeken worden opgeslagen voor een langere duur en gelezen wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="20382-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="20382-150">**Event hubs**: Event hubs zijn een goede optie voor het integreren met andere informatie over beveiliging en beheer van gebeurtenissen (SEIM) hulpmiddelen voor waarschuwingen over uw resources.</span><span class="sxs-lookup"><span data-stu-id="20382-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools to get alerts on your resources.</span></span>
* <span data-ttu-id="20382-151">**Meld u Analytics**: Log Analytics is het meest geschikt voor algemene realtime-controle van uw toepassing of trends kijken.</span><span class="sxs-lookup"><span data-stu-id="20382-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="20382-152">Schakel logboekregistratie in via PowerShell</span><span class="sxs-lookup"><span data-stu-id="20382-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="20382-153">Activiteit-logboekregistratie is standaard ingeschakeld voor elke Resource Manager-resource.</span><span class="sxs-lookup"><span data-stu-id="20382-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="20382-154">U moet toegang en prestaties van logboekregistratie voor het starten van de gegevens beschikbaar zijn via deze logboeken verzamelen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="20382-154">You must enable access and performance logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="20382-155">Als logboekregistratie wilt inschakelen, gebruikt u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="20382-155">To enable logging, use the following steps:</span></span>

1. <span data-ttu-id="20382-156">Houd er rekening mee uw storage-account resource-ID, waar de logboekgegevens wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="20382-156">Note your storage account's resource ID, where the log data is stored.</span></span> <span data-ttu-id="20382-157">Deze waarde is van het formulier: /subscriptions/\<subscriptionId\>/resourceGroups/\<Resourcegroepnaam\>/providers/Microsoft.Storage/storageAccounts/\<opslagaccountnaam\>.</span><span class="sxs-lookup"><span data-stu-id="20382-157">This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="20382-158">U kunt opslagaccount gebruiken in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="20382-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="20382-159">U kunt de Azure portal gebruiken om deze informatie te vinden.</span><span class="sxs-lookup"><span data-stu-id="20382-159">You can use the Azure portal to find this information.</span></span>

    ![Portal: resource-ID voor het opslagaccount](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="20382-161">Houd er rekening mee resource-ID van de toepassingsgateway van uw waarvoor logboekregistratie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="20382-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="20382-162">Deze waarde is van het formulier: /subscriptions/\<subscriptionId\>/resourceGroups/\<Resourcegroepnaam\>/providers/Microsoft.Network/applicationGateways/\<gateway toepassingsnaam\>.</span><span class="sxs-lookup"><span data-stu-id="20382-162">This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="20382-163">U kunt de portal gebruiken om deze informatie te vinden.</span><span class="sxs-lookup"><span data-stu-id="20382-163">You can use the portal to find this information.</span></span>

    ![Portal: resource-ID voor de toepassingsgateway](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="20382-165">Diagnostische logboekregistratie inschakelen met behulp van de volgende PowerShell-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="20382-165">Enable diagnostic logging by using the following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="20382-166">Activiteitenlogboeken vereisen een afzonderlijke opslagaccount niet.</span><span class="sxs-lookup"><span data-stu-id="20382-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="20382-167">Het gebruik van opslag voor toegangs- en prestatieregistratie kosten in rekening worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="20382-167">The use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-the-azure-portal"></a><span data-ttu-id="20382-168">Schakel logboekregistratie in via de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="20382-168">Enable logging through the Azure portal</span></span>

1. <span data-ttu-id="20382-169">Uw bron vinden in de Azure portal en klikt u op **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="20382-169">In the Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="20382-170">Er zijn drie logboeken beschikbaar voor Application Gateway:</span><span class="sxs-lookup"><span data-stu-id="20382-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="20382-171">Toegangslogboek</span><span class="sxs-lookup"><span data-stu-id="20382-171">Access log</span></span>
   * <span data-ttu-id="20382-172">Prestatielogboek</span><span class="sxs-lookup"><span data-stu-id="20382-172">Performance log</span></span>
   * <span data-ttu-id="20382-173">Firewall-logboek</span><span class="sxs-lookup"><span data-stu-id="20382-173">Firewall log</span></span>

2. <span data-ttu-id="20382-174">Als u wilt verzamelen van gegevens, klikt u op **diagnostische gegevens inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="20382-174">To start collecting data, click **Turn on diagnostics**.</span></span>

   ![Diagnostische gegevens inschakelen][1]

3. <span data-ttu-id="20382-176">De **diagnostische instellingen** blade bevat de instellingen voor diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="20382-176">The **Diagnostics settings** blade provides the settings for the diagnostic logs.</span></span> <span data-ttu-id="20382-177">In dit voorbeeld worden de logboeken met logboekanalyse opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="20382-177">In this example, Log Analytics stores the logs.</span></span> <span data-ttu-id="20382-178">Klik op **configureren** onder **logboekanalyse** voor het configureren van uw werkruimte.</span><span class="sxs-lookup"><span data-stu-id="20382-178">Click **Configure** under **Log Analytics** to configure your workspace.</span></span> <span data-ttu-id="20382-179">U kunt ook event hubs en storage-account gebruiken om op te slaan van de diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="20382-179">You can also use event hubs and a storage account to save the diagnostic logs.</span></span>

   ![Het configuratieproces wordt gestart][2]

4. <span data-ttu-id="20382-181">Kies een bestaande werkruimte van Operations Management Suite (OMS) of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="20382-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="20382-182">In dit voorbeeld wordt een bestaande.</span><span class="sxs-lookup"><span data-stu-id="20382-182">This example uses an existing one.</span></span>

   ![Opties voor OMS werkruimten][3]

5. <span data-ttu-id="20382-184">Bevestig de instellingen en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="20382-184">Confirm the settings and click **Save**.</span></span>

   ![Diagnostische instellingenblade met selecties][4]

### <a name="activity-log"></a><span data-ttu-id="20382-186">Activiteitenlogboek</span><span class="sxs-lookup"><span data-stu-id="20382-186">Activity log</span></span>

<span data-ttu-id="20382-187">Standaard genereert Azure het activiteitenlogboek.</span><span class="sxs-lookup"><span data-stu-id="20382-187">Azure generates the activity log by default.</span></span> <span data-ttu-id="20382-188">De logboeken gedurende 90 dagen bewaard in de gebeurtenislogboeken van Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="20382-188">The logs are preserved for 90 days in the Azure event logs store.</span></span> <span data-ttu-id="20382-189">Meer informatie over deze logboeken door te lezen de [weergeven van gebeurtenissen en het activiteitenlogboek](../monitoring-and-diagnostics/insights-debugging-with-events.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="20382-189">Learn more about these logs by reading the [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="20382-190">Toegangslogboek</span><span class="sxs-lookup"><span data-stu-id="20382-190">Access log</span></span>

<span data-ttu-id="20382-191">Het toegangslogboek wordt alleen gegenereerd als u deze op elk exemplaar van de toepassingsgateway, zoals beschreven in de voorgaande stappen hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="20382-191">The access log is generated only if you've enabled it on each Application Gateway instance, as detailed in the preceding steps.</span></span> <span data-ttu-id="20382-192">De gegevens worden opgeslagen in het opslagaccount dat u hebt opgegeven als u de logboekregistratie ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="20382-192">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="20382-193">Elke toegang van Application Gateway wordt geregistreerd in JSON-indeling, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="20382-193">Each access of Application Gateway is logged in JSON format, as shown in the following example:</span></span>


|<span data-ttu-id="20382-194">Waarde</span><span class="sxs-lookup"><span data-stu-id="20382-194">Value</span></span>  |<span data-ttu-id="20382-195">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="20382-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="20382-196">Exemplaar-id</span><span class="sxs-lookup"><span data-stu-id="20382-196">instanceId</span></span>     | <span data-ttu-id="20382-197">Gateway-instantie die de aanvraag wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="20382-197">Application Gateway instance that served the request.</span></span>        |
|<span data-ttu-id="20382-198">client-IP</span><span class="sxs-lookup"><span data-stu-id="20382-198">clientIP</span></span>     | <span data-ttu-id="20382-199">Oorspronkelijke IP-adres voor de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="20382-199">Originating IP for the request.</span></span>        |
|<span data-ttu-id="20382-200">enterpriseclient</span><span class="sxs-lookup"><span data-stu-id="20382-200">clientPort</span></span>     | <span data-ttu-id="20382-201">Poort voor de aanvraag afkomstig is.</span><span class="sxs-lookup"><span data-stu-id="20382-201">Originating port for the request.</span></span>       |
|<span data-ttu-id="20382-202">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="20382-202">httpMethod</span></span>     | <span data-ttu-id="20382-203">HTTP-methode die wordt gebruikt door de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="20382-203">HTTP method used by the request.</span></span>       |
|<span data-ttu-id="20382-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="20382-204">requestUri</span></span>     | <span data-ttu-id="20382-205">De URI van de aanvraag ontvangen.</span><span class="sxs-lookup"><span data-stu-id="20382-205">URI of the received request.</span></span>        |
|<span data-ttu-id="20382-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="20382-206">RequestQuery</span></span>     | <span data-ttu-id="20382-207">**Server-gerouteerd**: exemplaar van de Back-end-adresgroep die de aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="20382-207">**Server-Routed**: Back-end pool instance that was sent the request.</span></span> </br> <span data-ttu-id="20382-208">**X-AzureApplicationGateway-logboek-ID**: correlatie-ID van de aanvraag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="20382-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for the request.</span></span> <span data-ttu-id="20382-209">Het kan worden gebruikt om op te lossen problemen met de verkeer voor de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="20382-209">It can be used to troubleshoot traffic issues on the back-end servers.</span></span> </br><span data-ttu-id="20382-210">**STATUS van de SERVER**: HTTP-antwoordcode Application Gateway van de back-end ontvangen.</span><span class="sxs-lookup"><span data-stu-id="20382-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from the back end.</span></span>       |
|<span data-ttu-id="20382-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="20382-211">UserAgent</span></span>     | <span data-ttu-id="20382-212">De gebruikersagent van de HTTP-aanvraag-header.</span><span class="sxs-lookup"><span data-stu-id="20382-212">User agent from the HTTP request header.</span></span>        |
|<span data-ttu-id="20382-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="20382-213">httpStatus</span></span>     | <span data-ttu-id="20382-214">HTTP-statuscode geretourneerd naar de client van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="20382-214">HTTP status code returned to the client from Application Gateway.</span></span>       |
|<span data-ttu-id="20382-215">Httpversie</span><span class="sxs-lookup"><span data-stu-id="20382-215">httpVersion</span></span>     | <span data-ttu-id="20382-216">HTTP-versie van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="20382-216">HTTP version of the request.</span></span>        |
|<span data-ttu-id="20382-217">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="20382-217">receivedBytes</span></span>     | <span data-ttu-id="20382-218">Grootte van het pakket ontvangen in bytes.</span><span class="sxs-lookup"><span data-stu-id="20382-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="20382-219">SentBytes</span><span class="sxs-lookup"><span data-stu-id="20382-219">sentBytes</span></span>| <span data-ttu-id="20382-220">Grootte van het pakket dat is verzonden, in bytes.</span><span class="sxs-lookup"><span data-stu-id="20382-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="20382-221">timeTaken</span><span class="sxs-lookup"><span data-stu-id="20382-221">timeTaken</span></span>| <span data-ttu-id="20382-222">Totale tijdsduur (in milliseconden) die het duurt voordat een aanvraag te verwerken en de reactie daarop worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="20382-222">Length of time (in milliseconds) that it takes for a request to be processed and its response to be sent.</span></span> <span data-ttu-id="20382-223">Dit wordt berekend als het interval van de tijd wanneer Application Gateway ontvangt de eerste byte van een HTTP-aanvraag aan de tijd wanneer de bewerking is voltooid voor het verzenden van het antwoord.</span><span class="sxs-lookup"><span data-stu-id="20382-223">This is calculated as the interval from the time when Application Gateway receives the first byte of an HTTP request to the time when the response send operation finishes.</span></span> <span data-ttu-id="20382-224">Het is belangrijk te weten het veld tijd omvat gewoonlijk het tijdstip waarop de aanvraag en antwoord-pakketten worden overgebracht via het netwerk.</span><span class="sxs-lookup"><span data-stu-id="20382-224">It's important to note that the Time-Taken field usually includes the time that the request and response packets are traveling over the network.</span></span> |
|<span data-ttu-id="20382-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="20382-225">sslEnabled</span></span>| <span data-ttu-id="20382-226">Communicatie met de back-end-adresgroepen wordt aangegeven of SSL gebruikt.</span><span class="sxs-lookup"><span data-stu-id="20382-226">Whether communication to the back-end pools used SSL.</span></span> <span data-ttu-id="20382-227">Geldige waarden zijn in- of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="20382-227">Valid values are on and off.</span></span>|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a><span data-ttu-id="20382-228">Prestatielogboek</span><span class="sxs-lookup"><span data-stu-id="20382-228">Performance log</span></span>

<span data-ttu-id="20382-229">De prestatielogboek wordt alleen gegenereerd als u deze op elk exemplaar van de toepassingsgateway, zoals beschreven in de voorgaande stappen hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="20382-229">The performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in the preceding steps.</span></span> <span data-ttu-id="20382-230">De gegevens worden opgeslagen in het opslagaccount dat u hebt opgegeven als u de logboekregistratie ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="20382-230">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="20382-231">De prestatielogboekgegevens wordt gegenereerd met intervallen van 1 minuut.</span><span class="sxs-lookup"><span data-stu-id="20382-231">The performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="20382-232">De volgende gegevens worden geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="20382-232">The following data is logged:</span></span>


|<span data-ttu-id="20382-233">Waarde</span><span class="sxs-lookup"><span data-stu-id="20382-233">Value</span></span>  |<span data-ttu-id="20382-234">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="20382-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="20382-235">Exemplaar-id</span><span class="sxs-lookup"><span data-stu-id="20382-235">instanceId</span></span>     |  <span data-ttu-id="20382-236">Application Gateway-exemplaren waarvoor gegevens wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="20382-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="20382-237">Er is een rij per exemplaar voor een toepassingsgateway met meerdere-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="20382-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="20382-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="20382-238">healthyHostCount</span></span>     | <span data-ttu-id="20382-239">Het aantal orde hosts in de groep back-end.</span><span class="sxs-lookup"><span data-stu-id="20382-239">Number of healthy hosts in the back-end pool.</span></span>        |
|<span data-ttu-id="20382-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="20382-240">unHealthyHostCount</span></span>     | <span data-ttu-id="20382-241">Het aantal beschadigde hosts in de groep back-end.</span><span class="sxs-lookup"><span data-stu-id="20382-241">Number of unhealthy hosts in the back-end pool.</span></span>        |
|<span data-ttu-id="20382-242">requestCount</span><span class="sxs-lookup"><span data-stu-id="20382-242">requestCount</span></span>     | <span data-ttu-id="20382-243">Het aantal geleverde aanvragen.</span><span class="sxs-lookup"><span data-stu-id="20382-243">Number of requests served.</span></span>        |
|<span data-ttu-id="20382-244">Latentie</span><span class="sxs-lookup"><span data-stu-id="20382-244">latency</span></span> | <span data-ttu-id="20382-245">Latentie (in milliseconden) van aanvragen van het exemplaar naar de back-end die de aanvragen fungeert.</span><span class="sxs-lookup"><span data-stu-id="20382-245">Latency (in milliseconds) of requests from the instance to the back end that serves the requests.</span></span> |
|<span data-ttu-id="20382-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="20382-246">failedRequestCount</span></span>| <span data-ttu-id="20382-247">Het aantal mislukte aanvragen.</span><span class="sxs-lookup"><span data-stu-id="20382-247">Number of failed requests.</span></span>|
|<span data-ttu-id="20382-248">Doorvoer</span><span class="sxs-lookup"><span data-stu-id="20382-248">throughput</span></span>| <span data-ttu-id="20382-249">Gemiddelde doorvoersnelheid sinds de laatste logboek, gemeten in bytes per seconde.</span><span class="sxs-lookup"><span data-stu-id="20382-249">Average throughput since the last log, measured in bytes per second.</span></span>|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> <span data-ttu-id="20382-250">Latentie wordt berekend op basis van de tijd wanneer de eerste byte van de HTTP-aanvraag wordt ontvangen op het tijdstip waarop de laatste byte van het HTTP-antwoord is verzonden.</span><span class="sxs-lookup"><span data-stu-id="20382-250">Latency is calculated from the time when the first byte of the HTTP request is received to the time when the last byte of the HTTP response is sent.</span></span> <span data-ttu-id="20382-251">Het is de som van de verwerkingstijd van de toepassingsgateway plus de netwerkverbindingskosten voor de back-end, plus de tijd die de back-end nodig heeft om de aanvraag te verwerken.</span><span class="sxs-lookup"><span data-stu-id="20382-251">It's the sum of the Application Gateway processing time plus the network cost to the back end, plus the time that the back end takes to process the request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="20382-252">Firewall-logboek</span><span class="sxs-lookup"><span data-stu-id="20382-252">Firewall log</span></span>

<span data-ttu-id="20382-253">De firewall-logboek is gegenereerd, alleen als u deze voor elke application gateway, zoals beschreven in de voorgaande stappen hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="20382-253">The firewall log is generated only if you have enabled it for each application gateway, as detailed in the preceding steps.</span></span> <span data-ttu-id="20382-254">Dit logboek is ook vereist dat de web application firewall op een application gateway is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="20382-254">This log also requires that the web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="20382-255">De gegevens worden opgeslagen in het opslagaccount dat u hebt opgegeven als u de logboekregistratie ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="20382-255">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="20382-256">De volgende gegevens worden geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="20382-256">The following data is logged:</span></span>


|<span data-ttu-id="20382-257">Waarde</span><span class="sxs-lookup"><span data-stu-id="20382-257">Value</span></span>  |<span data-ttu-id="20382-258">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="20382-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="20382-259">Exemplaar-id</span><span class="sxs-lookup"><span data-stu-id="20382-259">instanceId</span></span>     | <span data-ttu-id="20382-260">Gateway toepassingsexemplaar voor welke firewall worden gegevens gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="20382-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="20382-261">Er is een rij per exemplaar voor een toepassingsgateway met meerdere-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="20382-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="20382-262">client-IP</span><span class="sxs-lookup"><span data-stu-id="20382-262">clientIp</span></span>     |   <span data-ttu-id="20382-263">Oorspronkelijke IP-adres voor de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="20382-263">Originating IP for the request.</span></span>      |
|<span data-ttu-id="20382-264">enterpriseclient</span><span class="sxs-lookup"><span data-stu-id="20382-264">clientPort</span></span>     |  <span data-ttu-id="20382-265">Poort voor de aanvraag afkomstig is.</span><span class="sxs-lookup"><span data-stu-id="20382-265">Originating port for the request.</span></span>       |
|<span data-ttu-id="20382-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="20382-266">requestUri</span></span>     | <span data-ttu-id="20382-267">De URL van de aanvraag ontvangen.</span><span class="sxs-lookup"><span data-stu-id="20382-267">URL of the received request.</span></span>       |
|<span data-ttu-id="20382-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="20382-268">ruleSetType</span></span>     | <span data-ttu-id="20382-269">Type van de regelset.</span><span class="sxs-lookup"><span data-stu-id="20382-269">Rule set type.</span></span> <span data-ttu-id="20382-270">De beschikbare waarde is OWASP.</span><span class="sxs-lookup"><span data-stu-id="20382-270">The available value is OWASP.</span></span>        |
|<span data-ttu-id="20382-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="20382-271">ruleSetVersion</span></span>     | <span data-ttu-id="20382-272">Regelset versie die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="20382-272">Rule set version used.</span></span> <span data-ttu-id="20382-273">Beschikbare waarden zijn 2.2.9 en 3.0.</span><span class="sxs-lookup"><span data-stu-id="20382-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="20382-274">ruleId</span><span class="sxs-lookup"><span data-stu-id="20382-274">ruleId</span></span>     | <span data-ttu-id="20382-275">Regel-ID van de activerende gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="20382-275">Rule ID of the triggering event.</span></span>        |
|<span data-ttu-id="20382-276">Bericht</span><span class="sxs-lookup"><span data-stu-id="20382-276">message</span></span>     | <span data-ttu-id="20382-277">Gebruiksvriendelijke bericht voor de triggergebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="20382-277">User-friendly message for the triggering event.</span></span> <span data-ttu-id="20382-278">Meer informatie vindt u in de detailsectie.</span><span class="sxs-lookup"><span data-stu-id="20382-278">More details are provided in the details section.</span></span>        |
|<span data-ttu-id="20382-279">Actie</span><span class="sxs-lookup"><span data-stu-id="20382-279">action</span></span>     |  <span data-ttu-id="20382-280">Actie op die op de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="20382-280">Action taken on the request.</span></span> <span data-ttu-id="20382-281">Beschikbare waarden zijn geblokkeerd en toegestaan.</span><span class="sxs-lookup"><span data-stu-id="20382-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="20382-282">Site</span><span class="sxs-lookup"><span data-stu-id="20382-282">site</span></span>     | <span data-ttu-id="20382-283">De site waarvoor het logboek is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="20382-283">Site for which the log was generated.</span></span> <span data-ttu-id="20382-284">Alleen globale wordt momenteel, omdat er regels zijn globale vermeld.</span><span class="sxs-lookup"><span data-stu-id="20382-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="20382-285">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="20382-285">details</span></span>     | <span data-ttu-id="20382-286">Details van de activerende gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="20382-286">Details of the triggering event.</span></span>        |
|<span data-ttu-id="20382-287">Details.Message</span><span class="sxs-lookup"><span data-stu-id="20382-287">details.message</span></span>     | <span data-ttu-id="20382-288">Beschrijving van de regel.</span><span class="sxs-lookup"><span data-stu-id="20382-288">Description of the rule.</span></span>        |
|<span data-ttu-id="20382-289">Details.Data</span><span class="sxs-lookup"><span data-stu-id="20382-289">details.data</span></span>     | <span data-ttu-id="20382-290">Specifieke gegevens gevonden in de aanvraag die overeenkomt met de regel.</span><span class="sxs-lookup"><span data-stu-id="20382-290">Specific data found in request that matched the rule.</span></span>         |
|<span data-ttu-id="20382-291">Details.File</span><span class="sxs-lookup"><span data-stu-id="20382-291">details.file</span></span>     | <span data-ttu-id="20382-292">Configuratiebestand die deel uitmaakt van de regel.</span><span class="sxs-lookup"><span data-stu-id="20382-292">Configuration file that contained the rule.</span></span>        |
|<span data-ttu-id="20382-293">Details.line</span><span class="sxs-lookup"><span data-stu-id="20382-293">details.line</span></span>     | <span data-ttu-id="20382-294">Regelnummer in het configuratiebestand dat de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="20382-294">Line number in the configuration file that triggered the event.</span></span>       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-the-activity-log"></a><span data-ttu-id="20382-295">Weergeven en analyseren van het activiteitenlogboek</span><span class="sxs-lookup"><span data-stu-id="20382-295">View and analyze the activity log</span></span>

<span data-ttu-id="20382-296">U kunt weergeven en analyseren van logboekgegevens van de activiteit met behulp van de volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="20382-296">You can view and analyze activity log data by using any of the following methods:</span></span>

* <span data-ttu-id="20382-297">**Azure-hulpprogramma's**: gegevens ophalen uit het activiteitenlogboek via Azure PowerShell, de Azure CLI, de REST-API van Azure of de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="20382-297">**Azure tools**: Retrieve information from the activity log through Azure PowerShell, the Azure CLI, the Azure REST API, or the Azure portal.</span></span> <span data-ttu-id="20382-298">Stapsgewijze instructies voor elke methode zijn aangegeven in de [activiteit bewerkingen met Resource Manager](../azure-resource-manager/resource-group-audit.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="20382-298">Step-by-step instructions for each method are detailed in the [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="20382-299">**Power BI**: als u nog geen hebt een [Power BI](https://powerbi.microsoft.com/pricing) account, kunt u proberen deze gratis.</span><span class="sxs-lookup"><span data-stu-id="20382-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="20382-300">Met behulp van de [activiteitenlogboeken Azure pack voor Power BI inhoud](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), u kunt uw gegevens analyseren met vooraf geconfigureerde dashboards die u gebruiken kunt of aanpassen.</span><span class="sxs-lookup"><span data-stu-id="20382-300">By using the [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-the-access-performance-and-firewall-logs"></a><span data-ttu-id="20382-301">Weergeven en analyseren van de toegang, prestaties en firewall-Logboeken</span><span class="sxs-lookup"><span data-stu-id="20382-301">View and analyze the access, performance, and firewall logs</span></span>

<span data-ttu-id="20382-302">Azure [logboekanalyse](../log-analytics/log-analytics-azure-networking-analytics.md) kan de teller en de event log-bestanden verzamelen van uw Blob storage-account.</span><span class="sxs-lookup"><span data-stu-id="20382-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect the counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="20382-303">Dit omvat visualisaties en krachtige zoekmogelijkheden hebben voor het analyseren van uw Logboeken.</span><span class="sxs-lookup"><span data-stu-id="20382-303">It includes visualizations and powerful search capabilities to analyze your logs.</span></span>

<span data-ttu-id="20382-304">U kunt ook verbinding maken met uw opslagaccount en ophalen van de JSON-logboekvermeldingen voor toegang en prestaties van Logboeken.</span><span class="sxs-lookup"><span data-stu-id="20382-304">You can also connect to your storage account and retrieve the JSON log entries for access and performance logs.</span></span> <span data-ttu-id="20382-305">Nadat u de JSON-bestanden hebt gedownload, kunt u deze converteren naar CSV en ze weergeven in Excel, Power BI of een ander hulpprogramma voor de weergave van gegevens.</span><span class="sxs-lookup"><span data-stu-id="20382-305">After you download the JSON files, you can convert them to CSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="20382-306">Als u bekend met Visual Studio en de basisconcepten bent van het wijzigen van waarden voor de constanten en variabelen in C#, kunt u de [Meld converter extra](https://github.com/Azure-Samples/networking-dotnet-log-converter) beschikbaar is via GitHub.</span><span class="sxs-lookup"><span data-stu-id="20382-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="20382-307">Metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="20382-307">Metrics</span></span>

<span data-ttu-id="20382-308">Metrische gegevens zijn een functie voor bepaalde waar u prestatiemeteritems kunt bekijken in de portal voor Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="20382-308">Metrics are a feature for certain Azure resources where you can view performance counters in the portal.</span></span> <span data-ttu-id="20382-309">Voor Application Gateway is een waarde nu beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="20382-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="20382-310">Met deze metriek wordt de doorvoer en kunt u deze bekijken in de portal.</span><span class="sxs-lookup"><span data-stu-id="20382-310">This metric is throughput, and you can see it in the portal.</span></span> <span data-ttu-id="20382-311">Blader naar een application gateway en klikt u op **metrische gegevens**.</span><span class="sxs-lookup"><span data-stu-id="20382-311">Browse to an application gateway and click **Metrics**.</span></span> <span data-ttu-id="20382-312">Als u wilt weergeven van de waarden, selecteer doorvoer in de **beschikbare metrische gegevens** sectie.</span><span class="sxs-lookup"><span data-stu-id="20382-312">To view the values, select throughput in the **Available metrics** section.</span></span> <span data-ttu-id="20382-313">In de volgende afbeelding ziet u een voorbeeld met de filters die u kunt de gegevens worden weergegeven in andere bereiken.</span><span class="sxs-lookup"><span data-stu-id="20382-313">In the following image, you can see an example with the filters that you can use to display the data in different time ranges.</span></span>

![Metrische weergave met filters][5]

<span data-ttu-id="20382-315">Zie voor een actuele lijst met metrische gegevens [ondersteund met een Azure-Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="20382-315">To see a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="20382-316">Regels voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="20382-316">Alert rules</span></span>

<span data-ttu-id="20382-317">U kunt regels voor waarschuwingen op basis van de metrische gegevens voor een bron op te starten.</span><span class="sxs-lookup"><span data-stu-id="20382-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="20382-318">Bijvoorbeeld, een waarschuwing een webhook aanroepen of e-beheerder als de doorvoer van de toepassingsgateway boven, onder of met een drempelwaarde voor een opgegeven periode is.</span><span class="sxs-lookup"><span data-stu-id="20382-318">For example, an alert can call a webhook or email an administrator if the throughput of the application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="20382-319">Het volgende voorbeeld wordt u begeleid bij het maken van een waarschuwingsregel die een e-mailbericht naar een beheerder na schendingen van doorvoer een drempelwaarde verzendt:</span><span class="sxs-lookup"><span data-stu-id="20382-319">The following example walks you through creating an alert rule that sends an email to an administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="20382-320">Klik op **metrische waarschuwing toevoegen** openen de **regel toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="20382-320">Click **Add metric alert** to open the **Add rule** blade.</span></span> <span data-ttu-id="20382-321">U kunt ook deze blade van de metrische gegevens blade bereiken.</span><span class="sxs-lookup"><span data-stu-id="20382-321">You can also reach this blade from the metrics blade.</span></span>

   ![Knop 'Metrische waarschuwing toevoegen'][6]

2. <span data-ttu-id="20382-323">Op de **regel toevoegen** blade invullen van de naam van de voorwaarde, en secties melden en op **OK**.</span><span class="sxs-lookup"><span data-stu-id="20382-323">On the **Add rule** blade, fill out the name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="20382-324">In de **voorwaarde** selector, selecteert u een van de vier waarden: **groter is dan**, **groter dan of gelijk**, **minder dan**, of **kleiner dan of gelijk zijn aan**.</span><span class="sxs-lookup"><span data-stu-id="20382-324">In the **Condition** selector, select one of the four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="20382-325">In de **periode** selector, selecteert u een periode van 5 minuten en 6 uur.</span><span class="sxs-lookup"><span data-stu-id="20382-325">In the **Period** selector, select a period from 5 minutes to 6 hours.</span></span>

   * <span data-ttu-id="20382-326">Als u selecteert **e-eigenaren, bijdragers en lezers**, het e-mailbericht worden dynamisch op basis van de gebruikers die toegang tot deze resource hebben.</span><span class="sxs-lookup"><span data-stu-id="20382-326">If you select **Email owners, contributors, and readers**, the email can be dynamic based on the users who have access to that resource.</span></span> <span data-ttu-id="20382-327">Anders kunt u opgeven van een door komma's gescheiden lijst met gebruikers in de **aanvullende beheerder email(s)** vak.</span><span class="sxs-lookup"><span data-stu-id="20382-327">Otherwise, you can provide a comma-separated list of users in the **Additional administrator email(s)** box.</span></span>

   ![Blade regel toevoegen][7]

<span data-ttu-id="20382-329">Als de drempelwaarde wordt overschreden, ontvangt een e-mailbericht is vergelijkbaar met de structuur in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="20382-329">If the threshold is breached, an email that's similar to the one in the following image arrives:</span></span>

![E-mailadres voor geschonden drempelwaarde][8]

<span data-ttu-id="20382-331">Een lijst met waarschuwingen wordt weergegeven nadat u een waarschuwing voor een metriek maken.</span><span class="sxs-lookup"><span data-stu-id="20382-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="20382-332">Deze biedt een overzicht van alle regels voor waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="20382-332">It provides an overview of all the alert rules.</span></span>

![Lijst met waarschuwingen en regels][9]

<span data-ttu-id="20382-334">Zie voor meer informatie over waarschuwingsmeldingen, [meldingen van waarschuwingen ontvangen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="20382-334">To learn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="20382-335">Voor meer informatie over webhooks en hoe u ze kunt gebruiken met waarschuwingen, gaat u naar [een webhook configureren op een Azure metrische waarschuwing](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="20382-335">To understand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="20382-336">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="20382-336">Next steps</span></span>

* <span data-ttu-id="20382-337">Teller en de gebeurtenislogboeken visualiseren met behulp van [logboekanalyse](../log-analytics/log-analytics-azure-networking-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="20382-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="20382-338">[Uw Azure activiteitenlogboek met Power BI visualiseren](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blogbericht.</span><span class="sxs-lookup"><span data-stu-id="20382-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="20382-339">[Weergeven en analyseren van Azure activiteitenlogboeken in Power BI en meer](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blogbericht.</span><span class="sxs-lookup"><span data-stu-id="20382-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png

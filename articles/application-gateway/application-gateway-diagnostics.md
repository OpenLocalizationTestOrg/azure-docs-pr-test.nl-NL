---
title: aaaMonitor toegang tot logboeken, Prestatielogboeken, back-end-status en metrische gegevens voor de toepassingsgateway | Microsoft Docs
description: Meer informatie over hoe tooenable en beheren van toegang en Prestatielogboeken voor Application Gateway
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
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="d4210-103">Back-end-status, diagnostische logboeken en metrische gegevens voor Application Gateway</span><span class="sxs-lookup"><span data-stu-id="d4210-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="d4210-104">U kunt de bronnen in de volgende manieren Hallo bewaken met behulp van Azure Application Gateway:</span><span class="sxs-lookup"><span data-stu-id="d4210-104">By using Azure Application Gateway, you can monitor resources in hello following ways:</span></span>

* <span data-ttu-id="d4210-105">[Status van de back-end](#back-end-health): Application Gateway biedt Hallo mogelijkheid toomonitor Hallo status van servers in Hallo Hallo back-end-adresgroepen via hello Azure-portal en via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4210-105">[Back-end health](#back-end-health): Application Gateway provides hello capability toomonitor hello health of hello servers in hello back-end pools through hello Azure portal and through PowerShell.</span></span> <span data-ttu-id="d4210-106">U vindt ook Hallo status van de back-end-adresgroepen Hallo via Hallo prestaties diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="d4210-106">You can also find hello health of hello back-end pools through hello performance diagnostic logs.</span></span>

* <span data-ttu-id="d4210-107">[Logboeken](#diagnostic-logs): Logboeken toestaan voor toegang, prestaties en andere gegevens toobe opgeslagen of gebruikt van een resource voor controledoeleinden.</span><span class="sxs-lookup"><span data-stu-id="d4210-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data toobe saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="d4210-108">[Metrische gegevens](#metrics): Application Gateway is momenteel een waarde.</span><span class="sxs-lookup"><span data-stu-id="d4210-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="d4210-109">Met deze metriek meet Hallo doorvoer van de toepassingsgateway Hallo in bytes per seconde.</span><span class="sxs-lookup"><span data-stu-id="d4210-109">This metric measures hello throughput of hello application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="d4210-110">Back-end-status</span><span class="sxs-lookup"><span data-stu-id="d4210-110">Back-end health</span></span>

<span data-ttu-id="d4210-111">Toepassingsgateway biedt Hallo mogelijkheid toomonitor Hallo status van afzonderlijke onderdelen van de back-end-adresgroepen Hallo via Hallo-portal, PowerShell en Hallo-opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="d4210-111">Application Gateway provides hello capability toomonitor hello health of individual members of hello back-end pools through hello portal, PowerShell, and hello command-line interface (CLI).</span></span> <span data-ttu-id="d4210-112">U kunt ook een geaggregeerde status vinden samenvatting van back-end-adresgroepen via Hallo prestaties diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="d4210-112">You can also find an aggregated health summary of back-end pools through hello performance diagnostic logs.</span></span> 

<span data-ttu-id="d4210-113">back-end-statusrapport Hallo weerspiegelt Hallo-uitvoer van Hallo Application Gateway health test toohello back-end-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="d4210-113">hello back-end health report reflects hello output of hello Application Gateway health probe toohello back-end instances.</span></span> <span data-ttu-id="d4210-114">Als scannen is voltooid en Hallo terug end kan verkeer ontvangen, als in orde wordt beschouwd.</span><span class="sxs-lookup"><span data-stu-id="d4210-114">When probing is successful and hello back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="d4210-115">Anders wordt deze orde beschouwd.</span><span class="sxs-lookup"><span data-stu-id="d4210-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4210-116">Als er een netwerkbeveiligingsgroep (NSG) op een Application Gateway-subnet, opent u poortbereiken 65503 65534 op Hallo Application Gateway-subnet voor binnenkomend verkeer.</span><span class="sxs-lookup"><span data-stu-id="d4210-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on hello Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="d4210-117">Deze poorten zijn vereist voor Hallo back-end health API toowork.</span><span class="sxs-lookup"><span data-stu-id="d4210-117">These ports are required for hello back-end health API toowork.</span></span>


### <a name="view-back-end-health-through-hello-portal"></a><span data-ttu-id="d4210-118">Status van de back-end via de portal Hallo weergeven</span><span class="sxs-lookup"><span data-stu-id="d4210-118">View back-end health through hello portal</span></span>

<span data-ttu-id="d4210-119">In de portal Hallo back-end health automatisch opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d4210-119">In hello portal, back-end health is provided automatically.</span></span> <span data-ttu-id="d4210-120">Selecteer in een bestaande toepassingsgateway **bewaking** > **back-end health**.</span><span class="sxs-lookup"><span data-stu-id="d4210-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="d4210-121">Elk lid in Hallo back-endpool wordt vermeld op deze pagina (of het is een NIC, IP of FQDN).</span><span class="sxs-lookup"><span data-stu-id="d4210-121">Each member in hello back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="d4210-122">De naam van de back-endpool, poort, HTTP-instellingen voor de naam van back-end en gezondheidsstatus worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d4210-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="d4210-123">Geldige waarden voor gezondheidsstatus zijn **goed**, **niet in orde**, en **onbekende**.</span><span class="sxs-lookup"><span data-stu-id="d4210-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="d4210-124">Als er een back-end-gezondheidsstatus van **onbekende**, zorg ervoor dat toegang toohello back-end niet wordt geblokkeerd door een regel voor het NSG, een door de gebruiker opgegeven routes (UDR) of een aangepaste DNS-server in het virtuele netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="d4210-124">If you see a back-end health status of **Unknown**, ensure that access toohello back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in hello virtual network.</span></span>

![Back-end-status][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="d4210-126">Status van de back-end via PowerShell weergeven</span><span class="sxs-lookup"><span data-stu-id="d4210-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="d4210-127">Hallo volgende PowerShell-code toont hoe tooview back-end health met behulp van Hallo `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d4210-127">hello following PowerShell code shows how tooview back-end health by using hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="d4210-128">Status van de back-end via Azure CLI 2.0 weergeven</span><span class="sxs-lookup"><span data-stu-id="d4210-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="d4210-129">Resultaten</span><span class="sxs-lookup"><span data-stu-id="d4210-129">Results</span></span>

<span data-ttu-id="d4210-130">Hallo volgende fragment toont een voorbeeld van antwoord Hallo:</span><span class="sxs-lookup"><span data-stu-id="d4210-130">hello following snippet shows an example of hello response:</span></span>

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

## <span data-ttu-id="d4210-131"><a name="diagnostic-logging"></a>Diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="d4210-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="d4210-132">U kunt verschillende typen Logboeken gebruiken in Azure toomanage en toepassingsgateways oplossen.</span><span class="sxs-lookup"><span data-stu-id="d4210-132">You can use different types of logs in Azure toomanage and troubleshoot application gateways.</span></span> <span data-ttu-id="d4210-133">U kunt toegang tot sommige van deze logboeken via Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="d4210-133">You can access some of these logs through hello portal.</span></span> <span data-ttu-id="d4210-134">Alle logboeken kunnen worden opgehaald uit Azure Blob storage en weergegeven in de verschillende hulpprogramma's, zoals [logboekanalyse](../log-analytics/log-analytics-azure-networking-analytics.md), Excel en Power BI.</span><span class="sxs-lookup"><span data-stu-id="d4210-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="d4210-135">U kunt meer informatie over Hallo verschillende typen logboeken van Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="d4210-135">You can learn more about hello different types of logs from hello following list:</span></span>

* <span data-ttu-id="d4210-136">**Activiteitenlogboek**: U kunt [Azure activiteitenlogboeken](../monitoring-and-diagnostics/insights-debugging-with-events.md) (voorheen bekend als operationele logboeken en controlelogboeken) tooview alle bewerkingen die zijn ingediend tooyour Azure-abonnement en hun status.</span><span class="sxs-lookup"><span data-stu-id="d4210-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) tooview all operations that are submitted tooyour Azure subscription, and their status.</span></span> <span data-ttu-id="d4210-137">Logboekvermeldingen activiteit worden standaard verzameld en u kunt ze weergeven in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d4210-137">Activity log entries are collected by default, and you can view them in hello Azure portal.</span></span>
* <span data-ttu-id="d4210-138">**Toegangslogboek**: U kunt gebruikmaken van deze patronen logboek tooview Application Gateway toegang en belangrijke informatie, inclusief Hallo aanroeper IP aangevraagde URL, antwoord latentie, retourcode en bytes in en uit analyseren. Een toegangslogboek verzameld om de 300 seconden.</span><span class="sxs-lookup"><span data-stu-id="d4210-138">**Access log**: You can use this log tooview Application Gateway access patterns and analyze important information, including hello caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="d4210-139">Dit logboek bevat één record per exemplaar van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="d4210-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="d4210-140">Hallo Application Gateway-exemplaar kan worden geïdentificeerd door de eigenschap instanceId Hallo.</span><span class="sxs-lookup"><span data-stu-id="d4210-140">hello Application Gateway instance can be identified by hello instanceId property.</span></span>
* <span data-ttu-id="d4210-141">**Prestatielogboek**: U kunt dit logboek tooview hoe Application Gateway-exemplaren uitvoert.</span><span class="sxs-lookup"><span data-stu-id="d4210-141">**Performance log**: You can use this log tooview how Application Gateway instances are performing.</span></span> <span data-ttu-id="d4210-142">Dit logboek bevat informatie over de prestaties voor elk exemplaar, met inbegrip van totaal aantal aanvragen die worden geleverd, doorvoer in bytes, totaal aantal aanvragen dat wordt geleverd, aantal mislukte aanvragen en in orde en slecht backend-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="d4210-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="d4210-143">Een prestatielogboek worden verzameld om de 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="d4210-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="d4210-144">**Firewall-logboek**: U kunt dit logboek tooview Hallo aanvragen die zijn geregistreerd via de modus voor detectie of ter voorkoming van een toepassingsgateway die is geconfigureerd met Hallo web application firewall.</span><span class="sxs-lookup"><span data-stu-id="d4210-144">**Firewall log**: You can use this log tooview hello requests that are logged through either detection or prevention mode of an application gateway that is configured with hello web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="d4210-145">Logboeken zijn alleen beschikbaar voor resources geïmplementeerd in hello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="d4210-145">Logs are available only for resources deployed in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="d4210-146">U kunt Logboeken niet gebruiken voor bronnen in het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="d4210-146">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="d4210-147">Zie voor een beter begrip van Hallo twee modellen, Hallo [Understanding Resource Manager-implementatie en klassieke implementatie](../azure-resource-manager/resource-manager-deployment-model.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="d4210-147">For a better understanding of hello two models, see hello [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="d4210-148">Hebt u drie opties voor het opslaan van uw logboeken:</span><span class="sxs-lookup"><span data-stu-id="d4210-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="d4210-149">**Storage-account**: Storage-accounts beste kunnen worden gebruikt voor Logboeken wanneer logboeken worden opgeslagen voor een langere duur en gelezen wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="d4210-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="d4210-150">**Event hubs**: Event hubs zijn een goede optie voor het integreren met andere informatie over beveiliging en beheer van gebeurtenissen (SEIM) hulpprogramma's tooget waarschuwingen op uw resources.</span><span class="sxs-lookup"><span data-stu-id="d4210-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools tooget alerts on your resources.</span></span>
* <span data-ttu-id="d4210-151">**Meld u Analytics**: Log Analytics is het meest geschikt voor algemene realtime-controle van uw toepassing of trends kijken.</span><span class="sxs-lookup"><span data-stu-id="d4210-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="d4210-152">Schakel logboekregistratie in via PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4210-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="d4210-153">Activiteit-logboekregistratie is standaard ingeschakeld voor elke Resource Manager-resource.</span><span class="sxs-lookup"><span data-stu-id="d4210-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="d4210-154">U moet toegang en prestaties logboekregistratie toostart Hallo gegevens beschikbaar zijn via deze logboeken verzamelt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d4210-154">You must enable access and performance logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="d4210-155">tooenable logboekregistratie van gebruik Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d4210-155">tooenable logging, use hello following steps:</span></span>

1. <span data-ttu-id="d4210-156">Houd er rekening mee uw storage-account resource-ID, waar Hallo logboekgegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d4210-156">Note your storage account's resource ID, where hello log data is stored.</span></span> <span data-ttu-id="d4210-157">Deze waarde is van het formulier Hallo: /subscriptions/\<subscriptionId\>/resourceGroups/\<Resourcegroepnaam\>/providers/Microsoft.Storage/storageAccounts/\<opslagaccountnaam\>.</span><span class="sxs-lookup"><span data-stu-id="d4210-157">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="d4210-158">U kunt opslagaccount gebruiken in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="d4210-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="d4210-159">U kunt deze informatie hello Azure portal toofind.</span><span class="sxs-lookup"><span data-stu-id="d4210-159">You can use hello Azure portal toofind this information.</span></span>

    ![Portal: resource-ID voor het opslagaccount](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="d4210-161">Houd er rekening mee resource-ID van de toepassingsgateway van uw waarvoor logboekregistratie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d4210-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="d4210-162">Deze waarde is van het formulier Hallo: /subscriptions/\<subscriptionId\>/resourceGroups/\<Resourcegroepnaam\>/providers/Microsoft.Network/applicationGateways/\<toepassingsgateway naam\>.</span><span class="sxs-lookup"><span data-stu-id="d4210-162">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="d4210-163">U kunt deze informatie Hallo portal toofind.</span><span class="sxs-lookup"><span data-stu-id="d4210-163">You can use hello portal toofind this information.</span></span>

    ![Portal: resource-ID voor de toepassingsgateway](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="d4210-165">Diagnostische logboekregistratie inschakelen met behulp van de volgende PowerShell-cmdlet Hallo:</span><span class="sxs-lookup"><span data-stu-id="d4210-165">Enable diagnostic logging by using hello following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="d4210-166">Activiteitenlogboeken vereisen een afzonderlijke opslagaccount niet.</span><span class="sxs-lookup"><span data-stu-id="d4210-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="d4210-167">Hallo gebruik van opslag voor toegang en prestatieregistratie leidt ertoe dat de kosten.</span><span class="sxs-lookup"><span data-stu-id="d4210-167">hello use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-hello-azure-portal"></a><span data-ttu-id="d4210-168">Inschakelen van logboekregistratie via hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="d4210-168">Enable logging through hello Azure portal</span></span>

1. <span data-ttu-id="d4210-169">In hello Azure-portal, zoek de bron en klik op **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="d4210-169">In hello Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="d4210-170">Er zijn drie logboeken beschikbaar voor Application Gateway:</span><span class="sxs-lookup"><span data-stu-id="d4210-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="d4210-171">Toegangslogboek</span><span class="sxs-lookup"><span data-stu-id="d4210-171">Access log</span></span>
   * <span data-ttu-id="d4210-172">Prestatielogboek</span><span class="sxs-lookup"><span data-stu-id="d4210-172">Performance log</span></span>
   * <span data-ttu-id="d4210-173">Firewall-logboek</span><span class="sxs-lookup"><span data-stu-id="d4210-173">Firewall log</span></span>

2. <span data-ttu-id="d4210-174">toostart verzamelen van gegevens, klikt u op **diagnostische gegevens inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="d4210-174">toostart collecting data, click **Turn on diagnostics**.</span></span>

   ![Diagnostische gegevens inschakelen][1]

3. <span data-ttu-id="d4210-176">Hallo **diagnostische instellingen** blade biedt Hallo-instellingen voor Hallo diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="d4210-176">hello **Diagnostics settings** blade provides hello settings for hello diagnostic logs.</span></span> <span data-ttu-id="d4210-177">In dit voorbeeld Slaat logboekanalyse Hallo Logboeken.</span><span class="sxs-lookup"><span data-stu-id="d4210-177">In this example, Log Analytics stores hello logs.</span></span> <span data-ttu-id="d4210-178">Klik op **configureren** onder **logboekanalyse** tooconfigure uw werkruimte.</span><span class="sxs-lookup"><span data-stu-id="d4210-178">Click **Configure** under **Log Analytics** tooconfigure your workspace.</span></span> <span data-ttu-id="d4210-179">U kunt ook event hubs en een storage account toosave Hallo diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="d4210-179">You can also use event hubs and a storage account toosave hello diagnostic logs.</span></span>

   ![Hallo configuratieproces wordt gestart][2]

4. <span data-ttu-id="d4210-181">Kies een bestaande werkruimte van Operations Management Suite (OMS) of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="d4210-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="d4210-182">In dit voorbeeld wordt een bestaande.</span><span class="sxs-lookup"><span data-stu-id="d4210-182">This example uses an existing one.</span></span>

   ![Opties voor OMS werkruimten][3]

5. <span data-ttu-id="d4210-184">Hallo-instellingen bevestigen en klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d4210-184">Confirm hello settings and click **Save**.</span></span>

   ![Diagnostische instellingenblade met selecties][4]

### <a name="activity-log"></a><span data-ttu-id="d4210-186">Activiteitenlogboek</span><span class="sxs-lookup"><span data-stu-id="d4210-186">Activity log</span></span>

<span data-ttu-id="d4210-187">Activiteitenlogboek hello Azure genereert standaard.</span><span class="sxs-lookup"><span data-stu-id="d4210-187">Azure generates hello activity log by default.</span></span> <span data-ttu-id="d4210-188">Hallo-logboeken worden bewaard gedurende 90 dagen in hello Azure gebeurtenislogboeken store.</span><span class="sxs-lookup"><span data-stu-id="d4210-188">hello logs are preserved for 90 days in hello Azure event logs store.</span></span> <span data-ttu-id="d4210-189">Meer informatie over deze logboeken door te lezen Hallo [weergeven van gebeurtenissen en het activiteitenlogboek](../monitoring-and-diagnostics/insights-debugging-with-events.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="d4210-189">Learn more about these logs by reading hello [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="d4210-190">Toegangslogboek</span><span class="sxs-lookup"><span data-stu-id="d4210-190">Access log</span></span>

<span data-ttu-id="d4210-191">Hallo toegangslogboek is gegenereerd, alleen als u deze op elk exemplaar van de toepassingsgateway, zoals beschreven in de vorige stappen Hallo hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d4210-191">hello access log is generated only if you've enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="d4210-192">Hallo-gegevens worden opgeslagen in Hallo storage-account die u hebt opgegeven dat wanneer u Hallo-logboekregistratie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d4210-192">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="d4210-193">Elke toegang van Application Gateway wordt geregistreerd in JSON-indeling, zoals wordt weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="d4210-193">Each access of Application Gateway is logged in JSON format, as shown in hello following example:</span></span>


|<span data-ttu-id="d4210-194">Waarde</span><span class="sxs-lookup"><span data-stu-id="d4210-194">Value</span></span>  |<span data-ttu-id="d4210-195">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d4210-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="d4210-196">Exemplaar-id</span><span class="sxs-lookup"><span data-stu-id="d4210-196">instanceId</span></span>     | <span data-ttu-id="d4210-197">Toepassingsgateway die aanvraag aangeboden Hallo-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="d4210-197">Application Gateway instance that served hello request.</span></span>        |
|<span data-ttu-id="d4210-198">client-IP</span><span class="sxs-lookup"><span data-stu-id="d4210-198">clientIP</span></span>     | <span data-ttu-id="d4210-199">Oorspronkelijke IP-adres voor Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d4210-199">Originating IP for hello request.</span></span>        |
|<span data-ttu-id="d4210-200">enterpriseclient</span><span class="sxs-lookup"><span data-stu-id="d4210-200">clientPort</span></span>     | <span data-ttu-id="d4210-201">Oorspronkelijke poort voor het Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d4210-201">Originating port for hello request.</span></span>       |
|<span data-ttu-id="d4210-202">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="d4210-202">httpMethod</span></span>     | <span data-ttu-id="d4210-203">HTTP-methode die wordt gebruikt door het Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d4210-203">HTTP method used by hello request.</span></span>       |
|<span data-ttu-id="d4210-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="d4210-204">requestUri</span></span>     | <span data-ttu-id="d4210-205">URI van Hallo-aanvraag ontvangen.</span><span class="sxs-lookup"><span data-stu-id="d4210-205">URI of hello received request.</span></span>        |
|<span data-ttu-id="d4210-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="d4210-206">RequestQuery</span></span>     | <span data-ttu-id="d4210-207">**Server-gerouteerd**: Back-end-pool-exemplaar dat Hallo-aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="d4210-207">**Server-Routed**: Back-end pool instance that was sent hello request.</span></span> </br> <span data-ttu-id="d4210-208">**X-AzureApplicationGateway-logboek-ID**: correlatie-ID Hallo aanvraag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d4210-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for hello request.</span></span> <span data-ttu-id="d4210-209">Het kan gebruikte tootroubleshoot verkeer problemen op Hallo back-endservers zijn.</span><span class="sxs-lookup"><span data-stu-id="d4210-209">It can be used tootroubleshoot traffic issues on hello back-end servers.</span></span> </br><span data-ttu-id="d4210-210">**STATUS van de SERVER**: HTTP-antwoordcode Application Gateway van Hallo back-end ontvangen.</span><span class="sxs-lookup"><span data-stu-id="d4210-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from hello back end.</span></span>       |
|<span data-ttu-id="d4210-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="d4210-211">UserAgent</span></span>     | <span data-ttu-id="d4210-212">De gebruikersagent van Hallo HTTP-aanvraag-header.</span><span class="sxs-lookup"><span data-stu-id="d4210-212">User agent from hello HTTP request header.</span></span>        |
|<span data-ttu-id="d4210-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="d4210-213">httpStatus</span></span>     | <span data-ttu-id="d4210-214">HTTP-statuscode geretourneerd toohello client Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="d4210-214">HTTP status code returned toohello client from Application Gateway.</span></span>       |
|<span data-ttu-id="d4210-215">Httpversie</span><span class="sxs-lookup"><span data-stu-id="d4210-215">httpVersion</span></span>     | <span data-ttu-id="d4210-216">HTTP-versie van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d4210-216">HTTP version of hello request.</span></span>        |
|<span data-ttu-id="d4210-217">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="d4210-217">receivedBytes</span></span>     | <span data-ttu-id="d4210-218">Grootte van het pakket ontvangen in bytes.</span><span class="sxs-lookup"><span data-stu-id="d4210-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="d4210-219">SentBytes</span><span class="sxs-lookup"><span data-stu-id="d4210-219">sentBytes</span></span>| <span data-ttu-id="d4210-220">Grootte van het pakket dat is verzonden, in bytes.</span><span class="sxs-lookup"><span data-stu-id="d4210-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="d4210-221">timeTaken</span><span class="sxs-lookup"><span data-stu-id="d4210-221">timeTaken</span></span>| <span data-ttu-id="d4210-222">Totale tijdsduur (in milliseconden) die het duurt voordat een aanvraag toobe verwerkt en de antwoord-toobe verzonden.</span><span class="sxs-lookup"><span data-stu-id="d4210-222">Length of time (in milliseconds) that it takes for a request toobe processed and its response toobe sent.</span></span> <span data-ttu-id="d4210-223">Dit wordt berekend als hello-interval van Hallo tijd wanneer de toepassingsgateway Hallo eerste byte van een HTTP-aanvraag toohello tijd wanneer de bewerking is voltooid voor het verzenden van antwoord Hallo ontvangt.</span><span class="sxs-lookup"><span data-stu-id="d4210-223">This is calculated as hello interval from hello time when Application Gateway receives hello first byte of an HTTP request toohello time when hello response send operation finishes.</span></span> <span data-ttu-id="d4210-224">Het is belangrijk toonote die meestal tijd veld Hallo Hallo tijd Hallo-aanvraag en antwoord-pakketten worden overgebracht via Hallo netwerk bevat.</span><span class="sxs-lookup"><span data-stu-id="d4210-224">It's important toonote that hello Time-Taken field usually includes hello time that hello request and response packets are traveling over hello network.</span></span> |
|<span data-ttu-id="d4210-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="d4210-225">sslEnabled</span></span>| <span data-ttu-id="d4210-226">Hiermee wordt aangegeven of communicatie toohello back-end-adresgroepen SSL gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d4210-226">Whether communication toohello back-end pools used SSL.</span></span> <span data-ttu-id="d4210-227">Geldige waarden zijn in- of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="d4210-227">Valid values are on and off.</span></span>|
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

### <a name="performance-log"></a><span data-ttu-id="d4210-228">Prestatielogboek</span><span class="sxs-lookup"><span data-stu-id="d4210-228">Performance log</span></span>

<span data-ttu-id="d4210-229">Hallo prestatielogboek wordt alleen gegenereerd als u deze hebt ingeschakeld op elk exemplaar van de toepassingsgateway, zoals beschreven in de vorige stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="d4210-229">hello performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="d4210-230">Hallo-gegevens worden opgeslagen in Hallo storage-account die u hebt opgegeven dat wanneer u Hallo-logboekregistratie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d4210-230">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="d4210-231">Hallo prestatielogboekgegevens wordt gegenereerd met intervallen van 1 minuut.</span><span class="sxs-lookup"><span data-stu-id="d4210-231">hello performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="d4210-232">Hallo volgt gegevens worden geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="d4210-232">hello following data is logged:</span></span>


|<span data-ttu-id="d4210-233">Waarde</span><span class="sxs-lookup"><span data-stu-id="d4210-233">Value</span></span>  |<span data-ttu-id="d4210-234">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d4210-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="d4210-235">Exemplaar-id</span><span class="sxs-lookup"><span data-stu-id="d4210-235">instanceId</span></span>     |  <span data-ttu-id="d4210-236">Application Gateway-exemplaren waarvoor gegevens wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d4210-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="d4210-237">Er is een rij per exemplaar voor een toepassingsgateway met meerdere-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="d4210-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="d4210-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="d4210-238">healthyHostCount</span></span>     | <span data-ttu-id="d4210-239">Het aantal orde hosts in Hallo back-endpool.</span><span class="sxs-lookup"><span data-stu-id="d4210-239">Number of healthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="d4210-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="d4210-240">unHealthyHostCount</span></span>     | <span data-ttu-id="d4210-241">Het aantal beschadigde hosts in Hallo back-endpool.</span><span class="sxs-lookup"><span data-stu-id="d4210-241">Number of unhealthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="d4210-242">requestCount</span><span class="sxs-lookup"><span data-stu-id="d4210-242">requestCount</span></span>     | <span data-ttu-id="d4210-243">Het aantal geleverde aanvragen.</span><span class="sxs-lookup"><span data-stu-id="d4210-243">Number of requests served.</span></span>        |
|<span data-ttu-id="d4210-244">Latentie</span><span class="sxs-lookup"><span data-stu-id="d4210-244">latency</span></span> | <span data-ttu-id="d4210-245">Latentie (in milliseconden) van aanvragen van Hallo exemplaar toohello back-end die Hallo aanvragen fungeert.</span><span class="sxs-lookup"><span data-stu-id="d4210-245">Latency (in milliseconds) of requests from hello instance toohello back end that serves hello requests.</span></span> |
|<span data-ttu-id="d4210-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="d4210-246">failedRequestCount</span></span>| <span data-ttu-id="d4210-247">Het aantal mislukte aanvragen.</span><span class="sxs-lookup"><span data-stu-id="d4210-247">Number of failed requests.</span></span>|
|<span data-ttu-id="d4210-248">Doorvoer</span><span class="sxs-lookup"><span data-stu-id="d4210-248">throughput</span></span>| <span data-ttu-id="d4210-249">Gemiddelde doorvoersnelheid sinds de laatste logboek hello, gemeten in bytes per seconde.</span><span class="sxs-lookup"><span data-stu-id="d4210-249">Average throughput since hello last log, measured in bytes per second.</span></span>|

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
> <span data-ttu-id="d4210-250">Latentie wordt berekend door Hallo tijd wanneer de eerste byte Hallo van Hallo HTTP-aanvraag is ontvangen toohello tijd wanneer de laatste byte Hallo Hallo HTTP-antwoord wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="d4210-250">Latency is calculated from hello time when hello first byte of hello HTTP request is received toohello time when hello last byte of hello HTTP response is sent.</span></span> <span data-ttu-id="d4210-251">De Hallo som van de toepassingsgateway verwerkingstijd Hallo plus hello netwerk kosten toohello terug beëindigen, plus Hallo hoelang back-end vergt tooprocess Hallo aanvraag Hallo.</span><span class="sxs-lookup"><span data-stu-id="d4210-251">It's hello sum of hello Application Gateway processing time plus hello network cost toohello back end, plus hello time that hello back end takes tooprocess hello request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="d4210-252">Firewall-logboek</span><span class="sxs-lookup"><span data-stu-id="d4210-252">Firewall log</span></span>

<span data-ttu-id="d4210-253">Hallo firewall-logboek is gegenereerd alleen als u deze hebt ingeschakeld voor elke application gateway, zoals beschreven in de vorige stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="d4210-253">hello firewall log is generated only if you have enabled it for each application gateway, as detailed in hello preceding steps.</span></span> <span data-ttu-id="d4210-254">Dit logboek is ook vereist dat deze Hallo web application firewall op een application gateway is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d4210-254">This log also requires that hello web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="d4210-255">Hallo-gegevens worden opgeslagen in Hallo storage-account die u hebt opgegeven dat wanneer u Hallo-logboekregistratie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d4210-255">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="d4210-256">Hallo volgt gegevens worden geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="d4210-256">hello following data is logged:</span></span>


|<span data-ttu-id="d4210-257">Waarde</span><span class="sxs-lookup"><span data-stu-id="d4210-257">Value</span></span>  |<span data-ttu-id="d4210-258">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d4210-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="d4210-259">Exemplaar-id</span><span class="sxs-lookup"><span data-stu-id="d4210-259">instanceId</span></span>     | <span data-ttu-id="d4210-260">Gateway toepassingsexemplaar voor welke firewall worden gegevens gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d4210-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="d4210-261">Er is een rij per exemplaar voor een toepassingsgateway met meerdere-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="d4210-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="d4210-262">client-IP</span><span class="sxs-lookup"><span data-stu-id="d4210-262">clientIp</span></span>     |   <span data-ttu-id="d4210-263">Oorspronkelijke IP-adres voor Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d4210-263">Originating IP for hello request.</span></span>      |
|<span data-ttu-id="d4210-264">enterpriseclient</span><span class="sxs-lookup"><span data-stu-id="d4210-264">clientPort</span></span>     |  <span data-ttu-id="d4210-265">Oorspronkelijke poort voor het Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d4210-265">Originating port for hello request.</span></span>       |
|<span data-ttu-id="d4210-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="d4210-266">requestUri</span></span>     | <span data-ttu-id="d4210-267">URL van het Hallo-aanvraag ontvangen.</span><span class="sxs-lookup"><span data-stu-id="d4210-267">URL of hello received request.</span></span>       |
|<span data-ttu-id="d4210-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="d4210-268">ruleSetType</span></span>     | <span data-ttu-id="d4210-269">Type van de regelset.</span><span class="sxs-lookup"><span data-stu-id="d4210-269">Rule set type.</span></span> <span data-ttu-id="d4210-270">Hallo beschikbare waarde is OWASP.</span><span class="sxs-lookup"><span data-stu-id="d4210-270">hello available value is OWASP.</span></span>        |
|<span data-ttu-id="d4210-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="d4210-271">ruleSetVersion</span></span>     | <span data-ttu-id="d4210-272">Regelset versie die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d4210-272">Rule set version used.</span></span> <span data-ttu-id="d4210-273">Beschikbare waarden zijn 2.2.9 en 3.0.</span><span class="sxs-lookup"><span data-stu-id="d4210-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="d4210-274">ruleId</span><span class="sxs-lookup"><span data-stu-id="d4210-274">ruleId</span></span>     | <span data-ttu-id="d4210-275">Regel-ID van Hallo gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="d4210-275">Rule ID of hello triggering event.</span></span>        |
|<span data-ttu-id="d4210-276">Bericht</span><span class="sxs-lookup"><span data-stu-id="d4210-276">message</span></span>     | <span data-ttu-id="d4210-277">Gebruiksvriendelijke bericht voor Hallo gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="d4210-277">User-friendly message for hello triggering event.</span></span> <span data-ttu-id="d4210-278">Meer informatie vindt u in de sectie details Hallo.</span><span class="sxs-lookup"><span data-stu-id="d4210-278">More details are provided in hello details section.</span></span>        |
|<span data-ttu-id="d4210-279">Actie</span><span class="sxs-lookup"><span data-stu-id="d4210-279">action</span></span>     |  <span data-ttu-id="d4210-280">Actie op die op het Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d4210-280">Action taken on hello request.</span></span> <span data-ttu-id="d4210-281">Beschikbare waarden zijn geblokkeerd en toegestaan.</span><span class="sxs-lookup"><span data-stu-id="d4210-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="d4210-282">Site</span><span class="sxs-lookup"><span data-stu-id="d4210-282">site</span></span>     | <span data-ttu-id="d4210-283">De site voor welke Hallo logboek is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d4210-283">Site for which hello log was generated.</span></span> <span data-ttu-id="d4210-284">Alleen globale wordt momenteel, omdat er regels zijn globale vermeld.</span><span class="sxs-lookup"><span data-stu-id="d4210-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="d4210-285">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="d4210-285">details</span></span>     | <span data-ttu-id="d4210-286">Details van gebeurtenis Hallo.</span><span class="sxs-lookup"><span data-stu-id="d4210-286">Details of hello triggering event.</span></span>        |
|<span data-ttu-id="d4210-287">Details.Message</span><span class="sxs-lookup"><span data-stu-id="d4210-287">details.message</span></span>     | <span data-ttu-id="d4210-288">Beschrijving van regel Hallo.</span><span class="sxs-lookup"><span data-stu-id="d4210-288">Description of hello rule.</span></span>        |
|<span data-ttu-id="d4210-289">Details.Data</span><span class="sxs-lookup"><span data-stu-id="d4210-289">details.data</span></span>     | <span data-ttu-id="d4210-290">Specifieke gegevens gevonden in de aanvraag die overeenkomende Hallo-regel.</span><span class="sxs-lookup"><span data-stu-id="d4210-290">Specific data found in request that matched hello rule.</span></span>         |
|<span data-ttu-id="d4210-291">Details.File</span><span class="sxs-lookup"><span data-stu-id="d4210-291">details.file</span></span>     | <span data-ttu-id="d4210-292">Configuratiebestand die Hallo regel opgenomen.</span><span class="sxs-lookup"><span data-stu-id="d4210-292">Configuration file that contained hello rule.</span></span>        |
|<span data-ttu-id="d4210-293">Details.line</span><span class="sxs-lookup"><span data-stu-id="d4210-293">details.line</span></span>     | <span data-ttu-id="d4210-294">Regelnummer in Hallo-configuratiebestand dat Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="d4210-294">Line number in hello configuration file that triggered hello event.</span></span>       |

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

### <a name="view-and-analyze-hello-activity-log"></a><span data-ttu-id="d4210-295">Weergeven en analyseren van Hallo activiteitenlogboek</span><span class="sxs-lookup"><span data-stu-id="d4210-295">View and analyze hello activity log</span></span>

<span data-ttu-id="d4210-296">U kunt weergeven en analyseren van logboekgegevens van de activiteit met behulp van de volgende methoden Hallo:</span><span class="sxs-lookup"><span data-stu-id="d4210-296">You can view and analyze activity log data by using any of hello following methods:</span></span>

* <span data-ttu-id="d4210-297">**Azure-hulpprogramma's**: gegevens ophalen uit Hallo activiteitenlogboek via Azure PowerShell, Hallo Hallo REST-API van Azure, Azure CLI of hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d4210-297">**Azure tools**: Retrieve information from hello activity log through Azure PowerShell, hello Azure CLI, hello Azure REST API, or hello Azure portal.</span></span> <span data-ttu-id="d4210-298">Stapsgewijze instructies voor elke methode zijn aangegeven in Hallo [activiteit bewerkingen met Resource Manager](../azure-resource-manager/resource-group-audit.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="d4210-298">Step-by-step instructions for each method are detailed in hello [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="d4210-299">**Power BI**: als u nog geen hebt een [Power BI](https://powerbi.microsoft.com/pricing) account, kunt u proberen deze gratis.</span><span class="sxs-lookup"><span data-stu-id="d4210-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="d4210-300">Met behulp van Hallo [activiteitenlogboeken Azure pack voor Power BI inhoud](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), u kunt uw gegevens analyseren met vooraf geconfigureerde dashboards die u gebruiken kunt of aanpassen.</span><span class="sxs-lookup"><span data-stu-id="d4210-300">By using hello [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a><span data-ttu-id="d4210-301">Weergeven en analyseren Hallo toegang, prestaties en firewall-Logboeken</span><span class="sxs-lookup"><span data-stu-id="d4210-301">View and analyze hello access, performance, and firewall logs</span></span>

<span data-ttu-id="d4210-302">Azure [logboekanalyse](../log-analytics/log-analytics-azure-networking-analytics.md) Hallo teller en de gebeurtenislogboek bestanden kan verzamelen van uw Blob storage-account.</span><span class="sxs-lookup"><span data-stu-id="d4210-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect hello counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="d4210-303">Het bevat visualisaties en krachtige zoekopdrachten mogelijkheden tooanalyze uw Logboeken.</span><span class="sxs-lookup"><span data-stu-id="d4210-303">It includes visualizations and powerful search capabilities tooanalyze your logs.</span></span>

<span data-ttu-id="d4210-304">U kunt ook verbinding maken met tooyour storage-account en ophalen van Hallo JSON logboekvermeldingen voor toegang en prestaties van Logboeken.</span><span class="sxs-lookup"><span data-stu-id="d4210-304">You can also connect tooyour storage account and retrieve hello JSON log entries for access and performance logs.</span></span> <span data-ttu-id="d4210-305">Nadat u Hallo JSON-bestanden hebt gedownload, kunt u deze tooCSV converteren en ze weergeven in Excel, Power BI of een ander hulpprogramma voor de weergave van gegevens.</span><span class="sxs-lookup"><span data-stu-id="d4210-305">After you download hello JSON files, you can convert them tooCSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="d4210-306">Als u bekend met Visual Studio en de basisconcepten bent van het wijzigen van waarden voor de constanten en variabelen in C#, kunt u Hallo [Meld converter extra](https://github.com/Azure-Samples/networking-dotnet-log-converter) beschikbaar is via GitHub.</span><span class="sxs-lookup"><span data-stu-id="d4210-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="d4210-307">Metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="d4210-307">Metrics</span></span>

<span data-ttu-id="d4210-308">Metrische gegevens zijn een functie voor bepaalde waar u prestatiemeteritems in de portal hello bekijken kunt Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="d4210-308">Metrics are a feature for certain Azure resources where you can view performance counters in hello portal.</span></span> <span data-ttu-id="d4210-309">Voor Application Gateway is een waarde nu beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="d4210-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="d4210-310">Met deze metriek wordt de doorvoer en kunt u deze bekijken in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="d4210-310">This metric is throughput, and you can see it in hello portal.</span></span> <span data-ttu-id="d4210-311">Toepassingsgateway tooan bladeren en klik op **metrische gegevens**.</span><span class="sxs-lookup"><span data-stu-id="d4210-311">Browse tooan application gateway and click **Metrics**.</span></span> <span data-ttu-id="d4210-312">tooview hello waarden, selecteer doorvoer in Hallo **beschikbare metrische gegevens** sectie.</span><span class="sxs-lookup"><span data-stu-id="d4210-312">tooview hello values, select throughput in hello **Available metrics** section.</span></span> <span data-ttu-id="d4210-313">In Hallo installatiekopie te volgen, kunt u een voorbeeld met Hallo filters waarmee u toodisplay Hallo gegevens in andere bereiken kunt bekijken.</span><span class="sxs-lookup"><span data-stu-id="d4210-313">In hello following image, you can see an example with hello filters that you can use toodisplay hello data in different time ranges.</span></span>

![Metrische weergave met filters][5]

<span data-ttu-id="d4210-315">toosee een actuele lijst met metrische gegevens, Zie [ondersteund met een Azure-Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d4210-315">toosee a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="d4210-316">Regels voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="d4210-316">Alert rules</span></span>

<span data-ttu-id="d4210-317">U kunt regels voor waarschuwingen op basis van de metrische gegevens voor een bron op te starten.</span><span class="sxs-lookup"><span data-stu-id="d4210-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="d4210-318">Bijvoorbeeld, een waarschuwing een webhook aanroepen of e-beheerder als het Hallo-doorvoer van toepassingsgateway Hallo boven, onder of met een drempelwaarde voor een opgegeven periode is.</span><span class="sxs-lookup"><span data-stu-id="d4210-318">For example, an alert can call a webhook or email an administrator if hello throughput of hello application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="d4210-319">Hallo volgende voorbeeld wordt u begeleid bij een waarschuwingsregel die beheerder tooan e-mailbericht na schendingen van doorvoer een drempelwaarde verzendt:</span><span class="sxs-lookup"><span data-stu-id="d4210-319">hello following example walks you through creating an alert rule that sends an email tooan administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="d4210-320">Klik op **metrische waarschuwing toevoegen** tooopen hello **regel toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="d4210-320">Click **Add metric alert** tooopen hello **Add rule** blade.</span></span> <span data-ttu-id="d4210-321">U kunt ook deze blade Hallo metrische gegevens blade bereiken.</span><span class="sxs-lookup"><span data-stu-id="d4210-321">You can also reach this blade from hello metrics blade.</span></span>

   ![Knop 'Metrische waarschuwing toevoegen'][6]

2. <span data-ttu-id="d4210-323">Op Hallo **regel toevoegen** blade invullen Hallo-naam, voorwaarde en secties melden en op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4210-323">On hello **Add rule** blade, fill out hello name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="d4210-324">In Hallo **voorwaarde** selector, selecteert u een van de Hallo vier waarden: **groter is dan**, **groter dan of gelijk**, **minder dan**, of  **Kleiner dan of gelijk zijn aan**.</span><span class="sxs-lookup"><span data-stu-id="d4210-324">In hello **Condition** selector, select one of hello four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="d4210-325">In Hallo **periode** selector, selecteer een periode van 5 minuten too6 uur.</span><span class="sxs-lookup"><span data-stu-id="d4210-325">In hello **Period** selector, select a period from 5 minutes too6 hours.</span></span>

   * <span data-ttu-id="d4210-326">Als u selecteert **e-eigenaren, bijdragers en lezers**, Hallo e-mail zijn dynamische op basis van het Hallo-gebruikers die toegang toothat bron hebben.</span><span class="sxs-lookup"><span data-stu-id="d4210-326">If you select **Email owners, contributors, and readers**, hello email can be dynamic based on hello users who have access toothat resource.</span></span> <span data-ttu-id="d4210-327">Anders kunt u een door komma's gescheiden lijst met gebruikers in Hallo opgeven **aanvullende beheerder email(s)** vak.</span><span class="sxs-lookup"><span data-stu-id="d4210-327">Otherwise, you can provide a comma-separated list of users in hello **Additional administrator email(s)** box.</span></span>

   ![Blade regel toevoegen][7]

<span data-ttu-id="d4210-329">Als Hallo drempelwaarde wordt overschreden, ontvangt een e-mailbericht is vergelijkbaar toohello in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="d4210-329">If hello threshold is breached, an email that's similar toohello one in hello following image arrives:</span></span>

![E-mailadres voor geschonden drempelwaarde][8]

<span data-ttu-id="d4210-331">Een lijst met waarschuwingen wordt weergegeven nadat u een waarschuwing voor een metriek maken.</span><span class="sxs-lookup"><span data-stu-id="d4210-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="d4210-332">Deze biedt een overzicht van alle Hallo waarschuwingsregels.</span><span class="sxs-lookup"><span data-stu-id="d4210-332">It provides an overview of all hello alert rules.</span></span>

![Lijst met waarschuwingen en regels][9]

<span data-ttu-id="d4210-334">toolearn meer informatie over waarschuwingsmeldingen, Zie [meldingen van waarschuwingen ontvangen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="d4210-334">toolearn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="d4210-335">toounderstand meer informatie over webhooks en hoe u ze kunt gebruiken met waarschuwingen, gaat u naar [een webhook configureren op een Azure metrische waarschuwing](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="d4210-335">toounderstand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4210-336">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d4210-336">Next steps</span></span>

* <span data-ttu-id="d4210-337">Teller en de gebeurtenislogboeken visualiseren met behulp van [logboekanalyse](../log-analytics/log-analytics-azure-networking-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="d4210-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="d4210-338">[Uw Azure activiteitenlogboek met Power BI visualiseren](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blogbericht.</span><span class="sxs-lookup"><span data-stu-id="d4210-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="d4210-339">[Weergeven en analyseren van Azure activiteitenlogboeken in Power BI en meer](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blogbericht.</span><span class="sxs-lookup"><span data-stu-id="d4210-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

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

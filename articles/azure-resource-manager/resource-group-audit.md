---
title: aaaView Azure activiteit logboeken toomonitor resources | Microsoft Docs
description: Gebruik Hallo activiteit logboeken tooreview-gebruikersacties en fouten. Toont PowerShell voor Azure Portal, Azure CLI en REST.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 8430ed2a9c1dfe5f13423a55d358e590b0facb22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a><span data-ttu-id="0a0ed-104">Activiteit weergeven registreert tooaudit acties voor bronnen</span><span class="sxs-lookup"><span data-stu-id="0a0ed-104">View activity logs tooaudit actions on resources</span></span>
<span data-ttu-id="0a0ed-105">Via activiteitenlogboeken, kunt u bepalen:</span><span class="sxs-lookup"><span data-stu-id="0a0ed-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="0a0ed-106">welke bewerkingen zijn uitgevoerd op Hallo van resources in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="0a0ed-106">what operations were taken on hello resources in your subscription</span></span>
* <span data-ttu-id="0a0ed-107">wie Hallo-bewerking gestart (Hoewel de bewerkingen die zijn gestart door een back-endservice niet retourneren een gebruiker als Hallo aanroeper)</span><span class="sxs-lookup"><span data-stu-id="0a0ed-107">who initiated hello operation (although operations initiated by a backend service do not return a user as hello caller)</span></span>
* <span data-ttu-id="0a0ed-108">Wanneer Hallo-bewerking heeft plaatsgevonden</span><span class="sxs-lookup"><span data-stu-id="0a0ed-108">when hello operation occurred</span></span>
* <span data-ttu-id="0a0ed-109">Hallo-status van Hallo-bewerking</span><span class="sxs-lookup"><span data-stu-id="0a0ed-109">hello status of hello operation</span></span>
* <span data-ttu-id="0a0ed-110">Hallo-waarden van andere eigenschappen die u kunnen helpen onderzoek Hallo-bewerking</span><span class="sxs-lookup"><span data-stu-id="0a0ed-110">hello values of other properties that might help you research hello operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="0a0ed-111">U kunt informatie ophalen uit Hallo activiteitenlogboeken via Hallo portal, PowerShell, Azure CLI, inzicht REST API of [Insights .NET-bibliotheek](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span><span class="sxs-lookup"><span data-stu-id="0a0ed-111">You can retrieve information from hello activity logs through hello portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="0a0ed-112">Portal</span><span class="sxs-lookup"><span data-stu-id="0a0ed-112">Portal</span></span>
1. <span data-ttu-id="0a0ed-113">tooview hello activiteitenlogboeken via Hallo-portal, selecteer **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-113">tooview hello activity logs through hello portal, select **Monitor**.</span></span>
   
    ![Selecteer activiteitenlogboeken](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="0a0ed-115">Of tooautomatically filter Hallo-logboek voor een bepaalde bron of de resourcegroep, selecteer **activiteitenlogboek** van die resourceblade.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-115">Or, tooautomatically filter hello activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="0a0ed-116">U ziet dat activiteitenlogboek hello wordt automatisch gefilterd op Hallo geselecteerd resource.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-116">Notice that hello activity log is automatically filtered by hello selected resource.</span></span>
   
    ![filteren op resource](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="0a0ed-118">In Hallo **activiteitenlogboek** blade ziet u een overzicht van recente bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-118">In hello **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![acties weergeven](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="0a0ed-120">toorestrict hello aantal bewerkingen die worden weergegeven, met selecteren verschillende voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-120">toorestrict hello number of operations displayed, select different conditions.</span></span> <span data-ttu-id="0a0ed-121">Hallo volgende afbeelding ziet u bijvoorbeeld Hallo **Timespan** en **gebeurtenis wordt gestart door** velden gewijzigd tooview Hallo acties die door een bepaalde gebruiker of toepassing voor Hallo afgelopen maand.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-121">For example, hello following image shows hello **Timespan** and **Event initiated by** fields changed tooview hello actions taken by a particular user or application for hello past month.</span></span> <span data-ttu-id="0a0ed-122">Selecteer **toepassen** tooview Hallo resultaten van de query.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-122">Select **Apply** tooview hello results of your query.</span></span>
   
    ![Stel filteropties](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="0a0ed-124">Als u toorun Hallo query later nodig hebt, selecteert u **opslaan** en Hallo query een naam geven.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-124">If you need toorun hello query again later, select **Save** and give hello query a name.</span></span>
   
    ![query opslaan](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="0a0ed-126">tooquickly een query uitvoert, kunt u een van de ingebouwde Hallo-query's zoals mislukte implementatie.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-126">tooquickly run a query, you can select one of hello built-in queries, such as failed deployments.</span></span>

    ![query selecteren](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="0a0ed-128">de geselecteerde query Hallo wordt automatisch ingesteld filterwaarden Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-128">hello selected query automatically sets hello required filter values.</span></span>

    ![implementatie-fouten weergeven](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="0a0ed-130">Selecteer een van de Hallo operations toosee een samenvatting van Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-130">Select one of hello operations toosee a summary of hello event.</span></span>

    ![de bewerking weergeven](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="0a0ed-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a0ed-132">PowerShell</span></span>
1. <span data-ttu-id="0a0ed-133">de logboekvermeldingen tooretrieve, Hallo uitvoeren **Get-AzureRmLog** opdracht.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-133">tooretrieve log entries, run hello **Get-AzureRmLog** command.</span></span> <span data-ttu-id="0a0ed-134">U vindt aanvullende parameters toofilter Hallo lijst met items.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-134">You provide additional parameters toofilter hello list of entries.</span></span> <span data-ttu-id="0a0ed-135">Als u een begin- en -tijd niet opgeeft, worden vermeldingen voor laatste uur Hallo geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-135">If you do not specify a start and end time, entries for hello last hour are returned.</span></span> <span data-ttu-id="0a0ed-136">Bijvoorbeeld: tooretrieve Hallo-bewerkingen voor een resourcegroep tijdens Hallo afgelopen uur uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="0a0ed-136">For example, tooretrieve hello operations for a resource group during hello past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="0a0ed-137">Hallo volgende voorbeeld ziet u hoe toouse Hallo activiteit Meld tooresearch bewerkingen die zijn uitgevoerd tijdens een opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-137">hello following example shows how toouse hello activity log tooresearch operations taken during a specified time.</span></span> <span data-ttu-id="0a0ed-138">Hallo zijn begin- en einddatums opgegeven in een datumnotatie.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-138">hello start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="0a0ed-139">Of u kunt functies toospecify Hallo datum datumbereik, zoals Hallo afgelopen 14 dagen.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-139">Or, you can use date functions toospecify hello date range, such as hello last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="0a0ed-140">Afhankelijk van het Hallo-begintijd die u opgeeft, kunnen Hallo eerdere opdrachten een lange lijst met bewerkingen voor Hallo resourcegroep geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-140">Depending on hello start time you specify, hello previous commands can return a long list of operations for hello resource group.</span></span> <span data-ttu-id="0a0ed-141">U kunt filteren Hallo resultaten voor wat u zoekt dankzij de zoekcriteria voldoen.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-141">You can filter hello results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="0a0ed-142">Als u tooresearch hoe een web-app is gestopt probeert, kunt u bijvoorbeeld Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="0a0ed-142">For example, if you are trying tooresearch how a web app was stopped, you could run hello following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="0a0ed-143">Die in dit voorbeeld ziet u dat een stopactie is uitgevoerd door someone@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. <span data-ttu-id="0a0ed-144">U kunt opzoeken Hallo-acties die door een bepaalde gebruiker, zelfs voor een resourcegroep die niet meer bestaat.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-144">You can look up hello actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="0a0ed-145">U kunt filteren op mislukte bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="0a0ed-146">U kunt zich richten op één fout door te kijken Hallo statusbericht voor dat item.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-146">You can focus on one error by looking at hello status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="0a0ed-147">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="0a0ed-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="0a0ed-148">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0a0ed-148">Azure CLI</span></span>
* <span data-ttu-id="0a0ed-149">logboekvermeldingen tooretrieve, u Hallo uitvoeren **azure-groep logboek weergeven** opdracht.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-149">tooretrieve log entries, you run hello **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="0a0ed-150">REST API</span><span class="sxs-lookup"><span data-stu-id="0a0ed-150">REST API</span></span>
<span data-ttu-id="0a0ed-151">Hallo REST-bewerkingen voor het werken met Hallo activiteitenlogboek deel uitmaken van Hallo [Insights REST-API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a0ed-151">hello REST operations for working with hello activity log are part of hello [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="0a0ed-152">tooretrieve activiteit logboekgebeurtenissen, Zie [lijst Hallo management gebeurtenissen in een abonnement](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a0ed-152">tooretrieve activity log events, see [List hello management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a0ed-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0a0ed-153">Next steps</span></span>
* <span data-ttu-id="0a0ed-154">Azure activiteitenlogboeken kunnen worden gebruikt met Power BI toogain meer inzicht over Hallo-acties in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="0a0ed-154">Azure Activity logs can be used with Power BI toogain greater insights about hello actions in your subscription.</span></span> <span data-ttu-id="0a0ed-155">Zie [weergeven en analyseren van Azure activiteitenlogboeken in Power BI en meer](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span><span class="sxs-lookup"><span data-stu-id="0a0ed-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="0a0ed-156">toolearn over het instellen van beveiligingsbeleid, Zie [toegangsbeheer op basis van rollen in Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0a0ed-156">toolearn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="0a0ed-157">toolearn over Hallo-opdrachten voor het weergeven van implementatiebewerkingen, Zie [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="0a0ed-157">toolearn about hello commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="0a0ed-158">hoe tooprevent verwijderingen van een resource voor alle gebruikers zien toolearn [resources met Azure Resource Manager vergrendelen](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0a0ed-158">toolearn how tooprevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>


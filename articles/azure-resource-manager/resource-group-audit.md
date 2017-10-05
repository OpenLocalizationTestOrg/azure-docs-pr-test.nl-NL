---
title: Azure activiteitenlogboeken om te controleren bronnen weergeven | Microsoft Docs
description: Gebruik de activiteitenlogboeken gebruikersacties controleren en fouten. Toont PowerShell voor Azure Portal, Azure CLI en REST.
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
ms.openlocfilehash: 9f90bc80c146c6c2da04aacbc110f7d389c0baa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="view-activity-logs-to-audit-actions-on-resources"></a><span data-ttu-id="86134-104">Activiteitenlogboeken bekijken om te controleren van de acties op resources</span><span class="sxs-lookup"><span data-stu-id="86134-104">View activity logs to audit actions on resources</span></span>
<span data-ttu-id="86134-105">Via activiteitenlogboeken, kunt u bepalen:</span><span class="sxs-lookup"><span data-stu-id="86134-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="86134-106">welke bewerkingen zijn uitgevoerd op de resources in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="86134-106">what operations were taken on the resources in your subscription</span></span>
* <span data-ttu-id="86134-107">wie heeft de bewerking gestart (Hoewel de bewerkingen die zijn gestart door een back-endservice niet retourneren als de aanroeper van een gebruiker)</span><span class="sxs-lookup"><span data-stu-id="86134-107">who initiated the operation (although operations initiated by a backend service do not return a user as the caller)</span></span>
* <span data-ttu-id="86134-108">Wanneer de bewerking is opgetreden</span><span class="sxs-lookup"><span data-stu-id="86134-108">when the operation occurred</span></span>
* <span data-ttu-id="86134-109">De status van de bewerking</span><span class="sxs-lookup"><span data-stu-id="86134-109">the status of the operation</span></span>
* <span data-ttu-id="86134-110">De bewerking van de waarden van andere eigenschappen die u kunnen helpen onderzoek</span><span class="sxs-lookup"><span data-stu-id="86134-110">the values of other properties that might help you research the operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="86134-111">U kunt informatie ophalen uit de activiteitenlogboeken van de via de portal, PowerShell, Azure CLI, inzicht REST API of [Insights .NET-bibliotheek](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span><span class="sxs-lookup"><span data-stu-id="86134-111">You can retrieve information from the activity logs through the portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="86134-112">Portal</span><span class="sxs-lookup"><span data-stu-id="86134-112">Portal</span></span>
1. <span data-ttu-id="86134-113">De om activiteitenlogboeken te raadplegen via de portal, selecteer **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="86134-113">To view the activity logs through the portal, select **Monitor**.</span></span>
   
    ![Selecteer activiteitenlogboeken](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="86134-115">Of selecteer automatisch filter het logboek voor een bepaalde bron of de resourcegroep: **activiteitenlogboek** van die resourceblade.</span><span class="sxs-lookup"><span data-stu-id="86134-115">Or, to automatically filter the activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="86134-116">U ziet dat het activiteitenlogboek automatisch wordt gefilterd op de geselecteerde bron.</span><span class="sxs-lookup"><span data-stu-id="86134-116">Notice that the activity log is automatically filtered by the selected resource.</span></span>
   
    ![filteren op resource](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="86134-118">In de **activiteitenlogboek** blade ziet u een overzicht van recente bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="86134-118">In the **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![acties weergeven](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="86134-120">Als u wilt beperken het aantal bewerkingen die worden weergegeven, selecteer andere voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="86134-120">To restrict the number of operations displayed, select different conditions.</span></span> <span data-ttu-id="86134-121">Bijvoorbeeld de volgende afbeelding toont de **Timespan** en **gebeurtenis wordt gestart door** velden gewijzigd om de acties die door een bepaalde gebruiker of toepassing voor de afgelopen maand weer te geven.</span><span class="sxs-lookup"><span data-stu-id="86134-121">For example, the following image shows the **Timespan** and **Event initiated by** fields changed to view the actions taken by a particular user or application for the past month.</span></span> <span data-ttu-id="86134-122">Selecteer **toepassen** de resultaten van uw query wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="86134-122">Select **Apply** to view the results of your query.</span></span>
   
    ![Stel filteropties](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="86134-124">Als u de query opnieuw uitvoert wilt, selecteert u **opslaan** en geef een naam op voor de query.</span><span class="sxs-lookup"><span data-stu-id="86134-124">If you need to run the query again later, select **Save** and give the query a name.</span></span>
   
    ![query opslaan](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="86134-126">Om snel een query uitvoert, kunt u een van de ingebouwde query's, zoals mislukte implementatie.</span><span class="sxs-lookup"><span data-stu-id="86134-126">To quickly run a query, you can select one of the built-in queries, such as failed deployments.</span></span>

    ![query selecteren](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="86134-128">De geselecteerde query stelt automatisch de vereiste filterwaarden.</span><span class="sxs-lookup"><span data-stu-id="86134-128">The selected query automatically sets the required filter values.</span></span>

    ![implementatie-fouten weergeven](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="86134-130">Selecteer een van de bewerkingen voor een overzicht van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="86134-130">Select one of the operations to see a summary of the event.</span></span>

    ![de bewerking weergeven](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="86134-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="86134-132">PowerShell</span></span>
1. <span data-ttu-id="86134-133">Uitvoeren voor het logboekvermeldingen ophalen, de **Get-AzureRmLog** opdracht.</span><span class="sxs-lookup"><span data-stu-id="86134-133">To retrieve log entries, run the **Get-AzureRmLog** command.</span></span> <span data-ttu-id="86134-134">U opgeven extra parameters om te filteren op de lijst met items.</span><span class="sxs-lookup"><span data-stu-id="86134-134">You provide additional parameters to filter the list of entries.</span></span> <span data-ttu-id="86134-135">Als u een begin- en -tijd niet opgeeft, worden vermeldingen voor het afgelopen uur geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="86134-135">If you do not specify a start and end time, entries for the last hour are returned.</span></span> <span data-ttu-id="86134-136">Als u bijvoorbeeld voor het ophalen van de bewerkingen voor een resourcegroep in het afgelopen uur uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="86134-136">For example, to retrieve the operations for a resource group during the past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="86134-137">Het volgende voorbeeld ziet hoe u het activiteitenlogboek onderzoek bewerkingen die zijn uitgevoerd tijdens een opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="86134-137">The following example shows how to use the activity log to research operations taken during a specified time.</span></span> <span data-ttu-id="86134-138">De begin- en einddatums zijn opgegeven in een datumnotatie.</span><span class="sxs-lookup"><span data-stu-id="86134-138">The start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="86134-139">Of u kunt de datumfuncties gebruiken om op te geven het datumbereik, zoals de afgelopen 14 dagen.</span><span class="sxs-lookup"><span data-stu-id="86134-139">Or, you can use date functions to specify the date range, such as the last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="86134-140">Afhankelijk van de begintijd die u opgeeft, kunnen de eerdere opdrachten een lange lijst met bewerkingen voor de resourcegroep geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="86134-140">Depending on the start time you specify, the previous commands can return a long list of operations for the resource group.</span></span> <span data-ttu-id="86134-141">U kunt de resultaten voor wat u zoekt dankzij de zoekcriteria filteren.</span><span class="sxs-lookup"><span data-stu-id="86134-141">You can filter the results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="86134-142">Als u probeert te onderzoeken hoe een web-app is gestopt, kunt u bijvoorbeeld de volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="86134-142">For example, if you are trying to research how a web app was stopped, you could run the following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="86134-143">Die in dit voorbeeld ziet u dat een stopactie is uitgevoerd door someone@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="86134-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

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

3. <span data-ttu-id="86134-144">U kunt de acties die door een bepaalde gebruiker, zelfs voor een resourcegroep die niet langer bestaat opzoeken.</span><span class="sxs-lookup"><span data-stu-id="86134-144">You can look up the actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="86134-145">U kunt filteren op mislukte bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="86134-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="86134-146">U kunt zich richten op één fout door te kijken het statusbericht voor dat item.</span><span class="sxs-lookup"><span data-stu-id="86134-146">You can focus on one error by looking at the status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="86134-147">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="86134-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="86134-148">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="86134-148">Azure CLI</span></span>
* <span data-ttu-id="86134-149">Voor het ophalen van logboekvermeldingen die u uitvoert het **azure-groep logboek weergeven** opdracht.</span><span class="sxs-lookup"><span data-stu-id="86134-149">To retrieve log entries, you run the **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="86134-150">REST API</span><span class="sxs-lookup"><span data-stu-id="86134-150">REST API</span></span>
<span data-ttu-id="86134-151">De REST-bewerkingen voor het werken met het activiteitenlogboek deel uitmaken van de [Insights REST-API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="86134-151">The REST operations for working with the activity log are part of the [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="86134-152">Zie voor het ophalen van de activiteit logboekgebeurtenissen [lijst van de management-gebeurtenissen in een abonnement](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span><span class="sxs-lookup"><span data-stu-id="86134-152">To retrieve activity log events, see [List the management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86134-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="86134-153">Next steps</span></span>
* <span data-ttu-id="86134-154">Azure activiteitenlogboeken kunnen worden gebruikt met Power BI om meer inzicht over de acties in uw abonnement te krijgen.</span><span class="sxs-lookup"><span data-stu-id="86134-154">Azure Activity logs can be used with Power BI to gain greater insights about the actions in your subscription.</span></span> <span data-ttu-id="86134-155">Zie [weergeven en analyseren van Azure activiteitenlogboeken in Power BI en meer](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span><span class="sxs-lookup"><span data-stu-id="86134-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="86134-156">Zie voor meer informatie over het instellen van beveiligingsbeleid [toegangsbeheer op basis van rollen in Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="86134-156">To learn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="86134-157">Zie voor meer informatie over de opdrachten voor het weergeven van implementatiebewerkingen, [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="86134-157">To learn about the commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="86134-158">Zie voor informatie over het voorkomen van een resource voor alle gebruikers zijn verwijderd, [resources met Azure Resource Manager vergrendelen](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="86134-158">To learn how to prevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>


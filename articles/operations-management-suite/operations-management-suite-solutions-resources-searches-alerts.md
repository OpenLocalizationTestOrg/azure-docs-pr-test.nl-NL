---
title: aaaSaved zoekopdrachten en waarschuwingen in de OMS-oplossingen | Microsoft Docs
description: "Oplossingen in OMS omvatten meestal opgeslagen zoekopdrachten in logboekanalyse tooanalyze gegevens verzameld door Hallo-oplossing.  Ze kunnen ook waarschuwingen toonotify Hallo-gebruiker definiëren of automatisch actie ondernemen in het antwoord tooa Kritiek probleem.  Dit artikel wordt beschreven hoe toodefine logboekanalyse opgeslagen zoekopdrachten en waarschuwingen in een ARM-sjabloon zodat ze kunnen worden opgenomen beheersystemen."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a><span data-ttu-id="6f5b9-105">Zoekopdrachten en waarschuwingen tooOMS beheeroplossing (Preview) toe te voegen logboekanalyse opgeslagen</span><span class="sxs-lookup"><span data-stu-id="6f5b9-105">Adding Log Analytics saved searches and alerts tooOMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="6f5b9-106">Dit is voorlopige documentatie voor het maken van oplossingen voor het beheer in OMS die zich momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="6f5b9-107">De hieronder beschreven schema is onderwerp toochange.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-107">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="6f5b9-108">[Oplossingen voor het beheer in OMS](operations-management-suite-solutions.md) omvatten meestal [opgeslagen zoekopdrachten](../log-analytics/log-analytics-log-searches.md) in logboekanalyse tooanalyze gegevens verzameld door Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics tooanalyze data collected by hello solution.</span></span>  <span data-ttu-id="6f5b9-109">Ze kunnen ook definiëren [waarschuwingen](../log-analytics/log-analytics-alerts.md) toonotify Hallo gebruiker of automatisch actie ondernemen in het antwoord tooa Kritiek probleem.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) toonotify hello user or automatically take action in response tooa critical issue.</span></span>  <span data-ttu-id="6f5b9-110">Dit artikel wordt beschreven hoe toodefine logboekanalyse opgeslagen zoekopdrachten en waarschuwingen in een [Resource Management-sjabloon](../resource-manager-template-walkthrough.md) zodat ze kunnen worden opgenomen [beheeroplossingen](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="6f5b9-110">This article describes how toodefine Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6f5b9-111">Hallo voorbeelden in dit artikel gebruiken parameters en variabelen die zijn beide vereist of algemene toomanagement oplossingen en wordt beschreven in [beheeroplossingen maken in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="6f5b9-111">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="6f5b9-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6f5b9-112">Prerequisites</span></span>
<span data-ttu-id="6f5b9-113">In dit artikel wordt ervan uitgegaan dat u al bekend met het te bent[maken van een beheeroplossing](operations-management-suite-solutions-creating.md) en Hallo-structuur van een [ARM-sjabloon](../resource-group-authoring-templates.md) en oplossingsbestand.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-113">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="6f5b9-114">Log Analytics-werkruimte</span><span class="sxs-lookup"><span data-stu-id="6f5b9-114">Log Analytics Workspace</span></span>
<span data-ttu-id="6f5b9-115">Alle resources in logboekanalyse zijn opgenomen in een [werkruimte](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="6f5b9-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="6f5b9-116">Zoals beschreven in [OMS werkruimte en de Automation-account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) Hallo-werkruimte niet is opgenomen in de oplossing voor het beheer van hello, maar moet bestaan voordat het Hallo-oplossing is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello workspace isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="6f5b9-117">Als het is niet beschikbaar, mislukken Hallo oplossing installatie.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-117">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="6f5b9-118">Hallo-naam van Hallo werkruimte is in Hallo-naam van elke resource logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-118">hello name of hello workspace is in hello name of each Log Analytics resource.</span></span>  <span data-ttu-id="6f5b9-119">Dit wordt gedaan Hallo-oplossing met Hallo **werkruimte** parameter zoals in het volgende voorbeeld van een resource savedsearch Hallo.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-119">This is done in hello solution with hello **workspace** parameter as in hello following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="6f5b9-120">Opgeslagen zoekopdrachten</span><span class="sxs-lookup"><span data-stu-id="6f5b9-120">Saved Searches</span></span>
<span data-ttu-id="6f5b9-121">Omvatten [opgeslagen zoekopdrachten](../log-analytics/log-analytics-log-searches.md) in een oplossing tooallow gebruikers tooquery gegevens verzameld door uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution tooallow users tooquery data collected by your solution.</span></span>  <span data-ttu-id="6f5b9-122">Opgeslagen zoekopdrachten worden weergegeven onder **Favorieten** in Hallo OMS-portal en **opgeslagen zoekacties** in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-122">Saved searches will appear under **Favorites** in hello OMS portal and **Saved Searches** in hello Azure portal .</span></span>  <span data-ttu-id="6f5b9-123">Een opgeslagen zoekopdracht is ook vereist voor elke waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="6f5b9-124">[Log Analytics opgeslagen zoekopdracht](../log-analytics/log-analytics-log-searches.md) resources zijn een type `Microsoft.OperationalInsights/workspaces/savedSearches` en hebben Hallo structuur te volgen.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have hello following structure.</span></span>  <span data-ttu-id="6f5b9-125">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



<span data-ttu-id="6f5b9-126">Elk van de eigenschappen van een opgeslagen zoekopdracht Hallo worden beschreven in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-126">Each of hello properties of a saved search are described in hello following table.</span></span> 

| <span data-ttu-id="6f5b9-127">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="6f5b9-127">Property</span></span> | <span data-ttu-id="6f5b9-128">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6f5b9-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6f5b9-129">category</span><span class="sxs-lookup"><span data-stu-id="6f5b9-129">category</span></span> | <span data-ttu-id="6f5b9-130">Hallo categorie voor Hallo opgeslagen zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-130">hello category for hello saved search.</span></span>  <span data-ttu-id="6f5b9-131">Alle opgeslagen zoekopdrachten in Hallo dezelfde oplossing vaak delen één categorie zodat ze samen worden gegroepeerd in Hallo-console.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-131">Any saved searches in hello same solution will often share a single category so they are grouped together in hello console.</span></span> |
| <span data-ttu-id="6f5b9-132">weergavenaam</span><span class="sxs-lookup"><span data-stu-id="6f5b9-132">displayname</span></span> | <span data-ttu-id="6f5b9-133">Naam toodisplay voor Hallo opgeslagen zoekopdracht in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-133">Name toodisplay for hello saved search in hello portal.</span></span> |
| <span data-ttu-id="6f5b9-134">query</span><span class="sxs-lookup"><span data-stu-id="6f5b9-134">query</span></span> | <span data-ttu-id="6f5b9-135">Query toorun.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-135">Query toorun.</span></span> |

> [!NOTE]
> <span data-ttu-id="6f5b9-136">Mogelijk moet u toouse escape-tekens in Hallo-query als deze tekens bevat die kunnen worden geïnterpreteerd als JSON.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-136">You may need toouse escape characters in hello query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="6f5b9-137">Bijvoorbeeld, als de query is **Type: AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write '**, deze worden geschreven in het oplossingsbestand Hallo als **Type: AzureActivity OperationName:\" Microsoft.Compute/virtualMachines/write\"**.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in hello solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="6f5b9-138">Waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="6f5b9-138">Alerts</span></span>
<span data-ttu-id="6f5b9-139">[Meld u Analytics waarschuwingen](../log-analytics/log-analytics-alerts.md) zijn gemaakt door regels voor waarschuwingen die een opgeslagen zoekopdracht op een vast interval uitvoert.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="6f5b9-140">Hallo-resultaten van Hallo query aan opgegeven criteria voldoen, een waarschuwing wordt vastgelegd als een of meer acties worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-140">If hello results of hello query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="6f5b9-141">Waarschuwingsregels in een beheersysteem bestaan Hallo na drie verschillende bronnen.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-141">Alert rules in a management solution are made up of hello following three different resources.</span></span>

- <span data-ttu-id="6f5b9-142">**Opgeslagen zoekopdracht.**</span><span class="sxs-lookup"><span data-stu-id="6f5b9-142">**Saved search.**</span></span>  <span data-ttu-id="6f5b9-143">Hiermee definieert u Hallo logboek zoeken die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-143">Defines hello log search that will be run.</span></span>  <span data-ttu-id="6f5b9-144">Meerdere regels voor waarschuwingen kunnen een enkele opgeslagen zoekopdracht delen.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="6f5b9-145">**Plannen.**</span><span class="sxs-lookup"><span data-stu-id="6f5b9-145">**Schedule.**</span></span>  <span data-ttu-id="6f5b9-146">Hiermee definieert u hoe vaak hello logboek zoekopdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-146">Defines how often hello log search will be run.</span></span>  <span data-ttu-id="6f5b9-147">Elke waarschuwingsregel wordt slechts één schema hebben.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="6f5b9-148">**Actie van de waarschuwing.**</span><span class="sxs-lookup"><span data-stu-id="6f5b9-148">**Alert action.**</span></span>  <span data-ttu-id="6f5b9-149">Elke waarschuwingsregel heeft een actie-resource met een type **waarschuwing** Hallo details van de waarschuwing Hallo zoals Hallo criteria voor wanneer een record voor een waarschuwing wordt gemaakt en de ernst van waarschuwing Hallo te definiëren.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-149">Each alert rule will have one action resource with a type of **Alert** that defines hello details of hello alert such as hello criteria for when an alert record will be created and hello alert's severity.</span></span>  <span data-ttu-id="6f5b9-150">Hallo actie resource definieert eventueel een e-mail en runbook-antwoord.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-150">hello action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="6f5b9-151">**De actie van de Webhook is (optioneel).**</span><span class="sxs-lookup"><span data-stu-id="6f5b9-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="6f5b9-152">Als Hallo waarschuwingsregel wordt een webhook aanroepen, wordt een actie van extra resource met een type vereist **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-152">If hello alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="6f5b9-153">Opgeslagen zoekopdracht resources hierboven zijn beschreven.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-153">Saved search resources are described above.</span></span>  <span data-ttu-id="6f5b9-154">Hallo worden andere resources hieronder beschreven.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-154">hello other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="6f5b9-155">Schema-resource</span><span class="sxs-lookup"><span data-stu-id="6f5b9-155">Schedule resource</span></span>

<span data-ttu-id="6f5b9-156">Een opgeslagen zoekopdracht kan een of meer schema's met het schema voor een afzonderlijke waarschuwingsregel hebben.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="6f5b9-157">Hallo bepaalt planning hoe vaak hello zoekopdracht wordt uitgevoerd en Hallo tijdsinterval via welke Hallo gegevens worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-157">hello schedule defines how often hello search is run and hello time interval over which hello data is retrieved.</span></span>  <span data-ttu-id="6f5b9-158">Planning resources zijn een type `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` en hebben Hallo structuur te volgen.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have hello following structure.</span></span> <span data-ttu-id="6f5b9-159">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



<span data-ttu-id="6f5b9-160">Hallo-eigenschappen voor schema-bronnen worden beschreven in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-160">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="6f5b9-161">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="6f5b9-161">Element name</span></span> | <span data-ttu-id="6f5b9-162">Vereist</span><span class="sxs-lookup"><span data-stu-id="6f5b9-162">Required</span></span> | <span data-ttu-id="6f5b9-163">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6f5b9-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6f5b9-164">ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="6f5b9-164">enabled</span></span>       | <span data-ttu-id="6f5b9-165">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-165">Yes</span></span> | <span data-ttu-id="6f5b9-166">Hiermee geeft u op of Hallo waarschuwing is ingeschakeld wanneer deze wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-166">Specifies whether hello alert is enabled when it's created.</span></span> |
| <span data-ttu-id="6f5b9-167">interval</span><span class="sxs-lookup"><span data-stu-id="6f5b9-167">interval</span></span>      | <span data-ttu-id="6f5b9-168">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-168">Yes</span></span> | <span data-ttu-id="6f5b9-169">Hoe vaak hello query wordt uitgevoerd in minuten.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-169">How often hello query runs in minutes.</span></span> |
| <span data-ttu-id="6f5b9-170">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="6f5b9-170">queryTimeSpan</span></span> | <span data-ttu-id="6f5b9-171">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-171">Yes</span></span> | <span data-ttu-id="6f5b9-172">De lengte van de tijd in minuten over welke tooevaluate resultaten.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-172">Length of time in minutes over which tooevaluate results.</span></span> |

<span data-ttu-id="6f5b9-173">Hallo planning resource dient is afhankelijk van Hallo opgeslagen zoekopdracht zodat deze gemaakt voordat het Hallo-schema.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-173">hello schedule resource should depend on hello saved search so that it's created before hello schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="6f5b9-174">Acties</span><span class="sxs-lookup"><span data-stu-id="6f5b9-174">Actions</span></span>
<span data-ttu-id="6f5b9-175">Er zijn twee soorten actie resource die is opgegeven door Hallo **Type** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-175">There are two types of action resource specified by hello **Type** property.</span></span>  <span data-ttu-id="6f5b9-176">Een planning vereist één **waarschuwing** actie waarmee wordt gedefinieerd Hallo details van de waarschuwingsregel Hallo en welke acties worden uitgevoerd wanneer een waarschuwing wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-176">A schedule requires one **Alert** action which defines hello details of hello alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="6f5b9-177">Het kan ook betekenen dat een **Webhook** actie als een webhook moet worden aangeroepen vanuit Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-177">It may also include a **Webhook** action if a webhook should be called from hello alert.</span></span>  

<span data-ttu-id="6f5b9-178">Actie resources zijn een type `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="6f5b9-179">Waarschuwingsacties</span><span class="sxs-lookup"><span data-stu-id="6f5b9-179">Alert actions</span></span>

<span data-ttu-id="6f5b9-180">Elke planning heeft een **waarschuwing** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="6f5b9-181">Hiermee definieert u Hallo details van Hallo waarschuwing en eventueel acties melding en herstel.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-181">This defines hello details of hello alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="6f5b9-182">Een melding verzendt een e-tooone of meer adressen.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-182">A notification sends an email tooone or more addresses.</span></span>  <span data-ttu-id="6f5b9-183">Een herstel wordt een runbook in Azure Automation tooattempt tooremediate Hallo gedetecteerd probleem gestart.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-183">A remediation starts a runbook in Azure Automation tooattempt tooremediate hello detected issue.</span></span>

<span data-ttu-id="6f5b9-184">Waarschuwing acties hebben Hallo structuur te volgen.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-184">Alert actions have hello following structure.</span></span>  <span data-ttu-id="6f5b9-185">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

<span data-ttu-id="6f5b9-186">Hallo-eigenschappen voor de actie waarschuwing resources worden beschreven in Hallo tabellen te volgen.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-186">hello properties for Alert action resources are described in hello following tables.</span></span>

| <span data-ttu-id="6f5b9-187">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="6f5b9-187">Element name</span></span> | <span data-ttu-id="6f5b9-188">Vereist</span><span class="sxs-lookup"><span data-stu-id="6f5b9-188">Required</span></span> | <span data-ttu-id="6f5b9-189">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6f5b9-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6f5b9-190">Type</span><span class="sxs-lookup"><span data-stu-id="6f5b9-190">Type</span></span> | <span data-ttu-id="6f5b9-191">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-191">Yes</span></span> | <span data-ttu-id="6f5b9-192">Type Hallo actie.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-192">Type of hello action.</span></span>  <span data-ttu-id="6f5b9-193">Dit is **waarschuwing** voor meldingen.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="6f5b9-194">Naam</span><span class="sxs-lookup"><span data-stu-id="6f5b9-194">Name</span></span> | <span data-ttu-id="6f5b9-195">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-195">Yes</span></span> | <span data-ttu-id="6f5b9-196">Weergavenaam voor Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-196">Display name for hello alert.</span></span>  <span data-ttu-id="6f5b9-197">Dit is Hallo-naam die wordt weergegeven in de console Hallo voor Hallo waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-197">This is hello name that's displayed in hello console for hello alert rule.</span></span> |
| <span data-ttu-id="6f5b9-198">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6f5b9-198">Description</span></span> | <span data-ttu-id="6f5b9-199">Nee</span><span class="sxs-lookup"><span data-stu-id="6f5b9-199">No</span></span> | <span data-ttu-id="6f5b9-200">Optionele beschrijving van waarschuwing Hallo.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-200">Optional description of hello alert.</span></span> |
| <span data-ttu-id="6f5b9-201">Ernst</span><span class="sxs-lookup"><span data-stu-id="6f5b9-201">Severity</span></span> | <span data-ttu-id="6f5b9-202">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-202">Yes</span></span> | <span data-ttu-id="6f5b9-203">Ernst van waarschuwing Hallo-record van Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="6f5b9-203">Severity of hello alert record from hello following values:</span></span><br><br> <span data-ttu-id="6f5b9-204">**Kritieke**</span><span class="sxs-lookup"><span data-stu-id="6f5b9-204">**Critical**</span></span><br><span data-ttu-id="6f5b9-205">**Waarschuwing**</span><span class="sxs-lookup"><span data-stu-id="6f5b9-205">**Warning**</span></span><br><span data-ttu-id="6f5b9-206">**Informatief**</span><span class="sxs-lookup"><span data-stu-id="6f5b9-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="6f5b9-207">Drempelwaarde</span><span class="sxs-lookup"><span data-stu-id="6f5b9-207">Threshold</span></span>
<span data-ttu-id="6f5b9-208">Deze sectie is vereist.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-208">This section is required.</span></span>  <span data-ttu-id="6f5b9-209">Het definieert Hallo-eigenschappen voor Hallo waarschuwingsdrempel.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-209">It defines hello properties for hello alert threshold.</span></span>

| <span data-ttu-id="6f5b9-210">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="6f5b9-210">Element name</span></span> | <span data-ttu-id="6f5b9-211">Vereist</span><span class="sxs-lookup"><span data-stu-id="6f5b9-211">Required</span></span> | <span data-ttu-id="6f5b9-212">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6f5b9-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6f5b9-213">Operator</span><span class="sxs-lookup"><span data-stu-id="6f5b9-213">Operator</span></span> | <span data-ttu-id="6f5b9-214">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-214">Yes</span></span> | <span data-ttu-id="6f5b9-215">De operator voor vergelijking van de volgende waarden Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="6f5b9-215">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="6f5b9-216">**gt = groter is dan<br>lt = kleiner dan**</span><span class="sxs-lookup"><span data-stu-id="6f5b9-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="6f5b9-217">Waarde</span><span class="sxs-lookup"><span data-stu-id="6f5b9-217">Value</span></span> | <span data-ttu-id="6f5b9-218">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-218">Yes</span></span> | <span data-ttu-id="6f5b9-219">Hallo waarde toocompare Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-219">hello value toocompare hello results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="6f5b9-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="6f5b9-220">MetricsTrigger</span></span>
<span data-ttu-id="6f5b9-221">Deze sectie is optioneel.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-221">This section is optional.</span></span>  <span data-ttu-id="6f5b9-222">Op te nemen voor een waarschuwing metrische meting.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="6f5b9-223">Metrische maateenheids waarschuwingen zijn momenteel in de openbare preview.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="6f5b9-224">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="6f5b9-224">Element name</span></span> | <span data-ttu-id="6f5b9-225">Vereist</span><span class="sxs-lookup"><span data-stu-id="6f5b9-225">Required</span></span> | <span data-ttu-id="6f5b9-226">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6f5b9-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6f5b9-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="6f5b9-227">TriggerCondition</span></span> | <span data-ttu-id="6f5b9-228">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-228">Yes</span></span> | <span data-ttu-id="6f5b9-229">Hiermee bepaalt u of Hallo drempelwaarde voor het totale aantal schendingen of opeenvolgende schendingen van Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="6f5b9-229">Specifies whether hello threshold is for total number of breaches or consecutive breaches from hello following values:</span></span><br><br><span data-ttu-id="6f5b9-230">**Totaal aantal<br>opeenvolgende**</span><span class="sxs-lookup"><span data-stu-id="6f5b9-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="6f5b9-231">Operator</span><span class="sxs-lookup"><span data-stu-id="6f5b9-231">Operator</span></span> | <span data-ttu-id="6f5b9-232">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-232">Yes</span></span> | <span data-ttu-id="6f5b9-233">De operator voor vergelijking van de volgende waarden Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="6f5b9-233">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="6f5b9-234">**gt = groter is dan<br>lt = kleiner dan**</span><span class="sxs-lookup"><span data-stu-id="6f5b9-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="6f5b9-235">Waarde</span><span class="sxs-lookup"><span data-stu-id="6f5b9-235">Value</span></span> | <span data-ttu-id="6f5b9-236">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-236">Yes</span></span> | <span data-ttu-id="6f5b9-237">Aantal Hallo tijden Hallo criteria moet zijn voldaan tootrigger Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-237">Number of hello times hello criteria must be met tootrigger hello alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="6f5b9-238">Beperking</span><span class="sxs-lookup"><span data-stu-id="6f5b9-238">Throttling</span></span>
<span data-ttu-id="6f5b9-239">Deze sectie is optioneel.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-239">This section is optional.</span></span>  <span data-ttu-id="6f5b9-240">Deze sectie bevatten als u wilt dat waarschuwingen van de toosuppress van Hallo dezelfde regel voor een bepaalde hoeveelheid tijd nadat een waarschuwing is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-240">Include this section if you want toosuppress alerts from hello same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="6f5b9-241">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="6f5b9-241">Element name</span></span> | <span data-ttu-id="6f5b9-242">Vereist</span><span class="sxs-lookup"><span data-stu-id="6f5b9-242">Required</span></span> | <span data-ttu-id="6f5b9-243">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6f5b9-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6f5b9-244">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="6f5b9-244">DurationInMinutes</span></span> | <span data-ttu-id="6f5b9-245">Ja als u beperking van element opgenomen</span><span class="sxs-lookup"><span data-stu-id="6f5b9-245">Yes if Throttling element included</span></span> | <span data-ttu-id="6f5b9-246">Het aantal minuten de waarschuwingen toosuppress na één van Hallo dezelfde waarschuwingsregel wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-246">Number of minutes toosuppress alerts after one from hello same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="6f5b9-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="6f5b9-247">EmailNotification</span></span>
 <span data-ttu-id="6f5b9-248">Deze sectie is optioneel opnemen als u wilt dat Hallo waarschuwing toosend mail tooone of meer geadresseerden.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-248">This section is optional  Include it if you want hello alert toosend mail tooone or more recipients.</span></span>

| <span data-ttu-id="6f5b9-249">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="6f5b9-249">Element name</span></span> | <span data-ttu-id="6f5b9-250">Vereist</span><span class="sxs-lookup"><span data-stu-id="6f5b9-250">Required</span></span> | <span data-ttu-id="6f5b9-251">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6f5b9-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6f5b9-252">ontvangers</span><span class="sxs-lookup"><span data-stu-id="6f5b9-252">Recipients</span></span> | <span data-ttu-id="6f5b9-253">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-253">Yes</span></span> | <span data-ttu-id="6f5b9-254">Door komma's gescheiden lijst met e-mailadres adressen toosend melding wanneer een waarschuwing wordt gemaakt, zoals in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-254">Comma delimited list of email addresses toosend notification when an alert is created such as in hello following example.</span></span><br><br><span data-ttu-id="6f5b9-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="6f5b9-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="6f5b9-256">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="6f5b9-256">Subject</span></span> | <span data-ttu-id="6f5b9-257">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-257">Yes</span></span> | <span data-ttu-id="6f5b9-258">De onderwerpregel van Hallo e-mail.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-258">Subject line of hello mail.</span></span> |
| <span data-ttu-id="6f5b9-259">Bijlage</span><span class="sxs-lookup"><span data-stu-id="6f5b9-259">Attachment</span></span> | <span data-ttu-id="6f5b9-260">Nee</span><span class="sxs-lookup"><span data-stu-id="6f5b9-260">No</span></span> | <span data-ttu-id="6f5b9-261">Bijlagen worden momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="6f5b9-262">Als dit element is opgenomen, worden deze **geen**.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="6f5b9-263">Herstel</span><span class="sxs-lookup"><span data-stu-id="6f5b9-263">Remediation</span></span>
<span data-ttu-id="6f5b9-264">Deze sectie is optioneel als u een runbook toostart in antwoord toohello waarschuwing wilt opnemen.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-264">This section is optional  Include it if you want a runbook toostart in response toohello alert.</span></span> |

| <span data-ttu-id="6f5b9-265">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="6f5b9-265">Element name</span></span> | <span data-ttu-id="6f5b9-266">Vereist</span><span class="sxs-lookup"><span data-stu-id="6f5b9-266">Required</span></span> | <span data-ttu-id="6f5b9-267">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6f5b9-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6f5b9-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="6f5b9-268">RunbookName</span></span> | <span data-ttu-id="6f5b9-269">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-269">Yes</span></span> | <span data-ttu-id="6f5b9-270">Naam van Hallo runbook toostart.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-270">Name of hello runbook toostart.</span></span> |
| <span data-ttu-id="6f5b9-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="6f5b9-271">WebhookUri</span></span> | <span data-ttu-id="6f5b9-272">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-272">Yes</span></span> | <span data-ttu-id="6f5b9-273">De URI van de webhook Hallo voor Hallo runbook.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-273">Uri of hello webhook for hello runbook.</span></span> |
| <span data-ttu-id="6f5b9-274">Verloopdatum</span><span class="sxs-lookup"><span data-stu-id="6f5b9-274">Expiry</span></span> | <span data-ttu-id="6f5b9-275">Nee</span><span class="sxs-lookup"><span data-stu-id="6f5b9-275">No</span></span> | <span data-ttu-id="6f5b9-276">Datum en tijd waarop het herstel Hallo verloopt.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-276">Date and time that hello remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="6f5b9-277">Webhookacties</span><span class="sxs-lookup"><span data-stu-id="6f5b9-277">Webhook actions</span></span>

<span data-ttu-id="6f5b9-278">Een proces starten webhookacties door het aanroepen van een URL en het eventueel geven een nettolading toobe verzonden.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-278">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span> <span data-ttu-id="6f5b9-279">Ze zijn vergelijkbaar tooRemediation acties maar ze zijn bedoeld voor webhooks die van processen dan Azure Automation-runbooks gebruikmaken mogelijk.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-279">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="6f5b9-280">Ze bieden ook een extra optie Hallo van het bieden van een nettolading toobe bezorgd toohello extern proces.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-280">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="6f5b9-281">Als de waarschuwing wordt een webhook aanroepen, dan deze een actie-resource met een type moet **Webhook** in toevoeging toohello **waarschuwing** actie resource.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition toohello **Alert** action resource.</span></span>  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

<span data-ttu-id="6f5b9-282">Hallo-eigenschappen voor Webhook actie resources worden beschreven in Hallo tabellen te volgen.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-282">hello properties for Webhook action resources are described in hello following tables.</span></span>

| <span data-ttu-id="6f5b9-283">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="6f5b9-283">Element name</span></span> | <span data-ttu-id="6f5b9-284">Vereist</span><span class="sxs-lookup"><span data-stu-id="6f5b9-284">Required</span></span> | <span data-ttu-id="6f5b9-285">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6f5b9-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6f5b9-286">type</span><span class="sxs-lookup"><span data-stu-id="6f5b9-286">type</span></span> | <span data-ttu-id="6f5b9-287">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-287">Yes</span></span> | <span data-ttu-id="6f5b9-288">Type Hallo actie.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-288">Type of hello action.</span></span>  <span data-ttu-id="6f5b9-289">Dit is **Webhook** voor webhookacties.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="6f5b9-290">naam</span><span class="sxs-lookup"><span data-stu-id="6f5b9-290">name</span></span> | <span data-ttu-id="6f5b9-291">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-291">Yes</span></span> | <span data-ttu-id="6f5b9-292">Weergavenaam voor Hallo actie.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-292">Display name for hello action.</span></span>  <span data-ttu-id="6f5b9-293">Dit wordt niet weergegeven in Hallo-console.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-293">This is not displayed in hello console.</span></span> |
| <span data-ttu-id="6f5b9-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="6f5b9-294">wehookUri</span></span> | <span data-ttu-id="6f5b9-295">Ja</span><span class="sxs-lookup"><span data-stu-id="6f5b9-295">Yes</span></span> | <span data-ttu-id="6f5b9-296">De URI voor Hallo webhook.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-296">Uri for hello webhook.</span></span> |
| <span data-ttu-id="6f5b9-297">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="6f5b9-297">customPayload</span></span> | <span data-ttu-id="6f5b9-298">Nee</span><span class="sxs-lookup"><span data-stu-id="6f5b9-298">No</span></span> | <span data-ttu-id="6f5b9-299">Aangepaste nettolading toobe toohello webhook verzonden.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-299">Custom payload toobe sent toohello webhook.</span></span> <span data-ttu-id="6f5b9-300">Hallo-indeling afhankelijk van welke webhook hello wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-300">hello format will depend on what hello webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="6f5b9-301">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="6f5b9-301">Sample</span></span>

<span data-ttu-id="6f5b9-302">Hier volgt een voorbeeld van een oplossing die bevatten die Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="6f5b9-302">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="6f5b9-303">Opgeslagen zoekopdracht</span><span class="sxs-lookup"><span data-stu-id="6f5b9-303">Saved search</span></span>
- <span data-ttu-id="6f5b9-304">Planning</span><span class="sxs-lookup"><span data-stu-id="6f5b9-304">Schedule</span></span>
- <span data-ttu-id="6f5b9-305">Actie waarschuwing</span><span class="sxs-lookup"><span data-stu-id="6f5b9-305">Alert action</span></span>
- <span data-ttu-id="6f5b9-306">Webhook-actie</span><span class="sxs-lookup"><span data-stu-id="6f5b9-306">Webhook action</span></span>

<span data-ttu-id="6f5b9-307">voorbeeld gebruikt Hallo [standaardoplossing parameters](operations-management-suite-solutions-solution-file.md#parameters) variabelen die meestal in een oplossing als gebruikt wordt toohardcoding waarden in de resourcedefinities Hallo geboden.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-307">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for hello email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


<span data-ttu-id="6f5b9-308">Hallo na parameterbestand biedt voorbeelden van waarden voor deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-308">hello following parameter file provides samples values for this solution.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="6f5b9-309">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6f5b9-309">Next steps</span></span>
* <span data-ttu-id="6f5b9-310">[Weergaven toevoegen](operations-management-suite-solutions-resources-views.md) tooyour-beheeroplossing.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-310">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="6f5b9-311">[Automation-runbooks en andere resources toevoegen](operations-management-suite-solutions-resources-automation.md) tooyour-beheeroplossing.</span><span class="sxs-lookup"><span data-stu-id="6f5b9-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>


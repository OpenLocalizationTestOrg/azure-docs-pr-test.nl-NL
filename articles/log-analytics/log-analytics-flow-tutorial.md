---
title: aaaAutomate Azure Log Analytics verwerkt met Microsoft-Flow
description: Meer informatie over hoe u kunt Microsoft Flow tooquickly herhaalbare processen automatiseren met behulp van hello Azure Log Analytics-connector.
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="e9e1f-103">Log Analytics-processen met Hallo-connector voor Microsoft-Flow automatiseren</span><span class="sxs-lookup"><span data-stu-id="e9e1f-103">Automate Log Analytics processes with hello connector for Microsoft Flow</span></span>
<span data-ttu-id="e9e1f-104">[Microsoft-Flow](https://ms.flow.microsoft.com) kunt u toocreate geautomatiseerde werkstromen met honderden acties voor diverse services.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you toocreate automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="e9e1f-105">De uitvoer van een actie kan worden gebruikt als invoer tooanother zodat u toocreate integratie tussen verschillende services.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-105">Output from one action can be used as input tooanother allowing you toocreate integration between different services.</span></span>  <span data-ttu-id="e9e1f-106">Hello Azure Log Analytics-connector voor Microsoft-Flow kunt u toobuild werkstromen die door het logboek van zoekopdrachten in logboekanalyse opgehaalde gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-106">hello Azure Log Analytics connector for Microsoft Flow allow you toobuild workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="e9e1f-107">U kunt bijvoorbeeld Microsoft Flow toouse Log Analytics-gegevens in een e-mailmelding vanuit Office 365 gebruiken, maakt een bug in Visual Studio Team Services of een toegestane bericht.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-107">For example, you can use Microsoft Flow toouse Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="e9e1f-108">Door een eenvoudige planning of van een bepaalde actie in een gekoppelde service, zoals wanneer een e-mailbericht of een tweet wordt ontvangen, kunt u een werkstroom activeren.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="e9e1f-109">Hello Azure Log Analytics-connector voor Microsoft-Flow vereist uw werkruimte toobe bijgewerkt toohello nieuwe logboekanalyse querytaal.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-109">hello Azure Log Analytics connector for Microsoft Flow requires your workspace toobe upgraded toohello new Log Analytics query language.</span></span> <span data-ttu-id="e9e1f-110">U kunt meer informatie over de nieuwe taal Hallo en uw werkruimte op Hallo procedure tooupgrade ophalen [Upgrade van uw Azure-logboekanalyse werkruimte toonew logboek zoekopdracht](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="e9e1f-110">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="e9e1f-111">Hallo-zelfstudie in dit artikel leert u hoe toocreate een stroom die automatisch verzonden resultaten van een zoekopdracht Log Analytics-logboek Hallo via e-mail, slechts één voorbeeld van hoe u Log Analytics in Microsoft Flow kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-111">hello tutorial in this article shows you how toocreate a flow that automatically sends hello results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="e9e1f-112">Stap 1: Een stroom maken</span><span class="sxs-lookup"><span data-stu-id="e9e1f-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="e9e1f-113">Aanmelden te[Microsoft Flow](http://flow.microsoft.com), en selecteer **mijn loopt**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-113">Sign in too[Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="e9e1f-114">Klik op **+ maken van leeg**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="e9e1f-115">Stap 2: Maak een trigger voor uw flow</span><span class="sxs-lookup"><span data-stu-id="e9e1f-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="e9e1f-116">Klik op **zoeken honderden connectors en triggers**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="e9e1f-117">Type **planning** in het zoekvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-117">Type **Schedule** in hello search box.</span></span>
3. <span data-ttu-id="e9e1f-118">Selecteer **planning**, en selecteer vervolgens **schema - terugkeerpatroon**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="e9e1f-119">In Hallo **frequentie** vak Selecteer **dag** en in Hallo **Interval** Voer **1**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-119">In hello **Frequency** box select **Day** and in hello **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="e9e1f-120">![Dialoogvenster voor Microsoft-Flow-trigger](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="e9e1f-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="e9e1f-121">Stap 3: Een actie logboekanalyse toevoegen</span><span class="sxs-lookup"><span data-stu-id="e9e1f-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="e9e1f-122">Klik op **+ een nieuwe stap**, en klik vervolgens op **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="e9e1f-123">Zoeken naar **Meld Analytics**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="e9e1f-124">Klik op **Azure Log Analytics-query uitvoeren en visualiseren resultaten**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="e9e1f-125">![Log Analytics query-venster uitvoeren](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="e9e1f-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-hello-log-analytics-action"></a><span data-ttu-id="e9e1f-126">Stap 4: Configureer Hallo logboekanalyse actie</span><span class="sxs-lookup"><span data-stu-id="e9e1f-126">Step 4: Configure hello Log Analytics action</span></span>

1. <span data-ttu-id="e9e1f-127">Geef details op Hallo voor uw werkruimte inclusief Hallo abonnement-ID, resourcegroep, en de naam van de werkruimte.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-127">Specify hello details for your workspace including hello Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="e9e1f-128">Log Analytics query toohello na Hallo toevoegen **Query** venster.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-128">Add hello following Log Analytics query toohello **Query** window.</span></span>  <span data-ttu-id="e9e1f-129">Dit is alleen een voorbeeldquery en u kunt vervangen door een andere waarmee gegevens worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="e9e1f-130">Selecteer **HTML-tabel** voor Hallo **grafiektype**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-130">Select **HTML Table** for hello **Chart Type**.</span></span><br><br><span data-ttu-id="e9e1f-131">![Log Analytics actie](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="e9e1f-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-hello-flow-toosend-email"></a><span data-ttu-id="e9e1f-132">Stap 5: Hallo stroom toosend e-mail configureren</span><span class="sxs-lookup"><span data-stu-id="e9e1f-132">Step 5: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="e9e1f-133">Klik op **nieuwe stap**, en klik vervolgens op **+ een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="e9e1f-134">Zoeken naar **OfficeOutlook 365**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="e9e1f-135">Klik op **Outlook in Office 365 – stuurt u een e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="e9e1f-136">![Selectievenster voor Office 365 Outlook](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="e9e1f-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="e9e1f-137">Hallo e-mailadres van een ontvanger opgeven in Hallo **naar** venster en een onderwerp in voor Hallo e-mailadres in **onderwerp**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-137">Specify hello email address of a recipient in hello **To** window and a subject for hello email in **Subject**.</span></span>
5. <span data-ttu-id="e9e1f-138">Klik ergens in Hallo **hoofdtekst** vak.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-138">Click anywhere in hello **Body** box.</span></span>  <span data-ttu-id="e9e1f-139">Een **dynamische inhoud** venster wordt geopend met waarden uit de vorige acties.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="e9e1f-140">Selecteer **hoofdtekst**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-140">Select **Body**.</span></span>  <span data-ttu-id="e9e1f-141">Dit is Hallo resultaten van Hallo-query in Hallo Log Analytics-actie.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-141">This is hello results of hello query in hello Log Analytics action.</span></span>
6. <span data-ttu-id="e9e1f-142">Klik op **geavanceerde opties weergeven**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="e9e1f-143">In Hallo **Is HTML** de optie **Ja**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-143">In hello **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="e9e1f-144">![Venster van Office 365 e-configuratie](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="e9e1f-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="e9e1f-145">Stap 6: Opslaan en testen van uw flow</span><span class="sxs-lookup"><span data-stu-id="e9e1f-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="e9e1f-146">In Hallo **stroom naam** vak en klik vervolgens op toevoegen van een naam voor uw flow **stroom maken**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-146">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="e9e1f-147">![Stroom opslaan](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="e9e1f-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="e9e1f-148">Hallo-stroom wordt nu gemaakt en wordt uitgevoerd na een dag is Hallo planning die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-148">hello flow is now created and will run after a day which is hello schedule you specified.</span></span> 
3. <span data-ttu-id="e9e1f-149">tooimmediately test Hallo flow, klikt u op **nu uitvoeren** en vervolgens **uitvoeren stroom**.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-149">tooimmediately test hello flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="e9e1f-150">![Stroom uitvoeren](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="e9e1f-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="e9e1f-151">Wanneer het Hallo-stroom is voltooid, controleert u Hallo mail van Hallo-ontvanger die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e9e1f-151">When hello flow completes, check hello mail of hello recipient that you specified.</span></span>  <span data-ttu-id="e9e1f-152">U moet een e-mailbericht met een hoofdtekst vergelijkbare toohello volgende hebt ontvangen:</span><span class="sxs-lookup"><span data-stu-id="e9e1f-152">You should have received a mail with a body similar toohello following:</span></span><br><br>![Voorbeeldbericht](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="e9e1f-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e9e1f-154">Next steps</span></span>

- <span data-ttu-id="e9e1f-155">Meer informatie over [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="e9e1f-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="e9e1f-156">Meer informatie over [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e9e1f-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>




---
title: Onderzoek en gebruiksgegevens delen met interactieve werkmappen in Azure Application Insights | Microsoft docs
description: Demografische analyse van gebruikers van uw web-app.
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: 75028b4fbda43d90f56690a33c7eb624fce049c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="8d49e-103">Onderzoek en gebruiksgegevens delen met interactieve werkmappen in Application Insights</span><span class="sxs-lookup"><span data-stu-id="8d49e-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="8d49e-104">Werkmappen combineren [Azure Application Insights](app-insights-overview.md) gegevensvisualisaties, [analysequery's](app-insights-analytics.md), en tekst in de interactieve documenten.</span><span class="sxs-lookup"><span data-stu-id="8d49e-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="8d49e-105">Werkmappen kunnen worden bewerkt door andere teamleden met toegang tot de dezelfde Azure-resource.</span><span class="sxs-lookup"><span data-stu-id="8d49e-105">Workbooks are editable by other team members with access to the same Azure resource.</span></span> <span data-ttu-id="8d49e-106">Dit betekent dat de query's en besturingselementen die worden gebruikt voor het maken van een werkmap zijn beschikbaar voor andere mensen lezen van de werkmap, zodat ze gemakkelijk te verkennen, uitbreiden en controleren op fouten.</span><span class="sxs-lookup"><span data-stu-id="8d49e-106">This means the queries and controls used to create a workbook are available to other people reading the workbook, making them easy to explore, extend, and check for mistakes.</span></span>

<span data-ttu-id="8d49e-107">Werkmappen worden gebruikt voor scenario's zoals:</span><span class="sxs-lookup"><span data-stu-id="8d49e-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="8d49e-108">Het gebruik van uw app verkennen wanneer u niet de metrische gegevens van belang van tevoren weet: aantal gebruikers, retentie, conversie tarieven, enzovoort. In tegenstelling tot andere gebruik hulpprogramma's voor webanalyse in Application Insights kunnen werkmappen u meerdere soorten visualisaties en analyses, waardoor ze ideaal voor dit soort vrije vorm exploratie combineren.</span><span class="sxs-lookup"><span data-stu-id="8d49e-108">Exploring the usage of your app when you don't know the metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="8d49e-109">Uitleg over naar uw team hoe een nieuw uitgebrachte functie wordt uitgevoerd, door de gebruiker weergegeven aantallen voor belangrijke interacties en andere metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="8d49e-109">Explaining to your team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="8d49e-110">Delen van de resultaten van een A / B-experiment in uw app met andere leden van uw team.</span><span class="sxs-lookup"><span data-stu-id="8d49e-110">Sharing the results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="8d49e-111">U kunt uitgelegd van de doelstellingen voor het experiment met tekst en vervolgens elk gebruik van metrische gegevens en Analytics query gebruikt voor het evalueren van het experiment, samen met duidelijke call-outs voor of elke metriek boven - of hieronder-doel is weergeven.</span><span class="sxs-lookup"><span data-stu-id="8d49e-111">You can explain the goals for the experiment with text, then show each usage metric and Analytics query used to evaluate the experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="8d49e-112">De impact van een storing rapportage over het gebruik van uw app, het combineren van gegevens, tekstuitleg en een beschrijving van de volgende stappen om te voorkomen dat uitval in de toekomst.</span><span class="sxs-lookup"><span data-stu-id="8d49e-112">Reporting the impact of an outage on the usage of your app, combining data, text explanation, and a discussion of next steps to prevent outages in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="8d49e-113">Uw Application Insights-resource moet bevatten paginaweergaven of aangepaste gebeurtenissen werkmappen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8d49e-113">Your Application Insights resource must contain page views or custom events to use workbooks.</span></span> <span data-ttu-id="8d49e-114">[Meer informatie over het instellen van uw app voor het verzamelen van paginaweergaven automatisch met de Application Insights JavaScript SDK](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="8d49e-114">[Learn how to set up your app to collect page views automatically with the Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="8d49e-115">Bewerken, rangschikken, klonen en secties van de werkmap verwijderen</span><span class="sxs-lookup"><span data-stu-id="8d49e-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="8d49e-116">Is een werkmap een en-klare van secties: onafhankelijk bewerkbare gebruik visualisaties, grafieken, tabellen, tekst of Analytics queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="8d49e-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="8d49e-117">De inhoud van een sectie werkmap bewerken, klikt u op de **bewerken** knop hieronder en naar rechts van de werkmap-sectie.</span><span class="sxs-lookup"><span data-stu-id="8d49e-117">To edit the contents of a workbook section, click the **Edit** button below and to the right of the workbook section.</span></span>

![Application Insights werkmappen sectie besturingselementen bewerken](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="8d49e-119">Wanneer u klaar bent u een sectie bewerkt, klikt u op **gedaan bewerken** in de linkerbenedenhoek van het gedeelte.</span><span class="sxs-lookup"><span data-stu-id="8d49e-119">When you're done editing a section, click **Done Editing** in the bottom left corner of the section.</span></span>

2. <span data-ttu-id="8d49e-120">Een duplicaat van een sectie toevoegen, klikt u op de **klonen in deze sectie** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8d49e-120">To create a duplicate of a section, click the **Clone this section** icon.</span></span> <span data-ttu-id="8d49e-121">Dubbele secties maken is een geweldige naar manier om een query zonder verlies van vorige iteraties herhalen.</span><span class="sxs-lookup"><span data-stu-id="8d49e-121">Creating duplicate sections is a great to way to iterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="8d49e-122">Als u wilt verplaatsen van een sectie in een werkmap, klikt u op de **omhoog** of **omlaag** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8d49e-122">To move up a section in a workbook, click the **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="8d49e-123">Een sectie als permanent wilt verwijderen, klikt u op de **verwijderen** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8d49e-123">To remove a section permanently, click the **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="8d49e-124">Gebruik gegevensvisualisatie secties toevoegen</span><span class="sxs-lookup"><span data-stu-id="8d49e-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="8d49e-125">Werkmappen bieden vier typen ingebouwde gebruik analytics visualisaties.</span><span class="sxs-lookup"><span data-stu-id="8d49e-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="8d49e-126">Alle antwoorden op een algemene vraag over het gebruik van uw app.</span><span class="sxs-lookup"><span data-stu-id="8d49e-126">Each answers a common question about the usage of your app.</span></span> <span data-ttu-id="8d49e-127">Tabellen en grafieken dan deze vier secties wilt toevoegen, voeg Analytics query secties (Zie hieronder).</span><span class="sxs-lookup"><span data-stu-id="8d49e-127">To add tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="8d49e-128">Voor het toevoegen van gebruikers, sessies, gebeurtenissen of bewaren sectie met uw werkmap, gebruik de **gebruikers toevoegen** of andere bijbehorende knop aan de onderkant van de werkmap of aan de onderkant van een willekeurig gedeelte.</span><span class="sxs-lookup"><span data-stu-id="8d49e-128">To add a Users, Sessions, Events, or Retention section to your workbook, use the **Add Users** or other corresponding button at the bottom of the workbook, or at the bottom of any section.</span></span>

![De sectie gebruikers in werkmappen](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="8d49e-130">**Gebruikers** secties beantwoorden 'hoeveel gebruikers een pagina weergegeven of gebruikt een functie van Mijn site?'</span><span class="sxs-lookup"><span data-stu-id="8d49e-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="8d49e-131">**Sessies** secties beantwoorden 'hoeveel sessies gebruikers hoeven te besteden aan een pagina te bekijken of met bepaalde functie van Mijn site?'</span><span class="sxs-lookup"><span data-stu-id="8d49e-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="8d49e-132">**Gebeurtenissen** secties beantwoorden ' hoe vaak gebruikers bepaalde pagina bekijken of bepaalde functie van Mijn site gebruiken?'</span><span class="sxs-lookup"><span data-stu-id="8d49e-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="8d49e-133">Elk van deze drie sectietypen biedt dezelfde set besturingselementen en visualisaties:</span><span class="sxs-lookup"><span data-stu-id="8d49e-133">Each of these three section types offers the same sets of controls and visualizations:</span></span>

* [<span data-ttu-id="8d49e-134">Meer informatie over het bewerken van gebruikers, sessies en gebeurtenissen secties</span><span class="sxs-lookup"><span data-stu-id="8d49e-134">Learn more about editing Users, Sessions, and Events sections</span></span>](app-insights-usage-segmentation.md)
* <span data-ttu-id="8d49e-135">Uitschakelen van de belangrijkste grafiek, histogram rasters, automatische insights en voorbeeld gebruikers visualisaties met behulp van de **grafiek weergeven**, **raster weergeven**, **Insights weergeven**, en **voorbeeld van deze gebruikers** selectievakjes aan het begin van elke sectie.</span><span class="sxs-lookup"><span data-stu-id="8d49e-135">Toggle the main chart, histogram grids, automatic insights, and sample users visualizations using the **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at the top of each section.</span></span>

![De sectie bewaren in werkmappen](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="8d49e-137">**Bewaartermijn** secties beantwoorden "Mensen die een pagina weergegeven of bepaalde functie op een dag of week gebruikt, hoeveel afkomstig terug in de volgende dag of week?"</span><span class="sxs-lookup"><span data-stu-id="8d49e-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* [<span data-ttu-id="8d49e-138">Meer informatie over het bewerken van retentie secties</span><span class="sxs-lookup"><span data-stu-id="8d49e-138">Learn more about editing Retention sections</span></span>](app-insights-usage-retention.md)
* <span data-ttu-id="8d49e-139">Overschakelen de optionele algehele bewaren grafiek met de **weergeven algehele bewaren grafiek** selectievakje aan de bovenkant van de sectie.</span><span class="sxs-lookup"><span data-stu-id="8d49e-139">Toggle the optional Overall Retention chart using the **Show overall retention chart** checkbox at the top of the section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="8d49e-140">Application Insights Analytics secties toevoegen</span><span class="sxs-lookup"><span data-stu-id="8d49e-140">Adding Application Insights Analytics sections</span></span>

![Analytics-sectie in werkmappen](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="8d49e-142">U kunt een gedeelte van de query Application Insights Analytics met uw werkmap toevoegen met de **toevoegen Analytics query** knop aan de onderkant van de werkmap of aan de onderkant van een willekeurig gedeelte.</span><span class="sxs-lookup"><span data-stu-id="8d49e-142">To add an Application Insights Analytics query section to your workbook, use the **Add Analytics query** button at the bottom of the workbook, or at the bottom of any section.</span></span>

<span data-ttu-id="8d49e-143">Analytics query secties kunnen u het toevoegen van willekeurige query's via uw Application Insights-gegevens in werkmappen.</span><span class="sxs-lookup"><span data-stu-id="8d49e-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="8d49e-144">Deze flexibiliteit betekent Analytics query secties zijn uw Ga om voor het beantwoorden van vragen over uw site dan de vier bovenstaande voor gebruikers, sessies, gebeurtenissen en retentie, zoals:</span><span class="sxs-lookup"><span data-stu-id="8d49e-144">This flexibility means Analytics query sections should be your go-to for answering any questions about your site other than the four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="8d49e-145">Het aantal uitzonderingen uw site throw tijdens dezelfde periode als een daling in gebruik</span><span class="sxs-lookup"><span data-stu-id="8d49e-145">How many exceptions did your site throw during the same time period as a decline in usage?</span></span>
* <span data-ttu-id="8d49e-146">Wat is de distributie van laadtijden voor pagina's voor gebruikers die bepaalde pagina bekijken?</span><span class="sxs-lookup"><span data-stu-id="8d49e-146">What was the distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="8d49e-147">Hoeveel gebruikers bepaalde set pagina's weergegeven op uw site, maar niet in een andere set pagina's?</span><span class="sxs-lookup"><span data-stu-id="8d49e-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="8d49e-148">Dit is handig om te begrijpen als u clusters van gebruikers die gebruikmaken van verschillende subsets van functionaliteit van uw site hebt (Gebruik de `join` operator met de `kind=leftanti` aanpassingsfunctie in de Log Analytics query language).</span><span class="sxs-lookup"><span data-stu-id="8d49e-148">This can be useful to understand if you have clusters of users who use different subsets of your site's functionality (use the `join` operator with the `kind=leftanti` modifier in the Log Analytics query language).</span></span>

<span data-ttu-id="8d49e-149">Gebruik de [Log Analytics query language reference](https://docs.loganalytics.io/) voor meer informatie over het schrijven van query's.</span><span class="sxs-lookup"><span data-stu-id="8d49e-149">Use the [Log Analytics query language reference](https://docs.loganalytics.io/) to learn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="8d49e-150">Tekst- en Markdown secties toe te voegen</span><span class="sxs-lookup"><span data-stu-id="8d49e-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="8d49e-151">Helpt zet koppen, uitleg en commentaar toe te voegen aan uw werkmappen een set van tabellen en grafieken in sprekersnotities.</span><span class="sxs-lookup"><span data-stu-id="8d49e-151">Adding headings, explanations, and commentary to your workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="8d49e-152">Tekst secties in ondersteuning voor werkmappen de [Markdown-syntaxis](https://daringfireball.net/projects/markdown/) voor tekstopmaak, zoals kopteksten, vet, cursief en lijsten met opsommingstekens.</span><span class="sxs-lookup"><span data-stu-id="8d49e-152">Text sections in workbooks support the [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="8d49e-153">Als u wilt een tekstsectie toevoegen aan uw werkmap, gebruiken de **tekst toevoegen** knop aan de onderkant van de werkmap of aan de onderkant van een willekeurig gedeelte.</span><span class="sxs-lookup"><span data-stu-id="8d49e-153">To add a text section to your workbook, use the **Add text** button at the bottom of the workbook, or at the bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="8d49e-154">Opslaan en delen van werkmappen met uw team</span><span class="sxs-lookup"><span data-stu-id="8d49e-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="8d49e-155">Werkmappen zijn opgeslagen in een Application Insights-resource in de **mijn rapporten** persoonlijke in u of in de sectie de **gedeeld rapporten** sectie die toegankelijk is voor iedereen met toegang tot de Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="8d49e-155">Workbooks are saved within an Application Insights resource, either in the **My Reports** section that's private to you or in the **Shared Reports** section that's accessible to everyone with access to the Application Insights resource.</span></span> <span data-ttu-id="8d49e-156">U kunt de werkmappen in de resource op de **Open** knop in de actiebalk.</span><span class="sxs-lookup"><span data-stu-id="8d49e-156">To view all the workbooks in the resource, click the **Open** button in the action bar.</span></span>

<span data-ttu-id="8d49e-157">Voor het delen van een werkmap die momenteel **mijn rapporten**:</span><span class="sxs-lookup"><span data-stu-id="8d49e-157">To share a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="8d49e-158">Klik op **Open** in de actiebalk</span><span class="sxs-lookup"><span data-stu-id="8d49e-158">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="8d49e-159">Klik op de knop '...' naast de werkmap die u wilt delen</span><span class="sxs-lookup"><span data-stu-id="8d49e-159">Click the "..." button beside the workbook you want to share</span></span>
3. <span data-ttu-id="8d49e-160">Klik op **verplaatsen naar de gedeelde rapporten**.</span><span class="sxs-lookup"><span data-stu-id="8d49e-160">Click **Move to Shared Reports**.</span></span>

<span data-ttu-id="8d49e-161">Als u wilt delen een werkmap met een koppeling of via e-mail, klikt u op **delen** in de actiebalk.</span><span class="sxs-lookup"><span data-stu-id="8d49e-161">To share a workbook with a link or via email, click **Share** in the action bar.</span></span> <span data-ttu-id="8d49e-162">Houd er rekening mee dat ontvangers van de koppeling moeten toegang hebben tot deze resource in de Azure portal om de werkmap weer te geven.</span><span class="sxs-lookup"><span data-stu-id="8d49e-162">Keep in mind that recipients of the link need access to this resource in the Azure portal to view the workbook.</span></span> <span data-ttu-id="8d49e-163">Als u wilt bewerken, ontvangers moeten minimaal Inzender-rechten voor de resource.</span><span class="sxs-lookup"><span data-stu-id="8d49e-163">To make edits, recipients need at least Contributor permissions for the resource.</span></span>

<span data-ttu-id="8d49e-164">Een koppeling naar een werkmap in een Azure-Dashboard vastmaken:</span><span class="sxs-lookup"><span data-stu-id="8d49e-164">To pin a link to a workbook to an Azure Dashboard:</span></span>

1. <span data-ttu-id="8d49e-165">Klik op **Open** in de actiebalk</span><span class="sxs-lookup"><span data-stu-id="8d49e-165">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="8d49e-166">Klik op de knop '...' naast de werkmap die u wilt vastmaken</span><span class="sxs-lookup"><span data-stu-id="8d49e-166">Click the "..." button beside the workbook you want to pin</span></span>
3. <span data-ttu-id="8d49e-167">Klik op **vastmaken aan dashboard**.</span><span class="sxs-lookup"><span data-stu-id="8d49e-167">Click **Pin to dashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d49e-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8d49e-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d49e-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8d49e-169">Next steps</span></span>
- <span data-ttu-id="8d49e-170">Om in te schakelen ervaringen gebruik, beginnen met het verzenden [aangepaste gebeurtenissen](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) of [paginaweergaven](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="8d49e-170">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="8d49e-171">Als u al aangepaste gebeurtenissen of paginaweergaven verzendt, gebruik de informatie over het gebruik hulpprogramma's voor meer informatie over hoe gebruikers gebruiken voor uw service.</span><span class="sxs-lookup"><span data-stu-id="8d49e-171">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="8d49e-172">Gebruikers, sessies, gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="8d49e-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="8d49e-173">Trechters</span><span class="sxs-lookup"><span data-stu-id="8d49e-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="8d49e-174">Retentie</span><span class="sxs-lookup"><span data-stu-id="8d49e-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="8d49e-175">Gebruikersstromen</span><span class="sxs-lookup"><span data-stu-id="8d49e-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="8d49e-176">Gebruikerscontext toevoegen</span><span class="sxs-lookup"><span data-stu-id="8d49e-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    

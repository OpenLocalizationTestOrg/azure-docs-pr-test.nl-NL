---
title: gebruiksgegevens aaaInvestigate en delen met interactieve werkmappen in Azure Application Insights | Microsoft docs
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
ms.openlocfilehash: bdcebe0f97fdad0a0b301df5950dc09698f5a4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="a554b-103">Onderzoek en gebruiksgegevens delen met interactieve werkmappen in Application Insights</span><span class="sxs-lookup"><span data-stu-id="a554b-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="a554b-104">Werkmappen combineren [Azure Application Insights](app-insights-overview.md) gegevensvisualisaties, [analysequery's](app-insights-analytics.md), en tekst in de interactieve documenten.</span><span class="sxs-lookup"><span data-stu-id="a554b-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="a554b-105">Werkmappen kunnen worden bewerkt door andere teamleden met toegang toohello dezelfde Azure-resource.</span><span class="sxs-lookup"><span data-stu-id="a554b-105">Workbooks are editable by other team members with access toohello same Azure resource.</span></span> <span data-ttu-id="a554b-106">Dit betekent dat het Hallo-query's en besturingselementen gebruikte toocreate een werkmap zijn beschikbaar tooother mensen lezen Hallo werkmap, zodat ze gemakkelijk tooexplore, uitbreiden en controleren op fouten.</span><span class="sxs-lookup"><span data-stu-id="a554b-106">This means hello queries and controls used toocreate a workbook are available tooother people reading hello workbook, making them easy tooexplore, extend, and check for mistakes.</span></span>

<span data-ttu-id="a554b-107">Werkmappen worden gebruikt voor scenario's zoals:</span><span class="sxs-lookup"><span data-stu-id="a554b-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="a554b-108">Hallo informatie over het gebruik van uw app verkennen wanneer u niet Hallo metrische gegevens van belang van tevoren weet: aantal gebruikers, retentie, conversie tarieven, enzovoort. In tegenstelling tot andere gebruik hulpprogramma's voor webanalyse in Application Insights kunnen werkmappen u meerdere soorten visualisaties en analyses, waardoor ze ideaal voor dit soort vrije vorm exploratie combineren.</span><span class="sxs-lookup"><span data-stu-id="a554b-108">Exploring hello usage of your app when you don't know hello metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="a554b-109">Waarin wordt uitgelegd hoe u een nieuw uitgebrachte functie presteert tooyour-team, door de gebruiker weergegeven aantallen voor belangrijke interacties en andere metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="a554b-109">Explaining tooyour team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="a554b-110">Delen Hallo resultaten van een A / B-experiment in uw app met andere leden van uw team.</span><span class="sxs-lookup"><span data-stu-id="a554b-110">Sharing hello results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="a554b-111">U kunt uitleggen Hallo doelstellingen voor Hallo experimenteren met tekst en vervolgens elk gebruik van metrische gegevens weergeven en Analytics query tooevaluate Hallo experiment, samen met duidelijke call-outs voor of elke metriek boven - of hieronder-doel is gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a554b-111">You can explain hello goals for hello experiment with text, then show each usage metric and Analytics query used tooevaluate hello experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="a554b-112">Hallo-impact van een storing op Hallo informatie over het gebruik van uw app, het combineren van gegevens, tekstuitleg en een beschrijving van de volgende stappen tooprevent storingen in toekomstige Hallo rapportage.</span><span class="sxs-lookup"><span data-stu-id="a554b-112">Reporting hello impact of an outage on hello usage of your app, combining data, text explanation, and a discussion of next steps tooprevent outages in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="a554b-113">Uw Application Insights-resource moet paginaweergaven of aangepaste gebeurtenissen toouse werkmappen bevatten.</span><span class="sxs-lookup"><span data-stu-id="a554b-113">Your Application Insights resource must contain page views or custom events toouse workbooks.</span></span> <span data-ttu-id="a554b-114">[Meer informatie over hoe tooset van uw app toocollect pagina automatisch bekijkt Hello Application Insights JavaScript SDK](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="a554b-114">[Learn how tooset up your app toocollect page views automatically with hello Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="a554b-115">Bewerken, rangschikken, klonen en secties van de werkmap verwijderen</span><span class="sxs-lookup"><span data-stu-id="a554b-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="a554b-116">Is een werkmap een en-klare van secties: onafhankelijk bewerkbare gebruik visualisaties, grafieken, tabellen, tekst of Analytics queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="a554b-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="a554b-117">tooedit hello inhoud van een sectie werkmap, klikt u op Hallo **bewerken** hieronder en toohello rechtsboven in de sectie van de werkmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="a554b-117">tooedit hello contents of a workbook section, click hello **Edit** button below and toohello right of hello workbook section.</span></span>

![Application Insights werkmappen sectie besturingselementen bewerken](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="a554b-119">Wanneer u klaar bent u een sectie bewerkt, klikt u op **gedaan bewerken** in de linkeronderhoek van Hallo sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="a554b-119">When you're done editing a section, click **Done Editing** in hello bottom left corner of hello section.</span></span>

2. <span data-ttu-id="a554b-120">toocreate een duplicaat van een sectie, klikt u op Hallo **klonen in deze sectie** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a554b-120">toocreate a duplicate of a section, click hello **Clone this section** icon.</span></span> <span data-ttu-id="a554b-121">Dubbele secties maken is een uitstekende tooway tooiterate van een query zonder verlies van vorige iteraties.</span><span class="sxs-lookup"><span data-stu-id="a554b-121">Creating duplicate sections is a great tooway tooiterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="a554b-122">toomove een sectie in een werkmap, klikt u op Hallo **omhoog** of **omlaag** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a554b-122">toomove up a section in a workbook, click hello **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="a554b-123">een sectie tooremove permanent, klikt u op Hallo **verwijderen** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a554b-123">tooremove a section permanently, click hello **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="a554b-124">Gebruik gegevensvisualisatie secties toevoegen</span><span class="sxs-lookup"><span data-stu-id="a554b-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="a554b-125">Werkmappen bieden vier typen ingebouwde gebruik analytics visualisaties.</span><span class="sxs-lookup"><span data-stu-id="a554b-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="a554b-126">Alle antwoorden op een algemene vraag over het gebruik van Hallo van uw app.</span><span class="sxs-lookup"><span data-stu-id="a554b-126">Each answers a common question about hello usage of your app.</span></span> <span data-ttu-id="a554b-127">tooadd tabellen en grafieken dan deze vier secties toevoegen Analytics query secties (Zie hieronder).</span><span class="sxs-lookup"><span data-stu-id="a554b-127">tooadd tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="a554b-128">tooadd gebruikers, sessies, gebeurtenissen of bewaren sectie tooyour werkmap, gebruik Hallo **gebruikers toevoegen** of andere bijbehorende knop onderaan Hallo Hallo werkmap of Hallo onder een willekeurig gedeelte aan.</span><span class="sxs-lookup"><span data-stu-id="a554b-128">tooadd a Users, Sessions, Events, or Retention section tooyour workbook, use hello **Add Users** or other corresponding button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

![De sectie gebruikers in werkmappen](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="a554b-130">**Gebruikers** secties beantwoorden 'hoeveel gebruikers een pagina weergegeven of gebruikt een functie van Mijn site?'</span><span class="sxs-lookup"><span data-stu-id="a554b-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="a554b-131">**Sessies** secties beantwoorden 'hoeveel sessies gebruikers hoeven te besteden aan een pagina te bekijken of met bepaalde functie van Mijn site?'</span><span class="sxs-lookup"><span data-stu-id="a554b-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="a554b-132">**Gebeurtenissen** secties beantwoorden ' hoe vaak gebruikers bepaalde pagina bekijken of bepaalde functie van Mijn site gebruiken?'</span><span class="sxs-lookup"><span data-stu-id="a554b-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="a554b-133">Elk van deze drie sectietypen biedt Hallo dezelfde set besturingselementen en visualisaties:</span><span class="sxs-lookup"><span data-stu-id="a554b-133">Each of these three section types offers hello same sets of controls and visualizations:</span></span>

* [<span data-ttu-id="a554b-134">Meer informatie over het bewerken van gebruikers, sessies en gebeurtenissen secties</span><span class="sxs-lookup"><span data-stu-id="a554b-134">Learn more about editing Users, Sessions, and Events sections</span></span>](app-insights-usage-segmentation.md)
* <span data-ttu-id="a554b-135">Hallo belangrijkste grafiek, histogram rasters, automatische insights en voorbeeld gebruikers visualisaties Hallo met in-of uitschakelen **grafiek weergeven**, **raster weergeven**, **Insights weergeven**, en **Voorbeeld van deze gebruikers** selectievakjes boven Hallo van elke sectie.</span><span class="sxs-lookup"><span data-stu-id="a554b-135">Toggle hello main chart, histogram grids, automatic insights, and sample users visualizations using hello **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at hello top of each section.</span></span>

![De sectie bewaren in werkmappen](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="a554b-137">**Bewaartermijn** secties beantwoorden "Mensen die een pagina weergegeven of bepaalde functie op een dag of week gebruikt, hoeveel afkomstig terug in de volgende dag of week?"</span><span class="sxs-lookup"><span data-stu-id="a554b-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* [<span data-ttu-id="a554b-138">Meer informatie over het bewerken van retentie secties</span><span class="sxs-lookup"><span data-stu-id="a554b-138">Learn more about editing Retention sections</span></span>](app-insights-usage-retention.md)
* <span data-ttu-id="a554b-139">Wisselknop Hallo optionele algehele bewaren grafiek met Hallo **weergeven algehele bewaren grafiek** selectievakje Hallo boven aan het Hallo-sectie.</span><span class="sxs-lookup"><span data-stu-id="a554b-139">Toggle hello optional Overall Retention chart using hello **Show overall retention chart** checkbox at hello top of hello section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="a554b-140">Application Insights Analytics secties toevoegen</span><span class="sxs-lookup"><span data-stu-id="a554b-140">Adding Application Insights Analytics sections</span></span>

![Analytics-sectie in werkmappen](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="a554b-142">een Application Insights Analytics query sectie tooyour-werkmap tooadd hello gebruiken **toevoegen Analytics query** knop onderaan Hallo Hallo werkmap of Hallo onder een willekeurig gedeelte aan.</span><span class="sxs-lookup"><span data-stu-id="a554b-142">tooadd an Application Insights Analytics query section tooyour workbook, use hello **Add Analytics query** button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

<span data-ttu-id="a554b-143">Analytics query secties kunnen u het toevoegen van willekeurige query's via uw Application Insights-gegevens in werkmappen.</span><span class="sxs-lookup"><span data-stu-id="a554b-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="a554b-144">Deze flexibiliteit betekent Analytics query secties moet uw Ga-toofor het beantwoorden van vragen over uw site dan Hallo vier bovenstaande voor gebruikers, sessies, gebeurtenissen en retentie, zoals:</span><span class="sxs-lookup"><span data-stu-id="a554b-144">This flexibility means Analytics query sections should be your go-toofor answering any questions about your site other than hello four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="a554b-145">Het aantal uitzonderingen heeft uw site throw tijdens Hallo dezelfde periode zijn opgegeven als een daling gebruik?</span><span class="sxs-lookup"><span data-stu-id="a554b-145">How many exceptions did your site throw during hello same time period as a decline in usage?</span></span>
* <span data-ttu-id="a554b-146">Wat is Hallo distributie van laadtijden voor pagina's voor gebruikers die bepaalde pagina bekijken?</span><span class="sxs-lookup"><span data-stu-id="a554b-146">What was hello distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="a554b-147">Hoeveel gebruikers bepaalde set pagina's weergegeven op uw site, maar niet in een andere set pagina's?</span><span class="sxs-lookup"><span data-stu-id="a554b-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="a554b-148">Dit kan handig toounderstand zijn als u clusters van gebruikers die gebruikmaken van verschillende subsets van functionaliteit van uw site hebt (gebruik Hallo `join` operator Hello `kind=leftanti` aanpassingsfunctie in Hallo Log Analytics query language).</span><span class="sxs-lookup"><span data-stu-id="a554b-148">This can be useful toounderstand if you have clusters of users who use different subsets of your site's functionality (use hello `join` operator with hello `kind=leftanti` modifier in hello Log Analytics query language).</span></span>

<span data-ttu-id="a554b-149">Gebruik Hallo [Log Analytics query language reference](https://docs.loganalytics.io/) toolearn meer over het schrijven van query's.</span><span class="sxs-lookup"><span data-stu-id="a554b-149">Use hello [Log Analytics query language reference](https://docs.loganalytics.io/) toolearn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="a554b-150">Tekst- en Markdown secties toe te voegen</span><span class="sxs-lookup"><span data-stu-id="a554b-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="a554b-151">Het toevoegen van koppen, uitleg en commentaar tooyour werkmappen, kunt een set van tabellen en grafieken omzetten in sprekersnotities.</span><span class="sxs-lookup"><span data-stu-id="a554b-151">Adding headings, explanations, and commentary tooyour workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="a554b-152">Secties in werkmappen tekst hello ondersteunen [Markdown-syntaxis](https://daringfireball.net/projects/markdown/) voor tekstopmaak, zoals kopteksten, vet, cursief en lijsten met opsommingstekens.</span><span class="sxs-lookup"><span data-stu-id="a554b-152">Text sections in workbooks support hello [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="a554b-153">een werkmap tooyour van tekst sectie tooadd gebruiken Hallo **tekst toevoegen** knop onderaan Hallo Hallo werkmap of Hallo onder een willekeurig gedeelte aan.</span><span class="sxs-lookup"><span data-stu-id="a554b-153">tooadd a text section tooyour workbook, use hello **Add text** button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="a554b-154">Opslaan en delen van werkmappen met uw team</span><span class="sxs-lookup"><span data-stu-id="a554b-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="a554b-155">Werkmappen zijn opgeslagen in een Application Insights-resource in Hallo **mijn rapporten** sectie persoonlijke tooyou of in Hallo **gedeeld rapporten** sectie toegankelijk tooeveryone met toegang toohello Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="a554b-155">Workbooks are saved within an Application Insights resource, either in hello **My Reports** section that's private tooyou or in hello **Shared Reports** section that's accessible tooeveryone with access toohello Application Insights resource.</span></span> <span data-ttu-id="a554b-156">tooview alle Hallo werkmappen in Hallo resource, klikt u op Hallo **Open** knop in de actiebalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="a554b-156">tooview all hello workbooks in hello resource, click hello **Open** button in hello action bar.</span></span>

<span data-ttu-id="a554b-157">een werkmap die momenteel tooshare **mijn rapporten**:</span><span class="sxs-lookup"><span data-stu-id="a554b-157">tooshare a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="a554b-158">Klik op **Open** in de actiebalk Hallo</span><span class="sxs-lookup"><span data-stu-id="a554b-158">Click **Open** in hello action bar</span></span>
2. <span data-ttu-id="a554b-159">Klik op de knop '...' hello naast Hallo werkmap gewenste tooshare</span><span class="sxs-lookup"><span data-stu-id="a554b-159">Click hello "..." button beside hello workbook you want tooshare</span></span>
3. <span data-ttu-id="a554b-160">Klik op **tooShared rapporten verplaatsen**.</span><span class="sxs-lookup"><span data-stu-id="a554b-160">Click **Move tooShared Reports**.</span></span>

<span data-ttu-id="a554b-161">tooshare een werkmap met een koppeling of via e-mail, klikt u op **Share** in de actiebalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="a554b-161">tooshare a workbook with a link or via email, click **Share** in hello action bar.</span></span> <span data-ttu-id="a554b-162">Houd er rekening mee dat ontvangers van Hallo koppeling toegang toothis resource in hello Azure portal tooview Hallo werkmap tot moeten.</span><span class="sxs-lookup"><span data-stu-id="a554b-162">Keep in mind that recipients of hello link need access toothis resource in hello Azure portal tooview hello workbook.</span></span> <span data-ttu-id="a554b-163">bewerkingen van toomake ontvangers moeten ten minste Inzender-rechten voor Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="a554b-163">toomake edits, recipients need at least Contributor permissions for hello resource.</span></span>

<span data-ttu-id="a554b-164">een koppeling tooa werkmap tooan Azure Dashboard toopin:</span><span class="sxs-lookup"><span data-stu-id="a554b-164">toopin a link tooa workbook tooan Azure Dashboard:</span></span>

1. <span data-ttu-id="a554b-165">Klik op **Open** in de actiebalk Hallo</span><span class="sxs-lookup"><span data-stu-id="a554b-165">Click **Open** in hello action bar</span></span>
2. <span data-ttu-id="a554b-166">Klik op de knop '...' hello naast Hallo werkmap gewenste toopin</span><span class="sxs-lookup"><span data-stu-id="a554b-166">Click hello "..." button beside hello workbook you want toopin</span></span>
3. <span data-ttu-id="a554b-167">Klik op **pincode toodashboard**.</span><span class="sxs-lookup"><span data-stu-id="a554b-167">Click **Pin toodashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a554b-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a554b-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="a554b-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a554b-169">Next steps</span></span>
- <span data-ttu-id="a554b-170">Gebruik tooenable optreedt, te beginnen met het verzenden [aangepaste gebeurtenissen](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) of [paginaweergaven](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="a554b-170">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="a554b-171">Als u al aangepaste gebeurtenissen of paginaweergaven verkennen Hallo gebruik hulpprogramma's voor toolearn verzendt hoe gebruikers de service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a554b-171">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="a554b-172">Gebruikers, sessies, gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="a554b-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="a554b-173">Trechters</span><span class="sxs-lookup"><span data-stu-id="a554b-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="a554b-174">Retentie</span><span class="sxs-lookup"><span data-stu-id="a554b-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="a554b-175">Gebruikersstromen</span><span class="sxs-lookup"><span data-stu-id="a554b-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="a554b-176">Gebruikerscontext toevoegen</span><span class="sxs-lookup"><span data-stu-id="a554b-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    

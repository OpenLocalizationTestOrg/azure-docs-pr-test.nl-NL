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
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a>Onderzoek en gebruiksgegevens delen met interactieve werkmappen in Application Insights

Werkmappen combineren [Azure Application Insights](app-insights-overview.md) gegevensvisualisaties, [analysequery's](app-insights-analytics.md), en tekst in de interactieve documenten. Werkmappen kunnen worden bewerkt door andere teamleden met toegang toohello dezelfde Azure-resource. Dit betekent dat het Hallo-query's en besturingselementen gebruikte toocreate een werkmap zijn beschikbaar tooother mensen lezen Hallo werkmap, zodat ze gemakkelijk tooexplore, uitbreiden en controleren op fouten.

Werkmappen worden gebruikt voor scenario's zoals:

* Hallo informatie over het gebruik van uw app verkennen wanneer u niet Hallo metrische gegevens van belang van tevoren weet: aantal gebruikers, retentie, conversie tarieven, enzovoort. In tegenstelling tot andere gebruik hulpprogramma's voor webanalyse in Application Insights kunnen werkmappen u meerdere soorten visualisaties en analyses, waardoor ze ideaal voor dit soort vrije vorm exploratie combineren.
* Waarin wordt uitgelegd hoe u een nieuw uitgebrachte functie presteert tooyour-team, door de gebruiker weergegeven aantallen voor belangrijke interacties en andere metrische gegevens.
* Delen Hallo resultaten van een A / B-experiment in uw app met andere leden van uw team. U kunt uitleggen Hallo doelstellingen voor Hallo experimenteren met tekst en vervolgens elk gebruik van metrische gegevens weergeven en Analytics query tooevaluate Hallo experiment, samen met duidelijke call-outs voor of elke metriek boven - of hieronder-doel is gebruikt.
* Hallo-impact van een storing op Hallo informatie over het gebruik van uw app, het combineren van gegevens, tekstuitleg en een beschrijving van de volgende stappen tooprevent storingen in toekomstige Hallo rapportage.

> [!NOTE]
> Uw Application Insights-resource moet paginaweergaven of aangepaste gebeurtenissen toouse werkmappen bevatten. [Meer informatie over hoe tooset van uw app toocollect pagina automatisch bekijkt Hello Application Insights JavaScript SDK](app-insights-javascript.md).
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a>Bewerken, rangschikken, klonen en secties van de werkmap verwijderen

Is een werkmap een en-klare van secties: onafhankelijk bewerkbare gebruik visualisaties, grafieken, tabellen, tekst of Analytics queryresultaten.

tooedit hello inhoud van een sectie werkmap, klikt u op Hallo **bewerken** hieronder en toohello rechtsboven in de sectie van de werkmap Hallo.

![Application Insights werkmappen sectie besturingselementen bewerken](./media/app-insights-usage-workbooks/editing-controls.png)

1. Wanneer u klaar bent u een sectie bewerkt, klikt u op **gedaan bewerken** in de linkeronderhoek van Hallo sectie Hallo.

2. toocreate een duplicaat van een sectie, klikt u op Hallo **klonen in deze sectie** pictogram. Dubbele secties maken is een uitstekende tooway tooiterate van een query zonder verlies van vorige iteraties.

3. toomove een sectie in een werkmap, klikt u op Hallo **omhoog** of **omlaag** pictogram.

4. een sectie tooremove permanent, klikt u op Hallo **verwijderen** pictogram.

## <a name="adding-usage-data-visualization-sections"></a>Gebruik gegevensvisualisatie secties toevoegen

Werkmappen bieden vier typen ingebouwde gebruik analytics visualisaties. Alle antwoorden op een algemene vraag over het gebruik van Hallo van uw app. tooadd tabellen en grafieken dan deze vier secties toevoegen Analytics query secties (Zie hieronder).

tooadd gebruikers, sessies, gebeurtenissen of bewaren sectie tooyour werkmap, gebruik Hallo **gebruikers toevoegen** of andere bijbehorende knop onderaan Hallo Hallo werkmap of Hallo onder een willekeurig gedeelte aan.

![De sectie gebruikers in werkmappen](./media/app-insights-usage-workbooks/users-section.png)

**Gebruikers** secties beantwoorden 'hoeveel gebruikers een pagina weergegeven of gebruikt een functie van Mijn site?'

**Sessies** secties beantwoorden 'hoeveel sessies gebruikers hoeven te besteden aan een pagina te bekijken of met bepaalde functie van Mijn site?'

**Gebeurtenissen** secties beantwoorden ' hoe vaak gebruikers bepaalde pagina bekijken of bepaalde functie van Mijn site gebruiken?'

Elk van deze drie sectietypen biedt Hallo dezelfde set besturingselementen en visualisaties:

* [Meer informatie over het bewerken van gebruikers, sessies en gebeurtenissen secties](app-insights-usage-segmentation.md)
* Hallo belangrijkste grafiek, histogram rasters, automatische insights en voorbeeld gebruikers visualisaties Hallo met in-of uitschakelen **grafiek weergeven**, **raster weergeven**, **Insights weergeven**, en **Voorbeeld van deze gebruikers** selectievakjes boven Hallo van elke sectie.

![De sectie bewaren in werkmappen](./media/app-insights-usage-workbooks/retention-section.png)

**Bewaartermijn** secties beantwoorden "Mensen die een pagina weergegeven of bepaalde functie op een dag of week gebruikt, hoeveel afkomstig terug in de volgende dag of week?"

* [Meer informatie over het bewerken van retentie secties](app-insights-usage-retention.md)
* Wisselknop Hallo optionele algehele bewaren grafiek met Hallo **weergeven algehele bewaren grafiek** selectievakje Hallo boven aan het Hallo-sectie.

## <a name="adding-application-insights-analytics-sections"></a>Application Insights Analytics secties toevoegen

![Analytics-sectie in werkmappen](./media/app-insights-usage-workbooks/analytics-section.png)

een Application Insights Analytics query sectie tooyour-werkmap tooadd hello gebruiken **toevoegen Analytics query** knop onderaan Hallo Hallo werkmap of Hallo onder een willekeurig gedeelte aan.

Analytics query secties kunnen u het toevoegen van willekeurige query's via uw Application Insights-gegevens in werkmappen. Deze flexibiliteit betekent Analytics query secties moet uw Ga-toofor het beantwoorden van vragen over uw site dan Hallo vier bovenstaande voor gebruikers, sessies, gebeurtenissen en retentie, zoals:

* Het aantal uitzonderingen heeft uw site throw tijdens Hallo dezelfde periode zijn opgegeven als een daling gebruik?
* Wat is Hallo distributie van laadtijden voor pagina's voor gebruikers die bepaalde pagina bekijken?
* Hoeveel gebruikers bepaalde set pagina's weergegeven op uw site, maar niet in een andere set pagina's? Dit kan handig toounderstand zijn als u clusters van gebruikers die gebruikmaken van verschillende subsets van functionaliteit van uw site hebt (gebruik Hallo `join` operator Hello `kind=leftanti` aanpassingsfunctie in Hallo Log Analytics query language).

Gebruik Hallo [Log Analytics query language reference](https://docs.loganalytics.io/) toolearn meer over het schrijven van query's.

## <a name="adding-text-and-markdown-sections"></a>Tekst- en Markdown secties toe te voegen

Het toevoegen van koppen, uitleg en commentaar tooyour werkmappen, kunt een set van tabellen en grafieken omzetten in sprekersnotities. Secties in werkmappen tekst hello ondersteunen [Markdown-syntaxis](https://daringfireball.net/projects/markdown/) voor tekstopmaak, zoals kopteksten, vet, cursief en lijsten met opsommingstekens.

een werkmap tooyour van tekst sectie tooadd gebruiken Hallo **tekst toevoegen** knop onderaan Hallo Hallo werkmap of Hallo onder een willekeurig gedeelte aan.

## <a name="saving-and-sharing-workbooks-with-your-team"></a>Opslaan en delen van werkmappen met uw team

Werkmappen zijn opgeslagen in een Application Insights-resource in Hallo **mijn rapporten** sectie persoonlijke tooyou of in Hallo **gedeeld rapporten** sectie toegankelijk tooeveryone met toegang toohello Application Insights-resource. tooview alle Hallo werkmappen in Hallo resource, klikt u op Hallo **Open** knop in de actiebalk Hallo.

een werkmap die momenteel tooshare **mijn rapporten**:

1. Klik op **Open** in de actiebalk Hallo
2. Klik op de knop '...' hello naast Hallo werkmap gewenste tooshare
3. Klik op **tooShared rapporten verplaatsen**.

tooshare een werkmap met een koppeling of via e-mail, klikt u op **Share** in de actiebalk Hallo. Houd er rekening mee dat ontvangers van Hallo koppeling toegang toothis resource in hello Azure portal tooview Hallo werkmap tot moeten. bewerkingen van toomake ontvangers moeten ten minste Inzender-rechten voor Hallo resource.

een koppeling tooa werkmap tooan Azure Dashboard toopin:

1. Klik op **Open** in de actiebalk Hallo
2. Klik op de knop '...' hello naast Hallo werkmap gewenste toopin
3. Klik op **pincode toodashboard**.

## <a name="next-steps"></a>Volgende stappen

## <a name="next-steps"></a>Volgende stappen
- Gebruik tooenable optreedt, te beginnen met het verzenden [aangepaste gebeurtenissen](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) of [paginaweergaven](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Als u al aangepaste gebeurtenissen of paginaweergaven verkennen Hallo gebruik hulpprogramma's voor toolearn verzendt hoe gebruikers de service gebruiken.
    - [Gebruikers, sessies, gebeurtenissen](app-insights-usage-segmentation.md)
    - [Trechters](usage-funnels.md)
    - [Retentie](app-insights-usage-retention.md)
    - [Gebruikersstromen](app-insights-usage-flows.md)
    - [Gebruikerscontext toevoegen](app-insights-usage-send-user-context.md)
    

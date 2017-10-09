---
title: Veelgestelde vragen over de aaaLog Analytics nieuwe logboek zoekopdracht | Microsoft Docs
description: Dit artikel bevat veelgestelde vragen met betrekking tot Hallo upgrade van logboekanalyse toohello nieuwe querytaal.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/27/2017
ms.author: bwren
ms.openlocfilehash: b8664c8329fab0547f270793fa13e8cdd06ba637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-new-log-search-faq-and-known-issues"></a>Meld u nieuwe logboekanalyse Veelgestelde vragen over het zoeken en bekende problemen

Dit artikel bevat veelgestelde vragen en bekende problemen met betrekking tot de upgrade Hallo van [nieuwe querytaal van logboekanalyse toohello](log-analytics-log-search-upgrade.md).  U moet gehele artikel doorlezen voordat u Hallo besluit tooupgrade uw werkruimte.


## <a name="alerts"></a>Waarschuwingen

### <a name="question-i-have-a-lot-of-alert-rules-do-i-need-toocreate-them-again-in-hello-new-language-after-i-upgrade"></a>Vraag: ik heb een groot aantal regels voor waarschuwingen. Moet ik toocreate ze opnieuw in de nieuwe taal Hallo nadat ik een upgrade uitvoeren?  
Nee, zijn uw waarschuwingsregels automatisch geconverteerde toohello nieuwe zoekopdracht taal tijdens de upgrade.  


## <a name="computer-groups"></a>Computergroepen

### <a name="question-im-getting-errors-when-trying-toouse-computer-groups--has-their-syntax-changed"></a>Vraag: Ik krijg fouten bij het toouse computergroepen.  Is de syntaxis ervan gewijzigd?
Ja, gegroepeerd Hallo-syntaxis voor het gebruik van de computer wijzigingen wanneer uw werkruimte wordt bijgewerkt.  Zie [computergroepen in logboekanalyse Meld zoekopdrachten](log-analytics-computer-groups.md) voor meer informatie.

### <a name="known-issue-groups-imported-from-active-directory"></a>Bekende probleem: groepen geïmporteerd vanuit Active Directory
U kunt een query die gebruikmaakt van een computergroep importeren uit Active Directory kan niet op dit moment maken.  Als tijdelijke oplossing totdat dit probleem is opgelost, maak een nieuwe computergroep Hallo geïmporteerd Active Directory-groep met en gebruik vervolgens de nieuwe groep in uw query.

Een voorbeeld van de query toocreate een nieuwe computergroep met geïmporteerde Active Directory-groep is als volgt:

    ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "AD Group Name" and TimeGenerated >= ago(24h) | distinct Computer


## <a name="dashboards"></a>Dashboards

### <a name="question-can-i-still-use-dashboards-in-an-upgraded-workspace"></a>Vraag: Kan ik nog steeds gebruiken dashboards in een bijgewerkte werkruimte?
U kunt doorgaan toouse alle tegels die u hebt toegevoegd te**mijn Dashboard** voordat uw werkruimte is bijgewerkt, maar u niet kunt bewerken die tegels of Voeg nieuwe toe.  U kunt doorgaan toocreate en weergaven met bewerken [ontwerper](log-analytics-view-designer.md) en maakt u dashboards in hello Azure-portal.


## <a name="log-searches"></a>Logboek zoekopdrachten

### <a name="question-i-have-saved-searches-outside-of-my-upgraded-workspace-can-i-convert-them-toohello-new-search-language-automatically"></a>Vraag: ik hebt opgeslagen zoekopdrachten buiten mijn bijgewerkte werkruimte. Kan ik converteren ze toohello nieuwe zoekopdracht taal automatisch?
U kunt elk criterium Hallo taal conversiehulpprogramma in Hallo logboek zoeken pagina tooconvert.  Er is geen methode tooautomatically converteren meerdere zoeken zonder te upgraden Hallo-werkruimte.

### <a name="question-why-are-my-query-results-not-sorted"></a>Vraag: Waarom wordt mijn queryresultaten niet is gesorteerd?
Resultaten worden niet standaard ingeschakeld in de nieuwe querytaal Hallo gesorteerd.  Gebruik Hallo [sorteren operator](https://go.microsoft.com/fwlink/?linkid=856079) toosort uw resultaten worden op een of meer eigenschappen.

### <a name="known-issue-search-results-in-a-list-may-include-properties-with-no-data"></a>Bekende probleem: zoekresultaten in een lijst met eigenschappen zonder gegevens kunnen bevatten
Logboek zoekresultaten in een lijst kunnen eigenschappen zonder gegevens weergeven.  Eerdere tooupgrade deze eigenschappen zou niet opgenomen.  Dit probleem wordt opgelost zodat leeg eigenschappen worden niet weergegeven.

### <a name="known-issue-selecting-a-value-in-a-chart-doesnt-display-detailed-results"></a>Bekende probleem: een waarde te selecteren in een grafiek, biedt geen gedetailleerde resultaten weergeven
Eerdere tooupgrade wanneer u een waarde hebt geselecteerd in een grafiek zou er een gedetailleerde lijst met records met Hallo geselecteerd waarde geretourneerd.  Na de upgrade, worden alleen Hallo één samengevatte regel wordt geretourneerd.  Dit probleem wordt op dat moment onderzocht.

## <a name="log-search-api"></a>API voor zoeken in logboeken

### <a name="question-does-hello-log-search-api-get-updated-after-i-upgrade"></a>Vraag: Wordt Hallo-API van zoekservice Log bijgewerkt nadat ik een upgrade uitvoeren?
Hallo [Log-API van zoekservice](log-analytics-log-search-api.md) bijgewerkte toohello nieuwe zoekopdracht taal nog niet is.  Blijven toouse Hallo verouderde querytaal met deze API, zelfs nadat u een upgrade uitvoeren van uw werkruimte.  Bijgewerkte documentatie zijn binnenkort beschikbaar voor Hallo Log-API van zoekservice wanneer deze wordt bijgewerkt.


## <a name="portals"></a>Portals

### <a name="question-should-i-use-hello-new-advanced-analytics-portal-or-keep-using-hello-log-search-portal"></a>Vraag: Moet ik Hallo nieuwe Advanced Analytics-portal te gebruiken of houden met Hallo logboek zoeken portal?
U ziet een vergelijking van Hallo twee portals op [Portals voor het maken en bewerken van logboek-query's in Azure-logboekanalyse](log-analytics-log-search-portals.md).  Elk heeft verschillende voordelen kunt u ervoor kiezen Hallo beste één voor uw vereisten.  Het algemene toowrite-query's in Hallo Advanced Analytics-portal is en plak ze in andere locaties zoals Designer bekijken.  Lees over [tooconsider problemen](log-analytics-log-search-portals.md#advanced-analytics-portal) die bij het uitvoeren.


## <a name="power-bi"></a>Power BI

### <a name="question-does-anything-change-with-powerbi-integration"></a>Vraag: Verandert met Power BI-integratie
Ja.  Zodra uw werkruimte is bijgewerkt wordt niet langer Hallo-proces voor het exporteren van logboekanalyse gegevens tooPower BI samenwerken.  Eventuele bestaande schema's die u hebt gemaakt voordat u de upgrade wordt uitgeschakeld.  Na de upgrade hello Azure Log Analytics gebruikt hetzelfde platform als Application Insights en gebruik van dezelfde tooexport Log Analytics-query's tooPower BI als verwerken Hallo [Hallo proces tooexport Application Insights tooPower BI query](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).

### <a name="known-issue-power-bi-request-size-limit"></a>Bekende probleem: groottelimiet voor Power BI-aanvraag
Er is een maximale grootte van 8 MB voor een Log Analytics-query die geëxporteerd tooPower BI worden kan.  Deze limiet wordt binnenkort worden verhoogd.


##<a name="powershell-cmdlets"></a>PowerShell-cmdlets

### <a name="question-does-hello-log-search-powershell-cmdlet-get-updated-after-i-upgrade"></a>Vraag: Hallo logboek zoeken PowerShell-cmdlet wordt bijgewerkt nadat ik een upgrade uitvoeren?
Hallo [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults) bijgewerkte toohello nieuwe zoekopdracht taal nog niet is.  Toouse hello verouderde querytaal met deze cmdlet blijven zelfs na de upgrade van uw werkruimte.  Bijgewerkte documentatie zijn binnenkort beschikbaar zijn voor de cmdlet Hallo wanneer deze wordt bijgewerkt.


## <a name="resource-manager-templates"></a>Resource Manager-sjablonen

### <a name="question-can-i-create-an-upgraded-workspace-with-a-resource-manager-template"></a>Vraag: Maak ik een bijgewerkte werkruimte met Resource Manager-sjabloon?
Ja.  U moet gebruiken een API-versie van 2017-03-15-preview en bevatten een **functies** sectie in uw sjabloon zoals in het volgende voorbeeld Hallo.

    "resources": [
        {
            "type": "Microsoft.OperationalInsights/workspaces",
            "apiVersion": "2017-03-15-preview",
            "name": "[parameters('workspaceName')]",
            "location": "[parameters('workspaceRegion')]",
            "properties": {
                "sku": {
                    "name": "Free"
                },
                "features": {
                    "legacy": 0,
                    "searchVersion": 1
                }
            }
        }
    ],



## <a name="solutions"></a>Oplossingen

### <a name="question-will-my-solutions-continue-toowork"></a>Vraag: Mijn oplossingen blijven toowork?
Alle oplossingen blijven toowork in een werkruimte bijgewerkte, hoewel de prestaties verbeteren als ze nieuwe querytaal geconverteerde toohello zijn.  Er zijn bekende problemen met het aantal bestaande oplossingen die in deze sectie worden beschreven.

### <a name="known-issue-capacity-and-performance-solution"></a>Bekende probleem: oplossing capaciteit en prestaties
Sommige onderdelen in Hallo Hallo [capaciteit en prestaties](log-analytics-capacity.md) weergave kan niet leeg zijn.  Een probleem met de oplossing toothis zijn binnenkort beschikbaar.

### <a name="known-issue-device-health-solution"></a>Bekende probleem: Apparaatstatus oplossing
Hallo [Apparaatstatus oplossing](https://docs.microsoft.com/windows/deployment/update/device-health-monitor) gegevens in een bijgewerkte werkruimte worden niet verzameld.  Een probleem met de oplossing toothis zijn binnenkort beschikbaar.

### <a name="known-issue-application-insights-connector"></a>Bekende probleem: Application Insights-connector
Perspectieven in [Application Insights-Connector oplossing](log-analytics-app-insights-connector.md) worden momenteel niet ondersteund in een bijgewerkte werkruimte.  Een probleem met de oplossing toothis wordt momenteel onder analyse.

## <a name="upgrade-process"></a>Het upgradeproces

### <a name="question-i-have-several-workspaces-can-i-upgrade-all-workspaces-at-hello-same-time"></a>Vraag: ik heb meerdere werkruimten. Kan ik een upgrade alle werkruimten op Hallo hetzelfde moment?  
Nee.  Upgrade geldt tooa één werkruimte telkens. Er is momenteel niet mogelijk van de upgrade van veel werkruimten tegelijk. Houd er rekening mee dat andere gebruikers van de werkruimte Hallo bijgewerkt ook worden beïnvloed.  

### <a name="question-will-existing-log-data-collected-in-my-workspace-be-modified-if-i-upgrade"></a>Vraag: Bestaande logboekgegevens verzameld in mijn werkruimte worden aangepast en zullen als ik een upgrade uitvoeren?  
Nee. Hallo logboek gegevens beschikbaar tooyour werkruimte zoekopdrachten wordt niet beïnvloed door het Hallo-upgrade. Opgeslagen zoekopdrachten, waarschuwingen en weergaven worden geconverteerde toohello nieuwe zoekopdracht taal automatisch.  

### <a name="question-what-happens-if-i-dont-upgrade-my-workspace"></a>Vraag: Wat gebeurt er als ik mijn werkruimte niet bijwerken?  
Hallo verouderde logboek zoeken in Hallo maanden die afkomstig zijn afgeschaft. Werkruimten die niet zijn bijgewerkt op dat moment worden automatisch geüpgraded.

### <a name="question-i-didnt-choose-tooupgrade-but-my-workspace-has-been-upgraded-anyway-what-happened"></a>Vraag: ik niet tooupgrade kiezen, maar mijn werkruimte toch is bijgewerkt. Wat is er gebeurd?  
Een andere beheerder van deze werkruimte kan Hallo werkruimte hebt bijgewerkt. Houd er rekening mee dat alle werkruimten automatisch worden bijgewerkt wanneer de nieuwe taal Hallo algemene beschikbaarheid bereikt.  

### <a name="question-i-have-upgraded-by-mistake-and-now-need-toocancel-it-and-restore-everything-back-what-should-i-do"></a>Vraag: ik per ongeluk hebt bijgewerkt en moet nu toocancel deze en terugzetten van back-alles. Wat moet ik doen?  
Geen probleem.  We maken een momentopname van de werkruimte voor de upgrade, zodat u deze kunt herstellen. Houd er rekening mee dat u zoekt, waarschuwingen of weergaven die u na Hallo upgrade echter verloren, worden opgeslagen.  toorestore uw werkruimte-omgeving, volg Hallo procedure op [kan ik gaat u terug wanneer ik een upgrade uitvoeren?](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)


## <a name="views"></a>Weergaven

### <a name="question-how-do-i-create-a-new-view-with-view-designer"></a>Vraag: Hoe maak ik een nieuwe weergave met Designer bekijken?
Eerdere tooupgrade u kunt een nieuwe weergave maken met ontwerper van een tegel op het hoofddashboard Hallo.  Wanneer uw werkruimte is geüpgraded, is deze tegel wordt verwijderd.  U kunt een nieuwe weergave maken met de Designer bekijken in Hallo OMS-portal door te klikken op de knop in het linkermenu Hallo + Hallo groen.

### <a name="known-issue-see-all-option-for-line-charts-in-views-doesnt-result-in-a-line-chart"></a>Bekende probleem: Zie de optie all voor lijndiagrammen in weergaven niet resulteren in een lijndiagram
Wanneer u klikt op op Hallo *alle* optie onderin Hallo van een deel van de grafiek regel in een weergave, krijgt u een tabel.  Eerdere tooupgrade zou u weergegeven met een lijndiagram.  Dit probleem wordt geanalyseerd voor een mogelijke wijziging.


## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [een upgrade van uw werkruimte toohello nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md).

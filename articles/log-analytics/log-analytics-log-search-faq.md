---
title: Log Analytics nieuwe logboek zoekopdracht Veelgestelde vragen | Microsoft Docs
description: Dit artikel bevat veelgestelde vragen met betrekking tot de upgrade van logboekanalyse op de nieuwe querytaal.
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
ms.openlocfilehash: d7bd0d780c265cc15ad09a73ede8c5a886005e37
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-new-log-search-faq-and-known-issues"></a>Meld u nieuwe logboekanalyse Veelgestelde vragen over het zoeken en bekende problemen

In dit artikel bevat veelgestelde vragen en bekende problemen met betrekking tot de upgrade van [logboekanalyse naar de nieuwe querytaal](log-analytics-log-search-upgrade.md).  U moet dit gehele artikel doorlezen voordat u de beslissing om bij te werken uw werkruimte.


## <a name="alerts"></a>Waarschuwingen

### <a name="question-i-have-a-lot-of-alert-rules-do-i-need-to-create-them-again-in-the-new-language-after-i-upgrade"></a>Vraag: ik heb een groot aantal regels voor waarschuwingen. Moet ik ze opnieuw maken in de nieuwe taal nadat ik een upgrade uitvoeren?  
Nee, de regels voor waarschuwingen automatisch geconverteerd naar de nieuwe zoekopdracht taal tijdens de upgrade.  


## <a name="computer-groups"></a>Computergroepen

### <a name="question-im-getting-errors-when-trying-to-use-computer-groups--has-their-syntax-changed"></a>Vraag: Ik krijg fouten bij het gebruik van computergroepen.  Is de syntaxis ervan gewijzigd?
Ja, de syntaxis voor het gebruik van de computer wijzigingen groups wanneer uw werkruimte wordt bijgewerkt.  Zie [computergroepen in logboekanalyse Meld zoekopdrachten](log-analytics-computer-groups.md) voor meer informatie.

### <a name="known-issue-groups-imported-from-active-directory"></a>Bekende probleem: groepen geïmporteerd vanuit Active Directory
U kunt een query die gebruikmaakt van een computergroep importeren uit Active Directory kan niet op dit moment maken.  Als tijdelijke oplossing totdat dit probleem is opgelost, maak een nieuwe computergroep met behulp van de geïmporteerde Active Directory-groep en vervolgens die nieuwe groep in uw query te gebruiken.

Een voorbeeldquery voor het maken van een nieuwe computergroep met geïmporteerde Active Directory-groep is als volgt:

    ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "AD Group Name" and TimeGenerated >= ago(24h) | distinct Computer


## <a name="dashboards"></a>Dashboards

### <a name="question-can-i-still-use-dashboards-in-an-upgraded-workspace"></a>Vraag: Kan ik nog steeds gebruiken dashboards in een bijgewerkte werkruimte?
U kunt blijven gebruiken alle tegels die u hebt toegevoegd aan **mijn Dashboard** voordat uw werkruimte is bijgewerkt, maar u niet kunt bewerken die tegels of Voeg nieuwe toe.  U kunt blijven maken en bewerken van weergaven met [ontwerper](log-analytics-view-designer.md) en ook dashboards maken in de Azure portal.


## <a name="log-searches"></a>Logboek zoekopdrachten

### <a name="question-i-have-saved-searches-outside-of-my-upgraded-workspace-can-i-convert-them-to-the-new-search-language-automatically"></a>Vraag: ik hebt opgeslagen zoekopdrachten buiten mijn bijgewerkte werkruimte. Kan ik converteren ze naar de nieuwe zoekopdracht taal automatisch?
Kunt u het conversiehulpprogramma taal in de zoekpagina logboek converteren van elkaar.  Er is geen methode om automatisch te converteren meerdere zoekacties zonder een upgrade van de werkruimte.

### <a name="question-why-are-my-query-results-not-sorted"></a>Vraag: Waarom wordt mijn queryresultaten niet is gesorteerd?
Resultaten worden niet standaard in de nieuwe querytaal gesorteerd.  Gebruik de [sorteren operator](https://go.microsoft.com/fwlink/?linkid=856079) uw resultaten sorteren op een of meer eigenschappen.

### <a name="known-issue-search-results-in-a-list-may-include-properties-with-no-data"></a>Bekende probleem: zoekresultaten in een lijst met eigenschappen zonder gegevens kunnen bevatten
Logboek zoekresultaten in een lijst kunnen eigenschappen zonder gegevens weergeven.  Vóór upgrade, zou deze eigenschappen niet opgenomen.  Dit probleem wordt opgelost zodat leeg eigenschappen worden niet weergegeven.

### <a name="known-issue-selecting-a-value-in-a-chart-doesnt-display-detailed-results"></a>Bekende probleem: een waarde te selecteren in een grafiek, biedt geen gedetailleerde resultaten weergeven
Wanneer u een waarde hebt geselecteerd in een grafiek, zou er vóór upgrade, een gedetailleerde lijst met records die overeenkomt met de geselecteerde waarde geretourneerd.  Na de upgrade, wordt alleen de samengevatte regel geretourneerd.  Dit probleem wordt op dat moment onderzocht.

## <a name="log-search-api"></a>API voor zoeken in logboeken

### <a name="question-does-the-log-search-api-get-updated-after-i-upgrade"></a>Vraag: De Search-API van het logboek wordt bijgewerkt nadat ik een upgrade uitvoeren?
De [Log-API van zoekservice](log-analytics-log-search-api.md) nog niet zijn bijgewerkt naar de nieuwe zoekopdracht taal.  Blijven de verouderde query language met deze API gebruiken, zelfs nadat u een upgrade uitvoeren van uw werkruimte.  Bijgewerkte documentatie zijn binnenkort beschikbaar voor de API van de zoekservice logboek wanneer deze wordt bijgewerkt.


## <a name="portals"></a>Portals

### <a name="question-should-i-use-the-new-advanced-analytics-portal-or-keep-using-the-log-search-portal"></a>Vraag: Moet ik gebruiken de nieuwe Advanced Analytics-portal of houden via de portal logboek zoeken?
U ziet een vergelijking van de twee portals op [Portals voor het maken en bewerken van logboek-query's in Azure-logboekanalyse](log-analytics-log-search-portals.md).  Elk heeft verschillende voordelen, zodat u de beste is voor uw behoeften kunt kiezen.  Het is gebruikelijk om te schrijven van query's in de portal Advanced Analytics en plak ze in andere locaties zoals Designer bekijken.  Lees over [overwegingen](log-analytics-log-search-portals.md#advanced-analytics-portal) die bij het uitvoeren.


## <a name="power-bi"></a>Power BI

### <a name="question-does-anything-change-with-powerbi-integration"></a>Vraag: Verandert met Power BI-integratie
Ja.  Zodra uw werkruimte is bijgewerkt en vervolgens het proces voor het exporteren van logboekanalyse gegevens met Power BI niet meer werken.  Eventuele bestaande schema's die u hebt gemaakt voordat u de upgrade wordt uitgeschakeld.  Na de upgrade, wordt Azure Log Analytics hetzelfde platform als Application Insights en u hetzelfde proces gebruiken om te exporteren Log Analytics-query's naar Power BI als [het proces voor het exporteren van Application Insights-query's naar Power BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).

### <a name="known-issue-power-bi-request-size-limit"></a>Bekende probleem: groottelimiet voor Power BI-aanvraag
Er is een maximale grootte van 8 MB voor een Log Analytics-query die kan worden geëxporteerd naar Power BI.  Deze limiet wordt binnenkort worden verhoogd.


##<a name="powershell-cmdlets"></a>PowerShell-cmdlets

### <a name="question-does-the-log-search-powershell-cmdlet-get-updated-after-i-upgrade"></a>Vraag: De logboek zoeken PowerShell-cmdlet wordt bijgewerkt nadat ik een upgrade uitvoeren?
De [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults) nog niet zijn bijgewerkt naar de nieuwe zoekopdracht taal.  Blijven de verouderde query language met deze cmdlet gebruiken, zelfs nadat u een upgrade uitvoeren van uw werkruimte.  Bijgewerkte documentatie zijn binnenkort beschikbaar zijn voor de cmdlet wordt bijgewerkt.


## <a name="resource-manager-templates"></a>Resource Manager-sjablonen

### <a name="question-can-i-create-an-upgraded-workspace-with-a-resource-manager-template"></a>Vraag: Maak ik een bijgewerkte werkruimte met Resource Manager-sjabloon?
Ja.  U moet gebruiken een API-versie van 2017-03-15-preview en bevatten een **functies** sectie in uw sjabloon zoals in het volgende voorbeeld.

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

### <a name="question-will-my-solutions-continue-to-work"></a>Vraag: Mijn oplossingen blijven werken?
Alle oplossingen blijven werken in een werkruimte bijgewerkte, hoewel de prestaties verbeteren als ze worden geconverteerd naar de nieuwe querytaal.  Er zijn bekende problemen met het aantal bestaande oplossingen die in deze sectie worden beschreven.

### <a name="known-issue-capacity-and-performance-solution"></a>Bekende probleem: oplossing capaciteit en prestaties
Sommige van de onderdelen in de [capaciteit en prestaties](log-analytics-capacity.md) weergave kan niet leeg zijn.  Een oplossing voor dit probleem zijn binnenkort beschikbaar.

### <a name="known-issue-device-health-solution"></a>Bekende probleem: Apparaatstatus oplossing
De [Apparaatstatus oplossing](https://docs.microsoft.com/windows/deployment/update/device-health-monitor) gegevens in een bijgewerkte werkruimte worden niet verzameld.  Een oplossing voor dit probleem zijn binnenkort beschikbaar.

### <a name="known-issue-application-insights-connector"></a>Bekende probleem: Application Insights-connector
Perspectieven in [Application Insights-Connector oplossing](log-analytics-app-insights-connector.md) worden momenteel niet ondersteund in een bijgewerkte werkruimte.  Een oplossing voor dit probleem wordt momenteel onder analyse.

## <a name="upgrade-process"></a>Het upgradeproces

### <a name="question-i-have-several-workspaces-can-i-upgrade-all-workspaces-at-the-same-time"></a>Vraag: ik heb meerdere werkruimten. Kan ik alle werkruimten op hetzelfde moment bijwerken?  
Nee.  Upgrade van toepassing op een enkele werkruimte telkens. Er is momenteel niet mogelijk van de upgrade van veel werkruimten tegelijk. Houd er rekening mee dat andere gebruikers van de bijgewerkte werkruimte ook worden beïnvloed.  

### <a name="question-will-existing-log-data-collected-in-my-workspace-be-modified-if-i-upgrade"></a>Vraag: Bestaande logboekgegevens verzameld in mijn werkruimte worden aangepast en zullen als ik een upgrade uitvoeren?  
Nee. De logboekgegevens die beschikbaar zijn voor uw werkruimte-zoekopdrachten wordt niet beïnvloed door de upgrade. Opgeslagen zoekopdrachten, wordt waarschuwingen, weergaven en automatisch worden geconverteerd naar de nieuwe zoekopdracht taal.  

### <a name="question-what-happens-if-i-dont-upgrade-my-workspace"></a>Vraag: Wat gebeurt er als ik mijn werkruimte niet bijwerken?  
De verouderde logboek zoekopdracht wordt in de komende maanden afgeschaft. Werkruimten die niet zijn bijgewerkt op dat moment worden automatisch geüpgraded.

### <a name="question-i-didnt-choose-to-upgrade-but-my-workspace-has-been-upgraded-anyway-what-happened"></a>Vraag: ik niet kiezen om bij te werken, maar mijn werkruimte toch is bijgewerkt. Wat is er gebeurd?  
Een andere beheerder van deze werkruimte kan de werkruimte zijn bijgewerkt. Houd er rekening mee dat alle werkruimten automatisch worden bijgewerkt wanneer de nieuwe taal algemene beschikbaarheid is bereikt.  

### <a name="question-i-have-upgraded-by-mistake-and-now-need-to-cancel-it-and-restore-everything-back-what-should-i-do"></a>Vraag: ik per ongeluk hebt bijgewerkt en nu wilt annuleren en alles terug te zetten. Wat moet ik doen?  
Geen probleem.  We maken een momentopname van de werkruimte voor de upgrade, zodat u deze kunt herstellen. Houd er rekening mee dat u zoekt, waarschuwingen of weergaven die u na de upgrade echter verloren, worden opgeslagen.  Volg de procedure op voor het herstellen van uw omgeving werkruimte [kan ik gaat u terug wanneer ik een upgrade uitvoeren?](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)


## <a name="views"></a>Weergaven

### <a name="question-how-do-i-create-a-new-view-with-view-designer"></a>Vraag: Hoe maak ik een nieuwe weergave met Designer bekijken?
U kunt voorafgaande aan de upgrade een nieuwe weergave maken met ontwerper van een tegel op het hoofddashboard.  Wanneer uw werkruimte is geüpgraded, is deze tegel wordt verwijderd.  U kunt een nieuwe weergave maken met de Designer bekijken in de OMS-portal door te klikken op de groene + knop in het menu links.

### <a name="known-issue-see-all-option-for-line-charts-in-views-doesnt-result-in-a-line-chart"></a>Bekende probleem: Zie de optie all voor lijndiagrammen in weergaven niet resulteren in een lijndiagram
Wanneer u klikt op in de *alle* optie onder aan een deel van de grafiek regel in een weergave, krijgt u een tabel.  Vóór upgrade, zou u worden gepresenteerd met een lijndiagram.  Dit probleem wordt geanalyseerd voor een mogelijke wijziging.


## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [uw werkruimte upgraden naar de nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md).

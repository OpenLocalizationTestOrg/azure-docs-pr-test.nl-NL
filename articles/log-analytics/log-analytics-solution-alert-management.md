---
title: aaaAlert beheeroplossing in Operations Management Suite (OMS) | Microsoft Docs
description: Hallo waarschuwing beheeroplossing in Log Analytics kunt u alle Hallo waarschuwingen in uw omgeving te analyseren.  In aanvulling tooconsolidating waarschuwingen gegenereerd in OMS, importeert deze waarschuwingen van verbonden beheergroepen van System Center Operations Manager in logboekanalyse.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fe5d534e-0418-4e2f-9073-8025e13271a8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: aff9bd8d88839c5227bb9ec3a1b5209a3cd7cdf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="alert-management-solution-in-operations-management-suite-oms"></a>Oplossing voor waarschuwingen in Operations Management Suite (OMS)

![Pictogram voor het beheer van waarschuwing](media/log-analytics-solution-alert-management/icon.png)

Hallo waarschuwingenbeheer oplossing helpt u bij analyseren van alle Hallo waarschuwingen in de opslagplaats logboekanalyse.  Deze waarschuwingen hebben afkomstig zijn uit verschillende bronnen, met inbegrip van deze bronnen [gemaakt door logboekanalyse](log-analytics-alerts.md) of [geïmporteerd uit Nagios of Zabbix](log-analytics-linux-agents.md).  Hallo oplossing ook importeert waarschuwingen van een [System Center Operations Manager-beheergroepen verbonden](log-analytics-om-agents.md).

## <a name="prerequisites"></a>Vereisten
Hallo-oplossing werkt met alle records in Hallo Log Analytics-opslagplaats met een type **waarschuwing**, dus u moet uitvoeren met de configuratie is vereist toocollect deze records.

- Voor logboekanalyse waarschuwingen, [waarschuwingsregels maken](log-analytics-alerts.md) toocreate waarschuwing records rechtstreeks in het Hallo-opslagplaats.
- Voor Nagios en Zabbix waarschuwingen, [configureren die servers](log-analytics-linux-agents.md) toosend tooLog Analytics waarschuwingen.
- Voor System Center Operations Manager-waarschuwingen [verbinding maken met Operations Manager management groep tooyour werkruimte voor logboekanalyse](log-analytics-om-agents.md).  Alle waarschuwingen die zijn gemaakt in System Center Operations Manager worden geïmporteerd in logboekanalyse.  

## <a name="configuration"></a>Configuratie
Hallo waarschuwingenbeheer oplossing tooyour OMS-werkruimte met behulp van Hallo proces dat wordt beschreven in toevoegen [oplossingen toevoegen](log-analytics-add-solutions.md).  Er is geen verdere configuratie nodig.

## <a name="management-packs"></a>Management packs
Als uw System Center Operations Manager-beheergroep verbonden tooyour OMS-werkruimte, worden waarna Hallo volgende management packs geïnstalleerd in System Center Operations Manager bij het toevoegen van deze oplossing.  Er is geen configuratie of onderhoud van Hallo management packs is vereist.  

* Microsoft System Center Advisor waarschuwing Management (Microsoft.IntelligencePacks.AlertManagement)

Zie voor meer informatie over hoe de oplossing management packs worden bijgewerkt, [verbinding maken met Operations Manager tooLog Analytics](log-analytics-om-agents.md).

## <a name="data-collection"></a>Gegevensverzameling
### <a name="agents"></a>Agents
Hallo volgende tabel beschrijft Hallo verbonden gegevensbronnen die worden ondersteund door deze oplossing.

| Verbonden bron | Ondersteuning | Beschrijving |
|:--- |:--- |:--- |
| [Windows-agents](log-analytics-windows-agents.md) | Nee |Directe Windows-agents genereren geen waarschuwingen.  Log Analytics waarschuwingen kunnen worden gemaakt van gebeurtenissen en prestatiegegevens verzameld via Windows-agents. |
| [Linux-agents](log-analytics-linux-agents.md) | Nee |Directe Linux-agents genereren geen waarschuwingen.  Log Analytics waarschuwingen kunnen worden gemaakt van gebeurtenissen en prestatiegegevens verzameld van Linux-agents.  Nagios en Zabbix waarschuwingen worden verzameld van deze servers waarvoor Hallo Linux-agent. |
| [System Center Operations Manager-beheergroep](log-analytics-om-agents.md) |Ja |Waarschuwingen die worden gegenereerd op de Operations Manager-agents zijn geleverd toohello-beheergroep en vervolgens doorgestuurd tooLog Analytics.<br><br>Een rechtstreekse verbinding tussen Operations Manager-agents tooLog Analytics is niet vereist. Waarschuwing gegevens doorgestuurd vanuit Hallo management groep toohello logboekanalyse opslagplaats. |


### <a name="collection-frequency"></a>Verzamelingsfrequentie
- Waarschuwing records zijn beschikbaar toohello oplossing zodra ze worden opgeslagen in het Hallo-opslagplaats.
- Waarschuwing gegevens worden verzonden vanuit Hallo Operations Manager management groep tooLog Analytics elke drie minuten.  

## <a name="using-hello-solution"></a>Met behulp van Hallo-oplossing
Wanneer u Hallo waarschuwingenbeheer oplossing tooyour OMS-werkruimte toevoegt, Hallo **waarschuwingenbeheer** tegel tooyour OMS dashboard is toegevoegd.  Deze tegel wordt weergegeven voor een aantal en de grafische weergave van Hallo aantal actieve waarschuwingen die zijn gegenereerd binnen Hallo afgelopen 24 uur.  U kunt dit tijdsbereik niet wijzigen.

![Waarschuwing Management tegel](media/log-analytics-solution-alert-management/tile.png)

Klik op Hallo **waarschuwingenbeheer** tegel tooopen hello **waarschuwingenbeheer** dashboard.  Hallo dashboard bevat Hallo kolommen in de volgende tabel Hallo.  Elke kolom bevat Hallo bovenste 10 waarschuwingen per aantal die overeenkomt met dat van de kolom criteria voor Hallo bereik en tijdbereik opgegeven.  U kunt een zoekopdracht logboek waarmee de volledige lijst Hallo door te klikken op uitvoeren **alle** onderin Hallo van Hallo kolom of door te klikken op de kolomkop Hallo.

| Kolom | Beschrijving |
|:--- |:--- |
| Kritieke waarschuwingen |Alle waarschuwingen weergegeven met een ernst kritiek gegroepeerd op de naam van waarschuwing.  Klik op een naam van waarschuwing toorun een logboek zoekopdracht retourneren van alle records voor deze waarschuwing. |
| Waarschuwingen |Alle waarschuwingen weergegeven met een ernst van waarschuwing gegroepeerd op de naam van waarschuwing.  Klik op een naam van waarschuwing toorun een logboek zoekopdracht retourneren van alle records voor deze waarschuwing. |
| Actieve SCOM-waarschuwingen |Alle waarschuwingen die zijn verzameld uit Operations Manager met elke status anders dan *gesloten* gegroepeerd op de bron die gegenereerde Hallo-waarschuwing. |
| Alle actieve waarschuwingen |Alle waarschuwingen weergegeven met alle ernst gegroepeerd op de naam van waarschuwing. Alleen dan bevat Operations Manager-waarschuwingen met elke status *gesloten*. |

Als u toohello rechts schuift, Hallo dashboard bevat enkele algemene query's die u kunt tooperform op een [logboek zoeken](log-analytics-log-searches.md) voor waarschuwingsgegevens.

![Waarschuwing Management dashboard](media/log-analytics-solution-alert-management/dashboard.png)


## <a name="log-analytics-records"></a>Log Analytics-records
Hallo waarschuwingenbeheer oplossing analyseert elke record met een type **waarschuwing**.  Waarschuwingen gemaakt met logboekanalyse of verzameld van Nagios of Zabbix worden niet rechtstreeks verzameld door Hallo-oplossing.

Hallo-oplossing waarschuwingen importeren uit System Center Operations Manager en maakt u een record voor elk met een type **waarschuwing** en een SourceSystem van **OpsManager**.  Deze records hebben Hallo eigenschappen in de volgende tabel Hallo:  

| Eigenschap | Beschrijving |
|:--- |:--- |
| Type |*Een waarschuwing* |
| SourceSystem |*OpsManager* |
| AlertContext |Details van gegevensitem Hallo waardoor Hallo waarschuwing toobe gegenereerd in XML-indeling. |
| AlertDescription |Gedetailleerde beschrijving van waarschuwing Hallo. |
| AlertId |GUID van Hallo waarschuwing. |
| AlertName |Naam van het Hallo-waarschuwing. |
| AlertPriority |Het prioriteitsniveau van Hallo waarschuwing. |
| AlertSeverity |Ernst van waarschuwing Hallo. |
| AlertState |Meest recente oplossingsstatus van Hallo waarschuwing. |
| LastModifiedBy |Naam van het Hallo-gebruiker die het Hallo-waarschuwing laatst is gewijzigd. |
| ManagementGroupName |Naam van beheergroep Hallo waar Hallo waarschuwing is gegenereerd. |
| RepeatCount |Aantal keren Hallo dezelfde waarschuwing is gegenereerd voor Hallo die dezelfde object bewaakt omdat het wordt omgezet. |
| ResolvedBy |Naam van het Hallo-gebruiker die Hallo waarschuwing opgelost. Leeg als Hallo waarschuwing nog niet opgelost is. |
| SourceDisplayName |Weergavenaam van Hallo bewakingsobject dat Hallo waarschuwing heeft gegenereerd. |
| SourceFullName |Volledige naam van Hallo bewakingsobject dat Hallo waarschuwing heeft gegenereerd. |
| TicketId |Ticket-ID voor de waarschuwing Hallo als Hallo System Center Operations Manager-omgeving is geïntegreerd met een proces voor het toewijzen van tickets voor waarschuwingen.  Lege van er is geen ticket-ID is toegewezen. |
| TimeGenerated |Datum en tijd waarop de waarschuwing Hallo is gemaakt. |
| TimeLastModified |Datum en tijd waarop de waarschuwing Hallo voor het laatst is gewijzigd. |
| TimeRaised |Datum en tijd waarop Hallo waarschuwing is gegenereerd. |
| TimeResolved |Datum en tijd waarop Hallo waarschuwing is opgelost. Leeg als Hallo waarschuwing nog niet opgelost is. |

## <a name="sample-log-searches"></a>Voorbeeldzoekopdrachten in logboeken
Hallo bevat volgende tabel voorbeelden logboek zoekt waarschuwing records die door deze oplossing worden verzameld: 

| Query’s uitvoeren | Beschrijving |
|:--- |:--- |
| Type waarschuwing SourceSystem = OpsManager AlertSeverity = fout TimeRaised = > nu 24 uur |Kritieke waarschuwingen die zijn gegenereerd tijdens het Hallo afgelopen 24 uur |
| Type waarschuwing AlertSeverity = waarschuwing TimeRaised = > nu 24 uur |Waarschuwingen die zijn gegenereerd tijdens het Hallo afgelopen 24 uur |
| Type waarschuwing SourceSystem = OpsManager AlertState =! gesloten TimeRaised = > nu - 24-UURS &#124; meting count() als tellen per SourceDisplayName |Bronnen met actieve waarschuwingen die zijn gegenereerd tijdens het Hallo afgelopen 24 uur |
| Type waarschuwing SourceSystem = OpsManager AlertSeverity = fout TimeRaised = > nu 24 uur AlertState! = gesloten |Kritieke waarschuwingen die zijn gegenereerd tijdens het Hallo afgelopen 24 uur die nog steeds actief zijn |
| Type waarschuwing SourceSystem = OpsManager TimeRaised = > nu 24 uur AlertState = gesloten |Waarschuwingen die zijn gegenereerd tijdens het Hallo afgelopen 24 uur die nu zijn gesloten |
| Type waarschuwing SourceSystem = OpsManager TimeRaised = > nu 1 dag &#124; meting count() als tellen per AlertSeverity |Waarschuwingen die in de afgelopen dag zijn gegroepeerd op hun ernst Hallo geactiveerd |
| Type waarschuwing SourceSystem = OpsManager TimeRaised = > nu 1 dag &#124; RepeatCount desc sorteren |Waarschuwingen die zijn gegenereerd tijdens het Hallo afgelopen dag zijn gesorteerd op basis van hun waarde aantal herhalingen |


>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), Hallo voorgaande query's zou Wijzig toohello volgende:
>
>| Query’s uitvoeren | Beschrijving |
|:---|:---|
| Waarschuwing &#124; waar SourceSystem == 'OpsManager' en AlertSeverity == "error" en TimeRaised > ago(24h) |Kritieke waarschuwingen die zijn gegenereerd tijdens het Hallo afgelopen 24 uur |
| Waarschuwing &#124; waar AlertSeverity == 'waarschuwing' en TimeRaised > ago(24h) |Waarschuwingen die zijn gegenereerd tijdens het Hallo afgelopen 24 uur |
| Waarschuwing &#124; waar SourceSystem == 'OpsManager' en AlertState! = 'Gesloten' en TimeRaised > ago(24h) &#124; Aantal samenvatten count() door SourceDisplayName = |Bronnen met actieve waarschuwingen die zijn gegenereerd tijdens het Hallo afgelopen 24 uur |
| Waarschuwing &#124; waar SourceSystem == 'OpsManager' en AlertSeverity == "error" en TimeRaised > ago(24h) en AlertState! = 'Gesloten' |Kritieke waarschuwingen die zijn gegenereerd tijdens het Hallo afgelopen 24 uur die nog steeds actief zijn |
| Waarschuwing &#124; waar SourceSystem == 'OpsManager' en TimeRaised > ago(24h) en AlertState == 'Gesloten' |Waarschuwingen die zijn gegenereerd tijdens het Hallo afgelopen 24 uur die nu zijn gesloten |
| Waarschuwing &#124; waar SourceSystem == 'OpsManager' en TimeRaised > ago(1d) &#124; Aantal samenvatten count() door AlertSeverity = |Waarschuwingen die in de afgelopen dag zijn gegroepeerd op hun ernst Hallo geactiveerd |
| Waarschuwing &#124; waar SourceSystem == 'OpsManager' en TimeRaised > ago(1d) &#124; sorteren op RepeatCount desc |Waarschuwingen die zijn gegenereerd tijdens het Hallo afgelopen dag zijn gesorteerd op basis van hun waarde aantal herhalingen |


## <a name="next-steps"></a>Volgende stappen
* Zie [Understanding alerts in Log Analytics](log-analytics-alerts.md) voor meer informatie over het genereren van waarschuwingen van Log Analytics.

---
title: aaaCollect en analyseren van Windows-gebeurtenislogboeken in OMS Log Analytics | Microsoft Docs
description: Windows-gebeurtenislogboeken zijn Hallo meest algemene gegevensbronnen die worden gebruikt door logboekanalyse.  In dit artikel wordt beschreven hoe tooconfigure verzameling van Windows-gebeurtenislogboeken en de details van records Hallo ze in Hallo OMS-opslagplaats maken.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: ee52f564-995b-450f-a6ba-0d7b1dac3f32
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: c05648af39258443f22fd11e1d751b5ccec8c391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-event-log-data-sources-in-log-analytics"></a>Gegevensbronnen van de Windows-gebeurtenislogboek in Log Analytics
Windows-gebeurtenislogboeken zijn een van de meest voorkomende Hallo [gegevensbronnen](log-analytics-data-sources.md) voor het verzamelen van gegevens met behulp van Windows-agents omdat veel toepassingen toohello Windows-gebeurtenislogboek schrijven.  U kunt gebeurtenissen verzamelen van Logboeken van de standaard zoals systeem en de toepassing in toevoeging toospecifying eventuele aangepaste logboeken gemaakt door toepassingen die u moet toomonitor.

![Windows-gebeurtenissen](media/log-analytics-data-sources-windows-events/overview.png)     

## <a name="configuring-windows-event-logs"></a>Configureren Windows gebeurtenislogboeken
Configureren van Windows-gebeurtenislogboeken op Hallo [menu Data in logboekanalyse-instellingen](log-analytics-data-sources.md#configuring-data-sources).

Log Analytics verzamelt alleen gebeurtenissen uit Hallo Windows-gebeurtenislogboeken die zijn opgegeven in het Hallo-instellingen.  U kunt een gebeurtenislogboek toevoegen door te typen Hallo-naam van Hallo logboek en te klikken op  **+** .  Voor elk logboek worden alleen Hallo gebeurtenissen met Hallo geselecteerd ernst verzameld.  Hallo ernstcategorieën voor bepaalde Hallo-logboek dat u wilt dat toocollect controleren.  U kan niet alle aanvullende criteria opgeven toofilter gebeurtenissen.

Terwijl u Hallo-naam van een gebeurtenislogboek typt, bevat logboekanalyse suggesties van algemene namen van gebeurtenislogboeken. Als de gewenste tooadd Hallo-logboek niet wordt weergegeven in de lijst hello, kunt u het nog steeds toevoegen door in de volledige naam van logboek Hallo Hallo te typen. U vindt de volledige naam van logboek Hallo Hallo met behulp van Logboeken. Open in Logboeken, Hallo *eigenschappen* pagina voor Hallo logboek en kopieer Hallo tekenreeks uit Hallo *volledige naam* veld.

![Windows-gebeurtenissen configureren](media/log-analytics-data-sources-windows-events/configure.png)

## <a name="data-collection"></a>Gegevensverzameling
Log Analytics verzamelt elke gebeurtenis die overeenkomt met een geselecteerde ernst van een bewaakte gebeurtenislogboek zoals Hallo gebeurtenis wordt gemaakt.  Hallo-agent registreert plaats daarvan in elk logboek die worden verzameld uit.  Hallo-agent voor een bepaalde periode offline gaat, klikt u vervolgens verzamelt Log Analytics gebeurtenissen van waar het laatst werd afgebroken, zelfs als de gebeurtenissen die zijn gemaakt terwijl de agent Hallo offline was.  Er is een kans voor deze toonot gebeurtenissen worden verzameld als Hallo gebeurtenislogboek met niet-geïnde gebeurtenissen wordt overschreven doorloopt tijdens het Hallo-agent is offline.

>[!NOTE]
>Log Analytics verzamelt geen controlegebeurtenissen die zijn gemaakt door SQL Server van bron *MSSQLSERVER* met gebeurtenis-ID 18453 met trefwoorden - *klassieke* of *Audit geslaagd* en trefwoord *0xa0000000000000*.
>

## <a name="windows-event-records-properties"></a>Windows-gebeurtenis registreert eigenschappen
Gebeurtenisrecords Windows hebben een soort **gebeurtenis** en Hallo eigenschappen in de volgende tabel Hallo hebben:

| Eigenschap | Beschrijving |
|:--- |:--- |
| Computer |Naam van Hallo-computer die gebeurtenis Hallo is verzameld. |
| Culture |De categorie van het Hallo-gebeurtenis. |
| EventData |Alle gebeurtenisgegevens in een onbewerkte indeling. |
| Gebeurtenis-id |Het aantal Hallo-gebeurtenis. |
| eventLevel |Ernst van gebeurtenis Hallo in numerieke vorm. |
| EventLevelName |Ernst van gebeurtenis Hallo in tekstvorm. |
| Gebeurtenislogboek |Naam van gebeurtenislogboek Hallo die gebeurtenis Hallo is verzameld. |
| ParameterXml |Gebeurtenis parameterwaarden in XML-indeling. |
| ManagementGroupName |De naam van de beheergroep Hallo voor System Center Operations Manager-agents.  Voor andere agents is deze waarde AOI-<workspace ID> |
| RenderedDescription |Beschrijving van gebeurtenis met parameterwaarden |
| Bron |De bron van Hallo-gebeurtenis. |
| SourceSystem |Type gebeurtenis van agent Hallo is verzameld. <br> OpsManager – Windows-agent, ofwel direct verbinding maken met of Operations Manager worden beheerd <br> Linux – alle Linux-agents  <br> AzureStorage – Azure Diagnostics |
| TimeGenerated |Datum en tijd Hallo-gebeurtenis is gemaakt in Windows. |
| Gebruikersnaam |Gebruikersnaam van het Hallo-account dat Hallo gebeurtenis is vastgelegd. |

## <a name="log-searches-with-windows-events"></a>Logboek van zoekopdrachten met Windows-gebeurtenissen
Hallo bevat volgende tabel voorbeelden van logboek-zoekopdrachten waarmee u Windows-gebeurtenis records ophalen.

| Query’s uitvoeren | Beschrijving |
|:--- |:--- |
| Type gebeurtenis = |Alle Windows-gebeurtenissen. |
| Type gebeurtenis EventLevelName = fout = |Alle Windows-gebeurtenissen met de ernst van de fout. |
| Type = gebeurtenis &#124; Meting count() door bron |Telling van Windows-gebeurtenissen op de bron. |
| Type gebeurtenis EventLevelName = = fout &#124; Meting count() door bron |Telling van Windows-foutgebeurtenissen door bron. |


>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), Hallo hierboven query's toohello volgende wilt wijzigen.
>
>| Query’s uitvoeren | Beschrijving |
|:---|:---|
| Gebeurtenis |Alle Windows-gebeurtenissen. |
| Gebeurtenis &#124; waar EventLevelName == "error" |Alle Windows-gebeurtenissen met de ernst van de fout. |
| Gebeurtenis &#124; count() door bron samenvatten |Telling van Windows-gebeurtenissen op de bron. |
| Gebeurtenis &#124; waar EventLevelName == "error" &#124; count() door bron samenvatten |Telling van Windows-foutgebeurtenissen door bron. |


## <a name="next-steps"></a>Volgende stappen
* Log Analytics toocollect andere configureren [gegevensbronnen](log-analytics-data-sources.md) voor analyse.
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) tooanalyze Hallo gegevens verzameld van gegevensbronnen en oplossingen.  
* Gebruik [aangepaste velden](log-analytics-custom-fields.md) tooparse Hallo gebeurtenisrecords in afzonderlijke velden.
* Configureer [verzameling van prestatiemeteritems](log-analytics-data-sources-performance-counters.md) van uw Windows-agents.

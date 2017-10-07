---
title: aaaIIS wordt geregistreerd in Log Analytics | Microsoft Docs
description: Internet Information Services (IIS) slaat gebruikersactiviteit in de logboekbestanden die kunnen worden verzameld door logboekanalyse.  In dit artikel wordt beschreven hoe tooconfigure verzameling van IIS-logboeken en details van records Hallo ze in Hallo OMS-opslagplaats maken.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: cec5ff0a-01f5-4262-b2e8-e3db7b7467d2
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: bwren
ms.openlocfilehash: c5575351090cdabaf651bcb49867794ee3a4b6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="iis-logs-in-log-analytics"></a>IIS-logboeken in Log Analytics
Internet Information Services (IIS) slaat gebruikersactiviteit in de logboekbestanden die kunnen worden verzameld door logboekanalyse.  

![IIS-logboeken](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a>Configureren van IIS-logboeken
Log Analytics worden gegevens verzameld uit logboekbestanden gemaakt door IIS, dus u moet [IIS configureren voor logboekregistratie](https://technet.microsoft.com/library/hh831775.aspx).

Log Analytics IIS-logboekbestanden opgeslagen in de W3C-indeling ondersteunt alleen en biedt geen ondersteuning voor aangepaste velden of geavanceerde IIS-registratie.  
Log Analytics verzamelt geen logboeken in systeemeigen NCSA of IIS-indeling.

Configureren van IIS-logboeken in logboekanalyse van Hallo [menu Data in logboekanalyse-instellingen](log-analytics-data-sources.md#configuring-data-sources).  Er is geen configuratie vereist dan selecteren **verzamelen W3C-indeling IIS-logboekbestanden**.

U wordt aangeraden wanneer u IIS-logboekverzameling inschakelt, u Hallo IIS-logboek overschakeling van de instelling op elke server configureren moet.

## <a name="data-collection"></a>Gegevensverzameling
Log Analytics verzamelt IIS logboekvermeldingen van elke bron verbonden ongeveer elke 15 minuten.  Hallo-agent registreert plaats daarvan in elk logboek die worden verzameld uit.  Als de agent Hallo offline gaat, vervolgens verzamelt Log Analytics gebeurtenissen van waar het laatst werd afgebroken, zelfs als de gebeurtenissen die zijn gemaakt terwijl de agent Hallo offline was.

## <a name="iis-log-record-properties"></a>Eigenschappen van IIS-logboek record
IIS-logboekrecords hebben een soort **W3CIISLog** en Hallo eigenschappen in de volgende tabel Hallo hebben:

| Eigenschap | Beschrijving |
|:--- |:--- |
| Computer |Naam van Hallo-computer die gebeurtenis Hallo is verzameld. |
| Overschrijving |IP-adres van Hallo-client. |
| csMethod |Methode voor het Hallo-aanvraag zoals GET of POST. |
| csReferer |Site die Hallo gebruiker een koppeling van de huidige site toohello gevolgd. |
| csUserAgent |Het type van de browser van Hallo-client. |
| csUserName |Naam van Hallo geverifieerde gebruiker die toegankelijk Hallo-server. Anonieme gebruikers worden aangeduid met een koppelteken. |
| csUriStem |Doel van de aanvraag is hello, zoals een webpagina. |
| csUriQuery |Query, indien van toepassing, die Hallo-client heeft geprobeerd tooperform. |
| ManagementGroupName |Naam van beheergroep Hallo voor Operations Manager-agents.  Dit is voor andere agents AOI -\<werkruimte-ID\> |
| RemoteIPCountry |Land van Hallo IP-adres van het Hallo-client. |
| RemoteIPLatitude |Breedtegraad van Hallo client-IP-adres. |
| RemoteIPLongitude |Lengtegraad van Hallo client-IP-adres. |
| scStatus |HTTP-statuscode. |
| scSubStatus |Fout-substatuscode geregistreerd. |
| scWin32Status |Windows-statuscode geregistreerd. |
| sIP |IP-adres van de webserver Hallo. |
| SourceSystem |OpsMgr |
| sPort |De poort op Hallo server Hallo-client is verbonden met. |
| sSiteName |Naam van Hallo ISS-site. |
| TimeGenerated |Datum en tijd Hallo-vermelding is geregistreerd. |
| timeTaken |Lengte van de tijd tooprocess Hallo aanvraag in milliseconden. |

## <a name="log-searches-with-iis-logs"></a>Logboek van zoekopdrachten met IIS-logboeken
Hallo bevat volgende tabel voorbeelden van logboek-query's die IIS-logboekrecords ophalen.

| Query’s uitvoeren | Beschrijving |
|:--- |:--- |
| Type W3CIISLog = |Alle records voor IIS-logboek. |
| Type = W3CIISLog scStatus = 500 |Alle IIS-logboekrecords met een status van het resultaat van 500. |
| Type = W3CIISLog &#124; Meting count() door overschrijving |Telling van IIS logboekvermeldingen op client-IP-adres. |
| Type = W3CIISLog csHost = 'www.contoso.com' &#124; Meting count() door csUriStem |Telling van IIS logboekvermeldingen met URL voor Hallo host www.contoso.com. |
| Type = W3CIISLog &#124; Meting Sum(csBytes) door Computer &#124; Top 500000 |Totaal aantal bytes dat is ontvangen door elke IIS-computer. |

>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), Hallo hierboven query's toohello volgende wilt wijzigen.

> | Query’s uitvoeren | Beschrijving |
|:--- |:--- |
| W3CIISLog |Alle records voor IIS-logboek. |
| W3CIISLog &#124; waar scStatus == 500 |Alle IIS-logboekrecords met een status van het resultaat van 500. |
| W3CIISLog &#124; count() overschrijving samenvatten |Telling van IIS logboekvermeldingen op client-IP-adres. |
| W3CIISLog &#124; waar csHost == 'www.contoso.com' &#124; count() csUriStem samenvatten |Telling van IIS logboekvermeldingen met URL voor Hallo host www.contoso.com. |
| W3CIISLog &#124; overzicht van sum(csBytes) door Computer &#124; 500000 duren |Totaal aantal bytes dat is ontvangen door elke IIS-computer. |

## <a name="next-steps"></a>Volgende stappen
* Log Analytics toocollect andere configureren [gegevensbronnen](log-analytics-data-sources.md) voor analyse.
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) tooanalyze Hallo gegevens verzameld van gegevensbronnen en oplossingen.
* Waarschuwingen configureren in logboekanalyse tooproactively zullen u informeren over belangrijke voorwaarden gevonden in de IIS-logboeken.

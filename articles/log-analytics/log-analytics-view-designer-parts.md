---
title: aaaPart verwijzing voor weergave Designer in OMS Log Analytics | Microsoft Docs
description: Weergave Designer in Log Analytics kunt u toocreate aangepaste weergaven in de OMS-console Hallo die verschillende visualisaties van gegevens in de OMS-opslagplaats Hallo bevatten. Dit artikel bevat een verwijzing van Hallo-instellingen voor elk Hallo visualisatie delen beschikbaar toouse in aangepaste weergaven.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 5718d620-b96e-4d33-8616-e127ee9379c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 6a19a451cf4cefd2fa5c94e6f61d812c4f820f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-visualization-part-reference"></a>Log Analytics-ontwerper visualisatie onderdeelverwijzing
Hallo-ontwerper in Log Analytics kunt u toocreate aangepaste weergaven in de OMS-console Hallo die verschillende visualisaties van gegevens uit de OMS-opslagplaats Hallo bevatten. Dit artikel bevat een verwijzing van Hallo-instellingen voor elk Hallo visualisatie delen beschikbaar toouse in aangepaste weergaven.

Er zijn andere artikelen die beschikbaar zijn voor weergave Designer:

* [Designer bekijken](log-analytics-view-designer.md) -overzicht van Hallo Designer bekijken en procedures voor het maken en bewerken van aangepaste weergaven.
* [Tegel verwijzing](log-analytics-view-designer-tiles.md) -verwijzing van instellingen voor elk Hallo Hallo tegels beschikbaar toouse in aangepaste weergaven.

>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [querytaal van nieuwe logboekanalyse](log-analytics-log-search-upgrade.md), en vervolgens de query's in alle weergaven moeten worden geschreven in Hallo [nieuwe querytaal](https://go.microsoft.com/fwlink/?linkid=856078).  De weergaven die zijn gemaakt voordat het Hallo-werkruimte is bijgewerkt worden doorloopt geconverteerd.

Hallo beschrijft volgende tabel Hallo verschillende soorten tegels beschikbaar in het Hallo-ontwerper.  Hallo in de volgende secties beschrijven elk tegeltype in detail en hun eigenschappen.

| Weergavetype | Beschrijving |
|:--- |:--- |
| [Lijst met query 's](#list-of-queries-part) |Geeft een lijst van logboek zoekquery's weer.  Hallo-gebruiker kunt klikken op elke query toodisplay de resultaten. |
| [Aantal & lijst met](#number-amp-list-part) |Kop heeft één nummer tonen aantal records uit een zoekquery logboek.  Hier weergegeven Hallo top tien resultaten van een query met een grafiek waarin Hallo relatieve waarde van een numerieke kolom of de wijziging gedurende een bepaalde periode. |
| [Twee getallen & lijst met](#two-numbers-amp-list-part) |Kop heeft twee getallen met het aantal records van de afzonderlijke logboek zoekquery's.  Hier weergegeven Hallo top tien resultaten van een query met een grafiek waarin Hallo relatieve waarde van een numerieke kolom of de wijziging gedurende een bepaalde periode. |
| [Ring & lijst met](#donut-amp-list-part) |Koptekst één getal gedestilleerd uit de kolom van een waarde in een logboek-query wordt weergegeven.  Hallo Ring worden resultaten van de eerste drie records Hallo grafisch weergegeven. |
| [Twee tijdlijnen & lijst met](#two-timelines-amp-list-part) |Koptekst geeft Hallo resultaten van query's twee logboek na verloop van tijd als kolomgrafieken met een toelichting één nummer samengevat in een waardenkolom die in een logboek-query.  Hier weergegeven Hallo top tien resultaten van een query met een grafiek waarin Hallo relatieve waarde van een numerieke kolom of de wijziging gedurende een bepaalde periode. |
| [Informatie](#information-part) |Koptekst wordt weergegeven voor statische tekst en een optionele link.  Een of meer artikelen met statische tekst en titel hier weergegeven. |
| [Lijndiagram, toelichting & lijst](#line-chart-callout-amp-list-part) |Koptekst bevat een lijndiagram met meerdere reeksen door een query logboek gedurende de tijd en een toelichting met een samengevatte waarde.  Hier weergegeven Hallo top tien resultaten van een query met een grafiek waarin Hallo relatieve waarde van een numerieke kolom of de wijziging gedurende een bepaalde periode. |
| [Lijndiagram & lijst met](#line-chart-amp-list-part) |Koptekst wordt een lijndiagram met meerdere reeksen door een query logboek weergegeven gedurende een bepaalde periode.  Hier weergegeven Hallo top tien resultaten van een query met een grafiek waarin Hallo relatieve waarde van een numerieke kolom of de wijziging gedurende een bepaalde periode. |
| [Stack van regel grafieken onderdeel](#stack-of-line-charts-part) |Drie afzonderlijke lijndiagrammen met meerdere reeksen door een query logboek weergegeven gedurende een bepaalde periode. |

## <a name="list-of-queries-part"></a>Lijst met query's onderdeel
Geeft een lijst van logboek zoekquery's weer.  Hallo-gebruiker kunt klikken op elke query toodisplay de resultaten.  Hallo-weergave bevat één query standaard en klikt u op **+ Query** tooadd extra query's.

![Lijst met query's weergeven](media/log-analytics-view-designer/view-list-queries.png)

| Instelling | Beschrijving |
|:--- |:--- |
| **Algemeen** | |
| Titel |Tekst toodisplay Hallo boven aan het Hallo-weergave. |
| Nieuwe groep |Selecteer een nieuwe groep toocreate in Hallo beginnen bij de huidige weergave Hallo. |
| Vooraf geselecteerd filters |Door komma's gescheiden lijst met eigenschappen tooinclude in het linkerdeelvenster filterdeelvenster Hallo wanneer Hallo gebruiker een query selecteert. |
| Modus weergeven |Beginweergave weergegeven als Hallo query hebt geselecteerd.  Hallo-gebruiker kan beschikbare weergaven selecteren nadat het Hallo-query is geopend. |
| **Query's** | |
| Zoekopdracht |Query toorun. |
| Beschrijvende naam |Beschrijvende naam van Hallo query toodisplay toohello gebruiker. |

## <a name="number--list-part"></a>Aantal & lijst met onderdeel
Kop heeft één nummer tonen aantal records uit een zoekquery logboek.  Hier weergegeven Hallo top tien resultaten van een query met een grafiek waarin Hallo relatieve waarde van een numerieke kolom of de wijziging gedurende een bepaalde periode.

![Lijst met query's weergeven](media/log-analytics-view-designer/view-number-list.png)

| Instelling | Beschrijving |
|:--- |:--- |
| **Algemeen** | |
| Groepstitel |Tekst toodisplay Hallo boven aan het Hallo-weergave. |
| Nieuwe groep |Selecteer een nieuwe groep toocreate in Hallo beginnen bij de huidige weergave Hallo. |
| Pictogram |De installatiekopie van bestand toodisplay volgende toohello resultaat in Hallo-header. |
| Pictogram gebruiken |Selecteer toohave Hallo pictogram weergegeven. |
| **Titel** | |
| Legenda |Tekst toodisplay Hallo boven aan het Hallo-header. |
| Query’s uitvoeren |Query toorun voor Hallo-header.  Hallo-telling van het aantal records dat wordt geretourneerd door de query Hallo Hallo wordt weergegeven. |
| **Lijst** | |
| Query’s uitvoeren |Query toorun voor Hallo-lijst.  de eerste twee eigenschappen Hallo voor Hallo eerste tien registreert in Hallo resultaten worden weergegeven.  eerste Hallo-eigenschap moet een waarde en Hallo tweede teksteigenschap een numerieke waarde zijn.  Balken worden automatisch gemaakt op basis van de relatieve waarde Hallo van Hallo numerieke kolom.<br><br>Hallo sorteeropdracht in Hallo query toosort Hallo records in de lijst hello gebruiken.  Hallo-gebruiker kan klikken Zie alle toorun Hallo opvragen en alle records. |
| Grafiek verbergen |Selecteer toodisable Hallo grafiek toohello rechts van Hallo numerieke kolom. |
| Sparklines inschakelen |Selecteer toodisplay sparkline in plaats van de horizontale balk.  Zie [algemene instellingen](#sparklines) voor meer informatie. |
| Kleur |Kleur van Hallo balken of sparklines. |
| De naam van & scheidingsteken |Willekeurig teken scheidingsteken als u wilt dat de eigenschap van de tekst hello tooparse in meerdere waarden.  Zie [algemene instellingen](#name-value-separator) voor meer informatie. |
| Navigatie-query |Toorun vragen wanneer Hallo gebruiker een item in Hallo lijst selecteert.  Zie [algemene instellingen](#navigation-query) voor meer informatie. |
| **Lijst** |**> Kolomtitels** |
| Naam |Tekst toodisplay Hallo boven aan de eerste kolom Hallo van Hallo-lijst. |
| Waarde |Tekst toodisplay Hallo boven aan de tweede kolom Hallo van Hallo-lijst. |
| **Lijst** |**> Drempelwaarden** |
| Drempelwaarden inschakelen |Selecteer tooenable drempelwaarden.  Zie [algemene instellingen](#thresholds) voor meer informatie. |

## <a name="two-numbers--list-part"></a>Twee getallen & lijst onderdeel
Kop heeft twee getallen met het aantal records van de afzonderlijke logboek zoekquery's.  Hier weergegeven Hallo top tien resultaten van een query met een grafiek waarin Hallo relatieve waarde van een numerieke kolom of de wijziging gedurende een bepaalde periode.

![Twee getallen & lijstweergave](media/log-analytics-view-designer/view-two-numbers-list.png)

| Instelling | Beschrijving |
|:--- |:--- |
| **Algemeen** | |
| Groepstitel |Tekst toodisplay Hallo boven aan het Hallo-weergave. |
| Nieuwe groep |Selecteer een nieuwe groep toocreate in Hallo beginnen bij de huidige weergave Hallo. |
| Pictogram |De installatiekopie van bestand toodisplay volgende toohello resultaat in Hallo-header. |
| Pictogram gebruiken |Selecteer toohave Hallo pictogram weergegeven. |
| **Titel** | |
| Legenda |Tekst toodisplay Hallo boven aan het Hallo-header. |
| Query’s uitvoeren |Query toorun voor Hallo-header.  Hallo-telling van het aantal records dat wordt geretourneerd door de query Hallo Hallo wordt weergegeven. |
| **Lijst** | |
| Query’s uitvoeren |Query toorun voor Hallo-lijst.  de eerste twee eigenschappen Hallo voor Hallo eerste tien registreert in Hallo resultaten worden weergegeven.  eerste Hallo-eigenschap moet een waarde en Hallo tweede teksteigenschap een numerieke waarde zijn.  Balken worden automatisch gemaakt op basis van de relatieve waarde Hallo van Hallo numerieke kolom.<br><br>Hallo sorteeropdracht in Hallo query toosort Hallo records in de lijst hello gebruiken.  Hallo-gebruiker kan klikken Zie alle toorun Hallo opvragen en alle records. |
| Grafiek verbergen |Selecteer toodisable Hallo grafiek toohello rechts van Hallo numerieke kolom. |
| Sparklines inschakelen |Selecteer toodisplay sparkline in plaats van de horizontale balk.  Zie [algemene instellingen](#sparklines) voor meer informatie. |
| Kleur |Kleur van Hallo balken of sparklines. |
| Bewerking |Bewerking tooperform voor Hallo sparkline.  Zie [algemene instellingen](#sparklines) voor meer informatie. |
| De naam van & scheidingsteken |Willekeurig teken scheidingsteken als u wilt dat de eigenschap van de tekst hello tooparse in meerdere waarden.  Zie [algemene instellingen](#name-value-separator) voor meer informatie. |
| Navigatie-query |Toorun vragen wanneer Hallo gebruiker een item in Hallo lijst selecteert.  Zie [algemene instellingen](#navigation-query) voor meer informatie. |
| **Lijst** |**> Kolomtitels** |
| Naam |Tekst toodisplay Hallo boven aan de eerste kolom Hallo van Hallo-lijst. |
| Waarde |Tekst toodisplay Hallo boven aan de tweede kolom Hallo van Hallo-lijst. |
| **Lijst** |**> Drempelwaarden** |
| Drempelwaarden inschakelen |Selecteer tooenable drempelwaarden.  Zie [algemene instellingen](#thresholds) voor meer informatie. |

## <a name="donut--list-part"></a>Ring & lijst met onderdeel
Koptekst één getal gedestilleerd uit de kolom van een waarde in een logboek-query wordt weergegeven.  Hallo Ring worden resultaten van de eerste drie records Hallo grafisch weergegeven.

![Ring & lijst weergeven](media/log-analytics-view-designer/view-donut-list.png)

| Instelling | Beschrijving |
|:--- |:--- |
| **Algemeen** | |
| Groepstitel |Tekst toodisplay bovenaan Hallo Hallo tegel. |
| Nieuwe groep |Selecteer een nieuwe groep toocreate in Hallo beginnen bij de huidige weergave Hallo. |
| Pictogram |De installatiekopie van bestand toodisplay volgende toohello resultaat in Hallo-header. |
| Pictogram gebruiken |Selecteer toohave Hallo pictogram weergegeven. |
| **Koptekst** | |
| Titel |Tekst toodisplay Hallo boven aan het Hallo-header. |
| Subtitel |Tekst toodisplay onder Hallo titel Hallo boven aan het Hallo-header. |
| **Ring** | |
| Query’s uitvoeren |Query toorun voor Hallo ring.  eerste Hallo-eigenschap moet een waarde en Hallo tweede teksteigenschap een numerieke waarde zijn. |
| **Ring** |**> Center** |
| Tekst |Tekst toodisplay onder Hallo waarde binnen Hallo ring. |
| Bewerking |Hallo bewerking tooperform op Hallo eigenschap toosummarize tooa één waarde.<br><br>-Som: Hallo waarden van alle records toevoegen.<br>-Percentage: Percentage Hallo records geretourneerd door de waarden in Hallo **leiden waarden die worden gebruikt in de bewerking center** toohello totaal aantal records in Hallo-query. |
| Resultaatwaarden die worden gebruikt in de bewerking center |(Optioneel) Klik op Hallo plusteken tooadd een of meer waarden.  Hallo-resultaten van Hallo query worden beperkt toorecords met Hallo eigenschapswaarden die u opgeeft.  Als er geen waarden worden toegevoegd, worden alle records opgenomen in Hallo-query. |
| **Extra opties** |**> Kleuren** |
| Kleur 1<br>Kleur 2<br>Kleur 3 |Hallo kleur voor Hallo van Hallo waarden weergegeven in Hallo ring selecteren. |
| **Extra opties** |**> Geavanceerde kleur toewijzen** |
| Waarde van veld |Hallo-typenaam van een veld toodisplay als een andere kleur als deze is opgenomen in de Hallo ring. |
| Kleur |Selecteer de kleur Hallo voor Hallo uniek veld. |
| **Lijst** | |
| Query’s uitvoeren |Query toorun voor Hallo-lijst.  Hallo-telling van het aantal records dat wordt geretourneerd door de query Hallo Hallo wordt weergegeven. |
| Grafiek verbergen |Selecteer toodisable Hallo grafiek toohello rechts van Hallo numerieke kolom. |
| Sparklines inschakelen |Selecteer toodisplay sparkline in plaats van de horizontale balk.  Zie [algemene instellingen](#sparklines) voor meer informatie. |
| Kleur |Kleur van Hallo balken of sparklines. |
| Bewerking |Bewerking tooperform voor Hallo sparkline.  Zie [algemene instellingen](#sparklines) voor meer informatie. |
| De naam van & scheidingsteken |Willekeurig teken scheidingsteken als u wilt dat de eigenschap van de tekst hello tooparse in meerdere waarden.  Zie [algemene instellingen](#name-value-separator) voor meer informatie. |
| Navigatie-query |Toorun vragen wanneer Hallo gebruiker een item in Hallo lijst selecteert.  Zie [algemene instellingen](#navigation-query) voor meer informatie. |
| **Lijst** |**> Kolomtitels** |
| Naam |Tekst toodisplay Hallo boven aan de eerste kolom Hallo van Hallo-lijst. |
| Waarde |Tekst toodisplay Hallo boven aan de tweede kolom Hallo van Hallo-lijst. |
| **Lijst** |**> Drempelwaarden** |
| Drempelwaarden inschakelen |Selecteer tooenable drempelwaarden.  Zie [algemene instellingen](#thresholds) voor meer informatie. |

## <a name="two-timelines--list-part"></a>Twee tijdlijnen & lijst met onderdeel
Koptekst geeft Hallo resultaten van query's twee logboek na verloop van tijd als kolomgrafieken met een toelichting één nummer samengevat in een waardenkolom die in een logboek-query.  Hier weergegeven Hallo top tien resultaten van een query met een grafiek waarin Hallo relatieve waarde van een numerieke kolom of de wijziging gedurende een bepaalde periode.

![Twee tijdlijnen & lijst weergeven](media/log-analytics-view-designer/view-two-timelines-list.png)

| Instelling | Beschrijving |
|:--- |:--- |
| **Algemeen** | |
| Groepstitel |Tekst toodisplay bovenaan Hallo Hallo tegel. |
| Nieuwe groep |Selecteer een nieuwe groep toocreate in Hallo beginnen bij de huidige weergave Hallo. |
| Pictogram |De installatiekopie van bestand toodisplay volgende toohello resultaat in Hallo-header. |
| Pictogram gebruiken |Selecteer toohave Hallo pictogram weergegeven. |
| **Grafiek eerste<br>tweede diagram** | |
| Legenda |Tekst toodisplay onder Hallo bijschrift voor de eerste reeks Hallo. |
| Kleur |Kleur toouse voor kolommen in de reeks Hallo Hallo. |
| Query’s uitvoeren |Query toorun voor de eerste reeks Hallo.  Hallo aantal Hallo records over elk tijdsinterval wordt vertegenwoordigd door Hallo grafiek kolommen. |
| Bewerking |Hallo bewerking tooperform op Hallo waarde toosummarize tooa één eigenschapswaarde voor Hallo toelichting.<br><br>-Som: De som van de waarde op Hallo van alle records.<br>-Gemiddelde: Het gemiddelde van de waarde op Hallo van alle records.<br>-Laatste: Voorbeeldwaarde vanaf het laatste Hallo-interval in Hallo diagram opgenomen.<br>-Het eerste voorbeeld: Waarde van de eerste interval Hallo opgenomen in de grafiek Hallo.<br>-Aantal: De telling van alle records die zijn geretourneerd door Hallo-query. |
| **Lijst** | |
| Query’s uitvoeren |Query toorun voor Hallo-lijst.  Hallo-telling van het aantal records dat wordt geretourneerd door de query Hallo Hallo wordt weergegeven. |
| Grafiek verbergen |Selecteer toodisable Hallo grafiek toohello rechts van Hallo numerieke kolom. |
| Sparklines inschakelen |Selecteer toodisplay sparkline in plaats van de horizontale balk.  Zie [algemene instellingen](#sparklines) voor meer informatie. |
| Kleur |Kleur van Hallo balken of sparklines. |
| Bewerking |Bewerking tooperform voor Hallo sparkline.  Zie [algemene instellingen](#sparklines) voor meer informatie. |
| Navigatie-query |Toorun vragen wanneer Hallo gebruiker een item in Hallo lijst selecteert.  Zie [algemene instellingen](#navigation-query) voor meer informatie. |
| **Lijst** |**> Kolomtitels** |
| Naam |Tekst toodisplay Hallo boven aan de eerste kolom Hallo van Hallo-lijst. |
| Waarde |Tekst toodisplay Hallo boven aan de tweede kolom Hallo van Hallo-lijst. |
| **Lijst** |**> Drempelwaarden** |
| Drempelwaarden inschakelen |Selecteer tooenable drempelwaarden.  Zie [algemene instellingen](#thresholds) voor meer informatie. |

## <a name="information-part"></a>Informatie-onderdeel
Koptekst wordt weergegeven voor statische tekst en een optionele link.  Een of meer artikelen met statische tekst en titel hier weergegeven.

![Informatie weergeven](media/log-analytics-view-designer/view-information.png)

| Instelling | Beschrijving |
|:--- |:--- |
| **Algemeen** | |
| Groepstitel |Tekst toodisplay bovenaan Hallo Hallo tegel. |
| Nieuwe groep |Selecteer een nieuwe groep toocreate in Hallo beginnen bij de huidige weergave Hallo. |
| Kleur |De achtergrondkleur voor Hallo-header. |
| **Koptekst** | |
| Installatiekopie |De installatiekopie van bestand toodisplay in Hallo-header. |
| Label |Tekst toodisplay in Hallo-header. |
| **Koptekst** |**> Koppeling** |
| Label |Tekst koppeling. |
| URL |De URL voor de koppeling. |
| **Informatie-Items** | |
| Titel |Tekst toodisplay voor de titel van elk item. |
| Inhoud |Tekst toodisplay voor elk item. |

## <a name="line-chart-callout--list-part"></a>Lijndiagram, toelichting & lijst onderdeel
Koptekst bevat een lijndiagram met meerdere reeksen door een query logboek gedurende de tijd en een toelichting met een samengevatte waarde.  Hier weergegeven Hallo top tien resultaten van een query met een grafiek waarin Hallo relatieve waarde van een numerieke kolom of de wijziging gedurende een bepaalde periode.

![Lijndiagram, toelichting & lijstweergave](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| Instelling | Beschrijving |
|:--- |:--- |
| **Algemeen** | |
| Groepstitel |Tekst toodisplay bovenaan Hallo Hallo tegel. |
| Nieuwe groep |Selecteer een nieuwe groep toocreate in Hallo beginnen bij de huidige weergave Hallo. |
| Pictogram |De installatiekopie van bestand toodisplay volgende toohello resultaat in Hallo-header. |
| Pictogram gebruiken |Selecteer toohave Hallo pictogram weergegeven. |
| **Koptekst** | |
| Titel |Tekst toodisplay Hallo boven aan het Hallo-header. |
| Subtitel |Tekst toodisplay onder Hallo titel Hallo boven aan het Hallo-header. |
| **Lijndiagram** | |
| Query’s uitvoeren |Query toorun Hallo lijndiagram.  eerste Hallo-eigenschap moet een waarde en Hallo tweede teksteigenschap een numerieke waarde zijn.  Dit is doorgaans een query die gebruikmaakt van Hallo **meting** toosummarize resultaten.  Als het Hallo-query gebruikt Hallo **interval** sleutelwoord vervolgens Hallo x-as van grafiekgebied Hallo gebruikt dit tijdsinterval blijft.  Als het Hallo-query bevat geen Hallo **interval** sleutelwoord en vervolgens elk uur intervallen worden gebruikt voor Hallo x-as. |
| **Lijndiagram** |**> Toelichting** |
| Titel van de toelichting |Tekst toodisplay boven Hallo toelichting waarde. |
| Naam van de gegevensreeks |De waarde van de eigenschap voor Hallo reeks toouse voor Hallo toelichting waarde.  Als geen reeksen is opgegeven, worden alle records uit Hallo query gebruikt. |
| Bewerking |Hallo bewerking tooperform op Hallo waarde toosummarize tooa één eigenschapswaarde voor Hallo toelichting.<br><br>-Gemiddelde: Het gemiddelde van de waarde op Hallo van alle records.<br>-Aantal telling van alle records geretourneerd door Hallo-query.<br>-Laatste: Voorbeeldwaarde vanaf het laatste Hallo-interval in Hallo diagram opgenomen.<br>-Max: Maximumwaarde van hello-intervallen opgenomen in de grafiek Hallo.<br>-Min: Minimumwaarde van hello-intervallen opgenomen in de grafiek Hallo.<br>-Som: De som van de waarde op Hallo van alle records. |
| **Lijndiagram** |**> Y-as** |
| Logaritmische schaal gebruiken |Selecteer toouse een logaritmische schaal voor Hallo y-as. |
| Eenheden |Hallo-eenheden voor Hallo waarden geretourneerd door Hallo query opgeven.  Deze informatie is gebruikte toodisplay labels op Hallo grafiek die aangeeft Hallo waardetypen en desgewenst voor het converteren van Hallo waarden.  Hallo eenheidstype geeft Hallo categorie van het Hallo-eenheid en definieert Hallo huidige eenheidstype waarden die beschikbaar zijn.  Als u een waarde in converteren toothen Hallo numerieke worden waarden van Hallo huidige eenheid type toohello converteren tootype geconverteerd. |
| Aangepast etiket |Tekst toodisplay voor Hallo Y-as volgende toohello label voor het eenheidstype Hallo.  Als er geen naam is opgegeven, wordt alleen het eenheidstype Hallo weergegeven. |
| **Lijst** | |
| Query’s uitvoeren |Query toorun voor Hallo-lijst.  Hallo-telling van het aantal records dat wordt geretourneerd door de query Hallo Hallo wordt weergegeven. |
| Grafiek verbergen |Selecteer toodisable Hallo grafiek toohello rechts van Hallo numerieke kolom. |
| Sparklines inschakelen |Selecteer toodisplay sparkline in plaats van de horizontale balk.  Zie [algemene instellingen](#sparklines) voor meer informatie. |
| Kleur |Kleur van Hallo balken of sparklines. |
| Bewerking |Bewerking tooperform voor Hallo sparkline.  Zie [algemene instellingen](#sparklines) voor meer informatie. |
| De naam van & scheidingsteken |Willekeurig teken scheidingsteken als u wilt dat de eigenschap van de tekst hello tooparse in meerdere waarden.  Zie [algemene instellingen](#name-value-separator) voor meer informatie. |
| Navigatie-query |Toorun vragen wanneer Hallo gebruiker een item in Hallo lijst selecteert.  Zie [algemene instellingen](#navigation-query) voor meer informatie. |
| **Lijst** |**> Kolomtitels** |
| Naam |Tekst toodisplay Hallo boven aan de eerste kolom Hallo van Hallo-lijst. |
| Waarde |Tekst toodisplay Hallo boven aan de tweede kolom Hallo van Hallo-lijst. |
| **Lijst** |**> Drempelwaarden** |
| Drempelwaarden inschakelen |Selecteer tooenable drempelwaarden.  Zie [algemene instellingen](#thresholds) voor meer informatie. |

## <a name="line-chart--list-part"></a>Grafiek & lijst met onderdeel van regel
Koptekst wordt een lijndiagram met meerdere reeksen door een query logboek weergegeven gedurende een bepaalde periode.  Hier weergegeven Hallo top tien resultaten van een query met een grafiek waarin Hallo relatieve waarde van een numerieke kolom of de wijziging gedurende een bepaalde periode.

![De weergave diagram & lijst met regels](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| Instelling | Beschrijving |
|:--- |:--- |
| **Algemeen** | |
| Groepstitel |Tekst toodisplay bovenaan Hallo Hallo tegel. |
| Nieuwe groep |Selecteer een nieuwe groep toocreate in Hallo beginnen bij de huidige weergave Hallo. |
| Pictogram |De installatiekopie van bestand toodisplay volgende toohello resultaat in Hallo-header. |
| Pictogram gebruiken |Selecteer toohave Hallo pictogram weergegeven. |
| **Koptekst** | |
| Titel |Tekst toodisplay Hallo boven aan het Hallo-header. |
| Subtitel |Tekst toodisplay onder Hallo titel Hallo boven aan het Hallo-header. |
| **Lijndiagram** | |
| Query’s uitvoeren |Query toorun Hallo lijndiagram.  eerste Hallo-eigenschap moet een waarde en Hallo tweede teksteigenschap een numerieke waarde zijn.  Dit is doorgaans een query die gebruikmaakt van Hallo **meting** toosummarize resultaten.  Als het Hallo-query gebruikt Hallo **interval** sleutelwoord vervolgens Hallo x-as van grafiekgebied Hallo gebruikt dit tijdsinterval blijft.  Als het Hallo-query bevat geen Hallo **interval** sleutelwoord en vervolgens elk uur intervallen worden gebruikt voor Hallo x-as. |
| **Lijndiagram** |**> Y-as** |
| Logaritmische schaal gebruiken |Selecteer toouse een logaritmische schaal voor Hallo y-as. |
| Eenheden |Hallo-eenheden voor Hallo waarden geretourneerd door Hallo query opgeven.  Deze informatie is gebruikte toodisplay labels op Hallo grafiek die aangeeft Hallo waardetypen en desgewenst voor het converteren van Hallo waarden.  Hallo eenheidstype geeft Hallo categorie van het Hallo-eenheid en definieert Hallo huidige eenheidstype waarden die beschikbaar zijn.  Als u een waarde in converteren toothen Hallo numerieke worden waarden van Hallo huidige eenheid type toohello converteren tootype geconverteerd. |
| Aangepast etiket |Tekst toodisplay voor Hallo Y-as volgende toohello label voor het eenheidstype Hallo.  Als er geen naam is opgegeven, wordt alleen het eenheidstype Hallo weergegeven. |
| **Lijst** | |
| Query’s uitvoeren |Query toorun voor Hallo-lijst.  Hallo-telling van het aantal records dat wordt geretourneerd door de query Hallo Hallo wordt weergegeven. |
| Grafiek verbergen |Selecteer toodisable Hallo grafiek toohello rechts van Hallo numerieke kolom. |
| Sparklines inschakelen |Selecteer toodisplay sparkline in plaats van de horizontale balk.  Zie [algemene instellingen](#sparklines) voor meer informatie. |
| Kleur |Kleur van Hallo balken of sparklines. |
| Bewerking |Bewerking tooperform voor Hallo sparkline.  Zie [algemene instellingen](#sparklines) voor meer informatie. |
| De naam van & scheidingsteken |Willekeurig teken scheidingsteken als u wilt dat de eigenschap van de tekst hello tooparse in meerdere waarden.  Zie [algemene instellingen](#name-value-separator) voor meer informatie. |
| Navigatie-query |Toorun vragen wanneer Hallo gebruiker een item in Hallo lijst selecteert.  Zie [algemene instellingen](#navigation-query) voor meer informatie. |
| **Lijst** |**> Kolomtitels** |
| Naam |Tekst toodisplay Hallo boven aan de eerste kolom Hallo van Hallo-lijst. |
| Waarde |Tekst toodisplay Hallo boven aan de tweede kolom Hallo van Hallo-lijst. |
| **Lijst** |**> Drempelwaarden** |
| Drempelwaarden inschakelen |Selecteer tooenable drempelwaarden.  Zie [algemene instellingen](#thresholds) voor meer informatie. |

## <a name="stack-of-line-charts-part"></a>Stack van regel grafieken onderdeel
Drie afzonderlijke lijndiagrammen met meerdere reeksen door een query logboek weergegeven gedurende een bepaalde periode.

![-Stack van lijndiagrammen](media/log-analytics-view-designer/view-stack-line-charts.png)

| Instelling | Beschrijving |
|:--- |:--- |
| **Algemeen** | |
| Groepstitel |Tekst toodisplay bovenaan Hallo Hallo tegel. |
| Nieuwe groep |Selecteer een nieuwe groep toocreate in Hallo beginnen bij de huidige weergave Hallo. |
| Pictogram |De installatiekopie van bestand toodisplay volgende toohello resultaat in Hallo-header. |
| **Grafiek 1<br>grafiek 2<br>grafiek 3** |**> Header** |
| Titel |Tekst toodisplay Hallo boven aan het Hallo-grafiek. |
| Subtitel |Tekst toodisplay onder Hallo titel Hallo boven aan het Hallo-grafiek. |
| **Grafiek 1<br>grafiek 2<br>grafiek 3** |**Lijndiagram** |
| Query’s uitvoeren |Query toorun Hallo lijndiagram.  eerste Hallo-eigenschap moet een waarde en Hallo tweede teksteigenschap een numerieke waarde zijn.  Dit is doorgaans een query die gebruikmaakt van Hallo **meting** toosummarize resultaten.  Als het Hallo-query gebruikt Hallo **interval** sleutelwoord vervolgens Hallo x-as van grafiekgebied Hallo gebruikt dit tijdsinterval blijft.  Als het Hallo-query bevat geen Hallo **interval** sleutelwoord en vervolgens elk uur intervallen worden gebruikt voor Hallo x-as. |
| **Grafiek** |**> Y-as** |
| Logaritmische schaal gebruiken |Selecteer toouse een logaritmische schaal voor Hallo y-as. |
| Eenheden |Hallo-eenheden voor Hallo waarden geretourneerd door Hallo query opgeven.  Deze informatie is gebruikte toodisplay labels op Hallo grafiek die aangeeft Hallo waardetypen en desgewenst voor het converteren van Hallo waarden.  Hallo eenheidstype geeft Hallo categorie van het Hallo-eenheid en definieert Hallo huidige eenheidstype waarden die beschikbaar zijn.  Als u een waarde in converteren toothen Hallo numerieke worden waarden van Hallo huidige eenheid type toohello converteren tootype geconverteerd. |
| Aangepast etiket |Tekst toodisplay voor Hallo Y-as volgende toohello label voor het eenheidstype Hallo.  Als er geen naam is opgegeven, wordt alleen het eenheidstype Hallo weergegeven. |

## <a name="common-settings"></a>Algemene instellingen
Hallo volgende secties beschrijven instellingen algemene tooseveral visualisatie delen.

### <a name="name-value-separator">De naam van & scheidingsteken</a>
Willekeurig teken scheidingsteken als u wilt dat tooparse Hallo teksteigenschap uit een lijst met query in meerdere waarden.  Als u een scheidingsteken opgeeft, kunt u namen opgeven voor elk veld dat is gescheiden door Hallo dezelfde scheidingsteken in het naamvak Hallo.

Neem bijvoorbeeld een eigenschap genaamd *locatie* die waarden, zoals opgenomen *Redmond gebouw 41* en *Bellevue Building12*.  U kunt opgeven: voor Hallo naam & scheidingsteken en *stad gebouw* voor Hallo naam.  Dit zou elke waarde in de twee eigenschappen aangeroepen parseren *stad* en *gebouw*.

### <a name="navigation-query">Navigatie-query</a>
Toorun vragen wanneer Hallo gebruiker een item in Hallo lijst selecteert.  Gebruik *{geselecteerde item}* tooinclude Hallo syntaxis voor het item dat Hallo van de geselecteerde gebruiker.

Bijvoorbeeld, als hello query heeft een kolom met de naam *Computer* en Hallo navigatie query *{geselecteerde item}*, een query zoals *Computer = 'Computer'* zou worden uitgevoerd wanneer Hallo-gebruiker een computer hebt geselecteerd.  Als Hallo navigatie query *Type gebeurtenis {geselecteerde item} =* vervolgens Hallo query *Type = gebeurtenis Computer = 'Computer'* zou worden uitgevoerd.

### <a name="sparklines">Sparklines</a>
Een sparkline is een kleine lijndiagram die laat Hallo-waarde van een item uit de lijst gedurende een bepaalde periode zien.  Voor visualisatie delen met een lijst, kunt u selecteren of een horizontale balk aangeeft toodisplay Hallo relatieve waarde van een numerieke kolom of een sparkline de waarde waarmee wordt aangegeven gedurende een bepaalde periode.

Hallo volgende tabel beschrijft Hallo-instellingen voor sparklines.

| Instelling | Beschrijving |
|:--- |:--- |
| Sparklines inschakelen |Selecteer toodisplay sparkline in plaats van de horizontale balk. |
| Bewerking |Als sparklines zijn ingeschakeld, is dit Hallo bewerking tooperform op elke eigenschap in Hallo toocalculate Hallo lijstwaarden voor Hallo sparkline.<br><br>-Laatste voorbeeld: De laatste waarde voor de reeks Hallo tijdens Hallo tijdsinterval.<br>-Max: Maximumwaarde voor de reeks Hallo tijdens Hallo tijdsinterval.<br>-Min: Minimumwaarde voor de reeks Hallo tijdens tijdsinterval Hallo.<br>-Som: De som van waarden voor de reeks Hallo tijdens Hallo tijdsinterval.<br>-Overzicht: Maakt gebruik van Hallo dezelfde meting opdracht als Hallo-query in Hallo-header. |

### <a name="thresholds">Drempelwaarden</a>
Drempelwaarden kunnen u toodisplay een gekleurde pictogram volgende tooeach item in een lijst waarin u een snelle visuele indicator van items die groter zijn dan een bepaalde waarde of een bepaald bereik vallen.  U kan bijvoorbeeld een groen pictogram voor items met een acceptabele waarde, geel als Hallo waarde valt binnen een bereik dat een waarschuwing geeft en rood weergegeven als deze groter is dan de foutwaarde van een.

Wanneer u drempelwaarden voor een deel inschakelt, moet u een of meer drempels opgeven.  Deze kleur wordt gebruikt als het Hallo-waarde van een item is groter dan de drempelwaarde en lager is dan de volgende drempelwaarde hello.  Als Hallo item groter dan vervolgens hoogste drempelwaarde is, wordt deze kleur ingesteld.   

Elke set drempelwaarde heeft een drempelwaarde met een waarde van **standaard**.  Dit is Hallo kleur is ingesteld als er geen andere waarden zijn overschreden.  U kunt toevoegen of verwijderen van drempelwaarden door te klikken op Hallo  **+**  of **x** knop.

Hallo volgende tabel beschrijft Hallo-instellingen voor tresholds.

| Instelling | Beschrijving |
|:--- |:--- |
| Drempelwaarden inschakelen |Selecteer een pictogram kleur toohello links van elke waarde die aangeeft van de relatieve toospecified health drempelwaarden toodisplay. |
| Naam |Geef een naam tooidentify Hallo drempelwaarde. |
| Drempelwaarde |Waarde voor Hallo drempelwaarde.  Hallo health kleur voor elk lijstitem is toohello kleur van Hallo hoogste drempelwaarde overschreden door Hallo-item-waarde ingesteld.  Er is een standaarddrempelwaarde Hallo kleur is als er geen drempelwaarde wordt overschreden. |
| Kleur |De kleur voor Hallo drempelwaarde. |

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) toosupport Hallo query's in visualisatie delen.

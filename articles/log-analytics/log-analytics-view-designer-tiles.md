---
title: aaaTile verwijzing voor weergave Designer in OMS Log Analytics | Microsoft Docs
description: Weergave Designer in Log Analytics kunt u toocreate aangepaste weergaven in de OMS-console Hallo die verschillende visualisaties van gegevens in de OMS-opslagplaats Hallo bevatten. Dit artikel bevat een verwijzing van Hallo-instellingen voor elk Hallo tegels beschikbaar toouse in aangepaste weergaven.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 41787c8f-6c13-4520-b0d3-5d3d84fcf142
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 4706abb16b8a3719f5dbe8c89cd61739391ab8f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-tile-reference"></a>Log Analytics-ontwerper tegel verwijzing
Hallo-ontwerper in Log Analytics kunt u toocreate aangepaste weergaven in de OMS-console Hallo die verschillende visualisaties van gegevens in de OMS-opslagplaats Hallo bevatten. Dit artikel bevat een verwijzing van Hallo-instellingen voor elk Hallo tegels beschikbaar toouse in aangepaste weergaven.

Er zijn andere artikelen die beschikbaar zijn voor weergave Designer:

* [Designer bekijken](log-analytics-view-designer.md) -overzicht van Hallo Designer bekijken en procedures voor het maken en bewerken van aangepaste weergaven.
* [Visualisatie onderdeelverwijzing](log-analytics-view-designer-parts.md) -verwijzing van instellingen voor elk Hallo Hallo tegels beschikbaar toouse in aangepaste weergaven.

>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [querytaal van nieuwe logboekanalyse](log-analytics-log-search-upgrade.md), en vervolgens de query's in alle weergaven moeten worden geschreven in Hallo [nieuwe querytaal](https://go.microsoft.com/fwlink/?linkid=856078).  De weergaven die zijn gemaakt voordat het Hallo-werkruimte is bijgewerkt worden doorloopt geconverteerd.

Hallo bevat volgende tabel Hallo verschillende soorten tegels beschikbaar in het Hallo-ontwerper.  Hallo in de volgende secties beschrijven elk tegeltype in detail en hun eigenschappen.

| Tegel | Beschrijving |
|:--- |:--- |
| [Aantal](#number-tile) |Enkel getal met het aantal records uit een query. |
| [Twee getallen](#two-numbers-tile) |Twee één getallen met het aantal records uit twee verschillende query's. |
| [Ring](#donut-tile) |Ring grafiek op basis van een query met een totale waarde in Hallo center. |
| [Lijndiagram & toelichting](#line-chart-amp-callout-tile) |Lijndiagram op basis van een query en een toelichting bij een totale waarde. |
| [Lijndiagram](#line-chart-tile) |Lijndiagram op basis van een query. |
| [Twee tijdlijnen](#two-timelines-tile) |Kolomdiagram met twee reeksen, die elk op basis van een afzonderlijke query. |

## <a name="number-tile"></a>Aantal tegel
Hallo **getal** tegel Hallo telling van records uit een query logboek en een label met één getal weergegeven.

![Aantal tegel](media/log-analytics-view-designer/tile-number.png)

| Instelling | Beschrijving |
|:--- |:--- |
| Naam |Tekst toodisplay bovenaan Hallo Hallo tegel. |
| Beschrijving |Tekst toodisplay onder de naam van de tegel Hallo. |
| **Tegel** | |
| Legenda |Tekst toodisplay onder Hallo-waarde. |
| Query’s uitvoeren |Query toorun.  Hallo-telling van het aantal records dat wordt geretourneerd door de query Hallo Hallo wordt weergegeven. |
| **Geavanceerde** |**> Gegevensstroom verificatie** |
| Ingeschakeld |Selecteer als gegevensstroom verificatie moet worden ingeschakeld voor Hallo tegel.  Dit biedt een alternatieve bericht als gegevens niet beschikbaar voor Hallo tegel zijn.  Dit is gewoonlijk gebruikte tooprovide een bericht in de tijdelijke periode Hallo wanneer Hallo weergave is geïnstalleerd en de gegevens afkomstig zijn beschikbaar. |
| Query’s uitvoeren |Query uitvoeren op toorun toocheck als gegevens beschikbaar voor Hallo weergave.  Als Hallo query geen resultaten oplevert, wordt een bericht weergegeven in plaats van de waarde van de belangrijkste query Hallo Hallo. |
| Bericht |Bericht toodisplay als Hallo-gegevensstroom verificatie query geen gegevens geretourneerd.  Als u geen bericht opgeeft *uitvoeren Assessment* wordt weergegeven. |


## <a name="two-numbers-tile"></a>Twee getallen tegel
Hallo **twee nummer** naast elkaar worden de twee getallen Hallo aantal records uit twee verschillende logboek-query's en een label voor elke softwaretoepassing wordt weergegeven.

![Twee getallen tegel](media/log-analytics-view-designer/tile-two-numbers.png)

| Instelling | Beschrijving |
|:--- |:--- |
| Naam |Tekst toodisplay bovenaan Hallo Hallo tegel. |
| Beschrijving |Tekst toodisplay onder de naam van de tegel Hallo. |
| **Eerste tegel** | |
| Legenda |Tekst toodisplay onder Hallo-waarde. |
| Query’s uitvoeren |Query toorun.  Hallo-telling van het aantal records dat wordt geretourneerd door de query Hallo Hallo wordt weergegeven. |
| **Tweede tegel** | |
| Legenda |Tekst toodisplay onder Hallo-waarde. |
| Query’s uitvoeren |Query toorun.  Hallo-telling van het aantal records dat wordt geretourneerd door de query Hallo Hallo wordt weergegeven. |
| **Geavanceerde** |**> Gegevensstroom verificatie** |
| Ingeschakeld |Selecteer als gegevensstroom verificatie moet worden ingeschakeld voor Hallo tegel.  Dit biedt een alternatieve bericht als gegevens niet beschikbaar voor Hallo tegel zijn.  Dit is gewoonlijk gebruikte tooprovide een bericht in de tijdelijke periode Hallo wanneer Hallo weergave is geïnstalleerd en de gegevens afkomstig zijn beschikbaar. |
| Query’s uitvoeren |Query uitvoeren op toorun toocheck als gegevens beschikbaar voor Hallo weergave.  Als Hallo query geen resultaten oplevert, wordt een bericht weergegeven in plaats van de waarde van de belangrijkste query Hallo Hallo. |
| Bericht |Bericht toodisplay als Hallo-gegevensstroom verificatie query geen gegevens geretourneerd.  Als u geen bericht opgeeft *uitvoeren Assessment* wordt weergegeven. |


## <a name="donut-tile"></a>Tegel ring
Hallo **ring** tegel één getal gedestilleerd uit de kolom van een waarde in een logboek-query wordt weergegeven.  Hallo Ring worden resultaten van de eerste drie records Hallo grafisch weergegeven.

![Tegel ring](media/log-analytics-view-designer/tile-donut.png)

| Instelling | Beschrijving |
|:--- |:--- |
| Naam |Tekst toodisplay bovenaan Hallo Hallo tegel. |
| Beschrijving |Tekst toodisplay onder de naam van de tegel Hallo. |
| **Ring** | |
| Query’s uitvoeren |Query toorun voor Hallo ring.  eerste Hallo-eigenschap moet een waarde en Hallo tweede teksteigenschap een numerieke waarde zijn.  Dit is doorgaans een query die gebruikmaakt van Hallo **meting** toosummarize resultaten. |
| **Ring** |**> Center** |
| Tekst |Tekst toodisplay onder Hallo waarde binnen Hallo ring. |
| Bewerking |Hallo bewerking tooperform op Hallo eigenschap toosummarize tooa één waarde.<br><br>-Som: Hallo waarden van alle records met waarde van de eigenschap Hallo toevoegen.<br>-Percentage: Percentage van de waarden van records met Hallo eigenschap waarde vergeleken toohello Hallo opgeteld opgeteld waarden van alle records. |
| Resultaatwaarden die worden gebruikt in de bewerking center |(Optioneel) Klik op Hallo plusteken tooadd een of meer waarden.  Hallo-resultaten van Hallo query worden beperkt toorecords met Hallo eigenschapswaarden die u opgeeft.  Als er geen waarden worden toegevoegd, dan alle records zijn opgenomen in Hallo query. |
| **Ring** |**> Aanvullende opties** |
| Kleuren |Hallo kleur toodisplay voor elk van de drie belangrijkste eigenschappen Hallo.  Als u toospecify alternatieve kleuren voor specifieke eigenschapswaarden wilt, gebruik geavanceerde kleur toewijzen. |
| Geavanceerde kleur toewijzen |Geeft een kleur voor specifieke waarden van eigenschappen.  Als Hallo-waarde die u opgeeft in bovenste drie Hallo vervolgens Hallo alternatieve kleur wordt weergegeven in plaats van de standaardkleur Hallo.  Als Hallo-eigenschap is niet bovenste drie Hallo en Hallo kleur niet wordt weergegeven. |
| **Geavanceerde** |**> Gegevensstroom verificatie** |
| Ingeschakeld |Selecteer als gegevensstroom verificatie moet worden ingeschakeld voor Hallo tegel.  Dit biedt een alternatieve bericht als gegevens niet beschikbaar voor Hallo tegel zijn.  Dit is gewoonlijk gebruikte tooprovide een bericht in de tijdelijke periode Hallo wanneer Hallo weergave is geïnstalleerd en de gegevens afkomstig zijn beschikbaar. |
| Query’s uitvoeren |Query uitvoeren op toorun toocheck als gegevens beschikbaar voor Hallo weergave.  Als Hallo query geen resultaten oplevert, wordt een bericht weergegeven in plaats van de waarde van de belangrijkste query Hallo Hallo. |
| Bericht |Bericht toodisplay als Hallo-gegevensstroom verificatie query geen gegevens geretourneerd.  Als u geen bericht opgeeft *uitvoeren Assessment* wordt weergegeven. |


## <a name="line-chart-tile"></a>Regel grafiek tegel
Hallo **lijndiagram** tegel wordt een lijndiagram met meerdere reeksen door een query logboek weergegeven gedurende een bepaalde periode.  

![Lijndiagram & toelichting tegel](media/log-analytics-view-designer/tile-line-chart.png)

| Instelling | Beschrijving |
|:--- |:--- |
| Naam |Tekst toodisplay bovenaan Hallo Hallo tegel. |
| Beschrijving |Tekst toodisplay onder de naam van de tegel Hallo. |
| **Lijndiagram** | |
| Query’s uitvoeren |Query toorun Hallo lijndiagram.  eerste Hallo-eigenschap moet een waarde en Hallo tweede teksteigenschap een numerieke waarde zijn.  Dit is doorgaans een query die gebruikmaakt van Hallo **meting** toosummarize resultaten.  Als het Hallo-query gebruikt Hallo **interval** sleutelwoord vervolgens Hallo x-as van grafiekgebied Hallo gebruikt dit tijdsinterval blijft.  Als het Hallo-query bevat geen Hallo **interval** sleutelwoord en vervolgens elk uur intervallen worden gebruikt voor Hallo x-as. |
| **Lijndiagram** |**> Y-as** |
| Logaritmische schaal gebruiken |Selecteer toouse een logaritmische schaal voor Hallo y-as. |
| Eenheden |Hallo-eenheden voor Hallo waarden geretourneerd door Hallo query opgeven.  Deze informatie is gebruikte toodisplay labels op Hallo grafiek die aangeeft Hallo waardetypen en desgewenst voor het converteren van Hallo waarden.  Hallo **eenheidstype** geeft Hallo categorie van het Hallo-eenheid en definieert Hallo **huidige eenheidstype** waarden die beschikbaar zijn.  Als u een waarde in selecteert **converteren naar** vervolgens Hallo numerieke waarden worden geconverteerd van Hallo **huidige eenheid** Typ toohello **converteren naar** type. |
| Aangepast etiket |Tekst toodisplay voor Hallo Y-as volgende toohello label voor het eenheidstype Hallo.  Als er geen naam is opgegeven, wordt alleen het eenheidstype Hallo weergegeven. |
| **Geavanceerde** |**> Gegevensstroom verificatie** |
| Ingeschakeld |Selecteer als gegevensstroom verificatie moet worden ingeschakeld voor Hallo tegel.  Dit biedt een alternatieve bericht als gegevens niet beschikbaar voor Hallo tegel zijn.  Dit is gewoonlijk gebruikte tooprovide een bericht in de tijdelijke periode Hallo wanneer Hallo weergave is geïnstalleerd en de gegevens afkomstig zijn beschikbaar. |
| Query’s uitvoeren |Query uitvoeren op toorun toocheck als gegevens beschikbaar voor Hallo weergave.  Als Hallo query geen resultaten oplevert, wordt een bericht weergegeven in plaats van de waarde van de belangrijkste query Hallo Hallo. |
| Bericht |Bericht toodisplay als Hallo-gegevensstroom verificatie query geen gegevens geretourneerd.  Als u geen bericht opgeeft *uitvoeren Assessment* wordt weergegeven. |


## <a name="line-chart--callout-tile"></a>De tegel diagram & toelichting regel
Hallo **regel grafiek & toelichting** tegel bevat een lijndiagram met meerdere reeksen door een query logboek gedurende de tijd en een toelichting met een samengevatte waarde.  

![Lijndiagram & toelichting tegel](media/log-analytics-view-designer/tile-line-chart-callout.png)

| Instelling | Beschrijving |
|:--- |:--- |
| Naam |Tekst toodisplay bovenaan Hallo Hallo tegel. |
| Beschrijving |Tekst toodisplay onder de naam van de tegel Hallo. |
| **Lijndiagram** | |
| Query’s uitvoeren |Query toorun Hallo lijndiagram.  eerste Hallo-eigenschap moet een waarde en Hallo tweede teksteigenschap een numerieke waarde zijn.  Dit is doorgaans een query die gebruikmaakt van Hallo **meting** toosummarize resultaten.  Als het Hallo-query gebruikt Hallo **interval** sleutelwoord vervolgens Hallo x-as van grafiekgebied Hallo gebruikt dit tijdsinterval blijft.  Als het Hallo-query bevat geen Hallo **interval** sleutelwoord en vervolgens elk uur intervallen worden gebruikt voor Hallo x-as. |
| **Lijndiagram** |**> Toelichting** |
| Toelichting |Titel tekst toodisplay boven Hallo toelichting waarde. |
| Naam van de gegevensreeks |De waarde van de eigenschap voor Hallo reeks toouse voor Hallo toelichting waarde.  Als geen reeksen is opgegeven, worden alle records uit Hallo query gebruikt. |
| Bewerking |Hallo bewerking tooperform op Hallo waarde toosummarize tooa één eigenschapswaarde voor Hallo toelichting.<br>-Gemiddelde: Het gemiddelde van de waarde op Hallo van alle records.<br><br>-Aantal: De telling van alle records die zijn geretourneerd door Hallo-query.<br>-Laatste: Voorbeeldwaarde vanaf het laatste Hallo-interval in Hallo diagram opgenomen.<br>-Max: Maximumwaarde van hello-intervallen opgenomen in de grafiek Hallo.<br>-Min: Minimumwaarde van hello-intervallen opgenomen in de grafiek Hallo.<br>-Som: De som van de waarde op Hallo van alle records. |
| **Lijndiagram** |**> Y-as** |
| Logaritmische schaal gebruiken |Selecteer toouse een logaritmische schaal voor Hallo y-as. |
| Eenheden |Hallo-eenheden voor Hallo waarden geretourneerd door Hallo query opgeven.  Deze informatie is gebruikte toodisplay labels op Hallo grafiek die aangeeft Hallo waardetypen en desgewenst voor het converteren van Hallo waarden.  Hallo **eenheidstype** geeft Hallo categorie van het Hallo-eenheid en definieert Hallo **huidige eenheidstype** waarden die beschikbaar zijn.  Als u een waarde in selecteert **converteren naar** vervolgens Hallo numerieke waarden worden geconverteerd van Hallo **huidige eenheid** Typ toohello **converteren naar** type. |
| Aangepast etiket |Tekst toodisplay voor Hallo Y-as volgende toohello label voor het eenheidstype Hallo.  Als er geen naam is opgegeven, wordt alleen het eenheidstype Hallo weergegeven. |
| **Geavanceerde** |**> Gegevensstroom verificatie** |
| Ingeschakeld |Selecteer als gegevensstroom verificatie moet worden ingeschakeld voor Hallo tegel.  Dit biedt een alternatieve bericht als gegevens niet beschikbaar voor Hallo tegel zijn.  Dit is gewoonlijk gebruikte tooprovide een bericht in de tijdelijke periode Hallo wanneer Hallo weergave is geïnstalleerd en de gegevens afkomstig zijn beschikbaar. |
| Query’s uitvoeren |Query uitvoeren op toorun toocheck als gegevens beschikbaar voor Hallo weergave.  Als Hallo query geen resultaten oplevert, wordt een bericht weergegeven in plaats van de waarde van de belangrijkste query Hallo Hallo. |
| Bericht |Bericht toodisplay als Hallo-gegevensstroom verificatie query geen gegevens geretourneerd.  Als u geen bericht opgeeft *uitvoeren Assessment* wordt weergegeven. |


## <a name="two-timelines-tile"></a>Twee tijdlijnen tegel
Hallo **twee tijdlijnen** tegel Hallo resultaten van twee logboek-query's worden weergegeven gedurende een bepaalde periode als kolomdiagrammen.  Een toelichting wordt weergegeven voor elke reeks.  

![Twee tijdlijnen tegel](media/log-analytics-view-designer/tile-two-timelines.png)

| Instelling | Beschrijving |
|:--- |:--- |
| Naam |Tekst toodisplay bovenaan Hallo Hallo tegel. |
| Beschrijving |Tekst toodisplay onder de naam van de tegel Hallo. |
| Eerste grafiek | |
| Legenda |Tekst toodisplay onder Hallo bijschrift voor de eerste reeks Hallo. |
| Kleur |Kleur toouse voor kolommen in de eerste reeks Hallo Hallo. |
| Grafiek-Query |Query toorun voor de eerste reeks Hallo.  Hallo aantal Hallo records over elk tijdsinterval wordt vertegenwoordigd door Hallo grafiek kolommen. |
| Bewerking |Hallo bewerking tooperform op Hallo waarde toosummarize tooa één eigenschapswaarde voor Hallo toelichting.<br><br>-Gemiddelde: Het gemiddelde van de waarde op Hallo van alle records.<br>-Aantal: De telling van alle records die zijn geretourneerd door Hallo-query.<br>-Laatste: Voorbeeldwaarde vanaf het laatste Hallo-interval in Hallo diagram opgenomen.<br>-Max: Maximumwaarde van hello-intervallen opgenomen in de grafiek Hallo. |
| **Tweede grafiek** | |
| Legenda |Tekst toodisplay onder Hallo bijschrift voor de tweede reeks Hallo. |
| Kleur |Kleur toouse voor Hallo kolommen in de tweede reeks Hallo. |
| Grafiek-Query |Query toorun voor de tweede reeks Hallo.  Hallo aantal Hallo records over elk tijdsinterval wordt vertegenwoordigd door Hallo grafiek kolommen. |
| Bewerking |Hallo bewerking tooperform op Hallo waarde toosummarize tooa één eigenschapswaarde voor Hallo toelichting.<br><br>-Gemiddelde: Het gemiddelde van de waarde op Hallo van alle records.<br>-Aantal: De telling van alle records die zijn geretourneerd door Hallo-query.<br>-Laatste: Voorbeeldwaarde vanaf het laatste Hallo-interval in Hallo diagram opgenomen.<br>-Max: Maximumwaarde van hello-intervallen opgenomen in de grafiek Hallo. |
| **Geavanceerde** |**> Gegevensstroom verificatie** |
| Ingeschakeld |Selecteer als gegevensstroom verificatie moet worden ingeschakeld voor Hallo tegel.  Dit biedt een alternatieve bericht als gegevens niet beschikbaar voor Hallo tegel zijn.  Dit is gewoonlijk gebruikte tooprovide een bericht in de tijdelijke periode Hallo wanneer Hallo weergave is geïnstalleerd en de gegevens afkomstig zijn beschikbaar. |
| Query’s uitvoeren |Query uitvoeren op toorun toocheck als gegevens beschikbaar voor Hallo weergave.  Als Hallo query geen resultaten oplevert, wordt een bericht weergegeven in plaats van de waarde van de belangrijkste query Hallo Hallo. |
| Bericht |Bericht toodisplay als Hallo-gegevensstroom verificatie query geen gegevens geretourneerd.  Als u geen bericht opgeeft *uitvoeren Assessment* wordt weergegeven. |


## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) toosupport Hallo query's in de tegels.
* Voeg [visualisatie delen](log-analytics-view-designer-parts.md) tooyour aangepaste weergave.

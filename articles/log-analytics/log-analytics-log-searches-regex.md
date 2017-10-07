---
title: aaaRegular expressies in de OMS-logboekanalyse Meld zoekopdrachten | Microsoft Docs
description: Kunt u Hallo RegEx-sleutelwoord in logboekanalyse logboek zoekopdrachten toohello Hallo filterresultaten volgens tooa reguliere expressie.  In dit artikel biedt Hallo-syntaxis voor deze expressies met enkele voorbeelden.
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
ms.date: 08/08/2017
ms.author: bwren
ms.openlocfilehash: 3033593dac2c50e911fc69054947d40d4a74369b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-regular-expressions-toofilter-log-searches-in-log-analytics"></a>Met behulp van reguliere expressies toofilter logboek zoekt in Log Analytics

[Meld u zoekopdrachten](log-analytics-log-searches.md) kunt u tooextract informatie uit Hallo Log Analytics-bibliotheek.  [Filterexpressies](log-analytics-search-reference.md#filter-expressions) kunt u de resultaten van de toofilter Hallo van Hallo zoeken op basis van criteria toospecific.  Hallo **RegEx** sleutelwoord kunt u toospecify een reguliere expressie voor dit filter.  

In dit artikel biedt details over de syntaxis met gewone uitdrukkingen Hallo door Log Analytics gebruikt.

> [!NOTE]
> U kunt alleen RegEx met doorzoekbare velden.  Zie voor meer informatie over de doorzoekbare velden **veldtypen** in [vinden van gegevens met behulp van logboek zoekopdrachten in logboekanalyse](log-analytics-log-searches.md#use-additional-filters).


## <a name="regex-keyword"></a>RegEx-sleutelwoord

Gebruik Hallo na syntaxis toouse hello **RegEx** -sleutelwoord in een logboek zoekopdracht.  U kunt andere secties in dit artikel toodetermine Hallo syntaxis van de reguliere expressie Hallo zelf Hallo.

    field:Regex("Regular Expression")
    field=Regex("Regular Expression")

Bijvoorbeeld, een reguliere expressie tooreturn waarschuwing toouse registreert met een type *waarschuwing* of *fout*, gebruikt u Hallo logboek zoeken te volgen.

    Type=Alert AlertSeverity=RegEx("Warning|Error")

## <a name="partial-matches"></a>Gedeeltelijke overeenkomsten
Houd er rekening mee dat Hallo reguliere expressie moet overeenkomen met volledige tekst van de eigenschap Hallo Hallo.  Gedeeltelijke overeenkomsten worden geen records geretourneerd.  Bijvoorbeeld, als u tooreturn records uit een computer met de naam srv01.contoso.com probeerde, Hallo na logboek zoeken zou **niet** records geretourneerd.

    Computer=RegEx("srv..")

Dit is omdat het eerste gedeelte alleen Hallo van Hallo naam overeenkomt met de reguliere expressie Hallo.  Hallo zou volgende twee logboek zoekopdrachten retourneren records van deze computer omdat ze overeenkomen met de volledige naam Hallo.

    Computer=RegEx("srv..@")
    Computer=RegEx("srv...contoso.com")

## <a name="characters"></a>Tekens
Geef andere tekens.

| Teken | Beschrijving | Voorbeeld | Voorbeeld komt overeen met |
|:--|:--|:--|:--|
| een | Een exemplaar van de Hallo-teken. | Computer=RegEx("Srv01.contoso.com") | Srv01.contoso.com |
| . | Een willekeurig teken. | Computer=RegEx("SRV...contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| een? | Nul of één exemplaar van Hallo-teken. | Computer RegEx = (' srv01?. Contoso.com') | srv0.contoso.com<br>Srv01.contoso.com |
| een * | Nul of meer exemplaren van Hallo-teken. | Computer=RegEx("Srv01*.contoso.com") | srv0.contoso.com<br>Srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| een + | Een of meer exemplaren van Hallo-teken. | Computer=RegEx("Srv01+.contoso.com") | Srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| [*abc*] | Overeenkomen met een willekeurig teken Hallo haakjes | Computer=RegEx("srv0[123].contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| [*een*-*z*] | Overeen met een enkel teken in Hallo bereik.  Kan bestaan uit meerdere adresbereiken. | Computer=RegEx("srv0[1-3].contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| [^*abc*] | Geen van de tekens Hallo Hallo haakjes | Computer=RegEx("srv0[^123].contoso.com") | srv05.contoso.com<br>SRV06.contoso.com<br>srv07.contoso.com |
| [^*een*-*z*] | Geen van Hallo tekens in Hallo bereik. | Computer=RegEx("srv0[^1-3].contoso.com") | srv05.contoso.com<br>SRV06.contoso.com<br>srv07.contoso.com |
| [*n*-*m*] | Overeen met een reeks numerieke tekens. | Computer=RegEx("SRV[01-03].contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| @ | Een tekenreeks. | Computer RegEx = ('srv@.contoso.com') | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |


## <a name="multiple-occurences-of-character"></a>Meerdere exemplaren van teken
Geef meerdere exemplaren van een bepaalde tekens.

| Teken | Beschrijving | Voorbeeld | Voorbeeld komt overeen met |
|:--|:--|:--|:--|
| een {n} |  *n*exemplaren van Hallo-teken. | Computer=RegEx("BW-Win-sc01{3}.bwren.Lab") | BW-win-sc0111.bwren.lab |
| een {n} |  *n*of meer exemplaren van Hallo-teken. | Computer=RegEx("BW-Win-sc01{3,}.bwren.Lab") | BW-win-sc0111.bwren.lab<br>BW-win-sc01111.bwren.lab<br>BW-win-sc011111.bwren.lab<br>BW-win-sc0111111.bwren.lab |
| {n, m} |  *n*te*m* exemplaren van Hallo-teken. | Computer=RegEx("BW-Win-sc01{3,5}.bwren.Lab") | BW-win-sc0111.bwren.lab<br>BW-win-sc01111.bwren.lab<br>BW-win-sc011111.bwren.lab |


## <a name="logical-expressions"></a>Logische expressies
Selecteer in meerdere waarden.

| Teken | Beschrijving | Voorbeeld | Voorbeeld komt overeen met |
|:--|:--|:--|:--|
| &#124; | Logische OR.  Resultaat wordt weergegeven als op een van de expressies overeenkomen. | Type waarschuwing AlertSeverity = = RegEx ('waarschuwing &#124; Fout") | Waarschuwing<br>Fout |
| & | Logische AND.  Resultaat wordt weergegeven als op beide expressies overeenkomen | EventData = regex (' (beveiliging.\* &. \*geslaagd. \*)") | Beveiligingscontrole geslaagd |


## <a name="literals"></a>Letterlijke waarden
Speciale tekens tooliteral tekens worden geconverteerd.  Dit omvat tekens die functionaliteit, zoals tooregular expressies bieden?-\*^\[\]{}\(\)+\|. &.

| Teken | Beschrijving | Voorbeeld | Voorbeeld komt overeen met |
|:--|:--|:--|:--|
| \\ | Converteert een speciaal teken tooa literal. | Status_CF =\\[fout\\] @<br>Status_CF fout =\\-@ | [Fout] Bestand niet gevonden.<br>Fout-bestand niet gevonden. |


## <a name="next-steps"></a>Volgende stappen

* Raken met [Meld zoekopdrachten](log-analytics-log-searches.md) tooview en analyseren in Hallo Log Analytics-opslagplaats.

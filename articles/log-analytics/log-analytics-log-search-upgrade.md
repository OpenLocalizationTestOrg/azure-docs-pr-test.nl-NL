---
title: Azure-logboekanalyse toonew zoekfunctie aaaUpgrading | Microsoft Docs
description: nieuwe logboekanalyse Hallo-querytaal is bijna hier en kunt u de openbare preview Hallo deelnemen.  Dit artikel wordt beschreven Hallo voordelen van de nieuwe taal Hallo en hoe tooconvert uw werkruimte.
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
ms.author: magoedte;bwren
ms.openlocfilehash: 7659c9d1467cab79d3a16e73b52b507ed281b002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-azure-log-analytics-workspace-toonew-log-search"></a>Upgrade van uw Azure-logboekanalyse werkruimte toonew logboek zoekopdracht

> [!NOTE]
> Upgrade toohello nieuwe Log Analytics-querytaal is momenteel optionele zodat u tijd te[aan de slag met de nieuwe taal Hallo](https://go.microsoft.com/fwlink/?linkid=856078).  

nieuwe logboekanalyse Hallo-querytaal is hier en u moet tooupgrade uw werkruimte tootake voordeel hiervan.  Dit artikel wordt beschreven Hallo voordelen van de nieuwe taal Hallo en hoe tooconvert uw werkruimte.  Als u geen tooupgrade nu kiest, wordt uw werkruimte voortgezet toooperate net als altijd heeft, maar wordt deze automatisch geconverteerd op een later tijdstip.  U ontvangt veel tijd en een melding wanneer deze datum is ingesteld.

In dit artikel biedt details over Hallo nieuwe taal en het Hallo-upgradeproces.

## <a name="why-hello-new-language"></a>Waarom Hallo nieuwe taal?
We begrijpen dat er pijn in een overgang is en wij zijn niet querytaal Hallo Hallo desgewenst ervan te wijzigen.  Er zijn diverse redenen die deze wijziging aanzienlijke waarde tooour Log Analytics-klanten biedt.

- **Eenvoudige maar krachtige.** Hallo nieuwe taal is eenvoudiger toounderstand en vergelijkbare tooSQL met meer constructs, zoals natuurlijke taal dan Hallo verouderde taal.
- **Volledige piping taal.**  Hallo nieuwe taal heeft uitgebreidere piping mogelijkheden dan Hallo verouderde taal.  Bijna alle doorgesluisd tooanother opdracht toocreate meer complexe query's dan eerder mogelijk zou kunnen worden uitgevoerd.
- **Extracties zoektijd veld.**  Hallo nieuwe taal ondersteunt meer geavanceerde runtime berekende velden dan Hallo verouderde taal.  U kunt complexe berekeningen gebruiken voor uitgebreide velden en vervolgens Hallo berekende velden te gebruiken voor aanvullende opdrachten, inclusief samenvoegingen en aggregaties.
- **Geavanceerde joins.**  nieuwe taal Hallo biedt meer geavanceerde joins dan Hallo verouderde taal inclusief Hallo mogelijkheid toojoin tabellen op meerdere velden, inner en outer joins te gebruiken en deelnemen aan op de uitgebreide velden.
- **Functies voor datum/tijd.**  Hallo nieuwe taal heeft dan Hallo verouderde taal geavanceerdere datum/tijd-functies.
- **Smart Analytics.**  de nieuwe taal Hallo beschikt over geavanceerde algoritmen tooevaluate patronen in de gegevenssets en vergelijk verschillende sets van gegevens.
- **Geavanceerde Analytics-portal.**  Hallo geavanceerde analyses portal biedt analysefuncties niet beschikbaar in Hallo logboekanalyse portal, met inbegrip van meerdere regels bewerken van query's, aanvullende visualisaties en geavanceerde diagnostische gegevens.
- **Consistentie met andere toepassingen.**  Hallo nieuwe taal en het Hallo geavanceerde Analytics-Portal al worden gebruikt voor analyses in Application Insights.  Implementeert voor logboekanalyse consistentie alle Azure-services.
- **Integratie met Power BI.** Query's in de nieuwe taal Hallo zijn geëxporteerde tooPower BI Desktop kunt u gebruikmaken van de mogelijkheden van de transformatie uitgebreide gegevens.
- **Nog veel meer.** Raadpleeg toohello [Azure Log Analytics Query Language](https://docs.loganalytics.io) site voor meer informatie en zelfstudies over Hallo nieuwe taal.


## <a name="when-can-i-upgrade"></a>Wanneer kan ik upgraden?
Hallo-upgrade wordt teruggedraaid uit in alle Azure-regio's zodat het mogelijk beschikbaar in bepaalde gebieden vóór andere.  Weet u wanneer uw werkruimte beschikbaar toobe bijgewerkt wanneer er Hallo paarse banner aan de bovenkant Hallo van uw werkruimte uitnodiging tooupgrade is.

![Upgrade 1](media/log-analytics-log-search-upgrade/upgrade-01a.png)

## <a name="what-happens-when-i-upgrade"></a>Wat gebeurt er wanneer ik een upgrade?
Als u uw werkruimte converteert, zijn alle opgeslagen zoekopdrachten, regels voor waarschuwingen en weergaven die u hebt gemaakt met de Hallo-ontwerper automatisch geconverteerde toohello nieuwe taal.  Zoekopdrachten die zijn opgenomen in oplossingen niet automatisch worden geconverteerd, maar ze zijn in plaats daarvan geconverteerd op Hallo snel wanneer u ze opent.  Dit is volledig transparant tooyou.

## <a name="can-i-go-back-after-i-upgrade"></a>Kan ik gaat u terug wanneer ik een upgrade uitvoeren?
Wanneer u bijwerkt, wordt een volledige back-up van uw werkruimte gemaakt met een momentopname van alle opgeslagen zoekopdrachten, waarschuwingsregel en weergaven.  Hiermee kunt u toorestore uw oude werkruimte als u later moet willen.

toorestore uw oude werkruimte te gaan**instellingen** in uw werkruimte en vervolgens **samenvatting Upgrade**.  U kunt vervolgens Hallo optie te selecteren**verouderde werkruimte terugzetten**.  

![Verouderde herstellen](media/log-analytics-log-search-upgrade/restore-legacy-b.png)

## <a name="how-do-i-perform-hello-upgrade"></a>Hoe voer ik Hallo upgrade uit?
U kunt uw werkruimte bijwerken wanneer er Hallo paarse banner Hallo boven aan het Hallo-portal.  

1.  Hallo-upgradeproces start door te klikken op Hallo paarse banner waarin staat dat **meer informatie en upgrade**.<br>![Upgrade 2](media/log-analytics-log-search-upgrade/upgrade-01a.png)<br>
2.  Lees Hallo aanvullende informatie over het Hallo-upgrade op Hallo Upgradegegevens pagina.<br>![Upgrade 2](media/log-analytics-log-search-upgrade/upgrade-03.png)<br>
3.  Klik op **nu bijwerken** toostart Hallo upgrade.<br>![Upgrade 4](media/log-analytics-log-search-upgrade/upgrade-04.png)<br>Een melding in de rechterbovenhoek Hallo weergegeven Hallo status.<br>![Upgrade 5](media/log-analytics-log-search-upgrade/upgrade-05.png)
4.  Dat is alles.  Bespreek toohello logboek zoeken pagina toohave kijken uw bijgewerkte werkruimte.<br>![Upgrade 6](media/log-analytics-log-search-upgrade/upgrade-06.png)<br>

Als u een probleem dat ervoor zorgt de upgrade toofail Hallo dat ondervindt, kunt u gaan toohello [discussieforum](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) en uw vraag plaatsen of [Maak een ondersteuningsaanvraag](../azure-supportability/how-to-create-azure-support-request.md) van hello Azure-portal.

## <a name="how-do-i-learn-hello-new-language"></a>Hoe ik Hallo nieuwe taal lezen?
Omdat deze wordt gebruikt door meerdere services gemaakte we een [externe site toohost Hallo documentatie](https://docs.loganalytics.io/) voor Hallo nieuwe taal.  Dit omvat zelfstudies, voorbeelden en een volledig overzicht van de toohelp die u toospeed actief. U kunt een zelfstudie over de nieuwe taal op Hallo doorlopen [aan de slag met query's](https://go.microsoft.com/fwlink/?linkid=856078) en toegang tot de Naslaggids Hallo op [logboekanalyse querytaal](https://go.microsoft.com/fwlink/?linkid=856079).  

Als u al bekend bent met Hallo verouderde logboekanalyse querytaal echter vervolgens kunt u Hallo taal converter tooyour werkruimte wordt toegevoegd als onderdeel van Hallo upgrade.

Typ in de verouderde query en klik vervolgens op **converteren** toosee Hallo versie vertaald.  U kunt vervolgens ofwel op Hallo knop toorun Hallo zoeken of kopiëren en Hallo geconverteerd query toouse ergens anders zoals een waarschuwingsregel plakken.

![Taal converter](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="next-steps"></a>Volgende stappen
- Bekijk een [zelfstudie over de nieuwe taal Hallo](https://go.microsoft.com/fwlink/?linkid=856078).
- Doorlopen een [zelfstudie over het gebruik Hallo logboek zoeken portal](log-analytics-log-search-log-search-portal.md) met nieuwe querytaal Hallo.
- Een inleiding toohello nieuwe ophalen [Advanced Analytics-portal](https://go.microsoft.com/fwlink/?linkid=856587).

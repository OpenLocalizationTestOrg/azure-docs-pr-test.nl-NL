---
title: aaaPortals voor het maken en bewerken van logboek-query's in Azure Log Analytics | Microsoft Docs
description: Dit artikel wordt beschreven Hallo portals dat u kunt in Azure-logboekanalyse toocreate gebruiken en logboek zoekopdrachten bewerken.
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
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 7a2657574a132b2c4298511bb31259e68113ac91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="portals-for-creating-and-editing-log-queries-in-azure-log-analytics"></a>Portals voor het maken en bewerken van logboek-query's in Azure Log Analytics

> [!NOTE]
> Dit artikel wordt beschreven portals in Azure-logboekanalyse Hallo nieuwe query language gebruiken.  U kunt meer informatie over de nieuwe taal Hallo en uw werkruimte op Hallo procedure tooupgrade ophalen [Upgrade van uw Azure-logboekanalyse werkruimte toonew logboek zoekopdracht](log-analytics-log-search-upgrade.md).  
>
> Als uw werkruimte niet bijgewerkte toohello nieuwe querytaal is, raadpleegt u te[vinden van gegevens met behulp van logboek zoekopdrachten in logboekanalyse](log-analytics-log-searches.md) voor meer informatie over de huidige versie Hallo van Hallo logboek zoeken portal.

U logboek van zoekopdrachten in een veelheid aan plaatsen in logboekanalyse tooretrieve gegevens vanuit de werkruimte hello gebruiken.  Bovendien tooworking interactief met gegevens echter geretourneerd voor het daadwerkelijk maken en bewerken van query's, hebt u twee opties die hieronder beschreven.  

## <a name="log-search-portal"></a>Logboek zoeken portal
Hallo logboek zoeken portal is toegankelijk vanuit hello Azure-portal of Hallo OMS-portal.  Het is geschikt voor het maken van eenvoudige query's die kunnen worden gemaakt op één regel.  Hallo logboek zoeken portal kan worden gebruikt zonder het starten van een externe portal en kunt u een breed scala aan functies tooperform met logboek zoekopdrachten inclusief maken van regels voor waarschuwingen, computergroepen maken en exporteren van Hallo resultaten van Hallo-query.  

Hallo logboek zoeken portal biedt meerdere functies voor het bewerken van Hallo query zonder een volledige kennis van Hallo querytaal.  U krijgt een overzicht van deze functies in [maken logboek zoekopdrachten in Azure-logboekanalyse met Hallo logboek zoeken portal](log-analytics-log-search-log-search-portal.md).


![Meld u portal zoeken](media/log-analytics-log-search-portals/log-search-portal.png)

## <a name="advanced-analytics-portal"></a>Geavanceerde Analytics-portal
Hallo geavanceerde analyses portal is een speciale portal geavanceerde functionaliteit niet beschikbaar in Hallo logboek zoeken portal.  Functies omvatten Hallo mogelijkheid tooedit een query op meerdere regels, code, afhankelijk van de context Intellisense en slimme Analytics selectief worden uitgevoerd.  Hallo Advanced Analytics-portal is het meest geschikt is voor het ontwerpen van complexe query's die zijn ofwel opgeslagen als een zoekopdracht logboek of gekopieerd en geplakt in andere Log Analytics-elementen.  U start Hallo Advanced Analytics-portal een koppeling in Hallo logboek zoeken portal.

![Geavanceerde Analytics-portal](media/log-analytics-log-search-portals/advanced-analytics-portal.png)


Vanwege de geavanceerde functies zult u meestal Hallo geavanceerde analyses portal gebruiken als uw primaire hulpprogramma voor het maken en bewerken van query's.  Nadat u hebt vastgesteld dat Hallo query werkt zoals verwacht en u zult Kopieer en plak deze ergens anders zoals Hallo logboek zoeken portal of Designer bekijken.  Omdat Hallo Advanced Analytics-portal echter query's met meerdere regels ondersteunt, moet u tootake Hallo volgende letten wanneer u een query van deze portal kopieert.

- Opmerkingen moeten worden verwijderd uit Hallo query voordat deze is gekopieerd en geplakt in een andere locatie.  U kunt een reactie op een regel door het twee slashes (/ /).  Wanneer u een query met meerdere regel in een enkele regel plakt, worden regeleinden verwijderd.  Als u opmerkingen zijn opgenomen, worden de alle tekens na de eerste opmerking Hallo beschouwd als onderdeel van Hallo opmerking.


## <a name="next-steps"></a>Volgende stappen

- Een zelfstudie over het gebruik van Hallo doorlopen [logboek zoeken portal](log-analytics-log-search-log-search-portal.md) of Hallo [Advanced Analytics-portal](https://go.microsoft.com/fwlink/?linkid=856587) toocreate query's.
- Bekijk een [zelfstudie over het schrijven van query's](https://go.microsoft.com/fwlink/?linkid=856078) Hallo nieuwe query language gebruiken.

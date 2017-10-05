---
title: Portals voor het maken en bewerken van logboek-query's in Azure Log Analytics | Microsoft Docs
description: In dit artikel beschrijft de portals die u kunt gebruiken in Azure-logboekanalyse maken en bewerken Meld zoekopdrachten.
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
ms.openlocfilehash: 29dfa31d38f85574f84ed351bc5c26224b1a7e16
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="portals-for-creating-and-editing-log-queries-in-azure-log-analytics"></a>Portals voor het maken en bewerken van logboek-query's in Azure Log Analytics

> [!NOTE]
> Dit artikel wordt beschreven portals in Azure-logboekanalyse met de nieuwe querytaal.  U kunt meer informatie over de nieuwe taal en ophalen van de procedure voor het bijwerken van de werkruimte op [Upgrade van uw Azure-logboekanalyse-werkruimte naar nieuwe logboek zoekopdracht](log-analytics-log-search-upgrade.md).  
>
> Als uw werkruimte is niet naar de nieuwe query language bijgewerkt, moet u verwijzen naar [vinden van gegevens met behulp van logboek zoekopdrachten in logboekanalyse](log-analytics-log-searches.md) voor meer informatie over de huidige versie van de portal logboek zoeken.

Logboek van zoekopdrachten in een veelheid aan plaatsen in Log Analytics kunt u gegevens ophalen uit de werkruimte.  Voor het daadwerkelijk maken en bewerken van query's werkt interactief met de geretourneerde gegevens niet alleen maar, hebt u twee opties die hieronder worden beschreven.  

## <a name="log-search-portal"></a>Logboek zoeken portal
De portal zoeken logboek is toegankelijk vanuit de Azure-portal of de OMS-portal.  Het is geschikt voor het maken van eenvoudige query's die kunnen worden gemaakt op één regel.  De portal logboek zoeken kan worden gebruikt zonder het starten van een externe portal en kunt u het uitvoeren van een breed scala aan functies met logboek zoekopdrachten inclusief maken van regels voor waarschuwingen, computergroepen maken en exporteren van de resultaten van de query.  

De portal logboek Search biedt meerdere functies voor het bewerken van de query zonder een volledige kennis van de querytaal.  U krijgt een overzicht van deze functies in [maken logboek zoekopdrachten in Azure-logboekanalyse via de portal zoeken logboek](log-analytics-log-search-log-search-portal.md).


![Meld u portal zoeken](media/log-analytics-log-search-portals/log-search-portal.png)

## <a name="advanced-analytics-portal"></a>Geavanceerde Analytics-portal
De geavanceerde analyses portal is een speciale portal geavanceerde functionaliteit niet beschikbaar in de portal logboek zoeken.  Het onderdeel biedt de mogelijkheid om te bewerken van een query op meerdere regels, voert u selectief code, afhankelijk van de context Intellisense en slimme Analytics.  De portal Advanced Analytics is het meest geschikt is voor het ontwerpen van complexe query's die zijn ofwel opgeslagen als een zoekopdracht logboek of gekopieerd en geplakt in andere Log Analytics-elementen.  U start de Advanced Analytics-portal via een koppeling in de portal logboek zoeken.

![Geavanceerde Analytics-portal](media/log-analytics-log-search-portals/advanced-analytics-portal.png)


Vanwege de geavanceerde functies, meestal gebruikt u de portal geavanceerde analyses als uw primaire hulpprogramma voor het maken en bewerken van query's.  Eenmaal hebt u vastgesteld dat de query werkt zoals verwacht en u zult Kopieer en plak deze ergens anders zoals de zoekfunctie portal of Designer bekijken.  Omdat de portal Advanced Analytics echter query's met meerdere regels ondersteunt, moet u het volgende in aanmerking nemen bij het kopiëren van een query in deze portal.

- Opmerkingen moeten worden verwijderd uit de query voordat deze is gekopieerd en geplakt in een andere locatie.  U kunt een reactie op een regel door het twee slashes (/ /).  Wanneer u een query met meerdere regel in een enkele regel plakt, worden regeleinden verwijderd.  Als u opmerkingen zijn opgenomen, hebben alle tekens na de eerste opmerking worden beschouwd als onderdeel van de opmerking.


## <a name="next-steps"></a>Volgende stappen

- Helpt u bij een zelfstudie over het gebruik van de [logboek zoeken portal](log-analytics-log-search-log-search-portal.md) of de [Advanced Analytics-portal](https://go.microsoft.com/fwlink/?linkid=856587) query's maken.
- Bekijk een [zelfstudie over het schrijven van query's](https://go.microsoft.com/fwlink/?linkid=856078) met de nieuwe querytaal.

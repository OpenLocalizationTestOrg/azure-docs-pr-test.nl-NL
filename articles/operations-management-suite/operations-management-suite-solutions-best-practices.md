---
title: aanbevolen procedures voor aaaOMSManagement oplossing | Microsoft Docs
description: 
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 08cf1c101e301d24fb5c2bf4bc02a978e508a198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-management-solutions-in-operations-management-suite-oms-preview"></a>Aanbevolen procedures voor het maken van oplossingen voor het beheer in Operations Management Suite (OMS) (Preview)
> [!NOTE]
> Dit is voorlopige documentatie voor het maken van oplossingen voor het beheer in OMS die zich momenteel in preview. De hieronder beschreven schema is onderwerp toochange.  

Dit artikel vindt u aanbevolen procedures voor [maken van een bestand van de oplossing management](operations-management-suite-solutions-solution-file.md) in Operations Management Suite (OMS).  Deze informatie wordt bijgewerkt extra aanbevelingen zijn aangeduid.

## <a name="data-sources"></a>Gegevensbronnen
- Gegevensbronnen kunnen worden [geconfigureerd met een Resource Manager-sjabloon](../log-analytics/log-analytics-template-workspace-configuration.md), maar ze moeten niet worden opgenomen in een oplossingsbestand.  Hallo reden is dat gegevensbronnen configureren momenteel niet idempotent is, wat betekent dat uw oplossing bestaande configuratie in de werkruimte Hallo van de gebruiker kan overschreven.<br><br>Uw oplossing moet mogelijk waarschuwings- en gebeurtenissen van het logboek voor toepassingsgebeurtenissen Hallo.  Als u dit als een gegevensbron in uw oplossing opgeeft, kunnen gegevens gebeurtenissen verwijderen als Hallo gebruiker dit niet is geconfigureerd in de werkruimte heeft.  Als u alle gebeurtenissen worden opgenomen, vervolgens u mogelijk worden overmatige gegevens en gebeurtenissen verzamelen in de werkruimte Hallo van de gebruiker.

- Als uw oplossing vereist dat gegevens uit een van de standaard gegevensbronnen hello, moet vervolgens u definiëren dit als een vereiste.  Status in de documentatie die klant Hallo moet configureren Hallo-gegevensbron op hun eigen.  
- Voeg een [stromen gegevensverificatie](../log-analytics/log-analytics-view-designer-tiles.md) bericht tooany-weergaven in uw oplossing tooinstruct Hallo gebruiker op gegevensbronnen die toobe nodig is geconfigureerd voor de vereiste gegevens toobe verzameld.  Dit bericht wordt weergegeven op de tegel Hallo van Hallo-weergave als vereiste gegevens niet worden gevonden.


## <a name="runbooks"></a>Runbooks
- Voeg een [Automation planning](../automation/automation-schedules.md) voor elk runbook in uw oplossing die toorun volgens een schema behoeften.
- Hallo omvatten [IngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) in uw oplossing toobe gebruikt door runbooks schrijven data toohello Log Analytics-opslagplaats.  Hallo-oplossing te configureren[verwijzing](operations-management-suite-solutions-solution-file.md#solution-resource) deze bron zodanig dat deze blijft als Hallo oplossing wordt verwijderd.  Hierdoor kunnen meerdere oplossingen tooshare Hallo-module.
- Gebruik [Automation-variabelen](../automation/automation-schedules.md) tooprovide toohello oplossing dat gebruikers toochange later willen wellicht waarden.  Zelfs als de oplossing Hallo geconfigureerde toocontain Hallo variabele is, kan de waarde nog worden gewijzigd.

## <a name="views"></a>Weergaven
- Alle oplossingen moeten één weergave die wordt weergegeven in Hallo gebruikersportal bevatten.  Hallo weergave kan bevatten meerdere [visualisatie delen](../log-analytics/log-analytics-view-designer-parts.md) tooillustrate verschillende sets gegevens.
- Voeg een [stromen gegevensverificatie](../log-analytics/log-analytics-view-designer-tiles.md) bericht tooany-weergaven in uw oplossing tooinstruct Hallo gebruiker op gegevensbronnen die toobe nodig is geconfigureerd voor de vereiste gegevens toobe verzameld.
- Hallo-oplossing te configureren[bevatten](operations-management-suite-solutions-solution-file.md#solution-resource) Hallo weergave zodat deze wordt verwijderd als Hallo oplossing wordt verwijderd.

## <a name="alerts"></a>Waarschuwingen
- Definiëren als een parameter in het oplossingsbestand Hallo Hallo Ontvangerslijst zodat Hallo-gebruiker ze definiëren kunt wanneer ze Hallo-oplossing installeren.
- Hallo-oplossing te configureren[verwijzing](operations-management-suite-solutions-solution-file.md#solution-resource) waarschuwing regels zodat van die gebruiker hun configuratie kunt wijzigen.  Ze wil toomake wijzigingen zoals het wijzigen van de adreslijst Hallo, Hallo drempelwaarde van waarschuwing Hallo wijzigen of uitschakelen van de waarschuwingsregel Hallo. 


## <a name="next-steps"></a>Volgende stappen
* Hallo basisproces van doorlopen [ontwerpen en bouwen van een beheeroplossing](operations-management-suite-solutions-creating.md).
* Meer informatie over hoe te[maken van een oplossingsbestand](operations-management-suite-solutions-solution-file.md).
* [Opgeslagen zoekopdrachten en waarschuwingen toevoegen](operations-management-suite-solutions-resources-searches-alerts.md) tooyour-beheeroplossing.
* [Weergaven toevoegen](operations-management-suite-solutions-resources-views.md) tooyour-beheeroplossing.
* [Automation-runbooks en andere resources toevoegen](operations-management-suite-solutions-resources-automation.md) tooyour-beheeroplossing.


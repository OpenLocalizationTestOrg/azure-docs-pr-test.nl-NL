---
title: "Azure Automation Runbook actie aaaUser geïnitieerde in Log Analytics | Microsoft Docs"
description: Dit artikel wordt beschreven hoe een Automation-runbook uit een Log Analytics toorun resultaat op aanvraag zoeken.
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 53c25431572babd5fd54bf964e4683077e2a4c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="take-action-with-an-automation-runbook-from-a-log-analytics-log-search-result"></a>Onderneem actie met een Automation-Runbook uit een zoekresultaat Log Analytics-logboek

In een logboek zoekresultaat in Azure Log Analytics, kunt u nu selecteren **maatregelen** toorun een Automation-runbook.  Hallo runbook kan worden gebruikt tooremediate Hallo probleem of enige andere actie uitvoert bijvoorbeeld verzamelen informatie over probleemoplossing, e-mailbericht verzenden of een serviceaanvraag maken. 

## <a name="components-and-features-used"></a>Gebruikte onderdelen en functies
* [Azure Automation-account](../automation/automation-offering-get-started.md)
* [Log Analytics-werkruimte](../log-analytics/log-analytics-overview.md)

## <a name="tooinitiate-runbook-from-log-search"></a>runbook tooinitiate van logboek zoeken

tootake actie van een gebeurtenis en een runbook in de zoekresultaten logboek initialiseren, u begint met het maken van een zoekopdracht logboek en uit Hallo resultaten u een runbook op aanvraag kunt aanroepen.  Dit kan worden bereikt vanaf Hallo logboek zoekfunctie in hello Azure of [OMS-portal](../log-analytics/log-analytics-log-searches.md).  In dit voorbeeld wordt een zoekopdracht logboek van hello Azure portal een eenvoudige demonstratie van deze functie uitvoeren.

1. Klik in hello Azure-portal, Hallo Hub-menu op **meer services** en selecteer **logboekanalyse**.  
2. Selecteer de werkruimte voor logboekanalyse op Hallo logboekanalyse blade en selecteer op Hallo werkruimte blade **logboek zoeken**.  
3. Op Hallo logboek Search-blade, voert u een zoekopdracht logboek.  
4. Van Hallo logboek zoekresultaten wilt weergeven, klikt u op Hallo ellips toohello links van één van Hallo velden en van select Hallo pop-up **maatregelen nemen op**.<br><br> ![Selecteer actie ondernemen in zoekresultaten](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png) 
5. Selecteer Hallo nemen actie Blade **uitvoeren van een runbook**, en op Hallo **uitvoeren van een runbook** blade kunt u een runbook toorun selecteren.  U kunt een willekeurig runbook selecteren in Hallo Automation-account in de werkruimte voor logboekanalyse gekoppelde toohello is.  Let op Hallo volgende:

    * Runbooks zijn ingedeeld in labels
    * Runbook invoerparameter waarden kunnen rechtstreeks vanuit Hallo velden van Hallo zoekresultaat worden geselecteerd.  Een vervolgkeuzelijst wordt weergegeven om alle beschikbare Hallo-velden uit Hallo resultaat tooselect van weer te geven.  
    * U kunt toorun hello runbook op een [hybride runbook worker](../automation/automation-hybrid-runbook-worker.md) dat u hebt geïnstalleerd op Hallo-machine waarop Hallo probleem is, hebt u een bijbehorende Hybrid Runbook Worker-groep die alleen deze computer als een lid bevat.  Als het Hallo-naam van de Hybrid Worker-groep Hallo overeenkomt met de naam van de Hallo van Hallo-computer die zich in een zoekresultaat Hallo-logboek, wordt automatisch Hallo groep geselecteerd.    

6. Nadat u op **uitvoeren**, Hallo runbook taakblade wordt geopend tooallow u tooreview Hallo status van Hallo-taak.   

Als u een runbook dat geconfigureerd toobe is selecteert [aangeroepen vanuit een waarschuwing voor logboekanalyse](../automation/automation-invoke-runbook-from-omsla-alert.md), heeft een invoerparameter aangeroepen **WebhookData** die **Object** type.  Als invoerparameter Hallo verplicht is, moet u toopass Hallo zoeken resultaten toohello runbook zodat het Hallo JSON-indeling van tekenreeks kunt converteren naar een objecttype zodat u toofilter op specifieke items waarnaar u in de runbook-activiteiten verwijst.  U dit doen door het selecteren van **zoekresultaat (Object)** uit de vervolgkeuzelijst Hallo.<br><br> ![Webhook-gegevensobject voor runbook-parameter selecteren](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)   
    
## <a name="next-steps"></a>Volgende stappen

* Bekijk Hallo [logboekanalyse Meld zoeken verwijzing](log-analytics-search-reference.md) tooview alle Hallo velden en beschikbaar zijn in logboekanalyse facetten zoeken.
* hoe een Automation-runbook tooinvoke automatisch, bekijk toolearn [een Azure Automation-runbook aanroept vanuit een waarschuwing OMS Log Analytics](../automation/automation-invoke-runbook-from-omsla-alert.md).  

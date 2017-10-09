---
title: een Azure Automation-Runbook uit een Log Analytics waarschuwing aaaCalling | Microsoft Docs
description: In dit artikel biedt een overzicht van hoe tooinvoke een Automation-runbook uit een Microsoft OMS Log Analytics-waarschuwing.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/31/2017
ms.author: magoedte
ms.openlocfilehash: 8b745d6e6c2b0294d676e010f52855cd51741cf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="calling-an-azure-automation-runbook-from-an-oms-log-analytics-alert"></a>Een Azure Automation-runbook aanroepen vanuit een Log Analytics-waarschuwing

Wanneer een waarschuwing is geconfigureerd in logboekanalyse toocreate mislukt record voor een waarschuwing als resultaten overeenkomt met een bepaald criterium, zoals een langdurige piek in de processorgebruik of een bepaalde toepassing proces kritieke toohello functionaliteit van een zakelijke toepassing en een overeenkomende gebeurtenis in het gebeurtenislogboek van Windows hello, schrijft deze waarschuwing kan automatisch een Automation-runbook wordt uitgevoerd in een poging tooauto-Hallo-probleem opgelost.  

Er zijn twee opties toocall een runbook bij het Hallo-waarschuwing configureren.  Met name:

1. Een webhook gebruiken.
   * Dit is Hallo enige beschikbare optie als de OMS-werkruimte geen gekoppelde tooan Automation-account is.
   * Als u al een Automation-account gekoppeld tooan OMS-werkruimte, wordt deze optie nog steeds beschikbaar is.  

2. Een runbook direct selecteren.
   * Deze optie is alleen beschikbaar als Hallo OMS-werkruimte gekoppelde tooan Automation-account.  

## <a name="calling-a-runbook-using-a-webhook"></a>Een runbook aanroepen met behulp van een webhook

Een webhook kunt u een bepaald runbook toostart in Azure Automation via één HTTP-aanvraag.  Voordat u configureert Hallo [logboekanalyse waarschuwing](../log-analytics/log-analytics-alerts.md#alert-rules) toocall hello runbook met behulp van een webhook als een waarschuwing actie moet u toofirst maken van een webhook voor Hallo runbook dat moet worden aangeroepen met deze methode.  Lees en volg de stappen in Hallo Hallo [maken van een webhook](automation-webhooks.md#creating-a-webhook) artikel en onthouden toorecord hello webhook-URL, zodat u ernaar verwijzen kunt tijdens het configureren van de waarschuwingsregel Hallo.   

## <a name="calling-a-runbook-directly"></a>Een runbook direct aanroepen

Als er Hallo Automation & besturingselement aanbieding geïnstalleerd en geconfigureerd in de OMS-werkruimte bij het configureren van Hallo runbookoptie acties voor Hallo waarschuwing, kunt u alle runbooks van Hallo bekijken **selecteert u een runbook** vervolgkeuzelijst en selecteer Hallo specifiek runbook gewenste toorun in antwoord toohello waarschuwing.  Hallo geselecteerd runbook kan worden uitgevoerd in een werkruimte hello Azure-cloud op of in een hybride runbook worker.  Wanneer Hallo waarschuwing is gemaakt met behulp van de runbookoptie hello, wordt een webhook gemaakt voor runbook Hallo.  U kunt Hallo webhook zien als u toohello Automation-account gaat en navigeer toohello webhook blade van Hallo geselecteerde runbook.  Als u de waarschuwing Hallo verwijdert, Hallo webhook wordt niet verwijderd, maar Hallo-gebruiker kunt Hallo webhook handmatig verwijderen.  Er is geen probleem als Hallo webhook niet worden verwijderd, is alleen een zwevende item die uiteindelijk toobe moet verwijderd in volgorde toomaintain een geordende Automation-account.  

## <a name="characteristics-of-a-runbook-for-both-options"></a>Kenmerken van een runbook (voor beide opties)

Beide methoden voor het aanroepen van Hallo runbook vanuit Hallo logboekanalyse waarschuwing hebben verschillende gedragskenmerken waarvoor toobe begrijpt voordat u uw regels voor waarschuwingen configureren.  

* U moet een runbook-invoerparameter hebben met de naam **WebhookData** en van het type **Object**.  Deze kan verplicht of optioneel zijn.  Hallo-waarschuwing wordt doorgegeven Hallo zoeken resultaten toohello runbook met behulp van deze invoerparameter.

        param  
         (  
          [Parameter (Mandatory=$true)]  
          [object] $WebhookData  
         )

*  U moet de code tooconvert hello WebhookData tooa PowerShell-object hebben.

    `$SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value`

    *$SearchResults* is een matrix met objecten; elk object Hallo velden met waarden van een zoekresultaat bevat

### <a name="webhookdata-inconsistencies-between-hello-webhook-option-and-runbook-option"></a>WebhookData inconsistenties tussen Hallo webhook optie en runbookoptie

* Bij het configureren van een waarschuwing toocall een Webhook invoeren van een webhook-URL die u voor een runbook hebt gemaakt en klikt u op Hallo **Test Webhook** knop.  Hallo resulterende WebhookData verzonden toohello runbook bevat geen ofwel *. SearchResult* of *. Zoekresultaten*.

*  Als u deze waarschuwing opslaat wanneer Hallo waarschuwing wordt geactiveerd en Hallo webhook aanroepen, Hallo WebhookData toohello runbook verzonden bevat *. SearchResult*.
* Als u een waarschuwing genereren en toocall een runbook (die u maakt ook een webhook) configureert, waarschuwing triggers WebhookData toohello runbook met worden verzonden wanneer Hallo *. Zoekresultaten*.

Dus in Hallo-codevoorbeeld hierboven, moet u tooget *. SearchResult* als Hallo waarschuwing een webhook aanroepen en tooget moet *. Zoekresultaten* als Hallo waarschuwing een runbook rechtstreeks aanroept.

## <a name="example-walkthrough"></a>Voorbeeldscenario

Wordt gedemonstreerd hoe dit werkt met behulp van Hallo na voorbeeld grafisch runbook, een Windows-service te starten.<br><br> ![Grafisch runbook dat Windows-service start](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice.png)<br>

Hallo runbook heeft één invoerparameter van het type **Object** die wordt aangeroepen **WebhookData** en bevat Hallo webhook gegevens van de waarschuwing die Hallo doorgegeven *. Zoekresultaten*.<br><br> ![Invoerparameters voor runbook](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice-inputparameter.png)<br>

In dit voorbeeld in logboekanalyse er gemaakt met twee aangepaste velden, *SvcDisplayName_CF* en *SvcState_CF*, tooextract Hallo service naam en het Hallo weergavestatus van Hallo-service (dat wil zeggen uitgevoerd of gestopt) geschreven logboek met systeemgebeurtenissen toohello van Hallo-gebeurtenis.  Vervolgens maken we een waarschuwingsregel Hello zoekopdracht te volgen: `Type=Event SvcDisplayName_CF="Print Spooler" SvcState_CF="stopped"` zodat we kan waarnemen Hallo afdrukspoolerservice op Hallo Windows-systeem wordt gestopt.  Alle services die van belang kan zijn, maar in dit voorbeeld verwijzen we een van de bestaande Hallo-services die opgenomen in het Windows-besturingssysteem Hallo zijn.  Hallo meldingsactie is geconfigureerde tooexecute ons runbook in dit voorbeeld gebruikt en uitgevoerd op Hallo Hybrid Runbook Worker die zijn ingeschakeld op Hallo doelsystemen.   

Hallo code runbookactiviteit **servicenaam ophalen van LA** wordt Hallo JSON-indeling van tekenreeks geconverteerd naar een type en object-filter op Hallo item *SvcDisplayName_CF* tooextract Hallo weergavenaam Hallo Windows-service en dit doorgeven naar de volgende Hallo-activiteit die wordt geverifieerd Hallo-service wordt gestopt voordat u probeert toorestart deze.  *SvcDisplayName_CF* is een [aangepast veld](../log-analytics/log-analytics-custom-fields.md) gemaakt in logboekanalyse toodemonstrate in dit voorbeeld.

    $SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value
    $SearchResults.SvcDisplayName_CF  

Wanneer het Hallo-service stopt, Hallo waarschuwingsregel in logboekanalyse detecteert een overeenkomst en om Hallo runbook te activeren en Hallo waarschuwingscontext toohello runbook verzenden. Hallo runbook zal actie ondernemen tooverify Hallo-service wordt gestopt, en als zodanig poging toorestart Hallo service en controleer of deze juist gestart en uitvoer Hallo resultaten.     

U kunt ook als u uw Automation-account gekoppeld tooyour OMS-werkruimte niet hebt, u Hallo waarschuwingsregel configureren met een webhook actie tootrigger hello runbook en Hallo runbook tooconvert Hallo JSON-indeling tekenreeks en filter op configureren*. SearchResult* eerder genoemde Hallo-richtlijnen te volgen.    

## <a name="next-steps"></a>Volgende stappen

* meer informatie over waarschuwingen in logboekanalyse toolearn en hoe toocreate, Zie [waarschuwingen in logboekanalyse](../log-analytics/log-analytics-alerts.md).

* hoe tootrigger runbooks met behulp van een webhook zien toounderstand [Azure Automation webhooks](automation-webhooks.md).

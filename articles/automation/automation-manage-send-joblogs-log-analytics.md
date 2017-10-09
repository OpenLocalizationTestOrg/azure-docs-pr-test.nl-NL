---
title: aaaForward Azure Automation-taak gegevens tooOMS Log Analytics | Microsoft Docs
description: In dit artikel laat zien hoe toosend taak status en runbook-taak streams tooMicrosoft Operations Management Suite Log Analytics toodeliver meer inzicht en beheer.
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: c12724c6-01a9-4b55-80ae-d8b7b99bd436
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/2017
ms.author: magoedte
ms.openlocfilehash: e78b6c6677d6502711ce828e2d32b7a91922ae26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-toolog-analytics-oms"></a>Taakstatus en taak streams doorsturen van Automation tooLog logboekanalyse (OMS)
Automatisering kan de runbook-taak status en taak streams tooyour Microsoft Operations Management Suite (OMS) werkruimte voor logboekanalyse verzenden.  Taak registreert en taak streams zichtbaar zijn in hello Azure-portal of PowerShell voor afzonderlijke taken en deze kunnen u eenvoudige onderzoeken tooperform. Met Log Analytics kunt u nu:

* Inzicht verkrijgen in uw Automation-taken
* Trigger een e-mailadres of de waarschuwing op basis van de status van de taak runbook (bijvoorbeeld is mislukt of onderbroken)
* Geavanceerde query's in uw taak stromen schrijven
* Taken correleren via Automation-accounts
* De taakgeschiedenis visualiseren gedurende een periode     

## <a name="prerequisites-and-deployment-considerations"></a>Vereisten en overwegingen voor de implementatie
verzenden van uw Automation toostart tooLog Analytics registreert, moet u:

1. Hallo November 2016 of later release van [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).
2. Een werkruimte voor logboekanalyse. Zie voor meer informatie [aan de slag met logboekanalyse](../log-analytics/log-analytics-get-started.md). 
3. Hallo ResourceId voor uw Azure Automation-account

toofind hello ResourceId voor uw Azure Automation-account en de werkruimte voor logboekanalyse Hallo PowerShell volgende uitvoeren:

```powershell
# Find hello ResourceId for hello Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find hello ResourceId for hello Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

Als er meerdere Automation-accounts of werkruimten, in de uitvoer Hallo Hallo voorafgaand aan de opdrachten, Hallo vinden *naam* u tooconfigure nodig hebt en kopieer Hallo-waarde voor *ResourceId*.

Als u nodig hebt toofind hello *naam* van uw Automation-account hello Azure-portal Selecteer in uw Automation-account van Hallo **Automation-account** blade en selecteer **alle instellingen**.  Van Hallo **alle instellingen** blade onder **Accountinstellingen** Selecteer **eigenschappen**.  In Hallo **eigenschappen** blade kunt u deze waarden noteren.<br> ![Eigenschappen van Automation-Account](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).

## <a name="set-up-integration-with-log-analytics"></a>Integratie met logboekanalyse instellen
1. Start op uw computer **Windows PowerShell** van Hallo **Start** scherm.  
2. Kopiëren en plakken Hallo PowerShell te volgen en Hallo-waarde voor Hallo bewerken `$workspaceId` en `$automationAccountId`.  Voor Hallo `-Environment` parameter, geldige waarden zijn *AzureCloud* of *AzureUSGovernment* , afhankelijk van de cloudomgeving Hallo u werkt.     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }

# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

Na dit script uitvoert, ziet u records in logboekanalyse binnen 10 minuten van nieuwe JobLogs of JobStreams wordt geschreven.

toosee hello Logboeken, Hallo logboekanalyse logboek zoekquery volgende uitvoeren:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="verify-configuration"></a>Configuratie controleren
tooconfirm dat uw Automation-account verzendt werkruimte voor logboekanalyse tooyour registreert, moet u controleren of diagnostische gegevens correct zijn ingesteld op Hallo Automation-account met behulp van de volgende PowerShell Hallo:

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }
# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

Zorg ervoor dat in Hallo uitvoer:
+ Onder *logboeken*, Hallo waarde voor *ingeschakeld* is *True*
+ waarde van Hallo *WorkspaceId* toohello ResourceId van de werkruimte voor logboekanalyse is ingesteld


## <a name="log-analytics-records"></a>Log Analytics-records
Diagnostische gegevens van Azure Automation maakt u twee soorten records in Log Analytics en zijn gelabeld als **Type = AzureDiagnostics**.

### <a name="job-logs"></a>Taaklogboeken
| Eigenschap | Beschrijving |
| --- | --- |
| TimeGenerated |Datum en tijd wanneer de runbooktaak Hallo uitgevoerd. |
| RunbookName_s |Hallo-naam van Hallo runbook. |
| Caller_s |Wie Hallo opnieuw gestart.  Mogelijke waarden zijn een e-mailadres of het systeem voor geplande taken. |
| Tenant_g | GUID die Hallo tenant voor Hallo aanroeper identificeert. |
| JobId_g |De GUID die Hallo-Id van de runbooktaak Hallo. |
| ResultType |Hallo-status van de runbooktaak Hallo.  Mogelijke waarden zijn:<br>- Gestart<br>- Gestopt<br>- Onderbroken<br>- Mislukt<br>-Voltooid |
| Category | Classificatie van Hallo type gegevens.  Hallo-waarde is voor automatisering kunt JobLogs. |
| OperationName | Hiermee geeft u Hallo bewerking uitgevoerd in Azure.  Hallo-waarde is voor automatisering kunt taak. |
| Resource | Naam van Hallo Automation-account |
| SourceSystem | Hoe logboekanalyse Hallo gegevens verzameld. Altijd *Azure* voor Azure diagnostics. |
| ResultDescription |Hierin wordt beschreven Hallo runbook taakstatus resultaat.  Mogelijke waarden zijn:<br>- Taak is gestart<br>- Taak is mislukt<br>- Taak is voltooid |
| CorrelationId |De GUID die Hallo correlatie-Id van de runbooktaak Hallo. |
| ResourceId |Hiermee geeft u een Azure Automation-account resource-id van runbook Hallo Hallo. |
| SubscriptionId | Hallo Azure-abonnement-Id (GUID) voor Hallo Automation-account. |
| ResourceGroup | De naam van de resourcegroep Hallo voor Hallo Automation-account. |
| ResourceProvider | MICROSOFT CORPORATION. AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |


### <a name="job-streams"></a>Taak stromen
| Eigenschap | Beschrijving |
| --- | --- |
| TimeGenerated |Datum en tijd wanneer de runbooktaak Hallo uitgevoerd. |
| RunbookName_s |Hallo-naam van Hallo runbook. |
| Caller_s |Wie Hallo opnieuw gestart.  Mogelijke waarden zijn een e-mailadres of het systeem voor geplande taken. |
| StreamType_s |Hallo-type van de taakstroom. Mogelijke waarden zijn:<br>- Voortgang<br>- Uitvoer<br>- Waarschuwing<br>- Fout<br>- Foutopsporing<br>- Uitgebreid |
| Tenant_g | GUID die Hallo tenant voor Hallo aanroeper identificeert. |
| JobId_g |De GUID die Hallo-Id van de runbooktaak Hallo. |
| ResultType |Hallo-status van de runbooktaak Hallo.  Mogelijke waarden zijn:<br>-In voortgang |
| Category | Classificatie van Hallo type gegevens.  Hallo-waarde is voor automatisering kunt JobStreams. |
| OperationName | Hiermee geeft u Hallo bewerking uitgevoerd in Azure.  Hallo-waarde is voor automatisering kunt taak. |
| Resource | Naam van Hallo Automation-account |
| SourceSystem | Hoe logboekanalyse Hallo gegevens verzameld. Altijd *Azure* voor Azure diagnostics. |
| ResultDescription |Bevat de uitvoerstroom Hallo van Hallo runbook. |
| CorrelationId |De GUID die Hallo correlatie-Id van de runbooktaak Hallo. |
| ResourceId |Hiermee geeft u een Azure Automation-account resource-id van runbook Hallo Hallo. |
| SubscriptionId | Hallo Azure-abonnement-Id (GUID) voor Hallo Automation-account. |
| ResourceGroup | De naam van de resourcegroep Hallo voor Hallo Automation-account. |
| ResourceProvider | MICROSOFT CORPORATION. AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |

## <a name="viewing-automation-logs-in-log-analytics"></a>Log Analytics Automation weer aanmeldt
Nu dat u hebt gestart met het verzenden van uw Automation-taak logboeken tooLog Analytics, laten we zien wat u kunt doen met deze logboeken in Log Analytics.

toosee hello Logboeken, Hallo volgende query worden uitgevoerd:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a>Een e-mailbericht verzenden wanneer een runbooktaak is mislukt of wordt onderbroken
Een van onze belangrijkste klant wordt gevraagd voor Hallo mogelijkheid toosend een e-mailbericht of een tekstvak wanneer er iets mis met een runbooktaak gaat.   

een waarschuwing toocreate regel u begint met het maken van een zoekopdracht logboek voor Hallo runbook Taakrecords die Hallo waarschuwing moeten worden aangeroepen.  Klik op Hallo **waarschuwing** toocreate knop en de waarschuwingsregel Hallo configureren.

1. Klik op de pagina overzicht van Log Analytics Hallo **logboek zoeken**.
2. Maken van een zoekquery logboek voor de waarschuwing door te zoeken naar Hallo queryveld volgende Hallo typen: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)` u kunt ook groeperen op Hallo RunbookName door gebruik te maken:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`   

   Als u de logboeken van meer dan een Automation-account of abonnement tooyour werkruimte hebt ingesteld, kunt u uw waarschuwingen per abonnement en de Automation-account kunt groeperen.  Automation-accountnaam kan worden afgeleid van Hallo Resource aan in de zoekopdracht Hallo van JobLogs.  
3. Hallo tooopen **waarschuwingsregel toevoegen** scherm, klikt u op **waarschuwing** bovenaan Hallo Hallo pagina. Zie voor meer informatie over Hallo opties tooconfigure Hallo waarschuwing [waarschuwingen in logboekanalyse](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-all-jobs-that-have-completed-with-errors"></a>Alle taken die zijn voltooid met fouten vinden
Bovendien tooalerting op fouten, vindt u wanneer een runbooktaak een fout niet wordt beëindigd heeft. In dergelijke gevallen PowerShell produceert een foutstroom, maar Hallo niet wordt beëindigd fouten niet ervoor zorgen dat uw taak toosuspend of mislukken.    

1. Klik in de werkruimte voor logboekanalyse op **logboek zoeken**.
2. Typ in Hallo queryveld `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` en klik vervolgens op **Search**.

### <a name="view-job-streams-for-a-job"></a>Weergave taak stromen voor een taak
Wanneer u een taak foutopsporing, kunt u ook toolook in Hallo taak stromen.  Hallo geeft volgende query alle Hallo stromen voor een enkele taak met GUID 2ebd22ea-e05e-4eb9 - 9d 76-d73cbd4356e0:   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a>Status van de historische taak weergeven
Ten slotte kunt u toovisualize uw Taakgeschiedenis gedurende een bepaalde periode.  U kunt deze query toosearch gebruiken voor Hallo status van uw taken gedurende een bepaalde periode.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> ![OMS historische taak Statusgrafiek](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)<br>

## <a name="summary"></a>Samenvatting
Door het verzenden van uw Automation-taak status en stroom gegevens tooLog Analytics, kunt u meer inzicht in de status van uw Automation-taken op Hallo ophalen:
+ Instellen van waarschuwingen toonotify u wanneer er een probleem
+ Met behulp van aangepaste weergaven en zoeken query's toovisualize gerelateerde uw runbookresultaten, de status van de runbook-taak en andere indicatoren of metrische gegevens.  

Log Analytics biedt meer operationeel inzicht tooyour Automation taken en adres incidenten sneller kan helpen.  

## <a name="next-steps"></a>Volgende stappen
* Zie toolearn meer informatie over hoe tooconstruct verschillende zoekquery's en bekijk Hallo Automation logboeken met Log Analytics taak [zoekopdrachten aanmelden met Log Analytics](../log-analytics/log-analytics-log-searches.md)
* hoe toocreate en ophalen uitvoer en foutberichten van runbooks, Zie toounderstand [Runbook uitvoer en berichten](automation-runbook-output-and-messages.md)
* meer over de uitvoering van runbook, hoe toomonitor runbooktaken en andere technische details, Zie toolearn [een runbooktaak bijhouden](automation-runbook-execution.md)
* toolearn meer informatie over OMS Log Analytics en verzameling gegevensbronnen, Zie [verzamelen van Azure storage-gegevens in het overzicht van de Log Analytics](../log-analytics/log-analytics-azure-storage.md)

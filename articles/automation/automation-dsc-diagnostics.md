---
title: aaaForward Azure Automation DSC reporting gegevens tooOMS Log Analytics | Microsoft Docs
description: Dit artikel wordt gedemonstreerd hoe toosend Desired State Configuration (DSC) reporting gegevens tooMicrosoft Operations Management Suite Log Analytics toodeliver meer inzicht en beheer.
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: eslesar
ms.openlocfilehash: 21f78d5549d53ba3d7e237f55d9086f380cf3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="forward-azure-automation-dsc-reporting-data-toooms-log-analytics"></a>Doorsturen van Azure Automation DSC reporting gegevens tooOMS Log Analytics

Automatisering kan DSC-knooppunt status tooyour Microsoft Operations Management Suite (OMS) Log Analytics gegevenswerkruimte verzenden.  
Status van naleving is zichtbaar in hello Azure-portal of PowerShell voor knooppunten en voor afzonderlijke DSC-resources in het knooppuntconfiguraties. Met Log Analytics kunt u het volgende doen:

* Informatie over de compatibiliteit voor beheerde knooppunten en afzonderlijke bronnen ophalen
* Activeren van een e-mailadres of de waarschuwing op basis van status van naleving
* Geavanceerde query's op uw beheerde knooppunten schrijven
* Status van naleving correleren via Automation-accounts
* De geschiedenis van naleving van knooppunt na verloop van tijd visualiseren

## <a name="prerequisites"></a>Vereisten

toostart verzenden van uw Automation DSC-rapporten tooLog Analytics, moet u:

* Hallo November 2016 of later release van [Azure PowerShell](/powershell/azure/overview) (v2.3.0).
* Een Azure Automation-account. Zie voor meer informatie [aan de slag met Azure Automation](automation-offering-get-started.md)
* Een werkruimte voor logboekanalyse met een **Automation en Control** serviceaanbieding. Zie voor meer informatie [aan de slag met logboekanalyse](../log-analytics/log-analytics-get-started.md).
* Ten minste één Azure Automation DSC-knooppunt. Zie voor meer informatie [machines voorbereiden voor beheer door Azure Automation DSC](automation-dsc-onboarding.md) 

## <a name="set-up-integration-with-log-analytics"></a>Integratie met logboekanalyse instellen

toobegin gegevens importeren uit Azure Automation DSC in Log Analytics, volledige Hallo stappen te volgen:

1. Tooyour aanmelden met Azure-account in PowerShell. Zie [aanmelden met Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/authenticate-azureps?view=azurermps-4.0.0)
1. Hallo ophalen _ResourceId_ van uw automation-account door het uitvoeren van de volgende PowerShell-opdracht Hallo: (als u meer dan een automation-account hebt, kiest u Hallo _ResourceID_ voor gewenste Hallo-account tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Automation Account
  Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"
  ```
1. Hallo ophalen _ResourceId_ van uw werkruimte voor logboekanalyse door het uitvoeren van de volgende PowerShell-opdracht Hallo: (als u meer dan één werkruimte hebt, kiest u Hallo _ResourceID_ voor gewenste Hallo-werkruimte tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Log Analytics workspace
  Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
  ```
1. Voer Hallo PowerShell-opdracht te volgen en vervangt `<AutomationResourceId>` en `<WorkspaceResourceId>` Hello _ResourceId_ waarden van elk van de vorige stappen Hallo:

  ```powershell
  Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $true -Categories "DscNodeStatus"
  ```

Als u importeren van gegevens uit Azure Automation DSC in logboekanalyse toostop wilt, Voer Hallo volgende PowerShell-opdracht.

```powershell
Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $false -Categories "DscNodeStatus"
```

## <a name="view-hello-dsc-logs"></a>Hallo DSC-logboeken bekijken

Na het instellen van integratie met Log Analytics voor uw Automation DSC-gegevens, een **logboek zoeken** knop wordt weergegeven op Hallo **DSC-knooppunten** blade van uw automation-account. Klik op Hallo **logboek zoeken** knop tooview Hallo logboeken voor gegevens van DSC-knooppunt.

![Logboek zoekknop](media/automation-dsc-diagnostics/log-search-button.png)

Hallo **logboek zoeken** blade wordt geopend en ziet u een **DscNodeStatusData** bewerking voor elk DSC-knooppunt en een **DscResourceStatusData** bewerking voor elk [DSC resource](https://msdn.microsoft.com/powershell/dsc/resources) in configuratie Hallo-toegepaste toothat knooppunt genoemd.

Hallo **DscResourceStatusData** bewerking bevat informatie over de fout voor eventuele DSC-resources die niet zijn geslaagd.

Klik op elke bewerking in toosee Hallo-Hallo lijstgegevens voor de bewerking.

U kunt ook Hallo logboeken weergeven door [zoeken in logboekanalyse. Zie [vinden van gegevens met behulp van logboek zoekopdrachten](../log-analytics/log-analytics-log-searches.md).
Type Hallo volgende query toofind uw DSC Logboeken:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus"`

U kunt ook Hallo query beperken door Hallo bewerkingsnaam. Bijvoorbeeld: "Type = AzureDiagnostics ResourceProvider ="MICROSOFT Corporation. Categorie AUTOMATION' = 'DscNodeStatus' OperationName = "DscNodeStatusData"

### <a name="send-an-email-when-a-dsc-compliance-check-fails"></a>Een e-mailbericht verzenden als een DSC-controle is mislukt

Een van onze belangrijkste klantaanvragen is voor Hallo mogelijkheid toosend een e-mailbericht of een tekstvak wanneer er iets mis met een DSC-configuratie gaat.   

een waarschuwing toocreate regel u begint met het maken van een zoekopdracht logboek voor Hallo DSC rapport records die Hallo waarschuwing moet worden aangeroepen.  Klik op Hallo **waarschuwing** toocreate knop en de waarschuwingsregel Hallo configureren.

1. Klik op de pagina overzicht van Log Analytics Hallo **logboek zoeken**.
1. Een zoekquery logboek voor de waarschuwing door te zoeken naar Hallo queryveld volgende Hallo typen maken:`Type=AzureDiagnostics Category=DscNodeStatus NodeName_s=DSCTEST1 OperationName=DscNodeStatusData ResultType=Failed`

  Als u de logboeken van meer dan een Automation-account of abonnement tooyour werkruimte hebt ingesteld, kunt u uw waarschuwingen per abonnement en de Automation-account kunt groeperen.  
  Automation-accountnaam kan worden afgeleid van Hallo Resource aan in de zoekopdracht Hallo van DscNodeStatusData.  
1. Hallo tooopen **waarschuwingsregel toevoegen** scherm, klikt u op **waarschuwing** bovenaan Hallo Hallo pagina. Zie voor meer informatie over Hallo opties tooconfigure Hallo waarschuwing [waarschuwingen in logboekanalyse](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-failed-dsc-resources-across-all-nodes"></a>Mislukte DSC-resources te vinden op alle knooppunten

Een voordeel van het gebruik van logboekanalyse is dat u naar mislukte controles op knooppunten zoeken kunt.
toofind alle exemplaren van DSC-resources die niet zijn geslaagd.

1. Klik op de pagina overzicht van Log Analytics Hallo **logboek zoeken**.
1. Een zoekquery logboek voor de waarschuwing door te zoeken naar Hallo queryveld volgende Hallo typen maken:`Type=AzureDiagnostics Category=DscNodeStatus OperationName=DscResourceStatusData ResultType=Failed`

### <a name="view-historical-dsc-node-status"></a>Historische status van DSC-knooppunt weergeven

Ten slotte kunt u toovisualize de geschiedenis van de status van de DSC-knooppunt gedurende een bepaalde periode.  
U kunt deze query toosearch gebruiken voor Hallo status van de status van uw DSC-knooppunt gedurende een bepaalde periode.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=DscNodeStatus NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  

Hiermee wordt een grafiek van Hallo knooppunt status weergegeven gedurende een bepaalde periode.

## <a name="log-analytics-records"></a>Log Analytics-records

Diagnostische gegevens van Azure Automation maakt twee categorieën van records in logboekanalyse.

### <a name="dscnodestatusdata"></a>DscNodeStatusData

| Eigenschap | Beschrijving |
| --- | --- |
| TimeGenerated |Datum en tijd waarop het Hallo-controle is uitgevoerd. |
| OperationName |DscNodeStatusData |
| ResultType |Hallo-knooppunt wordt aangegeven of compatibel. |
| NodeName_s |Hallo-naam van de beheerde Hallo-knooppunt. |
| NodeComplianceStatus_s |Hallo-knooppunt wordt aangegeven of compatibel. |
| DscReportStatus |Hiermee wordt aangegeven of Hallo-controle is geslaagd. |
| ConfigurationMode | Hallo-configuratie is hoe toegepaste toohello knooppunt. Mogelijke waarden zijn __'ApplyOnly'__,__'ApplyandMonitior'__, en __'ApplyandAutoCorrect'__. <ul><li>__ApplyOnly__: DSC Hallo-configuratie is van toepassing en niets meer tenzij u een nieuwe configuratie wordt doorgeschoven, is het doelknooppunt toohello of wanneer een nieuwe configuratie is opgehaald uit een server. Na de eerste toepassing van een nieuwe configuratie controleert het DSC niet voor afwijking van een eerder geconfigureerde status. DSC probeert tooapply Hallo configuratie, totdat hij erin slaagt voordat __ApplyOnly__ wordt van kracht. </li><li> __ApplyAndMonitor__: dit is de standaardwaarde Hallo. Hallo LCM geldt voor alle nieuwe configuraties. Als het doelknooppunt Hallo drifts van Hallo gewenst staat, rapporteert DSC na de eerste toepassing van een nieuwe configuratie Hallo discrepantie in Logboeken. DSC probeert tooapply Hallo configuratie, totdat hij erin slaagt voordat __ApplyAndMonitor__ wordt van kracht.</li><li>__ApplyAndAutoCorrect__: DSC eventuele nieuwe configuraties van toepassing. Na de eerste toepassing van een nieuwe configuratie als Hallo doelknooppunt drifts van Hallo gewenst staat, DSC rapporten Hallo discrepantie in Logboeken en vervolgens wordt de huidige configuratie Hallo opnieuw toegepast.</li></ul> |
| HostName_s | Hallo-naam van de beheerde Hallo-knooppunt. |
| IP-adres | Hallo IPv4-adres van Hallo beheerd knooppunt. |
| Category | DscNodeStatus |
| Resource | Hallo-naam van hello Azure Automation-account. |
| Tenant_g | GUID die Hallo tenant voor Hallo aanroeper identificeert. |
| NodeId_g |GUID die de beheerde knooppunt Hallo identificeert. |
| DscReportId_g |GUID die Hallo rapport identificeert. |
| LastSeenTime_t |Datum en tijd wanneer Hallo rapport voor het laatst is bekeken. |
| ReportStartTime_t |Datum en tijd waarop het Hallo-rapport is gestart. |
| ReportEndTime_t |Datum en tijd wanneer Hallo rapport is voltooid. |
| NumberOfResources_d |Hallo aantal DSC-resources in Hallo toegepast toohello configuratieknooppunt genoemd. |
| SourceSystem | Hoe logboekanalyse Hallo gegevens verzameld. Altijd *Azure* voor Azure diagnostics. |
| ResourceId |Hiermee geeft u hello Azure Automation-account. |
| ResultDescription | Hallo beschrijving voor deze bewerking. |
| SubscriptionId | Hallo Azure-abonnement-Id (GUID) voor Hallo Automation-account. |
| ResourceGroup | De naam van de resourcegroep Hallo voor Hallo Automation-account. |
| ResourceProvider | MICROSOFT CORPORATION. AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |De GUID die Hallo correlatie-Id van het rapport voor naleving van Hallo. |

### <a name="dscresourcestatusdata"></a>DscResourceStatusData

| Eigenschap | Beschrijving |
| --- | --- |
| TimeGenerated |Datum en tijd waarop het Hallo-controle is uitgevoerd. |
| OperationName |DscResourceStatusData|
| ResultType |Hiermee wordt aangegeven of Hallo resource is compatibel. |
| NodeName_s |Hallo-naam van de beheerde Hallo-knooppunt. |
| Category | DscNodeStatus |
| Resource | Hallo-naam van hello Azure Automation-account. |
| Tenant_g | GUID die Hallo tenant voor Hallo aanroeper identificeert. |
| NodeId_g |GUID die de beheerde knooppunt Hallo identificeert. |
| DscReportId_g |GUID die Hallo rapport identificeert. |
| DscResourceId_s |Hallo-naam van exemplaar van Hallo DSC-resource. |
| DscResourceName_s |Hallo-naam van Hallo DSC-resource. |
| DscResourceStatus_s |Hiermee wordt aangegeven of Hallo DSC-resource is compatibel. |
| DscModuleName_s |Hallo-naam van de PowerShell-module voor Hallo Hallo DSC-resource met. |
| DscModuleVersion_s |Hallo-versie van PowerShell-module voor Hallo met Hallo DSC-resource. |
| DscConfigurationName_s |Hallo-naam van Hallo configuratie toegepast toohello knooppunt. |
| ErrorCode_s | Hallo-foutcode als Hallo resource is mislukt. |
| ErrorMessage_s |Hallo-foutbericht als Hallo resource is mislukt. |
| DscResourceDuration_d |Hallo-tijd, in seconden, Hallo DSC-resource hebt uitgevoerd. |
| SourceSystem | Hoe logboekanalyse Hallo gegevens verzameld. Altijd *Azure* voor Azure diagnostics. |
| ResourceId |Hiermee geeft u hello Azure Automation-account. |
| ResultDescription | Hallo beschrijving voor deze bewerking. |
| SubscriptionId | Hallo Azure-abonnement-Id (GUID) voor Hallo Automation-account. |
| ResourceGroup | De naam van de resourcegroep Hallo voor Hallo Automation-account. |
| ResourceProvider | MICROSOFT CORPORATION. AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |De GUID die Hallo correlatie-Id van het rapport voor naleving van Hallo. |

## <a name="summary"></a>Samenvatting

Via het verzenden van uw Automation DSC gegevens tooLog Analytics, u kunt beter inzicht krijgen in Hallo status van uw Automation DSC-knooppunten op basis van:

* Instellen van waarschuwingen toonotify u wanneer er een probleem
* Met behulp van aangepaste weergaven en zoeken query's toovisualize gerelateerde uw runbookresultaten, de status van de runbook-taak en andere indicatoren of metrische gegevens.  

Log Analytics biedt meer inzicht tooyour Automation DSC gegevens en adres incidenten sneller kan helpen.  

## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over hoe tooconstruct verschillende zoekquery's en bekijk Automation DSC Hallo logboeken met Log Analytics toolearn [zoekopdrachten aanmelden met Log Analytics](../log-analytics/log-analytics-log-searches.md)
* Zie toolearn meer over het gebruik van Azure Automation DSC [aan de slag met Azure Automation DSC](automation-dsc-getting-started.md)
* toolearn meer informatie over OMS Log Analytics en verzameling gegevensbronnen, Zie [verzamelen van Azure storage-gegevens in het overzicht van de Log Analytics](../log-analytics/log-analytics-azure-storage.md)


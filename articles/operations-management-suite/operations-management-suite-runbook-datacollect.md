---
title: aaaCollecting Log Analytics-gegevens met een runbook in Azure Automation | Microsoft Docs
description: Stapsgewijze zelfstudie die helpt bij het maken van een runbook in Azure Automation toocollect gegevens in Hallo OMS-opslagplaats voor analyse door logboekanalyse.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a>Gegevens verzamelen in logboekanalyse met een Azure Automation-runbook
U kunt een aanzienlijke hoeveelheid gegevens in logboekanalyse verzamelen uit diverse bronnen, zoals [gegevensbronnen](../log-analytics/log-analytics-data-sources.md) op agents en ook [gegevens verzameld van Azure](../log-analytics/log-analytics-azure-storage.md).  Er zijn een scenario's waarbij u toocollect gegevens nodig hebt die niet worden geopend via deze standaard bronnen.  In dergelijke gevallen kunt u Hallo [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) toowrite gegevens tooLog Analytics vanaf elke client REST-API.  Een algemene methode tooperform deze gegevensverzameling is met behulp van een runbook in Azure Automation.   

Deze zelfstudie wordt begeleid Hallo-proces voor het maken en plannen van een runbook in Azure Automation toowrite gegevens tooLog Analytics.


## <a name="prerequisites"></a>Vereisten
Dit scenario vereist Hallo resources die zijn geconfigureerd in uw Azure-abonnement te volgen.  Beide mag een gratis account.

- [Meld u werkruimte](../log-analytics/log-analytics-get-started.md).
- [Azure automation-account](../automation/automation-offering-get-started.md).

## <a name="overview-of-scenario"></a>Overzicht van scenario
Voor deze zelfstudie schrijft u een runbook dat informatie over het automatiseren van taken verzamelt.  Azure Automation-Runbooks worden geïmplementeerd met PowerShell, zodat u beginnen door te schrijven en testen van een script in hello Azure Automation-editor.  Zodra u hebt gecontroleerd dat u Hallo vereist informatie wilt verzamelen, moet u schrijven die gegevens tooLog Analytics en controleer of aangepaste Hallo-gegevenstype.  Ten slotte gaat u een planning toostart hello runbook maken met regelmatige tussenpozen.

> [!NOTE]
> U kunt Azure Automation toosend taak informatie tooLog Analytics zonder dit runbook configureren.  Dit scenario wordt voornamelijk gebruikt toosupport Hallo zelfstudie en het wordt aanbevolen dat u tooa Hallo-test gegevenswerkruimte verzenden.  


## <a name="1-install-data-collector-api-module"></a>1. Data Collector API-module installeren
Elke [aanvraag van HTTP-Data Collector API Hallo](../log-analytics/log-analytics-data-collector-api.md#create-a-request) moet op de juiste manier zijn geformatteerd en autorisatie-header bevatten.  U kunt dit doen in uw runbook, maar u kunt beperken Hallo code vereist met behulp van een module die vereenvoudigt u dit proces.  Een module die u kunt gebruiken is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in PowerShell Gallery Hallo.

toouse een [module](../automation/automation-integration-modules.md) in een runbook moet worden geïnstalleerd in uw Automation-account.  Elk runbook in hetzelfde account kunt Hallo Hallo functies in Hallo-module.  U kunt een nieuwe module installeren door te selecteren **activa** > **Modules** > **toevoegen van een module** in uw Automation-account.  

Hallo PowerShell Gallery al beschikt u over een snelle optie toodeploy een module direct tooyour automation-account zodat u deze optie kunt gebruiken voor deze zelfstudie.  

![Module OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. Ga te[PowerShell Gallery](https://www.powershellgallery.com/).
2. Zoeken naar **OMSIngestionAPI**.
3. Klik op Hallo **tooAzure Automation implementeren** knop.
4. Selecteer uw automation-account en klik op **OK** tooinstall Hallo-module.


## <a name="2-create-automation-variables"></a>2. Automation-variabelen maken
[Automation-variabelen](..\automation\automation-variables.md) bevatten waarden die kunnen worden gebruikt door alle runbooks in uw Automation-account.  Zij runbooks meer flexibele doordat u toochange deze waarden zonder te bewerken Hallo werkelijke runbook. Elke aanvraag van Hallo HTTP Data Collector API vereist Hallo-ID en sleutel van Hallo OMS-werkruimte en variabele assets zijn ideaal toostore deze informatie.  

![Variabelen](media/operations-management-suite-runbook-datacollect/variables.png)

1. Navigeer in hello Azure-portal, tooyour Automation-account.
2. Selecteer **variabelen** onder **gedeelde Resources**.
2. Klik op **toevoegen van een variabele** en Hallo twee variabelen in de volgende tabel Hallo maken.

| Eigenschap | De waarde van de werkruimte-ID | De sleutelwaarde werkruimte |
|:--|:--|:--|
| Naam | WorkspaceId | WorkspaceKey |
| Type | Tekenreeks | Tekenreeks |
| Waarde | In de werkruimte-ID van de werkruimte voor logboekanalyse hello te plakken. | Plak met Hallo primaire of secundaire sleutel van de werkruimte voor logboekanalyse. |
| Versleuteld | Nee | Ja |



## <a name="3-create-runbook"></a>3. Runbook maken

Azure Automation heeft een editor in Hallo-portal waar u kunt bewerken en test uw runbook.  U hebt Hallo optie toouse Hallo script editor toowork met [PowerShell rechtstreeks](../automation/automation-edit-textual-runbook.md) of [maken van een grafisch runbook](../automation/automation-graphical-authoring-intro.md).  Voor deze zelfstudie werkt u met een PowerShell-script. 

![Runbook bewerken](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. Navigeer tooyour Automation-account.  
2. Klik op **Runbooks** > **een runbook toevoegen** > **een nieuw runbook maken**.
3. Runbooknaam hello, typt u **verzamelen-Automation-taken**.  Selecteer Hallo runbooktype **PowerShell**.
4. Klik op **maken** toocreate hello runbook en start Hallo-editor.
5. Kopieer en plak de volgende code in runbook Hallo Hallo.  Raadpleeg toohello opmerkingen in Hallo script voor een uitleg van Hallo-code.
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a>4. Runbook-test
Azure Automation omvat een omgeving te[test uw runbook](../automation/automation-testing-runbook.md) voordat u deze hebt gepubliceerd.  U kunt Hallo gegevens verzameld door Hallo runbook controleren en nagaan of dat deze tooLog Analytics schrijft zoals verwacht voordat het wordt gepubliceerd tooproduction. 
 
![Runbook-test](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. Klik op **opslaan** toosave hello runbook.
1. Klik op **testvenster** tooopen hello runbook in de testomgeving Hallo.
3. Nadat uw runbook parameters heeft, bent u waarden voor deze vraag tooenter.  Voer Hallo-naam van de resourcegroep Hallo en Hallo automation-account die gaat toocollect taakgegevens uit.
4. Klik op **Start** toohello hello runbook starten.
3. Hallo runbook wordt gestart met de status van **in de wachtrij geplaatst** voordat het kloonproces te**met**.  
3. Hallo runbook uitgebreide uitvoer moet worden weergegeven met Hallo-taken verzameld in json-indeling.  Als er geen taken worden weergegeven, klikt u vervolgens er mogelijk is er geen taken die zijn gemaakt in automation-account in Hallo Hallo afgelopen uur.  Probeer een runbook wordt gestart in Hallo automation-account en Voer Hallo test vervolgens opnieuw uit.
4. Zorg ervoor dat Hallo uitvoer wordt niet weergegeven na de eventuele fouten in Hallo opdracht tooLog Analytics.  U hebt een bericht vergelijkbaar toohello volgende.

    ![Post-uitvoer](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a>5. Controleer de records in Log Analytics
Als Hallo runbook in de test is voltooid en u gecontroleerd dat Hallo uitvoer is ontvangen, kunt u controleren Hallo records zijn gemaakt met een [logboek zoeken in logboekanalyse](../log-analytics/log-analytics-log-searches.md).

![Logboekuitvoer](media/operations-management-suite-runbook-datacollect/log-output.png)

1. Hallo Azure-portal, selecteer uw werkruimte voor logboekanalyse.
2. Klik op **Meld zoeken**.
3. Type Hallo na de opdracht `Type=AutomationJob_CL` en klik op de knop Zoeken Hallo. Houd er rekening mee dat het recordtype Hallo _CL die niet is opgegeven in de script Hallo bevat.  Dat achtervoegsel wordt automatisch toegevoegd toohello logboek type tooindicate dat het een type aangepaste logboek is.
4. Hier ziet u een of meer records geretourneerd die aangeeft dat runbook Hallo werkt zoals verwacht.


## <a name="6-publish-hello-runbook"></a>6. Hallo runbook publiceren
Nadat u hebt geverifieerd dat Hallo runbook correct werkt, moet u toopublish zodat u deze in productie kan uitvoeren.  U kunt doorgaan tooedit en Hallo runbook testen zonder de gepubliceerde versie Hallo worden gewijzigd.  

![Runbook publiceren](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. Automation-account tooyour retourneren.
2. Klik op **Runbooks** en selecteer **verzamelen-Automation-taken**.
3. Klik op **bewerken** en vervolgens **publiceren**.
4. Klik op **Ja** wanneer gestelde tooverify dat u wilt dat toooverwrite Hallo eerder gepubliceerde versie.

## <a name="7-set-logging-options"></a>7. Opties voor logboekregistratie instellen 
Test, die u zou kunnen tooview [uitgebreide uitvoer](../automation/automation-runbook-output-and-messages.md#message-streams) omdat u de variabele $VerbosePreference Hallo in Hallo script ingesteld.  Voor productie moet u tooset Hallo logboekeigenschappen voor Hallo runbook als u wilt dat tooview uitgebreide uitvoer.  Voor Hallo runbook in deze zelfstudie gebruikt, wordt dit Hallo json-gegevens worden verzonden tooLog Analytics weergegeven.

![Logboekregistratie en tracering](media/operations-management-suite-runbook-datacollect/logging.png)

1. Selecteer in het Hallo-eigenschappen voor uw runbook **logboekregistratie en tracering** onder **Runbookinstellingen**.
2. Wijzig de instelling Hallo voor **logboekregistratie van uitgebreide records** te**op**.
3. Klik op **Opslaan**.

## <a name="8-schedule-runbook"></a>8. Runbook plannen
Hallo meest voorkomende manier toostart een runbook dat bewakingsgegevens verzamelt is tooschedule het toorun automatisch.  U dit doen door het maken van een [schema in Azure Automation](../automation/automation-schedules.md) en tooyour runbook kunt koppelen.

![Runbook plannen](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. Selecteer in de eigenschappen voor uw runbook hello **planningen** onder **Resources**.
2. Klik op **toevoegen van een planning** > **koppelen van een planning tooyour runbook** > **Maak een nieuwe planning**.
5. Typ waarden voor Hallo planning en klik op volgende Hallo **maken**.

| Eigenschap | Waarde |
|:--|:--|
| Naam | AutomationJobs-per uur |
| Wordt gestart | Selecteer elk gewenst moment minstens 5 minuten afgelopen Hallo huidige tijd. |
| Terugkeerpatroon | Terugkerend |
| Herhaald elke | 1 uur |
| Vervaldatum van de set | Nee |

Als Hallo planning is gemaakt, moet u tooset Hallo parameterwaarden die worden gebruikt telkens wanneer die deze planning Hallo runbook wordt gestart.

6. Klik op **parameters configureren en instellingen uitvoeren**.
7. Vul in de waarden voor uw **ResourceGroupName** en **AutomationAccountName**.
8. Klik op **OK**. 

## <a name="9-verify-runbook-starts-on-schedule"></a>9. Controleer of u runbook wordt gestart volgens planning
Telkens wanneer een runbook wordt gestart, [wordt een taak gemaakt](../automation/automation-runbook-execution.md) en eventuele uitvoer in het logboek geregistreerd.  Dit zijn in feite Hallo verzamelen van dezelfde taken die Hallo runbook.  U kunt controleren dat Hallo runbook start zoals verwacht door het Hallo-taken voor het Hallo-runbook controleren na de begintijd Hallo voor Hallo planning is verstreken.

![Taken](media/operations-management-suite-runbook-datacollect/jobs.png)

1. Selecteer in de eigenschappen voor uw runbook hello **taken** onder **Resources**.
2. U ziet dat een lijst met taken voor elke keer Hallo runbook is gestart.
3. Klik op een van de Hallo taken tooview de details ervan.
4. Klik op **alle logboeken** tooview Hallo logboeken en uitvoer van Hallo runbook.
5. Schuif toohello onder toofind een vermelding vergelijkbare toohello in onderstaande afbeelding.<br>![Uitgebreide](media/operations-management-suite-runbook-datacollect/verbose.png)
6. Klik op deze vermelding tooview Hallo gedetailleerde json-gegevens die tooLog Analytics is verzonden.



## <a name="next-steps"></a>Volgende stappen
- Gebruik [ontwerper](../log-analytics/log-analytics-view-designer.md) toocreate weergeven van een weergave Hallo gegevens dat u toohello logboekanalyse opslagplaats hebt verzameld.
- Uw runbook in het pakket een [beheeroplossing](operations-management-suite-solutions-creating.md) toodistribute toocustomers.
- Meer informatie over [logboekanalyse](https://docs.microsoft.com/azure/log-analytics/).
- Meer informatie over [Azure Automation](https://docs.microsoft.com/azure/automation/).
- Meer informatie over Hallo [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).

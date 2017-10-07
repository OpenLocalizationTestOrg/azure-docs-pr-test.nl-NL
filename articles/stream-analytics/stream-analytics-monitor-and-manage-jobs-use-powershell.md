---
title: aaaMonitor en beheren van Stream Analytics-taken met PowerShell | Microsoft Docs
description: Meer informatie over hoe de Azure PowerShell-cmdlets en toomonitor toouse en Stream Analytics-taken beheren.
keywords: Azure powershell, azure powershell-cmdlets, powershell-opdracht powershell-scripts
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a>Bewaken en beheren van de Stream Analytics-taken met Azure PowerShell-cmdlets
Meer informatie over hoe toomonitor Stream Analytics-resources met Azure PowerShell-cmdlets en powershell-scripts die basic Stream Analytics-taken uitvoeren en beheren.

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a>Vereisten voor het uitvoeren van Azure PowerShell-cmdlets voor Stream Analytics
* Maak een Azure-resourcegroep in uw abonnement. Hallo Hieronder volgt een voorbeeld Azure PowerShell-script. Zie voor informatie Azure PowerShell [installeren en configureren van Azure PowerShell](/powershell/azure/overview);  

Azure PowerShell 0.9.8:  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

Azure PowerShell 1.0:  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> Stream Analytics-taken via een programma gemaakt beschikt niet over bewaking standaard ingeschakeld.  U kunt handmatig inschakelen voor bewaking in hello Azure-Portal door te navigeren pagina van de Monitor van toohello taak en klikt u op de knop inschakelen Hallo of u kunt hiervoor programmatisch Hallo stappen volgt zich bevindt op [Azure Stream Analytics - stroom van de Monitor Analytics-taken via programmacode](stream-analytics-monitor-jobs.md).
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a>Azure PowerShell-cmdlets voor Stream Analytics
Hallo volgende Azure PowerShell-cmdlets worden gebruikte toomonitor en Azure Stream Analytics-taken beheren. Houd er rekening mee dat Azure PowerShell verschillende versies heeft. 
**In de eerste opdracht vermelde Hallo voor Azure PowerShell 0.9.8 is Hallo voorbeelden is de tweede opdracht Hallo voor Azure PowerShell 1.0.** Hello Azure PowerShell 1.0 opdrachten hebben altijd 'AzureRM' in Hallo-opdracht.

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a>Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob
Informatie over de taak over een specifieke taak in de resourcegroep opgehaald of een lijst met alle Stream Analytics-taken in hello Azure-abonnement of de opgegeven resourcegroep is gedefinieerd.

**Voorbeeld 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob

Deze PowerShell-opdracht retourneert informatie over alle Hallo Stream Analytics-taken in hello Azure-abonnement.

**Voorbeeld 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Deze PowerShell-opdracht retourneert informatie over alle Hallo Stream Analytics-taken in de resourcegroep Hallo StreamAnalytics, standaard, centraal, VS.

**Voorbeeld 3**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Deze PowerShell-opdracht retourneert informatie over Hallo Stream Analytics-taak StreamingJob in de resourcegroep Hallo StreamAnalytics, standaard, centraal, VS.

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a>Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput
Geeft een lijst van alle Hallo invoerwaarden die zijn gedefinieerd in een opgegeven Stream Analytics-taak of informatie ophalen over een specifieke invoer.

**Voorbeeld 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Deze PowerShell-opdracht retourneert informatie over alle Hallo invoer in Hallo taak StreamingJob gedefinieerd.

**Voorbeeld 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Deze PowerShell-opdracht retourneert informatie over Hallo invoer met de naam gedefinieerd in taak Hallo StreamingJob EntryStream.

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a>Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput
Informatie over een specifieke uitvoer opgehaald of een lijst met alle Hallo-uitvoer die zijn gedefinieerd in een opgegeven Stream Analytics-taak.

**Voorbeeld 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Deze PowerShell-opdracht retourneert informatie over het Hallo-uitvoer in Hallo taak StreamingJob gedefinieerd.

**Voorbeeld 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Deze PowerShell-opdracht retourneert informatie over het Hallo-uitvoer met de naam gedefinieerd in taak Hallo StreamingJob uitvoer.

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a>Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota
Hiermee haalt u informatie over Hallo quotum van het streaming-eenheden in een opgegeven regio.

**Voorbeeld 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

Deze PowerShell-opdracht retourneert informatie over het Hallo-quota en het gebruik van streaming-eenheden in de regio VS-midden Hallo.

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a>Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation
Hiermee haalt u informatie over een specifieke transformatie gedefinieerd in een Stream Analytics-taak.

**Voorbeeld 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Deze PowerShell-opdracht retourneert informatie over Hallo transformatie StreamingJob in Hallo taak StreamingJob aangeroepen.

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a>Nieuwe AzureStreamAnalyticsInput | Nieuwe AzureRMStreamAnalyticsInput
Maakt u een nieuwe invoer binnen een Stream Analytics-taak of updates van een bestaande opgegeven invoer.

Hallo kan naam van Hallo invoer worden opgegeven in Hallo .json-bestand of op Hallo vanaf de opdrachtregel. Als beide worden opgegeven, moet Hallo-naam op de opdrachtregel Hallo hetzelfde als Hallo in Hallo-bestand worden Hallo.

Als u opgeeft dat al bestaat invoer en geef geen hello – Force-parameter Hallo cmdlet wordt u gevraagd of tooreplace Hallo bestaande invoer.

Als u opgeeft Hallo – Force-parameter en geef een bestaande naam invoeren, Hallo invoer worden vervangen zonder bevestiging.

Raadpleeg voor gedetailleerde informatie over Hallo JSON-bestandsstructuur en inhoud toohello [maken invoer (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-input] sectie Hallo [Stream Analytics Management REST-API Referentiebibliotheek][stream.analytics.rest.api.reference].

**Voorbeeld 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Deze PowerShell-opdracht maakt een nieuwe invoer van Hallo bestand Input.json. Als een bestaande invoer met Hallo naam die is opgegeven in de invoer definitiebestand Hallo al is gedefinieerd, wordt u gevraagd Hallo cmdlet of tooreplace deze.

**Voorbeeld 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Deze PowerShell-opdracht maakt een nieuwe invoer in Hallo taak EntryStream aangeroepen. Als een bestaande invoer met deze naam al is gedefinieerd, wordt u gevraagd Hallo cmdlet of tooreplace deze.

**Voorbeeld 3**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Deze PowerShell-opdracht vervangt Hallo definitie van Hallo bestaande invoerbron EntryStream aangeroepen met Hallo definitie uit het Hallo-bestand.

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a>Nieuwe AzureStreamAnalyticsJob | Nieuwe AzureRMStreamAnalyticsJob
Maakt een nieuwe Stream Analytics-taak in Microsoft Azure of updates Hallo definitie van een bestaande opgegeven taak.

Hallo-naam van Hallo taak kan worden opgegeven in Hallo .json-bestand of op Hallo-opdrachtregel. Als beide worden opgegeven, moet Hallo-naam op de opdrachtregel Hallo hetzelfde als Hallo in Hallo-bestand worden Hallo.

Als u een taaknaam opgeeft die al bestaat en geef geen hello – Force-parameter Hallo cmdlet wordt u gevraagd of tooreplace Hallo bestaande taak.

Als u opgeeft Hallo – Force-parameter en geef de taaknaam van een bestaande, wordt de taakdefinitie Hallo vervangen zonder bevestiging.

Raadpleeg voor gedetailleerde informatie over Hallo JSON-bestandsstructuur en inhoud toohello [Stream Analytics-taak maken] [ msdn-rest-api-create-stream-analytics-job] sectie Hallo [Stream Analytics Management REST API-verwijzing Bibliotheek][stream.analytics.rest.api.reference].

**Voorbeeld 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Deze PowerShell-opdracht maakt een nieuwe taak van Hallo definitie in JobDefinition.json. Als een bestaande taak met opgegeven in het bestand taak Hallo Hallo-naam al is gedefinieerd, wordt u gevraagd Hallo cmdlet of tooreplace deze.

**Voorbeeld 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Deze PowerShell-opdracht vervangt de taakdefinitie Hallo voor StreamingJob.

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a>Nieuwe AzureStreamAnalyticsOutput | Nieuwe AzureRMStreamAnalyticsOutput
Maakt een nieuwe uitvoer binnen een Stream Analytics-taak of een bestaande uitvoer-updates.  

Hallo-naam van Hallo uitvoer kan worden opgegeven op Hallo vanaf de opdrachtregel of Hallo .json-bestand. Als beide worden opgegeven, moet Hallo-naam op de opdrachtregel Hallo hetzelfde als Hallo in Hallo-bestand worden Hallo.

Als u opgeeft een uitvoer die al bestaat en geef geen hello – Force-parameter Hallo cmdlet wordt u gevraagd of tooreplace Hallo bestaande uitvoer.

Als u opgeeft Hallo – Force-parameter en geef de naam van een bestaande uitvoer, Hallo uitvoer worden vervangen zonder bevestiging.

Raadpleeg voor gedetailleerde informatie over Hallo JSON-bestandsstructuur en inhoud toohello [uitvoer maken (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-output] sectie Hallo [Stream Analytics Management REST-API Referentiebibliotheek][stream.analytics.rest.api.reference].

**Voorbeeld 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Deze PowerShell-opdracht maakt u een nieuwe uitvoer 'uitvoer' hello taak StreamingJob aangeroepen. Als een bestaande uitvoer met deze naam al is gedefinieerd, wordt u gevraagd Hallo cmdlet of tooreplace deze.

**Voorbeeld 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Deze PowerShell-opdracht vervangt Hallo definitie voor 'uitvoer' hello taak StreamingJob.

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a>Nieuwe AzureStreamAnalyticsTransformation | Nieuwe AzureRMStreamAnalyticsTransformation
Maakt u een nieuwe transformatie binnen een Stream Analytics-taak of Hallo bestaande transformatie-updates.

Hallo-naam van Hallo transformatie kan worden opgegeven in Hallo .json-bestand of op Hallo vanaf de opdrachtregel. Als beide worden opgegeven, moet Hallo-naam op de opdrachtregel Hallo hetzelfde als Hallo in Hallo-bestand worden Hallo.

Als u opgeeft dat al bestaat de transformatie en geef geen hello – Force-parameter Hallo cmdlet wordt u gevraagd of tooreplace Hallo bestaande transformatie.

Als u opgeeft Hallo – Force-parameter en geef de naam van een bestaande transformatie, Hallo transformatie worden vervangen zonder bevestiging.

Raadpleeg voor gedetailleerde informatie over Hallo JSON-bestandsstructuur en inhoud toohello [transformatie maken (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-transformation] sectie Hallo [Stream Analytics Management REST-API-referentiebibliotheek][stream.analytics.rest.api.reference].

**Voorbeeld 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Deze PowerShell-opdracht maakt een nieuwe transformatie StreamingJobTransform in Hallo taak StreamingJob aangeroepen. Als is al een bestaande transformatie gedefinieerd met deze naam, wordt u gevraagd Hallo cmdlet of tooreplace deze.

**Voorbeeld 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 Deze PowerShell-opdracht vervangt Hallo definitie van StreamingJobTransform in Hallo taak StreamingJob.

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a>Verwijder AzureStreamAnalyticsInput | Verwijder AzureRMStreamAnalyticsInput
Een specifieke invoer wordt asynchroon worden verwijderd uit een Stream Analytics-taak in Microsoft Azure.  
Als u opgeeft hello – Force parameter Hallo invoer worden verwijderd zonder bevestiging.

**Voorbeeld 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Deze PowerShell-opdracht verwijdert Hallo invoer EventStream in Hallo taak StreamingJob.  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a>Verwijder AzureStreamAnalyticsJob | Verwijder AzureRMStreamAnalyticsJob
Asynchroon Hiermee verwijdert u een specifieke Stream Analytics-taak in Microsoft Azure.  
Als u opgeeft hello – Force-parameter Hallo taak zal worden verwijderd zonder bevestiging.

**Voorbeeld 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Deze PowerShell-opdracht verwijdert Hallo taak StreamingJob.  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a>Verwijder AzureStreamAnalyticsOutput | Verwijder AzureRMStreamAnalyticsOutput
Een specifieke uitvoer wordt asynchroon worden verwijderd uit een Stream Analytics-taak in Microsoft Azure.  
Als u opgeeft hello – Force parameter Hallo uitvoer worden verwijderd zonder bevestiging.

**Voorbeeld 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Deze PowerShell-opdracht verwijdert Hallo uitvoer in Hallo taak StreamingJob uitvoer.  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a>Start AzureStreamAnalyticsJob | Start AzureRMStreamAnalyticsJob
Asynchroon implementeert en een Stream Analytics-taak start in Microsoft Azure.

**Voorbeeld 1**

Azure PowerShell 0.9.8:  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Azure PowerShell 1.0:  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Deze PowerShell-opdracht wordt gestart Hallo taak StreamingJob met een begintijd aangepaste uitvoer ingesteld tooDecember 12, 2012 12:12:12 UTC.

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a>Stop AzureStreamAnalyticsJob | Stop AzureRMStreamAnalyticsJob
Asynchroon stopt een Stream Analytics-taak wordt uitgevoerd in Microsoft Azure en ongedaan wijst bronnen toe die zijn die zijn gebruikt. Hallo blijven taakdefinitie en metagegevens beschikbaar in uw abonnement via hello Azure-portal en API's zodanig dat hello taak kan worden bewerkt en opnieuw opgestart. U wordt niet in rekening gebracht voor een taak gestopt Hallo status heeft.

**Voorbeeld 1**

Azure PowerShell 0.9.8:  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0:  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Deze PowerShell-opdracht stopt Hallo taak StreamingJob.  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a>Test AzureStreamAnalyticsInput | Test AzureRMStreamAnalyticsInput
Tests Hallo mogelijkheid van Stream Analytics tooconnect tooa opgegeven invoer.

**Voorbeeld 1**

Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0:  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Deze verbindingsstatus van PowerShell-opdracht tests Hallo Hallo EntryStream in StreamingJob invoer.  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a>Test AzureStreamAnalyticsOutput | Test AzureRMStreamAnalyticsOutput
Tests Hallo mogelijkheid van Stream Analytics tooconnect tooa opgegeven uitvoer.

**Voorbeeld 1**

Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0:  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Deze verbindingsstatus van PowerShell-opdracht tests Hallo Hallo uitvoer in StreamingJob uitvoer.  

## <a name="get-support"></a>Ondersteuning krijgen
Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics). 

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301


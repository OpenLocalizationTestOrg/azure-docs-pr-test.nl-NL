---
title: aaaTroubleshoot Azure Data Factory-problemen
description: Meer informatie over hoe tootroubleshoot problemen met het gebruik van Azure Data Factory.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a>Problemen met Data Factory oplossen
Dit artikel bevat tips voor probleemoplossing voor problemen bij het gebruik van Azure Data Factory. In dit artikel niet wordt vermeld in alle Hallo mogelijke problemen bij het gebruik Hallo-service, maar bevat informatie over sommige problemen en algemene tips voor probleemoplossing.   

## <a name="troubleshooting-tips"></a>Tips voor probleemoplossing
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a>Fout: Hallo-abonnement is niet geregistreerd toouse naamruimte 'Microsoft.DataFactory'
Als u dit foutbericht ontvangt, is niet hello Azure Data Factory-resourceprovider geregistreerd op uw computer. Hallo te volgen:

1. Start Azure PowerShell.
2. Tooyour aanmelden met Azure-account met behulp van de volgende opdracht Hallo.

    ```powershell
    Login-AzureRmAccount
    ```
3. Voer Hallo opdracht tooregister hello Azure Data Factory-provider te volgen.

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a>Probleem: Niet-geautoriseerde fout bij het uitvoeren van een Data Factory-cmdlet
U waarschijnlijk niet Hallo rechts Azure-account of -abonnement met hello Azure PowerShell gebruikt. Hallo na cmdlets tooselect Hallo rechts Azure-account en abonnement toouse Hello Azure PowerShell gebruiken.

1. Login-AzureRmAccount - gebruik Hallo juiste gebruikersnaam en wachtwoord
2. Get-AzureRmSubscription - weergave alle abonnementen voor account Hallo Hallo.
3. SELECT-AzureRmSubscription &lt;abonnementsnaam&gt; -Selecteer het juiste abonnement Hallo. Gebruik Hallo dezelfde is als die u toocreate een gegevensfactory op Hallo Azure-portal gebruiken.

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a>Probleem: Mislukken toolaunch Express-installatie van Data Management Gateway vanuit Azure-portal
Hallo snelle installatie voor Hallo Data Management Gateway vereist Internet Explorer of een compatibel webbrowser Microsoft ClickOnce. Als Hallo snelle installatie toostart mislukt, voert u een van de volgende Hallo:

* Internet Explorer of een webbrowser die Microsoft ClickOnce compatibel gebruiken.

    Als u Chrome gebruikt, gaat u toohello [Chrome web store](https://chrome.google.com/webstore/), zoeken met het sleutelwoord 'ClickOnce', kies een van de ClickOnce-extensies Hallo en deze installeren.

    Hallo dezelfde voor Firefox (install-invoegtoepassing). Klik op de knop Menu openen op Hallo werkbalk (drie horizontale lijnen in de rechterbovenhoek Hallo), invoegtoepassingen, zoeken met het sleutelwoord 'ClickOnce', kies een van de ClickOnce-extensies Hallo en deze installeren.
* Gebruik Hallo **handmatige installatie** koppeling weergegeven op Hallo van dezelfde blade in Hallo-portal. U gebruikt deze benadering toodownload-bestand voor installatie en het handmatig uitvoeren. Nadat het Hallo-installatie is voltooid, ziet u in het dialoogvenster van Hallo Data Management Gateway Configuration. Kopiëren Hallo **sleutel** uit portal welkomstscherm en het gebruik ervan in Hallo configuration manager toomanually Hallo gateway registreren bij Hallo-service.  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a>Probleem: Mislukken tooconnect tooon-premises SQL Server
Start **Data Management Gateway Configuration Manager** op Hallo van gateway-apparaat en gebruik Hallo **probleemoplossing** tootest Hallo verbinding tooSQL Server van de gatewaycomputer Hallo tabblad. Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a>Probleem: Invoer segmenten zijn in het wacht voor ooit op status
Hallo segmenten mogelijk **wachten** status vanwege toovarious redenen. Een veelvoorkomende redenen Hallo die Hallo is **externe** eigenschap is niet ingesteld te**true**. Een gegevensset die is geproduceerd buiten Hallo omvang van Azure Data Factory moet worden gemarkeerd met **externe** eigenschap. Deze eigenschap geeft aan dat gegevens Hallo externe en niet door pijplijnen binnen Hallo gegevensfactory back-ups. Hallo gegevenssegmenten zijn gemarkeerd als **gereed** nadat Hallo gegevens Hallo respectieve store beschikbaar is.

Zie de volgende voorbeeld voor het gebruik van Hallo HALLO hallo **externe** eigenschap. U kunt optioneel opgeven **externalData*** als u externe tootrue instelt.

Zie [gegevenssets](data-factory-create-datasets.md) artikel voor meer informatie over deze eigenschap.

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

tooresolve Hallo fout, Hallo toevoegen **externe** eigenschap en optionele Hallo **externalData** toohello JSON-definitie van de invoertabel Hallo sectie en maak deze opnieuw Hallo tabel.

### <a name="problem-hybrid-copy-operation-fails"></a>Probleem: Hybride kopieerbewerking mislukt
Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor stappen tootroubleshoot problemen met het kopiëren van/naar een on-premises gegevens opslaan met behulp van Data Management Gateway Hallo.

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a>Probleem: On-demand HDInsight inrichten mislukt
Wanneer u een gekoppelde service van het type HDInsightOnDemand gebruikt, moet u toospecify een linkedServiceName die tooan Azure Blob Storage verwijst. Data Factory-service gebruikt deze opslag toostore logboeken en de ondersteunende bestanden voor uw HDInsight-cluster op aanvraag.  Soms het inrichten van een HDInsight-cluster op aanvraag is mislukt met de volgende fout Hallo:

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

Deze fout geeft meestal aan dat Hallo-locatie van Hallo storage-account opgegeven in Hallo linkedServiceName zich niet in Hallo hetzelfde datacentrum locatie waar Hallo HDInsight inrichten er gebeurt. Voorbeeld: als uw gegevensfactory in VS-West en hello Azure-opslag bevindt zich in VS-Oost, Hallo inrichting mislukt op aanvraag in VS-West.

Daarnaast is er een tweede JSON-eigenschap, additionalLinkedServiceNames, waar extra opslagaccounts in HDInsight op aanvraag kunnen worden opgegeven. Deze extra gekoppelde opslagaccounts moet Hallo dezelfde locatie als Hallo HDInsight-cluster, of het is mislukt met de Hallo dezelfde fout.

### <a name="problem-custom-net-activity-fails"></a>Probleem: Aangepaste activiteit .NET mislukt
Zie [fouten opsporen in een pijplijn met een aangepaste activiteit](data-factory-use-custom-activities.md#troubleshoot-failures) voor gedetailleerde stappen.

## <a name="use-azure-portal-tootroubleshoot"></a>Azure portal tootroubleshoot gebruiken
### <a name="using-portal-blades"></a>Met de portal-blades
Zie [pijplijn bewaken](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) voor stappen.

### <a name="using-monitor-and-manage-app"></a>App voor controle en beheer gebruiken
Zie [bewaken en beheren van de data factory-pijplijnen bewaken en beheren van App met](data-factory-monitor-manage-app.md) voor meer informatie.

## <a name="use-azure-powershell-tootroubleshoot"></a>Azure PowerShell tootroubleshoot gebruiken
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a>Gebruik Azure PowerShell tootroubleshoot een fout opgetreden
Zie [Monitor Data Factory-pijplijnen met Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) voor meer informatie.

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png

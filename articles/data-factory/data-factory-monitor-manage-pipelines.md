---
title: aaaMonitor en pijplijnen beheren met behulp van hello Azure-portal en PowerShell | Microsoft Docs
description: Ontdek hoe toouse hello Azure portal en Azure PowerShell toomonitor en beheren van hello Azure data factory's en pijplijnen die u hebt gemaakt.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a>Bewaken en beheren van Azure Data Factory-pijplijnen met behulp van hello Azure-portal en PowerShell
> [!div class="op_single_selector"]
> * [Met behulp van Azure portal/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Met bewaking en beheer-app](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> Hallo-toepassing voor bewaking en beheer biedt een betere ondersteuning voor bewaking en het beheren van uw gegevenspijplijnen en het oplossen van problemen. Zie voor meer informatie over het gebruik van de toepassing hello [bewaken en beheren van Data Factory-pijplijnen met Hallo-app voor bewaking en beheer](data-factory-monitor-manage-app.md). 


Dit artikel wordt beschreven hoe u toomonitor, beheren en fouten opsporen in uw pijplijnen met behulp van Azure-portal en PowerShell. Hallo artikel biedt ook informatie over hoe toocreate waarschuwingen en u geïnformeerd over fouten.

## <a name="understand-pipelines-and-activity-states"></a>Pijplijnen en activiteiten statussen begrijpen
U kunt met behulp van hello Azure-portal:

* Uw data factory als een diagram weergeven.
* Activiteiten in een pijplijn weergeven.
* Invoer- en uitvoergegevenssets weergeven.

Deze sectie beschrijft ook hoe een segment gegevensset overgangen vanuit één status tooanother status.   

### <a name="navigate-tooyour-data-factory"></a>Navigeer tooyour data factory
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op **gegevensfactory** in Hallo-menu op Hallo links. Als u deze niet ziet, klikt u op **meer services >**, en klik vervolgens op **gegevensfactory** onder Hallo **INTELLIGENCE en analyse** categorie.

   ![Door alle Bladeren > gegevensfactory's](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. Op Hallo **gegevensfactory** blade, selecteer Hallo gegevensfactory die u geïnteresseerd bent in.

    ![Selecteer gegevensfactory](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   U ziet de startpagina Hallo voor Hallo data factory.

   ![Blade gegevensfactory](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a>Diagramweergave van uw data factory
Hallo **Diagram** weergave van een gegevensfactory biedt één van glas toomonitor en Hallo gegevensfactory en bijbehorende assets beheren. Hallo toosee **Diagram** van uw gegevensfactory weergeven, klikt u op **Diagram** op de startpagina Hallo voor Hallo data factory.

![Diagramweergave](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

U kunt inzoomen, uitzoomen, zoomen toofit, zoomen too100%, Hallo indeling vergrendelen van Hallo diagram en automatische positie gebruiken voor pijplijnen en gegevenssets. U ziet ook Hallo afkomst gegevens (dat wil zeggen items upstream- en downstreamitems van geselecteerde items weergeven).

### <a name="activities-inside-a-pipeline"></a>Activiteiten binnen een pijplijn
1. Met de rechtermuisknop op het Hallo-pijplijn en klik vervolgens op **pijplijn openen** toosee alle activiteiten in Hallo pipeline, samen met invoer- en uitvoergegevenssets voor Hallo activiteiten. Deze functie is handig als uw pijplijn meer dan één activiteit bevat en toounderstand Hallo operationele afkomst van één pijplijn gewenste.

    ![Menu Pijplijn openen](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. In de Hallo voorbeeld te volgen, ziet u een kopieeractiviteit in Hallo-pijplijn met een invoer en uitvoer. 

    ![Activiteiten binnen een pijplijn](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. U kunt back toohello startpagina van de gegevensfactory Hallo navigeren door te klikken op Hallo **gegevensfactory** koppeling in Hallo breadcrumb op Hallo linkerbovenhoek.

    ![Navigeer terug toodata factory](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a>Hallo-status van elke activiteit in een pijplijn weergeven
U kunt Hallo huidige status van een activiteit weergeven door Hallo status van Hallo gegevenssets die worden geproduceerd door Hallo activiteit weer te geven.

Door te dubbelklikken op Hallo **OutputBlobTable** in Hallo **Diagram**, ziet u alle Hallo-segmenten die worden geproduceerd door andere activiteiten bij uitvoering binnen een pijplijn. U kunt zien of Hallo kopieeractiviteit is uitgevoerd voor Hallo afgelopen acht uur en geproduceerd Hallo segmenten in Hallo **gereed** status.  

![Status van het Hallo-pipeline](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

Hallo gegevensset segmenten in de gegevensfactory Hallo kunnen een van volgende statussen Hallo hebben:

<table>
<tr>
    <th align="left">Status</th><th align="left">Subtoestand</th><th align="left">Beschrijving</th>
</tr>
<tr>
    <td rowspan="8">Wachten</td><td>ScheduleTime</td><td>Hallo-tijd is niet geleverd voor Hallo segment toorun.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>Hallo upstream-afhankelijkheden zijn niet gereed.</td>
</tr>
<tr>
<td>ComputeResources</td><td>Hallo rekenresources zijn niet beschikbaar.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Alle Hallo activiteitsinstanties zijn bezig met het uitvoeren van andere segmenten.</td>
</tr>
<tr>
<td>ActivityResume</td><td>Hallo-activiteit is onderbroken en Hallo segmenten kan niet worden uitgevoerd totdat het Hallo-activiteit is hervat.</td>
</tr>
<tr>
<td>Probeer het opnieuw</td><td>Er wordt opnieuw geprobeerd activiteit is uitgevoerd.</td>
</tr>
<tr>
<td>Validatie</td><td>Validatie is nog niet gestart.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>Validatie is wachten toobe opnieuw geprobeerd.</td>
</tr>
<tr>
<tr>
<td rowspan="2">InProgress</td><td>Valideren</td><td>Validatie wordt uitgevoerd.</td>
</tr>
<td>-</td>
<td>Hallo-segment wordt verwerkt.</td>
</tr>
<tr>
<td rowspan="4">Is mislukt</td><td>Time-out</td><td>Hallo activiteit uitvoeren duurde langer dan is toegestaan door Hallo-activiteit.</td>
</tr>
<tr>
<td>Geannuleerd</td><td>Hallo-segment is geannuleerd door in te grijpen.</td>
</tr>
<tr>
<td>Validatie</td><td>Validatie is mislukt.</td>
</tr>
<tr>
<td>-</td><td>Hallo-segment is mislukt toobe gegenereerd en/of gevalideerd.</td>
</tr>
<td>Gereed</td><td>-</td><td>Hallo-segment is gereed voor gebruik.</td>
</tr>
<tr>
<td>Overgeslagen</td><td>Geen</td><td>Hallo-segment wordt niet verwerkt.</td>
</tr>
<tr>
<td>Geen</td><td>-</td><td>Een segment tooexist gebruikt met een andere status, maar is teruggezet.</td>
</tr>
</table>



U kunt Hallo details over een segment weergeven door te klikken op een vermelding segment op Hallo **segmenten onlangs bijgewerkt** blade.

![Details van het segment](./media/data-factory-monitor-manage-pipelines/slice-details.png)

Als het Hallo-segment is meerdere keren uitgevoerd, ziet u meerdere rijen in Hallo **activiteit wordt uitgevoerd** lijst. U kunt details zien over een activiteit die wordt uitgevoerd door te klikken op Hallo uitvoeren vermelding in Hallo **activiteit wordt uitgevoerd** lijst. Hallo-lijst bevat alle Hallo-logboekbestanden, samen met een foutbericht als er een. Deze functie is handig logboeken voor tooview en foutopsporing zonder tooleave uw gegevensfactory.

![Details uitvoering van activiteit](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

Als Hallo segment niet in Hallo **gereed** staat, kunt u zien Hallo upstreamsegmenten die niet gereed zijn en blokkeren het huidige segment uitgevoerd Hallo Hallo **upstreamsegmenten die niet gereed** lijst. Deze functie is handig als uw segment **wachten** status en u wilt dat toounderstand Hallo upstream-afhankelijkheden die Hallo segment wacht op.

![Upstreamsegmenten die niet gereed zijn](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a>DataSet staat diagram
Nadat u een gegevensfactory implementeert en Hallo pijplijnen een ongeldige actieve periode hebben, segmenten Hallo gegevensset overgang van een status tooanother. Op dit moment volgt Hallo segment status Hallo status-diagram te volgen:

![Diagram van status](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

Hallo gegevensset status overgang stroom in gegevensfactory is de volgende Hallo: wachten-In-voortgang/In uitvoering (Validating) > -> gereed/mislukt.

Hallo-segment wordt gestart in een **wachten** staat, wacht voorwaarden toobe voldaan voordat deze wordt uitgevoerd. Vervolgens Hallo activiteit wordt uitgevoerd en probeert het Hallo-segment een **In uitvoering** status. Hallo activiteit is uitgevoerd, kan slagen of mislukken. Hallo-segment is gemarkeerd als **gereed** of **mislukt**, op basis van Hallo resultaat van het Hallo-uitvoering.

Kunt u herstellen Hallo segment toogo door Hallo **gereed** of **mislukt** status toohello **wachten** status. U kunt ook Hallo segment de status te markeren**overslaan**, waardoor Hallo-activiteit uit uitgevoerd en geen Hallo segment worden verwerkt.

## <a name="pause-and-resume-pipelines"></a>Onderbreken en hervatten pijplijnen
U kunt uw pijplijnen beheren met behulp van Azure PowerShell. U kunt bijvoorbeeld onderbreken en hervatten van pijplijnen door het uitvoeren van Azure PowerShell-cmdlets. 

> [!NOTE] 
> Hallo diagramweergave biedt geen ondersteuning voor het onderbreken en hervatten pijplijnen. Als u toouse een gebruikersinterface wilt, gebruikt u Hallo controleren en beheren van toepassing. Zie voor meer informatie over het gebruik van de toepassing hello [bewaken en beheren van Data Factory-pijplijnen met Hallo-app voor bewaking en beheer](data-factory-monitor-manage-app.md) artikel. 

U kunt onderbreken/uitstellen pijplijnen met behulp van Hallo **onderbreken AzureRmDataFactoryPipeline** PowerShell-cmdlet. Deze cmdlet is handig als u niet dat toorun uw pijplijnen wilt totdat een probleem is opgelost. 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
Bijvoorbeeld:

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

Nadat het Hallo-probleem is opgelost met Hallo pipeline, kunt u Hallo onderbroken pijplijn hervatten door Hallo volgende PowerShell-opdracht uitgevoerd:

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
Bijvoorbeeld:

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a>Fouten opsporen in pijplijnen
Azure Data Factory biedt uitgebreide mogelijkheden voor u toodebug en pijplijnen oplossen met behulp van hello Azure-portal en Azure PowerShell.

> [! Houd er rekening mee} is veel eenvoudiger tootroubleshot fouten bij het gebruik Hallo bewaking App en beheer. Zie voor meer informatie over het gebruik van de toepassing hello [bewaken en beheren van Data Factory-pijplijnen met Hallo-app voor bewaking en beheer](data-factory-monitor-manage-app.md) artikel. 

### <a name="find-errors-in-a-pipeline"></a>Fouten gevonden in een pijplijn
Als Hallo activiteit die wordt uitgevoerd in een pijplijn is mislukt, is het Hallo-gegevensset die wordt geproduceerd door Hallo pijplijn in een foutstatus vanwege fout Hallo. U kunt fouten opsporen en oplossen van fouten in Azure Data Factory met behulp van de volgende methoden Hallo.

#### <a name="use-hello-azure-portal-toodebug-an-error"></a>Gebruik hello Azure portal toodebug een fout opgetreden
1. Op Hallo **tabel** blade, klikt u op Hallo probleem segment dat Hallo is **Status** instellen te**mislukt**.

   ![Blade tabel met probleem segment](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. Op Hallo **gegevenssegment** blade, klikt u op Hallo activiteit die wordt uitgevoerd die niet zijn geslaagd.

   ![Gegevenssegment met een fout](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. Op Hallo **details uitvoering van activiteit** blade kunt u Hallo-bestanden die gekoppeld aan Hallo HDInsight verwerking zijn downloaden. Klik op **downloaden** voor Status/stderr toodownload Hallo foutenlogboekbestand met informatie over het Hallo-fout.

   ![Activiteit blade toewijzingdetails uitvoeren met de fout](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a>Gebruik PowerShell toodebug een fout opgetreden
1. Start **PowerShell**.
2. Voer Hallo **Get-AzureRmDataFactorySlice** opdracht toosee Hallo segmenten en hun status. U ziet een segment met Hallo status **mislukt**.        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   Bijvoorbeeld:

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   Vervang **StartDateTime** met begintijd van de pijplijn. 
3. Voer nu Hallo **Get-AzureRmDataFactoryRun** cmdlet tooget gegevens over Hallo activiteit uitvoeren voor Hallo segment.

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    Bijvoorbeeld:

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    Hallo-waarde van StartDateTime is Hallo begintijd voor Hallo fout/probleem segment dat u hebt genoteerd uit de vorige stap Hallo. datum / tijd-Hallo moet tussen dubbele aanhalingstekens worden geplaatst.
4. Hier ziet u uitvoer met meer informatie over Hallo-fout die is vergelijkbaar toohello volgende:

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. Hallo kan worden uitgevoerd **opslaan AzureRmDataFactoryLog** cmdlet uit met de id-waarde in Hallo uitvoer zien en Hallo logboekbestanden downloaden met behulp van Hallo Hallo **- DownloadLogsoption** voor Hallo-cmdlet.

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a>Fouten in een pijplijn opnieuw uitvoeren

> [!IMPORTANT]
> Is het eenvoudiger tootroubleshoot fouten en voer mislukte segmenten met behulp van Hallo voor bewaking en beheer-App. Zie voor meer informatie over het gebruik van de toepassing hello [bewaken en beheren van Data Factory-pijplijnen met Hallo-app voor bewaking en beheer](data-factory-monitor-manage-app.md). 

### <a name="use-hello-azure-portal"></a>Gebruik hello Azure-portal
Nadat u problemen oplossen en het opsporen van fouten in een pijplijn, kunt u fouten opnieuw uitvoeren door te navigeren toohello fout segment en te klikken op Hallo **uitvoeren** knop op de opdrachtbalk Hallo.

![Een mislukte segment opnieuw uitvoeren](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

In geval Hallo segment heeft validatie is mislukt vanwege een fout van beleid (bijvoorbeeld als gegevens niet beschikbaar is), kunt u Hallo fout corrigeren en validatie opnieuw uit door te klikken op Hallo **valideren** knop op de opdrachtbalk Hallo.

![Corrigeer de fouten en valideren](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a>Azure PowerShell gebruiken
U kunt fouten opnieuw uitvoeren met behulp van Hallo **Set-AzureRmDataFactorySliceStatus** cmdlet. Zie Hallo [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) onderwerp voor de syntaxis en andere details over Hallo-cmdlet.

**Voorbeeld:**

Hallo volgende voorbeeld wordt ingesteld Hallo status van alle segmenten voor Hallo tabel 'DAWikiAggregatedData' too'Waiting' in hello Azure-gegevensfactory 'WikiADF'.

Hallo 'UpdateType' too'UpstreamInPipeline is ingesteld, wat betekent dat de status van elk segment voor Hallo tabel en alle Hallo afhankelijke (upstream) tabellen too'Waiting zijn ingesteld. Hallo is andere mogelijke waarde voor deze parameter 'Afzonderlijk'.

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a>Waarschuwingen maken
Azure logboeken gebruikersgebeurtenissen als een Azure-resource (bijvoorbeeld een gegevensfactory) wordt gemaakt, bijgewerkt of verwijderd. U kunt waarschuwingen maken van deze gebeurtenissen. U kunt gebruiken Gegevensfactory toocapture verschillende metrische gegevens en waarschuwingen maken op de metrische gegevens. U wordt aangeraden dat u gebeurtenissen voor realtime-controle en metrische gegevens worden gebruikt voor historische doeleinden.

### <a name="alerts-on-events"></a>Waarschuwingen over gebeurtenissen
Gebeurtenissen van Azure bieden handig inzicht in wat in uw Azure-resources gebeurt er. Wanneer u van Azure Data Factory gebruikmaakt, gebeurtenissen worden gegenereerd wanneer:

* Een gegevensfactory is gemaakt, bijgewerkt of verwijderd.
* Verwerken van gegevens (als 'wordt uitgevoerd') is gestart of voltooid.
* Een HDInsight-cluster op aanvraag wordt gemaakt of verwijderd.

U kunt waarschuwingen van deze gebruikersgebeurtenissen maken en configureren toosend e-mailmeldingen toohello beheerder en coadministrators van Hallo-abonnement. Bovendien kunt u aanvullende e-mailadressen van de gebruikers hoeven tooreceive e-mailmeldingen Hallo voorwaarden wordt voldaan. Deze functie is handig als u tooget melding op fouten wilt en niet dat de monitor toocontinuously uw gegevensfactory wilt.

> [!NOTE]
> Op dit moment weergeven niet Hallo portal waarschuwingen op gebeurtenissen. Gebruik Hallo [app voor bewaking en beheer](data-factory-monitor-manage-app.md) toosee alle waarschuwingen.


#### <a name="specify-an-alert-definition"></a>Geef een definitie van een waarschuwing
de definitie van een waarschuwing toospecify, u een JSON-bestand met een beschrijving van Hallo-bewerkingen die u wilt dat een melding op toobe maken. In Hallo volgt, verzendt Hallo waarschuwing een e-mailmelding voor Hallo RunFinished bewerking. specifieke toobe, een e-mailmelding wordt verzonden wanneer een uitvoering in de gegevensfactory Hallo is voltooid en Hallo uitvoeren is mislukt (Status = FailedExecution).

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

U kunt verwijderen **subStatus** van Hallo JSON-definitie als u niet toobe gewaarschuwd op een specifieke fout wilt.

In dit voorbeeld wordt een Hallo-waarschuwing voor alle data Factory in uw abonnement. Als u wilt dat Hallo waarschuwing toobe instellen voor een bepaalde data factory, kunt u data factory **resourceUri** in Hallo **dataSource**:

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

Hallo bevat volgende tabel Hallo-lijst van beschikbare bewerkingen en statussen (en substatus).

| De naam van bewerking | Status | Substatus |
| --- | --- | --- |
| RunStarted |Gestart |Starting |
| RunFinished |Kan niet / is voltooid |FailedResourceAllocation<br/><br/>Geslaagd<br/><br/>FailedExecution<br/><br/>Time-out<br/><br/>< geannuleerd<br/><br/>FailedValidation<br/><br/>Afgebroken |
| OnDemandClusterCreateStarted |Gestart | |
| OnDemandClusterCreateSuccessful |Geslaagd | |
| OnDemandClusterDeleted |Geslaagd | |

Zie [waarschuwingsregel maken](https://msdn.microsoft.com/library/azure/dn510366.aspx) voor meer informatie over Hallo JSON-elementen die worden gebruikt in het Hallo-voorbeeld.

#### <a name="deploy-hello-alert"></a>Hallo waarschuwing implementeren
toodeploy hello waarschuwing, gebruik hello Azure PowerShell-cmdlet **New-AzureRmResourceGroupDeployment**, zoals weergegeven in het volgende voorbeeld Hallo:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

Nadat de resource Hallo implementatie is voltooid, ziet u Hallo volgende berichten:

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> U kunt Hallo [waarschuwingsregel maken](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST-API toocreate een waarschuwingsregel. Hallo JSON-nettolading is vergelijkbaar toohello JSON-voorbeeld.  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a>Hallo-lijst met Azure resourcegroepimplementaties ophalen
tooretrieve hello lijst met Azure resourcegroepimplementaties geïmplementeerd, gebruikt u de cmdlet Hallo **Get-AzureRmResourceGroupDeployment**, zoals weergegeven in het volgende voorbeeld Hallo:

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a>Oplossen van gebruikersgebeurtenissen
1. U kunt zien dat alle Hallo-gebeurtenissen die worden gegenereerd wanneer u op Hallo **metrische gegevens en bewerkingen** tegel.

    ![Tegel metrische gegevens en bewerkingen](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. Klik op Hallo **gebeurtenissen** tegel toosee Hallo gebeurtenissen.

    ![Tegel gebeurtenissen](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. Op Hallo **gebeurtenissen** blade ziet u informatie over gebeurtenissen en gefilterde gebeurtenissen.

    ![Blade gebeurtenissen](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. Klik op een **bewerking** in de lijst met bewerkingen Hallo dat een fout veroorzaakt.

    ![Een bewerking selecteren](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. Klik op een **fout** toosee Gebeurtenisdetails over Hallo-fout.

    ![Fout van gebeurtenis](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

Zie [inzicht van Azure-cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) ophalen of verwijderen van waarschuwingen voor PowerShell-cmdlets waarmee u tooadd kunt. Hier volgen enkele voorbeelden van het gebruik van Hallo **Get-AlertRule** cmdlet:

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

Hallo na de get-help opdrachten toosee details en voorbeelden voor Hallo Get AlertRule cmdlet wordt uitgevoerd.

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


Als er Hallo genereren van waarschuwingen gebeurtenissen op Hallo portalblade, maar u geen e-mailmeldingen ontvangen, controleert u of Hallo e-mailadres dat is opgegeven tooreceive e-mailberichten van externe afzenders is ingesteld. Hallo e-mailwaarschuwingen is mogelijk geblokkeerd door uw e-mailinstellingen.

### <a name="alerts-on-metrics"></a>Waarschuwingen op metrische gegevens
U kunt verschillende metrische gegevens vastleggen en waarschuwingen maken op de metrische gegevens in Data Factory. U kunt bewaken en waarschuwingen maken op Hallo metrische gegevens voor Hallo segmenten in de gegevensfactory te volgen:

* **Mislukte wordt uitgevoerd**
* **Geslaagde wordt uitgevoerd**

Deze metrische gegevens zijn nuttig en helpt u een overzicht van de algemene mislukte en geslaagde wordt uitgevoerd in de gegevensfactory hello tooget. Metrische gegevens zijn verzonden, elke keer dat er wordt een segment uitvoeren. Aan het begin van de Hallo van Hallo uur, wordt deze metrische gegevens worden geaggregeerd en gepusht tooyour storage-account. metrische gegevens voor tooenable, instellen van een opslagaccount.

#### <a name="enable-metrics"></a>Metrische gegevens inschakelen
tooenable metrische gegevens en klik op volgende Hallo van Hallo **Data Factory** blade:

**Bewaking** > **metriek** > **diagnostische instellingen** > **diagnostische gegevens**

![Diagnostische gegevens koppelen](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

Op Hallo **Diagnostics** blade, klikt u op **op**, selecteer Hallo storage-account en klikt u op **opslaan**.

![Blade diagnostische gegevens](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

Het Hallo metrische gegevens toobe zichtbaar zijn op Hallo tooone uur kan duren **bewaking** blade omdat metrische gegevens aggregatie per uur gebeurt.

### <a name="set-up-an-alert-on-metrics"></a>Instellen van een waarschuwing op metrische gegevens
Klik op Hallo **Data Factory metrische gegevens** tegel:

![Data factory metrische gegevens tegel](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

Op Hallo **metriek** blade, klikt u op **+ waarschuwing toevoegen** op Hallo-werkbalk.
![Metrische blade gegevensfactory > Waarschuwing toevoegen](./media/data-factory-monitor-manage-pipelines/add-alert.png)

Op Hallo **een waarschuwingsregel toevoegen** pagina Hallo van de volgende stappen uit en klik op **OK**.

* Voer een naam voor de waarschuwing hello (voorbeeld: 'is mislukt van de waarschuwing').
* Voer een beschrijving van waarschuwing hello (voorbeeld: 'een e-mailbericht verzenden wanneer een fout optreedt').
* Selecteer een waarde (vs "Wordt uitgevoerd is mislukt". 'Geslaagd wordt uitgevoerd').
* Geef een voorwaarde en de drempelwaarde.   
* Hallo periode opgeven.
* Geef op of een e-mailbericht moet worden verzonden tooowners, bijdragers en lezers.

![Metrische blade gegevensfactory > waarschuwingsregel toevoegen](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

Nadat Hallo waarschuwingsregel is toegevoegd, Hallo blade wordt gesloten en er nieuwe waarschuwing Hallo op Hallo **metriek** blade.

![Metrische blade gegevensfactory > nieuwe waarschuwing toegevoegd](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

U ziet ook het aantal waarschuwingen in Hallo Hallo **waarschuwing regels** tegel. Klik op Hallo **waarschuwing regels** tegel.

![Metrische blade gegevensfactory - regels voor waarschuwingen](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

Op Hallo **regels waarschuwingen** blade ziet u een bestaande waarschuwingen. tooadd een waarschuwing, klikt u op **waarschuwing toevoegen** op Hallo-werkbalk.

![Regels voor waarschuwingen-blade](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a>Meldingen van waarschuwingen
Nadat de waarschuwingsregel Hallo overeenkomt met Hallo voorwaarde, krijgt u een e-mailbericht met de tekst hello waarschuwing is geactiveerd. Nadat de Hallo probleem is opgelost en Hallo meldingsvoorwaarde meer komt niet overeen, krijgt u een e-mailbericht met de tekst hello waarschuwing is opgelost.

Dit gedrag is anders dan gebeurtenissen waarbij een melding wordt verzonden op elke fout die een waarschuwingsregel in aanmerking komt voor.

### <a name="deploy-alerts-by-using-powershell"></a>Waarschuwingen implementeren met behulp van PowerShell
U kunt waarschuwingen kunt implementeren voor metrische gegevens Hallo dezelfde manier voor gebeurtenissen.

**Definitie van waarschuwing**

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

Vervang *subscriptionId*, *resourceGroupName*, en *dataFactoryName* in Hallo voorbeeld met de juiste waarden.

*metricName* ondersteunt momenteel twee waarden:

* FailedRuns
* SuccessfulRuns

**Hallo waarschuwing implementeren**

toodeploy hello waarschuwing, gebruik hello Azure PowerShell-cmdlet **New-AzureRmResourceGroupDeployment**, zoals weergegeven in het volgende voorbeeld Hallo:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

Ziet het volgende bericht na een geslaagde implementatie:

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

U kunt ook Hallo **toevoegen AlertRule** cmdlet toodeploy een waarschuwingsregel. Zie Hallo [toevoegen AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) onderwerp voor meer informatie en voorbeelden.  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a>Een data factory tooa andere resourcegroep of abonnement verplaatsen
U kunt een data factory tooa andere resourcegroep of een ander abonnement verplaatsen met behulp van Hallo **verplaatsen** opdracht balk knop op de startpagina Hallo van uw gegevensfactory.

![Verplaatsen van de gegevensfactory](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

U kunt ook alle gerelateerde resources (zoals waarschuwingen die gekoppeld aan de gegevensfactory Hallo zijn), samen met de Hallo gegevensfactory verplaatsen.

![Dialoogvenster resources verplaatsen](./media/data-factory-monitor-manage-pipelines/MoveResources.png)

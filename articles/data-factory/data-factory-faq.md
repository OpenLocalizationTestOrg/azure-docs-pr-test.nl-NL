---
title: aaaAzure Data Factory - Veelgestelde vragen
description: Veelgestelde vragen over Azure Data Factory.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 532dec5a-7261-4770-8f54-bfe527918058
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 78289fb4b6e15d74772af6c71ec25c7d2ca1a0bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---frequently-asked-questions"></a>Azure Data Factory - Veelgestelde vragen
## <a name="general-questions"></a>Algemene vragen
### <a name="what-is-azure-data-factory"></a>Wat is Azure Data Factory?
Data Factory is een cloud-gebaseerde gegevensintegratie service die **automatiseert Hallo verplaatsing en transformatie van gegevens**. Net als een factory die de apparatuur wordt tootake grondstoffen en te transformeren in eindproducten, ingedeeld Data Factory bestaande services die onbewerkte gegevens verzamelen en transformeren in kant-en-klare informatie.

Data Factory kunt u toocreate gegevensgestuurde werkstromen toomove gegevens tussen zowel lokale en cloud gegevensarchieven als proces/transformatie-gegevens met behulp van compute services zoals Azure HDInsight en Azure Data Lake Analytics. Nadat u een pijplijn waarmee Hallo-actie die u nodig hebt gemaakt, kunt u het periodiek toorun (elk uur, dagelijks, wekelijks, enzovoort) plannen.   

Zie voor meer informatie [overzicht & hoofdconcepten](data-factory-introduction.md).

### <a name="where-can-i-find-pricing-details-for-azure-data-factory"></a>Waar vind ik prijsinformatie voor Azure Data Factory?
Zie [prijsinformatie voor Data Factory pagina] [ adf-pricing-details] voor Hallo prijsinformatie voor hello Azure Data Factory.  

### <a name="how-do-i-get-started-with-azure-data-factory"></a>Hoe ga ik aan de slag met Azure Data Factory?
* Zie voor een overzicht van Azure Data Factory [inleiding tooAzure Data Factory](data-factory-introduction.md).
* Voor een zelfstudie over het te**gegevens kopiëren of verplaatsen** Kopieeractiviteit gebruikt, Zie [gegevens uit Azure Blob Storage tooAzure SQL-Database kopiëren](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
* Voor een zelfstudie over het te**gegevens transformeren** met HDInsight Hive-activiteit. Zie [gegevens verwerken door het Hive-script uitvoeren op Hadoop-cluster](data-factory-build-your-first-pipeline.md)

### <a name="what-is-hello-data-factorys-region-availability"></a>Wat is Hallo Data Factory beschikbaarheid in regio's?
Data Factory is beschikbaar in **VS-West** en **Noord-Europa**. Hallo compute en storage-services die worden gebruikt door gegevensfactory's kunnen zich in andere regio's. Zie [ondersteunde regio's](data-factory-introduction.md#supported-regions).

### <a name="what-are-hello-limits-on-number-of-data-factoriespipelinesactivitiesdatasets"></a>Wat zijn Hallo beperkingen van het aantal data factory's / pijplijnen/activiteiten, gegevenssets?
Zie **Azure Data Factory limieten** sectie Hallo [Azure-abonnement en Service-limieten, quota's en beperkingen](../azure-subscription-service-limits.md#data-factory-limits) artikel.

### <a name="what-is-hello-authoringdeveloper-experience-with-azure-data-factory-service"></a>Wat is Hallo ontwerpen of ontwikkelaar ervaring met Azure Data Factory-service?
U kunt de auteur/maken data Factory met een van de volgende hulpprogramma's / SDK's Hallo:

* **Azure-portal** Hallo Data Factory blades in hello Azure-portal bieden uitgebreide gebruikersinterface voor u toocreate data factory's ad gekoppelde services. Hallo **Data Factory-Editor**, die ook deel uitmaakt van Hallo-portal, kunt u tooeasily gekoppelde services, tabellen, gegevenssets en pijplijnen maken door te geven van JSON-definities voor deze artefacten. Zie [bouwen van uw eerste gegevens pijplijn met Azure portal](data-factory-build-your-first-pipeline-using-editor.md) voor een voorbeeld van het gebruik van Hallo portal/editor toocreate en implementeren van een gegevensfactory.
* **Visual Studio** kunt u Visual Studio toocreate een Azure data factory. Zie [bouwen van uw eerste gegevens pijplijn met Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) voor meer informatie.
* **Azure PowerShell** Zie [maken en te bewaken Azure Data Factory met Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md) voor een zelfstudie/overzicht voor het maken van een gegevensfactory met behulp van PowerShell. Zie [Data Factory Cmdlet Reference] [ adf-powershell-reference] inhoud op MSDN-bibliotheek voor een uitgebreide documentatie over Data Factory-cmdlets.
* **.NET class Library** programmatisch kunt u data factory maken met behulp van de Data Factory .NET SDK. Zie [maken, bewaken en beheren van data Factory met .NET SDK](data-factory-create-data-factories-programmatically.md) voor een overzicht van het maken van een gegevensfactory met .NET SDK. Zie [Data Factory Class Library Reference] [ msdn-class-library-reference] voor een uitgebreide documentatie over Data Factory .NET SDK.
* **REST-API** kunt u ook Hallo REST-API die worden weergegeven door hello Azure Data Factory-service toocreate gebruiken en implementeren van de data Factory. Zie [Data Factory REST API Reference] [ msdn-rest-api-reference] voor een uitgebreide documentatie van de REST-API van Data Factory.
* **Azure Resource Manager-sjabloon** Zie [zelfstudie: uw eerste Azure-gegevensfactory bouwen met Azure Resource Manager-sjabloon](data-factory-build-your-first-pipeline-using-arm.md) voor meer informatie.

### <a name="can-i-rename-a-data-factory"></a>Kan ik de naam van een gegevensfactory wijzigen?
Nee. Net als andere Azure-resources kan niet Hallo-naam van een Azure data factory worden gewijzigd.

### <a name="can-i-move-a-data-factory-from-one-azure-subscription-tooanother"></a>Kan ik een gegevensfactory verplaatsen van een Azure-abonnement tooanother?
Ja. Gebruik Hallo **verplaatsen** knop op de blade gegevensfactory, zoals wordt weergegeven in het volgende diagram Hallo:

![Verplaatsen van de gegevensfactory](media/data-factory-faq/move-data-factory.png)

### <a name="what-are-hello-compute-environments-supported-by-data-factory"></a>Wat zijn Hallo berekeningsomgevingen die door Data Factory worden ondersteund?
Hallo bevat volgende tabel een overzicht van compute-omgevingen wordt ondersteund door de Data Factory en Hallo activiteiten die kunnen worden uitgevoerd op deze.

| Compute-omgeving | activities |
| --- | --- |
| [HDInsight-cluster op aanvraag](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) of [uw eigen HDInsight-cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop-Streaming](data-factory-hadoop-streaming-activity.md) |
| [Azure Batch](data-factory-compute-linked-services.md#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Azure Machine Learning](data-factory-compute-linked-services.md#azure-machine-learning-linked-service) |[Machine Learning-activiteiten: batchuitvoering en resources bijwerken](data-factory-azure-ml-batch-execution-activity.md) |
| [Azure Data Lake Analytics](data-factory-compute-linked-services.md#azure-data-lake-analytics-linked-service) |[Data Lake Analytics U-SQL](data-factory-usql-activity.md) |
| [Azure SQL](data-factory-compute-linked-services.md#azure-sql-linked-service), [Azure SQL datawarehouse](data-factory-compute-linked-services.md#azure-sql-data-warehouse-linked-service), [SQL Server](data-factory-compute-linked-services.md#sql-server-linked-service) |[Opgeslagen procedure](data-factory-stored-proc-activity.md) |

### <a name="how-does-azure-data-factory-compare-with-sql-server-integration-services-ssis"></a>Hoe Azure Data Factory vergelijken met SQL Server Integration Services (SSIS)? 
Zie Hallo [tegenover Azure Data Factory. SSIS](http://www.sqlbits.com/Sessions/Event15/Azure_Data_Factory_vs_SSIS) presentatie van een van onze MVP's (meest waardevolle Professionals): Reza Rad. Enkele Hallo recente wijzigingen in de Data Factory mogelijk niet weergegeven in het Hallo-presentatie. We toevoegen continu meer mogelijkheden tooAzure Data Factory. We toevoegen continu meer mogelijkheden tooAzure Data Factory. We zullen deze updates opnemen in Hallo vergelijking van gegevens integratietechnologieën van Microsoft enige tijd later dit jaar.   

## <a name="activities---faq"></a>Activiteiten - Veelgestelde vragen
### <a name="what-are-hello-different-types-of-activities-you-can-use-in-a-data-factory-pipeline"></a>Wat zijn de verschillende soorten activiteiten die kunt u in een Data Factory-pijplijn Hallo?
* [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) toomove gegevens.
* [Activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) tooprocess/transformatie-gegevens.

### <a name="when-does-an-activity-run"></a>Wanneer wordt een activiteit uitgevoerd?
Hallo **beschikbaarheid** configuratie-instelling in Hallo uitvoer gegevenstabel bepaalt wanneer Hallo activiteit wordt uitgevoerd. Als invoergegevenssets worden opgegeven, Hallo activiteit controleert of alle afhankelijkheden van Hallo invoergegevens is voldaan (dat wil zeggen, **gereed** status) voordat het wordt gestart.

## <a name="copy-activity---faq"></a>Kopieeractiviteit - Veelgestelde vragen
### <a name="is-it-better-toohave-a-pipeline-with-multiple-activities-or-a-separate-pipeline-for-each-activity"></a>Is het beter toohave een pijplijn met meerdere activiteiten of een afzonderlijke pijplijn voor elke activiteit?
Pijplijnen moeten toobundle gerelateerde activiteiten. Als Hallo gegevenssets die verbinding maken met deze niet worden gebruikt door een andere activiteit buiten Hallo pijplijn, kunt u Hallo activiteiten in één pijplijn bewaren. Op deze manier u hoeft dan niet toochain pijplijn actieve perioden zodat ze met elkaar worden uitgelijnd. Bovendien Hallo integriteit van gegevens in de interne toohello pijplijn beter behouden blijft wanneer het bijwerken van de pijplijn Hallo Hallo-tabellen. Pipeline-update in wezen stopt alle Hallo activiteiten binnen Hallo pipeline, verwijdert u deze en maakt deze opnieuw. Vanuit het perspectief ontwerpen, mogelijk eenvoudiger toosee Hallo stroom van gegevens binnen Hallo gerelateerde activiteiten in een JSON-bestand voor de Hallo pijplijn.

### <a name="what-are-hello-supported-data-stores"></a>Wat zijn Hallo gegevensarchieven ondersteund?
Kopieeractiviteit in Data Factory kopieert gegevens van een gegevensarchief bron data store tooa sink. Data Factory ondersteunt Hallo gegevensarchieven te volgen. Gegevens van elke bron kan worden geschreven als tooany sink. Hoe klikt u op een data store toolearn toocopy gegevens tooand van dat archief.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Gegevens worden opgeslagen met * on-premises kan worden of op Azure IaaS en moet u tooinstall [Data Management Gateway](data-factory-data-management-gateway.md) op een op-premises/Azure IaaS-machine.

### <a name="what-are-hello-supported-file-formats"></a>Wat zijn Hallo ondersteunde bestandsindelingen?
[!INCLUDE [data-factory-file-format](../../includes/data-factory-file-format.md)]

### <a name="where-is-hello-copy-operation-performed"></a>Waar wordt de kopieerbewerking Hallo uitgevoerd?
Zie [wereldwijd beschikbare gegevensverplaatsing](data-factory-data-movement-activities.md#global) sectie voor meer informatie. Kortom, wanneer een on-premises gegevensopslag is betrokken, wordt Hallo kopieerbewerking uitgevoerd door Hallo Data Management Gateway in uw on-premises omgeving. En wanneer Hallo gegevensverplaatsing tussen twee cloud-winkels, Hallo kopieerbewerking wordt uitgevoerd op Hallo regio dichtstbijzijnde toohello sink locatie in Hallo hetzelfde Geografie.

## <a name="hdinsight-activity---faq"></a>HDInsight-activiteit - Veelgestelde vragen
### <a name="what-regions-are-supported-by-hdinsight"></a>Welke regio's worden ondersteund door HDInsight?
Zie de sectie geografische beschikbaarheid in het volgende artikel Hallo Hallo: of [HDInsight prijsinformatie][hdinsight-supported-regions].

### <a name="what-region-is-used-by-an-on-demand-hdinsight-cluster"></a>Welke regio wordt gebruikt door een HDInsight-cluster op aanvraag?
Hallo HDInsight-cluster op aanvraag wordt gemaakt in Hallo dezelfde regio waar u toobe gebruikt met Hallo cluster opgegeven Hallo-opslag bestaat.    

### <a name="how-tooassociate-additional-storage-accounts-tooyour-hdinsight-cluster"></a>Hoe tooassociate extra opslagaccounts tooyour HDInsight-cluster?
Als u uw eigen HDInsight-Cluster (BYOC - Bring Your Own Cluster) gebruikt, raadpleegt u Hallo volgende onderwerpen:

* [Met behulp van een HDInsight-Cluster met alternatieve Opslagaccounts en Metastores][hdinsight-alternate-storage]
* [Extra Storage-Accounts gebruiken met HDInsight Hive][hdinsight-alternate-storage-2]

Als u een cluster op aanvraag die is gemaakt door Hallo Data Factory-service gebruikt, geeft u de extra opslagaccounts voor Hallo HDInsight gekoppelde service zodat Hallo Data Factory-service namens jou registreren kunt. Gebruik in Hallo JSON-definitie voor de gekoppelde service van Hallo op aanvraag, **additionalLinkedServiceNames** eigenschap toospecify alternatieve opslagaccounts zoals weergegeven in de volgende JSON-codefragment Hallo:

```JSON
{
    "name": "MyHDInsightOnDemandLinkedService",
    "properties":
    {
        "type": "HDInsightOnDemandLinkedService",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "LinkedService-SampleData",
            "additionalLinkedServiceNames": [ "otherLinkedServiceName1", "otherLinkedServiceName2" ]
        }
    }
}
```
Hallo bovenstaande voorbeeld vertegenwoordigen otherLinkedServiceName1 en otherLinkedServiceName2 gekoppelde services waarvan definities bevatten referenties die Hallo HDInsight-cluster moet tooaccess alternatieve opslagaccounts.

## <a name="slices---faq"></a>Segmenten - Veelgestelde vragen
### <a name="why-are-my-input-slices-not-in-ready-state"></a>Waarom wordt mijn invoersegmenten één keer niet in de status gereed?
Een algemene fout niet tot stand **externe** eigenschap te**waar** op Hallo is invoergegevensset wanneer Hallo invoergegevens externe toohello gegevensfactory (niet geproduceerd door Hallo data factory).

In de Hallo voorbeeld te volgen, hoeft u alleen tooset **externe** tootrue op **dataset1**.  

**DataFactory1** Pipeline 1: dataset1 -> activiteit1 -> dataset2 -> activiteit2 -> dataset3 pijplijn 2: dataset3 -> activiteit3 -> dataset4

Als u een andere data factory met een pipeline waarmee dataset4 (die wordt geproduceerd door de pijplijn 2 in gegevensfactory 1) hebt, moet u dataset4 markeren als een externe gegevensset omdat Hallo gegevensset wordt geproduceerd door een andere data factory (DataFactory1, niet DataFactory2).  

**DataFactory2**    
Pijplijn 1: dataset4 -> activity4 -> dataset5

Als de externe eigenschap Hallo juist is ingesteld, moet u controleren of Hallo invoergegevens in Hallo locatie die is opgegeven in de definitie van de invoergegevensset Hallo bestaat.

### <a name="how-toorun-a-slice-at-another-time-than-midnight-when-hello-slice-is-being-produced-daily"></a>Hoe een segment op een later tijdstip dan middernacht wanneer Hallo segment dagelijks wordt geproduceerd toorun?
Gebruik Hallo **offset** eigenschap toospecify Hallo tijdstip waarop u Hallo segment toobe geproduceerd. Zie [gegevensset beschikbaarheid](data-factory-create-datasets.md#dataset-availability) sectie voor meer informatie over deze eigenschap. Hier volgt een voorbeeld van een snelle:

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
Dagelijkse segmenten beginnen bij **06: 00** in plaats van Hallo standaard middernacht.     

### <a name="how-can-i-rerun-a-slice"></a>Hoe kan ik een segment opnieuw uitvoeren?
U kunt een segment in een van de volgende manieren Hallo opnieuw uitvoeren:

* Monitor and Manage App toorerun het venster van een activiteit of segment gebruiken. Zie [geselecteerde activiteit windows opnieuw uitvoeren](data-factory-monitor-manage-app.md#perform-batch-actions) voor instructies.   
* Klik op **uitvoeren** in de opdrachtbalk Hallo op Hallo **GEGEVENSSEGMENT** blade voor Hallo segment hello Azure-portal.
* Voer **Set-AzureRmDataFactorySliceStatus** cmdlet met de Status ingesteld te**wachten** voor Hallo segment.   

    ```PowerShell
    Set-AzureRmDataFactorySliceStatus -Status Waiting -ResourceGroupName $ResourceGroup -DataFactoryName $df -TableName $table -StartDateTime "02/26/2015 19:00:00" -EndDateTime "02/26/2015 20:00:00"
    ```
Zie [Set-AzureRmDataFactorySliceStatus] [ set-azure-datafactory-slice-status] voor meer informatie over het Hallo-cmdlet.

### <a name="how-long-did-it-take-tooprocess-a-slice"></a>Hoe lang duurt tooprocess een segment?
Activiteit venster Explorer in Monitor & App beheren hoe lang geduurd tooprocess een gegevenssegment tooknow gebruiken. Zie [activiteit venster Explorer](data-factory-monitor-manage-app.md#activity-window-explorer) voor meer informatie.

U kunt ook doen Hallo in hello Azure-portal te volgen:  

1. Klik op **gegevenssets** tegel op Hallo **DATA FACTORY** blade van uw gegevensfactory.
2. Klik op specifieke gegevensset op Hallo Hallo **gegevenssets** blade.
3. Selecteer Hallo-segment dat u geïnteresseerd in uit Hallo bent **recente segmenten** lijst op Hallo **tabel** blade.
4. Klik op uitvoeren vanaf Hallo Hallo-activiteit **activiteiten bij uitvoering** lijst op Hallo **GEGEVENSSEGMENT** blade.
5. Klik op **eigenschappen** tegel op Hallo **DETAILS uitvoering van activiteit** blade.
6. U ziet Hallo **duur** veld met een waarde. Deze waarde is Hallo tijd tooprocess Hallo segment.   

### <a name="how-toostop-a-running-slice"></a>Hoe een actieve segment toostop?
Als u toostop Hallo pijplijn wordt uitgevoerd moet, kunt u [onderbreken AzureRmDataFactoryPipeline](/powershell/module/azurerm.datafactories/suspend-azurermdatafactorypipeline) cmdlet. Op dit moment stopt onderbreken Hallo pijplijn niet Hallo segment uitvoeringen die uitgevoerd worden. Wanneer Hallo in uitvoering uitvoeringen klaar bent, is geen extra segment verwerkt.

Desgewenst kunt u echt toostop alle Hallo uitvoeringen onmiddellijk zou Hallo alleen manier worden toodelete Hallo pijplijn en maak deze opnieuw. Als u toodelete Hallo pijplijn kiest, hoeft u niet toodelete tabellen en gekoppelde services door Hallo pijplijn gebruikt.

[create-factory-using-dotnet-sdk]: data-factory-create-data-factories-programmatically.md
[msdn-class-library-reference]: /dotnet/api/microsoft.azure.management.datafactories.models
[msdn-rest-api-reference]: /rest/api/datafactory/

[adf-powershell-reference]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/azurerm.datafactories
[azure-portal]: http://portal.azure.com
[set-azure-datafactory-slice-status]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/set-azurermdatafactoryslicestatus

[adf-pricing-details]: http://go.microsoft.com/fwlink/?LinkId=517777
[hdinsight-supported-regions]: http://azure.microsoft.com/pricing/details/hdinsight/
[hdinsight-alternate-storage]: http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx
[hdinsight-alternate-storage-2]: http://blogs.msdn.com/b/cindygross/archive/2014/05/05/use-additional-storage-accounts-with-hdinsight-hive.aspx

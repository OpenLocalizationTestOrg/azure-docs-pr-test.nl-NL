---
title: aaaAzure Data Factory - voorbeelden
description: Bevat informatie over de voorbeelden die worden geleverd met hello Azure Data Factory-service.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c0538b90-2695-4c4c-a6c8-82f59111f4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: aa1c15eca21b34b7bcc64358b685d7606baaf691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---samples"></a>Azure Data Factory - voorbeelden
## <a name="samples-on-github"></a>Voorbeelden op GitHub
Hallo [GitHub Azure-DataFactory opslagplaats](https://github.com/azure/azure-datafactory) bevat enkele voorbeelden waarmee u snel extra met Azure Data Factory-service (of) Hallo scripts wijzigen en deze gebruiken in de eigen toepassing. Hallo Samples\JSON map bevat JSON-codefragmenten voor veelvoorkomende scenario's.

| Voorbeeld | Beschrijving |
|:--- |:--- |
| [Overzicht van de ADF](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFWalkthrough) |Dit voorbeeld bevat een overzicht van de end-to-end voor het verwerken van logboekbestanden met Azure Data Factory tooturn gegevens uit de logboekbestanden in tooinsights. <br/><br/>In dit overzicht Hallo Data Factory-pijplijn verzamelt voorbeeld Logboeken, processen verrijkt Hallo gegevens uit logboeken met referentiegegevens en transformeert Hallo gegevens tooevaluate Hallo effectiviteit van een marketingcampagne dat onlangs is gestart. |
| [JSON-voorbeelden](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON) |Dit voorbeeld ziet u voorbeelden van JSON voor veelvoorkomende scenario's. |
| [Gegevens van de HTTP-Downloadprogramma voor het voorbeeld](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample) |In dit voorbeeld showcases downloaden van gegevens van een HTTP-eindpunt tooAzure Blob Storage met behulp van aangepaste .NET-activiteit. |
| [Cross-AppDomain punt Net activiteit voorbeeld](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |Dit voorbeeld kunt u een aangepaste .NET-activiteit die geen beperkte tooassembly-versies die worden gebruikt door Hallo ADF starten (bijvoorbeeld WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, enz.) tooauthor. |
| [R-script uitvoeren](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample) |Dit voorbeeld bevat Hallo Data Factory aangepaste activiteit die gebruikt tooinvoke RScript.exe worden kan. Dit voorbeeld werkt alleen met uw eigen HDInsight-cluster (niet op aanvraag) die al R is geïnstalleerd is. |
| [Aanroepen van de projecten Spark in HDInsight Hadoop-cluster](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/Spark) |In dit voorbeeld laat zien hoe toouse MapReduce-activiteit tooinvoke een Spark-programma. Hallo spark wordt opgehaald alleen gegevens uit een Azure Blob-container tooanother. |
| [Twitter-analyse met behulp van Azure Machine Learning Batch score berekenen voor activiteit](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-AzureMLBatchScoringActivity) |Dit voorbeeld ziet u hoe toouse AzureMLBatchScoringActivity tooinvoke een Azure Machine Learning die model voert twitter-gevoel analyse, score berekenen voorspelling enzovoort. |
| [Twitter-analyse met behulp van aangepaste activiteit](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |Dit voorbeeld ziet u hoe een aangepaste activiteit .NET-tooinvoke een Azure Machine Learning-model waarmee toouse twitter gevoel analyse, score berekenen voorspelling enzovoort. |
| [Geparameteriseerde pijplijnen voor Azure Machine Learning](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ParameterizedPipelinesForAzureML/) |Hallo voorbeeld biedt een end-to-end C# code het toodeploy N pijplijnen voor score berekenen en retraining elk met een andere regio parameter waar Hallo lijst met regio's afkomstig is van een bestand parameters.txt, dat opgenomen in dit voorbeeld is. |
| [Verwijzing voor gegevensvernieuwing voor Azure Stream Analytics-taken](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs) |Dit voorbeeld ziet u hoe toouse Azure Data Factory en Azure Stream Analytics samen toorun Hallo-query's met de gegevens en instellingen Hallo verwijzing voor referentiegegevens volgens een schema vernieuwen. |
| [Hybride-pijplijn met On-premises Hortonworks Hadoop](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HybridPipelineWithOnPremisesHortonworksHadoop) |Hallo-voorbeeld gebruikt een lokale Hadoop-cluster als een compute-doel voor het uitvoeren van taken in de Data Factory, net zoals u andere compute-doelen toevoegt zou als een HDInsight Hadoop-cluster in de cloud op basis. |
| [JSON-hulpprogramma voor conversie](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSONConversionTool) |Dit hulpprogramma kunt u tooconvert JSONs van versie voorafgaande too2015-07-01-preview toolatest of 2015-07-01-preview (standaard). |
| [U-SQL-voorbeeldbestand invoer](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/U-SQL%20Sample%20Input%20File) |Dit bestand is een voorbeeld-bestand gebruikt door een U-SQL-activiteit. |
| [Blob-bestand verwijderen](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity) | Dit voorbeeld gepresenteerd een C#-bestand dat kan worden gebruikt als onderdeel van de ADF aangepaste .net activiteit toodelete-bestanden van bron hello Azure Blob-locatie nadat het Hallo-bestanden zijn gekopieerd.|

## <a name="azure-resource-manager-templates"></a>Azure Resource Manager-sjablonen
U vindt hello Azure Resource Manager-sjablonen voor Data Factory volgen op GitHub.

| Template | Beschrijving |
| --- | --- |
| [Kopiëren van Azure Blob Storage tooAzure SQL-Database](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy) |Implementatie van deze sjabloon maakt u een Azure data factory met een pijplijn die u gegevens vanaf hello Azure blob storage toohello Azure SQL database opgegeven |
| [Kopiëren van Salesforce tooAzure Blob-opslag](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy) |Implementatie van deze sjabloon maakt u een Azure data factory met een pijplijn die u gegevens vanaf Hallo Salesforce-account toohello Azure blob-opslag opgegeven. |
| [Transformeer gegevens door het Hive-script uitvoeren op een Azure HDInsight-cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) |Implementatie van deze sjabloon maakt u een Azure data factory met een pijplijn waarmee gegevens worden omgezet door Hallo voorbeeld Hive-script uitgevoerd op een Azure HDInsight Hadoop-cluster. |

## <a name="samples-in-azure-portal"></a>De voorbeelden in Azure-portal
U kunt Hallo **steekproef pijplijnen** tegel op Hallo-startpagina van uw data factory-pijplijnen toodeploy-voorbeeld en hun bijbehorende entiteiten (gegevenssets en gekoppelde services) in de gegevensfactory tooyour.

1. Maak een gegevensfactory of open een bestaande gegevensfactory. Zie [gegevens kopiëren van Blob Storage tooSQL-Database met de Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stappen toocreate een gegevensfactory.
2. In Hallo **DATA FACTORY** blade voor Hallo data factory, klikt u op Hallo **steekproef pijplijnen** tegel.

    ![Voorbeeld pijplijnen tegel](./media/data-factory-samples/SamplePipelinesTile.png)
3. In Hallo **steekproef pijplijnen** blade, klikt u op Hallo **voorbeeld** dat u wilt dat toodeploy.

    ![Voorbeeld pijplijnen-blade](./media/data-factory-samples/SampleTile.png)
4. Configuratie-instellingen voor Hallo voorbeeld opgeven. Bijvoorbeeld: uw Azure storage-account en de accountsleutel sleutel, naam van de Azure SQL-server, database, gebruikers-ID en wachtwoord, enzovoort.

    ![Voorbeeld-blade](./media/data-factory-samples/SampleBlade.png)
5. Nadat u klaar bent met het Hallo-configuratie-instellingen opgeven, klikt u op **maken** toocreate/implementeren Hallo voorbeeld pijplijnen en gekoppelde services/tabellen die worden gebruikt door Hallo pijplijnen.
6. U ziet Hallo status van implementatie op Hallo voorbeeld tegel die u eerder hebt geklikt op Hallo **steekproef pijplijnen** blade.

    ![Implementatiestatus](./media/data-factory-samples/DeploymentStatus.png)
7. Wanneer er Hallo **implementatie is voltooid** bericht op de tegel Hallo voor Hallo voorbeeld sluiten Hallo **steekproef pijplijnen** blade.  
8. Op **DATA FACTORY** blade ziet u dat het gekoppelde services, gegevenssets en pijplijnen tooyour data factory worden toegevoegd.  

    ![Blade Gegevensfactory](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="samples-in-visual-studio"></a>Voorbeelden Visual Studio
### <a name="prerequisites"></a>Vereisten
Hallo volgende op uw computer geïnstalleerd, moet u hebben:

* Visual Studio 2013 of Visual Studio 2015
* Download de Azure SDK voor Visual Studio 2013 of Visual Studio 2015. Navigeer te[Azure-downloadpagina](https://azure.microsoft.com/downloads/) en klik op **VS 2013** of **VS 2015** in Hallo **.NET** sectie.
* Download de nieuwste Azure Data Factory-invoegtoepassing Hallo voor Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) of [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Als u Visual Studio 2013 gebruikt, kunt u Hallo-invoegtoepassing ook bijwerken Hallo volgende stappen uit als volgt: klik op het menu Hallo **hulpprogramma's** -> **uitbreidingen en Updates**  ->  **Online** -> **Visual Studio-galerie** -> **Microsoft Azure Data Factory-hulpprogramma's voor Visual Studio**  ->  **Update**.

### <a name="use-data-factory-templates"></a>Gebruik Data Factory-sjablonen
1. Klik op **bestand** hello, wijst u in menu te**nieuw**, en klik op **Project**.
2. In Hallo **nieuw Project** dialoogvenster vak, Hallo volgende stappen:

   1. Selecteer **DataFactory** onder **sjablonen**.
   2. Selecteer **Data Factory sjablonen** in het rechterdeelvenster Hallo.
   3. Voer een **naam** voor Hallo-project.
   4. Selecteer een **locatie** voor Hallo-project.
   5. Klik op **OK**.

      ![Het dialoogvenster New Project](./media/data-factory-samples/vs-new-project-adf-templates.png)
3. In Hallo **Data Factory sjablonen** dialoogvenster, selecteer Hallo voorbeeldsjabloon van Hallo **Use Case sjablonen** sectie en op **volgende**. Hallo volgende stappen maakt u met behulp van Hallo **klant profilering** sjabloon. Stappen zijn vergelijkbaar voor andere voorbeelden Hallo.

    ![Dialoogvenster voor Data Factory-sjablonen](./media/data-factory-samples/vs-data-factory-templates-dialog.png)
4. In Hallo **Data Factory-configuratie** dialoogvenster, klikt u op **volgende** op Hallo **Data Factory-basisbeginselen** pagina.
5. Op Hallo **Configure data factory** pagina, Hallo volgende stappen:
   1. Selecteer **maken van nieuwe Gegevensfactory**. U kunt ook selecteren **bestaande data factory gebruiken**.
   2. Voer een **naam** voor Hallo data factory.
   3. Selecteer Hallo **Azure-abonnement** in die u Hallo data factory toobe gemaakt wilt.
   4. Selecteer Hallo **resourcegroep** voor Hallo data factory.
   5. Selecteer Hallo **VS-West**, **VS-Oost**, of **Noord-Europa** voor Hallo **regio**.
   6. Klik op **Volgende**.
6. In Hallo **gegevensarchieven configureren** pagina, geeft u een bestaande **Azure SQL-database** en **Azure storage-account** (of) maken van database-opslag en klik op volgende.
7. In Hallo **compute configureren** pagina, Selecteer standaardwaarden en klik op **volgende**.
8. In Hallo **samenvatting** pagina, controleert u alle instellingen en klik op **volgende**.
9. In Hallo **Implementatiestatus** pagina, wacht totdat het Hallo-implementatie is voltooid en klik op **voltooien**.
10. Met de rechtermuisknop op het project in Solution Explorer Hallo en klik op **publiceren**.
11. Als u ziet **tooyour Microsoft-account aanmelden** in het dialoogvenster Geef uw referenties voor het Hallo-account met Azure-abonnement en klikt u op **aanmelden**.
12. U ziet Hallo in het dialoogvenster te volgen:

    ![Het dialoogvenster Publish](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
13. In Hallo **Configure data factory** pagina, Hallo volgende stappen:

    1. Bevestig dat **bestaande data factory gebruiken** optie.
    2. Selecteer Hallo **gegevensfactory** moest u selecteert wanneer Hallo-sjabloon gebruikt.
    3. Klik op **volgende** tooswitch toohello **Publish Items** pagina. (Druk op **tabblad** toomove buiten Hallo naam veld tooif hello **volgende** knop is uitgeschakeld.)
14. In Hallo **Publish Items** pagina, zorg ervoor dat alle Data Factory-entiteiten zijn geselecteerd en klik op Hallo **volgende** tooswitch toohello **samenvatting** pagina.     
15. Controleer Hallo samenvatting en klik op **volgende** toostart Hallo implementatie proces en bekijkt hello **Implementatiestatus**.
16. In Hallo **Implementatiestatus** pagina ziet u Hallo status van implementatieproces Hallo. Klik op Voltooien nadat het Hallo-implementatie is voltooid.

Zie [(Visual Studio) van uw eerste gegevensfactory bouwen](data-factory-build-your-first-pipeline-using-vs.md) voor meer informatie over het gebruik van Visual Studio tooauthor Data Factory-entiteiten en publiceren van tooAzure.          

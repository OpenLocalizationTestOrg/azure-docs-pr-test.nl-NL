---
title: 'Data Factory-zelfstudie: eerste gegevens pijplijn | Microsoft Docs'
description: Deze Azure Data Factory-zelfstudie ziet u hoe toocreate en planning een gegevensfactory dat gegevens met Hive verwerkt een op een Hadoop-cluster script.
services: data-factory
keywords: Azure data factory zelfstudie, hadoop-cluster, hadoop hive
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.assetid: 81f36c76-6e78-4d93-a3f2-0317b413f1d0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: ed9c0ade4500d4ac1f7c2c2312c1fa675e0b1f02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-pipeline-tootransform-data-using-hadoop-cluster"></a>Zelfstudie: Bouw uw eerste pijplijn tootransform gegevens met Hadoop-cluster
> [!div class="op_single_selector"]
> * [Overzicht en vereisten](data-factory-build-your-first-pipeline.md)
> * [Azure Portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager-sjabloon](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)

In deze zelfstudie bouwt u uw eerste Azure-gegevensfactory met een pipeline gegevens. Hallo pijplijn getransformeerd invoergegevens door het Hive-script uitvoeren op gegevens in een Azure HDInsight (Hadoop) cluster tooproduce uitvoer.  

Dit artikel bevat een overzicht en vereisten voor Hallo zelfstudie. Nadat u Hallo vereisten hebt voltooid, kunt u doen met een van de volgende hulpprogramma's / SDK's Hallo Hallo-zelfstudie: Azure portal, Visual Studio, PowerShell, Resource Manager-sjabloon, REST-API. Selecteer een van de opties Hallo in Hallo vervolgkeuzelijst aan Hallo begin (of) koppelingen aan Hallo einde van dit artikel toodo Hallo zelfstudie met een van deze opties.    

## <a name="tutorial-overview"></a>Overzicht van de zelfstudie
In deze zelfstudie maakt uitvoeren u Hallo stappen:

1. Maak een **gegevensfactory**. Een gegevensfactory kan één of meer gegevenspijplijnen verplaatsen en transformeer gegevens bevatten. 

    In deze zelfstudie maakt u een pijplijn in Hallo data factory. 
2. Maak een **pijplijn**. Een pijplijn kan een of meer activiteiten bevatten (bijvoorbeeld: kopieeractiviteit, HDInsight Hive-activiteit). Dit voorbeeld gebruikt Hallo HDInsight Hive-activiteit die een Hive-script wordt uitgevoerd op een HDInsight Hadoop-cluster. Hallo script maakt eerst een tabel die verwijzingen Hallo onbewerkte web logboekgegevens opgeslagen in Azure blob storage en vervolgens partities onbewerkte gegevens Hallo op jaar en maand.

    In deze zelfstudie gebruikt Hallo pijplijn Hallo Hive-activiteit tootransform gegevens door een Hive-query uitgevoerd op een Azure HDInsight Hadoop-cluster. 
3. Maak **gekoppelde services**. Een gekoppelde service toolink maakt u een gegevensarchief of een compute-service toohello data factory. Een gegevensarchief zoals Azure Storage bevat invoer-en uitvoergegevens van activiteiten in Hallo pijplijn. Een compute-service zoals HDInsight Hadoop-cluster processen/transformaties gegevens.

    In deze zelfstudie maakt u twee gekoppelde services: **Azure Storage** en **Azure HDInsight**. Hello Azure Storage gekoppelde service wordt een Azure Storage-Account van de Hallo invoer-en uitvoergegevens toohello data factory. Azure HDInsight gekoppelde service wordt een Azure HDInsight-cluster dat is gebruikt tootransform gegevens toohello data factory. 
3. Maak **gegevenssets** voor invoer en uitvoer. Een invoergegevensset vertegenwoordigt Hallo invoer voor een activiteit in de pijplijn Hallo en een uitvoergegevensset Hallo uitvoer voor Hallo activiteit vertegenwoordigt.

    In deze zelfstudie, Hallo invoer en uitvoer gegevenssets Geef locaties van de invoer en uitvoergegevens in Azure Blob Storage Hallo. Hallo gekoppelde Azure Storage-service wordt aangegeven wat Azure Storage-Account wordt gebruikt. Een invoergegevensset geeft aan waar Hallo invoerbestanden zich bevinden en een uitvoergegevensset geeft aan waar de uitvoerbestanden Hallo worden geplaatst. 


Zie [inleiding tooAzure Data Factory](data-factory-introduction.md) artikel voor een gedetailleerd overzicht van Azure Data Factory.
  
Hier volgt Hallo **diagramweergave** van Hallo voorbeeld-gegevensfactory u in deze zelfstudie bouwt. **MyFirstPipeline** heeft één activiteit van het type Hive die verbruikt **AzureBlobInput** dataset als invoer en produceert **AzureBlobOutput** gegevensset als uitvoer. 

![Zelfstudie voor de Data Factory-diagramweergave](media/data-factory-build-your-first-pipeline/data-factory-tutorial-diagram-view.png)


In deze zelfstudie **inputdata** map Hallo **adfgetstarted** Azure blob-container bevat één bestand met de naam input.log. Dit logboekbestand bevat vermeldingen van drie maanden: januari, februari en maart 2016. Hier vindt u voor elke maand Hallo voorbeeld rijen in het invoerbestand Hallo. 

```
2016-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871 
2016-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2016-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

Wanneer het Hallo-bestand wordt verwerkt door de pijplijn Hallo met HDInsight Hive-activiteit, uitgevoerd Hallo activiteit een Hive-script op Hallo HDInsight-cluster partities voert gegevens op jaar en maand. Hallo script maakt drie uitvoermappen met een bestand met vermeldingen van elke maand.  

```
adfgetstarted/partitioneddata/year=2016/month=1/000000_0
adfgetstarted/partitioneddata/year=2016/month=2/000000_0
adfgetstarted/partitioneddata/year=2016/month=3/000000_0
```

Vanaf Hallo voorbeeld regels hierboven weergegeven, hello eerst een (met 2016-01-01) geschreven toohello 000000_0 bestand in de maand Hallo = 1 map. Op deze manier hello tweede is geschreven toohello bestand in Hallo maand = 2, map en Hallo derde een toohello bestand is geschreven in Hallo maand = 3 map.  

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, hebt u Hallo volgende vereisten:

1. U moet beschikken over een **Azure-abonnement**. Als u geen Azure-abonnement hebt, kunt u in enkele minuten een gratis proefaccount maken. Zie Hallo [gratis proefversie van](https://azure.microsoft.com/pricing/free-trial/) artikel over hoe u een gratis proefaccount kunt verkrijgen.
2. **Azure Storage** – u een algemene standaard Azure storage-account gebruiken voor het opslaan van Hallo gegevens in deze zelfstudie. Als u een algemene standaard Azure storage-account niet hebt, raadpleegt u Hallo [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) artikel. Nadat u Hallo storage-account hebt gemaakt, noteer Hallo **accountnaam** en **toegangssleutel**. Zie [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys) (Toegangssleutels voor opslag weergeven, kopiëren en opnieuw genereren).
3. Downloaden en bekijken Hallo Hive query-bestand (**HQL**) te vinden op: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql). Deze query transformeert invoergegevens tooproduce uitvoergegevens. 
4. Downloaden en bekijken Hallo voorbeeldinvoerbestand (**input.log**) te vinden op: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)
5. Maak een blobcontainer met de naam **adfgetstarted** in uw Azure-blobopslag. 
6. Uploaden **partitionweblogs.hql** bestand toohello **script** map in Hallo **adfgetstarted** container. Gebruik hulpprogramma's zoals [Microsoft Azure Storage Explorer](http://storageexplorer.com/). 
7. Uploaden **input.log** bestand toohello **inputdata** map in Hallo **adfgetstarted** container. 

Nadat u Hallo vereisten hebt voltooid, selecteert u een extra/SDK's toodo Hallo zelfstudie Hallo: 

- [Azure Portal](data-factory-build-your-first-pipeline-using-editor.md)
- [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
- [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
- [Resource Manager-sjabloon](data-factory-build-your-first-pipeline-using-arm.md)
- [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)

Azure-portal en Visual Studio bieden GUI-methode van het bouwen van uw gegevensfactory. Terwijl opties PowerShell, Resource Manager-sjabloon en de REST-API biedt script of programma manier van het bouwen van uw gegevensfactory.

> [!NOTE]
> Hallo gegevens pijplijn in deze zelfstudie getransformeerd invoergegevens tooproduce uitvoergegevens. Er worden geen gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats. Voor een zelfstudie over het toocopy van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: gegevens kopiëren van Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> U kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit. Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md) voor gedetailleerde informatie. 





  

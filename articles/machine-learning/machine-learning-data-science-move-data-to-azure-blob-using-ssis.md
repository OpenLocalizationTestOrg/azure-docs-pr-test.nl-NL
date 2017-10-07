---
title: aaaMove gegevens tooor uit Azure Blob Storage met SSIS-connectors | Microsoft Docs
description: Verplaats gegevens tooor uit Azure Blob Storage met SSIS-connectors.
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 96a1b5fb-34d1-4b9b-8d99-2bb8289e0398
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 15068af1c69f11e74e109ee5ae2b9f1a674ea388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooor-from-azure-blob-storage-using-ssis-connectors"></a>Verplaatsen van gegevens tooor uit Azure Blob Storage met SSIS-connectors
Hallo [SQL Server Integration Services Feature Pack voor Azure](https://msdn.microsoft.com/library/mt146770.aspx) onderdelen tooconnect tooAzure, overdracht van gegevens tussen Azure en on-premises gegevensbronnen en gegevens over het installatieproces opgeslagen in Azure biedt.

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

Nadat klanten on-premises gegevens naar de cloud hello verplaatst hebt, kunnen ze het willen openen van een Azure-service tooleverage Hallo kracht van Hallo suite Azure technologieën. Worden kan gebruikt, bijvoorbeeld in Azure Machine Learning of op een HDInsight-cluster.

Dit is doorgaans worden de eerste stap Hallo voor Hallo [SQL](machine-learning-data-science-process-sql-walkthrough.md) en [HDInsight](machine-learning-data-science-process-hive-walkthrough.md) scenario's.

Zie voor een beschrijving van de canonieke scenario's die gebruikmaken van SSIS tooaccomplish business voorkomen in hybride gegevens integratiescenario's moet, [doen meer met SQL Server Integration Services Feature Pack voor Azure](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) blog.

> [!NOTE]
> Voor een volledige inleiding tooAzure blob-opslag te verwijzen[basisbeginselen van Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) en te[Azure Blob-Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Vereisten
tooperform hello taken beschreven in dit artikel, moet u een Azure-abonnement en instellen van Azure storage-account hebben. U moet weten van uw Azure storage-account en de accountsleutel sleutel tooupload of gegevens te downloaden.

* tooset van een **Azure-abonnement**, Zie [gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).
* Voor instructies over het maken van een **opslagaccount** en voor het ophalen van account en belangrijke informatie, Zie [over Azure storage-accounts](../storage/common/storage-create-storage-account.md).

Hallo toouse **SSIS-connectors**, dient u te downloaden:

* **SQL Server 2014 of 2016-standaard (of hoger)**: Install SQL Server Integration Services bevat.
* **Microsoft SQL Server 2014 of 2016 Integration Services Feature Pack voor Azure**: deze kunnen worden gedownload, respectievelijk van Hallo [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366) en [integratie van SQL Server 2016 Services](https://www.microsoft.com/download/details.aspx?id=49492) pagina's.

> [!NOTE]
> SSIS met SQL Server is geïnstalleerd, maar is niet opgenomen in Hallo Express versie. Zie voor informatie over welke toepassingen zijn opgenomen in de verschillende edities van SQL Server, [edities van SQL Server](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)
> 
> 

Zie voor trainingsmateriaal op SSIS, [handen op Training voor SSIS](http://www.microsoft.com/download/details.aspx?id=20766)

Voor meer informatie over tooget up-en-uitgevoerd met behulp van SISS toobuild eenvoudig extractie, transformatie en laden (ETL)-pakketten, Zie [SSIS-zelfstudie: maken van een eenvoudige ETL-pakket](https://msdn.microsoft.com/library/ms169917.aspx).

## <a name="download-nyc-taxi-dataset"></a>Downloaden van de NYC Taxi gegevensset
Hallo beschreven hier gebruikt u een openbaar gegevensset--hello [NYC Taxi reizen](http://www.andresmh.com/nyctaxitrips/) gegevensset. Hallo-gegevensset bestaat uit ongeveer 173 miljoen taxi ritjes in NYC Hallo jaar 2013. Er zijn twee soorten gegevens: reis details gegevens en tarief gegevens. Als er een bestand voor elke maand is, hebben we 24 bestanden in alle die elk ongeveer 2GB gedecomprimeerd is.

## <a name="upload-data-tooazure-blob-storage"></a>Uploaden van gegevens tooAzure blob-opslag
toomove-gegevens met behulp van Hallo SSIS-functiepakket van lokale tooAzure blob-opslag, gebruiken we een exemplaar van Hallo [ **Azure Blob uploaden taak**](https://msdn.microsoft.com/library/mt146776.aspx), hier weergegeven:

![Configureer-gegevens-wetenschappelijke-vm](./media/machine-learning-data-science-move-data-to-azure-blob-using-ssis/ssis-azure-blob-upload-task.png)

Hallo-parameters die taak gebruikt Hallo worden hier beschreven:

| Veld | Beschrijving |
| --- | --- |
| **AzureStorageConnection** |Hiermee geeft u een bestaande Azure Storage Connection Manager of maakt u een nieuwe die verwijst tooan Azure storage-account dat toowhere Hallo blob bestanden wijst worden gehost. |
| **BlobContainer** |Geeft de naam Hallo van Hallo blob-container die bestanden geüpload Hallo als blobs bevatten. |
| **BlobDirectory** |Hiermee geeft u Hallo blob directory waarin het geüploade bestand Hallo is opgeslagen als een blok-blob. Hallo blob directory is een virtuele hiërarchische structuur. Als Hallo blob al bestaat, it ia vervangen. |
| **LocalDirectory** |Hiermee geeft u Hallo lokale directory met Hallo bestanden toobe geüpload. |
| **Bestandsnaam** |Hiermee geeft u een naam filter tooselect bestanden met de opgegeven naampatroon Hallo. Bijvoorbeeld: MySheet\*.xls\* bevat bestanden zoals MySheet001.xls en MySheetABC.xlsx |
| **TimeRangeFrom/TimeRangeTo** |Hiermee geeft u een filter tijdsbereik. Bestanden die zijn gewijzigd na *TimeRangeFrom* en vóór *TimeRangeTo* zijn opgenomen. |

> [!NOTE]
> Hallo **AzureStorageConnection** referenties moeten de juiste toobe en Hallo **BlobContainer** moet bestaan voordat Hallo overdracht wordt uitgevoerd.
> 
> 

## <a name="download-data-from-azure-blob-storage"></a>Downloaden van gegevens uit Azure blob-opslag
toodownload gegevens uit Azure blob storage tooon lokale opslag met SSIS, gebruikt u een exemplaar van Hallo [Azure Blob uploaden taak](https://msdn.microsoft.com/library/mt146779.aspx).

## <a name="more-advanced-ssis-azure-scenarios"></a>Meer geavanceerde scenario's voor SSIS-Azure
Hallo SSIS-functiepakket kunt u complexere stromen toobe verwerkt door taken voor pakketten samen. Hallo blob-gegevens kan bijvoorbeeld feed rechtstreeks in een HDInsight-cluster, waarvan de uitvoer terug tooa blob en vervolgens tooon lokale opslag kan worden gedownload. SSIS kunt Hive en Pig-taken uitvoeren op een HDInsight-cluster met extra SSIS-connectors:

* een Hive-script in een Azure HDInsight-cluster met SSIS, gebruik toorun [Azure HDInsight Hive-taak](https://msdn.microsoft.com/library/mt146771.aspx).
* een Pig-script op basis van een Azure HDInsight-cluster met SSIS, gebruik toorun [Azure HDInsight Pig-taak](https://msdn.microsoft.com/library/mt146781.aspx).


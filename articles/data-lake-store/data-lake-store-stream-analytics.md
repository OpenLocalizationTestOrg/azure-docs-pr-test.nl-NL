---
title: aaaStream gegevens van de Stream Analytics in Data Lake Store | Microsoft Docs
description: Azure Stream Analytics toostream gegevens worden gebruikt in Azure Data Lake Store
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a>Gegevens streamen van Azure Storage Blob naar Data Lake Store met behulp van Azure Stream Analytics
In dit artikel leert u hoe toouse Azure Data Lake opslaan als uitvoer voor een Azure Stream Analytics-taak. In dit artikel ziet u een eenvoudig scenario die gegevens uit een Azure Storage-blob (invoer leest) en schrijfbewerkingen Hallo data tooData Lake Store (uitvoer).

> [!NOTE]
> Op dit moment kunt maken en de configuratie van Data Lake Store voert voor Stream Analytics wordt alleen ondersteund in Hallo [klassieke Azure-Portal](https://manage.windowsazure.com). Sommige onderdelen van deze zelfstudie wordt daarom Hallo klassieke Azure-Portal gebruiken.
>
>

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).

* **Azure Storage-account**. U gebruikt een blob-container van deze account tooinput-gegevens voor een Stream Analytics-taak. Voor deze zelfstudie wordt ervan uitgegaan er een opslagaccount die is aangeroepen **storageforasa** en een container in Hallo rekening met de naam **storageforasacontainer**. Nadat u Hallo container hebt gemaakt, uploadt u een voorbeeld gegevens bestand tooit. 
  
* **Azure Data Lake Store-account**. Volg de instructies Hallo voor [aan de slag met Azure Data Lake Store met Azure Portal Hallo](data-lake-store-get-started-portal.md). Stel u hebt een Data Lake Store-account genoemd **asadatalakestore**. 

## <a name="create-a-stream-analytics-job"></a>Een Stream Analytics-taak maken
U begint met het maken van een Stream Analytics-taak die bestaat uit een invoerbron en een bestemming voor de uitvoer. Voor deze zelfstudie Hallo-bron is een Azure blob-container en Hallo bestemming is Data Lake Store.

1. Meld u aan bij toohello [Azure Portal](https://portal.azure.com).

2. Klik in het linkerdeelvenster hello, **Stream Analytics-taken**, en klik vervolgens op **toevoegen**.

    ![Maken van een Stream Analytics-taak](./media/data-lake-store-stream-analytics/create.job.png "een Stream Analytics-taak maken")

    > [!NOTE]
    > Zorg ervoor dat u taak maken in Hallo dezelfde regio bevinden als het Hallo-opslagaccount of u, worden extra kosten van het verplaatsen van gegevens tussen regio's.
    >

## <a name="create-a-blob-input-for-hello-job"></a>Een Blob-invoer voor Hallo-taak maken

1. Open Hallo-pagina voor Hallo Stream Analytics-taak in het linkerdeelvenster Hallo klikt u op Hallo **invoer** tabblad en klik vervolgens op **toevoegen**.

    ![Toevoegen van een taak invoer tooyour](./media/data-lake-store-stream-analytics/create.input.1.png "een taak invoer tooyour toevoegen")

2. Op Hallo **nieuwe invoer** blade Hallo volgende waarden bevatten.

    ![Toevoegen van een taak invoer tooyour](./media/data-lake-store-stream-analytics/create.input.2.png "een taak invoer tooyour toevoegen")

    * Voor **invoer alias**, voer een unieke naam voor Hallo taak invoer.
    * Voor **gegevensbrontype**, selecteer **gegevensstroom**.
    * Voor **bron**, selecteer **Blob storage**.
    * Voor **abonnement**, selecteer **gebruik blob storage uit het huidige abonnement**.
    * Voor **opslagaccount**, selecteer Hallo storage-account dat u hebt gemaakt als onderdeel van Hallo vereisten. 
    * Voor **Container**, selecteer Hallo-container die u hebt gemaakt in Hallo storage-account geselecteerd.
    * Voor **gebeurtenis serialisatie-indeling**, selecteer **CSV**.
    * Voor **scheidingsteken**, selecteer **tabblad**.
    * Voor **codering**, selecteer **UTF-8**.

    Klik op **Create**. Hallo portal nu voegt Hallo invoer en Hallo verbinding tooit wordt getest.


## <a name="create-a-data-lake-store-output-for-hello-job"></a>De uitvoer van een Data Lake Store voor Hallo-taak maken

1. Open de pagina Hallo voor Hallo Stream Analytics-taak, klikt u op Hallo **uitvoer** tabblad en klik vervolgens op **toevoegen**.

    ![Toevoegen van een taak van uitvoer tooyour](./media/data-lake-store-stream-analytics/create.output.1.png "een tooyour uitvoer taak toevoegen")

2. Op Hallo **nieuwe uitvoer** blade Hallo volgende waarden bevatten.

    ![Toevoegen van een taak van uitvoer tooyour](./media/data-lake-store-stream-analytics/create.output.2.png "een tooyour uitvoer taak toevoegen")

    * Voor **uitvoeraliassen**, voer een een unieke naam voor de taakuitvoer Hallo. Dit is een beschrijvende naam die is gebruikt in query's toodirect Hallo query uitvoer toothis Data Lake Store.
    * Voor **Sink**, selecteer **Data Lake Store**.
    * U zult de vraag tooauthorize toegang tot tooData Lake Store-account. Klik op **autoriseren**.

3. Op Hallo **nieuwe uitvoer** blade tooprovide Hallo waarden na te gaan.

    ![Toevoegen van een taak van uitvoer tooyour](./media/data-lake-store-stream-analytics/create.output.3.png "een tooyour uitvoer taak toevoegen")

    * Voor **accountnaam**, Hallo u al waar u Hallo taak uitvoer toobe verzonden gemaakt naar Data Lake Store-account selecteren.
    * Voor **pad voorvoegselpatroon**, voer een pad dat wordt gebruikt bestand toowrite uw bestanden binnen Hallo Data Lake Store-account opgegeven.
    * Voor **datumnotatie**, als u een datum-token in Hallo voorvoegsel pad gebruikt, kunt u Hallo datumnotatie waarin de bestanden zijn ingedeeld.
    * Voor **tijdnotatie**, als u een token tijd in het pad naar het voorvoegsel van de hello gebruikt, geef Hallo tijdnotatie waarin de bestanden zijn ingedeeld.
    * Voor **gebeurtenis serialisatie-indeling**, selecteer **CSV**.
    * Voor **scheidingsteken**, selecteer **tabblad**.
    * Voor **codering**, selecteer **UTF-8**.
    
    Klik op **Create**. Hallo portal nu Hallo uitvoer toegevoegd en Hallo verbinding tooit wordt getest.
    
## <a name="run-hello-stream-analytics-job"></a>Hallo Stream Analytics-taak uitgevoerd

1. toorun een Stream Analytics-taak, moet u een query uitvoeren vanaf Hallo **Query** tabblad. U kunt voor deze zelfstudie Hallo voorbeeldquery uitvoeren door te vervangen Hallo tijdelijke aanduidingen door Hallo taak aliassen invoer en uitvoer, zoals wordt weergegeven in onderstaande Hallo schermafbeelding.

    ![Voer query](./media/data-lake-store-stream-analytics/run.query.png "query uitvoeren")

2. Klik op **opslaan** vanaf de bovenkant Hallo van welkomstscherm en vervolgens van Hallo **overzicht** tabblad **Start**. Selecteer in het dialoogvenster Hallo **aangepaste tijd**, en stel vervolgens Hallo huidige datum en tijd.

    ![Taaktijd instellen](./media/data-lake-store-stream-analytics/run.query.2.png "taaktijd instellen")

    Klik op **Start** toostart Hallo taak. Tooa paar minuten toostart Hallo taak kan duren.

3. tootrigger hello toopick Hallo taakgegevens van Hallo-blob kopiëren een sample data bestand toohello blob-container. U krijgt een voorbeeldgegevensbestand van Hallo [Azure Data Lake Git-opslagplaats](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt). Kopieer Hallo-bestand voor deze zelfstudie **vehicle1_09142014.csv**. U kunt verschillende clients, zoals [Azure Opslagverkenner](http://storageexplorer.com/), tooupload gegevens tooa blob-container.

4. Van Hallo **overzicht** tabblad onder **bewaking**, Zie hoe Hallo gegevens is verwerkt.

    ![Monitor taak](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor taak")

5. Ten slotte kunt u controleren dat Hallo taak uitvoergegevens beschikbaar in Data Lake Store-account voor Hallo is. 

    ![Controleer of de uitvoer](./media/data-lake-store-stream-analytics/run.query.4.png "uitvoer controleren")

    In Hallo Data Explorer deelvenster ziet u dat Hallo uitvoer is geschreven tooa pad als opgegeven in Hallo uitvoerinstellingen Data Lake Store (`streamanalytics/job/output/{date}/{time}`).  

## <a name="see-also"></a>Zie ook
* [Maken van een HDInsight-cluster toouse Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

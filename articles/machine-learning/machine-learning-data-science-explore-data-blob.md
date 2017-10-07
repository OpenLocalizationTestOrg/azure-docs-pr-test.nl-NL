---
title: aaaExplore gegevens in Azure blob-opslag met Pandas | Microsoft Docs
description: Hoe tooexplore gegevens die zijn opgeslagen in Azure blob-container met behulp van Pandas.
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: feaa9e54-01e0-48c8-a917-1eba0f9d9ec7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 28f3c0aebf2300006066c4b19dcb1f0a76a1deb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a>Met Pandas gegevens verkennen in Azure Blok-opslag
Dit document bevat informatie over hoe tooexplore gegevens die zijn opgeslagen in Azure blob-container met behulp van [Pandas](http://pandas.pydata.org/) Python-pakket.

Hallo volgende **menu** tootopics waarin wordt beschreven hoe toouse hulpprogramma's voor tooexplore gegevens uit verschillende omgevingen voor opslag is gekoppeld. Deze taak is een stap in Hallo [gegevens wetenschap proces]().

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u hebt:

* Een Azure storage-account gemaakt. Als u instructies nodig hebt, raadpleegt u [een Azure Storage-account maken](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Uw gegevens opgeslagen in een Azure blob storage-account. Als u instructies nodig hebt, raadpleegt u [Moving gegevens tooand uit Azure Storage](../storage/common/storage-moving-data.md)

## <a name="load-hello-data-into-a-pandas-dataframe"></a>Hallo gegevens laden in een DataFrame Pandas
tooexplore en manipuleren van een gegevensset, moet eerst worden gedownload vanuit het Hallo blob bron tooa lokale bestand, die vervolgens kan worden geladen in een DataFrame Pandas. Hier volgen Hallo stappen toofollow voor deze procedure:

1. Hallo gegevens downloaden vanaf Azure blob met Hallo Python-codevoorbeeld met behulp van blob-service te volgen. Hallo-variabele in Hallo na de code die uw specifieke waarden vervangt: 
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        LOCALFILENAME= <local_file_name>        
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        #download from blob
        t1=time.time()
        blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
        blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILENAME)
        t2=time.time()
        print(("It takes %s seconds toodownload "+blobname) % (t2 - t1))
2. Hallo-gegevens lezen in een Pandas gegevens tijdskader van Hallo gedownload bestand.
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

Nu u bent gereed tooexplore Hallo gegevens en genereren van de functies voor deze gegevensset.

## <a name="blob-dataexploration"></a>Voorbeelden van gegevensverkenning met Pandas
Hier volgen enkele voorbeelden van de manieren tooexplore-gegevens met behulp van Pandas:

1. Hallo inspecteren **aantal rijen en kolommen** 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. **Inspecteer** eerste of laatste paar Hallo **rijen** in Hallo gegevensset te volgen:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Controleer de Hallo **gegevenstype** elke kolom is geïmporteerd als het gebruik van de volgende voorbeeldcode Hallo
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Controleer de Hallo **elementaire statistieken** voor Hallo kolommen in gegevensset als volgt Hallo
   
        dataframe_blobdata.describe()
5. Bekijkt hello aantal items voor elke waarde in de kolom als volgt
   
        dataframe_blobdata['<column_name>'].value_counts()
6. **Ontbrekende waarden tellen** versus werkelijke aantal vermeldingen in elke kolom met de volgende voorbeeldcode Hallo Hallo
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Als u hebt **ontbrekende waarden** voor een specifieke kolom in Hallo gegevens verwijderen ze als volgt:
   
     dataframe_blobdata_noNA dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape =
   
   Er is een andere manier tooreplace ontbrekende waarden met Hallo modusfunctie:
   
     dataframe_blobdata_mode dataframe_blobdata.fillna = ({< column_name >: .mode()[0]}) dataframe_blobdata ['< column_name >"]        
8. Maak een **histogram** getekend met een variabele aantal opslaglocaties tooplot Hallo distributie van een variabele    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Bekijk **correlaties** tussen variabelen met een scatterplot of functie van de ingebouwde correlation Hallo
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()


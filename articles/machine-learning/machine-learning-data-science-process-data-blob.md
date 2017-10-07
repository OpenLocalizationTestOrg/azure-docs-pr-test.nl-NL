---
title: aaaProcess Azure blob-gegevens met geavanceerde analyses | Microsoft Docs
description: Procesgegevens in Azure Blob-opslag.
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8a59078-91d3-4440-b85c-430363c3f4d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5911d4211c4135680555a8cdd99e745499a24215
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Azure blob-gegevens met geavanceerde analyses verwerken
Dit document bevat informatie over gegevens verkennen en genereren van de functies van de gegevens die zijn opgeslagen in Azure Blob-opslag. 

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Hallo gegevens laden in een frame Pandas-gegevens
In de volgorde tooexplore en manipuleren van een gegevensset, deze moet worden gedownload uit Hallo blob tooa lokale bronbestand die vervolgens kan worden geladen in een Pandas gegevensframe. Hier volgen Hallo stappen toofollow voor deze procedure:

1. Hallo gegevens downloaden vanaf Azure blob met Hallo Python voorbeeldcode met behulp van blob-service te volgen. Hallo-variabele in het Hallo-code hieronder vervangen door uw eigen specifieke waarden: 
   
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

## <a name="blob-dataexploration"></a>Gegevensverkenning
Hier volgen enkele voorbeelden van de manieren tooexplore-gegevens met behulp van Pandas:

1. Hallo aantal rijen en kolommen controleren 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. Hallo eerst controleren of de laatste paar rijen in dataset Hallo zoals hieronder:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Hallo-gegevenstype die elke kolom is geïmporteerd als het gebruik van de volgende voorbeeldcode Hallo controleren
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Hallo elementaire statistieken voor kolommen in gegevensset Hallo Hallo als volgt controleren
   
        dataframe_blobdata.describe()
5. Bekijkt hello aantal items voor elke waarde in de kolom als volgt
   
        dataframe_blobdata['<column_name>'].value_counts()
6. Ontbrekende waarden versus werkelijke aantal vermeldingen in elke kolom met de volgende voorbeeldcode Hallo Hallo tellen
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Als u ontbrekende waarden voor een specifieke kolom in Hallo gegevens hebt, kunt u ze als volgt verwijderen:
   
     dataframe_blobdata_noNA dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape =
   
   Er is een andere manier tooreplace ontbrekende waarden met Hallo modusfunctie:
   
     dataframe_blobdata_mode dataframe_blobdata.fillna = ({< column_name >: .mode()[0]}) dataframe_blobdata ['< column_name >"]        
8. Histogram tekent met variabele aantal opslaglocaties tooplot Hallo distributie van een variabele maken    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Bekijk correlatie tussen variabelen met een scatterplot of functie van de ingebouwde correlation Hallo
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <a name="blob-featuregen"></a>Functie generatie
Functies met behulp van Python als volgt kan worden gegenereerd:

### <a name="blob-countfeature"></a>Indicatorwaarde op basis van functie generatie
Categorische functies kunnen als volgt worden gemaakt:

1. Hallo-verdeling van Hallo categorische kolom controleren:
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. Indicatorwaarden voor elk van de kolomwaarden Hallo genereren
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. Hallo indicatorkolom met de oorspronkelijke gegevensframe Hallo koppelen 
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. Hallo oorspronkelijke variabele zelf verwijderen:
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <a name="blob-binningfeature"></a>Met binning functie generatie
Voor het genereren van binned functies gaan we als volgt:

1. Een reeks van kolommen toobin een numerieke kolom toevoegen
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. Met binning tooa reeks Boole-variabelen converteren
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. Ten slotte back Join Hallo dummy-variabelen-toohello oorspronkelijke gegevensframe
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <a name="sql-featuregen"></a>Het schrijven van gegevens back-tooAzure blob en gebruiken in Azure Machine Learning
Nadat u hebt Hallo gegevens verkend en Hallo benodigde onderdelen gemaakt, kunt u Hallo gegevens uploaden (actieve of featurized) tooan Azure blob- en deze wordt gebruikt in Azure Machine Learning met Hallo stappen te volgen: Houd er rekening mee dat extra functies kunnen worden gemaakt in Hallo Azure Machine Learning Studio ook. 

1. Hallo gegevens frame toolocal-bestand schrijven
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Hallo gegevens tooAzure blob als volgt uploaden:
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. Nu Hallo gegevens kunnen worden gelezen vanuit Hallo blob met Azure Machine Learning Hallo [importgegevens] [ import-data] module, zoals wordt weergegeven in het welkomstscherm hieronder:

![lezer blob][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/


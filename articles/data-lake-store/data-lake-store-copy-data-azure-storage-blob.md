---
title: aaaCopy gegevens uit Azure Storage-Blobs in Data Lake Store | Microsoft Docs
description: AdlCopy hulpprogramma toocopy gegevens gebruiken uit Azure Storage Blobs tooData Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: dc273ef8-96ef-47a6-b831-98e8a777a5c1
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: a3d4172eaefe7395cdef2fff72691bd70f642b78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-from-azure-storage-blobs-toodata-lake-store"></a>Gegevens kopiëren van Azure Storage Blobs tooData Lake Store
> [!div class="op_single_selector"]
> * [DistCp gebruiken](data-lake-store-copy-data-wasb-distcp.md)
> * [AdlCopy gebruiken](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Azure Data Lake Store biedt een opdrachtregelprogramma [AdlCopy](http://aka.ms/downloadadlcopy), toocopy gegevens uit de volgende bronnen Hallo:

* Uit Azure Storage-Blobs in Data Lake Store. U kunt AdlCopy toocopy gegevens van Data Lake Store tooAzure Storage-blobs niet gebruiken.
* Tussen twee Azure Data Lake Store-accounts.

U kunt ook Hallo AdlCopy hulpprogramma gebruiken in twee verschillende modi:

* **Zelfstandige**, waarbij Hallo hulpprogramma Data Lake Store resources tooperform Hallo taak gebruikt.
* **Gebruik van een Data Lake Analytics-account**, waarbij Hallo eenheden tooyour Data Lake Analytics-account toegewezen gebruikte tooperform Hallo kopieerbewerking zijn. U kunt de toouse deze optie wanneer u op zoek bent tooperform Hallo kopie taken op een voorspelbare wijze.

## <a name="prerequisites"></a>Vereisten
Voordat u dit artikel, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Azure Storage-Blobs** container met enkele gegevens.
* **Een Azure Data Lake Store-account**. Voor instructies over het toocreate één, Zie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Azure Data Lake Analytics-account (optioneel)** -Zie [aan de slag met Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md) account voor instructies over hoe toocreate een Data Lake opslaan.
* **AdlCopy hulpprogramma**. Installeer Hallo AdlCopy hulpprogramma van [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy).

## <a name="syntax-of-hello-adlcopy-tool"></a>Syntaxis van Hallo AdlCopy hulpprogramma
Hallo na syntaxis toowork met Hallo AdlCopy hulpprogramma gebruiken

    AdlCopy /Source <Blob or Data Lake Store source> /Dest <Data Lake Store destination> /SourceKey <Key for Blob account> /Account <Data Lake Analytics account> /Unit <Number of Analytics units> /Pattern

Hallo-parameters in Hallo syntaxis worden hieronder beschreven:

| Optie | Beschrijving |
| --- | --- |
| Bron |Hiermee geeft u Hallo-locatie van de brongegevens Hallo in hello Azure storage-blob. Hallo bron mag een blobcontainer een blob of een andere Data Lake Store-account. |
| Doel |Hiermee geeft u Hallo Data Lake Store bestemming toocopy aan. |
| SourceKey |Hiermee geeft u Hallo toegangssleutel voor opslag voor hello Azure storage-blob-bron. Dit is alleen vereist als Hallo-bron een blob-container of een blob is. |
| Account |**Optioneel**. Gebruik deze optie als u wilt dat de taak van toouse Azure Data Lake Analytics-account toorun Hallo kopiëren. Als u Hallo /Account optie Hallo syntaxis gebruiken maar geen een Data Lake Analytics-account opgeeft, AdlCopy maakt gebruik van een standaard account toorun Hallo taak. Ook als u deze optie gebruikt, moet u toevoegen Hallo bron (Azure Storage-Blob) en doel (Azure Data Lake Store) als gegevensbronnen voor uw Data Lake Analytics-account. |
| Eenheden |Geeft het aantal Data Lake Analytics-eenheden die wordt gebruikt voor de kopieertaak Hallo Hallo. Deze optie is verplicht als u Hallo **/Account** optie toospecify Hallo Data Lake Analytics-account. |
| patroon |Hiermee geeft u een regex-patroon waarmee wordt aangegeven welke toocopy blobs of bestanden. AdlCopy maakt gebruik van hoofdlettergevoelige overeenkomen. Hallo standaardpatroon gebruikt wanneer er geen patroon is opgegeven is toocopy alle items. Meerdere bestand patronen opgeven wordt niet ondersteund. |

## <a name="use-adlcopy-as-standalone-toocopy-data-from-an-azure-storage-blob"></a>AdlCopy (als zelfstandig) toocopy gegevens uit een Azure Storage-blob gebruiken
1. Open een opdrachtprompt en navigeer toohello directory waar AdlCopy is geïnstalleerd, doorgaans `%HOMEPATH%\Documents\adlcopy`.
2. Voer Hallo opdracht toocopy na een specifieke blob van Hallo bron container tooa Data Lake Store:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    Bijvoorbeeld:

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

    >[AZURE.NOTE] Hallo bovenstaande syntaxis geeft Hallo toobe gekopieerde tooa map in Hallo Data Lake Store-account. AdlCopy hulpprogramma maakt een map als de opgegeven mapnaam Hallo niet bestaat.

    U zult de vraag tooenter Hallo referenties voor hello Azure-abonnement waaronder die u een Data Lake Store-account hebt. Hier ziet u een vergelijkbare toohello volgende van uitvoer:

        Initializing Copy.
        Copy Started.
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.

1. U kunt ook alle Hallo blobs kopiëren uit een container toohello Data Lake Store-account met behulp van de volgende opdracht Hallo:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/ /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>        

    Bijvoorbeeld:

        AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

### <a name="performance-considerations"></a>Prestatieoverwegingen

Als u uit een Azure Blob Storage-account kopiëren wilt, wordt u mogelijk beperkt tijdens het kopiëren van Hallo blob storage-zijde. Hallo-prestaties van uw project kopiëren afnemen. toolearn meer informatie over het Hallo-limieten van Azure Blob Storage, Azure Storage-limieten op Zie [Azure-abonnement en Servicelimieten](../azure-subscription-service-limits.md).

## <a name="use-adlcopy-as-standalone-toocopy-data-from-another-data-lake-store-account"></a>AdlCopy (als zelfstandig) toocopy gegevens uit een andere Data Lake Store-account gebruiken
U kunt ook AdlCopy toocopy gegevens tussen twee Data Lake Store-accounts gebruiken.

1. Open een opdrachtprompt en navigeer toohello directory waar AdlCopy is geïnstalleerd, doorgaans `%HOMEPATH%\Documents\adlcopy`.
2. Hallo opdracht toocopy na een specifiek bestand van een Data Lake Store-account tooanother uitvoeren.

        AdlCopy /Source adl://<source_adls_account>.azuredatalakestore.net/<path_to_file> /dest adl://<dest_adls_account>.azuredatalakestore.net/<path>/

    Bijvoorbeeld:

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/909f2b.log /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

   > [!NOTE]
   > Hallo bovenstaande syntaxis geeft Hallo toobe gekopieerde tooa map in Hallo bestemming Data Lake Store-account. AdlCopy hulpprogramma maakt een map als de opgegeven mapnaam Hallo niet bestaat.
   >
   >

    U zult de vraag tooenter Hallo referenties voor hello Azure-abonnement waaronder die u een Data Lake Store-account hebt. Hier ziet u een vergelijkbare toohello volgende van uitvoer:

        Initializing Copy.
        Copy Started.|
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.
3. Hallo volgende opdracht worden alle bestanden gekopieerd vanuit een specifieke map in Hallo Data Lake Store-account tooa bronmap in Hallo doel Data Lake Store-account.

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/ /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

### <a name="performance-considerations"></a>Prestatieoverwegingen

Wanneer u AdlCopy als een zelfstandig hulpprogramma, Hallo-exemplaar wordt uitgevoerd op gedeelde, Azure beheerde bronnen. Hallo-prestaties mogelijk dat u in deze omgeving, is afhankelijk van systeembelasting en de beschikbare bronnen. Deze modus wordt beste voor kleinere overdrachten op basis van ad-hoc gebruikt. Er zijn geen parameters moeten toobe bij gebruik van AdlCopy als een zelfstandige tool zijn afgestemd.

## <a name="use-adlcopy-with-data-lake-analytics-account-toocopy-data"></a>AdlCopy (met Data Lake Analytics-account) toocopy gegevens gebruiken
U kunt ook uw Data Lake Analytics account toorun hello AdlCopy taak toocopy gegevens uit Azure storage blobs tooData Lake Store. Gebruik deze optie zou u meestal wanneer Hallo gegevens toobe verplaatst in Hallo reeks gigabytes en terabyte is en u wilt dat de prestaties beter en voorspelbare doorvoer.

toouse die uw Data Lake Analytics-account met AdlCopy toocopy van een Azure Storage-Blob Hallo bron (Azure Storage-Blob) moet worden toegevoegd als een gegevensbron voor uw Data Lake Analytics-account. Zie voor instructies over het toevoegen van aanvullende gegevensbronnen tooyour Data Lake Analytics-account [beheren Data Lake Analytics-account gegevensbronnen](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources).

> [!NOTE]
> Als u uit een Azure Data Lake Store-account als Hallo bron met behulp van een Data Lake Analytics-account kopiëren wilt, moet u niet tooassociate Hallo Data Lake Store-account met Hallo Data Lake Analytics-account. Hallo vereiste tooassociate Hallo bron opslag Hello Data Lake Analytics-account kan alleen als Hallo bron een Azure Storage-account is.
>
>

Voer Hallo volgende opdracht toocopy uit een Azure Storage-blob tooa Data Lake Store-account met behulp van Data Lake Analytics-account:

    AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Account <data_lake_analytics_account> /Unit <number_of_data_lake_analytics_units_to_be_used>

Bijvoorbeeld:

    AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Account mydatalakeanalyticaccount /Units 2

Voer op dezelfde manier Hallo volgende opdracht toocopy uit een Azure Storage-blob tooa Data Lake Store-account met behulp van Data Lake Analytics-account:

    AdlCopy /Source adl://mysourcedatalakestore.azuredatalakestore.net/mynewfolder/ /dest adl://mydestdatastore.azuredatalakestore.net/mynewfolder/ /Account mydatalakeanalyticaccount /Units 2

### <a name="performance-considerations"></a>Prestatieoverwegingen

Bij het kopiëren van gegevens binnen het bereik van terabytes Hallo biedt AdlCopy gebruik met uw eigen Azure Data Lake Analytics-account betere en meer voorspelbare prestaties. Hallo-parameter die moet worden afgestemd is Hallo aantal toouse voor de kopieertaak hello Azure Data Lake Analytics-eenheden. Het aantal eenheden Hallo vergroot, wordt Hallo prestaties van uw project kopiëren. Elk bestand toobe gekopieerd kan maximaal één eenheid kunt gebruiken. Meer eenheden dan het aantal bestanden worden gekopieerd Hallo geven verhoogd prestaties niet.

## <a name="use-adlcopy-toocopy-data-using-pattern-matching"></a>AdlCopy toocopy gegevens met jokertekens gebruiken
In deze sectie leest u hoe toouse AdlCopy toocopy gegevens uit een bron (in het onderstaande voorbeeld gebruiken we Azure Storage-Blob) tooa bestemming Data Lake Store-account met jokertekens. Bijvoorbeeld, kunt u Hallo stappen hieronder toocopy alle bestanden met de extensie CSV van Hallo bron blob toohello doel.

1. Open een opdrachtprompt en navigeer toohello directory waar AdlCopy is geïnstalleerd, doorgaans `%HOMEPATH%\Documents\adlcopy`.
2. Voer Hallo opdracht toocopy na alle bestanden met de extensie *.csv van een specifieke blob van Hallo bron container tooa Data Lake Store:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Pattern *.csv

    Bijvoorbeeld:

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/FoodInspectionData/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Pattern *.csv

## <a name="billing"></a>Facturering
* Als u Hallo AdlCopy hulpprogramma als zelfstandige die u wordt gefactureerd voor uitgaande kosten voor het verplaatsen van Hallo gegevens als bron hello Azure Storage-account zich niet in dezelfde regio als Hallo Data Lake Store.
* Als u Hallo AdlCopy hulpprogramma met uw Data Lake Analytics gebruiken-account standaard [Data Lake Analytics facturering tarieven](https://azure.microsoft.com/pricing/details/data-lake-analytics/) wordt toegepast.

## <a name="considerations-for-using-adlcopy"></a>Overwegingen voor het gebruik van AdlCopy
* AdlCopy (voor versie 1.0.5) ondersteunt kopiëren van gegevens uit bronnen die gezamenlijk meer dan duizenden bestanden en mappen hebben. Echter als u problemen die een grote gegevensset kopiëren, kunt u Hallo bestanden/mappen verdelen over verschillende submappen en Hallo pad toothose submappen als Hallo-bron in plaats daarvan.

## <a name="performance-considerations-for-using-adlcopy"></a>Prestatie-overwegingen voor het gebruik van AdlCopy

AdlCopy ondersteunt kopiëren van gegevens met duizenden bestanden en mappen. Als u een grote gegevensset kopiëren problemen ondervindt, kunt u Hallo bestanden/mappen verdelen naar kleinere submappen. AdlCopy is gebouwd voor ad-hoc exemplaren. Als u gegevens op periodieke basis toocopy probeert, moet u overwegen [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) die zorgt voor volledig beheer rond Hallo kopieerbewerkingen uitvoert.

## <a name="release-notes"></a>Releaseopmerkingen
* 1.0.13 - als u gegevens toohello kopieert hetzelfde Azure Data Lake Store-account via meerdere adlcopy opdrachten, hoeft u geen tooreenter uw referenties voor elke meer uitvoeren. Adlcopy nu opgeslagen in de cache die informatie over meerdere wordt uitgevoerd.

## <a name="next-steps"></a>Volgende stappen
* [Gegevens in Data Lake Store beveiligen](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics gebruiken met Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight gebruiken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

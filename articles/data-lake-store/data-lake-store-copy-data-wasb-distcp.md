---
title: aaaCopy gegevens tooand van WASB in Data Lake Store met Distcp | Microsoft Docs
description: Distcp hulpprogramma toocopy gegevens tooand gebruiken uit Azure Storage Blobs tooData Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a>Gebruik Distcp toocopy gegevens tussen Azure Storage-Blobs en Data Lake Store
> [!div class="op_single_selector"]
> * [DistCp gebruiken](data-lake-store-copy-data-wasb-distcp.md)
> * [AdlCopy gebruiken](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Nadat u een HDInsight-cluster met toegang tooa Data Lake Store-account hebt gemaakt, kunt u Hadoop-ecosysteem-hulpprogramma's zoals Distcp toocopy gegevens **tooand van** een HDInsight-cluster storage (WASB) naar een Data Lake Store-account. In dit artikel bevat instructies voor het tooachieve dit.

## <a name="prerequisites"></a>Vereisten
Voordat u dit artikel, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Een Azure Data Lake Store-account**. Voor instructies over het toocreate één, Zie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Azure HDInsight-cluster** met toegang tooa Data Lake Store-account. Zie [een HDInsight-cluster maken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Zorg ervoor dat u extern bureaublad inschakelen voor Hallo-cluster.

## <a name="do-you-learn-fast-with-videos"></a>Leert u snel met video's?
[Bekijk deze video](https://mix.office.com/watch/1liuojvdx6sie) over het toocopy gegevens tussen Azure Storage-Blobs en Data Lake Store met DistCp.

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a>Distcp gebruik van een cluster met HDInsight Linux

Een HDInsight-cluster wordt geleverd met Hallo Distcp hulpprogramma gebruikt toocopy gegevens uit verschillende bronnen in een HDInsight-cluster worden kan. Als u hebt Hallo HDInsight cluster toouse Data Lake Store als extra opslag geconfigureerd, hello Distcp hulpprogramma kan worden gebruikt out-of-the-box toocopy gegevens tooand uit een Data Lake Store-account. In dit gedeelte kijken we hoe toouse Hallo Distcp hulpprogramma.

1. Op het bureaublad SSH tooconnect toohello cluster te gebruiken. Zie [Connect tooa Linux gebaseerde HDInsight-cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md). Hallo-opdrachten uitvoeren vanaf Hallo SSH-prompt.

2. Controleer of u toegang hebt tot hello Azure Storage-Blobs (WASB). Hallo volgende opdracht uitvoeren:

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    Dit moet een lijst verstrekken van inhoud in Hallo storage-blob.
3. Daarnaast moet worden gecontroleerd of u toegang hebt tot Hallo Data Lake Store-account uit Hallo-cluster. Hallo volgende opdracht uitvoeren:

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    Dit moet een lijst met bestanden/mappen in Hallo Data Lake Store-account op te geven.
4. Distcp toocopy gegevens uit WASB tooa Data Lake Store-account gebruiken.

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    Hiermee worden gekopieerd Hallo inhoud Hallo **voorbeeld/data/gutenberg/** map in WASB te**/myfolder** in Hallo Data Lake Store-account.
5. Distcp toocopy gegevens uit Data Lake Store-account tooWASB op dezelfde manier gebruiken.

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    Hiermee worden gekopieerd Hallo inhoud van **/myfolder** in Hallo Data Lake Store-account te**voorbeeld/data/gutenberg/** map in WASB.

## <a name="performance-considerations-while-using-distcp"></a>Prestatie-overwegingen bij het gebruik van DistCp

Omdat DistCp's laagste granulatie is een enkel bestand, instelling Hallo maximumaantal gelijktijdige exemplaren Hallo belangrijkste parameter toooptimize deze tegen Data Lake Store. Dit wordt bepaald door het aantal mappers hello ('M ') parameter op Hallo-opdrachtregel. Deze parameter bepaalt Hallo kunt u het maximum aantal mappers die gebruikt toocopy gegevens worden. Standaardwaarde is 20.

**Voorbeeld**

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a>Hoe bepaal ik Hallo aantal mappers toouse?

Hier volgen een aantal richtlijnen.

* **Stap 1: Bepalen totale YARN geheugen** -Hallo eerste stap is toodetermine hello YARN geheugen beschikbaar toohello cluster waarop u Hallo DistCp taak uitvoert. Deze informatie is beschikbaar in Hallo Ambari portal die zijn gekoppeld aan het Hallo-cluster. Navigeer tooYARN en Hallo Configs tabblad toosee hello YARN geheugen weergeven. tooget hello totale YARN geheugen, Vermenigvuldig Hallo YARN-geheugen per knooppunt met het aantal knooppunten Hallo hebt in uw cluster.

* **Stap 2: Het aantal mappers Hallo berekenen** -waarde van Hallo **m** is gelijk toohello quotiënt van het totale YARN-geheugen, gedeeld door Hallo YARN container grootte. Hallo informatie over de grootte van de YARN-container is beschikbaar in ook Hallo Ambari-portal. Navigeer tooYARN en weergave Hallo Configs tabblad Hallo YARN container grootte in dit venster wordt weergegeven. Hallo vergelijking tooarrive Hallo aantal mappers (**m**) is

        m = (number of nodes * YARN memory for each node) / YARN container size

**Voorbeeld**

Stel dat u een 4 D14v2s knooppunten in cluster Hallo hebt en u tootransfer 10TB probeert van gegevens van 10 andere mappen. Elk van de mappen Hallo verschillende hoeveelheden gegevens bevatten en de bestandsgrootte Hallo binnen elke map verschillen.

* Totale geheugen van de YARN - van Hallo Ambari portal u bepalen dat Hallo YARN-geheugen is 96GB voor een D14-knooppunt. Ja, is de totale YARN-geheugen voor cluster met 4 knooppunten: 

        YARN memory = 4 * 96GB = 384GB

* Het aantal mappers - van Hallo u bepalen dat Hallo YARN container grootte is 3072 voor een clusterknooppunt D14 Ambari-portal. Dus is aantal mappers:

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

Als andere toepassingen geheugen gebruikt, kunt klikt u vervolgens u kiezen tooonly gebruik een deel van uw cluster YARN-geheugen voor DistCp.

### <a name="copying-large-datasets"></a>Kopiëren van grote gegevenssets

Als de grootte van Hallo gegevensset toobe Hallo verplaatst erg groot is (bijvoorbeeld > 1TB) of als u tal van verschillende mappen hebt, overweeg het gebruik van meerdere DistCp taken. Er is waarschijnlijk geen prestatieverbetering te bereiken, maar wordt het Hallo-taken verdeeld zodat als een taak mislukt, u alleen toorestart die specifieke taak in plaats van volledige Hallo-taak hoeft.

### <a name="limitations"></a>Beperkingen

* DistCp probeert toocreate mappers die in de prestaties van de grootte van toooptimize vergelijkbaar zijn. Het aantal mappers Hallo mogelijk niet altijd vergroot, prestaties.

* DistCp is beperkt tooonly één toewijzen per bestand. Daarom moet u niet meer mappers dan er bestanden hebben. Aangezien DistCp een-toewijzing alleen tooa bestand toewijzen kunt, wordt dit Hallo en de hoeveelheid gelijktijdigheid van taken die gebruikte toocopy grote bestanden kan worden beperkt.

* Als u een klein aantal grote bestanden hebt, hebt u ze in 256MB bestand segmenten toogive splitsen moet u meer potentiële gelijktijdigheid van taken. 
 
* Als u uit een Azure Blob Storage-account kopiëren wilt, kan uw taak kopiëren Hallo blob storage-zijde worden beperkt. Hallo-prestaties van uw project kopiëren afnemen. toolearn meer informatie over het Hallo-limieten van Azure Blob Storage, Azure Storage-limieten op Zie [Azure-abonnement en Servicelimieten](../azure-subscription-service-limits.md).

## <a name="see-also"></a>Zie ook
* [Gegevens kopiëren van Azure Storage Blobs tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md)
* [Gegevens in Data Lake Store beveiligen](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics gebruiken met Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight gebruiken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

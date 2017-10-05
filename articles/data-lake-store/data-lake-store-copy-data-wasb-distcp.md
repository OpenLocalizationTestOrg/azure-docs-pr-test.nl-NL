---
title: "Gegevens kopiëren naar en van WASB naar Data Lake Store met Distcp | Microsoft Docs"
description: "Distcp hulpprogramma gebruiken om gegevens te kopiëren naar en van Azure Storage-Blobs naar Data Lake Store"
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
ms.openlocfilehash: 356a93d330e9e8ce3eb3c6c982fc5c2e087846a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-distcp-to-copy-data-between-azure-storage-blobs-and-data-lake-store"></a>Distcp gebruiken om gegevens te kopiëren tussen Azure Storage-blobs en Data Lake Store
> [!div class="op_single_selector"]
> * [DistCp gebruiken](data-lake-store-copy-data-wasb-distcp.md)
> * [AdlCopy gebruiken](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Wanneer u een HDInsight-cluster dat toegang tot een Data Lake Store-account heeft hebt gemaakt, kunt u de Hadoop-ecosysteem-hulpprogramma's zoals Distcp gebruiken om gegevens te kopiëren **naar en uit** een HDInsight-cluster storage (WASB) naar een Data Lake Store-account. In dit artikel vindt instructies voor het om dit te bereiken.

## <a name="prerequisites"></a>Vereisten
Voordat u dit artikel gaat lezen, moet u beschikken over het volgende:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Een Azure Data Lake Store-account**. Zie voor instructies over het maken van een [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Azure HDInsight-cluster** met toegang tot een Data Lake Store-account. Zie [een HDInsight-cluster maken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Zorg ervoor dat u extern bureaublad inschakelen voor het cluster.

## <a name="do-you-learn-fast-with-videos"></a>Leert u snel met video's?
[Bekijk deze video](https://mix.office.com/watch/1liuojvdx6sie) voor het kopiëren van gegevens tussen Azure Storage-Blobs en Data Lake Store met DistCp.

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a>Distcp gebruik van een cluster met HDInsight Linux

Een HDInsight-cluster wordt geleverd met het hulpprogramma Distcp die kan worden gebruikt om gegevens te kopiëren uit verschillende bronnen in een HDInsight-cluster. Als u het HDInsight-cluster voor het gebruik van Data Lake Store als extra opslag hebt geconfigureerd, kan het hulpprogramma Distcp gebruikte out-of-the-box om gegevens te kopiëren naar en van een Data Lake Store-account zijn. In dit gedeelte kijken we hoe u het hulpprogramma Distcp.

1. Op het bureaublad SSH verbinding maken met het cluster te gebruiken. Zie [verbinding maken met een Linux gebaseerde HDInsight-cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md). Voer de opdrachten van de SSH-prompt.

2. Controleer of u toegang hebt tot de Azure Storage-Blobs (WASB). Voer de volgende opdracht uit:

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    Dit moet een lijst verstrekken van inhoud in de blob storage.
3. Daarnaast moet worden gecontroleerd of u toegang hebt tot het Data Lake Store-account van het cluster. Voer de volgende opdracht uit:

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    Dit moet een lijst met bestanden/mappen in het Data Lake Store-account op te geven.
4. Distcp gebruiken om gegevens van WASB kopiëren naar een Data Lake Store-account.

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    Hiermee kopieert de inhoud van de **voorbeeld/data/gutenberg/** map in WASB naar **/myfolder** in het Data Lake Store-account.
5. Op deze manier Distcp gebruiken om gegevens van Data Lake Store-account te WASB kopiëren.

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    Hiermee wordt de inhoud van gekopieerd **/myfolder** Data Lake Store-account dat **voorbeeld/data/gutenberg/** map in WASB.

## <a name="performance-considerations-while-using-distcp"></a>Prestatie-overwegingen bij het gebruik van DistCp

Omdat de laagste granulatie DistCp van één bestand is, is voor het instellen van het maximum aantal gelijktijdige exemplaren de belangrijkste parameter optimaliseren op basis van Data Lake Store. Dit wordt bepaald door het aantal mappers ('M ') parameter op de opdrachtregel. Deze parameter bepaalt het maximum aantal mappers dat wordt gebruikt om gegevens te kopiëren. Standaardwaarde is 20.

**Voorbeeld**

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-the-number-of-mappers-to-use"></a>Hoe bepaal ik het aantal mappers gebruiken?

Hier volgen een aantal richtlijnen.

* **Stap 1: Bepalen totale YARN geheugen** -de eerste stap is om te bepalen van de YARN-geheugen beschikbaar voor het cluster waarop u de taak DistCp uitvoert. Deze informatie is beschikbaar in de Ambari-portal die zijn gekoppeld aan het cluster. Navigeer naar YARN en Raadpleeg het tabblad configuraties om te zien van het geheugen YARN. Als u het totale YARN-geheugen, Vermenigvuldig de YARN-geheugen per knooppunt met het aantal knooppunten dat u hebt in uw cluster.

* **Stap 2: Het aantal mappers berekenen** -de waarde van **m** gelijk is aan het quotiënt van totale YARN-geheugen, gedeeld door de grootte van de container YARN. Informatie over de grootte van de YARN-container is beschikbaar in de Ambari-portal. Navigeer naar YARN en Raadpleeg het tabblad Configs. De grootte van de container YARN wordt in dit venster weergegeven. De vergelijking moet worden uitgevoerd op het aantal mappers (**m**) is

        m = (number of nodes * YARN memory for each node) / YARN container size

**Voorbeeld**

Stel dat u een 4 D14v2s knooppunten in het cluster hebt en u probeert 10TB gegevens overzetten van 10 andere mappen. Elk van de mappen verschillende hoeveelheden gegevens bevatten en de bestandsgrootte in elke map verschillen.

* Totale YARN geheugen - portal van de Ambari dat u vaststelt dat het geheugen YARN 96GB voor een D14-knooppunt. Ja, is de totale YARN-geheugen voor cluster met 4 knooppunten: 

        YARN memory = 4 * 96GB = 384GB

* Aantal mappers - u hebt vastgesteld dat de grootte van de container YARN 3072 voor een clusterknooppunt D14 uit de Ambari-portal. Dus is aantal mappers:

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

Als andere toepassingen geheugen gebruikt, kunt klikt u vervolgens u alleen een deel van uw cluster YARN-geheugen voor DistCp worden gebruikt.

### <a name="copying-large-datasets"></a>Kopiëren van grote gegevenssets

Wanneer de grootte van de gegevensset moet worden verplaatst erg groot is (bijvoorbeeld > 1TB) of als u tal van verschillende mappen hebt, overweeg het gebruik van meerdere DistCp taken. Er is waarschijnlijk geen prestatieverbetering te bereiken, maar wordt deze de taken verdeeld, zodat als een taak mislukt, u alleen hoeft wordt op te starten die specifieke taak in plaats van de hele taak.

### <a name="limitations"></a>Beperkingen

* DistCp probeert te maken van mappers met dezelfde grootte om prestaties te optimaliseren. Het aantal mappers mogelijk niet altijd betere prestaties.

* DistCp is beperkt tot slechts één toewijzen per bestand. Daarom moet u niet meer mappers dan er bestanden hebben. Aangezien DistCp alleen een toewijzen aan een bestand toewijzen kunt, beperkt dit de hoeveelheid gelijktijdigheid van taken die kan worden gebruikt voor het kopiëren van grote bestanden.

* Als u een klein aantal grote bestanden hebt, moet klikt u vervolgens u gesplitst in 256MB bestand segmenten zodat u meer potentiële gelijktijdigheid van taken. 
 
* Als u uit een Azure Blob Storage-account kopiëren wilt, kan uw taak kopiëren aan de kant van blob storage worden beperkt. De prestaties van uw project kopiëren afnemen. Zie voor meer informatie over de beperkingen van Azure Blob Storage, Azure Storage-limieten op [Azure-abonnement en Servicelimieten](../azure-subscription-service-limits.md).

## <a name="see-also"></a>Zie ook
* [Gegevens kopiëren van Azure Storage-Blobs naar Data Lake Store](data-lake-store-copy-data-azure-storage-blob.md)
* [Gegevens in Data Lake Store beveiligen](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics gebruiken met Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight gebruiken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

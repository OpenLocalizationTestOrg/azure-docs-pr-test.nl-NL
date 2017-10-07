---
title: Data Lake Store Hive-prestaties afstemmen richtlijnen aaaAzure | Microsoft Docs
description: Azure Data Lake Store Hive prestaties afstemmen richtlijnen
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: e44daeb6ad3b64e893c709df63b56444a330729f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a>Prestaties afstemmen richtlijnen voor Hive in HDInsight en Azure Data Lake Store

Hallo standaardinstellingen zijn tooprovide goede prestaties ingesteld op veel verschillende gebruiksscenario.  Voor i/o-intensieve query's kan Hive regelmatig tooget betere prestaties bij ADLS zijn.  

## <a name="prerequisites"></a>Vereisten

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Een Azure Data Lake Store-account**. Voor instructies over het toocreate één, Zie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Azure HDInsight-cluster** met toegang tooa Data Lake Store-account. Zie [een HDInsight-cluster maken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Zorg ervoor dat u extern bureaublad inschakelen voor Hallo-cluster.
* **Uitvoeren van Hive in HDInsight**.  toolearn over het uitvoeren van Hive-taken in HDInsight, Zie [op HDInsight Hive gebruiken] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)
* **Prestaties afstemmen richtlijnen op ADLS**.  Raadpleeg voor algemene prestaties concepten, [Data Lake Store prestaties afstemmen richtlijnen](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)

## <a name="parameters"></a>Parameters

Hier volgen Hallo belangrijkste instellingen tootune voor verbeterde ADLS-prestaties:

* **hive.tez.container.Size** – hello en de hoeveelheid geheugen die door elke taken worden gebruikt

* **grootte van tez.Grouping.min** : minimale grootte van elke toewijzen

* **grootte van tez.Grouping.Max** : maximale grootte van elke toewijzen

* **hive.Exec.reducer.bytes.per.reducer** : grootte van elke reducer

**hive.tez.container.Size** -Hallo container grootte bepaalt hoeveel geheugen beschikbaar is voor elke taak.  Dit is de belangrijkste invoer Hallo voor beheren Hallo gelijktijdigheid in Hive.  

**grootte van tez.Grouping.min** – deze parameter kunt u tooset Hallo minimale grootte van elke toewijzen.  Als het aantal mappers die Tez kiest Hallo kleiner dan Hallo-waarde van deze parameter is, gebruik Tez hier ingestelde Hallo-waarde.  

**grootte van tez.Grouping.Max** – Hallo parameter kunt u tooset Hallo maximale grootte van elke toewijzen.  Als het aantal mappers die Tez kiest Hallo groter dan Hallo-waarde van deze parameter is, gebruik Tez hier ingestelde Hallo-waarde.  

**hive.Exec.reducer.bytes.per.reducer** – Hallo grootte van elke reducer door deze parameter wordt ingesteld.  Standaard is elke reducer 256MB.  

## <a name="guidance"></a>Richtlijnen

**Stel hive.exec.reducer.bytes.per.reducer** – Hallo standaardwaarde goed werkt wanneer Hallo gegevens is gedecomprimeerd.  Voor gegevens die zijn gecomprimeerd, moet u de grootte van de Hallo van Hallo reducer beperken.  

**Stel hive.tez.container.size** – In elk knooppunt geheugen wordt opgegeven door yarn.nodemanager.resource.memory mb en moet worden correct is ingesteld op HDI-cluster standaard.  Zie voor meer informatie over het instellen van de juiste geheugen Hallo in YARN [boeken](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).

I/o-intensieve werkbelastingen kunnen profiteren van meer parallelle uitvoering door Hallo Tez container verkleinen. Hiermee geeft u Hallo gebruiker meer containers waardoor gelijktijdigheid van taken.  Sommige Hive-query's vereisen echter een aanzienlijke hoeveelheid geheugen (bijvoorbeeld MapJoin).  Als het Hallo-taak beschikt niet over voldoende geheugen, krijgt u een out-of geheugen-uitzondering tijdens runtime.  Als u buiten geheugen uitzonderingen ontvangt, moet u Hallo geheugen verhogen.   

Hallo aantal gelijktijdige taken die worden uitgevoerd of parallelle uitvoering wordt begrensd worden door Hallo totale YARN-geheugen.  Hallo aantal YARN-containers worden uitgevoerd, bepalen hoeveel gelijktijdige taken kunnen uitvoeren.  toofind hello YARN geheugen per knooppunt, kunt u tooAmbari gaan.  Navigeer tooYARN en Hallo Configs tabblad bekijkt.  Hallo YARN geheugen wordt weergegeven in dit venster.  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
Hallo sleutel tooimproving prestaties met ADLS is tooincrease Hallo gelijktijdigheid zo veel mogelijk.  Tez berekent automatisch het aantal taken die moeten worden gemaakt, dus u niet tooset hoeft Hallo deze.   

## <a name="example-calculation"></a>Voorbeeld van de berekening

Stel dat u hebt een cluster met 8 knooppunten D14.  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a>Beperkingen
**ADLS-beperking** 

UIf bereikt van Hallo beperkt bandbreedte opgegeven door ADLS, zou u taakfouten toosee start. Dit kan worden geïdentificeerd door observeren bandbreedteregeling fouten in de logboeken van de taak.  U kunt Hallo parallelle uitvoering verlagen door de Tez-container vergroten.  Als u meer gelijktijdigheid van taken bij uw werk nodig, neem dan contact met ons.   

toocheck als u zijn ophalen beperkt, moet u aan de clientzijde Hallo logboekregistratie voor foutopsporing tooenable Hallo. Hier ziet u hoe u dat kunt doen:

1. Put hello eigenschap in Hallo log4j eigenschappen in de Hive-configuratie te volgen. Dit kan worden gedaan vanuit de weergave Ambari: log4j.logger.com.microsoft.azure.datalake.store=DEBUG alle Hallo knooppunten /-service opnieuw starten voor Hallo config tootake effect.

2. Als u beperkt ophalen, ziet u Hallo 429 HTTP-foutcode in Hallo hive-logboekbestand. Hallo hive-logboekbestand bevindt zich in /tmp/&lt;gebruiker&gt;/hive.log

## <a name="further-information-on-hive-tuning"></a>Meer informatie over het afstemmen van Hive

Hier volgen enkele blogs waarmee uw Hive-query's optimaliseren:
* [Hive-query's optimaliseren voor Hadoop in HDInsight](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [Het oplossen van de prestaties van de Hive-query 's](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)
* [Ignite Neem contact op optimaliseren Hive in HDInsight](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)

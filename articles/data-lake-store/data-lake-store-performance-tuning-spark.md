---
title: Data Lake Store Spark prestaties afstemmen richtlijnen aaaAzure | Microsoft Docs
description: Azure Data Lake Store Spark prestaties afstemmen richtlijnen
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
ms.openlocfilehash: da1d172e9cb1199ad95605ea1718e78559f79650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-spark-on-hdinsight-and-azure-data-lake-store"></a>Prestaties afstemmen richtlijnen voor Spark in HDInsight en Azure Data Lake Store

Wanneer op de prestaties van Spark afstemmen, moet u tooconsider Hallo aantal apps dat wordt uitgevoerd op uw cluster.  Standaard kunt u 4 uitvoeren apps gelijktijdig op uw HDI-cluster (Opmerking: Hallo standaardinstelling is onderwerp toochange).  Kunt u beslissen toouse minder apps zodat u kunt de standaardinstellingen Hallo overschrijven en meer van de cluster hello voor deze apps gebruiken.  

## <a name="prerequisites"></a>Vereisten

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Een Azure Data Lake Store-account**. Voor instructies over het toocreate één, Zie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Azure HDInsight-cluster** met toegang tooa Data Lake Store-account. Zie [een HDInsight-cluster maken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Zorg ervoor dat u extern bureaublad inschakelen voor Hallo-cluster.
* **Spark-cluster uitgevoerd op Azure Data Lake Store**.  Zie voor meer informatie [gebruik HDInsight Spark-cluster tooanalyze gegevens in Data Lake Store](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)
* **Prestaties afstemmen richtlijnen op ADLS**.  Raadpleeg voor algemene prestaties concepten, [Data Lake Store prestaties afstemmen richtlijnen](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance) 

## <a name="parameters"></a>Parameters

Wanneer Spark van taken wordt uitgevoerd, moet u hier Hallo meest belangrijke instellingen die afgestemd tooincrease op de prestaties van ADLS worden kunnen zijn:

* **NUM Executor** -Hallo aantal gelijktijdige taken die kunnen worden uitgevoerd.

* **Executor geheugen** -Hallo en de hoeveelheid geheugen tooeach executor toegewezen.

* **Executor kernen** -Hallo aantal kernen tooeach executor toegewezen.                     

**NUM Executor** Num Executor stelt Hallo kunt u het maximum aantal taken dat parallel kan worden uitgevoerd.  Hallo werkelijke aantal taken dat parallel kan worden uitgevoerd, wordt begrensd door Hallo geheugen en CPU-resources in uw cluster.

**Executor geheugen** dit Hallo hoeveelheid geheugen die momenteel wordt gereserveerd tooeach executor is.  Hallo geheugen dat nodig is voor elke executor is afhankelijk van het Hallo-taak.  Voor complexe bewerkingen moet Hallo geheugen toobe hoger.  Voor eenvoudige bewerkingen zoals lezen en schrijven geheugenvereisten niet lager zijn.  Hallo hoeveelheid geheugen voor elke executor kan worden weergegeven in de Ambari.  In de Ambari, tooSpark navigeren en Hallo Configs tabblad bekijkt.  

**Executor kernen** Hiermee stelt u Hallo hoeveelheid kernen per executor waarmee wordt bepaald Hallo aantal parallelle threads dat kan worden uitgevoerd per executor gebruikt.  Bijvoorbeeld, als executor kernen = 2, en vervolgens elk executor 2 parallelle taken in Hallo executor kan worden uitgevoerd.  Hallo executor-kernen nodig zijn afhankelijk van het Hallo-taak.  I/o-intensief taken hoeven niet een grote hoeveelheid geheugen per taak, zodat elke executor meer parallelle taken kan verwerken.

Standaard worden twee virtuele YARN cores gedefinieerd voor elke fysieke kernen bij het uitvoeren van Spark in HDInsight.  Dit nummer biedt een goede balans van concurrecy en hoeveelheid context overschakelen vanuit meerdere threads.  

## <a name="guidance"></a>Richtlijnen

Tijdens het uitvoeren van Spark analytische workloads toowork met gegevens in Data Lake Store is het raadzaam dat u Hallo meest recente HDInsight versie tooget Hallo optimale prestaties met Data Lake Store. Wanneer de taak meer i/o-intensieve is, kunnen bepaalde parameters geconfigureerde tooimprove prestaties zijn.  Azure Data Lake Store is een uiterst schaalbare opslag platform dat maximale doorvoer kan verwerken.  Als Hallo taak hoofdzakelijk uit lees- of schrijfbewerkingen bestaat, kan vervolgens concurrency voor i/o-tooand van Azure Data Lake Store vergroot, prestaties.

Er zijn enkele algemene manieren tooincrease gelijktijdigheid van taken voor i/o-intensieve taken.

**Stap 1: Bepalen hoeveel apps worden uitgevoerd op uw cluster** – u moet weten hoe veel apps worden uitgevoerd op Hallo cluster Hallo huidige inclusief.  Hallo standaardwaarden voor elke Spark instelling wordt ervan uitgegaan dat er 4 apps tegelijkertijd worden uitgevoerd.  Daarom hebt u alleen 25% van Hallo cluster beschikbaar is voor elke app.  tooget betere prestaties, kunt u Hallo standaardwaarden overschrijven door het aantal Executor hello te wijzigen.  

**Stap 2: Stel executor geheugen** – hello eerst te beginnen tooset Hallo executor-geheugen is.  Hallo geheugen zijn afhankelijk van het Hallo-taak dat u gaat toorun zijn.  U kunt gelijktijdigheid vergroten door minder geheugen per executor toewijzen.  Als u buiten geheugen uitzonderingen ziet wanneer u uw taak uitvoert, moet u Hallo-waarde voor deze parameter verhogen.  Een alternatief is tooget meer geheugen met behulp van een cluster met hogere hoeveelheden geheugen of Hallo vergroten van het cluster.  Meer geheugen toe te voegen meer Executor toobe gebruikt, wat betekent meer gelijktijdigheid van taken dat.

**Stap 3: Stel executor kernen** – voor i/o-intensieve werkbelastingen die geen complexe bewerkingen, is het goed toostart met een groot aantal executor kernen tooincrease Hallo aantal parallelle taken per executor.  Instelling executor kernen too4 is een goede start.   

    executor-cores = 4
Hallo executor kernen aantal te verhogen, krijgt u meer parallelle uitvoering zodat u met verschillende executor-kernen experimenteren kunt.  Voor taken die u meer complexe bewerkingen hebt, moet u het aantal kernen per executor Hallo verminderen.  Als executor kernen kan hoger zijn dan 4, vervolgens garbagecollection inefficiënt en de prestaties nadelig beïnvloeden.

**Stap 4: YARN-geheugen van de cluster bepalen** – deze informatie is beschikbaar in Ambari.  Navigeer tooYARN en Hallo Configs tabblad bekijkt.  Hallo YARN geheugen wordt weergegeven in dit venster.  
Opmerking: wanneer u zich in Hallo-venster, u ziet ook YARN Hallo-container standaardgrootte.  Hallo YARN container grootte is hetzelfde als geheugen per executor parameter Hallo.

    Total YARN memory = nodes * YARN memory per node
**Stap 5: Num Executor berekenen**

**Geheugen-beperking berekenen** -Hallo num Executor parameter wordt begrensd door geheugen of CPU.  Hallo geheugen beperking wordt bepaald door de hoeveelheid beschikbare YARN-geheugen voor uw toepassing hello.  U moet nemen totale YARN-geheugen en die wordt gedeeld door executor-geheugen.  Hallo-beperking moet ongedaan worden geschaald voor Hallo aantal apps, zodat we door het aantal apps Hallo delen toobe.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
**CPU-beperking berekenen** -Hallo CPU-beperking wordt berekend als het totale aantal virtuele kernen gedeeld door het aantal kernen per executor Hallo Hallo.  Er zijn 2 virtuele kernen voor elke fysieke kernen.  Vergelijkbare toohello geheugen beperking, hebben we delen door het aantal apps Hallo.

    virtual cores = (nodes in cluster * # of physical cores in node * 2)
    CPU constraint = (total virtual cores / # of cores per executor) / # of apps
**Num Executor ingesteld** – Hallo num Executor parameter wordt bepaald door het duurt minimaal Hallo geheugen de beperkingen en Hallo CPU Hallo. 

    num-executors = Min (total virtual Cores / # of cores per executor, available YARN memory / executor-memory)   
Hoe hoger de waarde van getal Executor stijgt niet per se prestaties.  U moet rekening houden met het toevoegen van meer Executor wordt toegevoegd extra overhead voor elke extra executor die u kunt mogelijk de prestaties verslechteren.  NUM Executor wordt begrensd door Hallo clusterbronnen.    

## <a name="example-calculation"></a>Voorbeeld van de berekening

Stel dat u hebt momenteel een cluster bestaan uit 8 D4v2 knooppunten dat actief 2 apps Hallo waaronder u één toorun gaat.  

**Stap 1: Bepalen hoeveel apps worden uitgevoerd op uw cluster** – u weet dat u 2 hebt apps op uw cluster, inclusief Hallo een u toorun gaat.  

**Stap 2: Stel executor geheugen** – voor dit voorbeeld we bepalen 6 GB executor-geheugen is geschikt voor i/o-intensieve taak.  

    executor-memory = 6GB
**Stap 3: Stel executor kernen** – omdat dit een i/o-intensieve taak is, kunnen we Hallo aantal kernen voor elke too4 executor ingesteld.  Instelling kernen per executor toolarger dan 4 garbagecollection verzameling problemen kan veroorzaken.  

    executor-cores = 4
**Stap 4: YARN-geheugen van de cluster bepalen** – We tooAmbari toofind uit dat elke D4v2 25 GB geheugen YARN heeft navigeren.  Aangezien er 8 knooppunten, kan geheugen YARN Hallo 8 wordt vermenigvuldigd.

    Total YARN memory = nodes * YARN memory* per node
    Total YARN memory = 8 nodes * 25GB = 200GB
**Stap 5: Berekenen num Executor** – Hallo num Executor parameter wordt bepaald door het duurt minimaal Hallo geheugen de beperkingen en Hallo CPU gedeeld door Hallo Hallo # van apps die worden uitgevoerd op Spark.    

**Geheugen-beperking berekenen** – Hallo geheugen beperking wordt berekend als Hallo totale YARN geheugen gedeeld door Hallo geheugen per executor.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
    Memory constraint = (200GB / 6GB) / 2   
    Memory constraint = 16 (rounded)
**CPU-beperking berekenen** -Hallo CPU-beperking wordt berekend als totale yarn kernen gedeeld door het aantal kernen per executor Hallo Hallo.
    
    YARN cores = nodes in cluster * # of cores per node * 2   
    YARN cores = 8 nodes * 8 cores per D14 * 2 = 128
    CPU constraint = (total YARN cores / # of cores per executor) / # of apps
    CPU constraint = (128 / 4) / 2
    CPU constraint = 16
**Set num-Executor**

    num-executors = Min (memory constraint, CPU constraint)
    num-executors = Min (16, 16)
    num-executors = 16    


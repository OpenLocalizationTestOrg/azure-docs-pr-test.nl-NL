---
title: Data Lake Store MapReduce prestaties afstemmen richtlijnen aaaAzure | Microsoft Docs
description: Azure Data Lake Store MapReduce prestaties afstemmen richtlijnen
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
ms.openlocfilehash: e21414a23530e65613c85156af0209c88ec54d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-mapreduce-on-hdinsight-and-azure-data-lake-store"></a>Prestaties afstemmen richtlijnen voor MapReduce op HDInsight en Azure Data Lake Store


## <a name="prerequisites"></a>Vereisten

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Een Azure Data Lake Store-account**. Voor instructies over het toocreate één, Zie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Azure HDInsight-cluster** met toegang tooa Data Lake Store-account. Zie [een HDInsight-cluster maken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Zorg ervoor dat u extern bureaublad inschakelen voor Hallo-cluster.
* **Met behulp van MapReduce op HDInsight**.  Zie voor meer informatie [gebruik MapReduce in Hadoop in HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)  
* **Prestaties afstemmen richtlijnen op ADLS**.  Raadpleeg voor algemene prestaties concepten, [Data Lake Store prestaties afstemmen richtlijnen](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)  

## <a name="parameters"></a>Parameters

Bij het uitvoeren van MapReduce-taken zijn hier Hallo belangrijkste parameters die u kunt tooincrease prestaties op ADLS configureren:

* **Mapreduce.map.Memory.MB** – Hallo hoeveelheid geheugen tooallocate tooeach toewijzen
* **Mapreduce.job.Maps** – Hallo aantal taken per taak kaart
* **Mapreduce.reduce.Memory.MB** – Hallo hoeveelheid geheugen tooallocate tooeach reducer
* **Mapreduce.job.reduces** – Hallo aantal taken per taak verminderen

**Mapreduce.map.Memory / Mapreduce.reduce.memory** dit nummer moet worden aangepast op basis van hoeveel geheugen nodig is voor de kaart Hallo en/of taak verminderen.  de standaardwaarden Hallo van mapreduce.map.memory en mapreduce.reduce.memory kunnen worden weergegeven in de Ambari via Hallo Yarn-configuratie.  In de Ambari, tooYARN navigeren en Hallo Configs tabblad bekijkt.  Hallo YARN geheugen wordt weergegeven.  

**Mapreduce.job.Maps / Mapreduce.job.reduces** dit maximum aantal mappers of verkleiningstoestellen toobe gemaakt Hallo bepaalt.  het aantal splitsingen Hallo bepaalt hoeveel mappers voor Hallo MapReduce-taak wordt gemaakt.  Daarom kunnen er minder mappers dan u hebt opgegeven of er minder splitsingen dan het aantal aangevraagde mappers Hallo zijn.       

## <a name="guidance"></a>Richtlijnen

**Stap 1: Aantal actieve taken bepalen** -standaard MapReduce Hallo gehele cluster wordt gebruikt voor uw project.  Met behulp van minder mappers dan er beschikbaar containers kunt u minder Hallo-cluster.  Hallo-instructies in dit document wordt ervan uitgegaan dat uw toepassing is Hallo alleen uitgevoerd op uw cluster.      

**Stap 2: Stel mapreduce.map.memory/mapreduce.reduce.memory** : grootte van het geheugen voor kaart Hallo Hallo en verminderen taken zijn afhankelijk van uw specifieke taak.  Als u wilt dat tooincrease gelijktijdigheid van taken, kunt u de geheugengrootte Hallo verminderen.  Hallo aantal gelijktijdig uitgevoerde taken is afhankelijk van het aantal containers Hallo.  Hallo hoeveelheid geheugen per toewijzen of reducer verlaagt, kunnen meer containers worden gemaakt, die meer mappers of verkleiningstoestellen toorun gelijktijdig inschakelen.  Afnemende Hallo hoeveelheid geheugen te veel kan ertoe leiden dat bepaalde processen toorun onvoldoende geheugen.  Als u een heap-fout krijgt bij het uitvoeren van uw werk, moet u Hallo geheugen per toewijzen of reducer verhogen.  U moet rekening houden met toevoegen van meer containers worden toegevoegd extra overhead voor elke extra container die u kunt mogelijk de prestaties verslechteren.  Een ander alternatief is tooget meer geheugen met behulp van een cluster met hogere hoeveelheden geheugen of Hallo aantal knooppunten in het cluster te verhogen.  Meer geheugen toe te voegen meer containers toobe gebruikt, wat betekent meer gelijktijdigheid van taken dat.  

**Stap 3: Bepalen totale YARN geheugen** -tootune mapreduce.job.maps/mapreduce.job.reduces, moet u rekening houden Hallo hoeveelheid totale YARN-geheugen beschikbaar voor gebruik.  Deze informatie is beschikbaar in Ambari.  Navigeer tooYARN en Hallo Configs tabblad bekijkt.  Hallo YARN geheugen wordt weergegeven in dit venster.  U moet Hallo YARN geheugen met Hallo aantal knooppunten in het cluster tooget Hallo totale YARN geheugen vermenigvuldigen.

    Total YARN memory = nodes * YARN memory per node
Als u een leeg cluster gebruikt, kan geheugen Hallo totale YARN-geheugen voor uw cluster zijn.  Als er andere toepassingen zijn geheugen, kunt u tooonly gebruik een deel van uw cluster geheugen doordat het aantal mappers of verkleiningstoestellen toohello aantal containers hello wilt toouse.  

**Stap 4: Aantal YARN containers berekenen** – YARN containers Hallo hoeveelheid gelijktijdigheid van taken beschikbaar voor Hallo taak voorschrijven.  Totale hoeveelheid geheugen voor YARN nemen en die wordt gedeeld door mapreduce.map.memory.  

    # of YARN containers = total YARN memory / mapreduce.map.memory

**Stap 5: Stel mapreduce.job.maps/mapreduce.job.reduces** mapreduce.job.maps/mapreduce.job.reduces tooat ingesteld minimaal Hallo aantal beschikbare containers.  U kunt experimenteren verdere Hallo door aantal te verhogen mappers en verkleiningstoestellen toosee als u betere prestaties krijgt.  Houd er rekening mee dat meer mappers extra overhead hebben dus met te veel mappers de prestaties nadelig beïnvloeden.  

Planning van CPU- en CPU-isolatie zijn standaard uitgeschakeld zodat Hallo aantal YARN containers wordt beperkt door het geheugen.

## <a name="example-calculation"></a>Voorbeeld van de berekening

Stel dat u hebt momenteel een cluster die bestaan uit 8 D14 knooppunten en gewenste toorun een i/o-intensieve-taak.  Hier volgen Hallo berekeningen die u moet doen:

**Stap 1: Aantal actieve taken bepalen** -in ons voorbeeld gaan we ervan uit dat de taak is Hallo slechts één die wordt uitgevoerd.  

**Stap 2: Stel mapreduce.map.memory/mapreduce.reduce.memory** – in ons voorbeeld u een i/o-intensieve taak uitvoert en besluit 3 GB geheugen voor taken van de kaart is voldoende.

    mapreduce.map.memory = 3GB
**Stap 3: Bepalen totale YARN-geheugen**

    total memory from hello cluster is 8 nodes * 96GB of YARN memory for a D14 = 768GB
**Stap 4: Het aantal containers YARN berekenen**

    # of YARN containers = 768GB of available memory / 3 GB of memory =   256

**Stap 5: Mapreduce.job.maps/mapreduce.job.reduces instellen**

    mapreduce.map.jobs = 256

## <a name="limitations"></a>Beperkingen

**ADLS-beperking**

Als een multitenant-service stelt ADLS limieten van niveau bandbreedte.  Als u deze limiet bereikt, wordt u taakfouten toosee gestart. Dit kan worden geïdentificeerd door observeren bandbreedteregeling fouten in de logboeken van de taak.  Als u meer bandbreedte nodig hebt voor uw project, neem dan contact met ons.   

toocheck als u zijn ophalen beperkt, moet u aan de clientzijde Hallo logboekregistratie voor foutopsporing tooenable Hallo. Hier ziet u hoe u dat kunt doen:

1. Put hello na eigenschap in de eigenschappen van Hallo log4j in Ambari > YARN > Config > Geavanceerde yarn-log4j: log4j.logger.com.microsoft.azure.datalake.store=DEBUG

2. Alle Hallo knooppunten/service Hallo config tootake effect opnieuw starten.

3. Als u beperkt ophalen, ziet u Hallo 429 HTTP-foutcode in Hallo YARN-logboekbestand. Hallo YARN-logboekbestand bevindt zich in /tmp/&lt;gebruiker&gt;/yarn.log

## <a name="examples-toorun"></a>Voorbeelden tooRun

toodemonstrate vindt hoe MapReduce wordt uitgevoerd op Azure Data Lake Store hieronder u enkele voorbeeldcode die is uitgevoerd op een cluster met Hallo volgende instellingen:

* 16 knooppunten D14v2
* Hadoop-cluster HDI 3.6 uitgevoerd

Voor een beginpunt vindt hier u enkele voorbeeld opdrachten toorun MapReduce Teragen Terasort en Teravalidate.  U kunt deze opdrachten op basis van uw resources aanpassen.

**Teragen**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 10000000000 adl://example/data/1TB-sort-input

**Terasort**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 -Dmapreduce.job.reduces=512 -Dmapreduce.reduce.memory.mb=3072 adl://example/data/1TB-sort-input adl://example/data/1TB-sort-output

**Teravalidate**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapreduce.job.maps=512 -Dmapreduce.map.memory.mb=3072 adl://example/data/1TB-sort-output adl://example/data/1TB-sort-validate

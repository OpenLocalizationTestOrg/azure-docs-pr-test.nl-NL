---
title: aaaUse Ambari Tez weergave met HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse hello Ambari Tez toodebug Tez-taken weergeven op HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a>Ambari-weergaven toodebug Tez-taken op HDInsight gebruiken

Hallo Ambari-Webgebruikersinterface voor HDInsight bevat een Tez-weergave die kan worden gebruikt toounderstand en foutopsporing functies die gebruikmaken van Tez. Hallo Tez weergave kunt u toovisualize Hallo taak, zoals een grafiek van verbonden items Inzoomen op elk item en statistieken en logboekregistratie informatie ophalen.

> [!IMPORTANT]
> Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie voor meer informatie [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Vereisten

* Een Linux gebaseerde HDInsight-cluster. Zie voor stapsgewijze instructies voor het maken van een cluster, [aan de slag met HDInsight op basis van Linux](hdinsight-hadoop-linux-tutorial-get-started.md).
* Een moderne webbrowser met ondersteuning voor HTML5.

## <a name="understanding-tez"></a>Understanding Tez

Tez is een uitbreidbaar framework voor gegevensverwerking in Hadoop. deze groter snelheden dan traditionele MapReduce-verwerking biedt. Voor Linux gebaseerde HDInsight-clusters is het standaard-engine Hallo voor Hive.

Tez maakt een omgeleid acyclische grafiek (DAG) die worden beschreven Hallo volgorde van acties die zijn vereist voor taken. Afzonderlijke acties hoekpunten worden genoemd en het uitvoeren van een stukje Hallo algemene taak. Hallo werkelijke uitvoering van Hallo werk beschreven door een hoekpunt een taak wordt aangeroepen en kan worden verdeeld over meerdere knooppunten in cluster Hallo.

### <a name="understanding-hello-tez-view"></a>Understanding Hallo Tez weergeven

Hallo Tez-weergave bevat zowel historische gegevens en informatie over processen die worden uitgevoerd. Deze informatie laat zien hoe een taak wordt verdeeld tussen verschillende clusters. Wordt ook gebruikt door taken en hoekpunten tellers en informatie over de fout gerelateerd toohello taak. Kan deze u nuttige informatie in de volgende scenario's Hallo aanbieden:

* Bewaking langlopende processen, weer te geven, Hallo voortgang van de kaart en taken te verminderen.
* Historische gegevens voor de geslaagde of mislukte processen toolearn analyseren hoe verwerking kan worden verbeterd of waarom is mislukt.

## <a name="generate-a-dag"></a>Genereren van een DAG

Hallo Tez-weergave alleen gegevens bevat als een taak die gebruikmaakt van Hallo Tez-engine is momenteel wordt uitgevoerd of is eerder is uitgevoerd. Eenvoudige Hive-query's kunnen worden opgelost zonder Tez. Meer complexe query's die wilt filteren, groeperen, rangschikken, joins, enzovoort. Hallo Tez-engine gebruiken.

Volgende stappen toorun een Hive-query die gebruikmaakt van Tez hello gebruiken:

1. Navigeer in een webbrowser, toohttps://CLUSTERNAME.azurehdinsight.net, waarbij **CLUSTERNAME** Hallo-naam van uw HDInsight-cluster.

2. Selecteer Hallo Hallo menu bovenaan Hallo Hallo pagina **weergaven** pictogram. Dit pictogram ziet er als een reeks van de kwadraten uit. Selecteer in de vervolgkeuzelijst Hallo die wordt weergegeven, **Hive-weergave**.

    ![Hive-weergave selecteren](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. Wanneer Hallo Hive-weergave wordt geladen plakken Hallo volgende query uitvoeren op Hallo Query-Editor en klik vervolgens op **uitvoeren**.

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    Zodra Hallo-taak is voltooid, ziet u Hallo uitvoer weergegeven in Hallo **resultaten queryproces** sectie. Hallo resultaten moeten vergelijkbaar toohello volgende tekst:

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. Selecteer Hallo **logboek** tabblad. Ziet u informatie vergelijkbare toohello volgende tekst:

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    Hallo opslaan **App-id** waarde, zoals deze waarde wordt gebruikt in de volgende sectie Hallo.

## <a name="use-hello-tez-view"></a>Gebruik Hallo Tez weergeven

1. Selecteer Hallo Hallo menu bovenaan Hallo Hallo pagina **weergaven** pictogram. Selecteer in de vervolgkeuzelijst Hallo die wordt weergegeven, **Tez weergave**.

    ![Tez weergave selecteren](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. Als Hallo Tez weergave wordt geladen, ziet u een lijst met hive-query's die momenteel worden uitgevoerd, of zijn uitgevoerd op Hallo-cluster.

    ![Alle dag 's](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. Als u slechts één vermelding hebt, is het voor Hallo-query die u hebt uitgevoerd in de vorige sectie Hallo. Als u meerdere vermeldingen hebt, kunt u zoeken met behulp van Hallo velden bovenaan Hallo Hallo pagina.

4. Selecteer Hallo **Query-ID** voor een Hive-query. Informatie over het Hallo-query wordt weergegeven.

    ![Details van de DAG](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. Hallo tabbladen op deze pagina kunt u tooview Hallo volgende informatie:

    * **Details van een query**: meer informatie over Hallo Hive-query.
    * **Tijdlijn**: informatie over hoe lang duurde in elke fase van de verwerking.
    * **Configuraties**: Hallo-configuratie voor deze query gebruikt.

    Van __Query Details__ kunt u Hallo koppelingen toofind informatie over Hallo __toepassing__ of Hallo __DAG__ voor deze query.
    
    * Hallo __toepassing__ koppeling geeft informatie weer over Hallo YARN-toepassing voor deze query. Hier kunt u Hallo YARN-Logboeken openen.
    * Hallo __DAG__ koppeling geeft informatie weer over Hallo gerichte acyclische grafiek voor deze query. Hier kunt u een grafische weergave van Hallo DAG weergeven. U kunt ook informatie over Hallo hoekpunten binnen Hallo DAG vinden.

## <a name="next-steps"></a>Volgende stappen

U hebt geleerd hoe toouse hello Tez bekijken, meer informatie over [met behulp van Hive in HDInsight](hdinsight-use-hive.md).

Zie voor meer technische informatie op Tez hello [Tez-pagina op Hortonworks](http://hortonworks.com/hadoop/tez/).

Zie voor meer informatie over het gebruik van Ambari met HDInsight [beheren HDInsight-clusters met Hallo Ambari-Webgebruikersinterface](hdinsight-hadoop-manage-ambari.md)

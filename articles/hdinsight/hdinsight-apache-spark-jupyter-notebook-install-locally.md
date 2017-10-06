---
title: lokaal aaaInstall Jupyter & verbinding maken met tooan Azure HDInsight Spark-cluster | Microsoft Docs
description: Meer informatie over hoe tooinstall Jupyter-notebook lokaal op uw computer en sluit het tooan Apache Spark-cluster in Azure HDInsight.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a>Jupyter-notebook installeert op uw computer en sluit u tooApache Spark in HDInsight

In dit artikel leert u hoe tooinstall Jupyter-notebook Hello aangepaste PySpark (voor Python) en Spark (voor Scala) kernels met Spark magic, en koppel Hallo notebook tooan HDInsight-cluster. Er is een aantal redenen tooinstall Jupyter op uw lokale computer en kunnen er ook enkele uitdagingen. Zie voor meer informatie over dit Hallo sectie [waarom zou ik Jupyter installeren op mijn computer](#why-should-i-install-jupyter-on-my-computer) aan Hallo einde van dit artikel.

Er zijn drie belangrijke stappen die betrokken zijn bij het installeren van Jupyter en Hallo Spark magic op uw computer.

* Jupyter-notebook installeren
* Hallo PySpark en Spark kernels Hello Spark verwerkt Magic-pakket installeren
* Spark magische tooaccess Spark-cluster in HDInsight configureren

Zie voor meer informatie over aangepaste kernels Hallo en Hallo Spark magic beschikbaar voor Jupyter-notebooks met HDInsight-cluster [beschikbare Kernels voor Jupyter-notebooks met Apache Spark Linux-clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Vereisten
Hallo-vereisten die hier worden vermeld, zijn niet voor het installeren van Jupyter. Dit zijn voor maken van verbinding Hallo Jupyter-notebook tooan HDInsight-cluster nadat Hallo notebook is geïnstalleerd.

* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Een Apache Spark-cluster in HDInsight. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="install-jupyter-notebook-on-your-computer"></a>Jupyter-notebook op uw computer installeren

Voordat u de Jupyter-notebooks kunt installeren, moet u Python installeren. Zowel Python en Jupyter zijn beschikbaar als onderdeel van Hallo [Anaconda distributie](https://www.continuum.io/downloads). Als u Anaconda installeert, installeert u een distributiepunt van Python. Nadat Anaconda is geïnstalleerd, voegt u Hallo Jupyter installatie door de juiste opdrachten uit te voeren.

1. Hallo downloaden [Anaconda-installatieprogramma](https://www.continuum.io/downloads) voor uw platform en Voer Hallo setup. Tijdens het actieve Hallo-installatiewizard, moet dat u Hallo optie tooadd Anaconda tooyour padvariabele selecteren.
2. Hallo na de opdracht tooinstall Jupyter worden uitgevoerd.

        conda install jupyter

    Zie voor meer informatie over het installeren van Jupyter [installeren Jupyter met Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).

## <a name="install-hello-kernels-and-spark-magic"></a>Hallo kernels en Spark verwerkt Magic-pakket installeren

Voor instructies over hoe tooinstall Hallo Spark magic, Hallo PySpark en Spark-kernels Hallo installatie-instructies in Hallo volgen [sparkmagic documentatie](https://github.com/jupyter-incubator/sparkmagic#installation) op GitHub. Hallo eerste stap bij het Hallo Spark magische documentatie wordt u gevraagd tooinstall Spark magic. Deze eerste stap bij het Hallo-koppeling vervangen door Hallo-opdrachten, afhankelijk van de versie Hallo van Hallo maakt u verbinding met HDInsight-cluster te volgen. Volg daarna Hallo resterende stappen in Hallo Spark magische documentatie. Als u wilt dat tooinstall Hallo verschillende kernels, voert u stap 3 in Hallo sectie Spark magische installatie-instructies.

* Voor clusters v3.4, installeert u sparkmagic 0.2.3 door te voeren`pip install sparkmagic==0.2.3`

* Installeren voor clusters v3.5 en v3.6 sparkmagic 0.11.2 door`pip install sparkmagic==0.11.2`

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a>Spark magische tooconnect tooHDInsight Spark-cluster configureren

In deze sectie configureert u Hallo Spark magic die u eerder tooconnect tooan Apache Spark-cluster dat moet u al hebt gemaakt in Azure HDInsight geïnstalleerd.

1. Hallo Jupyter-configuratie-informatie wordt meestal opgeslagen in de basismap Hallo-gebruikers. de opdrachten toolocate uw basismap op een besturingssysteem of platform, type hello te volgen.

    Hallo Python shell starten. Typ op een opdrachtvenster Hallo volgende:

        python

    Voer op Hallo Python-shell, Hallo toofind opdracht out Hallo basismap te volgen.

        import os
        print(os.path.expanduser('~'))

2. Navigeer toohello basismap en maak een map **.sparkmagic** als deze niet al bestaat.
3. Maak een bestand met de naam in de map Hallo, **config.json** en Hallo JSON-fragment in het volgende toe te voegen.

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. Vervang **{USERNAME}**, **{CLUSTERDNSNAME}**, en **{BASE64ENCODEDPASSWORD}** met de juiste waarden. U kunt een aantal hulpprogramma's in uw favoriete programmeertaal of online toogenerate een met base64 gecodeerde wachtwoord gebruiken om uw huidige wachtwoord.

5. Hallo rechts heartbeatinstellingen configureren in `config.json`. U moet deze instellingen toevoegen op hetzelfde niveau als Hallo Hallo `kernel_python_credentials` en `kernel_scala_credentials` codefragmenten uw toegevoegde eerder. Zie voor een voorbeeld van hoe en waar tooadd heartbeat-instellingen Hallo [voorbeeld config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).

    * Voor `sparkmagic 0.2.3` (clusters met v3.4) omvatten:

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * Voor `sparkmagic 0.11.2` (clusters v3.5 en v3.6), zijn onder andere:

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    >Heartbeats worden verzonden tooensure sessies niet gelekt. Wanneer een computer toosleep gaat of wordt afgesloten, Hallo heartbeat is niet verzonden, wat resulteert in het Hallo-sessie wordt opgeschoond. Voor clusters v3.4, indien toodisable dit gedrag gewenst kunt u instellen Hallo Livy config `livy.server.interactive.heartbeat.timeout` te`0` van Hallo Ambari UI. Voor clusters v3.5, als u geen Hallo 3.5 configuratie bovenstaande instelt worden Hallo sessie niet verwijderd.

6. Jupyter starten. Gebruiken de volgende opdracht uit via de opdrachtprompt Hallo Hallo.

        jupyter notebook

7. Controleer of u kunt verbinding maken met Jupyter-notebook Hallo en dat u kunt Hallo Spark magic beschikbaar met Hallo kernels toohello-cluster. Hallo stappen uitvoeren.

    a. Maak een nieuwe notebook. Vanuit de rechterhoek hello, klikt u op **nieuw**. U ziet Hallo standaard kernel **Python2** en twee nieuwe kernels die u installeert, Hallo **PySpark** en **Spark**. Klik op **PySpark**.

    ![Kernels in Jupyter-notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter-notebook")

    b. Hallo volgende codefragment worden uitgevoerd.

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    Als u Hallo uitvoer met succes ophalen kunt, wordt uw verbinding toohello HDInsight-cluster getest.

    >[!TIP]
    >Als u tooupdate Hallo notebook configuratie tooconnect tooa naar een cluster wilt, moet u Hallo config.json bijwerken met Hallo nieuwe set waarden, zoals u in stap 3 hierboven.

## <a name="why-should-i-install-jupyter-on-my-computer"></a>Waarom zou ik Jupyter installeren op mijn computer?
Er is een getal van redenen waarom u mogelijk tooinstall Jupyter op uw computer wilt en klikt u vervolgens verbinding maken met tooa Spark in HDInsight-cluster.

* Hoewel Jupyter-notebooks al beschikbaar op Hallo Spark-cluster in Azure HDInsight zijn, biedt Jupyter installeert op uw computer u Hallo optie toocreate uw notitieblokken lokaal, uw toepassing testen op een actief cluster en vervolgens uploaden Hallo laptops toohello cluster. tooupload hello notitieblokken toohello cluster, kunt u ofwel uploaden dat ze met behulp van Hallo Jupyter-notebook die wordt uitgevoerd of Hallo cluster of toohello /HdiNotebooks map opslaan in Hallo storage-account is gekoppeld aan het Hallo-cluster. Zie voor meer informatie over hoe notitieblokken op Hallo cluster worden opgeslagen, [waar zijn Jupyter-notebooks opgeslagen](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?
* Met Hallo-laptops beschikbaar lokaal, kunt u toodifferent Spark-clusters op basis van uw vereisten voor toepassingsimplementatie.
* U kunt GitHub tooimplement een bronbeheersysteem en versiebeheer voor Hallo notitieblokken hebt. U kunt ook een samenwerkingsomgeving waar meerdere gebruikers met Hallo dezelfde werken kunnen hebben notebook.
* U kunt lokaal werken met notitieblokken zonder zelfs een cluster van. U hoeft alleen een cluster tootest uw notitieblokken tegen, niet toomanually beheren uw notitieblokken of een ontwikkelomgeving.
* Het is mogelijk beter tooconfigure uw eigen lokale ontwikkelingsomgeving dan tooconfigure hello Jupyter-installatie op Hallo-cluster.  U kunt profiteren van alle Hallo-software die u lokaal hebt geïnstalleerd zonder het configureren van een of meer externe clusters.

> [!WARNING]
> Met Jupyter op uw lokale computer geïnstalleerd, kunnen meerdere gebruikers Hallo uitvoeren dezelfde notebook op dezelfde Spark-cluster op Hallo Hallo hetzelfde moment. In een dergelijke situatie worden meerdere Livy sessies gemaakt. Als u een probleem ondervindt toodebug dat, moeten een complexe taak tootrack welke sessie Livy toowhich gebruiker behoort.
>
>

## <a name="seealso"></a>Zie ook
* [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenario's
* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen](hdinsight-apache-spark-eventhub-streaming.md)
* [Websitelogboekanalyse met Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Toepassingen maken en uitvoeren
* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Tools en uitbreidingen
* [De invoegtoepassing HDInsight Tools voor IntelliJ IDEA toocreate en verzenden van Spark Scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md)
* [De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Externe pakketten gebruiken met Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)

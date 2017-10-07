---
title: "aaaDeploy en beheren van Apache Storm-topologieën op HDInsight | Microsoft Docs"
description: "Ontdek hoe toodeploy, bewaken en beheren van Apache Storm-topologieën op HDInsight met behulp van Hallo Storm-Dashboard. Hadoop-hulpprogramma's voor Visual Studio gebruiken."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a>Implementeren en beheren van Apache Storm-topologieën op HDInsight op basis van Windows

Hallo Storm-Dashboard kunt u tooeasily implementeren en uitvoeren van Apache Storm-topologieën tooyour HDInsight-cluster met behulp van uw webbrowser. U kunt ook Hallo dashboard toomonitor gebruiken en beheren van actieve topologieën. Als u Visual Studio gebruikt, geef Hallo HDInsight Tools voor Visual Studio soortgelijke functies in Visual Studio.

Hallo Storm-Dashboard en Hallo Storm-onderdelen in HDInsight Tools Hallo afhankelijk Hallo Storm REST API, die gebruikt toocreate worden kunnen uw eigen oplossingen bewaking en beheer.

> [!IMPORTANT]
> Hallo stappen in dit document moet een Storm op HDInsight-cluster dat gebruik maakt van Windows hello-besturingssysteem. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.
>
> Zie voor meer informatie over het implementeren en beheren van Storm-topologieën met een HDInsight-cluster dat gebruik maakt van Linux [implementeren en beheren van Apache Storm-topologieën op HDInsight op basis van Linux](hdinsight-storm-deploy-monitor-topology-linux.md)

## <a name="prerequisites"></a>Vereisten

* **Apache Storm op HDInsight** -Zie [aan de slag met Apache Storm op HDInsight](hdinsight-apache-storm-tutorial-get-started.md) voor stapsgewijze instructies voor het maken van een cluster.

* Voor Hallo **Storm-Dashboard**: een moderne webbrowser met ondersteuning voor HTML5.

* Voor **Visual Studio** -SDK van Azure 2.5.1 of hoger en hello HDInsight Tools voor Visual Studio. Zie [aan de slag met HDInsight Tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall en Hallo HDInsight tools voor Visual Studio configureren.

    Een van de volgende versies van Visual Studio Hallo:

  * Visual Studio 2012 met Update 4

  * Visual Studio 2013 met Update 4 of Visual Studio 2013 Community

  * Visual Studio 2015 (alle versies)

  * Visual Studio 2017 (alle versies)

## <a name="storm-dashboard"></a>Storm-Dashboard

Hallo Storm-Dashboard is een webpagina die beschikbaar is op uw Storm-cluster. Hallo-URL is **https://&lt;clustername >.azurehdinsight.net/**, waarbij **clustername** Hallo-naam van uw Storm op HDInsight-cluster.

Vanaf de bovenkant van de Hallo Hallo Storm-Dashboard, selecteert u **indienen topologie**. Hallo-instructies op Hallo pagina toorun een voorbeeld topologie of tooupload volgen en voer een topologie die u hebt gemaakt.

![Hallo topologie pagina verzenden][storm-dashboard-submit]

### <a name="storm-ui"></a>Storm-gebruikersinterface

Hallo Storm-Dashboard, selecteer Hallo **Storm-gebruikersinterface** koppeling. Dit geeft informatie weer over Hallo-cluster in toevoeging tooany actieve topologieën.

![Hallo storm-gebruikersinterface][storm-dashboard-ui]

> [!NOTE]
> In sommige versies van Internet Explorer ontdekt u dat Hallo die storm-gebruikersinterface worden niet vernieuwd nadat u het eerst hebt bezocht. Bijvoorbeeld, kan niet worden weergegeven Hallo nieuwe topologieën die u hebt ingediend, of een topologie als actief kan worden weergegeven wanneer eerder gedeactiveerd. Microsoft is op de hoogte van dit probleem en werkt aan een oplossing.

#### <a name="main-page"></a>Hoofdpagina

Hallo hoofdpagina Hallo Storm-gebruikersinterface biedt Hallo volgende informatie:

* **Cluster samenvatting**: algemene informatie over Hallo Storm-cluster.

* **Topologie samenvatting**: een lijst met actieve topologieën. Hallo-koppelingen in deze sectie tooview meer informatie over specifieke topologieën gebruiken.

* **Supervisor samenvatting**: informatie over Hallo Storm supervisor.

* **Nimbus configuratie**: Nimbus-configuratie voor Hallo-cluster.

#### <a name="topology-summary"></a>Topologie samenvatting

Wanneer u een koppeling van Hallo **Topology summary** sectie vindt u informatie over het Hallo-topologie na Hallo:

* **Topologie samenvatting**: algemene informatie over het Hallo-topologie.

* **Topologie acties**: acties die u voor Hallo-topologie uitvoeren kunt.

  * **Activeren**: verwerking van een gedeactiveerde topologie wordt hervat.

  * **Deactiveren**: een actieve topologie wordt onderbroken.

  * **Opnieuw verdelen**: Hallo parallelle uitvoering van Hallo-topologie wordt aangepast. Nadat u het aantal knooppunten in cluster Hallo Hallo hebt gewijzigd, moet u actieve topologieën opnieuw verdelen. Hierdoor kan het Hallo-topologie tooadjust parallelle uitvoering toocompensate voor Hallo verhoogd of verlaagd van het aantal knooppunten in cluster Hallo.

      Zie voor meer informatie [begrijpen Hallo parallelle uitvoering van een Storm-topologie (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

  * **Kill**: een Storm-topologie wordt beëindigd nadat Hallo time-out opgegeven.

* **Topology stats**: statistieken over Hallo-topologie. Gebruik Hallo koppelingen in Hallo **venster** kolom tooset Hallo periode Hallo resterend posten op Hallo pagina.

* **Spouts**: Hallo spouts die wordt gebruikt door het Hallo-topologie. Hallo-koppelingen in deze sectie tooview meer informatie over specifieke spouts gebruiken.

* **Bolts**: Hallo bolts gebruikt door het Hallo-topologie. Gebruik Hallo koppelingen in deze sectie tooview meer informatie over specifieke bolts.

* **Topologieconfiguratie**: Hallo configuratie van de topologie Hallo geselecteerd.

#### <a name="spout-and-bolt-summary"></a>Spout en Bolt samenvatting

Selecteren van een spout in Hallo **Spouts** of **Bolts** secties Hallo volgende informatie over Hallo geselecteerd item wordt weergegeven:

* **Overzicht van onderdelen**: algemene informatie over Hallo spout of bolt.

* **Spout/Bolt stats**: statistieken over Hallo spout of Bolts. Gebruik Hallo koppelingen in Hallo **venster** kolom tooset Hallo periode Hallo resterend posten op Hallo pagina.

* **Input stats** (alleen Bolts): informatie over Hallo invoerstromen verbruikt door Hallo bolt.

* **Output stats**: informatie over Hallo stromen die door dit spout of Bolts.

* **Executor**: informatie over het Hallo-exemplaren van Hallo spout of bolt. Selecteer Hallo **poort** vermelding voor een specifieke executor tooview een logboek van diagnostische gegevens geproduceerd voor dit exemplaar.

* **Fouten**: alle informatie over de fout voor deze spout of Bolts.

## <a name="hdinsight-tools-for-visual-studio"></a>HDInsight-hulpprogramma's voor Visual Studio

Hallo HDInsight-hulpprogramma's kunnen worden gebruikt toosubmit C# of hybride topologieën tooyour Storm-cluster. Hallo stappen te volgen, gebruiken een voorbeeldtoepassing. Zie voor meer informatie over het maken van uw eigen topologieën met behulp van Hallo HDInsight Tools [C#-topologieën ontwikkelen met Hallo HDInsight Tools voor Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Gebruik Hallo volgende stappen toodeploy een voorbeeld tooyour Storm op HDInsight-cluster, en vervolgens weergeven en beheren van Hallo-topologie.

1. Als u hebt niet is gebeurd Hallo meest recente versie van Hallo HDInsight Tools voor Visual Studio, Zie [aan de slag met HDInsight Tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Open Visual Studio, selecteer **bestand** > **nieuw** > **Project**.

3. In Hallo **nieuw Project** dialoogvenster Vouw **geïnstalleerde** > **sjablonen**, en selecteer vervolgens **HDInsight**. Selecteer in de lijst met sjablonen Hallo **Storm voorbeeld**. Typ een naam voor de toepassing hello Hallo onderaan in het dialoogvenster voor Hallo in.

    ![Afbeelding](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **indienen tooStorm op HDInsight**.

   > [!NOTE]
   > Als u wordt gevraagd, voert u Hallo aanmeldingsreferenties voor uw Azure-abonnement. Als u meer dan één abonnement hebt, meldt u zich in toohello een bestand met uw Storm op HDInsight-cluster.

5. Selecteer uw Storm op HDInsight-cluster in Hallo **Storm-Cluster** vervolgkeuzelijst en selecteer vervolgens **indienen**. U kunt controleren of Hallo verzending is voltooid met Hallo **uitvoer** venster.

6. Wanneer het Hallo-topologie is ingediend, Hallo **Storm-topologieën** voor Hallo cluster moet worden weergegeven. Selecteer Hallo-topologie in Hallo lijst tooview informatie over Hallo topologie wordt uitgevoerd.

    ![monitor voor Visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > U kunt ook weergeven **Storm-topologieën** van **Server Explorer** door het uitbreiden van **Azure** > **HDInsight**, en klik vervolgens met de rechtermuisknop op een Storm op HDInsight-cluster en het selecteren van **weergave Storm-topologieën**.

    Selecteer Hallo shape voor Hallo spouts of bolts tooview informatie over deze onderdelen. Er wordt een nieuw venster geopend voor elk item geselecteerd.

   > [!NOTE]
   > Hallo-naam van Hallo topologie Hallo klassenaam van Hallo-topologie is (in dit geval `HelloWord`,) met een tijdstempel toegevoegd.

7. Van Hallo **Topology Summary** weergave, selecteer **Kill** toostop Hallo topologie.

   > [!NOTE]
   > Storm-topologieën blijft in uitvoering totdat ze zijn gestopt of Hallo cluster wordt verwijderd.


## <a name="rest-api"></a>REST API

Hallo Storm-gebruikersinterface is gebaseerd op Hallo REST API, zodat u kunt vergelijkbare management en de controlefunctionaliteit met behulp van Hallo REST-API. U kunt Hallo REST-API toocreate aangepaste hulpprogramma's gebruiken voor het beheren en controleren van Storm-topologieën.

Zie voor meer informatie [Storm UI REST-API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md). Hallo is volgende informatie specifiek toousing Hallo REST-API met Apache Storm op HDInsight.

### <a name="base-uri"></a>Basis-URI

Hallo basis-URI voor Hallo REST-API op HDInsight-clusters is **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**, waarbij **clustername** is Hallo-naam van uw Storm op HDInsight-cluster.

### <a name="authentication"></a>Authentication

Aanvragen toohello REST-API moet gebruiken **basisverificatie**, zodat u Hallo HDInsight-cluster beheerdersnaam en het wachtwoord gebruiken.

> [!NOTE]
> Omdat basisverificatie wordt verzonden met behulp van de versleutelde tekst, moet u **altijd** toosecure-HTTPS-communicatie met de Hallo-cluster gebruiken.

### <a name="return-values"></a>Waarden geretourneerd

Informatie die wordt geretourneerd vanaf Hallo REST-API is mogelijk alleen bruikbaar uit binnen Hallo cluster of virtuele machines op Hallo hetzelfde virtuele Azure-netwerk als Hallo-cluster. Hallo volledig gekwalificeerde domeinnaam (FQDN) geretourneerd voor Zookeeper-servers zijn bijvoorbeeld niet worden toegankelijk is vanaf Internet Hallo.

## <a name="next-steps"></a>Volgende stappen

Nu u hebt geleerd hoe toodeploy en monitor topologieën met behulp van Storm-Dashboard hello, kunt u nagaan hoe:

* [C#-topologieën met Hallo HDInsight Tools voor Visual Studio ontwikkelen](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [Java gebaseerde topologieën met Maven ontwikkelen](hdinsight-storm-develop-java-topology.md)

Zie voor een lijst van meer voorbeeldtopologieën [voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md).

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png

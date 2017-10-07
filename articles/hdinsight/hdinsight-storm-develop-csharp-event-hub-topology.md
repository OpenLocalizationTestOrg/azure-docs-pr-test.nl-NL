---
title: aaaProcess gebeurtenissen van Event Hubs met Storm - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe tooprocess gegevens uit Azure Event Hubs met een C# Storm-topologie gemaakt in Visual Studio met Hallo HDInsight tools voor Visual Studio.
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a>Procesgebeurtenissen van Azure Event Hubs met Storm op HDInsight (C#)

Meer informatie over hoe toowork met Azure Event Hubs van Apache Storm op HDInsight. Dit document wordt een C# Storm-topologie tooread en write gegevens uit Evbent Hubs

> [!NOTE]
> Zie voor een Java-versie van dit project, [verwerken van gebeurtenissen van Azure Event Hubs met Storm op HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="scpnet"></a>SCP.NET

Hallo stappen in dit document gebruikt SCP.NET, een NuGet-pakket dat u het eenvoudig toocreate C#-topologieën en -onderdelen voor gebruik met Storm op HDInsight maakt.

> [!IMPORTANT]
> Tijdens het Hallo stappen in dit document kan zijn afhankelijk van een Windows-ontwikkelomgeving met Visual Studio, Hallo gecompileerd project ingediende tooa Storm op HDInsight-cluster dat gebruik maakt van Linux. Op basis van Linux-clusters die zijn gemaakt na 28 oktober 2016 ondersteunen alleen SCP.NET topologieën.

HDInsight 3.4 en groter gebruiken Mono toorun C#-topologieën. Hallo-voorbeeld gebruikt in dit document werkt met HDInsight 3.6. Als u van plan om uw eigen .NET-oplossingen voor HDInsight te maken bent, controleert u Hallo [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/) document voor potentiële compatibiliteitsproblemen.

### <a name="cluster-versioning"></a>Cluster-versies

Hallo Microsoft.SCP.Net.SDK NuGet-pakket die u voor uw project gebruikt moet overeenkomen met de Hallo primaire versie van Storm op HDInsight is geïnstalleerd. HDInsight versie 3.5 en 3.6 Storm gebruiken 1.x, dus moet u SCP.NET versie 1.0.x.x met deze clusters gebruiken.

> [!IMPORTANT]
> Hallo-voorbeeld in dit document verwacht een HDInsight-3.5 of 3,6 cluster.
>
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

C#-topologieën moeten ook .NET 4.5 gericht.

## <a name="how-toowork-with-event-hubs"></a>Hoe toowork met Event Hubs

Microsoft biedt een set van Java-onderdelen die gebruikt toocommunicate met Event Hubs van een Storm-topologie worden kunnen. U vindt Hallo Java-archief (JAR)-bestand met een compatibele versie van HDInsight 3.6 van deze onderdelen bij [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).

> [!IMPORTANT]
> Tijdens het Hallo-onderdelen zijn geschreven in Java, kunt u deze eenvoudig gebruiken van een C#-topologie.

Hallo volgende onderdelen worden gebruikt in dit voorbeeld:

* __EventHubSpout__: leest de gegevens uit Event Hubs.
* __EventHubBolt__: schrijft gegevens tooEvent Hubs.
* __EventHubSpoutConfig__: tooconfigure EventHubSpout gebruikt.
* __EventHubBoltConfig__: tooconfigure EventHubBolt gebruikt.

### <a name="example-spout-usage"></a>Voorbeeld van spout syntaxis

SCP.NET biedt methoden voor het toevoegen van een EventHubSpout tooyour-topologie. Deze methoden maken het gemakkelijker tooadd een spout dan het gebruik van Hallo algemene methoden voor het toevoegen van een Java-component. Hallo volgende voorbeeld laat zien hoe een spout met behulp van toocreate Hallo __SetEventHubSpout__ en **EventHubSpoutConfig** methoden van SCP.NET:

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

Hallo vorige voorbeeld maakt u een nieuw spout-onderdeel met de naam __EventHubSpout__, en configureert deze toocommunicate met een event hub. Hallo parallelle uitvoering hint voor Hallo onderdeel is het aantal partities toohello ingesteld in Hallo event hub. Deze instelling kunt u Storm toocreate een exemplaar van Hallo-onderdeel voor elke partitie.

### <a name="example-bolt-usage"></a>Voorbeeld van bolt syntaxis

Gebruik Hallo **JavaComponmentConstructor** methode toocreate een exemplaar van Hallo bolt. Hallo volgende voorbeeld laat zien hoe toocreate en configureren van een nieuw exemplaar van Hallo **EventHubBolt**:

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> In dit voorbeeld wordt een Clojure expressie doorgegeven als een tekenreeks, in plaats van **JavaComponentConstructor** toocreate een **EventHubBoltConfig**, zoals Hallo spout voorbeeld hebt. De methode werkt. Hallo methode gebruiken die aanbevolen tooyou werkt.

## <a name="download-hello-completed-project"></a>Hallo voltooid-project downloaden

U kunt een volledige versie van het Hallo-project gemaakt in deze zelfstudie uit downloaden [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub). U moet echter nog steeds tooprovide configuratie-instellingen door Hallo stappen in deze zelfstudie te volgen.

### <a name="prerequisites"></a>Vereisten

* Een [Apache Storm op HDInsight-cluster versie 3.5 of 3.6](hdinsight-apache-storm-tutorial-get-started.md).

    > [!WARNING]
    > Hallo-voorbeeld gebruikt in dit document vereist Storm op HDInsight versie 3.5 of 3.6. Dit werkt niet met oudere versies van HDInsight, vanwege wijzigingen in de naam toobreaking klasse. Zie voor een versie van dit voorbeeld dat met oudere clusters werkt [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).

* Een [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* Hallo [Azure .NET SDK](http://azure.microsoft.com/downloads/).

* Hallo [HDInsight tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

* Java JDK 1.8 of hoger op uw ontwikkelomgeving. JDK downloads zijn beschikbaar op [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

  * Hallo **JAVA_HOME** omgeving variabele moet punt toohello directory met Java.
  * Hallo **%JAVA_HOME%/bin** directory in Hallo-pad moet worden uitgevoerd.

## <a name="download-hello-event-hubs-components"></a>Hallo Event Hubs-onderdelen downloaden

Download Hallo Event Hubs spout en Bolts onderdeel uit [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).

Maak een map met de naam `eventhubspout`, en Hallo-bestand op te slaan in directory Hallo.

## <a name="configure-event-hubs"></a>Event Hubs configureren

Event Hubs is Hallo gegevensbron voor dit voorbeeld. Gebruik Hallo informatie in 'Een event hub maken' Hallo-sectie van [aan de slag met Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

1. Nadat het Hallo event hub is gemaakt, weergeven Hallo **EventHub** blade in Azure portal en selecteer Hallo **gedeeld toegangsbeleid**. Selecteer **+ toevoegen** tooadd Hallo beleidsregels te volgen:

   | Naam | Machtigingen |
   | --- | --- |
   | schrijver |Verzenden |
   | lezer |Luisteren |

    ![Schermafbeelding van de Share access beleid-venster](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. Selecteer Hallo **lezer** en **writer** beleid. Kopieer en Hallo waarde primaire sleutel voor beide beleidsregels niet opslaan omdat deze waarden later worden gebruikt.

## <a name="configure-hello-eventhubwriter"></a>Hallo EventHubWriter configureren

1. Als u hebt niet is gebeurd Hallo meest recente versie van Hallo HDInsight tools voor Visual Studio, Zie [aan de slag met HDInsight tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Hallo-oplossing van downloaden [eventhub-storm-hybride](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).

3. In Hallo **EventHubWriter** project, open Hallo **App.config** bestand. Gebruik de informatie van de Hallo van Hallo event hub dat u eerder toofill geconfigureerd in Hallo-waarde voor Hallo sleutels te volgen:

   | Sleutel | Waarde |
   | --- | --- |
   | EventHubPolicyName |schrijver (als u een andere naam voor beleid met de Hallo gebruikt *verzenden* toestemming hebben, in plaats daarvan gebruikt.) |
   | EventHubPolicyKey |Hallo-sleutel voor Hallo writer beleid. |
   | EventHubNamespace |Hallo-naamruimte die uw event hub bevat. |
   | EventHubName |De naam van de event hub. |
   | EventHubPartitionCount |Hallo aantal partities in de event hub. |

4. Opslaan en sluiten Hallo **App.config** bestand.

## <a name="configure-hello-eventhubreader"></a>Hallo EventHubReader configureren

1. Open Hallo **EventHubReader** project.

2. Open Hallo **App.config** -bestand voor Hallo **EventHubReader**. Gebruik de informatie van de Hallo van Hallo event hub dat u eerder toofill geconfigureerd in Hallo-waarde voor Hallo sleutels te volgen:

   | Sleutel | Waarde |
   | --- | --- |
   | EventHubPolicyName |lezer (als u een andere naam voor beleid met de Hallo gebruikt *luisteren* toestemming hebben, in plaats daarvan gebruikt.) |
   | EventHubPolicyKey |Hallo-sleutel voor Hallo lezer beleid. |
   | EventHubNamespace |Hallo-naamruimte die uw event hub bevat. |
   | EventHubName |De naam van de event hub. |
   | EventHubPartitionCount |Hallo aantal partities in de event hub. |

3. Opslaan en sluiten Hallo **App.config** bestand.

## <a name="deploy-hello-topologies"></a>Hallo-topologieën implementeren

1. Van **Solution Explorer**, klik met de rechtermuisknop Hallo **EventHubReader** project en selecteer **indienen tooStorm op HDInsight**.

    ![Schermopname van Solution Explorer met indienen tooStorm op HDInsight gemarkeerd](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. Op Hallo **topologie indienen** in het dialoogvenster, selecteer uw **Storm-Cluster**. Vouw **aanvullende configuraties**, selecteer **Java bestandspaden**, selecteer **...** , en selecteer Hallo directory waarin Hallo JAR-bestand dat u eerder hebt gedownload. Tot slot op **indienen**.

    ![Dialoogvenster Schermafbeelding van de indienings-topologie](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. Wanneer het Hallo-topologie is ingediend, Hallo **Storm-topologieën Viewer** wordt weergegeven. tooview informatie over het Hallo-topologie, selecteer Hallo **EventHubReader** topologie in het linkerdeelvenster Hallo.

    ![Schermopname van Storm-topologieën Viewer](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. Van **Solution Explorer**, klik met de rechtermuisknop Hallo **EventHubWriter** project en selecteer **indienen tooStorm op HDInsight**.

5. Op Hallo **topologie indienen** in het dialoogvenster, selecteer uw **Storm-Cluster**. Vouw **aanvullende configuraties**, selecteer **Java bestandspaden**, selecteer **...** , en selecteer Hallo map Hallo JAR-bestand met u eerder hebt gedownload. Tot slot op **indienen**.

6. Wanneer het Hallo-topologie is ingediend, vernieuw de lijst met de Hallo-topologie in Hallo **Storm-topologieën Viewer** tooverify die beide topologieën op Hallo cluster worden uitgevoerd.

7. In **Storm-topologieën Viewer**, selecteer Hallo **EventHubReader** topologie.

8. tooopen hello onderdeel samenvatting voor Hallo bolt, dubbelklikt u op Hallo **LogBolt** onderdeel in het Hallo-diagram.

9. In Hallo **Executor** sectie, selecteert u een van de koppelingen Hallo in Hallo **poort** kolom. U ziet nu informatie die wordt geregistreerd door Hallo-onderdeel. Hallo geregistreerd informatie is vergelijkbaar toohello volgende tekst:

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a>Hallo topologieën stoppen

toostop hello topologieën, selecteert u elke topologie in Hallo **Storm-topologie Viewer**, klikt u vervolgens op **Kill**.

![Schermopname van Storm-topologie-Viewer met Kill knop gemarkeerd](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Uw cluster verwijderen

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Volgende stappen

In dit document hebt u geleerd hoe toouse Hallo Java Event Hubs spout en Bolts uit een C#-topologie-toowork met gegevens in Azure Event Hubs. toolearn meer informatie over het maken van C#-topologieën, Zie de volgende Hallo:

* [C#-topologieën ontwikkelen voor Apache Storm op HDInsight met behulp van Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Programmeerhandleiding voor SCP](hdinsight-storm-scp-programming-guide.md)
* [Voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md)

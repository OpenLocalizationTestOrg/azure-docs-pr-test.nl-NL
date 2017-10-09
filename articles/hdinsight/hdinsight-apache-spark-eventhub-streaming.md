---
title: aaaUse Apache Spark-streaming met Event Hubs in Azure HDInsight | Microsoft Docs
description: Een voorbeeld van Apache Spark-streaming voor hoe toosend data stream tooAzure Event Hub en ontvangt deze gebeurtenissen in HDInsight Spark-cluster met een scala-toepassing bouwen.
keywords: Apache spark-streaming, spark-streaming, spark-voorbeeld, apache spark-streaming bijvoorbeeld event hub azure voorbeeld, spark-voorbeeld
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a>Apache Spark-streaming: procesgegevens uit Azure Event Hubs met Spark-cluster in HDInsight

In dit artikel maakt u een Apache Spark-streaming-voorbeeld waarbij Hallo stappen te volgen:

1. U kunt een zelfstandige toepassing tooingest berichten gebruiken in een Azure Event Hub.

2. Met twee verschillende benaderingen ophalen u Hallo-berichten van Event Hub in realtime met behulp van een toepassing die wordt uitgevoerd in Spark-cluster in Azure HDInsight.

3. Als u streaming analytische pijplijnen toopersist gegevens toodifferent opslagsystemen bouwen of inzichten verkrijgen van gegevens op Hallo snel.

## <a name="prerequisites"></a>Vereisten

* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* Een Apache Spark-cluster in HDInsight. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="spark-streaming-concepts"></a>Concepten Spark-Streaming

Zie voor een gedetailleerde uitleg van Spark-streaming [Apache Spark-streaming-overzicht](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview). HDInsight biedt Hallo dezelfde streaming functies tooa Spark-cluster in Azure.  

## <a name="what-does-this-solution-do"></a>Wat doet deze oplossing?

Voer in dit artikel wordt een voorbeeld van de Spark-streaming toocreate Hallo stappen te volgen:

1. Maak een Azure Event Hub die u een stream van gebeurtenissen ontvangt.

2. Uitvoeren van een lokale zelfstandige toepassing die wordt gegenereerd gebeurtenissen en stuurt deze toohello Azure Event Hub. Hallo-voorbeeldtoepassing die dit biedt is gepubliceerd op [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).

3. Een streaming-toepassing op afstand uitvoeren op een Spark-cluster die streaming-gebeurtenissen van Azure Event Hub leest en analyse van de verschillende gegevensverwerking /.

## <a name="create-an-azure-event-hub"></a>Een Azure Event Hub maken

1. Meld u aan toohello [Azure Portal](https://ms.portal.azure.com), en klik op **nieuw** op Hallo linksboven welkomstscherm.

2. Klik op **Internet van dingen** en vervolgens op **Event Hubs**.

    ![Create event hub voor Spark-streaming-voorbeeld](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "maken event hub voor Spark-streaming-voorbeeld")

3. In Hallo **naamruimte maken** blade, voer de naam van een naamruimte. Kies Hallo prijscategorie (basis of standaard). Ook een Azure-abonnement, resourcegroep en locatie kiezen in welke toocreate Hallo-resource. Klik op **maken** toocreate Hallo naamruimte.

      ![Geef de naam van een event hub voor Spark-streaming-voorbeeld](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "bieden u de naam van een event hub voor Spark-streaming-voorbeeld")

    > [!NOTE]
    > U selecteert moet Hallo dezelfde **locatie** als uw cluster Apache Spark in HDInsight tooreduce latentie en kosten.
    >
    >

4. Klik op Hallo gemaakte naamruimte in Hallo Event Hubs naamruimte lijst.      


5. Klik op Hallo naamruimte blade **Event Hubs**, en klik vervolgens op **+ Event Hub** toocreate nieuwe Event Hub.
   
    ![Create event hub voor Spark-streaming-voorbeeld](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "maken event hub voor Spark-streaming-voorbeeld")

6. Typ een naam voor uw Event Hub, set Hallo partitie aantal too10 en bericht bewaren too1. We zijn Hallo-berichten in deze oplossing niet archiveren zodat u kunt Hallo rest als standaard laat en klik vervolgens op **maken**.
   
    ![Geef details van gebeurtenis hub voor Spark-streaming-voorbeeld](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "event hub-informatie opgeven voor Spark-streaming-voorbeeld")

7. Hallo nieuw gemaakte Event Hub wordt vermeld in Hallo Event Hub-blade.
    
     ![Event Hub voor Hallo Spark-streaming voorbeeld weergeven](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "weergave Event Hub voor Hallo Spark-streaming voorbeeld")

8. Klik op terug in Hallo naamruimte blade (geen Hallo specifieke Event Hub blade) **gedeeld toegangsbeleid**, en klik vervolgens op **RootManageSharedAccessKey**.
    
     ![Stel beleid in de Event Hub voor Hallo Spark-streaming voorbeeld](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Event Hub ingesteld beleid voor Hallo Spark-streaming voorbeeld")

9. Klik op Hallo kopie knop toocopy Hallo **RootManageSharedAccessKey** primaire sleutel en connection string toohello Klembord. Sla deze toouse verderop in de zelfstudie Hallo.
    
     ![Event Hub beleid sleutels voor Hallo Spark-streaming voorbeeld weergeven](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "weergave Event Hub beleid sleutels voor Hallo Spark-streaming voorbeeld")

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a>Verzenden van berichten tooAzure Event Hub met behulp van een voorbeeldtoepassing Scala

In deze sectie gebruikt u een zelfstandige lokale Scala toepassing die een stream van gebeurtenissen wordt gegenereerd en verzendt het tooAzure Event Hub die u eerder hebt gemaakt. Deze toepassing is beschikbaar op GitHub op [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer). Hier Hallo stappen wordt ervan uitgegaan dat u al deze GitHub-opslagplaats hebben forked.

1. Zorg ervoor dat er Hallo volgende geïnstalleerd op Hallo-computer waarop u deze toepassing uitvoert.

    * Oracle Java Development kit. Kunt u het installeren van [hier](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
    * Apache Maven. U kunt downloaden van [hier](https://maven.apache.org/download.cgi). Vindt u instructies tooinstall Maven [hier](https://maven.apache.org/install.html).

2. Open een opdrachtprompt en navigeer toohello locatie gekloond van GitHub-repo-Hallo voor de voorbeeldtoepassing Scala Hallo en Hallo na opdracht toobuild Hallo toepassing uitvoeren.

        mvn package

3. Hallo uitvoer jar voor toepassing hello, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, wordt gemaakt onder **/target** directory. U deze JAR verderop in dit artikel tootest Hallo volledige oplossing gebruiken.

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a>Toepassing tooreceive berichten van Event Hub maken in een Spark-cluster 

Er zijn twee benaderingen tooconnect Spark-Streaming en Azure Event Hubs, verbinding op basis van de ontvanger en Direct-DStream-verbinding. Direct DStream gebaseerd is op januari 2017 geïntroduceerd in Hallo 2.0.3 release. Dit moet omdat deze meer zodat tooreplace Hallo oorspronkelijke op basis van een ontvanger verbinding en resource-efficiënt. Meer details te vinden in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs). Directe DStream ondersteunt alleen Spark 2.0 +.

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a>Toepassingen met Hallo afhankelijkheid toospark eventhubs-connector maken

We ook publiceren Hallo staging-versie van Spark-EventHubs in GitHub. toouse hello staging-versie van Spark-EventHubs: Hallo eerste stap is het tooindicate GitHub als bron opslagplaats Hallo door toe te voegen Hallo vermelding toopom.xml te volgen:

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

Vervolgens kunt u toevoegen Hallo afhankelijkheid tooyour project tootake Hallo prerelease-versie te volgen.

Maven-afhankelijkheid

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

SBT afhankelijkheid

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a>Rechtstreekse verbinding DStream

Een vooraf samengestelde jar-bestand met voorbeelden met directe DStream kan worden gedownload [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).

Hallo jar-bestand bevat drie voorbeelden waarvan de broncode zijn beschikbaar op [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).

Duurt [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) als een voorbeeld:

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

In Hallo hierboven bijvoorbeeld `eventhubParameters` zijn Hallo parameters specifieke tooa één EventHubs-exemplaar en hebt u toopass het toohello `createDirectStreams` API die een directe DStream object tooa Event Hubs toewijzingsnaamruimte vormt. U kunt op Hallo Direct DStream object DStream API's die door framework Spark-Streaming-API aanroepen. In dit voorbeeld berekenen we Hallo frequentie van elk woord in hello laatste 3 micro batch-intervallen.

### <a name="receiver-based-connection"></a>Verbinding op basis van een ontvanger

Een Spark-streaming-voorbeeldtoepassing die zijn geschreven in Scala die gebeurtenissen en route Hallo toodifferent bestemmingen ontvangt, is beschikbaar op [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples). Hallo stappen hieronder tooupdate Hallo-toepassing voor de configuratie van uw Event Hub en Hallo uitvoer jar maken.

1. Start IntelliJ IDEA en van Hallo starten scherm selecteren **uitchecken uit versiebeheer** en klik vervolgens op **Git**.
   
    ![Apache Spark-streaming-voorbeeld - get-bronnen van Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark-streaming-voorbeeld - get-bronnen van Git")

2. In Hallo **kloon opslagplaats** in het dialoogvenster bieden Hallo URL toohello Git-opslagplaats tooclone uit, geef Hallo directory tooclone aan en klik op **kloon**.
   
    ![Apache Spark-streaming-voorbeeld - kloon van Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark-streaming-voorbeeld - kloon van Git")
3. Volg Hallo aanwijzingen tot Hallo project volledig is gekloond. Druk op **Alt + 1** tooopen hello **Project-weergave**. Het bestand is vergelijkbaar Hallo volgende.
   
    ![Apache Spark-streaming-voorbeeld - Project-weergave](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark-streaming-voorbeeld - Project-weergave")
4. Zorg ervoor dat de toepassingscode Hallo is gecompileerd met Java8. tooensure, klikt u op **bestand**, klikt u op **projectstructuur**, en op Hallo **Project** tabblad, stel projectniveau taal te**8 - lambda's, het type aantekeningen, enz.**.
   
    ![Apache Spark-streaming-voorbeeld - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark-streaming-voorbeeld: Set-compiler")
5. Open Hallo **pom.xml** en zorg ervoor dat Hallo Spark versie juist is. Onder `<properties>` knooppunt, zoekt u naar Hallo volgende codefragment en controleer of Hallo Spark versie.

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. Hallo toepassing vereist een afhankelijkheid jar aangeroepen **JDBC-stuurprogramma jar**. Dit is vereiste toowrite Hallo-berichten ontvangen van de Event Hub naar een Azure SQL database. U kunt deze jar downloaden (v4.1 of hoger) van [hier](https://msdn.microsoft.com/sqlserver/aa937724.aspx). Verwijzing toothis jar in Hallo project bibliotheek toevoegen. Voer Hallo stappen te volgen:
     
     1. Vanuit IntelliJ IDEA venster waarin het hebben van Hallo toepassing openen, klikt u op **bestand**, klikt u op **projectstructuur**, en klik vervolgens op **bibliotheken**. 
     2. Klik op Hallo pictogram toevoegen (![pictogram toevoegen](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), klikt u op **Java**, en navigeert u vervolgens toohello locatie waar u Hallo JDBC-stuurprogramma jar hebt gedownload. Ga als volgt Hallo prompts tooadd Hallo jar-bestand toohello project bibliotheek.

         ![ontbrekende afhankelijkheden toevoegen](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "ontbrekende afhankelijkheid potten toevoegen")
     3. Klik op **Toepassen**.

7. Hallo uitvoer jar-bestand maken. Hallo stappen uitvoeren.

   1. In Hallo **projectstructuur** in het dialoogvenster, klikt u op **artefacten** en klik vervolgens op Hallo plus symbool. Klik in het pop-updialoogvenster hello, op **JAR**, en klik vervolgens op **van modules met afhankelijkheden**.      
       
       ![Apache Spark streaming voorbeeld - JAR maken](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "streaming voorbeeld Apache Spark - JAR maken")
   2. In Hallo **maken JAR van Modules** dialoogvenster vak, klikt u op Hallo weglatingsteken (![weglatingsteken](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) tegen Hallo **Main klasse**.
   3. In Hallo **Main-klasse selecteren** dialoogvenster vak, selecteert u een van de beschikbare klassen Hallo en klik vervolgens op **OK**.
      
       ![Apache Spark-streaming-voorbeeld - Selecteer klasse voor jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark-streaming-voorbeeld - Selecteer klasse voor jar")
   4. In Hallo **maken JAR van Modules** dialoogvenster zorg die optie hello te**toohello doel JAR extraheren** is geselecteerd en klik vervolgens op **OK**. Hiermee maakt u een één JAR met alle afhankelijkheden.
      
       ![Apache Spark streaming voorbeeld - jar maken van modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "streaming voorbeeld Apache Spark - jar van modules maken")
   5. Hallo **uitvoer indeling** tabblad bevat alle Hallo potten die opgenomen als onderdeel van Hallo Maven-project zijn. U kunt selecteren en delete Hallo toepassingsgroepen waarop Scala toepassing hello heeft geen directe afhankelijkheid. Voor de toepassing hello hier maakt, kunt u alle maar Hallo laatste (**spark-streaming-gegevens-persistentie-voorbeelden gecompileerd uitvoer**). Hallo potten toodelete selecteren en klik vervolgens op Hallo **verwijderen** pictogram (![pictogram verwijderen](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).
      
       ![Apache Spark-streaming-voorbeeld - delete uitgepakt potten](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark-streaming-voorbeeld - potten uitgepakt verwijderen")
      
       Zorg ervoor dat **bouwen op Controleer** selectievakje is ingeschakeld, waardoor wordt gegarandeerd dat jar hello wordt gemaakt telkens wanneer Hallo-project wordt gemaakt of bijgewerkt. Klik op **Toepassen**.
   6. In Hallo **uitvoer indeling** tabblad rechts onderin Hallo Hallo **beschikbare elementen** vak hebt Hallo SQL JDBC jar dat u eerder toohello project bibliotheek toegevoegd. U moet deze toohello toevoegen **uitvoer indeling** tabblad. Met de rechtermuisknop op Hallo jar-bestand en klik vervolgens op **uitpakken naar uitvoer hoofdmap**.
      
       ![Apache Spark-streaming-voorbeeld - extract afhankelijkheid jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark-streaming-voorbeeld - extract afhankelijkheid jar")  
      
       Hallo **uitvoer indeling** tabblad ziet er nu als volgt.
      
       ![Apache Spark-streaming-voorbeeld - uiteindelijke uitvoer tabblad](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark-streaming-voorbeeld - tabblad uiteindelijke uitvoer")        
      
       In Hallo **projectstructuur** in het dialoogvenster, klikt u op **toepassen** en klik vervolgens op **OK**.    
   7. In de menubalk hello, klikt u op **bouwen**, en klik vervolgens op **Project maken**. U kunt ook klikken op **bouwen artefacten** toocreate Hallo jar. Hallo uitvoer jar gemaakt onder **\classes\artifacts**.
      
       ![Apache Spark streaming voorbeeld - uitvoer JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "streaming voorbeeld Apache Spark - uitvoer JAR")

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a>Hallo-toepassing op afstand uitvoeren op een Spark-cluster met behulp van Livy

In dit artikel gebruikt u Livy toorun Hallo Apache Spark-streaming toepassing op afstand op een Spark-cluster. Zie voor gedetailleerde informatie over hoe toouse Livy met HDInsight Spark-cluster, [indienen taken op afstand tooan Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md). Voordat u kunt Hallo Spark-streaming toepassing uitvoert, zijn er zijn een aantal dingen die u moet doen:

1. Hallo lokale zelfstandige toepassingsgebeurtenissen toogenerate Start en tooEvent Hub verzonden. Hallo opdracht toodo dus volgende gebruiken:

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. Kopiëren Hallo jar streaming (**spark-streaming-gegevens-persistentie-examples.jar**) toohello Azure Blob-opslag die is gekoppeld aan het Hallo-cluster. Hierdoor Hallo jar toegankelijk tooLivy. U kunt [ **AzCopy**](../storage/common/storage-use-azcopy.md), een opdracht hulpprogramma toodo dus regel. Er zijn veel andere clients kunt u tooupload gegevens. U vindt meer informatie hierover op [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md).
3. Installeer CURL op Hallo-computer waarop u deze toepassingen worden uitgevoerd. We gebruiken CURL tooinvoke hello Livy eindpunten toorun Hallo op afstand taken.

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a>Hallo Spark streaming tooreceive Hallo toepassingsgebeurtenissen uitvoeren in een Azure Storage-Blob als tekst

Open een opdrachtprompt, navigeer toohello directory waarin u CURL hebt geïnstalleerd en Voer Hallo opdracht (vervangen gebruikersnaam en wachtwoord en het cluster name) te volgen:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

parameters in bestand Hallo Hallo **inputBlob.txt** als volgt gedefinieerd:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Laat het ons weten wat Hallo-parameters in het invoerbestand Hallo zijn:

* **bestand** Hallo pad toohello toepassing jar-bestand op Hallo Azure storage-account is gekoppeld aan het Hallo-cluster is.
* **className** Hallo naam is van het Hallo-klasse in Hallo jar.
* **argumenten** Hallo lijst met argumenten dat is vereist door Hallo-klasse
* **numExecutors** Hallo aantal kernen die wordt gebruikt door Spark toorun Hallo streaming van toepassing is. Dit moet altijd ten minste tweemaal Hallo aantal Event Hub-partities.
* **executorMemory**, **executorCores**, **driverMemory** zijn parameters gebruikt tooassign vereist resources toohello streaming-toepassing.

> [!NOTE]
> U hoeft niet toocreate Hallo uitvoermappen (EventCheckpoint, EventCount/EventCount10) die worden gebruikt als parameters. streaming-toepassing Hello ze voor u gemaakt.
>
>

Wanneer u Hallo-opdracht uitvoert, ziet u uitvoer Hallo volgende:

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

Noteer Hallo batch-ID in de laatste regel Hallo van Hallo uitvoer (in dit voorbeeld is '1'). tooverify die toepassing hello met succes wordt uitgevoerd, kunt u uw Azure storage-account die is gekoppeld aan cluster Hallo bekijken en ziet u Hallo **/EventCount/EventCount10** map er hebt gemaakt. Deze map moet bevatten blobs die worden vastgelegd Hallo aantal gebeurtenissen dat is verwerkt in Hallo periode opgegeven voor parameter Hallo **batch interval in seconden**.

Hallo Spark-streaming toepassing blijft toorun totdat u het afsluiten. toodo gebruik dus Hallo volgende opdracht:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a>Hallo toepassingen uitvoeren tooreceive Hallo gebeurtenissen in een Azure Storage-Blob als JSON
Open een opdrachtprompt, navigeer toohello directory waarin u CURL hebt geïnstalleerd en Voer Hallo opdracht (vervangen gebruikersnaam en wachtwoord en het cluster name) te volgen:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

parameters in bestand Hallo Hallo **inputJSON.txt** als volgt gedefinieerd:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Hallo-parameters zijn vergelijkbaar toowhat die u hebt opgegeven voor de tekstuitvoer Hallo in de vorige stap Hallo. Opnieuw, hoeft u niet toocreate Hallo uitvoermappen (EventCheckpoint, EventCount/EventCount10) die worden gebruikt als parameters. streaming-toepassing Hello ze voor u gemaakt.

 Nadat u Hallo-opdracht uitvoert, u uw Azure storage-account die is gekoppeld aan cluster Hallo bekijken kunt en u Hallo ziet **/EventStore10** map er hebt gemaakt. Open elk bestand voorafgegaan door **onderdeel -** en ziet u Hallo gebeurtenissen in een JSON-indeling wordt verwerkt.

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a>Hallo toepassingen tooreceive Hallo gebeurtenissen uitvoeren in een Hive-tabel
toorun hello Spark-streaming toepassing streams gebeurtenissen in een component tabel u moet een aantal extra onderdelen. Dit zijn:

* datanucleus api-jdo 3.2.6.jar
* datanucleus-rdbms-3.2.9.jar
* datanucleus-core-3.2.10.jar
* hive-site.xml

Hallo **JAR** bestanden zijn beschikbaar op uw HDInsight Spark-cluster op `/usr/hdp/current/spark-client/lib`. Hallo **hive-site.xml** is beschikbaar op `/usr/hdp/current/spark-client/conf`.

U kunt [WinScp](http://winscp.net/eng/download.php) toocopy via deze bestanden vanaf Hallo cluster tooyour lokale computer. Vervolgens kunt u extra toocopy deze bestanden via tooyour storage-account die is gekoppeld aan het Hallo-cluster. Zie voor meer informatie over hoe tooupload toohello opslagaccount bestanden, [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md).

Zodra u hebt gekopieerd via Hallo bestanden tooyour Azure storage-account, open een opdrachtprompt, navigeer toohello directory waarin u CURL hebt geïnstalleerd en Voer Hallo opdracht (vervangen gebruikersnaam en wachtwoord en het cluster name) te volgen:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

parameters in bestand Hallo Hallo **inputHive.txt** als volgt gedefinieerd:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Hallo-parameters zijn vergelijkbaar toowhat die u hebt opgegeven voor de tekstuitvoer Hallo in de vorige stappen Hallo. Opnieuw, hoeft u geen toocreate Hallo uitvoer mappen (EventCheckpoint, EventCount/EventCount10) of Hallo uitvoer Hive-tabel (EventHiveTable10) die worden gebruikt als parameters. streaming-toepassing Hello ze voor u gemaakt. Houd er rekening mee dat Hallo **potten** en **bestanden** optie omvat paden toohello JAR-bestanden en Hallo hive-site.xml die u hebt gekopieerd via toohello storage-account.

tooverify die Hallo hive-tabel is gemaakt, kunt u SSH in Hallo-cluster en Hive-query's uitvoeren. Zie voor instructies [Hive gebruiken met Hadoop in HDInsight met SSH](hdinsight-hadoop-use-hive-ssh.md). Zodra u met het gebruik van SSH verbonden bent, kunt u uitvoeren na de opdracht tooverify Hallo die Hallo Hive-tabel **EventHiveTable10**, wordt gemaakt.

    show tables;

U ziet een uitvoer vergelijkbare toohello volgende:

    OK
    eventhivetable10
    hivesampletable

U kunt een SELECT-query ook tooview Hallo inhoud van Hallo tabel uitvoeren.

    SELECT * FROM eventhivetable10 LIMIT 10;

Hier ziet u uitvoer Hallo volgende:

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a>Hallo toepassingen tooreceive Hallo gebeurtenissen uitvoeren in een Azure SQL-databasetabel
Voordat u deze stap uitvoert, zorg ervoor dat u hebt een Azure SQL-database gemaakt. Zie voor instructies [maken van een SQL-database in minuten](../sql-database/sql-database-get-started.md). toocomplete dit sectie, moet u waarden voor de databasenaam, database-servernaam en Hallo database beheerdersreferenties als parameters. U hoeft niet toocreate Hallo databasetabel al. Hallo Spark-streaming toepassing die voor u gemaakt.

Open een opdrachtprompt, navigeer toohello directory waarin u CURL hebt geïnstalleerd en Voer Hallo volgende opdracht uit:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

parameters in bestand Hallo Hallo **inputSQL.txt** als volgt gedefinieerd:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

tooverify die toepassing hello met succes wordt uitgevoerd, kunt u toohello Azure SQL database met behulp van SQL Server Management Studio. Voor instructies over het toodo die Zie [tooSQL Database met SQL Server Management Studio verbinding](../sql-database/sql-database-connect-query-ssms.md). Wanneer u verbonden toohello database bent, kunt u navigeren toohello **EventContent** tabel die is gemaakt door Hallo streaming-toepassing. U kunt een snelle tooget Hallo querygegevens uit Hallo tabel uitvoeren. Voer Hallo query te volgen:

    SELECT * FROM EventCount

Hier ziet u uitvoer vergelijkbare toohello volgende:

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <a name="seealso"></a>Zie ook
* [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md)
* [Ontwerp van de verbinding op basis van de ontvanger en Direct DStream](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a>Scenario's
* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Websitelogboekanalyse met Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Toepassingen maken en uitvoeren
* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Tools en uitbreidingen
* [De invoegtoepassing HDInsight Tools voor toocreate IntelliJ IDEA gebruiken en het verzenden van Spark Scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md)
* [De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Externe pakketten gebruiken met Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/

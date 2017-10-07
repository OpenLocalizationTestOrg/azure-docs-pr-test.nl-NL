---
title: aaaCreate Java MapReduce voor Hadoop - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Apache Maven toocreate een op Java gebaseerde MapReduce-toepassing uitvoeren met Hadoop op Azure HDInsight.
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
ms.assetid: 9ee6384c-cb61-4087-8273-fb53fa27c1c3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 903a57a482395f7da79002188399a4d6288ff0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a>Het ontwikkelen van Java-MapReduce-programma's voor Hadoop in HDInsight

Meer informatie over hoe toouse Apache Maven toocreate een op Java gebaseerde MapReduce-toepassing uitvoeren met Hadoop op Azure HDInsight.

> [!NOTE]
> In dit voorbeeld is voor het meest recent getest op HDInsight 3.6.

## <a name="prerequisites"></a>Vereisten

* [Java-JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 of hoger (of een vergelijkbare groep, zoals OpenJDK).
    
    > [!NOTE]
    > HDInsight versie 3.4 en eerder gebruik Java 7. HDInsight 3.5 en groter Java 8 gebruikt.

* [Apache Maven](http://maven.apache.org/)

## <a name="configure-development-environment"></a>De ontwikkelomgeving configureren

Hallo kunnen volgende omgevingsvariabelen worden ingesteld wanneer u Java en Hallo JDK installeert. Echter, moet u controleren of ze bestaan en dat ze de juiste waarden voor uw systeem Hallo bevatten.

* `JAVA_HOME`-moet verwijzen toohello directory waar Hallo Java runtime environment (JRE) is geïnstalleerd. Bijvoorbeeld: op een OS X-, Unix- of Linux-systeem, heeft een waarde gelijkaardig te`/usr/lib/jvm/java-7-oracle`. In Windows, zou er een waarde gelijkaardig te`c:\Program Files (x86)\Java\jre1.7`

* `PATH`-moet bevatten Hallo paden te volgen:
  
  * `JAVA_HOME`(of equivalente paden Hallo)

  * `JAVA_HOME\bin`(of equivalente paden Hallo)

  * Hallo-directory waar Maven is geïnstalleerd

## <a name="create-a-maven-project"></a>Een Maven-project maken

1. Wijzigen van een terminalsessie of de opdrachtregel in uw ontwikkelomgeving mappen toohello gewenste locatie toostore dit project.

2. Gebruik Hallo `mvn` opdracht, die is geïnstalleerd met Maven, toogenerate hello scaffolding voor Hallo-project.

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > Als u met behulp van PowerShell, moet u Hallo tussen `-D` parameters tussen dubbele aanhalingstekens.
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    Met deze opdracht maakt u een map met Hallo door Hallo opgegeven `artifactID` parameter (**wordcountjava** in dit voorbeeld.) Deze map bevat de volgende items Hallo:

   * `pom.xml`-Hallo [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) die informatie bevat en configuratiedetails toobuild Hallo project gebruikt.

   * `src`-Hallo-map die de toepassing hello bevat.

3. Hallo verwijderen `src/test/java/org/apache/hadoop/examples/apptest.java` bestand. Het wordt niet gebruikt in dit voorbeeld.

## <a name="add-dependencies"></a>Afhankelijkheden toevoegen

1. Hallo bewerken `pom.xml` bestands- en toevoegen van de volgende tekst in Hallo Hallo `<dependencies>` sectie:
   
   ```xml
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-examples</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-client-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
   ```

    Hiermee definieert u vereiste bibliotheken (vermeld in &lt;artefact-id\>) met een specifieke versie (vermeld in &lt;versie\>). Tijdens het compileren worden van Hallo standaard Maven opslagplaats deze afhankelijkheden gedownload. U kunt Hallo [Maven-opslagplaats zoeken](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview meer.
   
    Hallo `<scope>provided</scope>` vertelt Maven dat deze afhankelijkheden niet moeten worden verpakt met de toepassing hello, die worden geleverd door HDInsight-cluster Hallo tijdens runtime.

    > [!IMPORTANT]
    > Hallo-versie die wordt gebruikt, moet overeenkomen met Hallo-versie van Hadoop aanwezig is op het cluster. Zie voor meer informatie over versies Hallo [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md) document.

2. Hallo na toohello toevoegen `pom.xml` bestand. Deze tekst moet binnen Hallo `<project>...</project>` labels Hallo-bestand, bijvoorbeeld tussen `</dependencies>` en `</project>`.

   ```xml
    <build>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
            <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                </transformer>
            </transformers>
            </configuration>
            <executions>
            <execution>
                <phase>package</phase>
                    <goals>
                    <goal>shade</goal>
                    </goals>
            </execution>
            </executions>
            </plugin>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.6.1</version>
            <configuration>
            <source>1.8</source>
            <target>1.8</target>
            </configuration>
        </plugin>
        </plugins>
    </build>
   ```

    Hallo eerste invoegtoepassing configureert Hallo [Maven grijs-invoegtoepassing](http://maven.apache.org/plugins/maven-shade-plugin/), die is gebruikt toobuild een uberjar (ook wel een fatjar genoemd), die door de toepassing hello vereiste afhankelijkheden bevat. Dit voorkomt ook dat licenties in Hallo jar pakket, waardoor problemen op sommige systemen kunnen worden gedupliceerd.

    de tweede invoegtoepassing Hallo configureert Hallo doel Java-versie.

    > [!NOTE]
    > HDInsight 3.4 en eerdere versies gebruiken Java 7. HDInsight 3.5 en groter Java 8 gebruikt.

3. Hallo opslaan `pom.xml` bestand.

## <a name="create-hello-mapreduce-application"></a>Hallo MapReduce-toepassing maken

1. Ga toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` map en wijzig de naam Hallo `App.java` bestand te`WordCount.java`.

2. Open Hallo `WordCount.java` -bestand in een teksteditor en Hallo inhoud vervangen door de volgende tekst hello:
   
    ```java
    package org.apache.hadoop.examples;

    import java.io.IOException;
    import java.util.StringTokenizer;
    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.fs.Path;
    import org.apache.hadoop.io.IntWritable;
    import org.apache.hadoop.io.Text;
    import org.apache.hadoop.mapreduce.Job;
    import org.apache.hadoop.mapreduce.Mapper;
    import org.apache.hadoop.mapreduce.Reducer;
    import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
    import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class WordCount {

        public static class TokenizerMapper
            extends Mapper<Object, Text, Text, IntWritable>{

        private final static IntWritable one = new IntWritable(1);
        private Text word = new Text();

        public void map(Object key, Text value, Context context
                        ) throws IOException, InterruptedException {
            StringTokenizer itr = new StringTokenizer(value.toString());
            while (itr.hasMoreTokens()) {
            word.set(itr.nextToken());
            context.write(word, one);
            }
        }
    }

    public static class IntSumReducer
            extends Reducer<Text,IntWritable,Text,IntWritable> {
        private IntWritable result = new IntWritable();

        public void reduce(Text key, Iterable<IntWritable> values,
                            Context context
                            ) throws IOException, InterruptedException {
            int sum = 0;
            for (IntWritable val : values) {
            sum += val.get();
            }
            result.set(sum);
            context.write(key, result);
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
        if (otherArgs.length != 2) {
            System.err.println("Usage: wordcount <in> <out>");
            System.exit(2);
        }
        Job job = new Job(conf, "word count");
        job.setJarByClass(WordCount.class);
        job.setMapperClass(TokenizerMapper.class);
        job.setCombinerClass(IntSumReducer.class);
        job.setReducerClass(IntSumReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
        FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
        System.exit(job.waitForCompletion(true) ? 0 : 1);
        }
    }
    ```
   
    Kennisgeving Hallo package name `org.apache.hadoop.examples` en Hallo klassennaam `WordCount`. U gebruikt deze namen wanneer u Hallo MapReduce-taak indienen.

3. Hallo-bestand opslaan.

## <a name="build-hello-application"></a>Hallo-toepassing bouwen

1. Wijzigen van toohello `wordcountjava` directory, als u nog geen er.

2. Na de opdracht toobuild een JAR-bestand met Hallo toepassing hello gebruiken:

   ```
   mvn clean package
   ```

    Met deze opdracht schoongemaakt eventuele vorige build-artefacten, downloadt u alle afhankelijkheden die nog niet hebt is geïnstalleerd, en vervolgens builds en pakket Hallo toepassing.

3. Zodra het Hallo-opdracht is voltooid, hello `wordcountjava/target` map bevat een bestand met de naam `wordcountjava-1.0-SNAPSHOT.jar`.
   
   > [!NOTE]
   > Hallo `wordcountjava-1.0-SNAPSHOT.jar` bestand is een uberjar waarin niet alleen Hallo WordCount taak, maar ook afhankelijkheden die taak Hallo vereist tijdens runtime.

## <a id="upload"></a>Hallo jar uploaden

Hallo opdracht tooupload Hallo jar-bestand toohello HDInsight headnode volgende gebruiken:

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

Met deze opdracht kopieert Hallo-bestanden van Hallo lokaal systeem toohello hoofdknooppunt. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

## <a name="run"></a>Hallo MapReduce-taak uitvoeren op Hadoop

1. Verbinding maken via SSH tooHDInsight. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

2. Gebruik na opdracht toorun hello MapReduce toepassing hello van Hallo-SSH-sessie:
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    Deze opdracht start Hallo WordCount MapReduce-toepassing. Hallo-bestand voor invoer is `/example/data/gutenberg/davinci.txt`, en de uitvoermap Hallo `/example/data/wordcountout`. Zowel Hallo-bestand voor invoer en uitvoer zijn opgeslagen toohello standaard opslagruimte voor Hallo-cluster.

3. Zodra het Hallo-taak is voltooid, gebruikt u Hallo opdrachtresultaten tooview hello te volgen:
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    U ontvangt een lijst met woorden en aantallen met waarden vergelijkbare toohello volgende tekst:
   
        zeal    1
        zelus   1
        zenith  2

## <a id="nextsteps"></a>Volgende stappen

In dit document hebt u geleerd hoe toodevelop een Java-MapReduce-taak. Zie de volgende documenten voor andere manieren toowork met HDInsight Hallo.

* [Hive gebruiken met HDInsight][hdinsight-use-hive]
* [Pig gebruiken met HDInsight][hdinsight-use-pig]
* [MapReduce gebruiken met HDInsight](hdinsight-use-mapreduce.md)

Zie voor meer informatie, ook Hallo [Java Developer Center](https://azure.microsoft.com/develop/java/).

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[powershell-PSCredential]: http://social.technet.microsoft.com/wiki/contents/articles/4546.working-with-passwords-secure-strings-and-credentials-in-windows-powershell.aspx


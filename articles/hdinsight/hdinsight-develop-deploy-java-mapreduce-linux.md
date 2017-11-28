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
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a><span data-ttu-id="f78f9-103">Het ontwikkelen van Java-MapReduce-programma's voor Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f78f9-103">Develop Java MapReduce programs for Hadoop on HDInsight</span></span>

<span data-ttu-id="f78f9-104">Meer informatie over hoe toouse Apache Maven toocreate een op Java gebaseerde MapReduce-toepassing uitvoeren met Hadoop op Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f78f9-104">Learn how toouse Apache Maven toocreate a Java-based MapReduce application, then run it with Hadoop on Azure HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="f78f9-105">In dit voorbeeld is voor het meest recent getest op HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="f78f9-105">This example was most recently tested on HDInsight 3.6.</span></span>

## <span data-ttu-id="f78f9-106"><a name="prerequisites"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="f78f9-106"><a name="prerequisites"></a>Prerequisites</span></span>

* <span data-ttu-id="f78f9-107">[Java-JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 of hoger (of een vergelijkbare groep, zoals OpenJDK).</span><span class="sxs-lookup"><span data-stu-id="f78f9-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="f78f9-108">HDInsight versie 3.4 en eerder gebruik Java 7.</span><span class="sxs-lookup"><span data-stu-id="f78f9-108">HDInsight versions 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="f78f9-109">HDInsight 3.5 en groter Java 8 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f78f9-109">HDInsight 3.5 and greater uses Java 8.</span></span>

* [<span data-ttu-id="f78f9-110">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="f78f9-110">Apache Maven</span></span>](http://maven.apache.org/)

## <a name="configure-development-environment"></a><span data-ttu-id="f78f9-111">De ontwikkelomgeving configureren</span><span class="sxs-lookup"><span data-stu-id="f78f9-111">Configure development environment</span></span>

<span data-ttu-id="f78f9-112">Hallo kunnen volgende omgevingsvariabelen worden ingesteld wanneer u Java en Hallo JDK installeert.</span><span class="sxs-lookup"><span data-stu-id="f78f9-112">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="f78f9-113">Echter, moet u controleren of ze bestaan en dat ze de juiste waarden voor uw systeem Hallo bevatten.</span><span class="sxs-lookup"><span data-stu-id="f78f9-113">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="f78f9-114">`JAVA_HOME`-moet verwijzen toohello directory waar Hallo Java runtime environment (JRE) is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f78f9-114">`JAVA_HOME` - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="f78f9-115">Bijvoorbeeld: op een OS X-, Unix- of Linux-systeem, heeft een waarde gelijkaardig te`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="f78f9-115">For example, on an OS X, Unix or Linux system, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="f78f9-116">In Windows, zou er een waarde gelijkaardig te`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="f78f9-116">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="f78f9-117">`PATH`-moet bevatten Hallo paden te volgen:</span><span class="sxs-lookup"><span data-stu-id="f78f9-117">`PATH` - should contain hello following paths:</span></span>
  
  * <span data-ttu-id="f78f9-118">`JAVA_HOME`(of equivalente paden Hallo)</span><span class="sxs-lookup"><span data-stu-id="f78f9-118">`JAVA_HOME` (or hello equivalent path)</span></span>

  * <span data-ttu-id="f78f9-119">`JAVA_HOME\bin`(of equivalente paden Hallo)</span><span class="sxs-lookup"><span data-stu-id="f78f9-119">`JAVA_HOME\bin` (or hello equivalent path)</span></span>

  * <span data-ttu-id="f78f9-120">Hallo-directory waar Maven is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="f78f9-120">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="f78f9-121">Een Maven-project maken</span><span class="sxs-lookup"><span data-stu-id="f78f9-121">Create a Maven project</span></span>

1. <span data-ttu-id="f78f9-122">Wijzigen van een terminalsessie of de opdrachtregel in uw ontwikkelomgeving mappen toohello gewenste locatie toostore dit project.</span><span class="sxs-lookup"><span data-stu-id="f78f9-122">From a terminal session, or command line in your development environment, change directories toohello location you want toostore this project.</span></span>

2. <span data-ttu-id="f78f9-123">Gebruik Hallo `mvn` opdracht, die is geïnstalleerd met Maven, toogenerate hello scaffolding voor Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="f78f9-123">Use hello `mvn` command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > <span data-ttu-id="f78f9-124">Als u met behulp van PowerShell, moet u Hallo tussen `-D` parameters tussen dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="f78f9-124">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="f78f9-125">Met deze opdracht maakt u een map met Hallo door Hallo opgegeven `artifactID` parameter (**wordcountjava** in dit voorbeeld.) Deze map bevat de volgende items Hallo:</span><span class="sxs-lookup"><span data-stu-id="f78f9-125">This command creates a directory with hello name specified by hello `artifactID` parameter (**wordcountjava** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="f78f9-126">`pom.xml`-Hallo [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) die informatie bevat en configuratiedetails toobuild Hallo project gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f78f9-126">`pom.xml` - hello [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used toobuild hello project.</span></span>

   * <span data-ttu-id="f78f9-127">`src`-Hallo-map die de toepassing hello bevat.</span><span class="sxs-lookup"><span data-stu-id="f78f9-127">`src` - hello directory that contains hello application.</span></span>

3. <span data-ttu-id="f78f9-128">Hallo verwijderen `src/test/java/org/apache/hadoop/examples/apptest.java` bestand.</span><span class="sxs-lookup"><span data-stu-id="f78f9-128">Delete hello `src/test/java/org/apache/hadoop/examples/apptest.java` file.</span></span> <span data-ttu-id="f78f9-129">Het wordt niet gebruikt in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f78f9-129">It is not used in this example.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="f78f9-130">Afhankelijkheden toevoegen</span><span class="sxs-lookup"><span data-stu-id="f78f9-130">Add dependencies</span></span>

1. <span data-ttu-id="f78f9-131">Hallo bewerken `pom.xml` bestands- en toevoegen van de volgende tekst in Hallo Hallo `<dependencies>` sectie:</span><span class="sxs-lookup"><span data-stu-id="f78f9-131">Edit hello `pom.xml` file and add hello following text inside hello `<dependencies>` section:</span></span>
   
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

    <span data-ttu-id="f78f9-132">Hiermee definieert u vereiste bibliotheken (vermeld in &lt;artefact-id\>) met een specifieke versie (vermeld in &lt;versie\>).</span><span class="sxs-lookup"><span data-stu-id="f78f9-132">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span></span> <span data-ttu-id="f78f9-133">Tijdens het compileren worden van Hallo standaard Maven opslagplaats deze afhankelijkheden gedownload.</span><span class="sxs-lookup"><span data-stu-id="f78f9-133">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="f78f9-134">U kunt Hallo [Maven-opslagplaats zoeken](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview meer.</span><span class="sxs-lookup"><span data-stu-id="f78f9-134">You can use hello [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview more.</span></span>
   
    <span data-ttu-id="f78f9-135">Hallo `<scope>provided</scope>` vertelt Maven dat deze afhankelijkheden niet moeten worden verpakt met de toepassing hello, die worden geleverd door HDInsight-cluster Hallo tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="f78f9-135">hello `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with hello application, as they are provided by hello HDInsight cluster at run-time.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f78f9-136">Hallo-versie die wordt gebruikt, moet overeenkomen met Hallo-versie van Hadoop aanwezig is op het cluster.</span><span class="sxs-lookup"><span data-stu-id="f78f9-136">hello version used should match hello version of Hadoop present on your cluster.</span></span> <span data-ttu-id="f78f9-137">Zie voor meer informatie over versies Hallo [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md) document.</span><span class="sxs-lookup"><span data-stu-id="f78f9-137">For more information on versions, see hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

2. <span data-ttu-id="f78f9-138">Hallo na toohello toevoegen `pom.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="f78f9-138">Add hello following toohello `pom.xml` file.</span></span> <span data-ttu-id="f78f9-139">Deze tekst moet binnen Hallo `<project>...</project>` labels Hallo-bestand, bijvoorbeeld tussen `</dependencies>` en `</project>`.</span><span class="sxs-lookup"><span data-stu-id="f78f9-139">This text must be inside hello `<project>...</project>` tags in hello file; for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="f78f9-140">Hallo eerste invoegtoepassing configureert Hallo [Maven grijs-invoegtoepassing](http://maven.apache.org/plugins/maven-shade-plugin/), die is gebruikt toobuild een uberjar (ook wel een fatjar genoemd), die door de toepassing hello vereiste afhankelijkheden bevat.</span><span class="sxs-lookup"><span data-stu-id="f78f9-140">hello first plugin configures hello [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used toobuild an uberjar (sometimes called a fatjar), which contains dependencies required by hello application.</span></span> <span data-ttu-id="f78f9-141">Dit voorkomt ook dat licenties in Hallo jar pakket, waardoor problemen op sommige systemen kunnen worden gedupliceerd.</span><span class="sxs-lookup"><span data-stu-id="f78f9-141">It also prevents duplication of licenses within hello jar package, which can cause problems on some systems.</span></span>

    <span data-ttu-id="f78f9-142">de tweede invoegtoepassing Hallo configureert Hallo doel Java-versie.</span><span class="sxs-lookup"><span data-stu-id="f78f9-142">hello second plugin configures hello target Java version.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f78f9-143">HDInsight 3.4 en eerdere versies gebruiken Java 7.</span><span class="sxs-lookup"><span data-stu-id="f78f9-143">HDInsight 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="f78f9-144">HDInsight 3.5 en groter Java 8 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f78f9-144">HDInsight 3.5 and greater uses Java 8.</span></span>

3. <span data-ttu-id="f78f9-145">Hallo opslaan `pom.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="f78f9-145">Save hello `pom.xml` file.</span></span>

## <a name="create-hello-mapreduce-application"></a><span data-ttu-id="f78f9-146">Hallo MapReduce-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="f78f9-146">Create hello MapReduce application</span></span>

1. <span data-ttu-id="f78f9-147">Ga toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` map en wijzig de naam Hallo `App.java` bestand te`WordCount.java`.</span><span class="sxs-lookup"><span data-stu-id="f78f9-147">Go toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename hello `App.java` file too`WordCount.java`.</span></span>

2. <span data-ttu-id="f78f9-148">Open Hallo `WordCount.java` -bestand in een teksteditor en Hallo inhoud vervangen door de volgende tekst hello:</span><span class="sxs-lookup"><span data-stu-id="f78f9-148">Open hello `WordCount.java` file in a text editor and replace hello contents with hello following text:</span></span>
   
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
   
    <span data-ttu-id="f78f9-149">Kennisgeving Hallo package name `org.apache.hadoop.examples` en Hallo klassennaam `WordCount`.</span><span class="sxs-lookup"><span data-stu-id="f78f9-149">Notice hello package name is `org.apache.hadoop.examples` and hello class name is `WordCount`.</span></span> <span data-ttu-id="f78f9-150">U gebruikt deze namen wanneer u Hallo MapReduce-taak indienen.</span><span class="sxs-lookup"><span data-stu-id="f78f9-150">You use these names when you submit hello MapReduce job.</span></span>

3. <span data-ttu-id="f78f9-151">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="f78f9-151">Save hello file.</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="f78f9-152">Hallo-toepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="f78f9-152">Build hello application</span></span>

1. <span data-ttu-id="f78f9-153">Wijzigen van toohello `wordcountjava` directory, als u nog geen er.</span><span class="sxs-lookup"><span data-stu-id="f78f9-153">Change toohello `wordcountjava` directory, if you are not already there.</span></span>

2. <span data-ttu-id="f78f9-154">Na de opdracht toobuild een JAR-bestand met Hallo toepassing hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f78f9-154">Use hello following command toobuild a JAR file containing hello application:</span></span>

   ```
   mvn clean package
   ```

    <span data-ttu-id="f78f9-155">Met deze opdracht schoongemaakt eventuele vorige build-artefacten, downloadt u alle afhankelijkheden die nog niet hebt is geïnstalleerd, en vervolgens builds en pakket Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="f78f9-155">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package hello application.</span></span>

3. <span data-ttu-id="f78f9-156">Zodra het Hallo-opdracht is voltooid, hello `wordcountjava/target` map bevat een bestand met de naam `wordcountjava-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="f78f9-156">Once hello command finishes, hello `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f78f9-157">Hallo `wordcountjava-1.0-SNAPSHOT.jar` bestand is een uberjar waarin niet alleen Hallo WordCount taak, maar ook afhankelijkheden die taak Hallo vereist tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="f78f9-157">hello `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only hello WordCount job, but also dependencies that hello job requires at runtime.</span></span>

## <span data-ttu-id="f78f9-158"><a id="upload"></a>Hallo jar uploaden</span><span class="sxs-lookup"><span data-stu-id="f78f9-158"><a id="upload"></a>Upload hello jar</span></span>

<span data-ttu-id="f78f9-159">Hallo opdracht tooupload Hallo jar-bestand toohello HDInsight headnode volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f78f9-159">Use hello following command tooupload hello jar file toohello HDInsight headnode:</span></span>

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

<span data-ttu-id="f78f9-160">Met deze opdracht kopieert Hallo-bestanden van Hallo lokaal systeem toohello hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="f78f9-160">This command copies hello files from hello local system toohello head node.</span></span> <span data-ttu-id="f78f9-161">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f78f9-161">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="f78f9-162"><a name="run"></a>Hallo MapReduce-taak uitvoeren op Hadoop</span><span class="sxs-lookup"><span data-stu-id="f78f9-162"><a name="run"></a>Run hello MapReduce job on Hadoop</span></span>

1. <span data-ttu-id="f78f9-163">Verbinding maken via SSH tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="f78f9-163">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="f78f9-164">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f78f9-164">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="f78f9-165">Gebruik na opdracht toorun hello MapReduce toepassing hello van Hallo-SSH-sessie:</span><span class="sxs-lookup"><span data-stu-id="f78f9-165">From hello SSH session, use hello following command toorun hello MapReduce application:</span></span>
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    <span data-ttu-id="f78f9-166">Deze opdracht start Hallo WordCount MapReduce-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f78f9-166">This command starts hello WordCount MapReduce application.</span></span> <span data-ttu-id="f78f9-167">Hallo-bestand voor invoer is `/example/data/gutenberg/davinci.txt`, en de uitvoermap Hallo `/example/data/wordcountout`.</span><span class="sxs-lookup"><span data-stu-id="f78f9-167">hello input file is `/example/data/gutenberg/davinci.txt`, and hello output directory is `/example/data/wordcountout`.</span></span> <span data-ttu-id="f78f9-168">Zowel Hallo-bestand voor invoer en uitvoer zijn opgeslagen toohello standaard opslagruimte voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f78f9-168">Both hello input file and output are stored toohello default storage for hello cluster.</span></span>

3. <span data-ttu-id="f78f9-169">Zodra het Hallo-taak is voltooid, gebruikt u Hallo opdrachtresultaten tooview hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="f78f9-169">Once hello job completes, use hello following command tooview hello results:</span></span>
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    <span data-ttu-id="f78f9-170">U ontvangt een lijst met woorden en aantallen met waarden vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="f78f9-170">You should receive a list of words and counts, with values similar toohello following text:</span></span>
   
        zeal    1
        zelus   1
        zenith  2

## <span data-ttu-id="f78f9-171"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f78f9-171"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="f78f9-172">In dit document hebt u geleerd hoe toodevelop een Java-MapReduce-taak.</span><span class="sxs-lookup"><span data-stu-id="f78f9-172">In this document, you have learned how toodevelop a Java MapReduce job.</span></span> <span data-ttu-id="f78f9-173">Zie de volgende documenten voor andere manieren toowork met HDInsight Hallo.</span><span class="sxs-lookup"><span data-stu-id="f78f9-173">See hello following documents for other ways toowork with HDInsight.</span></span>

* <span data-ttu-id="f78f9-174">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="f78f9-174">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="f78f9-175">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="f78f9-175">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* [<span data-ttu-id="f78f9-176">MapReduce gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="f78f9-176">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="f78f9-177">Zie voor meer informatie, ook Hallo [Java Developer Center](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="f78f9-177">For more information, see also hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

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


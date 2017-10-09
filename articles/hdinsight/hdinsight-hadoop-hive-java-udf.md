---
title: aaaJava gebruiker gedefinieerde functie (UDF met Hive in HDInsight - Azure) | Microsoft Docs
description: Meer informatie over hoe toocreate een op Java gebaseerde gebruiker gedefinieerde functie (UDF) die met Hive werkt. In dit voorbeeld UDF converteert een tabel van tekst tekenreeksen toolowercase.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 8d4f8efe-2f01-4a61-8619-651e873c7982
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 392b4cfb73299d2f6c1e8e825a4201b48d501388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="f37ac-104">Gebruik van een Java UDF met Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f37ac-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="f37ac-105">Meer informatie over hoe toocreate een op Java gebaseerde gebruiker gedefinieerde functie (UDF) die met Hive werkt.</span><span class="sxs-lookup"><span data-stu-id="f37ac-105">Learn how toocreate a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="f37ac-106">Hallo Java UDF in dit voorbeeld converteert een tabel van tekenreeksen tooall kleine tekens.</span><span class="sxs-lookup"><span data-stu-id="f37ac-106">hello Java UDF in this example converts a table of text strings tooall-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="f37ac-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f37ac-107">Requirements</span></span>

* <span data-ttu-id="f37ac-108">Een HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="f37ac-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="f37ac-109">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="f37ac-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f37ac-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f37ac-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="f37ac-111">De meeste stappen in dit document werken op zowel Windows - en Linux gebaseerde clusters.</span><span class="sxs-lookup"><span data-stu-id="f37ac-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="f37ac-112">Hallo stappen tooupload Hallo gecompileerd echter UDF toohello cluster en het specifieke tooLinux gebaseerde clusters worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f37ac-112">However, hello steps used tooupload hello compiled UDF toohello cluster and run it are specific tooLinux-based clusters.</span></span> <span data-ttu-id="f37ac-113">Koppelingen vindt u tooinformation die kan worden gebruikt met Windows gebaseerde clusters.</span><span class="sxs-lookup"><span data-stu-id="f37ac-113">Links are provided tooinformation that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="f37ac-114">[Java-JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 of hoger (of een vergelijkbare groep, zoals OpenJDK)</span><span class="sxs-lookup"><span data-stu-id="f37ac-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="f37ac-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="f37ac-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="f37ac-116">Een teksteditor of IDE voor Java</span><span class="sxs-lookup"><span data-stu-id="f37ac-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f37ac-117">Als u Hallo Python-bestanden op een Windows-client maakt, moet u een editor die LF als een regel beëindigen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f37ac-117">If you create hello Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="f37ac-118">Als u niet zeker of uw editor LF of CRLF gebruikt weet, raadpleegt u Hallo [probleemoplossing](#troubleshooting) sectie voor stapsgewijze instructies voor het verwijderen van Hallo CR-teken.</span><span class="sxs-lookup"><span data-stu-id="f37ac-118">If you are not sure whether your editor uses LF or CRLF, see hello [Troubleshooting](#troubleshooting) section for steps on removing hello CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="f37ac-119">Een voorbeeld Java UDF maken</span><span class="sxs-lookup"><span data-stu-id="f37ac-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="f37ac-120">Gebruik vanaf een opdrachtregel Hallo toocreate een nieuw Maven-project te volgen:</span><span class="sxs-lookup"><span data-stu-id="f37ac-120">From a command line, use hello following toocreate a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="f37ac-121">Als u met behulp van PowerShell, kunt u aanhalingstekens rond Hallo parameters moet zetten.</span><span class="sxs-lookup"><span data-stu-id="f37ac-121">If you are using PowerShell, you must put quotes around hello parameters.</span></span> <span data-ttu-id="f37ac-122">Bijvoorbeeld `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span><span class="sxs-lookup"><span data-stu-id="f37ac-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="f37ac-123">Deze opdracht maakt u een map met de naam **exampleudf**, die Hallo Maven-project bevat.</span><span class="sxs-lookup"><span data-stu-id="f37ac-123">This command creates a directory named **exampleudf**, which contains hello Maven project.</span></span>

2. <span data-ttu-id="f37ac-124">Zodra het Hallo-project is gemaakt, verwijdert u Hallo **src-exampleudf/Testscenario** map die is gemaakt als onderdeel van het Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="f37ac-124">Once hello project has been created, delete hello **exampleudf/src/test** directory that was created as part of hello project.</span></span>

3. <span data-ttu-id="f37ac-125">Open Hallo **exampleudf/pom.xml**, en vervang bestaande Hallo `<dependencies>` vermelding met Hallo XML te volgen:</span><span class="sxs-lookup"><span data-stu-id="f37ac-125">Open hello **exampleudf/pom.xml**, and replace hello existing `<dependencies>` entry with hello following XML:</span></span>

    ```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>2.7.3</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.hive</groupId>
            <artifactId>hive-exec</artifactId>
            <version>1.2.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
    ```

    <span data-ttu-id="f37ac-126">Deze vermeldingen opgeven Hallo-versie van Hadoop en Hive met HDInsight 3.5 opgenomen.</span><span class="sxs-lookup"><span data-stu-id="f37ac-126">These entries specify hello version of Hadoop and Hive included with HDInsight 3.5.</span></span> <span data-ttu-id="f37ac-127">U vindt meer informatie over het Hallo-versies van Hadoop en Hive met HDInsight wordt geleverd door Hallo [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md) document.</span><span class="sxs-lookup"><span data-stu-id="f37ac-127">You can find information on hello versions of Hadoop and Hive provided with HDInsight from hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="f37ac-128">Voeg een `<build>` sectie voordat Hallo `</project>` lijn op Hallo einde van Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="f37ac-128">Add a `<build>` section before hello `</project>` line at hello end of hello file.</span></span> <span data-ttu-id="f37ac-129">In deze sectie bevatten Hallo XML te volgen:</span><span class="sxs-lookup"><span data-stu-id="f37ac-129">This section should contain hello following XML:</span></span>

    ```xml
    <build>
        <plugins>
            <!-- build for Java 1.8. This is required by HDInsight 3.5  -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <!-- build an uber jar -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <!-- Keep us from getting a can't overwrite file error -->
                    <transformers>
                        <transformer
                                implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                        </transformer>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer">
                        </transformer>
                    </transformers>
                    <!-- Keep us from getting a bad signature error -->
                    <filters>
                        <filter>
                            <artifact>*:*</artifact>
                            <excludes>
                                <exclude>META-INF/*.SF</exclude>
                                <exclude>META-INF/*.DSA</exclude>
                                <exclude>META-INF/*.RSA</exclude>
                            </excludes>
                        </filter>
                    </filters>
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
        </plugins>
    </build>
    ```

    <span data-ttu-id="f37ac-130">Deze vermeldingen definiëren hoe toobuild Hallo project.</span><span class="sxs-lookup"><span data-stu-id="f37ac-130">These entries define how toobuild hello project.</span></span> <span data-ttu-id="f37ac-131">In het bijzonder Hallo versie van Java die Hallo project gebruikt en hoe toobuild een uberjar voor implementatie toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="f37ac-131">Specifically, hello version of Java that hello project uses and how toobuild an uberjar for deployment toohello cluster.</span></span>

    <span data-ttu-id="f37ac-132">Hallo-bestand opslaan als Hallo wijzigingen zijn aangebracht.</span><span class="sxs-lookup"><span data-stu-id="f37ac-132">Save hello file once hello changes have been made.</span></span>

4. <span data-ttu-id="f37ac-133">Wijzig de naam van **exampleudf/src/main/java/com/microsoft/examples/App.java** te**ExampleUDF.java**, en open vervolgens Hallo-bestand in uw editor.</span><span class="sxs-lookup"><span data-stu-id="f37ac-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** too**ExampleUDF.java**, and then open hello file in your editor.</span></span>

5. <span data-ttu-id="f37ac-134">Vervang de inhoud Hallo Hallo **ExampleUDF.java** bestand met de volgende Hallo en sla vervolgens Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="f37ac-134">Replace hello contents of hello **ExampleUDF.java** file with hello following, then save hello file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of hello UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of hello input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If hello value is null, return a null
            if(input == null)
                return null;
            // Lowercase hello input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="f37ac-135">Deze code implementeert een UDF die een string-waarde accepteert en retourneert een kleine versie van het Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="f37ac-135">This code implements a UDF that accepts a string value, and returns a lowercase version of hello string.</span></span>

## <a name="build-and-install-hello-udf"></a><span data-ttu-id="f37ac-136">Opbouwen en Hallo UDF installeren</span><span class="sxs-lookup"><span data-stu-id="f37ac-136">Build and install hello UDF</span></span>

1. <span data-ttu-id="f37ac-137">Gebruik Hallo opdracht toocompile te volgen en Hallo UDF pakket:</span><span class="sxs-lookup"><span data-stu-id="f37ac-137">Use hello following command toocompile and package hello UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="f37ac-138">Met deze opdracht maakt en pakketten UDF in Hallo Hallo `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` bestand.</span><span class="sxs-lookup"><span data-stu-id="f37ac-138">This command builds and packages hello UDF into hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="f37ac-139">Gebruik Hallo `scp` opdracht toocopy Hallo bestand toohello HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="f37ac-139">Use hello `scp` command toocopy hello file toohello HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="f37ac-140">Vervang `myuser` Hello SSH gebruikersaccount voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="f37ac-140">Replace `myuser` with hello SSH user account for your cluster.</span></span> <span data-ttu-id="f37ac-141">Vervang `mycluster` met de naam van de cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="f37ac-141">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="f37ac-142">Als u een wachtwoord toosecure Hallo SSH-account gebruikt, zijn na vragen aan gebruiker tooenter Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="f37ac-142">If you used a password toosecure hello SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="f37ac-143">Als u een certificaat gebruikt, moet u mogelijk toouse hello `-i` parameter toospecify Hallo persoonlijke sleutelbestand.</span><span class="sxs-lookup"><span data-stu-id="f37ac-143">If you used a certificate, you may need toouse hello `-i` parameter toospecify hello private key file.</span></span>

3. <span data-ttu-id="f37ac-144">Toohello-cluster via SSH verbinding.</span><span class="sxs-lookup"><span data-stu-id="f37ac-144">Connect toohello cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="f37ac-145">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f37ac-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="f37ac-146">Kopiëren van Hallo SSH-sessie, opslag tooHDInsight Hallo jar-bestanden.</span><span class="sxs-lookup"><span data-stu-id="f37ac-146">From hello SSH session, copy hello jar file tooHDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a><span data-ttu-id="f37ac-147">Hallo UDF van Hive gebruiken</span><span class="sxs-lookup"><span data-stu-id="f37ac-147">Use hello UDF from Hive</span></span>

1. <span data-ttu-id="f37ac-148">Gebruik Hallo toostart hello Beeline client Hallo SSH-sessie te volgen.</span><span class="sxs-lookup"><span data-stu-id="f37ac-148">Use hello following toostart hello Beeline client from hello SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="f37ac-149">Met deze opdracht wordt ervan uitgegaan dat u standaard Hallo van gebruikt **admin** voor Hallo aanmeldingsaccount voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="f37ac-149">This command assumes that you used hello default of **admin** for hello login account for your cluster.</span></span>

2. <span data-ttu-id="f37ac-150">Wanneer u bij Hallo aankomt `jdbc:hive2://localhost:10001/>` gevraagd, voert u Hallo tooadd Hallo UDF tooHive te volgen en deze weergeven als een functie.</span><span class="sxs-lookup"><span data-stu-id="f37ac-150">Once you arrive at hello `jdbc:hive2://localhost:10001/>` prompt, enter hello following tooadd hello UDF tooHive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="f37ac-151">In dit voorbeeld wordt ervan uitgegaan dat Azure Storage standaard opslagruimte voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f37ac-151">This example assumes that Azure Storage is default storage for hello cluster.</span></span> <span data-ttu-id="f37ac-152">Als uw cluster in plaats daarvan Data Lake Store gebruikt, wijzigt u Hallo `wasb:///` waarde te`adl:///`.</span><span class="sxs-lookup"><span data-stu-id="f37ac-152">If your cluster uses Data Lake Store instead, change hello `wasb:///` value too`adl:///`.</span></span>

3. <span data-ttu-id="f37ac-153">Hallo UDF tooconvert waarden opgehaald van tekenreeksen voor tabel-toolower gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f37ac-153">Use hello UDF tooconvert values retrieved from a table toolower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="f37ac-154">Deze query selecteert apparaatplatform (Android, Windows, iOS, enzovoort) uit de tabel Hallo HALLO hallo tekenreeks toolower geval converteren en ze weergeven.</span><span class="sxs-lookup"><span data-stu-id="f37ac-154">This query selects hello device platform (Android, Windows, iOS, etc.) from hello table, convert hello string toolower case, and then display them.</span></span> <span data-ttu-id="f37ac-155">Hallo-uitvoer wordt weergegeven vergelijkbaar toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="f37ac-155">hello output appears similar toohello following text:</span></span>

        +----------+--+
        |   _c0    |
        +----------+--+
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        +----------+--+

## <a name="next-steps"></a><span data-ttu-id="f37ac-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f37ac-156">Next steps</span></span>

<span data-ttu-id="f37ac-157">Zie voor andere manieren toowork met Hive, [Hive gebruiken met HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="f37ac-157">For other ways toowork with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="f37ac-158">Zie voor meer informatie over functies Hive User-Defined [Hive operatoren en door de gebruiker gedefinieerde functies](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) sectie van Hallo Hive wiki op apache.org.</span><span class="sxs-lookup"><span data-stu-id="f37ac-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of hello Hive wiki at apache.org.</span></span>

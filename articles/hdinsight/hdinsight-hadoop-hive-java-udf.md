---
title: Java gebruiker gedefinieerde functie (UDF met Hive in HDInsight - Azure) | Microsoft Docs
description: Informatie over het maken van een op Java gebaseerd gebruiker gedefinieerde functie (UDF die met Hive werkt). In dit voorbeeld UDF converteert een tabel van tekenreeksen in kleine letters.
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
ms.openlocfilehash: 481d234eaf88bdb210821084ee4154159470eda0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="d3596-104">Gebruik van een Java UDF met Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d3596-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="d3596-105">Informatie over het maken van een op Java gebaseerd gebruiker gedefinieerde functie (UDF die met Hive werkt).</span><span class="sxs-lookup"><span data-stu-id="d3596-105">Learn how to create a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="d3596-106">De Java-UDF in dit voorbeeld converteert een tabel van tekenreeksen alle kleine tekens.</span><span class="sxs-lookup"><span data-stu-id="d3596-106">The Java UDF in this example converts a table of text strings to all-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="d3596-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d3596-107">Requirements</span></span>

* <span data-ttu-id="d3596-108">Een HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="d3596-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="d3596-109">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="d3596-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d3596-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d3596-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="d3596-111">De meeste stappen in dit document werken op zowel Windows - en Linux gebaseerde clusters.</span><span class="sxs-lookup"><span data-stu-id="d3596-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="d3596-112">De stappen voor het uploaden van de gecompileerde UDF aan het cluster en voer dit zijn echter specifiek voor op basis van Linux-clusters.</span><span class="sxs-lookup"><span data-stu-id="d3596-112">However, the steps used to upload the compiled UDF to the cluster and run it are specific to Linux-based clusters.</span></span> <span data-ttu-id="d3596-113">Vindt u koppelingen naar informatie die kan worden gebruikt met Windows gebaseerde clusters.</span><span class="sxs-lookup"><span data-stu-id="d3596-113">Links are provided to information that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="d3596-114">[Java-JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 of hoger (of een vergelijkbare groep, zoals OpenJDK)</span><span class="sxs-lookup"><span data-stu-id="d3596-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="d3596-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="d3596-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="d3596-116">Een teksteditor of IDE voor Java</span><span class="sxs-lookup"><span data-stu-id="d3596-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d3596-117">Als u de Python-bestanden op een Windows-client maakt, moet u een editor die LF als een regel beëindigen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d3596-117">If you create the Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="d3596-118">Als u niet zeker of uw editor LF of CRLF gebruikt weet, raadpleegt u de [probleemoplossing](#troubleshooting) sectie voor stapsgewijze instructies voor het teken CR wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d3596-118">If you are not sure whether your editor uses LF or CRLF, see the [Troubleshooting](#troubleshooting) section for steps on removing the CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="d3596-119">Een voorbeeld Java UDF maken</span><span class="sxs-lookup"><span data-stu-id="d3596-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="d3596-120">Gebruik de volgende naar een nieuw Maven-project maken vanaf een opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="d3596-120">From a command line, use the following to create a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="d3596-121">Als u met behulp van PowerShell, kunt u aanhalingstekens rond de parameters moet zetten.</span><span class="sxs-lookup"><span data-stu-id="d3596-121">If you are using PowerShell, you must put quotes around the parameters.</span></span> <span data-ttu-id="d3596-122">Bijvoorbeeld `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span><span class="sxs-lookup"><span data-stu-id="d3596-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="d3596-123">Deze opdracht maakt u een map met de naam **exampleudf**, die het Maven-project bevat.</span><span class="sxs-lookup"><span data-stu-id="d3596-123">This command creates a directory named **exampleudf**, which contains the Maven project.</span></span>

2. <span data-ttu-id="d3596-124">Zodra het project is gemaakt, verwijdert de **src-exampleudf/Testscenario** map die is gemaakt als onderdeel van het project.</span><span class="sxs-lookup"><span data-stu-id="d3596-124">Once the project has been created, delete the **exampleudf/src/test** directory that was created as part of the project.</span></span>

3. <span data-ttu-id="d3596-125">Open de **exampleudf/pom.xml**, en vervang de bestaande `<dependencies>` vermelding met de volgende XML-code:</span><span class="sxs-lookup"><span data-stu-id="d3596-125">Open the **exampleudf/pom.xml**, and replace the existing `<dependencies>` entry with the following XML:</span></span>

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

    <span data-ttu-id="d3596-126">Deze vermeldingen Geef de versie van Hadoop en Hive met HDInsight 3.5 opgenomen.</span><span class="sxs-lookup"><span data-stu-id="d3596-126">These entries specify the version of Hadoop and Hive included with HDInsight 3.5.</span></span> <span data-ttu-id="d3596-127">U vindt meer informatie over de versies van Hadoop en Hive voorzien in HDInsight via de [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md) document.</span><span class="sxs-lookup"><span data-stu-id="d3596-127">You can find information on the versions of Hadoop and Hive provided with HDInsight from the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="d3596-128">Voeg een `<build>` sectie voordat de `</project>` regel aan het einde van het bestand.</span><span class="sxs-lookup"><span data-stu-id="d3596-128">Add a `<build>` section before the `</project>` line at the end of the file.</span></span> <span data-ttu-id="d3596-129">Deze sectie, moet de volgende XML bevatten:</span><span class="sxs-lookup"><span data-stu-id="d3596-129">This section should contain the following XML:</span></span>

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

    <span data-ttu-id="d3596-130">Deze vermeldingen definiëren hoe om het project te bouwen.</span><span class="sxs-lookup"><span data-stu-id="d3596-130">These entries define how to build the project.</span></span> <span data-ttu-id="d3596-131">In het bijzonder de versie van Java die gebruikmaakt van het project en het bouwen van een uberjar voor de implementatie van het cluster.</span><span class="sxs-lookup"><span data-stu-id="d3596-131">Specifically, the version of Java that the project uses and how to build an uberjar for deployment to the cluster.</span></span>

    <span data-ttu-id="d3596-132">Sla het bestand nadat de wijzigingen zijn aangebracht.</span><span class="sxs-lookup"><span data-stu-id="d3596-132">Save the file once the changes have been made.</span></span>

4. <span data-ttu-id="d3596-133">Wijzig de naam van **exampleudf/src/main/java/com/microsoft/examples/App.java** naar **ExampleUDF.java**, en open vervolgens het bestand in uw editor.</span><span class="sxs-lookup"><span data-stu-id="d3596-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** to **ExampleUDF.java**, and then open the file in your editor.</span></span>

5. <span data-ttu-id="d3596-134">Vervang de inhoud van de **ExampleUDF.java** door het volgende bestand en sla het bestand.</span><span class="sxs-lookup"><span data-stu-id="d3596-134">Replace the contents of the **ExampleUDF.java** file with the following, then save the file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of the UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of the input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If the value is null, return a null
            if(input == null)
                return null;
            // Lowercase the input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="d3596-135">Deze code implementeert een UDF die een string-waarde accepteert en retourneert een kleine versie van de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d3596-135">This code implements a UDF that accepts a string value, and returns a lowercase version of the string.</span></span>

## <a name="build-and-install-the-udf"></a><span data-ttu-id="d3596-136">Bouwen en de UDF installeren</span><span class="sxs-lookup"><span data-stu-id="d3596-136">Build and install the UDF</span></span>

1. <span data-ttu-id="d3596-137">Gebruik de volgende opdracht om te compileren en de UDF pakket:</span><span class="sxs-lookup"><span data-stu-id="d3596-137">Use the following command to compile and package the UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="d3596-138">Met deze opdracht maakt en pakketten van de UDF in de `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` bestand.</span><span class="sxs-lookup"><span data-stu-id="d3596-138">This command builds and packages the UDF into the `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="d3596-139">Gebruik de `scp` opdracht het bestand kopiëren naar het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d3596-139">Use the `scp` command to copy the file to the HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="d3596-140">Vervang `myuser` met het SSH-gebruikersaccount voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="d3596-140">Replace `myuser` with the SSH user account for your cluster.</span></span> <span data-ttu-id="d3596-141">Vervang `mycluster` met de naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="d3596-141">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="d3596-142">Als u een wachtwoord gebruikt om de SSH-account te beveiligen, wordt u gevraagd het wachtwoord invoeren.</span><span class="sxs-lookup"><span data-stu-id="d3596-142">If you used a password to secure the SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="d3596-143">Als u een certificaat gebruikt, moet u mogelijk gebruik van de `-i` parameter om een bestand met de persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="d3596-143">If you used a certificate, you may need to use the `-i` parameter to specify the private key file.</span></span>

3. <span data-ttu-id="d3596-144">Verbinding maken met het cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="d3596-144">Connect to the cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="d3596-145">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d3596-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="d3596-146">Kopieer het jar-bestand HDInsight-opslag van de SSH-sessie.</span><span class="sxs-lookup"><span data-stu-id="d3596-146">From the SSH session, copy the jar file to HDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-the-udf-from-hive"></a><span data-ttu-id="d3596-147">Gebruik de UDF van Hive</span><span class="sxs-lookup"><span data-stu-id="d3596-147">Use the UDF from Hive</span></span>

1. <span data-ttu-id="d3596-148">Gebruik de volgende op de client Beeline starten vanaf de SSH-sessie.</span><span class="sxs-lookup"><span data-stu-id="d3596-148">Use the following to start the Beeline client from the SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="d3596-149">Met deze opdracht wordt ervan uitgegaan dat u de standaardwaarde van gebruikt **admin** voor het aanmeldingsaccount voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="d3596-149">This command assumes that you used the default of **admin** for the login account for your cluster.</span></span>

2. <span data-ttu-id="d3596-150">Wanneer u aankomt bij de `jdbc:hive2://localhost:10001/>` gevraagd, voert u het volgende als u wilt de UDF toevoegen aan Hive en deze als een functie weer te geven.</span><span class="sxs-lookup"><span data-stu-id="d3596-150">Once you arrive at the `jdbc:hive2://localhost:10001/>` prompt, enter the following to add the UDF to Hive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="d3596-151">In dit voorbeeld wordt ervan uitgegaan dat Azure Storage standaard opslagruimte voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="d3596-151">This example assumes that Azure Storage is default storage for the cluster.</span></span> <span data-ttu-id="d3596-152">Als uw cluster in plaats daarvan Data Lake Store gebruikt, wijzigt u de `wasb:///` van waarde naar `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="d3596-152">If your cluster uses Data Lake Store instead, change the `wasb:///` value to `adl:///`.</span></span>

3. <span data-ttu-id="d3596-153">De UDF gebruiken om waarden opgehaald uit een tabel naar kleine letters tekenreeksen te converteren.</span><span class="sxs-lookup"><span data-stu-id="d3596-153">Use the UDF to convert values retrieved from a table to lower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="d3596-154">Deze query selecteert het platform van het apparaat (Android, Windows, iOS, enzovoort) uit de tabel, converteert u de tekenreeks voor kleine, en deze vervolgens weergeven.</span><span class="sxs-lookup"><span data-stu-id="d3596-154">This query selects the device platform (Android, Windows, iOS, etc.) from the table, convert the string to lower case, and then display them.</span></span> <span data-ttu-id="d3596-155">De uitvoer lijkt op de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="d3596-155">The output appears similar to the following text:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d3596-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d3596-156">Next steps</span></span>

<span data-ttu-id="d3596-157">Zie voor andere manieren om te werken met Hive, [Hive gebruiken met HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="d3596-157">For other ways to work with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="d3596-158">Zie voor meer informatie over functies Hive User-Defined [Hive operatoren en door de gebruiker gedefinieerde functies](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) sectie van de Hive-wiki op apache.org.</span><span class="sxs-lookup"><span data-stu-id="d3596-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of the Hive wiki at apache.org.</span></span>

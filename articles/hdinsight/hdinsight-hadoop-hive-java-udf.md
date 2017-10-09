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
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a>Gebruik van een Java UDF met Hive in HDInsight

Meer informatie over hoe toocreate een op Java gebaseerde gebruiker gedefinieerde functie (UDF) die met Hive werkt. Hallo Java UDF in dit voorbeeld converteert een tabel van tekenreeksen tooall kleine tekens.

## <a name="requirements"></a>Vereisten

* Een HDInsight-cluster 

    > [!IMPORTANT]
    > Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

    De meeste stappen in dit document werken op zowel Windows - en Linux gebaseerde clusters. Hallo stappen tooupload Hallo gecompileerd echter UDF toohello cluster en het specifieke tooLinux gebaseerde clusters worden uitgevoerd. Koppelingen vindt u tooinformation die kan worden gebruikt met Windows gebaseerde clusters.

* [Java-JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 of hoger (of een vergelijkbare groep, zoals OpenJDK)

* [Apache Maven](http://maven.apache.org/)

* Een teksteditor of IDE voor Java

    > [!IMPORTANT]
    > Als u Hallo Python-bestanden op een Windows-client maakt, moet u een editor die LF als een regel beëindigen gebruikt. Als u niet zeker of uw editor LF of CRLF gebruikt weet, raadpleegt u Hallo [probleemoplossing](#troubleshooting) sectie voor stapsgewijze instructies voor het verwijderen van Hallo CR-teken.

## <a name="create-an-example-java-udf"></a>Een voorbeeld Java UDF maken 

1. Gebruik vanaf een opdrachtregel Hallo toocreate een nieuw Maven-project te volgen:

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > Als u met behulp van PowerShell, kunt u aanhalingstekens rond Hallo parameters moet zetten. Bijvoorbeeld `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.

    Deze opdracht maakt u een map met de naam **exampleudf**, die Hallo Maven-project bevat.

2. Zodra het Hallo-project is gemaakt, verwijdert u Hallo **src-exampleudf/Testscenario** map die is gemaakt als onderdeel van het Hallo-project.

3. Open Hallo **exampleudf/pom.xml**, en vervang bestaande Hallo `<dependencies>` vermelding met Hallo XML te volgen:

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

    Deze vermeldingen opgeven Hallo-versie van Hadoop en Hive met HDInsight 3.5 opgenomen. U vindt meer informatie over het Hallo-versies van Hadoop en Hive met HDInsight wordt geleverd door Hallo [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md) document.

    Voeg een `<build>` sectie voordat Hallo `</project>` lijn op Hallo einde van Hallo-bestand. In deze sectie bevatten Hallo XML te volgen:

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

    Deze vermeldingen definiëren hoe toobuild Hallo project. In het bijzonder Hallo versie van Java die Hallo project gebruikt en hoe toobuild een uberjar voor implementatie toohello cluster.

    Hallo-bestand opslaan als Hallo wijzigingen zijn aangebracht.

4. Wijzig de naam van **exampleudf/src/main/java/com/microsoft/examples/App.java** te**ExampleUDF.java**, en open vervolgens Hallo-bestand in uw editor.

5. Vervang de inhoud Hallo Hallo **ExampleUDF.java** bestand met de volgende Hallo en sla vervolgens Hallo-bestand.

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

    Deze code implementeert een UDF die een string-waarde accepteert en retourneert een kleine versie van het Hallo-tekenreeks.

## <a name="build-and-install-hello-udf"></a>Opbouwen en Hallo UDF installeren

1. Gebruik Hallo opdracht toocompile te volgen en Hallo UDF pakket:

    ```bash
    mvn compile package
    ```

    Met deze opdracht maakt en pakketten UDF in Hallo Hallo `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` bestand.

2. Gebruik Hallo `scp` opdracht toocopy Hallo bestand toohello HDInsight-cluster.

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    Vervang `myuser` Hello SSH gebruikersaccount voor uw cluster. Vervang `mycluster` met de naam van de cluster Hallo. Als u een wachtwoord toosecure Hallo SSH-account gebruikt, zijn na vragen aan gebruiker tooenter Hallo wachtwoord. Als u een certificaat gebruikt, moet u mogelijk toouse hello `-i` parameter toospecify Hallo persoonlijke sleutelbestand.

3. Toohello-cluster via SSH verbinding.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

4. Kopiëren van Hallo SSH-sessie, opslag tooHDInsight Hallo jar-bestanden.

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a>Hallo UDF van Hive gebruiken

1. Gebruik Hallo toostart hello Beeline client Hallo SSH-sessie te volgen.

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    Met deze opdracht wordt ervan uitgegaan dat u standaard Hallo van gebruikt **admin** voor Hallo aanmeldingsaccount voor uw cluster.

2. Wanneer u bij Hallo aankomt `jdbc:hive2://localhost:10001/>` gevraagd, voert u Hallo tooadd Hallo UDF tooHive te volgen en deze weergeven als een functie.

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > In dit voorbeeld wordt ervan uitgegaan dat Azure Storage standaard opslagruimte voor Hallo-cluster. Als uw cluster in plaats daarvan Data Lake Store gebruikt, wijzigt u Hallo `wasb:///` waarde te`adl:///`.

3. Hallo UDF tooconvert waarden opgehaald van tekenreeksen voor tabel-toolower gebruiken.

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    Deze query selecteert apparaatplatform (Android, Windows, iOS, enzovoort) uit de tabel Hallo HALLO hallo tekenreeks toolower geval converteren en ze weergeven. Hallo-uitvoer wordt weergegeven vergelijkbaar toohello volgende tekst:

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

## <a name="next-steps"></a>Volgende stappen

Zie voor andere manieren toowork met Hive, [Hive gebruiken met HDInsight](hdinsight-use-hive.md).

Zie voor meer informatie over functies Hive User-Defined [Hive operatoren en door de gebruiker gedefinieerde functies](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) sectie van Hallo Hive wiki op apache.org.

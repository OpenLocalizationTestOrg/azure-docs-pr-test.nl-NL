---
title: aaaUse Azure Toolkit voor IntelliJ met Hortonworks Sandbox | Microsoft Docs
description: Meer informatie over hoe toouse HDInsight Tools in Azure Toolkit voor IntelliJ met Hortonworks Sandbox.
keywords: hadoop-hulpprogramma's, hive-query, intellij, hortonworks sandbox, azure toolkit voor intellij
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 2bf97068a9cec99fcc7b4ff9469b91d8cbe2a8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a>Gebruik van HDInsight Tools voor IntelliJ met Hortonworks Sandbox

Meer informatie over hoe toouse HDInsight Tools for IntelliJ toodevelop Apache Scala-toepassingen en test vervolgens de toepassingen op Hallo [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) uitgevoerd op uw werkstation. 

[IntelliJ IDEA](https://www.jetbrains.com/idea/) is een geïntegreerde Java-ontwikkelomgeving (IDE) voor het ontwikkelen van computersoftware. Nadat u hebt ontwikkeld en getest van uw toepassingen op de Hortonworks Sandbox, kunt u ze te[Azure HDInsight](hdinsight-hadoop-introduction.md).

## <a name="prerequisites"></a>Vereisten

Voordat u met deze zelfstudie begint, moet u over de volgende onderdelen beschikken:

- Hortonworks Data Platform HDP () 2.4 op de Hortonworks Sandbox uitgevoerd op uw lokale omgeving. tooconfigure HDP, Zie [hello Hadoop-ecosysteem aan een Hadoop-sandbox op een virtuele machine aan de slag](hdinsight-hadoop-emulator-get-started.md). 
    >[!NOTE]
    >HDInsight Tools for IntelliJ is getest met de HDP 2.4. tooget HDP 2.4, vouw **Hortonworks Sandbox archief** op Hallo [Hortonworks Sandbox site downloadt](http://hortonworks.com/downloads/#sandbox).

- [Java Developer Kit (JDK) versie 1.8 of hoger](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). JDK is vereist voor hello Azure Toolkit voor IntelliJ.

- [IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) Hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) invoegtoepassing en Hallo [Azure Toolkit voor IntelliJ](../azure-toolkit-for-intellij.md) invoegtoepassing. HDInsight Tools for IntelliJ is beschikbaar als onderdeel van hello Azure Toolkit voor IntelliJ. 

  tooinstall Hallo-invoegtoepassingen Hallo te volgen:

  1. Open IntelliJ IDEA.
  2. Op Hallo **Welkom** Schakel in het scherm **configureren**, en selecteer vervolgens **Plugins**.
  3. Selecteer **-invoegtoepassing installeren JetBrains** in de linkerbenedenhoek Hallo.
  4. Gebruik Hallo zoeken functie toosearch voor **Scala**, en selecteer vervolgens **installeren**.
  5. Selecteer **opnieuw IntelliJ IDEA** toocomplete Hallo-installatie.
  6. Herhaal stap 4 en 5 tooinstall hello **Azure Toolkit voor IntelliJ**. Zie voor meer informatie [installeren hello Azure Toolkit voor IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="create-a-spark-scala-application"></a>Een Spark Scala-toepassing maken

In deze sectie maakt u een voorbeeldproject Scala via IntelliJ IDEA. In de volgende sectie hello koppel IntelliJ IDEA toohello Hortonworks Sandbox (emulator) voordat u Hallo-project verzenden.

1. Open IntelliJ IDEA op uw werkstation. In Hallo **nieuw Project** dialoogvenster vak, Hallo te volgen:

   a. Selecteer **HDInsight** > **Spark in HDInsight (Scala)**.

   b. In Hallo **Build hulpprogramma** lijst, selecteert u Hallo te volgen, op basis van tooyour nodig:

    * **Maven**, voor ondersteuning van de wizard Scala project maken
    * **SBT**, voor het beheren van Hallo afhankelijkheden en bouwen voor Hallo Scala project

   ![het dialoogvenster Nieuw Project Hallo](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. Selecteer **volgende**.

3. In Hallo volgende **nieuw Project** dialoogvenster vak, Hallo te volgen:

    ![IntelliJ Scala eigenschappen-project maken](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    a. In Hallo **projectnaam** Voer de naam van het project.

    b. In Hallo **projectlocatie** Geef de projectlocatie van een.

    c. Volgende toohello **Project SDK** vervolgkeuzelijst, selecteer **nieuw**, selecteer **JDK**, en geef vervolgens de map Hallo van Java-JDK 1,7 of hoger. Selecteer **Java 1.8** voor Hallo Spark 2.x-cluster, of selecteer **Java 1.7** voor Hallo Spark 1.x-cluster. Hallo is standaardlocatie C:\Program Files\Java\jdk1.8.x_xxx.

    d. In Hallo **Spark versie** vervolgkeuzelijst, wizard voor het maken van project Scala integreert de juiste versie Hallo voor Spark SDK en Scala SDK. Als Hallo Spark-cluster versie ouder dan 2.0 is, selecteert u **Spark 1.x**. Selecteer anders **Spark2.x**. In dit voorbeeld maakt gebruik van Spark 1.6.2 (Scala 2.10.5). Zorg ervoor dat u van Hallo opslagplaats gemarkeerd Scala gebruikmaakt 2.10.x. Gebruik geen Hallo opslagplaats gemarkeerd Scala 2.11.x.

4. Selecteer **Voltooien**.

5. Als hello **Project** weergave nog niet is geopend, drukt u op **Alt + 1** tooopen deze.

6. In **Projectverkenner**, vouw Hallo-project en selecteer vervolgens **src**.

7. Met de rechtermuisknop op **src**, wijst u te**nieuw**, en selecteer vervolgens **Scala klasse**.

8. In Hallo **naam** vak, voer een naam in Hallo **soort** de optie **Object**, en selecteer vervolgens **OK**.

    ![Hallo maken nieuwe Scala klasse venster](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. Plak in Hallo .scala bestand Hallo code te volgen:

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. Op Hallo **bouwen** selecteert u **Build project**. Zorg ervoor dat Hallo compilatie met succes is voltooid.


## <a name="link-toohello-hortonworks-sandbox"></a>Toohello Hortonworks sandbox-koppeling

Voordat u tooa Hortonworks Sandbox (emulator) koppelen kunt, moet u een bestaande IntelliJ toepassing hebben.

toolink tooan emulator Hallo te volgen:

1. Open Hallo-project in IntelliJ.

2. Op Hallo **weergave** selecteert u **'s Windows**, en selecteer vervolgens **Azure Explorer**.

3. Vouw **Azure**, met de rechtermuisknop op **HDInsight**, en selecteer vervolgens **koppelen van een Emulator**.

4. In Hallo **Link A nieuwe Emulator** venster Voer Hallo wachtwoord hebt geconfigureerd voor het hoofdaccount Hallo Hallo Hortonworks Sandbox, vergelijkbare toothose waarden invoeren in de volgende schermafbeelding Hallo en selecteer vervolgens **OK** . 

   ![Hallo 'Koppeling een nieuwe Emulator' venster](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. tooconfigure Hallo-emulator, selecteer **Ja**.

Wanneer de emulator Hallo met succes is verbonden, worden Hallo-emulator (Hortonworks Sandbox) wordt vermeld in Hallo HDInsight-knooppunt.

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a>Hallo Spark Scala toepassing toohello Hortonworks Sandbox verzenden

Nadat u IntelliJ IDEA toohello emulator hebt gekoppeld, kunt u uw project verzenden.

een project tooan-emulator toosubmit Hallo te volgen:

1. In **Projectverkenner**, met de rechtermuisknop op het Hallo-project en selecteer vervolgens **indienen Spark toepassing tooHDInsight**.

2. Hallo te volgen:

    a. In Hallo **Spark-cluster (alleen voor Linux)** vervolgkeuzelijst, selecteert u uw lokale Hortonworks Sandbox.

    b. In Hallo **Main klassenaam** vak, kies of Hallo hoofdklasse naam invoeren. Voor deze zelfstudie is Hallo naam **GroupByTest**.

3. Selecteer **indienen**. Hallo taak verzending van Logboeken worden weergegeven in Hallo Spark verzending hulpprogramma venster.

## <a name="next-steps"></a>Volgende stappen

- hoe toocreate Spark scala-toepassingen voor HDInsight met behulp van HDInsight Tools voor IntelliJ, te gaan toolearn[gebruik HDInsight-hulpprogramma's in Azure Toolkit voor IntelliJ toocreate Spark scala-toepassingen voor HDInsight Spark Linux-cluster](hdinsight-apache-spark-intellij-tool-plugin.md).

- een video van HDInsight Tools for IntelliJ, toowatch te gaan[introduceren HDInsight Tools voor IntelliJ voor het ontwikkelen van Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).

- toolearn hoe toodebug Spark scala-toepassingen met behulp van Hallo toolkit op afstand in HDInsight via SSH, gaat u te[op afstand fouten opsporen in Spark scala-toepassingen op een HDInsight-cluster in Azure werkset voor IntelliJ via SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).

- toolearn hoe toodebug Spark scala-toepassingen met behulp van Hallo toolkit op afstand in HDInsight via VPN, gaat u te[gebruik HDInsight-hulpprogramma's in Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand op HDInsight Spark Linux-cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).

- hoe toouse HDInsight Tools voor Eclipse toocreate een Spark-toepassing te gaan toolearn[gebruik HDInsight-hulpprogramma's in Azure Toolkit voor Eclipse toocreate Spark scala-toepassingen](hdinsight-apache-spark-eclipse-tool-plugin.md).

- een video van HDInsight Tools voor Eclipse toowatch te gaan[HDInsight-hulpprogramma voor Eclipse toocreate Spark scala-toepassingen met](https://mix.office.com/watch/1rau2mopb6fha).

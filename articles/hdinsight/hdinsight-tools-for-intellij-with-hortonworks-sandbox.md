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
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="27d82-104">Gebruik van HDInsight Tools voor IntelliJ met Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="27d82-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="27d82-105">Meer informatie over hoe toouse HDInsight Tools for IntelliJ toodevelop Apache Scala-toepassingen en test vervolgens de toepassingen op Hallo [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) uitgevoerd op uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="27d82-105">Learn how toouse HDInsight Tools for IntelliJ toodevelop Apache Scala applications and then test hello applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="27d82-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is een geïntegreerde Java-ontwikkelomgeving (IDE) voor het ontwikkelen van computersoftware.</span><span class="sxs-lookup"><span data-stu-id="27d82-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="27d82-107">Nadat u hebt ontwikkeld en getest van uw toepassingen op de Hortonworks Sandbox, kunt u ze te[Azure HDInsight](hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="27d82-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them too[Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27d82-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="27d82-108">Prerequisites</span></span>

<span data-ttu-id="27d82-109">Voordat u met deze zelfstudie begint, moet u over de volgende onderdelen beschikken:</span><span class="sxs-lookup"><span data-stu-id="27d82-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="27d82-110">Hortonworks Data Platform HDP () 2.4 op de Hortonworks Sandbox uitgevoerd op uw lokale omgeving.</span><span class="sxs-lookup"><span data-stu-id="27d82-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="27d82-111">tooconfigure HDP, Zie [hello Hadoop-ecosysteem aan een Hadoop-sandbox op een virtuele machine aan de slag](hdinsight-hadoop-emulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="27d82-111">tooconfigure HDP, see [Get started in hello Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="27d82-112">HDInsight Tools for IntelliJ is getest met de HDP 2.4.</span><span class="sxs-lookup"><span data-stu-id="27d82-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="27d82-113">tooget HDP 2.4, vouw **Hortonworks Sandbox archief** op Hallo [Hortonworks Sandbox site downloadt](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="27d82-113">tooget HDP 2.4, expand **Hortonworks Sandbox Archive** on hello [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="27d82-114">[Java Developer Kit (JDK) versie 1.8 of hoger](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="27d82-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="27d82-115">JDK is vereist voor hello Azure Toolkit voor IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="27d82-115">JDK is required by hello Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="27d82-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) Hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) invoegtoepassing en Hallo [Azure Toolkit voor IntelliJ](../azure-toolkit-for-intellij.md) invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="27d82-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and hello [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="27d82-117">HDInsight Tools for IntelliJ is beschikbaar als onderdeel van hello Azure Toolkit voor IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="27d82-117">HDInsight Tools for IntelliJ is available as a part of hello Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="27d82-118">tooinstall Hallo-invoegtoepassingen Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="27d82-118">tooinstall hello plug-ins, do hello following:</span></span>

  1. <span data-ttu-id="27d82-119">Open IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="27d82-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="27d82-120">Op Hallo **Welkom** Schakel in het scherm **configureren**, en selecteer vervolgens **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="27d82-120">On hello **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="27d82-121">Selecteer **-invoegtoepassing installeren JetBrains** in de linkerbenedenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="27d82-121">Select **Install JetBrains plugin** in hello lower-left corner.</span></span>
  4. <span data-ttu-id="27d82-122">Gebruik Hallo zoeken functie toosearch voor **Scala**, en selecteer vervolgens **installeren**.</span><span class="sxs-lookup"><span data-stu-id="27d82-122">Use hello search function toosearch for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="27d82-123">Selecteer **opnieuw IntelliJ IDEA** toocomplete Hallo-installatie.</span><span class="sxs-lookup"><span data-stu-id="27d82-123">Select **Restart IntelliJ IDEA** toocomplete hello installation.</span></span>
  6. <span data-ttu-id="27d82-124">Herhaal stap 4 en 5 tooinstall hello **Azure Toolkit voor IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="27d82-124">Repeat step 4 and 5 tooinstall hello **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="27d82-125">Zie voor meer informatie [installeren hello Azure Toolkit voor IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="27d82-125">For more information, see [Install hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="27d82-126">Een Spark Scala-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="27d82-126">Create a Spark Scala application</span></span>

<span data-ttu-id="27d82-127">In deze sectie maakt u een voorbeeldproject Scala via IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="27d82-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="27d82-128">In de volgende sectie hello koppel IntelliJ IDEA toohello Hortonworks Sandbox (emulator) voordat u Hallo-project verzenden.</span><span class="sxs-lookup"><span data-stu-id="27d82-128">In hello next section, you link IntelliJ IDEA toohello Hortonworks Sandbox (emulator) before you submit hello project.</span></span>

1. <span data-ttu-id="27d82-129">Open IntelliJ IDEA op uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="27d82-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="27d82-130">In Hallo **nieuw Project** dialoogvenster vak, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="27d82-130">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="27d82-131">a.</span><span class="sxs-lookup"><span data-stu-id="27d82-131">a.</span></span> <span data-ttu-id="27d82-132">Selecteer **HDInsight** > **Spark in HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="27d82-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="27d82-133">b.</span><span class="sxs-lookup"><span data-stu-id="27d82-133">b.</span></span> <span data-ttu-id="27d82-134">In Hallo **Build hulpprogramma** lijst, selecteert u Hallo te volgen, op basis van tooyour nodig:</span><span class="sxs-lookup"><span data-stu-id="27d82-134">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

    * <span data-ttu-id="27d82-135">**Maven**, voor ondersteuning van de wizard Scala project maken</span><span class="sxs-lookup"><span data-stu-id="27d82-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="27d82-136">**SBT**, voor het beheren van Hallo afhankelijkheden en bouwen voor Hallo Scala project</span><span class="sxs-lookup"><span data-stu-id="27d82-136">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

   ![het dialoogvenster Nieuw Project Hallo](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="27d82-138">Selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="27d82-138">Select **Next**.</span></span>

3. <span data-ttu-id="27d82-139">In Hallo volgende **nieuw Project** dialoogvenster vak, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="27d82-139">In hello next **New Project** dialog box, do hello following:</span></span>

    ![IntelliJ Scala eigenschappen-project maken](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="27d82-141">a.</span><span class="sxs-lookup"><span data-stu-id="27d82-141">a.</span></span> <span data-ttu-id="27d82-142">In Hallo **projectnaam** Voer de naam van het project.</span><span class="sxs-lookup"><span data-stu-id="27d82-142">In hello **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="27d82-143">b.</span><span class="sxs-lookup"><span data-stu-id="27d82-143">b.</span></span> <span data-ttu-id="27d82-144">In Hallo **projectlocatie** Geef de projectlocatie van een.</span><span class="sxs-lookup"><span data-stu-id="27d82-144">In hello **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="27d82-145">c.</span><span class="sxs-lookup"><span data-stu-id="27d82-145">c.</span></span> <span data-ttu-id="27d82-146">Volgende toohello **Project SDK** vervolgkeuzelijst, selecteer **nieuw**, selecteer **JDK**, en geef vervolgens de map Hallo van Java-JDK 1,7 of hoger.</span><span class="sxs-lookup"><span data-stu-id="27d82-146">Next toohello **Project SDK** drop-down list, select **New**, select **JDK**, and then specify hello folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="27d82-147">Selecteer **Java 1.8** voor Hallo Spark 2.x-cluster, of selecteer **Java 1.7** voor Hallo Spark 1.x-cluster.</span><span class="sxs-lookup"><span data-stu-id="27d82-147">Select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span> <span data-ttu-id="27d82-148">Hallo is standaardlocatie C:\Program Files\Java\jdk1.8.x_xxx.</span><span class="sxs-lookup"><span data-stu-id="27d82-148">hello default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="27d82-149">d.</span><span class="sxs-lookup"><span data-stu-id="27d82-149">d.</span></span> <span data-ttu-id="27d82-150">In Hallo **Spark versie** vervolgkeuzelijst, wizard voor het maken van project Scala integreert de juiste versie Hallo voor Spark SDK en Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="27d82-150">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="27d82-151">Als Hallo Spark-cluster versie ouder dan 2.0 is, selecteert u **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="27d82-151">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="27d82-152">Selecteer anders **Spark2.x**.</span><span class="sxs-lookup"><span data-stu-id="27d82-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="27d82-153">In dit voorbeeld maakt gebruik van Spark 1.6.2 (Scala 2.10.5).</span><span class="sxs-lookup"><span data-stu-id="27d82-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="27d82-154">Zorg ervoor dat u van Hallo opslagplaats gemarkeerd Scala gebruikmaakt 2.10.x.</span><span class="sxs-lookup"><span data-stu-id="27d82-154">Make sure that you are using hello repository marked Scala 2.10.x.</span></span> <span data-ttu-id="27d82-155">Gebruik geen Hallo opslagplaats gemarkeerd Scala 2.11.x.</span><span class="sxs-lookup"><span data-stu-id="27d82-155">Do not use hello repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="27d82-156">Selecteer **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="27d82-156">Select **Finish**.</span></span>

5. <span data-ttu-id="27d82-157">Als hello **Project** weergave nog niet is geopend, drukt u op **Alt + 1** tooopen deze.</span><span class="sxs-lookup"><span data-stu-id="27d82-157">If hello **Project** view is not already open, press **Alt+1** tooopen it.</span></span>

6. <span data-ttu-id="27d82-158">In **Projectverkenner**, vouw Hallo-project en selecteer vervolgens **src**.</span><span class="sxs-lookup"><span data-stu-id="27d82-158">In **Project Explorer**, expand hello project, and then select **src**.</span></span>

7. <span data-ttu-id="27d82-159">Met de rechtermuisknop op **src**, wijst u te**nieuw**, en selecteer vervolgens **Scala klasse**.</span><span class="sxs-lookup"><span data-stu-id="27d82-159">Right-click **src**, point too**New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="27d82-160">In Hallo **naam** vak, voer een naam in Hallo **soort** de optie **Object**, en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="27d82-160">In hello **Name** box, enter a name, in hello **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![Hallo maken nieuwe Scala klasse venster](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="27d82-162">Plak in Hallo .scala bestand Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="27d82-162">In hello .scala file, paste hello following code:</span></span>

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

10. <span data-ttu-id="27d82-163">Op Hallo **bouwen** selecteert u **Build project**.</span><span class="sxs-lookup"><span data-stu-id="27d82-163">On hello **Build** menu, select **Build project**.</span></span> <span data-ttu-id="27d82-164">Zorg ervoor dat Hallo compilatie met succes is voltooid.</span><span class="sxs-lookup"><span data-stu-id="27d82-164">Make sure that hello compilation has been completed successfully.</span></span>


## <a name="link-toohello-hortonworks-sandbox"></a><span data-ttu-id="27d82-165">Toohello Hortonworks sandbox-koppeling</span><span class="sxs-lookup"><span data-stu-id="27d82-165">Link toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="27d82-166">Voordat u tooa Hortonworks Sandbox (emulator) koppelen kunt, moet u een bestaande IntelliJ toepassing hebben.</span><span class="sxs-lookup"><span data-stu-id="27d82-166">Before you can link tooa Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="27d82-167">toolink tooan emulator Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="27d82-167">toolink tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="27d82-168">Open Hallo-project in IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="27d82-168">Open hello project in IntelliJ.</span></span>

2. <span data-ttu-id="27d82-169">Op Hallo **weergave** selecteert u **'s Windows**, en selecteer vervolgens **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="27d82-169">On hello **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="27d82-170">Vouw **Azure**, met de rechtermuisknop op **HDInsight**, en selecteer vervolgens **koppelen van een Emulator**.</span><span class="sxs-lookup"><span data-stu-id="27d82-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="27d82-171">In Hallo **Link A nieuwe Emulator** venster Voer Hallo wachtwoord hebt geconfigureerd voor het hoofdaccount Hallo Hallo Hortonworks Sandbox, vergelijkbare toothose waarden invoeren in de volgende schermafbeelding Hallo en selecteer vervolgens **OK** .</span><span class="sxs-lookup"><span data-stu-id="27d82-171">In hello **Link A New Emulator** window, enter hello password that you've configured for hello root account of hello Hortonworks Sandbox, enter values similar toothose in hello following screenshot, and then select **OK**.</span></span> 

   ![Hallo 'Koppeling een nieuwe Emulator' venster](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="27d82-173">tooconfigure Hallo-emulator, selecteer **Ja**.</span><span class="sxs-lookup"><span data-stu-id="27d82-173">tooconfigure hello emulator, select **Yes**.</span></span>

<span data-ttu-id="27d82-174">Wanneer de emulator Hallo met succes is verbonden, worden Hallo-emulator (Hortonworks Sandbox) wordt vermeld in Hallo HDInsight-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="27d82-174">When hello emulator is connected successfully, hello emulator (Hortonworks Sandbox) is listed in hello HDInsight node.</span></span>

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a><span data-ttu-id="27d82-175">Hallo Spark Scala toepassing toohello Hortonworks Sandbox verzenden</span><span class="sxs-lookup"><span data-stu-id="27d82-175">Submit hello Spark Scala application toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="27d82-176">Nadat u IntelliJ IDEA toohello emulator hebt gekoppeld, kunt u uw project verzenden.</span><span class="sxs-lookup"><span data-stu-id="27d82-176">After you have linked IntelliJ IDEA toohello emulator, you can submit your project.</span></span>

<span data-ttu-id="27d82-177">een project tooan-emulator toosubmit Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="27d82-177">toosubmit a project tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="27d82-178">In **Projectverkenner**, met de rechtermuisknop op het Hallo-project en selecteer vervolgens **indienen Spark toepassing tooHDInsight**.</span><span class="sxs-lookup"><span data-stu-id="27d82-178">In **Project Explorer**, right-click hello project, and then select **Submit Spark application tooHDInsight**.</span></span>

2. <span data-ttu-id="27d82-179">Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="27d82-179">Do hello following:</span></span>

    <span data-ttu-id="27d82-180">a.</span><span class="sxs-lookup"><span data-stu-id="27d82-180">a.</span></span> <span data-ttu-id="27d82-181">In Hallo **Spark-cluster (alleen voor Linux)** vervolgkeuzelijst, selecteert u uw lokale Hortonworks Sandbox.</span><span class="sxs-lookup"><span data-stu-id="27d82-181">In hello **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="27d82-182">b.</span><span class="sxs-lookup"><span data-stu-id="27d82-182">b.</span></span> <span data-ttu-id="27d82-183">In Hallo **Main klassenaam** vak, kies of Hallo hoofdklasse naam invoeren.</span><span class="sxs-lookup"><span data-stu-id="27d82-183">In hello **Main class name** box, choose or enter hello main class name.</span></span> <span data-ttu-id="27d82-184">Voor deze zelfstudie is Hallo naam **GroupByTest**.</span><span class="sxs-lookup"><span data-stu-id="27d82-184">For this tutorial, hello name is **GroupByTest**.</span></span>

3. <span data-ttu-id="27d82-185">Selecteer **indienen**.</span><span class="sxs-lookup"><span data-stu-id="27d82-185">Select **Submit**.</span></span> <span data-ttu-id="27d82-186">Hallo taak verzending van Logboeken worden weergegeven in Hallo Spark verzending hulpprogramma venster.</span><span class="sxs-lookup"><span data-stu-id="27d82-186">hello job submission logs are shown in hello Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27d82-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="27d82-187">Next steps</span></span>

- <span data-ttu-id="27d82-188">hoe toocreate Spark scala-toepassingen voor HDInsight met behulp van HDInsight Tools voor IntelliJ, te gaan toolearn[gebruik HDInsight-hulpprogramma's in Azure Toolkit voor IntelliJ toocreate Spark scala-toepassingen voor HDInsight Spark Linux-cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="27d82-188">toolearn how toocreate Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="27d82-189">een video van HDInsight Tools for IntelliJ, toowatch te gaan[introduceren HDInsight Tools voor IntelliJ voor het ontwikkelen van Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).</span><span class="sxs-lookup"><span data-stu-id="27d82-189">toowatch a video of HDInsight Tools for IntelliJ, go too[Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="27d82-190">toolearn hoe toodebug Spark scala-toepassingen met behulp van Hallo toolkit op afstand in HDInsight via SSH, gaat u te[op afstand fouten opsporen in Spark scala-toepassingen op een HDInsight-cluster in Azure werkset voor IntelliJ via SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="27d82-190">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through SSH, go too[Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="27d82-191">toolearn hoe toodebug Spark scala-toepassingen met behulp van Hallo toolkit op afstand in HDInsight via VPN, gaat u te[gebruik HDInsight-hulpprogramma's in Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand op HDInsight Spark Linux-cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span><span class="sxs-lookup"><span data-stu-id="27d82-191">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through VPN, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="27d82-192">hoe toouse HDInsight Tools voor Eclipse toocreate een Spark-toepassing te gaan toolearn[gebruik HDInsight-hulpprogramma's in Azure Toolkit voor Eclipse toocreate Spark scala-toepassingen](hdinsight-apache-spark-eclipse-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="27d82-192">toolearn how toouse HDInsight Tools for Eclipse toocreate a Spark application, go too[Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="27d82-193">een video van HDInsight Tools voor Eclipse toowatch te gaan[HDInsight-hulpprogramma voor Eclipse toocreate Spark scala-toepassingen met](https://mix.office.com/watch/1rau2mopb6fha).</span><span class="sxs-lookup"><span data-stu-id="27d82-193">toowatch a video of HDInsight Tools for Eclipse, go too[Use HDInsight Tool for Eclipse toocreate Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>

---
title: Scala app maken om te worden uitgevoerd op Spark-clusters - Azure HDInsight | Microsoft Docs
description: Maak een toepassing Spark is geschreven in Scala met Apache Maven build-systeem als een bestaande Maven archetype voor Scala geleverd door IntelliJ IDEA.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 95dba08744357f8800b05e3d4b892e3a363d5985
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-scala-maven-application-to-run-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="b521b-103">Maak een Scala Maven-toepassing uit te voeren op Apache Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b521b-103">Create a Scala Maven application to run on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="b521b-104">Informatie over het maken van een toepassing Spark is geschreven in Scala met behulp van Maven met IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="b521b-104">Learn how to create a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="b521b-105">Het artikel Apache Maven gebruikt als de build-systeem en begint met een bestaande Maven archetype voor Scala geleverd door IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="b521b-105">The article uses Apache Maven as the build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="b521b-106">Maken van een toepassing Scala in IntelliJ IDEA omvat de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="b521b-106">Creating a Scala application in IntelliJ IDEA involves the following steps:</span></span>

* <span data-ttu-id="b521b-107">Maven gebruiken als de build-systeem.</span><span class="sxs-lookup"><span data-stu-id="b521b-107">Use Maven as the build system.</span></span>
* <span data-ttu-id="b521b-108">Werkt Project Object Model (POM) Spark module afhankelijkheden moeten worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="b521b-108">Update Project Object Model (POM) file to resolve Spark module dependencies.</span></span>
* <span data-ttu-id="b521b-109">Uw toepassing worden geschreven in Scala.</span><span class="sxs-lookup"><span data-stu-id="b521b-109">Write your application in Scala.</span></span>
* <span data-ttu-id="b521b-110">Genereert een jar-bestand dat kan worden verstuurd naar HDInsight Spark-clusters.</span><span class="sxs-lookup"><span data-stu-id="b521b-110">Generate a jar file that can be submitted to HDInsight Spark clusters.</span></span>
* <span data-ttu-id="b521b-111">Voer de toepassing in Spark-cluster met behulp van Livy.</span><span class="sxs-lookup"><span data-stu-id="b521b-111">Run the application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="b521b-112">HDInsight biedt ook een hulpprogramma van de invoegtoepassing voor IntelliJ IDEA vereenvoudigen van het proces van het maken en verzenden van toepassingen met een HDInsight Spark-cluster op Linux.</span><span class="sxs-lookup"><span data-stu-id="b521b-112">HDInsight also provides an IntelliJ IDEA plugin tool to ease the process of creating and submitting applications to an HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="b521b-113">Zie voor meer informatie [gebruik de invoegtoepassing HDInsight Tools for IntelliJ IDEA maken en verzenden van Spark scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="b521b-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b521b-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b521b-114">Prerequisites</span></span>

* <span data-ttu-id="b521b-115">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b521b-115">An Azure subscription.</span></span> <span data-ttu-id="b521b-116">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b521b-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b521b-117">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b521b-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="b521b-118">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b521b-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="b521b-119">Oracle Java Development kit.</span><span class="sxs-lookup"><span data-stu-id="b521b-119">Oracle Java Development kit.</span></span> <span data-ttu-id="b521b-120">Kunt u het installeren van [hier](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="b521b-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="b521b-121">Een Java IDE.</span><span class="sxs-lookup"><span data-stu-id="b521b-121">A Java IDE.</span></span> <span data-ttu-id="b521b-122">Dit artikel wordt IntelliJ IDEA 15.0.1 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b521b-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="b521b-123">Kunt u het installeren van [hier](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="b521b-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="b521b-124">Scala-invoegtoepassing voor IntelliJ IDEA installeren</span><span class="sxs-lookup"><span data-stu-id="b521b-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="b521b-125">Als IntelliJ IDEA installatie niet niet gevraagd voor het inschakelen van Scala-invoegtoepassing, IntelliJ IDEA starten en de volgende stappen voor het installeren van de invoegtoepassing doorlopen:</span><span class="sxs-lookup"><span data-stu-id="b521b-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through the following steps to install the plugin:</span></span>

1. <span data-ttu-id="b521b-126">IntelliJ IDEA Start en klik in het welkomstscherm op **configureren** en klik vervolgens op **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="b521b-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![Scala invoegtoepassing inschakelen](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="b521b-128">Klik in het volgende scherm op **-invoegtoepassing installeren JetBrains** van de linkerbenedenhoek.</span><span class="sxs-lookup"><span data-stu-id="b521b-128">In the next screen, click **Install JetBrains plugin** from the lower left corner.</span></span> <span data-ttu-id="b521b-129">In de **JetBrains Plugins Bladeren** dialoogvenster dat wordt geopend, Scala zoeken en klik vervolgens op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="b521b-129">In the **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![Scala-invoegtoepassing installeren](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="b521b-131">Nadat de invoegtoepassing is geïnstalleerd, klikt u op de **opnieuw IntelliJ IDEA knop** opnieuw opstarten van de IDE.</span><span class="sxs-lookup"><span data-stu-id="b521b-131">After the plugin installs successfully, click the **Restart IntelliJ IDEA button** to restart the IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="b521b-132">Een zelfstandige Scala-project maken</span><span class="sxs-lookup"><span data-stu-id="b521b-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="b521b-133">IntelliJ IDEA Start en een nieuw project maken.</span><span class="sxs-lookup"><span data-stu-id="b521b-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="b521b-134">De volgende opties in het dialoogvenster Nieuw project en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b521b-134">In the new project dialog box, make the following choices, and then click **Next**.</span></span>
   
    ![Maven-project maken](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="b521b-136">Selecteer **Maven** als het projecttype.</span><span class="sxs-lookup"><span data-stu-id="b521b-136">Select **Maven** as the project type.</span></span>
   * <span data-ttu-id="b521b-137">Geef een **Project SDK**.</span><span class="sxs-lookup"><span data-stu-id="b521b-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="b521b-138">Klik op Nieuw en navigeer naar de installatiemap Java doorgaans `C:\Program Files\Java\jdk1.8.0_66`.</span><span class="sxs-lookup"><span data-stu-id="b521b-138">Click New and navigate to the Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="b521b-139">Selecteer de **maken van archetype** optie.</span><span class="sxs-lookup"><span data-stu-id="b521b-139">Select the **Create from archetype** option.</span></span>
   * <span data-ttu-id="b521b-140">Selecteer in de lijst van archetypes **org.scala tools.archetypes:scala-archetype eenvoudige**.</span><span class="sxs-lookup"><span data-stu-id="b521b-140">From the list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="b521b-141">Hiermee wordt de juiste mapstructuur en de vereiste standaard afhankelijkheden voor het schrijven van Scala programma downloaden.</span><span class="sxs-lookup"><span data-stu-id="b521b-141">This will create the right directory structure and download the required default dependencies to write Scala program.</span></span>
2. <span data-ttu-id="b521b-142">Relevante waarden opgeven voor **GroupId**, **artefact-id**, en **versie**.</span><span class="sxs-lookup"><span data-stu-id="b521b-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="b521b-143">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b521b-143">Click **Next**.</span></span>
3. <span data-ttu-id="b521b-144">In het volgende dialoogvenster waarin u Maven-basismap en andere instellingen voor gebruikers opgeven, accepteer de standaardinstellingen en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b521b-144">In the next dialog box, where you specify Maven home directory and other user settings, accept the defaults and click **Next**.</span></span>
4. <span data-ttu-id="b521b-145">Geef een naam van het project en de locatie in het dialoogvenster laatste en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b521b-145">In the last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="b521b-146">Verwijder de **MySpec.Scala** op het bestand **src\test\scala\com\microsoft\spark\example**.</span><span class="sxs-lookup"><span data-stu-id="b521b-146">Delete the **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="b521b-147">U hoeft niet dit voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b521b-147">You do not need this for the application.</span></span>
6. <span data-ttu-id="b521b-148">Indien nodig, wijzig de naam van de bron- en standaardbestanden.</span><span class="sxs-lookup"><span data-stu-id="b521b-148">If required, rename the default source and test files.</span></span> <span data-ttu-id="b521b-149">Ga vanuit het linkerdeelvenster in de IntelliJ IDEA naar **src\main\scala\com.microsoft.spark.example**.</span><span class="sxs-lookup"><span data-stu-id="b521b-149">From the left pane in the IntelliJ IDEA, navigate to **src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="b521b-150">Met de rechtermuisknop op **App.scala**, klikt u op **opsplitsen**, bestandsnaam wijzigen, klikt u op en geef de nieuwe naam voor de toepassing in het dialoogvenster en klik op **opsplitsen**.</span><span class="sxs-lookup"><span data-stu-id="b521b-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in the dialog box, provide the new name for the application and then click **Refactor**.</span></span>
   
    ![De naam van bestanden](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="b521b-152">In de volgende stappen wordt om te definiëren van de afhankelijkheden voor de toepassing Spark Scala pom.xml bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="b521b-152">In the subsequent steps, you will update the pom.xml to define the dependencies for the Spark Scala application.</span></span> <span data-ttu-id="b521b-153">Voor deze afhankelijkheden worden gedownload en automatisch opgelost, moet u Maven dienovereenkomstig configureren.</span><span class="sxs-lookup"><span data-stu-id="b521b-153">For those dependencies to be downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![Maven configureren voor automatische downloads](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="b521b-155">Van de **bestand** menu, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="b521b-155">From the **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="b521b-156">In de **instellingen** dialoogvenster vak, gaat u naar **bouwen, kan worden uitgevoerd, implementatie** > **Build Tools** > **Maven** > **Importing**.</span><span class="sxs-lookup"><span data-stu-id="b521b-156">In the **Settings** dialog box, navigate to **Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="b521b-157">Selecteer de optie voor **Import Maven projects automatisch**.</span><span class="sxs-lookup"><span data-stu-id="b521b-157">Select the option to **Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="b521b-158">Klik op **toepassen**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b521b-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="b521b-159">Werk het bronbestand Scala zodanig dat de toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="b521b-159">Update the Scala source file to include your application code.</span></span> <span data-ttu-id="b521b-160">Open en de bestaande voorbeeldcode vervangen door de volgende code en sla de wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="b521b-160">Open and replace the existing sample code with the following code and save the changes.</span></span> <span data-ttu-id="b521b-161">Deze code leest de gegevens van de HVAC.csv (beschikbaar op alle HDInsight Spark-clusters), worden de rijen die alleen in de zesde kolom één cijfer hebben en schrijft de uitvoer naar **/HVACOut** onder de standaardcontainer opslag voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="b521b-161">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the sixth column, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO to wasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows which have only one digit in the 7th column in the CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. <span data-ttu-id="b521b-162">Werk de pom.xml.</span><span class="sxs-lookup"><span data-stu-id="b521b-162">Update the pom.xml.</span></span>
   
   1. <span data-ttu-id="b521b-163">Binnen `<project>\<properties>` Voeg de volgende:</span><span class="sxs-lookup"><span data-stu-id="b521b-163">Within `<project>\<properties>` add the following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="b521b-164">Binnen `<project>\<dependencies>` Voeg de volgende:</span><span class="sxs-lookup"><span data-stu-id="b521b-164">Within `<project>\<dependencies>` add the following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="b521b-165">Sla de wijzigingen aan pom.xml.</span><span class="sxs-lookup"><span data-stu-id="b521b-165">Save changes to pom.xml.</span></span>
10. <span data-ttu-id="b521b-166">Het JAR-bestand maken.</span><span class="sxs-lookup"><span data-stu-id="b521b-166">Create the .jar file.</span></span> <span data-ttu-id="b521b-167">IntelliJ IDEA kunt maken van de JAR als een artefact van een project.</span><span class="sxs-lookup"><span data-stu-id="b521b-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="b521b-168">De volgende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b521b-168">Perform the following steps.</span></span>
    
    1. <span data-ttu-id="b521b-169">Van de **bestand** menu, klikt u op **projectstructuur**.</span><span class="sxs-lookup"><span data-stu-id="b521b-169">From the **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="b521b-170">In de **projectstructuur** in het dialoogvenster, klikt u op **artefacten** en klik vervolgens op het plusteken.</span><span class="sxs-lookup"><span data-stu-id="b521b-170">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="b521b-171">Klik in het pop-updialoogvenster op **JAR**, en klik vervolgens op **van modules met afhankelijkheden**.</span><span class="sxs-lookup"><span data-stu-id="b521b-171">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![JAR maken](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="b521b-173">In de **maken JAR van Modules** dialoogvenster vak, klikt u op het weglatingsteken (![weglatingsteken](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) op basis van de **Main klasse**.</span><span class="sxs-lookup"><span data-stu-id="b521b-173">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against the **Main Class**.</span></span>
    4. <span data-ttu-id="b521b-174">In de **Main-klasse selecteren** dialoogvenster vak, selecteer de klasse die standaard wordt weergegeven en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b521b-174">In the **Select Main Class** dialog box, select the class that appears by default and then click **OK**.</span></span>
       
        ![JAR maken](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="b521b-176">In de **maken JAR van Modules** dialoogvenster vak, zorg ervoor dat de optie voor het **uitpakken naar het doel JAR** is geselecteerd en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b521b-176">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="b521b-177">Hiermee maakt u een één JAR met alle afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="b521b-177">This creates a single JAR with all dependencies.</span></span>
       
        ![JAR maken](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="b521b-179">Het tabblad van de indeling uitvoer geeft een lijst van alle potten die opgenomen als onderdeel van het Maven-project zijn.</span><span class="sxs-lookup"><span data-stu-id="b521b-179">The output layout tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="b521b-180">U kunt selecteren en het verwijderen van ongewenste waarop de toepassing Scala heeft geen directe afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="b521b-180">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="b521b-181">Voor de toepassing hier maakt, kunt u alles behalve het laatste bestand (**SparkSimpleApp compileren uitvoer**).</span><span class="sxs-lookup"><span data-stu-id="b521b-181">For the application we are creating here, you can remove all but the last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="b521b-182">Selecteer de potten om te verwijderen en klik vervolgens op de **verwijderen** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b521b-182">Select the jars to delete and then click the **Delete** icon.</span></span>
       
        ![JAR maken](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="b521b-184">Zorg ervoor dat **bouwen op Controleer** selectievakje is ingeschakeld, die zorgt ervoor dat de jar wordt gemaakt telkens wanneer het project wordt gemaakt of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="b521b-184">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="b521b-185">Klik op **toepassen** en vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="b521b-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="b521b-186">Klik in de menubalk op **bouwen**, en klik vervolgens op **Project maken**.</span><span class="sxs-lookup"><span data-stu-id="b521b-186">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="b521b-187">U kunt ook klikken op **bouwen artefacten** voor het maken van de jar.</span><span class="sxs-lookup"><span data-stu-id="b521b-187">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="b521b-188">De uitvoer jar wordt gemaakt onder **\out\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="b521b-188">The output jar is created under **\out\artifacts**.</span></span>
       
        ![JAR maken](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-the-application-on-the-spark-cluster"></a><span data-ttu-id="b521b-190">De toepassing uitvoert op het Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="b521b-190">Run the application on the Spark cluster</span></span>
<span data-ttu-id="b521b-191">De toepassing op het cluster uitgevoerd, moet u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="b521b-191">To run the application on the cluster, you must do the following:</span></span>

* <span data-ttu-id="b521b-192">**De toepassing jar kopiëren naar de Azure storage-blob** die zijn gekoppeld aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="b521b-192">**Copy the application jar to the Azure storage blob** associated with the cluster.</span></span> <span data-ttu-id="b521b-193">U kunt [ **AzCopy**](../storage/common/storage-use-azcopy.md), een opdrachtregelprogramma, om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="b521b-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="b521b-194">Er zijn veel andere clients ook die u kunt gebruiken om gegevens te uploaden.</span><span class="sxs-lookup"><span data-stu-id="b521b-194">There are a lot of other clients as well that you can use to upload data.</span></span> <span data-ttu-id="b521b-195">U vindt meer informatie hierover op [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="b521b-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="b521b-196">**Livy gebruiken voor het verzenden van de taak van een toepassing op afstand** aan het Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="b521b-196">**Use Livy to submit an application job remotely** to the Spark cluster.</span></span> <span data-ttu-id="b521b-197">Spark-clusters in HDInsight omvat Livy die beschrijft de REST-eindpunten om op afstand Spark-taken verzenden.</span><span class="sxs-lookup"><span data-stu-id="b521b-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints to remotely submit Spark jobs.</span></span> <span data-ttu-id="b521b-198">Zie voor meer informatie [Spark verzenden van taken op afstand met behulp van Livy met Spark-clusters in HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="b521b-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="b521b-199">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="b521b-199">Next step</span></span>

<span data-ttu-id="b521b-200">In dit artikel hebt u geleerd hoe u een Spark scala-toepassing maakt.</span><span class="sxs-lookup"><span data-stu-id="b521b-200">In this article you learned how to create a Spark scala application.</span></span> <span data-ttu-id="b521b-201">Ga naar het volgende artikel voor meer informatie over het uitvoeren van deze toepassing op een HDInsight Spark-cluster met behulp van Livy.</span><span class="sxs-lookup"><span data-stu-id="b521b-201">Advance to the next article to learn how to run this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="b521b-202">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="b521b-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)


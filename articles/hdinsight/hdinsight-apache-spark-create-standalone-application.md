---
title: aaaCreate Scala app toorun op Spark-clusters - Azure HDInsight | Microsoft Docs
description: Maak een toepassing Spark is geschreven in Scala met Apache Maven zoals Hallo systeem en een bestaande Maven archetype voor Scala geleverd door IntelliJ IDEA opbouwen.
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
ms.openlocfilehash: b25291b60921021486f55d78b4832a070a54d163
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="06f16-103">Maken van een toepassing Scala Maven toorun op Apache Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="06f16-103">Create a Scala Maven application toorun on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="06f16-104">Meer informatie over hoe een Spark-toepassing die is geschreven in Scala met behulp van Maven met IntelliJ IDEA toocreate.</span><span class="sxs-lookup"><span data-stu-id="06f16-104">Learn how toocreate a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="06f16-105">Hallo artikel gebruikt Apache Maven Hallo systeem bouwen en begint met een bestaande Maven archetype voor Scala geleverd door IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="06f16-105">hello article uses Apache Maven as hello build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="06f16-106">Maken van een toepassing Scala in IntelliJ IDEA omvat Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="06f16-106">Creating a Scala application in IntelliJ IDEA involves hello following steps:</span></span>

* <span data-ttu-id="06f16-107">Maven gebruiken als Hallo build-systeem.</span><span class="sxs-lookup"><span data-stu-id="06f16-107">Use Maven as hello build system.</span></span>
* <span data-ttu-id="06f16-108">Project Object Model (POM) tooresolve Spark module bestandsafhankelijkheden bijwerken.</span><span class="sxs-lookup"><span data-stu-id="06f16-108">Update Project Object Model (POM) file tooresolve Spark module dependencies.</span></span>
* <span data-ttu-id="06f16-109">Uw toepassing worden geschreven in Scala.</span><span class="sxs-lookup"><span data-stu-id="06f16-109">Write your application in Scala.</span></span>
* <span data-ttu-id="06f16-110">Genereert een jar-bestand dat verzonden tooHDInsight Spark-clusters worden kan.</span><span class="sxs-lookup"><span data-stu-id="06f16-110">Generate a jar file that can be submitted tooHDInsight Spark clusters.</span></span>
* <span data-ttu-id="06f16-111">Hallo-toepassing uitvoeren in Spark-cluster met behulp van Livy.</span><span class="sxs-lookup"><span data-stu-id="06f16-111">Run hello application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="06f16-112">HDInsight biedt ook een IntelliJ IDEA invoegtoepassing hulpprogramma tooease Hallo proces van het maken en verzenden van toepassingen tooan HDInsight Spark-cluster op Linux.</span><span class="sxs-lookup"><span data-stu-id="06f16-112">HDInsight also provides an IntelliJ IDEA plugin tool tooease hello process of creating and submitting applications tooan HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="06f16-113">Zie voor meer informatie [gebruik de invoegtoepassing HDInsight Tools for IntelliJ IDEA toocreate en het verzenden van Spark scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="06f16-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="06f16-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="06f16-114">Prerequisites</span></span>

* <span data-ttu-id="06f16-115">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="06f16-115">An Azure subscription.</span></span> <span data-ttu-id="06f16-116">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="06f16-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="06f16-117">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="06f16-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="06f16-118">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="06f16-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="06f16-119">Oracle Java Development kit.</span><span class="sxs-lookup"><span data-stu-id="06f16-119">Oracle Java Development kit.</span></span> <span data-ttu-id="06f16-120">Kunt u het installeren van [hier](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="06f16-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="06f16-121">Een Java IDE.</span><span class="sxs-lookup"><span data-stu-id="06f16-121">A Java IDE.</span></span> <span data-ttu-id="06f16-122">Dit artikel wordt IntelliJ IDEA 15.0.1 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="06f16-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="06f16-123">Kunt u het installeren van [hier](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="06f16-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="06f16-124">Scala-invoegtoepassing voor IntelliJ IDEA installeren</span><span class="sxs-lookup"><span data-stu-id="06f16-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="06f16-125">Als IntelliJ IDEA installatie niet niet gevraagd voor het inschakelen van Scala-invoegtoepassing, IntelliJ IDEA starten en te volgen stappen tooinstall Hallo invoegtoepassing Hallo doorlopen:</span><span class="sxs-lookup"><span data-stu-id="06f16-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through hello following steps tooinstall hello plugin:</span></span>

1. <span data-ttu-id="06f16-126">IntelliJ IDEA Start en klik in het welkomstscherm op **configureren** en klik vervolgens op **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="06f16-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![Scala invoegtoepassing inschakelen](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="06f16-128">Klik in het volgende scherm hello, op **JetBrains installeren invoegtoepassing** van linkerbenedenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="06f16-128">In hello next screen, click **Install JetBrains plugin** from hello lower left corner.</span></span> <span data-ttu-id="06f16-129">In Hallo **JetBrains Plugins Bladeren** dialoogvenster dat wordt geopend, Scala zoeken en klik vervolgens op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="06f16-129">In hello **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![Scala-invoegtoepassing installeren](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="06f16-131">Nadat het Hallo-invoegtoepassing is geïnstalleerd, klikt u op Hallo **opnieuw IntelliJ IDEA knop** toorestart Hallo IDE.</span><span class="sxs-lookup"><span data-stu-id="06f16-131">After hello plugin installs successfully, click hello **Restart IntelliJ IDEA button** toorestart hello IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="06f16-132">Een zelfstandige Scala-project maken</span><span class="sxs-lookup"><span data-stu-id="06f16-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="06f16-133">IntelliJ IDEA Start en een nieuw project maken.</span><span class="sxs-lookup"><span data-stu-id="06f16-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="06f16-134">Controleer in Hallo het dialoogvenster new project, Hallo volgende keuzes en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="06f16-134">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>
   
    ![Maven-project maken](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="06f16-136">Selecteer **Maven** als Hallo projecttype.</span><span class="sxs-lookup"><span data-stu-id="06f16-136">Select **Maven** as hello project type.</span></span>
   * <span data-ttu-id="06f16-137">Geef een **Project SDK**.</span><span class="sxs-lookup"><span data-stu-id="06f16-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="06f16-138">Klik op Nieuw en navigeer toohello Java-installatiemap, meestal `C:\Program Files\Java\jdk1.8.0_66`.</span><span class="sxs-lookup"><span data-stu-id="06f16-138">Click New and navigate toohello Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="06f16-139">Selecteer Hallo **maken van archetype** optie.</span><span class="sxs-lookup"><span data-stu-id="06f16-139">Select hello **Create from archetype** option.</span></span>
   * <span data-ttu-id="06f16-140">Selecteer in de lijst Hallo van archetypes, **org.scala tools.archetypes:scala-archetype eenvoudige**.</span><span class="sxs-lookup"><span data-stu-id="06f16-140">From hello list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="06f16-141">Hiermee wordt de juiste mapstructuur Hallo en Hallo vereist afhankelijkheden toowrite Scala standaardprogramma voor downloaden.</span><span class="sxs-lookup"><span data-stu-id="06f16-141">This will create hello right directory structure and download hello required default dependencies toowrite Scala program.</span></span>
2. <span data-ttu-id="06f16-142">Relevante waarden opgeven voor **GroupId**, **artefact-id**, en **versie**.</span><span class="sxs-lookup"><span data-stu-id="06f16-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="06f16-143">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="06f16-143">Click **Next**.</span></span>
3. <span data-ttu-id="06f16-144">Accepteer de standaardwaarden Hallo Hallo volgende in het dialoogvenster waarin u Maven-basismap en andere instellingen voor gebruikers opgeven, en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="06f16-144">In hello next dialog box, where you specify Maven home directory and other user settings, accept hello defaults and click **Next**.</span></span>
4. <span data-ttu-id="06f16-145">Geef een naam en locatie Hallo laatste in het dialoogvenster en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="06f16-145">In hello last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="06f16-146">Hallo verwijderen **MySpec.Scala** op het bestand **src\test\scala\com\microsoft\spark\example**.</span><span class="sxs-lookup"><span data-stu-id="06f16-146">Delete hello **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="06f16-147">U hoeft niet dit voor de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="06f16-147">You do not need this for hello application.</span></span>
6. <span data-ttu-id="06f16-148">Indien nodig, wijzig de naam Hallo standaard bron- en -bestanden.</span><span class="sxs-lookup"><span data-stu-id="06f16-148">If required, rename hello default source and test files.</span></span> <span data-ttu-id="06f16-149">Ga te vanuit het linkerdeelvenster Hallo in Hallo IntelliJ IDEA**src\main\scala\com.microsoft.spark.example**.</span><span class="sxs-lookup"><span data-stu-id="06f16-149">From hello left pane in hello IntelliJ IDEA, navigate too**src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="06f16-150">Met de rechtermuisknop op **App.scala**, klikt u op **opsplitsen**, bestandsnaam wijzigen, klikt u op en geef in het dialoogvenster hello, Hallo nieuwe naam voor de toepassing hello en klik op **opsplitsen**.</span><span class="sxs-lookup"><span data-stu-id="06f16-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in hello dialog box, provide hello new name for hello application and then click **Refactor**.</span></span>
   
    ![De naam van bestanden](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="06f16-152">In latere stappen Hallo wordt Hallo pom.xml toodefine Hallo afhankelijkheden voor Hallo Spark Scala-toepassing bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="06f16-152">In hello subsequent steps, you will update hello pom.xml toodefine hello dependencies for hello Spark Scala application.</span></span> <span data-ttu-id="06f16-153">Voor deze afhankelijkheden toobe gedownload en automatisch opgelost dat moet u Maven dienovereenkomstig configureren.</span><span class="sxs-lookup"><span data-stu-id="06f16-153">For those dependencies toobe downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![Maven configureren voor automatische downloads](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="06f16-155">Van Hallo **bestand** menu, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="06f16-155">From hello **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="06f16-156">In Hallo **instellingen** dialoogvenster Ga te**bouwen, kan worden uitgevoerd, implementatie** > **Build Tools** > **Maven**  >  **Importeren**.</span><span class="sxs-lookup"><span data-stu-id="06f16-156">In hello **Settings** dialog box, navigate too**Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="06f16-157">Hallo-optie te selecteren**Import Maven projects automatisch**.</span><span class="sxs-lookup"><span data-stu-id="06f16-157">Select hello option too**Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="06f16-158">Klik op **toepassen**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="06f16-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="06f16-159">Hallo Scala bron bestand tooinclude uw toepassingscode bijwerken.</span><span class="sxs-lookup"><span data-stu-id="06f16-159">Update hello Scala source file tooinclude your application code.</span></span> <span data-ttu-id="06f16-160">Open en vervang bestaande voorbeeldcode met de volgende code Hallo Hallo en Hallo wijzigingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="06f16-160">Open and replace hello existing sample code with hello following code and save hello changes.</span></span> <span data-ttu-id="06f16-161">Deze code Hallo gegevens leest uit Hallo HVAC.csv (beschikbaar op alle HDInsight Spark-clusters), haalt Hallo rijen met slechts één cijfer in Hallo zesde kolom en schrijft Hallo uitvoer te**/HVACOut** onder Hallo standaard opslag container voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="06f16-161">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello sixth column, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO toowasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows which have only one digit in hello 7th column in hello CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. <span data-ttu-id="06f16-162">Hallo pom.xml bijwerken.</span><span class="sxs-lookup"><span data-stu-id="06f16-162">Update hello pom.xml.</span></span>
   
   1. <span data-ttu-id="06f16-163">Binnen `<project>\<properties>` Hallo volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="06f16-163">Within `<project>\<properties>` add hello following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="06f16-164">Binnen `<project>\<dependencies>` Hallo volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="06f16-164">Within `<project>\<dependencies>` add hello following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="06f16-165">Sla de wijzigingen toopom.xml.</span><span class="sxs-lookup"><span data-stu-id="06f16-165">Save changes toopom.xml.</span></span>
10. <span data-ttu-id="06f16-166">Hallo JAR-bestand maken.</span><span class="sxs-lookup"><span data-stu-id="06f16-166">Create hello .jar file.</span></span> <span data-ttu-id="06f16-167">IntelliJ IDEA kunt maken van de JAR als een artefact van een project.</span><span class="sxs-lookup"><span data-stu-id="06f16-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="06f16-168">Hallo stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="06f16-168">Perform hello following steps.</span></span>
    
    1. <span data-ttu-id="06f16-169">Van Hallo **bestand** menu, klikt u op **projectstructuur**.</span><span class="sxs-lookup"><span data-stu-id="06f16-169">From hello **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="06f16-170">In Hallo **projectstructuur** in het dialoogvenster, klikt u op **artefacten** en klik vervolgens op Hallo plus symbool.</span><span class="sxs-lookup"><span data-stu-id="06f16-170">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="06f16-171">Klik in het pop-updialoogvenster hello, op **JAR**, en klik vervolgens op **van modules met afhankelijkheden**.</span><span class="sxs-lookup"><span data-stu-id="06f16-171">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![JAR maken](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="06f16-173">In Hallo **maken JAR van Modules** dialoogvenster vak, klikt u op Hallo weglatingsteken (![weglatingsteken](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) tegen Hallo **Main klasse**.</span><span class="sxs-lookup"><span data-stu-id="06f16-173">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against hello **Main Class**.</span></span>
    4. <span data-ttu-id="06f16-174">In Hallo **Main-klasse selecteren** in het dialoogvenster, selecteer Hallo-klasse die wordt standaard weergegeven en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="06f16-174">In hello **Select Main Class** dialog box, select hello class that appears by default and then click **OK**.</span></span>
       
        ![JAR maken](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="06f16-176">In Hallo **maken JAR van Modules** dialoogvenster zorg die optie hello te**toohello doel JAR extraheren** is geselecteerd en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="06f16-176">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="06f16-177">Hiermee maakt u een één JAR met alle afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="06f16-177">This creates a single JAR with all dependencies.</span></span>
       
        ![JAR maken](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="06f16-179">Hallo uitvoer indeling tabblad bevat alle Hallo potten die opgenomen als onderdeel van Hallo Maven-project zijn.</span><span class="sxs-lookup"><span data-stu-id="06f16-179">hello output layout tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="06f16-180">U kunt selecteren en delete Hallo toepassingsgroepen waarop Scala toepassing hello heeft geen directe afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="06f16-180">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="06f16-181">Voor de toepassing hello hier maakt, kunt u alle maar Hallo laatste (**SparkSimpleApp compileren uitvoer**).</span><span class="sxs-lookup"><span data-stu-id="06f16-181">For hello application we are creating here, you can remove all but hello last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="06f16-182">Hallo potten toodelete selecteren en klik vervolgens op Hallo **verwijderen** pictogram.</span><span class="sxs-lookup"><span data-stu-id="06f16-182">Select hello jars toodelete and then click hello **Delete** icon.</span></span>
       
        ![JAR maken](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="06f16-184">Zorg ervoor dat **bouwen op Controleer** selectievakje is ingeschakeld, waardoor wordt gegarandeerd dat jar hello wordt gemaakt telkens wanneer Hallo-project wordt gemaakt of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="06f16-184">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="06f16-185">Klik op **toepassen** en vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="06f16-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="06f16-186">In de menubalk hello, klikt u op **bouwen**, en klik vervolgens op **Project maken**.</span><span class="sxs-lookup"><span data-stu-id="06f16-186">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="06f16-187">U kunt ook klikken op **bouwen artefacten** toocreate Hallo jar.</span><span class="sxs-lookup"><span data-stu-id="06f16-187">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="06f16-188">Hallo uitvoer jar gemaakt onder **\out\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="06f16-188">hello output jar is created under **\out\artifacts**.</span></span>
       
        ![JAR maken](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a><span data-ttu-id="06f16-190">Hallo-toepassing uitvoeren op Hallo Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="06f16-190">Run hello application on hello Spark cluster</span></span>
<span data-ttu-id="06f16-191">toorun hello toepassing op Hallo-cluster, moet u doen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="06f16-191">toorun hello application on hello cluster, you must do hello following:</span></span>

* <span data-ttu-id="06f16-192">**Kopiëren Hallo toepassing jar toohello Azure storage-blob** die zijn gekoppeld aan het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="06f16-192">**Copy hello application jar toohello Azure storage blob** associated with hello cluster.</span></span> <span data-ttu-id="06f16-193">U kunt [ **AzCopy**](../storage/common/storage-use-azcopy.md), een opdracht hulpprogramma toodo dus regel.</span><span class="sxs-lookup"><span data-stu-id="06f16-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="06f16-194">Er zijn veel andere clients ook dat u tooupload gegevens kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="06f16-194">There are a lot of other clients as well that you can use tooupload data.</span></span> <span data-ttu-id="06f16-195">U vindt meer informatie hierover op [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="06f16-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="06f16-196">**Livy toosubmit een taak van toepassing op afstand gebruiken** toohello Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="06f16-196">**Use Livy toosubmit an application job remotely** toohello Spark cluster.</span></span> <span data-ttu-id="06f16-197">Spark-clusters in HDInsight omvat Livy die beschrijft de REST-eindpunten tooremotely indienen Spark-taken.</span><span class="sxs-lookup"><span data-stu-id="06f16-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints tooremotely submit Spark jobs.</span></span> <span data-ttu-id="06f16-198">Zie voor meer informatie [Spark verzenden van taken op afstand met behulp van Livy met Spark-clusters in HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="06f16-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="06f16-199">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="06f16-199">Next step</span></span>

<span data-ttu-id="06f16-200">In dit artikel u leert hoe toocreate een Spark scala-toepassing.</span><span class="sxs-lookup"><span data-stu-id="06f16-200">In this article you learned how toocreate a Spark scala application.</span></span> <span data-ttu-id="06f16-201">Geavanceerde toohello volgende artikel toolearn hoe toorun deze toepassing op een HDInsight Spark-cluster met behulp van Livy.</span><span class="sxs-lookup"><span data-stu-id="06f16-201">Advance toohello next article toolearn how toorun this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="06f16-202">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="06f16-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)


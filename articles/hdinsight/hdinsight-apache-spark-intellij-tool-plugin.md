---
title: 'Azure Toolkit voor IntelliJ: Spark toepassingen maken voor een HDInsight-cluster | Microsoft Docs'
description: Hello Azure Toolkit gebruiken voor Spark scala-toepassingen voor IntelliJ toodevelop is geschreven in Scala en verzend deze tooan HDInsight Spark-cluster.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="cf9c0-103">Gebruik Azure Toolkit voor IntelliJ toocreate Spark scala-toepassingen voor een HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="cf9c0-103">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="cf9c0-104">Gebruik hello Azure Toolkit voor IntelliJ invoegtoepassing toodevelop Spark toepassingen geschreven in Scala en deze vervolgens verzenden tooan HDInsight Spark-cluster rechtstreeks vanuit Hallo IntelliJ integrated development environment (IDE).</span><span class="sxs-lookup"><span data-stu-id="cf9c0-104">Use hello Azure Toolkit for IntelliJ plug-in toodevelop Spark applications written in Scala, and then submit them tooan HDInsight Spark cluster directly from hello IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="cf9c0-105">U kunt Hallo invoegtoepassing in een aantal manieren gebruiken:</span><span class="sxs-lookup"><span data-stu-id="cf9c0-105">You can use hello plug-in in a few ways:</span></span>

* <span data-ttu-id="cf9c0-106">Ontwikkelen en het verzenden van een Scala Spark-toepassing op een HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="cf9c0-107">Toegang tot de bronnen van uw Azure HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="cf9c0-108">Ontwikkelen en een Scala Spark-toepassing lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="cf9c0-109">toocreate van uw project, weergave Hallo [Spark scala-toepassingen maken met hello Azure Toolkit voor IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-109">toocreate your project, view hello [Create Spark Applications with hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf9c0-110">U kunt deze invoegtoepassing toocreate gebruiken en verzenden van toepassingen alleen voor een HDInsight Spark-cluster op Linux.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-110">You can use this plug-in toocreate and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="cf9c0-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cf9c0-111">Prerequisites</span></span>

- <span data-ttu-id="cf9c0-112">Een Apache Spark-cluster in HDInsight Linux.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="cf9c0-113">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="cf9c0-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="cf9c0-114">Oracle Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="cf9c0-115">U kunt deze installeren via Hallo [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="cf9c0-115">You can install it from hello [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="cf9c0-116">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-116">IntelliJ IDEA.</span></span> <span data-ttu-id="cf9c0-117">In dit artikel gebruikt versie 2017.1.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-117">This article uses version 2017.1.</span></span> <span data-ttu-id="cf9c0-118">U kunt deze installeren via Hallo [JetBrains website](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="cf9c0-118">You can install it from hello [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="cf9c0-119">Azure Toolkit voor IntelliJ installeren</span><span class="sxs-lookup"><span data-stu-id="cf9c0-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="cf9c0-120">Zie voor installatie-instructies [Azure Toolkit installeren voor IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="cf9c0-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-tooyour-azure-subscription"></a><span data-ttu-id="cf9c0-121">Meld u aan tooyour Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="cf9c0-121">Sign in tooyour Azure subscription</span></span>

1. <span data-ttu-id="cf9c0-122">Hallo IntelliJ IDE Start en Azure Explorer te openen.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-122">Start hello IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="cf9c0-123">Op Hallo **weergave** selecteert u **hulpprogramma Windows**, en selecteer vervolgens **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-123">On hello **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![Hello Azure Explorer-koppeling](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="cf9c0-125">Klik met de rechtermuisknop Hallo **Azure** knooppunt en selecteer vervolgens **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-125">Right-click hello **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="cf9c0-126">In Hallo **Azure aanmelden** dialoogvenster, **aanmelden**, en voer uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-126">In hello **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![Hello Azure teken in het dialoogvenster](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="cf9c0-128">Nadat u bent aangemeld, Hallo **Selecteer abonnementen** dialoogvenster lijsten alle Azure-abonnementen die zijn gekoppeld aan Hallo Hallo referenties.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-128">After you're signed in, hello **Select Subscriptions** dialog box lists all hello Azure subscriptions that are associated with hello credentials.</span></span> <span data-ttu-id="cf9c0-129">Selecteer Hallo **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-129">Select hello **Select** button.</span></span>

    ![dialoogvenster Hallo-abonnementen selecteren](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="cf9c0-131">Op Hallo **Azure Explorer** tabblad uit, vouw **HDInsight** tooview-Hallo HDInsight Spark-clusters die zich in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-131">On hello **Azure Explorer** tab, expand **HDInsight** tooview hello HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![HDInsight Spark-clusters in Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="cf9c0-133">tooview hello resources (bijvoorbeeld opslagaccounts) die gekoppeld aan cluster hello zijn, u kunt een naam van de cluster-knooppunt verder uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-133">tooview hello resources (for example, storage accounts) that are associated with hello cluster, you can further expand a cluster-name node.</span></span>
   
    ![Een uitgebreide naam van de cluster-knooppunt](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="cf9c0-135">Een Spark Scala-toepassing uitvoeren op een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="cf9c0-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="cf9c0-136">Start IntelliJ IDEA en maak vervolgens een project.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="cf9c0-137">In Hallo **nieuw Project** dialoogvenster vak, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="cf9c0-137">In hello **New Project** dialog box, do hello following:</span></span> 

   <span data-ttu-id="cf9c0-138">a.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-138">a.</span></span> <span data-ttu-id="cf9c0-139">Selecteer **HDInsight** > **Spark in HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="cf9c0-140">b.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-140">b.</span></span> <span data-ttu-id="cf9c0-141">In Hallo **Build hulpprogramma** lijst, selecteert u Hallo te volgen, op basis van tooyour nodig:</span><span class="sxs-lookup"><span data-stu-id="cf9c0-141">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="cf9c0-142">**Maven**, voor ondersteuning van de wizard Scala project maken</span><span class="sxs-lookup"><span data-stu-id="cf9c0-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="cf9c0-143">**SBT**, voor het beheren van Hallo afhankelijkheden en bouwen voor Hallo Scala project</span><span class="sxs-lookup"><span data-stu-id="cf9c0-143">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![het dialoogvenster Nieuw Project Hallo](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="cf9c0-145">Selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-145">Select **Next**.</span></span>

3. <span data-ttu-id="cf9c0-146">Hallo Scala maken van het project wizard detecteert automatisch of u Hallo Scala invoegtoepassing hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-146">hello Scala project-creation wizard automatically detects whether you've installed hello Scala plug-in.</span></span> <span data-ttu-id="cf9c0-147">Selecteer **installeren**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-147">Select **Install**.</span></span>

   ![Controle van de invoegtoepassing scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="cf9c0-149">toodownload hello Scala invoegtoepassing, selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-149">toodownload hello Scala plug-in, select **OK**.</span></span> <span data-ttu-id="cf9c0-150">Ga als volgt Hallo instructies toorestart IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-150">Follow hello instructions toorestart IntelliJ.</span></span> 

   ![Hallo Scala invoegtoepassing installatievenster](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="cf9c0-152">In Hallo **nieuw Project** venster Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="cf9c0-152">In hello **New Project** window, do hello following:</span></span>  

    ![Hallo Spark SDK selecteren](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="cf9c0-154">a.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-154">a.</span></span> <span data-ttu-id="cf9c0-155">Voer een naam en locatie.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-155">Enter a project name and location.</span></span>

   <span data-ttu-id="cf9c0-156">b.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-156">b.</span></span> <span data-ttu-id="cf9c0-157">In Hallo **Project SDK** vervolgkeuzelijst, selecteer **Java 1.8** voor Hallo Spark 2.x-cluster, of selecteer **Java 1.7** voor Hallo Spark 1.x-cluster.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-157">In hello **Project SDK** drop-down list, select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span>

   <span data-ttu-id="cf9c0-158">c.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-158">c.</span></span> <span data-ttu-id="cf9c0-159">In Hallo **Spark versie** vervolgkeuzelijst, wizard voor het maken van project Scala integreert de juiste versie Hallo voor Spark SDK en Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-159">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="cf9c0-160">Als Hallo Spark-cluster versie ouder dan 2.0 is, selecteert u **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-160">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="cf9c0-161">Selecteer anders **Spark2.x**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="cf9c0-162">In dit voorbeeld wordt **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="cf9c0-163">Selecteer **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-163">Select **Finish**.</span></span>

7. <span data-ttu-id="cf9c0-164">een artefact Hallo Spark project automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-164">hello Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="cf9c0-165">tooview hello artefacten, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="cf9c0-165">tooview hello artifact, do hello following:</span></span>

   <span data-ttu-id="cf9c0-166">a.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-166">a.</span></span> <span data-ttu-id="cf9c0-167">Op Hallo **bestand** selecteert u **projectstructuur**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-167">On hello **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="cf9c0-168">b.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-168">b.</span></span> <span data-ttu-id="cf9c0-169">In Hallo **projectstructuur** dialoogvenster, **artefacten** tooview Hallo standaard artefacten die wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-169">In hello **Project Structure** dialog box, select **Artifacts** tooview hello default artifact that is created.</span></span> <span data-ttu-id="cf9c0-170">U kunt ook uw eigen artefacten maken door het selecteren van Hallo plus -teken (**+**).</span><span class="sxs-lookup"><span data-stu-id="cf9c0-170">You can also create your own artifact by selecting hello plus sign (**+**).</span></span>

      ![Gegevens in het dialoogvenster Hallo artefact](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="cf9c0-172">De broncode van uw toepassing toevoegen door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="cf9c0-172">Add your application source code by doing hello following:</span></span>

   <span data-ttu-id="cf9c0-173">a.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-173">a.</span></span> <span data-ttu-id="cf9c0-174">In Projectverkenner met de rechtermuisknop op **src**, wijst u te**nieuw**, en selecteer vervolgens **Scala klasse**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-174">In Project Explorer, right-click **src**, point too**New**, and then select **Scala Class**.</span></span>
      
      ![Opdrachten voor het maken van een klasse Scala van Projectverkenner](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="cf9c0-176">b.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-176">b.</span></span> <span data-ttu-id="cf9c0-177">In Hallo **nieuwe Scala klasse maken** dialoogvenster vak, Geef een naam op, selecteer **Object** in Hallo **soort** vak en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-177">In hello **Create New Scala Class** dialog box, provide a name, select **Object** in hello **Kind** box, and then select **OK**.</span></span>
      
      ![Dialoogvenster Nieuwe Scala klasse maken](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="cf9c0-179">c.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-179">c.</span></span> <span data-ttu-id="cf9c0-180">In Hallo **MyClusterApp.scala** bestand, plak Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-180">In hello **MyClusterApp.scala** file, paste hello following code.</span></span> <span data-ttu-id="cf9c0-181">Hallo code Hallo gegevens leest uit HVAC.csv (beschikbaar op alle HDInsight Spark-clusters), haalt Hallo rijen met slechts één cijfer in Hallo zevende kolom in Hallo CSV-bestand, en schrijft Hallo uitvoer te**/HVACOut** onder Hallo-standaard Storage-container voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-181">hello code reads hello data from HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that have only one digit in hello seventh column in hello CSV file, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. <span data-ttu-id="cf9c0-182">Hallo-toepassing uitvoeren op een HDInsight Spark-cluster door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="cf9c0-182">Run hello application on an HDInsight Spark cluster by doing hello following:</span></span>

   <span data-ttu-id="cf9c0-183">a.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-183">a.</span></span> <span data-ttu-id="cf9c0-184">In Projectverkenner met de rechtermuisknop op de projectnaam Hallo en selecteer vervolgens **indienen Spark toepassing tooHDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-184">In Project Explorer, right-click hello project name, and then select **Submit Spark Application tooHDInsight**.</span></span>
      
      ![Hallo indienen Spark toepassing tooHDInsight opdracht](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="cf9c0-186">b.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-186">b.</span></span> <span data-ttu-id="cf9c0-187">U na vragen aan gebruiker tooenter zijn de referenties van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-187">You are prompted tooenter your Azure subscription credentials.</span></span> <span data-ttu-id="cf9c0-188">In Hallo **Spark verzending** in het dialoogvenster Hallo volgende waarden bevatten, en selecteer vervolgens **indienen**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-188">In hello **Spark Submission** dialog box, provide hello following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="cf9c0-189">Voor **Spark-clusters (alleen voor Linux)**, selecteer Hallo HDInsight Spark-cluster waarop toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-189">For **Spark clusters (Linux only)**, select hello HDInsight Spark cluster on which you want toorun your application.</span></span>

      * <span data-ttu-id="cf9c0-190">Selecteer een artefact uit Hallo IntelliJ project of Selecteer een van de vaste schijf Hallo.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-190">Select an artifact from hello IntelliJ project, or select one from hello hard drive.</span></span>

      * <span data-ttu-id="cf9c0-191">In Hallo **Main klassenaam** vak, selecteer Hallo weglatingsteken (**...** ), selecteer Hallo hoofdklasse in de broncode van uw toepassing en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-191">In hello **Main class name** box, select hello ellipsis (**...**), select hello main class in your application source code, and then select **OK**.</span></span>

        ![dialoogvenster voor Hallo Main-klasse selecteren](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="cf9c0-193">Omdat de toepassingscode Hallo in dit voorbeeld geen opdrachtregelargumenten vereist of verwijzen naar potten of bestanden, kunt u Hallo resterende selectievakjes leeg laten.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-193">Because hello application code in this example does not require command-line arguments or reference JARs or files, you can leave hello remaining boxes empty.</span></span> <span data-ttu-id="cf9c0-194">Nadat u Hallo informatie te verstrekken, eruit dialoogvenster Hallo Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-194">After you provide all hello information, hello dialog box should resemble hello following image.</span></span>
        
        ![Hallo Spark verzending van het dialoogvenster](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="cf9c0-196">c.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-196">c.</span></span> <span data-ttu-id="cf9c0-197">Hallo **Spark verzending** op Hallo onderaan Hallo venster tabblad moet beginnen met het Hallo de voortgang weergeven.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-197">hello **Spark Submission** tab at hello bottom of hello window should start displaying hello progress.</span></span> <span data-ttu-id="cf9c0-198">U kunt ook Hallo toepassing stoppen Hallo rode knop selecteren in Hallo **Spark verzending** venster.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-198">You can also stop hello application by selecting hello red button in hello **Spark Submission** window.</span></span>
      
      ![Hallo Spark verzending venster](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="cf9c0-200">toolearn hoe tooaccess Hallo taakuitvoer, raadpleegt u Hallo ' toegang en HDInsight Spark-clusters beheren met behulp van Azure Toolkit voor IntelliJ ' verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-200">toolearn how tooaccess hello job output, see hello "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="cf9c0-201">Uitvoeren of fouten opsporen in een Spark Scala-toepassing op een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="cf9c0-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="cf9c0-202">Aangeraden wordt ook een andere manier om Hallo Spark toepassing toohello-cluster in te dienen.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-202">We also recommend another way of submitting hello Spark application toohello cluster.</span></span> <span data-ttu-id="cf9c0-203">U kunt dit doen Hallo parameters door in te stellen Hallo **uitvoeren/Debug configuraties** IDE.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-203">You can do so by setting hello parameters in hello **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="cf9c0-204">Zie voor meer informatie [op afstand fouten opsporen in Spark scala-toepassingen op een HDInsight-cluster in Azure werkset voor IntelliJ via SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="cf9c0-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="cf9c0-205">Toegang tot en HDInsight Spark-clusters beheren met behulp van Azure Toolkit voor IntelliJ</span><span class="sxs-lookup"><span data-stu-id="cf9c0-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="cf9c0-206">U kunt verschillende bewerkingen kunt uitvoeren met behulp van Azure Toolkit voor IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-hello-job-view"></a><span data-ttu-id="cf9c0-207">Toegang Hallo taak weergeven</span><span class="sxs-lookup"><span data-stu-id="cf9c0-207">Access hello job view</span></span>
1. <span data-ttu-id="cf9c0-208">Vouw in Azure Explorer **HDInsight**Hallo Spark clusternaam uitvouwen en selecteer vervolgens **taken**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-208">In Azure Explorer, expand **HDInsight**, expand hello Spark cluster name, and then select **Jobs**.</span></span>  

    ![Taak weergave knooppunt](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="cf9c0-210">Klik in het rechterdeelvenster Hallo Hallo **Spark taak weergeven** tabblad geeft alle Hallo-toepassingen die op het Hallo-cluster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-210">In hello right pane, hello **Spark Job View** tab displays all hello applications that were run on hello cluster.</span></span> <span data-ttu-id="cf9c0-211">Selecteer de naam Hallo van Hallo toepassing waarvoor u toosee meer informatie wenst.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-211">Select hello name of hello application for which you want toosee more details.</span></span>

    ![App-details](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="cf9c0-213">toodisplay actieve taak basisinformatie, houd de muis boven Hallo taakgrafiek.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-213">toodisplay basic running job information, hover over hello job graph.</span></span> <span data-ttu-id="cf9c0-214">Selecteer een knooppunt op Hallo taakgrafiek tooview Hallo fasen grafiek en informatie die u elke taak die wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-214">tooview hello stages graph and information that every job generates, select a node on hello job graph.</span></span>

    ![Fase taakdetails](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="cf9c0-216">veelgebruikte Logboeken, zoals tooview *stuurprogramma Stderr*, *stuurprogramma Stdout*, en *Directory Info*, selecteer Hallo **logboek** tabblad.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-216">tooview frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select hello **Log** tab.</span></span>

    ![Logboekgegevens](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="cf9c0-218">U kunt ook Hallo Spark geschiedenis gebruikersinterface en Hallo gebruikersinterface van YARN (op niveau van de toepassing hello) weergeven door een koppeling Hallo boven aan het Hallo-venster te selecteren.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-218">You can also view hello Spark history UI and hello YARN UI (at hello application level) by selecting a link at hello top of hello window.</span></span>

### <a name="access-hello-spark-history-server"></a><span data-ttu-id="cf9c0-219">Toegang tot Hallo Spark geschiedenis van server</span><span class="sxs-lookup"><span data-stu-id="cf9c0-219">Access hello Spark history server</span></span>
1. <span data-ttu-id="cf9c0-220">Vouw in Azure Explorer **HDInsight**, met de rechtermuisknop op de naam van uw Spark-cluster en selecteer vervolgens **Open Spark geschiedenis UI**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="cf9c0-221">Wanneer u wordt gevraagd, voer de beheerdersreferenties Hallo-cluster, dat u hebt opgegeven bij het instellen van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-221">When you're prompted, enter hello cluster's admin credentials, which you specified when you set up hello cluster.</span></span>

3. <span data-ttu-id="cf9c0-222">Op Hallo Spark geschiedenis serverdashboard kunt u Hallo toepassing naam toolook voor Hallo toepassing dat u zojuist hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-222">On hello Spark history server dashboard, you can use hello application name toolook for hello application that you just finished running.</span></span> <span data-ttu-id="cf9c0-223">In Hallo voorafgaand aan code, stelt u de naam van de toepassing hello met behulp van `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-223">In hello preceding code, you set hello application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="cf9c0-224">De naam van uw toepassing Spark is daarom **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-hello-ambari-portal"></a><span data-ttu-id="cf9c0-225">Hallo Ambari portal starten</span><span class="sxs-lookup"><span data-stu-id="cf9c0-225">Start hello Ambari portal</span></span>
1. <span data-ttu-id="cf9c0-226">Vouw in Azure Explorer **HDInsight**, met de rechtermuisknop op de naam van uw Spark-cluster en selecteer vervolgens **beheerportal Open Cluster (Ambari)**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="cf9c0-227">Wanneer u wordt gevraagd, voert u beheerdersreferenties Hallo voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-227">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="cf9c0-228">U deze referenties hebt opgegeven tijdens het installatieproces Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-228">You specified these credentials during hello cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="cf9c0-229">Azure-abonnementen beheren</span><span class="sxs-lookup"><span data-stu-id="cf9c0-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="cf9c0-230">Azure-Toolkit voor IntelliJ bevat standaard Hallo Spark-clusters van alle uw Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-230">By default, Azure Toolkit for IntelliJ lists hello Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="cf9c0-231">Indien nodig, kunt u opgeven dat u wilt dat tooaccess Hallo-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-231">If necessary, you can specify hello subscriptions that you want tooaccess.</span></span> 

1. <span data-ttu-id="cf9c0-232">Azure Explorer met de rechtermuisknop op Hallo **Azure** de hoofd-knooppunt en selecteer vervolgens **abonnementen beheren**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-232">In Azure Explorer, right-click hello **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="cf9c0-233">Schakel in het dialoogvenster Hallo Hallo selectievakjes volgende toohello abonnementen u niet wilt dat tooaccess en selecteer vervolgens **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-233">In hello dialog box, clear hello check boxes next toohello subscriptions that you don't want tooaccess, and then select **Close**.</span></span> <span data-ttu-id="cf9c0-234">U kunt ook selecteren **Afmelden** als u wilt dat toosign buiten uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-234">You can also select **Sign Out** if you want toosign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="cf9c0-235">Een Spark Scala-toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="cf9c0-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="cf9c0-236">U kunt Azure Toolkit voor IntelliJ toorun Spark Scala-toepassingen lokaal op uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-236">You can use Azure Toolkit for IntelliJ toorun Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="cf9c0-237">Hallo toepassingen meestal niet nodig hebt toegang tot toocluster resources, zoals de storage-containers en u kunt uitvoeren en lokaal te testen.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-237">hello applications usually don't need access toocluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="cf9c0-238">Vereiste</span><span class="sxs-lookup"><span data-stu-id="cf9c0-238">Prerequisite</span></span>
<span data-ttu-id="cf9c0-239">Terwijl u Hallo lokale Spark Scala-toepassingen op een Windows-computer uitvoert, krijgt u mogelijk een uitzondering, zoals wordt beschreven in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="cf9c0-239">While you're running hello local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="cf9c0-240">Hallo uitzondering doet zich voor omdat WinUtils.exe in Windows ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-240">hello exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="cf9c0-241">tooresolve deze fout [downloaden Hallo uitvoerbare](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa locatie zoals **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-241">tooresolve this error, [download hello executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="cf9c0-242">Vervolgens voegt u de omgevingsvariabele Hallo **HADOOP_HOME**, en stelt u Hallo-waarde van variabele hello te**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-242">Then, add hello environment variable **HADOOP_HOME**, and set hello value of hello variable too**C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="cf9c0-243">Een lokale Spark Scala-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="cf9c0-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="cf9c0-244">IntelliJ IDEA Start en een project maken.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="cf9c0-245">In Hallo **nieuw Project** dialoogvenster vak, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="cf9c0-245">In hello **New Project** dialog box, do hello following:</span></span>
   
    <span data-ttu-id="cf9c0-246">a.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-246">a.</span></span> <span data-ttu-id="cf9c0-247">Selecteer **HDInsight** > **Spark in HDInsight lokaal uitvoeren voorbeeld (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="cf9c0-248">b.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-248">b.</span></span> <span data-ttu-id="cf9c0-249">In Hallo **Build hulpprogramma** lijst, selecteert u Hallo te volgen, op basis van tooyour nodig:</span><span class="sxs-lookup"><span data-stu-id="cf9c0-249">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="cf9c0-250">**Maven**, voor ondersteuning van de wizard Scala project maken</span><span class="sxs-lookup"><span data-stu-id="cf9c0-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="cf9c0-251">**SBT**, voor het beheren van Hallo afhankelijkheden en bouwen voor Hallo Scala project</span><span class="sxs-lookup"><span data-stu-id="cf9c0-251">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![het dialoogvenster Nieuw Project Hallo](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="cf9c0-253">Selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="cf9c0-254">In het volgende venster hello, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="cf9c0-254">In hello next window, do hello following:</span></span>
   
    <span data-ttu-id="cf9c0-255">a.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-255">a.</span></span> <span data-ttu-id="cf9c0-256">Voer een naam en locatie.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-256">Enter a project name and location.</span></span>

    <span data-ttu-id="cf9c0-257">b.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-257">b.</span></span> <span data-ttu-id="cf9c0-258">In Hallo **Project SDK** vervolgkeuzelijst, selecteert u een Java-versie die is hoger dan versie 1.7.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-258">In hello **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="cf9c0-259">c.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-259">c.</span></span> <span data-ttu-id="cf9c0-260">In Hallo **Spark versie** vervolgkeuzelijst, de versie van de optie Hallo van Scala dat u wilt dat toouse: Scala 2.11.x voor Spark 2.0 of Scala 2.10.x voor Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-260">In hello **Spark Version** drop-down list, select hello version of Scala that you want toouse: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![het dialoogvenster Nieuw Project Hallo](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="cf9c0-262">Selecteer **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-262">Select **Finish**.</span></span>

6. <span data-ttu-id="cf9c0-263">Hallo-sjabloon wordt toegevoegd een voorbeeldcode (**LogQuery**) onder Hallo **src** map die u lokaal op uw computer uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-263">hello template adds a sample code (**LogQuery**) under hello **src** folder that you can run locally on your computer.</span></span>
   
    ![Locatie van LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="cf9c0-265">Klik met de rechtermuisknop Hallo **LogQuery** toepassing en selecteer vervolgens **uitvoeren 'LogQuery'**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-265">Right-click hello **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="cf9c0-266">Op Hallo **uitvoeren** tabblad Hallo onderin, ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="cf9c0-266">On hello **Run** tab at hello bottom, you see an output like hello following:</span></span>
   
   ![Spark toepassing lokale resultaat van uitgevoerde](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a><span data-ttu-id="cf9c0-268">Bestaande IntelliJ IDEA toepassingen toouse Azure Toolkit voor IntelliJ converteren</span><span class="sxs-lookup"><span data-stu-id="cf9c0-268">Convert existing IntelliJ IDEA applications toouse Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="cf9c0-269">Hallo bestaande Spark Scala-toepassingen die u hebt gemaakt in IntelliJ IDEA toobe compatibel is met de Azure-Toolkit voor IntelliJ kunnen worden geconverteerd.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-269">You can convert hello existing Spark Scala applications that you created in IntelliJ IDEA toobe compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="cf9c0-270">Vervolgens kunt u Hallo invoegtoepassing toosubmit Hallo toepassingen tooan HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-270">You can then use hello plug-in toosubmit hello applications tooan HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="cf9c0-271">Voor een bestaande Spark Scala-toepassing die is gemaakt via IntelliJ IDEA, Hallo gekoppeld .iml bestand te openen.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open hello associated .iml file.</span></span>

2. <span data-ttu-id="cf9c0-272">In de hoofdmap van het Hallo niveau is een **module** element Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="cf9c0-272">At hello root level is a **module** element like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="cf9c0-273">Hallo element tooadd bewerken `UniqueKey="HDInsightTool"` dus die Hallo **module** element ziet eruit als Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="cf9c0-273">Edit hello element tooadd `UniqueKey="HDInsightTool"` so that hello **module** element looks like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="cf9c0-274">Hallo wijzigingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-274">Save hello changes.</span></span> <span data-ttu-id="cf9c0-275">Nu moet uw toepassing compatibel zijn met Azure Toolkit voor IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="cf9c0-276">U kunt dit testen met de rechtermuisknop op de projectnaam Hallo in Projectverkenner.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-276">You can test it by right-clicking hello project name in Project Explorer.</span></span> <span data-ttu-id="cf9c0-277">pop-upmenu Hallo heeft nu Hallo optie **indienen Spark toepassing tooHDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-277">hello pop-up menu now has hello option **Submit Spark Application tooHDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="cf9c0-278">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="cf9c0-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="cf9c0-279">Fout bij lokaal uitvoeren: *gebruik een grotere heapgrootte*</span><span class="sxs-lookup"><span data-stu-id="cf9c0-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="cf9c0-280">Als u een 32-bits Java SDK tijdens de uitvoering van lokale, kunt u in Spark 1.6 Hallo volgende fouten tegenkomen:</span><span class="sxs-lookup"><span data-stu-id="cf9c0-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter hello following errors:</span></span>

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

<span data-ttu-id="cf9c0-281">Deze fouten optreden omdat hello, heap-grootte niet groot genoeg zijn voor Spark toorun is.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-281">These errors happen because hello heap size is not large enough for Spark toorun.</span></span> <span data-ttu-id="cf9c0-282">Spark vereist ten minste 471 MB.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="cf9c0-283">(Zie voor meer informatie [SPARK 12081](https://issues.apache.org/jira/browse/SPARK-12081).) Een eenvoudige oplossing is toouse een 64-bits Java SDK.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is toouse a 64-bit Java SDK.</span></span> <span data-ttu-id="cf9c0-284">U kunt ook Hallo JVM-instellingen in IntelliJ wijzigen door toe te voegen Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="cf9c0-284">You can also change hello JVM settings in IntelliJ by adding hello following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Toe te voegen opties toohello vak 'VM options' IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="cf9c0-286">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="cf9c0-286">FAQ</span></span>
<span data-ttu-id="cf9c0-287">kiest u een toepassing tooAzure Data Lake Store toosubmit **interactief** modus tijdens hello Azure aanmelden.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-287">toosubmit an application tooAzure Data Lake Store, choose **Interactive** mode during hello Azure sign-in process.</span></span> <span data-ttu-id="cf9c0-288">Als u selecteert **automatisch** modus, kunt u een foutmelding krijgt.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-288">If you select **Automated** mode, you can get an error.</span></span>

![interactief aanmelden](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="cf9c0-290">Nu we dit heeft opgelost.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-290">Now, we resolved it.</span></span> <span data-ttu-id="cf9c0-291">U kunt een Azure Data Lake Cluster toosubmit uw toepassing met een methode voor aanmelden.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-291">You can choose an Azure Data Lake Cluster toosubmit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="cf9c0-292">Feedback en bekende problemen</span><span class="sxs-lookup"><span data-stu-id="cf9c0-292">Feedback and known issues</span></span>
<span data-ttu-id="cf9c0-293">Op dit moment wordt bekijken Spark uitvoer rechtstreeks niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="cf9c0-294">Als u suggesties of feedback hebt, of als er problemen optreden wanneer u deze invoegtoepassing gebruikt, een e-mail sturen naar hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="cf9c0-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="cf9c0-295"><a name="seealso"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cf9c0-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="cf9c0-296">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf9c0-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="cf9c0-297">Demo</span><span class="sxs-lookup"><span data-stu-id="cf9c0-297">Demo</span></span>
* <span data-ttu-id="cf9c0-298">Maak Scala project (video): [Spark Scala-toepassingen maken](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="cf9c0-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="cf9c0-299">Foutopsporing op afstand (video): [gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand op HDInsight-Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="cf9c0-299">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="cf9c0-300">Scenario's</span><span class="sxs-lookup"><span data-stu-id="cf9c0-300">Scenarios</span></span>
* [<span data-ttu-id="cf9c0-301">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="cf9c0-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="cf9c0-302">Spark met Machine Learning: Spark in HDInsight tooanalyze bouwen met behulp van HVAC-gegevens temperatuur gebruiken</span><span class="sxs-lookup"><span data-stu-id="cf9c0-302">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="cf9c0-303">Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="cf9c0-303">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="cf9c0-304">Spark-Streaming: Spark in HDInsight toobuild realtime streamingtoepassingen gebruiken</span><span class="sxs-lookup"><span data-stu-id="cf9c0-304">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="cf9c0-305">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf9c0-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="cf9c0-306">Maken en uitvoeren van toepassingen</span><span class="sxs-lookup"><span data-stu-id="cf9c0-306">Creating and running applications</span></span>
* [<span data-ttu-id="cf9c0-307">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="cf9c0-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="cf9c0-308">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="cf9c0-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="cf9c0-309">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="cf9c0-309">Tools and extensions</span></span>
* [<span data-ttu-id="cf9c0-310">Gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand via VPN-verbinding</span><span class="sxs-lookup"><span data-stu-id="cf9c0-310">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="cf9c0-311">Gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand via SSH</span><span class="sxs-lookup"><span data-stu-id="cf9c0-311">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="cf9c0-312">Gebruik van HDInsight Tools voor IntelliJ met Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="cf9c0-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="cf9c0-313">HDInsight-hulpprogramma's gebruiken in Azure Toolkit voor Eclipse toocreate Spark scala-toepassingen</span><span class="sxs-lookup"><span data-stu-id="cf9c0-313">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="cf9c0-314">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf9c0-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="cf9c0-315">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf9c0-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="cf9c0-316">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="cf9c0-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="cf9c0-317">Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="cf9c0-317">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="cf9c0-318">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="cf9c0-318">Managing resources</span></span>
* [<span data-ttu-id="cf9c0-319">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf9c0-319">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="cf9c0-320">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="cf9c0-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)


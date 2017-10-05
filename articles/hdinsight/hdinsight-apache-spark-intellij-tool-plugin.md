---
title: 'Azure Toolkit voor IntelliJ: Spark toepassingen maken voor een HDInsight-cluster | Microsoft Docs'
description: De Azure-werkset voor IntelliJ gebruiken voor het ontwikkelen van Spark scala-toepassingen die zijn geschreven in Scala en deze verzenden naar een HDInsight Spark-cluster.
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
ms.openlocfilehash: 19cb8f436fa4d86f323013a5d4b3b50bf6c80a1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-create-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="1cef9-103">Gebruik van Azure Toolkit voor IntelliJ Spark-toepassingen voor een HDInsight-cluster maken</span><span class="sxs-lookup"><span data-stu-id="1cef9-103">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="1cef9-104">Gebruik de Azure-Toolkit voor IntelliJ-invoegtoepassing voor het ontwikkelen van Spark scala-toepassingen die zijn geschreven in Scala en deze vervolgens verzenden naar een HDInsight Spark-cluster rechtstreeks vanuit de IntelliJ integrated development environment (IDE).</span><span class="sxs-lookup"><span data-stu-id="1cef9-104">Use the Azure Toolkit for IntelliJ plug-in to develop Spark applications written in Scala, and then submit them to an HDInsight Spark cluster directly from the IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="1cef9-105">U kunt de invoegtoepassing gebruiken in een aantal manieren:</span><span class="sxs-lookup"><span data-stu-id="1cef9-105">You can use the plug-in in a few ways:</span></span>

* <span data-ttu-id="1cef9-106">Ontwikkelen en het verzenden van een Scala Spark-toepassing op een HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="1cef9-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="1cef9-107">Toegang tot de bronnen van uw Azure HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="1cef9-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="1cef9-108">Ontwikkelen en een Scala Spark-toepassing lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1cef9-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="1cef9-109">Voor het maken van uw project, geven de [Spark scala-toepassingen maken met de Azure-Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span><span class="sxs-lookup"><span data-stu-id="1cef9-109">To create your project, view the [Create Spark Applications with the Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1cef9-110">U kunt deze invoegtoepassing gebruiken voor het maken en verzenden van toepassingen alleen voor een HDInsight Spark-cluster op Linux.</span><span class="sxs-lookup"><span data-stu-id="1cef9-110">You can use this plug-in to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="1cef9-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1cef9-111">Prerequisites</span></span>

- <span data-ttu-id="1cef9-112">Een Apache Spark-cluster in HDInsight Linux.</span><span class="sxs-lookup"><span data-stu-id="1cef9-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="1cef9-113">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="1cef9-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="1cef9-114">Oracle Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="1cef9-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="1cef9-115">U kunt installeren vanuit de [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="1cef9-115">You can install it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="1cef9-116">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="1cef9-116">IntelliJ IDEA.</span></span> <span data-ttu-id="1cef9-117">In dit artikel gebruikt versie 2017.1.</span><span class="sxs-lookup"><span data-stu-id="1cef9-117">This article uses version 2017.1.</span></span> <span data-ttu-id="1cef9-118">U kunt installeren vanuit de [JetBrains website](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="1cef9-118">You can install it from the [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="1cef9-119">Azure Toolkit voor IntelliJ installeren</span><span class="sxs-lookup"><span data-stu-id="1cef9-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="1cef9-120">Zie voor installatie-instructies [Azure Toolkit installeren voor IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="1cef9-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-to-your-azure-subscription"></a><span data-ttu-id="1cef9-121">Meld u aan bij uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="1cef9-121">Sign in to your Azure subscription</span></span>

1. <span data-ttu-id="1cef9-122">Start de IntelliJ IDE en Azure Explorer te openen.</span><span class="sxs-lookup"><span data-stu-id="1cef9-122">Start the IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="1cef9-123">Op de **weergave** selecteert u **hulpprogramma Windows**, en selecteer vervolgens **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-123">On the **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![De Azure Explorer-koppeling](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="1cef9-125">Met de rechtermuisknop op de **Azure** knooppunt en selecteer vervolgens **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-125">Right-click the **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="1cef9-126">In de **Azure aanmelden** dialoogvenster, **aanmelden**, en voer uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="1cef9-126">In the **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![Het dialoogvenster Azure aanmelden](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="1cef9-128">Nadat u bent aangemeld, de **abonnementen Selecteer** in het dialoogvenster geeft een lijst van alle Azure-abonnementen die gekoppeld aan de referenties zijn.</span><span class="sxs-lookup"><span data-stu-id="1cef9-128">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions that are associated with the credentials.</span></span> <span data-ttu-id="1cef9-129">Selecteer de **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="1cef9-129">Select the **Select** button.</span></span>

    ![Het dialoogvenster abonnementen selecteren](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="1cef9-131">Op de **Azure Explorer** tabblad uit, vouw **HDInsight** om weer te geven van de HDInsight Spark-clusters die zich in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="1cef9-131">On the **Azure Explorer** tab, expand **HDInsight** to view the HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![HDInsight Spark-clusters in Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="1cef9-133">Als u wilt weergeven van de bronnen (bijvoorbeeld opslagaccounts) die gekoppeld aan het cluster zijn, kunt u een naam van de cluster-knooppunt verder uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="1cef9-133">To view the resources (for example, storage accounts) that are associated with the cluster, you can further expand a cluster-name node.</span></span>
   
    ![Een uitgebreide naam van de cluster-knooppunt](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="1cef9-135">Een Spark Scala-toepassing uitvoeren op een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="1cef9-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="1cef9-136">Start IntelliJ IDEA en maak vervolgens een project.</span><span class="sxs-lookup"><span data-stu-id="1cef9-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="1cef9-137">In de **nieuw Project** dialoogvenster de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="1cef9-137">In the **New Project** dialog box, do the following:</span></span> 

   <span data-ttu-id="1cef9-138">a.</span><span class="sxs-lookup"><span data-stu-id="1cef9-138">a.</span></span> <span data-ttu-id="1cef9-139">Selecteer **HDInsight** > **Spark in HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="1cef9-140">b.</span><span class="sxs-lookup"><span data-stu-id="1cef9-140">b.</span></span> <span data-ttu-id="1cef9-141">In de **Build hulpprogramma** , selecteert u een van de volgende, afhankelijk van uw behoeften:</span><span class="sxs-lookup"><span data-stu-id="1cef9-141">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="1cef9-142">**Maven**, voor ondersteuning van de wizard Scala project maken</span><span class="sxs-lookup"><span data-stu-id="1cef9-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="1cef9-143">**SBT**, voor het beheren van de afhankelijkheden en bouwen voor het project Scala</span><span class="sxs-lookup"><span data-stu-id="1cef9-143">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![Het dialoogvenster Nieuw Project](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="1cef9-145">Selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-145">Select **Next**.</span></span>

3. <span data-ttu-id="1cef9-146">Het maken van het project Scala wizard detecteert automatisch of u de invoegtoepassing Scala hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1cef9-146">The Scala project-creation wizard automatically detects whether you've installed the Scala plug-in.</span></span> <span data-ttu-id="1cef9-147">Selecteer **installeren**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-147">Select **Install**.</span></span>

   ![Controle van de invoegtoepassing scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="1cef9-149">Selecteer voor het downloaden van de invoegtoepassing Scala **OK**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-149">To download the Scala plug-in, select **OK**.</span></span> <span data-ttu-id="1cef9-150">Volg de instructies IntelliJ opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="1cef9-150">Follow the instructions to restart IntelliJ.</span></span> 

   ![Het dialoogvenster Scala-invoegtoepassing installeren](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="1cef9-152">In de **nieuw Project** venster de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="1cef9-152">In the **New Project** window, do the following:</span></span>  

    ![De Spark SDK selecteren](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="1cef9-154">a.</span><span class="sxs-lookup"><span data-stu-id="1cef9-154">a.</span></span> <span data-ttu-id="1cef9-155">Voer een naam en locatie.</span><span class="sxs-lookup"><span data-stu-id="1cef9-155">Enter a project name and location.</span></span>

   <span data-ttu-id="1cef9-156">b.</span><span class="sxs-lookup"><span data-stu-id="1cef9-156">b.</span></span> <span data-ttu-id="1cef9-157">In de **Project SDK** vervolgkeuzelijst, selecteer **Java 1.8** voor het Spark-cluster voor 2.x of selecteer **Java 1.7** voor de 1.x Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="1cef9-157">In the **Project SDK** drop-down list, select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span>

   <span data-ttu-id="1cef9-158">c.</span><span class="sxs-lookup"><span data-stu-id="1cef9-158">c.</span></span> <span data-ttu-id="1cef9-159">In de **Spark versie** vervolgkeuzelijst, wizard van Scala project maken voor Spark SDK en Scala SDK de juiste versie kan worden geïntegreerd.</span><span class="sxs-lookup"><span data-stu-id="1cef9-159">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="1cef9-160">Als de Spark-cluster versie ouder dan 2.0 is, selecteert u **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-160">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="1cef9-161">Selecteer anders **Spark2.x**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="1cef9-162">In dit voorbeeld wordt **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="1cef9-163">Selecteer **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-163">Select **Finish**.</span></span>

7. <span data-ttu-id="1cef9-164">Het Spark-project wordt automatisch een artefact voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1cef9-164">The Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="1cef9-165">Als u wilt weergeven van het artefact, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="1cef9-165">To view the artifact, do the following:</span></span>

   <span data-ttu-id="1cef9-166">a.</span><span class="sxs-lookup"><span data-stu-id="1cef9-166">a.</span></span> <span data-ttu-id="1cef9-167">Op de **bestand** selecteert u **projectstructuur**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-167">On the **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="1cef9-168">b.</span><span class="sxs-lookup"><span data-stu-id="1cef9-168">b.</span></span> <span data-ttu-id="1cef9-169">In de **projectstructuur** dialoogvenster, **artefacten** om weer te geven van de standaard-artefacten die is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1cef9-169">In the **Project Structure** dialog box, select **Artifacts** to view the default artifact that is created.</span></span> <span data-ttu-id="1cef9-170">U kunt ook uw eigen artefacten maken door het plusteken (**+**).</span><span class="sxs-lookup"><span data-stu-id="1cef9-170">You can also create your own artifact by selecting the plus sign (**+**).</span></span>

      ![Informatie over de artefacten in het dialoogvenster](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="1cef9-172">De broncode van uw toepassing toevoegen als volgt:</span><span class="sxs-lookup"><span data-stu-id="1cef9-172">Add your application source code by doing the following:</span></span>

   <span data-ttu-id="1cef9-173">a.</span><span class="sxs-lookup"><span data-stu-id="1cef9-173">a.</span></span> <span data-ttu-id="1cef9-174">In Projectverkenner met de rechtermuisknop op **src**, wijs **nieuw**, en selecteer vervolgens **Scala klasse**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-174">In Project Explorer, right-click **src**, point to **New**, and then select **Scala Class**.</span></span>
      
      ![Opdrachten voor het maken van een klasse Scala van Projectverkenner](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="1cef9-176">b.</span><span class="sxs-lookup"><span data-stu-id="1cef9-176">b.</span></span> <span data-ttu-id="1cef9-177">In de **nieuwe Scala klasse maken** dialoogvenster vak, Geef een naam op, selecteer **Object** in de **soort** vak en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-177">In the **Create New Scala Class** dialog box, provide a name, select **Object** in the **Kind** box, and then select **OK**.</span></span>
      
      ![Dialoogvenster Nieuwe Scala klasse maken](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="1cef9-179">c.</span><span class="sxs-lookup"><span data-stu-id="1cef9-179">c.</span></span> <span data-ttu-id="1cef9-180">In de **MyClusterApp.scala** bestand, plak de volgende code.</span><span class="sxs-lookup"><span data-stu-id="1cef9-180">In the **MyClusterApp.scala** file, paste the following code.</span></span> <span data-ttu-id="1cef9-181">De code leest de gegevens van HVAC.csv (beschikbaar op alle HDInsight Spark-clusters), worden de rijen waarvoor slechts één cijfer in de zevende kolom in het CSV-bestand en schrijft de uitvoer naar **/HVACOut** onder de standaardcontainer voor opslag voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="1cef9-181">The code reads the data from HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that have only one digit in the seventh column in the CSV file, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find the rows that have only one digit in the seventh column in the CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. <span data-ttu-id="1cef9-182">Voer de toepassing op een HDInsight Spark-cluster als volgt:</span><span class="sxs-lookup"><span data-stu-id="1cef9-182">Run the application on an HDInsight Spark cluster by doing the following:</span></span>

   <span data-ttu-id="1cef9-183">a.</span><span class="sxs-lookup"><span data-stu-id="1cef9-183">a.</span></span> <span data-ttu-id="1cef9-184">In Projectverkenner met de rechtermuisknop op de projectnaam en selecteer vervolgens **Spark toepassing verzenden naar HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-184">In Project Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>
      
      ![De toepassing Spark verzenden naar HDInsight-opdracht](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="1cef9-186">b.</span><span class="sxs-lookup"><span data-stu-id="1cef9-186">b.</span></span> <span data-ttu-id="1cef9-187">U wordt gevraagd de referenties van uw Azure-abonnement in te voeren.</span><span class="sxs-lookup"><span data-stu-id="1cef9-187">You are prompted to enter your Azure subscription credentials.</span></span> <span data-ttu-id="1cef9-188">In de **Spark verzending** in het dialoogvenster bieden de volgende waarden en selecteer vervolgens **indienen**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-188">In the **Spark Submission** dialog box, provide the following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="1cef9-189">Voor **Spark-clusters (alleen voor Linux)**, selecteert u het HDInsight Spark-cluster waarop u wilt dat uw toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="1cef9-189">For **Spark clusters (Linux only)**, select the HDInsight Spark cluster on which you want to run your application.</span></span>

      * <span data-ttu-id="1cef9-190">Selecteer een artefact van het project IntelliJ of Selecteer een van de vaste schijf.</span><span class="sxs-lookup"><span data-stu-id="1cef9-190">Select an artifact from the IntelliJ project, or select one from the hard drive.</span></span>

      * <span data-ttu-id="1cef9-191">In de **Main klassenaam** Selecteer het weglatingsteken (**...** ), selecteert u de belangrijkste klasse in de broncode van uw toepassing en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-191">In the **Main class name** box, select the ellipsis (**...**), select the main class in your application source code, and then select **OK**.</span></span>

        ![Het dialoogvenster Main-klasse selecteren](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="1cef9-193">Omdat de toepassingscode die in dit voorbeeld geen opdrachtregelargumenten vereist of verwijzen naar potten of bestanden, kunt u de resterende selectievakjes leeg laten.</span><span class="sxs-lookup"><span data-stu-id="1cef9-193">Because the application code in this example does not require command-line arguments or reference JARs or files, you can leave the remaining boxes empty.</span></span> <span data-ttu-id="1cef9-194">Nadat u de informatie te verstrekken, moet de volgende afbeelding eruitzien als in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1cef9-194">After you provide all the information, the dialog box should resemble the following image.</span></span>
        
        ![Het dialoogvenster Spark verzending](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="1cef9-196">c.</span><span class="sxs-lookup"><span data-stu-id="1cef9-196">c.</span></span> <span data-ttu-id="1cef9-197">De **Spark verzending** tabblad aan de onderkant van het venster moet worden gestart om de voortgang weer te geven.</span><span class="sxs-lookup"><span data-stu-id="1cef9-197">The **Spark Submission** tab at the bottom of the window should start displaying the progress.</span></span> <span data-ttu-id="1cef9-198">U kunt ook de toepassing stoppen door het selecteren van de rode knop in de **Spark verzending** venster.</span><span class="sxs-lookup"><span data-stu-id="1cef9-198">You can also stop the application by selecting the red button in the **Spark Submission** window.</span></span>
      
      ![Het venster Spark verzending](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="1cef9-200">Zie voor meer informatie over het openen van de taakuitvoer van de, het ' toegang en HDInsight Spark-clusters beheren met behulp van Azure Toolkit voor IntelliJ ' verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="1cef9-200">To learn how to access the job output, see the "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="1cef9-201">Uitvoeren of fouten opsporen in een Spark Scala-toepassing op een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="1cef9-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="1cef9-202">Aangeraden wordt ook een andere manier om de Spark-toepassing aan het cluster in te dienen.</span><span class="sxs-lookup"><span data-stu-id="1cef9-202">We also recommend another way of submitting the Spark application to the cluster.</span></span> <span data-ttu-id="1cef9-203">U kunt dit doen door het instellen van de parameters in de **uitvoeren/Debug configuraties** IDE.</span><span class="sxs-lookup"><span data-stu-id="1cef9-203">You can do so by setting the parameters in the **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="1cef9-204">Zie voor meer informatie [op afstand fouten opsporen in Spark scala-toepassingen op een HDInsight-cluster in Azure werkset voor IntelliJ via SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="1cef9-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="1cef9-205">Toegang tot en HDInsight Spark-clusters beheren met behulp van Azure Toolkit voor IntelliJ</span><span class="sxs-lookup"><span data-stu-id="1cef9-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="1cef9-206">U kunt verschillende bewerkingen kunt uitvoeren met behulp van Azure Toolkit voor IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="1cef9-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-the-job-view"></a><span data-ttu-id="1cef9-207">Toegang tot de taakweergave van de</span><span class="sxs-lookup"><span data-stu-id="1cef9-207">Access the job view</span></span>
1. <span data-ttu-id="1cef9-208">Vouw in Azure Explorer **HDInsight**, vouw de naam van het Spark-cluster en selecteer vervolgens **taken**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-208">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then select **Jobs**.</span></span>  

    ![Taak weergave knooppunt](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="1cef9-210">In het rechterdeelvenster de **Spark taakweergave** tabblad geeft alle toepassingen die op het cluster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1cef9-210">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span></span> <span data-ttu-id="1cef9-211">Selecteer de naam van de toepassing waarvoor u wilt voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1cef9-211">Select the name of the application for which you want to see more details.</span></span>

    ![App-details](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="1cef9-213">Als u wilt weergeven basisinformatie actieve taak, de muisaanwijzer op de taakgrafiek.</span><span class="sxs-lookup"><span data-stu-id="1cef9-213">To display basic running job information, hover over the job graph.</span></span> <span data-ttu-id="1cef9-214">Als u wilt weergeven in de grafiek fasen en informatie die elke taak genereert, selecteer een knooppunt in de taakgrafiek.</span><span class="sxs-lookup"><span data-stu-id="1cef9-214">To view the stages graph and information that every job generates, select a node on the job graph.</span></span>

    ![Fase taakdetails](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="1cef9-216">Om weer te geven vaak gebruikt u Logboeken, zoals *stuurprogramma Stderr*, *stuurprogramma Stdout*, en *Directory Info*, selecteer de **logboek** tabblad.</span><span class="sxs-lookup"><span data-stu-id="1cef9-216">To view frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select the **Log** tab.</span></span>

    ![Logboekgegevens](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="1cef9-218">U kunt ook de geschiedenis Spark gebruikersinterface en de gebruikersinterface van YARN (op het toepassingsniveau) weergeven door een koppeling aan de bovenkant van het venster te selecteren.</span><span class="sxs-lookup"><span data-stu-id="1cef9-218">You can also view the Spark history UI and the YARN UI (at the application level) by selecting a link at the top of the window.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="1cef9-219">Toegang tot de server van de geschiedenis van Spark</span><span class="sxs-lookup"><span data-stu-id="1cef9-219">Access the Spark history server</span></span>
1. <span data-ttu-id="1cef9-220">Vouw in Azure Explorer **HDInsight**, met de rechtermuisknop op de naam van uw Spark-cluster en selecteer vervolgens **Open Spark geschiedenis UI**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="1cef9-221">Wanneer u wordt gevraagd, typt u de beheerdersreferenties van het cluster, dat u hebt opgegeven bij het instellen van het cluster.</span><span class="sxs-lookup"><span data-stu-id="1cef9-221">When you're prompted, enter the cluster's admin credentials, which you specified when you set up the cluster.</span></span>

3. <span data-ttu-id="1cef9-222">Op het dashboard van de server in de Spark geschiedenis, kunt u de naam van de toepassing op zoek naar de toepassing dat u zojuist hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="1cef9-222">On the Spark history server dashboard, you can use the application name to look for the application that you just finished running.</span></span> <span data-ttu-id="1cef9-223">In de bovenstaande code stelt u de naam van de toepassing met behulp van `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="1cef9-223">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="1cef9-224">De naam van uw toepassing Spark is daarom **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-the-ambari-portal"></a><span data-ttu-id="1cef9-225">Start de Ambari-portal</span><span class="sxs-lookup"><span data-stu-id="1cef9-225">Start the Ambari portal</span></span>
1. <span data-ttu-id="1cef9-226">Vouw in Azure Explorer **HDInsight**, met de rechtermuisknop op de naam van uw Spark-cluster en selecteer vervolgens **beheerportal Open Cluster (Ambari)**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="1cef9-227">Wanneer u wordt gevraagd, typt u de beheerdersreferenties voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="1cef9-227">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="1cef9-228">U kunt deze referenties opgegeven tijdens het installatieproces van het cluster.</span><span class="sxs-lookup"><span data-stu-id="1cef9-228">You specified these credentials during the cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="1cef9-229">Azure-abonnementen beheren</span><span class="sxs-lookup"><span data-stu-id="1cef9-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="1cef9-230">Azure-Toolkit voor IntelliJ bevat standaard het Spark-clusters van alle uw Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="1cef9-230">By default, Azure Toolkit for IntelliJ lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="1cef9-231">Indien nodig, kunt u de abonnementen die u wilt openen.</span><span class="sxs-lookup"><span data-stu-id="1cef9-231">If necessary, you can specify the subscriptions that you want to access.</span></span> 

1. <span data-ttu-id="1cef9-232">In Azure Explorer met de rechtermuisknop op de **Azure** de hoofd-knooppunt en selecteer vervolgens **abonnementen beheren**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-232">In Azure Explorer, right-click the **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="1cef9-233">Schakel de selectievakjes naast de abonnementen die u niet wilt openen, en selecteer vervolgens in het dialoogvenster **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-233">In the dialog box, clear the check boxes next to the subscriptions that you don't want to access, and then select **Close**.</span></span> <span data-ttu-id="1cef9-234">U kunt ook selecteren **Afmelden** als u wilt afmelden bij uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1cef9-234">You can also select **Sign Out** if you want to sign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="1cef9-235">Een Spark Scala-toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1cef9-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="1cef9-236">U kunt Azure Toolkit voor IntelliJ gebruiken Spark Scala-toepassingen lokaal uitvoeren op uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="1cef9-236">You can use Azure Toolkit for IntelliJ to run Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="1cef9-237">De toepassingen die normaal gesproken geen toegang nodig tot clusterresources, zoals de storage-containers en u kunt uitvoeren en lokaal te testen.</span><span class="sxs-lookup"><span data-stu-id="1cef9-237">The applications usually don't need access to cluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="1cef9-238">Vereiste</span><span class="sxs-lookup"><span data-stu-id="1cef9-238">Prerequisite</span></span>
<span data-ttu-id="1cef9-239">Terwijl u de lokale Spark Scala-toepassingen op een Windows-computer uitvoert, krijgt u mogelijk een uitzondering, zoals wordt beschreven in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="1cef9-239">While you're running the local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="1cef9-240">De uitzondering is omdat WinUtils.exe in Windows ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="1cef9-240">The exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="1cef9-241">Deze fout op te lossen [downloaden van het uitvoerbare bestand](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) naar een locatie zoals **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-241">To resolve this error, [download the executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="1cef9-242">Voeg de omgevingsvariabele **HADOOP_HOME**, en stel de waarde van de variabele **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-242">Then, add the environment variable **HADOOP_HOME**, and set the value of the variable to **C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="1cef9-243">Een lokale Spark Scala-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1cef9-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="1cef9-244">IntelliJ IDEA Start en een project maken.</span><span class="sxs-lookup"><span data-stu-id="1cef9-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="1cef9-245">In de **nieuw Project** dialoogvenster de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="1cef9-245">In the **New Project** dialog box, do the following:</span></span>
   
    <span data-ttu-id="1cef9-246">a.</span><span class="sxs-lookup"><span data-stu-id="1cef9-246">a.</span></span> <span data-ttu-id="1cef9-247">Selecteer **HDInsight** > **Spark in HDInsight lokaal uitvoeren voorbeeld (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="1cef9-248">b.</span><span class="sxs-lookup"><span data-stu-id="1cef9-248">b.</span></span> <span data-ttu-id="1cef9-249">In de **Build hulpprogramma** , selecteert u een van de volgende, afhankelijk van uw behoeften:</span><span class="sxs-lookup"><span data-stu-id="1cef9-249">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="1cef9-250">**Maven**, voor ondersteuning van de wizard Scala project maken</span><span class="sxs-lookup"><span data-stu-id="1cef9-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="1cef9-251">**SBT**, voor het beheren van de afhankelijkheden en bouwen voor het project Scala</span><span class="sxs-lookup"><span data-stu-id="1cef9-251">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![Het dialoogvenster Nieuw Project](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="1cef9-253">Selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="1cef9-254">In het volgende venster de volgende doen:</span><span class="sxs-lookup"><span data-stu-id="1cef9-254">In the next window, do the following:</span></span>
   
    <span data-ttu-id="1cef9-255">a.</span><span class="sxs-lookup"><span data-stu-id="1cef9-255">a.</span></span> <span data-ttu-id="1cef9-256">Voer een naam en locatie.</span><span class="sxs-lookup"><span data-stu-id="1cef9-256">Enter a project name and location.</span></span>

    <span data-ttu-id="1cef9-257">b.</span><span class="sxs-lookup"><span data-stu-id="1cef9-257">b.</span></span> <span data-ttu-id="1cef9-258">In de **Project SDK** vervolgkeuzelijst, selecteert u een Java-versie die is hoger dan versie 1.7.</span><span class="sxs-lookup"><span data-stu-id="1cef9-258">In the **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="1cef9-259">c.</span><span class="sxs-lookup"><span data-stu-id="1cef9-259">c.</span></span> <span data-ttu-id="1cef9-260">In de **Spark versie** vervolgkeuzelijst, selecteert u de versie van Scala die u wilt gebruiken: Scala 2.11.x voor Spark 2.0 of Scala 2.10.x voor Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="1cef9-260">In the **Spark Version** drop-down list, select the version of Scala that you want to use: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![Het dialoogvenster Nieuw Project](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="1cef9-262">Selecteer **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-262">Select **Finish**.</span></span>

6. <span data-ttu-id="1cef9-263">De sjabloon wordt toegevoegd een voorbeeldcode (**LogQuery**) onder de **src** map die u lokaal op uw computer uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="1cef9-263">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span></span>
   
    ![Locatie van LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="1cef9-265">Met de rechtermuisknop op de **LogQuery** toepassing en selecteer vervolgens **uitvoeren 'LogQuery'**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-265">Right-click the **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="1cef9-266">Op de **uitvoeren** tabblad onderaan, ziet u de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="1cef9-266">On the **Run** tab at the bottom, you see an output like the following:</span></span>
   
   ![Spark toepassing lokale resultaat van uitgevoerde](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-to-use-azure-toolkit-for-intellij"></a><span data-ttu-id="1cef9-268">Bestaande IntelliJ IDEA toepassingen met Azure Toolkit voor IntelliJ converteren</span><span class="sxs-lookup"><span data-stu-id="1cef9-268">Convert existing IntelliJ IDEA applications to use Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="1cef9-269">U kunt de bestaande Spark Scala converteren toepassingen die u in IntelliJ IDEA voor compatibiliteit met Azure Toolkit voor IntelliJ gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1cef9-269">You can convert the existing Spark Scala applications that you created in IntelliJ IDEA to be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="1cef9-270">Vervolgens kunt u de invoegtoepassing voor het verzenden van de toepassingen naar een HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="1cef9-270">You can then use the plug-in to submit the applications to an HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="1cef9-271">Voor een bestaande Spark Scala-toepassing die is gemaakt via IntelliJ IDEA, het bijbehorende .iml-bestand te openen.</span><span class="sxs-lookup"><span data-stu-id="1cef9-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open the associated .iml file.</span></span>

2. <span data-ttu-id="1cef9-272">In de hoofdmap van het niveau is een **module** element als volgt:</span><span class="sxs-lookup"><span data-stu-id="1cef9-272">At the root level is a **module** element like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="1cef9-273">Bewerk het element om toe te voegen `UniqueKey="HDInsightTool"` zodat de **module** element ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="1cef9-273">Edit the element to add `UniqueKey="HDInsightTool"` so that the **module** element looks like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="1cef9-274">Sla de wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="1cef9-274">Save the changes.</span></span> <span data-ttu-id="1cef9-275">Nu moet uw toepassing compatibel zijn met Azure Toolkit voor IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="1cef9-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="1cef9-276">U kunt dit testen met de rechtermuisknop op de projectnaam in Projectverkenner.</span><span class="sxs-lookup"><span data-stu-id="1cef9-276">You can test it by right-clicking the project name in Project Explorer.</span></span> <span data-ttu-id="1cef9-277">Het pop-upmenu heeft nu de optie **Spark toepassing verzenden naar HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="1cef9-277">The pop-up menu now has the option **Submit Spark Application to HDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1cef9-278">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="1cef9-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="1cef9-279">Fout bij lokaal uitvoeren: *gebruik een grotere heapgrootte*</span><span class="sxs-lookup"><span data-stu-id="1cef9-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="1cef9-280">Als u een 32-bits Java SDK tijdens de uitvoering van lokale, kunt u in Spark 1.6, de volgende fouten tegenkomen:</span><span class="sxs-lookup"><span data-stu-id="1cef9-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter the following errors:</span></span>

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

<span data-ttu-id="1cef9-281">Deze fouten optreden omdat de heapgrootte is niet groot genoeg zijn voor Spark om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="1cef9-281">These errors happen because the heap size is not large enough for Spark to run.</span></span> <span data-ttu-id="1cef9-282">Spark vereist ten minste 471 MB.</span><span class="sxs-lookup"><span data-stu-id="1cef9-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="1cef9-283">(Zie voor meer informatie [SPARK 12081](https://issues.apache.org/jira/browse/SPARK-12081).) Een eenvoudige oplossing is een 64-bits Java SDK gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1cef9-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is to use a 64-bit Java SDK.</span></span> <span data-ttu-id="1cef9-284">U kunt ook de JVM-instellingen in IntelliJ wijzigen door de volgende opties toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="1cef9-284">You can also change the JVM settings in IntelliJ by adding the following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Opties toe te voegen aan het vak 'VM options' in IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="1cef9-286">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="1cef9-286">FAQ</span></span>
<span data-ttu-id="1cef9-287">Als u een toepassing met Azure Data Lake Store, kies **interactief** modus tijdens het proces voor Azure aanmelden.</span><span class="sxs-lookup"><span data-stu-id="1cef9-287">To submit an application to Azure Data Lake Store, choose **Interactive** mode during the Azure sign-in process.</span></span> <span data-ttu-id="1cef9-288">Als u selecteert **automatisch** modus, kunt u een foutmelding krijgt.</span><span class="sxs-lookup"><span data-stu-id="1cef9-288">If you select **Automated** mode, you can get an error.</span></span>

![interactief aanmelden](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="1cef9-290">Nu we dit heeft opgelost.</span><span class="sxs-lookup"><span data-stu-id="1cef9-290">Now, we resolved it.</span></span> <span data-ttu-id="1cef9-291">U kunt een Azure Data Lake-Cluster verzenden van uw toepassing met een methode voor aanmelden.</span><span class="sxs-lookup"><span data-stu-id="1cef9-291">You can choose an Azure Data Lake Cluster to submit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="1cef9-292">Feedback en bekende problemen</span><span class="sxs-lookup"><span data-stu-id="1cef9-292">Feedback and known issues</span></span>
<span data-ttu-id="1cef9-293">Op dit moment wordt bekijken Spark uitvoer rechtstreeks niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="1cef9-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="1cef9-294">Als u suggesties of feedback hebt, of als er problemen optreden wanneer u deze invoegtoepassing gebruikt, een e-mail sturen naar hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="1cef9-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="1cef9-295"><a name="seealso"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1cef9-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="1cef9-296">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1cef9-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="1cef9-297">Demo</span><span class="sxs-lookup"><span data-stu-id="1cef9-297">Demo</span></span>
* <span data-ttu-id="1cef9-298">Maak Scala project (video): [Spark Scala-toepassingen maken](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="1cef9-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="1cef9-299">Foutopsporing op afstand (video): [gebruik Azure Toolkit voor IntelliJ fouten opsporen in Spark scala-toepassingen op afstand op HDInsight-Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="1cef9-299">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="1cef9-300">Scenario's</span><span class="sxs-lookup"><span data-stu-id="1cef9-300">Scenarios</span></span>
* [<span data-ttu-id="1cef9-301">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="1cef9-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="1cef9-302">Spark met Machine Learning: Spark in HDInsight analyseren gebouwtemperatuur met behulp van HVAC-gegevens gebruiken</span><span class="sxs-lookup"><span data-stu-id="1cef9-302">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="1cef9-303">Spark met Machine Learning: Spark in HDInsight gebruiken om voedselinspectieresultaten te voorspellen</span><span class="sxs-lookup"><span data-stu-id="1cef9-303">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="1cef9-304">Spark-Streaming: Spark in HDInsight voor het bouwen van realtime streamingtoepassingen gebruiken</span><span class="sxs-lookup"><span data-stu-id="1cef9-304">Spark Streaming: Use Spark in HDInsight to build real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="1cef9-305">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1cef9-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="1cef9-306">Maken en uitvoeren van toepassingen</span><span class="sxs-lookup"><span data-stu-id="1cef9-306">Creating and running applications</span></span>
* [<span data-ttu-id="1cef9-307">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="1cef9-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="1cef9-308">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="1cef9-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="1cef9-309">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="1cef9-309">Tools and extensions</span></span>
* [<span data-ttu-id="1cef9-310">Azure-Toolkit voor IntelliJ gebruiken om op te sporen Spark scala-toepassingen op afstand via VPN-verbinding</span><span class="sxs-lookup"><span data-stu-id="1cef9-310">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="1cef9-311">Azure-Toolkit voor IntelliJ gebruiken om op te sporen Spark-toepassingen op afstand via SSH</span><span class="sxs-lookup"><span data-stu-id="1cef9-311">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="1cef9-312">Gebruik van HDInsight Tools voor IntelliJ met Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="1cef9-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="1cef9-313">Gebruik van HDInsight-hulpprogramma's in Azure Toolkit voor Eclipse Spark-toepassingen maken</span><span class="sxs-lookup"><span data-stu-id="1cef9-313">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="1cef9-314">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1cef9-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="1cef9-315">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="1cef9-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="1cef9-316">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="1cef9-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="1cef9-317">Jupyter op uw computer installeren en verbinding maken met een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="1cef9-317">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="1cef9-318">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="1cef9-318">Managing resources</span></span>
* [<span data-ttu-id="1cef9-319">Resources beheren voor het Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1cef9-319">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="1cef9-320">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="1cef9-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)


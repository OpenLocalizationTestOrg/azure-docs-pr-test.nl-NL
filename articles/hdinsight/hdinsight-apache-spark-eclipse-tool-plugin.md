---
title: Toolkit voor Eclipse - toepassingen voor HDInsight Spark Scala maken aaaAzure | Microsoft Docs
description: HDInsight Tools gebruiken in Azure Toolkit voor Spark scala-toepassingen voor Eclipse toodevelop is geschreven in Scala en deze tooan HDInsight Spark-cluster te verzenden, rechtstreeks vanuit Hallo Eclipse IDE.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 3ab70857c1e81f591a1c7e29bc1706ec4899ff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-eclipse-toocreate-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="064ad-103">Gebruik Azure Toolkit voor Eclipse toocreate Spark scala-toepassingen voor een HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="064ad-103">Use Azure Toolkit for Eclipse toocreate Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="064ad-104">HDInsight Tools gebruiken in Azure Toolkit voor geschreven in Scala van Eclipse toodevelop Spark scala-toepassingen en deze tooan Azure HDInsight Spark-cluster, rechtstreeks vanuit Hallo Eclipse IDE verzenden.</span><span class="sxs-lookup"><span data-stu-id="064ad-104">Use HDInsight Tools in Azure Toolkit for Eclipse toodevelop Spark applications written in Scala and submit them tooan Azure HDInsight Spark cluster, directly from hello Eclipse IDE.</span></span> <span data-ttu-id="064ad-105">U kunt Hallo HDInsight Tools-invoegtoepassing op verschillende manieren gebruiken:</span><span class="sxs-lookup"><span data-stu-id="064ad-105">You can use hello HDInsight Tools plug-in in a few different ways:</span></span>

* <span data-ttu-id="064ad-106">toodevelop en het verzenden van een Scala Spark-toepassing op een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="064ad-106">toodevelop and submit a Scala Spark application on an HDInsight Spark cluster</span></span>
* <span data-ttu-id="064ad-107">tooaccess uw resources Azure HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="064ad-107">tooaccess your Azure HDInsight Spark cluster resources</span></span>
* <span data-ttu-id="064ad-108">toodevelop en een Scala Spark-toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="064ad-108">toodevelop and run a Scala Spark application locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="064ad-109">Dit hulpprogramma kan worden gebruikt toocreate en verzenden van toepassingen alleen voor een HDInsight Spark-cluster op Linux.</span><span class="sxs-lookup"><span data-stu-id="064ad-109">This tool can be used toocreate and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="064ad-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="064ad-110">Prerequisites</span></span>

* <span data-ttu-id="064ad-111">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="064ad-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="064ad-112">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="064ad-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="064ad-113">Oracle Java Development Kit versie 8, die wordt gebruikt voor Hallo Eclipse IDE tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="064ad-113">Oracle Java Development Kit version 8, which is used for hello Eclipse IDE runtime.</span></span> <span data-ttu-id="064ad-114">U kunt dit downloaden van Hallo [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="064ad-114">You can download it from hello [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="064ad-115">Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="064ad-115">Eclipse IDE.</span></span> <span data-ttu-id="064ad-116">In dit artikel maakt gebruik van Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="064ad-116">This article uses Eclipse Neon.</span></span> <span data-ttu-id="064ad-117">U kunt deze installeren via Hallo [Eclipse website](https://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="064ad-117">You can install it from hello [Eclipse website](https://www.eclipse.org/downloads/).</span></span>   
* <span data-ttu-id="064ad-118">Spark SDK.</span><span class="sxs-lookup"><span data-stu-id="064ad-118">Spark SDK.</span></span> <span data-ttu-id="064ad-119">U kunt downloaden van [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="064ad-119">You can download it from [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span></span>


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a><span data-ttu-id="064ad-120">HDInsight-hulpprogramma's in Azure Toolkit voor Eclipse en Scala-invoegtoepassing installeren</span><span class="sxs-lookup"><span data-stu-id="064ad-120">Install HDInsight Tools in Azure Toolkit for Eclipse and Scala Plugin</span></span>
### <a name="install-hdinsight-tools"></a><span data-ttu-id="064ad-121">HDInsight-hulpprogramma's installeren</span><span class="sxs-lookup"><span data-stu-id="064ad-121">Install HDInsight Tools</span></span>
<span data-ttu-id="064ad-122">HDInsight Tools voor Eclipse is beschikbaar als onderdeel van Azure Toolkit voor Eclipse.</span><span class="sxs-lookup"><span data-stu-id="064ad-122">HDInsight Tools for Eclipse is available as part of Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="064ad-123">Zie voor installatie-instructies [Azure Toolkit installeren voor Eclipse](../azure-toolkit-for-eclipse-installation.md).</span><span class="sxs-lookup"><span data-stu-id="064ad-123">For installation instructions, see [Installing Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse-installation.md).</span></span>
### <a name="install-scala-plugin"></a><span data-ttu-id="064ad-124">Scala-invoegtoepassing installeren</span><span class="sxs-lookup"><span data-stu-id="064ad-124">Install Scala Plugin</span></span>
<span data-ttu-id="064ad-125">Wanneer u Hallo Intellij opent, detecteert Hallo HDInsight Tools automatisch of u Scala invoegtoepassing geïnstalleerd of niet.</span><span class="sxs-lookup"><span data-stu-id="064ad-125">When you open hello Intellij, hello HDInsight Tools auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="064ad-126">Klik op **OK** toocontinue en volg Hallo instructies tooinstall door Hallo Eclipse Marketplace.</span><span class="sxs-lookup"><span data-stu-id="064ad-126">Click **OK** toocontinue and follow hello instructions tooinstall by hello Eclipse Marketplace.</span></span>

 ![Automatische installatie Scala-invoegtoepassing](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-tooyour-azure-subscription"></a><span data-ttu-id="064ad-128">Meld u aan tooyour Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="064ad-128">Sign in tooyour Azure subscription</span></span>
1. <span data-ttu-id="064ad-129">Start Eclipse IDE Hallo en Azure Explorer te openen.</span><span class="sxs-lookup"><span data-stu-id="064ad-129">Start hello Eclipse IDE and open Azure Explorer.</span></span> <span data-ttu-id="064ad-130">Op Hallo **venster** menu, klikt u op **weergave tonen**, en klik vervolgens op **andere**.</span><span class="sxs-lookup"><span data-stu-id="064ad-130">On hello **Window** menu, click **Show View**, and then click **Other**.</span></span> <span data-ttu-id="064ad-131">Vouw in het dialoogvenster Hallo dat wordt geopend, **Azure**, klikt u op **Azure Explorer**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="064ad-131">In hello dialog box that opens, expand **Azure**, click **Azure Explorer**, and then click **OK**.</span></span>

    ![Het dialoogvenster weergave weergeven](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. <span data-ttu-id="064ad-133">Klik met de rechtermuisknop Hallo **Azure** knooppunt en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="064ad-133">Right-click hello **Azure** node, and then click **Sign in**.</span></span>
3. <span data-ttu-id="064ad-134">In Hallo **Azure aanmelden** dialoogvenster vak, kies de verificatiemethode hello, klik op **aanmelden**, en voer uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="064ad-134">In hello **Azure Sign In** dialog box, choose hello authentication method, click **Sign in**, and enter your Azure credentials.</span></span>
   
    ![Azure Sign In het dialoogvenster](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. <span data-ttu-id="064ad-136">Nadat u bent aangemeld, Hallo **Selecteer abonnementen** dialoogvenster lijsten alle hello Azure-abonnementen die zijn gekoppeld aan het Hallo-referenties.</span><span class="sxs-lookup"><span data-stu-id="064ad-136">After you're signed in, hello **Select Subscriptions** dialog box lists all hello Azure subscriptions associated with hello credentials.</span></span> <span data-ttu-id="064ad-137">Klik op **Selecteer** tooclose Hallo dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="064ad-137">Click **Select** tooclose hello dialog box.</span></span>

    ![Selecteer in het dialoogvenster voor abonnementen](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. <span data-ttu-id="064ad-139">Op Hallo **Azure Explorer** tabblad uit, vouw **HDInsight** toosee hello HDInsight Spark-clusters in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="064ad-139">On hello **Azure Explorer** tab, expand **HDInsight** toosee hello HDInsight Spark clusters under your subscription.</span></span>
   
    ![HDInsight Spark-clusters in Azure Explorer](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. <span data-ttu-id="064ad-141">U kunt een naam knooppunt toosee Hallo clusterbronnen (bijvoorbeeld opslagaccounts) die zijn gekoppeld aan cluster Hallo verder uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="064ad-141">You can further expand a cluster name node toosee hello resources (for example, storage accounts) associated with hello cluster.</span></span>
   
    ![Uitbreiden van een cluster naam toosee resources](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="064ad-143">Een Spark Scala-project voor een HDInsight Spark-cluster instellen</span><span class="sxs-lookup"><span data-stu-id="064ad-143">Set up a Spark Scala project for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="064ad-144">Klik in Hallo Eclipse IDE werkruimte **bestand**, klikt u op **nieuw**, en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="064ad-144">In hello Eclipse IDE workspace, click **File**, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="064ad-145">Vouw in de wizard Nieuw Project hello, **HDInsight**, selecteer **Spark in HDInsight (Scala)**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="064ad-145">In hello New Project wizard, expand **HDInsight**, select **Spark on HDInsight (Scala)**, and then click **Next**.</span></span>

    ![Hallo Spark in HDInsight (Scala) project selecteren](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. <span data-ttu-id="064ad-147">Hallo Scala project maken wizard automatisch detecteert of de Scala invoegtoepassing geïnstalleerd of niet.</span><span class="sxs-lookup"><span data-stu-id="064ad-147">hello Scala project creation wizard auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="064ad-148">Klik op **OK** toocontinue Hallo Scala invoegtoepassing en vervolgens volg Hallo instructies toorestart Eclipse downloaden.</span><span class="sxs-lookup"><span data-stu-id="064ad-148">Click **OK** toocontinue downloading hello Scala plugin, then follow hello instructions toorestart Eclipse.</span></span>

    ![controle van scala](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. <span data-ttu-id="064ad-150">In Hallo **nieuw HDInsight Scala Project** in het dialoogvenster Hallo volgende waarden bevatten, en klik vervolgens op **volgende**:</span><span class="sxs-lookup"><span data-stu-id="064ad-150">In hello **New HDInsight Scala Project** dialog box, provide hello following values, and then click **Next**:</span></span>
   * <span data-ttu-id="064ad-151">Voer een naam voor Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="064ad-151">Enter a name for hello project.</span></span>
   * <span data-ttu-id="064ad-152">In Hallo **JRE** gebied, zorg ervoor dat **gebruik van een uitvoeringsomgeving JRE** te is ingesteld,**JavaSE 1.7** of hoger.</span><span class="sxs-lookup"><span data-stu-id="064ad-152">In hello **JRE** area, make sure that **Use an execution environment JRE** is set too**JavaSE-1.7** or later.</span></span>
   * <span data-ttu-id="064ad-153">Zorg ervoor dat SDK Spark is set toohello locatie waar u Hallo SDK hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="064ad-153">Make sure that Spark SDK is set toohello location where you downloaded hello SDK.</span></span> <span data-ttu-id="064ad-154">Hallo koppeling toohello downloadlocatie is opgenomen in Hallo [vereisten](#prerequisites) eerder in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="064ad-154">hello link toohello download location is included in hello [prerequisites](#prerequisites) earlier in this article.</span></span> <span data-ttu-id="064ad-155">U kunt ook Hallo SDK downloaden van Hallo opgenomen in het dialoogvenster Hallo koppeling.</span><span class="sxs-lookup"><span data-stu-id="064ad-155">You can also download hello SDK from hello link included in hello dialog box.</span></span>

    ![Het dialoogvenster New Project van HDInsight Scala](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  <span data-ttu-id="064ad-157">In het volgende dialoogvenster hello, klikt u op Hallo **bibliotheken** tabblad en klik vervolgens op Hallo standaardinstellingen behouden **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="064ad-157">In hello next dialog box, click hello **Libraries** tab and keep hello defaults, and then click **Finish**.</span></span> 
   
    ![Tabblad bibliotheken](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="064ad-159">Een Scala-toepassing voor een HDInsight Spark-cluster maken</span><span class="sxs-lookup"><span data-stu-id="064ad-159">Create a Scala application for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="064ad-160">Vouw in Eclipse IDE, vanuit de Explorer-pakket, Hallo Hallo-project dat u eerder hebt gemaakt, met de rechtermuisknop op **src**, wijst u te**nieuw**, en klik vervolgens op **andere**.</span><span class="sxs-lookup"><span data-stu-id="064ad-160">In hello Eclipse IDE, from Package Explorer, expand hello project that you created earlier, right-click **src**, point too**New**, and then click **Other**.</span></span>
2. <span data-ttu-id="064ad-161">In Hallo **een wizard selecteren** dialoogvenster Vouw **Scala Wizards**, klikt u op **Scala Object**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="064ad-161">In hello **Select a wizard** dialog box, expand **Scala Wizards**, click **Scala Object**, and then click **Next**.</span></span>
   
    ![Selecteer in het dialoogvenster wizard](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. <span data-ttu-id="064ad-163">In Hallo **nieuw bestand maken** in het dialoogvenster een naam voor het Hallo-object invoeren, en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="064ad-163">In hello **Create New File** dialog box, enter a name for hello object, and then click **Finish**.</span></span>
   
    ![Dialoogvenster nieuwe bestanden maken](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. <span data-ttu-id="064ad-165">Plak de volgende code in de teksteditor Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="064ad-165">Paste hello following code in hello text editor:</span></span>
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows that have only one digit in hello seventh column in hello CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. <span data-ttu-id="064ad-166">Hallo-toepassing uitvoeren op een HDInsight Spark-cluster:</span><span class="sxs-lookup"><span data-stu-id="064ad-166">Run hello application on an HDInsight Spark cluster:</span></span>
   
   1. <span data-ttu-id="064ad-167">Met de rechtermuisknop op de projectnaam Hallo vanuit de Explorer-pakket, en selecteer vervolgens **indienen Spark toepassing tooHDInsight**.</span><span class="sxs-lookup"><span data-stu-id="064ad-167">From Package Explorer, right-click hello project name, and then select **Submit Spark Application tooHDInsight**.</span></span>        
   2. <span data-ttu-id="064ad-168">In Hallo **Spark verzending** in het dialoogvenster Hallo volgende waarden bevatten, en klik vervolgens op **indienen**:</span><span class="sxs-lookup"><span data-stu-id="064ad-168">In hello **Spark Submission** dialog box, provide hello following values, and then click **Submit**:</span></span>
      
      * <span data-ttu-id="064ad-169">Voor **clusternaam**, selecteer Hallo HDInsight Spark-cluster waarop toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="064ad-169">For **Cluster Name**, select hello HDInsight Spark cluster on which you want toorun your application.</span></span>
      * <span data-ttu-id="064ad-170">Selecteer een artefact in Eclipse-project Hallo of Selecteer een vanaf een vaste schijf.</span><span class="sxs-lookup"><span data-stu-id="064ad-170">Select an artifact from hello Eclipse project, or select one from a hard drive.</span></span> <span data-ttu-id="064ad-171">Hallo-standaardwaarde, hangt af van Hallo item die u met de rechtermuisknop in explorer pakket.</span><span class="sxs-lookup"><span data-stu-id="064ad-171">hello default value depends on hello item you right-click from package explorer.</span></span>
      * <span data-ttu-id="064ad-172">In Hallo **Main klassenaam** dropdownlist, verzending van wizard weer met alle objectnamen uit het geselecteerde project.</span><span class="sxs-lookup"><span data-stu-id="064ad-172">In hello **Main class name** dropdownlist, submission wizard displays all object names from your selected project.</span></span> <span data-ttu-id="064ad-173">Selecteer of voer een gewenste toorun.</span><span class="sxs-lookup"><span data-stu-id="064ad-173">Select or input one that you want toorun.</span></span> <span data-ttu-id="064ad-174">Als u artefact van harde schijf selecteert, moet u hoofdklasse naam zelf invoeren.</span><span class="sxs-lookup"><span data-stu-id="064ad-174">If you select artifact from hard disk, you need input main class name by yourself.</span></span> 
      * <span data-ttu-id="064ad-175">Omdat de toepassingscode Hallo in dit voorbeeld geen geen opdrachtregelargumenten of verwijzen naar potten of bestanden, kunt u Hallo resterende tekstvakken leeg laten.</span><span class="sxs-lookup"><span data-stu-id="064ad-175">Because hello application code in this example does not require any command-line arguments or reference JARs or files, you can leave hello remaining text boxes empty.</span></span>
        
       ![Dialoogvenster Spark verzending](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. <span data-ttu-id="064ad-177">Hallo **Spark verzending** tabblad moet beginnen met het Hallo voortgang weergeven.</span><span class="sxs-lookup"><span data-stu-id="064ad-177">hello **Spark Submission** tab should start displaying hello progress.</span></span> <span data-ttu-id="064ad-178">U kunt de toepassing hello stoppen Hallo rode knop in Hallo **Spark verzending** venster.</span><span class="sxs-lookup"><span data-stu-id="064ad-178">You can stop hello application by clicking hello red button in hello **Spark Submission** window.</span></span> <span data-ttu-id="064ad-179">U kunt ook Hallo-logboeken voor deze specifieke toepassing uitvoeren door te klikken op het pictogram wereldbol hello (aangeduid met Hallo blauw vak in Hallo installatiekopie) weergeven.</span><span class="sxs-lookup"><span data-stu-id="064ad-179">You can also view hello logs for this specific application run by clicking hello globe icon (denoted by hello blue box in hello image).</span></span>
      
       ![Verzending van Spark-venster](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a><span data-ttu-id="064ad-181">Toegang tot en HDInsight Spark-clusters beheren met behulp van HDInsight-hulpprogramma's in Azure Toolkit voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="064ad-181">Access and manage HDInsight Spark clusters by using HDInsight Tools in Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="064ad-182">U kunt verschillende bewerkingen kunt uitvoeren met behulp van HDInsight-hulpprogramma's, waaronder toegang tot Hallo taakuitvoer.</span><span class="sxs-lookup"><span data-stu-id="064ad-182">You can perform various operations by using HDInsight Tools, including accessing hello job output.</span></span>

### <a name="access-hello-job-view"></a><span data-ttu-id="064ad-183">Toegang Hallo taak weergeven</span><span class="sxs-lookup"><span data-stu-id="064ad-183">Access hello job view</span></span>
1. <span data-ttu-id="064ad-184">Vouw in Azure Explorer **HDInsight**Hallo Spark clusternaam uitvouwen en klik vervolgens op **taken**.</span><span class="sxs-lookup"><span data-stu-id="064ad-184">In Azure Explorer, expand **HDInsight**, expand hello Spark cluster name, and then click **Jobs**.</span></span> 

    ![Taak weergave knooppunt](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="064ad-186">Klik op Hallo **taken** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="064ad-186">Click on hello **Jobs** node.</span></span> <span data-ttu-id="064ad-187">Hallo HDInsight Tools detecteert automatisch welk of u Hallo E (fx) clipse invoegtoepassing geïnstalleerd of niet.</span><span class="sxs-lookup"><span data-stu-id="064ad-187">hello HDInsight Tools auto-detects whether you installed hello E(fx)clipse plugin or not.</span></span> <span data-ttu-id="064ad-188">Klik op **OK** toocontinue en volg Hallo instructies tooinstall Hallo Eclipse Marketplace en Eclipse opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="064ad-188">Click **OK** toocontinue and follow hello instructions tooinstall hello Eclipse Marketplace and restart Eclipse.</span></span>

    ![Clipse E (fx) installeren](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. <span data-ttu-id="064ad-190">Open Hallo taakweergave van Hallo **taken** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="064ad-190">Open hello Job View from hello **Jobs** node.</span></span> <span data-ttu-id="064ad-191">Klik in het rechterdeelvenster Hallo Hallo **Spark taak weergeven** tabblad geeft alle Hallo-toepassingen die op het Hallo-cluster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="064ad-191">In hello right pane, hello **Spark Job View** tab displays all hello applications that were run on hello cluster.</span></span> <span data-ttu-id="064ad-192">Klik op de naam Hallo van Hallo toepassing waarvoor u toosee meer informatie wenst.</span><span class="sxs-lookup"><span data-stu-id="064ad-192">Click hello name of hello application for which you want toosee more details.</span></span>

    ![App-details](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. <span data-ttu-id="064ad-194">Als u de muisaanwijzer op Hallo taakgrafiek, wordt standaard uitgevoerd taak gegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="064ad-194">If you hover on hello job graph, it displays basic running job info.</span></span> <span data-ttu-id="064ad-195">Te klikken op Hallo taakgrafiek toont Hallo fasen grafiek en gegevens die elke taak genereert.</span><span class="sxs-lookup"><span data-stu-id="064ad-195">Clicking on hello job graph shows hello stages graph and info that every job generates.</span></span>

    ![Fase taakdetails](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. <span data-ttu-id="064ad-197">Veelgebruikte Logboeken, waaronder stuurprogramma Stderr, stuurprogramma Stdout en Directory-gegevens worden weergegeven in Hallo **logboek** tabblad.</span><span class="sxs-lookup"><span data-stu-id="064ad-197">Frequently used logs, including Driver Stderr, Driver Stdout, and Directory Info, are listed in hello **Log** tab.</span></span>

    ![Logboekgegevens](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. <span data-ttu-id="064ad-199">U kunt ook Hallo Spark geschiedenis gebruikersinterface en Hallo gebruikersinterface van YARN (op niveau van de toepassing hello) openen door te klikken op de respectieve hyperlink Hallo Hallo boven aan het Hallo-venster.</span><span class="sxs-lookup"><span data-stu-id="064ad-199">You can also open hello Spark history UI and hello YARN UI (at hello application level) by clicking hello respective hyperlink at hello top of hello window.</span></span>

### <a name="access-hello-storage-container-for-hello-cluster"></a><span data-ttu-id="064ad-200">Toegang Hallo storage-container voor Hallo-cluster</span><span class="sxs-lookup"><span data-stu-id="064ad-200">Access hello storage container for hello cluster</span></span>
1. <span data-ttu-id="064ad-201">Vouw in Azure Explorer Hallo **HDInsight** hoofdmap knooppunt toosee een lijst met HDInsight Spark-clusters die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="064ad-201">In Azure Explorer, expand hello **HDInsight** root node toosee a list of HDInsight Spark clusters that are available.</span></span>
2. <span data-ttu-id="064ad-202">Hallo cluster naam toosee Hallo storage-account en Hallo standaardopslagcontainer voor Hallo-cluster uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="064ad-202">Expand hello cluster name toosee hello storage account and hello default storage container for hello cluster.</span></span>
   
    ![Storage-account en het standaard storage-container](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. <span data-ttu-id="064ad-204">Klik op Hallo containernaam voor opslag die is gekoppeld aan het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="064ad-204">Click hello storage container name associated with hello cluster.</span></span> <span data-ttu-id="064ad-205">Dubbelklik in het rechterdeelvenster Hallo Hallo **HVACOut** map.</span><span class="sxs-lookup"><span data-stu-id="064ad-205">In hello right pane, double-click hello **HVACOut** folder.</span></span> <span data-ttu-id="064ad-206">Open een Hallo **onderdeel -** toosee Hallo uitvoer van de toepassing hello bestanden.</span><span class="sxs-lookup"><span data-stu-id="064ad-206">Open one of hello **part-** files toosee hello output of hello application.</span></span>

### <a name="access-hello-spark-history-server"></a><span data-ttu-id="064ad-207">Toegang tot Hallo Spark geschiedenis van server</span><span class="sxs-lookup"><span data-stu-id="064ad-207">Access hello Spark history server</span></span>
1. <span data-ttu-id="064ad-208">Met de rechtermuisknop op de naam van uw Spark-cluster in Azure Explorer en selecteer vervolgens **Open Spark geschiedenis UI**.</span><span class="sxs-lookup"><span data-stu-id="064ad-208">In Azure Explorer, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> <span data-ttu-id="064ad-209">Wanneer u wordt gevraagd, voert u beheerdersreferenties Hallo voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="064ad-209">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="064ad-210">U moet hebben opgegeven deze tijdens het Hallo-cluster inrichten.</span><span class="sxs-lookup"><span data-stu-id="064ad-210">You must have specified these while provisioning hello cluster.</span></span>
2. <span data-ttu-id="064ad-211">In Hallo Spark geschiedenis serverdashboard gebruikt u Hallo toepassing naam toolook voor Hallo toepassing dat u zojuist hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="064ad-211">In hello Spark history server dashboard, you use hello application name toolook for hello application that you just finished running.</span></span> <span data-ttu-id="064ad-212">In Hallo voorafgaand aan code, stelt u de naam van de toepassing hello met behulp van `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="064ad-212">In hello preceding code, you set hello application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="064ad-213">Daarom de naam van uw toepassing Spark is **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="064ad-213">Hence, your Spark application name was **MyClusterApp**.</span></span>

### <a name="start-hello-ambari-portal"></a><span data-ttu-id="064ad-214">Hallo Ambari portal starten</span><span class="sxs-lookup"><span data-stu-id="064ad-214">Start hello Ambari portal</span></span>
1. <span data-ttu-id="064ad-215">Met de rechtermuisknop op de naam van uw Spark-cluster in Azure Explorer en selecteer vervolgens **beheerportal Open Cluster (Ambari)**.</span><span class="sxs-lookup"><span data-stu-id="064ad-215">In Azure Explorer, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 
2. <span data-ttu-id="064ad-216">Wanneer u wordt gevraagd, voert u beheerdersreferenties Hallo voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="064ad-216">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="064ad-217">U moet hebben opgegeven deze tijdens het Hallo-cluster inrichten.</span><span class="sxs-lookup"><span data-stu-id="064ad-217">You must have specified these while provisioning hello cluster.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="064ad-218">Azure-abonnementen beheren</span><span class="sxs-lookup"><span data-stu-id="064ad-218">Manage Azure subscriptions</span></span>
<span data-ttu-id="064ad-219">HDInsight-hulpprogramma's in Azure Toolkit voor Eclipse bevat standaard Hallo Spark-clusters van alle uw Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="064ad-219">By default, HDInsight Tools in Azure Toolkit for Eclipse lists hello Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="064ad-220">Indien nodig, kunt u Hallo abonnementen waarvoor u tooaccess Hallo cluster wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="064ad-220">If necessary, you can specify hello subscriptions for which you want tooaccess hello cluster.</span></span> 

1. <span data-ttu-id="064ad-221">Azure Explorer met de rechtermuisknop op Hallo **Azure** de hoofd-knooppunt en klik vervolgens op **abonnementen beheren**.</span><span class="sxs-lookup"><span data-stu-id="064ad-221">In Azure Explorer, right-click hello **Azure** root node, and then click **Manage Subscriptions**.</span></span> 
2. <span data-ttu-id="064ad-222">In het dialoogvenster hello, schakel de selectievakjes Hallo voor Hallo-abonnement dat u niet wilt dat tooaccess en klik vervolgens op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="064ad-222">In hello dialog box, clear hello check boxes for hello subscription that you don't want tooaccess, and then click **Close**.</span></span> <span data-ttu-id="064ad-223">U kunt ook klikken op **Afmelden** als u wilt dat toosign buiten uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="064ad-223">You can also click **Sign Out** if you want toosign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="064ad-224">Een Spark Scala-toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="064ad-224">Run a Spark Scala application locally</span></span>
<span data-ttu-id="064ad-225">Kunt u HDInsight-hulpprogramma's in Azure Toolkit voor Eclipse toorun Spark Scala-toepassingen lokaal op uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="064ad-225">You can use HDInsight Tools in Azure Toolkit for Eclipse toorun Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="064ad-226">Normaal gesproken deze toepassingen toegang toocluster resources, zoals een opslagcontainer niet nodig en u kunt uitvoeren en lokaal te testen.</span><span class="sxs-lookup"><span data-stu-id="064ad-226">Typically, these applications don't need access toocluster resources such as a storage container, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="064ad-227">Vereiste</span><span class="sxs-lookup"><span data-stu-id="064ad-227">Prerequisite</span></span>
<span data-ttu-id="064ad-228">Terwijl u Hallo lokale Spark Scala-toepassingen op een Windows-computer uitvoert, krijgt u mogelijk een uitzondering zoals toegelicht in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="064ad-228">While you're running hello local Spark Scala application on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="064ad-229">Deze uitzondering doet zich voor omdat **WinUtils.exe** ontbreekt in Windows.</span><span class="sxs-lookup"><span data-stu-id="064ad-229">This exception occurs because **WinUtils.exe** is missing in Windows.</span></span> 

<span data-ttu-id="064ad-230">tooresolve deze fout, moet u [downloaden Hallo uitvoerbare](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa locatie, zoals **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="064ad-230">tooresolve this error, you must [download hello executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="064ad-231">Vervolgens moet u de omgevingsvariabele Hallo toevoegen **HADOOP_HOME** en stelt u Hallo-waarde van variabele hello te**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="064ad-231">You must then add hello environment variable **HADOOP_HOME** and set hello value of hello variable too**C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="064ad-232">Een lokale Spark Scala-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="064ad-232">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="064ad-233">Start Eclipse en maak een project.</span><span class="sxs-lookup"><span data-stu-id="064ad-233">Start Eclipse and create a project.</span></span> <span data-ttu-id="064ad-234">In Hallo **nieuw Project** in het dialoogvenster Hallo volgende keuzes maken en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="064ad-234">In hello **New Project** dialog box, make hello following choices, and then click **Next**.</span></span>
   
   * <span data-ttu-id="064ad-235">Selecteer in het linkerdeelvenster Hallo **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="064ad-235">In hello left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="064ad-236">Selecteer in het rechterdeelvenster Hallo **Spark in HDInsight lokale uitvoeren voorbeeld (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="064ad-236">In hello right pane, select **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    ![Het dialoogvenster Nieuw project](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. <span data-ttu-id="064ad-238">details van tooprovide hello, volg de stappen 3 tot en met 6 uit eerdere sectie Hallo [instellen van een Spark Scala-project voor een HDInsight Spark-cluster](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).</span><span class="sxs-lookup"><span data-stu-id="064ad-238">tooprovide hello project details, follow steps 3 through 6 from hello earlier section [Set up a Spark Scala project for an HDInsight Spark cluster](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).</span></span>
3. <span data-ttu-id="064ad-239">Hallo-sjabloon wordt toegevoegd een voorbeeldcode (**LogQuery**) onder Hallo **src** map die u lokaal op uw computer uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="064ad-239">hello template adds a sample code (**LogQuery**) under hello **src** folder that you can run locally on your computer.</span></span>
   
    ![Locatie van LogQuery](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. <span data-ttu-id="064ad-241">Klik met de rechtermuisknop Hallo **LogQuery** -toepassing te verwijzen**uitvoeren als**, en klik vervolgens op **1 Scala toepassing**.</span><span class="sxs-lookup"><span data-stu-id="064ad-241">Right-click hello **LogQuery** application, point too**Run As**, and then click **1 Scala Application**.</span></span> <span data-ttu-id="064ad-242">Ziet u uitvoer zoals deze in Hallo **Console** tabblad Hallo onderaan:</span><span class="sxs-lookup"><span data-stu-id="064ad-242">You will see an output like this in hello **Console** tab at hello bottom:</span></span>
   
   ![Spark toepassing lokale resultaat van uitgevoerde](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a><span data-ttu-id="064ad-244">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="064ad-244">FAQ</span></span>
<span data-ttu-id="064ad-245">kiest u een toepassing tooAzure Data Lake Store toosubmit **interactief** modus tijdens hello Azure aanmelden.</span><span class="sxs-lookup"><span data-stu-id="064ad-245">toosubmit an application tooAzure Data Lake Store, choose **Interactive** mode during hello Azure sign-in process.</span></span> <span data-ttu-id="064ad-246">Als u selecteert **automatisch** modus, kunt u een foutmelding krijgt.</span><span class="sxs-lookup"><span data-stu-id="064ad-246">If you select **Automated** mode, you can get an error.</span></span>

![interactief aanmelden](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

<span data-ttu-id="064ad-248">Nu we dit heeft opgelost.</span><span class="sxs-lookup"><span data-stu-id="064ad-248">Now, we resolved it.</span></span> <span data-ttu-id="064ad-249">U kunt een Azure Data Lake Cluster toosubmit uw toepassing met een methode voor aanmelden.</span><span class="sxs-lookup"><span data-stu-id="064ad-249">You can choose an Azure Data Lake Cluster toosubmit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="064ad-250">Feedback en bekende problemen</span><span class="sxs-lookup"><span data-stu-id="064ad-250">Feedback and known issues</span></span>
<span data-ttu-id="064ad-251">Op dit moment wordt bekijken Spark uitvoer rechtstreeks niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="064ad-251">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="064ad-252">Als u suggesties of feedback hebt, of als u problemen ondervindt bij het gebruik van dit hulpprogramma, kunt u gratis toosend ons een e-mailbericht op hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="064ad-252">If you have any suggestions or feedback, or if you encounter any problems when using this tool, feel free toosend us an email at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="064ad-253"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="064ad-253"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="064ad-254">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="064ad-254">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="064ad-255">Scenario's</span><span class="sxs-lookup"><span data-stu-id="064ad-255">Scenarios</span></span>
* [<span data-ttu-id="064ad-256">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="064ad-256">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="064ad-257">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="064ad-257">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="064ad-258">Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="064ad-258">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="064ad-259">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="064ad-259">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="064ad-260">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="064ad-260">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="064ad-261">Maken en uitvoeren van toepassingen</span><span class="sxs-lookup"><span data-stu-id="064ad-261">Creating and running applications</span></span>
* [<span data-ttu-id="064ad-262">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="064ad-262">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="064ad-263">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="064ad-263">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="064ad-264">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="064ad-264">Tools and extensions</span></span>
* [<span data-ttu-id="064ad-265">Gebruik van Azure Toolkit voor IntelliJ toocreate en het verzenden van Spark Scala-toepassingen</span><span class="sxs-lookup"><span data-stu-id="064ad-265">Use Azure Toolkit for IntelliJ toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="064ad-266">Gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand via VPN-verbinding</span><span class="sxs-lookup"><span data-stu-id="064ad-266">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="064ad-267">Gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand via SSH</span><span class="sxs-lookup"><span data-stu-id="064ad-267">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="064ad-268">Gebruik van HDInsight Tools voor IntelliJ met Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="064ad-268">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="064ad-269">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="064ad-269">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="064ad-270">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="064ad-270">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="064ad-271">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="064ad-271">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="064ad-272">Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="064ad-272">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="064ad-273">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="064ad-273">Managing resources</span></span>
* [<span data-ttu-id="064ad-274">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="064ad-274">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="064ad-275">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="064ad-275">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)


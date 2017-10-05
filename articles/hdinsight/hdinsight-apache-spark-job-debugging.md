---
title: Fouten opsporen in Apache Spark taken uitgevoerd op Azure HDInsight | Microsoft Docs
description: Gebruikersinterface van YARN, Spark-UI en Spark geschiedenis server bijhouden en foutopsporing van taken die worden uitgevoerd op een Spark-cluster in Azure HDInsight gebruiken
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: bf66757cc9439a969c9f28abc0b95055ff697c3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="948a7-103">Fouten opsporen in Apache Spark taken uitgevoerd op Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="948a7-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="948a7-104">In dit artikel leert u hoe bijhouden en fouten opsporen in Spark-taken op via de gebruikersinterface van YARN, Spark-gebruikersinterface en de Server van de geschiedenis van Spark HDInsight-clusters worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="948a7-104">In this article you will learn how to track and debug Spark jobs running on HDInsight clusters using the YARN UI, Spark UI, and the Spark History Server.</span></span> <span data-ttu-id="948a7-105">Voor dit artikel gaat we een Spark-taak met een laptop beschikbaar met het Spark-cluster **Machine learning: Predictive Analytics op voeding inspectie gegevens met behulp van MLLib**.</span><span class="sxs-lookup"><span data-stu-id="948a7-105">For this article, we will start a Spark job using a notebook available with the Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="948a7-106">U kunt de onderstaande stappen voor het bijhouden van een toepassing die u verzonden met een andere benadering, bijvoorbeeld **spark indienen**.</span><span class="sxs-lookup"><span data-stu-id="948a7-106">You can use the steps below to track an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="948a7-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="948a7-107">Prerequisites</span></span>
<span data-ttu-id="948a7-108">U hebt het volgende:</span><span class="sxs-lookup"><span data-stu-id="948a7-108">You must have the following:</span></span>

* <span data-ttu-id="948a7-109">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="948a7-109">An Azure subscription.</span></span> <span data-ttu-id="948a7-110">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="948a7-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="948a7-111">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="948a7-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="948a7-112">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="948a7-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="948a7-113">U moet worden begonnen met de notebook uitgevoerd  **[Machine learning: Predictive Analytics op voeding inspectie gegevens met behulp van MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span><span class="sxs-lookup"><span data-stu-id="948a7-113">You should have started running the notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="948a7-114">Volg de koppeling voor instructies over het uitvoeren van deze laptop.</span><span class="sxs-lookup"><span data-stu-id="948a7-114">For instructions on how to run this notebook, follow the link.</span></span>  

## <a name="track-an-application-in-the-yarn-ui"></a><span data-ttu-id="948a7-115">Een toepassing in de gebruikersinterface van YARN bijhouden</span><span class="sxs-lookup"><span data-stu-id="948a7-115">Track an application in the YARN UI</span></span>
1. <span data-ttu-id="948a7-116">Start de gebruikersinterface van YARN.</span><span class="sxs-lookup"><span data-stu-id="948a7-116">Launch the YARN UI.</span></span> <span data-ttu-id="948a7-117">Klik in de cluster-blade op **Cluster-Dashboard**, en klik vervolgens op **YARN**.</span><span class="sxs-lookup"><span data-stu-id="948a7-117">From the cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![Gebruikersinterface van YARN starten](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="948a7-119">U kunt ook kunt u ook de gebruikersinterface van YARN van de Ambari UI starten.</span><span class="sxs-lookup"><span data-stu-id="948a7-119">Alternatively, you can also launch the YARN UI from the Ambari UI.</span></span> <span data-ttu-id="948a7-120">Start de UI Ambari van de cluster-blade, klikt u op **Cluster-Dashboard**, en klik vervolgens op **HDInsight-Cluster-Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="948a7-120">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="948a7-121">Klik op de UI Ambari **YARN**, klikt u op **snelkoppelingen**, klikt u op de actieve resourcemanager en klik vervolgens op **ResourceManager UI**.</span><span class="sxs-lookup"><span data-stu-id="948a7-121">From the Ambari UI, click **YARN**, click **Quick Links**, click the active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="948a7-122">Omdat u de Jupyter-notebooks met Spark-taak gestart, de toepassing heeft de naam **remotesparkmagics** (dit is de naam op voor alle toepassingen die worden gestart vanuit de laptops).</span><span class="sxs-lookup"><span data-stu-id="948a7-122">Because you started the Spark job using Jupyter notebooks, the application has the name **remotesparkmagics** (this is the name for all applications that are started from the notebooks).</span></span> <span data-ttu-id="948a7-123">Klik op de toepassings-ID op basis van de naam van de toepassing voor meer informatie over de taak.</span><span class="sxs-lookup"><span data-stu-id="948a7-123">Click the application ID against the application name to get more information about the job.</span></span> <span data-ttu-id="948a7-124">De toepassingsweergave wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="948a7-124">This launches the application view.</span></span>
   
    ![Spark toepassings-ID vinden](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="948a7-126">Voor dergelijke toepassingen die worden gestart vanuit de Jupyter-notebooks, is de status altijd **met** voordat u de notebook afgesloten.</span><span class="sxs-lookup"><span data-stu-id="948a7-126">For such applications that are launched from the Jupyter notebooks, the status is always **RUNNING** until you exit the notebook.</span></span>
3. <span data-ttu-id="948a7-127">Uit de toepassingsweergave, kunt u inzoomen verder uitzoeken de containers die zijn gekoppeld aan de toepassing en de logboeken (stdout/stderr).</span><span class="sxs-lookup"><span data-stu-id="948a7-127">From the application view, you can drill down further to find out the containers associated with the application and the logs (stdout/stderr).</span></span> <span data-ttu-id="948a7-128">U kunt de Spark-gebruikersinterface ook starten door te klikken op de koppeling die overeenkomt met de **bijhouden URL**, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="948a7-128">You can also launch the Spark UI by clicking the linking corresponding to the **Tracking URL**, as shown below.</span></span> 
   
    ![Container logboeken downloaden](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-the-spark-ui"></a><span data-ttu-id="948a7-130">Een toepassing in de gebruikersinterface van Spark bijhouden</span><span class="sxs-lookup"><span data-stu-id="948a7-130">Track an application in the Spark UI</span></span>
<span data-ttu-id="948a7-131">In de gebruikersinterface Spark, kunt u inzoomen op de Spark-taken die zijn geïnitieerd door de toepassing die u eerder hebt gestart.</span><span class="sxs-lookup"><span data-stu-id="948a7-131">In the Spark UI, you can drill down into the Spark jobs that are spawned by the application you started earlier.</span></span>

1. <span data-ttu-id="948a7-132">Start de Spark-gebruikersinterface uit de toepassingsweergave, klikt u op de koppeling tegen de **bijhouden URL**, zoals weergegeven in de bovenstaande schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="948a7-132">To launch the Spark UI, from the application view, click the link against the **Tracking URL**, as shown in the screen capture above.</span></span> <span data-ttu-id="948a7-133">U kunt alle Spark-taken die worden gestart door de toepassing die wordt uitgevoerd in de Jupyter-notebook kunt zien.</span><span class="sxs-lookup"><span data-stu-id="948a7-133">You can see all the Spark jobs that are launched by the application running in the Jupyter notebook.</span></span>
   
    ![Spark-taken weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="948a7-135">Klik op de **Executor** tabblad verwerking en opslag van gegevens voor elke executor kunt bekijken.</span><span class="sxs-lookup"><span data-stu-id="948a7-135">Click the **Executors** tab to see processing and storage information for each executor.</span></span> <span data-ttu-id="948a7-136">U kunt ook de aanroepstack ophalen door te klikken op de **Thread Dump** koppeling.</span><span class="sxs-lookup"><span data-stu-id="948a7-136">You can also retrieve the call stack by clicking on the **Thread Dump** link.</span></span>
   
    ![Spark Executor weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="948a7-138">Klik op de **fasen** tabblad voor een overzicht van de fasen die zijn gekoppeld aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="948a7-138">Click the **Stages** tab to see the stages associated with the application.</span></span>
   
    ![Spark fasen weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="948a7-140">Elk stadium kan hebben meerdere taken waarvoor u Uitvoeringsstatistieken, zoals weergeven kunt hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="948a7-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![Spark fasen weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="948a7-142">U kunt de detailpagina fase DAG visualisatie starten.</span><span class="sxs-lookup"><span data-stu-id="948a7-142">From the stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="948a7-143">Vouw de **DAG visualisatie** koppelen aan de bovenkant van de pagina, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="948a7-143">Expand the **DAG Visualization** link at the top of the page, as shown below.</span></span>
   
    ![Spark fasen DAG visualisatie weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="948a7-145">DAG of directe Aclyic grafiek vertegenwoordigt de verschillende fasen in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="948a7-145">DAG or Direct Aclyic Graph represents the different stages in the application.</span></span> <span data-ttu-id="948a7-146">Elke blauw vak in de grafiek vertegenwoordigt een Spark-bewerking aangeroepen vanuit de toepassing.</span><span class="sxs-lookup"><span data-stu-id="948a7-146">Each blue box in the graph represents a Spark operation invoked from the application.</span></span>
5. <span data-ttu-id="948a7-147">Op de pagina fase details kunt u ook de tijdlijnweergave toepassing starten.</span><span class="sxs-lookup"><span data-stu-id="948a7-147">From the stage details page, you can also launch the application timeline view.</span></span> <span data-ttu-id="948a7-148">Vouw de **gebeurtenis tijdlijn** koppelen aan de bovenkant van de pagina, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="948a7-148">Expand the **Event Timeline** link at the top of the page, as shown below.</span></span>
   
    ![Spark fasen gebeurtenis tijdlijn weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="948a7-150">Hiermee worden de gebeurtenissen Spark weergegeven in de vorm van een tijdlijn.</span><span class="sxs-lookup"><span data-stu-id="948a7-150">This displays the Spark events in the form of a timeline.</span></span> <span data-ttu-id="948a7-151">De tijdlijnweergave is beschikbaar op drie niveaus tussen jobs binnen een taak en binnen een fase.</span><span class="sxs-lookup"><span data-stu-id="948a7-151">The timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="948a7-152">De afbeelding hierboven worden de tijdlijnweergave voor een bepaald stadium.</span><span class="sxs-lookup"><span data-stu-id="948a7-152">The image above captures the timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="948a7-153">Als u selecteert de **zoomen inschakelen** selectievakje, kunt u bladeren naar links en naar rechts tussen de tijdlijnweergave.</span><span class="sxs-lookup"><span data-stu-id="948a7-153">If you select the **Enable zooming** check box, you can scroll left and right across the timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="948a7-154">Andere tabbladen in de gebruikersinterface van Spark bevatten nuttige informatie over het Spark-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="948a7-154">Other tabs in the Spark UI provide useful information about the Spark instance as well.</span></span>
   
   * <span data-ttu-id="948a7-155">Tabblad opslag - als de toepassing een RDDs maakt vindt u informatie over die in het tabblad opslag.</span><span class="sxs-lookup"><span data-stu-id="948a7-155">Storage tab - If your application creates an RDDs, you can find information about those in the Storage tab.</span></span>
   * <span data-ttu-id="948a7-156">Tabblad omgeving - op dit tabblad bevat veel nuttige informatie over uw Spark-exemplaar, zoals de</span><span class="sxs-lookup"><span data-stu-id="948a7-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as the</span></span> 
     * <span data-ttu-id="948a7-157">Versie van scala</span><span class="sxs-lookup"><span data-stu-id="948a7-157">Scala version</span></span>
     * <span data-ttu-id="948a7-158">Gebeurtenislogboek van directory die is gekoppeld aan het cluster</span><span class="sxs-lookup"><span data-stu-id="948a7-158">Event log directory associated with the cluster</span></span>
     * <span data-ttu-id="948a7-159">Het aantal kernen executor voor de toepassing</span><span class="sxs-lookup"><span data-stu-id="948a7-159">Number of executor cores for the application</span></span>
     * <span data-ttu-id="948a7-160">Enz.</span><span class="sxs-lookup"><span data-stu-id="948a7-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-the-spark-history-server"></a><span data-ttu-id="948a7-161">Voor meer informatie over voltooide taken met behulp van de Server van de geschiedenis van Spark</span><span class="sxs-lookup"><span data-stu-id="948a7-161">Find information about completed jobs using the Spark History Server</span></span>
<span data-ttu-id="948a7-162">Zodra een taak is voltooid, wordt de informatie over de taak permanent in de Server van de geschiedenis van Spark.</span><span class="sxs-lookup"><span data-stu-id="948a7-162">Once a job is completed, the information about the job is persisted in the Spark History Server.</span></span>

1. <span data-ttu-id="948a7-163">Start de Server van de Spark geschiedenis van de cluster-blade, klikt u op **Cluster-Dashboard**, en klik vervolgens op **Spark geschiedenis Server**.</span><span class="sxs-lookup"><span data-stu-id="948a7-163">To launch the Spark History Server, from the cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Spark geschiedenis Server starten](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="948a7-165">U kunt ook kunt u ook de Spark geschiedenis Server gebruikersinterface van de Ambari UI starten.</span><span class="sxs-lookup"><span data-stu-id="948a7-165">Alternatively, you can also launch the Spark History Server UI from the Ambari UI.</span></span> <span data-ttu-id="948a7-166">Start de UI Ambari van de cluster-blade, klikt u op **Cluster-Dashboard**, en klik vervolgens op **HDInsight-Cluster-Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="948a7-166">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="948a7-167">Klik op de UI Ambari **Spark**, klikt u op **snelkoppelingen**, en klik vervolgens op **Spark geschiedenis Server UI**.</span><span class="sxs-lookup"><span data-stu-id="948a7-167">From the Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="948a7-168">Hier ziet u de voltooide toepassingen vermeld.</span><span class="sxs-lookup"><span data-stu-id="948a7-168">You will see all the completed applications listed.</span></span> <span data-ttu-id="948a7-169">Klik op een toepassings-ID om in te zoomen in een toepassing voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="948a7-169">Click an application ID to drill down into an application for more info.</span></span>
   
    ![Spark geschiedenis Server starten](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="948a7-171">Zie ook</span><span class="sxs-lookup"><span data-stu-id="948a7-171">See also</span></span>
*  [<span data-ttu-id="948a7-172">Resources beheren voor het Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="948a7-172">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="948a7-173">Voor gegevensanalisten</span><span class="sxs-lookup"><span data-stu-id="948a7-173">For data analysts</span></span>

* [<span data-ttu-id="948a7-174">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="948a7-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="948a7-175">Spark met Machine Learning: Spark in HDInsight gebruiken om voedselinspectieresultaten te voorspellen</span><span class="sxs-lookup"><span data-stu-id="948a7-175">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="948a7-176">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="948a7-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="948a7-177">Analyse van Application Insights-telemetriegegevens met behulp van Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="948a7-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="948a7-178">Gebruik Caffe op Azure HDInsight Spark voor gedistribueerde grondige learning</span><span class="sxs-lookup"><span data-stu-id="948a7-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="948a7-179">Voor Spark-ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="948a7-179">For Spark developers</span></span>

* [<span data-ttu-id="948a7-180">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="948a7-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="948a7-181">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="948a7-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="948a7-182">De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om Spark Scala-toepassingen te maken en in te dienen</span><span class="sxs-lookup"><span data-stu-id="948a7-182">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="948a7-183">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="948a7-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="948a7-184">De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om op afstand fouten in Spark Scala-toepassingen op te lossen</span><span class="sxs-lookup"><span data-stu-id="948a7-184">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="948a7-185">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="948a7-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="948a7-186">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="948a7-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="948a7-187">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="948a7-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="948a7-188">Jupyter op uw computer installeren en verbinding maken met een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="948a7-188">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)



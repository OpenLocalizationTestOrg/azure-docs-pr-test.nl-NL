---
title: Apache Spark aaaDebug taken die worden uitgevoerd op Azure HDInsight | Microsoft Docs
description: Gebruikersinterface van YARN, Spark-UI en Spark geschiedenis tootrack en foutopsporing servertaken uitgevoerd op een Spark-cluster in Azure HDInsight gebruiken
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
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="c4b2c-103">Fouten opsporen in Apache Spark taken uitgevoerd op Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4b2c-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="c4b2c-104">In dit artikel leert u hoe tootrack en foutopsporing Spark taken worden uitgevoerd op HDInsight-clusters met Hallo gebruikersinterface van YARN Spark-gebruikersinterface en Hallo Spark geschiedenis Server.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-104">In this article you will learn how tootrack and debug Spark jobs running on HDInsight clusters using hello YARN UI, Spark UI, and hello Spark History Server.</span></span> <span data-ttu-id="c4b2c-105">Voor dit artikel gaat we een Spark-taak met een laptop beschikbaar met Hallo Spark-cluster, **Machine learning: Predictive Analytics op voeding inspectie gegevens met behulp van MLLib**.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-105">For this article, we will start a Spark job using a notebook available with hello Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="c4b2c-106">U kunt stappen hieronder tootrack een toepassing die u verzonden met een andere benadering, bijvoorbeeld hello gebruiken **spark indienen**.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-106">You can use hello steps below tootrack an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4b2c-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c4b2c-107">Prerequisites</span></span>
<span data-ttu-id="c4b2c-108">U moet Hallo volgende hebben:</span><span class="sxs-lookup"><span data-stu-id="c4b2c-108">You must have hello following:</span></span>

* <span data-ttu-id="c4b2c-109">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-109">An Azure subscription.</span></span> <span data-ttu-id="c4b2c-110">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="c4b2c-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="c4b2c-111">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="c4b2c-112">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="c4b2c-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="c4b2c-113">U moet hebben gestart Hallo-notebook  **[Machine learning: Predictive Analytics op voeding inspectie gegevens met behulp van MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-113">You should have started running hello notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="c4b2c-114">Voor instructies over het toorun deze laptop, volg Hallo koppeling.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-114">For instructions on how toorun this notebook, follow hello link.</span></span>  

## <a name="track-an-application-in-hello-yarn-ui"></a><span data-ttu-id="c4b2c-115">Een toepassing in de gebruikersinterface van YARN Hallo bijhouden</span><span class="sxs-lookup"><span data-stu-id="c4b2c-115">Track an application in hello YARN UI</span></span>
1. <span data-ttu-id="c4b2c-116">Start Hallo gebruikersinterface van YARN.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-116">Launch hello YARN UI.</span></span> <span data-ttu-id="c4b2c-117">Cluster-blade hello, klikt u op **Cluster-Dashboard**, en klik vervolgens op **YARN**.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-117">From hello cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![Gebruikersinterface van YARN starten](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="c4b2c-119">U kunt ook kunt u ook Hallo gebruikersinterface van YARN van Hallo Ambari UI starten.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-119">Alternatively, you can also launch hello YARN UI from hello Ambari UI.</span></span> <span data-ttu-id="c4b2c-120">toolaunch hello Ambari UI, cluster-blade hello, klikt u op **Cluster-Dashboard**, en klik vervolgens op **HDInsight-Cluster-Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-120">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="c4b2c-121">Hallo Ambari UI, klik op **YARN**, klikt u op **snelkoppelingen**op Hallo active resourcemanager en klik vervolgens op **ResourceManager UI**.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-121">From hello Ambari UI, click **YARN**, click **Quick Links**, click hello active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="c4b2c-122">Omdat u Hallo Spark taak met Jupyter-notebooks gestart, Hallo toepassing hello naam heeft **remotesparkmagics** (dit is de naam Hallo voor alle toepassingen die worden gestart vanaf Hallo notitieblokken).</span><span class="sxs-lookup"><span data-stu-id="c4b2c-122">Because you started hello Spark job using Jupyter notebooks, hello application has hello name **remotesparkmagics** (this is hello name for all applications that are started from hello notebooks).</span></span> <span data-ttu-id="c4b2c-123">Klik op Hallo toepassings-ID tegen Hallo toepassing naam tooget meer informatie over het Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-123">Click hello application ID against hello application name tooget more information about hello job.</span></span> <span data-ttu-id="c4b2c-124">Hallo toepassingsweergave wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-124">This launches hello application view.</span></span>
   
    ![Spark toepassings-ID vinden](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="c4b2c-126">Voor dergelijke toepassingen die worden gestart vanuit Jupyter-notebooks Hallo Hallo status is altijd **met** voordat u Hallo notebook afgesloten.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-126">For such applications that are launched from hello Jupyter notebooks, hello status is always **RUNNING** until you exit hello notebook.</span></span>
3. <span data-ttu-id="c4b2c-127">Uit de weergave van de toepassing hello, kunt u verder toofind uit Hallo containers die zijn gekoppeld aan het Hallo-Logboeken (stdout/stderr) en toepassing hello inzoomen.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-127">From hello application view, you can drill down further toofind out hello containers associated with hello application and hello logs (stdout/stderr).</span></span> <span data-ttu-id="c4b2c-128">U kunt ook Hallo Spark UI starten door te klikken op Hallo bijbehorende toohello koppelen **bijhouden URL**, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-128">You can also launch hello Spark UI by clicking hello linking corresponding toohello **Tracking URL**, as shown below.</span></span> 
   
    ![Container logboeken downloaden](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a><span data-ttu-id="c4b2c-130">Bijhouden van een toepassing in Hallo Spark-gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="c4b2c-130">Track an application in hello Spark UI</span></span>
<span data-ttu-id="c4b2c-131">In Hallo Spark-gebruikersinterface, kunt u inzoomen op Hallo Spark taken die zijn geïnitieerd door Hallo-toepassing die u eerder hebt gestart.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-131">In hello Spark UI, you can drill down into hello Spark jobs that are spawned by hello application you started earlier.</span></span>

1. <span data-ttu-id="c4b2c-132">toolaunch hello Spark-gebruikersinterface uit de weergave van de toepassing hello, klik op de koppeling Hallo tegen Hallo **bijhouden URL**, zoals weergegeven in de schermopname Hallo hierboven.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-132">toolaunch hello Spark UI, from hello application view, click hello link against hello **Tracking URL**, as shown in hello screen capture above.</span></span> <span data-ttu-id="c4b2c-133">Hier ziet u alle taken van de Hallo Spark dat door de toepassing hello die wordt uitgevoerd in de Jupyter-notebook Hallo worden gestart.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-133">You can see all hello Spark jobs that are launched by hello application running in hello Jupyter notebook.</span></span>
   
    ![Spark-taken weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="c4b2c-135">Klik op Hallo **Executor** toosee verwerking en opslag van gegevens voor elke executor tabblad.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-135">Click hello **Executors** tab toosee processing and storage information for each executor.</span></span> <span data-ttu-id="c4b2c-136">U kunt ook de aanroepstack Hallo ophalen door te klikken op Hallo **Thread Dump** koppeling.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-136">You can also retrieve hello call stack by clicking on hello **Thread Dump** link.</span></span>
   
    ![Spark Executor weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="c4b2c-138">Klik op Hallo **fasen** toosee Hallo fasen gekoppeld aan de toepassing hello tabblad.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-138">Click hello **Stages** tab toosee hello stages associated with hello application.</span></span>
   
    ![Spark fasen weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="c4b2c-140">Elk stadium kan hebben meerdere taken waarvoor u Uitvoeringsstatistieken, zoals weergeven kunt hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![Spark fasen weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="c4b2c-142">U kunt Hallo fase pagina met details DAG visualisatie starten.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-142">From hello stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="c4b2c-143">Vouw Hallo **DAG visualisatie** koppelen bovenaan Hallo Hallo pagina, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-143">Expand hello **DAG Visualization** link at hello top of hello page, as shown below.</span></span>
   
    ![Spark fasen DAG visualisatie weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="c4b2c-145">Vertegenwoordigt de verschillende stadia in Hallo toepassing hello DAG of directe Aclyic grafiek.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-145">DAG or Direct Aclyic Graph represents hello different stages in hello application.</span></span> <span data-ttu-id="c4b2c-146">Elke blauw vak in Hallo grafiek vertegenwoordigt een Spark-bewerking aangeroepen vanuit Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-146">Each blue box in hello graph represents a Spark operation invoked from hello application.</span></span>
5. <span data-ttu-id="c4b2c-147">Hallo fase pagina met details kunt u ook Hallo toepassing tijdlijnweergave starten.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-147">From hello stage details page, you can also launch hello application timeline view.</span></span> <span data-ttu-id="c4b2c-148">Vouw Hallo **gebeurtenis tijdlijn** koppelen bovenaan Hallo Hallo pagina, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-148">Expand hello **Event Timeline** link at hello top of hello page, as shown below.</span></span>
   
    ![Spark fasen gebeurtenis tijdlijn weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="c4b2c-150">Hiermee worden Hallo Spark gebeurtenissen weergegeven in de vorm Hallo van een tijdlijn.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-150">This displays hello Spark events in hello form of a timeline.</span></span> <span data-ttu-id="c4b2c-151">Hallo tijdlijnweergave is beschikbaar op drie niveaus tussen jobs binnen een taak en binnen een fase.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-151">hello timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="c4b2c-152">Hallo afbeelding hierboven vastgelegd Hallo tijdlijnweergave voor een bepaald stadium.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-152">hello image above captures hello timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="c4b2c-153">Als u Hallo selecteert **zoomen inschakelen** selectievakje, kunt u bladeren naar links en naar rechts over Hallo tijdlijnweergave.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-153">If you select hello **Enable zooming** check box, you can scroll left and right across hello timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="c4b2c-154">Andere tabbladen in Hallo Spark UI bevatten nuttige informatie over ook Hallo Spark-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-154">Other tabs in hello Spark UI provide useful information about hello Spark instance as well.</span></span>
   
   * <span data-ttu-id="c4b2c-155">Tabblad opslag - als de toepassing een RDDs maakt vindt u informatie over die in het tabblad Hallo-opslag.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-155">Storage tab - If your application creates an RDDs, you can find information about those in hello Storage tab.</span></span>
   * <span data-ttu-id="c4b2c-156">Tabblad omgeving - op dit tabblad bevat veel nuttige informatie over uw Spark-exemplaar, zoals Hallo</span><span class="sxs-lookup"><span data-stu-id="c4b2c-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as hello</span></span> 
     * <span data-ttu-id="c4b2c-157">Versie van scala</span><span class="sxs-lookup"><span data-stu-id="c4b2c-157">Scala version</span></span>
     * <span data-ttu-id="c4b2c-158">Gebeurtenislogboek van directory die is gekoppeld aan het Hallo-cluster</span><span class="sxs-lookup"><span data-stu-id="c4b2c-158">Event log directory associated with hello cluster</span></span>
     * <span data-ttu-id="c4b2c-159">Het aantal kernen voor toepassing hello executor</span><span class="sxs-lookup"><span data-stu-id="c4b2c-159">Number of executor cores for hello application</span></span>
     * <span data-ttu-id="c4b2c-160">Enz.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a><span data-ttu-id="c4b2c-161">Voor meer informatie over voltooide taken met behulp van Hallo Spark geschiedenis van Server</span><span class="sxs-lookup"><span data-stu-id="c4b2c-161">Find information about completed jobs using hello Spark History Server</span></span>
<span data-ttu-id="c4b2c-162">Zodra een taak is voltooid, wordt Hallo informatie over Hallo taak permanent in Hallo Spark geschiedenis Server.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-162">Once a job is completed, hello information about hello job is persisted in hello Spark History Server.</span></span>

1. <span data-ttu-id="c4b2c-163">toolaunch hello Spark geschiedenis Server, cluster-blade hello, klikt u op **Cluster-Dashboard**, en klik vervolgens op **Spark geschiedenis Server**.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-163">toolaunch hello Spark History Server, from hello cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Spark geschiedenis Server starten](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="c4b2c-165">U kunt ook kunt u ook Hallo Spark geschiedenis Server UI uit Hallo Ambari UI starten.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-165">Alternatively, you can also launch hello Spark History Server UI from hello Ambari UI.</span></span> <span data-ttu-id="c4b2c-166">toolaunch hello Ambari UI, cluster-blade hello, klikt u op **Cluster-Dashboard**, en klik vervolgens op **HDInsight-Cluster-Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-166">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="c4b2c-167">Hallo Ambari UI, klik op **Spark**, klikt u op **snelkoppelingen**, en klik vervolgens op **Spark geschiedenis Server UI**.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-167">From hello Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="c4b2c-168">Hier ziet u alle Hallo voltooid toepassingen vermeld.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-168">You will see all hello completed applications listed.</span></span> <span data-ttu-id="c4b2c-169">Op een aanvraag-ID toodrill omlaag in een toepassing voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c4b2c-169">Click an application ID toodrill down into an application for more info.</span></span>
   
    ![Spark geschiedenis Server starten](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="c4b2c-171">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c4b2c-171">See also</span></span>
*  [<span data-ttu-id="c4b2c-172">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4b2c-172">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="c4b2c-173">Voor gegevensanalisten</span><span class="sxs-lookup"><span data-stu-id="c4b2c-173">For data analysts</span></span>

* [<span data-ttu-id="c4b2c-174">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="c4b2c-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="c4b2c-175">Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="c4b2c-175">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="c4b2c-176">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4b2c-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="c4b2c-177">Analyse van Application Insights-telemetriegegevens met behulp van Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4b2c-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="c4b2c-178">Gebruik Caffe op Azure HDInsight Spark voor gedistribueerde grondige learning</span><span class="sxs-lookup"><span data-stu-id="c4b2c-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="c4b2c-179">Voor Spark-ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="c4b2c-179">For Spark developers</span></span>

* [<span data-ttu-id="c4b2c-180">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="c4b2c-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c4b2c-181">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="c4b2c-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="c4b2c-182">De invoegtoepassing HDInsight Tools voor IntelliJ IDEA toocreate en verzenden van Spark Scala-toepassingen</span><span class="sxs-lookup"><span data-stu-id="c4b2c-182">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="c4b2c-183">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="c4b2c-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="c4b2c-184">De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken</span><span class="sxs-lookup"><span data-stu-id="c4b2c-184">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="c4b2c-185">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4b2c-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="c4b2c-186">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4b2c-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="c4b2c-187">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="c4b2c-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="c4b2c-188">Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="c4b2c-188">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)



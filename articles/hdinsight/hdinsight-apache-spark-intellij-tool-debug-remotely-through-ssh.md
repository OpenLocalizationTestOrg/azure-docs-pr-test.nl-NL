---
title: 'Azure Toolkit voor IntelliJ: fouten opsporen in Spark scala-toepassingen op afstand via SSH | Microsoft Docs'
description: Stapsgewijze instructies voor hoe toouse HDInsight-hulpprogramma's in Azure Toolkit voor IntelliJ toodebug toepassingen op afstand op HDInsight-clusters via SSH
keywords: foutopsporing op afstand intellij, externe foutopsporing intellij, ssh, intellij, hdinsight, fouten opsporen in intellij, foutopsporing
services: hdinsight
documentationcenter: 
author: jejiang
manager: DJ
editor: Jenny Jiang
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 08/24/2017
ms.author: Jenny Jiang
ms.openlocfilehash: bf3ab9d04c2ff9fcb6bbbdeefb11f55a12fbd845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a><span data-ttu-id="0f3ac-104">Fouten opsporen in Spark scala-toepassingen op een HDInsight-cluster in Azure werkset voor IntelliJ via SSH</span><span class="sxs-lookup"><span data-stu-id="0f3ac-104">Debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH</span></span>

<span data-ttu-id="0f3ac-105">In dit artikel vindt u stapsgewijze instructies voor het HDInsight-hulpprogramma's in Azure Toolkit toouse voor IntelliJ toodebug toepassingen op afstand op een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-105">This article provides step-by-step guidance on how toouse HDInsight Tools in Azure Toolkit for IntelliJ toodebug applications remotely on an HDInsight cluster.</span></span> <span data-ttu-id="0f3ac-106">toodebug uw project, kunt u ook Hallo weergeven [fouten opsporen in HDInsight Spark-toepassingen met Azure Toolkit voor IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-106">toodebug your project, you can also view hello [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span></span>

<span data-ttu-id="0f3ac-107">**Vereisten**</span><span class="sxs-lookup"><span data-stu-id="0f3ac-107">**Prerequisites**</span></span>

* <span data-ttu-id="0f3ac-108">**HDInsight-hulpprogramma's in Azure Toolkit voor IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-108">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="0f3ac-109">Dit hulpprogramma maakt deel uit van Azure Toolkit voor IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-109">This tool is part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="0f3ac-110">Zie voor meer informatie [Azure Toolkit installeren voor IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span><span class="sxs-lookup"><span data-stu-id="0f3ac-110">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="0f3ac-111">**Azure Toolkit voor IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-111">**Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="0f3ac-112">Deze toolkit toocreate Spark scala-toepassingen gebruiken voor een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-112">Use this toolkit toocreate Spark applications for an HDInsight cluster.</span></span> <span data-ttu-id="0f3ac-113">Voor meer informatie instructies Hallo in [gebruik Azure Toolkit voor IntelliJ toocreate Spark scala-toepassingen voor een HDInsight-cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span><span class="sxs-lookup"><span data-stu-id="0f3ac-113">For more information, follow hello instructions in [Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span></span>
* <span data-ttu-id="0f3ac-114">**HDInsight SSH-service met gebruikersnaam en wachtwoord management**.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-114">**HDInsight SSH service with username and password management**.</span></span> <span data-ttu-id="0f3ac-115">Zie voor meer informatie [tooHDInsight (Hadoop) verbinding via SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) en [SSH gebruiken tunneling tooaccess Ambari web-UI, JobHistory, NameNode, Oozie en andere web-UI](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span><span class="sxs-lookup"><span data-stu-id="0f3ac-115">For more information, see [Connect tooHDInsight (Hadoop) by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Use SSH tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span></span> 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a><span data-ttu-id="0f3ac-116">Een Spark Scala-toepassing maken en te configureren voor foutopsporing op afstand</span><span class="sxs-lookup"><span data-stu-id="0f3ac-116">Create a Spark Scala application and configure it for remote debugging</span></span>

1. <span data-ttu-id="0f3ac-117">Start IntelliJ IDEA en maak vervolgens een project.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-117">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="0f3ac-118">In Hallo **nieuw Project** dialoogvenster vak, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="0f3ac-118">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="0f3ac-119">a.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-119">a.</span></span> <span data-ttu-id="0f3ac-120">Selecteer **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-120">Select **HDInsight**.</span></span> 

   <span data-ttu-id="0f3ac-121">b.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-121">b.</span></span> <span data-ttu-id="0f3ac-122">Selecteer een Java of Scala sjabloon op basis van uw voorkeur.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-122">Select a Java or Scala template based on your preference.</span></span> <span data-ttu-id="0f3ac-123">Selecteer tussen Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="0f3ac-123">Select between hello following options:</span></span>

      - <span data-ttu-id="0f3ac-124">**Spark in HDInsight (Scala)**</span><span class="sxs-lookup"><span data-stu-id="0f3ac-124">**Spark on HDInsight (Scala)**</span></span>

      - <span data-ttu-id="0f3ac-125">**Spark in HDInsight (Java)**</span><span class="sxs-lookup"><span data-stu-id="0f3ac-125">**Spark on HDInsight (Java)**</span></span>

      - <span data-ttu-id="0f3ac-126">**Spark in HDInsight-Cluster uitvoeren voorbeeld (Scala)**</span><span class="sxs-lookup"><span data-stu-id="0f3ac-126">**Spark on HDInsight Cluster Run Sample (Scala)**</span></span>

      <span data-ttu-id="0f3ac-127">In dit voorbeeld wordt een **Spark in HDInsight-Cluster uitvoeren voorbeeld (Scala)** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-127">This example uses a **Spark on HDInsight Cluster Run Sample (Scala)** template.</span></span>

   <span data-ttu-id="0f3ac-128">c.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-128">c.</span></span> <span data-ttu-id="0f3ac-129">In Hallo **Build hulpprogramma** lijst, selecteert u Hallo te volgen, op basis van tooyour nodig:</span><span class="sxs-lookup"><span data-stu-id="0f3ac-129">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      - <span data-ttu-id="0f3ac-130">**Maven**, voor ondersteuning van de wizard Scala project maken</span><span class="sxs-lookup"><span data-stu-id="0f3ac-130">**Maven**, for Scala project-creation wizard support</span></span>

      -  <span data-ttu-id="0f3ac-131">**SBT**, voor het beheren van Hallo afhankelijkheden en bouwen voor Hallo Scala project</span><span class="sxs-lookup"><span data-stu-id="0f3ac-131">**SBT**, for managing hello dependencies and building for hello Scala project</span></span> 

      ![Een debug-project maken](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   <span data-ttu-id="0f3ac-133">d.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-133">d.</span></span> <span data-ttu-id="0f3ac-134">Selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-134">Select **Next**.</span></span>     
 
3. <span data-ttu-id="0f3ac-135">In Hallo volgende **nieuw Project** venster Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="0f3ac-135">In hello next **New Project** window, do hello following:</span></span>

   ![Selecteer Hallo Spark-SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   <span data-ttu-id="0f3ac-137">a.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-137">a.</span></span> <span data-ttu-id="0f3ac-138">Voer een naam van het project en de projectlocatie.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-138">Enter a project name and project location.</span></span>

   <span data-ttu-id="0f3ac-139">b.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-139">b.</span></span> <span data-ttu-id="0f3ac-140">In Hallo **Project SDK** vervolgkeuzelijst, selecteer **Java 1.8** voor **2.x Spark** cluster of selecteer **Java 1.7** voor **Spark 1. x** cluster.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-140">In hello **Project SDK** drop-down list, select **Java 1.8** for **Spark 2.x** cluster or select **Java 1.7** for **Spark 1.x** cluster.</span></span>

   <span data-ttu-id="0f3ac-141">c.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-141">c.</span></span> <span data-ttu-id="0f3ac-142">In Hallo **Spark versie** vervolgkeuzelijst, Hallo Scala project maken wizard integreert de juiste versie Hallo voor Spark SDK en Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-142">In hello **Spark Version** drop-down list, hello Scala project creation wizard integrates hello correct version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="0f3ac-143">Als Hallo spark-cluster versie ouder dan 2.0 is, selecteert u **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-143">If hello spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="0f3ac-144">Selecteer anders **2.x Spark.**</span><span class="sxs-lookup"><span data-stu-id="0f3ac-144">Otherwise, select **Spark 2.x.**</span></span> <span data-ttu-id="0f3ac-145">In dit voorbeeld wordt **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-145">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

   <span data-ttu-id="0f3ac-146">d.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-146">d.</span></span> <span data-ttu-id="0f3ac-147">Selecteer **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-147">Select **Finish**.</span></span>

4. <span data-ttu-id="0f3ac-148">Selecteer **src** > **belangrijkste** > **scala** tooopen uw code in Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-148">Select **src** > **main** > **scala** tooopen your code in hello project.</span></span> <span data-ttu-id="0f3ac-149">In dit voorbeeld wordt Hallo **SparkCore_wasbloTest** script.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-149">This example uses hello **SparkCore_wasbloTest** script.</span></span>

5. <span data-ttu-id="0f3ac-150">Hallo tooaccess **configuraties bewerken** menu, selecteer Hallo-pictogram in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-150">tooaccess hello **Edit Configurations** menu, select hello icon in hello upper-right corner.</span></span> <span data-ttu-id="0f3ac-151">U kunt vanuit dit menu maken of bewerken Hallo configuraties voor foutopsporing op afstand.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-151">From this menu, you can create or edit hello configurations for remote debugging.</span></span>

   ![Configuraties bewerken](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. <span data-ttu-id="0f3ac-153">In Hallo **uitvoeren/Debug configuraties** in het dialoogvenster, selecteer Hallo plus -teken (**+**).</span><span class="sxs-lookup"><span data-stu-id="0f3ac-153">In hello **Run/Debug Configurations** dialog box, select hello plus sign (**+**).</span></span> <span data-ttu-id="0f3ac-154">Selecteer vervolgens Hallo **Submit Spark Job** optie.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-154">Then select hello **Submit Spark Job** option.</span></span>

   ![Nieuwe configuratie toevoegen](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. <span data-ttu-id="0f3ac-156">Geef gegevens voor **naam**, **Spark-cluster**, en **Main klassenaam**.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-156">Enter information for **Name**, **Spark cluster**, and **Main class name**.</span></span> <span data-ttu-id="0f3ac-157">Selecteer vervolgens **geavanceerde configuratie**.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-157">Then select **Advanced configuration**.</span></span> 

   ![Configuraties voor foutopsporing uitvoeren](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. <span data-ttu-id="0f3ac-159">In Hallo **Spark verzending van geavanceerde configuratie** dialoogvenster, **foutopsporing op afstand inschakelen Spark**.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-159">In hello **Spark Submission Advanced Configuration** dialog box, select **Enable Spark remote debug**.</span></span> <span data-ttu-id="0f3ac-160">Hallo-SSH-gebruikersnaam invoeren en een wachtwoord invoeren of een bestand met een persoonlijke sleutel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-160">Enter hello SSH username, and then enter a password or use a private key file.</span></span> <span data-ttu-id="0f3ac-161">toosave hello configuratie, selecteert u **OK**.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-161">toosave hello configuration, select **OK**.</span></span>

   ![Spark foutopsporing op afstand inschakelen](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. <span data-ttu-id="0f3ac-163">Hallo-configuratie wordt nu opgeslagen met de Hallo-naam die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-163">hello configuration is now saved with hello name you provided.</span></span> <span data-ttu-id="0f3ac-164">tooview configuratiedetails hello, selecteer Hallo configuratienaam.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-164">tooview hello configuration details, select hello configuration name.</span></span> <span data-ttu-id="0f3ac-165">toomake gewijzigd, schakelt u **configuraties bewerken**.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-165">toomake changes, select **Edit Configurations**.</span></span> 

10. <span data-ttu-id="0f3ac-166">Nadat u de configuratie-instellingen Hallo hebt voltooid, kunt u Hallo-project uitvoeren op externe Hallo-cluster of foutopsporing op afstand uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-166">After you complete hello configurations settings, you can run hello project against hello remote cluster or perform remote debugging.</span></span>

## <a name="learn-how-tooperform-remote-debugging"></a><span data-ttu-id="0f3ac-167">Meer informatie over hoe foutopsporing op afstand tooperform</span><span class="sxs-lookup"><span data-stu-id="0f3ac-167">Learn how tooperform remote debugging</span></span>
### <a name="scenario-1-perform-remote-run"></a><span data-ttu-id="0f3ac-168">Scenario 1: Extern uitvoeren uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0f3ac-168">Scenario 1: Perform remote run</span></span>

<span data-ttu-id="0f3ac-169">In deze sectie wordt uitgelegd hoe u dat toodebug stuurprogramma's en Executor.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-169">In this section, we show you how toodebug drivers and executors.</span></span>

    import org.apache.spark.{SparkConf, SparkContext}

    object LogQuery {
      val exampleApacheLogs = List(
        """10.10.10.10 - "FRED" [18/Jan/2013:17:56:07 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 315 "http://referall.com/" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.350 "-" - "" 265 923 934 ""
          | 62.24.11.25 images.com 1358492167 - Whatup""".stripMargin.lines.mkString,
        """10.10.10.10 - "FRED" [18/Jan/2013:18:02:37 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 306 "http:/referall.com" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.352 "-" - "" 256 977 988 ""
          | 0 73.23.2.15 images.com 1358492557 - Whatup""".stripMargin.lines.mkString
      )
      def main(args: Array[String]) {
        val sparkconf = new SparkConf().setAppName("Log Query")
        val sc = new SparkContext(sparkconf)
        val dataSet = sc.parallelize(exampleApacheLogs)
        // scalastyle:off
        val apacheLogRegex =
          """^([\d.]+) (\S+) (\S+) \[([\w\d:/]+\s[+\-]\d{4})\] "(.+?)" (\d{3}) ([\d\-]+) "([^"]+)" "([^"]+)".*""".r
        // scalastyle:on
        /** Tracks hello total query count and number of aggregate bytes for a particular group. */
        class Stats(val count: Int, val numBytes: Int) extends Serializable {
          def merge(other: Stats): Stats = new Stats(count + other.count, numBytes + other.numBytes)
          override def toString: String = "bytes=%s\tn=%s".format(numBytes, count)
        }
        def extractKey(line: String): (String, String, String) = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              if (user != "\"-\"") (ip, user, query)
              else (null, null, null)
            case _ => (null, null, null)
          }
        }
        def extractStats(line: String): Stats = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              new Stats(1, bytes.toInt)
            case _ => new Stats(1, 0)
          }
        }
        
        dataSet.map(line => (extractKey(line), extractStats(line)))
          .reduceByKey((a, b) => a.merge(b))
          .collect().foreach{
          case (user, query) => println("%s\t%s".format(user, query))}

        sc.stop()
      }
    }


1. <span data-ttu-id="0f3ac-170">Dingen instellen en selecteer vervolgens Hallo **Debug** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-170">Set up breaking points, and then select hello **Debug** icon.</span></span>

   ![Selecteer Hallo debug-pictogram](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. <span data-ttu-id="0f3ac-172">Als de uitvoering van het programma Hallo Hallo belangrijk punt bereikt, ziet u een **stuurprogramma** tabblad en de twee **Executor** tabbladen in Hallo **foutopsporingsprogramma** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-172">When hello program execution reaches hello breaking point, you see a **Driver** tab and two **Executor** tabs in hello **Debugger** pane.</span></span> <span data-ttu-id="0f3ac-173">Selecteer Hallo **hervatten programma** pictogram toocontinue Hallo code, die vervolgens de volgende onderbrekingspunt Hallo bereikt en is gericht op Hallo overeenkomt met **Executor** tabblad. U kunt logboekbestanden voor het uitvoeren voor overeenkomende Hallo Hallo bekijken **Console** tabblad.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-173">Select hello **Resume Program** icon toocontinue running hello code, which then reaches hello next breakpoint and focuses on hello corresponding **Executor** tab. You can review hello execution logs on hello corresponding **Console** tab.</span></span>

   ![Tabblad foutopsporing](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="0f3ac-175">Scenario 2: Voer foutopsporing op afstand en het verhelpen van problemen</span><span class="sxs-lookup"><span data-stu-id="0f3ac-175">Scenario 2: Perform remote debugging and bug fixing</span></span>
<span data-ttu-id="0f3ac-176">In deze sectie zien we u hoe toodynamically update Hallo variabelewaarde met behulp van Hallo IntelliJ foutopsporing mogelijkheid voor een eenvoudige oplossing.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-176">In this section, we show you how toodynamically update hello variable value by using hello IntelliJ debugging capability for a simple fix.</span></span> <span data-ttu-id="0f3ac-177">In de Hallo volgende codevoorbeeld, wordt een uitzondering opgetreden omdat Hallo doelbestand al bestaat.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-177">In hello following code example, an exception is thrown because hello target file already exists.</span></span>
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find hello rows that have only one digit in hello sixth column.
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)

            try {
              var target = "wasb:///HVACout2_testdebug1";
              rdd1.saveAsTextFile(target);
            } catch {
              case ex: Exception => {
                throw ex;
              }
            }
          }
        }


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="0f3ac-178">foutopsporing op afstand tooperform en het verhelpen van problemen</span><span class="sxs-lookup"><span data-stu-id="0f3ac-178">tooperform remote debugging and bug fixing</span></span>
1. <span data-ttu-id="0f3ac-179">Twee dingen instellen en selecteer vervolgens Hallo **Debug** pictogram toostart Hallo proces foutopsporing op afstand.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-179">Set up two breaking points, and then select hello **Debug** icon toostart hello remote debugging process.</span></span>

2. <span data-ttu-id="0f3ac-180">Hallo-code reageert op Hallo eerste belangrijk punt en Hallo-parameter en de variabele gegevens worden weergegeven in Hallo **variabelen** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-180">hello code stops at hello first breaking point, and hello parameter and variable information are shown in hello **Variables** pane.</span></span> 

3. <span data-ttu-id="0f3ac-181">Selecteer Hallo **hervatten programma** pictogram toocontinue.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-181">Select hello **Resume Program** icon toocontinue.</span></span> <span data-ttu-id="0f3ac-182">Hallo-code reageert op Hallo tweede punt.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-182">hello code stops at hello second point.</span></span> <span data-ttu-id="0f3ac-183">Hallo-uitzondering is opgetreden, zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-183">hello exception is caught as expected.</span></span>

  ![Genereert fout](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. <span data-ttu-id="0f3ac-185">Selecteer Hallo **hervatten programma** pictogram opnieuw.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-185">Select hello **Resume Program** icon again.</span></span> <span data-ttu-id="0f3ac-186">Hallo **HDInsight Spark verzending** venster een fout met 'job run is mislukt' weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-186">hello **HDInsight Spark Submission** window displays a "job run failed" error.</span></span>

  ![Verzending van de fout](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. <span data-ttu-id="0f3ac-188">toodynamically update Hallo variabelewaarde via Hallo IntelliJ foutopsporing functie, selecteer **Debug** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-188">toodynamically update hello variable value by using hello IntelliJ debugging capability, select **Debug** again.</span></span> <span data-ttu-id="0f3ac-189">Hallo **variabelen** deelvenster opnieuw wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-189">hello **Variables** pane appears again.</span></span> 

6. <span data-ttu-id="0f3ac-190">Klik met de rechtermuisknop Hallo doel op Hallo **Debug** tabblad en selecteer vervolgens **waarde instellen**.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-190">Right-click hello target on hello **Debug** tab, and then select **Set Value**.</span></span> <span data-ttu-id="0f3ac-191">Voer vervolgens een nieuwe waarde voor Hallo-variabele.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-191">Next, enter a new value for hello variable.</span></span> <span data-ttu-id="0f3ac-192">Selecteer vervolgens **Enter** toosave Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-192">Then select **Enter** toosave hello value.</span></span> 

  ![Waarde instellen](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. <span data-ttu-id="0f3ac-194">Selecteer Hallo **hervatten programma** pictogram toocontinue toorun Hallo programma.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-194">Select hello **Resume Program** icon toocontinue toorun hello program.</span></span> <span data-ttu-id="0f3ac-195">Dit moment is geen uitzondering opgetreden.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-195">This time, no exception is caught.</span></span> <span data-ttu-id="0f3ac-196">U kunt zien dat Hallo-project met succes wordt uitgevoerd zonder eventuele uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-196">You can see that hello project runs successfully without any exceptions.</span></span>

  ![Fouten opsporen in zonder uitzondering](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <span data-ttu-id="0f3ac-198"><a name="seealso"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0f3ac-198"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="0f3ac-199">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f3ac-199">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="0f3ac-200">Demo</span><span class="sxs-lookup"><span data-stu-id="0f3ac-200">Demo</span></span>
* <span data-ttu-id="0f3ac-201">Maak Scala project (video): [Spark Scala-toepassingen maken](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="0f3ac-201">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="0f3ac-202">Foutopsporing op afstand (video): [gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand op een HDInsight-cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="0f3ac-202">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="0f3ac-203">Scenario's</span><span class="sxs-lookup"><span data-stu-id="0f3ac-203">Scenarios</span></span>
* [<span data-ttu-id="0f3ac-204">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="0f3ac-204">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="0f3ac-205">Spark met Machine Learning: Spark in HDInsight tooanalyze bouwen met behulp van HVAC-gegevens temperatuur gebruiken</span><span class="sxs-lookup"><span data-stu-id="0f3ac-205">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="0f3ac-206">Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="0f3ac-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="0f3ac-207">Spark-Streaming: Spark in HDInsight toobuild realtime streamingtoepassingen gebruiken</span><span class="sxs-lookup"><span data-stu-id="0f3ac-207">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="0f3ac-208">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f3ac-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="0f3ac-209">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0f3ac-209">Create and run applications</span></span>
* [<span data-ttu-id="0f3ac-210">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="0f3ac-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="0f3ac-211">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="0f3ac-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="0f3ac-212">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="0f3ac-212">Tools and extensions</span></span>
* [<span data-ttu-id="0f3ac-213">Gebruik Azure Toolkit voor IntelliJ toocreate Spark scala-toepassingen voor een HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="0f3ac-213">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="0f3ac-214">Gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand via VPN-verbinding</span><span class="sxs-lookup"><span data-stu-id="0f3ac-214">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="0f3ac-215">Gebruik van HDInsight Tools voor IntelliJ met Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="0f3ac-215">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="0f3ac-216">HDInsight-hulpprogramma's gebruiken in Azure Toolkit voor Eclipse toocreate Spark scala-toepassingen</span><span class="sxs-lookup"><span data-stu-id="0f3ac-216">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="0f3ac-217">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f3ac-217">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="0f3ac-218">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight Hallo</span><span class="sxs-lookup"><span data-stu-id="0f3ac-218">Kernels available for Jupyter notebook in hello Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="0f3ac-219">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="0f3ac-219">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="0f3ac-220">Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="0f3ac-220">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="0f3ac-221">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="0f3ac-221">Manage resources</span></span>
* [<span data-ttu-id="0f3ac-222">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f3ac-222">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="0f3ac-223">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="0f3ac-223">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

---
title: aaaTroubleshoot YARN met behulp van Azure HDInsight | Microsoft Docs
description: Vind antwoorden op vragen over het werken met Apache Hadoop YARN en Azure HDInsight toocommon.
keywords: HDInsight, YARN Veelgestelde vragen over Azure, probleemoplossingsgids, veelgestelde vragen
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: F76786A9-99AB-4B85-9B15-CA03528FC4CD
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: 800d9738cb27e05a64db470ee58565af3b85aa99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a><span data-ttu-id="cea24-104">YARN oplossen met behulp van Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cea24-104">Troubleshoot YARN by using Azure HDInsight</span></span>

<span data-ttu-id="cea24-105">Meer informatie over de meestvoorkomende problemen Hallo en hun oplossingen bij het werken met Apache Hadoop YARN nettoladingen in Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="cea24-105">Learn about hello top issues and their resolutions when working with Apache Hadoop YARN payloads in Apache Ambari.</span></span>

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a><span data-ttu-id="cea24-106">Hoe maak een nieuwe YARN-wachtrij op een cluster</span><span class="sxs-lookup"><span data-stu-id="cea24-106">How do I create a new YARN queue on a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="cea24-107">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="cea24-107">Resolution steps</span></span> 

<span data-ttu-id="cea24-108">Gebruik Hallo volgende stappen in de Ambari toocreate een nieuwe YARN-wachtrij en saldo Hallo capaciteit verdeling over alle Hallo wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="cea24-108">Use hello following steps in Ambari toocreate a new YARN queue, and then balance hello capacity allocation among all hello queues.</span></span> 

<span data-ttu-id="cea24-109">In dit voorbeeld twee bestaande wachtrijen (**standaard** en **thriftsvr**) beide zijn gewijzigd van 50% capaciteit too25% capaciteit, waarmee Hallo nieuwe wachtrij (spark) 50% capaciteit.</span><span class="sxs-lookup"><span data-stu-id="cea24-109">In this example, two existing queues (**default** and **thriftsvr**) both are changed from 50% capacity too25% capacity, which gives hello new queue (spark) 50% capacity.</span></span>
| <span data-ttu-id="cea24-110">Wachtrij</span><span class="sxs-lookup"><span data-stu-id="cea24-110">Queue</span></span> | <span data-ttu-id="cea24-111">Capaciteit</span><span class="sxs-lookup"><span data-stu-id="cea24-111">Capacity</span></span> | <span data-ttu-id="cea24-112">Maximale capaciteit</span><span class="sxs-lookup"><span data-stu-id="cea24-112">Maximum capacity</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cea24-113">Standaard</span><span class="sxs-lookup"><span data-stu-id="cea24-113">default</span></span> | <span data-ttu-id="cea24-114">25%</span><span class="sxs-lookup"><span data-stu-id="cea24-114">25%</span></span> | <span data-ttu-id="cea24-115">50%</span><span class="sxs-lookup"><span data-stu-id="cea24-115">50%</span></span> |
| <span data-ttu-id="cea24-116">thrftsvr</span><span class="sxs-lookup"><span data-stu-id="cea24-116">thrftsvr</span></span> | <span data-ttu-id="cea24-117">25%</span><span class="sxs-lookup"><span data-stu-id="cea24-117">25%</span></span> | <span data-ttu-id="cea24-118">50%</span><span class="sxs-lookup"><span data-stu-id="cea24-118">50%</span></span> |
| <span data-ttu-id="cea24-119">Spark</span><span class="sxs-lookup"><span data-stu-id="cea24-119">spark</span></span> | <span data-ttu-id="cea24-120">50%</span><span class="sxs-lookup"><span data-stu-id="cea24-120">50%</span></span> | <span data-ttu-id="cea24-121">50%</span><span class="sxs-lookup"><span data-stu-id="cea24-121">50%</span></span> |

1. <span data-ttu-id="cea24-122">Selecteer Hallo **Ambari-weergaven** pictogram en selecteer vervolgens Hallo rasterpatroon.</span><span class="sxs-lookup"><span data-stu-id="cea24-122">Select hello **Ambari Views** icon, and then select hello grid pattern.</span></span> <span data-ttu-id="cea24-123">Selecteer vervolgens **YARN Queue Manager**.</span><span class="sxs-lookup"><span data-stu-id="cea24-123">Next, select **YARN Queue Manager**.</span></span>

    ![Selecteer Hallo Ambari-weergaven pictogram](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. <span data-ttu-id="cea24-125">Selecteer Hallo **standaard** wachtrij.</span><span class="sxs-lookup"><span data-stu-id="cea24-125">Select hello **default** queue.</span></span>

    ![Hallo wachtrij selecteren](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. <span data-ttu-id="cea24-127">Voor Hallo **standaard** wachtrij, wijzigt u Hallo **capaciteit** van 50% too25%.</span><span class="sxs-lookup"><span data-stu-id="cea24-127">For hello **default** queue, change hello **capacity** from 50% too25%.</span></span> <span data-ttu-id="cea24-128">Voor Hallo **thriftsvr** wachtrij, wijzigt u Hallo **capaciteit** too25%.</span><span class="sxs-lookup"><span data-stu-id="cea24-128">For hello **thriftsvr** queue, change hello **capacity** too25%.</span></span>

    ![Hallo capaciteit too25% voor Hallo standaard en thriftsvr wachtrijen wijzigen](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. <span data-ttu-id="cea24-130">selecteert u een nieuwe wachtrij toocreate **wachtrij toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cea24-130">toocreate a new queue, select **Add Queue**.</span></span>

    ![Selecteer een wachtrij toevoegen](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. <span data-ttu-id="cea24-132">Naam Hallo nieuwe wachtrij.</span><span class="sxs-lookup"><span data-stu-id="cea24-132">Name hello new queue.</span></span>

    ![Naam Hallo wachtrij Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. <span data-ttu-id="cea24-134">Hallo laat **capaciteit** waarden op 50% en selecteer vervolgens Hallo **acties** knop.</span><span class="sxs-lookup"><span data-stu-id="cea24-134">Leave hello **capacity** values at 50%, and then select hello **Actions** button.</span></span>

    ![Selecteer de actieknop Hallo](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. <span data-ttu-id="cea24-136">Selecteer **opslaan en vernieuw wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="cea24-136">Select **Save and Refresh Queues**.</span></span>

    ![Selecteer opslaan en wachtrijen vernieuwen](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

<span data-ttu-id="cea24-138">Deze wijzigingen zijn onmiddellijk op Hallo YARN Scheduler UI zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="cea24-138">These changes are visible immediately on hello YARN Scheduler UI.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="cea24-139">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="cea24-139">Additional reading</span></span>

- [<span data-ttu-id="cea24-140">YARN CapacityScheduler</span><span class="sxs-lookup"><span data-stu-id="cea24-140">YARN CapacityScheduler</span></span>](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a><span data-ttu-id="cea24-141">Hoe kan ik YARN-logboeken downloaden vanaf een cluster</span><span class="sxs-lookup"><span data-stu-id="cea24-141">How do I download YARN logs from a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="cea24-142">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="cea24-142">Resolution steps</span></span> 

1. <span data-ttu-id="cea24-143">Verbinding toohello HDInsight-cluster via een Secure Shell (SSH)-client.</span><span class="sxs-lookup"><span data-stu-id="cea24-143">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="cea24-144">Zie voor meer informatie [lezen van aanvullende](#additional-reading-2).</span><span class="sxs-lookup"><span data-stu-id="cea24-144">For more information, see [Additional reading](#additional-reading-2).</span></span>

2. <span data-ttu-id="cea24-145">toolist alle toepassings-id's van Hallo YARN toepassingen die momenteel worden uitgevoerd, Hallo Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="cea24-145">toolist all hello application IDs of hello YARN applications that are currently running, run hello following command:</span></span>

    ```apache
    yarn top
    ```
    <span data-ttu-id="cea24-146">Hallo-id's vermeld in Hallo **APPLICATIONID** kolom.</span><span class="sxs-lookup"><span data-stu-id="cea24-146">hello IDs are listed in hello **APPLICATIONID** column.</span></span> <span data-ttu-id="cea24-147">U kunt Logboeken downloaden van Hallo **APPLICATIONID** kolom.</span><span class="sxs-lookup"><span data-stu-id="cea24-147">You can download logs from hello **APPLICATIONID** column.</span></span>

    ```apache
    YARN top - 18:00:07, up 19d, 0:14, 0 active users, queue(s): root
    NodeManager(s): 4 total, 4 active, 0 unhealthy, 0 decommissioned, 0 lost, 0 rebooted
    Queue(s) Applications: 2 running, 10 submitted, 0 pending, 8 completed, 0 killed, 0 failed
    Queue(s) Mem(GB): 97 available, 3 allocated, 0 pending, 0 reserved
    Queue(s) VCores: 58 available, 2 allocated, 0 pending, 0 reserved
    Queue(s) Containers: 2 allocated, 0 pending, 0 reserved

                      APPLICATIONID USER             TYPE      QUEUE   #CONT  #RCONT  VCORES RVCORES     MEM    RMEM  VCORESECS    MEMSECS %PROGR       TIME NAME
     application_1490377567345_0007 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628407    2442611  10.00   18:20:20 Thrift JDBC/ODBC Server
     application_1490377567345_0006 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628430    2442645  10.00   18:20:20 Thrift JDBC/ODBC Server
    ```

3. <span data-ttu-id="cea24-148">toodownload YARN-logboeken voor container voor alle toepassing modellen Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="cea24-148">toodownload YARN container logs for all application masters, use hello following command:</span></span>
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    <span data-ttu-id="cea24-149">Met deze opdracht maakt een logbestand met de naam amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="cea24-149">This command creates a log file named amlogs.txt.</span></span> 

4. <span data-ttu-id="cea24-150">toodownload YARN-logboeken voor container voor alleen Hallo nieuwste toepassing master, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="cea24-150">toodownload YARN container logs for only hello latest application master, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    <span data-ttu-id="cea24-151">Met deze opdracht maakt een logbestand met de naam latestamlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="cea24-151">This command creates a log file named latestamlogs.txt.</span></span> 

4. <span data-ttu-id="cea24-152">toodownload YARN-logboeken voor container voor de eerste twee toepassing modellen Hallo Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="cea24-152">toodownload YARN container logs for hello first two application masters, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    <span data-ttu-id="cea24-153">Met deze opdracht maakt een logbestand met de naam first2amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="cea24-153">This command creates a log file named first2amlogs.txt.</span></span> 

5. <span data-ttu-id="cea24-154">toodownload alle YARN-Logboeken in container gebruiken Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="cea24-154">toodownload all YARN container logs, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    <span data-ttu-id="cea24-155">Met deze opdracht maakt een logbestand met de naam logs.txt.</span><span class="sxs-lookup"><span data-stu-id="cea24-155">This command creates a log file named logs.txt.</span></span> 

6. <span data-ttu-id="cea24-156">toodownload hello YARN container logboek voor een specifieke container, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="cea24-156">toodownload hello YARN container log for a specific container, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    <span data-ttu-id="cea24-157">Met deze opdracht maakt een logbestand met de naam containerlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="cea24-157">This command creates a log file named containerlogs.txt.</span></span>

### <span data-ttu-id="cea24-158"><a name="additional-reading-2"></a>Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="cea24-158"><a name="additional-reading-2"></a>Additional reading</span></span>

- [<span data-ttu-id="cea24-159">TooHDInsight (Hadoop) verbinding via SSH</span><span class="sxs-lookup"><span data-stu-id="cea24-159">Connect tooHDInsight (Hadoop) by using SSH</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [<span data-ttu-id="cea24-160">Apache Hadoop YARN-concepten en toepassingen</span><span class="sxs-lookup"><span data-stu-id="cea24-160">Apache Hadoop YARN concepts and applications</span></span>](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)








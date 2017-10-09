---
title: websitelogboeken aaaAnalyze met Python-bibliotheken in Spark - Azure | Microsoft Docs
description: Deze laptop laat zien hoe de gegevens met een aangepaste bibliotheek met Spark op Azure HDInsight voor het vastleggen van tooanalyze.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="1358c-103">Websitelogboeken analyseren met een aangepaste Python-bibliotheek met Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1358c-103">Analyze website logs using a custom Python library with Spark cluster on HDInsight</span></span>

<span data-ttu-id="1358c-104">Deze laptop laat zien hoe de gegevens met een aangepaste bibliotheek met Spark in HDInsight voor het vastleggen van tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="1358c-104">This notebook demonstrates how tooanalyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="1358c-105">de aangepaste bibliotheek Hello we gebruiken is een Python-bibliotheek aangeroepen **iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="1358c-105">hello custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="1358c-106">Deze zelfstudie is ook beschikbaar als een Jupyter-notebook op een cluster Spark (Linux) die u in HDInsight maakt.</span><span class="sxs-lookup"><span data-stu-id="1358c-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="1358c-107">Hallo-notebook ervaring kunt u Hallo Python codefragmenten uit Hallo laptop zelf uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1358c-107">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="1358c-108">tooperform hello zelfstudie uit binnen een laptop, een Spark-cluster maken, een Jupyter-notebook starten (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), en voer vervolgens de notebook Hallo **logboeken analyseren met behulp van een aangepaste library.ipynb Spark** onder Hallo  **PySpark** map.</span><span class="sxs-lookup"><span data-stu-id="1358c-108">tooperform hello tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run hello notebook **Analyze logs with Spark using a custom library.ipynb** under hello **PySpark** folder.</span></span>
>
>

<span data-ttu-id="1358c-109">**Vereisten:**</span><span class="sxs-lookup"><span data-stu-id="1358c-109">**Prerequisites:**</span></span>

<span data-ttu-id="1358c-110">U moet Hallo volgende hebben:</span><span class="sxs-lookup"><span data-stu-id="1358c-110">You must have hello following:</span></span>

* <span data-ttu-id="1358c-111">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1358c-111">An Azure subscription.</span></span> <span data-ttu-id="1358c-112">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="1358c-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="1358c-113">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1358c-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="1358c-114">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="1358c-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="1358c-115">Onbewerkte gegevens opslaan als een RDD</span><span class="sxs-lookup"><span data-stu-id="1358c-115">Save raw data as an RDD</span></span>
<span data-ttu-id="1358c-116">In deze sectie gebruiken we Hallo [Jupyter](https://jupyter.org) laptop die is gekoppeld aan een Apache Spark-cluster in HDInsight toorun taken die uw onbewerkte voorbeeldgegevens verwerken en opslaan als een Hive-tabel.</span><span class="sxs-lookup"><span data-stu-id="1358c-116">In this section, we use hello [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight toorun jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="1358c-117">Hallo voorbeeldgegevens is een CSV-bestand (hvac.csv) beschikbaar in alle clusters standaard.</span><span class="sxs-lookup"><span data-stu-id="1358c-117">hello sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="1358c-118">Nadat uw gegevens wordt opgeslagen als een Hive-tabel, in de volgende sectie Hallo er wordt verbinding gemaakt toohello Hive-tabel met BI-hulpprogramma's als Power BI en Tableau.</span><span class="sxs-lookup"><span data-stu-id="1358c-118">Once your data is saved as a Hive table, in hello next section we will connect toohello Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="1358c-119">Van Hallo [Azure-portal](https://portal.azure.com/), vanaf Hallo startboard, klikt u op Hallo tegel voor uw Spark-cluster (als u toohello startboard vastgemaakt).</span><span class="sxs-lookup"><span data-stu-id="1358c-119">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="1358c-120">U kunt ook tooyour cluster onder navigeren **door alles bladeren** > **HDInsight-Clusters**.</span><span class="sxs-lookup"><span data-stu-id="1358c-120">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="1358c-121">Klik op Hallo blade Spark-cluster **Cluster-Dashboard**, en klik vervolgens op **Jupyter-Notebook**.</span><span class="sxs-lookup"><span data-stu-id="1358c-121">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="1358c-122">Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="1358c-122">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1358c-123">U mogelijk ook Hallo Jupyter-Notebook voor uw cluster door de volgende URL in uw browser openen-Hallo bereiken.</span><span class="sxs-lookup"><span data-stu-id="1358c-123">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="1358c-124">Vervang **CLUSTERNAME** met Hallo-naam van het cluster:</span><span class="sxs-lookup"><span data-stu-id="1358c-124">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="1358c-125">Maak een nieuwe notebook.</span><span class="sxs-lookup"><span data-stu-id="1358c-125">Create a new notebook.</span></span> <span data-ttu-id="1358c-126">Klik op **Nieuw** en klik vervolgens op **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="1358c-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="1358c-127">![Een nieuwe Jupyter-notebook maken](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Een nieuwe Jupyter-notebook maken")</span><span class="sxs-lookup"><span data-stu-id="1358c-127">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="1358c-128">Een nieuwe notebook gemaakt en geopend met de Hallo naam Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="1358c-128">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="1358c-129">Klik op Hallo notebook naam Hallo boven en een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="1358c-129">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="1358c-130">![Geef een naam voor de notebook Hallo](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Geef een naam voor de notebook Hallo")</span><span class="sxs-lookup"><span data-stu-id="1358c-130">![Provide a name for hello notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Provide a name for hello notebook")</span></span>
5. <span data-ttu-id="1358c-131">Omdat u de notebook met behulp van Hallo PySpark-kernel hebt gemaakt, hoeft u geen toocreate contexten expliciet.</span><span class="sxs-lookup"><span data-stu-id="1358c-131">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="1358c-132">Hallo Spark en Hive-contexten worden automatisch voor u gemaakt wanneer u de eerste codecel Hallo uitvoert.</span><span class="sxs-lookup"><span data-stu-id="1358c-132">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="1358c-133">U kunt starten door het Hallo-typen die vereist voor dit scenario zijn te importeren.</span><span class="sxs-lookup"><span data-stu-id="1358c-133">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="1358c-134">Plak Hallo volgende codefragment in een lege cel en druk vervolgens op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="1358c-134">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="1358c-135">Maak een RDD Hallo logboek voorbeeldgegevens gebruikt al beschikbaar op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="1358c-135">Create an RDD using hello sample log data already available on hello cluster.</span></span> <span data-ttu-id="1358c-136">U toegang hebt tot Hallo-gegevens in die zijn gekoppeld aan het cluster op Hallo Hallo standaardopslagaccount **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span><span class="sxs-lookup"><span data-stu-id="1358c-136">You can access hello data in hello default storage account associated with hello cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="1358c-137">Haal die een voorbeeldlogboek ingesteld tooverify die Hallo vorige stap is voltooid.</span><span class="sxs-lookup"><span data-stu-id="1358c-137">Retrieve a sample log set tooverify that hello previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="1358c-138">U ziet een uitvoer vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="1358c-138">You should see an output similar toohello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="1358c-139">Analyseren van gegevens aan het logboek met een aangepaste Python-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="1358c-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="1358c-140">In bovenstaande Hallo uitvoer, de eerste paar regels Hallo Hallo koptekstgegevens opnemen en elke resterende regel overeenkomt met Hallo schema beschreven in deze header.</span><span class="sxs-lookup"><span data-stu-id="1358c-140">In hello output above, hello first couple lines include hello header information and each remaining line matches hello schema described in that header.</span></span> <span data-ttu-id="1358c-141">Deze logboeken parseren kan ingewikkeld zijn.</span><span class="sxs-lookup"><span data-stu-id="1358c-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="1358c-142">Ja, gebruiken we een aangepaste Python-bibliotheek (**iislogparser.py**) op die manier kunt dergelijke eenvoudiger logboeken parseren.</span><span class="sxs-lookup"><span data-stu-id="1358c-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="1358c-143">Deze bibliotheek is standaard opgenomen in uw Spark-cluster in HDInsight op **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="1358c-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="1358c-144">Deze bibliotheek is echter niet in Hallo `PYTHONPATH` zodat we kan niet worden gebruikt door het gebruik van een instructie importeren zoals `import iislogparser`.</span><span class="sxs-lookup"><span data-stu-id="1358c-144">However, this library is not in hello `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="1358c-145">toouse deze bibliotheek we tooall Hallo worker-knooppunten moet distribueren.</span><span class="sxs-lookup"><span data-stu-id="1358c-145">toouse this library, we must distribute it tooall hello worker nodes.</span></span> <span data-ttu-id="1358c-146">Hallo volgende codefragment worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1358c-146">Run hello following snippet.</span></span>

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="1358c-147">`iislogparser`biedt een functie `parse_log_line` die retourneert `None` als een regel van een veldnamenrij is en een exemplaar van Hallo retourneert `LogLine` klasse als een regel worden ontdekt.</span><span class="sxs-lookup"><span data-stu-id="1358c-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of hello `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="1358c-148">Gebruik Hallo `LogLine` klasse tooextract Hallo alleen logboek regels uit Hallo RDD:</span><span class="sxs-lookup"><span data-stu-id="1358c-148">Use hello `LogLine` class tooextract only hello log lines from hello RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="1358c-149">Ophalen van een aantal uitgepakte logboek regels tooverify die Hallo stap is voltooid.</span><span class="sxs-lookup"><span data-stu-id="1358c-149">Retrieve a couple of extracted log lines tooverify that hello step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="1358c-150">Hallo-uitvoer moet vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="1358c-150">hello output should be similar toohello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="1358c-151">Hallo `LogLine` op zijn beurt, is enkele nuttige methoden zoals klasse, `is_error()`, die of een logboekvermelding een foutcode heeft retourneert.</span><span class="sxs-lookup"><span data-stu-id="1358c-151">hello `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="1358c-152">Gebruik deze toocompute Hallo aantal fouten in Hallo uitgepakt logboek regels en meld u vervolgens alle Hallo fouten tooa ander bestand.</span><span class="sxs-lookup"><span data-stu-id="1358c-152">Use this toocompute hello number of errors in hello extracted log lines, and then log all hello errors tooa different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="1358c-153">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="1358c-153">You should see an output like hello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="1358c-154">U kunt ook **Matplotlib** tooconstruct een visualisatie van Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="1358c-154">You can also use **Matplotlib** tooconstruct a visualization of hello data.</span></span> <span data-ttu-id="1358c-155">Bijvoorbeeld, als u tooisolate Hallo oorzaak van aanvragen die gedurende lange tijd worden uitgevoerd wilt, kunt u toofind Hallo bestanden die Hallo gemiddeld tooserve voor de meeste tijd duren.</span><span class="sxs-lookup"><span data-stu-id="1358c-155">For example, if you want tooisolate hello cause of requests that run for a long time, you might want toofind hello files that take hello most time tooserve on average.</span></span>
   <span data-ttu-id="1358c-156">Hallo codefragment onderstaande Hallo bovenste 25 resources die een aanvraag voor de meeste tijd tooserve duurde opgehaald.</span><span class="sxs-lookup"><span data-stu-id="1358c-156">hello snippet below retrieves hello top 25 resources that took most time tooserve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="1358c-157">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="1358c-157">You should see an output like hello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. <span data-ttu-id="1358c-158">U kunt ook deze informatie in de vorm Hallo van tekent aanwezig.</span><span class="sxs-lookup"><span data-stu-id="1358c-158">You can also present this information in hello form of plot.</span></span> <span data-ttu-id="1358c-159">Als een eerste stap toocreate tekent laat het ons een tijdelijke tabel maakt **AverageTime**.</span><span class="sxs-lookup"><span data-stu-id="1358c-159">As a first step toocreate a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="1358c-160">Hallo tabel groepen Hallo registreert tijd toosee als er een ongebruikelijke latentiepieken op een willekeurig moment.</span><span class="sxs-lookup"><span data-stu-id="1358c-160">hello table groups hello logs by time toosee if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="1358c-161">Vervolgens kunt u uitvoeren Hallo SQL query tooget na alle Hallo records in Hallo **AverageTime** tabel.</span><span class="sxs-lookup"><span data-stu-id="1358c-161">You can then run hello following SQL query tooget all hello records in hello **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="1358c-162">Hallo `%%sql` magic gevolgd door `-o averagetime` zorgt ervoor dat Hallo-uitvoer van Hallo query lokaal worden bewaard op Hallo Jupyter-server (meestal Hallo headnode van Hallo cluster).</span><span class="sxs-lookup"><span data-stu-id="1358c-162">hello `%%sql` magic followed by `-o averagetime` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="1358c-163">Hallo-uitvoer is doorgevoerd als een [Pandas](http://pandas.pydata.org/) dataframe Hello naam opgegeven **averagetime**.</span><span class="sxs-lookup"><span data-stu-id="1358c-163">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **averagetime**.</span></span>

   <span data-ttu-id="1358c-164">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="1358c-164">You should see an output like hello following:</span></span>

   <span data-ttu-id="1358c-165">![Uitvoer van de SQL-query](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "uitvoer van de SQL-query")</span><span class="sxs-lookup"><span data-stu-id="1358c-165">![SQL query output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL query output")</span></span>

   <span data-ttu-id="1358c-166">Voor meer informatie over Hallo `%%sql` magic, Zie [Parameters ondersteund Hello %% sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="1358c-166">For more information about hello `%%sql` magic, see [Parameters supported with hello %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="1358c-167">U kunt nu Matplotlib gebruiken, een bibliotheek tooconstruct visualisatie van gegevens, toocreate tekent gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1358c-167">You can now use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="1358c-168">Omdat Hallo grafiek moet worden gemaakt van Hallo lokaal persistent **averagetime** dataframe, Hallo codefragment moet beginnen met Hallo `%%local` verwerkt Magic-pakket.</span><span class="sxs-lookup"><span data-stu-id="1358c-168">Because hello plot must be created from hello locally persisted **averagetime** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="1358c-169">Dit zorgt ervoor dat Hallo-code op Hallo Jupyter server lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1358c-169">This ensures that hello code is run locally on hello Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="1358c-170">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="1358c-170">You should see an output like hello following:</span></span>

   <span data-ttu-id="1358c-171">![Uitvoer Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib uitvoer")</span><span class="sxs-lookup"><span data-stu-id="1358c-171">![Matplotlib output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="1358c-172">Als u klaar bent met het uitvoeren van de toepassing hello moet afsluiten Hallo notebook toorelease Hallo resources.</span><span class="sxs-lookup"><span data-stu-id="1358c-172">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="1358c-173">toodo geval is, uit Hallo **bestand** menu op Hallo laptop, klikt u op **sluiten en stoppen**.</span><span class="sxs-lookup"><span data-stu-id="1358c-173">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="1358c-174">Deze wordt afgesloten en sluiten Hallo notebook.</span><span class="sxs-lookup"><span data-stu-id="1358c-174">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="1358c-175"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="1358c-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="1358c-176">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1358c-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="1358c-177">Scenario's</span><span class="sxs-lookup"><span data-stu-id="1358c-177">Scenarios</span></span>
* [<span data-ttu-id="1358c-178">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="1358c-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="1358c-179">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="1358c-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="1358c-180">Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="1358c-180">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="1358c-181">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="1358c-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="1358c-182">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1358c-182">Create and run applications</span></span>
* [<span data-ttu-id="1358c-183">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="1358c-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="1358c-184">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="1358c-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="1358c-185">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="1358c-185">Tools and extensions</span></span>
* [<span data-ttu-id="1358c-186">De invoegtoepassing HDInsight Tools voor IntelliJ IDEA toocreate en verzenden van Spark Scala-toepassingen</span><span class="sxs-lookup"><span data-stu-id="1358c-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="1358c-187">De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken</span><span class="sxs-lookup"><span data-stu-id="1358c-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="1358c-188">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1358c-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="1358c-189">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="1358c-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="1358c-190">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="1358c-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="1358c-191">Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="1358c-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="1358c-192">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="1358c-192">Manage resources</span></span>
* [<span data-ttu-id="1358c-193">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1358c-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="1358c-194">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="1358c-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

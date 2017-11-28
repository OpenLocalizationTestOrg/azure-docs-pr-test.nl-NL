---
title: aaaUse Zeppelin-notebooks met Apache Spark in Azure HDInsight-cluster | Microsoft Docs
description: Stapsgewijze instructies over hoe toouse Zeppelin-notebooks met Apache Spark in Azure HDInsight-clusters.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="972b1-103">Zeppelin-notebooks met Apache Spark-cluster in Azure HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="972b1-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="972b1-104">HDInsight Spark-clusters bevatten Zeppelin-notebooks waarmee u toorun Spark taken kunt.</span><span class="sxs-lookup"><span data-stu-id="972b1-104">HDInsight Spark clusters include Zeppelin notebooks that you can use toorun Spark jobs.</span></span> <span data-ttu-id="972b1-105">In dit artikel leert u hoe toouse Hallo Zeppelin laptop op een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="972b1-105">In this article, you learn how toouse hello Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="972b1-106">Zeppelin-notebooks zijn alleen beschikbaar voor Spark 1.6.3 in HDInsight 3.5 en Spark 2.1.0 in HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="972b1-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="972b1-107">**Vereisten:**</span><span class="sxs-lookup"><span data-stu-id="972b1-107">**Prerequisites:**</span></span>

* <span data-ttu-id="972b1-108">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="972b1-108">An Azure subscription.</span></span> <span data-ttu-id="972b1-109">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="972b1-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="972b1-110">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="972b1-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="972b1-111">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="972b1-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="972b1-112">Een laptop Zeppelin starten</span><span class="sxs-lookup"><span data-stu-id="972b1-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="972b1-113">Klik op Hallo blade Spark-cluster **Cluster-Dashboard**, en klik vervolgens op **Zeppelin-Notebook**.</span><span class="sxs-lookup"><span data-stu-id="972b1-113">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="972b1-114">Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="972b1-114">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="972b1-115">U mogelijk ook Hallo Zeppelin-Notebook voor uw cluster door de volgende URL in uw browser openen-Hallo bereiken.</span><span class="sxs-lookup"><span data-stu-id="972b1-115">You may also reach hello Zeppelin Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="972b1-116">Vervang **CLUSTERNAME** met Hallo-naam van het cluster:</span><span class="sxs-lookup"><span data-stu-id="972b1-116">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="972b1-117">Maak een nieuwe notebook.</span><span class="sxs-lookup"><span data-stu-id="972b1-117">Create a new notebook.</span></span> <span data-ttu-id="972b1-118">Hallo-headerdeelvenster, klik op **Notebook**, en klik vervolgens op **nieuwe notitie maken**.</span><span class="sxs-lookup"><span data-stu-id="972b1-118">From hello header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="972b1-119">![Maak een nieuwe Zeppelin-notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "een nieuwe Zeppelin-notebook maken")</span><span class="sxs-lookup"><span data-stu-id="972b1-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="972b1-120">Voer een naam voor de notebook Hallo en klik vervolgens op **opmerking maken**.</span><span class="sxs-lookup"><span data-stu-id="972b1-120">Enter a name for hello notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="972b1-121">Zorg er ook Hallo notebook header toont een verbonden status.</span><span class="sxs-lookup"><span data-stu-id="972b1-121">Also, make sure hello notebook header shows a connected status.</span></span> <span data-ttu-id="972b1-122">Dit wordt aangeduid met een groen punt in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="972b1-122">It is denoted by a green dot in hello top-right corner.</span></span>
   
    <span data-ttu-id="972b1-123">![Zeppelin-notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin-notebook status")</span><span class="sxs-lookup"><span data-stu-id="972b1-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="972b1-124">Laad voorbeeldgegevens in een tijdelijke tabel.</span><span class="sxs-lookup"><span data-stu-id="972b1-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="972b1-125">Wanneer u een Spark-cluster in HDInsight, Hallo voorbeeldgegevensbestand, maakt **hvac.csv**, is het opslagaccount gekopieerde toohello gekoppeld onder **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="972b1-125">When you create a Spark cluster in HDInsight, hello sample data file, **hvac.csv**, is copied toohello associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="972b1-126">Plak in lege alinea Hallo die standaard wordt gemaakt in de nieuwe notebook hello, Hallo codefragment te volgen.</span><span class="sxs-lookup"><span data-stu-id="972b1-126">In hello empty paragraph that is created by default in hello new notebook, paste hello following snippet.</span></span>
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    <span data-ttu-id="972b1-127">Druk op **SHIFT + ENTER** of klik op Hallo **afspelen** knop voor Hallo alinea toorun Hallo codefragment.</span><span class="sxs-lookup"><span data-stu-id="972b1-127">Press **SHIFT + ENTER** or click hello **Play** button for hello paragraph toorun hello snippet.</span></span> <span data-ttu-id="972b1-128">Hallo-status op Hallo-rechtsonder in Hallo lid moet worden voortgezet van gereed in behandeling zijnde tooFINISHED die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="972b1-128">hello status on hello right-corner of hello paragraph should progress from READY, PENDING, RUNNING tooFINISHED.</span></span> <span data-ttu-id="972b1-129">Hallo-uitvoer wordt weergegeven aan de onderkant Hallo Hallo dezelfde paragraph.</span><span class="sxs-lookup"><span data-stu-id="972b1-129">hello output shows up at hello bottom of hello same paragraph.</span></span> <span data-ttu-id="972b1-130">Hallo schermafbeelding ziet er Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="972b1-130">hello screenshot looks like hello following:</span></span>
   
    <span data-ttu-id="972b1-131">![Een tijdelijke tabel maken van ruwe gegevens](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "een tijdelijke tabel maken van ruwe gegevens")</span><span class="sxs-lookup"><span data-stu-id="972b1-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="972b1-132">U kunt ook een titel tooeach alinea opgeven.</span><span class="sxs-lookup"><span data-stu-id="972b1-132">You can also provide a title tooeach paragraph.</span></span> <span data-ttu-id="972b1-133">Vanuit de rechterhoek hello, klikt u op Hallo **instellingen** pictogram en klik vervolgens op **titel weergeven**.</span><span class="sxs-lookup"><span data-stu-id="972b1-133">From hello right-hand corner, click hello **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="972b1-134">U kunt nu Spark SQL-instructies uitvoeren op Hallo **hvac** tabel.</span><span class="sxs-lookup"><span data-stu-id="972b1-134">You can now run Spark SQL statements on hello **hvac** table.</span></span> <span data-ttu-id="972b1-135">Plak Hallo volgende query in een nieuw lid.</span><span class="sxs-lookup"><span data-stu-id="972b1-135">Paste hello following query in a new paragraph.</span></span> <span data-ttu-id="972b1-136">Hallo query haalt Hallo gebouw-ID en Hallo verschil tussen het Hallo-doel en de werkelijke temperaturen voor elke bouwen op een bepaalde datum.</span><span class="sxs-lookup"><span data-stu-id="972b1-136">hello query retrieves hello building ID and hello difference between hello target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="972b1-137">Druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="972b1-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="972b1-138">Hallo **% sql** instructie op Hallo begin vertelt Hallo notebook toouse hello Livy Scala interpreter.</span><span class="sxs-lookup"><span data-stu-id="972b1-138">hello **%sql** statement at hello beginning tells hello notebook toouse hello Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="972b1-139">Hallo volgende schermafbeelding ziet u uitvoer Hallo.</span><span class="sxs-lookup"><span data-stu-id="972b1-139">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="972b1-140">![Voer een Spark SQL-instructie Hallo notebook met](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "een Spark SQL-instructie met behulp van de notebook Hallo uitvoert")</span><span class="sxs-lookup"><span data-stu-id="972b1-140">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using hello notebook")</span></span>
   
     <span data-ttu-id="972b1-141">Klik op Hallo weergave opties (gemarkeerd in de rechthoek) tooswitch tussen verschillende manieren voor Hallo dezelfde uitvoer.</span><span class="sxs-lookup"><span data-stu-id="972b1-141">Click hello display options (highlighted in rectangle) tooswitch between different representations for hello same output.</span></span> <span data-ttu-id="972b1-142">Klik op **instellingen** toochoose welke consitutes Hallo sleutel en waarden in Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="972b1-142">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="972b1-143">schermopname hierboven gebruikt Hallo **buildingID** als Hallo-sleutel en de gemiddelde Hallo van **temp_diff** Hallo-waarde.</span><span class="sxs-lookup"><span data-stu-id="972b1-143">hello screen capture above uses **buildingID** as hello key and hello average of **temp_diff** as hello value.</span></span>
6. <span data-ttu-id="972b1-144">U kunt ook Spark SQL-instructies voor het gebruik van variabelen in Hallo-query uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="972b1-144">You can also run Spark SQL statements using variables in hello query.</span></span> <span data-ttu-id="972b1-145">Hallo volgende codefragment bevat hoe toodefine een variabele, **Temp**, in de query Hallo met Hallo mogelijke waarden die u wilt tooquery met.</span><span class="sxs-lookup"><span data-stu-id="972b1-145">hello next snippet shows how toodefine a variable, **Temp**, in hello query with hello possible values you want tooquery with.</span></span> <span data-ttu-id="972b1-146">Wanneer u Hallo query voor het eerst uitvoert, wordt een vervolgkeuzelijst wordt automatisch gevuld met Hallo-waarden die u hebt opgegeven voor het Hallo-variabele.</span><span class="sxs-lookup"><span data-stu-id="972b1-146">When you first run hello query, a drop-down is automatically populated with hello values you specified for hello variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="972b1-147">In dit fragment plakken in een nieuwe alinea en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="972b1-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="972b1-148">Hallo volgende schermafbeelding ziet u uitvoer Hallo.</span><span class="sxs-lookup"><span data-stu-id="972b1-148">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="972b1-149">![Voer een Spark SQL-instructie Hallo notebook met](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "een Spark SQL-instructie met behulp van de notebook Hallo uitvoert")</span><span class="sxs-lookup"><span data-stu-id="972b1-149">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using hello notebook")</span></span>
   
    <span data-ttu-id="972b1-150">Voor de volgende query's, kunt u een nieuwe waarde te selecteren in de vervolgkeuzelijst Hallo en Hallo query opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="972b1-150">For subsequent queries, you can select a new value from hello drop-down and run hello query again.</span></span> <span data-ttu-id="972b1-151">Klik op **instellingen** toochoose welke consitutes Hallo sleutel en waarden in Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="972b1-151">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="972b1-152">schermopname hierboven gebruikt Hallo **buildingID** als sleutel Hallo Hallo gemiddelde van **temp_diff** Hallo-waarde en **targettemp** als Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="972b1-152">hello screen capture above uses **buildingID** as hello key, hello average of **temp_diff** as hello value, and **targettemp** as hello group.</span></span>
7. <span data-ttu-id="972b1-153">Hallo Livy interpreter tooexit Hallo toepassing opnieuw.</span><span class="sxs-lookup"><span data-stu-id="972b1-153">Restart hello Livy interpreter tooexit hello application.</span></span> <span data-ttu-id="972b1-154">toodo Hiertoe opent u interpreter instellingen door te klikken op Hallo vastgelegd in de gebruikersnaam van Hallo rechterbovenhoek en klik vervolgens op **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="972b1-154">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="972b1-155">![Start interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive-uitvoer")</span><span class="sxs-lookup"><span data-stu-id="972b1-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="972b1-156">Schuif tooLivy interpreter instellingen en klik vervolgens op **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="972b1-156">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="972b1-157">![Opnieuw opstarten Hallo Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "hello Zeppelin intepreter starten")</span><span class="sxs-lookup"><span data-stu-id="972b1-157">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a><span data-ttu-id="972b1-158">Hoe gebruik ik externe pakketten met Hallo notebook</span><span class="sxs-lookup"><span data-stu-id="972b1-158">How do I use external packages with hello notebook?</span></span>
<span data-ttu-id="972b1-159">U kunt Hallo Zeppelin-notebook in Apache Spark-cluster in HDInsight (Linux) toouse externe, community bijgedragen pakketten die niet opgenomen out-of-the-box in Hallo cluster zijn configureren.</span><span class="sxs-lookup"><span data-stu-id="972b1-159">You can configure hello Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed packages that are not included out-of-the-box in hello cluster.</span></span> <span data-ttu-id="972b1-160">U kunt zoeken Hallo [Maven opslagplaats](http://search.maven.org/) voor Hallo volledige lijst met pakketten die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="972b1-160">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="972b1-161">U kunt ook een lijst met beschikbare pakketten opvragen uit andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="972b1-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="972b1-162">Bijvoorbeeld, een volledige lijst met pakketten community bijgedragen is beschikbaar op [Spark pakketten](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="972b1-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="972b1-163">In dit artikel ziet u hoe toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakket met de Jupyter-notebook Hallo.</span><span class="sxs-lookup"><span data-stu-id="972b1-163">In this article, you will see how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>

1. <span data-ttu-id="972b1-164">Open interpreter instellingen.</span><span class="sxs-lookup"><span data-stu-id="972b1-164">Open interpreter settings.</span></span> <span data-ttu-id="972b1-165">In de rechterbovenhoek hello, Hallo vastgelegd in de gebruikersnaam van de op en klik op **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="972b1-165">From hello top-right corner, click hello logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="972b1-166">![Start interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive-uitvoer")</span><span class="sxs-lookup"><span data-stu-id="972b1-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="972b1-167">Schuif tooLivy interpreter instellingen en klik vervolgens op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="972b1-167">Scroll tooLivy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="972b1-168">![Wijzig de instellingen van de interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "interpreter instellingen wijzigen")</span><span class="sxs-lookup"><span data-stu-id="972b1-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="972b1-169">Voeg een nieuwe sleutel aangeroepen **livy.spark.jars.packages** en stel de waarde in de indeling Hallo `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="972b1-169">Add a new key, called **livy.spark.jars.packages** and set its value in hello format `group:id:version`.</span></span> <span data-ttu-id="972b1-170">Dus als u wilt dat toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakket, moet u Hallo waarde instellen van Hallo sleutel te`com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="972b1-170">So, if you want toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set hello value of hello key too`com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="972b1-171">![Wijzig de instellingen van de interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "interpreter instellingen wijzigen")</span><span class="sxs-lookup"><span data-stu-id="972b1-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="972b1-172">Klik op **opslaan** en Hallo Livy interpreter opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="972b1-172">Click **Save** and then restart hello Livy interpreter.</span></span>
4. <span data-ttu-id="972b1-173">**Tip**: als u wilt dat toounderstand hoe tooarrive op Hallo-waarde van Hallo sleutel, hier hierboven hoe.</span><span class="sxs-lookup"><span data-stu-id="972b1-173">**Tip**: If you want toounderstand how tooarrive at hello value of hello key entered above, here's how.</span></span>
   
    <span data-ttu-id="972b1-174">a.</span><span class="sxs-lookup"><span data-stu-id="972b1-174">a.</span></span> <span data-ttu-id="972b1-175">Hallo-pakket niet vinden in Hallo Maven-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="972b1-175">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="972b1-176">Voor deze zelfstudie gebruikt we [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="972b1-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="972b1-177">b.</span><span class="sxs-lookup"><span data-stu-id="972b1-177">b.</span></span> <span data-ttu-id="972b1-178">Verzamel uit de opslagplaats hello, Hallo waarden voor **GroupId**, **artefact-id**, en **versie**.</span><span class="sxs-lookup"><span data-stu-id="972b1-178">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="972b1-179">![Externe pakketten gebruiken met Jupyter-notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "externe pakketten gebruiken met Jupyter-notebook")</span><span class="sxs-lookup"><span data-stu-id="972b1-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="972b1-180">c.</span><span class="sxs-lookup"><span data-stu-id="972b1-180">c.</span></span> <span data-ttu-id="972b1-181">Samenvoegen van Hallo drie waarden, gescheiden door een dubbele punt (**:**).</span><span class="sxs-lookup"><span data-stu-id="972b1-181">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a><span data-ttu-id="972b1-182">Waar zijn Hallo Zeppelin-notebooks opgeslagen?</span><span class="sxs-lookup"><span data-stu-id="972b1-182">Where are hello Zeppelin notebooks saved?</span></span>
<span data-ttu-id="972b1-183">Hallo Zeppelin-notebooks worden toohello cluster headnodes opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="972b1-183">hello Zeppelin notebooks are saved toohello cluster headnodes.</span></span> <span data-ttu-id="972b1-184">Dus als u Hallo cluster verwijdert, Hallo notitieblokken eveneens worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="972b1-184">So, if you delete hello cluster, hello notebooks will be deleted as well.</span></span> <span data-ttu-id="972b1-185">Als u uw notitieblokken toopreserve voor later gebruik op andere clusters wilt, moet u deze exporteren wanneer u klaar bent met het Hallo-taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="972b1-185">If you want toopreserve your notebooks for later use on other clusters, you must export them after you have finished running hello jobs.</span></span> <span data-ttu-id="972b1-186">tooexport een laptop, klikt u op Hallo **exporteren** pictogram zoals weergegeven in onderstaande Hallo-afbeelding.</span><span class="sxs-lookup"><span data-stu-id="972b1-186">tooexport a notebook, click hello **Export** icon as shown in hello image below.</span></span>

<span data-ttu-id="972b1-187">![Downloaden van de notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "downloaden Hallo notebook")</span><span class="sxs-lookup"><span data-stu-id="972b1-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download hello notebook")</span></span>

<span data-ttu-id="972b1-188">Dit bespaart Hallo notebook als een JSON-bestand op uw downloadlocatie.</span><span class="sxs-lookup"><span data-stu-id="972b1-188">This saves hello notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="972b1-189">Sessiebeheer Livy</span><span class="sxs-lookup"><span data-stu-id="972b1-189">Livy session management</span></span>
<span data-ttu-id="972b1-190">Wanneer u het eerste code alinea Hallo in uw laptop Zeppelin uitvoert, wordt een nieuwe sessie van Livy gemaakt in uw HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="972b1-190">When you run hello first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="972b1-191">Deze sessie worden verdeeld over alle Zeppelin-notebooks die u maakt.</span><span class="sxs-lookup"><span data-stu-id="972b1-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="972b1-192">Als voor een bepaalde reden Hallo Livy sessie is afgesloten (cluster opnieuw opstarten, enzovoort), kunt u niet kunt toorun taken van Hallo Zeppelin notebook.</span><span class="sxs-lookup"><span data-stu-id="972b1-192">If for some reason hello Livy session is killed (cluster reboot, etc.), you will not be able toorun jobs from hello Zeppelin notebook.</span></span>

<span data-ttu-id="972b1-193">In dat geval moet u de volgende stappen uit voordat u kunt de uitvoering van taken van een laptop Zeppelin Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="972b1-193">In such a case, you must perform hello following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="972b1-194">Opnieuw opstarten Hallo Livy interpreter uit Hallo Zeppelin laptop.</span><span class="sxs-lookup"><span data-stu-id="972b1-194">Restart hello Livy interpreter from hello Zeppelin notebook.</span></span> <span data-ttu-id="972b1-195">toodo Hiertoe opent u interpreter instellingen door te klikken op Hallo vastgelegd in de gebruikersnaam van Hallo rechterbovenhoek en klik vervolgens op **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="972b1-195">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="972b1-196">![Start interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive-uitvoer")</span><span class="sxs-lookup"><span data-stu-id="972b1-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="972b1-197">Schuif tooLivy interpreter instellingen en klik vervolgens op **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="972b1-197">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="972b1-198">![Opnieuw opstarten Hallo Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "hello Zeppelin intepreter starten")</span><span class="sxs-lookup"><span data-stu-id="972b1-198">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>
3. <span data-ttu-id="972b1-199">Een codecel uitvoeren vanaf een bestaande Zeppelin-notebook.</span><span class="sxs-lookup"><span data-stu-id="972b1-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="972b1-200">Hiermee maakt u een nieuwe sessie van Livy in Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="972b1-200">This creates a new Livy session in hello HDInsight cluster.</span></span>

## <span data-ttu-id="972b1-201"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="972b1-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="972b1-202">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="972b1-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="972b1-203">Scenario's</span><span class="sxs-lookup"><span data-stu-id="972b1-203">Scenarios</span></span>
* [<span data-ttu-id="972b1-204">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="972b1-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="972b1-205">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="972b1-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="972b1-206">Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="972b1-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="972b1-207">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="972b1-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="972b1-208">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="972b1-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="972b1-209">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="972b1-209">Create and run applications</span></span>
* [<span data-ttu-id="972b1-210">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="972b1-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="972b1-211">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="972b1-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="972b1-212">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="972b1-212">Tools and extensions</span></span>
* [<span data-ttu-id="972b1-213">De invoegtoepassing HDInsight Tools voor toocreate IntelliJ IDEA gebruiken en het verzenden van Spark Scala-toepassingen</span><span class="sxs-lookup"><span data-stu-id="972b1-213">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="972b1-214">De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken</span><span class="sxs-lookup"><span data-stu-id="972b1-214">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="972b1-215">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="972b1-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="972b1-216">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="972b1-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="972b1-217">Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="972b1-217">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="972b1-218">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="972b1-218">Manage resources</span></span>
* [<span data-ttu-id="972b1-219">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="972b1-219">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="972b1-220">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="972b1-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 








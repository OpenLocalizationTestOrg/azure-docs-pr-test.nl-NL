---
title: Zeppelin-notebooks gebruiken met Apache Spark-cluster in Azure HDInsight | Microsoft Docs
description: Stapsgewijze instructies voor het gebruik van Zeppelin-notebooks met Apache Spark-clusters op Azure HDInsight.
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
ms.openlocfilehash: 7fe5e3ec68e82945b972d2dd44f2cc3b8cf395d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="45e31-103">Zeppelin-notebooks met Apache Spark-cluster in Azure HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="45e31-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="45e31-104">HDInsight Spark-clusters bevatten Zeppelin-notebooks die u gebruiken kunt om uit te voeren Spark taken.</span><span class="sxs-lookup"><span data-stu-id="45e31-104">HDInsight Spark clusters include Zeppelin notebooks that you can use to run Spark jobs.</span></span> <span data-ttu-id="45e31-105">In dit artikel leert u hoe u de notebook Zeppelin gebruikt op een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="45e31-105">In this article, you learn how to use the Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="45e31-106">Zeppelin-notebooks zijn alleen beschikbaar voor Spark 1.6.3 in HDInsight 3.5 en Spark 2.1.0 in HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="45e31-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="45e31-107">**Vereisten:**</span><span class="sxs-lookup"><span data-stu-id="45e31-107">**Prerequisites:**</span></span>

* <span data-ttu-id="45e31-108">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="45e31-108">An Azure subscription.</span></span> <span data-ttu-id="45e31-109">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="45e31-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="45e31-110">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="45e31-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="45e31-111">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="45e31-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="45e31-112">Een laptop Zeppelin starten</span><span class="sxs-lookup"><span data-stu-id="45e31-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="45e31-113">Klik in de blade Spark-cluster op **Cluster-Dashboard**, en klik vervolgens op **Zeppelin-Notebook**.</span><span class="sxs-lookup"><span data-stu-id="45e31-113">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="45e31-114">Voer de beheerdersreferenties voor het cluster in als u daarom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="45e31-114">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="45e31-115">U mogelijk ook de Zeppelin-Notebook voor uw cluster bereiken door de volgende URL in uw browser te openen.</span><span class="sxs-lookup"><span data-stu-id="45e31-115">You may also reach the Zeppelin Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="45e31-116">Vervang **CLUSTERNAME** door de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="45e31-116">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="45e31-117">Maak een nieuwe notebook.</span><span class="sxs-lookup"><span data-stu-id="45e31-117">Create a new notebook.</span></span> <span data-ttu-id="45e31-118">Klik in het headerdeelvenster **Notebook**, en klik vervolgens op **nieuwe notitie maken**.</span><span class="sxs-lookup"><span data-stu-id="45e31-118">From the header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="45e31-119">![Maak een nieuwe Zeppelin-notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "een nieuwe Zeppelin-notebook maken")</span><span class="sxs-lookup"><span data-stu-id="45e31-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="45e31-120">Voer een naam voor de notebook en klik vervolgens op **opmerking maken**.</span><span class="sxs-lookup"><span data-stu-id="45e31-120">Enter a name for the notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="45e31-121">Controleer ook of dat de notebook-header bevat een verbonden status.</span><span class="sxs-lookup"><span data-stu-id="45e31-121">Also, make sure the notebook header shows a connected status.</span></span> <span data-ttu-id="45e31-122">Dit wordt aangeduid met een groen punt in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="45e31-122">It is denoted by a green dot in the top-right corner.</span></span>
   
    <span data-ttu-id="45e31-123">![Zeppelin-notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin-notebook status")</span><span class="sxs-lookup"><span data-stu-id="45e31-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="45e31-124">Laad voorbeeldgegevens in een tijdelijke tabel.</span><span class="sxs-lookup"><span data-stu-id="45e31-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="45e31-125">Wanneer u een Spark-cluster in HDInsight, het voorbeeldgegevensbestand maakt **hvac.csv**, wordt gekopieerd naar de bijbehorende opslagaccount onder **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="45e31-125">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="45e31-126">Plak het volgende codefragment in de lege alinea die standaard in de nieuwe laptop is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="45e31-126">In the empty paragraph that is created by default in the new notebook, paste the following snippet.</span></span>
   
        %livy.spark
        //The above magic instructs Zeppelin to use the Livy Scala interpreter
   
        // Create an RDD using the default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map the values in the .csv file to the schema
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
   
    <span data-ttu-id="45e31-127">Druk op **SHIFT + ENTER** of klik op de **afspelen** knop voor de alinea om uit te voeren van het fragment.</span><span class="sxs-lookup"><span data-stu-id="45e31-127">Press **SHIFT + ENTER** or click the **Play** button for the paragraph to run the snippet.</span></span> <span data-ttu-id="45e31-128">De status van de rechterbenedenhoek van de alinea moet de voortgang van READY, PENDING, die wordt uitgevoerd op voltooid.</span><span class="sxs-lookup"><span data-stu-id="45e31-128">The status on the right-corner of the paragraph should progress from READY, PENDING, RUNNING to FINISHED.</span></span> <span data-ttu-id="45e31-129">De uitvoer wordt weergegeven aan de onderkant van dezelfde paragraph.</span><span class="sxs-lookup"><span data-stu-id="45e31-129">The output shows up at the bottom of the same paragraph.</span></span> <span data-ttu-id="45e31-130">De schermafbeelding ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="45e31-130">The screenshot looks like the following:</span></span>
   
    <span data-ttu-id="45e31-131">![Een tijdelijke tabel maken van ruwe gegevens](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "een tijdelijke tabel maken van ruwe gegevens")</span><span class="sxs-lookup"><span data-stu-id="45e31-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="45e31-132">U kunt ook een titel op elke alinea opgeven.</span><span class="sxs-lookup"><span data-stu-id="45e31-132">You can also provide a title to each paragraph.</span></span> <span data-ttu-id="45e31-133">Klik in de rechterhoek op de **instellingen** pictogram en klik vervolgens op **titel weergeven**.</span><span class="sxs-lookup"><span data-stu-id="45e31-133">From the right-hand corner, click the **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="45e31-134">U kunt nu Spark SQL-instructies uitvoeren op de **hvac** tabel.</span><span class="sxs-lookup"><span data-stu-id="45e31-134">You can now run Spark SQL statements on the **hvac** table.</span></span> <span data-ttu-id="45e31-135">Plak de volgende query in een nieuwe alinea.</span><span class="sxs-lookup"><span data-stu-id="45e31-135">Paste the following query in a new paragraph.</span></span> <span data-ttu-id="45e31-136">De query haalt de gebouw-ID en het verschil tussen het doel en de werkelijke temperaturen voor elke bouwen op een bepaalde datum.</span><span class="sxs-lookup"><span data-stu-id="45e31-136">The query retrieves the building ID and the difference between the target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="45e31-137">Druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="45e31-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="45e31-138">De **% sql** instructie aan het begin vertelt de notebook de interpreter Livy Scala gebruiken.</span><span class="sxs-lookup"><span data-stu-id="45e31-138">The **%sql** statement at the beginning tells the notebook to use the Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="45e31-139">De volgende schermafbeelding ziet u de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="45e31-139">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="45e31-140">![Voer een Spark SQL-instructie met behulp van de notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "een Spark SQL-instructie met behulp van de notebook uitvoert")</span><span class="sxs-lookup"><span data-stu-id="45e31-140">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using the notebook")</span></span>
   
     <span data-ttu-id="45e31-141">Klik op de weergaveopties (gemarkeerd rechthoek) om te schakelen tussen de verschillende manieren voor dezelfde uitvoer.</span><span class="sxs-lookup"><span data-stu-id="45e31-141">Click the display options (highlighted in rectangle) to switch between different representations for the same output.</span></span> <span data-ttu-id="45e31-142">Klik op **instellingen** kiezen welke consitutes de sleutel en de waarden in de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="45e31-142">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="45e31-143">Maakt gebruik van de bovenstaande schermafbeelding **buildingID** als de sleutel en het gemiddelde van **temp_diff** als de waarde.</span><span class="sxs-lookup"><span data-stu-id="45e31-143">The screen capture above uses **buildingID** as the key and the average of **temp_diff** as the value.</span></span>
6. <span data-ttu-id="45e31-144">U kunt ook Spark SQL-instructies voor het gebruik van variabelen in de query uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="45e31-144">You can also run Spark SQL statements using variables in the query.</span></span> <span data-ttu-id="45e31-145">Het volgende fragment toont hoe een variabele definiëren **Temp**, in de query met de mogelijke waarden die u wilt zoeken met.</span><span class="sxs-lookup"><span data-stu-id="45e31-145">The next snippet shows how to define a variable, **Temp**, in the query with the possible values you want to query with.</span></span> <span data-ttu-id="45e31-146">Wanneer u de query voor het eerst uitvoert, wordt een vervolgkeuzelijst automatisch ingevuld met de waarden die u hebt opgegeven voor de variabele.</span><span class="sxs-lookup"><span data-stu-id="45e31-146">When you first run the query, a drop-down is automatically populated with the values you specified for the variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="45e31-147">In dit fragment plakken in een nieuwe alinea en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="45e31-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="45e31-148">De volgende schermafbeelding ziet u de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="45e31-148">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="45e31-149">![Voer een Spark SQL-instructie met behulp van de notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "een Spark SQL-instructie met behulp van de notebook uitvoert")</span><span class="sxs-lookup"><span data-stu-id="45e31-149">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using the notebook")</span></span>
   
    <span data-ttu-id="45e31-150">U kunt voor de volgende query's, selecteert u een nieuwe waarde in de vervolgkeuzelijst en voer de query opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="45e31-150">For subsequent queries, you can select a new value from the drop-down and run the query again.</span></span> <span data-ttu-id="45e31-151">Klik op **instellingen** kiezen welke consitutes de sleutel en de waarden in de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="45e31-151">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="45e31-152">Maakt gebruik van de bovenstaande schermafbeelding **buildingID** als de sleutel, wordt het gemiddelde van **temp_diff** als de waarde en **targettemp** als de groep.</span><span class="sxs-lookup"><span data-stu-id="45e31-152">The screen capture above uses **buildingID** as the key, the average of **temp_diff** as the value, and **targettemp** as the group.</span></span>
7. <span data-ttu-id="45e31-153">Start de interpreter Livy om af te sluiten van de toepassing opnieuw.</span><span class="sxs-lookup"><span data-stu-id="45e31-153">Restart the Livy interpreter to exit the application.</span></span> <span data-ttu-id="45e31-154">Om dit te doen interpreter instellingen openen door te klikken op de geregistreerde gebruikersnaam in de rechterbovenhoek en klik vervolgens op **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="45e31-154">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="45e31-155">![Start interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive-uitvoer")</span><span class="sxs-lookup"><span data-stu-id="45e31-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="45e31-156">Schuif naar Livy interpreter instellingen en klik vervolgens op **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="45e31-156">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="45e31-157">![Opnieuw opstarten van de intepreter Livy](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "opnieuw opstarten van de intepreter Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="45e31-157">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-the-notebook"></a><span data-ttu-id="45e31-158">Hoe gebruik ik externe pakketten met de notebook</span><span class="sxs-lookup"><span data-stu-id="45e31-158">How do I use external packages with the notebook?</span></span>
<span data-ttu-id="45e31-159">U kunt de notebook Zeppelin in Apache Spark-cluster in HDInsight (Linux) configureren voor het gebruik van externe, community bijgedragen pakketten die niet opgenomen out-of-the-box in het cluster zijn.</span><span class="sxs-lookup"><span data-stu-id="45e31-159">You can configure the Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) to use external, community-contributed packages that are not included out-of-the-box in the cluster.</span></span> <span data-ttu-id="45e31-160">U kunt zoeken in de [Maven opslagplaats](http://search.maven.org/) voor de volledige lijst met pakketten die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="45e31-160">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="45e31-161">U kunt ook een lijst met beschikbare pakketten opvragen uit andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="45e31-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="45e31-162">Bijvoorbeeld, een volledige lijst met pakketten community bijgedragen is beschikbaar op [Spark pakketten](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="45e31-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="45e31-163">In dit artikel ziet u hoe u de [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakket met de Jupyter-notebook.</span><span class="sxs-lookup"><span data-stu-id="45e31-163">In this article, you will see how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>

1. <span data-ttu-id="45e31-164">Open interpreter instellingen.</span><span class="sxs-lookup"><span data-stu-id="45e31-164">Open interpreter settings.</span></span> <span data-ttu-id="45e31-165">Klikt u op de geregistreerde gebruikersnaam in de rechterbovenhoek en klik vervolgens op **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="45e31-165">From the top-right corner, click the logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="45e31-166">![Start interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive-uitvoer")</span><span class="sxs-lookup"><span data-stu-id="45e31-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="45e31-167">Schuif naar Livy interpreter instellingen en klik vervolgens op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="45e31-167">Scroll to Livy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="45e31-168">![Wijzig de instellingen van de interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "interpreter instellingen wijzigen")</span><span class="sxs-lookup"><span data-stu-id="45e31-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="45e31-169">Voeg een nieuwe sleutel aangeroepen **livy.spark.jars.packages** en stel de waarde in de notatie `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="45e31-169">Add a new key, called **livy.spark.jars.packages** and set its value in the format `group:id:version`.</span></span> <span data-ttu-id="45e31-170">Dus als u wilt gebruiken de [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakket, moet u de waarde van de sleutel instellen `com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="45e31-170">So, if you want to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set the value of the key to `com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="45e31-171">![Wijzig de instellingen van de interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "interpreter instellingen wijzigen")</span><span class="sxs-lookup"><span data-stu-id="45e31-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="45e31-172">Klik op **opslaan** en start vervolgens opnieuw de interpreter Livy.</span><span class="sxs-lookup"><span data-stu-id="45e31-172">Click **Save** and then restart the Livy interpreter.</span></span>
4. <span data-ttu-id="45e31-173">**Tip**: als u wilt weten hoe moet worden uitgevoerd op de waarde van de sleutel dat hierboven is opgegeven, wordt hier hoe.</span><span class="sxs-lookup"><span data-stu-id="45e31-173">**Tip**: If you want to understand how to arrive at the value of the key entered above, here's how.</span></span>
   
    <span data-ttu-id="45e31-174">a.</span><span class="sxs-lookup"><span data-stu-id="45e31-174">a.</span></span> <span data-ttu-id="45e31-175">Het pakket niet vinden in de opslagplaats met Maven.</span><span class="sxs-lookup"><span data-stu-id="45e31-175">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="45e31-176">Voor deze zelfstudie gebruikt we [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="45e31-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="45e31-177">b.</span><span class="sxs-lookup"><span data-stu-id="45e31-177">b.</span></span> <span data-ttu-id="45e31-178">Verzamel de waarden voor uit de opslagplaats **GroupId**, **artefact-id**, en **versie**.</span><span class="sxs-lookup"><span data-stu-id="45e31-178">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="45e31-179">![Externe pakketten gebruiken met Jupyter-notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "externe pakketten gebruiken met Jupyter-notebook")</span><span class="sxs-lookup"><span data-stu-id="45e31-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="45e31-180">c.</span><span class="sxs-lookup"><span data-stu-id="45e31-180">c.</span></span> <span data-ttu-id="45e31-181">De drie waarden, gescheiden door een dubbele punt (**:**).</span><span class="sxs-lookup"><span data-stu-id="45e31-181">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-the-zeppelin-notebooks-saved"></a><span data-ttu-id="45e31-182">Waar worden de Zeppelin-notebooks opgeslagen?</span><span class="sxs-lookup"><span data-stu-id="45e31-182">Where are the Zeppelin notebooks saved?</span></span>
<span data-ttu-id="45e31-183">Zeppelin-notebooks worden opgeslagen in de cluster-headnodes.</span><span class="sxs-lookup"><span data-stu-id="45e31-183">The Zeppelin notebooks are saved to the cluster headnodes.</span></span> <span data-ttu-id="45e31-184">Dus als u het cluster verwijdert, wordt de laptops ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="45e31-184">So, if you delete the cluster, the notebooks will be deleted as well.</span></span> <span data-ttu-id="45e31-185">Als u uw notitieblokken voor later gebruik op andere clusters behouden wilt, moet u deze exporteren wanneer u klaar bent met het uitvoeren van de taken.</span><span class="sxs-lookup"><span data-stu-id="45e31-185">If you want to preserve your notebooks for later use on other clusters, you must export them after you have finished running the jobs.</span></span> <span data-ttu-id="45e31-186">Als u wilt exporteren een laptop, klikt u op de **exporteren** pictogram zoals weergegeven in de onderstaande afbeelding.</span><span class="sxs-lookup"><span data-stu-id="45e31-186">To export a notebook, click the **Export** icon as shown in the image below.</span></span>

<span data-ttu-id="45e31-187">![Downloaden van de notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "downloaden van de notebook")</span><span class="sxs-lookup"><span data-stu-id="45e31-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download the notebook")</span></span>

<span data-ttu-id="45e31-188">Hiermee wordt de notebook opgeslagen als een JSON-bestand op uw downloadlocatie.</span><span class="sxs-lookup"><span data-stu-id="45e31-188">This saves the notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="45e31-189">Sessiebeheer Livy</span><span class="sxs-lookup"><span data-stu-id="45e31-189">Livy session management</span></span>
<span data-ttu-id="45e31-190">Wanneer u de eerste alinea in de code in uw laptop Zeppelin uitvoert, wordt een nieuwe sessie van Livy gemaakt in uw HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="45e31-190">When you run the first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="45e31-191">Deze sessie worden verdeeld over alle Zeppelin-notebooks die u maakt.</span><span class="sxs-lookup"><span data-stu-id="45e31-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="45e31-192">Als de Livy sessie is beëindigd voor een bepaalde reden (cluster opnieuw opstarten, enzovoort), is het niet mogelijk om uit te voeren taken van de notebook Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="45e31-192">If for some reason the Livy session is killed (cluster reboot, etc.), you will not be able to run jobs from the Zeppelin notebook.</span></span>

<span data-ttu-id="45e31-193">In dat geval moet u de volgende stappen uitvoeren voordat u taken uitvoert vanuit een Zeppelin-notebook kunt starten.</span><span class="sxs-lookup"><span data-stu-id="45e31-193">In such a case, you must perform the following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="45e31-194">De interpreter Livy van de notebook Zeppelin opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="45e31-194">Restart the Livy interpreter from the Zeppelin notebook.</span></span> <span data-ttu-id="45e31-195">Om dit te doen interpreter instellingen openen door te klikken op de geregistreerde gebruikersnaam in de rechterbovenhoek en klik vervolgens op **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="45e31-195">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="45e31-196">![Start interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive-uitvoer")</span><span class="sxs-lookup"><span data-stu-id="45e31-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="45e31-197">Schuif naar Livy interpreter instellingen en klik vervolgens op **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="45e31-197">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="45e31-198">![Opnieuw opstarten van de intepreter Livy](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "opnieuw opstarten van de intepreter Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="45e31-198">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>
3. <span data-ttu-id="45e31-199">Een codecel uitvoeren vanaf een bestaande Zeppelin-notebook.</span><span class="sxs-lookup"><span data-stu-id="45e31-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="45e31-200">Hiermee maakt u een nieuwe sessie van Livy in het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="45e31-200">This creates a new Livy session in the HDInsight cluster.</span></span>

## <span data-ttu-id="45e31-201"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="45e31-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="45e31-202">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="45e31-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="45e31-203">Scenario's</span><span class="sxs-lookup"><span data-stu-id="45e31-203">Scenarios</span></span>
* [<span data-ttu-id="45e31-204">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="45e31-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="45e31-205">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="45e31-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="45e31-206">Spark met Machine Learning: Spark in HDInsight gebruiken om voedselinspectieresultaten te voorspellen</span><span class="sxs-lookup"><span data-stu-id="45e31-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="45e31-207">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="45e31-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="45e31-208">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="45e31-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="45e31-209">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="45e31-209">Create and run applications</span></span>
* [<span data-ttu-id="45e31-210">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="45e31-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="45e31-211">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="45e31-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="45e31-212">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="45e31-212">Tools and extensions</span></span>
* [<span data-ttu-id="45e31-213">De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om Spark Scala-toepassingen te maken en in te dienen</span><span class="sxs-lookup"><span data-stu-id="45e31-213">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="45e31-214">De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om op afstand fouten in Spark Scala-toepassingen op te lossen</span><span class="sxs-lookup"><span data-stu-id="45e31-214">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="45e31-215">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="45e31-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="45e31-216">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="45e31-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="45e31-217">Jupyter op uw computer installeren en verbinding maken met een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="45e31-217">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="45e31-218">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="45e31-218">Manage resources</span></span>
* [<span data-ttu-id="45e31-219">Resources beheren voor het Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="45e31-219">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="45e31-220">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="45e31-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 








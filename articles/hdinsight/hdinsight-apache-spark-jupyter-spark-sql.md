---
title: Een Apache Spark-cluster maken in Azure HDInsight | Microsoft Docs
description: HDInsight Spark-snelstartgids over het maken van een Apache Spark-cluster in HDInsight.
keywords: spark-snelstartgids,interactieve spark,interactieve query,hdinsight spark,azure spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: ad4330a1fc7f8de154d9aaa8df3acc2ab59b9dc1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="7e259-104">Een Apache Spark-cluster maken in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e259-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="7e259-105">In dit artikel leert u hoe u een Apache Spark-cluster maakt in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e259-105">In this article, you learn how to create an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="7e259-106">Zie [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md) voor informatie over Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e259-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="7e259-107">![Snelstartdiagram waarin de stappen worden beschreven voor het maken van een Apache Spark-cluster in Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark-snelstartgids met behulp van Apache Spark in HDInsight. Geïllustreerde stappen: maken van een cluster; interactieve Spark-query uitvoeren")</span><span class="sxs-lookup"><span data-stu-id="7e259-107">![Quickstart diagram describing steps to create an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e259-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7e259-108">Prerequisites</span></span>

* <span data-ttu-id="7e259-109">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="7e259-109">**An Azure subscription**.</span></span> <span data-ttu-id="7e259-110">Voordat u met deze zelfstudie begint, moet u een Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="7e259-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="7e259-111">Zie [Maak vandaag nog uw gratis Azure-account](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="7e259-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="7e259-112">HDInsight Spark-cluster maken</span><span class="sxs-lookup"><span data-stu-id="7e259-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="7e259-113">In deze sectie maakt u een HDInsight Spark-cluster met behulp van een [Azure Resource Manager-sjabloon](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span><span class="sxs-lookup"><span data-stu-id="7e259-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="7e259-114">Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md) voor andere methoden voor het maken van clusters.</span><span class="sxs-lookup"><span data-stu-id="7e259-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="7e259-115">Klik op de volgende afbeelding om de sjabloon in Azure Portal te openen.</span><span class="sxs-lookup"><span data-stu-id="7e259-115">Click the following image to open the template in the Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="7e259-116">Voer de volgende waarden in:</span><span class="sxs-lookup"><span data-stu-id="7e259-116">Enter the following values:</span></span>

    <span data-ttu-id="7e259-117">![HDInsight Spark-cluster maken met behulp van een Azure Resource Manager-sjabloon](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Spark-cluster maken in HDInsight met behulp van een Azure Resource Manager-sjabloon")</span><span class="sxs-lookup"><span data-stu-id="7e259-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="7e259-118">**Abonnement**: selecteer uw Azure-abonnement voor dit cluster.</span><span class="sxs-lookup"><span data-stu-id="7e259-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="7e259-119">**Resourcegroep**: maak een nieuwe resourcegroep of selecteer een bestaande.</span><span class="sxs-lookup"><span data-stu-id="7e259-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="7e259-120">Deze resourcegroep wordt gebruikt om Azure-resources voor uw projecten te beheren.</span><span class="sxs-lookup"><span data-stu-id="7e259-120">Resource group is used to manage Azure resources for your projects.</span></span>
    * <span data-ttu-id="7e259-121">**Locatie**: selecteer een locatie voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="7e259-121">**Location**: Select a location for the resource group.</span></span> <span data-ttu-id="7e259-122">De sjabloon gebruikt deze locatie voor het maken van het cluster en als standaardclusteropslag.</span><span class="sxs-lookup"><span data-stu-id="7e259-122">The template uses this location for creating the cluster as well as for the default cluster storage.</span></span>
    * <span data-ttu-id="7e259-123">**Clusternaam**: geef een naam op voor het HDInsight-cluster dat u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="7e259-123">**ClusterName**: Enter a name for the HDInsight cluster that you want to create.</span></span>
    * <span data-ttu-id="7e259-124">**Spark-versie**: selecteer **2.0** als Spark-versie die u in het cluster wilt installeren.</span><span class="sxs-lookup"><span data-stu-id="7e259-124">**Spark version**: Select **2.0** as the version that you want to install on the cluster.</span></span>
    * <span data-ttu-id="7e259-125">**Clusteraanmeldgegevens**: de standaardaanmeldnaam is admin.</span><span class="sxs-lookup"><span data-stu-id="7e259-125">**Cluster login name and password**: The default login name is admin.</span></span>
    * <span data-ttu-id="7e259-126">**SSH-aanmeldgegevens**.</span><span class="sxs-lookup"><span data-stu-id="7e259-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="7e259-127">Noteer deze waarden.</span><span class="sxs-lookup"><span data-stu-id="7e259-127">Write down these values.</span></span>  <span data-ttu-id="7e259-128">U hebt ze later in de zelfstudie nodig.</span><span class="sxs-lookup"><span data-stu-id="7e259-128">You need them later in the tutorial.</span></span>

3. <span data-ttu-id="7e259-129">Selecteer **Ik ga akkoord met de bovenstaande voorwaarden**, selecteer **Vastmaken aan dashboard** en klik op **Kopen**.</span><span class="sxs-lookup"><span data-stu-id="7e259-129">Select **I agree to the terms and conditions stated above**, select **Pin to dashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="7e259-130">U ziet een nieuwe tegel met de titel Implementatie indienen voor Sjabloonimplementatie.</span><span class="sxs-lookup"><span data-stu-id="7e259-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="7e259-131">Het duurt ongeveer 20 minuten om het cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="7e259-131">It takes about 20 minutes to create the cluster.</span></span>

<span data-ttu-id="7e259-132">Als u een probleem ondervindt met het maken van HDInsight-clusters, beschikt u mogelijk niet over de juiste machtigingen om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="7e259-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have the right permissions to do so.</span></span> <span data-ttu-id="7e259-133">Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7e259-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="7e259-134">In dit artikel wordt een Spark-cluster gemaakt dat [Azure Storage-blobs als clusteropslag](hdinsight-hadoop-use-blob-storage.md) gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7e259-134">This article creates a Spark cluster that uses [Azure Storage Blobs as the cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="7e259-135">U kunt ook een Spark-cluster maken dat [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) als standaardopslag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7e259-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as the default storage.</span></span> <span data-ttu-id="7e259-136">Zie [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) (Een HDInsight-cluster maken met Data Lake Store) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="7e259-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="7e259-137">Een Hive-query uitvoeren met Spark SQL</span><span class="sxs-lookup"><span data-stu-id="7e259-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="7e259-138">Als u een Jupyter-notebook gebruikt dat is geconfigureerd voor uw HDInsight Spark-cluster, krijgt u een vooraf ingestelde `sqlContext` waarmee u Hive-query's kunt uitvoeren met behulp van Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="7e259-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use to run Hive queries using Spark SQL.</span></span> <span data-ttu-id="7e259-139">In deze sectie leert u hoe u een Jupyter-notebook start en vervolgens een eenvoudige Hive-query uitvoert.</span><span class="sxs-lookup"><span data-stu-id="7e259-139">In this section, you learn how to start a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="7e259-140">Open de [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7e259-140">Open the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="7e259-141">Als u ervoor hebt gekozen om het cluster vast te maken aan het dashboard, klikt u vanuit het dashboard op de clustertegel om de clusterblade te starten.</span><span class="sxs-lookup"><span data-stu-id="7e259-141">If you opted to pin the cluster to the dashboard, click the cluster tile from the dashboard to launch the cluster blade.</span></span>

    <span data-ttu-id="7e259-142">Als u het cluster niet hebt vastgemaakt aan het dashboard, klikt u in het linkerdeelvenster op **HDInsight clusters** en vervolgens op het cluster dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7e259-142">If you did not pin the cluster to the dashboard, from the left pane, click **HDInsight clusters**, and then click the cluster you created.</span></span>

3. <span data-ttu-id="7e259-143">Klik in **Snelkoppelingen** op **Clusterdashboards** en klik vervolgens op **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="7e259-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="7e259-144">Voer de beheerdersreferenties voor het cluster in als u daarom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="7e259-144">If prompted, enter the admin credentials for the cluster.</span></span>

   <span data-ttu-id="7e259-145">![Jupyter-notebook openen om de interactieve Spark SQL-query uit te voeren](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Jupyter-notebook openen om de interactieve Spark SQL-query uit te voeren")</span><span class="sxs-lookup"><span data-stu-id="7e259-145">![Open Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook to run interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="7e259-146">Mogelijk kunt u de Jupyter-notebook voor uw cluster ook openen door de volgende URL in uw browser te openen.</span><span class="sxs-lookup"><span data-stu-id="7e259-146">You may also access the Jupyter notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="7e259-147">Vervang **CLUSTERNAME** door de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="7e259-147">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="7e259-148">Maak een notebook.</span><span class="sxs-lookup"><span data-stu-id="7e259-148">Create a notebook.</span></span> <span data-ttu-id="7e259-149">Klik op **Nieuw** en klik vervolgens op **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="7e259-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="7e259-150">![Jupyter-notebook maken om de interactieve Spark SQL-query uit te voeren](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Jupyter-notebook maken om de interactieve Spark SQL-query uit te voeren")</span><span class="sxs-lookup"><span data-stu-id="7e259-150">![Create a Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook to run interactive Spark SQL query")</span></span>

   <span data-ttu-id="7e259-151">Er wordt een nieuwe notebook gemaakt en geopend met de naam Untitled (Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="7e259-151">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="7e259-152">Klik bovenaan op de naam van de notebook en wijzig deze desgewenst in een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="7e259-152">Click the notebook name at the top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="7e259-153">![Een naam opgeven voor de Jupyter-notebook waarop de interactieve Spark-query wordt uitgevoerd](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Een naam opgeven voor de Jupyter-notebook waarop de interactieve Spark-query wordt uitgevoerd")</span><span class="sxs-lookup"><span data-stu-id="7e259-153">![Provide a name for the Jupter notebook to run interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for the Jupter notebook to run interactive Spark query from")</span></span>

5.  <span data-ttu-id="7e259-154">Plak de volgende code in een lege cel en druk op **Shift+Enter** om de code uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="7e259-154">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to run the code.</span></span> <span data-ttu-id="7e259-155">In de onderstaande code `%%sql` ('sql magic' genoemd) wordt de Jupyter-notebook geïnstrueerd om de vooraf ingestelde `sqlContext` te gebruiken voor het uitvoeren van de Hive-query.</span><span class="sxs-lookup"><span data-stu-id="7e259-155">In the code below `%%sql` (called the sql magic) tells Jupyter notebook to use the preset `sqlContext` to run the Hive query.</span></span> <span data-ttu-id="7e259-156">De query haalt de bovenste 10 rijen op van een Hive-tabel (**hivesampletable**) die standaard beschikbaar is in alle HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="7e259-156">The query retrieves the top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="7e259-157">![Hive-query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive-query in HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="7e259-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="7e259-158">Voor meer informatie over de context van de '`%%sql` magic' en de vooraf ingestelde waarden raadpleegt u [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md) (Voor een HDInsight-cluster beschikbare Jupyter-kernels).</span><span class="sxs-lookup"><span data-stu-id="7e259-158">For more information on the `%%sql` magic and the preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="7e259-159">Telkens wanneer u in Jupyter een query uitvoert, toont de venstertitel van uw webbrowser de status **(Bezet)** en de notebooktitel.</span><span class="sxs-lookup"><span data-stu-id="7e259-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="7e259-160">Ook ziet u een gevulde cirkel naast de **PySpark**-tekst in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="7e259-160">You also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="7e259-161">Wanneer de taak is voltooid, verandert deze in een lege cirkel.</span><span class="sxs-lookup"><span data-stu-id="7e259-161">After the job is completed, it changes to a hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="7e259-162">Het scherm moet worden vernieuwd om de query-uitvoer weer te geven.</span><span class="sxs-lookup"><span data-stu-id="7e259-162">The screen should refresh to show the query output.</span></span>

    <span data-ttu-id="7e259-163">![Uitvoer van Hive-query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Uitvoer van Hive-query in HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="7e259-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="7e259-164">Sluit de notebook af om de clusterresources vrij te geven nadat u de toepassing hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7e259-164">Shut down the notebook to release the cluster resources after you have finished running the application.</span></span> <span data-ttu-id="7e259-165">Dit doet u door in het menu **Bestand** in de notebook te klikken op **Sluiten en stoppen**.</span><span class="sxs-lookup"><span data-stu-id="7e259-165">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="7e259-166">Als u van plan bent de volgende stappen op een later tijdstip uit te voeren, zorg er dan voor dat u het HDInsight-cluster dat u in dit artikel hebt gemaakt, verwijdert.</span><span class="sxs-lookup"><span data-stu-id="7e259-166">If you plan to complete the next steps at a later time, make sure you delete the HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="7e259-167">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="7e259-167">Next step</span></span> 

<span data-ttu-id="7e259-168">In dit artikel hebt u geleerd hoe u een HDInsight Spark-cluster maakt en een eenvoudige Spark SQL-query uitvoert.</span><span class="sxs-lookup"><span data-stu-id="7e259-168">In this article you learned how to create an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="7e259-169">Ga naar het volgende artikel voor meer informatie over het gebruik van een HDInsight Spark-cluster om interactieve query's uit te voeren op voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="7e259-169">Advance to the next article to learn how to use an HDInsight Spark cluster to run interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="7e259-170">Interactieve query's uitvoeren op een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="7e259-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)




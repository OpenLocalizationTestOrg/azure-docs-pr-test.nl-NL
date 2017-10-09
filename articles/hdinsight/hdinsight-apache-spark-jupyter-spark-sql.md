---
title: aaaCreate een Apache Spark-cluster in Azure HDInsight | Microsoft Docs
description: HDInsight Spark Quick Start op hoe toocreate een Apache Spark-cluster in HDInsight.
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
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="4bafa-104">Een Apache Spark-cluster maken in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4bafa-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="4bafa-105">In dit artikel leert u hoe toocreate een Apache Spark-cluster in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4bafa-105">In this article, you learn how toocreate an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="4bafa-106">Zie [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md) voor informatie over Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4bafa-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="4bafa-107">![Quick Start-diagram met een beschrijving van stappen toocreate een Apache Spark-cluster in Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark snel aan de slag met Apache Spark in HDInsight. Geïllustreerde stappen: maken van een cluster; interactieve Spark-query uitvoeren")</span><span class="sxs-lookup"><span data-stu-id="4bafa-107">![Quickstart diagram describing steps toocreate an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4bafa-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4bafa-108">Prerequisites</span></span>

* <span data-ttu-id="4bafa-109">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="4bafa-109">**An Azure subscription**.</span></span> <span data-ttu-id="4bafa-110">Voordat u met deze zelfstudie begint, moet u een Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="4bafa-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="4bafa-111">Zie [Maak vandaag nog uw gratis Azure-account](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="4bafa-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="4bafa-112">HDInsight Spark-cluster maken</span><span class="sxs-lookup"><span data-stu-id="4bafa-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="4bafa-113">In deze sectie maakt u een HDInsight Spark-cluster met behulp van een [Azure Resource Manager-sjabloon](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span><span class="sxs-lookup"><span data-stu-id="4bafa-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="4bafa-114">Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md) voor andere methoden voor het maken van clusters.</span><span class="sxs-lookup"><span data-stu-id="4bafa-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="4bafa-115">Klik op Hallo installatiekopie tooopen Hallo sjabloon in hello Azure-portal te volgen.</span><span class="sxs-lookup"><span data-stu-id="4bafa-115">Click hello following image tooopen hello template in hello Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="4bafa-116">Voer Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="4bafa-116">Enter hello following values:</span></span>

    <span data-ttu-id="4bafa-117">![HDInsight Spark-cluster maken met behulp van een Azure Resource Manager-sjabloon](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Spark-cluster maken in HDInsight met behulp van een Azure Resource Manager-sjabloon")</span><span class="sxs-lookup"><span data-stu-id="4bafa-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="4bafa-118">**Abonnement**: selecteer uw Azure-abonnement voor dit cluster.</span><span class="sxs-lookup"><span data-stu-id="4bafa-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="4bafa-119">**Resourcegroep**: maak een nieuwe resourcegroep of selecteer een bestaande.</span><span class="sxs-lookup"><span data-stu-id="4bafa-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="4bafa-120">Resourcegroep is gebruikte toomanage Azure-resources voor uw projecten.</span><span class="sxs-lookup"><span data-stu-id="4bafa-120">Resource group is used toomanage Azure resources for your projects.</span></span>
    * <span data-ttu-id="4bafa-121">**Locatie**: Selecteer een locatie voor resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="4bafa-121">**Location**: Select a location for hello resource group.</span></span> <span data-ttu-id="4bafa-122">Hallo-sjabloon maakt gebruik van deze locatie voor het maken van Hallo cluster ook als voor Hallo standaard clusteropslag.</span><span class="sxs-lookup"><span data-stu-id="4bafa-122">hello template uses this location for creating hello cluster as well as for hello default cluster storage.</span></span>
    * <span data-ttu-id="4bafa-123">**Clusternaam**: Voer een naam voor Hallo HDInsight-cluster dat u wilt dat toocreate.</span><span class="sxs-lookup"><span data-stu-id="4bafa-123">**ClusterName**: Enter a name for hello HDInsight cluster that you want toocreate.</span></span>
    * <span data-ttu-id="4bafa-124">**Spark versie**: Selecteer **2.0** als Hallo-versie die u tooinstall op Hallo-cluster wilt.</span><span class="sxs-lookup"><span data-stu-id="4bafa-124">**Spark version**: Select **2.0** as hello version that you want tooinstall on hello cluster.</span></span>
    * <span data-ttu-id="4bafa-125">**Cluster-aanmeldingsnaam en wachtwoord**: Hallo standaardaanmeldnaam is admin.</span><span class="sxs-lookup"><span data-stu-id="4bafa-125">**Cluster login name and password**: hello default login name is admin.</span></span>
    * <span data-ttu-id="4bafa-126">**SSH-aanmeldgegevens**.</span><span class="sxs-lookup"><span data-stu-id="4bafa-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="4bafa-127">Noteer deze waarden.</span><span class="sxs-lookup"><span data-stu-id="4bafa-127">Write down these values.</span></span>  <span data-ttu-id="4bafa-128">U moet ze later in de zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="4bafa-128">You need them later in hello tutorial.</span></span>

3. <span data-ttu-id="4bafa-129">Selecteer **ik ga akkoord toohello voorwaarden bovengenoemde**, selecteer **pincode toodashboard**, en klik vervolgens op **aankoop**.</span><span class="sxs-lookup"><span data-stu-id="4bafa-129">Select **I agree toohello terms and conditions stated above**, select **Pin toodashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="4bafa-130">U ziet een nieuwe tegel met de titel Implementatie indienen voor Sjabloonimplementatie.</span><span class="sxs-lookup"><span data-stu-id="4bafa-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="4bafa-131">Het duurt ongeveer 20 minuten toocreate Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="4bafa-131">It takes about 20 minutes toocreate hello cluster.</span></span>

<span data-ttu-id="4bafa-132">Als u een probleem met het maken van HDInsight-clusters, kan het zijn dat u geen Hallo juiste machtigingen toodo dus hebt.</span><span class="sxs-lookup"><span data-stu-id="4bafa-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have hello right permissions toodo so.</span></span> <span data-ttu-id="4bafa-133">Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4bafa-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="4bafa-134">In dit artikel maakt u een Spark-cluster dat gebruik maakt [Azure Storage-Blobs als Hallo cluster opslag](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="4bafa-134">This article creates a Spark cluster that uses [Azure Storage Blobs as hello cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="4bafa-135">U kunt ook een Spark-cluster maakt gebruik van maken [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) als Hallo standaard opslag.</span><span class="sxs-lookup"><span data-stu-id="4bafa-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as hello default storage.</span></span> <span data-ttu-id="4bafa-136">Zie [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) (Een HDInsight-cluster maken met Data Lake Store) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="4bafa-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="4bafa-137">Een Hive-query uitvoeren met Spark SQL</span><span class="sxs-lookup"><span data-stu-id="4bafa-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="4bafa-138">Als u een Jupyter-notebook geconfigureerd voor uw HDInsight Spark-cluster gebruikt, krijgt u een vooraf ingestelde `sqlContext` waarmee u kunt toorun Hive-query's met behulp van Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="4bafa-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use toorun Hive queries using Spark SQL.</span></span> <span data-ttu-id="4bafa-139">In deze sectie leest u hoe een Jupyter-notebook toostart en voer vervolgens een eenvoudige Hive-query.</span><span class="sxs-lookup"><span data-stu-id="4bafa-139">In this section, you learn how toostart a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="4bafa-140">Open Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4bafa-140">Open hello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="4bafa-141">Als u toopin Hallo cluster toohello-dashboard hebt gekozen, klikt u op Hallo cluster tegel Hallo dashboard toolaunch Hallo cluster blade.</span><span class="sxs-lookup"><span data-stu-id="4bafa-141">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="4bafa-142">Als u niet Hallo cluster toohello dashboard in het linkerdeelvenster hello vastmaken, klikt u op **HDInsight-clusters**, en klik vervolgens op Hallo cluster die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4bafa-142">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="4bafa-143">Klik in **Snelkoppelingen** op **Clusterdashboards** en klik vervolgens op **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="4bafa-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="4bafa-144">Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="4bafa-144">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="4bafa-145">![Open Jupyter-notebook toorun interactieve Spark SQL-query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter-notebook toorun interactieve Spark SQL-query")</span><span class="sxs-lookup"><span data-stu-id="4bafa-145">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="4bafa-146">Hallo Jupyter-notebook zijn ook toegankelijk voor uw cluster door openen Hallo URL te volgen in uw browser.</span><span class="sxs-lookup"><span data-stu-id="4bafa-146">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="4bafa-147">Vervang **CLUSTERNAME** met Hallo-naam van het cluster:</span><span class="sxs-lookup"><span data-stu-id="4bafa-147">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="4bafa-148">Maak een notebook.</span><span class="sxs-lookup"><span data-stu-id="4bafa-148">Create a notebook.</span></span> <span data-ttu-id="4bafa-149">Klik op **Nieuw** en klik vervolgens op **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="4bafa-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="4bafa-150">![Maken van een Jupyter-notebook toorun interactieve Spark SQL-query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "maken van een Jupyter-notebook toorun interactieve Spark SQL-query")</span><span class="sxs-lookup"><span data-stu-id="4bafa-150">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="4bafa-151">Een nieuwe notebook gemaakt en geopend met de naam van de Hallo Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="4bafa-151">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="4bafa-152">Klik op Hallo notebook naam Hallo boven en een beschrijvende naam invoeren als u wilt.</span><span class="sxs-lookup"><span data-stu-id="4bafa-152">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="4bafa-153">![Geef een naam op voor Hallo Jupter notebook toorun interactieve Spark query van](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "voor Hallo Jupter notebook toorun interactieve Spark query van een naam opgeven")</span><span class="sxs-lookup"><span data-stu-id="4bafa-153">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5.  <span data-ttu-id="4bafa-154">Plakken Hallo volgende code in een lege cel en druk vervolgens op **SHIFT + ENTER** toorun Hallo code.</span><span class="sxs-lookup"><span data-stu-id="4bafa-154">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="4bafa-155">In onderstaande Hallo code `%%sql` (aangeroepen Hallo sql magic) vertelt Jupyter-notebook toouse Hallo voorinstelling `sqlContext` toorun Hallo Hive-query.</span><span class="sxs-lookup"><span data-stu-id="4bafa-155">In hello code below `%%sql` (called hello sql magic) tells Jupyter notebook toouse hello preset `sqlContext` toorun hello Hive query.</span></span> <span data-ttu-id="4bafa-156">Hallo query top 10 rijen Hallo opgehaald uit een Hive-tabel (**hivesampletable**) die is standaard beschikbaar in alle HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="4bafa-156">hello query retrieves hello top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="4bafa-157">![Hive-query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive-query in HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="4bafa-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="4bafa-158">Voor meer informatie over Hallo `%%sql` magic en Hallo voorinstelling contexten, Zie [Jupyter beschikbare kernels voor een HDInsight-cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="4bafa-158">For more information on hello `%%sql` magic and hello preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="4bafa-159">Telkens wanneer u een query in Jupyter uitvoert, ziet u de venstertitel van uw web-browser een **(bezet)** status samen met de notebooktitel Hallo.</span><span class="sxs-lookup"><span data-stu-id="4bafa-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="4bafa-160">U ziet ook een gevulde cirkel volgende toohello **PySpark** tekst in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="4bafa-160">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="4bafa-161">Nadat het Hallo-taak is voltooid, verandert deze tooa lege cirkel.</span><span class="sxs-lookup"><span data-stu-id="4bafa-161">After hello job is completed, it changes tooa hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="4bafa-162">welkomstscherm moet uitvoer van tooshow Hallo query vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="4bafa-162">hello screen should refresh tooshow hello query output.</span></span>

    <span data-ttu-id="4bafa-163">![Uitvoer van Hive-query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Uitvoer van Hive-query in HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="4bafa-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="4bafa-164">Hallo-notebook toorelease Hallo-clusterbronnen afgesloten nadat u klaar bent met het uitvoeren van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="4bafa-164">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="4bafa-165">toodo geval is, uit Hallo **bestand** menu op Hallo laptop, klikt u op **sluiten en stoppen**.</span><span class="sxs-lookup"><span data-stu-id="4bafa-165">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="4bafa-166">Als u van plan toocomplete Hallo volgende stappen op een later tijdstip bent, zorg er dan voor dat u Hallo HDInsight cluster die u hebt gemaakt in dit artikel verwijdert.</span><span class="sxs-lookup"><span data-stu-id="4bafa-166">If you plan toocomplete hello next steps at a later time, make sure you delete hello HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="4bafa-167">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="4bafa-167">Next step</span></span> 

<span data-ttu-id="4bafa-168">In dit artikel hebt u geleerd hoe toocreate een HDInsight Spark-cluster en voer een basic Spark SQL-query.</span><span class="sxs-lookup"><span data-stu-id="4bafa-168">In this article you learned how toocreate an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="4bafa-169">Ga toohello volgende artikel toolearn hoe toouse een HDInsight Spark-cluster toorun interactieve query's op voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="4bafa-169">Advance toohello next article toolearn how toouse an HDInsight Spark cluster toorun interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="4bafa-170">Interactieve query's uitvoeren op een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="4bafa-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)




---
title: Apache Spark gestructureerde streamen met Kafka - Azure HDInsight | Microsoft Docs
description: Informatie over het gebruik van Apache Spark-streaming (DStream) om gegevens van of naar Apache Kafka. In dit voorbeeld kunt u gegevens met behulp van een Jupyter-notebook in Spark in HDInsight streamen.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 02b49e13e8f54c3d55310f4d2b21c7e09c91fe81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="52e18-104">Gestructureerde Streaming van Spark met Kafka (preview) op HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="52e18-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="52e18-105">Informatie over het gebruik van gestructureerde Spark-Streaming gegevens lezen uit Apache Kafka in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="52e18-105">Learn how to use Spark Structured Streaming to read data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="52e18-106">Spark gestructureerd streaming is een stream-verwerkingsengine gebouwd op Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="52e18-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="52e18-107">Hiermee kunt u streaming berekeningen Express hetzelfde zijn als batch berekening op statische gegevens.</span><span class="sxs-lookup"><span data-stu-id="52e18-107">It allows you to express streaming computations the same as batch computation on static data.</span></span> <span data-ttu-id="52e18-108">Zie voor meer informatie over het gestructureerde Streaming de [gestructureerde Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) op Apache.org.</span><span class="sxs-lookup"><span data-stu-id="52e18-108">For more information on Structured Streaming, see the [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52e18-109">In dit voorbeeld gebruikt 2.1 Spark in HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="52e18-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="52e18-110">Gestructureerde Streaming wordt beschouwd als __alpha__ op Spark 2.1.</span><span class="sxs-lookup"><span data-stu-id="52e18-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="52e18-111">De stappen in dit document wordt een Azure-resourcegroep met zowel een Spark in HDInsight en een Kafka op HDInsight-cluster maken</span><span class="sxs-lookup"><span data-stu-id="52e18-111">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="52e18-112">Deze clusters zijn beide zich binnen een virtueel netwerk van Azure, waardoor het Spark-cluster rechtstreeks communiceren met de Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="52e18-112">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="52e18-113">Wanneer u klaar bent met de stappen in dit document, vergeet niet de clusters om te voorkomen dat de overtollige kosten te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="52e18-113">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="52e18-114">Clusters maken</span><span class="sxs-lookup"><span data-stu-id="52e18-114">Create the clusters</span></span>

<span data-ttu-id="52e18-115">Apache Kafka op HDInsight biedt geen toegang voor de beleggingsmakelaars Kafka via het openbare internet.</span><span class="sxs-lookup"><span data-stu-id="52e18-115">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="52e18-116">Alles wat wordt gesproken naar Kafka moet zich in hetzelfde virtuele netwerk van Azure als de knooppunten in het cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="52e18-116">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="52e18-117">In dit voorbeeld worden de Kafka- en Spark-clusters bevinden zich in een Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="52e18-117">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="52e18-118">Het volgende diagram toont hoe de communicatie tussen clusters stroomt:</span><span class="sxs-lookup"><span data-stu-id="52e18-118">The following diagram shows how communication flows between the clusters:</span></span>

![Diagram van Spark en Kafka clusters in een Azure-netwerk](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="52e18-120">De service Kafka is beperkt tot communicatie binnen het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="52e18-120">The Kafka service is limited to communication within the virtual network.</span></span> <span data-ttu-id="52e18-121">Andere services op het cluster, zoals SSH en Ambari, zijn toegankelijk via het internet.</span><span class="sxs-lookup"><span data-stu-id="52e18-121">Other services on the cluster, such as SSH and Ambari, can be accessed over the internet.</span></span> <span data-ttu-id="52e18-122">Zie voor meer informatie over de openbare poorten beschikbaar met HDInsight [poorten en URI's die worden gebruikt door HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="52e18-122">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="52e18-123">U kunt een Azure-netwerk Kafka, maken en handmatig Spark-clusters, is het ook eenvoudiger te gebruiken van een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="52e18-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="52e18-124">Gebruik de volgende stappen voor het implementeren van een Azure-netwerk Kafka, en Spark-clusters met uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="52e18-124">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="52e18-125">Gebruik de volgende knop om te melden bij Azure en opent u de sjabloon in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="52e18-125">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="52e18-126">De Azure Resource Manager-sjabloon bevindt zich op **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span><span class="sxs-lookup"><span data-stu-id="52e18-126">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="52e18-127">Deze sjabloon maakt u de volgende bronnen:</span><span class="sxs-lookup"><span data-stu-id="52e18-127">This template creates the following resources:</span></span>

    * <span data-ttu-id="52e18-128">Een Kafka op 3.5 HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="52e18-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="52e18-129">Een Spark in HDInsight 3.6 cluster.</span><span class="sxs-lookup"><span data-stu-id="52e18-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="52e18-130">Een virtueel netwerk in Azure die de HDInsight-clusters bevat.</span><span class="sxs-lookup"><span data-stu-id="52e18-130">An Azure Virtual Network, which contains the HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="52e18-131">De gestructureerde streaming laptop gebruikt in dit voorbeeld vereist Spark in HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="52e18-131">The structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="52e18-132">Als u een eerdere versie van Spark in HDInsight gebruikt, ontvangt u fouten bij gebruik van de notebook.</span><span class="sxs-lookup"><span data-stu-id="52e18-132">If you use an earlier version of Spark on HDInsight, you receive errors when using the notebook.</span></span>

2. <span data-ttu-id="52e18-133">Gebruik de volgende informatie voor het vullen van de vermeldingen op de **aangepaste implementatie** blade:</span><span class="sxs-lookup"><span data-stu-id="52e18-133">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Aangepaste HDInsight-implementatie](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="52e18-135">**Resourcegroep**: Maak een groep of een bestaande set selecteren.</span><span class="sxs-lookup"><span data-stu-id="52e18-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="52e18-136">Deze groep bevat het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="52e18-136">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="52e18-137">**Locatie**: Selecteer een locatie geografisch dicht bij u.</span><span class="sxs-lookup"><span data-stu-id="52e18-137">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="52e18-138">**Clusternaam baseren**: deze waarde wordt gebruikt als de basisnaam aan voor de Spark en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="52e18-138">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="52e18-139">Bijvoorbeeld, voeren **hdi** maakt een Spark-cluster spark hdi__ met de naam en een Kafka-cluster met de naam **kafka hdi**.</span><span class="sxs-lookup"><span data-stu-id="52e18-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="52e18-140">**Aanmeldingsnaam van gebruiker cluster**: de beheerdersgebruikersnaam voor Spark en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="52e18-140">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="52e18-141">**Aanmeldingswachtwoord cluster**: het beheerderswachtwoord voor de Spark en Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="52e18-141">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="52e18-142">**SSH-gebruikersnaam**: de SSH-gebruiker maken voor Spark en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="52e18-142">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="52e18-143">**SSH-wachtwoord**: het wachtwoord voor de SSH-gebruiker voor de Spark en Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="52e18-143">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="52e18-144">Lees de **voorwaarden en bepalingen**, en selecteer vervolgens **ik ga akkoord met de voorwaarden en bepalingen bovengenoemde**.</span><span class="sxs-lookup"><span data-stu-id="52e18-144">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="52e18-145">Controleer ten slotte **vastmaken aan dashboard** en selecteer vervolgens **aankoop**.</span><span class="sxs-lookup"><span data-stu-id="52e18-145">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="52e18-146">Het duurt ongeveer 20 minuten om de clusters te maken.</span><span class="sxs-lookup"><span data-stu-id="52e18-146">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="52e18-147">Zodra de resources zijn gemaakt, wordt u omgeleid naar de blade met resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="52e18-147">Once the resources have been created, you are redirected to the resource group blade.</span></span>

![Resourcegroepblade voor het vnet en clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="52e18-149">Merk op dat de namen van de HDInsight-clusters **spark BASENAME** en **kafka BASENAME**, waarbij BASENAME is de naam die u hebt opgegeven in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="52e18-149">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="52e18-150">U kunt deze namen in latere stappen gebruiken bij het verbinden met de clusters.</span><span class="sxs-lookup"><span data-stu-id="52e18-150">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="get-the-kafka-brokers"></a><span data-ttu-id="52e18-151">De Kafka beleggingsmakelaars ophalen</span><span class="sxs-lookup"><span data-stu-id="52e18-151">Get the Kafka brokers</span></span>

<span data-ttu-id="52e18-152">De code in dit voorbeeld maakt verbinding met de Kafka broker hosts in het cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="52e18-152">The code in this example connects to the Kafka broker hosts in the Kafka cluster.</span></span> <span data-ttu-id="52e18-153">Gebruik de Kafka broker hosts vindt het volgende PowerShell- of Bash-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="52e18-153">To find the Kafka broker hosts, use the following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
$clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> <span data-ttu-id="52e18-154">In dit voorbeeld verwacht `$PASSWORD` bevat het wachtwoord voor de cluster-aanmelding en `$CLUSTERNAME` bevat de naam van het cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="52e18-154">This example expects `$PASSWORD` to contain the password for the cluster login, and `$CLUSTERNAME` to contain the name of the Kafka cluster.</span></span>
>
> <span data-ttu-id="52e18-155">In dit voorbeeld wordt de [jq](https://stedolan.github.io/jq/) hulpprogramma voor het parseren van gegevens buiten het JSON-document.</span><span class="sxs-lookup"><span data-stu-id="52e18-155">This example uses the [jq](https://stedolan.github.io/jq/) utility to parse data out of the JSON document.</span></span>

<span data-ttu-id="52e18-156">De uitvoer lijkt op het volgende:</span><span class="sxs-lookup"><span data-stu-id="52e18-156">The output is similar to the following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="52e18-157">Deze gegevens niet opslaan omdat het wordt gebruikt in de volgende secties van dit document.</span><span class="sxs-lookup"><span data-stu-id="52e18-157">Save this information, as it is used in the following sections of this document.</span></span>

## <a name="get-the-notebooks"></a><span data-ttu-id="52e18-158">De laptops ophalen</span><span class="sxs-lookup"><span data-stu-id="52e18-158">Get the notebooks</span></span>

<span data-ttu-id="52e18-159">De code voor het voorbeeld in dit document beschreven is beschikbaar op [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span><span class="sxs-lookup"><span data-stu-id="52e18-159">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-the-notebooks"></a><span data-ttu-id="52e18-160">De laptops uploaden</span><span class="sxs-lookup"><span data-stu-id="52e18-160">Upload the notebooks</span></span>

<span data-ttu-id="52e18-161">Gebruik de volgende stappen voor het uploaden van de laptops van het project met uw Spark in HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="52e18-161">Use the following steps to upload the notebooks from the project to your Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="52e18-162">In uw webbrowser verbinding maken met de Jupyter-notebook in Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="52e18-162">In your web browser, connect to the Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="52e18-163">Vervang in de volgende URL `CLUSTERNAME` met de naam van uw cluster Kafka:</span><span class="sxs-lookup"><span data-stu-id="52e18-163">In the following URL, replace `CLUSTERNAME` with the name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="52e18-164">Wanneer u wordt gevraagd, typt u de cluster-aanmelding (admin) en het wachtwoord die worden gebruikt wanneer u het cluster hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="52e18-164">When prompted, enter the cluster login (admin) and password used when you created the cluster.</span></span>

2. <span data-ttu-id="52e18-165">Gebruik vanaf boven aan de rechterkant van de pagina, de __uploaden__ knop voor het uploaden van de __stroom Tweets To_Kafka.ipynb__ bestand aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="52e18-165">From the upper right side of the page, use the __Upload__ button to upload the __Stream-Tweets-To_Kafka.ipynb__ file to the cluster.</span></span> <span data-ttu-id="52e18-166">Selecteer __Open__ het uploaden wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="52e18-166">Select __Open__ to start the upload.</span></span>

    ![Gebruik de knop uploaden te selecteren en een laptop uploaden](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Selecteer het bestand KafkaStreaming.ipynb](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="52e18-169">Zoeken naar de __stroom Tweets To_Kafka.ipynb__ vermelding in de lijst van notitieblokken en selecteer __uploaden__ knop ernaast.</span><span class="sxs-lookup"><span data-stu-id="52e18-169">Find the __Stream-Tweets-To_Kafka.ipynb__ entry in the list of notebooks, and select __Upload__ button beside it.</span></span>

    ![Gebruik de knop uploaden naast de vermelding KafkaStreaming.ipynb te uploaden naar de server notebook](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="52e18-171">Herhaal stap 1-3 laden van de __Spark-gestructureerd-Streaming-van-Kafka.ipynb__ notebook.</span><span class="sxs-lookup"><span data-stu-id="52e18-171">Repeat steps 1-3 to load the __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="52e18-172">Tweets in Kafka laden</span><span class="sxs-lookup"><span data-stu-id="52e18-172">Load tweets into Kafka</span></span>

<span data-ttu-id="52e18-173">Zodra de bestanden zijn geüpload, selecteert u de __stroom Tweets To_Kafka.ipynb__ vermelding de notebook te openen.</span><span class="sxs-lookup"><span data-stu-id="52e18-173">Once the files have been uploaded, select the __Stream-Tweets-To_Kafka.ipynb__ entry to open the notebook.</span></span> <span data-ttu-id="52e18-174">Volg de stappen in de notebook tweets in Kafka laden.</span><span class="sxs-lookup"><span data-stu-id="52e18-174">Follow the steps in the notebook to load tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="52e18-175">Proces tweets met gestructureerde Spark-Streaming</span><span class="sxs-lookup"><span data-stu-id="52e18-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="52e18-176">Selecteer in de startpagina Jupyter-Notebook de __Spark-gestructureerd-Streaming-van-Kafka.ipynb__ vermelding.</span><span class="sxs-lookup"><span data-stu-id="52e18-176">From the Jupyter Notebook home page, select the __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="52e18-177">Volg de stappen in de notebook tweets laden vanaf Kafka met gestructureerde Spark-Streaming.</span><span class="sxs-lookup"><span data-stu-id="52e18-177">Follow the steps in the notebook to load tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52e18-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="52e18-178">Next steps</span></span>

<span data-ttu-id="52e18-179">U hebt geleerd hoe u gestructureerde Spark-Streaming, Zie de volgende documenten voor meer informatie over het werken met Spark en Kafka:</span><span class="sxs-lookup"><span data-stu-id="52e18-179">Now that you have learned how to use Spark Structured Streaming, see the following documents to learn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="52e18-180">[Het gebruik van Spark-streaming (DStream) met Kafka](hdinsight-apache-spark-with-kafka.md).</span><span class="sxs-lookup"><span data-stu-id="52e18-180">[How to use Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="52e18-181">Beginnen met Jupyter-Notebook en Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="52e18-181">Start with Jupyter Notebook and Spark on HDInsight</span></span>](hdinsight-apache-spark-jupyter-spark-sql.md)
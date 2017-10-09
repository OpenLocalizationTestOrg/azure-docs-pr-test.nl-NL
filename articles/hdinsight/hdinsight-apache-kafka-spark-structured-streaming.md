---
title: aaaApache gestructureerde Streaming van Spark met Kafka - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Apache Spark (DStream) tooget streaminggegevens van of naar Apache Kafka. In dit voorbeeld kunt u gegevens met behulp van een Jupyter-notebook in Spark in HDInsight streamen.
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
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="f8839-104">Gestructureerde Streaming van Spark met Kafka (preview) op HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="f8839-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="f8839-105">Meer informatie over hoe toouse tooread gegevens gestructureerde Spark-Streaming van Apache Kafka in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8839-105">Learn how toouse Spark Structured Streaming tooread data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="f8839-106">Spark gestructureerd streaming is een stream-verwerkingsengine gebouwd op Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="f8839-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="f8839-107">Hiermee kunt dat u tooexpress streaming berekeningen Hallo hetzelfde als batch berekening op statische gegevens.</span><span class="sxs-lookup"><span data-stu-id="f8839-107">It allows you tooexpress streaming computations hello same as batch computation on static data.</span></span> <span data-ttu-id="f8839-108">Zie voor meer informatie over het gestructureerde Streaming Hallo [gestructureerde Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) op Apache.org.</span><span class="sxs-lookup"><span data-stu-id="f8839-108">For more information on Structured Streaming, see hello [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8839-109">In dit voorbeeld gebruikt 2.1 Spark in HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="f8839-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="f8839-110">Gestructureerde Streaming wordt beschouwd als __alpha__ op Spark 2.1.</span><span class="sxs-lookup"><span data-stu-id="f8839-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="f8839-111">Hallo stappen in dit document wordt een Azure-resourcegroep met zowel een Spark in HDInsight en een Kafka op HDInsight-cluster maken</span><span class="sxs-lookup"><span data-stu-id="f8839-111">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="f8839-112">Deze clusters zijn beide zich binnen een virtueel netwerk van Azure, waardoor Hallo Spark-cluster toodirectly communiceren met de Hallo Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="f8839-112">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="f8839-113">Wanneer u klaar bent met de stappen in dit document Hallo onthouden toodelete Hallo clusters tooavoid overtollige kosten.</span><span class="sxs-lookup"><span data-stu-id="f8839-113">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="f8839-114">Hallo-clusters maken</span><span class="sxs-lookup"><span data-stu-id="f8839-114">Create hello clusters</span></span>

<span data-ttu-id="f8839-115">Apache Kafka op HDInsight biedt geen toegang tot toohello Kafka beleggingsmakelaars via openbaar internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="f8839-115">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="f8839-116">Alles wat vertelt tooKafka moet zich in hetzelfde virtuele Azure-netwerk als knooppunten in Hallo HALLO hallo Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="f8839-116">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="f8839-117">Bijvoorbeeld, bevinden zowel hello Kafka- en Spark-clusters zich in een Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="f8839-117">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="f8839-118">Hallo volgende diagram ziet u hoe de communicatie tussen clusters met Hallo loopt:</span><span class="sxs-lookup"><span data-stu-id="f8839-118">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagram van Spark en Kafka clusters in een Azure-netwerk](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="f8839-120">Hallo Kafka-service is beperkt toocommunication in Hallo virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="f8839-120">hello Kafka service is limited toocommunication within hello virtual network.</span></span> <span data-ttu-id="f8839-121">Andere services op Hallo cluster Hallo zoals SSH en Ambari, toegankelijk is via internet.</span><span class="sxs-lookup"><span data-stu-id="f8839-121">Other services on hello cluster, such as SSH and Ambari, can be accessed over hello internet.</span></span> <span data-ttu-id="f8839-122">Zie voor meer informatie over Hallo openbare poorten beschikbaar met HDInsight [poorten en URI's die worden gebruikt door HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="f8839-122">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="f8839-123">U kunt een Azure-netwerk, Kafka en Spark clusters handmatig maken, is het eenvoudiger toouse een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f8839-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="f8839-124">Gebruik Hallo volgende stappen uit voor een Azure-netwerk Kafka, toodeploy en Spark-clusters tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f8839-124">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="f8839-125">Hallo na de knop toosign in tooAzure en open Hallo-sjabloon in hello Azure-portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f8839-125">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="f8839-126">Hello Azure Resource Manager-sjabloon bevindt zich op **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span><span class="sxs-lookup"><span data-stu-id="f8839-126">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="f8839-127">Met deze sjabloon maakt Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="f8839-127">This template creates hello following resources:</span></span>

    * <span data-ttu-id="f8839-128">Een Kafka op 3.5 HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="f8839-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="f8839-129">Een Spark in HDInsight 3.6 cluster.</span><span class="sxs-lookup"><span data-stu-id="f8839-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="f8839-130">Een virtueel netwerk in Azure die Hallo HDInsight-clusters bevat.</span><span class="sxs-lookup"><span data-stu-id="f8839-130">An Azure Virtual Network, which contains hello HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f8839-131">Hallo gestructureerde streaming-notebook gebruikt in dit voorbeeld vereist Spark in HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="f8839-131">hello structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="f8839-132">Als u een eerdere versie van Spark in HDInsight, er fouten als Hallo notebook.</span><span class="sxs-lookup"><span data-stu-id="f8839-132">If you use an earlier version of Spark on HDInsight, you receive errors when using hello notebook.</span></span>

2. <span data-ttu-id="f8839-133">Gebruik Hallo informatie toopopulate Hallo vermeldingen op Hallo volgen **aangepaste implementatie** blade:</span><span class="sxs-lookup"><span data-stu-id="f8839-133">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Aangepaste HDInsight-implementatie](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="f8839-135">**Resourcegroep**: Maak een groep of een bestaande set selecteren.</span><span class="sxs-lookup"><span data-stu-id="f8839-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="f8839-136">Deze groep bevat Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="f8839-136">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="f8839-137">**Locatie**: Selecteer een locatie geografisch sluiten tooyou.</span><span class="sxs-lookup"><span data-stu-id="f8839-137">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="f8839-138">**Clusternaam baseren**: deze waarde wordt gebruikt als basisnaam voor Hallo Spark en Kafka clusters Hallo.</span><span class="sxs-lookup"><span data-stu-id="f8839-138">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="f8839-139">Bijvoorbeeld, voeren **hdi** maakt een Spark-cluster spark hdi__ met de naam en een Kafka-cluster met de naam **kafka hdi**.</span><span class="sxs-lookup"><span data-stu-id="f8839-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="f8839-140">**Aanmeldingsnaam van gebruiker cluster**: Hallo-beheerdersgebruikersnaam voor Hallo Spark en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="f8839-140">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="f8839-141">**Aanmeldingswachtwoord cluster**: Hallo beheerder gebruikerswachtwoord voor Hallo Spark en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="f8839-141">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="f8839-142">**SSH-gebruikersnaam**: Hallo SSH gebruiker toocreate voor Hallo Spark en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="f8839-142">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="f8839-143">**SSH-wachtwoord**: Hallo-wachtwoord voor Hallo SSH-gebruiker voor Hallo Spark en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="f8839-143">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="f8839-144">Lees Hallo **voorwaarden en bepalingen**, en selecteer vervolgens **ik ga akkoord toohello voorwaarden bovengenoemde**.</span><span class="sxs-lookup"><span data-stu-id="f8839-144">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="f8839-145">Controleer ten slotte **pincode toodashboard** en selecteer vervolgens **aankoop**.</span><span class="sxs-lookup"><span data-stu-id="f8839-145">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="f8839-146">Het duurt ongeveer 20 minuten toocreate Hallo-clusters.</span><span class="sxs-lookup"><span data-stu-id="f8839-146">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="f8839-147">Zodra het Hallo-resources zijn gemaakt, bent u omgeleide toohello resourcegroepblade.</span><span class="sxs-lookup"><span data-stu-id="f8839-147">Once hello resources have been created, you are redirected toohello resource group blade.</span></span>

![Resourcegroepblade voor Hallo vnet en clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="f8839-149">Merk op dat de namen van HDInsight-clusters Hallo Hallo zijn **spark BASENAME** en **kafka BASENAME**, waarbij BASENAME Hallo-naam die u hebt opgegeven toohello sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f8839-149">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="f8839-150">U deze namen in latere stappen gebruiken om verbinding te maken van clusters toohello.</span><span class="sxs-lookup"><span data-stu-id="f8839-150">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="get-hello-kafka-brokers"></a><span data-ttu-id="f8839-151">Hallo Kafka beleggingsmakelaars ophalen</span><span class="sxs-lookup"><span data-stu-id="f8839-151">Get hello Kafka brokers</span></span>

<span data-ttu-id="f8839-152">Hallo code in dit voorbeeld maakt verbinding toohello Kafka-hosts in Hallo Kafka cluster broker.</span><span class="sxs-lookup"><span data-stu-id="f8839-152">hello code in this example connects toohello Kafka broker hosts in hello Kafka cluster.</span></span> <span data-ttu-id="f8839-153">toofind hello Kafka broker hosts, gebruikt u Hallo PowerShell- of Bash voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="f8839-153">toofind hello Kafka broker hosts, use hello following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
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
> <span data-ttu-id="f8839-154">In dit voorbeeld verwacht `$PASSWORD` toocontain Hallo wachtwoord voor aanmelding Hallo-cluster, en `$CLUSTERNAME` toocontain Hallo naam Hallo Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="f8839-154">This example expects `$PASSWORD` toocontain hello password for hello cluster login, and `$CLUSTERNAME` toocontain hello name of hello Kafka cluster.</span></span>
>
> <span data-ttu-id="f8839-155">In dit voorbeeld wordt Hallo [jq](https://stedolan.github.io/jq/) hulpprogramma tooparse gegevens buiten Hallo JSON-document.</span><span class="sxs-lookup"><span data-stu-id="f8839-155">This example uses hello [jq](https://stedolan.github.io/jq/) utility tooparse data out of hello JSON document.</span></span>

<span data-ttu-id="f8839-156">Hallo uitvoer is vergelijkbaar toohello de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="f8839-156">hello output is similar toohello following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="f8839-157">Deze gegevens niet opslaan omdat het wordt gebruikt in de volgende secties van dit document Hallo.</span><span class="sxs-lookup"><span data-stu-id="f8839-157">Save this information, as it is used in hello following sections of this document.</span></span>

## <a name="get-hello-notebooks"></a><span data-ttu-id="f8839-158">Hallo-laptops ophalen</span><span class="sxs-lookup"><span data-stu-id="f8839-158">Get hello notebooks</span></span>

<span data-ttu-id="f8839-159">Hallo code Hallo zoals beschreven in dit document is beschikbaar op [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span><span class="sxs-lookup"><span data-stu-id="f8839-159">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-hello-notebooks"></a><span data-ttu-id="f8839-160">Hallo-laptops uploaden</span><span class="sxs-lookup"><span data-stu-id="f8839-160">Upload hello notebooks</span></span>

<span data-ttu-id="f8839-161">Volgende stappen tooupload Hallo notitieblokken uit Hallo project tooyour Spark in HDInsight-cluster hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f8839-161">Use hello following steps tooupload hello notebooks from hello project tooyour Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="f8839-162">In uw webbrowser verbinding toohello Jupyter-notebook in Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="f8839-162">In your web browser, connect toohello Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="f8839-163">Hallo-URL, na Vervang in `CLUSTERNAME` met de naam van uw cluster Kafka Hallo:</span><span class="sxs-lookup"><span data-stu-id="f8839-163">In hello following URL, replace `CLUSTERNAME` with hello name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="f8839-164">Voer desgevraagd Hallo cluster aanmeldingsnaam (admin) en het wachtwoord die worden gebruikt wanneer u Hallo cluster hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f8839-164">When prompted, enter hello cluster login (admin) and password used when you created hello cluster.</span></span>

2. <span data-ttu-id="f8839-165">Gebruik vanaf Hallo bovenste rechts Hallo pagina, Hallo __uploaden__ knop tooupload hello __stroom Tweets To_Kafka.ipynb__ toohello bestandscluster.</span><span class="sxs-lookup"><span data-stu-id="f8839-165">From hello upper right side of hello page, use hello __Upload__ button tooupload hello __Stream-Tweets-To_Kafka.ipynb__ file toohello cluster.</span></span> <span data-ttu-id="f8839-166">Selecteer __Open__ toostart Hallo uploaden.</span><span class="sxs-lookup"><span data-stu-id="f8839-166">Select __Open__ toostart hello upload.</span></span>

    ![Hallo uploaden knop tooselect gebruiken en een laptop te uploaden](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Hallo KafkaStreaming.ipynb bestand selecteren](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="f8839-169">Hallo zoeken __stroom Tweets To_Kafka.ipynb__ vermelding in de lijst Hallo van notitieblokken en selecteer __uploaden__ knop ernaast.</span><span class="sxs-lookup"><span data-stu-id="f8839-169">Find hello __Stream-Tweets-To_Kafka.ipynb__ entry in hello list of notebooks, and select __Upload__ button beside it.</span></span>

    ![Gebruik Hallo uploaden knop naast Hallo KafkaStreaming.ipynb vermelding tooupload het toohello notebook server](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="f8839-171">Herhaal stap 1-3 tooload hello __Spark-gestructureerd-Streaming-van-Kafka.ipynb__ notebook.</span><span class="sxs-lookup"><span data-stu-id="f8839-171">Repeat steps 1-3 tooload hello __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="f8839-172">Tweets in Kafka laden</span><span class="sxs-lookup"><span data-stu-id="f8839-172">Load tweets into Kafka</span></span>

<span data-ttu-id="f8839-173">Zodra het Hallo-bestanden zijn geüpload, selecteert u Hallo __stroom Tweets To_Kafka.ipynb__ vermelding tooopen Hallo notebook.</span><span class="sxs-lookup"><span data-stu-id="f8839-173">Once hello files have been uploaded, select hello __Stream-Tweets-To_Kafka.ipynb__ entry tooopen hello notebook.</span></span> <span data-ttu-id="f8839-174">Stappen Hallo in Hallo notebook tooload tweets in Kafka.</span><span class="sxs-lookup"><span data-stu-id="f8839-174">Follow hello steps in hello notebook tooload tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="f8839-175">Proces tweets met gestructureerde Spark-Streaming</span><span class="sxs-lookup"><span data-stu-id="f8839-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="f8839-176">Hallo Jupyter-Notebook startpagina, selecteer Hallo __Spark-gestructureerd-Streaming-van-Kafka.ipynb__ vermelding.</span><span class="sxs-lookup"><span data-stu-id="f8839-176">From hello Jupyter Notebook home page, select hello __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="f8839-177">Stappen Hallo in Hallo notebook tooload tweets van Kafka met gestructureerde Spark-Streaming.</span><span class="sxs-lookup"><span data-stu-id="f8839-177">Follow hello steps in hello notebook tooload tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8839-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f8839-178">Next steps</span></span>

<span data-ttu-id="f8839-179">U hebt geleerd hoe toouse Spark gestructureerde Streaming Hallo documenten toolearn meer over het werken met Spark en Kafka volgende zien:</span><span class="sxs-lookup"><span data-stu-id="f8839-179">Now that you have learned how toouse Spark Structured Streaming, see hello following documents toolearn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="f8839-180">[Hoe toouse streaming (DStream) met Kafka Spark](hdinsight-apache-spark-with-kafka.md).</span><span class="sxs-lookup"><span data-stu-id="f8839-180">[How toouse Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="f8839-181">Beginnen met Jupyter-Notebook en Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8839-181">Start with Jupyter Notebook and Spark on HDInsight</span></span>](hdinsight-apache-spark-jupyter-spark-sql.md)
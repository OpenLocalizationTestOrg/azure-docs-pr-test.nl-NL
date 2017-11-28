---
title: aaaApache Spark streamen met Kafka - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Spark Apache Spark toostream gegevens van of naar Apache Kafka DStreams gebruiken. In dit voorbeeld kunt u gegevens met behulp van een Jupyter-notebook in Spark in HDInsight streamen.
keywords: Voorbeeld van kafka, zookeeper kafka, spark streaming kafka, spark-streaming kafka-voorbeeld
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="ba17f-105">Apache Spark-streaming (DStream) voorbeeld met Kafka (preview) op HDInsight</span><span class="sxs-lookup"><span data-stu-id="ba17f-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="ba17f-106">Meer informatie over hoe toouse Spark Apache Spark toostream gegevens van of naar Apache Kafka op HDInsight met behulp van DStreams.</span><span class="sxs-lookup"><span data-stu-id="ba17f-106">Learn how toouse Spark Apache Spark toostream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="ba17f-107">In dit voorbeeld wordt een Jupyter-notebook die wordt uitgevoerd op Hallo Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="ba17f-107">This example uses a Jupyter notebook that runs on hello Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="ba17f-108">Hallo stappen in dit document wordt een Azure-resourcegroep met zowel een Spark in HDInsight en een Kafka op HDInsight-cluster maken</span><span class="sxs-lookup"><span data-stu-id="ba17f-108">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="ba17f-109">Deze clusters zijn beide zich binnen een virtueel netwerk van Azure, waardoor Hallo Spark-cluster toodirectly communiceren met de Hallo Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="ba17f-109">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="ba17f-110">Wanneer u klaar bent met de stappen in dit document Hallo onthouden toodelete Hallo clusters tooavoid overtollige kosten.</span><span class="sxs-lookup"><span data-stu-id="ba17f-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="ba17f-111">Hallo-clusters maken</span><span class="sxs-lookup"><span data-stu-id="ba17f-111">Create hello clusters</span></span>

<span data-ttu-id="ba17f-112">Apache Kafka op HDInsight biedt geen toegang tot toohello Kafka beleggingsmakelaars via openbaar internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba17f-112">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="ba17f-113">Alles wat vertelt tooKafka moet zich in hetzelfde virtuele Azure-netwerk als knooppunten in Hallo HALLO hallo Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="ba17f-113">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="ba17f-114">Bijvoorbeeld, bevinden zowel hello Kafka- en Spark-clusters zich in een Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="ba17f-114">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="ba17f-115">Hallo volgende diagram ziet u hoe de communicatie tussen clusters met Hallo loopt:</span><span class="sxs-lookup"><span data-stu-id="ba17f-115">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagram van Spark en Kafka clusters in een Azure-netwerk](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="ba17f-117">Hoewel Kafka zelf beperkt toocommunication binnen het virtuele netwerk hello, Hallo andere services op Hallo cluster zoals SSH en Ambari toegankelijk is via internet.</span><span class="sxs-lookup"><span data-stu-id="ba17f-117">Though Kafka itself is limited toocommunication within hello virtual network, other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="ba17f-118">Zie voor meer informatie over Hallo openbare poorten beschikbaar met HDInsight [poorten en URI's die worden gebruikt door HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="ba17f-118">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="ba17f-119">U kunt een Azure-netwerk, Kafka en Spark clusters handmatig maken, is het eenvoudiger toouse een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="ba17f-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="ba17f-120">Gebruik Hallo volgende stappen uit voor een Azure-netwerk Kafka, toodeploy en Spark-clusters tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ba17f-120">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="ba17f-121">Hallo na de knop toosign in tooAzure en open Hallo-sjabloon in hello Azure-portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ba17f-121">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="ba17f-122">Hello Azure Resource Manager-sjabloon bevindt zich op **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="ba17f-122">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="ba17f-123">de beschikbaarheid van de tooguarantee van Kafka op HDInsight, uw cluster moet ten minste drie worker-knooppunten bevatten.</span><span class="sxs-lookup"><span data-stu-id="ba17f-123">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="ba17f-124">Deze sjabloon maakt een Kafka-cluster dat drie worker-knooppunten bevat.</span><span class="sxs-lookup"><span data-stu-id="ba17f-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="ba17f-125">Deze sjabloon maakt een 3.6 HDInsight-cluster voor Kafka- en Spark.</span><span class="sxs-lookup"><span data-stu-id="ba17f-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="ba17f-126">Gebruik Hallo informatie toopopulate Hallo vermeldingen op Hallo volgen **aangepaste implementatie** blade:</span><span class="sxs-lookup"><span data-stu-id="ba17f-126">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Aangepaste HDInsight-implementatie](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="ba17f-128">**Resourcegroep**: Maak een groep of een bestaande set selecteren.</span><span class="sxs-lookup"><span data-stu-id="ba17f-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="ba17f-129">Deze groep bevat Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ba17f-129">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="ba17f-130">**Locatie**: Selecteer een locatie geografisch sluiten tooyou.</span><span class="sxs-lookup"><span data-stu-id="ba17f-130">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="ba17f-131">**Clusternaam baseren**: deze waarde wordt gebruikt als basisnaam voor Hallo Spark en Kafka clusters Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba17f-131">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="ba17f-132">Bijvoorbeeld, voeren **hdi** maakt een Spark-cluster spark hdi__ met de naam en een Kafka-cluster met de naam **kafka hdi**.</span><span class="sxs-lookup"><span data-stu-id="ba17f-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="ba17f-133">**Aanmeldingsnaam van gebruiker cluster**: Hallo-beheerdersgebruikersnaam voor Hallo Spark en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="ba17f-133">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="ba17f-134">**Aanmeldingswachtwoord cluster**: Hallo beheerder gebruikerswachtwoord voor Hallo Spark en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="ba17f-134">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="ba17f-135">**SSH-gebruikersnaam**: Hallo SSH gebruiker toocreate voor Hallo Spark en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="ba17f-135">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="ba17f-136">**SSH-wachtwoord**: Hallo-wachtwoord voor Hallo SSH-gebruiker voor Hallo Spark en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="ba17f-136">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="ba17f-137">Lees Hallo **voorwaarden en bepalingen**, en selecteer vervolgens **ik ga akkoord toohello voorwaarden bovengenoemde**.</span><span class="sxs-lookup"><span data-stu-id="ba17f-137">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="ba17f-138">Controleer ten slotte **pincode toodashboard** en selecteer vervolgens **aankoop**.</span><span class="sxs-lookup"><span data-stu-id="ba17f-138">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="ba17f-139">Het duurt ongeveer 20 minuten toocreate Hallo-clusters.</span><span class="sxs-lookup"><span data-stu-id="ba17f-139">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="ba17f-140">Zodra het Hallo-resources zijn gemaakt, bent u omgeleide tooa blade voor de resourcegroep Hallo Hallo clusters en webdashboard met.</span><span class="sxs-lookup"><span data-stu-id="ba17f-140">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Resourcegroepblade voor Hallo vnet en clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="ba17f-142">Merk op dat de namen van HDInsight-clusters Hallo Hallo zijn **spark BASENAME** en **kafka BASENAME**, waarbij BASENAME Hallo-naam die u hebt opgegeven toohello sjabloon.</span><span class="sxs-lookup"><span data-stu-id="ba17f-142">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="ba17f-143">U deze namen in latere stappen gebruiken om verbinding te maken van clusters toohello.</span><span class="sxs-lookup"><span data-stu-id="ba17f-143">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="use-hello-notebooks"></a><span data-ttu-id="ba17f-144">Hallo-notebooks gebruiken</span><span class="sxs-lookup"><span data-stu-id="ba17f-144">Use hello notebooks</span></span>

<span data-ttu-id="ba17f-145">Hallo code Hallo zoals beschreven in dit document is beschikbaar op [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="ba17f-145">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="ba17f-146">Volg de stappen Hallo in Hallo `README.md` bestand toocomplete in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ba17f-146">Follow hello steps in hello `README.md` file toocomplete this example.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="ba17f-147">Hallo-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="ba17f-147">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="ba17f-148">Aangezien Hallo stappen in dit document beide maken clusters in dezelfde Azure-resourcegroep hello, kunt u de resourcegroep Hallo in hello Azure-portal verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ba17f-148">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="ba17f-149">Verwijderen Hallo groep verwijdert u alle resources die zijn gemaakt op basis van dit document, hello Azure Virtual Network en storage-account door Hallo clusters worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ba17f-149">Deleting hello group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba17f-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ba17f-150">Next steps</span></span>

<span data-ttu-id="ba17f-151">In dit voorbeeld hebt u geleerd hoe toouse tooread Spark en tooKafka schrijven.</span><span class="sxs-lookup"><span data-stu-id="ba17f-151">In this example, you learned how toouse Spark tooread and write tooKafka.</span></span> <span data-ttu-id="ba17f-152">Hallo toodiscover koppelingen volgen andere manieren toowork met Kafka gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ba17f-152">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* [<span data-ttu-id="ba17f-153">Aan de slag met Apache Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ba17f-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="ba17f-154">MirrorMaker toocreate een replica van Kafka op HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="ba17f-154">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="ba17f-155">Apache Storm gebruiken met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ba17f-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)


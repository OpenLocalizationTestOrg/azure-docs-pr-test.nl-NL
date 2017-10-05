---
title: Apache Spark-streaming met Kafka - Azure HDInsight | Microsoft Docs
description: Informatie over het gebruik van Spark Apache Spark als stream gegevens van of naar Apache Kafka met DStreams. In dit voorbeeld kunt u gegevens met behulp van een Jupyter-notebook in Spark in HDInsight streamen.
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
ms.openlocfilehash: 81fa319f6fb94bdabacd8f68d14b9a1063a9749a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="f2c65-105">Apache Spark-streaming (DStream) voorbeeld met Kafka (preview) op HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2c65-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="f2c65-106">Informatie over het gebruik van Spark Apache Spark als stream gegevens van of naar Apache Kafka op HDInsight met behulp van DStreams.</span><span class="sxs-lookup"><span data-stu-id="f2c65-106">Learn how to use Spark Apache Spark to stream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="f2c65-107">In dit voorbeeld wordt een Jupyter-notebook die wordt uitgevoerd op het Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="f2c65-107">This example uses a Jupyter notebook that runs on the Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="f2c65-108">De stappen in dit document wordt een Azure-resourcegroep met zowel een Spark in HDInsight en een Kafka op HDInsight-cluster maken</span><span class="sxs-lookup"><span data-stu-id="f2c65-108">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="f2c65-109">Deze clusters zijn beide zich binnen een virtueel netwerk van Azure, waardoor het Spark-cluster rechtstreeks communiceren met de Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="f2c65-109">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="f2c65-110">Wanneer u klaar bent met de stappen in dit document, vergeet niet de clusters om te voorkomen dat de overtollige kosten te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f2c65-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="f2c65-111">Clusters maken</span><span class="sxs-lookup"><span data-stu-id="f2c65-111">Create the clusters</span></span>

<span data-ttu-id="f2c65-112">Apache Kafka op HDInsight biedt geen toegang voor de beleggingsmakelaars Kafka via het openbare internet.</span><span class="sxs-lookup"><span data-stu-id="f2c65-112">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="f2c65-113">Alles wat wordt gesproken naar Kafka moet zich in hetzelfde virtuele netwerk van Azure als de knooppunten in het cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="f2c65-113">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="f2c65-114">In dit voorbeeld worden de Kafka- en Spark-clusters bevinden zich in een Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="f2c65-114">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="f2c65-115">Het volgende diagram toont hoe de communicatie tussen clusters stroomt:</span><span class="sxs-lookup"><span data-stu-id="f2c65-115">The following diagram shows how communication flows between the clusters:</span></span>

![Diagram van Spark en Kafka clusters in een Azure-netwerk](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="f2c65-117">Hoewel Kafka zelf beperkt tot communicatie binnen het virtuele netwerk is, zijn andere services op het cluster zoals SSH en Ambari toegankelijk via internet.</span><span class="sxs-lookup"><span data-stu-id="f2c65-117">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="f2c65-118">Zie voor meer informatie over de openbare poorten beschikbaar met HDInsight [poorten en URI's die worden gebruikt door HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="f2c65-118">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="f2c65-119">U kunt een Azure-netwerk Kafka, maken en handmatig Spark-clusters, is het ook eenvoudiger te gebruiken van een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f2c65-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="f2c65-120">Gebruik de volgende stappen voor het implementeren van een Azure-netwerk Kafka, en Spark-clusters met uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f2c65-120">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="f2c65-121">Gebruik de volgende knop om te melden bij Azure en opent u de sjabloon in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f2c65-121">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="f2c65-122">De Azure Resource Manager-sjabloon bevindt zich op **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="f2c65-122">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="f2c65-123">Om beschikbaarheid van Kafka op HDInsight te garanderen, moet uw cluster ten minste drie werkknooppunten bevatten.</span><span class="sxs-lookup"><span data-stu-id="f2c65-123">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="f2c65-124">Deze sjabloon maakt een Kafka-cluster dat drie worker-knooppunten bevat.</span><span class="sxs-lookup"><span data-stu-id="f2c65-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="f2c65-125">Deze sjabloon maakt een 3.6 HDInsight-cluster voor Kafka- en Spark.</span><span class="sxs-lookup"><span data-stu-id="f2c65-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="f2c65-126">Gebruik de volgende informatie voor het vullen van de vermeldingen op de **aangepaste implementatie** blade:</span><span class="sxs-lookup"><span data-stu-id="f2c65-126">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Aangepaste HDInsight-implementatie](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="f2c65-128">**Resourcegroep**: Maak een groep of een bestaande set selecteren.</span><span class="sxs-lookup"><span data-stu-id="f2c65-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="f2c65-129">Deze groep bevat het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="f2c65-129">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="f2c65-130">**Locatie**: Selecteer een locatie geografisch dicht bij u.</span><span class="sxs-lookup"><span data-stu-id="f2c65-130">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="f2c65-131">**Clusternaam baseren**: deze waarde wordt gebruikt als de basisnaam aan voor de Spark en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="f2c65-131">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="f2c65-132">Bijvoorbeeld, voeren **hdi** maakt een Spark-cluster spark hdi__ met de naam en een Kafka-cluster met de naam **kafka hdi**.</span><span class="sxs-lookup"><span data-stu-id="f2c65-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="f2c65-133">**Aanmeldingsnaam van gebruiker cluster**: de beheerdersgebruikersnaam voor Spark en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="f2c65-133">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="f2c65-134">**Aanmeldingswachtwoord cluster**: het beheerderswachtwoord voor de Spark en Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="f2c65-134">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="f2c65-135">**SSH-gebruikersnaam**: de SSH-gebruiker maken voor Spark en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="f2c65-135">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="f2c65-136">**SSH-wachtwoord**: het wachtwoord voor de SSH-gebruiker voor de Spark en Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="f2c65-136">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="f2c65-137">Lees de **voorwaarden en bepalingen**, en selecteer vervolgens **ik ga akkoord met de voorwaarden en bepalingen bovengenoemde**.</span><span class="sxs-lookup"><span data-stu-id="f2c65-137">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="f2c65-138">Controleer ten slotte **vastmaken aan dashboard** en selecteer vervolgens **aankoop**.</span><span class="sxs-lookup"><span data-stu-id="f2c65-138">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="f2c65-139">Het duurt ongeveer 20 minuten om de clusters te maken.</span><span class="sxs-lookup"><span data-stu-id="f2c65-139">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="f2c65-140">Zodra de resources zijn gemaakt, wordt u omgeleid naar een blade voor de resourcegroep die de clusters en webdashboard bevat.</span><span class="sxs-lookup"><span data-stu-id="f2c65-140">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Resourcegroepblade voor het vnet en clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="f2c65-142">Merk op dat de namen van de HDInsight-clusters **spark BASENAME** en **kafka BASENAME**, waarbij BASENAME is de naam die u hebt opgegeven in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f2c65-142">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="f2c65-143">U kunt deze namen in latere stappen gebruiken bij het verbinden met de clusters.</span><span class="sxs-lookup"><span data-stu-id="f2c65-143">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="use-the-notebooks"></a><span data-ttu-id="f2c65-144">De notebooks gebruiken</span><span class="sxs-lookup"><span data-stu-id="f2c65-144">Use the notebooks</span></span>

<span data-ttu-id="f2c65-145">De code voor het voorbeeld in dit document beschreven is beschikbaar op [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="f2c65-145">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="f2c65-146">Volg de stappen in de `README.md` bestand om te voltooien in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f2c65-146">Follow the steps in the `README.md` file to complete this example.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="f2c65-147">Het cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="f2c65-147">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="f2c65-148">Aangezien de stappen in dit document beide clusters in de groep met dezelfde Azure-resource maakt, kunt u de resourcegroep in de Azure portal kunt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f2c65-148">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="f2c65-149">De groep verwijdert, worden alle resources die zijn gemaakt op basis van dit document, Azure Virtual Network en storage-account door de clusters worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f2c65-149">Deleting the group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2c65-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f2c65-150">Next steps</span></span>

<span data-ttu-id="f2c65-151">In dit voorbeeld hebt u geleerd Spark gebruiken om te lezen en schrijven naar Kafka.</span><span class="sxs-lookup"><span data-stu-id="f2c65-151">In this example, you learned how to use Spark to read and write to Kafka.</span></span> <span data-ttu-id="f2c65-152">Gebruik de volgende koppelingen voor het detecteren van andere manieren om te werken met Kafka:</span><span class="sxs-lookup"><span data-stu-id="f2c65-152">Use the following links to discover other ways to work with Kafka:</span></span>

* [<span data-ttu-id="f2c65-153">Aan de slag met Apache Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2c65-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="f2c65-154">MirrorMaker gebruiken voor het maken van een replica van Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2c65-154">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="f2c65-155">Apache Storm gebruiken met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2c65-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)


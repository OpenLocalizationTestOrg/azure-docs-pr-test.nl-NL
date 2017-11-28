---
title: Schaalverhoging met Apache Kafka - Azure HDInsight | Microsoft Docs
description: Leer hoe u beheerde schijven voor een Apache Kafka-cluster configureert in Azure HDInsight om de schaalbaarheid te verhogen.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/14/2017
ms.author: larryfr
ms.openlocfilehash: 880a186a3d9a23b013294b0121e8265270d160cc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a><span data-ttu-id="17685-103">Opslag en schaalbaarheid configureren voor Apache Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="17685-103">Configure storage and scalability for Apache Kafka on HDInsight</span></span>

<span data-ttu-id="17685-104">Leer hoe u het aantal beheerde schijven configureert dat wordt gebruikt in Apache Kafka in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="17685-104">Learn how to configure the number of managed disks used by Apache Kafka on HDInsight.</span></span>

<span data-ttu-id="17685-105">Kafka in HDInsight maakt gebruik van de lokale schijf van de virtuele machines in het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="17685-105">Kafka on HDInsight uses the local disk of the virtual machines in the HDInsight cluster.</span></span> <span data-ttu-id="17685-106">Aangezien Kafka veel gebruikmaakt van invoer/uitvoer, wordt [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) gebruikt voor een hoge doorvoer en meer opslag per knooppunt.</span><span class="sxs-lookup"><span data-stu-id="17685-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) is used to provide high throughput and provide more storage per node.</span></span> <span data-ttu-id="17685-107">Als u de traditionele VHD (virtuele harde schijven) gebruikt voor Kafka, heeft elk knooppunt een limiet van 1 TB.</span><span class="sxs-lookup"><span data-stu-id="17685-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited to 1 TB.</span></span> <span data-ttu-id="17685-108">Met beheerde schijven kunt u meerdere schijven gebruiken en zodat elk knooppunt in het cluster een limiet heeft van 16 TB.</span><span class="sxs-lookup"><span data-stu-id="17685-108">With managed disks, you can use multiple disks to achieve 16 TB for each node in the cluster.</span></span>

<span data-ttu-id="17685-109">In het volgende diagram ziet u een vergelijking tussen Kafka in HDInsight voordat beheerde schijven werden gebruikt, en Kafka in HDInsight met beheerde schijven:</span><span class="sxs-lookup"><span data-stu-id="17685-109">The following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span></span>

![Diagram waarin Kafka in HDInsight wordt weergegeven met één virtuele harde schijf per VM versus meerdere beheerde schijven per VM](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a><span data-ttu-id="17685-111">Beheerde schijven configureren: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="17685-111">Configure managed disks: Azure portal</span></span>

1. <span data-ttu-id="17685-112">Volg de stappen in [Een HDInsight-cluster maken](hdinsight-hadoop-create-linux-clusters-portal.md) voor de algemene stappen voor het maken van een cluster met behulp van de portal.</span><span class="sxs-lookup"><span data-stu-id="17685-112">Follow the steps in the [Create an HDInsight cluster](hdinsight-hadoop-create-linux-clusters-portal.md) to understand the common steps to create a cluster using the portal.</span></span> <span data-ttu-id="17685-113">Voltooi het creatieproces met behulp van de portal niet.</span><span class="sxs-lookup"><span data-stu-id="17685-113">Do not complete the portal creation process.</span></span>

2. <span data-ttu-id="17685-114">Gebruik op de blade __Clustergrootte__ het veld __Schijven per werkknooppunt__ om het aantal schijven te configureren.</span><span class="sxs-lookup"><span data-stu-id="17685-114">From the __Cluster size__ blade, use the __Disks per worker node__ field to configure the number of disks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="17685-115">Het type beheerde schijf is __Standaard__ (HDD) of __Premium__ (SSD).</span><span class="sxs-lookup"><span data-stu-id="17685-115">The type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="17685-116">Premium-schijven worden gebruikt met virtuele machines uit de DS- en GS-reeks.</span><span class="sxs-lookup"><span data-stu-id="17685-116">Premium disks are used with DS and GS series VMs.</span></span> <span data-ttu-id="17685-117">Alle andere VM-typen gebruiken standaardschijven.</span><span class="sxs-lookup"><span data-stu-id="17685-117">All other VM types use standard.</span></span>

    ![Afbeelding van de blade Clustergrootte met de schijven gemarkeerd per werkknooppunt](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a><span data-ttu-id="17685-119">Beheerde schijven configureren: Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="17685-119">Configure managed disks: Resource Manager template</span></span>

<span data-ttu-id="17685-120">Als u het aantal schijven wilt beheren dat wordt gebruikt in de werkknooppunten van een Kafka-cluster, gebruikt u de volgende sectie van de sjabloon:</span><span class="sxs-lookup"><span data-stu-id="17685-120">To control the number of disks used by the worker nodes in a Kafka cluster, use the following section of the template:</span></span>

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

<span data-ttu-id="17685-121">Op [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json) vindt u een volledige sjabloon waarin wordt weergegeven hoe u beheerde schijven kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="17685-121">You can find a complete template that demonstrates how to configure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="17685-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="17685-122">Next steps</span></span>

<span data-ttu-id="17685-123">Zie de volgende documenten voor meer informatie over het werken Kafka in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="17685-123">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="17685-124">MirrorMaker gebruiken voor het maken van een replica van Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="17685-124">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="17685-125">Apache Storm gebruiken met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="17685-125">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="17685-126">Apache Spark gebruiken met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="17685-126">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="17685-127">Verbinding maken met Kafka via een Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="17685-127">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [<span data-ttu-id="17685-128">HDInsight-blog over beheerde schijven met Kafka</span><span class="sxs-lookup"><span data-stu-id="17685-128">HDInsight blog on managed disks with Kafka</span></span>](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)
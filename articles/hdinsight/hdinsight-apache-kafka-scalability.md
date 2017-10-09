---
title: schaalt aaaApache Kafka - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe tooconfigure schijven voor Apache Kafka-cluster op Azure HDInsight tooincrease schaalbaarheid beheerd.
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
ms.openlocfilehash: b51114b33359f2c385f057a7a7a5b134cad27e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a><span data-ttu-id="9d45f-103">Opslag en schaalbaarheid configureren voor Apache Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9d45f-103">Configure storage and scalability for Apache Kafka on HDInsight</span></span>

<span data-ttu-id="9d45f-104">Meer informatie over hoe tooconfigure Hallo aantal beheerde schijven gebruikt door Apache Kafka op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9d45f-104">Learn how tooconfigure hello number of managed disks used by Apache Kafka on HDInsight.</span></span>

<span data-ttu-id="9d45f-105">Kafka op HDInsight maakt gebruik van de lokale schijf Hallo Hallo virtuele machines Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9d45f-105">Kafka on HDInsight uses hello local disk of hello virtual machines in hello HDInsight cluster.</span></span> <span data-ttu-id="9d45f-106">Omdat Kafka zwaar, zeer i/o is [Azure beheerd schijven](../virtual-machines/windows/managed-disks-overview.md) gebruikte tooprovide hoge doorvoersnelheid is en bieden meer opslagruimte per knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9d45f-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) is used tooprovide high throughput and provide more storage per node.</span></span> <span data-ttu-id="9d45f-107">Als traditionele virtuele harde schijven (VHD) zijn gebruikt voor Kafka, is in elk knooppunt beperkt too1 TB.</span><span class="sxs-lookup"><span data-stu-id="9d45f-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited too1 TB.</span></span> <span data-ttu-id="9d45f-108">Met beheerde schijven kunt u meerdere schijven tooachieve 16 TB voor elk knooppunt in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="9d45f-108">With managed disks, you can use multiple disks tooachieve 16 TB for each node in hello cluster.</span></span>

<span data-ttu-id="9d45f-109">Hallo biedt volgende diagram een vergelijking tussen Kafka op HDInsight voordat de beheerde schijven en Kafka in HDInsight met beheerde schijven:</span><span class="sxs-lookup"><span data-stu-id="9d45f-109">hello following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span></span>

![Diagram waarin Kafka in HDInsight wordt weergegeven met één virtuele harde schijf per VM versus meerdere beheerde schijven per VM](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a><span data-ttu-id="9d45f-111">Beheerde schijven configureren: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9d45f-111">Configure managed disks: Azure portal</span></span>

1. <span data-ttu-id="9d45f-112">Volg de stappen Hallo in Hallo [maken van een HDInsight-cluster](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand Hallo algemene stappen toocreate een cluster met de Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="9d45f-112">Follow hello steps in hello [Create an HDInsight cluster](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello common steps toocreate a cluster using hello portal.</span></span> <span data-ttu-id="9d45f-113">Hallo maken van de portal proces niet worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="9d45f-113">Do not complete hello portal creation process.</span></span>

2. <span data-ttu-id="9d45f-114">Van Hallo __clustergrootte__ blade, gebruik Hallo __schijven per werkrolknooppunt__ veld tooconfigure Hallo aantal schijven.</span><span class="sxs-lookup"><span data-stu-id="9d45f-114">From hello __Cluster size__ blade, use hello __Disks per worker node__ field tooconfigure hello number of disks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9d45f-115">Hallo type beheerde schijf kan zijn __standaard__ (HDD) of __Premium__ (SSD).</span><span class="sxs-lookup"><span data-stu-id="9d45f-115">hello type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="9d45f-116">Premium-schijven worden gebruikt met virtuele machines uit de DS- en GS-reeks.</span><span class="sxs-lookup"><span data-stu-id="9d45f-116">Premium disks are used with DS and GS series VMs.</span></span> <span data-ttu-id="9d45f-117">Alle andere VM-typen gebruiken standaardschijven.</span><span class="sxs-lookup"><span data-stu-id="9d45f-117">All other VM types use standard.</span></span>

    ![Afbeelding van Hallo cluster grootte blade met Hallo schijven per werkrolknooppunt gemarkeerd](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a><span data-ttu-id="9d45f-119">Beheerde schijven configureren: Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="9d45f-119">Configure managed disks: Resource Manager template</span></span>

<span data-ttu-id="9d45f-120">toocontrol hello aantal schijven gebruikt door Hallo worker-knooppunten in een cluster Kafka, gebruik Hallo gedeelte van de sjabloon hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d45f-120">toocontrol hello number of disks used by hello worker nodes in a Kafka cluster, use hello following section of hello template:</span></span>

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

<span data-ttu-id="9d45f-121">U vindt een volledige sjabloon die u laat zien hoe tooconfigure schijven op beheerd [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span><span class="sxs-lookup"><span data-stu-id="9d45f-121">You can find a complete template that demonstrates how tooconfigure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d45f-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d45f-122">Next steps</span></span>

<span data-ttu-id="9d45f-123">Zie voor meer informatie over het werken met Kafka op HDInsight Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d45f-123">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="9d45f-124">MirrorMaker toocreate een replica van Kafka op HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="9d45f-124">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="9d45f-125">Apache Storm gebruiken met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9d45f-125">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="9d45f-126">Apache Spark gebruiken met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9d45f-126">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="9d45f-127">TooKafka verbinding via een virtueel Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="9d45f-127">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [<span data-ttu-id="9d45f-128">HDInsight-blog over beheerde schijven met Kafka</span><span class="sxs-lookup"><span data-stu-id="9d45f-128">HDInsight blog on managed disks with Kafka</span></span>](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)
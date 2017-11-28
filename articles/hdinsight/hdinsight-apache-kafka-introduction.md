---
title: aaaAn inleiding tooApache Kafka op HDInsight - Azure | Microsoft Docs
description: 'Meer informatie over de Apache-Kafka op HDInsight: Wat is, wat het doet en waar toofind voorbeelden en ophalen van informatie gestart.'
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: larryfr
ms.openlocfilehash: 1bc198d4cf93a4682030d4fa5f71030f49ad64be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a><span data-ttu-id="b3892-103">Inleiding tot Apache Kafka in HDInsight (preview)</span><span class="sxs-lookup"><span data-stu-id="b3892-103">Introducing Apache Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="b3892-104">[Apache Kafka](https://kafka.apache.org) is een open source gedistribueerde streaming-platform die gebruikt toobuild realtime worden kan streaming gegevenspijplijnen en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b3892-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used toobuild real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="b3892-105">Kafka biedt ook bericht broker functionaliteit vergelijkbaar tooa berichtenwachtrij, kunt u publiceren en abonneren toonamed gegevensstromen.</span><span class="sxs-lookup"><span data-stu-id="b3892-105">Kafka also provides message broker functionality similar tooa message queue, where you can publish and subscribe toonamed data streams.</span></span> <span data-ttu-id="b3892-106">Kafka op HDInsight biedt u een beheerde, maximaal beschikbare en zeer schaalbare service in Hallo Microsoft Azure-cloud.</span><span class="sxs-lookup"><span data-stu-id="b3892-106">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in hello Microsoft Azure cloud.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="b3892-107">Waarom Kafka op HDInsight gebruiken?</span><span class="sxs-lookup"><span data-stu-id="b3892-107">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="b3892-108">Kafka biedt Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="b3892-108">Kafka provides hello following features:</span></span>

* <span data-ttu-id="b3892-109">Messaging-patroon publiceren / abonneren: Kafka biedt een producent-API voor het publiceren van records tooa Kafka onderwerp.</span><span class="sxs-lookup"><span data-stu-id="b3892-109">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records tooa Kafka topic.</span></span> <span data-ttu-id="b3892-110">Hallo Consumer-API wordt gebruikt wanneer u zich abonneert tooa onderwerp.</span><span class="sxs-lookup"><span data-stu-id="b3892-110">hello Consumer API is used when subscribing tooa topic.</span></span>

* <span data-ttu-id="b3892-111">Streamverwerking: Kafka wordt vaak gebruikt met Apache Storm of Spark voor streamverwerking in realtime.</span><span class="sxs-lookup"><span data-stu-id="b3892-111">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="b3892-112">Kafka 0.10.0.0 (HDInsight versie 3.5) geïntroduceerd om een streaming-API waarmee u toobuild oplossingen streaming zonder dat Storm of Spark.</span><span class="sxs-lookup"><span data-stu-id="b3892-112">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you toobuild streaming solutions without requiring Storm or Spark.</span></span>

* <span data-ttu-id="b3892-113">Horizontale schaal: Kafka partities streams op Hallo-knooppunten in Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b3892-113">Horizontal scale: Kafka partitions streams across hello nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="b3892-114">Consumer-processen kunnen worden gekoppeld aan afzonderlijke partities tooprovide taakverdeling wanneer records worden verbruikt.</span><span class="sxs-lookup"><span data-stu-id="b3892-114">Consumer processes can be associated with individual partitions tooprovide load balancing when consuming records.</span></span>

* <span data-ttu-id="b3892-115">Levering op volgorde: binnen elke partitie records worden opgeslagen in de stroom Hallo Hallo zodat ze werden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="b3892-115">In-order delivery: Within each partition, records are stored in hello stream in hello order that they were received.</span></span> <span data-ttu-id="b3892-116">Door één consumentenproces aan een partitie te koppelen, kunt u garanderen dat de records in de juiste volgorde worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b3892-116">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

* <span data-ttu-id="b3892-117">Fouttolerantie: Kunnen partities worden gerepliceerd tussen knooppunten tooprovide fouttolerantie.</span><span class="sxs-lookup"><span data-stu-id="b3892-117">Fault-tolerant: Partitions can be replicated between nodes tooprovide fault tolerance.</span></span>

* <span data-ttu-id="b3892-118">Integratie met Azure beheerd schijven: beheerde schijven biedt hogere schaal en doorvoer voor Hallo-schijven die worden gebruikt door Hallo virtuele machines in Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b3892-118">Integration with Azure Managed Disks: Managed disks provides higher scale and throughput for hello disks used by hello virtual machines in hello HDInsight cluster.</span></span>

    <span data-ttu-id="b3892-119">Beheerde schijven zijn standaard ingeschakeld voor Kafka in HDInsight en Hallo aantal schijven gebruikt per knooppunt kan worden geconfigureerd tijdens het maken van HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b3892-119">Managed disks are enabled by default for Kafka on HDInsight, and hello number of disks used per node can be configured during HDInsight creation.</span></span> <span data-ttu-id="b3892-120">Zie [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) voor meer informatie over beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="b3892-120">For more information on managed disks, see [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span></span>

    <span data-ttu-id="b3892-121">Zie [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md) (Schaalbaarheid verhogen van Kafka in HDInsight) voor informatie over het configureren van beheerde schijven met Kafka in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b3892-121">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

## <a name="use-cases"></a><span data-ttu-id="b3892-122">Gebruiksvoorbeelden</span><span class="sxs-lookup"><span data-stu-id="b3892-122">Use cases</span></span>

* <span data-ttu-id="b3892-123">**Messaging-**: aangezien het Hallo ondersteunt bericht patroon voor publiceren / abonneren, Kafka wordt vaak gebruikt als broker bericht.</span><span class="sxs-lookup"><span data-stu-id="b3892-123">**Messaging**: Since it supports hello publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="b3892-124">**Bijhouden van activiteiten**: aangezien Kafka logboekregistratie in volgorde van records, biedt het kan worden gebruikt tootrack en activiteiten opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="b3892-124">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used tootrack and re-create activities.</span></span> <span data-ttu-id="b3892-125">Bijvoorbeeld gebruikersacties op een website of in een toepassing.</span><span class="sxs-lookup"><span data-stu-id="b3892-125">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="b3892-126">**Aggregatie**: stream verwerking gebruikt, kunt u statistische gegevens uit verschillende stromen toocombine en Hallo-gegevens in de operationele gegevens centraliseren.</span><span class="sxs-lookup"><span data-stu-id="b3892-126">**Aggregation**: Using stream processing, you can aggregate information from different streams toocombine and centralize hello information into operational data.</span></span>

* <span data-ttu-id="b3892-127">**Transformatie**: met streamverwerking kunt u de gegevens uit meerdere invoeronderwerpen combineren en vertalen naar één of meer uitvoeronderwerpen.</span><span class="sxs-lookup"><span data-stu-id="b3892-127">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3892-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b3892-128">Next steps</span></span>

<span data-ttu-id="b3892-129">Gebruik Hallo volgende koppelingen toolearn hoe toouse Apache Kafka op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b3892-129">Use hello following links toolearn how toouse Apache Kafka on HDInsight:</span></span>

* [<span data-ttu-id="b3892-130">Aan de slag met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3892-130">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)

* [<span data-ttu-id="b3892-131">MirrorMaker toocreate een replica van Kafka op HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="b3892-131">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

* [<span data-ttu-id="b3892-132">Apache Storm gebruiken met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3892-132">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

* [<span data-ttu-id="b3892-133">Apache Spark gebruiken met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3892-133">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)

* [<span data-ttu-id="b3892-134">TooKafka verbinding via een virtueel Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="b3892-134">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)

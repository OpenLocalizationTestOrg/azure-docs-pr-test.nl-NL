---
title: Hoge beschikbaarheid met Apache Kafka - Azure HDInsight | Microsoft Docs
description: Informatie over hoge beschikbaarheid garanderen met Apache Kafka in Azure HDInsight. Informatie over het opnieuw verdelen van partitiereplica's in Kafka zodat deze zich bevinden op verschillende foutdomeinen binnen de Azure-regio met HDInsight.
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
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: f8164d1c3483b28e5f2abcc8035da78880daec1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="fa78b-104">Hoge beschikbaarheid van uw gegevens met Apache Kafka (preview) in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa78b-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="fa78b-105">Informatie over het configureren van partitiereplica's voor Kafka-onderwerpen om te profiteren van de onderliggende rek-configuratie van de hardware.</span><span class="sxs-lookup"><span data-stu-id="fa78b-105">Learn how to configure partition replicas for Kafka topics to take advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="fa78b-106">Deze configuratie waarborgt de beschikbaarheid van gegevens die zijn opgeslagen in Apache Kafka op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fa78b-106">This configuration ensures the availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="fa78b-107">Probleem- en updatedomeinen met Kafka</span><span class="sxs-lookup"><span data-stu-id="fa78b-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="fa78b-108">Een foutdomein is een logische groepering van de onderliggende hardware in een Azure-datacenter.</span><span class="sxs-lookup"><span data-stu-id="fa78b-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="fa78b-109">Elk foutdomein deelt een algemene voedingsbron en netwerkswitch.</span><span class="sxs-lookup"><span data-stu-id="fa78b-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="fa78b-110">De virtuele machines en beheerde schijven die de knooppunten in een HDInsight-cluster implementeren zijn verdeeld over deze foutdomeinen.</span><span class="sxs-lookup"><span data-stu-id="fa78b-110">The virtual machines and managed disks that implement the nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="fa78b-111">Deze architectuur beperkt de potentiële impact van problemen met de fysieke hardware.</span><span class="sxs-lookup"><span data-stu-id="fa78b-111">This architecture limits the potential impact of physical hardware failures.</span></span>

<span data-ttu-id="fa78b-112">Elke Azure-regio heeft een bepaald aantal foutdomeinen.</span><span class="sxs-lookup"><span data-stu-id="fa78b-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="fa78b-113">Zie de [Beschikbaarheidssets](../virtual-machines/linux/regions-and-availability.md#availability-sets)-documentatie voor een lijst met domeinen en het aantal foutdomeinen die ze bevatten.</span><span class="sxs-lookup"><span data-stu-id="fa78b-113">For a list of domains and the number of fault domains they contain, see the [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa78b-114">Kafka is niet bekend met foutdomeinen.</span><span class="sxs-lookup"><span data-stu-id="fa78b-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="fa78b-115">Wanneer u een onderwerp in Kafka maakt, is het daarom mogelijk dat alle partitiereplica's in hetzelfde foutdomein worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="fa78b-115">When you create a topic in Kafka, it may store all partition replicas in the same fault domain.</span></span> <span data-ttu-id="fa78b-116">Als oplossing voor dit probleem bieden we het [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) (hulpprogramma voor het opnieuw indelen van Kafka-partities).</span><span class="sxs-lookup"><span data-stu-id="fa78b-116">To solve this problem, we provide the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-to-rebalance-partition-replicas"></a><span data-ttu-id="fa78b-117">Wanneer partitiereplica 's opnieuw moeten worden ingedeeld</span><span class="sxs-lookup"><span data-stu-id="fa78b-117">When to rebalance partition replicas</span></span>

<span data-ttu-id="fa78b-118">Om de hoogst mogelijke beschikbaarheid van uw Kafka-gegevens te waarborgen, moet u de partitiereplica's voor uw onderwerp op de volgende tijden opnieuw indelen:</span><span class="sxs-lookup"><span data-stu-id="fa78b-118">To ensure the highest availability of your Kafka data, you should rebalance the partition replicas for your topic at the following times:</span></span>

* <span data-ttu-id="fa78b-119">wanneer een nieuw onderwerp of partitie wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="fa78b-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="fa78b-120">wanneer u een cluster opschaalt</span><span class="sxs-lookup"><span data-stu-id="fa78b-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="fa78b-121">Replicatiefactor</span><span class="sxs-lookup"><span data-stu-id="fa78b-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa78b-122">Wij raden het gebruik aan van een Azure-regio die drie foutdomeinen bevat en van een replicatiefactor van 3.</span><span class="sxs-lookup"><span data-stu-id="fa78b-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="fa78b-123">Als u een regio met slechts twee foutdomeinen moet gebruiken, gebruik dan een replicatiefactor van 4 om de replica's gelijkmatig te verdelen over de twee foutdomeinen.</span><span class="sxs-lookup"><span data-stu-id="fa78b-123">If you must use a region that contains only two fault domains, use a replication factor of 4 to spread the replicas evenly across the two fault domains.</span></span>

<span data-ttu-id="fa78b-124">Zie het document [Aan de slag met Apache Kafka in HDInsight](hdinsight-apache-kafka-get-started.md) voor een voorbeeld van het maken van onderwerpen en instellen van de replicatiefactor.</span><span class="sxs-lookup"><span data-stu-id="fa78b-124">For an example of creating topics and setting the replication factor, see the [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-to-rebalance-partition-replicas"></a><span data-ttu-id="fa78b-125">Hoe partitiereplica 's opnieuw moeten worden ingedeeld</span><span class="sxs-lookup"><span data-stu-id="fa78b-125">How to rebalance partition replicas</span></span>

<span data-ttu-id="fa78b-126">Gebruik het [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) (hulpprogramma voor het opnieuw indelen van Kafka-partities) om de geselecteerde onderwerpen opnieuw in te delen.</span><span class="sxs-lookup"><span data-stu-id="fa78b-126">Use the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) to rebalance selected topics.</span></span> <span data-ttu-id="fa78b-127">Dit hulpprogramma moet vanaf een SSH-sessie naar het hoofdknooppunt van het Kafka-cluster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fa78b-127">This tool must be ran from an SSH session to the head node of your Kafka cluster.</span></span>

<span data-ttu-id="fa78b-128">Zie het document [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie over verbinding maken met HDInsight met behulp van SSH.</span><span class="sxs-lookup"><span data-stu-id="fa78b-128">For more information on connecting to HDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa78b-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fa78b-129">Next steps</span></span>

* [<span data-ttu-id="fa78b-130">Schaalbaarheid van Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa78b-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="fa78b-131">Spiegeling met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa78b-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
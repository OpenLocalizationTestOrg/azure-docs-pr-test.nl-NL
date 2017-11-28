---
title: beschikbaarheid van aaaHigh met Apache Kafka - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe tooensure hoge beschikbaarheid met Apache Kafka in Azure HDInsight. Meer informatie over hoe toorebalance replica's in Kafka partitie zodat ze zich op verschillende foutdomeinen binnen hello Azure-regio met HDInsight.
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
ms.openlocfilehash: 337468f36b531f83c2999e87907de89cf3d19dd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="4e43e-104">Hoge beschikbaarheid van uw gegevens met Apache Kafka (preview) in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e43e-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="4e43e-105">Meer informatie over hoe tooconfigure partitie replica's voor Kafka onderwerpen tootake profiteren van de onderliggende hardware configuratie van rack.</span><span class="sxs-lookup"><span data-stu-id="4e43e-105">Learn how tooconfigure partition replicas for Kafka topics tootake advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="4e43e-106">Deze configuratie zorgt er Hallo beschikbaarheid van gegevens die zijn opgeslagen in de Apache-Kafka op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e43e-106">This configuration ensures hello availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="4e43e-107">Probleem- en updatedomeinen met Kafka</span><span class="sxs-lookup"><span data-stu-id="4e43e-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="4e43e-108">Een foutdomein is een logische groepering van de onderliggende hardware in een Azure-datacenter.</span><span class="sxs-lookup"><span data-stu-id="4e43e-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="4e43e-109">Elk foutdomein deelt een algemene voedingsbron en netwerkswitch.</span><span class="sxs-lookup"><span data-stu-id="4e43e-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="4e43e-110">Hallo virtuele machines en beheerde schijven die Hallo knooppunten binnen een HDInsight-cluster implementeren zijn verdeeld over deze domeinen met fouten.</span><span class="sxs-lookup"><span data-stu-id="4e43e-110">hello virtual machines and managed disks that implement hello nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="4e43e-111">Deze architectuur beperkt Hallo potentiële impact van problemen met de fysieke hardware.</span><span class="sxs-lookup"><span data-stu-id="4e43e-111">This architecture limits hello potential impact of physical hardware failures.</span></span>

<span data-ttu-id="4e43e-112">Elke Azure-regio heeft een bepaald aantal foutdomeinen.</span><span class="sxs-lookup"><span data-stu-id="4e43e-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="4e43e-113">Zie voor een lijst van domeinen en het aantal foutdomeinen ze bevatten Hallo Hallo [beschikbaarheidssets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentatie.</span><span class="sxs-lookup"><span data-stu-id="4e43e-113">For a list of domains and hello number of fault domains they contain, see hello [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e43e-114">Kafka is niet bekend met foutdomeinen.</span><span class="sxs-lookup"><span data-stu-id="4e43e-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="4e43e-115">Wanneer u een onderwerp in Kafka maakt, kan deze alle replica's opslaan in Hallo hetzelfde foutdomein.</span><span class="sxs-lookup"><span data-stu-id="4e43e-115">When you create a topic in Kafka, it may store all partition replicas in hello same fault domain.</span></span> <span data-ttu-id="4e43e-116">toosolve dit probleem, bieden we Hallo [Kafka partitie deel opnieuw hulpprogramma](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="4e43e-116">toosolve this problem, we provide hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-toorebalance-partition-replicas"></a><span data-ttu-id="4e43e-117">Wanneer de replica's voor het partitioneren van toorebalance</span><span class="sxs-lookup"><span data-stu-id="4e43e-117">When toorebalance partition replicas</span></span>

<span data-ttu-id="4e43e-118">tooensure hello hoogste beschikbaarheid van uw gegevens Kafka, u moet opnieuw verdelen Hallo partitie replica's voor uw onderwerp op Hallo volgende tijden:</span><span class="sxs-lookup"><span data-stu-id="4e43e-118">tooensure hello highest availability of your Kafka data, you should rebalance hello partition replicas for your topic at hello following times:</span></span>

* <span data-ttu-id="4e43e-119">wanneer een nieuw onderwerp of partitie wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="4e43e-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="4e43e-120">wanneer u een cluster opschaalt</span><span class="sxs-lookup"><span data-stu-id="4e43e-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="4e43e-121">Replicatiefactor</span><span class="sxs-lookup"><span data-stu-id="4e43e-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e43e-122">Wij raden het gebruik aan van een Azure-regio die drie foutdomeinen bevat en van een replicatiefactor van 3.</span><span class="sxs-lookup"><span data-stu-id="4e43e-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="4e43e-123">Als u een regio met slechts twee domeinen met fouten gebruiken moet, gebruikt u een factor van de replicatie van 4 toospread Hallo-replica's gelijkmatig tussen de twee domeinen met fouten Hallo.</span><span class="sxs-lookup"><span data-stu-id="4e43e-123">If you must use a region that contains only two fault domains, use a replication factor of 4 toospread hello replicas evenly across hello two fault domains.</span></span>

<span data-ttu-id="4e43e-124">Zie voor een voorbeeld van het maken van onderwerpen en -instelling Hallo replicatie factor Hallo [beginnen met Kafka op HDInsight](hdinsight-apache-kafka-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="4e43e-124">For an example of creating topics and setting hello replication factor, see hello [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-toorebalance-partition-replicas"></a><span data-ttu-id="4e43e-125">Hoe toorebalance partitie-replica 's</span><span class="sxs-lookup"><span data-stu-id="4e43e-125">How toorebalance partition replicas</span></span>

<span data-ttu-id="4e43e-126">Gebruik Hallo [Kafka partitie deel opnieuw hulpprogramma](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance onderwerpen geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="4e43e-126">Use hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance selected topics.</span></span> <span data-ttu-id="4e43e-127">Dit hulpprogramma moet vanaf een SSH-sessie toohello hoofdknooppunt van het cluster Kafka worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4e43e-127">This tool must be ran from an SSH session toohello head node of your Kafka cluster.</span></span>

<span data-ttu-id="4e43e-128">Zie voor meer informatie over tooHDInsight via SSH verbinding te maken, de [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="4e43e-128">For more information on connecting tooHDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e43e-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4e43e-129">Next steps</span></span>

* [<span data-ttu-id="4e43e-130">Schaalbaarheid van Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e43e-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="4e43e-131">Spiegeling met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e43e-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
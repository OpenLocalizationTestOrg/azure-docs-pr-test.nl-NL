---
title: aaaUpgrade HDInsight-cluster tooa nieuwere versie-Azure | Microsoft Docs
description: Meer informatie over hoe tooUpgrade HDInsight-cluster tooa nieuwere versie.
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a><span data-ttu-id="3e843-103">HDInsight-cluster tooa nieuwere versie upgraden</span><span class="sxs-lookup"><span data-stu-id="3e843-103">Upgrade HDInsight cluster tooa newer version</span></span>
<span data-ttu-id="3e843-104">tootake profiteren van Hallo nieuwste functies van HDInsight, het beste een HDInsight-clusters bijgewerkte toolatest versie.</span><span class="sxs-lookup"><span data-stu-id="3e843-104">tootake advantage of hello latest HDInsight features, we recommend that HDInsight clusters be upgraded toolatest version.</span></span> <span data-ttu-id="3e843-105">Ga als volgt Hallo hieronder richtlijnen tooupgrade de versies van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="3e843-105">Follow hello below guidelines tooupgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="3e843-106">HDInsight-clusters versie 3.2 en 3.3 bijna intrekkingsdatum zijn.</span><span class="sxs-lookup"><span data-stu-id="3e843-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="3e843-107">Zie voor informatie over de ondersteunde versie van HDInsight, [HDInsight onderdeel versies](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="3e843-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="3e843-108">Upgradetaken</span><span class="sxs-lookup"><span data-stu-id="3e843-108">Upgrade tasks</span></span>
<span data-ttu-id="3e843-109">Hallo werkstroom tooupgrade HDInsight-Cluster is als volgt.</span><span class="sxs-lookup"><span data-stu-id="3e843-109">hello workflow tooupgrade HDInsight Cluster is as follows.</span></span>

![Werkstroom voor serverupgrades diagram](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="3e843-111">Elke sectie van dit document toounderstand wijzigingen die nodig zijn bij een upgrade van uw HDInsight-cluster lezen.</span><span class="sxs-lookup"><span data-stu-id="3e843-111">Read each section of this document toounderstand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="3e843-112">Maak een cluster als een test/quality assurance-omgeving.</span><span class="sxs-lookup"><span data-stu-id="3e843-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="3e843-113">Zie voor meer informatie over het maken van een cluster [meer informatie over hoe toocreate Linux gebaseerde HDInsight-clusters](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="3e843-113">For more information on creating a cluster, see [Learn how toocreate Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="3e843-114">Kopie bestaande taken, de gegevensbronnen en de sinks toohello nieuwe omgeving.</span><span class="sxs-lookup"><span data-stu-id="3e843-114">Copy existing jobs, data sources, and sinks toohello new environment.</span></span> <span data-ttu-id="3e843-115">Zie [gegevens kopiëren tooTest omgeving](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3e843-115">See [Copy Data tooTest Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="3e843-116">Validatie toomake ervoor dat uw taken werken zoals verwacht op het nieuwe cluster Hallo testen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3e843-116">Perform validation testing toomake sure that your jobs work as expected on hello new cluster.</span></span>


<span data-ttu-id="3e843-117">Zodra u hebt gecontroleerd dat alles werkt zoals verwacht, plant u uitvaltijd voor Hallo-migratie.</span><span class="sxs-lookup"><span data-stu-id="3e843-117">Once you have verified that everything works as expected, schedule downtime for hello migration.</span></span> <span data-ttu-id="3e843-118">Tijdens deze uitvaltijd Hallo volgende acties:</span><span class="sxs-lookup"><span data-stu-id="3e843-118">During this downtime, do hello following actions:</span></span>

1.  <span data-ttu-id="3e843-119">Back-up die lokaal zijn opgeslagen op de clusterknooppunten Hallo tijdelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="3e843-119">Back up any transient data stored locally on hello cluster nodes.</span></span> <span data-ttu-id="3e843-120">Bijvoorbeeld, als u gegevens hebt opgeslagen rechtstreeks op een hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="3e843-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="3e843-121">Hallo bestaande cluster verwijderen.</span><span class="sxs-lookup"><span data-stu-id="3e843-121">Delete hello existing cluster.</span></span>
3.  <span data-ttu-id="3e843-122">Een cluster maken in Hallo hetzelfde VNET subnet met de meest recente (of ondersteunde) HDI versie gebruikt dezelfde standaard gegevensopslag die eerder cluster gebruikt Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="3e843-122">Create a cluster in hello same VNET subnet with latest (or supported) HDI version using hello same default data store that hello previous cluster used.</span></span> <span data-ttu-id="3e843-123">Hierdoor Hallo nieuwe cluster toocontinue werken met uw bestaande productiegegevens.</span><span class="sxs-lookup"><span data-stu-id="3e843-123">This allows hello new cluster toocontinue working against your existing production data.</span></span>
4.  <span data-ttu-id="3e843-124">Importeer tijdelijke gegevens die u een back-up.</span><span class="sxs-lookup"><span data-stu-id="3e843-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="3e843-125">Start taken/doorgaan met het verwerken met behulp van het nieuwe cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="3e843-125">Start jobs/continue processing using hello new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e843-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3e843-126">Next Steps</span></span>
* [<span data-ttu-id="3e843-127">Meer informatie over hoe toocreate Linux gebaseerde HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="3e843-127">Learn how toocreate Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="3e843-128">Verbinding maken via SSH tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="3e843-128">Connect tooHDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="3e843-129">Beheer op basis van Linux clusters met Ambari</span><span class="sxs-lookup"><span data-stu-id="3e843-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)


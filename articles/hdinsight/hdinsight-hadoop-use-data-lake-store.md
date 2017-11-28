---
title: aaaUse Data Lake Store met Hadoop in Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe tooquery gegevens van Azure Data Lake Store en toostore resultaten van de analyse.
keywords: blob storage, hdfs, gestructureerde gegevens, niet-gestructureerde gegevens, data lake store
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="b9fb7-104">Data Lake Store gebruiken met Azure HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="b9fb7-104">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="b9fb7-105">tooanalyze gegevens in HDInsight-cluster, kunt u Hallo gegevens opslaan ofwel in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), of beide.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-105">tooanalyze data in HDInsight cluster, you can store hello data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="b9fb7-106">Beide opties voor opslag kunnen u toosafely verwijdert u het die hdinsight-clusters worden gebruikt voor berekeningen zonder verlies van gebruikersgegevens.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="b9fb7-107">In dit artikel wordt beschreven hoe Data Lake Store werkt met HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-107">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="b9fb7-108">toolearn hoe Azure Storage werkt met HDInsight-clusters, Zie [Azure Storage gebruiken met Azure HDInsight-clusters](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b9fb7-108">toolearn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="b9fb7-109">Zie [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) (Hadoop-clusters maken in HDInsight) voor meer informatie over het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-109">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b9fb7-110">De toegang tot Data Lake Store verloopt altijd via een beveiligd kanaal, zodat er geen `adls`-bestandssysteemschemanaam is.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-110">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="b9fb7-111">U gebruikt altijd `adl`.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-111">You always use `adl`.</span></span>
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a><span data-ttu-id="b9fb7-112">Beschikbaarheid van HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="b9fb7-112">Availabilities for HDInsight clusters</span></span>

<span data-ttu-id="b9fb7-113">Hadoop ondersteunt een notatie van het standaardbestandssysteem Hallo.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-113">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="b9fb7-114">Hallo standaardbestandssysteem impliceert een standaardschema en instantie.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-114">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="b9fb7-115">Het kan ook gebruikte tooresolve relatieve paden zijn.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-115">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="b9fb7-116">Tijdens het Hallo HDInsight-cluster maken, kunt u een blob-container in Azure Storage als het standaardbestandssysteem Hallo opgeven of u kunt Azure Storage of Azure Data Lake Store met HDInsight 3.5 en nieuwere versies selecteren als Hallo bestanden van het systeem met een enkele uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-116">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> 

<span data-ttu-id="b9fb7-117">HDInsight-clusters kunnen Data Lake Store op twee manieren gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b9fb7-117">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="b9fb7-118">Als Hallo standaard opslag</span><span class="sxs-lookup"><span data-stu-id="b9fb7-118">As hello default storage</span></span>
* <span data-ttu-id="b9fb7-119">als extra opslag, met Azure Storage Blob als standaardopslag.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-119">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="b9fb7-120">Vanaf nu slechts enkele Hallo HDInsight clusterondersteuning typen/versies met Data Lake Store als standaard opslag en extra opslagaccounts:</span><span class="sxs-lookup"><span data-stu-id="b9fb7-120">As of now, only some of hello HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="b9fb7-121">HDInsight-clustertype</span><span class="sxs-lookup"><span data-stu-id="b9fb7-121">HDInsight cluster type</span></span> | <span data-ttu-id="b9fb7-122">Data Lake Store als standaardopslag</span><span class="sxs-lookup"><span data-stu-id="b9fb7-122">Data Lake Store as default storage</span></span> | <span data-ttu-id="b9fb7-123">Data Lake Store als extra opslag</span><span class="sxs-lookup"><span data-stu-id="b9fb7-123">Data Lake Store as additional storage</span></span>| <span data-ttu-id="b9fb7-124">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="b9fb7-124">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="b9fb7-125">HDInsight-versie 3.6</span><span class="sxs-lookup"><span data-stu-id="b9fb7-125">HDInsight version 3.6</span></span> | <span data-ttu-id="b9fb7-126">Ja</span><span class="sxs-lookup"><span data-stu-id="b9fb7-126">Yes</span></span> | <span data-ttu-id="b9fb7-127">Ja</span><span class="sxs-lookup"><span data-stu-id="b9fb7-127">Yes</span></span> | |
| <span data-ttu-id="b9fb7-128">HDInsight-versie 3.5</span><span class="sxs-lookup"><span data-stu-id="b9fb7-128">HDInsight version 3.5</span></span> | <span data-ttu-id="b9fb7-129">Ja</span><span class="sxs-lookup"><span data-stu-id="b9fb7-129">Yes</span></span> | <span data-ttu-id="b9fb7-130">Ja</span><span class="sxs-lookup"><span data-stu-id="b9fb7-130">Yes</span></span> | <span data-ttu-id="b9fb7-131">Met uitzondering van HBase Hallo</span><span class="sxs-lookup"><span data-stu-id="b9fb7-131">With hello exception of HBase</span></span>|
| <span data-ttu-id="b9fb7-132">HDInsight-versie 3.4</span><span class="sxs-lookup"><span data-stu-id="b9fb7-132">HDInsight version 3.4</span></span> | <span data-ttu-id="b9fb7-133">Nee</span><span class="sxs-lookup"><span data-stu-id="b9fb7-133">No</span></span> | <span data-ttu-id="b9fb7-134">Ja</span><span class="sxs-lookup"><span data-stu-id="b9fb7-134">Yes</span></span> | |
| <span data-ttu-id="b9fb7-135">HDInsight-versie 3.3</span><span class="sxs-lookup"><span data-stu-id="b9fb7-135">HDInsight version 3.3</span></span> | <span data-ttu-id="b9fb7-136">Nee</span><span class="sxs-lookup"><span data-stu-id="b9fb7-136">No</span></span> | <span data-ttu-id="b9fb7-137">Nee</span><span class="sxs-lookup"><span data-stu-id="b9fb7-137">No</span></span> | |
| <span data-ttu-id="b9fb7-138">HDInsight-versie 3.2</span><span class="sxs-lookup"><span data-stu-id="b9fb7-138">HDInsight version 3.2</span></span> | <span data-ttu-id="b9fb7-139">Nee</span><span class="sxs-lookup"><span data-stu-id="b9fb7-139">No</span></span> | <span data-ttu-id="b9fb7-140">Ja</span><span class="sxs-lookup"><span data-stu-id="b9fb7-140">Yes</span></span> | |
| <span data-ttu-id="b9fb7-141">HDInsight Premium (laag)</span><span class="sxs-lookup"><span data-stu-id="b9fb7-141">HDInsight Premium (tier)</span></span>| <span data-ttu-id="b9fb7-142">Nee</span><span class="sxs-lookup"><span data-stu-id="b9fb7-142">No</span></span> | <span data-ttu-id="b9fb7-143">Nee</span><span class="sxs-lookup"><span data-stu-id="b9fb7-143">No</span></span> | |
| <span data-ttu-id="b9fb7-144">Storm</span><span class="sxs-lookup"><span data-stu-id="b9fb7-144">Storm</span></span> | | |<span data-ttu-id="b9fb7-145">U kunt Data Lake Store toowrite gegevens van een Storm-topologie.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-145">You can use Data Lake Store toowrite data from a Storm topology.</span></span> <span data-ttu-id="b9fb7-146">U kunt Data Lake Store ook gebruiken voor referentiegegevens die vervolgens kunnen worden gelezen door een Storm-topologie.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-146">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="b9fb7-147">Met behulp van Data Lake Store als extra storage-account niet van invloed op prestaties of Hallo mogelijkheid tooread of tooAzure opslag schrijven van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-147">Using Data Lake Store as an additional storage account does not affect performance or hello ability tooread or write tooAzure storage from hello cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="b9fb7-148">Data Lake Store als standaardopslag gebruiken</span><span class="sxs-lookup"><span data-stu-id="b9fb7-148">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="b9fb7-149">Wanneer HDInsight met Data Lake Store als standaard opslag wordt geïmplementeerd, worden Hallo cluster-gerelateerde bestanden opgeslagen in Data Lake Store in Hallo locatie te volgen:</span><span class="sxs-lookup"><span data-stu-id="b9fb7-149">When HDInsight is deployed with Data Lake Store as default storage, hello cluster-related files are stored in Data Lake Store in hello following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="b9fb7-150">waar `<cluster_root_path>` Hallo naam is van een map die u in Data Lake Store maakt.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-150">where `<cluster_root_path>` is hello name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="b9fb7-151">Als u een pad naar de hoofdmap van ieder cluster opgeeft, kunt u dezelfde Data Lake Store-account voor meer dan één cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-151">By specifying a root path for each cluster, you can use hello same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="b9fb7-152">U kunt dus instellingen hebben waarbij:</span><span class="sxs-lookup"><span data-stu-id="b9fb7-152">So, you can have a setup where:</span></span>

* <span data-ttu-id="b9fb7-153">Cluster1 kunt Hallo pad gebruiken`adl://mydatalakestore/cluster1storage`</span><span class="sxs-lookup"><span data-stu-id="b9fb7-153">Cluster1 can use hello path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="b9fb7-154">Cluster2 kunt Hallo pad gebruiken`adl://mydatalakestore/cluster2storage`</span><span class="sxs-lookup"><span data-stu-id="b9fb7-154">Cluster2 can use hello path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="b9fb7-155">U ziet dat beide clusters gebruik Hallo Hallo dezelfde Data Lake Store-account **mydatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-155">Notice that both hello clusters use hello same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="b9fb7-156">Elk cluster heeft toegang tot tooits eigenaar hoofdmap bestandssysteem in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-156">Each cluster has access tooits own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="b9fb7-157">Hello Azure portal implementatie-ervaring met name wordt u gevraagd een mapnaam toouse zoals **/clusters/\<clustername >** voor Hallo hoofdpad.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-157">hello Azure portal deployment experience in particular prompts you toouse a folder name such as **/clusters/\<clustername>** for hello root path.</span></span>

<span data-ttu-id="b9fb7-158">toobe kunnen toouse een Data Lake Store als standaard opslag, moet u verlenen Hallo service principal toegang toohello paden te volgen:</span><span class="sxs-lookup"><span data-stu-id="b9fb7-158">toobe able toouse a Data Lake Store as default storage, you must grant hello service principal access toohello following paths:</span></span>

- <span data-ttu-id="b9fb7-159">Hallo Data Lake Store-account root.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-159">hello Data Lake Store account root.</span></span>  <span data-ttu-id="b9fb7-160">Bijvoorbeeld: adl://mydatalakestore/.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-160">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="b9fb7-161">Hallo-map voor alle mappen van het cluster.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-161">hello folder for all cluster folders.</span></span>  <span data-ttu-id="b9fb7-162">Bijvoorbeeld: adl://mydatalakestore/clusters.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-162">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="b9fb7-163">Hallo-map voor het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-163">hello folder for hello cluster.</span></span>  <span data-ttu-id="b9fb7-164">Bijvoorbeeld: adl://mydatalakestore/clusters/cluster1storage.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-164">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="b9fb7-165">Zie [Configure Data Lake store access](#configure-data-lake-store-access) voor meer informatie over het maken van service-principal en het verlenen van toegang.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-165">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="b9fb7-166">Data Lake Store als extra opslag gebruiken</span><span class="sxs-lookup"><span data-stu-id="b9fb7-166">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="b9fb7-167">U kunt Data Lake Store als extra opslag voor ook Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-167">You can use Data Lake Store as additional storage for hello cluster as well.</span></span> <span data-ttu-id="b9fb7-168">In dergelijke gevallen kan Hallo standaard clusteropslag zijn van een Azure Storage-Blob of een Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-168">In such cases, hello cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="b9fb7-169">Als u een HDInsight-taken op Hallo-gegevens die zijn opgeslagen in Data Lake Store als extra opslagruimte uitvoert, moet u Hallo volledig gekwalificeerde pad toohello bestanden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-169">If you are running HDInsight jobs against hello data stored in Data Lake Store as additional storage, you must use hello fully-qualified path toohello files.</span></span> <span data-ttu-id="b9fb7-170">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b9fb7-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="b9fb7-171">Er is geen **cluster_root_path** in nu Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-171">Note that there's no **cluster_root_path** in hello URL now.</span></span> <span data-ttu-id="b9fb7-172">Dat komt doordat Data Lake Store is niet een standaard-opslag in dit geval zodat toodo hoeft u Hallo pad toohello bestanden.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-172">That's because Data Lake Store is not a default storage in this case so all you need toodo is provide hello path toohello files.</span></span>

<span data-ttu-id="b9fb7-173">toobe kunnen toouse een Data Lake Store als extra opslagruimte, hoeft u alleen toogrant Hallo service principal toegang toohello paden waar uw bestanden worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-173">toobe able toouse a Data Lake Store as additional storage, you only need toogrant hello service principal access toohello paths where your files are stored.</span></span>  <span data-ttu-id="b9fb7-174">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b9fb7-174">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="b9fb7-175">Zie [Configure Data Lake store access](#configure-data-lake-store-access) voor meer informatie over het maken van service-principal en het verlenen van toegang.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-175">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="b9fb7-176">Meerdere Data Lake Store-accounts gebruiken</span><span class="sxs-lookup"><span data-stu-id="b9fb7-176">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="b9fb7-177">Een Data Lake Store-account als extra toe te voegen en het toevoegen van meer dan één Data Lake Store worden accounts bereikt door geeft Hallo HDInsight-cluster toestemming van de gegevens in een of meer Data Lake Store-accounts.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-177">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving hello HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="b9fb7-178">Zie [Toegang tot Data Lake Store configureren](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="b9fb7-178">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="b9fb7-179">Toegang tot Data Lake Store configureren</span><span class="sxs-lookup"><span data-stu-id="b9fb7-179">Configure Data Lake store access</span></span>

<span data-ttu-id="b9fb7-180">tooconfigure Data Lake store toegang vanaf uw HDInsight-cluster, moet u een Azure Active directory (Azure AD) service-principal hebben.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-180">tooconfigure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="b9fb7-181">Alleen een Azure AD-beheerder kan een service-principal maken.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-181">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="b9fb7-182">Hallo-service-principal moet worden gemaakt met een certificaat.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-182">hello service principal must be created with a certificate.</span></span> <span data-ttu-id="b9fb7-183">Zie voor meer informatie [Toegang tot Data Lake Store configureren](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) en [Service-principal maken met zelfondertekend certificaat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="b9fb7-183">For more information, see [Configure Data Lake Store access](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="b9fb7-184">Als u toouse Azure Data Lake Store als extra opslag voor HDInsight-cluster gaat, wordt aangeraden dat u dit doen terwijl u Hallo-cluster maakt, zoals beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-184">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="b9fb7-185">Het toevoegen van Azure Data Lake Store als extra opslagruimte tooan is bestaand HDInsight-cluster een ingewikkeld proces en foutgevoelige tooerrors.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-185">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

## <a name="access-files-from-hello-cluster"></a><span data-ttu-id="b9fb7-186">Toegang tot bestanden Hallo-cluster</span><span class="sxs-lookup"><span data-stu-id="b9fb7-186">Access files from hello cluster</span></span>

<span data-ttu-id="b9fb7-187">Er zijn verschillende manieren Hallo-bestanden in Data Lake Store is toegankelijk vanuit een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-187">There are several ways you can access hello files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="b9fb7-188">**De volledig gekwalificeerde naam Hallo**.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-188">**Using hello fully qualified name**.</span></span> <span data-ttu-id="b9fb7-189">Met deze methode voert u Hallo volledig pad toohello bestand opgeven dat u wilt dat tooaccess.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-189">With this approach, you provide hello full path toohello file that you want tooaccess.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="b9fb7-190">**Met behulp van de verkorte padindeling Hallo**.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-190">**Using hello shortened path format**.</span></span> <span data-ttu-id="b9fb7-191">Met deze methode voert u Hallo pad up toohello cluster hoofdmap vervangen door adl: / / /.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-191">With this approach, you replace hello path up toohello cluster root with adl:///.</span></span> <span data-ttu-id="b9fb7-192">Dus in bovenstaande Hallo voorbeeld, kunt u vervangen `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` met `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-192">So, in hello example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="b9fb7-193">**Met behulp van het relatieve pad Hallo**.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-193">**Using hello relative path**.</span></span> <span data-ttu-id="b9fb7-194">Met deze methode voert u alleen Hallo relatief pad toohello bestand opgeven dat u wilt dat tooaccess.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-194">With this approach, you only provide hello relative path toohello file that you want tooaccess.</span></span> <span data-ttu-id="b9fb7-195">Als bijvoorbeeld Hallo volledige pad toohello bestand is:</span><span class="sxs-lookup"><span data-stu-id="b9fb7-195">For example, if hello complete path toohello file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="b9fb7-196">U hebt toegang tot hetzelfde sample.log bestand Hallo met behulp van deze relatief pad in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-196">You can access hello same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a><span data-ttu-id="b9fb7-197">HDInsight-clusters maken met toegang tot tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="b9fb7-197">Create HDInsight clusters with access tooData Lake Store</span></span>

<span data-ttu-id="b9fb7-198">Gebruik Hallo koppelingen voor gedetailleerde instructies te volgen op hoe toocreate HDInsight-clusters met toegang tot tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-198">Use hello following links for detailed instructions on how toocreate HDInsight clusters with access tooData Lake Store.</span></span>

* [<span data-ttu-id="b9fb7-199">Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="b9fb7-199">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="b9fb7-200">PowerShell gebruiken (met Data Lake Store als standaardopslag)</span><span class="sxs-lookup"><span data-stu-id="b9fb7-200">Using PowerShell (with Data Lake Store as default storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [<span data-ttu-id="b9fb7-201">PowerShell gebruiken (met Data Lake Store als extra opslag)</span><span class="sxs-lookup"><span data-stu-id="b9fb7-201">Using PowerShell (with Data Lake Store as additional storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [<span data-ttu-id="b9fb7-202">Azure-sjablonen gebruiken</span><span class="sxs-lookup"><span data-stu-id="b9fb7-202">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="b9fb7-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b9fb7-203">Next steps</span></span>
<span data-ttu-id="b9fb7-204">In dit artikel hebt u geleerd hoe toouse HDFS-compatibele Azure Data Lake Store met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-204">In this article, you learned how toouse HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="b9fb7-205">Hiermee kunt u toobuild schaalbare, op lange termijn, archiveren voor gegevensverzameling en gebruik HDInsight toounlock Hallo informatie binnen Hallo opgeslagen gestructureerde en ongestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="b9fb7-205">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="b9fb7-206">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="b9fb7-206">For more information, see:</span></span>

* <span data-ttu-id="b9fb7-207">[Aan de slag met Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="b9fb7-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="b9fb7-208">Aan de slag met Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b9fb7-208">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="b9fb7-209">[Uploaden van gegevens tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="b9fb7-209">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="b9fb7-210">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="b9fb7-210">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="b9fb7-211">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="b9fb7-211">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="b9fb7-212">[Azure Storage Shared Access Signatures toorestrict toegang toodata gebruiken met HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="b9fb7-212">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  

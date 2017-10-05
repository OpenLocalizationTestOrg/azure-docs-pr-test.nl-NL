---
title: Data Lake Store met Hadoop in Azure HDInsight gebruiken| Microsoft Docs
description: Informatie over hoe u gegevens opvraagt uit Azure Data Lake Store en hoe u resultaten van uw analyse opslaat.
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
ms.openlocfilehash: 28a836aff65636ef0031ac63f633d746436d7e4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="d96f0-104">Data Lake Store gebruiken met Azure HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="d96f0-104">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="d96f0-105">Als u gegevens wilt analyseren in een HDInsight-cluster, kunt u de gegevens opslaan in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md) of beide.</span><span class="sxs-lookup"><span data-stu-id="d96f0-105">To analyze data in HDInsight cluster, you can store the data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="d96f0-106">Met beide opslagopties kunt u de HDInsight-clusters die worden gebruikt voor berekeningen, veilig verwijderen zonder dat er gebruikersgegevens verloren gaan.</span><span class="sxs-lookup"><span data-stu-id="d96f0-106">Both storage options enable you to safely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="d96f0-107">In dit artikel wordt beschreven hoe Data Lake Store werkt met HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="d96f0-107">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="d96f0-108">Zie [Azure Storage gebruiken met Azure HDInsight-clusters](hdinsight-hadoop-use-blob-storage.md) voor informatie over de werking van Azure Storage met HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="d96f0-108">To learn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="d96f0-109">Zie [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) (Hadoop-clusters maken in HDInsight) voor meer informatie over het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="d96f0-109">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d96f0-110">De toegang tot Data Lake Store verloopt altijd via een beveiligd kanaal, zodat er geen `adls`-bestandssysteemschemanaam is.</span><span class="sxs-lookup"><span data-stu-id="d96f0-110">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="d96f0-111">U gebruikt altijd `adl`.</span><span class="sxs-lookup"><span data-stu-id="d96f0-111">You always use `adl`.</span></span>
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a><span data-ttu-id="d96f0-112">Beschikbaarheid van HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="d96f0-112">Availabilities for HDInsight clusters</span></span>

<span data-ttu-id="d96f0-113">Hadoop ondersteunt een notatie van het standaardbestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="d96f0-113">Hadoop supports a notion of the default file system.</span></span> <span data-ttu-id="d96f0-114">Het standaardbestandssysteem impliceert een standaardschema en instantie.</span><span class="sxs-lookup"><span data-stu-id="d96f0-114">The default file system implies a default scheme and authority.</span></span> <span data-ttu-id="d96f0-115">De toepassing kan ook worden gebruikt om relatieve paden om te zetten.</span><span class="sxs-lookup"><span data-stu-id="d96f0-115">It can also be used to resolve relative paths.</span></span> <span data-ttu-id="d96f0-116">Wanneer u het HDInsight-cluster maakt, kunt u in Azure Storage een blobcontainer opgeven als het standaardbestandssysteem. Met HDInsight 3.5 en latere versies kunt u ook Azure Storage of Azure Data Lake Store als het standaardbestandssysteem selecteren met een paar uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="d96f0-116">During the HDInsight cluster creation process, you can specify a blob container in Azure Storage as the default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as the default files system with a few exceptions.</span></span> 

<span data-ttu-id="d96f0-117">HDInsight-clusters kunnen Data Lake Store op twee manieren gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d96f0-117">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="d96f0-118">als standaardopslag</span><span class="sxs-lookup"><span data-stu-id="d96f0-118">As the default storage</span></span>
* <span data-ttu-id="d96f0-119">als extra opslag, met Azure Storage Blob als standaardopslag.</span><span class="sxs-lookup"><span data-stu-id="d96f0-119">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="d96f0-120">Op dit moment ondersteunt slechts een deel van de HDInsight-clustertypen/-versies het gebruik van Data Lake Store als standaardopslag en extra opslagaccounts:</span><span class="sxs-lookup"><span data-stu-id="d96f0-120">As of now, only some of the HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="d96f0-121">HDInsight-clustertype</span><span class="sxs-lookup"><span data-stu-id="d96f0-121">HDInsight cluster type</span></span> | <span data-ttu-id="d96f0-122">Data Lake Store als standaardopslag</span><span class="sxs-lookup"><span data-stu-id="d96f0-122">Data Lake Store as default storage</span></span> | <span data-ttu-id="d96f0-123">Data Lake Store als extra opslag</span><span class="sxs-lookup"><span data-stu-id="d96f0-123">Data Lake Store as additional storage</span></span>| <span data-ttu-id="d96f0-124">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="d96f0-124">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="d96f0-125">HDInsight-versie 3.6</span><span class="sxs-lookup"><span data-stu-id="d96f0-125">HDInsight version 3.6</span></span> | <span data-ttu-id="d96f0-126">Ja</span><span class="sxs-lookup"><span data-stu-id="d96f0-126">Yes</span></span> | <span data-ttu-id="d96f0-127">Ja</span><span class="sxs-lookup"><span data-stu-id="d96f0-127">Yes</span></span> | |
| <span data-ttu-id="d96f0-128">HDInsight-versie 3.5</span><span class="sxs-lookup"><span data-stu-id="d96f0-128">HDInsight version 3.5</span></span> | <span data-ttu-id="d96f0-129">Ja</span><span class="sxs-lookup"><span data-stu-id="d96f0-129">Yes</span></span> | <span data-ttu-id="d96f0-130">Ja</span><span class="sxs-lookup"><span data-stu-id="d96f0-130">Yes</span></span> | <span data-ttu-id="d96f0-131">Met uitzondering van HBase</span><span class="sxs-lookup"><span data-stu-id="d96f0-131">With the exception of HBase</span></span>|
| <span data-ttu-id="d96f0-132">HDInsight-versie 3.4</span><span class="sxs-lookup"><span data-stu-id="d96f0-132">HDInsight version 3.4</span></span> | <span data-ttu-id="d96f0-133">Nee</span><span class="sxs-lookup"><span data-stu-id="d96f0-133">No</span></span> | <span data-ttu-id="d96f0-134">Ja</span><span class="sxs-lookup"><span data-stu-id="d96f0-134">Yes</span></span> | |
| <span data-ttu-id="d96f0-135">HDInsight-versie 3.3</span><span class="sxs-lookup"><span data-stu-id="d96f0-135">HDInsight version 3.3</span></span> | <span data-ttu-id="d96f0-136">Nee</span><span class="sxs-lookup"><span data-stu-id="d96f0-136">No</span></span> | <span data-ttu-id="d96f0-137">Nee</span><span class="sxs-lookup"><span data-stu-id="d96f0-137">No</span></span> | |
| <span data-ttu-id="d96f0-138">HDInsight-versie 3.2</span><span class="sxs-lookup"><span data-stu-id="d96f0-138">HDInsight version 3.2</span></span> | <span data-ttu-id="d96f0-139">Nee</span><span class="sxs-lookup"><span data-stu-id="d96f0-139">No</span></span> | <span data-ttu-id="d96f0-140">Ja</span><span class="sxs-lookup"><span data-stu-id="d96f0-140">Yes</span></span> | |
| <span data-ttu-id="d96f0-141">HDInsight Premium (laag)</span><span class="sxs-lookup"><span data-stu-id="d96f0-141">HDInsight Premium (tier)</span></span>| <span data-ttu-id="d96f0-142">Nee</span><span class="sxs-lookup"><span data-stu-id="d96f0-142">No</span></span> | <span data-ttu-id="d96f0-143">Nee</span><span class="sxs-lookup"><span data-stu-id="d96f0-143">No</span></span> | |
| <span data-ttu-id="d96f0-144">Storm</span><span class="sxs-lookup"><span data-stu-id="d96f0-144">Storm</span></span> | | |<span data-ttu-id="d96f0-145">U kunt Data Lake Store gebruiken om gegevens te schrijven op basis van een Storm-topologie.</span><span class="sxs-lookup"><span data-stu-id="d96f0-145">You can use Data Lake Store to write data from a Storm topology.</span></span> <span data-ttu-id="d96f0-146">U kunt Data Lake Store ook gebruiken voor referentiegegevens die vervolgens kunnen worden gelezen door een Storm-topologie.</span><span class="sxs-lookup"><span data-stu-id="d96f0-146">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="d96f0-147">Het gebruik van Data Lake Store als extra opslagaccount heeft geen invloed op de prestaties of de mogelijkheid om te lezen of schrijven naar Azure-opslag vanuit het cluster.</span><span class="sxs-lookup"><span data-stu-id="d96f0-147">Using Data Lake Store as an additional storage account does not affect performance or the ability to read or write to Azure storage from the cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="d96f0-148">Data Lake Store als standaardopslag gebruiken</span><span class="sxs-lookup"><span data-stu-id="d96f0-148">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="d96f0-149">Wanneer HDInsight met Data Lake Store als standaardopslag is geïmplementeerd, worden de clusterbestanden in Data Lake Store op de volgende locatie opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="d96f0-149">When HDInsight is deployed with Data Lake Store as default storage, the cluster-related files are stored in Data Lake Store in the following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="d96f0-150">waar `<cluster_root_path>` de naam is van een map die u in Data Lake Store maakt.</span><span class="sxs-lookup"><span data-stu-id="d96f0-150">where `<cluster_root_path>` is the name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="d96f0-151">Als u voor elk cluster een pad naar een hoofdmap opgeeft, kunt u hetzelfde Data Lake Store-account voor meer dan één cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d96f0-151">By specifying a root path for each cluster, you can use the same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="d96f0-152">U kunt dus instellingen hebben waarbij:</span><span class="sxs-lookup"><span data-stu-id="d96f0-152">So, you can have a setup where:</span></span>

* <span data-ttu-id="d96f0-153">Cluster1 het pad `adl://mydatalakestore/cluster1storage` kan gebruiken</span><span class="sxs-lookup"><span data-stu-id="d96f0-153">Cluster1 can use the path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="d96f0-154">Cluster2 het pad `adl://mydatalakestore/cluster2storage` kan gebruiken</span><span class="sxs-lookup"><span data-stu-id="d96f0-154">Cluster2 can use the path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="d96f0-155">U ziet dat beide clusters hetzelfde Data Lake Store-account **mydatalakestore** gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d96f0-155">Notice that both the clusters use the same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="d96f0-156">Elk cluster heeft toegang tot een eigen basisbestandssysteem in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d96f0-156">Each cluster has access to its own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="d96f0-157">In het Azure Portal-implementatiescenario wordt u gevraagd voor het pad naar de hoofdmap een mapnaam te gebruiken zoals **/clusters/\<clusternaam>**.</span><span class="sxs-lookup"><span data-stu-id="d96f0-157">The Azure portal deployment experience in particular prompts you to use a folder name such as **/clusters/\<clustername>** for the root path.</span></span>

<span data-ttu-id="d96f0-158">Om Data Lake Store te gebruiken als standaardopslag, moet u de service-principal toegang verlenen tot de volgende paden:</span><span class="sxs-lookup"><span data-stu-id="d96f0-158">To be able to use a Data Lake Store as default storage, you must grant the service principal access to the following paths:</span></span>

- <span data-ttu-id="d96f0-159">De hoofdmap van het Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="d96f0-159">The Data Lake Store account root.</span></span>  <span data-ttu-id="d96f0-160">Bijvoorbeeld: adl://mydatalakestore/.</span><span class="sxs-lookup"><span data-stu-id="d96f0-160">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="d96f0-161">De map voor alle mappen van het cluster.</span><span class="sxs-lookup"><span data-stu-id="d96f0-161">The folder for all cluster folders.</span></span>  <span data-ttu-id="d96f0-162">Bijvoorbeeld: adl://mydatalakestore/clusters.</span><span class="sxs-lookup"><span data-stu-id="d96f0-162">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="d96f0-163">De map voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="d96f0-163">The folder for the cluster.</span></span>  <span data-ttu-id="d96f0-164">Bijvoorbeeld: adl://mydatalakestore/clusters/cluster1storage.</span><span class="sxs-lookup"><span data-stu-id="d96f0-164">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="d96f0-165">Zie [Configure Data Lake store access](#configure-data-lake-store-access) voor meer informatie over het maken van service-principal en het verlenen van toegang.</span><span class="sxs-lookup"><span data-stu-id="d96f0-165">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="d96f0-166">Data Lake Store als extra opslag gebruiken</span><span class="sxs-lookup"><span data-stu-id="d96f0-166">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="d96f0-167">U kunt ook Data Lake Store gebruiken als extra opslag voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="d96f0-167">You can use Data Lake Store as additional storage for the cluster as well.</span></span> <span data-ttu-id="d96f0-168">In dergelijke gevallen kan de standaardopslag voor het cluster een Azure Storage Blob of een Data Lake Store-account zijn.</span><span class="sxs-lookup"><span data-stu-id="d96f0-168">In such cases, the cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="d96f0-169">Als u HDInsight-taken uitvoert voor gegevens die in Data Lake Store als extra opslag zijn opgeslagen, dient u het volledige pad naar de bestanden te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d96f0-169">If you are running HDInsight jobs against the data stored in Data Lake Store as additional storage, you must use the fully-qualified path to the files.</span></span> <span data-ttu-id="d96f0-170">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d96f0-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="d96f0-171">U ziet dat er nu geen **cluster_root_path** in de URL is.</span><span class="sxs-lookup"><span data-stu-id="d96f0-171">Note that there's no **cluster_root_path** in the URL now.</span></span> <span data-ttu-id="d96f0-172">Dat komt doordat Data Lake Store in dit geval geen standaardopslag is, dus u hoeft alleen het pad naar de bestanden op te geven.</span><span class="sxs-lookup"><span data-stu-id="d96f0-172">That's because Data Lake Store is not a default storage in this case so all you need to do is provide the path to the files.</span></span>

<span data-ttu-id="d96f0-173">Om een Data Lake Store als extra opslagruimte te kunnen gebruiken, moet u alleen de service-principal toegang verlenen tot de paden waar uw bestanden worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d96f0-173">To be able to use a Data Lake Store as additional storage, you only need to grant the service principal access to the paths where your files are stored.</span></span>  <span data-ttu-id="d96f0-174">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d96f0-174">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="d96f0-175">Zie [Configure Data Lake store access](#configure-data-lake-store-access) voor meer informatie over het maken van service-principal en het verlenen van toegang.</span><span class="sxs-lookup"><span data-stu-id="d96f0-175">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="d96f0-176">Meerdere Data Lake Store-accounts gebruiken</span><span class="sxs-lookup"><span data-stu-id="d96f0-176">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="d96f0-177">Een Data Lake Store-account als extra toevoegen en het toevoegen van meerdere Data Lake Store-accounts wordt bereikt door het HDInsight-cluster te machtigen voor gegevens in een of meer Data Lake Store-accounts.</span><span class="sxs-lookup"><span data-stu-id="d96f0-177">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving the HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="d96f0-178">Zie [Toegang tot Data Lake Store configureren](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="d96f0-178">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="d96f0-179">Toegang tot Data Lake Store configureren</span><span class="sxs-lookup"><span data-stu-id="d96f0-179">Configure Data Lake store access</span></span>

<span data-ttu-id="d96f0-180">Voor het configureren van toegang tot de Data Lake Store vanuit uw HDInsight-cluster moet u een Azure Active Directory (Azure AD) service-principal hebben.</span><span class="sxs-lookup"><span data-stu-id="d96f0-180">To configure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="d96f0-181">Alleen een Azure AD-beheerder kan een service-principal maken.</span><span class="sxs-lookup"><span data-stu-id="d96f0-181">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="d96f0-182">De service-principal moet worden gemaakt met een certificaat.</span><span class="sxs-lookup"><span data-stu-id="d96f0-182">The service principal must be created with a certificate.</span></span> <span data-ttu-id="d96f0-183">Zie voor meer informatie [Toegang tot Data Lake Store configureren](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) en [Service-principal maken met zelfondertekend certificaat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="d96f0-183">For more information, see [Configure Data Lake Store access](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="d96f0-184">Als u Azure Data Lake Store als extra opslag voor HDInsight-cluster wilt gebruiken, is het raadzaam dat te doen terwijl u het cluster maakt zoals beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="d96f0-184">If you are going to use Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create the cluster as described in this article.</span></span> <span data-ttu-id="d96f0-185">Azure Data Lake Store als extra opslagruimte toevoegen aan een bestaand HDInsight-cluster is een ingewikkeld proces en gevoelig voor fouten.</span><span class="sxs-lookup"><span data-stu-id="d96f0-185">Adding Azure Data Lake Store as additional storage to an existing HDInsight cluster is a complicated process and prone to errors.</span></span>
>

## <a name="access-files-from-the-cluster"></a><span data-ttu-id="d96f0-186">Bestanden openen vanuit het cluster</span><span class="sxs-lookup"><span data-stu-id="d96f0-186">Access files from the cluster</span></span>

<span data-ttu-id="d96f0-187">Er is een aantal manieren waarop u de bestanden in Data Lake Store vanuit een HDInsight-cluster kunt openen.</span><span class="sxs-lookup"><span data-stu-id="d96f0-187">There are several ways you can access the files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="d96f0-188">**De volledig gekwalificeerde naam gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="d96f0-188">**Using the fully qualified name**.</span></span> <span data-ttu-id="d96f0-189">Met deze methode geeft u het volledige pad op naar het bestand dat u wilt openen.</span><span class="sxs-lookup"><span data-stu-id="d96f0-189">With this approach, you provide the full path to the file that you want to access.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="d96f0-190">**De verkorte padnotatie gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="d96f0-190">**Using the shortened path format**.</span></span> <span data-ttu-id="d96f0-191">Met deze methode vervangt u het pad tot de hoofdmap van het cluster door adl:///.</span><span class="sxs-lookup"><span data-stu-id="d96f0-191">With this approach, you replace the path up to the cluster root with adl:///.</span></span> <span data-ttu-id="d96f0-192">In het bovenstaande voorbeeld kunt u `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` vervangen door `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="d96f0-192">So, in the example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="d96f0-193">**Het relatieve pad gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="d96f0-193">**Using the relative path**.</span></span> <span data-ttu-id="d96f0-194">Met deze methode geeft u alleen het volledige relatieve pad op naar het bestand dat u wilt openen.</span><span class="sxs-lookup"><span data-stu-id="d96f0-194">With this approach, you only provide the relative path to the file that you want to access.</span></span> <span data-ttu-id="d96f0-195">Als dit bijvoorbeeld het volledige pad naar het bestand is:</span><span class="sxs-lookup"><span data-stu-id="d96f0-195">For example, if the complete path to the file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="d96f0-196">U kunt hetzelfde bestand sample.log in plaats daarvan via dit relatieve pad openen.</span><span class="sxs-lookup"><span data-stu-id="d96f0-196">You can access the same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-to-data-lake-store"></a><span data-ttu-id="d96f0-197">HDInsight-clusters maken met toegang tot Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d96f0-197">Create HDInsight clusters with access to Data Lake Store</span></span>

<span data-ttu-id="d96f0-198">Gebruik de volgende koppelingen voor gedetailleerde instructies over het maken van HDInsight-clusters met toegang tot Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d96f0-198">Use the following links for detailed instructions on how to create HDInsight clusters with access to Data Lake Store.</span></span>

* [<span data-ttu-id="d96f0-199">Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="d96f0-199">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="d96f0-200">PowerShell gebruiken (met Data Lake Store als standaardopslag)</span><span class="sxs-lookup"><span data-stu-id="d96f0-200">Using PowerShell (with Data Lake Store as default storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [<span data-ttu-id="d96f0-201">PowerShell gebruiken (met Data Lake Store als extra opslag)</span><span class="sxs-lookup"><span data-stu-id="d96f0-201">Using PowerShell (with Data Lake Store as additional storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [<span data-ttu-id="d96f0-202">Azure-sjablonen gebruiken</span><span class="sxs-lookup"><span data-stu-id="d96f0-202">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="d96f0-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d96f0-203">Next steps</span></span>
<span data-ttu-id="d96f0-204">In dit artikel hebt u geleerd hoe u HDFS-compatibele Azure Data Lake Store kunt gebruiken met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d96f0-204">In this article, you learned how to use HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="d96f0-205">Zodoende kunt u een schaalbare, duurzame, archiveringsoplossing voor gegevensverzameling bouwen en HDInsight gebruiken om de informatie te ontsluiten in de opgeslagen gestructureerde en ongestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="d96f0-205">This allows you to build scalable, long-term, archiving data acquisition solutions and use HDInsight to unlock the information inside the stored structured and unstructured data.</span></span>

<span data-ttu-id="d96f0-206">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="d96f0-206">For more information, see:</span></span>

* <span data-ttu-id="d96f0-207">[Aan de slag met Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="d96f0-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="d96f0-208">Aan de slag met Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d96f0-208">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="d96f0-209">[Gegevens uploaden naar HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="d96f0-209">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="d96f0-210">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="d96f0-210">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="d96f0-211">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="d96f0-211">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="d96f0-212">[Handtekeningen voor gedeelde toegang van Azure Storage gebruiken om de toegang tot gegevens te beperken met HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="d96f0-212">[Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight][hdinsight-use-sas]</span></span>

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

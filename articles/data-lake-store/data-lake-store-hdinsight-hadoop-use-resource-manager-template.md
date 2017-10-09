---
title: aaaUse Azure-sjablonen toocreate HDInsight en Data Lake Store | Microsoft Docs
description: Gebruik Azure Resource Manager-sjablonen toocreate en HDInsight-clusters gebruiken met Azure Data Lake Store
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="716fd-103">Een HDInsight-cluster maken met Data Lake Store met Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="716fd-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="716fd-104">Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="716fd-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="716fd-105">Met behulp van PowerShell (voor opslag van de standaard)</span><span class="sxs-lookup"><span data-stu-id="716fd-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="716fd-106">Met behulp van PowerShell (voor extra opslagruimte)</span><span class="sxs-lookup"><span data-stu-id="716fd-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="716fd-107">Resource Manager gebruiken</span><span class="sxs-lookup"><span data-stu-id="716fd-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="716fd-108">Meer informatie over hoe toouse Azure PowerShell tooconfigure een HDInsight-cluster met Azure Data Lake Store **als extra opslagruimte**.</span><span class="sxs-lookup"><span data-stu-id="716fd-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="716fd-109">Voor ondersteunde clustertypen, worden Data Lake Store gebruikt als een standaard-opslag- of aanvullende storage-account.</span><span class="sxs-lookup"><span data-stu-id="716fd-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="716fd-110">Wanneer Data Lake Store als extra opslagruimte wordt gebruikt, Hallo storage-standaardaccount voor Hallo clusters is nog steeds Azure Storage-Blobs (WASB) en Hallo cluster-gerelateerde bestanden (zoals Logboeken, enzovoort) worden nog steeds geschreven toohello standaard opslag tijdens het Hallo-gegevens die u hebt gewenste tooprocess kunnen worden opgeslagen in een Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="716fd-110">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="716fd-111">Met behulp van Data Lake Store als extra storage-account heeft geen gevolgen voor prestaties of de Hallo mogelijkheid tooread schrijftijd toohello opslag van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="716fd-111">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="716fd-112">Met behulp van Data Lake Store voor opslag van HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="716fd-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="716fd-113">Hier volgen enkele belangrijke overwegingen voor het gebruik van HDInsight met Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="716fd-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="716fd-114">Optie toocreate HDInsight-clusters met toegang tooData Lake Store als standaard opslag is beschikbaar voor HDInsight versie 3.5 en 3.6.</span><span class="sxs-lookup"><span data-stu-id="716fd-114">Option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="716fd-115">Optie toocreate HDInsight-clusters met toegang tooData Lake Store als extra opslag is beschikbaar voor HDInsight versie 3.2, 3.4, 3.5 en 3.6.</span><span class="sxs-lookup"><span data-stu-id="716fd-115">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="716fd-116">In dit artikel inrichten we een Hadoop-cluster met Data Lake Store als extra opslagruimte.</span><span class="sxs-lookup"><span data-stu-id="716fd-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="716fd-117">Zie voor instructies over hoe toocreate een Hadoop-cluster met Data Lake Store als standaard opslag, [een HDInsight-cluster maken met Data Lake Store met Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="716fd-117">For instructions on how toocreate a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="716fd-118">Vereisten</span><span class="sxs-lookup"><span data-stu-id="716fd-118">Prerequisites</span></span>
<span data-ttu-id="716fd-119">Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="716fd-119">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="716fd-120">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="716fd-120">**An Azure subscription**.</span></span> <span data-ttu-id="716fd-121">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="716fd-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="716fd-122">**Azure PowerShell 1.0 of hoger**.</span><span class="sxs-lookup"><span data-stu-id="716fd-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="716fd-123">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="716fd-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="716fd-124">**Azure Active Directory Service-Principal**.</span><span class="sxs-lookup"><span data-stu-id="716fd-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="716fd-125">Stappen in deze zelfstudie bieden instructies over het toocreate een service-principal in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="716fd-125">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="716fd-126">U moet echter een Azure AD-beheerder toobe kunnen toocreate een service-principal.</span><span class="sxs-lookup"><span data-stu-id="716fd-126">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="716fd-127">Als u een Azure AD-beheerder bent, kunt u deze vereiste overslaan en doorgaan met het Hallo-zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="716fd-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="716fd-128">**Als u niet een Azure AD-beheerder**, u zich niet kunnen tooperform Hallo stappen vereist toocreate een service-principal.</span><span class="sxs-lookup"><span data-stu-id="716fd-128">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="716fd-129">In dat geval moet uw Azure AD-beheerder eerst een service-principal maken voordat u een HDInsight-cluster met Data Lake Store maken kunt.</span><span class="sxs-lookup"><span data-stu-id="716fd-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="716fd-130">Bovendien Hallo service-principal moet worden gemaakt met een certificaat, zoals beschreven op [een service-principal maken met certificaat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="716fd-130">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="716fd-131">Een HDInsight-cluster maken met Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="716fd-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="716fd-132">Hallo Resource Manager-sjabloon en Hallo vereisten voor het gebruik van de sjabloon hello, zijn beschikbaar op GitHub op [een HDInsight Linux-cluster met nieuwe Data Lake Store implementeren](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="716fd-132">hello Resource Manager template, and hello prerequisites for using hello template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="716fd-133">Volg Hallo instructies op deze koppeling toocreate een HDInsight-cluster met Azure Data Lake Store als extra opslagruimte Hallo.</span><span class="sxs-lookup"><span data-stu-id="716fd-133">Follow hello instructions provided at this link toocreate an HDInsight cluster with Azure Data Lake Store as hello additional storage.</span></span>

<span data-ttu-id="716fd-134">Hallo-instructies op de hierboven genoemde Hallo-koppeling vereist PowerShell.</span><span class="sxs-lookup"><span data-stu-id="716fd-134">hello instructions at hello link mentioned above require PowerShell.</span></span> <span data-ttu-id="716fd-135">Voordat u met deze instructies begint, zorg er dan voor dat u zich aanmeldt tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="716fd-135">Before you start with those instructions, make sure you log in tooyour Azure account.</span></span> <span data-ttu-id="716fd-136">Op het bureaublad een nieuw Azure PowerShell-venster openen en voer de volgende codefragmenten Hallo.</span><span class="sxs-lookup"><span data-stu-id="716fd-136">From your desktop, open a new Azure PowerShell window, and enter hello following snippets.</span></span> <span data-ttu-id="716fd-137">Wanneer de vraag toolog, zorg ervoor dat u zich aanmelden als een Hallo abonnement beheerders/eigenaars:</span><span class="sxs-lookup"><span data-stu-id="716fd-137">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a><span data-ttu-id="716fd-138">Voorbeeld gegevens toohello Azure Data Lake Store uploaden</span><span class="sxs-lookup"><span data-stu-id="716fd-138">Upload sample data toohello Azure Data Lake Store</span></span>
<span data-ttu-id="716fd-139">Hallo Resource Manager-sjabloon een nieuwe Data Lake Store-account maakt en koppelt dit aan Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="716fd-139">hello Resource Manager template creates a new Data Lake Store account and associates it with hello HDInsight cluster.</span></span> <span data-ttu-id="716fd-140">U moet nu uploaden sommige sample data toohello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="716fd-140">You must now upload some sample data toohello Data Lake Store.</span></span> <span data-ttu-id="716fd-141">U hebt deze gegevens in Hallo zelfstudie toorun taken van een HDInsight-cluster die toegang gegevens in Data Lake Store hello tot later nodig.</span><span class="sxs-lookup"><span data-stu-id="716fd-141">You'll need this data later in hello tutorial toorun jobs from an HDInsight cluster that access data in hello Data Lake Store.</span></span> <span data-ttu-id="716fd-142">Voor instructies over het tooupload van gegevens, Zie [uploaden van een bestand tooyour Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span><span class="sxs-lookup"><span data-stu-id="716fd-142">For instructions on how tooupload data, see [Upload a file tooyour Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="716fd-143">Als u een aantal gegevens voorbeeld tooupload zoekt, kunt u krijgen Hallo **Ambulance Data** map uit Hallo [Azure Data Lake Git-opslagplaats](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="716fd-143">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-hello-sample-data"></a><span data-ttu-id="716fd-144">Stel relevante ACL's op Hallo voorbeeldgegevens</span><span class="sxs-lookup"><span data-stu-id="716fd-144">Set relevant ACLs on hello sample data</span></span>
<span data-ttu-id="716fd-145">toomake ervoor Hallo voorbeeldgegevens die u uploadt, is toegankelijk vanuit Hallo HDInsight-cluster, moet u ervoor zorgen dat hello Azure AD-toepassing die de identiteit van de gebruikte tooestablish tussen Hallo HDInsight-cluster en Data Lake Store toegang toohello bestand/map waarin die u zich heeft tooaccess probeert.</span><span class="sxs-lookup"><span data-stu-id="716fd-145">toomake sure hello sample data you upload is accessible from hello HDInsight cluster, you must ensure that hello Azure AD application that is used tooestablish identity between hello HDInsight cluster and Data Lake Store has access toohello file/folder you are trying tooaccess.</span></span> <span data-ttu-id="716fd-146">toodo dit Hallo volgende stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="716fd-146">toodo this, perform hello following steps.</span></span>

1. <span data-ttu-id="716fd-147">Hallo-naam van hello Azure AD-toepassing die is gekoppeld aan de HDInsight-cluster en Hallo Data Lake Store vinden.</span><span class="sxs-lookup"><span data-stu-id="716fd-147">Find hello name of hello Azure AD application that is associated with HDInsight cluster and hello Data Lake Store.</span></span> <span data-ttu-id="716fd-148">Eenzijdige toolook voor de naam van de Hallo tooopen hello HDInsight-cluster blade dat u met Resource Manager-sjabloon Hallo gemaakt, klikt u op Hallo **Cluster AAD-identiteit** tabblad en zoekt u Hallo-waarde van **Service-Principal Weergavenaam**.</span><span class="sxs-lookup"><span data-stu-id="716fd-148">One way toolook for hello name is tooopen hello HDInsight cluster blade that you created using hello Resource Manager template, click hello **Cluster AAD Identity** tab, and look for hello value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="716fd-149">Bieden nu toegang toothis Azure AD-toepassing op Hallo bestand of de map die u wilt dat tooaccess van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="716fd-149">Now, provide access toothis Azure AD application on hello file/folder that you want tooaccess from hello HDInsight cluster.</span></span> <span data-ttu-id="716fd-150">Zie tooset Hallo rechts ACL's op Hallo bestand of de map in Data Lake Store [beveiligen van gegevens in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span><span class="sxs-lookup"><span data-stu-id="716fd-150">tooset hello right ACLs on hello file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="716fd-151">Testtaken uitvoeren op Hallo HDInsight-cluster toouse Hallo Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="716fd-151">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="716fd-152">Nadat u een HDInsight-cluster hebt geconfigureerd, kunt u uitvoeren testtaken op Hallo cluster tootest die Hallo HDInsight cluster toegang heeft tot Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="716fd-152">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="716fd-153">toodo dus voeren we een voorbeeld Hive-taak die u een tabel met voorbeeldgegevens Hallo maakt dat u hebt geüpload eerdere tooyour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="716fd-153">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="716fd-154">In deze sectie gaat u SSH in een cluster in HDInsight Linux en Voer Hallo een Hive-voorbeeldquery.</span><span class="sxs-lookup"><span data-stu-id="716fd-154">In this section you will SSH into an HDInsight Linux cluster and run hello a sample Hive query.</span></span> <span data-ttu-id="716fd-155">Als u een Windows-client gebruikt, wordt u aangeraden **PuTTY**, die kan worden gedownload vanaf [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="716fd-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="716fd-156">Zie voor meer informatie over het gebruik van PuTTY [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="716fd-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="716fd-157">Eenmaal zijn verbonden, start u Hallo CLI Hive via Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="716fd-157">Once connected, start hello Hive CLI by using hello following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="716fd-158">Gebruik Hallo CLI Hallo na toocreate instructies een nieuwe tabel met de naam te geven **voertuigen** met behulp van de voorbeeldgegevens Hallo in Hallo Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="716fd-158">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="716fd-159">U ziet een uitvoer vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="716fd-159">You should see an output similar toohello following:</span></span>

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="716fd-160">Toegang tot Data Lake Store met HDFS-opdrachten</span><span class="sxs-lookup"><span data-stu-id="716fd-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="716fd-161">Wanneer u Hallo HDInsight cluster toouse Data Lake Store hebt geconfigureerd, kunt u Hallo HDFS shell-opdrachten tooaccess Hallo store.</span><span class="sxs-lookup"><span data-stu-id="716fd-161">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="716fd-162">In deze sectie gaat u SSH in een cluster in HDInsight Linux en Voer Hallo HDFS-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="716fd-162">In this section you will SSH into an HDInsight Linux cluster and run hello HDFS commands.</span></span> <span data-ttu-id="716fd-163">Als u een Windows-client gebruikt, wordt u aangeraden **PuTTY**, die kan worden gedownload vanaf [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="716fd-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="716fd-164">Zie voor meer informatie over het gebruik van PuTTY [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="716fd-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="716fd-165">Eenmaal zijn verbonden, gebruik Hallo HDFS bestandssysteem toolist Hallo opdrachtbestanden in Hallo Data Lake Store te volgen.</span><span class="sxs-lookup"><span data-stu-id="716fd-165">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="716fd-166">Hallo-bestand dat u hebt geüpload eerdere toohello Data Lake Store moet u deze lijst.</span><span class="sxs-lookup"><span data-stu-id="716fd-166">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="716fd-167">U kunt ook Hallo `hdfs dfs -put` opdracht tooupload sommige bestanden toohello Data Lake Store en gebruik vervolgens `hdfs dfs -ls` tooverify of Hallo bestanden geüpload.</span><span class="sxs-lookup"><span data-stu-id="716fd-167">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="716fd-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="716fd-168">Next steps</span></span>
* [<span data-ttu-id="716fd-169">Gegevens kopiëren van Azure Storage Blobs tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="716fd-169">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)

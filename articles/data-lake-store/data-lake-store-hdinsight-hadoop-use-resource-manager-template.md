---
title: Azure-sjablonen gebruiken voor het maken van HDInsight en Data Lake Store | Microsoft Docs
description: Gebruik van Azure Resource Manager-sjablonen maken en gebruiken van HDInsight-clusters met Azure Data Lake Store
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
ms.openlocfilehash: 6f43423096f0e74f41afea275e4ec9801dc2cea5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="1f5c7-103">Een HDInsight-cluster maken met Data Lake Store met Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="1f5c7-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f5c7-104">Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="1f5c7-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="1f5c7-105">Met behulp van PowerShell (voor opslag van de standaard)</span><span class="sxs-lookup"><span data-stu-id="1f5c7-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="1f5c7-106">Met behulp van PowerShell (voor extra opslagruimte)</span><span class="sxs-lookup"><span data-stu-id="1f5c7-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="1f5c7-107">Resource Manager gebruiken</span><span class="sxs-lookup"><span data-stu-id="1f5c7-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="1f5c7-108">Informatie over het gebruik van Azure PowerShell voor het configureren van een HDInsight-cluster met Azure Data Lake Store **als extra opslagruimte**.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-108">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="1f5c7-109">Voor ondersteunde clustertypen, worden Data Lake Store gebruikt als een standaard-opslag- of aanvullende storage-account.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="1f5c7-110">Wanneer Data Lake Store als extra opslagruimte wordt gebruikt, is het standaardopslagaccount voor de clusters nog steeds Azure Storage-Blobs (WASB) en de cluster-gerelateerde bestanden (zoals Logboeken, enz.) worden nog steeds naar de standaard-opslag geschreven terwijl de gegevens die u wilt laten verwerken, kunnen worden opgeslagen in een Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-110">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="1f5c7-111">Met behulp van Data Lake Store als extra storage-account heeft geen gevolgen voor prestaties of de mogelijkheid om te lezen/schrijven naar de opslag van het cluster.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-111">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="1f5c7-112">Met behulp van Data Lake Store voor opslag van HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="1f5c7-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="1f5c7-113">Hier volgen enkele belangrijke overwegingen voor het gebruik van HDInsight met Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="1f5c7-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="1f5c7-114">De optie voor het maken van HDInsight-clusters met toegang tot Data Lake Store als standaard opslag beschikbaar voor HDInsight versie 3.5 en 3.6.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-114">Option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="1f5c7-115">De optie voor het maken van HDInsight-clusters met toegang tot Data Lake Store als extra opslag beschikbaar voor HDInsight versie 3.2, 3.4 3.5 en 3.6.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-115">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="1f5c7-116">In dit artikel inrichten we een Hadoop-cluster met Data Lake Store als extra opslagruimte.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="1f5c7-117">Zie voor instructies over het maken van een Hadoop-cluster met Data Lake Store als standaard opslag [een HDInsight-cluster maken met Data Lake Store met Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1f5c7-117">For instructions on how to create a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f5c7-118">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1f5c7-118">Prerequisites</span></span>
<span data-ttu-id="1f5c7-119">Voordat u met deze zelfstudie begint, moet u het volgende hebben of hebben gedaan:</span><span class="sxs-lookup"><span data-stu-id="1f5c7-119">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="1f5c7-120">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-120">**An Azure subscription**.</span></span> <span data-ttu-id="1f5c7-121">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f5c7-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1f5c7-122">**Azure PowerShell 1.0 of hoger**.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="1f5c7-123">Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1f5c7-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="1f5c7-124">**Azure Active Directory Service-Principal**.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="1f5c7-125">De stappen in deze zelfstudie bevatten instructies voor het maken van een service-principal in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-125">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="1f5c7-126">U moet echter een Azure AD-beheerder om te kunnen maken van een service-principal.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-126">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="1f5c7-127">Als u een Azure AD-beheerder bent, kunt u deze vereiste overslaan en doorgaan met de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="1f5c7-128">**Als u niet een Azure AD-beheerder**, u kan niet worden de stappen die zijn vereist voor het maken van een service-principal uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-128">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="1f5c7-129">In dat geval moet uw Azure AD-beheerder eerst een service-principal maken voordat u een HDInsight-cluster met Data Lake Store maken kunt.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="1f5c7-130">Ook de service-principal moet worden gemaakt met een certificaat, zoals beschreven op [een service-principal maken met certificaat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="1f5c7-130">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="1f5c7-131">Een HDInsight-cluster maken met Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1f5c7-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="1f5c7-132">De Resource Manager-sjabloon en de vereisten voor het gebruik van de sjabloon zijn beschikbaar op GitHub op [een HDInsight Linux-cluster met nieuwe Data Lake Store implementeren](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="1f5c7-132">The Resource Manager template, and the prerequisites for using the template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="1f5c7-133">Volg de instructies op deze koppeling te maken van een HDInsight-cluster met Azure Data Lake Store als extra opslagruimte.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-133">Follow the instructions provided at this link to create an HDInsight cluster with Azure Data Lake Store as the additional storage.</span></span>

<span data-ttu-id="1f5c7-134">De instructies in de bovenstaande koppeling vereisen PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-134">The instructions at the link mentioned above require PowerShell.</span></span> <span data-ttu-id="1f5c7-135">Zorg voordat u met deze instructies begint, dat u aanmelden bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-135">Before you start with those instructions, make sure you log in to your Azure account.</span></span> <span data-ttu-id="1f5c7-136">Een nieuw Azure PowerShell-venster openen vanaf het bureaublad en voer de volgende codefragmenten.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-136">From your desktop, open a new Azure PowerShell window, and enter the following snippets.</span></span> <span data-ttu-id="1f5c7-137">Wanneer u wordt gevraagd om u aan te melden, zorg dan dat u zich aanmeldt als een van de beheerders/eigenaars van het abonnement:</span><span class="sxs-lookup"><span data-stu-id="1f5c7-137">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

```
# Log in to your Azure account
Login-AzureRmAccount

# List all the subscriptions associated to your account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-to-the-azure-data-lake-store"></a><span data-ttu-id="1f5c7-138">Voorbeeldgegevens uploadt naar de Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1f5c7-138">Upload sample data to the Azure Data Lake Store</span></span>
<span data-ttu-id="1f5c7-139">De Resource Manager-sjabloon een nieuwe Data Lake Store-account maakt en koppelt u deze aan het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-139">The Resource Manager template creates a new Data Lake Store account and associates it with the HDInsight cluster.</span></span> <span data-ttu-id="1f5c7-140">Nu moet u voorbeeldgegevens uploadt naar Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-140">You must now upload some sample data to the Data Lake Store.</span></span> <span data-ttu-id="1f5c7-141">U moet deze gegevens verderop in de zelfstudie taken uitvoeren vanuit een HDInsight-cluster die toegang tot gegevens in de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-141">You'll need this data later in the tutorial to run jobs from an HDInsight cluster that access data in the Data Lake Store.</span></span> <span data-ttu-id="1f5c7-142">Zie voor instructies over het uploaden van gegevens [een bestand uploaden naar uw Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span><span class="sxs-lookup"><span data-stu-id="1f5c7-142">For instructions on how to upload data, see [Upload a file to your Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="1f5c7-143">Als u nog geen voorbeeldgegevens hebt om te uploaden, kunt u de map **Ambulance Data** uit de [Azure Data Lake Git-opslagplaats](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-143">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-the-sample-data"></a><span data-ttu-id="1f5c7-144">Stel relevante ACL's op de voorbeeldgegevens</span><span class="sxs-lookup"><span data-stu-id="1f5c7-144">Set relevant ACLs on the sample data</span></span>
<span data-ttu-id="1f5c7-145">Om te zorgen dat de voorbeeldgegevens die u uploadt, is toegankelijk vanaf het HDInsight-cluster, moet u ervoor zorgen dat de Azure AD-toepassing die wordt gebruikt voor het tot stand brengen identiteit tussen de HDInsight-cluster en de Data Lake Store toegang heeft tot het bestand of de map die u probeert te openen.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-145">To make sure the sample data you upload is accessible from the HDInsight cluster, you must ensure that the Azure AD application that is used to establish identity between the HDInsight cluster and Data Lake Store has access to the file/folder you are trying to access.</span></span> <span data-ttu-id="1f5c7-146">U doet dit door de volgende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-146">To do this, perform the following steps.</span></span>

1. <span data-ttu-id="1f5c7-147">Zoek de naam van de Azure AD-toepassing die is gekoppeld aan het HDInsight-cluster en de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-147">Find the name of the Azure AD application that is associated with HDInsight cluster and the Data Lake Store.</span></span> <span data-ttu-id="1f5c7-148">Een manier om te zoeken naar de naam is de HDInsight-cluster-blade die u hebt gemaakt met behulp van de Resource Manager-sjabloon te openen, klikt u op de **Cluster AAD-identiteit** tabblad en zoekt u de waarde van **weergavenaam van Service-Principal**.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-148">One way to look for the name is to open the HDInsight cluster blade that you created using the Resource Manager template, click the **Cluster AAD Identity** tab, and look for the value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="1f5c7-149">Nu bieden toegang tot deze Azure AD-toepassing op het bestand of de map die u wilt openen vanuit het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-149">Now, provide access to this Azure AD application on the file/folder that you want to access from the HDInsight cluster.</span></span> <span data-ttu-id="1f5c7-150">Zie het instellen van de juiste ACL's op het bestand/map in Data Lake Store [beveiligen van gegevens in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span><span class="sxs-lookup"><span data-stu-id="1f5c7-150">To set the right ACLs on the file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="1f5c7-151">Testtaken uitvoeren op het HDInsight-cluster te gebruiken van de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1f5c7-151">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="1f5c7-152">Nadat u een HDInsight-cluster hebt geconfigureerd, kunt u testtaken uitvoeren op het cluster om te testen of de HDInsight-cluster toegang Data Lake Store tot.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-152">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="1f5c7-153">Om dit te doen, voeren we een voorbeeld Hive-taak die u maakt een tabel met de voorbeeldgegevens die u eerder hebt geüpload naar uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-153">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="1f5c7-154">In deze sectie wordt u SSH in een cluster in HDInsight Linux en voer de een Hive-voorbeeldquery.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-154">In this section you will SSH into an HDInsight Linux cluster and run the a sample Hive query.</span></span> <span data-ttu-id="1f5c7-155">Als u een Windows-client gebruikt, wordt u aangeraden **PuTTY**, die kan worden gedownload vanaf [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="1f5c7-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="1f5c7-156">Zie voor meer informatie over het gebruik van PuTTY [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="1f5c7-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="1f5c7-157">Eenmaal zijn verbonden, start u de CLI Hive met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="1f5c7-157">Once connected, start the Hive CLI by using the following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="1f5c7-158">De volgende instructies om een nieuwe tabel met de naam te maken met behulp van de CLI Voer **voertuigen** met behulp van de voorbeeldgegevens in de Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="1f5c7-158">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="1f5c7-159">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="1f5c7-159">You should see an output similar to the following:</span></span>

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


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="1f5c7-160">Toegang tot Data Lake Store met HDFS-opdrachten</span><span class="sxs-lookup"><span data-stu-id="1f5c7-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="1f5c7-161">Wanneer u het HDInsight-cluster voor het gebruik van Data Lake Store hebt geconfigureerd, kunt u de HDFS-shell-opdrachten voor toegang tot de store.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-161">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="1f5c7-162">In deze sectie wordt u SSH in een HDInsight Linux-cluster en voer de HDFS-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-162">In this section you will SSH into an HDInsight Linux cluster and run the HDFS commands.</span></span> <span data-ttu-id="1f5c7-163">Als u een Windows-client gebruikt, wordt u aangeraden **PuTTY**, die kan worden gedownload vanaf [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="1f5c7-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="1f5c7-164">Zie voor meer informatie over het gebruik van PuTTY [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="1f5c7-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="1f5c7-165">Eenmaal zijn verbonden, gebruikt u de volgende opdracht uit HDFS-bestandssysteem voor het weergeven van de bestanden in de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-165">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="1f5c7-166">Dit moet het bestand dat u eerder hebt geüpload naar de Data Lake Store weergeven.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-166">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="1f5c7-167">U kunt ook de `hdfs dfs -put` opdracht voor sommige bestanden uploaden naar Data Lake Store en vervolgens gebruik `hdfs dfs -ls` om te controleren of de bestanden zijn geüpload.</span><span class="sxs-lookup"><span data-stu-id="1f5c7-167">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1f5c7-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1f5c7-168">Next steps</span></span>
* [<span data-ttu-id="1f5c7-169">Gegevens kopiëren van Azure Storage-Blobs naar Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1f5c7-169">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)

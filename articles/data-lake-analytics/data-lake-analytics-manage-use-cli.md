---
title: aaaManage Azure Data Lake Analytics met Azure-opdrachtregelinterface | Microsoft Docs
description: Meer informatie over hoe toomanage Data Lake Analytics-accounts, gegevensbronnen, taken en gebruikers met Azure CLI
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="112f9-103">Azure Data Lake Analytics beheren met Azure-opdrachtregelinterface (CLI)</span><span class="sxs-lookup"><span data-stu-id="112f9-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="112f9-104">Meer informatie over hoe Hallo toomanage Azure Data Lake Analytics-accounts, gegevensbronnen, gebruikers en taken met behulp van Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="112f9-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure CLI.</span></span> <span data-ttu-id="112f9-105">toosee management onderwerpen met een ander hulpprogramma, klikt u op Hallo tabblad select bovenaan.</span><span class="sxs-lookup"><span data-stu-id="112f9-105">toosee management topics using other tools, click hello tab select above.</span></span>


<span data-ttu-id="112f9-106">**Vereisten**</span><span class="sxs-lookup"><span data-stu-id="112f9-106">**Prerequisites**</span></span>

<span data-ttu-id="112f9-107">Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="112f9-107">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="112f9-108">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="112f9-108">**An Azure subscription**.</span></span> <span data-ttu-id="112f9-109">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="112f9-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="112f9-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="112f9-110">**Azure CLI**.</span></span> <span data-ttu-id="112f9-111">Zie [Azure CLI installeren en configureren](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="112f9-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="112f9-112">Download en installeer Hallo **voorlopige versie** [Azure CLI-hulpprogramma's](https://github.com/MicrosoftBigData/AzureDataLake/releases) in volgorde toocomplete deze demo.</span><span class="sxs-lookup"><span data-stu-id="112f9-112">Download and install hello **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order toocomplete this demo.</span></span>
* <span data-ttu-id="112f9-113">**Verificatie**met Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="112f9-113">**Authentication**, using hello following command:</span></span>
  
        azure login
    <span data-ttu-id="112f9-114">Zie voor meer informatie over verificatie met een werk- of schoolaccount [tooan Azure-abonnement verbinden van hello Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="112f9-114">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="112f9-115">**Modus van Azure Resource Manager toohello switch**met Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="112f9-115">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="112f9-116">**toolist hello Data Lake Store- en Data Lake Analytics-opdrachten:**</span><span class="sxs-lookup"><span data-stu-id="112f9-116">**toolist hello Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="112f9-117">Accounts beheren</span><span class="sxs-lookup"><span data-stu-id="112f9-117">Manage accounts</span></span>
<span data-ttu-id="112f9-118">Voordat u een Data Lake Analytics-taken uitvoert, moet u een Data Lake Analytics-account hebben.</span><span class="sxs-lookup"><span data-stu-id="112f9-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="112f9-119">In tegenstelling tot Azure HDInsight betaalt niet u voor een Analytics-account wanneer deze een taak niet wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="112f9-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="112f9-120">U betaalt alleen voor Hallo keer wanneer een taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="112f9-120">You only pay for hello time when it is running a job.</span></span>  <span data-ttu-id="112f9-121">Zie voor meer informatie [overzicht van Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="112f9-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="112f9-122">Accounts maken</span><span class="sxs-lookup"><span data-stu-id="112f9-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="112f9-123">Bijwerken van accounts</span><span class="sxs-lookup"><span data-stu-id="112f9-123">Update accounts</span></span>
<span data-ttu-id="112f9-124">Hallo volgende opdracht werkt Hallo eigenschappen van een bestaande Data Lake Analytics-Account</span><span class="sxs-lookup"><span data-stu-id="112f9-124">hello following command updates hello properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="112f9-125">Lijst van accounts</span><span class="sxs-lookup"><span data-stu-id="112f9-125">List accounts</span></span>
<span data-ttu-id="112f9-126">Lijst met Data Lake Analytics-accounts</span><span class="sxs-lookup"><span data-stu-id="112f9-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="112f9-127">Lijst met Data Lake Analytics-accounts binnen een specifieke resourcegroep</span><span class="sxs-lookup"><span data-stu-id="112f9-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="112f9-128">Details van een specifieke Data Lake Analytics-account ophalen</span><span class="sxs-lookup"><span data-stu-id="112f9-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="112f9-129">Data Lake Analytics-accounts te verwijderen</span><span class="sxs-lookup"><span data-stu-id="112f9-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="112f9-130">Account gegevensbronnen beheren</span><span class="sxs-lookup"><span data-stu-id="112f9-130">Manage account data sources</span></span>
<span data-ttu-id="112f9-131">Data Lake Analytics ondersteunt momenteel Hallo gegevensbronnen te volgen:</span><span class="sxs-lookup"><span data-stu-id="112f9-131">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="112f9-132">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="112f9-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="112f9-133">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="112f9-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="112f9-134">Wanneer u een Analytics-account maakt, moet u een Azure Data Lake Storage-account toobe Hallo storage-standaardaccount toewijzen.</span><span class="sxs-lookup"><span data-stu-id="112f9-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account toobe hello default storage account.</span></span> <span data-ttu-id="112f9-135">Hallo storage-standaardaccount ADL wordt gebruikt toostore taak metagegevens en taak controlelogboeken.</span><span class="sxs-lookup"><span data-stu-id="112f9-135">hello default ADL storage account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="112f9-136">Nadat u een Analytics-account hebt gemaakt, kunt u extra Data Lake Storage-accounts en/of Azure Storage-account toevoegen.</span><span class="sxs-lookup"><span data-stu-id="112f9-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-hello-default-adl-storage-account"></a><span data-ttu-id="112f9-137">Hallo ADL standaardopslagaccount vinden</span><span class="sxs-lookup"><span data-stu-id="112f9-137">Find hello default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="112f9-138">Hallo-waarde wordt vermeld onder eigenschappen: datalakeStoreAccount:name.</span><span class="sxs-lookup"><span data-stu-id="112f9-138">hello value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="112f9-139">Extra Azure Blob storage-accounts toevoegen</span><span class="sxs-lookup"><span data-stu-id="112f9-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="112f9-140">Alleen Blob storage korte namen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="112f9-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="112f9-141">Gebruik geen FQDN-naam, bijvoorbeeld 'myblob.blob.core.windows.net'.</span><span class="sxs-lookup"><span data-stu-id="112f9-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="112f9-142">Extra Data Lake Store-accounts toevoegen</span><span class="sxs-lookup"><span data-stu-id="112f9-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="112f9-143">[-d] is een optionele schakeloptie tooindicate of Hallo Data Lake wordt toegevoegd Hallo Data Lake-standaardaccount.</span><span class="sxs-lookup"><span data-stu-id="112f9-143">[-d] is an optional switch tooindicate whether hello Data Lake being added is hello default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="112f9-144">Bestaande gegevensbron bijwerken</span><span class="sxs-lookup"><span data-stu-id="112f9-144">Update existing data source</span></span>
<span data-ttu-id="112f9-145">een bestaande Data Lake Store-account toobe Hallo standaardwaarde tooset:</span><span class="sxs-lookup"><span data-stu-id="112f9-145">tooset an existing Data Lake Store account toobe hello default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="112f9-146">een bestaande Blob storage-accountsleutel tooupdate:</span><span class="sxs-lookup"><span data-stu-id="112f9-146">tooupdate an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="112f9-147">Lijst van gegevensbronnen:</span><span class="sxs-lookup"><span data-stu-id="112f9-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Gegevensbron voor Data Lake Analytics-lijst](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="112f9-149">Gegevensbronnen verwijderen:</span><span class="sxs-lookup"><span data-stu-id="112f9-149">Delete data sources:</span></span>
<span data-ttu-id="112f9-150">toodelete een Data Lake Store-account:</span><span class="sxs-lookup"><span data-stu-id="112f9-150">toodelete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="112f9-151">toodelete een Blob storage-account:</span><span class="sxs-lookup"><span data-stu-id="112f9-151">toodelete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="112f9-152">Taken beheren</span><span class="sxs-lookup"><span data-stu-id="112f9-152">Manage jobs</span></span>
<span data-ttu-id="112f9-153">U moet een Data Lake Analytics-account hebben voordat u een taak kunt maken.</span><span class="sxs-lookup"><span data-stu-id="112f9-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="112f9-154">Zie voor meer informatie [beheren Data Lake Analytics-accounts](#manage-accounts).</span><span class="sxs-lookup"><span data-stu-id="112f9-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="112f9-155">Taken weergeven</span><span class="sxs-lookup"><span data-stu-id="112f9-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Gegevensbron voor Data Lake Analytics-lijst](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="112f9-157">Taakdetails van de ophalen</span><span class="sxs-lookup"><span data-stu-id="112f9-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="112f9-158">Verzenden van taken</span><span class="sxs-lookup"><span data-stu-id="112f9-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="112f9-159">Hallo standaardprioriteit van een taak is 1000 en Hallo standaard mate van parallelle uitvoering voor een taak is 1.</span><span class="sxs-lookup"><span data-stu-id="112f9-159">hello default priority of a job is 1000, and hello default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="112f9-160">Taken annuleren</span><span class="sxs-lookup"><span data-stu-id="112f9-160">Cancel jobs</span></span>
<span data-ttu-id="112f9-161">Hallo lijst opdracht toofind Hallo taak-id gebruiken en gebruik vervolgens annuleren toocancel Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="112f9-161">Use hello list command toofind hello job id, and then use cancel toocancel hello job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="112f9-162">Catalogus beheren</span><span class="sxs-lookup"><span data-stu-id="112f9-162">Manage catalog</span></span>
<span data-ttu-id="112f9-163">Hallo U-SQL-catalogus is toostructure gebruikte gegevens en code zodat ze kunnen worden gedeeld door de U-SQL-scripts.</span><span class="sxs-lookup"><span data-stu-id="112f9-163">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="112f9-164">Hallo catalogus kunt Hallo hoogste prestaties mogelijk met gegevens in Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="112f9-164">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="112f9-165">Zie [U-SQL-catalogus gebruiken](data-lake-analytics-use-u-sql-catalog.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="112f9-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="112f9-166">Lijst met catalogusitems</span><span class="sxs-lookup"><span data-stu-id="112f9-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="112f9-167">Hallo-typen zijn database, schema, assembly, externe gegevensbron, tabel, functie met tabelwaarden of tabelstatistieken.</span><span class="sxs-lookup"><span data-stu-id="112f9-167">hello types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="112f9-168">ARM-groepen gebruiken</span><span class="sxs-lookup"><span data-stu-id="112f9-168">Use ARM groups</span></span>
<span data-ttu-id="112f9-169">Toepassingen bestaan in het algemeen uit meerdere onderdelen, bijvoorbeeld een web-app, database, databaseserver, opslag en services van derden.</span><span class="sxs-lookup"><span data-stu-id="112f9-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="112f9-170">Azure Resource Manager (ARM) kunt u toowork met Hallo resources in uw toepassing als een groep waarnaar wordt verwezen tooas een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="112f9-170">Azure Resource Manager (ARM) enables you toowork with hello resources in your application as a group, referred tooas an Azure Resource Group.</span></span> <span data-ttu-id="112f9-171">U kunt implementeren, bijwerken, bewaken of verwijder alle Hallo resources voor uw toepassing in een enkele, gecoördineerde bewerking.</span><span class="sxs-lookup"><span data-stu-id="112f9-171">You can deploy, update, monitor or delete all of hello resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="112f9-172">Voor implementatie gebruikt u een sjabloon. Deze sjabloon kan voor verschillende omgevingen worden gebruikt, zoals testen, faseren en productie.</span><span class="sxs-lookup"><span data-stu-id="112f9-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="112f9-173">U kunt facturering voor uw organisatie verduidelijken door Hallo Samengevoegde kosten voor de hele groep Hallo weer te geven.</span><span class="sxs-lookup"><span data-stu-id="112f9-173">You can clarify billing for your organization by viewing hello rolled-up costs for hello entire group.</span></span> <span data-ttu-id="112f9-174">Zie [Overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="112f9-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="112f9-175">Een Data Lake Analytics-service kan Hallo volgende onderdelen bevatten:</span><span class="sxs-lookup"><span data-stu-id="112f9-175">A Data Lake Analytics service can include hello following components:</span></span>

* <span data-ttu-id="112f9-176">Azure Data Lake Analytics-account</span><span class="sxs-lookup"><span data-stu-id="112f9-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="112f9-177">Vereiste standaard Azure Data Lake Storage-account</span><span class="sxs-lookup"><span data-stu-id="112f9-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="112f9-178">Aanvullende Azure Data Lake Storage-accounts</span><span class="sxs-lookup"><span data-stu-id="112f9-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="112f9-179">Extra Azure Storage-accounts</span><span class="sxs-lookup"><span data-stu-id="112f9-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="112f9-180">U kunt al deze onderdelen onder één ARM groep toomake maken ze gemakkelijker toomanage.</span><span class="sxs-lookup"><span data-stu-id="112f9-180">You can create all these components under one ARM group toomake them easier toomanage.</span></span>

![Azure Data Lake Analytics-account en opslag](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="112f9-182">Een Data Lake Analytics-account en de afhankelijke opslagaccounts Hallo moeten worden geplaatst in Hallo dezelfde Azure-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="112f9-182">A Data Lake Analytics account and hello dependent storage accounts must be placed in hello same Azure data center.</span></span>
<span data-ttu-id="112f9-183">Hallo ARM groep kan echter in een ander datacenter worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="112f9-183">hello ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="112f9-184">Zie ook</span><span class="sxs-lookup"><span data-stu-id="112f9-184">See also</span></span>
* [<span data-ttu-id="112f9-185">Overzicht van Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="112f9-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="112f9-186">Aan de slag met Data Lake Analytics met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="112f9-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="112f9-187">Azure Data Lake Analytics beheren met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="112f9-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="112f9-188">Azure Data Lake Analytics-taken bewaken en problemen oplossen met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="112f9-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)


---
title: aaaGet de slag met Azure Data Lake Analytics met Azure CLI 2.0 | Microsoft Docs
description: 'Informatie over hoe toouse hello Azure Command-line Interface 2.0 toocreate een Data Lake Analytics-account maken van een Data Lake Analytics-taak met U-SQL, en het Hallo-taak verzenden. '
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a><span data-ttu-id="b4293-103">Aan de slag met Azure Data Lake Analytics met Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b4293-103">Get started with Azure Data Lake Analytics using Azure CLI 2.0</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="b4293-104">In deze zelfstudie ontwikkelt u een taak voor het lezen van een TSV-bestand (door tabs gescheiden waarden) en het converteren ervan naar een CSV-bestand (door komma's gescheiden waarden).</span><span class="sxs-lookup"><span data-stu-id="b4293-104">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated values (CSV) file.</span></span> <span data-ttu-id="b4293-105">toogo via Hallo dezelfde zelfstudie met behulp van andere ondersteunde hulpprogramma's, gebruik Hallo vervolgkeuzelijst bovenaan Hallo van deze sectie.</span><span class="sxs-lookup"><span data-stu-id="b4293-105">toogo through hello same tutorial using other supported tools, use hello dropdown list on hello top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4293-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b4293-106">Prerequisites</span></span>
<span data-ttu-id="b4293-107">Voordat u deze zelfstudie begint, moet u de volgende items Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="b4293-107">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="b4293-108">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="b4293-108">**An Azure subscription**.</span></span> <span data-ttu-id="b4293-109">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b4293-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b4293-110">**Azure CLI 2.0**.</span><span class="sxs-lookup"><span data-stu-id="b4293-110">**Azure CLI 2.0**.</span></span> <span data-ttu-id="b4293-111">Zie [Azure CLI installeren en configureren](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b4293-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="b4293-112">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="b4293-112">Log in tooAzure</span></span>

<span data-ttu-id="b4293-113">toolog in tooyour Azure-abonnement:</span><span class="sxs-lookup"><span data-stu-id="b4293-113">toolog in tooyour Azure subscription:</span></span>

```
azurecli
az login
```

<span data-ttu-id="b4293-114">U aangevraagde toobrowse tooa URL zijn en voer een verificatiecode op te geven.</span><span class="sxs-lookup"><span data-stu-id="b4293-114">You are requested toobrowse tooa URL, and enter an authentication code.</span></span>  <span data-ttu-id="b4293-115">En volg Hallo instructies tooenter uw referenties.</span><span class="sxs-lookup"><span data-stu-id="b4293-115">And then follow hello instructions tooenter your credentials.</span></span>

<span data-ttu-id="b4293-116">Zodra u zich hebt aangemeld, worden Hallo aanmelding opdracht uw abonnementen.</span><span class="sxs-lookup"><span data-stu-id="b4293-116">Once you have logged in, hello login command lists your subscriptions.</span></span>

<span data-ttu-id="b4293-117">een specifiek abonnement toouse:</span><span class="sxs-lookup"><span data-stu-id="b4293-117">toouse a specific subscription:</span></span>

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="b4293-118">Een Data Lake Analytics-account maken</span><span class="sxs-lookup"><span data-stu-id="b4293-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="b4293-119">U hebt een Data Lake Analytics-account nodig voordat u taken kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b4293-119">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="b4293-120">toocreate een Data Lake Analytics-account, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="b4293-120">toocreate a Data Lake Analytics account, you must specify hello following items:</span></span>

* <span data-ttu-id="b4293-121">**Azure-resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="b4293-121">**Azure Resource Group**.</span></span> <span data-ttu-id="b4293-122">Er moet een Data Lake Analytics-account zijn gemaakt binnen een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="b4293-122">A Data Lake Analytics account must be created within an Azure Resource group.</span></span> <span data-ttu-id="b4293-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) kunt u toowork met Hallo resources in uw toepassing als groep.</span><span class="sxs-lookup"><span data-stu-id="b4293-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you toowork with hello resources in your application as a group.</span></span> <span data-ttu-id="b4293-124">U kunt implementeren, bijwerken of verwijderen alle Hallo resources voor uw toepassing in een enkele, gecoördineerde bewerking.</span><span class="sxs-lookup"><span data-stu-id="b4293-124">You can deploy, update, or delete all of hello resources for your application in a single, coordinated operation.</span></span>  

<span data-ttu-id="b4293-125">toolist hello bestaande resourcegroepen in uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="b4293-125">toolist hello existing resource groups under your subscription:</span></span>

```
az group list
```

<span data-ttu-id="b4293-126">een nieuwe resourcegroep toocreate:</span><span class="sxs-lookup"><span data-stu-id="b4293-126">toocreate a new resource group:</span></span>

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* <span data-ttu-id="b4293-127">**Naam van Data Lake Analytics-account**.</span><span class="sxs-lookup"><span data-stu-id="b4293-127">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="b4293-128">Elk Data Lake Analytics-account heeft een naam.</span><span class="sxs-lookup"><span data-stu-id="b4293-128">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="b4293-129">**Locatie**.</span><span class="sxs-lookup"><span data-stu-id="b4293-129">**Location**.</span></span> <span data-ttu-id="b4293-130">Gebruik een van de hello Azure-datacenters die ondersteuning biedt voor Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="b4293-130">Use one of hello Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="b4293-131">**Data Lake Store-standaardaccount**: elk Data Lake Store Analytics-account heeft een Data Lake Store-standaardaccount.</span><span class="sxs-lookup"><span data-stu-id="b4293-131">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>

<span data-ttu-id="b4293-132">toolist hello bestaande Data Lake Store-account:</span><span class="sxs-lookup"><span data-stu-id="b4293-132">toolist hello existing Data Lake Store account:</span></span>

```
az dls account list
```

<span data-ttu-id="b4293-133">toocreate een nieuw Data Lake Store-account:</span><span class="sxs-lookup"><span data-stu-id="b4293-133">toocreate a new Data Lake Store account:</span></span>

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

<span data-ttu-id="b4293-134">Hallo na syntaxis toocreate een Data Lake Analytics-account gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b4293-134">Use hello following syntax toocreate a Data Lake Analytics account:</span></span>

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="b4293-135">U kunt na het maken van een account gebruiken Hallo opdrachten toolist Hallo accounts te volgen en accountdetails weergeven:</span><span class="sxs-lookup"><span data-stu-id="b4293-135">After creating an account, you can use hello following commands toolist hello accounts and show account details:</span></span>

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a><span data-ttu-id="b4293-136">Uploaden van gegevens tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="b4293-136">Upload data tooData Lake Store</span></span>
<span data-ttu-id="b4293-137">In deze zelfstudie verwerkt u een aantal zoeklogboeken.</span><span class="sxs-lookup"><span data-stu-id="b4293-137">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="b4293-138">Hallo-zoeklogboek kan worden opgeslagen in Data Lake store of Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="b4293-138">hello search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="b4293-139">Hello Azure-portal biedt een gebruikersinterface voor het kopiëren van sommige sample data bestanden toohello Data Lake Store-standaardaccount, waaronder een zoeklogboekbestand.</span><span class="sxs-lookup"><span data-stu-id="b4293-139">hello Azure portal provides a user interface for copying some sample data files toohello default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="b4293-140">Zie [brongegevens voorbereiden](data-lake-analytics-get-started-portal.md) tooupload Hallo gegevens toohello Data Lake Store-standaardaccount.</span><span class="sxs-lookup"><span data-stu-id="b4293-140">See [Prepare source data](data-lake-analytics-get-started-portal.md) tooupload hello data toohello default Data Lake Store account.</span></span>

<span data-ttu-id="b4293-141">tooupload bestanden met CLI 2.0, gebruik Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="b4293-141">tooupload files using CLI 2.0, use hello following commands:</span></span>

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="b4293-142">Data Lake Analytics heeft ook toegang tot Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="b4293-142">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="b4293-143">Zie voor het uploaden van Blob-opslag voor gegevens tooAzure [Using hello Azure CLI met Azure Storage](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b4293-143">For uploading data tooAzure Blob storage, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="b4293-144">Data Lake Analytics-taken verzenden</span><span class="sxs-lookup"><span data-stu-id="b4293-144">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="b4293-145">Hallo Data Lake Analytics-taken worden geschreven in Hallo U-SQL-taal.</span><span class="sxs-lookup"><span data-stu-id="b4293-145">hello Data Lake Analytics jobs are written in hello U-SQL language.</span></span> <span data-ttu-id="b4293-146">toolearn meer informatie over U-SQL, Zie [aan de slag met U-SQL-taal](data-lake-analytics-u-sql-get-started.md) en [eence van U-SQL-taal](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="b4293-146">toolearn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="b4293-147">**een Data Lake Analytics-taakscript toocreate**</span><span class="sxs-lookup"><span data-stu-id="b4293-147">**toocreate a Data Lake Analytics job script**</span></span>

<span data-ttu-id="b4293-148">Maak een tekstbestand met het volgende U-SQL-script en sla van Hallo tekst bestand tooyour werkstation:</span><span class="sxs-lookup"><span data-stu-id="b4293-148">Create a text file with following U-SQL script, and save hello text file tooyour workstation:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="b4293-149">Dit U-SQL-script leest Hallo brongegevensbestand met **Extractors.Tsv()**, en maakt vervolgens een CSV-bestand met **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="b4293-149">This U-SQL script reads hello source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

<span data-ttu-id="b4293-150">Het Wijzig Hallo twee paden niet, tenzij u Hallo bronbestand naar een andere locatie kopiëren.</span><span class="sxs-lookup"><span data-stu-id="b4293-150">Don't modify hello two paths unless you copy hello source file into a different location.</span></span>  <span data-ttu-id="b4293-151">Data Lake Analytics maakt de uitvoermap Hallo als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="b4293-151">Data Lake Analytics creates hello output folder if it doesn't exist.</span></span>

<span data-ttu-id="b4293-152">Het is eenvoudiger toouse relatieve paden voor bestanden die zijn opgeslagen in Data Lake Store-standaardaccounts.</span><span class="sxs-lookup"><span data-stu-id="b4293-152">It is simpler toouse relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="b4293-153">Maar u kunt ook absolute paden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b4293-153">You can also use absolute paths.</span></span>  <span data-ttu-id="b4293-154">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b4293-154">For example:</span></span>

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

<span data-ttu-id="b4293-155">U moet absolute paden tooaccess bestanden in gekoppelde Storage-accounts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b4293-155">You must use absolute paths tooaccess files in linked Storage accounts.</span></span>  <span data-ttu-id="b4293-156">Hallo-syntaxis voor bestanden die zijn opgeslagen in het gekoppelde Azure Storage-account is:</span><span class="sxs-lookup"><span data-stu-id="b4293-156">hello syntax for files stored in linked Azure Storage account is:</span></span>

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> <span data-ttu-id="b4293-157">Azure Blob-containers met openbare blobs worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b4293-157">Azure Blob container with public blobs are not supported.</span></span>      
> <span data-ttu-id="b4293-158">Azure Blob-containers met openbare containers worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b4293-158">Azure Blob container with public containers are not supported.</span></span>      
>

<span data-ttu-id="b4293-159">**toosubmit taken**</span><span class="sxs-lookup"><span data-stu-id="b4293-159">**toosubmit jobs**</span></span>

<span data-ttu-id="b4293-160">Gebruik Hallo syntaxis toosubmit een taak te volgen.</span><span class="sxs-lookup"><span data-stu-id="b4293-160">Use hello following syntax toosubmit a job.</span></span>

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="b4293-161">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b4293-161">For example:</span></span>

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="b4293-162">**toolist taken en de taakdetails weergeven**</span><span class="sxs-lookup"><span data-stu-id="b4293-162">**toolist jobs and show job details**</span></span>

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="b4293-163">**toocancel taken**</span><span class="sxs-lookup"><span data-stu-id="b4293-163">**toocancel jobs**</span></span>

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a><span data-ttu-id="b4293-164">Taakresultaten ophalen</span><span class="sxs-lookup"><span data-stu-id="b4293-164">Retrieve job results</span></span>

<span data-ttu-id="b4293-165">Nadat een taak is voltooid, kunt u gebruiken Hallo opdrachten toolist Hallo uitvoerbestanden te volgen en Hallo bestanden downloaden:</span><span class="sxs-lookup"><span data-stu-id="b4293-165">After a job is completed, you can use hello following commands toolist hello output files, and download hello files:</span></span>

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="b4293-166">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b4293-166">For example:</span></span>

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="b4293-167">Pijplijnen en herhalingen</span><span class="sxs-lookup"><span data-stu-id="b4293-167">Pipelines and recurrences</span></span>

<span data-ttu-id="b4293-168">**Meer informatie over pijplijnen en herhalingen**</span><span class="sxs-lookup"><span data-stu-id="b4293-168">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="b4293-169">Gebruik Hallo `az dla job pipeline` opdrachten toosee Hallo pijplijn informatie taken eerder is verzonden.</span><span class="sxs-lookup"><span data-stu-id="b4293-169">Use hello `az dla job pipeline` commands toosee hello pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="b4293-170">Gebruik Hallo `az dla job recurrence` opdrachten toosee Hallo terugkeerpatroon informatie voor eerder ingediende taken.</span><span class="sxs-lookup"><span data-stu-id="b4293-170">Use hello `az dla job recurrence` commands toosee hello recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a><span data-ttu-id="b4293-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b4293-171">Next steps</span></span>

* <span data-ttu-id="b4293-172">toosee hello referentiedocument Data Lake Analytics CLI 2.0, Zie [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span><span class="sxs-lookup"><span data-stu-id="b4293-172">toosee hello Data Lake Analytics CLI 2.0 reference document, see [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="b4293-173">toosee hello referentiedocument Data Lake Store CLI 2.0, Zie [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="b4293-173">toosee hello Data Lake Store CLI 2.0 reference document, see [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="b4293-174">Zie voor een complexere query toosee [websitelogboeken analyseren met Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="b4293-174">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>

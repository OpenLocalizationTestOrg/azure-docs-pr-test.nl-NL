---
title: aaaCreate Hive-tabellen en laden van gegevens uit Azure Blob Storage | Microsoft Docs
description: Hive-tabellen maken en te laden van gegevens in blob toohive tabellen
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="be5da-103">Hive-tabellen maken en gegevens uit Azure Blob-opslag laden</span><span class="sxs-lookup"><span data-stu-id="be5da-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="be5da-104">Dit onderwerp bevat algemene Hive-query's die Hive-tabellen maken en gegevens uit Azure blob-opslag laden.</span><span class="sxs-lookup"><span data-stu-id="be5da-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="be5da-105">Sommige richtlijnen is ook beschikbaar op het Hive-tabellen te partitioneren en over het gebruik van Hallo geoptimaliseerd rij kolommen (ORC) opmaak tooimprove prestaties van query's.</span><span class="sxs-lookup"><span data-stu-id="be5da-105">Some guidance is also provided on partitioning Hive tables and on using hello Optimized Row Columnar (ORC) formatting tooimprove query performance.</span></span>

<span data-ttu-id="be5da-106">Dit **menu** koppelingen tootopics waarin wordt beschreven hoe tooingest gegevens in de doel-omgevingen waar Hallo gegevens kunnen worden opgeslagen en verwerkt tijdens Hallo Team gegevens wetenschap proces (TDSP).</span><span class="sxs-lookup"><span data-stu-id="be5da-106">This **menu** links tootopics that describe how tooingest data into target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="be5da-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="be5da-107">Prerequisites</span></span>
<span data-ttu-id="be5da-108">In dit artikel wordt ervan uitgegaan dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="be5da-108">This article assumes that you have:</span></span>

* <span data-ttu-id="be5da-109">Een Azure storage-account gemaakt.</span><span class="sxs-lookup"><span data-stu-id="be5da-109">Created an Azure storage account.</span></span> <span data-ttu-id="be5da-110">Als u instructies nodig hebt, raadpleegt u [over Azure storage-accounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="be5da-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="be5da-111">Een aangepaste Hadoop-cluster met Hallo HDInsight-service wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="be5da-111">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="be5da-112">Als u instructies nodig hebt, raadpleegt u [aanpassen Azure HDInsight Hadoop-clusters voor geavanceerde analyses](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="be5da-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="be5da-113">Ingeschakelde RAS toohello cluster aangemeld en Hallo Hadoop opdrachtregelconsole geopend.</span><span class="sxs-lookup"><span data-stu-id="be5da-113">Enabled remote access toohello cluster, logged in, and opened hello Hadoop Command-Line console.</span></span> <span data-ttu-id="be5da-114">Als u instructies nodig hebt, raadpleegt u [toegang Hallo Head knooppunt van Hadoop-Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="be5da-114">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="be5da-115">Uploaden van gegevens tooAzure blob-opslag</span><span class="sxs-lookup"><span data-stu-id="be5da-115">Upload data tooAzure blob storage</span></span>
<span data-ttu-id="be5da-116">Als u een virtuele machine in Azure gemaakt op basis van Hallo instructies in [instellen van een virtuele machine van Azure voor geavanceerde analyses](machine-learning-data-science-setup-virtual-machine.md), dit scriptbestand had moet zijn gedownloade toohello *C:\\ Gebruikers\\\<gebruikersnaam\>\\documenten\\gegevens wetenschappelijke Scripts* map op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="be5da-116">If you created an Azure virtual machine by following hello instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded toohello *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on hello virtual machine.</span></span> <span data-ttu-id="be5da-117">Deze Hive-query's vereisen alleen plug-in uw eigen gegevensschema en de Azure blob storage-configuratie in Hallo juiste velden toobe gereed voor verzending.</span><span class="sxs-lookup"><span data-stu-id="be5da-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in hello appropriate fields toobe ready for submission.</span></span>

<span data-ttu-id="be5da-118">Er wordt ervan uitgegaan dat Hallo-gegevens voor Hive-tabellen een **niet-gecomprimeerde** tabelvorm en dat Hallo gegevens zijn geüpload toohello standaard (of extra tooan) container van Hallo storage-account die wordt gebruikt door Hallo Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="be5da-118">We assume that hello data for Hive tables is in an **uncompressed** tabular format, and that hello data has been uploaded toohello default (or tooan additional) container of hello storage account used by hello Hadoop cluster.</span></span>

<span data-ttu-id="be5da-119">Als u wilt dat toopractice op Hallo **NYC Taxi reis gegevens**, moet u:</span><span class="sxs-lookup"><span data-stu-id="be5da-119">If you want toopractice on hello **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="be5da-120">**Download** Hallo 24 [NYC Taxi reis gegevens](http://www.andresmh.com/nyctaxitrips) -bestanden (12 reis bestanden en 12 tarief-bestanden)</span><span class="sxs-lookup"><span data-stu-id="be5da-120">**download** hello 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="be5da-121">**Pak** alle bestanden in CSV-bestanden, en vervolgens</span><span class="sxs-lookup"><span data-stu-id="be5da-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="be5da-122">**uploaden** ze toohello standaard (of juiste container) van Azure storage-account dat is gemaakt door Hallo procedure beschreven in Hallo Hallo [aanpassen Azure HDInsight Hadoop-clusters voor Advanced Analytics-proces en technologie ](machine-learning-data-science-customize-hadoop-cluster.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="be5da-122">**upload** them toohello default (or appropriate container) of hello Azure storage account that was created by hello procedure outlined in hello [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="be5da-123">Hallo proces tooupload Hallo .csv-bestanden toohello standaardcontainer op Hallo opslagaccount vindt u op dit [pagina](machine-learning-data-science-process-hive-walkthrough.md#upload).</span><span class="sxs-lookup"><span data-stu-id="be5da-123">hello process tooupload hello .csv files toohello default container on hello storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="be5da-124"><a name="submit"></a>Hoe toosubmit Hive-query's</span><span class="sxs-lookup"><span data-stu-id="be5da-124"><a name="submit"></a>How toosubmit Hive queries</span></span>
<span data-ttu-id="be5da-125">Hive-query's kunnen worden verzonden met behulp van:</span><span class="sxs-lookup"><span data-stu-id="be5da-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="be5da-126">Indienen van Hive-query's via de opdrachtregel voor Hadoop in headnode van Hadoop-cluster</span><span class="sxs-lookup"><span data-stu-id="be5da-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="be5da-127">Indienen van Hive-query's met Hallo Hive-Editor</span><span class="sxs-lookup"><span data-stu-id="be5da-127">Submit Hive queries with hello Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="be5da-128">Indienen van Hive-query's met Azure PowerShell-opdrachten</span><span class="sxs-lookup"><span data-stu-id="be5da-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="be5da-129">Hive-query's zijn SQL-achtige.</span><span class="sxs-lookup"><span data-stu-id="be5da-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="be5da-130">Als u bekend met SQL bent, vindt u Hallo [Hive voor SQL gebruikers cheats blad](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) nuttig.</span><span class="sxs-lookup"><span data-stu-id="be5da-130">If you are familiar with SQL, you may find hello [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="be5da-131">Bij het indienen van een Hive-query kunt u Hallo bestemming van Hallo-uitvoer van Hive-query's ook bepalen of deze nu op Hallo scherm of tooa lokaal bestand op het hoofdknooppunt Hallo of tooan Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="be5da-131">When submitting a Hive query, you can also control hello destination of hello output from Hive queries, whether it be on hello screen or tooa local file on hello head node or tooan Azure blob.</span></span>

### <span data-ttu-id="be5da-132"><a name="headnode"></a> 1. Indienen van Hive-query's via de opdrachtregel voor Hadoop in headnode van Hadoop-cluster</span><span class="sxs-lookup"><span data-stu-id="be5da-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="be5da-133">Als Hallo Hive-is query complex is of verzenden dat deze rechtstreeks in het hoofdknooppunt van het Hadoop-cluster Hallo Hallo doorgaans toofaster Schakel rond dan verzendt, wordt deze met een Hive-Editor of Azure PowerShell-scripts leidt.</span><span class="sxs-lookup"><span data-stu-id="be5da-133">If hello Hive query is complex, submitting it directly in hello head node of hello Hadoop cluster typically leads toofaster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="be5da-134">Hoofdknooppunt van het Hadoop-cluster Hallo toohello aanmelden, opent u Hallo Hadoop vanaf de opdrachtregel op Hallo bureaublad van hoofdknooppunt Hallo en voer de opdracht `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="be5da-134">Log in toohello head node of hello Hadoop cluster, open hello Hadoop Command Line on hello desktop of hello head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="be5da-135">Hebt u drie manieren toosubmit Hive-query's in Hallo Hadoop-opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="be5da-135">You have three ways toosubmit Hive queries in hello Hadoop Command Line:</span></span>

* <span data-ttu-id="be5da-136">rechtstreeks</span><span class="sxs-lookup"><span data-stu-id="be5da-136">directly</span></span>
* <span data-ttu-id="be5da-137">met behulp van .hql bestanden</span><span class="sxs-lookup"><span data-stu-id="be5da-137">using .hql files</span></span>
* <span data-ttu-id="be5da-138">Hello Hive opdrachtconsole</span><span class="sxs-lookup"><span data-stu-id="be5da-138">with hello Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="be5da-139">Indienen van Hive-query's rechtstreeks in Hadoop vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="be5da-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="be5da-140">U kunt een opdracht zoals uitvoeren `hive -e "<your hive query>;` toosubmit eenvoudige Hive-query's rechtstreeks in Hadoop vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="be5da-140">You can run command like `hive -e "<your hive query>;` toosubmit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="be5da-141">Hier volgt een voorbeeld, waarbij Hallo rode vak overzichten Hallo opdracht die is ingediend door Hallo Hive-query en Hallo groene vak overzichten Hallo uitvoer van Hallo Hive-query.</span><span class="sxs-lookup"><span data-stu-id="be5da-141">Here is an example, where hello red box outlines hello command that submits hello Hive query, and hello green box outlines hello output from hello Hive query.</span></span>

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="be5da-143">Indienen van Hive-query's in .hql bestanden</span><span class="sxs-lookup"><span data-stu-id="be5da-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="be5da-144">Wanneer Hallo Hive-query gecompliceerdere is en meerdere regels heeft, is query's in de opdrachtregel of Hive-opdrachtconsole bewerken het niet praktisch.</span><span class="sxs-lookup"><span data-stu-id="be5da-144">When hello Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="be5da-145">Een alternatief is toouse een teksteditor in het hoofdknooppunt van Hallo Hadoop-cluster toosave Hallo Hive-query's in een bestand .hql in een lokale map van het hoofdknooppunt Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="be5da-145">An alternative is toouse a text editor in hello head node of hello Hadoop cluster toosave hello Hive queries in a .hql file in a local directory of hello head node.</span></span> <span data-ttu-id="be5da-146">Vervolgens Hallo Hive-query in Hallo .hql bestand kan worden verzonden met behulp van Hallo `-f` argument als volgt:</span><span class="sxs-lookup"><span data-stu-id="be5da-146">Then hello Hive query in hello .hql file can be submitted by using hello `-f` argument as follows:</span></span>

    hive -f "<path toohello .hql file>"

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="be5da-148">**Onderdrukken voortgang Statusoverzicht scherm van Hive-query 's**</span><span class="sxs-lookup"><span data-stu-id="be5da-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="be5da-149">Standaard nadat Hive-query wordt verzonden in Hadoop opdrachtregel wordt Hallo voortgang van Hallo kaart/verminderen taak afgedrukt op het scherm.</span><span class="sxs-lookup"><span data-stu-id="be5da-149">By default, after Hive query is submitted in Hadoop Command Line, hello progress of hello Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="be5da-150">toosuppress Hallo scherm afdrukken van de voortgang van de taak kaart/verminderen hello, kunt u een argument `-S` ("S" in hoofdletters) in Hallo opdrachtregel als volgt:</span><span class="sxs-lookup"><span data-stu-id="be5da-150">toosuppress hello screen print of hello Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in hello command line as follows:</span></span>

    hive -S -f "<path toohello .hql file>"
<span data-ttu-id="be5da-151">.</span><span class="sxs-lookup"><span data-stu-id="be5da-151">.</span></span>    <span data-ttu-id="be5da-152">hive -S -e '<Hive queries>'</span><span class="sxs-lookup"><span data-stu-id="be5da-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="be5da-153">Indienen van Hive-query's in de opdrachtconsole Hive.</span><span class="sxs-lookup"><span data-stu-id="be5da-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="be5da-154">U kunt ook eerst Hallo Hive opdrachtconsole invoeren door de opdracht uit te voeren `hive` in Hadoop vanaf de opdrachtregel, en verzend Hive-query's in de opdrachtconsole Hive.</span><span class="sxs-lookup"><span data-stu-id="be5da-154">You can also first enter hello Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="be5da-155">Hier volgt een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="be5da-155">Here is an example.</span></span> <span data-ttu-id="be5da-156">In dit voorbeeld Hallo twee rode vakken markeren Hallo-opdrachten gebruikt tooenter Hallo Hive opdrachtconsole en Hallo Hive-query verzonden in de Hive-opdrachtconsole, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="be5da-156">In this example, hello two red boxes highlight hello commands used tooenter hello Hive command console, and hello Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="be5da-157">Hallo groen vak licht Hallo-uitvoer van Hallo Hive-query.</span><span class="sxs-lookup"><span data-stu-id="be5da-157">hello green box highlights hello output from hello Hive query.</span></span>

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="be5da-159">de eerdere voorbeelden Hallo uitvoerresultaten rechtstreeks Hallo Hive-query op het scherm.</span><span class="sxs-lookup"><span data-stu-id="be5da-159">hello previous examples directly output hello Hive query results on screen.</span></span> <span data-ttu-id="be5da-160">U kunt ook Hallo tooa lokale uitvoerbestand op Hallo hoofdknooppunt of tooan Azure blob schrijven.</span><span class="sxs-lookup"><span data-stu-id="be5da-160">You can also write hello output tooa local file on hello head node, or tooan Azure blob.</span></span> <span data-ttu-id="be5da-161">Vervolgens gebruikt u andere hulpprogramma's toofurther analyseren Hallo-uitvoer van Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="be5da-161">Then, you can use other tools toofurther analyze hello output of Hive queries.</span></span>

<span data-ttu-id="be5da-162">**Hive query resultaten tooa lokale bestand voor uitvoer.**</span><span class="sxs-lookup"><span data-stu-id="be5da-162">**Output Hive query results tooa local file.**</span></span>
<span data-ttu-id="be5da-163">toooutput Hive query resultaten tooa lokale map op het hoofdknooppunt hello, hebt u toosubmit Hallo Hive-query in Hallo Hadoop vanaf de opdrachtregel als volgt:</span><span class="sxs-lookup"><span data-stu-id="be5da-163">toooutput Hive query results tooa local directory on hello head node, you have toosubmit hello Hive query in hello Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in hello head node>

<span data-ttu-id="be5da-164">In Hallo voorbeeld te volgen, Hallo-uitvoer van Hive-query is geschreven in een bestand `hivequeryoutput.txt` in directory `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="be5da-164">In hello following example, hello output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="be5da-166">**Uitvoer Hive query resultaten tooan Azure-blobopslag**</span><span class="sxs-lookup"><span data-stu-id="be5da-166">**Output Hive query results tooan Azure blob**</span></span>

<span data-ttu-id="be5da-167">U kunt ook Hallo Hive query resultaten tooan Azure blob, binnen de standaardcontainer Hallo van Hadoop-cluster Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="be5da-167">You can also output hello Hive query results tooan Azure blob, within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="be5da-168">Hallo Hive-query voor deze is als volgt:</span><span class="sxs-lookup"><span data-stu-id="be5da-168">hello Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

<span data-ttu-id="be5da-169">In de Hallo voorbeeld te volgen, Hallo uitvoer van Hive-query tooa blob directory geschreven `queryoutputdir` binnen de standaardcontainer Hallo van Hallo Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="be5da-169">In hello following example, hello output of Hive query is written tooa blob directory `queryoutputdir` within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="be5da-170">Hier hoeft u alleen tooprovide Hallo mapnaam, zonder Hallo blob-naam.</span><span class="sxs-lookup"><span data-stu-id="be5da-170">Here, you only need tooprovide hello directory name, without hello blob name.</span></span> <span data-ttu-id="be5da-171">Een fout gegenereerd als u zowel de directory en de blob-namen, zoals opgeeft `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="be5da-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="be5da-173">Als u de standaardcontainer Hallo van Hallo Hadoop-cluster met behulp van Azure Storage Explorer opent, ziet u uitvoer Hallo van Hallo Hive-query zoals weergegeven in de volgende afbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="be5da-173">If you open hello default container of hello Hadoop cluster using Azure Storage Explorer, you can see hello output of hello Hive query as shown in hello following figure.</span></span> <span data-ttu-id="be5da-174">U kunt toepassen Hallo filter (gemarkeerd met een rood kader) tooonly ophalen Hallo blob met de opgegeven letters in namen.</span><span class="sxs-lookup"><span data-stu-id="be5da-174">You can apply hello filter (highlighted by red box) tooonly retrieve hello blob with specified letters in names.</span></span>

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="be5da-176"><a name="hive-editor"></a> 2. Indienen van Hive-query's met Hallo Hive-Editor</span><span class="sxs-lookup"><span data-stu-id="be5da-176"><a name="hive-editor"></a> 2. Submit Hive queries with hello Hive Editor</span></span>
<span data-ttu-id="be5da-177">U kunt ook Hallo Query Console (Hive-Editor) gebruiken door een URL van Hallo formulier *https://&#60; De naam van de Hadoop-cluster >.azurehdinsight.net/Home/HiveEditor* in een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="be5da-177">You can also use hello Query Console (Hive Editor) by entering a URL of hello form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="be5da-178">U moet zijn geregistreerd in Hallo Zie deze console en dus moet u uw hier Hadoop-cluster-referenties.</span><span class="sxs-lookup"><span data-stu-id="be5da-178">You must be logged in hello see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="be5da-179"><a name="ps"></a> 3. Indienen van Hive-query's met Azure PowerShell-opdrachten</span><span class="sxs-lookup"><span data-stu-id="be5da-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="be5da-180">U kunt ook PowerShell toosubmit Hive-query's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="be5da-180">You can also use PowerShell toosubmit Hive queries.</span></span> <span data-ttu-id="be5da-181">Zie voor instructies [indienen Hive-taken met behulp van PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="be5da-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="be5da-182"><a name="create-tables"></a>Hive-database en tabellen maken</span><span class="sxs-lookup"><span data-stu-id="be5da-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="be5da-183">Hallo Hive-query's gedeeld in Hallo [GitHub-opslagplaats](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) en van daaruit kan worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="be5da-183">hello Hive queries are shared in hello [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="be5da-184">Hier volgt Hallo Hive-query waarmee een Hive-tabel.</span><span class="sxs-lookup"><span data-stu-id="be5da-184">Here is hello Hive query that creates a Hive table.</span></span>

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

<span data-ttu-id="be5da-185">Hier volgen beschrijvingen van Hallo Hallo velden die u nodig hebt tooplug in en andere configuraties:</span><span class="sxs-lookup"><span data-stu-id="be5da-185">Here are hello descriptions of hello fields that you need tooplug in and other configurations:</span></span>

* <span data-ttu-id="be5da-186">**&#60; databasenaam >**: Hallo-naam van Hallo-database die u toocreate wilt.</span><span class="sxs-lookup"><span data-stu-id="be5da-186">**&#60;database name>**: hello name of hello database that you want toocreate.</span></span> <span data-ttu-id="be5da-187">Desgewenst kunt u alleen toouse Hallo standaarddatabase Hallo query *database maken...*  kunnen worden weggelaten.</span><span class="sxs-lookup"><span data-stu-id="be5da-187">If you just want toouse hello default database, hello query *create database...* can be omitted.</span></span>
* <span data-ttu-id="be5da-188">**&#60; tabelnaam >**: Hallo-naam van de gewenste toocreate binnen de opgegeven database Hallo Hallo-tabel.</span><span class="sxs-lookup"><span data-stu-id="be5da-188">**&#60;table name>**: hello name of hello table that you want toocreate within hello specified database.</span></span> <span data-ttu-id="be5da-189">Als u toouse Hallo standaarddatabase wilt, Hallo tabel rechtstreeks kan worden verwezen door *&#60; tabelnaam >* zonder &#60; databasenaam >.</span><span class="sxs-lookup"><span data-stu-id="be5da-189">If you want toouse hello default database, hello table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="be5da-190">**&#60; veldscheidingsteken >**: Hallo scheidingsteken die velden in Hallo gegevens bestand toobe begrenst geüpload toohello Hive-tabel.</span><span class="sxs-lookup"><span data-stu-id="be5da-190">**&#60;field separator>**: hello separator that delimits fields in hello data file toobe uploaded toohello Hive table.</span></span>
* <span data-ttu-id="be5da-191">**&#60; regelscheiding >**: regels in het gegevensbestand Hallo begrenst Hallo scheidingsteken.</span><span class="sxs-lookup"><span data-stu-id="be5da-191">**&#60;line separator>**: hello separator that delimits lines in hello data file.</span></span>
* <span data-ttu-id="be5da-192">**&#60; opslaglocatie >**: hello Azure storage toosave Hallo locatiegegevens van Hive-tabellen.</span><span class="sxs-lookup"><span data-stu-id="be5da-192">**&#60;storage location>**: hello Azure storage location toosave hello data of Hive tables.</span></span> <span data-ttu-id="be5da-193">Als u geen opgeeft *locatie &#60; opslaglocatie >*, Hallo database en hello tabellen zijn opgeslagen in *hive/datawarehouse/* map in de standaardcontainer Hallo van Hallo Hive cluster standaard.</span><span class="sxs-lookup"><span data-stu-id="be5da-193">If you do not specify *LOCATION &#60;storage location>*, hello database and hello tables are stored in *hive/warehouse/* directory in hello default container of hello Hive cluster by default.</span></span> <span data-ttu-id="be5da-194">Als u toospecify Hallo-opslaglocatie wilt, heeft de opslaglocatie Hallo toobe binnen de standaardcontainer Hallo voor Hallo-database en tabellen.</span><span class="sxs-lookup"><span data-stu-id="be5da-194">If you want toospecify hello storage location, hello storage location has toobe within hello default container for hello database and tables.</span></span> <span data-ttu-id="be5da-195">Deze locatie heeft een toobe verwezen als locatie relatieve toohello standaardcontainer van Hallo-cluster op Hallo-indeling van *' wasb: / / / &#60; map 1 > / "* of *' wasb: / / / &#60; map 1 > / &#60; map 2 > / "*, enzovoort. Nadat het Hallo-query wordt uitgevoerd, worden Hallo relatieve mappen in Hallo standaardcontainer gemaakt.</span><span class="sxs-lookup"><span data-stu-id="be5da-195">This location has toobe referred as location relative toohello default container of hello cluster in hello format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After hello query is executed, hello relative directories are created within hello default container.</span></span>
* <span data-ttu-id="be5da-196">**TBLPROPERTIES("SKIP.header.line.Count"="1")**: als het gegevensbestand Hallo een kopregel heeft, hebt u tooadd deze eigenschap **aan Hallo einde** Hallo *tabel maken* query.</span><span class="sxs-lookup"><span data-stu-id="be5da-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If hello data file has a header line, you have tooadd this property **at hello end** of hello *create table* query.</span></span> <span data-ttu-id="be5da-197">Anders is Hallo kopregel geladen als een tabel, record toohello.</span><span class="sxs-lookup"><span data-stu-id="be5da-197">Otherwise, hello header line is loaded as a record toohello table.</span></span> <span data-ttu-id="be5da-198">Als het Hallo-gegevensbestand geen een kopregel heeft, kan deze configuratie worden weggelaten in Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="be5da-198">If hello data file does not have a header line, this configuration can be omitted in hello query.</span></span>

## <span data-ttu-id="be5da-199"><a name="load-data"></a>TooHive gegevenstabellen laden</span><span class="sxs-lookup"><span data-stu-id="be5da-199"><a name="load-data"></a>Load data tooHive tables</span></span>
<span data-ttu-id="be5da-200">Hier volgt Hallo Hive-query die gegevens in een Hive-tabel laadt.</span><span class="sxs-lookup"><span data-stu-id="be5da-200">Here is hello Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="be5da-201">**&#60; pad tooblob gegevens >**: als Hallo blob bestand geüpload toobe toohello Hive-tabel in de standaardcontainer Hallo Hallo HDInsight Hadoop-cluster, Hallo *&#60; pad tooblob gegevens >* moet Hallo-indeling *' wasb: / / / &#60; directory in deze container > / &#60; blob-bestandsnaam >'*.</span><span class="sxs-lookup"><span data-stu-id="be5da-201">**&#60;path tooblob data>**: If hello blob file toobe uploaded toohello Hive table is in hello default container of hello HDInsight Hadoop cluster, hello *&#60;path tooblob data>* should be in hello format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="be5da-202">Hallo blob-bestand kan ook worden in een extra container Hallo HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="be5da-202">hello blob file can also be in an additional container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="be5da-203">In dit geval *&#60; pad tooblob gegevens >* moet Hallo indeling *' wasb: / / &#60; containernaam > @&#60; opslagaccountnaam >.blob.core.windows.net/ &#60; blob-bestandsnaam >'*.</span><span class="sxs-lookup"><span data-stu-id="be5da-203">In this case, *&#60;path tooblob data>* should be in hello format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="be5da-204">Hallo heeft toobe geüpload blob-tooHive gegevenstabel toobe in Hallo standaard of extra container van Hallo storage-account voor Hallo Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="be5da-204">hello blob data toobe uploaded tooHive table has toobe in hello default or additional container of hello storage account for hello Hadoop cluster.</span></span> <span data-ttu-id="be5da-205">Anders Hallo *gegevens laden* klagen dat deze geen toegang gegevens Hallo tot query is mislukt.</span><span class="sxs-lookup"><span data-stu-id="be5da-205">Otherwise, hello *LOAD DATA* query fails complaining that it cannot access hello data.</span></span>
  >
  >

## <span data-ttu-id="be5da-206"><a name="partition-orc"></a>Onderwerpen over geavanceerde: gepartitioneerde tabel en archief Hive-gegevens in ORC-indeling</span><span class="sxs-lookup"><span data-stu-id="be5da-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="be5da-207">Als Hallo gegevens groot is, is partitioneren van tabel Hallo nuttig is voor query's die u alleen tooscan enkele partities van Hallo tabel hoeft.</span><span class="sxs-lookup"><span data-stu-id="be5da-207">If hello data is large, partitioning hello table is beneficial for queries that only need tooscan a few partitions of hello table.</span></span> <span data-ttu-id="be5da-208">Het is bijvoorbeeld redelijke toopartition Hallo logboekgegevens van een website door datums.</span><span class="sxs-lookup"><span data-stu-id="be5da-208">For instance, it is reasonable toopartition hello log data of a web site by dates.</span></span>

<span data-ttu-id="be5da-209">In aanvulling toopartitioning Hive-tabellen, het is ook nuttig toostore Hallo Hive gegevens in Hallo geoptimaliseerd rij kolommen (ORC)-indeling.</span><span class="sxs-lookup"><span data-stu-id="be5da-209">In addition toopartitioning Hive tables, it is also beneficial toostore hello Hive data in hello Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="be5da-210">Zie voor meer informatie over het ORC opmaak <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">met behulp van ORC-bestanden verbetert de prestaties wanneer Hive lezen, schrijven en verwerken van gegevens</a>.</span><span class="sxs-lookup"><span data-stu-id="be5da-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="be5da-211">Gepartitioneerde tabel</span><span class="sxs-lookup"><span data-stu-id="be5da-211">Partitioned table</span></span>
<span data-ttu-id="be5da-212">Hier volgt Hallo Hive-query die een gepartitioneerde tabel maakt en gegevens worden geladen in de App.</span><span class="sxs-lookup"><span data-stu-id="be5da-212">Here is hello Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="be5da-213">Tijdens het opvragen van gepartitioneerde tabellen, verdient het tooadd Hallo partitie voorwaarde in Hallo **begin** Hallo `where` component deze verbetert Hallo effectiviteit aanzienlijk te zoeken.</span><span class="sxs-lookup"><span data-stu-id="be5da-213">When querying partitioned tables, it is recommended tooadd hello partition condition in hello **beginning** of hello `where` clause as this improves hello efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="be5da-214"><a name="orc"></a>Hive-gegevens opslaat in ORC-indeling</span><span class="sxs-lookup"><span data-stu-id="be5da-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="be5da-215">U kan niet rechtstreeks gegevens uit blob-opslag laden in de Hive-tabellen die zijn opgeslagen in Hallo ORC-indeling.</span><span class="sxs-lookup"><span data-stu-id="be5da-215">You cannot directly load data from blob storage into Hive tables that is stored in hello ORC format.</span></span> <span data-ttu-id="be5da-216">Hier volgen de stappen Hallo die Hallo moet u tootake tooload gegevens van Azure blobs tooHive tabellen die zijn opgeslagen in ORC-indeling.</span><span class="sxs-lookup"><span data-stu-id="be5da-216">Here are hello steps that hello you need tootake tooload data from Azure blobs tooHive tables stored in ORC format.</span></span>

<span data-ttu-id="be5da-217">Maken van een externe tabel **opgeslagen AS TEXTFILE** en laden van gegevens uit blob storage toohello tabel.</span><span class="sxs-lookup"><span data-stu-id="be5da-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage toohello table.</span></span>

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="be5da-218">Een interne tabel maken met de Hallo Hallo hetzelfde schema als externe tabel Hallo in stap 1, hello dezelfde veldscheidingsteken en op te slaan Hive-gegevens in Hallo ORC-indeling.</span><span class="sxs-lookup"><span data-stu-id="be5da-218">Create an internal table with hello same schema as hello external table in step 1, with hello same field delimiter, and store hello Hive data in hello ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="be5da-219">Selecteer de gegevens uit de externe tabel Hallo in stap 1 en invoegen in Hallo ORC tabel</span><span class="sxs-lookup"><span data-stu-id="be5da-219">Select data from hello external table in step 1 and insert into hello ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="be5da-220">Als Hallo TEXTFILE tabel *&#60; databasenaam >. &#60; externe textfile tabelnaam >* partities bevat, in stap 3 hello `SELECT * FROM <database name>.<external textfile table name>` opdracht selecteert Hallo partitie variabele een veld in Hallo gegevensset geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="be5da-220">If hello TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, hello `SELECT * FROM <database name>.<external textfile table name>` command selects hello partition variable as a field in hello returned data set.</span></span> <span data-ttu-id="be5da-221">Opneemt in Hallo *&#60; databasenaam >. &#60; ORC-tabelnaam >* mislukt sinds *&#60; databasenaam >. &#60; ORC-tabelnaam >* heeft geen Hallo partitie variabele als een veld in het tabelschema Hallo.</span><span class="sxs-lookup"><span data-stu-id="be5da-221">Inserting it into hello *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have hello partition variable as a field in hello table schema.</span></span> <span data-ttu-id="be5da-222">In dit geval moet u toospecifically Selecteer Hallo velden toobe ingevoegd te*&#60; databasenaam >. &#60; ORC-tabelnaam >* als volgt:</span><span class="sxs-lookup"><span data-stu-id="be5da-222">In this case, you need toospecifically select hello fields toobe inserted too*&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="be5da-223">Het is veilig toodrop hello *&#60; externe textfile tabelnaam >* wanneer met behulp van de query te volgen nadat alle gegevens Hallo is ingevoegd in *&#60; databasenaam >. &#60; ORC-tabelnaam >*:</span><span class="sxs-lookup"><span data-stu-id="be5da-223">It is safe toodrop hello *&#60;external textfile table name>* when using hello following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="be5da-224">Na deze procedure uitvoert, moet u een tabel met gegevens in Hallo ORC indeling gereed toouse hebben.</span><span class="sxs-lookup"><span data-stu-id="be5da-224">After following this procedure, you should have a table with data in hello ORC format ready toouse.</span></span>  

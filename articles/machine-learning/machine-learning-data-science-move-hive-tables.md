---
title: Hive-tabellen maken en te laden van gegevens uit Azure Blob Storage | Microsoft Docs
description: Hive-tabellen maken en te laden van gegevens in blob naar de hive-tabellen
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
ms.openlocfilehash: eca4ecd8f639bb9816903f4b1d1f999755da819c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="14c4f-103">Hive-tabellen maken en gegevens uit Azure Blob-opslag laden</span><span class="sxs-lookup"><span data-stu-id="14c4f-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="14c4f-104">Dit onderwerp bevat algemene Hive-query's die Hive-tabellen maken en gegevens uit Azure blob-opslag laden.</span><span class="sxs-lookup"><span data-stu-id="14c4f-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="14c4f-105">Sommige richtlijnen is ook beschikbaar op het Hive-tabellen te partitioneren en over het gebruik van de optimale rij kolommen (ORC) opmaak ter verbetering van de prestaties van query's.</span><span class="sxs-lookup"><span data-stu-id="14c4f-105">Some guidance is also provided on partitioning Hive tables and on using the Optimized Row Columnar (ORC) formatting to improve query performance.</span></span>

<span data-ttu-id="14c4f-106">Dit **menu** koppelingen naar onderwerpen waarin wordt beschreven hoe u opnemen van gegevens in de doel-omgevingen waarin de gegevens kunnen worden opgeslagen en verwerkt tijdens het Team gegevens wetenschap proces (TDSP).</span><span class="sxs-lookup"><span data-stu-id="14c4f-106">This **menu** links to topics that describe how to ingest data into target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="14c4f-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="14c4f-107">Prerequisites</span></span>
<span data-ttu-id="14c4f-108">In dit artikel wordt ervan uitgegaan dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="14c4f-108">This article assumes that you have:</span></span>

* <span data-ttu-id="14c4f-109">Een Azure storage-account gemaakt.</span><span class="sxs-lookup"><span data-stu-id="14c4f-109">Created an Azure storage account.</span></span> <span data-ttu-id="14c4f-110">Als u instructies nodig hebt, raadpleegt u [over Azure storage-accounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="14c4f-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="14c4f-111">Een aangepaste Hadoop-cluster met de HDInsight-service wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="14c4f-111">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span>  <span data-ttu-id="14c4f-112">Als u instructies nodig hebt, raadpleegt u [aanpassen Azure HDInsight Hadoop-clusters voor geavanceerde analyses](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="14c4f-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="14c4f-113">Ingeschakelde externe toegang tot het cluster aangemeld en de Hadoop-opdrachtregelconsole geopend.</span><span class="sxs-lookup"><span data-stu-id="14c4f-113">Enabled remote access to the cluster, logged in, and opened the Hadoop Command-Line console.</span></span> <span data-ttu-id="14c4f-114">Als u instructies nodig hebt, raadpleegt u [toegang tot de hoofd-knooppunt van Hadoop-Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="14c4f-114">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="14c4f-115">Gegevens uploaden naar Azure blob-opslag</span><span class="sxs-lookup"><span data-stu-id="14c4f-115">Upload data to Azure blob storage</span></span>
<span data-ttu-id="14c4f-116">Als u een virtuele machine in Azure gemaakt op basis van de instructies in [instellen van een virtuele machine van Azure voor geavanceerde analyses](machine-learning-data-science-setup-virtual-machine.md), dit scriptbestand moet worden gedownload naar de *C:\\gebruikers \\ \<gebruikersnaam\>\\documenten\\gegevens wetenschappelijke Scripts* map op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="14c4f-116">If you created an Azure virtual machine by following the instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded to the *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on the virtual machine.</span></span> <span data-ttu-id="14c4f-117">Deze Hive-query's vereisen alleen plug-in uw eigen gegevensschema en de configuratie van de Azure blob-opslag in de juiste velden gereed is voor verzending.</span><span class="sxs-lookup"><span data-stu-id="14c4f-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in the appropriate fields to be ready for submission.</span></span>

<span data-ttu-id="14c4f-118">Er wordt ervan uitgegaan dat de gegevens voor Hive-tabellen een **niet-gecomprimeerde** tabelvorm en die de gegevens is geüpload naar de standaardwaarde (of een extra) container van het opslagaccount dat wordt gebruikt door het Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="14c4f-118">We assume that the data for Hive tables is in an **uncompressed** tabular format, and that the data has been uploaded to the default (or to an additional) container of the storage account used by the Hadoop cluster.</span></span>

<span data-ttu-id="14c4f-119">Als u wilt oefenen op de **NYC Taxi reis gegevens**, moet u:</span><span class="sxs-lookup"><span data-stu-id="14c4f-119">If you want to practice on the **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="14c4f-120">**Download** de 24 [NYC Taxi reis gegevens](http://www.andresmh.com/nyctaxitrips) -bestanden (12 reis bestanden en 12 tarief-bestanden)</span><span class="sxs-lookup"><span data-stu-id="14c4f-120">**download** the 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="14c4f-121">**Pak** alle bestanden in CSV-bestanden, en vervolgens</span><span class="sxs-lookup"><span data-stu-id="14c4f-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="14c4f-122">**uploaden** ze naar de standaard (of de juiste container) van de Azure storage-account dat is gemaakt door de procedure beschreven in de [aanpassen Azure HDInsight Hadoop-clusters voor Advanced Analytics-proces en technologie](machine-learning-data-science-customize-hadoop-cluster.md)onderwerp.</span><span class="sxs-lookup"><span data-stu-id="14c4f-122">**upload** them to the default (or appropriate container) of the Azure storage account that was created by the procedure outlined in the [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="14c4f-123">Het proces voor het uploaden van de CSV-bestanden naar de standaardcontainer op het opslagaccount kan worden gevonden op deze [pagina](machine-learning-data-science-process-hive-walkthrough.md#upload).</span><span class="sxs-lookup"><span data-stu-id="14c4f-123">The process to upload the .csv files to the default container on the storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="14c4f-124"><a name="submit"></a>Het indienen van Hive-query 's</span><span class="sxs-lookup"><span data-stu-id="14c4f-124"><a name="submit"></a>How to submit Hive queries</span></span>
<span data-ttu-id="14c4f-125">Hive-query's kunnen worden verzonden met behulp van:</span><span class="sxs-lookup"><span data-stu-id="14c4f-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="14c4f-126">Indienen van Hive-query's via de opdrachtregel voor Hadoop in headnode van Hadoop-cluster</span><span class="sxs-lookup"><span data-stu-id="14c4f-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="14c4f-127">Indienen van Hive-query's met de Hive-Editor</span><span class="sxs-lookup"><span data-stu-id="14c4f-127">Submit Hive queries with the Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="14c4f-128">Indienen van Hive-query's met Azure PowerShell-opdrachten</span><span class="sxs-lookup"><span data-stu-id="14c4f-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="14c4f-129">Hive-query's zijn SQL-achtige.</span><span class="sxs-lookup"><span data-stu-id="14c4f-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="14c4f-130">Als u bekend met SQL bent, vindt u de [Hive voor SQL gebruikers cheats blad](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) nuttig.</span><span class="sxs-lookup"><span data-stu-id="14c4f-130">If you are familiar with SQL, you may find the [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="14c4f-131">Bij het indienen van een Hive-query kunt u ook de bestemming van de uitvoer van Hive-query's beheren, ongeacht of deze op het scherm of naar een lokaal bestand op het hoofdknooppunt of met een Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="14c4f-131">When submitting a Hive query, you can also control the destination of the output from Hive queries, whether it be on the screen or to a local file on the head node or to an Azure blob.</span></span>

### <span data-ttu-id="14c4f-132"><a name="headnode"></a> 1. Indienen van Hive-query's via de opdrachtregel voor Hadoop in headnode van Hadoop-cluster</span><span class="sxs-lookup"><span data-stu-id="14c4f-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="14c4f-133">Als de Hive-query complexe, leidt verzendt, wordt deze rechtstreeks in het hoofdknooppunt van het Hadoop-cluster meestal tot sneller inschakelen om dan verzendt, wordt deze met een Editor Hive of Azure PowerShell-scripts.</span><span class="sxs-lookup"><span data-stu-id="14c4f-133">If the Hive query is complex, submitting it directly in the head node of the Hadoop cluster typically leads to faster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="14c4f-134">Aanmelden met het hoofdknooppunt van het Hadoop-cluster, opent u de Hadoop-opdrachtregel op het bureaublad van het hoofdknooppunt en voer de opdracht `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="14c4f-134">Log in to the head node of the Hadoop cluster, open the Hadoop Command Line on the desktop of the head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="14c4f-135">Hebt u drie manieren om Hive-query's in de Hadoop-opdrachtregel verzenden:</span><span class="sxs-lookup"><span data-stu-id="14c4f-135">You have three ways to submit Hive queries in the Hadoop Command Line:</span></span>

* <span data-ttu-id="14c4f-136">rechtstreeks</span><span class="sxs-lookup"><span data-stu-id="14c4f-136">directly</span></span>
* <span data-ttu-id="14c4f-137">met behulp van .hql bestanden</span><span class="sxs-lookup"><span data-stu-id="14c4f-137">using .hql files</span></span>
* <span data-ttu-id="14c4f-138">met de Hive-opdrachtconsole</span><span class="sxs-lookup"><span data-stu-id="14c4f-138">with the Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="14c4f-139">Indienen van Hive-query's rechtstreeks in Hadoop vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="14c4f-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="14c4f-140">U kunt een opdracht zoals uitvoeren `hive -e "<your hive query>;` verzenden eenvoudige Hive-query's rechtstreeks in Hadoop vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="14c4f-140">You can run command like `hive -e "<your hive query>;` to submit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="14c4f-141">Hier volgt een voorbeeld, waarbij een rood kader geeft een overzicht van de opdracht die is ingediend door de Hive-query en het groene vak geeft een overzicht van de uitvoer van de Hive-query.</span><span class="sxs-lookup"><span data-stu-id="14c4f-141">Here is an example, where the red box outlines the command that submits the Hive query, and the green box outlines the output from the Hive query.</span></span>

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="14c4f-143">Indienen van Hive-query's in .hql bestanden</span><span class="sxs-lookup"><span data-stu-id="14c4f-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="14c4f-144">Wanneer de Hive-query gecompliceerdere is en meerdere regels heeft, is query's in de opdrachtregel of Hive-opdrachtconsole bewerken het niet praktisch.</span><span class="sxs-lookup"><span data-stu-id="14c4f-144">When the Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="14c4f-145">Een alternatief is het gebruik van een teksteditor in het hoofdknooppunt van het Hadoop-cluster de Hive-query's opslaan in een bestand .hql in een lokale map van het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="14c4f-145">An alternative is to use a text editor in the head node of the Hadoop cluster to save the Hive queries in a .hql file in a local directory of the head node.</span></span> <span data-ttu-id="14c4f-146">Vervolgens kan de Hive-query in het bestand .hql worden verzonden met behulp van de `-f` argument als volgt:</span><span class="sxs-lookup"><span data-stu-id="14c4f-146">Then the Hive query in the .hql file can be submitted by using the `-f` argument as follows:</span></span>

    hive -f "<path to the .hql file>"

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="14c4f-148">**Onderdrukken voortgang Statusoverzicht scherm van Hive-query 's**</span><span class="sxs-lookup"><span data-stu-id="14c4f-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="14c4f-149">Standaard nadat Hive-query wordt verzonden in Hadoop opdrachtregel wordt de voortgang van de taak van de kaart/verkleinen afgedrukt op het scherm.</span><span class="sxs-lookup"><span data-stu-id="14c4f-149">By default, after Hive query is submitted in Hadoop Command Line, the progress of the Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="14c4f-150">Als u wilt onderdrukken het afdrukken van het scherm van de voortgang van de taak kaart/verminderen, kunt u een argument `-S` ("S" in hoofdletters) in de opdracht regel als volgt:</span><span class="sxs-lookup"><span data-stu-id="14c4f-150">To suppress the screen print of the Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in the command line as follows:</span></span>

    hive -S -f "<path to the .hql file>"
<span data-ttu-id="14c4f-151">.</span><span class="sxs-lookup"><span data-stu-id="14c4f-151">.</span></span>    <span data-ttu-id="14c4f-152">hive -S -e '<Hive queries>'</span><span class="sxs-lookup"><span data-stu-id="14c4f-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="14c4f-153">Indienen van Hive-query's in de opdrachtconsole Hive.</span><span class="sxs-lookup"><span data-stu-id="14c4f-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="14c4f-154">U kunt ook eerst de opdrachtconsole Hive invoeren door de opdracht uit te voeren `hive` in Hadoop vanaf de opdrachtregel, en verzend Hive-query's in de opdrachtconsole Hive.</span><span class="sxs-lookup"><span data-stu-id="14c4f-154">You can also first enter the Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="14c4f-155">Hier volgt een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="14c4f-155">Here is an example.</span></span> <span data-ttu-id="14c4f-156">In dit voorbeeld zijn de twee rode vakken Markeer de opdrachten voor het invoeren van de Hive-opdrachtconsole en de Hive-query verzonden in de Hive-opdrachtconsole, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="14c4f-156">In this example, the two red boxes highlight the commands used to enter the Hive command console, and the Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="14c4f-157">Het groene vak licht de uitvoer van de Hive-query.</span><span class="sxs-lookup"><span data-stu-id="14c4f-157">The green box highlights the output from the Hive query.</span></span>

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="14c4f-159">De eerdere voorbeelden uitvoer rechtstreeks van de resultaten van de Hive-query op het scherm.</span><span class="sxs-lookup"><span data-stu-id="14c4f-159">The previous examples directly output the Hive query results on screen.</span></span> <span data-ttu-id="14c4f-160">U kunt de uitvoer ook schrijven naar een lokaal bestand op het hoofdknooppunt of met een Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="14c4f-160">You can also write the output to a local file on the head node, or to an Azure blob.</span></span> <span data-ttu-id="14c4f-161">Vervolgens kunt u andere hulpprogramma's voor het analyseren van verdere de uitvoer van Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="14c4f-161">Then, you can use other tools to further analyze the output of Hive queries.</span></span>

<span data-ttu-id="14c4f-162">**Hive-query naar een lokaal bestand uitvoerresultaten.**</span><span class="sxs-lookup"><span data-stu-id="14c4f-162">**Output Hive query results to a local file.**</span></span>
<span data-ttu-id="14c4f-163">Om het Hive-query naar een lokale map op het hoofdknooppunt uitvoerresultaten, hebt u als volgt de Hive-query in de Hadoop-opdrachtregel verzenden:</span><span class="sxs-lookup"><span data-stu-id="14c4f-163">To output Hive query results to a local directory on the head node, you have to submit the Hive query in the Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in the head node>

<span data-ttu-id="14c4f-164">In het volgende voorbeeld wordt de uitvoer van Hive-query naar een bestand is geschreven `hivequeryoutput.txt` in directory `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="14c4f-164">In the following example, the output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="14c4f-166">**Resultaten voor de uitvoer Hive-query naar een Azure-blob**</span><span class="sxs-lookup"><span data-stu-id="14c4f-166">**Output Hive query results to an Azure blob**</span></span>

<span data-ttu-id="14c4f-167">U kunt ook de resultaten van de Hive-query naar een Azure-blob, binnen de standaardcontainer van het Hadoop-cluster uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="14c4f-167">You can also output the Hive query results to an Azure blob, within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="14c4f-168">De Hive-query voor deze is als volgt:</span><span class="sxs-lookup"><span data-stu-id="14c4f-168">The Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within the default container> <select clause from ...>

<span data-ttu-id="14c4f-169">In het volgende voorbeeld wordt de uitvoer van Hive-query naar een blob-map geschreven. `queryoutputdir` binnen de standaardcontainer van het Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="14c4f-169">In the following example, the output of Hive query is written to a blob directory `queryoutputdir` within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="14c4f-170">Hier alleen moet u de naam van de map zonder de blob-naam opgeven.</span><span class="sxs-lookup"><span data-stu-id="14c4f-170">Here, you only need to provide the directory name, without the blob name.</span></span> <span data-ttu-id="14c4f-171">Een fout gegenereerd als u zowel de directory en de blob-namen, zoals opgeeft `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="14c4f-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="14c4f-173">Als u de standaard-container van het Hadoop-cluster met behulp van Azure Storage Explorer opent, ziet u de uitvoer van de Hive-query wordt weergegeven in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="14c4f-173">If you open the default container of the Hadoop cluster using Azure Storage Explorer, you can see the output of the Hive query as shown in the following figure.</span></span> <span data-ttu-id="14c4f-174">U kunt het filter (gemarkeerd met een rood kader) voor het ophalen van de blob met de opgegeven letters in namen alleen toepassen.</span><span class="sxs-lookup"><span data-stu-id="14c4f-174">You can apply the filter (highlighted by red box) to only retrieve the blob with specified letters in names.</span></span>

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="14c4f-176"><a name="hive-editor"></a> 2. Indienen van Hive-query's met de Hive-Editor</span><span class="sxs-lookup"><span data-stu-id="14c4f-176"><a name="hive-editor"></a> 2. Submit Hive queries with the Hive Editor</span></span>
<span data-ttu-id="14c4f-177">U kunt ook de Query-Console (Hive-Editor) gebruiken door een URL van het formulier *https://&#60; De naam van de Hadoop-cluster >.azurehdinsight.net/Home/HiveEditor* in een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="14c4f-177">You can also use the Query Console (Hive Editor) by entering a URL of the form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="14c4f-178">U moet zijn geregistreerd in de zien deze console en dus moet u uw hier Hadoop-cluster-referenties.</span><span class="sxs-lookup"><span data-stu-id="14c4f-178">You must be logged in the see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="14c4f-179"><a name="ps"></a> 3. Indienen van Hive-query's met Azure PowerShell-opdrachten</span><span class="sxs-lookup"><span data-stu-id="14c4f-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="14c4f-180">U kunt ook PowerShell gebruiken voor het indienen van Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="14c4f-180">You can also use PowerShell to submit Hive queries.</span></span> <span data-ttu-id="14c4f-181">Zie voor instructies [indienen Hive-taken met behulp van PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="14c4f-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="14c4f-182"><a name="create-tables"></a>Hive-database en tabellen maken</span><span class="sxs-lookup"><span data-stu-id="14c4f-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="14c4f-183">Het Hive-query's worden gedeeld in de [GitHub-opslagplaats](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) en van daaruit kan worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="14c4f-183">The Hive queries are shared in the [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="14c4f-184">Hier volgt de Hive-query waarmee een Hive-tabel.</span><span class="sxs-lookup"><span data-stu-id="14c4f-184">Here is the Hive query that creates a Hive table.</span></span>

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

<span data-ttu-id="14c4f-185">Hier volgen de beschrijvingen van de velden die u plug moet-- en andere configuraties:</span><span class="sxs-lookup"><span data-stu-id="14c4f-185">Here are the descriptions of the fields that you need to plug in and other configurations:</span></span>

* <span data-ttu-id="14c4f-186">**&#60; databasenaam >**: de naam van de database die u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="14c4f-186">**&#60;database name>**: the name of the database that you want to create.</span></span> <span data-ttu-id="14c4f-187">Als u alleen wilt gebruiken de standaard-database, de query *database maken...*  kunnen worden weggelaten.</span><span class="sxs-lookup"><span data-stu-id="14c4f-187">If you just want to use the default database, the query *create database...* can be omitted.</span></span>
* <span data-ttu-id="14c4f-188">**&#60; tabelnaam >**: de naam van de tabel die u wilt maken binnen de opgegeven database.</span><span class="sxs-lookup"><span data-stu-id="14c4f-188">**&#60;table name>**: the name of the table that you want to create within the specified database.</span></span> <span data-ttu-id="14c4f-189">Als u gebruiken de standaard-database wilt, de tabel rechtstreeks kan worden verwezen door *&#60; tabelnaam >* zonder &#60; databasenaam >.</span><span class="sxs-lookup"><span data-stu-id="14c4f-189">If you want to use the default database, the table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="14c4f-190">**&#60; veldscheidingsteken >**: het scheidingsteken op waarmee de velden in het gegevensbestand kunnen worden geüpload naar de Hive-tabel.</span><span class="sxs-lookup"><span data-stu-id="14c4f-190">**&#60;field separator>**: the separator that delimits fields in the data file to be uploaded to the Hive table.</span></span>
* <span data-ttu-id="14c4f-191">**&#60; regelscheiding >**: het scheidingsteken die regels in het gegevensbestand begrenst.</span><span class="sxs-lookup"><span data-stu-id="14c4f-191">**&#60;line separator>**: the separator that delimits lines in the data file.</span></span>
* <span data-ttu-id="14c4f-192">**&#60; opslaglocatie >**: de Azure-opslag-locatie voor het opslaan van de gegevens van Hive-tabellen.</span><span class="sxs-lookup"><span data-stu-id="14c4f-192">**&#60;storage location>**: the Azure storage location to save the data of Hive tables.</span></span> <span data-ttu-id="14c4f-193">Als u geen opgeeft *locatie &#60; opslaglocatie >*, tabellen en de database worden opgeslagen in *hive/datawarehouse/* map in de standaardcontainer van het cluster Hive standaard.</span><span class="sxs-lookup"><span data-stu-id="14c4f-193">If you do not specify *LOCATION &#60;storage location>*, the database and the tables are stored in *hive/warehouse/* directory in the default container of the Hive cluster by default.</span></span> <span data-ttu-id="14c4f-194">Als u de opslaglocatie opgeven wilt, is de opslaglocatie zich binnen de standaardcontainer voor de database en tabellen.</span><span class="sxs-lookup"><span data-stu-id="14c4f-194">If you want to specify the storage location, the storage location has to be within the default container for the database and tables.</span></span> <span data-ttu-id="14c4f-195">Deze locatie moet worden verwezen als locatie ten opzichte van de standaard-container van het cluster in de indeling van *' wasb: / / / &#60; map 1 > / "* of *' wasb: / / / &#60; map 1 > / &#60; map 2 > /'*, enzovoort. Nadat de query wordt uitgevoerd, worden de relatieve mappen in de standaardcontainer gemaakt.</span><span class="sxs-lookup"><span data-stu-id="14c4f-195">This location has to be referred as location relative to the default container of the cluster in the format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After the query is executed, the relative directories are created within the default container.</span></span>
* <span data-ttu-id="14c4f-196">**TBLPROPERTIES("SKIP.header.line.Count"="1")**: als het gegevensbestand een kopregel heeft, hebt u deze eigenschap toevoegen **aan het einde** van de *tabel maken* query.</span><span class="sxs-lookup"><span data-stu-id="14c4f-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If the data file has a header line, you have to add this property **at the end** of the *create table* query.</span></span> <span data-ttu-id="14c4f-197">Anders wordt de kopregel geladen als een record aan de tabel.</span><span class="sxs-lookup"><span data-stu-id="14c4f-197">Otherwise, the header line is loaded as a record to the table.</span></span> <span data-ttu-id="14c4f-198">Als het gegevensbestand geen een kopregel heeft, kan deze configuratie worden weggelaten in de query.</span><span class="sxs-lookup"><span data-stu-id="14c4f-198">If the data file does not have a header line, this configuration can be omitted in the query.</span></span>

## <span data-ttu-id="14c4f-199"><a name="load-data"></a>Laden van gegevens naar de Hive-tabellen</span><span class="sxs-lookup"><span data-stu-id="14c4f-199"><a name="load-data"></a>Load data to Hive tables</span></span>
<span data-ttu-id="14c4f-200">Hier volgt de Hive-query die gegevens in een Hive-tabel laadt.</span><span class="sxs-lookup"><span data-stu-id="14c4f-200">Here is the Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path to blob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="14c4f-201">**&#60; pad naar de blob-gegevens >**: als de blob-bestand wilt uploaden naar de Hive-tabel in de standaardcontainer van HDInsight Hadoop-cluster de *&#60; pad naar de blob-gegevens >* moet de indeling *' wasb: / / / &#60; directory in deze container > / &#60; blob-bestandsnaam >'*.</span><span class="sxs-lookup"><span data-stu-id="14c4f-201">**&#60;path to blob data>**: If the blob file to be uploaded to the Hive table is in the default container of the HDInsight Hadoop cluster, the *&#60;path to blob data>* should be in the format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="14c4f-202">De blob-bestand kan ook worden in een extra container van het HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="14c4f-202">The blob file can also be in an additional container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="14c4f-203">In dit geval *&#60; pad naar de blob-gegevens >* moet de indeling *' wasb: / / &#60; containernaam > @&#60; opslagaccountnaam >.blob.core.windows.net/ &#60; blob-bestandsnaam >'*.</span><span class="sxs-lookup"><span data-stu-id="14c4f-203">In this case, *&#60;path to blob data>* should be in the format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="14c4f-204">De blob-gegevens kunnen worden geüpload naar de Hive-tabel is in de standaardinstellingen of extra container van het opslagaccount voor het Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="14c4f-204">The blob data to be uploaded to Hive table has to be in the default or additional container of the storage account for the Hadoop cluster.</span></span> <span data-ttu-id="14c4f-205">Anders wordt de *gegevens laden* query klagen dat deze geen toegang de gegevens tot is mislukt.</span><span class="sxs-lookup"><span data-stu-id="14c4f-205">Otherwise, the *LOAD DATA* query fails complaining that it cannot access the data.</span></span>
  >
  >

## <span data-ttu-id="14c4f-206"><a name="partition-orc"></a>Onderwerpen over geavanceerde: gepartitioneerde tabel en archief Hive-gegevens in ORC-indeling</span><span class="sxs-lookup"><span data-stu-id="14c4f-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="14c4f-207">Als de gegevens te groot is, is partitioneren van de tabel nuttig voor query's die alleen moeten worden gescand van enkele partities van de tabel.</span><span class="sxs-lookup"><span data-stu-id="14c4f-207">If the data is large, partitioning the table is beneficial for queries that only need to scan a few partitions of the table.</span></span> <span data-ttu-id="14c4f-208">Bijvoorbeeld, kan men redelijkerwijs voor het partitioneren van de logboekgegevens van een website door datums.</span><span class="sxs-lookup"><span data-stu-id="14c4f-208">For instance, it is reasonable to partition the log data of a web site by dates.</span></span>

<span data-ttu-id="14c4f-209">Naast het partitioneren van Hive-tabellen, is het ook nuttig om de Hive-gegevens opslaat in de indeling geoptimaliseerd rij kolommen (ORC).</span><span class="sxs-lookup"><span data-stu-id="14c4f-209">In addition to partitioning Hive tables, it is also beneficial to store the Hive data in the Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="14c4f-210">Zie voor meer informatie over het ORC opmaak <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">met behulp van ORC-bestanden verbetert de prestaties wanneer Hive lezen, schrijven en verwerken van gegevens</a>.</span><span class="sxs-lookup"><span data-stu-id="14c4f-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="14c4f-211">Gepartitioneerde tabel</span><span class="sxs-lookup"><span data-stu-id="14c4f-211">Partitioned table</span></span>
<span data-ttu-id="14c4f-212">Hier volgt de Hive-query die een gepartitioneerde tabel maakt en gegevens worden geladen in de App.</span><span class="sxs-lookup"><span data-stu-id="14c4f-212">Here is the Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="14c4f-213">Tijdens het opvragen van gepartitioneerde tabellen, verdient het toevoegen van de voorwaarde van de partitie in de **begin** van de `where` component als dit verbetert de effectiviteit van aanzienlijk zoeken.</span><span class="sxs-lookup"><span data-stu-id="14c4f-213">When querying partitioned tables, it is recommended to add the partition condition in the **beginning** of the `where` clause as this improves the efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="14c4f-214"><a name="orc"></a>Hive-gegevens opslaat in ORC-indeling</span><span class="sxs-lookup"><span data-stu-id="14c4f-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="14c4f-215">U kan niet rechtstreeks gegevens uit blob-opslag laden in de Hive-tabellen die zijn opgeslagen in de ORC-indeling.</span><span class="sxs-lookup"><span data-stu-id="14c4f-215">You cannot directly load data from blob storage into Hive tables that is stored in the ORC format.</span></span> <span data-ttu-id="14c4f-216">Hier volgen de stappen die u moet uitvoeren om te laden van gegevens van Azure blobs voor Hive-tabellen die zijn opgeslagen in ORC-indeling.</span><span class="sxs-lookup"><span data-stu-id="14c4f-216">Here are the steps that the you need to take to load data from Azure blobs to Hive tables stored in ORC format.</span></span>

<span data-ttu-id="14c4f-217">Maken van een externe tabel **opgeslagen AS TEXTFILE** en laden van gegevens uit blob-opslag naar de tabel.</span><span class="sxs-lookup"><span data-stu-id="14c4f-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage to the table.</span></span>

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

        LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="14c4f-218">Een interne tabel maken met hetzelfde schema als de externe tabel in stap 1, met dezelfde veldscheidingsteken en het Hive-gegevens opslaat in de ORC-indeling.</span><span class="sxs-lookup"><span data-stu-id="14c4f-218">Create an internal table with the same schema as the external table in step 1, with the same field delimiter, and store the Hive data in the ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="14c4f-219">Selecteer de gegevens van de externe tabel in stap 1 en in de tabel ORC invoegen</span><span class="sxs-lookup"><span data-stu-id="14c4f-219">Select data from the external table in step 1 and insert into the ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="14c4f-220">Als de tabel TEXTFILE *&#60; databasenaam >. &#60; externe textfile tabelnaam >* partities in stap 3 heeft de `SELECT * FROM <database name>.<external textfile table name>` opdracht wordt de variabele partitie geselecteerd als een veld in de geretourneerde gegevensset.</span><span class="sxs-lookup"><span data-stu-id="14c4f-220">If the TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, the `SELECT * FROM <database name>.<external textfile table name>` command selects the partition variable as a field in the returned data set.</span></span> <span data-ttu-id="14c4f-221">Invoegen in de *&#60; databasenaam >. &#60; ORC-tabelnaam >* mislukt sinds *&#60; databasenaam >. &#60; ORC-tabelnaam >* heeft niet de partitie-variabele als een veld in het tabelschema.</span><span class="sxs-lookup"><span data-stu-id="14c4f-221">Inserting it into the *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have the partition variable as a field in the table schema.</span></span> <span data-ttu-id="14c4f-222">In dit geval moet u de velden die moeten worden ingevoegd in specifiek selecteren *&#60; databasenaam >. &#60; ORC-tabelnaam >* als volgt:</span><span class="sxs-lookup"><span data-stu-id="14c4f-222">In this case, you need to specifically select the fields to be inserted to *&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="14c4f-223">Het is veilig verwijderen de *&#60; externe textfile tabelnaam >* wanneer met behulp van de volgende query nadat alle gegevens is ingevoegd in *&#60; databasenaam >. &#60; ORC-tabelnaam >*:</span><span class="sxs-lookup"><span data-stu-id="14c4f-223">It is safe to drop the *&#60;external textfile table name>* when using the following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="14c4f-224">Na deze procedure uitvoert, moet u een tabel met gegevens in de klaar voor gebruik ORC-indeling hebben.</span><span class="sxs-lookup"><span data-stu-id="14c4f-224">After following this procedure, you should have a table with data in the ORC format ready to use.</span></span>  

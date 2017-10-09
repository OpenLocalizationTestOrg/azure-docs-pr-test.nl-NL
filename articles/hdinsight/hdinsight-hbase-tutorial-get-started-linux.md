---
title: aaaGet gestart met een voorbeeld van HBase op HDInsight - Azure | Microsoft Docs
description: Volg deze Apache HBase voorbeeld toostart met hadoop op HDInsight. Tabellen maken van Hallo HBase-shell en hierin zoeken met Hive.
keywords: hbase-opdracht, hbase-voorbeeld
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a><span data-ttu-id="db5d8-105">Aan de slag met een voorbeeld van Apache HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="db5d8-105">Get started with an Apache HBase example in HDInsight</span></span>

<span data-ttu-id="db5d8-106">Ontdek hoe toocreate een HBase-cluster in HDInsight, HBase-tabellen maken en query uitvoeren op tabellen met Hive.</span><span class="sxs-lookup"><span data-stu-id="db5d8-106">Learn how toocreate an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="db5d8-107">Zie [Overzicht van HDInsight HBase][hdinsight-hbase-overview] voor algemene informatie over HBase.</span><span class="sxs-lookup"><span data-stu-id="db5d8-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="db5d8-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="db5d8-108">Prerequisites</span></span>
<span data-ttu-id="db5d8-109">Voordat u probeert deze HBase-voorbeeld, hebt u de volgende items Hallo:</span><span class="sxs-lookup"><span data-stu-id="db5d8-109">Before you begin trying this HBase example, you must have hello following items:</span></span>

* <span data-ttu-id="db5d8-110">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="db5d8-110">**An Azure subscription**.</span></span> <span data-ttu-id="db5d8-111">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="db5d8-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="db5d8-112">[Secure Shell (SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="db5d8-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="db5d8-113">[curl](http://curl.haxx.se/download.html).</span><span class="sxs-lookup"><span data-stu-id="db5d8-113">[curl](http://curl.haxx.se/download.html).</span></span>

## <a name="create-hbase-cluster"></a><span data-ttu-id="db5d8-114">Een HBase-cluster maken</span><span class="sxs-lookup"><span data-stu-id="db5d8-114">Create HBase cluster</span></span>
<span data-ttu-id="db5d8-115">Hallo volgende procedure maakt gebruik van een Azure Resource Manager-sjabloon toocreate een versie 3.4 op basis van Linux HBase-cluster en Hallo afhankelijke Azure Storage-standaardaccount.</span><span class="sxs-lookup"><span data-stu-id="db5d8-115">hello following procedure uses an Azure Resource Manager template toocreate a version 3.4 Linux-based HBase cluster and hello dependent default Azure Storage account.</span></span> <span data-ttu-id="db5d8-116">Zie toounderstand Hallo parameters die worden gebruikt in de procedure Hallo en andere methoden voor het maken van cluster [maken Linux gebaseerde Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="db5d8-116">toounderstand hello parameters used in hello procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="db5d8-117">Klik op Hallo installatiekopie tooopen Hallo sjabloon in hello Azure-portal te volgen.</span><span class="sxs-lookup"><span data-stu-id="db5d8-117">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="db5d8-118">Hallo-sjabloon bevindt zich in een openbare blob-container.</span><span class="sxs-lookup"><span data-stu-id="db5d8-118">hello template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="db5d8-119">Van Hallo **aangepaste implementatie** blade Voer Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="db5d8-119">From hello **Custom deployment** blade, enter hello following values:</span></span>
   
   * <span data-ttu-id="db5d8-120">**Abonnement**: Selecteer uw Azure-abonnement dat is gebruikt toocreate Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="db5d8-120">**Subscription**: Select your Azure subscription that is used toocreate hello cluster.</span></span>
   * <span data-ttu-id="db5d8-121">**Resourcegroep**: maak een Azure-resourcebeheergroep of gebruik een bestaande.</span><span class="sxs-lookup"><span data-stu-id="db5d8-121">**Resource group**: Create an Azure Resource Management group or use an existing one.</span></span>
   * <span data-ttu-id="db5d8-122">**Locatie**: locatie van resourcegroep Hallo Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="db5d8-122">**Location**: Specify hello location of hello resource group.</span></span> 
   * <span data-ttu-id="db5d8-123">**Clusternaam**: Voer een naam voor Hallo HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="db5d8-123">**ClusterName**: Enter a name for hello HBase cluster.</span></span>
   * <span data-ttu-id="db5d8-124">**Cluster-aanmeldingsnaam en wachtwoord**: Hallo standaardaanmeldnaam is **admin**.</span><span class="sxs-lookup"><span data-stu-id="db5d8-124">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="db5d8-125">**SSH-gebruikersnaam en wachtwoord**: de standaardgebruikersnaam Hallo **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="db5d8-125">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="db5d8-126">U kunt de naam wijzigen.</span><span class="sxs-lookup"><span data-stu-id="db5d8-126">You can rename it.</span></span>
     
     <span data-ttu-id="db5d8-127">Andere parameters zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="db5d8-127">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="db5d8-128">Elk cluster is afhankelijk van een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="db5d8-128">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="db5d8-129">Nadat u een cluster hebt verwijderd, behoudt Hallo gegevens in Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="db5d8-129">After you delete a cluster, hello data retains in hello storage account.</span></span> <span data-ttu-id="db5d8-130">Hallo clusternaam van het standaardopslagaccount is Hallo naam waaraan 'store' is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="db5d8-130">hello cluster default storage account name is hello cluster name with "store" appended.</span></span> <span data-ttu-id="db5d8-131">Deze is vastgelegd in de sectie met sjabloonvariabelen Hallo.</span><span class="sxs-lookup"><span data-stu-id="db5d8-131">It is hardcoded in hello template variables section.</span></span>
3. <span data-ttu-id="db5d8-132">Selecteer **ik ga akkoord toohello voorwaarden bovengenoemde**, en klik vervolgens op **aankoop**.</span><span class="sxs-lookup"><span data-stu-id="db5d8-132">Select **I agree toohello terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="db5d8-133">Het duurt ongeveer 20 minuten toocreate een cluster.</span><span class="sxs-lookup"><span data-stu-id="db5d8-133">It takes about 20 minutes toocreate a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="db5d8-134">Nadat een HBase-cluster wordt verwijderd, kunt u een ander HBase-cluster maken met behulp van Hallo dezelfde standaard blob-container.</span><span class="sxs-lookup"><span data-stu-id="db5d8-134">After an HBase cluster is deleted, you can create another HBase cluster by using hello same default blob container.</span></span> <span data-ttu-id="db5d8-135">het nieuwe cluster Hallo hervat Hallo HBase-tabellen die u hebt gemaakt in het oorspronkelijke cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="db5d8-135">hello new cluster picks up hello HBase tables you created in hello original cluster.</span></span> <span data-ttu-id="db5d8-136">tooavoid inconsistenties, we raden aan Hallo HBase-tabellen uit te schakelen voordat u het Hallo-cluster verwijderen.</span><span class="sxs-lookup"><span data-stu-id="db5d8-136">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="db5d8-137">Tabellen maken en gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="db5d8-137">Create tables and insert data</span></span>
<span data-ttu-id="db5d8-138">U kunt SSH tooconnect tooHBase clusters gebruiken en gebruik vervolgens de HBase-Shell toocreate HBase-tabellen, gegevens en gegevens opvragen invoegen.</span><span class="sxs-lookup"><span data-stu-id="db5d8-138">You can use SSH tooconnect tooHBase clusters and then use HBase Shell toocreate HBase tables, insert data, and query data.</span></span> <span data-ttu-id="db5d8-139">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="db5d8-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="db5d8-140">Gegevens worden weergegeven voor de meeste mensen in tabelvorm Hallo:</span><span class="sxs-lookup"><span data-stu-id="db5d8-140">For most people, data appears in hello tabular format:</span></span>

![Tabelgegevens in HDInsight HBase][img-hbase-sample-data-tabular]

<span data-ttu-id="db5d8-142">In HBase (een implementatie van BigTable) lijkt hello dezelfde gegevens:</span><span class="sxs-lookup"><span data-stu-id="db5d8-142">In HBase (an implementation of BigTable), hello same data looks like:</span></span>

![BigTable-gegevens in HDInsight HBase][img-hbase-sample-data-bigtable]


<span data-ttu-id="db5d8-144">**toouse hello HBase-shell**</span><span class="sxs-lookup"><span data-stu-id="db5d8-144">**toouse hello HBase shell**</span></span>

1. <span data-ttu-id="db5d8-145">Voer Hallo na HBase-opdracht uit in SSH:</span><span class="sxs-lookup"><span data-stu-id="db5d8-145">From SSH, run hello following HBase command:</span></span>
   
    ```bash
    hbase shell
    ```

2. <span data-ttu-id="db5d8-146">Maak een HBase met twee kolomfamilies:</span><span class="sxs-lookup"><span data-stu-id="db5d8-146">Create an HBase with two-column families:</span></span>

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. <span data-ttu-id="db5d8-147">Voeg enkele gegeven in:</span><span class="sxs-lookup"><span data-stu-id="db5d8-147">Insert some data:</span></span>
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![HDInsight Hadoop HBase-shell][img-hbase-shell]
4. <span data-ttu-id="db5d8-149">Een enkel rij ophalen</span><span class="sxs-lookup"><span data-stu-id="db5d8-149">Get a single row</span></span>
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    <span data-ttu-id="db5d8-150">U ziet Hallo dezelfde resultaten als het gebruik van de scanopdracht Hallo omdat er slechts één rij.</span><span class="sxs-lookup"><span data-stu-id="db5d8-150">You shall see hello same results as using hello scan command because there is only one row.</span></span>
   
    <span data-ttu-id="db5d8-151">Zie voor meer informatie over Hallo HBase-tabelschema [inleiding tooHBase schemaontwerp][hbase-schema].</span><span class="sxs-lookup"><span data-stu-id="db5d8-151">For more information about hello HBase table schema, see [Introduction tooHBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="db5d8-152">Raadpleeg de [Snelzoekgids voor Apache HBase][hbase-quick-start] voor meer HBase-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="db5d8-152">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="db5d8-153">Hallo-shell afsluiten</span><span class="sxs-lookup"><span data-stu-id="db5d8-153">Exit hello shell</span></span>
   
    ```hbaseshell
    exit
    ```

<span data-ttu-id="db5d8-154">**toobulk load gegevens in HBase-tabel met contacten Hallo**</span><span class="sxs-lookup"><span data-stu-id="db5d8-154">**toobulk load data into hello contacts HBase table**</span></span>

<span data-ttu-id="db5d8-155">U kunt in HBase verschillende methoden gebruiken om gegevens in tabellen te laden.</span><span class="sxs-lookup"><span data-stu-id="db5d8-155">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="db5d8-156">Zie [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load) (Bulkgsgewijs laden) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="db5d8-156">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="db5d8-157">Een voorbeeld van een gegevensbestand is te vinden in een openbare Azure Blob-container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span><span class="sxs-lookup"><span data-stu-id="db5d8-157">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="db5d8-158">Hallo-inhoud van het gegevensbestand Hallo is:</span><span class="sxs-lookup"><span data-stu-id="db5d8-158">hello content of hello data file is:</span></span>

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

<span data-ttu-id="db5d8-159">U kunt desgewenst een tekstbestand maken en uploaden Hallo bestand tooyour eigen opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="db5d8-159">You can optionally create a text file and upload hello file tooyour own storage account.</span></span> <span data-ttu-id="db5d8-160">Zie voor instructies Hallo [gegevens voor Hadoop-taken in HDInsight uploaden][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="db5d8-160">For hello instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="db5d8-161">Deze procedure maakt gebruik van Hallo contactpersonen HBase-tabel die u hebt gemaakt in de laatste procedure Hallo.</span><span class="sxs-lookup"><span data-stu-id="db5d8-161">This procedure uses hello Contacts HBase table you have created in hello last procedure.</span></span>
> 

1. <span data-ttu-id="db5d8-162">Uitvoeren vanuit SSH Hallo opdracht tootransform Hallo gegevens bestand tooStoreFiles en op te slaan op een relatief pad is opgegeven door Dimporttsv.bulk.output te volgen.</span><span class="sxs-lookup"><span data-stu-id="db5d8-162">From SSH, run hello following command tootransform hello data file tooStoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span></span>  <span data-ttu-id="db5d8-163">Als u zich in HBase-Shell, gebruikt u Hallo afsluiten opdracht tooexit.</span><span class="sxs-lookup"><span data-stu-id="db5d8-163">If you are in HBase Shell, use hello exit command tooexit.</span></span>

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. <span data-ttu-id="db5d8-164">Voer Hallo volgende opdracht tooupload Hallo gegevens uit/storedatafileoutput toohello HBase-tabel:</span><span class="sxs-lookup"><span data-stu-id="db5d8-164">Run hello following command tooupload hello data from  /example/data/storeDataFileOutput toohello HBase table:</span></span>
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. <span data-ttu-id="db5d8-165">U kunt Hallo HBase-shell openen en Hallo scan opdracht toolist Hallo tabelinhoud gebruiken.</span><span class="sxs-lookup"><span data-stu-id="db5d8-165">You can open hello HBase shell, and use hello scan command toolist hello table content.</span></span>

## <a name="use-hive-tooquery-hbase"></a><span data-ttu-id="db5d8-166">Gebruik Hive tooquery HBase</span><span class="sxs-lookup"><span data-stu-id="db5d8-166">Use Hive tooquery HBase</span></span>

<span data-ttu-id="db5d8-167">Met Hive kunt u een query uitvoeren op de gegevens in HBase-tabellen.</span><span class="sxs-lookup"><span data-stu-id="db5d8-167">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="db5d8-168">In deze sectie maakt u een Hive-tabel die wordt toegewezen toohello HBase-tabel en gebruikt deze tooquery Hallo gegevens in uw HBase-tabel.</span><span class="sxs-lookup"><span data-stu-id="db5d8-168">In this section, you create a Hive table that maps toohello HBase table and uses it tooquery hello data in your HBase table.</span></span>

1. <span data-ttu-id="db5d8-169">Open **PuTTY**, en maak verbinding toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="db5d8-169">Open **PuTTY**, and connect toohello cluster.</span></span>  <span data-ttu-id="db5d8-170">Zie Hallo-instructies in de vorige procedure Hallo.</span><span class="sxs-lookup"><span data-stu-id="db5d8-170">See hello instructions in hello previous procedure.</span></span>
2. <span data-ttu-id="db5d8-171">Gebruik van Hallo SSH-sessie, Hallo opdracht toostart Beeline te volgen:</span><span class="sxs-lookup"><span data-stu-id="db5d8-171">From hello SSH session, use hello following command toostart Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="db5d8-172">Zie voor meer informatie over Beeline [Hive gebruiken met Hadoop in HDInsight met Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="db5d8-172">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
       
3. <span data-ttu-id="db5d8-173">Voer Hallo volgende HiveQL-script toocreate een Hive-tabel die is toegewezen toohello HBase-tabel.</span><span class="sxs-lookup"><span data-stu-id="db5d8-173">Run hello following HiveQL script  toocreate a Hive table that maps toohello HBase table.</span></span> <span data-ttu-id="db5d8-174">Zorg ervoor dat u hebt gemaakt dat Hallo voorbeeldtabel waarnaar eerder in deze zelfstudie Hallo HBase-shell met voordat u deze instructie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="db5d8-174">Make sure that you have created hello sample table referenced earlier in this tutorial by using hello HBase shell before you run this statement.</span></span>

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. <span data-ttu-id="db5d8-175">Hallo volgende HiveQL-script tooquery Hallo gegevens in HBase-tabel Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="db5d8-175">Run hello following HiveQL script tooquery hello data in hello HBase table:</span></span>

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="db5d8-176">HBase REST API's gebruiken met Curl</span><span class="sxs-lookup"><span data-stu-id="db5d8-176">Use HBase REST APIs using Curl</span></span>

<span data-ttu-id="db5d8-177">Hallo REST API is beveiligd via [basisverificatie](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="db5d8-177">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="db5d8-178">U moet aanvragen altijd maken met behulp van beveiligde HTTP (HTTPS) toohelp ervoor te zorgen dat uw referenties veilig toohello server worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="db5d8-178">You shall always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>

2. <span data-ttu-id="db5d8-179">Gebruik Hallo opdracht toolist Hallo bestaande HBase-tabellen te volgen:</span><span class="sxs-lookup"><span data-stu-id="db5d8-179">Use hello following command toolist hello existing HBase tables:</span></span>

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. <span data-ttu-id="db5d8-180">Gebruik Hallo opdracht toocreate een nieuwe HBase-tabel met twee kolomfamilies te volgen:</span><span class="sxs-lookup"><span data-stu-id="db5d8-180">Use hello following command toocreate a new HBase table with two-column families:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    <span data-ttu-id="db5d8-181">Hallo-schema is opgegeven in Hallo JSon-indeling.</span><span class="sxs-lookup"><span data-stu-id="db5d8-181">hello schema is provided in hello JSon format.</span></span>
4. <span data-ttu-id="db5d8-182">Gebruik Hallo volgende opdracht tooinsert sommige gegevens:</span><span class="sxs-lookup"><span data-stu-id="db5d8-182">Use hello following command tooinsert some data:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    <span data-ttu-id="db5d8-183">U moet base64 Hallo opgegeven waarden in Hallo -d switch coderen.</span><span class="sxs-lookup"><span data-stu-id="db5d8-183">You must base64 encode hello values specified in hello -d switch.</span></span> <span data-ttu-id="db5d8-184">In het Hallo-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="db5d8-184">In hello example:</span></span>
   
   * <span data-ttu-id="db5d8-185">MTAwMA==: 1000</span><span class="sxs-lookup"><span data-stu-id="db5d8-185">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="db5d8-186">UGVyc29uYWw6TmFtZQ==: Persoonlijk:Naam</span><span class="sxs-lookup"><span data-stu-id="db5d8-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="db5d8-187">Sm9obiBEb2xl: Joep Davids</span><span class="sxs-lookup"><span data-stu-id="db5d8-187">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="db5d8-188">[False rijsleutel](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) tooinsert, kunt u meerdere waarden voor (batch).</span><span class="sxs-lookup"><span data-stu-id="db5d8-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you tooinsert multiple (batched) values.</span></span>
5. <span data-ttu-id="db5d8-189">Gebruik Hallo opdracht tooget een rij te volgen:</span><span class="sxs-lookup"><span data-stu-id="db5d8-189">Use hello following command tooget a row:</span></span>
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

<span data-ttu-id="db5d8-190">Zie [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest) (Snelzoekgids voor Apache HBase) voor meer informatie over HBase REST.</span><span class="sxs-lookup"><span data-stu-id="db5d8-190">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

> [!NOTE]
> <span data-ttu-id="db5d8-191">Thrift wordt niet ondersteund door HBase in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="db5d8-191">Thrift is not supported by HBase in HDInsight.</span></span>
>
> <span data-ttu-id="db5d8-192">Wanneer u Curl of andere REST-communicatie met WebHCat, moet u Hallo aanvragen verifiëren door het Hallo-gebruikersnaam en wachtwoord voor Hallo HDInsight Clusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="db5d8-192">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="db5d8-193">Als onderdeel van Hallo Uniform Resource Identifier (URI) toosend Hallo aanvragen toohello server gebruikt, moet u de clusternaam hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="db5d8-193">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server:</span></span>
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    <span data-ttu-id="db5d8-194">U ontvangt een reactie vergelijkbaar toohello antwoord te volgen:</span><span class="sxs-lookup"><span data-stu-id="db5d8-194">You should receive a response similar toohello following response:</span></span>
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a><span data-ttu-id="db5d8-195">De clusterstatus controleren</span><span class="sxs-lookup"><span data-stu-id="db5d8-195">Check cluster status</span></span>
<span data-ttu-id="db5d8-196">HBase in HDInsight wordt geleverd met een webgebruikersinterface voor het bewaken van clusters.</span><span class="sxs-lookup"><span data-stu-id="db5d8-196">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="db5d8-197">Hallo Webgebruikersinterface gebruikt, kunt u statistieken of informatie over regio's aanvragen.</span><span class="sxs-lookup"><span data-stu-id="db5d8-197">Using hello Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="db5d8-198">**tooaccess hello HBase Master UI**</span><span class="sxs-lookup"><span data-stu-id="db5d8-198">**tooaccess hello HBase Master UI**</span></span>

1. <span data-ttu-id="db5d8-199">Meld u aan bij Hallo Hallo Ambari-Webgebruikersinterface op https://&lt;Clustername >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="db5d8-199">Sign into hello hello Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="db5d8-200">Klik op **HBase** in het linkermenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="db5d8-200">Click **HBase** from hello left menu.</span></span>
3. <span data-ttu-id="db5d8-201">Klik op **snelle koppelingen** op Hallo bovenaan pagina hello, punt toohello actieve Zookeeper knooppunt koppeling, en klik vervolgens op **HBase Master UI**.</span><span class="sxs-lookup"><span data-stu-id="db5d8-201">Click **Quick links** on hello top of hello page, point toohello active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="db5d8-202">Hallo gebruikersinterface in een ander browsertabblad wordt geopend:</span><span class="sxs-lookup"><span data-stu-id="db5d8-202">hello UI is opened in another browser tab:</span></span>

  ![HDInsight HBase HMaster-interface](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="db5d8-204">Hallo HBase Master UI bevat Hallo uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="db5d8-204">hello HBase Master UI contains hello following sections:</span></span>

  - <span data-ttu-id="db5d8-205">regioservers</span><span class="sxs-lookup"><span data-stu-id="db5d8-205">region servers</span></span>
  - <span data-ttu-id="db5d8-206">back-upmasters</span><span class="sxs-lookup"><span data-stu-id="db5d8-206">backup masters</span></span>
  - <span data-ttu-id="db5d8-207">tabellen</span><span class="sxs-lookup"><span data-stu-id="db5d8-207">tables</span></span>
  - <span data-ttu-id="db5d8-208">taken</span><span class="sxs-lookup"><span data-stu-id="db5d8-208">tasks</span></span>
  - <span data-ttu-id="db5d8-209">softwarekenmerken</span><span class="sxs-lookup"><span data-stu-id="db5d8-209">software attributes</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="db5d8-210">Hallo-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="db5d8-210">Delete hello cluster</span></span>
<span data-ttu-id="db5d8-211">tooavoid inconsistenties, we raden aan Hallo HBase-tabellen uit te schakelen voordat u het Hallo-cluster verwijderen.</span><span class="sxs-lookup"><span data-stu-id="db5d8-211">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="db5d8-212">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="db5d8-212">Troubleshoot</span></span>

<span data-ttu-id="db5d8-213">Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="db5d8-213">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="db5d8-214">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="db5d8-214">Next steps</span></span>
<span data-ttu-id="db5d8-215">In dit artikel hebt u geleerd hoe toocreate een HBase-cluster en hoe toocreate tabellen en weergaven gegevens in deze tabellen vanuit Hallo Hallo HBase-shell.</span><span class="sxs-lookup"><span data-stu-id="db5d8-215">In this article, you learned how toocreate an HBase cluster and how toocreate tables and view hello data in those tables from hello HBase shell.</span></span> <span data-ttu-id="db5d8-216">U hebt ook geleerd hoe toouse een Hive query uitvoeren op gegevens in HBase-tabellen en hoe toouse HBase C# REST API's toocreate Hallo een HBase-tabel en gegevens ophalen uit de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="db5d8-216">You also learned how toouse a Hive query on data in HBase tables and how toouse hello HBase C# REST APIs toocreate an HBase table and retrieve data from hello table.</span></span>

<span data-ttu-id="db5d8-217">toolearn meer, Zie:</span><span class="sxs-lookup"><span data-stu-id="db5d8-217">toolearn more, see:</span></span>

* <span data-ttu-id="db5d8-218">[Overzicht van HDInsight HBase][hdinsight-hbase-overview]: HBase is een Apache, open-source NoSQL-database op basis van Hadoop. HBase biedt willekeurige toegang en een sterke consistentie voor grote hoeveelheden ongestructureerde en semigestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="db5d8-218">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png

---
title: aaaUse Hadoop Hive met Curl in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe tooremotely indienen Pig tooHDInsight met Curl taken.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="93696-103">Hive-query's uitvoeren met Hadoop in HDInsight met behulp van REST</span><span class="sxs-lookup"><span data-stu-id="93696-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="93696-104">Meer informatie over hoe toouse hello WebHCat REST-API toorun Hive query's met Hadoop op Azure HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="93696-104">Learn how toouse hello WebHCat REST API toorun Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="93696-105">[CURL](http://curl.haxx.se/) gebruikte toodemonstrate hoe u met HDInsight werken kunt met behulp van onbewerkte HTTP-aanvragen is.</span><span class="sxs-lookup"><span data-stu-id="93696-105">[Curl](http://curl.haxx.se/) is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="93696-106">Hallo [jq](http://stedolan.github.io/jq/) hulpprogramma gebruikte tooprocess Hallo JSON-gegevens geretourneerd van de REST-aanvragen is.</span><span class="sxs-lookup"><span data-stu-id="93696-106">hello [jq](http://stedolan.github.io/jq/) utility is used tooprocess hello JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="93696-107">Als u al bekend bent met Hadoop op basis van Linux-servers gebruiken, maar nieuwe tooHDInsight zijn, raadpleegt u Hallo [wat u moet tooknow over Hadoop op Linux gebaseerde HDInsight](hdinsight-hadoop-linux-information.md) document.</span><span class="sxs-lookup"><span data-stu-id="93696-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see hello [What you need tooknow about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="93696-108"><a id="curl"></a>Hive-query's uitvoeren</span><span class="sxs-lookup"><span data-stu-id="93696-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="93696-109">Wanneer u cURL of andere REST-communicatie met WebHCat, moet u Hallo aanvragen verifiëren door het Hallo-gebruikersnaam en wachtwoord voor Hallo HDInsight Clusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="93696-109">When using cURL or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="93696-110">Hallo-opdrachten in deze sectie, vervangt u **gebruikersnaam** met Hallo gebruiker tooauthenticate toohello cluster en vervang **wachtwoord** met wachtwoord voor gebruikersaccount Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="93696-110">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="93696-111">Vervang **CLUSTERNAME** met Hallo-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="93696-111">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="93696-112">Hallo REST API is beveiligd via [basisverificatie](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="93696-112">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="93696-113">toohelp ervoor te zorgen dat uw referenties veilig toohello server verzonden, altijd aanvragen indienen via HTTP Secure (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="93696-113">toohelp ensure that your credentials are securely sent toohello server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="93696-114">Gebruik vanaf een opdrachtregel Hallo opdracht tooverify dat u verbinding tooyour HDInsight-cluster maken kunt te volgen:</span><span class="sxs-lookup"><span data-stu-id="93696-114">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="93696-115">U ontvangt een reactie vergelijkbaar toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="93696-115">You receive a response similar toohello following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="93696-116">Hallo-parameters die worden gebruikt in deze opdracht zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="93696-116">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="93696-117">**-u** -Hallo-gebruikersnaam en wachtwoord tooauthenticate Hallo aanvraag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="93696-117">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="93696-118">**-G** -geeft aan dat deze aanvraag een GET-bewerking.</span><span class="sxs-lookup"><span data-stu-id="93696-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="93696-119">Hallo begin van het Hallo-URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is dezelfde Hallo voor alle aanvragen.</span><span class="sxs-lookup"><span data-stu-id="93696-119">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="93696-120">Hallo-pad, **/status**, geeft aan dat verzoek Hallo tooreturn status WebHCat (ook wel bekend als Templeton) voor Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="93696-120">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> <span data-ttu-id="93696-121">U kunt ook Hallo-versie van Hive met behulp van de volgende opdracht Hallo aanvragen:</span><span class="sxs-lookup"><span data-stu-id="93696-121">You can also request hello version of Hive by using hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="93696-122">Deze aanvraag retourneert een reactie vergelijkbaar toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="93696-122">This request returns a response similar toohello following text:</span></span>

       <span data-ttu-id="93696-123">{{'module': 'hive', 'versie': "0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="93696-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="93696-124">Gebruik Hallo na een tabel met de naam toocreate **log4jLogs**:</span><span class="sxs-lookup"><span data-stu-id="93696-124">Use hello following toocreate a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="93696-125">Hallo parameters voor deze aanvraag te volgen:</span><span class="sxs-lookup"><span data-stu-id="93696-125">hello following parameters used with this request:</span></span>

   * <span data-ttu-id="93696-126">**-d** - sinds `-G` niet wordt gebruikt, Hallo aanvraag standaard toohello POST-methode.</span><span class="sxs-lookup"><span data-stu-id="93696-126">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="93696-127">`-d`Hiermee geeft u Hallo waarden die worden verzonden met Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="93696-127">`-d` specifies hello data values that are sent with hello request.</span></span>

     * <span data-ttu-id="93696-128">**User.name** -Hallo-gebruiker die het Hallo-opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="93696-128">**user.name** - hello user that is running hello command.</span></span>
     * <span data-ttu-id="93696-129">**uitvoeren van** -HiveQL-instructies tooexecute Hallo.</span><span class="sxs-lookup"><span data-stu-id="93696-129">**execute** - hello HiveQL statements tooexecute.</span></span>
     * <span data-ttu-id="93696-130">**statusdir** -Hallo-map die de status voor deze taak Hallo naar worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="93696-130">**statusdir** - hello directory that hello status for this job is written to.</span></span>

     <span data-ttu-id="93696-131">Deze instructies uitvoeren Hallo volgende acties:</span><span class="sxs-lookup"><span data-stu-id="93696-131">These statements perform hello following actions:</span></span>
   * <span data-ttu-id="93696-132">**DROP TABLE** -als Hallo tabel al bestaat, wordt deze verwijderd.</span><span class="sxs-lookup"><span data-stu-id="93696-132">**DROP TABLE** - If hello table already exists, it is deleted.</span></span>
   * <span data-ttu-id="93696-133">**EXTERNE tabel maken** -maakt een nieuwe 'extern' tabel in Hive.</span><span class="sxs-lookup"><span data-stu-id="93696-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="93696-134">Alleen de tabeldefinitie Hallo opslaan externe tabellen in Hive.</span><span class="sxs-lookup"><span data-stu-id="93696-134">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="93696-135">Hallo-gegevens in de oorspronkelijke locatie Hallo gelaten.</span><span class="sxs-lookup"><span data-stu-id="93696-135">hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="93696-136">Externe tabellen moeten worden gebruikt wanneer u van plan Hallo onderliggende gegevens toobe bijgewerkt door een externe bron bent.</span><span class="sxs-lookup"><span data-stu-id="93696-136">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="93696-137">Bijvoorbeeld, een uploadproces geautomatiseerde gegevens of een andere MapReduce-bewerking.</span><span class="sxs-lookup"><span data-stu-id="93696-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="93696-138">Verwijderen van een externe tabel komt **niet** Hallo gegevens alleen Hallo tabeldefinitie kunt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="93696-138">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="93696-139">**INDELING van de rij** : hoe Hallo gegevens zijn opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="93696-139">**ROW FORMAT** - How hello data is formatted.</span></span> <span data-ttu-id="93696-140">Hallo-velden in elk logboek worden gescheiden door een spatie.</span><span class="sxs-lookup"><span data-stu-id="93696-140">hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="93696-141">**AS TEXTFILE locatie opgeslagen** - Hallo gegevens worden opgeslagen (directory Hallo bijvoorbeeld/gegevens) en dat deze is opgeslagen als tekst.</span><span class="sxs-lookup"><span data-stu-id="93696-141">**STORED AS TEXTFILE LOCATION** - Where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="93696-142">**Selecteer** -selecteert een telling van alle rijen waarin kolom **t4** Hallo waarde bevat **[fout]**.</span><span class="sxs-lookup"><span data-stu-id="93696-142">**SELECT** - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="93696-143">Deze instructie retourneert een waarde van **3** omdat er zijn drie rijen met deze waarde.</span><span class="sxs-lookup"><span data-stu-id="93696-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="93696-144">U ziet dat Hallo spaties tussen HiveQL-instructies worden vervangen door Hallo `+` gebruikt in combinatie met Curl teken.</span><span class="sxs-lookup"><span data-stu-id="93696-144">Notice that hello spaces between HiveQL statements are replaced by hello `+` character when used with Curl.</span></span> <span data-ttu-id="93696-145">Tussen aanhalingstekens waarden met een spatie, zoals het Hallo-scheidingsteken mag niet worden vervangen door `+`.</span><span class="sxs-lookup"><span data-stu-id="93696-145">Quoted values that contain a space, such as hello delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="93696-146">**INPUT__FILE__NAME zoals '% 25.log'** - deze instructie limieten Hallo tooonly gebruik zoekbestanden eindigt op. log.</span><span class="sxs-lookup"><span data-stu-id="93696-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits hello search tooonly use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="93696-147">Hallo `%25` is Hallo URL gecodeerde vorm van %, waardoor u Hallo werkelijke conditie `like '%.log'`.</span><span class="sxs-lookup"><span data-stu-id="93696-147">hello `%25` is hello URL encoded form of %, so hello actual condition is `like '%.log'`.</span></span> <span data-ttu-id="93696-148">Hallo % heeft toobe URL gecodeerd, zoals dit beschouwd als een speciaal teken in URL's.</span><span class="sxs-lookup"><span data-stu-id="93696-148">hello % has toobe URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="93696-149">Met deze opdracht moet een taak-ID die gebruikt toocheck Hallo status van Hallo taak worden kan retourneren.</span><span class="sxs-lookup"><span data-stu-id="93696-149">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

       <span data-ttu-id="93696-150">{{'id': "job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="93696-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="93696-151">toocheck Hallo status van taak hello, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="93696-151">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="93696-152">Vervang **JOBID** met Hallo-waarde geretourneerd in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="93696-152">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="93696-153">Bijvoorbeeld, als hello retourneert de waarde is `{"id":"job_1415651640909_0026"}`, klikt u vervolgens **JOBID** zou `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="93696-153">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="93696-154">Als het Hallo-taak is voltooid, is het Hallo-status **geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="93696-154">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="93696-155">Deze aanvraag Curl retourneert een notatie JSON (JavaScript Object)-document met informatie over het Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="93696-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job.</span></span> <span data-ttu-id="93696-156">Jq wordt gebruikt tooretrieve Hallo alleen statuswaarde.</span><span class="sxs-lookup"><span data-stu-id="93696-156">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="93696-157">Zodra het Hallo-status van taak hello te is gewijzigd**geslaagd**, kunt u resultaten van de taak Hallo Hallo ophalen uit Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="93696-157">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="93696-158">Hallo `statusdir` parameter doorgegeven aan Hallo query bevat Hallo locatie van het uitvoerbestand Hallo; in dit geval **voorbeeld/curl**.</span><span class="sxs-lookup"><span data-stu-id="93696-158">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="93696-159">Dit adres Hallo uitvoer opslaat in Hallo **voorbeeld/curl** map in het Hallo-clusters standaard opslag.</span><span class="sxs-lookup"><span data-stu-id="93696-159">This address stores hello output in hello **example/curl** directory in hello clusters default storage.</span></span>

    <span data-ttu-id="93696-160">U kunt de lijst en deze bestanden downloaden met behulp van Hallo [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="93696-160">You can list and download these files by using hello [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="93696-161">Zie voor meer informatie over het gebruik van Azure CLI Hallo met Azure Storage Hallo [2.0 voor Azure CLI gebruiken met Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span><span class="sxs-lookup"><span data-stu-id="93696-161">For more information on using hello Azure CLI with Azure Storage, see hello [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="93696-162">Gebruik Hallo na toocreate instructies een nieuwe 'interne' tabel met de naam **foutenlogboeken**:</span><span class="sxs-lookup"><span data-stu-id="93696-162">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="93696-163">Deze instructies uitvoeren Hallo volgende acties:</span><span class="sxs-lookup"><span data-stu-id="93696-163">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="93696-164">**MAKEN van tabel als niet bestaat** -maakt een tabel, als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="93696-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="93696-165">Deze instructie maakt u een interne tabel die is opgeslagen in Hallo Hive-datawarehouse en volledig wordt beheerd door Hive.</span><span class="sxs-lookup"><span data-stu-id="93696-165">This statement creates an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="93696-166">In tegenstelling tot externe tabellen verwijdert de Hallo onderliggende gegevens ook een interne tabel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="93696-166">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="93696-167">**OPGESLAGEN AS ORC** -Hallo-gegevens opslaat in geoptimaliseerd rij kolommen (ORC)-indeling.</span><span class="sxs-lookup"><span data-stu-id="93696-167">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="93696-168">ORC is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.</span><span class="sxs-lookup"><span data-stu-id="93696-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="93696-169">**INSERT OVERSCHRIJVEN... Selecteer** -rijen uit Hallo geselecteerd **log4jLogs** tabel met **[fout]**, en vervolgens voegt gegevens in Hallo Hallo **foutenlogboeken** tabel.</span><span class="sxs-lookup"><span data-stu-id="93696-169">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>
   * <span data-ttu-id="93696-170">**Selecteer** -selecteert alle rijen uit Hallo nieuwe **foutenlogboeken** tabel.</span><span class="sxs-lookup"><span data-stu-id="93696-170">**SELECT** - Selects all rows from hello new **errorLogs** table.</span></span>

6. <span data-ttu-id="93696-171">Gebruik Hallo taak-ID toocheck Hallo status van Hallo taak geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="93696-171">Use hello job ID returned toocheck hello status of hello job.</span></span> <span data-ttu-id="93696-172">Gebruik hello Azure CLI zoals hierboven beschreven toodownload en bekijkt hello resultaten zodra deze is voltooid.</span><span class="sxs-lookup"><span data-stu-id="93696-172">Once it has succeeded, use hello Azure CLI as described previously toodownload and view hello results.</span></span> <span data-ttu-id="93696-173">Hallo-uitvoer moet drie regels, die allemaal bevatten bevatten **[fout]**.</span><span class="sxs-lookup"><span data-stu-id="93696-173">hello output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="93696-174"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="93696-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="93696-175">Voor algemene informatie over Hive met HDInsight:</span><span class="sxs-lookup"><span data-stu-id="93696-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="93696-176">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="93696-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="93696-177">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="93696-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="93696-178">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="93696-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="93696-179">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="93696-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="93696-180">Als u van Tez met Hive gebruikmaakt, raadpleegt u Hallo volgende documenten voor het opsporen van informatie:</span><span class="sxs-lookup"><span data-stu-id="93696-180">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="93696-181">Hallo Ambari Tez weergave op Linux gebaseerde HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="93696-181">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="93696-182">Zie voor meer informatie over Hallo REST-API die wordt gebruikt in dit document Hallo [WebHCat verwijzing](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span><span class="sxs-lookup"><span data-stu-id="93696-182">For more information on hello REST API used in this document, see hello [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx



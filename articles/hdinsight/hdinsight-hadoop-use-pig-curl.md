---
title: aaaUse Pig met REST in HDInsight - Azure Hadoop | Microsoft Docs
description: Meer informatie over hoe toouse REST toorun Pig Latin taken op een Hadoop-cluster in Azure HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="2f1f5-103">Pig-taken uitvoeren met Hadoop in HDInsight met behulp van REST</span><span class="sxs-lookup"><span data-stu-id="2f1f5-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="2f1f5-104">Meer informatie over hoe toorun Pig Latin taken doordat REST aanvragen tooan Azure HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-104">Learn how toorun Pig Latin jobs by making REST requests tooan Azure HDInsight cluster.</span></span> <span data-ttu-id="2f1f5-105">CURL is gebruikte toodemonstrate hoe u kunt werken met HDInsight met behulp van Hallo WebHCat REST-API.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-105">Curl is used toodemonstrate how you can interact with HDInsight using hello WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="2f1f5-106">Als u al bekend bent met Hadoop op basis van Linux-servers gebruiken, maar nieuwe tooHDInsight zijn, raadpleegt u [Linux gebaseerde HDInsight Tips](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="2f1f5-106">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="2f1f5-107"><a id="prereq"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="2f1f5-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="2f1f5-108">Een Azure HDInsight (Hadoop in HDInsight)-cluster (op basis van Linux of op basis van Windows)</span><span class="sxs-lookup"><span data-stu-id="2f1f5-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="2f1f5-109">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2f1f5-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="2f1f5-111">CURL</span><span class="sxs-lookup"><span data-stu-id="2f1f5-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="2f1f5-112">jq</span><span class="sxs-lookup"><span data-stu-id="2f1f5-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="2f1f5-113"><a id="curl"></a>Pig-taken uitvoeren met behulp van Curl</span><span class="sxs-lookup"><span data-stu-id="2f1f5-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="2f1f5-114">Hallo REST API is beveiligd via [basistoegang verificatie](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="2f1f5-114">hello REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="2f1f5-115">Altijd aanvragen indienen via HTTP Secure (HTTPS) tooensure dat uw referenties veilig toohello server worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-115">Always make requests by using Secure HTTP (HTTPS) tooensure that your credentials are securely sent toohello server.</span></span>
>
> <span data-ttu-id="2f1f5-116">Wanneer met Hallo-opdrachten in deze sectie vervangt `USERNAME` met Hallo gebruiker tooauthenticate toohello cluster en vervang `PASSWORD` met wachtwoord voor gebruikersaccount Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-116">When using hello commands in this section, replace `USERNAME` with hello user tooauthenticate toohello cluster, and replace `PASSWORD` with hello password for hello user account.</span></span> <span data-ttu-id="2f1f5-117">Vervang `CLUSTERNAME` met Hallo-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-117">Replace `CLUSTERNAME` with hello name of your cluster.</span></span>
>


1. <span data-ttu-id="2f1f5-118">Gebruik vanaf een opdrachtregel Hallo opdracht tooverify dat u verbinding tooyour HDInsight-cluster maken kunt te volgen:</span><span class="sxs-lookup"><span data-stu-id="2f1f5-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="2f1f5-119">U ontvangt Hallo volgende JSON-antwoord:</span><span class="sxs-lookup"><span data-stu-id="2f1f5-119">You should receive hello following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="2f1f5-120">Hallo-parameters die worden gebruikt in deze opdracht zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="2f1f5-120">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="2f1f5-121">**-u**: Hallo-gebruikersnaam en wachtwoord gebruikt tooauthenticate Hallo aanvraag</span><span class="sxs-lookup"><span data-stu-id="2f1f5-121">**-u**: hello user name and password used tooauthenticate hello request</span></span>
    * <span data-ttu-id="2f1f5-122">**-G**: geeft aan dat deze aanvraag een aanvraag voor ophalen</span><span class="sxs-lookup"><span data-stu-id="2f1f5-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="2f1f5-123">Hallo begin van het Hallo-URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is dezelfde Hallo voor alle aanvragen.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-123">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="2f1f5-124">Hallo-pad, **/status**, geeft aan dat verzoek Hallo tooreturn Hallo status van WebHCat (ook wel bekend als Templeton) voor Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-124">hello path, **/status**, indicates that hello request is tooreturn hello status of WebHCat (also known as Templeton) for hello server.</span></span>

2. <span data-ttu-id="2f1f5-125">Hallo code toosubmit een Pig Latin taak toohello cluster volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2f1f5-125">Use hello following code toosubmit a Pig Latin job toohello cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="2f1f5-126">Hallo-parameters die worden gebruikt in deze opdracht zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="2f1f5-126">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="2f1f5-127">**-d**: omdat `-G` niet wordt gebruikt, Hallo aanvraag standaard toohello POST-methode.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-127">**-d**: Because `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="2f1f5-128">`-d`Hiermee geeft u Hallo waarden die worden verzonden met Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-128">`-d` specifies hello data values that are sent with hello request.</span></span>

    * <span data-ttu-id="2f1f5-129">**User.name**: Hallo-gebruiker die het Hallo-opdracht wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="2f1f5-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="2f1f5-130">**uitvoeren van**: Hallo Pig Latin instructies tooexecute</span><span class="sxs-lookup"><span data-stu-id="2f1f5-130">**execute**: hello Pig Latin statements tooexecute</span></span>
    * <span data-ttu-id="2f1f5-131">**statusdir**: Hallo-map die Hallo status voor deze taak wordt geschreven naar</span><span class="sxs-lookup"><span data-stu-id="2f1f5-131">**statusdir**: hello directory that hello status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="2f1f5-132">U ziet dat Hallo spaties in Pig Latin-instructies worden vervangen door Hallo `+` gebruikt in combinatie met Curl teken.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-132">Notice that hello spaces in Pig Latin statements are replaced by hello `+` character when used with Curl.</span></span>

    <span data-ttu-id="2f1f5-133">Met deze opdracht als resultaat moet een taak-ID die gebruikte toocheck Hallo status van Hallo taak, bijvoorbeeld kan zijn:</span><span class="sxs-lookup"><span data-stu-id="2f1f5-133">This command should return a job ID that can be used toocheck hello status of hello job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="2f1f5-134">status van de toocheck Hallo van Hallo taak, gebruik Hallo na de opdracht</span><span class="sxs-lookup"><span data-stu-id="2f1f5-134">toocheck hello status of hello job, use hello following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="2f1f5-135">Vervang `JOBID` met Hallo-waarde geretourneerd in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-135">Replace `JOBID` with hello value returned in hello previous step.</span></span> <span data-ttu-id="2f1f5-136">Bijvoorbeeld, als hello retourneert de waarde is `{"id":"job_1415651640909_0026"}`, klikt u vervolgens `JOBID` is `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-136">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="2f1f5-137">Als het Hallo-taak is voltooid, is het Hallo-status **geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-137">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2f1f5-138">Deze retourneert een JavaScript Object Notation JSON ()-document met informatie over het Hallo-taak en jq is gebruikte tooretrieve Curl-aanvraag Hallo alleen statuswaarde.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job, and jq is used tooretrieve only hello state value.</span></span>

## <span data-ttu-id="2f1f5-139"><a id="results"></a>Resultaten weergeven</span><span class="sxs-lookup"><span data-stu-id="2f1f5-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="2f1f5-140">Wanneer de status van taak Hallo Hallo te is gewijzigd**geslaagd**, kunt u de resultaten van de taak Hallo Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-140">When hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job.</span></span> <span data-ttu-id="2f1f5-141">Hallo `statusdir` parameter doorgegeven aan Hallo query bevat Hallo locatie van het uitvoerbestand Hallo; in dit geval `/example/pigcurl`.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="2f1f5-142">HDInsight kunt gebruiken Azure Storage of Azure Data Lake Store als Hallo standaard gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-142">HDInsight can use either Azure Storage or Azure Data Lake Store as hello default data store.</span></span> <span data-ttu-id="2f1f5-143">Er zijn verschillende manieren tooget op Hallo-gegevens die zijn afhankelijk van wat u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-143">There are various ways tooget at hello data depending on which one you use.</span></span> <span data-ttu-id="2f1f5-144">Zie voor meer informatie, opslagsectie staat Hallo Hallo [Linux gebaseerde HDInsight-informatie](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-144">For more information, see hello storage section of hello [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="2f1f5-145"><a id="summary"></a>Samenvatting</span><span class="sxs-lookup"><span data-stu-id="2f1f5-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="2f1f5-146">Zoals wordt beschreven in dit document, kunt u een onbewerkte HTTP-aanvraag toorun, bewaken en Hallo-resultaten van Pig-taken weergeven op uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="2f1f5-146">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="2f1f5-147">Zie voor meer informatie over Hallo REST-interface gebruikt in dit artikel, Hallo [WebHCat verwijzing](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="2f1f5-147">For more information about hello REST interface used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="2f1f5-148"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f1f5-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="2f1f5-149">Voor algemene informatie over Pig op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="2f1f5-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="2f1f5-150">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f1f5-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="2f1f5-151">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="2f1f5-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="2f1f5-152">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f1f5-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="2f1f5-153">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f1f5-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

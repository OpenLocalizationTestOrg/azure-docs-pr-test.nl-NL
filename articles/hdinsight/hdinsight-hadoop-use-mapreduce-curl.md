---
title: aaaUse MapReduce en Curl met Hadoop in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe tooremotely uitvoeren MapReduce-taken met Hadoop op HDInsight met Curl.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="48c1a-103">MapReduce-taken uitvoeren met Hadoop op HDInsight met behulp van REST</span><span class="sxs-lookup"><span data-stu-id="48c1a-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="48c1a-104">Meer informatie over hoe toouse hello WebHCat REST-API toorun MapReduce taken op een Hadoop op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="48c1a-104">Learn how toouse hello WebHCat REST API toorun MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="48c1a-105">CURL is gebruikte toodemonstrate hoe u met HDInsight werken kunt met behulp van onbewerkte HTTP-aanvragen toorun MapReduce-taken.</span><span class="sxs-lookup"><span data-stu-id="48c1a-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="48c1a-106">Als u al bekend bent met Hadoop op basis van Linux-servers gebruiken, maar u staat op het nieuwe tooHDInsight, Zie Hallo [wat u moet tooknow over Hadoop op basis van Linux in HDInsight](hdinsight-hadoop-linux-information.md) document.</span><span class="sxs-lookup"><span data-stu-id="48c1a-106">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see hello [What you need tooknow about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <span data-ttu-id="48c1a-107"><a id="prereq"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="48c1a-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="48c1a-108">Een Hadoop op HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="48c1a-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="48c1a-109">CURL</span><span class="sxs-lookup"><span data-stu-id="48c1a-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="48c1a-110">jq</span><span class="sxs-lookup"><span data-stu-id="48c1a-110">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="48c1a-111"><a id="curl"></a>MapReduce-taken met Curl uitvoeren</span><span class="sxs-lookup"><span data-stu-id="48c1a-111"><a id="curl"></a>Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="48c1a-112">Wanneer u Curl of andere REST-communicatie met WebHCat gebruikt, moet u Hallo aanvragen verifiëren door te geven Hallo HDInsight-cluster administrator-gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="48c1a-112">When you use Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="48c1a-113">Als onderdeel van Hallo URI die gebruikte toosend Hallo aanvragen toohello server, moet u de clusternaam hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="48c1a-113">You must use hello cluster name as part of hello URI that is used toosend hello requests toohello server.</span></span>
>
> <span data-ttu-id="48c1a-114">Hallo-opdrachten in deze sectie, vervangt u **gebruikersnaam** met Hallo gebruiker tooauthenticate toohello cluster en **wachtwoord** met wachtwoord voor gebruikersaccount Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="48c1a-114">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="48c1a-115">Vervang **CLUSTERNAME** met Hallo-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="48c1a-115">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="48c1a-116">Hallo REST API is beveiligd met behulp van [basistoegang verificatie](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="48c1a-116">hello REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="48c1a-117">U moet aanvragen altijd maken met behulp van HTTPS tooensure dat uw referenties veilig toohello server worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="48c1a-117">You should always make requests by using HTTPS tooensure that your credentials are securely sent toohello server.</span></span>


1. <span data-ttu-id="48c1a-118">Gebruik vanaf een opdrachtregel Hallo opdracht tooverify dat u verbinding tooyour HDInsight-cluster maken kunt te volgen:</span><span class="sxs-lookup"><span data-stu-id="48c1a-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="48c1a-119">U ontvangt een reactie vergelijkbaar toohello JSON te volgen:</span><span class="sxs-lookup"><span data-stu-id="48c1a-119">You should receive a response similar toohello following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="48c1a-120">Hallo-parameters die worden gebruikt in deze opdracht zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="48c1a-120">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="48c1a-121">**-u**: Hiermee geeft u Hallo-gebruikersnaam en wachtwoord gebruikt tooauthenticate Hallo aanvraag</span><span class="sxs-lookup"><span data-stu-id="48c1a-121">**-u**: Indicates hello user name and password used tooauthenticate hello request</span></span>
   * <span data-ttu-id="48c1a-122">**-G**: geeft aan dat deze bewerking een GET-aanvraag</span><span class="sxs-lookup"><span data-stu-id="48c1a-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="48c1a-123">Hallo vanaf Hallo URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is dezelfde Hallo voor alle aanvragen.</span><span class="sxs-lookup"><span data-stu-id="48c1a-123">hello beginning of hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span>

2. <span data-ttu-id="48c1a-124">toosubmit MapReduce-taak Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="48c1a-124">toosubmit a MapReduce job, use hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="48c1a-125">Hallo-einde van Hallo URI (mapreduce/jar) ziet WebHCat of er een MapReduce-taak op deze aanvraag wordt gestart van een klasse in een jar-bestand.</span><span class="sxs-lookup"><span data-stu-id="48c1a-125">hello end of hello URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="48c1a-126">Hallo-parameters die worden gebruikt in deze opdracht zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="48c1a-126">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="48c1a-127">**-d**: `-G` niet wordt gebruikt, dus Hallo aanvraag standaard toohello POST-methode.</span><span class="sxs-lookup"><span data-stu-id="48c1a-127">**-d**: `-G` is not used, so hello request defaults toohello POST method.</span></span> <span data-ttu-id="48c1a-128">`-d`Hiermee geeft u Hallo waarden die worden verzonden met Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="48c1a-128">`-d` specifies hello data values that are sent with hello request.</span></span>
    * <span data-ttu-id="48c1a-129">**User.name**: Hallo-gebruiker die het Hallo-opdracht wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="48c1a-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="48c1a-130">**JAR**: Hallo-locatie van Hallo jar-bestand waarin de klasse toobe uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="48c1a-130">**jar**: hello location of hello jar file that contains class toobe ran</span></span>
    * <span data-ttu-id="48c1a-131">**klasse**: klasse met Hallo MapReduce logica Hallo</span><span class="sxs-lookup"><span data-stu-id="48c1a-131">**class**: hello class that contains hello MapReduce logic</span></span>
    * <span data-ttu-id="48c1a-132">**arg**: Hallo argumenten toobe doorgegeven toohello MapReduce-taak.</span><span class="sxs-lookup"><span data-stu-id="48c1a-132">**arg**: hello arguments toobe passed toohello MapReduce job.</span></span> <span data-ttu-id="48c1a-133">In dit geval invoer Hallo tekst bestands- en Hallo directory die worden gebruikt voor het Hallo-uitvoer</span><span class="sxs-lookup"><span data-stu-id="48c1a-133">In this case, hello input text file and hello directory that are used for hello output</span></span>

     <span data-ttu-id="48c1a-134">Met deze opdracht moet een taak-ID die gebruikt toocheck Hallo status van Hallo taak worden kan retourneren:</span><span class="sxs-lookup"><span data-stu-id="48c1a-134">This command should return a job ID that can be used toocheck hello status of hello job:</span></span>

       <span data-ttu-id="48c1a-135">{{'id': "job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="48c1a-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="48c1a-136">toocheck Hallo status van taak hello, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="48c1a-136">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="48c1a-137">Vervang Hallo **JOBID** met Hallo-waarde geretourneerd in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="48c1a-137">Replace hello **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="48c1a-138">Bijvoorbeeld, als hello retourneert de waarde is `{"id":"job_1415651640909_0026"}`, vervolgens Hallo JOBID zou worden `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="48c1a-138">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then hello JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="48c1a-139">Als het Hallo-taak is voltooid, Hallo status geretourneerd is `SUCCEEDED`.</span><span class="sxs-lookup"><span data-stu-id="48c1a-139">If hello job is complete, hello state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="48c1a-140">Deze aanvraag Curl retourneert een JSON-document met informatie over het Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="48c1a-140">This Curl request returns a JSON document with information about hello job.</span></span> <span data-ttu-id="48c1a-141">Jq wordt gebruikt tooretrieve Hallo alleen statuswaarde.</span><span class="sxs-lookup"><span data-stu-id="48c1a-141">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="48c1a-142">Wanneer de status van taak Hallo Hallo te is gewijzigd`SUCCEEDED`, kunt u resultaten van de taak Hallo Hallo ophalen uit Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="48c1a-142">When hello state of hello job has changed too`SUCCEEDED`, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="48c1a-143">Hallo `statusdir` parameter die wordt doorgegeven met Hallo query Hallo locatie van het uitvoerbestand Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="48c1a-143">hello `statusdir` parameter that is passed with hello query contains hello location of hello output file.</span></span> <span data-ttu-id="48c1a-144">In dit voorbeeld is Hallo locatie `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="48c1a-144">In this example, hello location is `/example/curl`.</span></span> <span data-ttu-id="48c1a-145">Dit adres Hallo-uitvoer van Hallo taak opslaat in Hallo-clusters standaard opslag op `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="48c1a-145">This address stores hello output of hello job in hello clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="48c1a-146">U kunt de lijst en deze bestanden downloaden met behulp van Hallo [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="48c1a-146">You can list and download these files by using hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="48c1a-147">Zie voor meer informatie over het werken met blobs uit hello Azure CLI Hallo [Using hello Azure CLI 2.0 met Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span><span class="sxs-lookup"><span data-stu-id="48c1a-147">For more information on working with blobs from hello Azure CLI, see hello [Using hello Azure CLI 2.0 with Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <span data-ttu-id="48c1a-148"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="48c1a-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="48c1a-149">Voor algemene informatie over MapReduce-taken in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="48c1a-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="48c1a-150">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="48c1a-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="48c1a-151">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="48c1a-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="48c1a-152">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="48c1a-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="48c1a-153">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="48c1a-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="48c1a-154">Zie voor meer informatie over Hallo REST-interface die wordt gebruikt in dit artikel, Hallo [WebHCat verwijzing](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="48c1a-154">For more information about hello REST interface that is used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

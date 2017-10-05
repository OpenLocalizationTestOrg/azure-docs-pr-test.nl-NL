---
title: Gebruik MapReduce en Curl met Hadoop in HDInsight - Azure | Microsoft Docs
description: Informatie over het op afstand MapReduce-taken uitvoeren met Hadoop in HDInsight met Curl.
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
ms.openlocfilehash: 8238bb829df95dcb8c99c0b7fff53c627a56f47c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="f9dca-103">MapReduce-taken uitvoeren met Hadoop op HDInsight met behulp van REST</span><span class="sxs-lookup"><span data-stu-id="f9dca-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="f9dca-104">Informatie over het gebruik van de REST-API WebHCat MapReduce-taken uitvoeren op een Hadoop op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="f9dca-104">Learn how to use the WebHCat REST API to run MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="f9dca-105">CURL wordt gebruikt om u te laten zien hoe u kunt werken met HDInsight met behulp van onbewerkte HTTP-aanvragen voor MapReduce-taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f9dca-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="f9dca-106">Als u al bekend bent met Hadoop op basis van Linux-servers gebruiken, maar u niet bekend met HDInsight bent, raadpleegt u de [wat u moet weten over Hadoop op basis van Linux in HDInsight](hdinsight-hadoop-linux-information.md) document.</span><span class="sxs-lookup"><span data-stu-id="f9dca-106">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see the [What you need to know about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <span data-ttu-id="f9dca-107"><a id="prereq"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="f9dca-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="f9dca-108">Een Hadoop op HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="f9dca-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="f9dca-109">CURL</span><span class="sxs-lookup"><span data-stu-id="f9dca-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="f9dca-110">jq</span><span class="sxs-lookup"><span data-stu-id="f9dca-110">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="f9dca-111"><a id="curl"></a>MapReduce-taken met Curl uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f9dca-111"><a id="curl"></a>Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="f9dca-112">Wanneer u Curl of andere REST-communicatie met WebHCat gebruikt, moet u de aanvragen verifiëren door te geven van de gebruikersnaam van de beheerder voor HDInsight-cluster en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="f9dca-112">When you use Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="f9dca-113">U moet de clusternaam gebruiken als onderdeel van de URI die wordt gebruikt voor het versturen van aanvragen naar de server.</span><span class="sxs-lookup"><span data-stu-id="f9dca-113">You must use the cluster name as part of the URI that is used to send the requests to the server.</span></span>
>
> <span data-ttu-id="f9dca-114">Voor de opdrachten in deze sectie vervangt u **gebruikersnaam** met de gebruiker om het cluster te verifiëren en **wachtwoord** met het wachtwoord voor het gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="f9dca-114">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="f9dca-115">Vervang **CLUSTERNAME** door de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="f9dca-115">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
>
> <span data-ttu-id="f9dca-116">De REST-API is beveiligd met behulp van [basistoegang verificatie](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="f9dca-116">The REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="f9dca-117">U moet aanvragen altijd maken met behulp van HTTPS om ervoor te zorgen dat uw referenties veilig worden verzonden naar de server.</span><span class="sxs-lookup"><span data-stu-id="f9dca-117">You should always make requests by using HTTPS to ensure that your credentials are securely sent to the server.</span></span>


1. <span data-ttu-id="f9dca-118">Gebruik een opdrachtregel met de volgende opdracht om te controleren of u verbinding met uw HDInsight-cluster kunt maken:</span><span class="sxs-lookup"><span data-stu-id="f9dca-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="f9dca-119">U ontvangt een reactie vergelijkbaar met de volgende JSON:</span><span class="sxs-lookup"><span data-stu-id="f9dca-119">You should receive a response similar to the following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="f9dca-120">In deze opdracht worden de volgende parameters gebruikt:</span><span class="sxs-lookup"><span data-stu-id="f9dca-120">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="f9dca-121">**-u**: geeft aan dat de gebruikersnaam en wachtwoord voor het verifiëren van de aanvraag</span><span class="sxs-lookup"><span data-stu-id="f9dca-121">**-u**: Indicates the user name and password used to authenticate the request</span></span>
   * <span data-ttu-id="f9dca-122">**-G**: geeft aan dat deze bewerking een GET-aanvraag</span><span class="sxs-lookup"><span data-stu-id="f9dca-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="f9dca-123">Het begin van de URI **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hetzelfde voor alle aanvragen.</span><span class="sxs-lookup"><span data-stu-id="f9dca-123">The beginning of the URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span>

2. <span data-ttu-id="f9dca-124">Als u een MapReduce-taak, moet u de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f9dca-124">To submit a MapReduce job, use the following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="f9dca-125">Het einde van de URI (mapreduce/jar) ziet WebHCat of er een MapReduce-taak op deze aanvraag wordt gestart van een klasse in een jar-bestand.</span><span class="sxs-lookup"><span data-stu-id="f9dca-125">The end of the URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="f9dca-126">In deze opdracht worden de volgende parameters gebruikt:</span><span class="sxs-lookup"><span data-stu-id="f9dca-126">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="f9dca-127">**-d**: `-G` niet wordt gebruikt, zodat de aanvraag wordt standaard ingesteld op de POST-methode.</span><span class="sxs-lookup"><span data-stu-id="f9dca-127">**-d**: `-G` is not used, so the request defaults to the POST method.</span></span> <span data-ttu-id="f9dca-128">`-d`Hiermee geeft u de waarden die worden verzonden met de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="f9dca-128">`-d` specifies the data values that are sent with the request.</span></span>
    * <span data-ttu-id="f9dca-129">**User.name**: de gebruiker die de opdracht wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="f9dca-129">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="f9dca-130">**JAR**: de locatie van de jar-bestand met de klasse om te worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="f9dca-130">**jar**: The location of the jar file that contains class to be ran</span></span>
    * <span data-ttu-id="f9dca-131">**klasse**: de klasse met de MapReduce-logica</span><span class="sxs-lookup"><span data-stu-id="f9dca-131">**class**: The class that contains the MapReduce logic</span></span>
    * <span data-ttu-id="f9dca-132">**arg**: de argumenten worden doorgegeven aan de MapReduce-taak.</span><span class="sxs-lookup"><span data-stu-id="f9dca-132">**arg**: The arguments to be passed to the MapReduce job.</span></span> <span data-ttu-id="f9dca-133">In dit geval, het bestand invoertekst en de map die worden gebruikt voor de uitvoer</span><span class="sxs-lookup"><span data-stu-id="f9dca-133">In this case, the input text file and the directory that are used for the output</span></span>

     <span data-ttu-id="f9dca-134">Met deze opdracht als resultaat moet een taak-ID die kan worden gebruikt om de status van de taak te controleren:</span><span class="sxs-lookup"><span data-stu-id="f9dca-134">This command should return a job ID that can be used to check the status of the job:</span></span>

       <span data-ttu-id="f9dca-135">{{'id': "job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="f9dca-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="f9dca-136">Als u wilt de status van de taak controleren, moet u de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f9dca-136">To check the status of the job, use the following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="f9dca-137">Vervang de **JOBID** met de waarde die wordt geretourneerd in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="f9dca-137">Replace the **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="f9dca-138">Bijvoorbeeld, als de retourwaarde is `{"id":"job_1415651640909_0026"}`, en vervolgens de JOBID is `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="f9dca-138">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then the JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="f9dca-139">Als de taak voltooid is, wordt de status geretourneerd is `SUCCEEDED`.</span><span class="sxs-lookup"><span data-stu-id="f9dca-139">If the job is complete, the state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f9dca-140">Deze aanvraag Curl retourneert een JSON-document met informatie over de taak.</span><span class="sxs-lookup"><span data-stu-id="f9dca-140">This Curl request returns a JSON document with information about the job.</span></span> <span data-ttu-id="f9dca-141">Jq wordt gebruikt voor het ophalen van de waarde van de status.</span><span class="sxs-lookup"><span data-stu-id="f9dca-141">Jq is used to retrieve only the state value.</span></span>

4. <span data-ttu-id="f9dca-142">Wanneer de status van de taak is gewijzigd in `SUCCEEDED`, kunt u de resultaten van de taak ophalen uit Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="f9dca-142">When the state of the job has changed to `SUCCEEDED`, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="f9dca-143">De `statusdir` parameter die wordt doorgegeven aan de query bevat de locatie van het uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="f9dca-143">The `statusdir` parameter that is passed with the query contains the location of the output file.</span></span> <span data-ttu-id="f9dca-144">In dit voorbeeld is de locatie `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="f9dca-144">In this example, the location is `/example/curl`.</span></span> <span data-ttu-id="f9dca-145">Dit adres slaat de uitvoer van de taak in de opslag van de standaard clusters op `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="f9dca-145">This address stores the output of the job in the clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="f9dca-146">U kunt de lijst en deze bestanden downloaden met behulp van de [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f9dca-146">You can list and download these files by using the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="f9dca-147">Zie voor meer informatie over het werken met blobs met Azure CLI het [met behulp van de Azure CLI 2.0 met Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span><span class="sxs-lookup"><span data-stu-id="f9dca-147">For more information on working with blobs from the Azure CLI, see the [Using the Azure CLI 2.0 with Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <span data-ttu-id="f9dca-148"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f9dca-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="f9dca-149">Voor algemene informatie over MapReduce-taken in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="f9dca-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="f9dca-150">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9dca-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="f9dca-151">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="f9dca-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="f9dca-152">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9dca-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f9dca-153">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9dca-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="f9dca-154">Zie voor meer informatie over de REST-interface die wordt gebruikt in dit artikel, de [WebHCat verwijzing](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="f9dca-154">For more information about the REST interface that is used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>
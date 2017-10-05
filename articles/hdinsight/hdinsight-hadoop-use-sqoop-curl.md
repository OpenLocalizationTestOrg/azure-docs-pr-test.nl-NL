---
title: Hadoop Sqoop gebruiken met Curl in HDInsight - Azure | Microsoft Docs
description: Informatie over het op afstand Sqoop om taken te verzenden naar HDInsight met Curl.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0975aedf58c6e110726dd3308eae5f9ad3907cc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="016ac-103">Sqoop taken uitvoeren met Hadoop in HDInsight met Curl</span><span class="sxs-lookup"><span data-stu-id="016ac-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="016ac-104">Informatie over het gebruik van Curl Sqoop taken uitvoeren op een Hadoop-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="016ac-104">Learn how to use Curl to run Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="016ac-105">CURL wordt gebruikt om u te laten zien hoe u kunt werken met HDInsight met behulp van onbewerkte HTTP-aanvragen worden uitgevoerd, controleren en ophalen van de resultaten van Sqoop taken.</span><span class="sxs-lookup"><span data-stu-id="016ac-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run, monitor, and retrieve the results of Sqoop jobs.</span></span> <span data-ttu-id="016ac-106">Dit werkt met behulp van de WebHCat REST-API (voorheen bekend als Templeton) geleverd door uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="016ac-106">This works by using the WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="016ac-107">Als u al bekend bent met Hadoop op basis van Linux-servers gebruiken, maar niet bekend met HDInsight bent, raadpleegt u [informatie over het gebruik van HDInsight op Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="016ac-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="016ac-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="016ac-108">Prerequisites</span></span>
<span data-ttu-id="016ac-109">Voor het voltooien van de stappen in dit artikel, moet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="016ac-109">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="016ac-110">Een Hadoop op HDInsight-cluster (Linux of op basis van Windows)</span><span class="sxs-lookup"><span data-stu-id="016ac-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="016ac-111">CURL</span><span class="sxs-lookup"><span data-stu-id="016ac-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="016ac-112">jq</span><span class="sxs-lookup"><span data-stu-id="016ac-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="016ac-113">Sqoop taken verzenden met behulp van Curl</span><span class="sxs-lookup"><span data-stu-id="016ac-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="016ac-114">Wanneer u Curl of een andere REST-communicatie gebruikt met WebHCat, moet u de aanvragen verifiëren door de gebruikersnaam en het wachtwoord voor de beheerder van het HDInsight-cluster op te geven.</span><span class="sxs-lookup"><span data-stu-id="016ac-114">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="016ac-115">U moet ook de clusternaam gebruiken als onderdeel van de URI (Uniform Resource Identifier) die wordt gebruikt om de aanvragen naar de server te verzenden.</span><span class="sxs-lookup"><span data-stu-id="016ac-115">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server.</span></span>
> 
> <span data-ttu-id="016ac-116">Voor de opdrachten in deze sectie vervangt u **USERNAME** door de gebruiker die moet worden geverifieerd bij het cluster en vervangt u **PASSWORD** door het wachtwoord voor het gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="016ac-116">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="016ac-117">Vervang **CLUSTERNAME** door de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="016ac-117">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
> 
> <span data-ttu-id="016ac-118">De REST API is beveiligd via [basisverificatie](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="016ac-118">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="016ac-119">U moet aanvragen altijd uitvoeren via een beveiligde HTTP-verbinding (HTTPS). Zo zorgt u ervoor dat uw referenties veilig worden verzonden naar de server.</span><span class="sxs-lookup"><span data-stu-id="016ac-119">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>
> 
> 

1. <span data-ttu-id="016ac-120">Gebruik een opdrachtregel met de volgende opdracht om te controleren of u verbinding met uw HDInsight-cluster kunt maken:</span><span class="sxs-lookup"><span data-stu-id="016ac-120">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="016ac-121">Het antwoord dat u ontvangt, is vergelijkbaar met het volgende antwoord:</span><span class="sxs-lookup"><span data-stu-id="016ac-121">You should receive a response similar to the following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="016ac-122">In deze opdracht worden de volgende parameters gebruikt:</span><span class="sxs-lookup"><span data-stu-id="016ac-122">The parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="016ac-123">**-u**: de gebruikersnaam en het wachtwoord voor het verifiëren van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="016ac-123">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="016ac-124">**-G**: hiermee wordt aangegeven dat dit een GET-aanvraag is.</span><span class="sxs-lookup"><span data-stu-id="016ac-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="016ac-125">Het begin van de URL **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hetzelfde voor alle aanvragen.</span><span class="sxs-lookup"><span data-stu-id="016ac-125">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be the same for all requests.</span></span> <span data-ttu-id="016ac-126">Het pad **/status**, geeft aan dat de aanvraag is de status van WebHCat (ook wel bekend als Templeton) voor de server.</span><span class="sxs-lookup"><span data-stu-id="016ac-126">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> 
2. <span data-ttu-id="016ac-127">Gebruik de volgende voor het verzenden van een taak sqoop:</span><span class="sxs-lookup"><span data-stu-id="016ac-127">Use the following to submit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="016ac-128">In deze opdracht worden de volgende parameters gebruikt:</span><span class="sxs-lookup"><span data-stu-id="016ac-128">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="016ac-129">**-d** - sinds `-G` niet wordt gebruikt, de aanvraag wordt standaard ingesteld op de POST-methode.</span><span class="sxs-lookup"><span data-stu-id="016ac-129">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="016ac-130">`-d`Hiermee geeft u de waarden die worden verzonden met de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="016ac-130">`-d` specifies the data values that are sent with the request.</span></span>

        * <span data-ttu-id="016ac-131">**User.name** -de gebruiker die de opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="016ac-131">**user.name** - The user that is running the command.</span></span>

        * <span data-ttu-id="016ac-132">**opdracht** -Sqoop van de opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="016ac-132">**command** - The Sqoop command to execute.</span></span>

        * <span data-ttu-id="016ac-133">**statusdir** -de map die de status voor deze taak om te worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="016ac-133">**statusdir** - The directory that the status for this job will be written to.</span></span>

    <span data-ttu-id="016ac-134">Met deze opdracht moet een taak-ID die kan worden gebruikt om te controleren van de status van de taak retourneren.</span><span class="sxs-lookup"><span data-stu-id="016ac-134">This command should return a job ID that can be used to check the status of the job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="016ac-135">Gebruik de volgende opdracht om te controleren van de status van de taak.</span><span class="sxs-lookup"><span data-stu-id="016ac-135">To check the status of the job, use the following command.</span></span> <span data-ttu-id="016ac-136">Vervang **JOBID** met de waarde die wordt geretourneerd in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="016ac-136">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="016ac-137">Bijvoorbeeld, als de retourwaarde is `{"id":"job_1415651640909_0026"}`, klikt u vervolgens **JOBID** zou `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="016ac-137">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="016ac-138">Als de taak is voltooid, worden de status **geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="016ac-138">If the job has finished, the state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="016ac-139">Deze aanvraag Curl retourneert een notatie JSON (JavaScript Object)-document met informatie over de taak. jq wordt gebruikt voor het ophalen van de waarde van de status.</span><span class="sxs-lookup"><span data-stu-id="016ac-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job; jq is used to retrieve only the state value.</span></span>
   > 
   > 
2. <span data-ttu-id="016ac-140">Zodra de status van de taak is gewijzigd in **geslaagd**, kunt u de resultaten van de taak ophalen uit Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="016ac-140">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="016ac-141">De `statusdir` parameter doorgegeven aan de query bevat de locatie van het uitvoerbestand; in dit geval **wasb: / / / voorbeeld/curl**.</span><span class="sxs-lookup"><span data-stu-id="016ac-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="016ac-142">Dit adres slaat de uitvoer van de taak in de **voorbeeld/curl** directory op de standaard storage-container die wordt gebruikt door uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="016ac-142">This address stores the output of the job in the **example/curl** directory on the default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="016ac-143">U kunt de lijst en deze bestanden downloaden met behulp van de [Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="016ac-143">You can list and download these files by using the [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="016ac-144">Bijvoorbeeld naar de lijst met bestanden in **voorbeeld/curl**, gebruik de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="016ac-144">For example, to list files in **example/curl**, use the following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="016ac-145">U kunt een bestand downloaden, gebruikt u het volgende:</span><span class="sxs-lookup"><span data-stu-id="016ac-145">To download a file, use the following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="016ac-146">U moet opgeven de opslagaccountnaam die de blob met behulp van bevat de `-a` en `-k` parameters of stel de **AZURE\_opslag\_ACCOUNT** en **AZURE \_Opslag\_toegang\_sleutel** omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="016ac-146">You must either specify the storage account name that contains the blob by using the `-a` and `-k` parameters, or set the **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="016ac-147">Zie < een href = "hdinsight-upload-data.md" target = "_blank" voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="016ac-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="016ac-148">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="016ac-148">Limitations</span></span>
* <span data-ttu-id="016ac-149">Bulksgewijs export - met Linux gebaseerde HDInsight, de Sqoop-connector gebruikt voor het exporteren van gegevens naar Microsoft SQL Server of Azure SQL Database biedt momenteel geen ondersteuning voor bulksgewijs invoegen.</span><span class="sxs-lookup"><span data-stu-id="016ac-149">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="016ac-150">Batchverwerking - met HDInsight op basis van Linux, wanneer u de `-batch` bij het uitvoeren van invoeg-switch, Sqoop meerdere invoegen in plaats van de bewerkingen insert batchverwerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="016ac-150">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="016ac-151">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="016ac-151">Summary</span></span>
<span data-ttu-id="016ac-152">Zoals wordt beschreven in dit document, kunt u een onbewerkte HTTP-aanvraag uitvoeren, bewaken en bekijk de resultaten van Sqoop taken op uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="016ac-152">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="016ac-153">Zie voor meer informatie over de REST-interface in dit artikel gebruikt de <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST-API-handleiding</a>.</span><span class="sxs-lookup"><span data-stu-id="016ac-153">For more information on the REST interface used in this article, see the <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="016ac-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="016ac-154">Next steps</span></span>
<span data-ttu-id="016ac-155">Voor algemene informatie over Hive met HDInsight:</span><span class="sxs-lookup"><span data-stu-id="016ac-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="016ac-156">Sqoop gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="016ac-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="016ac-157">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="016ac-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="016ac-158">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="016ac-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="016ac-159">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="016ac-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="016ac-160">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="016ac-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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



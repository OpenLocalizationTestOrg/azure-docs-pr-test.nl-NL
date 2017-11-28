---
title: aaaUse Hadoop Sqoop met Curl in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe tooremotely Sqoop taken tooHDInsight met Curl verzenden.
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
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="7e84f-103">Sqoop taken uitvoeren met Hadoop in HDInsight met Curl</span><span class="sxs-lookup"><span data-stu-id="7e84f-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="7e84f-104">Meer informatie over hoe toouse Curl toorun Sqoop taken op een Hadoop-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e84f-104">Learn how toouse Curl toorun Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="7e84f-105">CURL is gebruikte toodemonstrate hoe u met HDInsight werken kunt met behulp van onbewerkte HTTP-aanvragen toorun, bewaken en ophalen Hallo resultaten van Sqoop taken.</span><span class="sxs-lookup"><span data-stu-id="7e84f-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun, monitor, and retrieve hello results of Sqoop jobs.</span></span> <span data-ttu-id="7e84f-106">Dit werkt met behulp van Hallo WebHCat REST-API (voorheen bekend als Templeton) geleverd door uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7e84f-106">This works by using hello WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="7e84f-107">Als u al bekend bent met Hadoop op basis van Linux-servers gebruiken, maar nieuwe tooHDInsight zijn, raadpleegt u [informatie over het gebruik van HDInsight op Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="7e84f-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7e84f-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7e84f-108">Prerequisites</span></span>
<span data-ttu-id="7e84f-109">toocomplete hello stappen in dit artikel, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="7e84f-109">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="7e84f-110">Een Hadoop op HDInsight-cluster (Linux of op basis van Windows)</span><span class="sxs-lookup"><span data-stu-id="7e84f-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="7e84f-111">CURL</span><span class="sxs-lookup"><span data-stu-id="7e84f-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="7e84f-112">jq</span><span class="sxs-lookup"><span data-stu-id="7e84f-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="7e84f-113">Sqoop taken verzenden met behulp van Curl</span><span class="sxs-lookup"><span data-stu-id="7e84f-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="7e84f-114">Wanneer u Curl of andere REST-communicatie met WebHCat, moet u Hallo aanvragen verifiëren door het Hallo-gebruikersnaam en wachtwoord voor Hallo HDInsight Clusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="7e84f-114">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="7e84f-115">Als onderdeel van Hallo Uniform Resource Identifier (URI) toosend Hallo aanvragen toohello server gebruikt, moet u de clusternaam hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7e84f-115">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server.</span></span>
> 
> <span data-ttu-id="7e84f-116">Hallo-opdrachten in deze sectie, vervangt u **gebruikersnaam** met Hallo gebruiker tooauthenticate toohello cluster en vervang **wachtwoord** met wachtwoord voor gebruikersaccount Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7e84f-116">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="7e84f-117">Vervang **CLUSTERNAME** met Hallo-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="7e84f-117">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
> 
> <span data-ttu-id="7e84f-118">Hallo REST API is beveiligd via [basisverificatie](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="7e84f-118">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="7e84f-119">U moet aanvragen altijd maken met behulp van beveiligde HTTP (HTTPS) toohelp ervoor te zorgen dat uw referenties veilig toohello server worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="7e84f-119">You should always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>
> 
> 

1. <span data-ttu-id="7e84f-120">Gebruik vanaf een opdrachtregel Hallo opdracht tooverify dat u verbinding tooyour HDInsight-cluster maken kunt te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e84f-120">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="7e84f-121">U ontvangt een reactie vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="7e84f-121">You should receive a response similar toohello following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="7e84f-122">Hallo-parameters die worden gebruikt in deze opdracht zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="7e84f-122">hello parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="7e84f-123">**-u** -Hallo-gebruikersnaam en wachtwoord tooauthenticate Hallo aanvraag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7e84f-123">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="7e84f-124">**-G**: hiermee wordt aangegeven dat dit een GET-aanvraag is.</span><span class="sxs-lookup"><span data-stu-id="7e84f-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="7e84f-125">Hallo begin van het Hallo-URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, worden dezelfde Hallo voor alle aanvragen.</span><span class="sxs-lookup"><span data-stu-id="7e84f-125">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be hello same for all requests.</span></span> <span data-ttu-id="7e84f-126">Hallo-pad, **/status**, geeft aan dat verzoek Hallo tooreturn status WebHCat (ook wel bekend als Templeton) voor Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="7e84f-126">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> 
2. <span data-ttu-id="7e84f-127">Hallo na toosubmit een taak sqoop gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7e84f-127">Use hello following toosubmit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="7e84f-128">Hallo-parameters die worden gebruikt in deze opdracht zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="7e84f-128">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="7e84f-129">**-d** - sinds `-G` niet wordt gebruikt, Hallo aanvraag standaard toohello POST-methode.</span><span class="sxs-lookup"><span data-stu-id="7e84f-129">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="7e84f-130">`-d`Hiermee geeft u Hallo waarden die worden verzonden met Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="7e84f-130">`-d` specifies hello data values that are sent with hello request.</span></span>

        * <span data-ttu-id="7e84f-131">**User.name** -Hallo-gebruiker die het Hallo-opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7e84f-131">**user.name** - hello user that is running hello command.</span></span>

        * <span data-ttu-id="7e84f-132">**opdracht** -Hallo Sqoop opdracht tooexecute.</span><span class="sxs-lookup"><span data-stu-id="7e84f-132">**command** - hello Sqoop command tooexecute.</span></span>

        * <span data-ttu-id="7e84f-133">**statusdir** -Hallo-map die de status voor deze taak Hallo naar worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="7e84f-133">**statusdir** - hello directory that hello status for this job will be written to.</span></span>

    <span data-ttu-id="7e84f-134">Met deze opdracht moet een taak-ID die gebruikt toocheck Hallo status van Hallo taak worden kan retourneren.</span><span class="sxs-lookup"><span data-stu-id="7e84f-134">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="7e84f-135">toocheck Hallo status van taak hello, gebruik Hallo na de opdracht.</span><span class="sxs-lookup"><span data-stu-id="7e84f-135">toocheck hello status of hello job, use hello following command.</span></span> <span data-ttu-id="7e84f-136">Vervang **JOBID** met Hallo-waarde geretourneerd in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="7e84f-136">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="7e84f-137">Bijvoorbeeld, als hello retourneert de waarde is `{"id":"job_1415651640909_0026"}`, klikt u vervolgens **JOBID** zou `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="7e84f-137">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="7e84f-138">Als het Hallo-taak is voltooid, Hallo status worden **geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="7e84f-138">If hello job has finished, hello state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7e84f-139">Deze aanvraag Curl retourneert een notatie JSON (JavaScript Object)-document met informatie over het Hallo-taak jq wordt gebruikt tooretrieve Hallo alleen statuswaarde.</span><span class="sxs-lookup"><span data-stu-id="7e84f-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job; jq is used tooretrieve only hello state value.</span></span>
   > 
   > 
2. <span data-ttu-id="7e84f-140">Zodra het Hallo-status van taak hello te is gewijzigd**geslaagd**, kunt u resultaten van de taak Hallo Hallo ophalen uit Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="7e84f-140">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="7e84f-141">Hallo `statusdir` parameter doorgegeven aan Hallo query bevat Hallo locatie van het uitvoerbestand Hallo; in dit geval **wasb: / / / voorbeeld/curl**.</span><span class="sxs-lookup"><span data-stu-id="7e84f-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="7e84f-142">Dit adres Hallo-uitvoer van Hallo taak opslaat in Hallo **voorbeeld/curl** directory op Hallo standaardopslagcontainer die wordt gebruikt door uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7e84f-142">This address stores hello output of hello job in hello **example/curl** directory on hello default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="7e84f-143">U kunt de lijst en deze bestanden downloaden met behulp van Hallo [Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7e84f-143">You can list and download these files by using hello [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="7e84f-144">Bijvoorbeeld toolist bestanden **voorbeeld/curl**, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7e84f-144">For example, toolist files in **example/curl**, use hello following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="7e84f-145">toodownload een bestand, gebruikt u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="7e84f-145">toodownload a file, use hello following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="7e84f-146">U moet opgeven Hallo opslagaccountnaam Hallo blob bevat met behulp van Hallo `-a` en `-k` parameters of set Hallo **AZURE\_opslag\_ACCOUNT** en **AZURE\_opslag\_toegang\_sleutel** omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="7e84f-146">You must either specify hello storage account name that contains hello blob by using hello `-a` and `-k` parameters, or set hello **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="7e84f-147">Zie < een href = "hdinsight-upload-data.md" target = "_blank" voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7e84f-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="7e84f-148">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="7e84f-148">Limitations</span></span>
* <span data-ttu-id="7e84f-149">Bulk-export - met Linux gebaseerde HDInsight, Hallo Sqoop connector die wordt gebruikt tooexport gegevens tooMicrosoft SQL Server of Azure SQL Database biedt momenteel geen ondersteuning voor bulksgewijs invoegen.</span><span class="sxs-lookup"><span data-stu-id="7e84f-149">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="7e84f-150">Batchverwerking - met HDInsight op basis van Linux bij gebruik van Hallo `-batch` bij het uitvoeren van invoeg-switch, Sqoop meerdere invoegen in plaats van batchverwerking Hallo insert-bewerkingen wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7e84f-150">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching hello insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="7e84f-151">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="7e84f-151">Summary</span></span>
<span data-ttu-id="7e84f-152">Zoals wordt beschreven in dit document, kunt u een onbewerkte HTTP-aanvraag toorun, bewaken en Hallo resultaten weergeven met Sqoop taken op uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7e84f-152">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="7e84f-153">Zie voor meer informatie over Hallo REST-interface gebruikt in dit artikel Hallo <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST-API-handleiding</a>.</span><span class="sxs-lookup"><span data-stu-id="7e84f-153">For more information on hello REST interface used in this article, see hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e84f-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7e84f-154">Next steps</span></span>
<span data-ttu-id="7e84f-155">Voor algemene informatie over Hive met HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7e84f-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="7e84f-156">Sqoop gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e84f-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="7e84f-157">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7e84f-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="7e84f-158">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e84f-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7e84f-159">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e84f-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="7e84f-160">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e84f-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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



---
title: aaaUnderstand en los WebHCat fouten op HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe tooabout veelvoorkomende fouten geretourneerd door WebHCat in HDInsight en hoe tooresolve ze.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="d87e5-103">Begrijpen en oplossen van fouten die zijn ontvangen van WebHCat in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d87e5-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="d87e5-104">Meer informatie over fouten die zijn ontvangen bij het gebruik van WebHCat met HDInsight en hoe tooresolve ze.</span><span class="sxs-lookup"><span data-stu-id="d87e5-104">Learn about errors received when using WebHCat with HDInsight, and how tooresolve them.</span></span> <span data-ttu-id="d87e5-105">WebHCat wordt intern gebruikt door de client-side '-hulpprogramma's zoals Azure PowerShell en Hallo Data Lake Tools voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d87e5-105">WebHCat is used internally by client-side tools such as Azure PowerShell and hello Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="d87e5-106">Wat is WebHCat</span><span class="sxs-lookup"><span data-stu-id="d87e5-106">What is WebHCat</span></span>

<span data-ttu-id="d87e5-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is een REST-API voor [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), een tabel en storage management-laag voor Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d87e5-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="d87e5-108">WebHCat is standaard ingeschakeld op HDInsight-clusters en wordt gebruikt door verschillende hulpprogramma's voor toosubmit taken, kunt u de status van taak, enz. zonder logboekregistratie in toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="d87e5-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools toosubmit jobs, get job status, etc. without logging in toohello cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="d87e5-109">Configuratie wijzigen</span><span class="sxs-lookup"><span data-stu-id="d87e5-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d87e5-110">Aantal Hallo fouten die in dit document optreden als een geconfigureerde maximum is overschreden.</span><span class="sxs-lookup"><span data-stu-id="d87e5-110">Several of hello errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="d87e5-111">Wanneer Hallo resolutie stap u kunt een waarde wijzigen noemt, moet u een Hallo na wijziging van tooperform hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d87e5-111">When hello resolution step mentions that you can change a value, you must use one of hello following tooperform hello change:</span></span>

* <span data-ttu-id="d87e5-112">Voor **Windows** clusters: een script tooconfigure Hallo actiewaarde gebruiken tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="d87e5-112">For **Windows** clusters: Use a script action tooconfigure hello value during cluster creation.</span></span> <span data-ttu-id="d87e5-113">Zie voor meer informatie [ontwikkelen scriptacties](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="d87e5-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="d87e5-114">Voor **Linux** clusters: gebruik Ambari (web of REST-API) toomodify Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="d87e5-114">For **Linux** clusters: Use Ambari (web or REST API) toomodify hello value.</span></span> <span data-ttu-id="d87e5-115">Zie voor meer informatie [beheren HDInsight met Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="d87e5-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d87e5-116">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="d87e5-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d87e5-117">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d87e5-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="d87e5-118">Standaardconfiguratie</span><span class="sxs-lookup"><span data-stu-id="d87e5-118">Default configuration</span></span>

<span data-ttu-id="d87e5-119">Als Hallo na standaardwaarden zijn overschreden, kan deze WebHCat prestaties verslechteren of er fouten optreden:</span><span class="sxs-lookup"><span data-stu-id="d87e5-119">If hello following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="d87e5-120">Instelling</span><span class="sxs-lookup"><span data-stu-id="d87e5-120">Setting</span></span> | <span data-ttu-id="d87e5-121">Wat het doet</span><span class="sxs-lookup"><span data-stu-id="d87e5-121">What it does</span></span> | <span data-ttu-id="d87e5-122">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="d87e5-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d87e5-123">[yarn.scheduler.Capacity.maximum-toepassingen][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="d87e5-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="d87e5-124">maximum aantal taken dat gelijktijdig actief kunnen zijn Hallo (in behandeling of wordt uitgevoerd)</span><span class="sxs-lookup"><span data-stu-id="d87e5-124">hello maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="d87e5-125">10.000</span><span class="sxs-lookup"><span data-stu-id="d87e5-125">10,000</span></span> |
| <span data-ttu-id="d87e5-126">[templeton.Exec.Max-processor][max-procs]</span><span class="sxs-lookup"><span data-stu-id="d87e5-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="d87e5-127">Hallo kunt u het maximum aantal aanvragen dat gelijktijdig kunnen worden geleverd</span><span class="sxs-lookup"><span data-stu-id="d87e5-127">hello maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="d87e5-128">20</span><span class="sxs-lookup"><span data-stu-id="d87e5-128">20</span></span> |
| <span data-ttu-id="d87e5-129">[mapreduce.jobhistory.Max-leeftijd-ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="d87e5-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="d87e5-130">het aantal dagen dat de taakgeschiedenis Hallo blijven behouden</span><span class="sxs-lookup"><span data-stu-id="d87e5-130">hello number of days that job history are retained</span></span> |<span data-ttu-id="d87e5-131">7 dagen</span><span class="sxs-lookup"><span data-stu-id="d87e5-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="d87e5-132">Te veel aanvragen</span><span class="sxs-lookup"><span data-stu-id="d87e5-132">Too many requests</span></span>

<span data-ttu-id="d87e5-133">**HTTP-statuscode**: 429</span><span class="sxs-lookup"><span data-stu-id="d87e5-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="d87e5-134">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d87e5-134">Cause</span></span> | <span data-ttu-id="d87e5-135">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d87e5-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="d87e5-136">Hallo maximum aantal gelijktijdige aanvragen afgehandeld door WebHCat per minuut (standaard 20) is overschreden</span><span class="sxs-lookup"><span data-stu-id="d87e5-136">You have exceeded hello maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="d87e5-137">Uw werkbelasting tooensure dat u niet verzenden van meer dan Hallo maximum aantal gelijktijdige aanvragen of Hallo gelijktijdige aanvraaglimiet door het wijzigen van verhogen verminderen `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="d87e5-137">Reduce your workload tooensure that you do not submit more than hello maximum number of concurrent requests or increase hello concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="d87e5-138">Zie voor meer informatie [configuratie wijzigen](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="d87e5-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="d87e5-139">Server niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="d87e5-139">Server unavailable</span></span>

<span data-ttu-id="d87e5-140">**HTTP-statuscode**: 503</span><span class="sxs-lookup"><span data-stu-id="d87e5-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="d87e5-141">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d87e5-141">Cause</span></span> | <span data-ttu-id="d87e5-142">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d87e5-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="d87e5-143">Deze statuscode treedt meestal op tijdens de failover tussen Hallo primaire en secundaire HeadNode voor Hallo-cluster</span><span class="sxs-lookup"><span data-stu-id="d87e5-143">This status code usually occurs during failover between hello primary and secondary HeadNode for hello cluster</span></span> |<span data-ttu-id="d87e5-144">Wacht twee minuten en probeer opnieuw Hallo</span><span class="sxs-lookup"><span data-stu-id="d87e5-144">Wait two minutes, then retry hello operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="d87e5-145">Onjuiste aanvraag inhoud: kan de taak niet vinden.</span><span class="sxs-lookup"><span data-stu-id="d87e5-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="d87e5-146">**HTTP-statuscode**: 400</span><span class="sxs-lookup"><span data-stu-id="d87e5-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="d87e5-147">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d87e5-147">Cause</span></span> | <span data-ttu-id="d87e5-148">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d87e5-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="d87e5-149">Taakdetails zijn opgeschoond door Hallo Taakgeschiedenis schoner</span><span class="sxs-lookup"><span data-stu-id="d87e5-149">Job details have been cleaned up by hello job history cleaner</span></span> |<span data-ttu-id="d87e5-150">bewaartermijn voor Taakgeschiedenis Hallo is 7 dagen.</span><span class="sxs-lookup"><span data-stu-id="d87e5-150">hello default retention period for job history is 7 days.</span></span> <span data-ttu-id="d87e5-151">Hallo bewaartermijn kan worden gewijzigd door het wijzigen van `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="d87e5-151">hello default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="d87e5-152">Zie voor meer informatie [configuratie wijzigen](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="d87e5-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="d87e5-153">Taak is afgebroken vanwege tooa failover</span><span class="sxs-lookup"><span data-stu-id="d87e5-153">Job has been killed due tooa failover</span></span> |<span data-ttu-id="d87e5-154">Verzending van de taak voor up tootwo minuten opnieuw proberen</span><span class="sxs-lookup"><span data-stu-id="d87e5-154">Retry job submission for up tootwo minutes</span></span> |
| <span data-ttu-id="d87e5-155">Er is een ongeldige taak-id gebruikt</span><span class="sxs-lookup"><span data-stu-id="d87e5-155">An Invalid job id was used</span></span> |<span data-ttu-id="d87e5-156">Controleer als Hallo taak-id juist is</span><span class="sxs-lookup"><span data-stu-id="d87e5-156">Check if hello job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="d87e5-157">Ongeldige gateway</span><span class="sxs-lookup"><span data-stu-id="d87e5-157">Bad gateway</span></span>

<span data-ttu-id="d87e5-158">**HTTP-statuscode**: 502</span><span class="sxs-lookup"><span data-stu-id="d87e5-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="d87e5-159">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d87e5-159">Cause</span></span> | <span data-ttu-id="d87e5-160">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d87e5-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="d87e5-161">Interne garbagecollection plaatsvindt binnen Hallo WebHCat-proces</span><span class="sxs-lookup"><span data-stu-id="d87e5-161">Internal garbage collection is occurring within hello WebHCat process</span></span> |<span data-ttu-id="d87e5-162">Wacht totdat garbagecollection verzameling toofinish of Hallo WebHCat-service opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="d87e5-162">Wait for garbage collection toofinish or restart hello WebHCat service</span></span> |
| <span data-ttu-id="d87e5-163">Time-out opgetreden bij het wachten op een reactie van Hallo ResourceManager service.</span><span class="sxs-lookup"><span data-stu-id="d87e5-163">Time out waiting on a response from hello ResourceManager service.</span></span> <span data-ttu-id="d87e5-164">Deze fout kan optreden wanneer het aantal actieve toepassingen Hallo maximum Hallo geconfigureerd (standaard 10.000 gaat)</span><span class="sxs-lookup"><span data-stu-id="d87e5-164">This error can occur when hello number of active applications goes hello configured maximum (default 10,000)</span></span> |<span data-ttu-id="d87e5-165">Wachten tot taken toocomplete momenteel wordt uitgevoerd of Hallo gelijktijdige taaklimiet verhogen door het wijzigen van `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="d87e5-165">Wait for currently running jobs toocomplete or increase hello concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="d87e5-166">Zie voor meer informatie, Hallo [wijzigen configuratie](#modifying-configuration) sectie.</span><span class="sxs-lookup"><span data-stu-id="d87e5-166">For more information, see hello [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="d87e5-167">Poging tooretrieve alle taken via Hallo [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) aanroep bij `Fields` te is ingesteld`*`</span><span class="sxs-lookup"><span data-stu-id="d87e5-167">Attempting tooretrieve all jobs through hello [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set too`*`</span></span> |<span data-ttu-id="d87e5-168">Geen opgehaald *alle* taakgegevens.</span><span class="sxs-lookup"><span data-stu-id="d87e5-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="d87e5-169">Gebruik in plaats daarvan `jobid` tooretrieve details voor taken alleen groter is dan een bepaalde taak-id. Of gebruik geen`Fields`</span><span class="sxs-lookup"><span data-stu-id="d87e5-169">Instead use `jobid` tooretrieve details for jobs only greater than certain job id. Or, do not use `Fields`</span></span> |
| <span data-ttu-id="d87e5-170">Hallo WebHCat-service is niet actief tijdens de failover HeadNode</span><span class="sxs-lookup"><span data-stu-id="d87e5-170">hello WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="d87e5-171">Wacht twee minuten en probeer Hallo opnieuw</span><span class="sxs-lookup"><span data-stu-id="d87e5-171">Wait for two minutes and retry hello operation</span></span> |
| <span data-ttu-id="d87e5-172">Er zijn meer dan 500 in behandeling zijnde taken die worden verzonden via WebHCat</span><span class="sxs-lookup"><span data-stu-id="d87e5-172">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="d87e5-173">Wacht totdat het momenteel in behandeling zijnde taken vóór het verzenden van meer taken zijn voltooid</span><span class="sxs-lookup"><span data-stu-id="d87e5-173">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml

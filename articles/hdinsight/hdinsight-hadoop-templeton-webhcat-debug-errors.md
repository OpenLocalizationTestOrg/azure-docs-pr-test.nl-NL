---
title: Begrijpen en los fouten op HDInsight - Azure WebHCat | Microsoft Docs
description: Informatie over hoe voor informatie over veelvoorkomende fouten geretourneerd door WebHCat in HDInsight en hoe u deze kunt oplossen.
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
ms.openlocfilehash: 6d8162e0d64ec9fc42690392b7c822593c0c2767
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="bc5ec-103">Begrijpen en oplossen van fouten die zijn ontvangen van WebHCat in HDInsight</span><span class="sxs-lookup"><span data-stu-id="bc5ec-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="bc5ec-104">Meer informatie over fouten die zijn ontvangen bij het gebruik van WebHCat met HDInsight en hoe u deze kunt oplossen.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-104">Learn about errors received when using WebHCat with HDInsight, and how to resolve them.</span></span> <span data-ttu-id="bc5ec-105">WebHCat wordt intern gebruikt door de client-side '-hulpprogramma's zoals Azure PowerShell en Data Lake Tools voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-105">WebHCat is used internally by client-side tools such as Azure PowerShell and the Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="bc5ec-106">Wat is WebHCat</span><span class="sxs-lookup"><span data-stu-id="bc5ec-106">What is WebHCat</span></span>

<span data-ttu-id="bc5ec-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is een REST-API voor [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), een tabel en storage management-laag voor Hadoop.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="bc5ec-108">WebHCat is standaard ingeschakeld op HDInsight-clusters en wordt gebruikt door verschillende hulpprogramma's voor het verzenden van taken, taakstatus, enz. krijgen zonder in te loggen aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools to submit jobs, get job status, etc. without logging in to the cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="bc5ec-109">Configuratie wijzigen</span><span class="sxs-lookup"><span data-stu-id="bc5ec-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc5ec-110">Verschillende van de in dit document vermelde fouten optreden als een geconfigureerde maximum is overschreden.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-110">Several of the errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="bc5ec-111">Wanneer de stap resolutie u kunt een waarde wijzigen noemt, moet u een van de volgende gebruiken om uit te voeren van de wijziging:</span><span class="sxs-lookup"><span data-stu-id="bc5ec-111">When the resolution step mentions that you can change a value, you must use one of the following to perform the change:</span></span>

* <span data-ttu-id="bc5ec-112">Voor **Windows** clusters: het gebruik van een scriptactie voor het configureren van de waarde tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-112">For **Windows** clusters: Use a script action to configure the value during cluster creation.</span></span> <span data-ttu-id="bc5ec-113">Zie voor meer informatie [ontwikkelen scriptacties](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="bc5ec-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="bc5ec-114">Voor **Linux** clusters: gebruik Ambari (web of REST-API) om de waarde te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-114">For **Linux** clusters: Use Ambari (web or REST API) to modify the value.</span></span> <span data-ttu-id="bc5ec-115">Zie voor meer informatie [beheren HDInsight met Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="bc5ec-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc5ec-116">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bc5ec-117">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="bc5ec-118">Standaardconfiguratie</span><span class="sxs-lookup"><span data-stu-id="bc5ec-118">Default configuration</span></span>

<span data-ttu-id="bc5ec-119">Als de volgende standaardwaarden zijn overschreden, kan de WebHCat prestaties verslechteren of er fouten optreden:</span><span class="sxs-lookup"><span data-stu-id="bc5ec-119">If the following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="bc5ec-120">Instelling</span><span class="sxs-lookup"><span data-stu-id="bc5ec-120">Setting</span></span> | <span data-ttu-id="bc5ec-121">Wat het doet</span><span class="sxs-lookup"><span data-stu-id="bc5ec-121">What it does</span></span> | <span data-ttu-id="bc5ec-122">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="bc5ec-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc5ec-123">[yarn.scheduler.Capacity.maximum-toepassingen][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="bc5ec-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="bc5ec-124">Het maximum aantal taken dat gelijktijdig actief kunnen zijn (in behandeling of wordt uitgevoerd)</span><span class="sxs-lookup"><span data-stu-id="bc5ec-124">The maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="bc5ec-125">10.000</span><span class="sxs-lookup"><span data-stu-id="bc5ec-125">10,000</span></span> |
| <span data-ttu-id="bc5ec-126">[templeton.Exec.Max-processor][max-procs]</span><span class="sxs-lookup"><span data-stu-id="bc5ec-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="bc5ec-127">Het maximum aantal aanvragen dat gelijktijdig kunnen worden geleverd</span><span class="sxs-lookup"><span data-stu-id="bc5ec-127">The maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="bc5ec-128">20</span><span class="sxs-lookup"><span data-stu-id="bc5ec-128">20</span></span> |
| <span data-ttu-id="bc5ec-129">[mapreduce.jobhistory.Max-leeftijd-ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="bc5ec-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="bc5ec-130">Het aantal dagen dat de taakgeschiedenis worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-130">The number of days that job history are retained</span></span> |<span data-ttu-id="bc5ec-131">7 dagen</span><span class="sxs-lookup"><span data-stu-id="bc5ec-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="bc5ec-132">Te veel aanvragen</span><span class="sxs-lookup"><span data-stu-id="bc5ec-132">Too many requests</span></span>

<span data-ttu-id="bc5ec-133">**HTTP-statuscode**: 429</span><span class="sxs-lookup"><span data-stu-id="bc5ec-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="bc5ec-134">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="bc5ec-134">Cause</span></span> | <span data-ttu-id="bc5ec-135">Oplossing</span><span class="sxs-lookup"><span data-stu-id="bc5ec-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="bc5ec-136">U hebt het maximum aantal gelijktijdige aanvragen afgehandeld door WebHCat per minuut (standaard 20) overschreden</span><span class="sxs-lookup"><span data-stu-id="bc5ec-136">You have exceeded the maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="bc5ec-137">Verminder de werkbelasting om ervoor te zorgen dat u niet verzenden van meer dan het maximum aantal gelijktijdige aanvragen of verhoog de limiet voor gelijktijdige aanvragen door het wijzigen van `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-137">Reduce your workload to ensure that you do not submit more than the maximum number of concurrent requests or increase the concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="bc5ec-138">Zie voor meer informatie [configuratie wijzigen](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="bc5ec-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="bc5ec-139">Server niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="bc5ec-139">Server unavailable</span></span>

<span data-ttu-id="bc5ec-140">**HTTP-statuscode**: 503</span><span class="sxs-lookup"><span data-stu-id="bc5ec-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="bc5ec-141">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="bc5ec-141">Cause</span></span> | <span data-ttu-id="bc5ec-142">Oplossing</span><span class="sxs-lookup"><span data-stu-id="bc5ec-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="bc5ec-143">Deze statuscode treedt meestal op tijdens de failover tussen de primaire en secundaire HeadNode voor het cluster</span><span class="sxs-lookup"><span data-stu-id="bc5ec-143">This status code usually occurs during failover between the primary and secondary HeadNode for the cluster</span></span> |<span data-ttu-id="bc5ec-144">Wacht twee minuten en probeer het opnieuw</span><span class="sxs-lookup"><span data-stu-id="bc5ec-144">Wait two minutes, then retry the operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="bc5ec-145">Onjuiste aanvraag inhoud: kan de taak niet vinden.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="bc5ec-146">**HTTP-statuscode**: 400</span><span class="sxs-lookup"><span data-stu-id="bc5ec-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="bc5ec-147">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="bc5ec-147">Cause</span></span> | <span data-ttu-id="bc5ec-148">Oplossing</span><span class="sxs-lookup"><span data-stu-id="bc5ec-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="bc5ec-149">Taakdetails zijn opgeschoond door de taakgeschiedenis schoner</span><span class="sxs-lookup"><span data-stu-id="bc5ec-149">Job details have been cleaned up by the job history cleaner</span></span> |<span data-ttu-id="bc5ec-150">De bewaartermijn voor Taakgeschiedenis is 7 dagen.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-150">The default retention period for job history is 7 days.</span></span> <span data-ttu-id="bc5ec-151">De bewaartermijn kan worden gewijzigd door het wijzigen van `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-151">The default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="bc5ec-152">Zie voor meer informatie [configuratie wijzigen](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="bc5ec-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="bc5ec-153">Taak is afgebroken als gevolg van een failover</span><span class="sxs-lookup"><span data-stu-id="bc5ec-153">Job has been killed due to a failover</span></span> |<span data-ttu-id="bc5ec-154">Verzending van de taak voor maximaal twee minuten opnieuw proberen</span><span class="sxs-lookup"><span data-stu-id="bc5ec-154">Retry job submission for up to two minutes</span></span> |
| <span data-ttu-id="bc5ec-155">Er is een ongeldige taak-id gebruikt</span><span class="sxs-lookup"><span data-stu-id="bc5ec-155">An Invalid job id was used</span></span> |<span data-ttu-id="bc5ec-156">Controleer of de taak-id juist is</span><span class="sxs-lookup"><span data-stu-id="bc5ec-156">Check if the job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="bc5ec-157">Ongeldige gateway</span><span class="sxs-lookup"><span data-stu-id="bc5ec-157">Bad gateway</span></span>

<span data-ttu-id="bc5ec-158">**HTTP-statuscode**: 502</span><span class="sxs-lookup"><span data-stu-id="bc5ec-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="bc5ec-159">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="bc5ec-159">Cause</span></span> | <span data-ttu-id="bc5ec-160">Oplossing</span><span class="sxs-lookup"><span data-stu-id="bc5ec-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="bc5ec-161">Interne garbagecollection plaatsvindt in het proces van WebHCat</span><span class="sxs-lookup"><span data-stu-id="bc5ec-161">Internal garbage collection is occurring within the WebHCat process</span></span> |<span data-ttu-id="bc5ec-162">Wachten op garbagecollection voltooid of de WebHCat-service opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="bc5ec-162">Wait for garbage collection to finish or restart the WebHCat service</span></span> |
| <span data-ttu-id="bc5ec-163">Time-out opgetreden bij het wachten op een reactie van de ResourceManager-service.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-163">Time out waiting on a response from the ResourceManager service.</span></span> <span data-ttu-id="bc5ec-164">Deze fout kan optreden wanneer het aantal actieve toepassingen het geconfigureerde maximum (standaard 10.000 gaat)</span><span class="sxs-lookup"><span data-stu-id="bc5ec-164">This error can occur when the number of active applications goes the configured maximum (default 10,000)</span></span> |<span data-ttu-id="bc5ec-165">Wachten op de momenteel actieve taken om te voltooien of de gelijktijdige taaklimiet verhogen door het wijzigen van `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-165">Wait for currently running jobs to complete or increase the concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="bc5ec-166">Zie voor meer informatie de [wijzigen configuratie](#modifying-configuration) sectie.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-166">For more information, see the [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="bc5ec-167">Het ophalen van alle taken via de [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) aanroep bij `Fields` is ingesteld op`*`</span><span class="sxs-lookup"><span data-stu-id="bc5ec-167">Attempting to retrieve all jobs through the [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set to `*`</span></span> |<span data-ttu-id="bc5ec-168">Geen opgehaald *alle* taakgegevens.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="bc5ec-169">Gebruik in plaats daarvan `jobid` details voor taken alleen groter is dan een bepaalde taak-id ophalen.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-169">Instead use `jobid` to retrieve details for jobs only greater than certain job id.</span></span> <span data-ttu-id="bc5ec-170">Of gebruik geen`Fields`</span><span class="sxs-lookup"><span data-stu-id="bc5ec-170">Or, do not use `Fields`</span></span> |
| <span data-ttu-id="bc5ec-171">De WebHCat-service is niet actief tijdens de failover HeadNode</span><span class="sxs-lookup"><span data-stu-id="bc5ec-171">The WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="bc5ec-172">Wacht twee minuten en probeer het opnieuw</span><span class="sxs-lookup"><span data-stu-id="bc5ec-172">Wait for two minutes and retry the operation</span></span> |
| <span data-ttu-id="bc5ec-173">Er zijn meer dan 500 in behandeling zijnde taken die worden verzonden via WebHCat</span><span class="sxs-lookup"><span data-stu-id="bc5ec-173">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="bc5ec-174">Wacht totdat het momenteel in behandeling zijnde taken vóór het verzenden van meer taken zijn voltooid</span><span class="sxs-lookup"><span data-stu-id="bc5ec-174">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml

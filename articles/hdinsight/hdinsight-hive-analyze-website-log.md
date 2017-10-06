---
title: aaaUse Hive met Hadoop voor websitelogboekanalyse - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Hive met HDInsight tooanalyze website registreert. U hebt een logboekbestand gebruiken als invoer in een tabel met HDInsight en HiveQL tooquery Hallo gegevens worden gebruikt.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6fb7b5c2-8df4-40b1-a9e2-6815080004f9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 9cbce3cc8cf8bc3ad104dc4ca6a5628802c8fe89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a><span data-ttu-id="dfea5-104">Hive gebruiken met HDInsight op basis van Windows tooanalyze logboeken van websites</span><span class="sxs-lookup"><span data-stu-id="dfea5-104">Use Hive with Windows-based HDInsight tooanalyze logs from websites</span></span>
<span data-ttu-id="dfea5-105">Meer informatie over hoe toouse HiveQL met HDInsight tooanalyze registreert vanaf een website.</span><span class="sxs-lookup"><span data-stu-id="dfea5-105">Learn how toouse HiveQL with HDInsight tooanalyze logs from a website.</span></span> <span data-ttu-id="dfea5-106">Websitelogboekanalyse kunt gebruikte toosegment worden uw doelgroep op basis van soortgelijke activiteiten, categoriseren bezoekers door demografische gegevens en toofind uit Hallo inhoud die ze bekijken en Hallo websites die afkomstig zijn uit.</span><span class="sxs-lookup"><span data-stu-id="dfea5-106">Website log analysis can be used toosegment your audience based on similar activities, categorize site visitors by demographics, and toofind out hello content they view, hello websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dfea5-107">Hallo stappen in dit document alleen werken met HDInsight op basis van Windows-clusters.</span><span class="sxs-lookup"><span data-stu-id="dfea5-107">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="dfea5-108">HDInsight is alleen beschikbaar in Windows voor versies lager is dan HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="dfea5-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="dfea5-109">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="dfea5-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="dfea5-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dfea5-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="dfea5-111">In dit voorbeeld gebruikt u een HDInsight-cluster tooanalyze website logboek bestanden tooget inzicht in de frequentie van toohello-website bezoeken van externe websites Hallo in een dag.</span><span class="sxs-lookup"><span data-stu-id="dfea5-111">In this sample, you will use an HDInsight cluster tooanalyze website log files tooget insight into hello frequency of visits toohello website from external websites in a day.</span></span> <span data-ttu-id="dfea5-112">U hebt ook een overzicht van website-fouten die Hallo gebruikers ondervinden genereren.</span><span class="sxs-lookup"><span data-stu-id="dfea5-112">You'll also generate a summary of website errors that hello users experience.</span></span> <span data-ttu-id="dfea5-113">U leert hoe:</span><span class="sxs-lookup"><span data-stu-id="dfea5-113">You will learn how to:</span></span>

* <span data-ttu-id="dfea5-114">Verbinding maken met tooa Azure Blob storage, waarin de logboekbestanden van de website.</span><span class="sxs-lookup"><span data-stu-id="dfea5-114">Connect tooa Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="dfea5-115">Maken van HIVE-tabellen tooquery deze logboeken.</span><span class="sxs-lookup"><span data-stu-id="dfea5-115">Create HIVE tables tooquery those logs.</span></span>
* <span data-ttu-id="dfea5-116">HIVE-query's tooanalyze Hallo gegevens maken.</span><span class="sxs-lookup"><span data-stu-id="dfea5-116">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="dfea5-117">Microsoft Excel tooconnect tooHDInsight gebruiken (met behulp van open database connectivity (ODBC) tooretrieve hallo geanalyseerd-gegevens.</span><span class="sxs-lookup"><span data-stu-id="dfea5-117">Use Microsoft Excel tooconnect tooHDInsight (by using open database connectivity (ODBC) tooretrieve hello analyzed data.</span></span>

![HDI. Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="dfea5-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dfea5-119">Prerequisites</span></span>
* <span data-ttu-id="dfea5-120">U moet een Hadoop-cluster in Azure HDInsight hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="dfea5-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="dfea5-121">Zie voor instructies [HDInsight-Clusters inrichten][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="dfea5-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="dfea5-122">U moet Microsoft Excel 2013 of Excel 2010 is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="dfea5-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="dfea5-123">U moet hebben [stuurprogramma Microsoft Hive ODBC](http://www.microsoft.com/download/details.aspx?id=40886) tooimport gegevens van Hive in Excel.</span><span class="sxs-lookup"><span data-stu-id="dfea5-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) tooimport data from Hive into Excel.</span></span>

## <a name="toorun-hello-sample"></a><span data-ttu-id="dfea5-124">toorun Hallo-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="dfea5-124">toorun hello sample</span></span>
1. <span data-ttu-id="dfea5-125">Van Hallo [Azure Portal](https://portal.azure.com/), Hallo Startboard (als u er Hallo cluster hebt vastgemaakt), klik op Hallo cluster tegel waarop toorun Hallo voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="dfea5-125">From hello [Azure Portal](https://portal.azure.com/), from hello Startboard (if you pinned hello cluster there), click hello cluster tile on which you want toorun hello sample.</span></span>
2. <span data-ttu-id="dfea5-126">Bij Hallo cluster blade onder **snelkoppelingen**, klikt u op **Cluster-Dashboard**, en klik vervolgens vanuit Hallo **Cluster-Dashboard** blade, klikt u op **HDInsight-Cluster Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="dfea5-126">From hello cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from hello **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="dfea5-127">U kunt ook rechtstreeks Hallo dashboard openen met behulp van Hallo URL te volgen:</span><span class="sxs-lookup"><span data-stu-id="dfea5-127">Alternatively, you can directly open hello dashboard by using hello following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="dfea5-128">Wanneer u wordt gevraagd, kunt u verifiëren met behulp van Hallo beheerder-gebruikersnaam en wachtwoord die u hebt gebruikt bij het inrichten van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="dfea5-128">When prompted, authenticate by using hello administrator user name and password you used when provisioning hello cluster.</span></span>
3. <span data-ttu-id="dfea5-129">Van de webpagina Hallo dat wordt geopend, klikt u op Hallo **Getting Started galerie** tabblad en klik vervolgens onder Hallo **oplossingen met voorbeeldgegevens** categorie, klikt u op Hallo **Websitelogboekanalyse** voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="dfea5-129">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="dfea5-130">Volg de aanwijzingen Hallo van Hallo webpagina toofinish Hallo steekproef.</span><span class="sxs-lookup"><span data-stu-id="dfea5-130">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfea5-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dfea5-131">Next steps</span></span>
<span data-ttu-id="dfea5-132">Probeer Hallo voorbeeld te volgen: [analyseren van sensorgegevens met Hive met HDInsight](hdinsight-hive-analyze-sensor-data.md).</span><span class="sxs-lookup"><span data-stu-id="dfea5-132">Try hello following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png

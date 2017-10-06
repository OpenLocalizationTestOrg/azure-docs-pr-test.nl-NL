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
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a>Hive gebruiken met HDInsight op basis van Windows tooanalyze logboeken van websites
Meer informatie over hoe toouse HiveQL met HDInsight tooanalyze registreert vanaf een website. Websitelogboekanalyse kunt gebruikte toosegment worden uw doelgroep op basis van soortgelijke activiteiten, categoriseren bezoekers door demografische gegevens en toofind uit Hallo inhoud die ze bekijken en Hallo websites die afkomstig zijn uit.

> [!IMPORTANT]
> Hallo stappen in dit document alleen werken met HDInsight op basis van Windows-clusters. HDInsight is alleen beschikbaar in Windows voor versies lager is dan HDInsight 3.4. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

In dit voorbeeld gebruikt u een HDInsight-cluster tooanalyze website logboek bestanden tooget inzicht in de frequentie van toohello-website bezoeken van externe websites Hallo in een dag. U hebt ook een overzicht van website-fouten die Hallo gebruikers ondervinden genereren. U leert hoe:

* Verbinding maken met tooa Azure Blob storage, waarin de logboekbestanden van de website.
* Maken van HIVE-tabellen tooquery deze logboeken.
* HIVE-query's tooanalyze Hallo gegevens maken.
* Microsoft Excel tooconnect tooHDInsight gebruiken (met behulp van open database connectivity (ODBC) tooretrieve hallo geanalyseerd-gegevens.

![HDI. Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a>Vereisten
* U moet een Hadoop-cluster in Azure HDInsight hebt ingericht. Zie voor instructies [HDInsight-Clusters inrichten][hdinsight-provision].
* U moet Microsoft Excel 2013 of Excel 2010 is geïnstalleerd.
* U moet hebben [stuurprogramma Microsoft Hive ODBC](http://www.microsoft.com/download/details.aspx?id=40886) tooimport gegevens van Hive in Excel.

## <a name="toorun-hello-sample"></a>toorun Hallo-voorbeeld
1. Van Hallo [Azure Portal](https://portal.azure.com/), Hallo Startboard (als u er Hallo cluster hebt vastgemaakt), klik op Hallo cluster tegel waarop toorun Hallo voorbeeld.
2. Bij Hallo cluster blade onder **snelkoppelingen**, klikt u op **Cluster-Dashboard**, en klik vervolgens vanuit Hallo **Cluster-Dashboard** blade, klikt u op **HDInsight-Cluster Dashboard**. U kunt ook rechtstreeks Hallo dashboard openen met behulp van Hallo URL te volgen:

         https://<clustername>.azurehdinsight.net

    Wanneer u wordt gevraagd, kunt u verifiëren met behulp van Hallo beheerder-gebruikersnaam en wachtwoord die u hebt gebruikt bij het inrichten van Hallo-cluster.
3. Van de webpagina Hallo dat wordt geopend, klikt u op Hallo **Getting Started galerie** tabblad en klik vervolgens onder Hallo **oplossingen met voorbeeldgegevens** categorie, klikt u op Hallo **Websitelogboekanalyse** voorbeeld.
4. Volg de aanwijzingen Hallo van Hallo webpagina toofinish Hallo steekproef.

## <a name="next-steps"></a>Volgende stappen
Probeer Hallo voorbeeld te volgen: [analyseren van sensorgegevens met Hive met HDInsight](hdinsight-hive-analyze-sensor-data.md).

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png

---
title: aaaAnalyze sensorgegevens met behulp van Hive en Hadoop - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe tooanalyze sensorgegevens met behulp van Hallo Query Console Hive met HDInsight (Hadoop) en vervolgens visualiseren Hallo-gegevens in Microsoft Excel met PowerView.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 70e595705c33d9835dc9809161f79c3ac5ece870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a>Hallo Hive-Query-Console gebruiken met Hadoop in HDInsight-sensorgegevens analyseren

Meer informatie over hoe tooanalyze sensorgegevens met behulp van Hallo Query Console Hive met HDInsight (Hadoop) en vervolgens Hallo-gegevens in Microsoft Excel visualiseren met behulp van Power View.

> [!IMPORTANT]
> Hallo stappen in dit document alleen werken met HDInsight op basis van Windows-clusters. HDInsight is alleen beschikbaar in Windows voor versies lager is dan HDInsight 3.4. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.


In dit voorbeeld gebruikt u Hive tooprocess historische gegevens en identificeren van problemen met verwarming en airconditioning systemen. In het bijzonder het identificeren van systemen zijn tooreliably kan niet een set temperaturen onderhouden door Hallo volgende taken uitvoeren:

* Maken van HIVE-tabellen tooquery opgeslagen gegevens in bestanden met door komma's gescheiden waarden (CSV).
* HIVE-query's tooanalyze Hallo gegevens maken.
* tooretrieve hello geanalyseerd gegevens, gebruikt u Microsoft Excel tooconnect tooHDInsight.
* toovisualize hello gegevens, gebruikt u Power View.

![Een diagram van architectuur Hallo-oplossing](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a>Vereisten

* Een HDInsight (Hadoop)-cluster: Zie [maken Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) voor meer informatie over het maken van een cluster.
* Microsoft Excel 2013

  > [!NOTE]
  > Microsoft Excel wordt gebruikt voor gegevensvisualisatie met [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).

* [Microsoft Hive ODBC-stuurprogramma](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a>toorun Hallo-voorbeeld

1. Navigeer vanuit de webbrowser toohello volgende URL: 

         https://<clustername>.azurehdinsight.net

    Vervang `<clustername>` met Hallo-naam van uw HDInsight-cluster.

    Wanneer u wordt gevraagd, kunt u verifiëren met behulp van Hallo beheerder-gebruikersnaam en wachtwoord die u hebt gebruikt bij het inrichten van dit cluster.

2. Van de webpagina Hallo dat wordt geopend, klikt u op Hallo **Getting Started galerie** tabblad en klik vervolgens onder Hallo **oplossingen met voorbeeldgegevens** categorie, klikt u op Hallo **Sensor Data-analyse** voorbeeld.

    ![Gestarte afbeelding ophalen](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. Volg de aanwijzingen Hallo van Hallo webpagina toofinish Hallo steekproef.

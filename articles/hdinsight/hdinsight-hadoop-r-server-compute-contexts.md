---
title: aaaCompute context opties voor R Server op HDInsight - Azure | Microsoft Docs
description: Meer informatie over Hallo verschillende rekenscenario context opties beschikbaar toousers met op HDInsight R Server
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0deb0b1c-4094-459b-94fc-ec9b774c1f8a
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3b0d0cc3caa390797dcff8c73d66cd3ad78bcaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="compute-context-options-for-r-server-on-hdinsight"></a>COMPUTE context opties voor R Server op HDInsight

Microsoft R Server op Azure HDInsight bepaalt hoe aanroepen uitgevoerd door de instelling Hallo compute-context. In dit artikel bevat een overzicht van Hallo-opties die beschikbaar toospecify of en hoe de uitvoering is geparallelliseerde over kernen van Hallo edge-knooppunt of HDInsight-cluster.

Hallo edge-knooppunt van een cluster biedt een handige locatie tooconnect toohello cluster en toorun uw R-scripts. Met een edge-knooppunt hebt u Hallo optie actief Hallo geparallelliseerde gedistribueerd functies van ScaleR over Hallo kernen van Hallo edge-knooppunt server. U kunt ook uitvoeren ze via Hallo knooppunten van het Hallo-cluster met behulp van ScaleR verminderen van Hadoop-kaart of Spark compute-contexten.

## <a name="microsoft-r-server-on-azure-hdinsight"></a>Microsoft R Server op Azure HDInsight
[Microsoft R Server op Azure HDInsight](hdinsight-hadoop-r-server-overview.md) Hallo nieuwste mogelijkheden voor analyses op basis van R biedt. Het kan gebruiken gegevens die zijn opgeslagen in een HDFS-container in uw [Azure Blob](../storage/common/storage-introduction.md "Azure Blob storage") storage-account, een Data Lake store of Hallo lokale Linux-bestandssysteem. Aangezien R Server is gebouwd op open-source R, wordt in Hallo R gebaseerde toepassingen die u bouwt Hallo 8000 + open-source R-pakketten kunnen toepassen. Ze kunnen ook gebruiken Hallo routines in [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler), van Microsoft big analytics gegevenspakket die is opgenomen in R Server.  

## <a name="compute-contexts-for-an-edge-node"></a>COMPUTE contexten voor een edge-knooppunt
In het algemeen een R-script wordt uitgevoerd in R Server op Hallo edge-knooppunt uitgevoerd binnen Hallo R-interpreter op dat knooppunt. Hallo-uitzonderingen zijn de stappen die een ScaleR functie aanroept. Hallo ScaleR aanroepen uitgevoerd in een compute-omgeving die wordt bepaald door de manier waarop u Hallo ScaleR compute context instelt.  Wanneer u uw R-script vanaf een edge-knooppunt uitvoeren, wordt de mogelijke waarden Hallo Hallo compute context zijn:

- lokale opeenvolgende (*'local'*)
- lokale parallel (*'localpar'*)
- Kaart verminderen
- Spark

Hallo *'local'* en *'localpar'* opties verschillen alleen in het **rxExec** aanroepen uitgevoerd. Ze beide uitgevoerd andere rx-functieaanroepen op een parallelle manier over alle beschikbare kernen tenzij anders opgegeven door middel van Hallo ScaleR **numCoresToUse** optie, bijvoorbeeld `rxOptions(numCoresToUse=6)`. Parallelle uitvoeringsopties bieden optimale prestaties.

Hallo volgende tabel geeft een overzicht van Hallo die verschillende compute context opties tooset hoe aanroepen uitgevoerd:

| COMPUTE-context  | Hoe tooset                      | Uitvoeringscontext                        |
| ---------------- | ------------------------------- | ---------------------------------------- |
| Lokale sequentiële | rxSetComputeContext('local')    | Uitvoering geparallelliseerde over Hallo kernen van Hallo edge-knooppunt-server, met uitzondering van rxExec-aanroepen, opeenvolgend worden uitgevoerd |
| Lokale parallel   | rxSetComputeContext('localpar') | Uitvoering geparallelliseerde over Hallo kernen van Hallo edge-knooppunt server |
| Spark            | RxSpark()                       | Geparallelliseerde gedistribueerde uitvoering via Spark op Hallo-knooppunten van Hallo HDI-cluster |
| Kaart verminderen       | RxHadoopMR()                    | Geparallelliseerde gedistribueerde uitvoeren via het verminderen van de kaart op Hallo-knooppunten van Hallo HDI-cluster |

## <a name="guidelines-for-deciding-on-a-compute-context"></a>Richtlijnen voor het kiezen van een compute-context

Welke van Hallo drie opties die u kiest die geparallelliseerde uitvoering bieden is afhankelijk van Hallo aard van uw werk analytics, Hallo grootte en Hallo-locatie van uw gegevens. Er is geen eenvoudige formule waarin wordt uitgelegd welke context toouse berekenen. Er zijn echter enkele principes waarmee u bij het maken van de juiste keuze Hallo of ten minste, zodat u kunt beperken uw keuzes gemaakt voordat u een benchmark uitvoert. Deze richtsnoer omvatten:

- Hallo lokale Linux-bestandssysteem is sneller dan HDFS.
- Herhaalde analyses zijn sneller als Hallo gegevens lokaal is, en als het zich in XDF.
- Het is beter toostream kleine hoeveelheden gegevens uit een tekst-gegevensbron. Als Hallo hoeveelheid gegevens groter is, converteert u deze tooXDF voor analyse.
- Hallo-overhead voor het kopiëren of streaming Hallo gegevens toohello edge-knooppunt voor analyse wordt voor zeer grote hoeveelheden gegevens.
- Spark is sneller dan kaart verminderen voor analyse in Hadoop.

Deze principes gezien, bieden hello volgende secties een aantal algemene regels van miniatuur voor het selecteren van een compute-context.

### <a name="local"></a>Lokaal
* Als de hoeveelheid gegevens tooanalyze Hallo is klein en vereist geen herhaalde analyse, klikt u vervolgens stream deze rechtstreeks in het Hallo analysis routinematig gebruik *'local'* of *'localpar'*.
* Als Hallo hoeveelheid gegevens tooanalyze kleine of middelgrote en herhaalde analyse is vereist, vervolgens kopieert het lokale bestandssysteem toohello tooXDF importeren en analyseren via *'local'* of *'localpar'*.

### <a name="hadoop-spark"></a>Hadoop, Spark
* Als de hoeveelheid gegevens tooanalyze Hallo groot is, vervolgens importeren tooa Spark DataFrame met **RxHiveData** of **RxParquetData**, of tooXDF in HDFS (tenzij er een probleem is met de opslag), en analyseren met behulp van Hallo Spark COMPUTE context.

### <a name="hadoop-map-reduce"></a>Beperken van Hadoop-kaart
* Hallo kaart verminderen compute context alleen gebruiken als u een onoverkomelijke probleem met de Hallo Spark compute context optreden omdat in het algemeen langzamer.  

## <a name="inline-help-on-rxsetcomputecontext"></a>Inline-help op rxSetComputeContext
Voor meer informatie en voorbeelden van ScaleR compute contexten, raadpleegt u Hallo inline in R help op Hallo rxSetComputeContext methode, bijvoorbeeld:

    > ?rxSetComputeContext

U kunt ook verwijzen toohello '[ScaleR gedistribueerde Computing handleiding](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)' die beschikbaar is in Hallo [R Server MSDN](https://msdn.microsoft.com/library/mt674634.aspx "R Server op MSDN") bibliotheek.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd over Hallo-opties die beschikbaar toospecify zijn of en hoe de uitvoering is geparallelliseerde over kernen van Hallo edge-knooppunt of HDInsight-cluster. toolearn meer informatie over hoe toouse R Server met HDInsight-clusters, Zie Hallo volgende onderwerpen:

* [Overzicht van R Server voor Hadoop](hdinsight-hadoop-r-server-overview.md)
* [Aan de slag met R Server voor Hadoop](hdinsight-hadoop-r-server-get-started.md)
* [RStudio Server tooHDInsight toevoegen (indien niet worden toegevoegd tijdens het maken van het cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Opties voor Azure-opslag voor R Server op HDInsight](hdinsight-hadoop-r-server-storage.md)


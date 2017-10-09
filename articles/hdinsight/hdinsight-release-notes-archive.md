---
title: aaaArchived release-opmerkingen - Hadoop-onderdelen in Azure HDInsight | Microsoft Docs
description: Gearchiveerde release-opmerkingen voor oudere versies van Hadoop-onderdelen voor Azure HDInsight.
services: hdinsight
documentationcenter: 
editor: cgronlun
manager: jhubbard
author: nitinme
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 7a99c77f4557ca8c1dabe924cc67b2e0a134f8c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-archive-for-hadoop-components-on-azure-hdinsight"></a>Release-opmerkingen (archief) voor Hadoop-onderdelen op Azure HDInsight

In dit artikel bevat informatie over Hallo **oudere** Azure HDInsight LDR-updates. Zie voor informatie over meer recente versies, [HDInsight releaseopmerkingen](hdinsight-release-notes.md).

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie voor meer informatie [HDInsight versioning artikel](hdinsight-component-versioning.md).



## <a name="notes-for-08302016-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight 30-08-2016
Hallo volledige versienummers voor Linux gebaseerde HDInsight-clusters geïmplementeerd met deze release:

| HDI | HDI-cluster versie | HDP | HDP Build | Ambari-Build |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8268980 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8268980 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8269383 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

Hallo volledige versienummers voor HDInsight op basis van Windows-clusters geïmplementeerd met deze release:

| HDI | HDI-cluster versie | HDP | HDP Build |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1033.2559206 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1033.2559206 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1033.2559206 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1033.2559206 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1033.2559206 |2.3 |2.3.3.1-25 |


## <a name="08172016---release-of-r-server-on-hdinsight"></a>17-08-2016 - release van op HDInsight R Server
* R Server 8.0.5 - hoofdzakelijk een bug fix-release. Zie Hallo [R Server Release-opmerkingen](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes) voor meer informatie.
* AzureML-pakket op de edge-knooppunt Hallo - [dit pakket R](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) schakelt R modellen toobe gepubliceerd en gebruikt als een webservice Azure ML.  Zie Hallo ['Model operationeel'](hdinsight-hadoop-r-server-overview.md#operationalize-a-model) sectie van onze ['Overzicht van R Server op HDInsight'](hdinsight-hadoop-r-server-overview.md) artikel voor meer informatie.
* Linux-afhankelijkheden van Hallo [top 100 meest populaire R-pakketten](https://github.com/metacran/cranlogs) -deze pakketafhankelijkheden Linux worden nu vooraf geïnstalleerd.
* Optie toouse hello CRAN opslagplaats bij het toevoegen van R-pakketten toohello gegevensknooppunten. Zie voor meer informatie ['Aan de slag met R Server in HDInsight'](hdinsight-hadoop-r-server-get-started.md).
* Verbeterde Hallo betrouwbaarheid voor het leveren van R Server wanneer er clusters worden gemaakt.

## <a name="notes-for-08012016-release-of-hdinsight"></a>Opmerkingen voor 01/08/2016-release van HDInsight
Hallo volledige versienummers voor Linux gebaseerde HDInsight-clusters geïmplementeerd met deze release:

| HDI | HDI-cluster versie | HDP | HDP Build | Ambari-Build |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8028416 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8028416 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8053402 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

Hallo volledige versienummers voor HDInsight op basis van Windows-clusters geïmplementeerd met deze release:

| HDI | HDI-cluster versie | HDP | HDP Build |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1005.2488842 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1005.2488842 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1005.2488842 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1005.2488842 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1005.2488842 |2.3 |2.3.3.1-25 |

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type van het cluster (bijvoorbeeld Spark, Hadoop, HBase of Storm) | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| Wijzigingen tooHDInsight 3.4 clusters |Hallo standaardwaarden voor de volgende hive-configuraties zijn gewijzigd voor betere prestaties <ul><li>`hive.vectorized.execution.reduce.enabled=true`</li><li>`hive.tez.min.partition.factor=1f`</li><li>`hive.tez.max.partition.factor=3f`</li><li>`tez.shuffle-vertex-manager.min-src-fraction=0.9`</li><li>`tez.shuffle-vertex-manager.max-src-fraction=0.95`</li><li>`tez.runtime.shuffle.connect.timeout= 30000`</li></ul> |Service |Alle |N.v.t. |
| Volgende correcties zijn opgenomen in deze release |HIVE-13632, HIVE-12897,HIVE-12907,HIVE-12908,HIVE-12988,HIVE-13510,HIVE-13572,HIVE-13716,HIVE-13726,HIVE-12505,HIVE-13632,HIVE-13661,HIVE-13705,HIVE-13743,HIVE-13810,HIVE-13857,HIVE-13902,HIVE-13911,HIVE-13933 |Service |Alle |N.v.t. |

## <a name="notes-for-07142016-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight 14-07-2016
Hallo volledige versienummers voor Linux gebaseerde HDInsight-clusters geïmplementeerd met deze release:

| HDI | HDI-cluster versie | HDP | HDP Build | Ambari-Build |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7932505 |2.2 |2.2.9.1-11 |2.2.1.12-2 |
| 3.3 |3.3.1000.0.7932505 |2.3 |2.3.3.1-18 |2.2.1.12-2 |
| 3.4 |3.4.1000.0.7933003 |2.4 |2.4.2.0 |2.2.1.12-2 |

Hallo volledige versienummers voor HDInsight op basis van Windows-clusters geïmplementeerd met deze release:

| HDI | HDI-cluster versie | HDP | HDP Build |
| --- | --- | --- | --- |
| 2.1 |2.1.10.989.2441725 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.989.2441725 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.989.2441725 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.989.2441725 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.989.2441725 |2.3 |2.3.3.1-21 |

## <a name="notes-for-07072016-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight 07-07-2016
Hallo volledige versienummers voor Linux gebaseerde HDInsight-clusters geïmplementeerd met deze release:

| HDI | HDI-cluster versie | HDP | HDP Build |
| --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7864996 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.1000.0.7864996 |2.3 |2.3.3.1-18 |
| 3.4 |3.4.1000.0.7861906 |2.4 |2.4.2.0 |

Hallo volledige versienummers voor HDInsight op basis van Windows-clusters geïmplementeerd met deze release:

| HDI | HDI-cluster versie | HDP | HDP Build |
| --- | --- | --- | --- |
| 2.1 |2.1.10.977.2413853 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.977.2413853 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.977.2413853 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.977.2413853 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.977.2413853 |2.3 |2.3.3.1-21 |

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type van het cluster (bijvoorbeeld Spark, Hadoop, HBase of Storm) | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| [HDInsight Tools for IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md) |Invoegtoepassing voor IntelliJ IDEA voor HDInsight Spark-clusters is nu geïntegreerd met Azure Toolkit voor IntelliJ. Deze biedt ondersteuning voor Azure SDK v2.9.1, meest recente Java SDK's, en alle Hallo functies van Hallo zelfstandige HDInsight Plugin voor IntelliJ bevat. |Hulpprogramma's |Spark |N.v.t. |
| [HDInsight Tools voor Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md) |Azure Toolkit voor Eclipse ondersteunt nu HDInsight Spark-clusters. Hiermee kunt Hallo volgende kenmerken: <ul><li>Maken en een Spark-toepassing eenvoudig in Scala en Java schrijven met de eerste klasse voor het ontwerpen van ondersteuning voor IntelliSense auto-indeling, foutcontrole, enzovoort.</li><li>Hallo Spark-toepassing lokaal testen.</li><li>Verzenden van taken tooHDInsight Spark-cluster en Hallo resultaten ophalen.</li><li>TooAzure aanmelden en toegang tot alle Hallo Spark-clusters die zijn gekoppeld aan uw Azure-abonnementen.</li><li>Navigeer alle Hallo gekoppeld storage-resources van uw HDInsight Spark-cluster.</li></ul> |Hulpprogramma's |Spark |N.v.t. |

Vanaf deze release, hebben we Hallo Gast OS patch beleid voor Linux gebaseerde HDInsight-clusters gewijzigd. Hallo-doel van het nieuwe beleid Hallo is toosignificantly Verminder het aantal herstarts Hallo vanwege toopatching. elke maandag of donderdag begint bij 12: 00 A.M. UTC op een wijze gespreid over de knooppunten in een bepaald cluster Hallo nieuwe beleid patches virtuele machines (VM's) op Linux-clusters. Echter een bepaalde virtuele machine alleen wordt opnieuw opgestart vanwege tooguest OS patches maximaal één keer elke 30 dagen. Bovendien Hallo eerste keer opnieuw opstarten voor een nieuw cluster gebeurt niet eerder zijn dan 30 dagen na de aanmaakdatum Hallo-cluster.

> [!NOTE]
> Deze wijzigingen zijn alleen van toepassing toonewly clusters gemaakt gelijk of groter dan deze versie.
>
>

## <a name="notes-for-06062016-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight 06-06-2016
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

| HDP | HDI-versie | Spark versie | Ambari-Build-nummer | HDP Build-nummer |
| --- | --- | --- | --- | --- |
| 2.3 |3.3.1000.0.7702215 |1.5.2 |2.2.1.8-2 |2.3.3.1-18 |
| 2.4 |3.4.1000.0.7702224 |1.6.1 |2.2.1.8-2 |2.4.2.0 |

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type van het cluster (bijvoorbeeld Spark, Hadoop, HBase of Storm) | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| Spark in HDInsight is algemeen beschikbaar |Deze versie biedt verbeteringen in de beschikbaarheid, schaalbaarheid en productiviteit tooopen bron Apache Spark in HDInsight. <ul><li>De toonaangevende beschikbaarheids-SLA van 99,9%, waardoor het geschikt is voor veeleisende werklast.</li><li>Schaalbare opslaglaag met behulp van Azure Data Lake Store.</li><li>Productiviteitsprogramma's voor elke fase van gegevensverkenning en ontwikkeling. Jupyter-notebooks met aangepaste Spark kernel inschakelen interactieve gegevensverkenning, integratie met BI-dashboards zoals Power BI, Tableau en Qlik is geschikt is voor het delen van gegevens snel en continue rapportage, IntelliJ-invoegtoepassing is betrouwbare optie voor de lange termijn code artefact ontwikkeling en foutopsporing.</li></ul> |Service |Spark |N.v.t. |
| HDInsight Tools for IntelliJ |Dit is een invoegtoepassing voor IntelliJ IDEA voor HDInsight Spark-clusters. Hiermee kunt Hallo volgende kenmerken:<ul><li>Maken en een Spark-toepassing eenvoudig in Scala en Java schrijven met de eerste klasse voor het ontwerpen van ondersteuning voor IntelliSense auto-indeling, foutcontrole, enzovoort.</li><li>Hallo Spark-toepassing lokaal testen.</li><li>Verzenden van taken tooHDInsight Spark-cluster en Hallo resultaten ophalen.</li><li>TooAzure aanmelden en toegang tot alle Hallo Spark-clusters die zijn gekoppeld aan uw Azure-abonnementen.</li><li>Navigeer alle Hallo gekoppeld storage-resources van uw HDInsight Spark-cluster.</li><li>Navigeer alle Hallo taken geschiedenis en taak informatie voor uw HDInsight Spark-cluster.</li><li>Fouten opsporen in Spark taken op afstand vanaf uw computer.</li></ul> |Hulpprogramma's |Spark |N.v.t. |

## <a name="notes-for-05132016-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight 13-05-2016
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight (Windows) 2.1.10.875.2159884 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight (Windows) 3.0.6.875.2159884 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight (Windows) 3.1.4.922.2266903 (2.1.15.0-2374 HDP - ongewijzigd)
* HDInsight (Windows) 3.2.7.922.2266903 (HDP 2.2.9.1-11)
* HDInsight (Windows) 3.3.0.922.2266903 (HDP 2.3.3.1-18)
* HDInsight (Linux) 3.2.1000.0.7565644 (HDP 2.2.9.1-11)
* HDInsight (Linux) 3.3.1000.0.7565644 (HDP 2.3.3.1-18)
* HDInsight (Linux) 3.4.1000.0.7548380 (HDP 2.4.2.0)

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type van het cluster (bijvoorbeeld Spark, Hadoop, HBase of Storm) | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| Spark versie update en andere oplossingen voor problemen |Deze release versie van de Hallo Spark in HDInsight-cluster too1.6.1 updates en oplossingen van andere fouten |Service |Spark |N.v.t. |

## <a name="notes-for-04112016-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight 11-04-2016
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight (Windows) 2.1.10.889.2191206 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight (Windows) 3.0.6.889.2191206 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight (Windows) 3.1.4.889.2191206 (2.1.15.0-2374 HDP - ongewijzigd)
* HDInsight (Windows) 3.2.7.889.2191206 (HDP 2.2.9.1-10)
* HDInsight (Windows) 3.3.0.889.2191206 (HDP 2.3.3.1-16-ongewijzigd)
* HDInsight (Linux) 3.2.1000.0.7339916 (HDP 2.2.9.1-10)
* HDInsight (Linux) 3.3.1000.0.7339916 (HDP 2.3.3.1-16)
* HDInsight (Linux) 3.4.1000.0.7338911 (HDP 2.4.1.1-3)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| Aangepaste metastore upgrade problemen voor HDI 3.4 |Maken van het cluster mislukken als u een aangepaste metastore die eerder werd gebruikt op een lagere versie van een andere HDInsight-cluster gebruikt. Dit is vervallen tooan upgrade scriptfout die is nu opgelost |Maken van het cluster |Alle |N.v.t. |
| Crashherstelbewerking Livy |Taak status tolerantie biedt voor elke taak die is verzonden via Livy |Betrouwbaarheid |Spark op Linux |N.v.t. |
| Jupyter inhoud HA |Biedt Hallo mogelijkheid toosave en de belasting Jupyter-notebook inhoud tooand van Hallo storage-account is gekoppeld aan het Hallo-cluster. Zie voor meer informatie [beschikbare Kernels voor Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-kernels.md). |Laptops |Spark op Linux |N.v.t. |
| Verwijderen van hiveContext in Jupyter-Notebooks |Gebruik `%%sql` magische in plaats van `%%hive` verwerkt Magic-pakket. SqlContext is gelijkwaardig toohiveContext. Zie voor meer informatie [beschikbare Kernels voor Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-kernels.md) |Laptops |Spark-clusters op Linux |N.v.t. |
| Afschaffing van oudere versies van Spark |Oudere versie Spark 1.3.1 is verwijderd uit het Hallo-service op 5/31 |Service |Spark-clusters in Windows |N.v.t. |

## <a name="notes-for-03292016-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight 29-03-2016
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight (Windows) 2.1.10.875.2159884 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight (Windows) 3.0.6.875.2159884 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight (Windows) 3.1.4.875.2159884 (2.1.15.0-2374 HDP - ongewijzigd)
* HDInsight (Windows) 3.2.7.875.2159884 (2.2.9.1-7 HDP - ongewijzigd)
* HDInsight (Windows) 3.3.0.875.2159884 (HDP 2.3.3.1-16)
* HDInsight (Linux) 3.2.1000.0.7193255 (2.2.9.1-8 HDP - ongewijzigd)
* HDInsight (Linux) 3.3.1000.0.7193255 (2.3.3.1-7 HDP - ongewijzigd)
* HDInsight (Linux) 3.4.1000.0.7195842 (HDP 2.4.1.0-327)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| Toegevoegde 3.4 HDInsight-versie en bijgewerkte HDP versies voor alle HDInsight-clusters |Deze release we HDInsight v3.4 (op basis van HDP 2.4) hebt toegevoegd en andere versies HDP, ook al bijgewerkt. 2.4 HDP release-opmerkingen beschikbaar zijn [hier](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html) en meer informatie over de versies van HDInsight kan worden gevonden [hier](hdinsight-component-versioning.md). |Service |Alle Linux-clusters |N.v.t. |
| HDInsight Premium |HDInsight is nu beschikbaar in twee categorieën - Standard en Premium. HDInsight Premium is momenteel in Preview en alleen beschikbaar voor Hadoop en Spark-clusters op Linux. Zie voor meer informatie [hier](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium). |Service |Hadoop en Spark op Linux |N.v.t. |
| Microsoft R Server |HDInsight Premium biedt Microsoft R Server die opgenomen met Hadoop en Spark-clusters op Linux worden kunnen. Zie voor meer informatie [overzicht van op HDInsight R Server](hdinsight-hadoop-r-server-overview.md). |Service |Hadoop en Spark op Linux |N.v.t. |
| Spark 1.6.0 |3.4 HDInsight-clusters bevatten nu Spark 1.6.0 |Service |Spark-clusters op Linux |N.v.t. |
| Verbeteringen voor Jupyter-notebook |Jupyter-notebooks met Spark-clusters bieden aanvullende Spark nu kernels. Ze bevatten ook verbeteringen ten zoals het gebruik van %% magic, auto-visualisatie en integratie met Python visualisatie-bibliotheken (zoals matplotlib). Zie voor meer informatie [beschikbare Kernels voor Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-kernels.md). |Service |Spark-clusters op Linux |N.v.t. |

## <a name="notes-for-03222016-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight 22-03-2016
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight (Windows) 2.1.10.875.2159884 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight (Windows) 3.0.6.875.2159884 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight (Windows) 3.1.4.875.2159884 (2.1.15.0-2374 HDP - ongewijzigd)
* HDInsight (Windows) 3.2.7.875.2159884 (2.2.9.1-7 HDP - ongewijzigd)
* HDInsight (Windows) 3.3.0.875.2159884 (HDP 2.3.3.1-16)
* HDInsight (Linux) 3.2.1000.0.7193255 (2.2.9.1-8 HDP - ongewijzigd)
* HDInsight (Linux) 3.3.1000.0.7193255 (2.3.3.1-7 HDP - ongewijzigd)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| Bijgewerkte versies van HDInsight voor alle HDInsight-clusters |Met deze versie bijgewerkt HDInsight-versies voor alle HDInsight-clusters |Service |Alle |N.v.t. |

## <a name="notes-for-03102016-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight 10-03-2016
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight (Windows) 2.1.10.859.2123216 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight (Windows) 3.0.6.859.2123216 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight (Windows) 3.1.4.859.2123216 (2.1.15.0-2374 HDP - ongewijzigd)
* HDInsight (Windows) 3.2.7.859.2123216 (HDP 2.2.9.1-7)
* HDInsight (Windows) 3.3.0.859.2123216 (2.3.3.1-5 HDP - ongewijzigd)
* HDInsight (Linux) 3.2.1000.7076817 (HDP 2.2.9.1-8)
* HDInsight (Linux) 3.3.1000.7076817 (HDP 2.3.3.1-7)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| Bijgewerkte versies van HDInsight voor alle HDInsight-clusters |Met deze versie bijgewerkt HDInsight-versies voor alle HDInsight-clusters |Service |Alle |N.v.t. |

## <a name="notes-for-01272016-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight 27-01-2016
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight (Windows) 2.1.10.817.2028315 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight (Windows) 3.0.6.817.2028315 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight (Windows) 3.1.4.817.2028315 (2.1.15.0-2374 HDP - ongewijzigd)
* HDInsight (Windows) 3.2.7.817.2028315 (HDP 2.2.9.1-1)
* HDInsight (Windows) 3.3.0.817.2028315 (2.3.3.1-5 HDP - ongewijzigd)
* HDInsight (Linux) 3.2.1000.4072335 (HDP 2.2.9.1-1)
* HDInsight (Linux) 3.3.1000.4072335 (HDP 2.3.3.1-1)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| Bijgewerkte versies van HDInsight voor alle HDInsight-clusters |Met deze versie bijgewerkt HDInsight-versies voor alle HDInsight-clusters |Service |Alle |N.v.t. |

## <a name="notes-for-12022015-release-of-hdinsight"></a>Opmerkingen voor 02-12-2015-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight (Windows) 2.1.10.763.1931434 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight (Windows) 3.0.6.763.1931434 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight (Windows) 3.1.4.763.1931434 (2.1.15.0-2374 HDP - ongewijzigd)
* HDInsight (Windows) 3.2.7.763.1931434 (2.2.7.1-34 HDP - ongewijzigd)
* HDInsight (Windows) 3.3.1000.0 (HDP 2.3.3.1-5)
* HDInsight (Linux) 3.2.1000.0.6392801 (2.2.7.1-34 HDP - ongewijzigd)
* HDInsight (Linux) 3.3.1000.0 (HDP 2.3.3.0-3039)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| Toegevoegde 3.3 HDInsight-versie en bijgewerkte HDP versies voor alle HDInsight-clusters |Deze release we HDInsight v3.3 (op basis van HDP 2.3) hebt toegevoegd en andere versies HDP, ook al bijgewerkt. 2.3 HDP release-opmerkingen beschikbaar zijn [hier](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html) en meer informatie over de versies van HDInsight kan worden gevonden [hier](hdinsight-component-versioning.md). |Service |Alle |N.v.t. |

## <a name="notes-for-11302015-release-of-hdinsight"></a>Opmerkingen voor 30-11-2015-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight (Windows) 2.1.10.757.1923908 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight (Windows) 3.0.6.757.1923908 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight (Windows) 3.1.4.757.1923908 (2.1.15.0-2374 HDP - ongewijzigd)
* HDInsight (Windows) 3.2.7.757.1923908 (HDP 2.2.7.1-34)
* HDInsight (Linux) 3.2.1000.0.6392801 (HDP 2.2.7.1-34)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| Bijgewerkte versies van HDInsight voor alle HDInsight-clusters en HDP versies voor 3.2 HDInsight-clusters (Windows en Linux) |Met deze versie, zijn de versies van HDInsight en HDP bijgewerkt |Service |Alle |N.v.t. |

## <a name="notes-for-10272015-release-of-hdinsight"></a>Opmerkingen voor 27/10/2015-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight (Windows) 2.1.10.726.1866228 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight (Windows) 3.0.6.726.1866228 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight (Windows) 3.1.4.726.1866228 (2.1.15.0-2374 HDP - ongewijzigd)
* HDInsight (Windows) 3.2.7.726.1866228 (HDP 2.2.7.1-33)
* HDInsight (Linux) 3.2.1000.0.6035701 (HDP 2.2.7.1-33)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| Bijgewerkte versies van HDInsight voor alle HDInsight-clusters (Windows en Linux) |Met deze versie, zijn de versies van HDInsight en HDP bijgewerkt |Service |Alle |N.v.t. |
| Vaste Jupyter voor Windows Spark-clusters met hoofdletters clusters |Clusters die DNS-namen die zijn opgegeven in hoofdletters had heeft problemen met Jupyter-notebooks vanwege tooan oorsprong aanvraag selectievakje. Hallo fix is toochange Hallo DNS-naam voor de Jupyter configuratie toolower geval. |Service |HDInsight Spark (Windows) |N.v.t. |

## <a name="notes-for-10202015-release-of-hdinsight"></a>Opmerkingen voor 20-10-2015-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.716.1846990 (Windows) (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight 3.0.6.716.1846990 (Windows) (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight 3.1.4.716.1846990 (Windows) (HDP 2.1.16.0-2374)
* HDInsight 3.2.7.716.1846990 (Windows) (HDP 2.2.7.1-0004)
* HDInsight 3.2.1000.0.5930166 (Linux) (HDP 2.2.7.1-0004)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| Standaard HDP versie gewijzigd tooHDP 2.2 |de standaardversie Hallo voor HDInsight Windows-clusters is gewijzigde tooHDP 2.2. HDInsight versie 3.2 (HDP 2.2) is al in het algemeen beschikbaar is in sinds februari 2015. Deze wijziging alleen Hallo standaard cluster versie worden gespiegeld als een expliciete keuze niet heeft plaatsgevonden tijdens het Hallo-cluster met hello Azure-portal, PowerShell-cmdlets of Hallo SDK wordt ingericht. |Service |Alle |N.v.t. |
| Wijzigingen in de indeling van virtuele machine voor het implementeren van meerdere HDInsight op Linux-clusters in één virtueel netwerk |Ondersteuning voor het implementeren van meerdere HDInsight Linux-clusters in één virtueel netwerk wordt toegevoegd in deze release. Als onderdeel van update Hallo-indeling van de namen van de virtuele machine in Hallo-cluster is gewijzigd van headnode\*, workernode\* en zookeepernode\* toohn\*, omlaag\*, en zk\* respectievelijk. Het is niet een aanbevolen procedure tootake een directe afhankelijkheid op Hallo-indeling van de namen van de virtuele machine, aangezien dit onderwerp toochange. Gebruik 'hostname -f' op de lokale machine Hallo of Ambari APIs toodetermine Hallo lijst met hosts en Hallo toewijzing van onderdelen toohosts. U vindt meer informatie op [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md) en [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md). |Service |HDInsight-clusters op Linux |N.v.t. |
| Wijzigingen in de configuratie |Hallo volgende configuraties zijn nu beschikbaar voor 3.1 HDInsight-clusters: <ul><li>tez.yarn.ATS.Enabled en yarn.log.server.url. Hiermee kunnen Hallo toepassingsserver tijdlijn en Hallo logboek server toobe kunnen tooserve uit logboeken.</li></ul>Voor clusters van HDInsight 3.2, zijn Hallo volgende configuraties gewijzigd: <ul><li>mapreduce.fileoutputcommitter.Algorithm.Version is too2 ingesteld. Dit maakt gebruik van V2-versie Hallo Hallo FileOutputCommitter.</li></ul> |Service |Alle |N.v.t. |

## <a name="notes-for-09092015-release-of-hdinsight"></a>Opmerkingen voor 09-09/2015-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.675.1768697 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight 3.0.6.675.1768697 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight 3.1.4.675.1768697 (2.1.15.0-2334 HDP - ongewijzigd)
* HDInsight 3.2.6.675.1768697 (2.2.6.1-0012 HDP - ongewijzigd)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| Bijgewerkte versies van HDInsight voor alle HDInsight-clusters |Met deze release zijn HDInsight versies bijgewerkt |Service |Alle |N.v.t. |

## <a name="notes-for-07312015-release-of-hdinsight"></a>Opmerkingen voor 07/31/2015-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.640.1695824 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight 3.0.6.640.1695824 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight 3.1.4.640.1695824 (2.1.15.0-2334 HDP - ongewijzigd)
* HDInsight 3.2.6.640.1695824 (2.2.6.1-0012 HDP - ongewijzigd)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| Spark-cluster knooppunt teruggezet werkstroom oplossen |Een fout die was het gevolg van Spark clusterknooppunten toonot herstellen na het terugzetten van de installatiekopie vast |Service |Spark |N.v.t. |

## <a name="notes-for-07312015-release-of-hdinsight"></a>Opmerkingen voor 07/31/2015-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.635.1684502 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight 3.0.6.635.1684502 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight 3.1.4.635.1684502 (2.1.15.0-2334 HDP - ongewijzigd)
* HDInsight 3.2.6.635.1684502 (2.2.6.1-0012 HDP - ongewijzigd)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| Bijgewerkte versies van HDInsight voor alle HDInsight-clusters |Met deze release zijn HDInsight versies bijgewerkt |Service |Alle |N.v.t. |

## <a name="notes-for-07072015-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight 07-07-2015
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.610.1630216 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight 3.0.6.610.1630216 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight 3.1.4.610.1630216 (2.1.15.0-2334 HDP - ongewijzigd)
* HDInsight 3.2.4.610.1630216 (HDP 2.2.6.1-0012)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

| Titel | Beschrijving | Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK) | Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster | JIRA (indien van toepassing) |
| --- | --- | --- | --- | --- |
| Bijgewerkte HDP versies voor 3.2 HDInsight-clusters |Met deze versie implementeert 3.2 HDInsight HDP 2.2.6.1-0012 |Service |Alle |N.v.t. |

## <a name="notes-for-06262015-release-of-hdinsight"></a>Opmerkingen voor 06/26/2015-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.601.1610731 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight 3.0.6.601.1610731 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight 3.1.4.601.1610731 (2.1.15.0-2334 HDP - ongewijzigd)
* HDInsight 3.2.4.601.1610731 (HDP 2.2.6.1-0011)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

<table border="1">
<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK)</p></th>
<th>Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td>Bijgewerkte HDP versies voor 3.2 HDInsight-clusters</td>
<td>Met deze versie implementeert 3.2 HDInsight HDP 2.2.6.1</td>
<td>Service</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-06182015-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight 06-18-2015
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.596.1601657 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight 3.0.6.596.1601657 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight 3.1.4.596.1601657 (HDP 2.1.15.0-2334)
* HDInsight 3.2.4.596.1601657 (HDP 2.2.6.1-0002)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

<table border="1">
<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK)</p></th>
<th>Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td>Aanvullende HTTPS-poorten geopend</td>
<td>Hallo-cloudservice wordt nu geopend 5 poorten 8001 too8005 op Hallo cluster bijvoorbeeld op https://<clustername>.azurehdinsight.net:8001/. Aanvragen toothese URL's worden geverifieerd met behulp van dezelfde Hallo basisverificatie wachtwoord mechanisme als poort 443. Deze poorten binden toohello dezelfde op Hallo active headnode poort. Scriptacties kunnen gebruikte toomake klant services luisteren op deze poorten op Hallo headnode en route toooutside Hallo cluster zijn.</td>
<td>Cloudservice</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Onregelmatige MapReduce willekeurige volgorde probleem voor HDInsight 3.2</td>
<td>Oplossing voor een zeldzame, onregelmatige-race condition in willekeurige volgorde kaart verminderen op grote clusters, wat leidt tot mislukte incidentele taken. Zie <a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE 6361</a> voor meer informatie.</td>
<td>Hadoop-Core</td>
<td>Alle</td>
<td><a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a></td>
</tr>
<tr>
<td>TooLatest Azure Java SDK 2.2 voor HDInsight 3.2 verplaatsen</td>
<td>Toolatest versie van Azure SDK voor Java gebruikt door Hallo WASB stuurprogramma Hallo verplaatst. Hallo nieuwste SDK heeft enkele oplossingen en Hallo release-opmerkingen voor Hallo dezelfde zijn beschikbaar op https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt.</td>
<td>Hadoop-Core</td>
<td>Alle</td>
<td><a href="https://issues.apache.org/jira/browse/HADOOP-11959" target="_blank">HADOOP-11959</a></td>
</tr>
<tr>
<td>TooHDP 2.1.15 voor 3.1 HDInsight-clusters verplaatsen</td>
<td>Release-opmerkingen Hortonworks voor Hallo release beschikbaar zijn <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.15-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.15.html" target="_blank">hier</a>.</td>
<td>HDP</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-06042015-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight 06-04-2015
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.583.1575584 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight 3.0.6.583.1575584 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight 3.1.3.583.1575584 (2.1.12.1-0003 HDP - ongewijzigd)
* HDInsight 3.2.4.583.1575584 (HDP 2.2.6.1-1)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

<table border="1">
<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK)</p></th>
<th>Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td>Herstel voor 502 Ongeldige gateway-fout voor Storm-clusters</td>
<td>Deze release corrigeert een bug die invloed hebben op Hallo taak verzending API Hallo website toobe, waardoor omlaag na opnieuw opstarten.</td>
<td>Service</td>
<td>Storm</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-06012015-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight 06-01-2015
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.577.1563827 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight 3.0.6.577.1563827 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight 3.1.3.577.1563827 (2.1.12.1-0003 HDP - ongewijzigd))
* HDInsight 3.2.4.577.1563827 (2.2.6.0-2800 HDP - ongewijzigd)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

<table border="1">
<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK)</p></th>
<th>Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td>Verschillende oplossingen voor problemen</td>
<td>Deze release corrigeert bugs gerelateerde toocluster inrichten.</td>
<td>Service</td>
<td>Alle clustertypen</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-05272015-release-of-hdinsight"></a>Opmerkingen voor 05-27-2015-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 3.2.4.570.1554102 (HDP 2.2.6.0-2800)
* Andere clusterversies van het en de SDK worden niet geïmplementeerd als onderdeel van deze release.

Deze versie bevat Hallo volgende updates:

<table border="1">
<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK)</p></th>
<th>Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td>2.2 HDP update</td>
<td>Deze versie van HDInsight 3.2 HDP 2.2.6 bevat, en brengt enkele belangrijke bugfixes tooHDInsight. Hallo volledige release-opmerkingen zijn beschikbaar op <a href="http://dev.hortonworks.com.s3.amazonaws.com/HDPDocuments/HDP2/HDP-2.2.6/HDP_RelNotes_v226/index.html">HDP 2.2.6 releaseopmerkingen</a>.</td>
<td>HDP</td>
<td>Alle clustertypen</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>TooDefault Yarn Container geheugenconfiguratie wijzigen</td>
<td>In deze update Hallo beschikbaar geheugen tooYARN standaardcontainers (yarn.nodemanager.resource.memory mb en yarn.scheduler.maximum toewijzing mb) door knooppunt Manager gestart, is toegenomen too5632MB. Dit was eerder verminderde too4608MB, maar op basis van verschillende taak wordt uitgevoerd, nieuwe waarde Hallo moet bieden betere betrouwbaarheid en prestaties toomost taken, dus kan een betere standaard. Gebruikelijke als er kritieke afhankelijkheid van deze geheugenconfiguratie, stelt u deze expliciet tijdens het Hallo-cluster maken.</td>
<td>HDP</td>
<td>Alle clustertypen</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Standaard Config pariteit voor HBase en Storm-clusters</td>
<td>Deze update herstelt Hbase en Storm-clusters toouse Hallo dezelfde waarden van YARN configs als Hadoop-clusters. Dit wordt gedaan voor pariteit alle typen van de cluster.</td>
<td>HDP</td>
<td>HBase, Storm</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-05202015-release-of-hdinsight"></a>Opmerkingen voor 20-05-2015-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.564.1542093 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight 3.0.6.564.1542093 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight 3.1.3.564.1542093 (HDP 2.1.12.1-0003)
* HDInsight 3.2.4.564.1542093 (HDP 2.2.4.6-2)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

<table border="1">
<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK)</p></th>
<th>Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td>SCP.NET EventHub-ondersteuning</td>
<td>Hallo bijgewerkt cluster pakketten voor HDInsight Storm Breng tooSCP.NET van nieuwe functies. U hebt nu toegang toonew API's in de topologie builder dat het eenvoudiger toouse EventHubSpout of Java Spouts. U moet uw SCP.NET client SDK toowork bijwerken met nieuwe clusters zoals Hallo contracten zijn bijgewerkt. Nieuwe API's, het gebruik en release-opmerkingen (waaronder bugfixes) Raadpleeg voor meer informatie over Hallo toohello Leesmij opgenomen in Hallo SCP.NET NuGet-pakket.</td>
<td>VS Tooling</td>
<td>Storm 3.2 HDInsight-clusters</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>JDBC-stuurprogramma-update</td>
<td>Bijgewerkte Hallo stuurprogramma toohello SQL Server versie in sqljdbc_4.1.5605.100 ondersteund.</td>
<td>Metastore</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-04272015-release-of-hdinsight"></a>Opmerkingen voor 04/27/2015-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.537.1486660 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight 3.0.6.537.1486660 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight 3.1.3.537.1486660 (2.1.12.0-2329 HDP - ongewijzigd)
* HDInsight 3.2.3.537.1486660 (HDP 2.2.2.2-4)
* SDK 1.5.8

Deze versie bevat Hallo volgende updates:

<table border="1">
<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK)</p></th>
<th>Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td>DLL-afhankelijkheid oplossen</td>
<td>Hiermee verwijdert u een HDInsight-afhankelijkheid van eenheid Test Framework.</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Fout-oplossing voor race condition</td>
<td>Aanvraag voor een cluster maken nu wacht op de PUT-aanvragen toobe geaccepteerd voordat polling op Hallo-status</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-04142015-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight-04-14-2015
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.521.1453250 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight 3.0.6.521.1453250 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight 3.1.3.521.1453250 (2.1.12.0-2329 HDP - ongewijzigd)
* HDInsight 3.2.3.525.1459730 (HDP 2.2.2.2-2)
* SDK 1.5.6 WORDEN UITGEZET

Deze versie bevat Hallo volgende updates:

<table border="1">
<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK)</p></th>
<th>Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td>Tez oplossingen voor problemen</td>
<td>Oplossingen voor Apache TEZ 2214 en TEZ 1923 zijn opgenomen in deze release van HDI 3.2. Deze zijn nodig voor bepaalde Hive-query's op Tez waarvoor tooshuffle een aanzienlijke hoeveelheid gegevens.
</td>
<td>HDP</td>
<td>Hadoop</td>
<td><a href="https://issues.apache.org/jira/browse/TEZ-2214">TEZ 2214</a></br><a href="https://issues.apache.org/jira/browse/TEZ-1923">TEZ 1923</a></td>
</tr>
</table>

## <a name="notes-for-04062015-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight-04-06-2015
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.521.1453250 (1.3.12.0-01795 HDP - ongewijzigd)
* HDInsight 3.0.6.521.1453250 (2.0.13.0-2117 HDP - ongewijzigd)
* HDInsight 3.1.3.521.1453250 (2.1.12.0-2329 HDP - ongewijzigd)
* HDInsight 3.2.3.521.1453250 (HDP 2.2.2.2-1)
* SDK 1.5.6 WORDEN UITGEZET

Deze versie bevat Hallo volgende updates:

<table border="1">
<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK)</p></th>
<th>Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td>HDInsight SDK voor .NET 1.5.6 worden uitgezet</td>
<td>Updates tooremove sommige interne klassen voor HDInsight op Linux.</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Bibliotheek voor Avro 1.5.6 worden uitgezet</td>
<td>Toegevoegd <b>KnownTypeAttribute</b> voor methode <b>GetAllKnownTypes</b>. Vaste NullReferenceException wanneer een type null voor GetAllKnownTypes methode is.</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Oplossingen voor problemen</td>
<td>Verschillende oplossingen voor problemen toohello service</td>
<td>Service</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-04012015-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight-04-01-2015
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.513.1431705 (HDP 1.3.12.0-01795)
* HDInsight 3.0.6.513.1431705 (HDP 2.0.13.0-2117)
* HDInsight 3.1.3.513.1431705 (HDP 2.1.12.0-2329)
* HDInsight 3.2.3.513.1431705 (HDP 2.2.2.1-2600)
* SDK 1.5.5

Deze versie bevat Hallo volgende updates:

<table border="1">
<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK)</p></th>
<th>Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td>Mogelijkheid tooenable-of uitschakelen extern bureaublad-referenties op Windows-clusters via .NET SDK</td>
<td>Programmatische ondersteuning voor in- of uitschakelen van RDP-referenties op Windows-clusters.</td>
<td>SDK</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Mogelijkheid tooenable extern bureaublad-referenties op clusters terwijl ze zijn ingericht</td>
<td>Programmatische ondersteuning voor het inschakelen van extern bureaublad-referenties zoals Hallo-cluster wordt gemaakt. Hiermee verwijdert u Hallo-proces voor de eerste inrichting Hallo-cluster en vervolgens het inschakelen van extern bureaublad.</td>
<td>SDK</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Bijgewerkte Python too2.7.8</td>
<td>Bijgewerkte Python op HDInsight-Clusters tooPython punt 2.7.8, die een aantal belangrijke beveiliging bevat oplossingen voor HDInsight versie 2.1, 3.0, 3.1 en 3.2</td>
<td>Service</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>YARN-configuratiewijziging</td>
<td>Gewijzigde YARN configuratie yarn.resourcemanager.max: voltooid toepassingen too1000 voor alle clustertypen voor HDInsight versie 3.1 en 3.2. Deze waarde bepaalt alleen Hallo lijst met voltooide toepassingen in de gebruikersinterface van YARN Hallo. tooget informatie over toepassingen die zijn ingediend voorafgaande toohello lijst met toepassingen die worden weergegeven op het Hallo-gebruikersinterface kunt u rechtstreeks toohello geschiedenis Server gaan.</td>
<td>YARN</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Grootte van de knooppunten in een HBase-cluster</td>
<td>HBase-clusters wordt nu toestaan vergroten of verkleinen van knooppunten (omhoog en omlaag) voor HDInsight versie 3.1 en 3.2</td>
<td>Service</td>
<td>HBase</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>JDBC upgrade</td>
<td>SQL-JDBC-stuurprogramma is bijgewerkte tooversion sqljdbc_4.0.2206.100 voor HDInsight versie 3.2. Deze versie bevat belangrijke verbeteringen.</td>
<td>HDP</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>JVM-configuratie-update</td>
<td>Bijgewerkte JVM configuratie networkaddress.cache.ttl too300 seconden van de standaardwaarde Hallo van-1 voor HDInsight versie 3.1 en 3.2. Deze configuratiewaarde bepaalt Hallo cachebeleid voor de naam van geslaagde zoekacties van Hallo naamservice. Hiermee een probleem is opgelost verwante toogrowing en HBase-clusters te verkleinen.</td>
<td>Service</td>
<td>HBase</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Upgrade tooAzure opslag-SDK voor Java 2.0</td>
<td>HDInsight versie 3.2 is bijgewerkte toouse Hallo meest recente versie van hello Azure-opslag-SDK voor Java. Dit document bevat verschillende belangrijke oplossingen voor problemen via Hallo 0.6.0 huidige versie.</td>
<td>HDP</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Bijgewerkte tooApache WASB broncode</td>
<td>HDInsight versie 3.2 nu maakt gebruik van de meest recente code voor Hallo WASB bestandssysteem stuurprogramma van Apache Hadoop Hallo. Met deze wijziging wordt nu Hallo WASB stuurprogramma geleverd als een afzonderlijke jar. Dit is alleen een wijziging in de pakketten en bevat geen eventuele wijzigingen toobehavior van Hallo WASB stuurprogramma. Hallo-naam van deze JAR-bestand is hadoop-azure-2.6.0.jar.</td>
<td>HDP</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Bestandsnaam-updates in HDInsight 3.2 JAR</td>
<td>Deze update tooHDInsight versie 3.2 bevat verschillende oplossingen voor problemen en enkele interne potten geleverd als onderdeel van HDP zijn bijgewerkt. Deze JAR filesare interne toohello HDP pakket en niet voor direct gebruik door toepassingen van de klant. Toepassingen moeten hun eigen versie van Hallo potten pakket, zodat een upgrade toohello HDP interne JARs, mogen niet verbreking toepassingen van de klant.</td>
<td>HDP</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-03032015-release-of-hdinsight"></a>Opmerkingen bij de release van HDInsight 03-03-2015
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.488.1375841 (1.3.9.0-01351 HDP - ongewijzigd)
* HDInsight 3.0.6.488.1375841 (2.0.9.0-2097 HDP - ongewijzigd)
* HDInsight 3.1.3.488.1375841 (2.1.10.0-2290 HDP - ongewijzigd)
* HDInsight 3.2.3.488.1375841 (HDP-2.2.10.0-. 2340 - ongewijzigd)
* SDK 1.5.0 (ongewijzigd)

Deze versie bevat Hallo na update:

<table border="1">
<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Betrokken gebied (bijvoorbeeld, service, onderdeel of SDK)</p></th>
<th>Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster</th>
<th>JIRA</th>
</tr>
<tr>
<td>Verbeteringen van de betrouwbaarheid</td>
<td>Er aangebracht oplossingen waarmee Hallo service tooscale beter met de toegenomen belasting Hallo met opzicht toocluster maken.</td>
<td>Service</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-02182015-release-of-hdinsight"></a>Opmerkingen voor 02-18-2015-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.471.1342507 (1.3.9.0-01351 HDP - ongewijzigd)
* HDInsight 3.0.6.471.1342507 (2.0.9.0-2097 HDP - ongewijzigd)
* HDInsight 3.1.3.471.1342507 (2.1.10.0-2290 HDP - ongewijzigd)
* HDInsight 3.2.3.471.1342507 (HDP-2.2.10.0-. 2340)
* SDK 1.5.0

Deze versie bevat Hallo volgende updates:

<table border="1">
<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK)</p></th>
<th>Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td>3.2 voor HDInsight-clusters</td>
<td>Hadoop 2.6/HDP2.2 is beschikbaar met HDInsight 3.2-clusters. Bevat belangrijke updates tooall Hallo open source-onderdelen. Zie voor meer informatie, wat is er nieuw in HDInsight en <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html" target="_blank">HDP 2.2.0.0 Release-opmerkingen</a>.</td>
<td>Open source software</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>HDInsight op Linux (Preview)</td>
<td>Clusters kunnen worden geïmplementeerd op Ubuntu Linux wordt uitgevoerd. Zie de sectie aan de slag met HDInsight op Linux voor meer informatie.</td>
<td>Service</td>
<td>Hadoop</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Storm algemene beschikbaarheid</td>
<td>Apache Storm-clusters zijn algemeen beschikbaar. Voor meer informatie Zie slag gaan met Storm in HDInsight.</td>
<td>Service</td>
<td>Storm</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Grootten van virtuele machines</td>
<td>Azure HDInsight is beschikbaar op meer typen virtuele machines en groottes. HDInsight kan gebruikmaken van A2 tooA7-groottes gebouwd voor algemene doeleinden; D-reeks knooppunten die functie SSD-schijven (SSD's) en 60 procent sneller processors; en A8- en A9-groottes met InfiniBand voor snel netwerken ondersteunen.</td>
<td>Service</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Clusterschaling</td>
<td>U kunt het aantal gegevensknooppunten voor een actief HDInsight-cluster Hallo wijzigen zonder toodelete of opnieuw te maken. Op dit moment wordt alleen voor Hadoop-Query en Apache Storm-clustertypen over deze mogelijkheid beschikken maar ondersteuning voor het type van Apache HBase-cluster is snel toofollow. Zie voor meer informatie, beheert HDInsight-clusters.</td>
<td>Service</td>
<td>Hadoop, Storm</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Visual Studio Tools</td>
<td>Bovendien is toocomplete tooling voor Apache Storm, Hallo tooling voor Apache Hive in Visual Studio voltooiing van de bijgewerkte tooinclude-instructie, lokale validatie en verbeterde ondersteuning voor foutopsporing. Zie voor meer informatie aan de slag met HDInsight Hadoop-hulpprogramma's voor Visual Studio.</td>
<td>Tooling</td>
<td>Hadoop</td>
<td>N.v.t.</td>
</tr>
<td>Hadoop-Connector voor Azure Cosmos DB</td>
<td>U kunt met Hadoop-Connector voor Azure Cosmos DB, complexe aggregaties, analyse en bewerkingen uitvoeren via uw schema minder JSON-documenten die zijn opgeslagen in Azure Cosmos DB verzamelingen of database-accounts. Zie voor meer informatie en een zelfstudie uitvoeren Hadoop-taken met behulp van Azure DB die Cosmos en HDInsight.</td>
<td>Service</td>
<td>Hadoop</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Oplossingen voor problemen</td>
<td>Er zijn verschillende kleine oplossingen voor problemen voor services van HDInsight aangebracht. Er is geen gedragswijzigingen klantgerichte worden verwacht.</td>
<td>Service</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-02062015-release-of-hdinsight"></a>Opmerkingen voor 02-06-2015-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.463.1325367 (1.3.9.0-01351 HDP - ongewijzigd)
* HDInsight 3.0.6.463.1325367 (2.0.9.0-2097 HDP - ongewijzigd)
* HDInsight 3.1.2.463.1325367 (HDP 2.1.10.0-2290)
* N.V.T. SDK

Deze versie bevat Hallo volgende updates:

<table border="1">
<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK)</p></th>
<th>Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td>Oplossingen voor problemen</td>
<td>Er zijn verschillende kleine oplossingen voor problemen voor services van HDInsight aangebracht. Er is geen gedragswijzigingen klantgerichte worden verwacht.</td>
<td>Service</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>HDP 2.1 onderhoud update</td>
<td>HDInsight 3.1 is bijgewerkte toodeploy HDP 2.1.10.0. Zie voor meer informatie <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.10/bk_releasenotes_hdp_2.1/content/ch_relnotes-HDP-2.1.10.html" target="_blank">releaseopmerkingen HDP-2.1.10</a>. </td>
<td>Open source software</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Binaire HDP-updates</td>
<td>Er zijn een paar JAR-bestanden in HBase voor waarop het bestand namen zijn bijgewerkt. Deze JAR-bestanden worden intern gebruikt door HBase, zodat deze niet verwacht wordt dat klanten hebben van een afhankelijkheid op Hallo namen van deze JAR-bestanden. Deze omvatten:
<ul>
<li>./lib/jetty-6.1.26.hwx.jar</li>
<li>./lib/jetty-sslengine-6.1.26.hwx.jar</li>
<li>./lib/jetty-Util-6.1.26.hwx.jar</li>
</ul>
</td>
<td>Open source software</td>
<td>HBase</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-1292015-release-of-hdinsight"></a>Opmerkingen voor 1-29-2015-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.455.1309616 (1.3.9.0-01351 HDP - ongewijzigd)
* HDInsight 3.0.6.455.1309616 (2.0.9.0-2097 HDP - ongewijzigd)
* HDInsight 3.1.2.455.1309616 (2.1.9.0-2196 HDP - ongewijzigd)
* N.V.T. SDK

Deze versie bevat Hallo na update:

<table border="1">

<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Betrokken gebied (bijvoorbeeld, Service, onderdeel of SDK)</p></th>
<th>Type (bijvoorbeeld Hadoop, HBase of Storm)-cluster</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td>Oplossingen voor problemen</td>
<td>Er zijn een aantal belangrijke problemen opgelost ter verbetering van de betrouwbaarheid van HDInsight-Clusters Hallo Hallo tijdens upgrades Azure aangebracht.</td>
<td>Service</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-152015-release-of-hdinsight"></a>Opmerkingen voor 1-5-2015-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release:

* HDInsight 2.1.10.420.1246118 (1.3.9.0-01351 HDP - ongewijzigd)
* HDInsight 3.0.6.420.1246118 (2.0.9.0-2097 HDP - ongewijzigd)
* HDInsight 3.1.2.420.1246118 (2.1.9.0-2196 HDP - ongewijzigd)

Deze versie bevat Hallo volgende updates:

<table border="1">

<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Onderdeel</th>
<th>Clustertype</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td>Voorbeelden voor het trendanalyse Twitter en op basis van Mahout filmaanbevelingen</td>
<td><p>In deze release heeft Hallo HDInsight Query console twee aanvullende voorbeelden:</p>

<p><b>Het trendanalyse Twitter</b><br>
Openbare API's die worden geleverd door sites zoals Twitter zijn nuttig gegevensbron voor het analyseren en kennis van populaire trends. Informatie over hoe toouse Hive tooget een lijst met Twitter-gebruikers die verzonden hello meeste tweets met een bepaald woord in deze zelfstudie. </p>

<p><b>Mahout film aanbeveling</b><br>
Apache Mahout is een Apache Hadoop-machine learning-bibliotheek. Mahout bevat algoritmen voor het verwerken van gegevens (zoals filteren, classificatie en clustering). In deze zelfstudie gebruikt u een aanbeveling engine toogenerate filmaanbevelingen op basis van films die je vrienden hebt gezien.</p></td>
<td>Query-console</td>
<td>Hadoop</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Wijzig de waarde toodefault voor Hive-configuratie: hive.auto.convert.join.noconditionaltask.size</td>
<td><p>De configuratie van deze grootte is van toepassing tooautomatically geconverteerd kaart joins. Hallo-waarde vertegenwoordigt Hallo som van Hallo grootten van tabellen die kunnen worden geconverteerd toohash-toewijzingen die in het geheugen passen. In een eerdere versie, wordt deze waarde verhoogd van Hallo standaardwaarde van 10 MB too128 MB. Hallo nieuwe waarde van 128 MB veroorzaakt echter taken toofail vanwege toolack van geheugen. Als u deze release wordt teruggezet Hallo standaardwaarde back-too10 MB. Klanten kunnen nog steeds kiezen toooverride deze waarde tijdens het maken van het cluster opgegeven query's en bijbehorende omvang van de tabel. Voor meer informatie over deze instelling en hoe toooverride, Zie <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.0.2/ds_Hive/optimize-joins.html#JoinOptimization-OptimizeAutoJoinConversion" target="_blank">Join autoconversie optimaliseren</a> in Hortonworks documentatie. </p></td>
<td>Hive</td>
<td>Hadoop, Hbase</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-12232014-release-of-hdinsight"></a>Opmerkingen voor 23-12-2014-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release zijn:

* HDInsight 2.1.10.420.1246783 (HDP versie ongewijzigd)
* HDInsight 3.0.6.420.1246783 (HDP versie ongewijzigd)
* HDInsight 3.1.1.420.1246783 (HDP versie ongewijzigd)

Deze versie bevat Hallo na update:

<table border="1">
<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Onderdeel</th>
<th>Clustertype</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td>Fouten bij het maken van onregelmatige cluster vanwege tooexcessive laden</td>
<td><p>Verbeterde algoritme voor het downloaden van pakketten HDP tijdens het maken van een cluster kunt krachtiger afhandeling van fouten vanwege tooexcessive laden.</p></td>
<td>Service</td>
<td>Hadoop, Hbase, Storm</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-12182014-release-of-hdinsight"></a>Opmerkingen voor 18-12-2014-release van HDInsight
Deze versie bevat Hallo update voor het onderdeel te volgen:

<table border="1">
<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Onderdeel</th>
<th>Clustertype</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td><a href = "hdinsight-hadoop-customize-cluster.md" target="_blank">Cluster aanpassing algemene beschikbaarheid</a></td>
<td><p>Aanpassing biedt Hallo mogelijkheid voor u toocustomize uw Azure HDInsight-clusters met projecten die beschikbaar via Hallo Apache Hadoop-ecosysteem zijn. Met deze nieuwe functie kunt u experimenteren en implementeren van Hadoop-projecten tooAzure HDInsight. Dit wordt ingeschakeld via Hallo **scriptactie** functie waarmee Hadoop-clusters op willekeurige manieren aanpassen kunt met behulp van aangepaste scripts. Deze aanpassing is beschikbaar op alle soorten HDInsight-clusters met Hadoop, HBase en Storm. toodemonstrate hello stroom van deze mogelijkheid, hebben we Hallo proces tooinstall Hallo populaire gedocumenteerd <a href = "hdinsight-hadoop-spark-install.md" target="_blank">Spark</a>, <a href = "hdinsight-hadoop-r-scripts.md" target="_blank">R</a>, <a href = "hdinsight-hadoop-solr-install.md" target="_blank">Solr</a>, en <a href = "hdinsight-hadoop-giraph-install.md" target="_blank">Giraph</a> modules. Deze release ook Hallo voegt functionaliteit toe voor klanten toospecify hun aangepaste scriptactie via hello Azure-portal biedt richtlijnen en aanbevolen procedures over hoe toobuild aangepaste acties Help-methoden met een script en bevat richtlijnen over het tootest Hallo scriptactie. </p></td>
<td>Functie algemene beschikbaarheid</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-12052014-release-of-hdinsight"></a>Opmerkingen voor 05-12-2014-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release zijn:

* HDInsight 2.1.9.406.1221105 (HDP 1.3.9.0-01351)
* HDInsight 3.0.5.406.1221105 (HDP 2.0.9.0-2097)
* HDInsight 3.1.1.406.1221105 (HDP 2.1.9.0-2196)
* HDInsight SDK N.V.T.

Deze versie bevat Hallo onderdeelupdates te volgen:

<table border="1">
<tr>
<th>Titel</th>
<th>Beschrijving</th>
<th>Onderdeel</th>
<th>Clustertype</th>
<th>JIRA (indien van toepassing)</th>
</tr>
<tr>
<td>Fout-oplossing: onregelmatige fout tijdens het toevoegen van een groot aantal partities tooa tabel in een DDL Hive </td>
<td><p>Als er een fout met Hallo Hive-metastore database een onregelmatige verbinding bij het toevoegen van een groot aantal partities tooa Hive-tabel, kan Hallo Hive DDL mislukken. Hallo instructie isseen in het foutenlogboek van Hallo Hive volgen als deze fout optreedt: </p><p>' Fout [hoofd]: ql. Stuurprogramma (SessionState.java:printError(547)) - is mislukt: fout bij uitvoering, retourcode 1 van org.apache.hadoop.hive.ql.exec.DDLTask. MetaException (message:java.lang.RuntimeException: commitTransaction is aangeroepen maar openTransactionCalls = 0. Dit waarschijnlijk geeft aan dat er niet in balans aanroepen tooopenTransaction/commitTransaction)"</p></td>
<td>Hive</td>
<td>Hadoop, Hbase</td>
<td>HIVE-482 (dit is een interne JIRA kan niet extern worden aangehaald. Worden hier vermeld ter referentie.)</td>
</tr>
<tr>
<td>Fout-oplossing: incidentele loopt vast in Hallo HDInsight Query-Console</td>
<td>Als dit gebeurt, kunt hello volgende instructie bekijken in Hallo WebHCat logboek voor Hallo WebHCat launcher taak: <p>' org.apache.hive.hcatalog.templeton.CatchallExceptionMapper | org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.yarn.exceptions.YarnRuntimeException): geschiedenisbestand {wasb voor url toohello geschiedenisbestand} kan niet worden geladen. "</p></td>
<td>WebHCat</td>
<td>Hadoop</td>
<td>HIVE-482 (dit is een interne JIRA kan niet extern worden aangehaald. Worden hier vermeld ter referentie.)</td>
</tr>
<tr>
<td>Fout-oplossing: incidentele piek in de latentie van Hbase-query's</td>
<td>Als dit gebeurt, ziet gebruikers een incidentele piek van 3 seconden in Hallo latentie van Hbase-query's. </td>
<td>HDInsight-Cluster-Gateway</td>
<td>HBase</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Wijzigingen in HDP JAR-bestand de naam</td>
<td>Voor HDI-cluster versie 3.0, is er een aantal wijzigingen toohello interne JAR-bestanden geïnstalleerd HDP. jetty-6.1.26.jar is vervangen door jetty 6.1.26.hwx.jar. jetty-util-6.1.26.jar is vervangen door jetty-util-6.1.26.hwx.jar. Deze wijzigingen toepassen tooHadoop, Mahout, WebHCat en Oozie-projecten.</td>
<td>Hadoop, Mahout, WebHCat, Oozie</td>
<td>Hadoop, HBase</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-11212014-release-of-hdinsight"></a>Opmerkingen voor 21-11-2014-release van HDInsight
Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release zijn:

* HDInsight 2.1.9.382.1169709 (geen wijziging van 14-11-2014)
* HDInsight 3.0.5.382.1169709 (geen wijziging van 14-11-2014)
* HDInsight 3.1.1.382.1169709 (geen wijziging van 14-11-2014)
* HDInsight SDK 1.4.0

Deze versie bevat Hallo onderdeelupdates te volgen:

<table border="1">
<tr><th>Titel</th><th>Beschrijving</th><th>Onderdeel</th><th>Clustertype</th><th>JIRA (indien van toepassing)</th></tr>
<tr>
<td>Toegang tot logboeken</td>
<td>Mogelijkheid tooprogrammatically opsommen-toepassingen die zijn uitgevoerd op uw clusters en toodownload relevante toepassingsspecifieke of container-specifieke logboeken toohelp foutopsporing problematische toepassingen.</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Mogelijkheid toospecify regionaam in IHdInsightClient.DeleteCluster </td>
<td>Hello Azure HDInsight SDK biedt Hallo mogelijkheid toospecify regionaam bij gebruik van **DeleteCluster**. Dit helpt deblokkeren van klanten die heeft twee resources met dezelfde naam in verschillende regio's en had toodelete kan niet een van beide.</td>
<td>SDK</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>ClusterDetails.DeploymentId</td>
<td>Hallo **ClusterDetails** object retourneert een **DeploymentID** veld dat een unieke id voor Hallo cluster vertegenwoordigt. Kan worden gegarandeerd toobe uniek zijn voor het maken van het cluster probeert Hello dezelfde namen.</td>
<td>SDK</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
</table>

## <a name="notes-for-11142014-release-of-hdinsight"></a>Opmerkingen voor 14-11-2014-release van HDInsight

Hallo volledige versienummers voor HDInsight-clusters die zijn geïmplementeerd met deze release zijn:

* HDInsight 2.1.9.382.1169709
* HDInsight 3.0.5.382.1169709
* HDInsight 3.1.1.382.1169709

Deze release bevat Hallo volgende nieuwe functies, onderdeelupdates en oplossingen voor problemen.

<table border="1">
<tr><th>Titel</th><th>Beschrijving</th><th>Onderdeel</th><th>Clustertype</th><th>JIRA (indien van toepassing)</th></tr>
<tr>
<td>Scriptactie (Preview)</td>
<td>Voorbeeld van Hallo cluster aanpassing functie waarmee de wijziging van Hadoop-clusters op willekeurige manieren met behulp van aangepaste scripts. Gebruikers kunnen met deze functie experimenteren en projecten die beschikbaar zijn vanuit Hallo Apache Hadoop-ecosysteem tooAzure die hdinsight-clusters implementeren. Deze aanpassing-functie is beschikbaar op alle soorten HDInsight-clusters, waaronder Hadoop, HBase en Storm.</td>
<td>Nieuwe functie</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Vooraf gedefinieerde taken voor de logboekanalyse Azure websites en opslag</td>
<td>Hallo HDInsight Query Console heeft een aan de slag galerie die ondersteuning biedt voor oplossingen die werken op uw gegevens of voorbeeldgegevens.
<p>**Oplossingen die voor uw gegevens werken**:<br>
Wij hebben taken gemaakt voor een aantal Hallo meest voorkomende gegevens analysis scenario's tooprovide een beginpunt voor het maken van uw eigen oplossingen. U kunt uw gegevens met Hallo taak toosee hoe het werkt. Wanneer u klaar bent, moet u vervolgens gebruiken wat u hebt geleerd, toocreate een oplossing die is gemodelleerd naar vooraf gedefinieerde Hallo-taak.</p>
<p>**Oplossingen die op voorbeeldgegevens werken**:<br>
Meer informatie over hoe toowork met HDInsight door enkele algemene scenario's (zoals het analyseren van weblogboeken en sensorgegevens) doorlopen. U leert hoe toouse HDInsight tooanalyze dergelijke gegevens en hoe u verbinding kunt maken van andere toepassingen en services toothis-gegevens. Gegevens visualiseren door verbinding te maken tooMicrosoft Excel bevat een voorbeeld van Hallo power van deze benadering.</p></td>
<td>Query-console</td>
<td>Hadoop</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Geheugen-geheugenlek fix in Templeton</td>
<td>Een geheugenlek in Templeton die van invloed op klanten die was langlopende clusters of 100s van taak zijn verzenden aanvragen dat per seconde is opgelost. Hallo is probleem gemanifesteerd als Templeton 5xx-fouten en Hallo tijdelijke oplossing toorestart Hallo-service. Hallo tijdelijke oplossing is niet meer nodig.</td>
<td>Templeton</td>
<td>Alle</td>
<td>https://Issues.apache.org/jira/Browse/HADOOP-11248</td>
</tr>
</table>

> [!NOTE]
> toodemonstrate hello nieuwe mogelijkheden beschikbaar gesteld door de cluster-aanpassing Hallo procedures met scriptactie tooinstall Spark en R-modules op een cluster hebt zijn gedocumenteerd. Zie voor meer informatie:

* [Installeren en gebruiken van Spark 1.0 op HDInsight-clusters](hdinsight-hadoop-spark-install.md)
* [Installeren en gebruiken van R op HDInsight Hadoop-clusters](hdinsight-hadoop-r-scripts.md)

## <a name="notes-for-11072014-release-of-hdinsight"></a>Opmerkingen voor 07-11-2014-release van HDInsight

Hallo volledige versienummers voor HDInsight-clusters die geïmplementeerd met deze release zijn:

* HDInsight 2.1 2.1.9.374.1153876
* HDInsight 3.0 3.0.5.374.1153876
* HDInsight 3.1 3.1.1.374.1153876

Deze versie bevat Hallo onderdeelupdates te volgen:

<table border="1">
<tr><th>Titel</th><th>Beschrijving</th><th>Onderdeel</th><th>Clustertype</th><th>JIRA (indien van toepassing)</th></tr>
<tr>
<td>HDP 2.1.7</td>
<td>Deze release is gebaseerd op Hortonworks Data Platform HDP () 2.1.7. Zie voor meer informatie <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html" target="_blank">Release-opmerkingen voor HDP 2.1.7</a>.</td>
<td>HDP</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>YARN tijdlijn Server</td>
<td>Hallo YARN tijdlijn Server (ook wel bekend als hello geschiedenis van algemene toepassingsserver) is standaard ingeschakeld. Hallo tijdlijn Server bevat algemene informatie over voltooide toepassingen (zoals toepassings-ID, toepassingsnaam, toepassingsstatus, toepassing verzending van de tijd en voltooiingstijd van toepassing).

De informatie over deze toepassing kan worden opgehaald uit het hoofdknooppunt Hallo via Hallo URI http://headnodehost:8188 of door actieve Hallo YARN-opdracht: yarn toepassing - lijst - appStates alle.

Deze informatie kan ook worden opgehaald op afstand al een REST-API op https://{ClusterDnsName}. azurehdinsight.NET/ws/V1/applicationhistory/.

Voor meer informatie gedetailleerde, Zie <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN tijdlijn Server</a>.</td>
<td>YARN-service</td>
<td>Hadoop, HBase</td>
<td>N.v.t.</td>
</tr>
<tr>
<td>Cluster-implementatie-ID</td>
<td>Beginnen met de SDK-versie 1.3.3.1.5426.29232, gebruikers toegang krijgen tot een unieke ID voor elk cluster dat is uitgegeven HDInsight. Dit kunnen klanten toofigure uit unieke exemplaren van clusters wanneer een DNS-naam wordt hergebruikt over maken of verwijderen van scenario's.</td>
<td>SDK</td>
<td>Alle</td>
<td>N.v.t.</td>
</tr>
</table>

> [!NOTE]
> Hallo-fout waardoor Hallo volledige versienummer niet worden weergegeven in de portal Hallo of worden geretourneerd door SDK Hallo of door Windows PowerShell is verholpen in deze release.

## <a name="notes-for-10152014-release"></a>Opmerkingen voor 15-10-2014-release

Deze hotfix-versie vast een geheugenlek Templeton die van invloed op een zware gebruikers Hallo van Templeton. In sommige gevallen ziet gebruikers die Templeton sterk uitgeoefend gemanifesteerd als 500 foutcodes omdat Hallo aanvragen zou niet over voldoende geheugen toorun fouten. Hallo-oplossing voor dit probleem is toorestart hello Templeton-service. Dit probleem is opgelost.

## <a name="notes-for-1072014-release"></a>Opmerkingen voor 7-10-2014-release

* Wanneer u de Ambari-eindpunt, 'https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}' hello *hostnaam* retourneert veld volledig gekwalificeerd Hallo domeinnaam (FQDN) van Hallo-knooppunt in plaats van alleen Hallo hostnaam zijn. Bijvoorbeeld, in plaats van het retourneren van '**headnode0**", krijgt u de FQDN-naam Hallo"**headnode0. { ClusterDNS} azurehdinsight.NET .net**'. Deze wijziging is vereist toofacilitate scenario's waarbij meerdere clustertypen (zoals HBase en Hadoop) kunnen worden geïmplementeerd in een virtueel netwerk. Dit gebeurt, bijvoorbeeld: bij gebruik van HBase als een back-end-platform voor Hadoop.

* We hebben opgegeven nieuwe geheugeninstellingen voor de implementatie van de standaard Hallo van Hallo HDInsight-cluster. Vorige standaardinstellingen geheugen geen afdoende rekening Hallo richtlijnen voor het Hallo aantal CPU-kernen worden geïmplementeerd. Deze nieuwe geheugeninstellingen leveren betere standaardinstellingen (aan de hand van de aanbevelingen Hortonworks). toochange, verwijzen toohello SDK-documentatie over het wijzigen van de configuratie van het cluster. Hallo nieuwe geheugeninstellingen die worden gebruikt door Hallo standaard 4 CPU core (8 container) HDInsight-cluster worden gespecificeerd in de volgende tabel Hallo. (Hallo waarden gebruikt eerdere toothis release worden ook gegeven getallen.)

<table border="1">
<tr><th>Onderdeel</th><th>Toewijzing van geheugen</th></tr>
<tr><td> yarn.scheduler.minimum-toewijzing</td><td>768 MB (eerder 512 MB)</td></tr>
<tr><td> yarn.scheduler.maximum-toewijzing</td><td>6144 MB (ongewijzigd)</td></tr>
<tr><td>yarn.nodemanager.resource.Memory</td><td>6144 MB (ongewijzigd)</td></tr>
<tr><td>mapreduce.map.Memory</td><td>768 MB (eerder 512 MB)</td></tr>
<tr><td>mapreduce.map.Java.opts</td><td>kiest = Xmx512m (eerder - Xmx410m)</td></tr>
<tr><td>mapreduce.reduce.Memory</td><td>1.536 MB (eerder 1024 MB)</td></tr>
<tr><td>mapreduce.reduce.Java.opts</td><td>kiest = Xmx1024m (eerder - Xmx819m)</td></tr>
<tr><td>yarn.app.mapreduce.AM.resource</td><td>768 MB (eerder 1024 MB)</td></tr>
<tr><td>yarn.app.mapreduce.AM.Command</td><td>kiest = Xmx512m (eerder - Xmx819m)</td></tr>
<tr><td>mapreduce.Task.IO.Sort</td><td>256 MB (eerder 200 MB)</td></tr>
<tr><td>tez.AM.resource.Memory</td><td>1.536 MB (ongewijzigd)</td></tr>
</table>

Zie voor meer informatie over configuratie-instellingen voor Hallo geheugen is gebruikt door de YARN en MapReduce op Hallo Hortonworks Data Platform dat wordt gebruikt door HDInsight [HDP geheugen configuratie-instellingen bepalen](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1-latest/bk_installing_manually_book/content/rpm-chap1-11.html). Een hulpprogramma verstrekt Hortonworks ook de juiste geheugeninstellingen toocalculate.

Met betrekking tot hello Azure PowerShell en Hallo HDInsight SDK foutbericht weergegeven: '*Cluster is niet geconfigureerd voor HTTP-services toegang*':

* Deze fout is een bekend [compatibiliteitsprobleem](https://social.msdn.microsoft.com/Forums/azure/a7de016d-8de1-4385-b89e-d2e7a1a9d927/hdinsight-powershellsdk-error-cluster-is-not-configured-for-http-services-access?forum=hdinsight) die kunnen optreden vanwege tooa verschil in Hallo Hallo HDInsight SDK of Azure PowerShell en Hallo versie van Hallo-cluster. Clusters die zijn gemaakt op 8-15 of hoger hebben ondersteuning voor nieuwe inrichting mogelijkheid in virtuele netwerken. Maar deze mogelijkheid is niet correct geïnterpreteerd door oudere versies van Hallo HDInsight SDK of Azure PowerShell. Hallo-resultaat is een fout in bepaalde bewerkingen van de verzending van taak. Als u HDInsight SDK-API's of Azure PowerShell-cmdlets gebruiken (**gebruik AzureRmHDInsightCluster** of **Invoke-AzureRmHDInsightHiveJob**) toosubmit taken, deze bewerkingen kunnen mislukken met fout het Hallo-bericht ' *Cluster <clustername> is niet geconfigureerd voor HTTP-services toegang*. " Of (afhankelijk van de Hallo bewerking), krijgt u mogelijk andere foutberichten worden weergegeven, zoals '*kan geen verbinding maken toocluster*'.
* Deze compatibiliteitsproblemen worden omgezet in de meest recente versies Hallo van Hallo HDInsight SDK en Azure PowerShell. Het is raadzaam bijwerken Hallo HDInsight SDK tooversion 1.3.1.6 of hoger en Azure PowerShell extra tooversion 0.8.8 of hoger. U krijgt toegang tot toohello nieuwste HDInsight SDK uit [Nuget](http://nuget.codeplex.com/wikipage?title=Getting%20Started) en hulpprogramma's van Azure PowerShell op Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

## <a name="notes-for-9122014-release-of-hdinsight-31"></a>Notities bij 12-9-2014-release van HDInsight 3.1
* Deze release is gebaseerd op Hortonworks Data Platform HDP () 2.1.5. Zie voor een lijst met Hallo bugs opgelost in deze release, Hallo [opgelost in deze Release](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.5/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.5-fixed.html) pagina op Hallo Hortonworks site.
* Hallo Pig bibliotheken map, bestand Hallo 'avro mapred 1.7.4.jar' is gewijzigd te 'avro-mapred-1.7.4-hadoop2.jar." Hallo-inhoud van dit bestand bevat een kleine oplossingen oplossing die niet belangrijk. Het verdient aanbeveling dat klanten Maak een directe afhankelijkheid van de naam van de Hallo Hallo JAR-bestand tooavoid einden wanneer bestanden worden gewijzigd.

## <a name="notes-for-8212014-release"></a>Opmerkingen voor 21-8-2014-release
* We toevoegen Hallo WebHCat-configuratie (HIVE-7155), waardoor de Hallo standaard geheugenlimiet voor een domeincontroller Templeton taak too1 GB ingesteld na. (Hallo vorige standaardwaarde is 512 MB.)

     templeton.Mapper.Memory.MB (1024 =)

  * Deze wijziging adressen Hallo na een fout met bepaalde Hive-query's vanwege toolower geheugenlimieten: "Container wordt uitgevoerd buiten de limieten van fysiek geheugen."
  * toorevert toohello oude standaardinstellingen, u kunt deze configuratie waarde too512 via Azure PowerShell instellen tijdens het maken van een cluster met behulp van de volgende opdracht Hallo:

      Voeg AzureRmHDInsightConfigValues-Core @{"templeton.mapper.memory.mb"="512";}
* Hallo-hostnaam van Hallo zookeeper rol te is gewijzigd*zookeeper*. Dit heeft gevolgen voor naamomzetting binnen Hallo-cluster, maar het heeft geen invloed op de externe REST-API's. Als u onderdelen die gebruik Hallo *zookeepernode* hostnaam, moet u tooupdate ze toouse nieuwe naam. Hallo nieuwe namen voor Hallo drie zookeeper-knooppunten zijn:

  * zookeeper0
  * zookeeper1
  * zookeeper2
* HBase versie ondersteuningsmatrix wordt bijgewerkt. Alleen HDInsight versie 3.1 (HBase versie 0,98) wordt ondersteund voor de productie van HBase-werkbelastingen. Versie 3.0 (die is beschikbaar voor het voorbeeld) wordt niet ondersteund zwevend doorsturen.

## <a name="notes-about-clusters-created-prior-too8152014"></a>Opmerkingen over clusters gemaakt voorafgaande 15-too8/2014
Een Azure PowerShell of de HDInsight SDK foutbericht ' Cluster <clustername> is niet geconfigureerd voor HTTP-services toegang ' (of afhankelijk van de bewerking hello, andere foutberichten, zoals: 'Kan geen verbinding maken toocluster') kan optreden vanwege tooa versie verschil tussen Azure PowerShell of Hallo HDInsight SDK en een cluster. Clusters die zijn gemaakt op 8-15 of hoger hebben ondersteuning voor nieuwe inrichting mogelijkheid in virtuele netwerken. Deze mogelijkheid is niet correct geïnterpreteerd door oudere versies van hello Azure PowerShell of Hallo HDInsight SDK, wat tot fouten van de verzending van taakbewerkingen leidt. Als u HDInsight SDK-API's of Azure PowerShell-cmdlets (zoals gebruik AzureRmHDInsightCluster of Invoke-AzureRmHDInsightHiveJob) toosubmit taken gebruikt, wordt deze bewerkingen mislukken met een Hallo foutberichten die worden beschreven.

Deze compatibiliteitsproblemen worden omgezet in de meest recente versies Hallo van Hallo HDInsight SDK en Azure PowerShell. Het is raadzaam bijwerken Hallo HDInsight SDK tooversion 1.3.1.6 of hoger en Azure PowerShell extra tooversion 0.8.8 of hoger. U krijgt toegang tot toohello nieuwste HDInsight SDK uit [NuGet][nuget-link]. Hulpprogramma's hello Azure PowerShell toegang kunt krijgen via [Microsoft Web Platform Installer][webpi-link].

## <a name="notes-for-7282014-release"></a>Opmerkingen voor 28-7-2014-release
* **HDInsight die beschikbaar zijn in nieuwe gebieden**: HDInsight geografische aanwezigheid toothree regio's is uitgevouwen. HDInsight-klanten kunnen clusters maken in deze regio's:
  * Oost-Azië
  * Noord-centraal VS
  * Zuid-centraal VS
* HDInsight versie 1.6 (HDP 1.1 en Hadoop 1.0.3) en HDInsight versie 2.1 (HDP1.3 en Hadoop 1.2) zijn van hello Azure-portal verwijderd. Hadoop-clusters toocreate kan worden voortgezet voor deze versies met behulp van Azure PowerShell-cmdlet Hallo [nieuw AzureRmHDInsightCluster](http://msdn.microsoft.com/library/dn593744.aspx) of met behulp van Hallo [HDInsight SDK](http://msdn.microsoft.com/library/azure/dn469975.aspx). Zie voor meer informatie [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md).
* Hortonworks Data Platform HDP ()-wijzigingen in deze release:

<table border="1">
<tr><th>HDP</th><th>Wijzigingen</th></tr>
<tr><td>1.3 HDP / HDI 2.1</td><td>Er zijn geen wijzigingen</td></tr>
<tr><td>HDP 2.0 / HDI 3.0</td><td>Er zijn geen wijzigingen</td></tr>
<tr><td>2.1 HDP / HDI 3.1</td><td>zookeeper: [3.4.5.2.1.3.0-1948]-[3.4.5.2.1.3.2-0002] ></td></tr>
</table>

## <a name="notes-for-6242014-release"></a>Opmerkingen voor 24-6-2014-release
Deze versie bevat verbeteringen toohello HDInsight-service:

* **HDP 2.1 beschikbaarheid**: HDInsight 3.1 (met daarin HDP 2.1) is algemeen beschikbaar en is de standaardversie Hallo voor nieuwe clusters.
* **HBase - verbeteringen in Azure portal**: maken We HBase-clusters beschikbaar in Preview. U kunt HBase-clusters maken vanuit de portal Hallo met een paar klikken.

Met HBase, kunt u tal van realtime werkbelastingen op HDInsight, van interactieve websites die werken met grote gegevenssets tooservices opslaan sensor- en telemetriegegevens van miljoenen eindpunten maken. de volgende stap Hallo zou tooanalyze Hallo gegevens in deze werkbelastingen met Hadoop-taken en dit is mogelijk in HDInsight via Azure PowerShell en Hallo Hive cluster-dashboard.

### <a name="apache-mahout-preinstalled-on-hdinsight-31"></a>Apache Mahout vooraf is geïnstalleerd op HDInsight 3.1
 [Mahout](http://hortonworks.com/hadoop/mahout/) vooraf is geïnstalleerd op HDInsight 3.1 Hadoop-clusters, zodat u taken Mahout zonder Hallo nodig is voor extra clusterconfiguratie kunt uitvoeren. Bijvoorbeeld, u kunt externe in een Hadoop-cluster met behulp van Remote Desktop Protocol (RDP) en zonder aanvullende stappen kunt u Hallo na Hello World Mahout opdracht uitvoeren:

        mahout org.apache.mahout.classifier.df.tools.Describe -p /user/hdp/glass.data -f /user/hdp/glass.info -d I 9 N L

        mahout org.apache.mahout.classifier.df.BreimanExample -d /user/hdp/glass.data -ds /user/hdp/glass.info -i 10 -t 100

Zie voor een uitgebreidere uitleg van deze procedure Hallo-documentatie voor Hallo [Breiman voorbeeld](https://mahout.apache.org/users/classification/breiman-example.html) op Hallo Apache Mahout website.

### <a name="hive-queries-can-use-tez-in-hdinsight-31"></a>Hive-query's kunnen Tez gebruiken in HDInsight 3.1
Hive 0,13 is beschikbaar in HDInsight 3.1 en is in staat van het uitvoeren van query's op basis van Tez die aanzienlijke prestatieverbeteringen kan worden hergebruikt.
Tez is niet standaard ingeschakeld voor Hive-query's. toouse, moet u ervoor kiezen. U kunt Tez inschakelen door het volgende codefragment Hallo uitvoeren:

        set hive.execution.engine=tez;
        select sc_status, count(*), histogram_numeric(sc_bytes,5) from website_logs_orc_local group by sc_status;

Hortonworks heeft een gedetailleerd overzicht van Hive query prestatieverbeteringen met Tez gepubliceerd die wordt geleverd in presteert. Zie voor meer informatie [Benchmarking Apache Hive 13 voor Enterprise Hadoop](http://hortonworks.com/blog/benchmarking-apache-hive-13-enterprise-hadoop/).

Zie voor meer informatie [Hive op Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez).

### <a name="global-availability"></a>Globale beschikbaarheid
Hallo-versie van HDInsight op Hadoop 2.2, heeft Microsoft HDInsight beschikbaar gesteld in alle belangrijke locaties waarin Azure beschikbaar is. Hallo west-Europa en Zuidoost-Azië datacenters hebben in het bijzonder online is gebracht. Hierdoor kunnen klanten toolocate clusters in een datacenter dat sluiten en mogelijk in een zone van vergelijkbare nalevingsvereisten.

### <a name="dos--donts-between-cluster-versions"></a>DOS & moet doen tussen clusterversies van het
**Oozie metastores gebruikt met een 3.1 HDInsight-cluster zijn niet achterwaarts compatibel met 2.1 HDInsight-clusters en kan niet worden gebruikt met de vorige versie**.

Een aangepaste Oozie-metastore database geïmplementeerd met een 3.1 HDInsight-cluster kan niet opnieuw worden gebruikt met een 2.1 HDInsight-cluster. Dit is Hallo geval zelfs als Hallo metastore afkomstig met een 2.1 HDInsight-cluster is. Dit scenario wordt niet ondersteund omdat Hallo metastore schema bijgewerkt opgehaald gebruikt in combinatie met een 3.1 HDInsight-cluster, zodat het is niet meer compatibel is met het Hallo-metastore vereist door Hallo 2.1 HDInsight-clusters. Elke poging tooreuse een Oozie-metastore die is gebruikt met een 3.1 HDInsight-cluster weergeven Hallo 2.1 HDInsight-cluster onbruikbaar.

**Oozie metastores kan niet worden gedeeld tussen verschillende clusters.**

Oozie metastores zijn aangesloten toospecific clusters en ze kunnen niet worden gedeeld tussen verschillende clusters.

### <a name="breaking-changes"></a>Wijzigingen op te splitsen
**Syntaxis van het voorvoegsel**: alleen Hallo ' wasb: / / ' syntaxis wordt ondersteund in HDInsight 3.1 en 3.0-clusters. Hallo oudere ' asv: / / ' syntaxis wordt ondersteund in HDInsight 2.1 en 1.6-clusters, maar wordt niet ondersteund in HDInsight 3.1 of 3.0-clusters. Dit betekent dat alle taken die worden verzonden tooan HDInsight 3.1 of 3.0 expliciet cluster maakt gebruik van Hallo ' asv: / / ' gebruiken, zullen mislukken. Hallo ' wasb: / / ' syntaxis in plaats daarvan moet worden gebruikt. Ook taken die worden verzonden tooany HDInsight 3.1 of 3.0-clusters die zijn gemaakt met een bestaande metastore met expliciete verwijst tooresources met Hallo ' asv: / / ' gebruiken, zullen mislukken. Deze metastores moeten opnieuw worden gemaakt met de Hallo toobe ' wasb: / / ' syntaxis tooaddress resources.

**Poorten**: Hallo-poorten die door Hallo HDInsight-service zijn gewijzigd. Hallo-poortnummers die zijn gebruikt zijn binnen het Hallo-poortbereik van Hallo Windows-besturingssysteem. Poorten worden automatisch toegewezen vanuit een vooraf gedefinieerde kortstondige bereik voor tijdelijke Internet protocol-communicatie. Hallo nieuwe set toegestane poortnummers voor Hortonworks Data Platform HDP ()-service zijn buiten dit bereik tooavoid conflicten die kunnen optreden met Hallo poorten gebruikt door services worden uitgevoerd op het hoofdknooppunt Hallo uitgevoerd. nieuwe poortnummers Hallo leidt doorgaans niet tot een grote wijzigingen. Hallo nummers zijn als volgt:

 **HDInsight 1.6 (HDP 1.1)**

<table border="1">
<tr><th>Naam</th><th>Waarde</th></tr>
<tr><td>DFS.http.Address</td><td>namenodehost:30070</td></tr>
<tr><td>DFS.datanode.Address</td><td>0.0.0.0:30010</td></tr>
<tr><td>DFS.datanode.http.Address</td><td>0.0.0.0:30075</td></tr>
<tr><td>DFS.datanode.IPC.Address</td><td>0.0.0.0:30020</td></tr>
<tr><td>DFS.Secondary.http.Address</td><td>0.0.0.0:30090</td></tr>
<tr><td>mapred.job.Tracker.http.Address</td><td>jobtrackerhost:30030</td></tr>
<tr><td>mapred.Task.Tracker.http.Address</td><td>0.0.0.0:30060</td></tr>
<tr><td>mapreduce.history.server.http.Address</td><td>0.0.0.0:31111</td></tr>
<tr><td>templeton.Port</td><td>30111</td></tr>
</table>

 **HDInsight 3.1 en 3.0 (HDP 2.1 en 2.0)**

<table border="1">
<tr><th>Naam</th><th>Waarde</th></tr>
<tr><td>DFS.namenode.HTTP-adres</td><td>namenodehost:30070</td></tr>
<tr><td>DFS.namenode.https-adres</td><td>headnodehost:30470</td></tr>
<tr><td>DFS.datanode.Address</td><td>0.0.0.0:30010</td></tr>
<tr><td>DFS.datanode.http.Address</td><td>0.0.0.0:30075</td></tr>
<tr><td>DFS.datanode.IPC.Address</td><td>0.0.0.0:30020</td></tr>
<tr><td>DFS.namenode.Secondary.HTTP-adres</td><td>0.0.0.0:30090</td></tr>
<tr><td>yarn.nodemanager.WebApp.Address</td><td>0.0.0.0:30060</td></tr>
<tr><td>templeton.Port</td><td>30111</td></tr>
</table>

### <a name="dependencies"></a>Afhankelijkheden
Hallo zijn volgende afhankelijkheden toegevoegd in HDInsight 3.x (HDP2.x):

* guice servlet
* optiq-core
* javax.inject
* activering
* jsr305
* geronimo-jaspic_1.0_spec
* jul naar slf4j
* Java-xmlbuilder
* ant
* Commons-compiler
* jdo-api
* Commons math3
* paranamer
* jaxb impl
* stringtemplate
* eigenbase xom
* Jersey servlet
* Commons exec
* jaxb-api
* jetty-all-server
* janino
* xercesImpl
* optiq avatica
* jta
* eigenbase-eigenschappen
* groovy-alle
* hamcrest-core
* E-mail
* linq4j
* jpam
* Jersey-client
* aopalliance
* geronimo-annotation_1.0_spec
* ant starten
* Jersey guice
* XML-API 's
* stax-api
* Asm commons
* Asm-structuur
* wadl
* geronimo-jta_1.1_spec
* guice
* leveldbjni-alle
* snelheid
* jettison
* treffende java
* jetty-alle
* Commons dbcp

Hallo volgende afhankelijkheden bestaan niet meer in HDInsight 3.x (HDP2.x):

* jdeb
* kfs
* sqlline
* klimop
* aspectjrt
* JSON
* Core
* jdo2-api
* avro mapred
* datanucleus enhancer
* JSP
* Commons-logboekregistratie-api
* Commons math
* JavaEWAH
* aspectjtools
* javolution
* hdfsproxy
* hbase
* treffende

### <a name="version-changes"></a>Wijzigingen in versie
Hallo volgende versiewijzigingen zijn aangebracht tussen HDInsight 2.x (HDP1.x) en HDInsight 3.x (HDP2.x):

* core-metrische gegevens: [2.1.2]-[3.0.0] >
* derbynet: [10.4.2.0]-[10.10.1.1] >
* datanucleus: ['rdbms-3.0.8'] -> ['rdbms-3.2.9']
* Jasper-compiler: [5.5.12]-[5.5.23] >
* log4j: ['en met 1.2.15', '1.2.16'] -> ['1.2.16', '1.2.17']
* derbyclient: [10.4.2.0]-[10.10.1.1] >
* httpcore: [4.2.4]-[4.2.5] >
* hsqldb: [1.8.0.10]-[2.0.0] >
* jets3t: [0.6.1]-[0.9.0] >
* java-protobuf: [2.4.1]-[2.5.0] >
* derby: [10.4.2.0]-[10.10.1.1] >
* Jasper: ['runtime-5.5.12'] -> ['runtime-5.5.23']
* Commons daemon: [1.0.1]-[1.0.13] >
* core-datanucleus: [3.0.9]-[3.2.10] >
* datanucleus-api-jdo: [3.0.7]-[3.2.6] >
* zookeeper: [3.4.5.1.3.9.0-01320]-[3.4.5.2.1.3.0-1948] >
* bonecp: [0.7.1.RELEASE] -> ['
* 0.8.0.RELEASE']

### <a name="drivers"></a>Stuurprogramma's
Hallo Java Database Connectivity (JDBC)-stuurprogramma voor SQL Server wordt intern gebruikt door HDInsight en wordt niet gebruikt voor externe bewerkingen. Als u wilt tooconnect tooHDInsight met behulp van de Open Database Connectivity (ODBC), gebruik Hallo Microsoft Hive ODBC-stuurprogramma. Zie voor meer informatie [tooHDInsight Excel verbinding maken met het stuurprogramma Microsoft Hive ODBC Hallo](hdinsight-connect-excel-hive-odbc-driver.md).

### <a name="bug-fixes"></a>Oplossingen voor problemen
Met deze release, hebben we Hallo volgende versies van HDInsight met verschillende oplossingen voor problemen vernieuwd:

* HDInsight 2.1 (HDP 1.3)
* HDInsight 3.0 (HDP 2.0)
* HDInsight 3.1 (HDP 2.1)

## <a name="hortonworks-release-notes"></a>Hortonworks release-opmerkingen
Releaseopmerkingen voor Hallo Hortonworks Data Platforms (HDPs) die worden gebruikt door de versie-HDInsight-clusters zijn beschikbaar op Hallo volgende locaties:

* HDInsight versie 3.1 maakt gebruik van een Hadoop-distributie die is gebaseerd op Hallo [Hortonworks Data Platform 2.1.7][hdp-2-1-7]. Dit is gemaakt bij gebruik van Azure-portal Hallo na 7-11-2014 van Hallo standaard Hadoop-cluster. 3.1 HDInsight-clusters die zijn gemaakt voordat 7-11-2014 zijn gebaseerd op Hallo [Hortonworks Data Platform 2.1.1][hdp-2-1-1]
* HDInsight versie 3.0 gebruikt een Hadoop-distributie die is gebaseerd op Hallo [Hortonworks Data Platform 2.0][hdp-2-0-8].
* HDInsight versie 2.1 maakt gebruik van een Hadoop-distributie die is gebaseerd op Hallo [Hortonworks Data Platform 1.3][hdp-1-3-0].
* HDInsight versie 1.6 maakt gebruik van een Hadoop-distributie die is gebaseerd op Hallo [Hortonworks Data Platform 1.1][hdp-1-1-0].

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[nuget-link]: https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.HDInsight/

[webpi-link]: http://go.microsoft.com/?linkid=9811175&clcid=0x409

[hdinsight-install-spark]: ../hdinsight-hadoop-spark-install/
[hdinsight-r-scripts]: ../hdinsight-hadoop-r-scripts/

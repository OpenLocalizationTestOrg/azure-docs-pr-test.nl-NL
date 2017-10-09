---
title: aaaHadoop onderdelen en versies - Azure HDInsight | Microsoft Docs
description: Informatie over Hallo Hadoop-onderdelen en -versies in HDInsight en Hallo serviceniveaus beschikbaar in deze cloud-distributie van Hortonworks Data Platform.
keywords: hadoop-versies, hadoop-ecosysteem onderdelen, hadoop-onderdelen, hoe toocheck hadoop-versie
services: hdinsight
editor: cgronlun
manager: asadk
author: bprakash
tags: azure-portal
documentationcenter: 
ms.assetid: 367b3f4a-f7d3-4e59-abd0-5dc59576f1ff
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: bprakash
ms.openlocfilehash: b661d901b0113458c3501ec06454fc8841189672
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-hadoop-components-and-versions-available-with-hdinsight"></a>Wat zijn Hallo Hadoop-onderdelen en versies die beschikbaar met HDInsight?

Meer informatie over Hallo Apache Hadoop-ecosysteem onderdelen en versies in Microsoft Azure HDInsight, evenals Hallo serviceniveaus Standard en Premium. Leer ook hoe toocheck Hadoop component versies in HDInsight. 

Elke versie HDInsight is een cloud-distributiepunt van een versie van Hortonworks Data Platform HDP ().

## <a name="hadoop-components-available-with-different-hdinsight-versions"></a>Hadoop-onderdelen met verschillende versies van HDInsight
Azure HDInsight biedt ondersteuning voor meerdere versies van Hadoop-cluster die op elk gewenst moment kunnen worden geïmplementeerd. Elke versie keuze maakt een specifieke versie van Hallo HDP distributie en een reeks onderdelen die deel uitmaken van dit distributiepunt. Vanaf 17 februari 2017-cluster Hallo standaard gebruikt door Azure HDInsight versie 3.5 is en is gebaseerd op HDP 2.5.

Hallo onderdeel versies die zijn gekoppeld aan de versies van HDInsight-cluster worden weergegeven in de volgende tabel Hallo. 

> [!NOTE]
> de standaardversie Hallo voor Hallo HDInsight-service kan zonder voorafgaande kennisgeving worden gewijzigd. Als u een afhankelijkheid versie hebt, Hallo HDInsight version opgeven wanneer u clusters met de Hallo .NET SDK met Azure PowerShell en Azure CLI maken.

| Onderdeel | HDInsight 3.6 (standaard) | HDInsight 3.5 | HDInsight 3.4 | HDInsight 3.3 | 3.2 voor HDInsight | HDInsight 3.1 | HDInsight 3.0 |
| --- | --- | --- | --- | --- | --- | --- |--- |
| Hortonworks Data Platform |2.6 |2.5 |2.4 |2.3 |2.2 |2.1.7 |2.0 |
| Apache Hadoop en YARN |2.7.3 |2.7.3 |2.7.1 |2.7.1 |2.6.0 |2.4.0 |2.2.0 |
| Apache Tez |0.7.0 |0.7.0 |0.7.0 |0.7.0 |0.5.2 |0.4.0 |-|
| Apache Pig |0.16.0 |0.16.0 |0.15.0 |0.15.0 |0.14.0 |0.12.1 |0.12.0 |
| Apache Hive en HCatalog |1.2.1 |1.2.1 |1.2.1 |1.2.1 |0.14.0 |0.13.1 |0.12.0 |
| Apache Hive2 | 2.1.0 |-|-|-|-|-|-|
| Apache Tez Hive2 | 0.8.4 |-|-|-|-|-|-|
| Apache Zwerver | 0.7.0 |0.6.0 |-|-|-|-|-|
| Apache HBase |1.1.2 |1.1.2 |1.1.2 |1.1.1 |0.98.4 |0.98.0 |-|
| Apache Sqoop |1.4.6 |1.4.6 |1.4.6 |1.4.6 |1.4.5 |1.4.4 |1.4.4 |
| Apache Oozie |4.2.0 |4.2.0 |4.2.0 |4.2.0 |4.1.0 |4.0.0 |4.0.0 |
| Apache Zookeeper |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.5 |3.4.5 |
| Apache Storm |1.1.0 |1.0.1 |0.10.0 |0.10.0 |0.9.3 |0.9.1 |-|
| Apache Mahout |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0 |0.9.0 |-|
| Apache Phoenix |4.7.0 |4.7.0 |4.4.0 |4.4.0 |4.2.0 |4.0.0.2.1.7.0-2162 |-|
| Apache Spark |2.1.0 (alleen voor Linux) |1.6.2 + 2.0 (alleen voor Linux) |1.6.0 (alleen voor Linux) |1.5.2 (alleen experimentele build Linux) |1.3.1 (alleen Windows) |-|-|
| Apache Kafka | 0.10.0 | 0.10.0 | 0.9.0 |-|-|-|-|
| Apache Ambari | 2.5.0 | 2.4.0 | 2.2.1 | 2.1.0 |-|-|-|
| Apache Zeppelin | 0.7.0 |-|-|-|-|-|-|
| Mono |4.2.1 |4.2.1 |3.2.8 |-|-|-|

## <a name="check-for-current-hadoop-component-version-information"></a>Controleren op huidige Hadoop component versie-informatie

Hallo Hadoop-ecosysteem onderdeel versies die zijn gekoppeld met versies van HDInsight-cluster kunnen met updates tooHDInsight wijzigen. Hallo Ambari REST-API wordt gebruikt door toocheck Hallo Hadoop-onderdelen en tooverify welke versies worden gebruikt voor een cluster. Hallo **GetComponentInformation** opdracht haalt informatie over de onderdelen van service. Zie voor meer informatie, Hallo [Ambari documentatie][ambari-docs].

Voor Windows-clusters, een andere manier Hallo toocheck componentversie is toolog in tooa cluster met behulp van extern bureaublad en bekijkt hello inhoud van Hallo C:\apps\dist\ directory.

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie voor meer informatie [buiten gebruik stellen van Windows op HDInsight](#hdinsight-windows-retirement).

### <a name="release-notes"></a>Releaseopmerkingen

Zie [HDInsight releaseopmerkingen](hdinsight-release-notes.md) voor extra release-opmerkingen op Hallo nieuwste versies van HDInsight.

## <a name="supported-hdinsight-versions"></a>Ondersteunde versies van HDInsight
Hallo bevat volgende tabel Hallo-versies van HDInsight die momenteel beschikbaar op Hallo Azure-portal zijn. Hallo HDP versies die overeenkomen met de HDInsight-versie tooeach worden samen met de Hallo product release datums weergegeven. Hallo-ondersteuning is verlopen en buiten gebruik stellen datums worden ook gegeven wanneer deze zijn bepaald.

> [!NOTE]
> Na de ondersteuning voor een versie is verlopen, deze mogelijk niet beschikbaar is via de klassieke Hallo Microsoft Azure-portal. Clusterversies blijven echter beschikbaar via Hallo toobe `Version` parameter in Windows PowerShell Hallo [nieuw AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619331.aspx) opdracht en de .NET SDK Hallo tot Hallo versie intrekkingsdatum.
> 
> Maximaal beschikbare clusters met twee hoofdknooppunten worden standaard voor HDInsight versie 2.1 en hoger geïmplementeerd. Ze zijn niet beschikbaar voor HDInsight versie 1.6-clusters.

| HDInsight-versie | HDP versie | BESTURINGSSYSTEEM VAN VIRTUELE MACHINE | Hoge beschikbaarheid | Releasedatum | Beschikbaarheid op Hallo Azure-portal | Ondersteuning voor vervaldatum | Vervaldatum |
| --- | --- | --- | --- | --- | --- | --- | --- |
| HDInsight 3.6 |HDP 2.6 |Ubuntu 16 |Ja |4 april 2017 |Ja | | |
| HDInsight 3.5 |HDP 2,5 |Ubuntu 16 |Ja |30 september 2016 |Ja |5 september 2017 |31 mei 2018 |
| HDInsight 3.4 |2.4 HDP |Ubuntu 14.0.4 TNS |Ja |29 maart 2016 |Ja |29 december 2016 |9 januari 2018 |
| HDInsight 3.3 |2.3 HDP |Windows Server 2012 R2 |Ja |2 december 2015 |Ja |27 juni 2016 |31 juli 2018 |
| HDInsight 3.3 |2.3 HDP |Ubuntu 14.0.4 TNS |Ja |2 december 2015 |Ja |27 juni 2016 |31 juli 2017 |
| 3.2 voor HDInsight |HDP 2.2 |Ubuntu 12.04 TNS of Windows Server 2012 R2 |Ja |18 februari 2015 |Nee |1 maart 2016 |1 april 2017 |
| HDInsight 3.1 |HDP 2.1 |Windows Server 2012 R2 |Ja |24 juni 2014 |Nee |18 mei 2015 |30 juni 2016 |
| HDInsight 3.0 |HDP 2.0 |Windows Server 2012 R2 |Ja |11 februari 2014 |Nee |17 september 2014 |30 juni 2015 |
| HDInsight 2.1 |1.3 HDP |Windows Server 2012 R2 |Ja |28 oktober 2013 |Nee |12 mei 2014 |31 mei 2015 |
| HDInsight 1.6 |HDP 1.1 | |Nee |28 oktober 2013 |Nee |26 april 2014 |31 mei 2015 |

## <a name="hdinsight-windows-retirement"></a>HDInsight Windows buiten gebruik stellen
Microsoft Azure HDInsight versie 3.3 is de laatste versie van HDInsight op Windows hello. Hallo is intrekkingsdatum voor HDInsight in Windows 31 juli 2018. Als u een HDInsight-clusters op Windows 3.3 of eerder hebt, moet u tooHDInsight op Linux (HDInsight versie 3.5 of nieuwer) voordat 31 juli 2018 migreren. Migreren van toohello Linux-besturingssysteem kunt u tooretain Hallo mogelijkheid toocreate of het formaat van uw HDInsight-clusters. Ondersteuning voor HDInsight versie 3.3 in Windows is verlopen op 27 juni 2016.

Beginnen met HDInsight versie 3.4, heeft Microsoft uitgegeven HDInsight alleen op Hallo Linux-besturingssysteem. Als gevolg hiervan zijn sommige Hallo-onderdelen in HDInsight beschikbaar voor Linux alleen. Deze omvatten Apache Zwerver, Kafka, interactieve Hive, Spark, HDInsight-toepassingen en Azure Data Lake Store als primaire Hallo-bestandssysteem. Toekomstige versies van HDInsight zijn alleen beschikbaar op Hallo Linux-besturingssysteem. Er zijn geen toekomstige versies van HDInsight in Windows. 

## <a name="faqs"></a>Veelgestelde vragen

### <a name="what-is-hello-timeline-for-retiring-hdinsight-on-windows"></a>Wat is de tijdlijn voor het buiten gebruik stellen HDInsight op Windows hello?
31 juli 2018, is Hallo intrekkingsdatum voor HDInsight in Windows. Als Hallo geplande intrekkingsdatum verschilt voor uw regio, krijgt u een melding afzonderlijk. 

### <a name="what-is-hello-impact-of-retiring-hdinsight-on-windows-for-existing-customers"></a>Wat is Hallo gevolgen van het buiten gebruik stellen van HDInsight in Windows voor bestaande klanten?
Nadat HDInsight op Windows is buiten gebruik gesteld, kan u een nieuw HDInsight Windows-cluster maken of vergroten of verkleinen van een bestaand HDInsight Windows-cluster. Ondersteuning voor HDInsight versie 3.3 verlopen op 27 juni 2016. Er is daarom geen ondersteuning of oplossingen voor problemen voor HDInsight 3.3 of eerdere versies. Toekomstige versies van HDInsight zijn alleen beschikbaar op Hallo Linux-besturingssysteem. Er zijn geen toekomstige versies van HDInsight in Windows.
 
### <a name="which-versions-of-hdinsight-on-windows-are-affected"></a>Welke versies van HDInsight op Windows optreedt?
Azure HDInsight versie 3.3 is de laatste versie van HDInsight voor Windows hello. Voordat u HDInsight op Windows is buiten gebruik gesteld, gemigreerd alle HDInsight Windows clusters versie 3.3 of eerder moet tooHDInsight op Linux versie 3.5 of hoger. Migreren van uw tooHDInsight clusters op Linux, kunt u tooretain Hallo mogelijkheid toocreate nieuwe clusters of bestaande clusters vergroten of verkleinen. 

### <a name="what-do-i-need-toodo"></a>Wat kan ik toodo nodig?
Uw HDInsight Windows-clusters tooa ondersteund HDInsight Linux-cluster te migreren voordat 31 juli 2018. Meer informatie Hallo [HDInsight migratie document](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). Zie voor meer informatie over Azure HDInsight versies Hallo lijst met [ondersteunde versies](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-component-versioning#supported-hdinsight-versions). 

### <a name="where-do-i-find-hello-cluster-os-type"></a>Waar vind ik Hallo cluster BS-type
Ga in de Azure-portal hello, toohello overzichtspagina van HDInsight-Cluster en zoek **type Cluster** onder **Essentials**. Hallo-clustertypen besturingssysteem worden op deze pagina weergegeven. 

### <a name="i-cant-migrate-tooan-hdinsight-linux-cluster-by-july-31-2018-what-is-hello-impact-toomy-hdinsight-windows-cluster"></a>Ik kan geen tooan HDInsight Linux-cluster migreert met 31 juli 2018. Wat is Hallo impact toomy HDInsight Windows-cluster?
Hallo HDInsight Windows-cluster wordt uitgevoerd als-is, maar u kunt een nieuw HDInsight Windows-cluster maken of een bestaand HDInsight Windows-cluster vergroten of verkleinen. 

### <a name="my-cluster-has-a-net-dependency-how-do-i-resolve-this-dependency-on-linux"></a>Mijn cluster heeft een .NET-afhankelijkheid. Hoe kan ik deze afhankelijkheid op Linux oplossen?
U kunt uw Linux-cluster afhankelijkheid oplossen met behulp van Hallo [Mono project](http://www.mono-project.com/). Deze implementatie open-source van .NET is beschikbaar voor HDInsight Linux-clusters. Meer informatie Hallo [HDInsight migratie document](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). 

### <a name="im-a-new-customer-for-hdinsight-on-windows-how-can-i-create-an-hdinsight-windows-cluster"></a>Ik ben een nieuwe klant voor HDInsight in Windows. Hoe kan ik een HDInsight Windows-cluster maken?
Vanaf 3 juli 2017 kunnen alleen bestaande HDInsight Windows-klanten nieuwe HDInsight Windows clusters maken. Nieuwe klanten kunnen een HDInsight Windows-cluster maken in hello Azure-portal met behulp van PowerShell of Hallo SDK. U kunt het beste nieuwe klanten een Linux-HDInsight-cluster maken. Bestaande klanten kunnen nieuwe HDInsight Windows clusters maken tot Hallo HDInsight op Windows intrekkingsdatum. 

### <a name="is-there-a-pricing-impact-associated-with-moving-from-hdinsight-on-windows-toohdinsight-on-linux"></a>Is er een prijscategorie invloed die zijn gekoppeld aan het verplaatsen van HDInsight op Windows-tooHDInsight op Linux?
Nee, Hallo prijzen is hello dezelfde voor HDInsight op beide OS. 

### <a name="what-are-hello-customer-advantages-associated-with-hello-move-tooonly-using-hdinsight-on-linux"></a>Wat zijn Hallo klant voordelen die zijn gekoppeld aan Hallo tooonly met HDInsight op Linux verplaatsen?
* Snellere tijd op de markt voor open-source big data-technologieën via Hallo HDInsight-service
* Een grote community en ecosysteem voor ondersteuning
* Mogelijkheid tooexercise actieve ontwikkeling door Hallo open source community voor Hadoop en andere technologieën voor big data

### <a name="does-hdinsight-on-linux-provide-additional-functionality-beyond-what-is-available-in-hdinsight-on-windows"></a>Biedt HDInsight op Linux aanvullende functionaliteit naast wat beschikbaar in HDInsight op Windows is?
Beginnen met HDInsight versie 3.4, heeft Microsoft uitgegeven HDInsight alleen op Hallo Linux-besturingssysteem. Als gevolg hiervan zijn sommige Hallo-onderdelen in HDInsight beschikbaar voor Linux alleen. Deze omvatten Apache Zwerver, Kafka, interactieve Hive, Spark, HDInsight-toepassingen en Azure Data Lake Store als primaire Hallo-bestandssysteem. 

## <a name="service-level-agreement-for-hdinsight-cluster-versions"></a>Serviceovereenkomst voor versies van HDInsight-cluster
Hallo serviceovereenkomst (SLA) is gedefinieerd in termen van een _ondersteuning venster_. Hallo ondersteuning venster is Hallo periode die een HDInsight-cluster versie wordt ondersteund door de klantenservice van Microsoft. Als het Hallo-versie heeft een _ondersteunen vervaldatum_ die is doorgegeven, Hallo HDInsight-cluster is buiten Hallo ondersteuning venster. Zie voor meer informatie over ondersteunde versies Hallo lijst met [ondersteunde versies van HDInsight-cluster](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). vervaldatum van Hallo-ondersteuning voor een opgegeven HDInsight versie X (nadat er een nieuwere versie van de X + 1 beschikbaar is) wordt berekend als hello later van:  

* Formule 1: 180 dagen toohello datum wanneer Hallo HDInsight-cluster versie X werd uitgebracht toevoegen.
* Formule 2: 90 dagen toohello datum wanneer Hallo HDInsight-cluster versie X + 1 wordt beschikbaar gesteld in Azure-portal toevoegen.

Hallo _intrekkingsdatum_ Hallo datum waarna Hallo-cluster versie kan niet worden gemaakt op HDInsight. Vanaf 31 juli 2017 u kan niet de grootte van een HDInsight-cluster na de datum buiten gebruik stellen. 

> [!NOTE]
> HDInsight Windows-clusters (inclusief versie 2.1, 3.0, 3.1, 3.2 en 3.3) worden uitgevoerd op Azure Gast OS-familie versie 4, die gebruikmaakt van Hallo 64-bits versie van Windows Server 2012 R2. Azure Gast OS-familie versie 4 ondersteunt Hallo .NET Framework versie 4.0, 4.5 4.5.1 en 4.5.2.

## <a name="hortonworks-release-notes-associated-with-hdinsight-versions"></a>Hortonworks release-opmerkingen die zijn gekoppeld aan de versies van HDInsight

Hallo sectie koppelingen toorelease notities voor Hallo Hortonworks Data Platform distributies en de Apache-onderdelen die worden gebruikt met HDInsight.
* HDInsight-cluster versie 3.6 maakt gebruik van een Hadoop-distributie die is gebaseerd op [Hortonworks Data Platform 2.6](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.0/bk_release-notes/content/ch_relnotes.html).
* HDInsight-cluster versie 3.5 maakt gebruik van een Hadoop-distributie die is gebaseerd op [Hortonworks Data Platform 2.5](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.5.0/bk_release-notes/content/ch_relnotes_v250.html). HDInsight-cluster versie 3.5 is Hallo _standaard_ Hadoop-cluster dat is gemaakt in hello Azure-portal.
* HDInsight-cluster versie 3.4 maakt gebruik van een Hadoop-distributie die is gebaseerd op [Hortonworks Data Platform 2.4](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html).
* HDInsight-cluster versie 3.3 maakt gebruik van een Hadoop-distributie die is gebaseerd op [Hortonworks Data Platform 2.3](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html).

  * [Opmerkingen bij de release van Apache Storm](https://storm.apache.org/2015/11/05/storm0100-released.html) zijn beschikbaar op Hallo Apache website.
  * [Apache Hive releaseopmerkingen](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12332384&styleName=Text&projectId=12310843) zijn beschikbaar op Hallo Apache website.
* HDInsight-cluster versie 3.2 maakt gebruik van een Hadoop-distributie die is gebaseerd op [Hortonworks Data Platform 2.2][hdp-2-2].

  * Releaseopmerkingen voor specifieke onderdelen van Apache beschikbaar zijn als volgt: [Hive 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310843&version=12326450), [Pig 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310730&version=12326954), [HBase 0.98.4](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310753&version=12326810), [Phoenix 4.2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12315120&version=12327581), [M/R 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310941&version=12327180), [HDFS 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310942&version=12327181), [YARN 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12313722&version=12327197), [algemene](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310240&version=12327179), [Tez 0.5.2](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314426&version=12328742), [Ambari 2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12312020&version=12327486), [Storm-0.9.3](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314820&version=12327112), en [Oozie 4.1.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12324960&projectId=12311620).
* HDInsight-cluster versie 3.1 maakt gebruik van een Hadoop-distributie die is gebaseerd op [Hortonworks Data Platform 2.1.7][hdp-2-1-7]. 3.1 HDInsight-clusters die zijn gemaakt vóór November, 7, 2014, zijn gebaseerd op [Hortonworks Data Platform 2.1.1][hdp-2-1-1].
* HDInsight-cluster versie 3.0 maakt gebruik van een Hadoop-distributie die is gebaseerd op [Hortonworks Data Platform 2.0][hdp-2-0-8].
* HDInsight-cluster versie 2.1 maakt gebruik van een Hadoop-distributie die is gebaseerd op [Hortonworks Data Platform 1.3][hdp-1-3-0].
* HDInsight-cluster versie 1.6 maakt gebruik van een Hadoop-distributie die is gebaseerd op [Hortonworks Data Platform 1.1][hdp-1-1-0].

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard en HDInsight Premium

Azure HDInsight biedt Hallo big data cloud twee categorieën aanbiedingen: _standaard_ en _Premium_. Hallo volgende tabel bevat functies die beschikbaar zijn _alleen_ in HDInsight Premium. Functies die niet expliciet worden beschreven in de tabel Hallo zijn beschikbaar in HDInsight Standard en Premium.

> [!NOTE]
> Hello HDInsight Premium aanbieding momenteel in preview en alleen beschikbaar voor Linux-clusters is.

| HDInsight Premium-functie | Beschrijving |
| --- | --- |
| Domein-HDInsight-clusters |Lid worden van HDInsight-clusters tooAzure Active Directory (Azure AD)-domeinen voor beveiliging op bedrijfsniveau. In HDInsight Premium kunt u een lijst met werknemers van uw bedrijf die kan worden geverifieerd via Azure AD-toolog op tooan HDInsight-cluster configureren. Hallo-ondernemingsadministrator toegangsbeheer op basis van rollen voor Hive-beveiliging kunt configureren met behulp van [Apache Zwerver](http://hortonworks.com/apache/ranger/) en beperk de data access-toouse alleen zoveel nodig. Ten slotte Hallo beheerder gegevens die worden gebruikt door werknemers kunt controleren en wijzigingen tooaccess beleid, waardoor het bereiken van een hoge mate van toezicht van hun bedrijfsbronnen controleren. Zie voor meer informatie [HDInsight-clusters domein configureren](hdinsight-domain-joined-configure.md). |

### <a name="cluster-types-supported-in-hdinsight-premium"></a>Clustertypen worden ondersteund in HDInsight Premium
Hallo bevat volgende tabel de clustertypen Hallo die worden ondersteund in HDInsight Premium.

| Clustertype | Standard | Premium (Preview) |
| --- | --- | --- |
| Hadoop |Ja |Ja (alleen HDInsight 3.6) |
| Spark |Ja |Nee |
| HBase |Ja |Nee |
| Storm |Ja |Nee |
| R Server |Ja |Nee |
| Interactieve Hive (Preview) |Ja |Nee |
| Kafka (Preview) |Ja |Nee | 

### <a name="support-for-azure-data-lake-store-in-hdinsight-premium"></a>Ondersteuning voor Azure Data Lake Store in HDInsight Premium

HDInsight Premium-clusters bieden geen ondersteuning voor het gebruik van Azure Data Lake Store als primaire opslag. U kunt Azure Data Lake Store echter gebruiken als extra opslag met clusters van HDInsight Premium.

### <a name="pricing-and-sla"></a>Prijzen en SLA
Zie voor meer informatie over de prijzen en SLA voor HDInsight Premium [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="default-node-configuration-and-virtual-machine-sizes-for-clusters"></a>Standaard configuratie en de virtuele machine knooppuntgrootten voor clusters
Hallo tabellen lijst Hallo standaard virtuele machine (VM) grootten voor HDInsight-clusters te volgen.

> [!IMPORTANT]
> Als u meer dan 32 worker-knooppunten in een cluster, moet u een grootte van het hoofdknooppunt met ten minste 8 kerngeheugens en 14 GB RAM-geheugen.
> 
> 

* Alle ondersteunde regio's, behalve Brazilië-Zuid en Japan-West:

  | Clustertype | Hadoop | HBase | Storm | Spark | R Server |
  | --- | --- | --- | --- | --- | --- |
  | HEAD: standaard VM-grootte |D3 v2 |D3 v2 |A3 |D12 v2 |D12 v2 |
  | HEAD: aanbevolen VM-grootten |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |A3, A4, A5 |D12 v2, D13 v2, D14 v2 |D12 v2, D13 v2, D14 v2 |
  | Worker: standaard VM-grootte |D3 v2 |D3 v2 |D3 v2 |Windows: D12 v2; Linux: D4 v2 |Windows: D12 v2; Linux: D4 v2 |
  | Werknemer: aanbevolen VM-grootten |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |
  | ZooKeeper: standaard VM-grootte | |A3 |A2 | | |
  | ZooKeeper: aanbevolen VM-grootten | |A3, A4, A5 |A2, A3, A4 | | |
  | Rand: standaard VM-grootte | | | | |Windows: D12 v2; Linux: D4 v2 |
  | Rand: aanbevolen VM-grootte | | | | |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |
* Brazilië-Zuid en Japan-West alleen (geen grootten v2):

  | Clustertype | Hadoop | HBase | Storm | Spark | R Server |
  | --- | --- | --- | --- | --- | --- |
  | HEAD: standaard VM-grootte |D3 |D3 |A3 |D12 |D12 |
  | HEAD: aanbevolen VM-grootten |D3, D4 D12 |D3, D4 D12 |A3, A4, A5 |D12, D13 D14 |D12, D13 D14 |
  | Worker: standaard VM-grootte |D3 |D3 |D3 |Windows: D12; Linux: D4 |Windows: D12; Linux: D4 |
  | Werknemer: aanbevolen VM-grootten |D3, D4 D12 |D3, D4 D12 |D3, D4 D12 |Windows: D12, D13 D14; Linux: D4, D12, D13 D14 |Windows: D12, D13 D14; Linux: D4, D12, D13 D14 |
  | ZooKeeper: standaard VM-grootte | |A2 |A2 | | |
  | ZooKeeper: aanbevolen VM-grootten | |A2, A3, A4 |A2, A3, A4 | | |
  | Rand: standaard VM-grootten | | | | |Windows: D12; Linux: D4 |
  | Rand: aanbevolen VM-grootten | | | | |Windows: D12, D13 D14; Linux: D4, D12, D13 D14 |

> [!NOTE]
> - HEAD staat bekend als *Nimbus* type voor Hallo Storm-cluster.
> - Werknemer staat bekend als *Supervisor* type voor Hallo Storm-cluster.
> - Werknemer staat bekend als *regio* type voor Hallo HBase-cluster.

## <a name="next-steps"></a>Volgende stappen
- [Setup voor Hadoop, Spark en meer informatie over de HDInsight-cluster](hdinsight-hadoop-provision-linux-clusters.md)
- [Werken in Hadoop in HDInsight via Windows-PC](hdinsight-hadoop-windows-tools.md)

[Supported HDInsight versions]:(#supported-hdinsight-versions)

[image-hdi-versioning-versionscreen]: ./media/hdinsight-component-versioning/hdi-versioning-version-screen.png

[wa-forums]: http://azure.microsoft.com/support/forums/

[connect-excel-with-hive-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md

[hdp-2-2]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[ambari-docs]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[zookeeper]: http://zookeeper.apache.org/

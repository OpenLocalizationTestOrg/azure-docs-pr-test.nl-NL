---
title: aaaEnable heap dumpbestanden voor Hadoop op HDInsight - Azure-services | Microsoft Docs
description: Schakel heap dumpbestanden voor Hadoop-services voor foutopsporing en analyse van Linux gebaseerde HDInsight-clusters.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8f151adb-f687-41e4-aca0-82b551953725
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 49e30f26e1a83f19e068e9da253b5548caec70d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a>Dumpbestanden voor Hadoop-services op Linux gebaseerde HDInsight heap inschakelen

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Dumpbestanden voor heap bevatten een momentopname van de toepassing hello geheugen, met inbegrip van waarden van variabelen Hallo gelijktijdig Hallo Hallo dump is gemaakt. Ze zijn daarom nuttig voor het oplossen van problemen die tijdens runtime optreden.

> [!IMPORTANT]
> Hallo werken stappen in dit document alleen met HDInsight-clusters die gebruikmaken van Linux. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a name="whichServices"></a>Services

U kunt de heap dumpbestanden voor Hallo na services inschakelen:

* **hcatalog** -tempelton
* **hive** -hiveserver2, metastore, derbyserver
* **mapreduce** -jobhistoryserver
* **yarn** -resourcemanager, nodemanager, timelineserver
* **hdfs** -datanode, secondarynamenode, namenode

U kunt ook heap dumpbestanden voor Hallo kaart inschakelen en de processen die worden uitgevoerd door HDInsight.

## <a name="configuration"></a>Understanding heap dump configuratie

Dumpbestanden voor heap zijn ingeschakeld door de opties (ook wel aangeduid als kiest, of parameters) toohello JVM wanneer een service wordt gestart. Voor de meeste Hadoop-services, kunt u Hallo shell-script waarmee toostart Hallo service toopass deze opties wijzigen.

In elk script is een exporteren voor  **\* \_OPTS**, toohello JVM die Hallo opties bevat die worden doorgegeven. Bijvoorbeeld in Hallo **hadoop env.sh** script, Hallo-regel die begint met `export HADOOP_NAMENODE_OPTS=` Hallo opties voor Hallo NameNode service bevat.

Overzicht en verminderen processen zijn enigszins verschillen, omdat deze bewerkingen een onderliggend proces van Hallo MapReduce-service zijn. Elk toewijzen of verminder proces wordt uitgevoerd in een container onderliggend en er zijn twee vermeldingen die Hallo JVM opties bevatten. Beide opgenomen in **mapred site.xml**:

* **mapreduce.Admin.map.child.Java.opts**
* **mapreduce.Admin.reduce.child.Java.opts**

> [!NOTE]
> U wordt aangeraden met Ambari toomodify beide Hallo scripts en mapred site.xml-instellingen als Ambari verwerken wijzigingen tussen knooppunten in cluster hello te repliceren. Zie Hallo [Ambari met behulp van](#using-ambari) sectie voor specifieke stappen.

### <a name="enable-heap-dumps"></a>Heapdumps inschakelen

Hallo volgende optie wordt ingeschakeld heap dumpbestanden wanneer er een OutOfMemoryError optreedt:

    -XX:+HeapDumpOnOutOfMemoryError

Hallo  **+**  geeft aan dat deze optie is ingeschakeld. Hallo standaard is uitgeschakeld.

> [!WARNING]
> Dumpbestanden voor heap zijn niet ingeschakeld voor services van Hadoop in HDInsight standaard zoals dumpbestanden Hallo kunnen oplopen. Als u ze voor het oplossen van inschakelt, moet u ze zodra u hebt gereproduceerd Hallo probleem en de verzamelde Hallo dumpbestanden toodisable.

### <a name="dump-location"></a>Locatie van de dump

de standaardlocatie Hallo voor Hallo-bestand is de huidige werkmap Hallo. U kunt bepalen wanneer hello bestand wordt opgeslagen met behulp van de volgende optie Hallo:

    -XX:HeapDumpPath=/path

Bijvoorbeeld, met behulp van `-XX:HeapDumpPath=/tmp` Hallo dumpbestanden toobe opgeslagen in Hallo map directory veroorzaakt.

### <a name="scripts"></a>Scripts

U kunt ook een script activeren wanneer een **OutOfMemoryError** optreedt. Bijvoorbeeld, is een melding activeren zodat u dat Hallo-fout weet opgetreden. Gebruik Hallo volgende optie tootrigger een script op een __OutOfMemoryError__:

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> Aangezien Hadoop een gedistribueerd systeem is, moet elk script dat wordt gebruikt op alle knooppunten in cluster Hallo die Hallo-service wordt uitgevoerd op worden geplaatst.
> 
> Hallo script moet ook worden op een locatie die toegankelijk is voor Hallo account Hallo-service wordt uitgevoerd als moet machtigingen voor uitvoeren. Bijvoorbeeld, u kunt desgewenst toostore scripts in `/usr/local/bin` en gebruik `chmod go+rx /usr/local/bin/filename.sh` toogrant lees- en schrijfrechten hebben.

## <a name="using-ambari"></a>Ambari gebruiken

toomodify Hallo-configuratie voor een service, gebruik Hallo stappen te volgen:

1. Open Hallo Ambari-webgebruikersinterface voor uw cluster. Hallo-URL is https://YOURCLUSTERNAME.azurehdinsight.net.

    Wanneer u wordt gevraagd, worden geverifieerd toohello site met de accountnaam Hallo HTTP (standaard: admin) en het wachtwoord voor uw cluster.

   > [!NOTE]
   > U mogelijk gevraagd een tweede maal door Ambari voor Hallo-gebruikersnaam en wachtwoord. Als dit het geval is, voert u dezelfde naam en het wachtwoord Hallo

2. Hallo-lijst met aan de linkerkant Hallo Selecteer Hallo servicegebied u toomodify. Bijvoorbeeld: **HDFS**. Selecteer bij Hallo center Hallo **Configs** tabblad.

    ![Afbeelding van Ambari web met HDFS Configs tabblad is geselecteerd](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. Met behulp van Hallo **Filter...**  -item, voer **kiest**. Alleen items met deze tekst worden weergegeven.

    ![Gefilterde lijst](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. Hallo zoeken  **\* \_OPTS** vermelding voor Hallo service u wilt tooenable heap dumpbestanden voor en voeg Hallo-opties wilt tooenable. Ik heb toegevoegd in Hallo installatiekopie te volgen, `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** post:

    ![HADOOP_NAMENODE_OPTS met - XX: + HeapDumpOnOutOfMemoryError - XX: HeapDumpPath = / tmp /](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > Wanneer inschakelen heap dumpbestanden voor Hallo toewijzen of onderliggend proces verminderen, zoekt u naar Hallo velden met de naam **mapreduce.admin.map.child.java.opts** en **mapreduce.admin.reduce.child.java.opts**.

    Gebruik Hallo **opslaan** knop toosave Hallo wijzigingen. U kunt een korte notitie Hallo wijzigingen met een beschrijving invoeren.

5. Nadat de Hallo wijzigingen zijn toegepast, Hallo **opnieuw opstarten vereist** pictogram wordt weergegeven naast een of meer services.

    ![opnieuw opstarten vereist het pictogram en start opnieuw op de knop](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. Selecteer elke service die u een herstart moet en gebruik van Hallo **serviceacties** knop te**inschakelen op onderhoudsmodus**. Onderhoudsmodus wordt voorkomen dat waarschuwingen van Hallo-service wordt gegenereerd wanneer u deze opnieuw starten.

    ![Menu Onderhoud-modus inschakelen](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. Nadat u de onderhoudsmodus hebt ingeschakeld, gebruikt u Hallo **opnieuw** knop voor Hallo-service te**alle verricht opnieuw starten**

    ![Start opnieuw alle van invloed op een vermelding](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > vermeldingen voor Hallo Hallo **opnieuw** knop kan afwijken voor andere services.

8. Zodra het Hallo-services opnieuw zijn opgestart, gebruikt u Hallo **serviceacties** te knop**inschakelen uit onderhoudsmodus**. Deze Ambari tooresume bewaking voor waarschuwingen voor Hallo-service.


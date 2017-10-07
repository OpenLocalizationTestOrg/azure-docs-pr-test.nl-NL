---
title: Hive-bibliotheken aaaAdd tijdens het HDInsight-cluster maken - Azure | Microsoft Docs
description: Meer informatie over hoe tooadd Hive-bibliotheken (jar-bestanden), tooan HDInsight-cluster tijdens het maken van het cluster.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a>Aangepaste Hive-bibliotheken toevoegen bij het maken van uw HDInsight-cluster

Als er bibliotheken die u vaak met Hive in HDInsight gebruikt, is dit document bevat informatie over het gebruik van een scriptactie toopre load Hallo bibliotheken tijdens het maken van het cluster. Bibliotheken toegevoegd met Hallo stappen in dit document wereldwijd beschikbaar zijn in de Hive - er is geen toouse nodig [JAR toevoegen](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload ze.

## <a name="how-it-works"></a>Hoe werkt het?

Wanneer u een cluster maakt, kunt u eventueel een scriptactie die een script wordt uitgevoerd op de clusterknooppunten Hallo terwijl ze worden gemaakt. Hallo-script in dit document accepteert één parameter, die een WASB-locatie met Hallo-bibliotheken (opgeslagen als jar-bestanden) toobe vooraf is geladen.

Tijdens het maken van het cluster Hallo script Hallo bestanden inventariseert, kopieert u ze toohello `/usr/lib/customhivelibs/` directory op de knooppunten hoofd- en werkrollen, worden deze vervolgens toegevoegd toohello `hive.aux.jars.path` eigenschap in Hallo `core-site.xml` bestand. Op Linux gebaseerde clusters werkt het ook Hallo `hive-env.sh` bestand met de Hallo-locatie van Hallo-bestanden.

> [!NOTE]
> Met behulp van scriptacties Hallo in dit artikel maakt Hallo bibliotheken beschikbaar zijn in Hallo volgen scenario's:
>
> * **HDInsight op basis van Linux** : wanneer met behulp van een client Hive Hallo **WebHCat**, en **HiveServer2**.
> * **HDInsight op basis van Windows** : wanneer met behulp van Hallo Hive-client en **WebHCat**.

## <a name="hello-script"></a>Hallo-script

**De locatie van script**

Voor **op basis van Linux-clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)

Voor **Windows gebaseerde clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

**Vereisten**

* Hallo scripts moet toegepaste tooboth hello **hoofdknooppunten** en **Worker-knooppunten**.

* Hallo potten die u wenst tooinstall moeten worden opgeslagen in Azure Blob Storage in een **enkele container**.

* Hallo Hallo-bibliotheek met jar-bestanden met storage-account **moet** toohello gekoppelde HDInsight-cluster worden tijdens het maken van. Moet het standaardopslagaccount hello of een account toegevoegd via __optionele configuratie__.

* Hallo WASB pad toohello container moet worden opgegeven als een parameter toohello scriptactie. Bijvoorbeeld, als hello potten worden opgeslagen in een container met de naam **bibliotheken** op een opslagaccount met de naam **mystorage**, Hallo-parameter zouden worden  **wasb://libs@mystorage.blob.core.windows.net/** .

  > [!NOTE]
  > Dit document wordt ervan uitgegaan dat u hebt al een opslagaccount, blob-container en maken geüploade Hallo bestanden tooit.
  >
  > Als u geen opslagaccount hebt gemaakt, kunt u doen via Hallo [Azure-portal](https://portal.azure.com). U kunt vervolgens een hulpprogramma zoals gebruiken [Azure Opslagverkenner](http://storageexplorer.com/) toocreate een container in het Hallo-account en het uploaden van bestanden tooit.

## <a name="create-a-cluster-using-hello-script"></a>Een cluster met behulp van Hallo script maken

> [!NOTE]
> Hallo stappen te volgen maken een Linux gebaseerde HDInsight-cluster. selecteert u een cluster op basis van Windows toocreate **Windows** cluster als Hallo OS bij het maken van Hallo-cluster en hello (PowerShell) voor Windows script gebruiken in plaats van Hallo bash-scripts.
>
> U kunt ook Azure PowerShell of Hallo HDInsight .NET SDK toocreate een cluster met behulp van dit script gebruiken. Zie voor meer informatie over het gebruik van deze methoden [aanpassen HDInsight-clusters met scriptacties](hdinsight-hadoop-customize-cluster-linux.md).

1. Start met het inrichten van een cluster met behulp van de stappen in Hallo [HDInsight-clusters inrichten op Linux](hdinsight-hadoop-provision-linux-clusters.md), maar inrichting niet voltooid.

2. Op Hallo **optionele configuratie** blade Selecteer **scriptacties**, en geef Hallo volgende informatie:

   * **NAAM**: Voer een beschrijvende naam voor de scriptactie Hallo.

   * **SCRIPT-URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh

   * **HEAD**: Schakel deze optie.

   * **WERKNEMER**: Schakel deze optie.

   * **ZOOKEEPER**: leeg laten.

   * **PARAMETERS**: Hallo WASB adres toohello container en storage-account invoeren dat Hallo potten bevat. Bijvoorbeeld:  **wasb://libs@mystorage.blob.core.windows.net/** .

3. Hallo Hallo onderaan in **scriptacties**, hello gebruiken **Selecteer** knop toosave Hallo configuratie.

4. Op Hallo **optionele configuratie** blade Selecteer **gekoppelde Storage-Accounts** en selecteer Hallo **van een sleutel opslag** koppeling. Selecteer opslagaccount Hallo Hallo potten met en gebruik vervolgens Hallo **Selecteer** knoppen toosave instellingen en return Hallo **optionele configuratie** blade.

5. Gebruik Hallo **Selecteer** knop onderin Hallo Hallo **optionele configuratie** blade toosave Hallo optionele configuratie-informatie.

6. Doorgaan Hallo cluster inrichten, zoals beschreven in [HDInsight-clusters inrichten op Linux](hdinsight-hadoop-provision-linux-clusters.md).

Zodra het maken van clusters is voltooid, u kunt toouse Hallo potten toegevoegd via dit script uit Hive zonder toouse Hallo worden `ADD JAR` instructie.

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over het werken met Hive [Hive gebruiken met HDInsight](hdinsight-use-hive.md)

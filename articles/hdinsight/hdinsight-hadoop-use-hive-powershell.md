---
title: aaaUse Hadoop Hive met PowerShell in HDInsight - Azure | Microsoft Docs
description: Gebruik PowerShell toorun Hive-query's in Hadoop op HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a>Uitvoeren van Hive-query's met behulp van PowerShell
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Dit document bevat een voorbeeld van het gebruik van Azure PowerShell in hello Azure-resourcegroep modus toorun Hive-query's in een Hadoop op HDInsight-cluster.

> [!NOTE]
> Dit document biedt geen een gedetailleerde beschrijving van wat Hallo HiveQL-instructies die worden gebruikt in de voorbeelden Hallo doen. Zie voor informatie over Hallo HiveQL die wordt gebruikt in dit voorbeeld, [Hive gebruiken met Hadoop op HDInsight](hdinsight-use-hive.md).

**Vereisten**

* **Een Azure HDInsight-cluster**: het maakt niet uit of Windows hello cluster of op basis van Linux.

  > [!IMPORTANT]
  > Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* **Een werkstation met Azure PowerShell**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a>Uitvoeren van Hive-query's met Azure PowerShell

Azure PowerShell biedt *cmdlets* waarmee u kunt uitvoeren tooremotely Hive-query's op HDInsight. Intern maakt u Hallo cmdlets REST-aanroepen te[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) op Hallo HDInsight-cluster.

Hallo worden volgende cmdlets gebruikt bij het uitvoeren van Hive-query's in een externe HDInsight-cluster:

* **Add-AzureRmAccount**: Azure PowerShell verifieert tooyour Azure-abonnement
* **Nieuwe AzureRmHDInsightHiveJobDefinition**: maakt een *taak definitie* opgegeven met behulp van Hallo HiveQL-instructies
* **Start AzureRmHDInsightJob**: Hallo taak definitie tooHDInsight verzendt, Hallo taak start en retourneert een *taak* -object dat gebruikt toocheck Hallo status van Hallo-taak worden kan
* **Wacht AzureRmHDInsightJob**: Hallo object toocheck Hallo taakstatus van Hallo taak gebruikt. Wacht totdat het Hallo-taak is voltooid of Hallo wachttijd is overschreden.
* **Get-AzureRmHDInsightJobOutput**: tooretrieve Hallo uitvoer van Hallo taak gebruikt
* **Aanroepen AzureRmHDInsightHiveJob**: toorun HiveQL-instructies gebruikt. Deze cmdlet blokken Hallo-query is voltooid en geeft vervolgens Hallo resultaten
* **Gebruik AzureRmHDInsightCluster**: Sets Hallo huidige cluster toouse voor Hallo **Invoke-AzureRmHDInsightHiveJob** opdracht

Hallo volgende stappen laten zien hoe toouse deze cmdlets toorun een taak in uw HDInsight-cluster:

1. Hallo code als volgt met een editor opslaan **hivejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. Open een nieuw **Azure PowerShell** opdrachtprompt. Locatie van de mappen toohello Hallo wijzigen **hivejob.ps1** bestand en gebruik vervolgens Hallo opdrachtscript toorun hello te volgen:

        .\hivejob.ps1

    Wanneer het Hallo-script wordt uitgevoerd, bent u na vragen aan gebruiker tooenter Hallo cluster naam en het Hallo HTTPS/Admin accountreferenties voor Hallo-cluster. Hebt u mogelijk ook na vragen aan gebruiker toolog in tooyour Azure-abonnement.

3. Wanneer het Hallo-taak is voltooid, wordt informatie vergelijkbare toohello thext te volgen:

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. Zoals eerder gezegd **Invoke-Hive** kan worden gebruikt toorun een query en wachten op antwoord Hallo. Hallo script toosee de werking van Invoke-Hive volgende gebruiken:

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    Hallo-uitvoer ziet er Hallo volgende tekst:

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > Voor meer HiveQL-query's, kunt u hello Azure PowerShell **hier tekenreeksen** cmdlet of HiveQL scriptbestanden. Hallo volgende codefragment bevat hoe toouse hello **Invoke-Hive** cmdlet toorun een scriptbestand HiveQL. Hallo HiveQL scriptbestand moet worden geüpload toowasb: / /.
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > Voor meer informatie over **hier tekenreeksen**, Zie <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">met behulp van Windows PowerShell hier-tekenreeksen</a>.

## <a name="troubleshooting"></a>Problemen oplossen

Als er geen informatie wordt geretourneerd wanneer Hallo-taak is voltooid, is een fout kan zijn opgetreden tijdens de verwerking. Foutgegevens tooview voor deze taak toevoegen na einde toohello Hallo Hallo **hivejob.ps1** bestand, opslaan en vervolgens opnieuw uit te voeren.

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Deze cmdlet retourneert Hallo-informatie die is geschreven tooSTDERR terwijl u Hallo taak werd uitgevoerd op Hallo-server.

## <a name="summary"></a>Samenvatting

Zoals u ziet, Azure PowerShell biedt een eenvoudige manier toorun Hive-query's in een HDInsight-cluster, Hallo monitor status van taken en Hallo uitvoer ophalen.

## <a name="next-steps"></a>Volgende stappen

Voor algemene informatie over Hive in HDInsight:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)

Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:

* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)
* [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md)

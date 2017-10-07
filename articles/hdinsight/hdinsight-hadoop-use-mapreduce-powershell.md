---
title: aaaUse MapReduce en PowerShell gebruiken met Hadoop - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse PowerShell tooremotely MapReduce-taken uitvoeren met Hadoop op HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 59524f0e8813d4c017f92bccb2e50d4c018acf71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a>MapReduce-taken uitvoeren met Hadoop in HDInsight met behulp van PowerShell

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Dit document bevat een voorbeeld van het gebruik van Azure PowerShell toorun een MapReduce-taak in een Hadoop op HDInsight-cluster.

## <a id="prereq"></a>Vereisten

* **Een Azure HDInsight (Hadoop in HDInsight)-cluster**

  > [!IMPORTANT]
  > Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* **Een werkstation met Azure PowerShell**.

## <a id="powershell"></a>Voer een MapReduce-taak met Azure PowerShell

Azure PowerShell biedt *cmdlets* waarmee u kunt uitvoeren tooremotely MapReduce-taken in HDInsight. Intern, dit wordt gerealiseerd met behulp van REST-aanroepen te[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (voorheen Templeton) uitgevoerd op Hallo HDInsight-cluster.

Hallo worden volgende cmdlets gebruikt bij het uitvoeren van MapReduce-taken in een externe HDInsight-cluster.

* **Login-AzureRmAccount**: Azure PowerShell verifieert tooyour Azure-abonnement.

* **Nieuwe AzureRmHDInsightMapReduceJobDefinition**: maakt een nieuw *taak definitie* opgegeven met behulp van Hallo MapReduce-informatie.

* **Start AzureRmHDInsightJob**: Hallo taak definitie tooHDInsight verzendt, Hallo taak start en retourneert een *taak* -object dat gebruikt toocheck Hallo status van Hallo-taak worden kan.

* **Wacht AzureRmHDInsightJob**: Hallo object toocheck Hallo taakstatus van Hallo taak gebruikt. Wacht totdat het Hallo-taak is voltooid of Hallo wachttijd is overschreden.

* **Get-AzureRmHDInsightJobOutput**: tooretrieve Hallo uitvoer van Hallo taak gebruikt.

Hallo volgende stappen laten zien hoe toouse deze cmdlets toorun een taak in uw HDInsight-cluster.

1. Hallo code als volgt met een editor opslaan **mapreducejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. Open een nieuw **Azure PowerShell** opdrachtprompt. Locatie van de mappen toohello Hallo wijzigen **mapreducejob.ps1** bestand en gebruik vervolgens Hallo opdrachtscript toorun hello te volgen:

        .\mapreducejob.ps1

    Wanneer u Hallo script uitvoert, wordt u gevraagd Hallo-naam van Hallo HDInsight-cluster en Hallo HTTPS/Admin-accountnaam en wachtwoord voor Hallo-cluster. Hebt u mogelijk ook na vragen aan gebruiker tooauthenticate tooyour Azure-abonnement.

3. Wanneer het Hallo-taak is voltooid, wordt uitvoer vergelijkbare toohello tekst te volgen:

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    Deze uitvoer geeft aan dat Hallo-taak is voltooid.

    > [!NOTE]
    > Als hello **ExitCode** is een waarde dan 0, Zie [probleemoplossing](#troubleshooting).

    In dit voorbeeld worden ook opgeslagen Hallo gedownloade bestanden tooan **uitvoer.txt** bestand in map Hallo met Hallo-script uit.

### <a name="view-output"></a>Uitvoer weergeven

Open Hallo **uitvoer.txt** bestand in een tekst-editor toosee Hallo woorden en telt geproduceerd door Hallo-taak.

> [!NOTE]
> Hallo uitvoerbestanden van een MapReduce-taak zijn niet-wijzigbaar. Als u dit voorbeeld opnieuw uitvoeren, moet u dus toochange Hallo-naam van het uitvoerbestand Hallo.

## <a id="troubleshooting"></a>Problemen oplossen

Als er geen informatie wordt geretourneerd wanneer Hallo-taak is voltooid, is een fout kan zijn opgetreden tijdens de verwerking. de foutgegevens tooview voor deze taak toevoegen na einde van de opdracht toohello Hallo Hallo **mapreducejob.ps1** bestand, opslaan en vervolgens opnieuw uit te voeren.

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Deze cmdlet retourneert Hallo-informatie die is geschreven tooSTDERR terwijl u Hallo taak werd uitgevoerd op de server Hallo en mogelijk kunt u bepalen waarom de Hallo-taak is mislukt.

## <a id="summary"></a>Samenvatting

Zoals u ziet, Azure PowerShell biedt een eenvoudige manier toorun MapReduce-taken op een HDInsight-cluster, de status van de taak Hallo monitor en ophalen Hallo uitvoer.

## <a id="nextsteps"></a>Volgende stappen

Voor algemene informatie over MapReduce-taken in HDInsight:

* [Gebruik MapReduce op HDInsight Hadoop](hdinsight-use-mapreduce.md)

Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)
* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)

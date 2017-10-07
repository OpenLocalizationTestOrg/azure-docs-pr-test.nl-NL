---
title: aaaUse Pig met PowerShell in HDInsight - Azure Hadoop | Microsoft Docs
description: Meer informatie over hoe toosubmit Pig-taken tooa Hadoop-cluster in HDInsight met Azure PowerShell.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a>Azure PowerShell toorun Pig-taken gebruiken met HDInsight

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Dit document bevat een voorbeeld van het gebruik van Azure PowerShell toosubmit Pig-taken tooa Hadoop op HDInsight-cluster. Pig kunt u toowrite MapReduce-taken met behulp van een andere taal (Pig Latin) modellen gegevenstransformaties, in plaats van toewijzen en functies te beperken.

> [!NOTE]
> Dit document biedt geen een gedetailleerde beschrijving van wat Hallo Pig Latin-instructies gebruikt in de voorbeelden Hallo doen. Zie voor meer informatie over Hallo Pig Latin in dit voorbeeld gebruikt [Pig gebruiken met Hadoop op HDInsight](hdinsight-use-pig.md).

## <a id="prereq"></a>Vereisten

* **Een Azure HDInsight-cluster**

  > [!IMPORTANT]
  > Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* **Een werkstation met Azure PowerShell**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a id="powershell"></a>Pig-taken met behulp van PowerShell uitgevoerd

Azure PowerShell biedt *cmdlets* waarmee u kunt uitvoeren tooremotely Pig-taken in HDInsight. Intern PowerShell REST-aanroepen te gebruikt[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) uitgevoerd op Hallo HDInsight-cluster.

Hallo worden volgende cmdlets gebruikt bij het uitvoeren van Pig-taken op een externe HDInsight-cluster:

* **Login-AzureRmAccount**: Azure PowerShell verifieert tooyour Azure-abonnement
* **Nieuwe AzureRmHDInsightPigJobDefinition**: maakt een *taak definitie* opgegeven met behulp van Hallo Pig Latin-instructies
* **Start AzureRmHDInsightJob**: Hallo taak definitie tooHDInsight verzendt, Hallo taak start en retourneert een *taak* -object dat gebruikt toocheck Hallo status van Hallo-taak worden kan
* **Wacht AzureRmHDInsightJob**: Hallo object toocheck Hallo taakstatus van Hallo taak gebruikt. Wacht totdat het Hallo-taak is voltooid of Hallo wachttijd is overschreden.
* **Get-AzureRmHDInsightJobOutput**: tooretrieve Hallo uitvoer van Hallo taak gebruikt

Hallo volgende stappen laten zien hoe toouse deze cmdlets toorun een taak op uw HDInsight-cluster.

1. Hallo code als volgt met een editor opslaan **pigjob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. Open een nieuw Windows PowerShell-opdrachtprompt. Locatie van de mappen toohello Hallo wijzigen **pigjob.ps1** bestand en gebruik vervolgens Hallo opdrachtscript toorun hello te volgen:

        .\pigjob.ps1

    U bent na vragen aan gebruiker toolog in tooyour Azure-abonnement. Vervolgens wordt u gevraagd om Hallo HTTPs/Admin-accountnaam en wachtwoord voor Hallo HDInsight-cluster.

2. Het moet informatie vergelijkbare toohello tekst volgende retourneren wanneer op Hallo-taak is voltooid:

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="troubleshooting"></a>Problemen oplossen

Als er geen informatie wordt geretourneerd wanneer Hallo-taak is voltooid, is een fout kan zijn opgetreden tijdens de verwerking. de foutgegevens tooview voor deze taak toevoegen na einde van de opdracht toohello Hallo Hallo **pigjob.ps1** bestand, opslaan en vervolgens opnieuw uit te voeren.

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

Dit Hallo-informatie die is geschreven tooSTDERR terwijl u Hallo taak werd uitgevoerd op Hallo-server retourneert en mogelijk kunt u bepalen waarom de Hallo-taak is mislukt.

## <a id="summary"></a>Samenvatting
Zoals u ziet, Azure PowerShell biedt een eenvoudige manier toorun Pig-taken op een HDInsight-cluster, de status van de taak Hallo monitor en ophalen Hallo uitvoer.

## <a id="nextsteps"></a>Volgende stappen
Voor algemene informatie over Pig in HDInsight:

* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)

Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)
* [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md)

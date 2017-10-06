---
title: aaaInstall of Mono op HDInsight - Azure bijwerken | Microsoft Docs
description: Meer informatie over hoe toouse een specifieke versie van Mono met HDInsight-cluster. Mono is gebruikte toorun .NET-toepassingen op Linux gebaseerde HDInsight-clusters.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: hdinsightactive
ms.openlocfilehash: 1e8a8aaeff231c93a9e232379448517b326da965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a>Installeren of bijwerken van Mono in HDInsight

Meer informatie over hoe tooinstall een specifieke versie van [Mono](https://www.mono-project.com) op HDInsight 3.4 of hoger.

Mono op HDInsight 3.4 en hoger is geïnstalleerd en is gebruikte toorun .NET-toepassingen. Zie voor informatie over het Hallo-versie van Mono opgenomen in elke versie van HDInsight, [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md). tooinstall een andere versie op het cluster, gebruik Hallo scriptactie in dit document. 

## <a name="how-it-works"></a>Hoe werkt het?

Dit script accepteert Hallo parameter te volgen:

* __Mono versienummer__: Hallo-versie van Mono tooinstall. Hallo-versie moet beschikbaar zijn vanuit [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).

Hallo script installeert Hallo Mono-pakketten te volgen:

* __Mono-voltooid__

* __CA-certificaten-mono__

## <a name="hello-script"></a>Hallo-script

__Locatie script__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)

__Vereisten__:

* Hallo script moet worden toegepast op Hallo __hoofdknooppunten__ en __worker-knooppunten__.

## <a name="toouse-hello-script"></a>toouse hello script

Voor informatie over hoe toouse dit script met HDInsight, zien Hallo [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document. U kunt gebruiken Hallo script via de hello Azure-portal, Azure PowerShell of Azure CLI Hallo.

Tijdens het volgende script actie document hello, gebruikt u Hallo URI te volgen:

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> Bij het configureren van HDInsight met dit script, markeert u Hallo script als __persistente__. Deze instelling kunt HDInsight tooapply Hallo script tooworker knooppunten die zijn toegevoegd door te schalen van bewerkingen.


## <a name="next-steps"></a>Volgende stappen

U hebt geleerd hoe tooupgrade of een specifieke versie van Mono installeren op HDInsight. Zie voor meer informatie over het gebruik van .NET-toepassingen met Mono op HDInsight Hallo documenten te volgen:

* [.NET gebruiken voor het streamen van MapReduce in HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [.NET met Hive en Pig in HDInsight gebruiken](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [C#-oplossingen met Storm op HDInsight ontwikkelen](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [.NET-oplossingen migreren HDInsight op basis van tooLinux](hdinsight-hadoop-migrate-dotnet-to-linux.md)

Zie voor meer informatie over het gebruik van scriptacties [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md)
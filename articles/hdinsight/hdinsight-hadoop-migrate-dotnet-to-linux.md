---
title: aaaUse .NET met Hadoop MapReduce op Linux gebaseerde HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse .NET-toepassingen voor streaming MapReduce op Linux gebaseerde HDInsight.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a>Migreren van .NET-oplossingen voor HDInsight op basis van Windows HDInsight op basis van tooLinux

Linux gebaseerde HDInsight-clusters gebruik [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET-toepassingen. Mono kunt u toouse .NET onderdelen zoals MapReduce-toepassingen met HDInsight op basis van Linux. In dit document wordt meer informatie over hoe toomigrate .NET oplossingen voor Windows gebaseerde HDInsight-clusters toowork met Mono op Linux gebaseerde HDInsight gemaakt.

## <a name="mono-compatibility-with-net"></a>Mono compatibiliteit met .NET

Mono versie 4.2.1 is opgenomen in HDInsight versie 3.5. Zie voor meer informatie over Hallo-versie van Mono opgenomen met HDInsight [HDInsight onderdeel versies](hdinsight-component-versioning.md). tooinstall een specifieke versie van Mono, Zie Hallo [installeren of update Mono](hdinsight-hadoop-install-mono.md) document.

Zie voor gedetailleerde informatie over de compatibiliteit tussen Mono en .NET Hallo [Mono compatibiliteit (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.

> [!IMPORTANT]
> Hallo SCP.NET framework is compatibel met Mono. Zie voor meer informatie over het gebruik van SCP.NET met Mono [Gebruik Visual Studio toodevelop C#-topologieën voor Apache Storm op HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="automated-portability-analysis"></a>Analyse van geautomatiseerde draagbaarheid

Hallo [.NET draagbaarheid Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) gebruikte toogenerate een rapport van compatibiliteitsproblemen tussen de toepassing en Mono kan zijn. Volgende stappen tooconfigure Hallo analyzer toocheck Hallo uw toepassing voor Mono draagbaarheid gebruiken:

1. Hallo installeren [.NET draagbaarheid Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer). Selecteer Hallo-versie van Visual Studio toouse tijdens de installatie.

2. Selecteer in Visual Studio 2015 __analyseren__ > __draagbaarheid Analyzer instellingen__, en zorg ervoor dat __4.5__ Hallo is ingecheckt __Mono__  sectie.

    ![4.5 Mono sectie voor Hallo analyzer instellingen ingecheckt](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    Selecteer __OK__ toosave Hallo configuratie.

3. Selecteer __analyseren__ > __analyseren Assembly draagbaarheid__. Selecteer Hallo-assembly die uw oplossing bevat, en selecteer vervolgens __Open__ toobegin analyse.

4. Zodra de analyse is voltooid, selecteert u __analyseren__ > __analyserapporten weergeven__. In __draagbaarheid analyseresultaten__, selecteer __rapport openen__ tooopen een rapport.

    ![Draagbaarheid analyzer resultaten dialoogvenster](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> Hallo analyzer kan geen catch elk probleem met uw oplossing. Bijvoorbeeld, een bestandspad van `c:\temp\file.txt` wordt beschouwd als OK omdat Mono wordt uitgevoerd op Windows en Hallo pad ongeldig in deze context is. Hallo-pad is echter niet geldig voor een Linux-platform.

## <a name="manual-portability-analysis"></a>Handmatige draagbaarheid analyse

Voer een handmatige controle van uw code met Hallo informatie in Hallo [toepassing draagbaarheid (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.

## <a name="modify-and-build"></a>Wijzigen en maken

U kunt Visual Studio-toobuild toouse blijven uw .NET-oplossingen voor HDInsight. Echter, moet u ervoor zorgen dat Hallo-project is geconfigureerde toouse .NET Framework 4.5.

## <a name="deploy-and-test"></a>Implementeren en testen

Als u uw oplossing met behulp van Hallo aanbevelingen van Hallo .NET draagbaarheid Analyzer of van een handmatige analyse hebt gewijzigd, moet u het testen met HDInsight. Hallo-oplossing op een Linux gebaseerde HDInsight-cluster te testen, waarschijnlijk subtiele problemen die toobe gecorrigeerd moeten. Het is raadzaam dat u aanvullende logboekregistratie inschakelen in uw toepassing bij het testen.

Zie voor meer informatie over de toegang tot logboeken Hallo documenten te volgen:

* [Toegang tot YARN-toepassingslogboeken in een HDInsight-cluster op basis van Linux](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a>Volgende stappen

* [Gebruik C# met MapReduce in HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [Gebruik van de gebruiker gedefinieerde functies C# met Hive en Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [C#-topologieën ontwikkelen voor Storm op HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md)
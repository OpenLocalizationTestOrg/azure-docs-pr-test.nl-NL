---
title: aaaUpgrade HDInsight-cluster tooa nieuwere versie-Azure | Microsoft Docs
description: Meer informatie over hoe tooUpgrade HDInsight-cluster tooa nieuwere versie.
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a>HDInsight-cluster tooa nieuwere versie upgraden
tootake profiteren van Hallo nieuwste functies van HDInsight, het beste een HDInsight-clusters bijgewerkte toolatest versie. Ga als volgt Hallo hieronder richtlijnen tooupgrade de versies van uw HDInsight-cluster.

> [!NOTE]
> HDInsight-clusters versie 3.2 en 3.3 bijna intrekkingsdatum zijn. Zie voor informatie over de ondersteunde versie van HDInsight, [HDInsight onderdeel versies](hdinsight-component-versioning.md#supported-hdinsight-versions).
>
>

## <a name="upgrade-tasks"></a>Upgradetaken
Hallo werkstroom tooupgrade HDInsight-Cluster is als volgt.

![Werkstroom voor serverupgrades diagram](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. Elke sectie van dit document toounderstand wijzigingen die nodig zijn bij een upgrade van uw HDInsight-cluster lezen.
2. Maak een cluster als een test/quality assurance-omgeving. Zie voor meer informatie over het maken van een cluster [meer informatie over hoe toocreate Linux gebaseerde HDInsight-clusters](hdinsight-hadoop-provision-linux-clusters.md)
3. Kopie bestaande taken, de gegevensbronnen en de sinks toohello nieuwe omgeving. Zie [gegevens kopiëren tooTest omgeving](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) voor meer informatie.
4. Validatie toomake ervoor dat uw taken werken zoals verwacht op het nieuwe cluster Hallo testen uitvoeren.


Zodra u hebt gecontroleerd dat alles werkt zoals verwacht, plant u uitvaltijd voor Hallo-migratie. Tijdens deze uitvaltijd Hallo volgende acties:

1.  Back-up die lokaal zijn opgeslagen op de clusterknooppunten Hallo tijdelijke gegevens. Bijvoorbeeld, als u gegevens hebt opgeslagen rechtstreeks op een hoofdknooppunt.
2.  Hallo bestaande cluster verwijderen.
3.  Een cluster maken in Hallo hetzelfde VNET subnet met de meest recente (of ondersteunde) HDI versie gebruikt dezelfde standaard gegevensopslag die eerder cluster gebruikt Hallo Hallo. Hierdoor Hallo nieuwe cluster toocontinue werken met uw bestaande productiegegevens.
4.  Importeer tijdelijke gegevens die u een back-up.
5.  Start taken/doorgaan met het verwerken met behulp van het nieuwe cluster Hallo.

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over hoe toocreate Linux gebaseerde HDInsight-clusters](hdinsight-hadoop-provision-linux-clusters.md)
* [Verbinding maken via SSH tooHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Beheer op basis van Linux clusters met Ambari](hdinsight-hadoop-manage-ambari.md)


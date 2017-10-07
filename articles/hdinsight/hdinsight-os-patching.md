---
title: toepassing van patches planning voor Linux gebaseerde HDInsight-clusters - Azure aaaConfigure OS | Microsoft Docs
description: Meer informatie over hoe tooconfigure OS patch planning voor Linux gebaseerde HDInsight-clusters.
services: hdinsight
documentationcenter: 
author: bprakash
manager: asadk
editor: bprakash
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: bhanupr
ms.openlocfilehash: 1598d64e594d7e8a68573fc63dd86051a5a9d025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="os-patching-for-hdinsight"></a>OS patches voor HDInsight 
Als een beheerde service voor Hadoop, HDInsight geregeld patchen Hallo OS Hallo onderliggende virtuele machines die worden gebruikt door HDInsight-clusters. Vanaf 1 augustus 2016, hebben we Hallo Gast OS patch beleid voor Linux gebaseerde HDInsight-clusters (versie 3.4 of hoger) gewijzigd. Hallo-doel van het nieuwe beleid Hallo is toosignificantly Verminder het aantal herstarts Hallo vanwege toopatching. Nieuw beleid Hallo blijven toopatch virtuele machines (VM's) op Linux-clusters elke maandag of donderdag begint bij 12: 00 A.M. UTC op een wijze gespreid over de knooppunten in een opgegeven cluster. Een bepaalde virtuele machine wordt echter alleen maximaal één keer elke 30 dagen vanwege tooguest OS patches opnieuw. Bovendien Hallo eerste keer opnieuw opstarten voor een nieuw cluster gebeurt niet eerder zijn dan 30 dagen na de aanmaakdatum Hallo-cluster. Patches worden van kracht zodra Hallo virtuele machines opnieuw worden opgestart.

## <a name="how-tooconfigure-hello-os-patching-schedule-for-linux-based-hdinsight-clusters"></a>Hoe tooconfigure Hallo OS patch planning voor Linux gebaseerde HDInsight-clusters
Hallo virtuele machines in een HDInsight-cluster moet toobe af en toe opnieuw opgestart zodat belangrijke beveiligingspatches kunnen worden geïnstalleerd. Vanaf 1 augustus 2016 krijgen nieuwe Linux gebaseerde HDInsight-clusters (versie 3.4 of hoger) opnieuw opgestart met Hallo schema te volgen:

1. Een virtuele machine in de cluster Hallo kunnen alleen opnieuw opstarten patches voor maximaal één keer binnen een periode van 30 dagen.
2. Hallo opnieuw worden opgestart, gebeurt beginnen bij 12: 00 A.M. UTC.
3. Hallo opnieuw opstarten proces is gespreid over virtuele machines in de cluster hello, dus Hallo cluster nog steeds beschikbaar tijdens Hallo opnieuw opstarten is.
4. Hallo eerste keer opnieuw opstarten voor een nieuw cluster gebeurt niet eerder zijn dan 30 dagen na de aanmaakdatum Hallo-cluster.

Hallo scriptactie die wordt beschreven in dit artikel gebruikt, kunt u wijzigen Hallo OS patch planning als volgt:
1. In- of uitschakelen van automatische opnieuw wordt opgestart
2. Set Hallo frequentie van opnieuw wordt opgestart (in dagen tussen opnieuw is opgestart)
3. Hallo dag Hallo weekdag opnieuw instellen

> [!NOTE]
> Deze scriptactie werkt alleen met Linux gebaseerde HDInsight-clusters die zijn gemaakt na 1e augustus 2016. Patches worden van kracht wanneer virtuele machines opnieuw worden opgestart. 
>

## <a name="how-toouse-hello-script"></a>Hoe toouse script Hallo 

Met dit script vereist wanneer Hallo volgende informatie:
1. Hallo scriptlocatie: https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh.  HDInsight gebruikt deze URI toofind en Hallo-script uitvoeren op alle Hallo virtuele machines in Hallo-cluster.
  
2. knooppunt clustertypen waarmee Hallo script wordt toegepast op Hallo: headnode, workernode, zookeeper. Dit script moet toegepaste tooall knooppunttypen in Hallo-cluster. Als u is geen toegepaste tooa knooppunttype en Hallo virtuele voortgezet machines voor dat knooppunttype toouse Hallo vorige patch planning.


3.  Parameter: Dit script accepteert drie numerieke parameters:

    | Parameter | Definitie |
    | --- | --- |
    | Automatisch opnieuw wordt opgestart in-of uitschakelen |0 of 1. De waarde 0 wordt automatisch opnieuw wordt opgestart uitgeschakeld terwijl 1 automatisch opnieuw wordt opgestart schakelt. |
    | Frequentie |7 too90 (inclusief). Hallo aantal dagen toowait voordat opnieuw wordt opgestart nadat Hallo virtuele machines voor patches waarvoor opnieuw opstarten. |
    | Dag van week |1 too7 (inclusief). Een waarde van 1 betekent Hallo opnieuw moet worden uitgevoerd op een maandag en 7 betekent een Sunday.For bijvoorbeeld met behulp van parameters van 1 60 2 resulteert in het automatisch opnieuw wordt opgestart elke 60 dagen (maximaal) op dinsdag. |
    | Persistentie |Wanneer u een bestaand cluster voor script actie tooan toepast, kunt u Hallo script als persistent markeren. Persistente scripts worden toegepast wanneer nieuwe workernodes toohello cluster door te schalen bewerkingen worden toegevoegd. |

> [!NOTE]
> U moet dit script markeren als bij het toepassen van het bestaande cluster tooan persistent. Een nieuwe knooppunten die zijn gemaakt door te schalen operations Gebruik anders Hallo standaard patchen planning.
Als u Hallo script als onderdeel van het proces voor het maken van cluster Hallo toepast, wordt deze automatisch bewaard.
>

## <a name="next-steps"></a>Volgende stappen

Voor specifieke stappen over het gebruik van de scriptactie hello, raadpleegt u uit te voeren in Hallo Hallo [Linuz aanpassen op basis van een HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md):

* [Gebruik de scriptactie van een tijdens het maken van het cluster](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)
* [Toepassen van een script actie tooa met cluster](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)

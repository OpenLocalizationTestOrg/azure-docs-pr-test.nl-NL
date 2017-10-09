---
title: aaaHow toodelete een HDInsight-cluster - Azure | Microsoft Docs
description: Informatie over de Hallo verschillende manieren waarop u een HDInsight-cluster kunt verwijderen.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 5b9d9a09eecfdcfaed7a1f5ebab440e13bd358b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a>Een HDInsight-cluster met behulp van uw browser, PowerShell of Azure CLI Hallo verwijderen

HDInsight-cluster omdat facturering begint zodra een cluster wordt gemaakt en stopt wanneer het Hallo-cluster is verwijderd. Facturering is pro rato per minuut, dus u uw cluster altijd verwijderen moet wanneer deze niet langer in gebruik. In dit document leert u hoe een cluster met toodelete hello Azure-portal, Azure PowerShell en hello Azure CLI 1.0.

> [!IMPORTANT]
> Verwijderen van een HDInsight-cluster hello Azure Storage-accounts niet verwijderen of Data Lake Store Hallo cluster gekoppeld. U kunt de gegevens die zijn opgeslagen in deze services in toekomstige Hallo hergebruiken.

## <a name="azure-portal"></a>Azure Portal

1. Meld u bij toohello [Azure-portal](https://portal.azure.com) en selecteer uw HDInsight-cluster. Als uw HDInsight-cluster niet vastgemaakt toohello dashboard is, kunt u voor het zoeken op naam met Hallo zoekveld opgegeven.
   
    ![Portal zoeken](./media/hdinsight-delete-cluster/navbar.png)

2. Eenmaal Hallo blade wordt geopend voor Hallo-cluster, selecteert u Hallo **verwijderen** pictogram. Wanneer u wordt gevraagd, selecteert u **Ja** toodelete Hallo-cluster.
   
    ![Pictogram verwijderen](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a>Azure PowerShell

Gebruik van een PowerShell-prompt Hallo opdracht toodelete Hallo cluster te volgen:

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

Vervang **CLUSTERNAME** met Hallo-naam van uw HDInsight-cluster.

## <a name="azure-cli-10"></a>Azure CLI 1.0

Gebruik vanaf een opdrachtprompt Hallo toodelete Hallo cluster te volgen:

    azure hdinsight cluster delete CLUSTERNAME

Vervang **CLUSTERNAME** met Hallo-naam van uw HDInsight-cluster.

> [!NOTE]
> Azure CLI 2.0 ondersteunt geen verwijderen HDInsight-clusters op dit moment (31 juli 2017).
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
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a><span data-ttu-id="5f9ba-103">Een HDInsight-cluster met behulp van uw browser, PowerShell of Azure CLI Hallo verwijderen</span><span class="sxs-lookup"><span data-stu-id="5f9ba-103">Delete an HDInsight cluster using your browser, PowerShell, or hello Azure CLI</span></span>

<span data-ttu-id="5f9ba-104">HDInsight-cluster omdat facturering begint zodra een cluster wordt gemaakt en stopt wanneer het Hallo-cluster is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5f9ba-104">HDInsight cluster billing starts once a cluster is created and stops when hello cluster is deleted.</span></span> <span data-ttu-id="5f9ba-105">Facturering is pro rato per minuut, dus u uw cluster altijd verwijderen moet wanneer deze niet langer in gebruik.</span><span class="sxs-lookup"><span data-stu-id="5f9ba-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="5f9ba-106">In dit document leert u hoe een cluster met toodelete hello Azure-portal, Azure PowerShell en hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="5f9ba-106">In this document, you learn how toodelete a cluster using hello Azure portal, Azure PowerShell, and hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f9ba-107">Verwijderen van een HDInsight-cluster hello Azure Storage-accounts niet verwijderen of Data Lake Store Hallo cluster gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="5f9ba-107">Deleting an HDInsight cluster does not delete hello Azure Storage accounts or Data Lake Store associated with hello cluster.</span></span> <span data-ttu-id="5f9ba-108">U kunt de gegevens die zijn opgeslagen in deze services in toekomstige Hallo hergebruiken.</span><span class="sxs-lookup"><span data-stu-id="5f9ba-108">You can reuse data stored in those services in hello future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="5f9ba-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5f9ba-109">Azure portal</span></span>

1. <span data-ttu-id="5f9ba-110">Meld u bij toohello [Azure-portal](https://portal.azure.com) en selecteer uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="5f9ba-110">Log in toohello [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="5f9ba-111">Als uw HDInsight-cluster niet vastgemaakt toohello dashboard is, kunt u voor het zoeken op naam met Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5f9ba-111">If your HDInsight cluster is not pinned toohello dashboard, you can search for it by name using hello search field.</span></span>
   
    ![Portal zoeken](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="5f9ba-113">Eenmaal Hallo blade wordt geopend voor Hallo-cluster, selecteert u Hallo **verwijderen** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5f9ba-113">Once hello blade opens for hello cluster, select hello **Delete** icon.</span></span> <span data-ttu-id="5f9ba-114">Wanneer u wordt gevraagd, selecteert u **Ja** toodelete Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="5f9ba-114">When prompted, select **Yes** toodelete hello cluster.</span></span>
   
    ![Pictogram verwijderen](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="5f9ba-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f9ba-116">Azure PowerShell</span></span>

<span data-ttu-id="5f9ba-117">Gebruik van een PowerShell-prompt Hallo opdracht toodelete Hallo cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="5f9ba-117">From a PowerShell prompt, use hello following command toodelete hello cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="5f9ba-118">Vervang **CLUSTERNAME** met Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="5f9ba-118">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="5f9ba-119">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5f9ba-119">Azure CLI 1.0</span></span>

<span data-ttu-id="5f9ba-120">Gebruik vanaf een opdrachtprompt Hallo toodelete Hallo cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="5f9ba-120">From a prompt, use hello following toodelete hello cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="5f9ba-121">Vervang **CLUSTERNAME** met Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="5f9ba-121">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="5f9ba-122">Azure CLI 2.0 ondersteunt geen verwijderen HDInsight-clusters op dit moment (31 juli 2017).</span><span class="sxs-lookup"><span data-stu-id="5f9ba-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (July 31, 2017).</span></span>
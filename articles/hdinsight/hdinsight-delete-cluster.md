---
title: Het verwijderen van een HDInsight-cluster - Azure | Microsoft Docs
description: Informatie over de verschillende manieren waarop u een HDInsight-cluster kunt verwijderen.
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
ms.openlocfilehash: 65dac529df15d2dd43eec17673d82a2832f7692e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-the-azure-cli"></a><span data-ttu-id="b4a76-103">Verwijderen van een HDInsight-cluster met behulp van uw browser, PowerShell of Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b4a76-103">Delete an HDInsight cluster using your browser, PowerShell, or the Azure CLI</span></span>

<span data-ttu-id="b4a76-104">HDInsight-cluster omdat facturering begint zodra een cluster wordt gemaakt en stopt wanneer het cluster wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b4a76-104">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span></span> <span data-ttu-id="b4a76-105">Facturering is pro rato per minuut, dus u uw cluster altijd verwijderen moet wanneer deze niet langer in gebruik.</span><span class="sxs-lookup"><span data-stu-id="b4a76-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="b4a76-106">In dit document, informatie over het verwijderen van een cluster met behulp van de Azure-portal, Azure PowerShell en de Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="b4a76-106">In this document, you learn how to delete a cluster using the Azure portal, Azure PowerShell, and the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4a76-107">Verwijderen van een HDInsight-cluster, wordt de Azure Storage-accounts niet verwijderd of de Data Lake Store die zijn gekoppeld aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="b4a76-107">Deleting an HDInsight cluster does not delete the Azure Storage accounts or Data Lake Store associated with the cluster.</span></span> <span data-ttu-id="b4a76-108">U kunt gegevens die zijn opgeslagen in deze services in de toekomst opnieuw gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b4a76-108">You can reuse data stored in those services in the future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="b4a76-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b4a76-109">Azure portal</span></span>

1. <span data-ttu-id="b4a76-110">Meld u aan bij de [Azure-portal](https://portal.azure.com) en selecteer uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b4a76-110">Log in to the [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="b4a76-111">Als uw HDInsight-cluster niet aan het dashboard vastgemaakt is, kunt u voor het zoeken op naam met het zoekveld.</span><span class="sxs-lookup"><span data-stu-id="b4a76-111">If your HDInsight cluster is not pinned to the dashboard, you can search for it by name using the search field.</span></span>
   
    ![Portal zoeken](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="b4a76-113">Zodra de blade wordt geopend voor het cluster, selecteert u de **verwijderen** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b4a76-113">Once the blade opens for the cluster, select the **Delete** icon.</span></span> <span data-ttu-id="b4a76-114">Wanneer u wordt gevraagd, selecteert u **Ja** verwijderen van het cluster.</span><span class="sxs-lookup"><span data-stu-id="b4a76-114">When prompted, select **Yes** to delete the cluster.</span></span>
   
    ![Pictogram verwijderen](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="b4a76-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4a76-116">Azure PowerShell</span></span>

<span data-ttu-id="b4a76-117">Gebruik de volgende opdracht het cluster verwijderen uit een PowerShell-prompt:</span><span class="sxs-lookup"><span data-stu-id="b4a76-117">From a PowerShell prompt, use the following command to delete the cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="b4a76-118">Vervang **CLUSTERNAME** door de naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b4a76-118">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="b4a76-119">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b4a76-119">Azure CLI 1.0</span></span>

<span data-ttu-id="b4a76-120">Gebruik de volgende het cluster verwijderen uit de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="b4a76-120">From a prompt, use the following to delete the cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="b4a76-121">Vervang **CLUSTERNAME** door de naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b4a76-121">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="b4a76-122">Azure CLI 2.0 ondersteunt geen verwijderen HDInsight-clusters op dit moment (31 juli 2017).</span><span class="sxs-lookup"><span data-stu-id="b4a76-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (July 31, 2017).</span></span>
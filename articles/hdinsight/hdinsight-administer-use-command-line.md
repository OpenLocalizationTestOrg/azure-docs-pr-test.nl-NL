---
title: aaaManage Hadoop-clusters met Azure CLI - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure-opdrachtregelinterface toomanage Hadoop-clusters in Azure HDInsight. Hello Azure CLI werkt op Windows, Mac en Linux.
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 03b0cff9331c1c581095b80cc6d1177d843ffa83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a><span data-ttu-id="d7669-104">Hadoop-clusters in HDInsight met behulp van Azure CLI Hallo beheren</span><span class="sxs-lookup"><span data-stu-id="d7669-104">Manage Hadoop clusters in HDInsight using hello Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="d7669-105">Meer informatie over hoe toouse hello [Azure-opdrachtregelinterface](../cli-install-nodejs.md) toomanage Hadoop-clusters in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d7669-105">Learn how toouse hello [Azure Command-line Interface](../cli-install-nodejs.md) toomanage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="d7669-106">Hello Azure CLI is geïmplementeerd in Node.js.</span><span class="sxs-lookup"><span data-stu-id="d7669-106">hello Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="d7669-107">en kan worden gebruikt op elk platform dat ondersteuning biedt voor Node.js, zoals Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="d7669-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="d7669-108">Dit artikel behandelt alleen hello Azure CLI gebruiken met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d7669-108">This article covers only using hello Azure CLI with HDInsight.</span></span> <span data-ttu-id="d7669-109">Voor algemene richtlijnen over het toouse Azure CLI, Zie [installeren en configureren van Azure CLI][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="d7669-109">For a general guide on how toouse Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="d7669-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d7669-110">Prerequisites</span></span>
<span data-ttu-id="d7669-111">Voordat u dit artikel, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="d7669-111">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="d7669-112">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="d7669-112">**An Azure subscription**.</span></span> <span data-ttu-id="d7669-113">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d7669-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="d7669-114">**Azure CLI** -Zie [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) voor installatie en configuratie-informatie.</span><span class="sxs-lookup"><span data-stu-id="d7669-114">**Azure CLI** - See [Install and configure hello Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="d7669-115">**Verbinding maken met tooAzure**met Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d7669-115">**Connect tooAzure**, using hello following command:</span></span>
  
        azure login
  
    <span data-ttu-id="d7669-116">Zie voor meer informatie over verificatie met een werk- of schoolaccount [tooan Azure-abonnement verbinden van hello Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="d7669-116">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="d7669-117">**Modus van Azure Resource Manager toohello switch**met Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d7669-117">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="d7669-118">tooget hulp nodig hebt, gebruik Hallo **-h** overschakelen.</span><span class="sxs-lookup"><span data-stu-id="d7669-118">tooget help, use hello **-h** switch.</span></span>  <span data-ttu-id="d7669-119">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d7669-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a><span data-ttu-id="d7669-120">Maken van clusters met Hallo CLI</span><span class="sxs-lookup"><span data-stu-id="d7669-120">Create clusters with hello CLI</span></span>
<span data-ttu-id="d7669-121">Zie [clusters maken in HDInsight met behulp van Azure CLI Hallo](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d7669-121">See [Create clusters in HDInsight using hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="d7669-122">Een lijst en clusterdetails weergeven</span><span class="sxs-lookup"><span data-stu-id="d7669-122">List and show cluster details</span></span>
<span data-ttu-id="d7669-123">Gebruik Hallo opdrachten toolist te volgen en clusterdetails weergeven:</span><span class="sxs-lookup"><span data-stu-id="d7669-123">Use hello following commands toolist and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="d7669-124">![Opdrachtregelprogramma weergave van de lijst met clusters][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="d7669-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="d7669-125">Clusters verwijderen</span><span class="sxs-lookup"><span data-stu-id="d7669-125">Delete clusters</span></span>
<span data-ttu-id="d7669-126">Gebruik Hallo opdracht toodelete een cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="d7669-126">Use hello following command toodelete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="d7669-127">U kunt ook een cluster verwijderen door het verwijderen van resourcegroep Hallo die Hallo cluster bevat.</span><span class="sxs-lookup"><span data-stu-id="d7669-127">You can also delete a cluster by deleting hello resource group that contains hello cluster.</span></span> <span data-ttu-id="d7669-128">Let op: Hiermee verwijdert u alle Hallo bronnen in Hallo-groep met inbegrip van Hallo storage-standaardaccount.</span><span class="sxs-lookup"><span data-stu-id="d7669-128">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="d7669-129">Clusters schalen</span><span class="sxs-lookup"><span data-stu-id="d7669-129">Scale clusters</span></span>
<span data-ttu-id="d7669-130">toochange hello Hadoop clustergrootte:</span><span class="sxs-lookup"><span data-stu-id="d7669-130">toochange hello Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="d7669-131">HTTP-toegang voor een cluster in-of uitschakelen</span><span class="sxs-lookup"><span data-stu-id="d7669-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="d7669-132">RDP-toegang voor een cluster in-of uitschakelen</span><span class="sxs-lookup"><span data-stu-id="d7669-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="d7669-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d7669-133">Next steps</span></span>
<span data-ttu-id="d7669-134">In dit artikel hebt u geleerd hoe tooperform verschillende HDInsight-cluster beheertaken.</span><span class="sxs-lookup"><span data-stu-id="d7669-134">In this article, you have learned how tooperform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="d7669-135">toolearn Zie meer Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d7669-135">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="d7669-136">[HDInsight beheren met behulp van hello Azure Portal][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="d7669-136">[Administer HDInsight by using hello Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="d7669-137">[HDInsight met behulp van Azure PowerShell beheren][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="d7669-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="d7669-138">[Aan de slag met Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="d7669-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="d7669-139">[Hoe toouse hello Azure CLI][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="d7669-139">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "Lijst en clusters weer te geven"

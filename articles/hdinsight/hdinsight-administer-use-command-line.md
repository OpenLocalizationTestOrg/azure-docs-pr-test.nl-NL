---
title: Met Azure CLI - Azure HDInsight Hadoop-clusters beheren | Microsoft Docs
description: Informatie over het gebruiken van de Azure-opdrachtregelinterface voor het beheren van Hadoop-clusters in Azure HDInsight. De Azure CLI werkt op Windows, Mac en Linux.
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
ms.openlocfilehash: 0ee9f2f28978b207dcaf8f77950bd82a897d3fd1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-the-azure-cli"></a><span data-ttu-id="c7e18-104">Hadoop-clusters in HDInsight met behulp van de Azure CLI beheren</span><span class="sxs-lookup"><span data-stu-id="c7e18-104">Manage Hadoop clusters in HDInsight using the Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="c7e18-105">Meer informatie over het gebruik van de [Azure-opdrachtregelinterface](../cli-install-nodejs.md) voor het beheren van Hadoop-clusters in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7e18-105">Learn how to use the [Azure Command-line Interface](../cli-install-nodejs.md) to manage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="c7e18-106">De Azure CLI is geïmplementeerd in Node.js</span><span class="sxs-lookup"><span data-stu-id="c7e18-106">The Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="c7e18-107">en kan worden gebruikt op elk platform dat ondersteuning biedt voor Node.js, zoals Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="c7e18-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="c7e18-108">In dit artikel behandelt alleen het gebruik van de Azure CLI met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7e18-108">This article covers only using the Azure CLI with HDInsight.</span></span> <span data-ttu-id="c7e18-109">Zie voor een algemene richtlijnen over het gebruik van Azure CLI [installeren en configureren van Azure CLI][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="c7e18-109">For a general guide on how to use Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="c7e18-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c7e18-110">Prerequisites</span></span>
<span data-ttu-id="c7e18-111">Voordat u dit artikel gaat lezen, moet u beschikken over het volgende:</span><span class="sxs-lookup"><span data-stu-id="c7e18-111">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="c7e18-112">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="c7e18-112">**An Azure subscription**.</span></span> <span data-ttu-id="c7e18-113">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="c7e18-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="c7e18-114">**Azure CLI**: zie [De Azure CLI installeren en configureren](../cli-install-nodejs.md) voor informatie over de installatie en configuratie.</span><span class="sxs-lookup"><span data-stu-id="c7e18-114">**Azure CLI** - See [Install and configure the Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="c7e18-115">**Verbinding maken met Azure**, met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c7e18-115">**Connect to Azure**, using the following command:</span></span>
  
        azure login
  
    <span data-ttu-id="c7e18-116">Zie [Verbinding maken met een Azure-abonnement met Azure CLI](../xplat-cli-connect.md) voor meer informatie over verificatie met een werk- of schoolaccount.</span><span class="sxs-lookup"><span data-stu-id="c7e18-116">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="c7e18-117">**Overschakelen naar de modus Azure Resource Manager** met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c7e18-117">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="c7e18-118">Als u help, gebruikt de **-h** overschakelen.</span><span class="sxs-lookup"><span data-stu-id="c7e18-118">To get help, use the **-h** switch.</span></span>  <span data-ttu-id="c7e18-119">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c7e18-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-the-cli"></a><span data-ttu-id="c7e18-120">Clusters maken met de CLI</span><span class="sxs-lookup"><span data-stu-id="c7e18-120">Create clusters with the CLI</span></span>
<span data-ttu-id="c7e18-121">Zie [clusters maken in HDInsight met behulp van de Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c7e18-121">See [Create clusters in HDInsight using the Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="c7e18-122">Een lijst en clusterdetails weergeven</span><span class="sxs-lookup"><span data-stu-id="c7e18-122">List and show cluster details</span></span>
<span data-ttu-id="c7e18-123">Gebruik de volgende opdrachten te kunnen aanbieden en clusterdetails weergeven:</span><span class="sxs-lookup"><span data-stu-id="c7e18-123">Use the following commands to list and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="c7e18-124">![Opdrachtregelprogramma weergave van de lijst met clusters][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="c7e18-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="c7e18-125">Clusters verwijderen</span><span class="sxs-lookup"><span data-stu-id="c7e18-125">Delete clusters</span></span>
<span data-ttu-id="c7e18-126">Gebruik de volgende opdracht om te verwijderen van een cluster:</span><span class="sxs-lookup"><span data-stu-id="c7e18-126">Use the following command to delete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="c7e18-127">U kunt ook een cluster verwijderen door de resourcegroep waarin het cluster te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c7e18-127">You can also delete a cluster by deleting the resource group that contains the cluster.</span></span> <span data-ttu-id="c7e18-128">Let op: Hiermee verwijdert u alle resources in de groep met inbegrip van het standaardopslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c7e18-128">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="c7e18-129">Clusters schalen</span><span class="sxs-lookup"><span data-stu-id="c7e18-129">Scale clusters</span></span>
<span data-ttu-id="c7e18-130">De grootte van Hadoop-cluster wijzigen:</span><span class="sxs-lookup"><span data-stu-id="c7e18-130">To change the Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="c7e18-131">HTTP-toegang voor een cluster in-of uitschakelen</span><span class="sxs-lookup"><span data-stu-id="c7e18-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="c7e18-132">RDP-toegang voor een cluster in-of uitschakelen</span><span class="sxs-lookup"><span data-stu-id="c7e18-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="c7e18-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c7e18-133">Next steps</span></span>
<span data-ttu-id="c7e18-134">In dit artikel hebt u geleerd hoe verschillende HDInsight-cluster administratieve taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c7e18-134">In this article, you have learned how to perform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="c7e18-135">Zie voor meer informatie de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="c7e18-135">To learn more, see the following articles:</span></span>

* <span data-ttu-id="c7e18-136">[HDInsight beheren met behulp van de Azure Portal][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="c7e18-136">[Administer HDInsight by using the Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="c7e18-137">[HDInsight met behulp van Azure PowerShell beheren][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="c7e18-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="c7e18-138">[Aan de slag met Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="c7e18-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="c7e18-139">[Het gebruik van de Azure CLI][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="c7e18-139">[How to use the Azure CLI][azure-command-line-tools]</span></span>

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

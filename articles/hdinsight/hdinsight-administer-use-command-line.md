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
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a>Hadoop-clusters in HDInsight met behulp van Azure CLI Hallo beheren
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Meer informatie over hoe toouse hello [Azure-opdrachtregelinterface](../cli-install-nodejs.md) toomanage Hadoop-clusters in Azure HDInsight. Hello Azure CLI is geïmplementeerd in Node.js. en kan worden gebruikt op elk platform dat ondersteuning biedt voor Node.js, zoals Windows, Mac en Linux.

Dit artikel behandelt alleen hello Azure CLI gebruiken met HDInsight. Voor algemene richtlijnen over het toouse Azure CLI, Zie [installeren en configureren van Azure CLI][azure-command-line-tools].

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a>Vereisten
Voordat u dit artikel, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Azure CLI** -Zie [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) voor installatie en configuratie-informatie.
* **Verbinding maken met tooAzure**met Hallo volgende opdracht:
  
        azure login
  
    Zie voor meer informatie over verificatie met een werk- of schoolaccount [tooan Azure-abonnement verbinden van hello Azure CLI](../xplat-cli-connect.md).
* **Modus van Azure Resource Manager toohello switch**met Hallo volgende opdracht:
  
        azure config mode arm

tooget hulp nodig hebt, gebruik Hallo **-h** overschakelen.  Bijvoorbeeld:

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a>Maken van clusters met Hallo CLI
Zie [clusters maken in HDInsight met behulp van Azure CLI Hallo](hdinsight-hadoop-create-linux-clusters-azure-cli.md).

## <a name="list-and-show-cluster-details"></a>Een lijst en clusterdetails weergeven
Gebruik Hallo opdrachten toolist te volgen en clusterdetails weergeven:

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

![Opdrachtregelprogramma weergave van de lijst met clusters][image-cli-clusterlisting]

## <a name="delete-clusters"></a>Clusters verwijderen
Gebruik Hallo opdracht toodelete een cluster te volgen:

    azure hdinsight cluster delete <Cluster Name>

U kunt ook een cluster verwijderen door het verwijderen van resourcegroep Hallo die Hallo cluster bevat. Let op: Hiermee verwijdert u alle Hallo bronnen in Hallo-groep met inbegrip van Hallo storage-standaardaccount.

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a>Clusters schalen
toochange hello Hadoop clustergrootte:

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a>HTTP-toegang voor een cluster in-of uitschakelen
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a>RDP-toegang voor een cluster in-of uitschakelen
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe tooperform verschillende HDInsight-cluster beheertaken. toolearn Zie meer Hallo artikelen te volgen:

* [HDInsight beheren met behulp van hello Azure Portal][hdinsight-admin-portal]
* [HDInsight met behulp van Azure PowerShell beheren][hdinsight-admin-powershell]
* [Aan de slag met Azure HDInsight][hdinsight-get-started]
* [Hoe toouse hello Azure CLI][azure-command-line-tools]

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

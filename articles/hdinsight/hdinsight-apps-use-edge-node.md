---
title: aaaUse leeg edge-knooppunten op Hadoop-clusters in HDInsight - Azure | Microsoft Docs
description: Hoe een leeg edge-knooppunt tooan HDInsight tooadd cluster kunnen worden gebruikt als een client, en vervolgens test/host uw HDInsight-toepassingen.
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: 9c910905b51f2fe92e6e5d47d86a32bd5247c2cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a>Lege edge-knooppunten op Hadoop-clusters in HDInsight gebruiken

Meer informatie over hoe een lege tooadd edge-knooppunt tooan HDInsight-cluster. Een leeg edge-knooppunt is een virtuele Linux-machine met Hallo hulpprogramma's voor dezelfde client geïnstalleerd en geconfigureerd zoals headnodes hello in maar met geen Hadoop-services die worden uitgevoerd. U kunt Hallo edge-knooppunt gebruiken voor toegang tot cluster hello, testen van uw clienttoepassingen en die als host fungeert voor uw clienttoepassingen. 

U kunt een leeg edge-knooppunt tooan bestaand HDInsight-cluster, het nieuwe cluster tooa toevoegen wanneer u Hallo-cluster maakt. Toevoegen van een leeg edge-knooppunt wordt uitgevoerd met behulp van Azure Resource Manager-sjabloon.  Hallo volgende voorbeeld laat zien hoe deze wordt uitgevoerd met behulp van een sjabloon:

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

Zoals u in het Hallo-voorbeeld, kunt u eventueel aanroepen een [script actie](hdinsight-hadoop-customize-cluster-linux.md) tooperform aanvullende configuratiestappen, zoals het installeren van [Apache Hue](hdinsight-hadoop-hue-linux.md) in Hallo edge-knooppunt. Hallo script actiescript moet openbaar toegankelijk zijn op Hallo web.  Bijvoorbeeld, als het Hallo-script wordt opgeslagen in Azure storage, gebruiken openbare containers of openbare blobs.

Hallo rand knooppuntgrootte virtuele machine moet voldoen aan Hallo HDInsight-cluster worker knooppunt vm vereiste grootte. Zie voor Hallo worker knooppunt vm-grootten aanbevolen, [maken Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).

Nadat u een edge-knooppunt hebt gemaakt, kunt u toohello edge-knooppunt via SSH verbinding en het uitvoeren van de client extra tooaccess hello Hadoop-cluster in HDInsight.

> [!WARNING] 
> Gebruik een lege edge-knooppunt met HDInsight is momenteel in preview. Aangepaste onderdelen die zijn geïnstalleerd op de edge-knooppunt Hallo ontvangt binnen commercieel redelijke ondersteuning van Microsoft. Dit kan leiden bij het oplossen van problemen die kunnen optreden. Of u resources waarnaar wordt verwezen toocommunity voor verdere ondersteuning. Hallo Hieronder volgen enkele Hallo meeste actieve sites voor het ophalen van help van Hallo-community:
>
> * [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * [http://stackoverflow.com](http://stackoverflow.com).
>
> Als u een Apache-technologie gebruikt, hebt u mogelijk hulp kunnen toofind via Hallo Apache projectsites op [http://apache.org](http://apache.org), zoals Hallo [Hadoop](http://hadoop.apache.org/) site.

## <a name="add-an-edge-node-tooan-existing-cluster"></a>Toevoegen van een edge-knooppunt tooan bestaand cluster
In deze sectie gebruikt u een Resource Manager-sjabloon tooadd een edge-knooppunt tooan bestaande HDInsight-cluster.  Hallo Resource Manager-sjabloon kunt u vinden in [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/). Hallo Resource Manager-sjabloon roept een scriptactie zich bevindt op https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. Hallo-script heeft geen acties uitvoeren.  Het is toodemonstrate scriptactie aanroept vanuit een Resource Manager-sjabloon.

**een bestaand cluster voor leeg edge-knooppunt tooan tooadd**

1. Een HDInsight-cluster maken als u nog niet hebt.  Zie [Hadoop-zelfstudie: aan de slag met Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).
2. Klik op Hallo installatiekopie toosign in tooAzure en open hello Azure Resource Manager-sjabloon in hello Azure-portal. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Configureer Hallo volgende eigenschappen:
   
   * **Abonnement**: Selecteer een Azure-abonnement gebruikt voor het Hallo-cluster maken.
   * **Resourcegroep**: Selecteer Hallo resourcegroep gebruikt voor Hallo bestaand HDInsight-cluster.
   * **Locatie**: Selecteer Hallo-locatie van Hallo bestaand HDInsight-cluster.
   * **Clusternaam**: Voer Hallo-naam van een bestaand HDInsight-cluster.
   * **Edge-Knooppuntgrootte**: Selecteer een van de VM-grootten Hallo. Hallo vm-grootte moet voldoen aan de vereisten voor Hallo worker knooppunt vm-grootte. Zie voor Hallo worker knooppunt vm-grootten aanbevolen, [maken Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).
   * **Edge-knooppunt voorvoegsel**: Hallo standaardwaarde is **nieuwe**.  Naam Hallo edge-knooppunt is met de Hallo-standaardwaarde, **nieuwe edgenode**.  Hallo-voorvoegsel van het Hallo-portal, kunt u aanpassen. U kunt ook de volledige naam van de sjabloon Hallo Hallo aanpassen.

4. Controleer **ik ga akkoord toohello voorwaarden bovengenoemde**, en klik vervolgens op **aankoop** toocreate Hallo edge-knooppunt.

>[!IMPORTANT]
> Zorg ervoor dat tooselect hello Azure-resourcegroep voor Hallo bestaand HDInsight-cluster.  Anders krijgt u Hallo fout bericht 'kan aangevraagde bewerking op geneste resource niet uitvoeren. Bovenliggende resource '&lt;ClusterName >' niet gevonden. "

## <a name="add-an-edge-node-when-creating-a-cluster"></a>Een edge-knooppunt toevoegen bij het maken van een cluster
In deze sectie gebruikt u een Resource Manager sjabloon toocreate HDInsight-cluster met een edge-knooppunt.  Hallo Resource Manager-sjabloon kunt u vinden in Hallo [galerie van Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/). Hallo Resource Manager-sjabloon roept een scriptactie zich bevindt op https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. Hallo-script heeft geen acties uitvoeren.  Het is toodemonstrate scriptactie aanroept vanuit een Resource Manager-sjabloon.

**een bestaand cluster voor leeg edge-knooppunt tooan tooadd**

1. Een HDInsight-cluster maken als u nog niet hebt.  Zie [aan de slag met Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).
2. Klik op Hallo installatiekopie toosign in tooAzure en open hello Azure Resource Manager-sjabloon in hello Azure-portal. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Configureer Hallo volgende eigenschappen:
   
   * **Abonnement**: Selecteer een Azure-abonnement gebruikt voor het Hallo-cluster maken.
   * **Resourcegroep**: Maak een nieuwe resourcegroep gebruikt voor het Hallo-cluster.
   * **Locatie**: Selecteer een locatie voor resourcegroep Hallo.
   * **Clusternaam**: Voer een naam voor het nieuwe cluster toocreate Hallo.
   * **Aanmeldingsnaam van gebruiker cluster**: Voer Hallo Hadoop HTTP-gebruikersnaam.  Hallo standaardnaam is **admin**.
   * **Aanmeldingswachtwoord cluster**: Geef het wachtwoord Hallo Hadoop HTTP-gebruiker.
   * **SSH gebruikersnaam**: Voer Hallo SSH-gebruikersnaam. Hallo standaardnaam is **sshuser**.
   * **SSH wachtwoord**: Geef het wachtwoord Hallo SSH-gebruiker.
   * **Installeren van de scriptactie**: Hallo standaardwaarde voor het doorlopen van deze zelfstudie houden.
     
     Sommige eigenschappen zijn vastgelegd in de sjabloon Hallo: clustertype, aantal Cluster worker-knooppunten, de grootte van de Edge-knooppunt en de naam van de Edge-knooppunt.
4. Controleer **ik ga akkoord toohello voorwaarden bovengenoemde**, en klik vervolgens op **aankoop** toocreate Hallo cluster met Hallo edge-knooppunt.

## <a name="access-an-edge-node"></a>Toegang tot een edge-knooppunt
Hallo edge-knooppunt ssh-eindpunt is &lt;EdgeNodeName >.&lt; ClusterName >-ssh.azurehdinsight.net:22.  Bijvoorbeeld, nieuwe-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.

Hallo edge-knooppunt wordt weergegeven als een toepassing op Hallo Azure-portal.  Hallo portal biedt u informatie tooaccess Hallo Hallo edge-knooppunt via SSH.

**tooverify hello edge-knooppunt SSH-eindpunt**

1. Meld u aan bij toohello [Azure-portal](https://portal.azure.com).
2. Open Hallo HDInsight-cluster met een edge-knooppunt.
3. Klik op **toepassingen** Hallo cluster-blade. U ziet Hallo edge-knooppunt.  Hallo standaardnaam is **nieuwe edgenode**.
4. Klik op Hallo edge-knooppunt. U ziet Hallo SSH-eindpunt.

**toouse Hive op Hallo edge-knooppunt**

1. Gebruik SSH tooconnect toohello edge-knooppunt. Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.

2. Nadat u toohello edge-knooppunt SSH hebt gekoppeld, gebruikt u Hallo opdrachtconsole tooopen Hallo Hive te volgen:
   
        hive
3. Voer Hallo opdracht tooshow Hive-tabellen in het Hallo-cluster te volgen:
   
        show tables;

## <a name="delete-an-edge-node"></a>Verwijderen van een edge-knooppunt
U kunt een edge-knooppunt verwijderen uit hello Azure-portal.

**tooaccess een edge-knooppunt**

1. Meld u aan bij toohello [Azure-portal](https://portal.azure.com).
2. Open Hallo HDInsight-cluster met een edge-knooppunt.
3. Klik op **toepassingen** Hallo cluster-blade. U ziet een lijst met knooppunten van de rand.  
4. Klik met de rechtermuisknop Hallo edge-knooppunt u toodelete wilt en klik vervolgens op **verwijderen**.
5. Klik op **Ja** tooconfirm.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe tooadd een edge-knooppunt en hoe tooaccess Hallo edge-knooppunt. toolearn Zie meer Hallo artikelen te volgen:

* [HDInsight-toepassingen installeren](hdinsight-apps-install-applications.md): meer informatie over hoe tooinstall een tooyour van de toepassing HDInsight-clusters.
* [Aangepaste HDInsight-toepassingen installeren](hdinsight-apps-install-custom-applications.md): meer informatie over hoe een niet-gepubliceerde HDInsight-toepassing tooHDInsight toodeploy.
* [HDInsight-toepassingen publiceren](hdinsight-apps-publish-applications.md): meer informatie over hoe toopublish uw aangepaste HDInsight-toepassingen tooAzure Marketplace.
* [MSDN: Een HDInsight-toepassing installeren](https://msdn.microsoft.com/library/mt706515.aspx): meer informatie over hoe toodefine HDInsight-toepassingen.
* [Met behulp van de scriptactie Linux gebaseerde HDInsight-clusters aanpassen](hdinsight-hadoop-customize-cluster-linux.md): meer informatie over hoe toouse scriptactie tooinstall aanvullende toepassingen.
* [Hadoop op basis van Linux-clusters maken in HDInsight met behulp van Resource Manager-sjablonen](hdinsight-hadoop-create-linux-clusters-arm-templates.md): meer informatie over hoe toocall Resource Manager-sjablonen toocreate HDInsight-clusters.


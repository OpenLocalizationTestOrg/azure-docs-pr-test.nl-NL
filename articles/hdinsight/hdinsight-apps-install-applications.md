---
title: aaaInstall van derden Hadoop-toepassingen in Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe tooinstall van derden Hadoop-toepassingen in Azure HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: eaf5904d-41e2-4a5f-8bec-9dde069039c2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/16/2017
ms.author: jgao
ms.openlocfilehash: 00071517c81a17c01dccedf9e8dd5d0cabb38567
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-third-party-hadoop-applications-on-azure-hdinsight"></a>Hadoop-toepassingen van derden op Azure HDInsight installeren

In dit artikel leert u hoe tooinstall een al gepubliceerde toepassing van derden Hadoop in Azure HDInsight. Zie voor instructies voor de installatie van uw eigen toepassing [Aangepaste HDInsight-toepassingen installeren](hdinsight-apps-install-custom-applications.md).

Een HDInsight-toepassing is een toepassing die gebruikers kunnen installeren op een op Linux gebaseerd HDInsight-cluster. Deze toepassingen kunnen zijn ontwikkeld door Microsoft, door onafhankelijke softwareleveranciers (ISV) of door u zelf.  

Momenteel zijn er vier gepubliceerde toepassingen:

* **DATAIKU DDS op HDInsight**: Dataiku DSS (gegevens wetenschappelijke Studio) is een software waarmee gegevens tooprototype professionals (gegevenswetenschappers, bedrijfsanalisten, ontwikkelaars...), bouwen en implementeren van zeer specifieke services die onbewerkte gegevens transformeren indrukwekkende business voorspellingen.
* **Datameer**: [Datameer](http://www.datameer.com/documentation/display/DAS50/Home?ls=Partners&lsd=Microsoft&c=Partners&cd=Microsoft) analisten biedt een interactieve manier toodiscover, analyseren en visualiseren Hallo resultaten van Big Data. Trek in extra gegevensbronnen gemakkelijk toodiscover nieuwe relaties en u snel moet Hallo-antwoorden krijgen.
* **Gegevensverzamelaar Streamsets voor HDnsight** biedt een complete IDE integrated development environment () kunt u ontwerpen, testen, implementeren en beheren any-to-any pijplijnen die stroom en batch gegevens net opnemen, en omvatten diverse stroom transformaties: alle zonder toowrite aangepaste code. 
* **Cask CDAP voor HDInsight** biedt Hallo unified eerst integratieplatform voor big data dat wordt het Hallo tijd tooproduction voor data-toepassingen en gegevens meren met 80%. Deze toepassing biedt alleen ondersteuning voor standaard HBase 3.4-clusters.
* **H2O kunstmatige Intelligence voor HDInsight (bèta)** H2O mineraalwater ondersteunt Hallo algoritmen voor gedistribueerde te volgen: GLM, Naïve Bayes, gedistribueerde willekeurige Forest, kleurovergang versterking Machine, Deep Neural Networks, Deep leren, K-means, PCA, Lage waarden van positie modellen, Afwijkingsdetectie en Autoencoders gegeneraliseerd.
* **Kyligence Analytics Platform** Kyligence Analytics Platform (KAP) is een enterprise-ready datawarehouse aangedreven door Apache Kylin en Apache Hadoop; het onderliggende seconde Querylatentie voor grootschalige gegevensset machtigt en gegevensanalyse voor vereenvoudigt zakelijke gebruikers en analisten. 
* **SnapLogic Hadooplex** hello SnapLogic Hadooplex uitgevoerd op HDInsight kunt tooget toobusiness insights klanten sneller door selfservice gegevensopname en voorbereiding vanaf vrijwel elke bron toohello Microsoft Azure-cloud platform.
* **Spark-taakserver voor KNIME Spark Executor** Spark-taakserver voor KNIME Spark Executor gebruikte tooconnect hello KNIME Analytics Platform tooHDInsight clusters is.

Hallo-instructies in dit artikel Azure portal gebruiken. U kunt hello Azure Resource Manager-sjabloon exporteren vanuit de portal hello of een kopie van de Resource Manager-sjabloon Hallo verkrijgen van leveranciers en gebruik Azure PowerShell en Azure CLI toodeploy Hallo sjabloon.  Zie [Op Linux gebaseerde Hadoop-clusters maken in HDInsight met behulp van Resource Manager-sjablonen](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

## <a name="prerequisites"></a>Vereisten
Als u tooinstall HDInsight-toepassingen op een bestaand HDInsight-cluster wilt, moet u een HDInsight-cluster hebben. toocreate, Zie [clusters maken](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). U kunt ook HDInsight-toepassingen installeren wanneer u een HDInsight-cluster maakt.

## <a name="install-applications-tooexisting-clusters"></a>Installeren van toepassingen tooexisting clusters
Hallo volgende procedure laat zien u hoe tooinstall HDInsight-toepassingen tooan bestaand HDInsight-cluster.

**tooinstall een HDInsight-toepassing**

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op **HDInsight-Clusters** in het linkermenu Hallo.  Als u dit niet ziet, klikt u op **Meer services** en vervolgens op **HDInsight-clusters**.
3. Klik op een HDInsight-cluster.  Als u deze niet hebt, maakt u die eerst.  Zie [Clusters maken](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).
4. Klik op **toepassingen** onder Hallo **configuraties** categorie. Hier ziet u een lijst met geïnstalleerde toepassingen. Als u geen toepassingen vinden, betekent dit dat er is geen toepassingen voor deze versie van Hallo HDInsight-cluster.
   
    ![Menu van HDInsight-toepassingenportal](./media/hdinsight-apps-install-applications/hdinsight-apps-portal-menu.png)
5. Klik op **toevoegen** in Hallo blade menu. 
   
    ![HDInsight-toepassingen, geïnstalleerde apps](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps.png)
   
    Er wordt een lijst met bestaande HDInsight-toepassingen weergegeven.
   
    ![HDInsight-toepassingen, beschikbare toepassingen](./media/hdinsight-apps-install-applications/hdinsight-apps-list.png)
6. Klik op een van de toepassingen hello, accepteer de juridische bepalingen Hallo en klik op **Selecteer**.

U kunt de status van de installatie van de bedrijfsportal meldingen Hallo Hallo zien (Klik op Hallo belpictogram bovenaan Hallo van Hallo portal). Na het Hallo wordt toepassing geïnstalleerd, wordt toepassing hello op Hallo geïnstalleerde Apps blade wordt weergegeven.

## <a name="install-applications-during-cluster-creation"></a>Toepassingen installeren tijdens het maken van het cluster
Hallo optie tooinstall HDInsight-toepassingen hebt u wanneer u een cluster maakt. HDInsight-toepassingen zijn tijdens hello wordt geïnstalleerd als Hallo cluster wordt gemaakt en wordt in Hallo actief is. Hallo volgende procedure laat zien u hoe tooinstall HDInsight-toepassingen wanneer u een cluster maakt.

**tooinstall een HDInsight-toepassing**

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op **Nieuw**, klik op **Gegevens en analyse** en klik vervolgens op **HDInsight**.
3. Voer **Clusternaam** in: deze naam moet uniek zijn.
4. Klik op **abonnement** tooselect hello Azure-abonnement dat wordt gebruikt voor het Hallo-cluster.
5. Klik op **Clustertype selecteren** en selecteer vervolgens:
   
   * **Type cluster**: als u niet welke toochoose weet, selecteert u **Hadoop**. Het is meest populaire clustertype Hallo.
   * **Besturingssysteem**: selecteer **Linux**.
   * **Versie**: standaardversie hello gebruiken als u niet welke toochoose weet. Zie [HDInsight-clusterversies](hdinsight-component-versioning.md) voor meer informatie.
   * **Cluster-laag**: Azure HDInsight biedt Hallo big data cloud twee categorieën aanbiedingen: lagen Standard en Premium-laag. Zie [Clusterlagen](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers) voor meer informatie.
6. Klik op **toepassingen**, klikt u op een van de Hallo gepubliceerde toepassingen en klik vervolgens op **Selecteer**.
7. Klik op **referenties** en voer vervolgens een wachtwoord voor gebruiker met beheerdersrechten Hallo. U moet ook tooenter een **SSH-gebruikersnaam** en een **wachtwoord** of **openbare sleutel**, namelijk gebruikte tooauthenticate Hallo SSH-gebruiker. Met behulp van een openbare sleutel is Hallo aanbevolen benadering. Klik op **Selecteer** op Hallo onder toosave Hallo referenties configuratie.
8. Klik op **gegevensbron**, selecteer een van de bestaande opslagaccounts hello of een nieuwe opslag account toobe gebruikt als Hallo storage-standaardaccount voor Hallo cluster maken.
9. Klik op **resourcegroep** tooselect een bestaande resource groep, of klik op **nieuw** toocreate een nieuwe resourcegroep
10. Op Hallo **nieuwe HDInsight-Cluster** blade ervoor te zorgen dat **pincode tooStartboard** is geselecteerd en klik vervolgens op **maken**. 

## <a name="list-installed-hdinsight-apps-and-properties"></a>Lijst van geïnstalleerde HDInsight-apps en -eigenschappen
Hallo portal ziet u dat een lijst met Hallo HDInsight-toepassingen voor een cluster en het Hallo-eigenschappen van elke geïnstalleerde toepassing geïnstalleerd.

**toolist HDInsight-toepassing en de weergave-eigenschappen**

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op **HDInsight-Clusters** in het linkermenu Hallo.  Als u dit niet ziet, klikt u op **Bladeren** en vervolgens op **HDInsight-clusters**.
3. Klik op een HDInsight-cluster.
4. Van Hallo **instellingen** blade, klikt u op **toepassingen** onder Hallo **algemene** categorie. Hallo geïnstalleerde Apps blade geeft een lijst van alle Hallo geïnstalleerd toepassingen. 
   
    ![HDInsight-toepassingen, geïnstalleerde apps](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps-with-apps.png)
5. Klik op een Hallo geïnstalleerd toepassingen tooshow Hallo eigenschap. Hallo blade lijsten met eigenschappen:
   
   * De naam van de app: de naam van de toepassing.
   * Status: toepassingsstatus. 
   * Webpagina: URL van Hallo van Hallo-webtoepassing die u toohello edge-knooppunt hebt geïmplementeerd. Hallo-referentie is hetzelfde als HTTP Hallo gebruikersreferenties die u hebt geconfigureerd voor de cluster Hallo Hallo.
   * HTTP-eindpunt: Hallo referentie is hetzelfde als HTTP Hallo gebruikersreferenties die u hebt geconfigureerd voor de cluster Hallo Hallo. 
   * SSH-eindpunt: U kunt SSH tooconnect toohello edge-knooppunt. Hallo SSH-referenties zijn hetzelfde als het Hallo SSH gebruikersreferenties die u hebt geconfigureerd voor Hallo cluster Hallo. Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.
6. toodelete een toepassing, met de rechtermuisknop op het Hallo-toepassing en klik vervolgens op **verwijderen** in het contextmenu Hallo.

## <a name="connect-toohello-edge-node"></a>Verbinding maken met toohello edge-knooppunt
U kunt toohello edge-knooppunt met behulp van HTTP- en SSH verbinden. Hallo eindpuntinformatie vinden van Hallo [portal](#list-installed-hdinsight-apps-and-properties). Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.

Hallo HTTP-eindpunt referenties zijn Hallo HTTP-gebruikersreferenties die u hebt geconfigureerd voor HDInsight-cluster Hallo; Hallo SSH-eindpunt referenties zijn Hallo SSH-referenties die u hebt geconfigureerd voor Hallo HDInsight-cluster.

## <a name="troubleshoot"></a>Problemen oplossen
Zie [Hallo installatie oplossen](hdinsight-apps-install-custom-applications.md#troubleshoot-the-installation).

## <a name="next-steps"></a>Volgende stappen
* [Aangepaste HDInsight-toepassingen installeren](hdinsight-apps-install-custom-applications.md): meer informatie over hoe een niet-gepubliceerde HDInsight-toepassing tooHDInsight toodeploy.
* [HDInsight-toepassingen publiceren](hdinsight-apps-publish-applications.md): meer informatie over hoe toopublish uw aangepaste HDInsight-toepassingen tooAzure Marketplace.
* [MSDN: Een HDInsight-toepassing installeren](https://msdn.microsoft.com/library/mt706515.aspx): meer informatie over hoe toodefine HDInsight-toepassingen.
* [Met behulp van de scriptactie Linux gebaseerde HDInsight-clusters aanpassen](hdinsight-hadoop-customize-cluster-linux.md): meer informatie over hoe toouse scriptactie tooinstall aanvullende toepassingen.
* [Hadoop op basis van Linux-clusters maken in HDInsight met behulp van Resource Manager-sjablonen](hdinsight-hadoop-create-linux-clusters-arm-templates.md): meer informatie over hoe toocall Resource Manager-sjablonen toocreate HDInsight-clusters.
* [Lege edge-knooppunten gebruiken in HDInsight](hdinsight-apps-use-edge-node.md): meer informatie over hoe toouse een lege edge-knooppunt voor toegang tot HDInsight-cluster, HDInsight-toepassingen testen en hosten van HDInsight-toepassingen.


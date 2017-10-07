---
title: aaaInstall uw eigen aangepaste Hadoop-toepassingen in Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe tooinstall HDInsight-toepassingen op HDInsight-toepassingen.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e556b29c-8176-4bc5-a90b-aa01abfd3aee
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ed3148f2c4d4d2b568d84e44fa6d76bb5a001902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-custom-hadoop-applications-on-azure-hdinsight"></a>Aangepaste Hadoop-toepassingen installeren op Azure HDInsight

In dit artikel leert u hoe tooinstall een Hadoop-toepassing in Azure HDInsight, die niet is gepubliceerd toohello Azure-portal. Hallo-toepassing die u in dit artikel installeren wilt is [Hue](http://gethue.com/).

Een HDInsight-toepassing is een toepassing die gebruikers kunnen installeren op een op Linux gebaseerd HDInsight-cluster.  Deze toepassingen kunnen zijn ontwikkeld door Microsoft, door onafhankelijke softwareleveranciers (ISV) of door u zelf.  

Andere verwante artikelen:

* [HDInsight-toepassingen installeren](hdinsight-apps-install-applications.md): meer informatie over hoe tooinstall een tooyour van de toepassing HDInsight-clusters.
* [HDInsight-toepassingen publiceren](hdinsight-apps-publish-applications.md): meer informatie over hoe toopublish uw aangepaste HDInsight-toepassingen tooAzure Marketplace.
* [MSDN: Een HDInsight-toepassing installeren](https://msdn.microsoft.com/library/mt706515.aspx): meer informatie over hoe toodefine HDInsight-toepassingen.

## <a name="prerequisites"></a>Vereisten
Als u tooinstall HDInsight-toepassingen op een bestaand HDInsight-cluster wilt, moet u een HDInsight-cluster hebben. toocreate, Zie [clusters maken](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). U kunt ook HDInsight-toepassingen installeren wanneer u een HDInsight-cluster maakt.

## <a name="install-hdinsight-applications"></a>HDInsight-toepassingen installeren
HDInsight-toepassingen kunnen worden geïnstalleerd wanneer u een cluster of een bestaand HDInsight-cluster tooan maakt. Zie [MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx) (MSDN: een HDInsight-toepassing installeren) voor het definiëren van Azure Resource Manager-sjablonen.

Hallo-bestanden die nodig zijn voor het implementeren van deze toepassing (Hue):

* [azuredeploy.JSON](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/azuredeploy.json): Hallo Resource Manager-sjabloon voor het installeren van HDInsight-toepassing. Zie [MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx) (MSDN: een HDInsight-toepassing installeren) om uw eigen Resource Manager-sjabloon te ontwikkelen.
* [HUE-install_v0.sh](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/scripts/Hue-install_v0.sh): Hallo scriptactie wordt aangeroepen door Hallo Resource Manager-sjabloon voor het configureren van Hallo edge-knooppunt.
* [HUE-binaries.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): Hallo binaire hue-bestand wordt aangeroepen vanuit hui-install_v0.sh.
* [HUE-binaire bestanden-14-04.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): Hallo binaire hue-bestand wordt aangeroepen vanuit hui-install_v0.sh.
* [webwasb-tomcat.tar.gz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/webwasb-tomcat.tar.gz): een voorbeeldweb-app (Tomcat) die wordt aangeroepen vanuit hui-install_v0.sh.

**tooinstall Hue tooan bestaand HDInsight-cluster**

1. Klik op Hallo installatiekopie toosign in tooAzure en open Hallo Resource Manager-sjabloon in hello Azure-Portal.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2FIaas-Applications%2Fmaster%2FHue%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Deze knop opent u een Resource Manager-sjabloon op Hallo Azure-portal.  Hallo Resource Manager-sjabloon bevindt zich op [https://github.com/hdinsight/Iaas-Applications/tree/master/Hue](https://github.com/hdinsight/Iaas-Applications/tree/master/Hue).  toolearn hoe toowrite deze Resource Manager-sjabloon, Zie [MSDN: een HDInsight-toepassing installeren](https://msdn.microsoft.com/library/mt706515.aspx).
2. Van Hallo **Parameters** blade Hallo volgende invoeren:

   * **Clusternaam**: Voer Hallo-naam van Hallo cluster waar u tooinstall Hallo-toepassing. Dit cluster moet een bestaand cluster zijn.
3. Klik op **OK** toosave Hallo parameters.
4. Van Hallo **aangepaste implementatie** blade Voer **resourcegroep**.  Hallo-resourcegroep is een container waarin Hallo-cluster, Hallo afhankelijke opslagaccount en andere resources zijn gegroepeerd. Dit is vereist toouse Hallo dezelfde resourcegroep als Hallo-cluster.
5. Klik op **Juridische voorwaarden** en vervolgens op **Maken**.
6. Controleer of Hallo **pincode toodashboard** selectievakje is ingeschakeld en klik vervolgens op **maken**. Hier ziet u de installatiestatus Hallo van Hallo tegel vastgemaakt toohello portal dashboard en het Hallo-portalmelding (Klik op Hallo belpictogram bovenaan Hallo van Hallo portal).  Het duurt ongeveer 10 minuten tooinstall Hallo toepassing.

**tooinstall Hue tijdens het maken van een cluster**

1. Klik op Hallo installatiekopie toosign in tooAzure en open Hallo Resource Manager-sjabloon in hello Azure-Portal.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhdinsightapps%2Fcreate-linux-based-hadoop-cluster-in-hdinsight.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Deze knop opent u een Resource Manager-sjabloon op Hallo Azure-portal.  Hallo Resource Manager-sjabloon bevindt zich op [https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json](https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json).  toolearn hoe toowrite deze Resource Manager-sjabloon, Zie [MSDN: een HDInsight-toepassing installeren](https://msdn.microsoft.com/library/mt706515.aspx).
2. Ga als volgt Hallo instructie toocreate cluster en Hue te installeren. Zie [Op Linux gebaseerde Hadoop-clusters maken in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) voor meer informatie over het maken van HDInsight-clusters.

Bovendien toohello Azure-portal, u kunt ook [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-powershell) en [Azure CLI](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-cli) toocall Resource Manager-sjablonen.

## <a name="validate-hello-installation"></a>Hallo installatie valideren
U kunt Hallo toepassingsstatus op Hallo van de installatie van de toepassing hello Azure portal toovalidate controleren. Bovendien kunt u ook valideren alle HTTP-eindpunten zijn gegenereerd zoals verwacht en Hallo webpagina als er een:

**tooopen hello Hue-portal**

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op **HDInsight-Clusters** in het linkermenu Hallo.  Als u dit niet ziet, klikt u op **Bladeren** en vervolgens op **HDInsight-clusters**.
3. Klik op Hallo cluster waar u de toepassing hello hebt geïnstalleerd.
4. Van Hallo **instellingen** blade, klikt u op **toepassingen** onder Hallo **algemene** categorie. U ziet **hue** die worden vermeld in Hallo **geïnstalleerde Apps** blade.
5. Klik op **hue** uit Hallo lijst toolist Hallo eigenschappen.  
6. Klik op Hallo webpagina koppeling toovalidate Hallo website; Open een browser toovalidate Hallo Hue-webgebruikersinterface, open Hallo SSH-eindpunt gebruik van SSH Hallo HTTP-eindpunt. Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.

## <a name="troubleshoot-hello-installation"></a>Problemen oplossen Hallo-installatie
U kunt controleren Hallo toepassingsinstallatiestatus van Hallo portalmelding (Klik op Hallo belpictogram bovenaan Hallo van Hallo portal).

Als de installatie van een toepassing is mislukt, kunt u Hallo foutberichten en foutopsporingsgegevens op 3 plaatsen:

* HDInsight-toepassingen: algemene foutgegevens.

    Hallo cluster openen vanuit Hallo-portal en toepassingen van de blade instellingen Hallo op:

    ![Fout bij het installeren van HDInsight-toepassingen](./media/hdinsight-apps-install-applications/hdinsight-apps-error.png)
* HDInsight-scriptactie: als het foutbericht Hallo HDInsight-toepassingen een mislukte scriptactie aangeeft, meer informatie over de Hallo script fout weergegeven in het deelvenster scriptacties Hallo.

    Klik op scriptactie van de blade instellingen Hallo. Geschiedenis van de scriptactie ziet foutberichten Hallo

    ![Scriptactiefout voor HDInsight-toepassingen](./media/hdinsight-apps-install-applications/hdinsight-apps-script-action-error.png)
* Ambari-webgebruikersinterface: Als het installatiescript Hallo Hallo oorzaak van de Hallo-fout is, gebruik Ambari-Webgebruikersinterface toocheck volledige logboeken over de installatiescripts Hallo.

    Zie [Probleemoplossing](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) voor meer informatie .

## <a name="remove-hdinsight-applications"></a>HDInsight-toepassingen verwijderen
Er zijn verschillende manieren toodelete HDInsight-toepassingen.

### <a name="use-portal"></a>De portal gebruiken
**tooremove een toepassing met behulp van Hallo-portal**

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op **HDInsight-Clusters** in het linkermenu Hallo.  Als u dit niet ziet, klikt u op **Bladeren** en vervolgens op **HDInsight-clusters**.
3. Klik op Hallo cluster waar u de toepassing hello hebt geïnstalleerd.
4. Van Hallo **instellingen** blade, klikt u op **toepassingen** onder Hallo **algemene** categorie. Er wordt een lijst met geïnstalleerde toepassingen weergegeven. Voor deze zelfstudie **hue** die worden vermeld in Hallo **geïnstalleerde Apps** blade.
5. Met de rechtermuisknop op de toepassing hello u tooremove wilt en klik vervolgens op **verwijderen**.
6. Klik op **Ja** tooconfirm.

U kunt ook Hallo cluster verwijderen of verwijderen van resourcegroep Hallo waarin de toepassing hello vanuit de portal Hallo.

### <a name="use-azure-powershell"></a>Azure PowerShell gebruiken
Met Azure PowerShell, kunt u Hallo cluster verwijderen of Hallo resourcegroep verwijderen. Zie [Clusters verwijderen met behulp van Azure PowerShell](hdinsight-administer-use-powershell.md#delete-clusters).

### <a name="use-azure-cli"></a>Azure CLI gebruiken
Met Azure CLI, kunt u Hallo cluster verwijderen of Hallo resourcegroep verwijderen. Zie [Clusters verwijderen met behulp van Azure CLI](hdinsight-administer-use-command-line.md#delete-clusters).

## <a name="next-steps"></a>Volgende stappen
* [MSDN: Een HDInsight-toepassing installeren](https://msdn.microsoft.com/library/mt706515.aspx): meer informatie over hoe toodevelop Resource Manager-sjablonen voor het implementeren van HDInsight-toepassingen.
* [HDInsight-toepassingen installeren](hdinsight-apps-install-applications.md): meer informatie over hoe tooinstall een tooyour van de toepassing HDInsight-clusters.
* [HDInsight-toepassingen publiceren](hdinsight-apps-publish-applications.md): meer informatie over hoe toopublish uw aangepaste HDInsight-toepassingen tooAzure Marketplace.
* [Met behulp van de scriptactie Linux gebaseerde HDInsight-clusters aanpassen](hdinsight-hadoop-customize-cluster-linux.md): meer informatie over hoe toouse scriptactie tooinstall aanvullende toepassingen.
* [Hadoop op basis van Linux-clusters maken in HDInsight met behulp van Resource Manager-sjablonen](hdinsight-hadoop-create-linux-clusters-arm-templates.md): meer informatie over hoe toocall Resource Manager-sjablonen toocreate HDInsight-clusters.
* [Lege edge-knooppunten gebruiken in HDInsight](hdinsight-apps-use-edge-node.md): meer informatie over hoe toouse een lege edge-knooppunt voor toegang tot HDInsight-cluster, HDInsight-toepassingen testen en hosten van HDInsight-toepassingen.

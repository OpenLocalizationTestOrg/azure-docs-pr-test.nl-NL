---
title: aaaManage Hadoop-clusters in HDInsight met behulp van Azure portal | Microsoft Docs
description: Meer informatie over hoe toocreate en beheren van HDInsight-clusters met hello Azure-portal.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: c242d43d4ccea7cf1e7be19c3f3d7ed3c4f50918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Hadoop-clusters in HDInsight beheren met behulp van hello Azure-portal
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Met behulp van Hallo [Azure-portal][azure-portal], kunt u in Azure HDInsight Hadoop-clusters beheren. Hallo tabselector voor informatie over het beheren van Hadoop-clusters in HDInsight met andere hulpprogramma's gebruiken.

**Vereisten**

Voordat u dit artikel, moet u de volgende items Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="open-hello-portal"></a>Open Hallo-portal
1. Aanmelden te[https://portal.azure.com](https://portal.azure.com).
2. Nadat u Hallo portal opent, kunt u:

   * Klik op **nieuw** van Hallo linkermenu toocreate een nieuw cluster:

       ![knop Nieuw HDInsight-cluster](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * Klik op **HDInsight-Clusters** van Hallo Hallo linkermenu toolist bestaande clusters

       ![Knop Azure portal HDInsight-cluster](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       Als er geen HDInsight-cluster, klik op **meer services** op Hallo onderaan Hallo lijst en klik vervolgens op **HDInsight-clusters** onder Hallo **Intelligence en analyse** sectie.


## <a name="create-clusters"></a>Clusters maken
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

HDInsight werkt met een breed bereik van Hadoop-onderdelen. Zie voor Hallo lijst Hallo-onderdelen die zijn geverifieerd en ondersteund [welke versie van Hadoop is in Azure HDInsight](hdinsight-component-versioning.md). Zie voor informatie over Hallo algemene cluster maken, [maken Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

### <a name="access-control-requirements"></a>Vereisten voor toegangsbeheer

Wanneer u een HDInsight-cluster maakt, moet u een Azure-abonnement opgeven. Dit cluster kan worden gemaakt in een nieuwe Azure-resourcegroep of een bestaande resourcegroep. U kunt Hallo tooverify stappen te volgen uw machtigingen voor het maken van HDInsight-clusters:

- toouse een bestaande resourcegroep.

    1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
    2. Klik op **resourcegroepen** uit Hallo linkermenu toolist Hallo-resourcegroepen.
    3. Klik op Hallo resourcegroep gewenste toouse voor het maken van uw HDInsight-cluster.
    4. Klik op **toegangsbeheer (IAM)**, en controleer of u (of een groep waarvan u deel uitmaakt) hebben ten minste Hallo Inzender toegang toohello resourcegroep.

- toocreate een nieuwe resourcegroep

    1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
    2. Klik op **abonnement** in het linkermenu Hallo. Het heeft pictogram van een gele sleutel. U ziet een lijst met abonnementen.
    3. Klik op Hallo-abonnement dat u toocreate clusters. 
    4. Klik op **mijn machtigingen**.  Het bevat uw [rol](../active-directory/role-based-access-control-what-is.md#built-in-roles) op Hallo-abonnement. U moet ten minste Inzender toegang toocreate HDInsight-cluster.

Als u Hallo NoRegisteredProviderFound fout of Hallo MissingSubscriptionRegistration fout ontvangt, raadpleegt u [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](../azure-resource-manager/resource-manager-common-deployment-errors.md).

## <a name="list-and-show-clusters"></a>Lijst en clusters weer te geven
1. Aanmelden te[https://portal.azure.com](https://portal.azure.com).
2. Klik op **HDInsight-Clusters** van Hallo Hallo linkermenu toolist bestaande clusters.
3. Klik op de clusternaam Hallo. Als Hallo clusterlijst te lang is, kunt u filteren op Hallo Hallo pagina bovenaan.
4. Klik op een cluster met Hallo lijst toosee Hallo-overzichtspagina:

    ![Azure portal HDInsight-cluster essentials](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    * **Dashboard**: wordt geopend Hallo cluster-dashboard, dat Ambari Web voor op basis van Linux-clusters.
    * **Secure Shell**: toont Hallo instructies tooconnect toohello cluster met behulp van Secure Shell (SSH) verbinding.
    * **Cluster schalen**: Hiermee kunt u toochange Hallo aantal worker-knooppunten voor dit cluster.
    * **Verwijderen**: verwijderingen Hallo-cluster.
    * **Activiteitenlogboeken**: weergeven en query activiteitenlogboeken.
    * **Toegangsbeheer (IAM)**: roltoewijzingen gebruiken.  Zie [rol toewijzingen toomanage toegang tooyour Azure-abonnementresources gebruiken](../active-directory/role-based-access-control-configure.md).
    * **Labels**: Hiermee kunt u tooset sleutel/waarde-paren toodefine een aangepaste taxonomie van uw cloud-services. Bijvoorbeeld, u kunt maken met een sleutel met de naam **project**, en gebruik vervolgens een overeenkomende waarde voor alle services die zijn gekoppeld aan een bepaald project.
    * **Diagnosticeren en oplossen van problemen met**: informatie over probleemoplossing weergeven.
    * **Hiermee vergrendelt u**: toevoegen vergrendeling tooprevent Hallo cluster wordt gewijzigd of verwijderd.
    * **Automatiseringsscript**: weergeven en exporteren hello Azure Resource Manager-sjabloon voor Hallo-cluster. U kunt op dit moment alleen Hallo afhankelijke Azure storage-account exporteren. Zie [maken Linux gebaseerde Hadoop-clusters in HDInsight met behulp van Azure Resource Manager-sjablonen](hdinsight-hadoop-create-linux-clusters-arm-templates.md).
    * **Snel starten**: geeft informatie weer die u helpt aan de slag met HDInsight.
    * **Hulpprogramma's voor HDInsight**: Help-informatie voor HDInsight gerelateerde hulpprogramma's.
    * **Aanmelding cluster**: Hallo cluster aanmeldingsgegevens worden weergegeven.
    * **Abonnement Core gebruik**: weergave Hallo kernen gebruikt en beschikbaar voor uw abonnement.
    * **Cluster schalen**: verhogen en de afname Hallo aantal worker clusterknooppunten. Zie[schalen clusters](hdinsight-administer-use-management-portal.md#scale-clusters).
    * **Secure Shell**: toont Hallo instructies tooconnect toohello cluster met behulp van Secure Shell (SSH) verbinding. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.
    * **HDInsight-Partner**: toevoegen of verwijderen Hallo huidige HDInsight-Partner.
    * **Met externe Metastores**: Hallo Hive en Oozie metastores weergeven. Hallo metastores kan alleen worden geconfigureerd tijdens het Hallo-cluster maken. Zie [gebruik Hive/Oozie-metastore](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).
    * **Acties script**: uitvoeren Bash-scripts op Hallo-cluster. Zie [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).
    * **Toepassingen**: toevoegen/verwijderen HDInsight-toepassingen.  Zie [aangepaste HDInsight-toepassingen installeren](hdinsight-apps-install-custom-applications.md).
    * **Eigenschappen**: Hallo clustereigenschappen weergeven.
    * **Storage-accounts**: Hallo storage-accounts en Hallo sleutels weergeven. Hallo storage-accounts zijn geconfigureerd tijdens het Hallo-cluster maken.
    * **AAD-identiteit cluster**:
    * **Nieuw ondersteuningsverzoek**: Hiermee kunt u toocreate een ondersteuningsticket met Microsoft ondersteuning.
    
6. Klik op **eigenschappen**:

    Hallo-eigenschappen zijn:

   * **Hostname**: de naam van het Cluster.
   * **Cluster-URL**. Hallo-URL voor Hallo Ambari webinterface.
   * **Status**: omvatten afgebroken, geaccepteerd, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, operationeel is, wordt uitgevoerd, fout, te verwijderen, verwijderd, time-out, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization
   * **Regio**: Azure-locatie. Zie voor een lijst van ondersteunde Azure locaties Hallo **regio** vervolgkeuzelijst op [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).
   * **Aanmaakdatum**.
   * **Besturingssysteem**: beide **Windows** of **Linux**.
   * **Type**: Hadoop, HBase, Storm, Spark.
   * **Versie**. Zie [HDInsight-versies](hdinsight-component-versioning.md)
   * **Abonnement**: de naam van het abonnement.
   * **Standaardgegevensbron**: Hallo standaardbestandssysteem cluster.
   * **De grootte van de worker-knooppunten**.
   * **De grootte van knooppunt HEAD**.

## <a name="delete-clusters"></a>Clusters verwijderen
Verwijderen van een cluster worden niet verwijderd Hallo standaardopslagaccount of alle gekoppelde opslagaccounts weergegeven. U kunt Hallo cluster opnieuw maken met behulp van Hallo dezelfde opslagaccounts en metastores dezelfde Hallo. Het is aanbevolen toouse wanneer u Hallo cluster opnieuw maakt een standaard Blob-container.

1. Meld u aan toohello [Portal][azure-portal].
2. Klik op **HDInsight-Clusters** in het linkermenu Hallo. Als er geen **HDInsight-Clusters**, klikt u op **meer services** eerste.
3. Klik op Hallo-cluster dat u wilt dat toodelete.
4. Klik op **verwijderen** van Hallo bovenste menu en volg de instructies in Hallo.

Zie ook [onderbreken/afsluiten clusters](#pauseshut-down-clusters).

## <a name="add-additional-storage-accounts"></a>Extra opslagaccounts toevoegen

U kunt extra Azure Storage-accounts en Azure Data Lake Store-accounts toevoegen nadat een cluster wordt gemaakt. Zie voor meer informatie [toevoegen van extra opslagruimte accounts tooHDInsight](./hdinsight-hadoop-add-storage.md).

## <a name="scale-clusters"></a>Clusters schalen
Hallo-cluster schalen van functie kunt u toochange Hallo aantal worker-knooppunten gebruikt door een cluster dat wordt uitgevoerd in Azure HDInsight zonder toore-Hallo cluster maken.

> [!NOTE]
> Alleen clusters met HDInsight versie 3.1.3 of hoger worden ondersteund. Als u niet zeker Hallo versie van het cluster weet, kunt u de eigenschappenpagina Hallo controleren.  Zie [lijst en geeft weer clusters](#list-and-show-clusters).
>
>

Hallo gevolgen van het aantal gegevensknooppunten voor elk type ondersteund door HDInsight cluster Hallo wijzigen:

* Hadoop

    Hallo aantal worker-knooppunten van een Hadoop-cluster dat wordt uitgevoerd zonder enige impact op alle taken die in behandeling of wordt uitgevoerd, kunt u naadloos verhogen. Nieuwe taken kunnen ook worden verzonden tijdens het Hallo-bewerking wordt uitgevoerd. Fouten in een bewerking voor schaal worden probleemloos verwerkt zodat hello cluster altijd functioneel is overblijft.

    Wanneer een Hadoop-cluster wordt verkleind door het aantal gegevensknooppunten hello te verminderen, worden sommige services in de cluster Hallo Hallo opnieuw gestart. Dit gedrag zorgt ervoor dat alle actieve en in behandeling zijnde taken toofail op Hallo Hallo schalen van de bewerking is voltooid. U kunt echter Hallo taken verzenden zodra Hallo-bewerking voltooid is.
* HBase

    U kunt naadloos toevoegen of verwijderen van knooppunten tooyour HBase-cluster, terwijl deze wordt uitgevoerd. Regionale Servers worden automatisch verdeeld binnen een paar minuten na voltooiing van Hallo bewerking schalen. U kunt echter ook handmatig Hallo regionale servers verdelen door logboekregistratie in toohello headnode van het cluster en actieve Hallo volgende opdrachten uit een opdrachtpromptvenster:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    Zie voor meer informatie over het gebruik van HBase-shell Hallo]
* Storm

    U kunt naadloos toevoegen of verwijderen van gegevens knooppunten tooyour Storm-cluster, terwijl deze wordt uitgevoerd. Maar nadat de bewerking schalen Hallo installatie is voltooid, moet u toorebalance Hallo topologie.

    Herverdeling kan worden uitgevoerd op twee manieren:

  * Storm-webgebruikersinterface
  * Hulpprogramma voor opdrachtregelinterface (CLI)

    Raadpleeg toohello [Apache Storm documentatie](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) voor meer informatie.

    Hallo Storm-webgebruikersinterface is beschikbaar op Hallo HDInsight-cluster:

    ![HDInsight Storm scale deel opnieuw](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    Hier volgt een voorbeeld hoe toouse Hallo CLI toorebalance Hallo Storm-topologie opdracht:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**tooscale clusters**

1. Meld u aan toohello [Portal][azure-portal].
2. Klik op **HDInsight-Clusters** in het linkermenu Hallo.
3. Klik op de gewenste tooscale Hallo-cluster.
3. Klik op **Cluster schalen**.
4. Voer **nummer van Worker-knooppunten**. Hallo-limiet voor Hallo aantal clusterknooppunten verschilt per Azure-abonnementen. Neem contact op met facturering tooincrease hello ondersteuningslimiet.  kostengegevens Hallo weerspiegelt Hallo aangebrachte wijzigingen toohello aantal knooppunten.

    ![HDInsight hadoop hbase, storm spark schaal](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a>Onderbreken/clusters afsluiten

De meeste Hadoop-taken zijn batchtaken die alleen van tijd tot tijd worden uitgevoerd. Voor de meeste Hadoop-clusters, er zijn grote perioden tijd dat Hallo-cluster niet wordt gebruikt voor verwerking. Met HDInsight worden uw gegevens opgeslagen in Azure Storage zodat u een cluster veilig kunt verwijderen wanneer deze niet wordt gebruikt.
Voor een HDInsight-cluster worden ook kosten in rekening gebracht, zelfs wanneer het niet wordt gebruikt. Aangezien Hallo kosten voor Hallo cluster vaak zoveel hoger zijn dan Hallo kosten voor opslag, is het financieel aantrekkelijk toodelete clusters wanneer ze zich niet in gebruik.

Er zijn veel manieren u kunt programmeren Hallo proces:

* Gebruiker Azure Data Factory. Zie [maken via bellen op Linux gebaseerde Hadoop-clusters in HDInsight met behulp van Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) gekoppelde services voor het maken van HDInsight op aanvraag.
* Azure PowerShell gebruiken.  Zie [analyseren vertraging vluchtgegevens](hdinsight-analyze-flight-delay-data.md).
* Azure CLI gebruiken. Zie [HDInsight-clusters beheren met Azure CLI](hdinsight-administer-use-command-line.md).
* HDInsight .NET SDK gebruiken. Zie [indienen Hadoop-taken](hdinsight-submit-hadoop-jobs-programmatically.md).

Zie voor Hallo prijsgegevens, [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/). een cluster met Hallo Portal toodelete Zie [clusters verwijderen](#delete-clusters)


## <a name="upgrade-clusters"></a>Bijwerken van clusters

Zie [Upgrade HDInsight-cluster tooa nieuwere versie](./hdinsight-upgrade-cluster.md).

## <a name="change-passwords"></a>Wachtwoorden wijzigen
Een HDInsight-cluster kan twee gebruikersaccounts hebben. de gebruikersaccount van de HDInsight-cluster (ook Hallo Gebruikersaccount HTTP) en Hallo SSH gebruikersaccount worden gemaakt tijdens het maken van een Hallo. U kunt Hallo Ambari web UI toochange Hallo cluster user account gebruikersnaam en wachtwoord script acties toochange Hallo SSH gebruikersaccount

### <a name="change-hello-cluster-user-password"></a>Wachtwoord gebruiker Hallo-cluster wijzigen
U kunt Hallo Ambari-Webgebruikersinterface toochange Hallo Cluster gebruikerswachtwoord gebruiken. toolog in tooAmbari, moet u Hallo bestaande cluster gebruikersnaam en wachtwoord gebruiken.

> [!NOTE]
> Veranderende Hallo cluster (admin) gebruikerswachtwoord kan ertoe leiden dat het script acties uitgevoerd op deze toofail cluster. Als u een persistente scriptacties die zijn gericht op worker-knooppunten hebt, mislukken deze scripts wanneer u knooppunten toohello cluster via formaat operations toevoegt. Zie voor meer informatie over scriptacties [aanpassen HDInsight-clusters met behulp van scriptacties](hdinsight-hadoop-customize-cluster-linux.md).
>
>

1. Meld u aan toohello Ambari-Webgebruikersinterface met Hallo gebruikersreferenties voor HDInsight-cluster. Hallo standaardgebruikersnaam **admin**. Hallo-URL is **https://&lt;de naam van de HDInsight-Cluster > azurehdinsight.net**.
2. Klik op **Admin** van Hallo bovenste menu en klik vervolgens op 'Ambari beheren'.
3. In het linkermenu hello, klikt u op **gebruikers**.
4. Klik op **Admin**.
5. Klik op **wachtwoord wijzigen**.

Ambari verandert vervolgens Hallo-wachtwoord op alle knooppunten in het Hallo-cluster.

### <a name="change-hello-ssh-user-password"></a>Wachtwoord wijzigen Hallo SSH-gebruiker
1. Hallo na tekst als een bestand met de naam met een teksteditor opslaan **changepassword.sh**.

   > [!IMPORTANT]
   > U moet een editor die gebruikmaakt van LF als Hallo regel beëindigen. Als Hallo editor CRLF gebruikt, vervolgens Hallo script werkt niet.
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. Upload Hallo tooa opslaglocatie die toegankelijk zijn vanuit HDInsight met behulp van een HTTP of HTTPS-adres. Bijvoorbeeld een bestand met een openbare opslaan zoals OneDrive of Azure Blob-opslag. Hallo URI (HTTP of HTTPS-adres) toohello bestand niet opslaan omdat deze URI in de volgende stap Hallo nodig is.
3. Hallo Azure-portal, klik op **HDInsight-Clusters**.
4. Klik op uw HDInsight-cluster.
4. Klik op **acties Script**.
4. Van Hallo **scriptacties** blade Selecteer **nieuwe indienen**. Wanneer Hallo **scriptactie indienen** blade wordt weergegeven, Voer Hallo volgende informatie:

   | Veld | Waarde |
   | --- | --- |
   | Naam |Ssh wachtwoord wijzigen |
   | Bash script URI |Hallo URI toohello changepassword.sh bestand |
   | Knooppunten (Head, Worker, Nimbus, leidinggevende, Zookeeper, enz.) |✓ voor alle knooppunttypen vermeld |
   | Parameters |Hallo SSH-gebruikersnaam en vervolgens Hallo nieuw wachtwoord invoeren. Er moet één spatie tussen Hallo-gebruikersnaam en het Hallo-wachtwoord. |
   | Deze scriptactie... |Laat dit veld uitgeschakeld. |
5. Selecteer **maken** tooapply Hallo script. Zodra het Hallo-script is voltooid, bent u kunnen tooconnect toohello cluster via SSH met het nieuwe wachtwoord Hallo.

## <a name="grantrevoke-access"></a>Toegang verlenen of in te trekken
HDInsight-clusters hebben Hallo HTTP-webservices (al deze services hebt RESTful eindpunten) te volgen:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Standaard worden deze services verleend om toegang te krijgen. U kunt in te trekken/verlenen toegang met behulp van Hallo [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) en [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).

## <a name="find-hello-subscription-id"></a>Hallo abonnements-ID vinden

**toofind uw Azure-abonnement id's**

1. Meld u aan toohello [Portal][azure-portal].
2. Klik op **abonnementen**. Elk abonnement heeft een naam en ID.

Elk cluster is gebonden tooan Azure-abonnement. abonnement-ID wordt weergegeven op de cluster Hallo Hallo **essentiële** tegel. Zie [lijst en geeft weer clusters](#list-and-show-clusters).

## <a name="find-hello-resource-group"></a>Hallo resourcegroep vinden
In de modus Azure Resource Manager Hallo elke HDInsight-cluster gemaakt met een Azure Resource Manager-groep. Hallo Resource Manager-groep die tooappears in deel uitmaakt van een cluster:

* Hallo clusterlijst heeft een **resourcegroep** kolom.
* Cluster **essentiële** tegel.  

Zie [lijst en geeft weer clusters](#list-and-show-clusters).

## <a name="find-hello-default-storage-account"></a>Hallo standaardopslagaccount vinden
Elke HDInsight-cluster heeft storage-standaardaccount. Hallo standaardopslagaccount en de sleutels voor een cluster wordt weergegeven onder **Opslagaccounts**. Zie [lijst en geeft weer clusters](#list-and-show-clusters).

## <a name="run-hive-queries"></a>Hive-query's uitvoeren
Hive-taak niet rechtstreeks vanuit hello Azure-portal kan niet worden uitgevoerd, maar u Hallo Hive-weergave op de Ambari-Webgebruikersinterface kunt gebruiken.

**toorun Hive-query's met Ambari Hive-weergave**

1. Meld u aan toohello Ambari-Webgebruikersinterface met Hallo gebruikersreferenties voor HDInsight-cluster. Hallo standaardgebruikersnaam **admin**. Hallo-URL is **https://&lt;de naam van de HDInsight-Cluster > azurehdinsight.net**.
2. Open de Hive-weergave zoals weergegeven in de volgende schermafbeelding Hallo:  

    ![HDInsight hive-weergave](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. Klik op **Query** in het bovenste menu Hallo.
4. Voer een Hive-query in **Query-Editor**, en klik vervolgens op **Execute**.

## <a name="monitor-jobs"></a>Taken controleren
Zie [HDInsight-clusters beheren met behulp van Hallo Ambari-Webgebruikersinterface](hdinsight-hadoop-manage-ambari.md#monitoring).

## <a name="browse-files"></a>Blader door bestanden
Hello Azure-portal kunt u inhoud van de standaardcontainer Hallo Hallo bladeren.

1. Aanmelden te[https://portal.azure.com](https://portal.azure.com).
2. Klik op **HDInsight-Clusters** van Hallo Hallo linkermenu toolist bestaande clusters.
3. Klik op de clusternaam Hallo. Als Hallo clusterlijst te lang is, kunt u filteren op Hallo Hallo pagina bovenaan.
4. Klik op **Opslagaccounts** vanuit het menu links Hallo-cluster.
5. Klik op een opslagaccount.
7. Klik op Hallo **Blobs** tegel.
8. Klik op de naam van de container standaard Hallo.

## <a name="monitor-cluster-usage"></a>Gebruik van het beeldscherm cluster
Hallo **gebruik** hello HDInsight-cluster-blade sectie geeft informatie weer over Hallo aantal kernen beschikbaar tooyour abonnement voor gebruik met HDInsight, evenals Hallo aantal kernen toothis cluster en hoe ze zijn toegewezen voor Hallo knooppunten binnen dit cluster toegewezen. Zie [lijst en geeft weer clusters](#list-and-show-clusters).

> [!IMPORTANT]
> toomonitor hello services geleverd door Hallo HDInsight-cluster, moet u de Ambari Web gebruiken of Hallo Ambari REST-API. Zie voor meer informatie over het gebruik van Ambari [HDInsight-clusters beheren met Ambari](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="connect-tooa-cluster"></a>Verbinding maken met cluster tooa

* [Hive gebruiken met HDInsight](hdinsight-hadoop-use-hive-ambari-view.md)
* [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd sommige functies basic administratieve. toolearn Zie meer Hallo artikelen te volgen:

* [HDInsight met behulp van Azure PowerShell beheren](hdinsight-administer-use-powershell.md)
* [Beheer van HDInsight Azure CLI gebruiken](hdinsight-administer-use-command-line.md)
* [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md)
* [Hive in HDInsight gebruiken](hdinsight-use-hive.md)
* [Pig gebruiken in HDInsight](hdinsight-use-pig.md)
* [Sqoop gebruiken in HDInsight](hdinsight-use-sqoop.md)
* [Aan de slag met Azure HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Welke versie van Hadoop is in Azure HDInsight?](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Hadoop-opdrachtregel"

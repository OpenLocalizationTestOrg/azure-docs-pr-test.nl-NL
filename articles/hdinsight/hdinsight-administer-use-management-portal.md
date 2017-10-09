---
title: aaaManage Windows gebaseerde Hadoop-clusters in HDInsight met behulp hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe tooadminister HDInsight-Service. Een HDInsight-cluster, open Hallo interactieve JavaScript-console en open Hallo Hadoop opdrachtconsole maken.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 9295a988-bd88-453a-8c8b-55fa103bf39c
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: a237726b0e37a08005ce22e96581739e93edb050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-based-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Hadoop op basis van Windows-clusters in HDInsight beheren met behulp van hello Azure-portal

Met behulp van Hallo [Azure-portal][azure-portal], u kunt Windows gebaseerde Hadoop-clusters maken in Azure HDInsight Hadoop-gebruikerswachtwoord wijzigen en enable Remote Desktop Protocol (RDP), zodat u toegang hebt tot Hallo Hadoop opdrachtconsole op Hallo-cluster.

Hallo-informatie in dit artikel is alleen van toepassing op basis van tooWindow HDInsight-clusters. Zie voor meer informatie over het beheren van clusters op basis van Linux [beheren Hadoop-clusters in HDInsight met behulp van Azure-portal Hallo](hdinsight-administer-use-portal-linux.md).

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.


## <a name="prerequisites"></a>Vereisten

Voordat u dit artikel, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Azure Storage-account** -An HDInsight cluster gebruikmaakt van een Azure Blob storage-container als het standaardbestandssysteem Hallo. Zie voor meer informatie over hoe Azure Blob-opslag een naadloze ervaring met HDInsight-clusters biedt [Azure Blob Storage gebruiken met HDInsight](hdinsight-hadoop-use-blob-storage.md). Zie voor meer informatie over het maken van een Azure Storage-account [hoe tooCreate een Opslagaccount](../storage/common/storage-create-storage-account.md).

## <a name="open-hello-portal"></a>Hallo Portal openen
1. Aanmelden te[https://portal.azure.com](https://portal.azure.com).
2. Nadat u Hallo portal opent, kunt u:

   * Klik op **nieuw** van Hallo linkermenu toocreate een nieuw cluster:

       ![knop Nieuw HDInsight-cluster](./media/hdinsight-administer-use-management-portal/azure-portal-new-button.png)
   * Klik op **HDInsight-Clusters** in het linkermenu Hallo.

       ![Knop Azure portal HDInsight-cluster](./media/hdinsight-administer-use-management-portal/azure-portal-hdinsight-button.png)

     Als **HDInsight** niet weergegeven in het linkermenu hello, klikt u op **Bladeren**.

     ![Azure portal cluster bladerknop](./media/hdinsight-administer-use-management-portal/azure-portal-browse-button.png)

## <a name="create-clusters"></a>Clusters maken
Zie voor Hallo maken instructies met Hallo Portal [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md).

HDInsight werkt met een breed bereik van Hadoop-onderdelen. Zie voor Hallo lijst Hallo-onderdelen die zijn geverifieerd en ondersteund [welke versie van Hadoop is in Azure HDInsight](hdinsight-component-versioning.md). U kunt HDInsight aanpassen met behulp van een Hallo volgende opties:

* Scriptactie toorun aangepaste scripts gebruiken die een tooeither cluster kunnen aanpassen clusterconfiguratie wijzigen of aangepaste onderdelen zoals Giraph of Solr installeren. Zie voor meer informatie [aanpassen HDInsight-cluster via scriptactie](hdinsight-hadoop-customize-cluster.md).
* Hallo cluster aanpassing parameters in Hallo HDInsight .NET SDK of Azure PowerShell gebruiken tijdens het maken van het cluster. Deze wijzigingen in de configuratie vervolgens blijven behouden via Hallo levensduur van Hallo-cluster en worden niet beïnvloed door cluster knooppunt reimages die Azure-platform regelmatig voor onderhoud uitvoert. Zie voor meer informatie over het gebruik van Hallo cluster aanpassing parameters [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md).
* Sommige systeemeigen Java-onderdelen, zoals Mahout en trapsgewijze, kunnen worden uitgevoerd op Hallo cluster als JAR-bestanden. Deze JAR-bestanden kunnen worden gedistribueerd tooAzure Blob-opslag en tooHDInsight clusters via Hadoop taak verzending mechanismen verzonden. Zie voor meer informatie [Hadoop verzenden via een programma taken](hdinsight-submit-hadoop-jobs-programmatically.md).

  > [!NOTE]
  > Als u problemen JAR-bestanden tooHDInsight clusters implementeren of als het aanroepen van de JAR-bestanden op HDInsight-clusters, neem contact op met [Microsoft Support](https://azure.microsoft.com/support/options/).
  >
  > Trapsgewijze bewerking wordt niet ondersteund door HDInsight en is niet in aanmerking komen voor Microsoft Support. Zie voor een lijst met ondersteunde onderdelen, [wat is er nieuw in Hallo-clusterversies geleverd door HDInsight](hdinsight-component-versioning.md).
  >
  >

Installatie van de aangepaste software op Hallo-cluster met behulp van de verbinding met extern bureaublad wordt niet ondersteund. Vermijd het opslaan van bestanden op Hallo-stations van hoofdknooppunt hello, omdat ze niet verloren als u nodig hebt toore-Hallo-clusters maken. Het is raadzaam bestanden opslaan op Azure Blob-opslag. BLOB-opslag is permanent.

## <a name="list-and-show-clusters"></a>Lijst en clusters weer te geven
1. Aanmelden te[https://portal.azure.com](https://portal.azure.com).
2. Klik op **HDInsight-Clusters** in het linkermenu Hallo.
3. Klik op de clusternaam Hallo. Als Hallo clusterlijst te lang is, kunt u filteren op Hallo Hallo pagina bovenaan.
4. Dubbelklik op een cluster met Hallo lijst tooshow Hallo details.

    **Menu en essentials**:

    ![Azure portal HDInsight-cluster essentials](./media/hdinsight-administer-use-management-portal/hdinsight-essentials.png)

   * toocustomize hello menu met de rechtermuisknop ergens op Hallo menu en klik vervolgens op **aanpassen**.
   * **Instellingen** en **alle instellingen**: Hiermee Hallo **instellingen** blade voor Hallo-cluster, zodat u tooaccess gedetailleerde configuratie-informatie voor Hallo-cluster.
   * **Dashboard**, **Cluster-Dashboard** en **URL: dit zijn alle manieren tooaccess Hallo cluster-dashboard, dat Ambari Web voor op basis van Linux-clusters. -**Secure Shell **: Toont Hallo instructies tooconnect toohello cluster met behulp van Secure Shell (SSH) verbinding.
   * **Cluster schalen**: Hiermee kunt u toochange Hallo aantal worker-knooppunten voor dit cluster.
   * **Verwijderen**: verwijderingen Hallo-cluster.
   * **Quick Start**: geeft informatie weer waarmee u kunt aan de slag met HDInsight.
   * ** Gebruikers: Hiermee kunt u machtigingen voor tooset *portal management* van dit cluster voor andere gebruikers op uw Azure-abonnement.

     > [!IMPORTANT]
     > Dit *alleen* is van invloed op toegang en machtigingen toothis cluster in hello Azure-portal en heeft geen effect op wie verbinding met tooor indienen taken toohello HDInsight-cluster maken kan.
     >
     >
   * **Labels**: labels kunt u tooset sleutel/waarde-paren toodefine een aangepaste taxonomie van uw cloud-services. Bijvoorbeeld, u kunt maken met een sleutel met de naam **project**, en gebruik vervolgens een overeenkomende waarde voor alle services die zijn gekoppeld aan een bepaald project.
   * **Ambari-weergaven**: tooAmbari Web koppelingen.

     > [!IMPORTANT]
     > toomanage hello services geleverd door Hallo HDInsight-cluster, moet u de Ambari Web gebruiken of Hallo Ambari REST-API. Zie voor meer informatie over het gebruik van Ambari [HDInsight-clusters beheren met Ambari](hdinsight-hadoop-manage-ambari.md).
     >
     >

     **Gebruik**:

     ![Gebruik Azure portal HDInsight-cluster](./media/hdinsight-administer-use-management-portal/hdinsight-portal-cluster-usage.png)
5. Klik op **instellingen**.

    ![Gebruik Azure portal HDInsight-cluster](./media/hdinsight-administer-use-management-portal/hdinsight.portal.cluster.settings.png)

   * **Eigenschappen**: Hallo clustereigenschappen weergeven.
   * **AAD-identiteit cluster**:
   * **Azure Storage-sleutels**: Hallo standaardopslagaccount en de bijbehorende sleutel weergeven. Hallo storage-account is de configuratie tijdens het Hallo-cluster maken.
   * **Aanmelding cluster**: Hallo cluster HTTP-gebruikersnaam en wachtwoord wijzigen.
   * **Met externe Metastores**: Hallo Hive en Oozie metastores weergeven. Hallo metastores kan alleen worden geconfigureerd tijdens het Hallo-cluster maken.
   * **Cluster schalen**: verhogen en de afname Hallo aantal worker clusterknooppunten.
   * **Extern bureaublad**: inschakelen en uitschakelen van toegang tot extern bureaublad (RDP) en Hallo RDP-gebruikersnaam configureren.  Hallo RDP-gebruikersnaam moet verschillen van Hallo HTTP-gebruikersnaam.
   * **Partner of Record**:

     > [!NOTE]
     > Dit is een algemene lijst met beschikbare instellingen; niet alle niet aanwezig is voor alle clustertypen.
     >
     >
6. Klik op **eigenschappen**:

    sectie met eigenschappen Hello wordt Hallo volgende weergegeven:

   * **Hostname**: de naam van het Cluster.
   * **Cluster-URL**.
   * **Status**: omvatten afgebroken, geaccepteerd, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, operationeel is, wordt uitgevoerd, fout, te verwijderen, verwijderd, time-out, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization
   * **Regio**: Azure-locatie. Zie voor een lijst van ondersteunde Azure locaties Hallo **regio** vervolgkeuzelijst op [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).
   * **Gegevens die zijn gemaakt**.
   * **Besturingssysteem**: beide **Windows** of **Linux**.
   * **Type**: Hadoop, HBase, Storm, Spark.
   * **Versie**. Zie [HDInsight-versies](hdinsight-component-versioning.md)
   * **Abonnement**: de naam van het abonnement.
   * **Abonnements-ID**.
   * **Primaire gegevensbron**. Hello Azure Blob storage-account gebruikt als Hallo standaard Hadoop-bestandssysteem.
   * **Worker-knooppunten prijscategorie**.
   * **Hoofdknooppunt prijscategorie**.

## <a name="delete-clusters"></a>Clusters verwijderen
Verwijderen van een cluster wordt niet verwijderd Hallo standaardopslagaccount of alle gekoppelde opslagaccounts weergegeven. U kunt Hallo cluster opnieuw maken met behulp van Hallo dezelfde opslagaccounts en metastores dezelfde Hallo.

1. Meld u aan toohello [Portal][azure-portal].
2. Klik op **door alles bladeren** in het linkermenu hello, klikt u op **HDInsight-Clusters**, klikt u op de clusternaam van uw.
3. Klik op **verwijderen** van Hallo bovenste menu en volg de instructies in Hallo.

Zie ook [onderbreken/afsluiten clusters](#pauseshut-down-clusters).

## <a name="scale-clusters"></a>Clusters schalen
Hallo-cluster schalen van functie kunt u toochange Hallo aantal worker-knooppunten gebruikt door een cluster dat wordt uitgevoerd in Azure HDInsight zonder toore-Hallo cluster maken.

> [!NOTE]
> Alleen clusters met HDInsight versie 3.1.3 of hoger worden ondersteund. Als u niet zeker Hallo versie van het cluster weet, kunt u de eigenschappenpagina Hallo controleren.  Zie [lijst en geeft weer clusters](#list-and-show-clusters).
>
>

Hallo gevolgen van het aantal gegevensknooppunten voor elk type ondersteund door HDInsight cluster Hallo wijzigen:

* Hadoop

    Hallo aantal worker-knooppunten van een Hadoop-cluster dat wordt uitgevoerd zonder enige impact op alle taken die in behandeling of wordt uitgevoerd, kunt u naadloos verhogen. Nieuwe taken kunnen ook worden verzonden tijdens het Hallo-bewerking wordt uitgevoerd. Fouten in een bewerking voor schaal worden probleemloos verwerkt zodat hello cluster altijd functioneel is overblijft.

    Wanneer een Hadoop-cluster wordt verkleind door het aantal gegevensknooppunten hello te verminderen, worden sommige services in de cluster Hallo Hallo opnieuw gestart. Dit zorgt ervoor dat alle actieve en in behandeling zijnde taken toofail op Hallo Hallo schalen van de bewerking is voltooid. U kunt echter Hallo taken verzenden zodra Hallo-bewerking voltooid is.
* HBase

    U kunt naadloos toevoegen of verwijderen van knooppunten tooyour HBase-cluster, terwijl deze wordt uitgevoerd. Regionale Servers worden automatisch verdeeld binnen een paar minuten na voltooiing van Hallo bewerking schalen. U kunt echter ook handmatig Hallo regionale servers verdelen door logboekregistratie in Hallo headnode van het cluster en actieve Hallo volgende opdrachten uit een opdrachtpromptvenster:

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

    ![HDInsight storm scale deel opnieuw](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)

    Hier volgt een voorbeeld hoe toouse Hallo CLI toorebalance Hallo Storm-topologie opdracht:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**tooscale clusters**

1. Meld u aan toohello [Portal][azure-portal].
2. Klik op **door alles bladeren** in het linkermenu hello, klikt u op **HDInsight-Clusters**, klikt u op de clusternaam van uw.
3. Klik op **instellingen** van Hallo bovenste menu en klik vervolgens op **Scale Cluster**.
4. Voer **nummer van Worker-knooppunten**. Hallo-limiet voor aantal clusterknooppunt Hallo verschilt per Azure-abonnementen. Neem contact op met facturering tooincrease hello ondersteuningslimiet.  kostengegevens Hallo bevatten Hallo aangebrachte wijzigingen toohello aantal knooppunten.

    ![HDInsight Hadoop HBase, Storm Spark schaal](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a>Onderbreken/clusters afsluiten
De meeste Hadoop-taken zijn batchtaken die alleen van tijd tot tijd worden uitgevoerd. Voor de meeste Hadoop-clusters, er zijn grote perioden tijd dat Hallo-cluster niet wordt gebruikt voor verwerking. Met HDInsight worden uw gegevens opgeslagen in Azure Storage zodat u een cluster veilig kunt verwijderen wanneer deze niet wordt gebruikt.
Voor een HDInsight-cluster worden ook kosten in rekening gebracht, zelfs wanneer het niet wordt gebruikt. Aangezien Hallo kosten voor Hallo cluster vaak zoveel hoger zijn dan Hallo kosten voor opslag, is het financieel aantrekkelijk toodelete clusters wanneer ze zich niet in gebruik.

Er zijn veel manieren u kunt programmeren Hallo proces:

* Gebruiker Azure Data Factory. Zie [gekoppelde Service van Azure HDInsight](../data-factory/data-factory-compute-linked-services.md) en [transformeren en analyseren met Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md) voor op aanvraag en zelf gedefinieerde HDInsight gekoppelde services.
* Azure PowerShell gebruiken.  Zie [analyseren vertraging vluchtgegevens](hdinsight-analyze-flight-delay-data.md).
* Azure CLI gebruiken. Zie [HDInsight-clusters beheren met Azure CLI](hdinsight-administer-use-command-line.md).
* HDInsight .NET SDK gebruiken. Zie [indienen Hadoop-taken](hdinsight-submit-hadoop-jobs-programmatically.md).

Zie voor Hallo prijsgegevens, [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/). een cluster met Hallo Portal toodelete Zie [clusters verwijderen](#delete-clusters)

## <a name="change-cluster-username"></a>Wijziging cluster gebruikersnaam
Een HDInsight-cluster kan twee gebruikersaccounts hebben. Hallo gebruikersaccount van de HDInsight-cluster wordt gemaakt tijdens het maken van een Hallo. U kunt ook een RDP-gebruikersaccount voor toegang tot cluster Hallo via RDP maken. Zie [extern bureaublad inschakelen](#connect-to-hdinsight-clusters-by-using-rdp).

**toochange hello HDInsight-cluster-gebruikersnaam en wachtwoord**

1. Meld u aan toohello [Portal][azure-portal].
2. Klik op **door alles bladeren** in het linkermenu hello, klikt u op **HDInsight-Clusters**, klikt u op de clusternaam van uw.
3. Klik op **instellingen** van Hallo bovenste menu en klik vervolgens op **Cluster aanmelding**.
4. Als **Cluster aanmelding** is ingeschakeld, klikt u op **uitschakelen**, en klik vervolgens op **inschakelen** voordat u Hallo gebruikersnaam en wachtwoord kunt wijzigen...
5. Wijziging Hallo **Cluster aanmeldingsnaam** en/of Hallo **Cluster aanmeldingswachtwoord**, en klik vervolgens op **opslaan**.

    ![HDInsight cluster gebruiker gebruikersnaam wachtwoord http gebruiker wijzigen](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="grantrevoke-access"></a>Toegang verlenen of in te trekken
HDInsight-clusters hebben Hallo HTTP-webservices (al deze services hebt RESTful eindpunten) te volgen:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Standaard worden deze services verleend om toegang te krijgen. U kunt in te trekken/verlenen toegang Hallo van hello Azure-portal.

> [!NOTE]
> Door het Hallo toegang verlenen/intrekken, wordt u opnieuw ingesteld Hallo cluster-gebruikersnaam en wachtwoord.
>
>

**toogrant of in te trekken HTTP services webtoegang**

1. Meld u aan toohello [Portal][azure-portal].
2. Klik op **door alles bladeren** in het linkermenu hello, klikt u op **HDInsight-Clusters**, klikt u op de clusternaam van uw.
3. Klik op **instellingen** van Hallo bovenste menu en klik vervolgens op **Cluster aanmelding**.
4. Als **Cluster aanmelding** is ingeschakeld, klikt u op **uitschakelen**, en klik vervolgens op **inschakelen** voordat u Hallo gebruikersnaam en wachtwoord kunt wijzigen...
5. Voor **Clusteraanmeldgegevens** en **Cluster aanmeldingswachtwoord**, (respectievelijk) Hallo nieuwe gebruikersnaam en wachtwoord invoeren voor Hallo-cluster.
6. Klik op **OPSLAAN**.

    ![HDInsight eindtotaal HTTP-web-Servicetoegang verwijderen](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="find-hello-default-storage-account"></a>Hallo standaardopslagaccount vinden
Elke HDInsight-cluster heeft storage-standaardaccount. Hallo standaardopslagaccount en de sleutels voor een cluster wordt weergegeven onder **instellingen**/**eigenschappen**/**Azure Opslagsleutels**. Zie [lijst en geeft weer clusters](#list-and-show-clusters).

## <a name="find-hello-resource-group"></a>Hallo resourcegroep vinden
In de modus Azure Resource Manager Hallo wordt elke HDInsight-cluster gemaakt met een Azure-resourcegroep. Hello Azure-resourcegroep die tooappears in deel uitmaakt van een cluster:

* Hallo clusterlijst heeft een **resourcegroep** kolom.
* Cluster **essentiële** tegel.  

Zie [lijst en geeft weer clusters](#list-and-show-clusters).

## <a name="open-hdinsight-query-console"></a>HDInsight-Query-console openen
Hallo HDInsight Query console bevat Hallo volgende kenmerken:

* **Hive-Editor**: een GUI-webinterface voor het indienen van Hive-taken.  Zie [uitvoeren Hive-query's met behulp van Hallo Query Console](hdinsight-hadoop-use-hive-query-console.md).

    ![HDInsight portal hive-editor](./media/hdinsight-administer-use-management-portal/hdinsight-hive-editor.png)
* **Taakgeschiedenis**: Monitor Hadoop-taken.  

    ![De portal Taakgeschiedenis HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-job-history.png)

    Klik op **querynaam** tooshow Hallo details taakeigenschappen, inclusief **Job Query**, en ** Taakuitvoer. U kunt ook query Hallo zowel Hallo uitvoer tooyour werkstation downloaden.
* **Bestand Browser**: bladeren Hallo storage-standaardaccount en Hallo gekoppelde opslagaccounts.

    ![Portal bladeren browser HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-file-browser.png)

    Hallo op Hallo-schermafbeelding  **<Account>**  type wordt aangegeven Hallo item is een Azure storage-account.  Klik op Hallo account naam toobrowse Hallo bestanden.
* **Hadoop-gebruikersinterface**.

    ![Portal HDInsight Hadoop UI](./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-ui.png)

    Van **Hadoop UI*, kunt u bladeren in bestanden en controleert u Logboeken.
* **Yarn UI**.

    ![YARN gebruikersinterface van de HDInsight-portal](./media/hdinsight-administer-use-management-portal/hdinsight-yarn-ui.png)

## <a name="run-hive-queries"></a>Hive-query's uitvoeren
tooran Hive-taken uit het Hallo-Portal klikt u op **Hive-Editor** in HDInsight Query Hallo-console. Zie [openen HDInsight Query console](#open-hdinsight-query-console).

## <a name="monitor-jobs"></a>Taken controleren
toomonitor taken van Hallo-Portal klikt u op **Taakgeschiedenis** in HDInsight Query Hallo-console. Zie [openen HDInsight Query console](#open-hdinsight-query-console).

## <a name="browse-files"></a>Blader door bestanden
toobrowse bestanden opgeslagen in het standaardopslagaccount hello en gekoppelde opslagaccounts hello, klikt u op **bestandsbrowser** in HDInsight Query Hallo-console. Zie [openen HDInsight Query console](#open-hdinsight-query-console).

U kunt ook Hallo **Hallo bestandssysteem** hulpprogramma van Hallo **Hadoop UI** in Hallo HDInsight-console.  Zie [openen HDInsight Query console](#open-hdinsight-query-console).

## <a name="monitor-cluster-usage"></a>Gebruik van het beeldscherm cluster
Hallo **gebruik** hello HDInsight-cluster-blade sectie geeft informatie weer over Hallo aantal kernen beschikbaar tooyour abonnement voor gebruik met HDInsight, evenals Hallo aantal kernen toothis cluster en hoe ze zijn toegewezen voor Hallo knooppunten binnen dit cluster toegewezen. Zie [lijst en geeft weer clusters](#list-and-show-clusters).

> [!IMPORTANT]
> toomonitor hello services geleverd door Hallo HDInsight-cluster, moet u de Ambari Web gebruiken of Hallo Ambari REST-API. Zie voor meer informatie over het gebruik van Ambari [HDInsight-clusters beheren met Ambari](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="open-hadoop-ui"></a>Open Hadoop-gebruikersinterface
toomonitor hello cluster bladeren Hallo-bestandssysteem en controleer de logboeken, klikt u op **Hadoop UI** in HDInsight Query Hallo-console. Zie [openen HDInsight Query console](#open-hdinsight-query-console).

## <a name="open-yarn-ui"></a>Yarn UI openen
toouse Yarn-gebruikersinterface, klikt u op **gebruikersinterface van Yarn** in HDInsight Query Hallo-console. Zie [openen HDInsight Query console](#open-hdinsight-query-console).

## <a name="connect-tooclusters-using-rdp"></a>Verbinding maken met RDP tooclusters
Hallo-referenties voor Hallo-cluster dat u hebt opgegeven bij het maken van de toegang toohello services op het Hallo-cluster, maar niet toohello cluster zelf via Extern bureaublad te geven. U kunt toegang tot extern bureaublad inschakelen wanneer u een cluster inrichten of nadat een cluster is ingericht. Zie voor instructies over het inschakelen van extern bureaublad bij het maken van Hallo [maken HDInsight-cluster](hdinsight-hadoop-provision-linux-clusters.md).

**tooenable extern bureaublad**

1. Meld u aan toohello [Portal][azure-portal].
2. Klik op **door alles bladeren** in het linkermenu hello, klikt u op **HDInsight-Clusters**, klikt u op de clusternaam van uw.
3. Klik op **instellingen** van Hallo bovenste menu en klik vervolgens op **extern bureaublad**.
4. Voer **verloopt op**, **gebruikersnaam voor extern bureaublad** en **extern bureaublad-wachtwoord**, en klik vervolgens op **inschakelen**.

    ![HDInsight uitschakelen extern bureaublad configureren](./media/hdinsight-administer-use-management-portal/hdinsight.portal.remote.desktop.png)

    Hallo-standaardwaarden voor verloopt op is een week.

   > [!NOTE]
   > U kunt ook Hallo HDInsight .NET SDK tooenable extern bureaublad gebruiken op een cluster. Gebruik Hallo **EnableRdp** methode op Hallo HDInsight clientobject in Hallo manier te volgen: **client. EnableRdp (clusternaam, locatie, 'rdpuser', 'rdppassword', DateTime.Now.AddDays(6))**. Op deze manier toodisable extern bureaublad op Hallo-cluster, kunt u **client. DisableRdp (clustername, locatie)**. Zie voor meer informatie over deze methoden [HDInsight .NET SDK-naslaginformatie](http://go.microsoft.com/fwlink/?LinkId=529017). Dit is alleen van toepassing op HDInsight-clusters met Windows.
   >
   >

**tooconnect tooa cluster via RDP**

1. Meld u aan toohello [Portal][azure-portal].
2. Klik op **door alles bladeren** in het linkermenu hello, klikt u op **HDInsight-Clusters**, klikt u op de clusternaam van uw.
3. Klik op **instellingen** van Hallo bovenste menu en klik vervolgens op **extern bureaublad**.
4. Klik op **Connect** en volg de instructies Hallo. Als Connect uitschakelen, moet u het eerst inschakelen. Zorg ervoor dat met Hallo extern bureaublad-gebruikersnaam en wachtwoord.  U kunt Hallo Cluster gebruikersreferenties niet gebruiken.

## <a name="open-hadoop-command-line"></a>Open Hadoop-opdrachtregel
tooconnect toohello cluster met behulp van extern bureaublad en gebruik Hallo Hadoop-opdrachtregel, u moet eerst hebt ingeschakeld extern bureaublad toegang toohello cluster zoals beschreven in de vorige sectie Hallo.

**tooopen een Hadoop-opdrachtregel**

1. Verbinding maken met extern bureaublad toohello-cluster.
2. Dubbelklik in het Hallo-bureaublad op **Hadoop-opdrachtregel**.

    ![HDI. HadoopCommandLine][image-hadoopcommandline]

    Zie voor meer informatie over Hadoop opdrachten [Hadoop opdrachten verwijzing](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).

In de vorige schermafbeelding Hallo heeft mapnaam Hallo Hallo Hadoop versienummer dat is ingesloten. Hallo-versienummer kunt gewijzigd op basis van Hallo-versie van Hallo Hadoop-onderdelen geïnstalleerd op Hallo-cluster. U kunt de Hadoop-omgeving variabelen toorefer toothose mappen. Bijvoorbeeld:

    cd %hadoop_home%
    cd %hive_home%
    cd %hbase_home%
    cd %pig_home%
    cd %sqoop_home%
    cd %hcatalog_home%

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe toocreate een HDInsight-cluster met behulp van de Portal Hallo en hoe tooopen Hallo Hadoop-opdrachtregelprogramma. toolearn Zie meer Hallo artikelen te volgen:

* [HDInsight met behulp van Azure PowerShell beheren](hdinsight-administer-use-powershell.md)
* [Beheer van HDInsight Azure CLI gebruiken](hdinsight-administer-use-command-line.md)
* [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md)
* [Hadoop-taken programmatisch verzenden](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Aan de slag met Azure HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Welke versie van Hadoop is in Azure HDInsight?](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-command-line.png "Hadoop-opdrachtregel"

---
title: aaaTips voor het gebruik van Hadoop op Linux gebaseerde HDInsight - Azure | Microsoft Docs
description: Implementatie tips voor het gebruik van HDInsight (Hadoop) op basis van Linux-clusters op een vertrouwde Linux-omgeving uitgevoerd in hello Azure-cloud.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c41c611c-5798-4c14-81cc-bed1e26b5609
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: a555622605079c9beae88ece872042e36d540c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="information-about-using-hdinsight-on-linux"></a>Informatie over het gebruik van HDInsight op Linux

Azure HDInsight-clusters bieden Hadoop op een vertrouwde Linux-omgeving worden uitgevoerd in hello Azure-cloud. Voor de meeste zaken werkt deze moet exact als elke andere Hadoop op Linux-installatie. Dit document is illustreert van specifieke verschillen die u houden moet rekening.

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a name="prerequisites"></a>Vereisten

Veel van de stappen in dit document hello gebruiken Hallo opdrachtregelprogramma's, die toobe op uw systeem geïnstalleerd wellicht te volgen.

* [cURL](https://curl.haxx.se/) -toocommunicate gebruikt met webservices
* [jq](https://stedolan.github.io/jq/) -gebruikt tooparse JSON-documenten
* [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (preview) - gebruikte tooremotely Azure-services beheren

## <a name="users"></a>Gebruikers

Tenzij [domein](hdinsight-domain-joined-introduction.md), HDInsight moet worden beschouwd als een **één gebruiker** system. Een SSH-account voor één gebruiker is gemaakt met de Hallo-cluster met administrator-niveau machtigingen. Aanvullende SSH-accounts kunnen worden gemaakt, maar ze hebben ook beheerder toegang toohello cluster.

Domein HDInsight biedt ondersteuning voor meerdere gebruikers en meer gedetailleerde instellingen voor machtigingen en de rol. Zie voor meer informatie [beheren domein HDInsight-clusters](hdinsight-domain-joined-manage.md).

## <a name="domain-names"></a>Domeinnamen

domain name (FQDN) toouse Hallo volledig gekwalificeerd bij het verbinden van toohello cluster van internet is Hallo  **&lt;clustername >. azurehdinsight.net** of (voor SSH)  **&lt;clustername-ssh >. azurehdinsight.net**.

Intern heeft elk knooppunt in de cluster Hallo een naam die is toegewezen tijdens de configuratie van het cluster. clusternamen toofind hello, Zie Hallo **Hosts** pagina op Hallo Ambari-Webgebruikersinterface. U kunt ook Hallo tooreturn een lijst met hosts uit Hallo Ambari REST-API te volgen:

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts" | jq '.items[].Hosts.host_name'

Vervang **wachtwoord** met Hallo Hallo beheerderaccount, wachtwoord en **CLUSTERNAME** met Hallo-naam van het cluster. Deze opdracht retourneert een JSON-document dat een lijst van Hallo hosts in Hallo cluster bevat. Jq is gebruikte tooextract hello `host_name` elementwaarde voor elke host.

Als u toofind Hallo-naam van Hallo knooppunt voor een bepaalde service moet, kunt u Ambari voor dat onderdeel opvragen. Bijvoorbeeld toofind Hallo hosts voor Hallo HDFS naam knooppunt Hallo volgende opdracht gebruiken:

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/NAMENODE" | jq '.host_components[].HostRoles.host_name'

Met deze opdracht retourneert een JSON-document met een beschrijving van Hallo-service en vervolgens jq ophaalt uit alleen Hallo `host_name` waarde voor Hallo-hosts.

## <a name="remote-access-tooservices"></a>Externe toegang tooservices

* **Ambari (web)** -https://&lt;clustername >. azurehdinsight.net

    Verifiëren met behulp van de gebruiker die beheerder Hallo cluster en het wachtwoord en meld u vervolgens aan tooAmbari.

    Verificatie is tekst zonder opmaak - altijd gebruik HTTPS toohelp voor zorgen dat Hallo verbinding veilig is.

    > [!IMPORTANT]
    > Sommige van de Hallo web UI beschikbaar via Ambari toegang knooppunten met de naam van een interne domein. Interne domein namen zijn niet openbaar toegankelijk zijn via internet Hallo. Het foutbericht 'de server is niet gevonden'-fouten bij het tooaccess sommige functies via Hallo Internet.
    >
    > toouse hello volledige functionaliteit van Hallo Ambari-webgebruikersinterface, een SSH-tunnel tooproxy web verkeer toohello hoofdknooppunt cluster gebruiken. Zie [SSH-Tunneling gebruiken tooaccess Ambari web-UI, ResourceManager JobHistory, NameNode, Oozie en andere web-UI](hdinsight-linux-ambari-ssh-tunnel.md)

* **Ambari (REST)** -https://&lt;clustername >.azurehdinsight.net/ambari

    > [!NOTE]
    > Verifiëren met behulp van de gebruiker die beheerder Hallo cluster en het wachtwoord.
    >
    > Verificatie is tekst zonder opmaak - altijd gebruik HTTPS toohelp voor zorgen dat Hallo verbinding veilig is.

* **WebHCat (Templeton)** -https://&lt;clustername >.azurehdinsight.net/templeton

    > [!NOTE]
    > Verifiëren met behulp van de gebruiker die beheerder Hallo cluster en het wachtwoord.
    >
    > Verificatie is tekst zonder opmaak - altijd gebruik HTTPS toohelp voor zorgen dat Hallo verbinding veilig is.

* **SSH** - &lt;clustername >-ssh.azurehdinsight.net op poort 22 of 23. Poort 22 is gebruikte tooconnect toohello primaire headnode, terwijl 23 gebruikte tooconnect toohello secundaire is. Zie voor meer informatie over de hoofdknooppunten Hallo [beschikbaarheid en betrouwbaarheid van Hadoop-clusters in HDInsight](hdinsight-high-availability-linux.md).

    > [!NOTE]
    > U kunt alleen toegang tot hoofdknooppunten Hallo-cluster via SSH vanaf een clientcomputer. Eenmaal zijn verbonden, kunt u met behulp van SSH uit een headnode Hallo worker-knooppunten benaderen.

## <a name="file-locations"></a>Bestandslocaties

Hadoop-gerelateerde bestanden vindt u op de clusterknooppunten Hallo op `/usr/hdp`. Deze map bevat Hallo submappen te volgen:

* **2.2.4.9-1**: Hallo mapnaam is versie Hallo Hallo Hortonworks Data Platform die door HDInsight worden gebruikt. Hallo-nummer op het cluster is mogelijk anders dan Hallo een hier vermeld.
* **huidige**: deze map bevat koppelingen toosubdirectories onder Hallo **2.2.4.9-1** directory. Deze map bestaat zodat er geen tooremember Hallo versienummer.

Van de voorbeeldgegevens en JAR-bestanden kunnen u vinden op Hadoop Distributed File System op `/example` en`/HdiSamples`

## <a name="hdfs-azure-storage-and-data-lake-store"></a>HDFS-, Azure-opslag- en Data Lake Store

In de meeste Hadoop-distributies HDFS ondersteund door de lokale opslag op Hallo virtuele machines in het Hallo-cluster. Lokale opslag kan worden voor een cloud-gebaseerde oplossing kostbare waar u in rekening worden gebracht per uur of per minuut voor rekenresources.

HDInsight gebruikt ofwel blobs in Azure Storage of Azure Data Lake Store als Hallo standaardarchief. Deze services bieden Hallo volgende voordelen:

* Goedkope langdurige opslag
* Toegankelijkheid van externe services zoals websites, bestand uploaden/downloaden van hulpprogramma's, verschillende SDK's van taal en webbrowsers

> [!WARNING]
> HDInsight biedt alleen ondersteuning voor __algemeen__ Azure Storage-accounts. Het ondersteunt momenteel geen Hallo __Blob storage__ accounttype.

Een Azure Storage-account kan bevatten up too4.75 TB, hoewel afzonderlijke blobs (of bestanden vanuit het perspectief van een HDInsight) alleen omhoog too195 GB kunnen gaan. Azure Data Lake Store kunnen worden uitgebreid dynamisch toohold trillions van bestanden, met afzonderlijke bestanden groter zijn dan een petabyte. Zie voor meer informatie [Understanding blobs](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) en [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).

Wanneer u Azure Storage of Data Lake Store, hebt u geen toodo iets speciale uit HDInsight tooaccess Hallo gegevens. Bijvoorbeeld, Hallo volgende opdracht geeft een lijst van bestanden in Hallo `/example/data` map ongeacht of deze wordt opgeslagen op Azure Storage of de Data Lake Store:

    hdfs dfs -ls /example/data

### <a name="uri-and-scheme"></a>URI- en schema

Sommige opdrachten moet u mogelijk toospecify Hallo schema als onderdeel van Hallo URI bij het openen van een bestand. Bijvoorbeeld, Hallo Storm-HDFS-component, moet u toospecify Hallo schema. Wanneer u de opslag van niet-standaard (opslag toegevoegd als 'Extra' opslagruimte toohello cluster), moet u altijd Hallo schema als onderdeel van Hallo URI gebruiken.

Wanneer u __Azure Storage__, gebruikt u een Hallo URI-schema's te volgen:

* `wasb:///`: Toegang standaard opslag met behulp van niet-gecodeerde communicatie.

* `wasbs:///`: Toegang standaard opslag met behulp van gecodeerde communicatie.  Hallo wasbs schema wordt alleen uit HDInsight versie 3.6 en hoger ondersteund.

* `wasb://<container-name>@<account-name>.blob.core.windows.net/`: Wordt gebruikt om te communiceren met een niet-standaard opslagaccount. Bijvoorbeeld, wanneer u hebt een extra storage-account of wanneer toegang tot gegevens opgeslagen in een openbaar toegankelijke storage-account.

Wanneer u __Data Lake Store__, gebruikt u een Hallo URI-schema's te volgen:

* `adl:///`: Toegang tot Hallo default Data Lake Store voor Hallo-cluster.

* `adl://<storage-name>.azuredatalakestore.net/`: Wordt gebruikt om te communiceren met een niet-standaard Data Lake Store. Ook tooaccess gegevens buiten de hoofdmap Hallo van uw HDInsight-cluster gebruikt.

> [!IMPORTANT]
> Wanneer u de Data Lake Store als Hallo standaardopslag voor HDInsight, moet u een pad binnen Hallo store toouse opgeven als de hoofdmap Hallo van HDInsight-opslag. het standaardpad Hallo is `/clusters/<cluster-name>/`.
>
> Wanneer u `/` of `adl:///` tooaccess gegevens, u kunt alleen toegang tot gegevens die zijn opgeslagen in de hoofdmap hello (bijvoorbeeld `/clusters/<cluster-name>/`) van Hallo-cluster. tooaccess gegevens overal in de Windows store voor hello gebruiken Hallo `adl://<storage-name>.azuredatalakestore.net/` indeling.

### <a name="what-storage-is-hello-cluster-using"></a>Welke opslag wordt gebruikt door Hallo cluster

Voor Hallo cluster kunt u Ambari tooretrieve Hallo standaardconfiguratie-opslag. Gebruik Hallo volgende opdracht tooretrieve HDFS-configuratiegegevens met curl en filteren met behulp van [jq](https://stedolan.github.io/jq/):

```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'```

> [!NOTE]
> Dit retourneert Hallo eerste toegepast toohello configuratieserver (`service_config_version=1`), die deze informatie bevat. U moet mogelijk toolist alle configuratieversies toofind Hallo recentste is.

Met deze opdracht retourneert een waarde van een vergelijkbare toohello URI's te volgen:

* `wasb://<container-name>@<account-name>.blob.core.windows.net`Als een Azure Storage-account wordt gebruikt.

    Hallo accountnaam heet Hallo hello Azure Storage-account, terwijl de containernaam Hallo Hallo blob-container die Hallo hoofdmap van de clusteropslag Hallo is.

* `adl://home`Als u Azure Data Lake Store. naam van tooget Hallo Data Lake Store, gebruik Hallo REST-aanroep te volgen:

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'```

    Met deze opdracht retourneert Hallo hostnaam te volgen: `<data-lake-store-account-name>.azuredatalakestore.net`.

    tooget hello map binnen Hallo store Hallo hoofdmap HDInsight, gebruik Hallo REST-aanroep te volgen:

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'```

    Met deze opdracht retourneert een pad vergelijkbare toohello in het pad naar: `/clusters/<hdinsight-cluster-name>/`.

U vindt ook Hallo storage-gegevens met behulp van hello Azure-portal met behulp van Hallo stappen te volgen:

1. In Hallo [Azure-portal](https://portal.azure.com/), selecteer uw HDInsight-cluster.

2. Van Hallo **eigenschappen** sectie **Opslagaccounts**. Hallo storage-gegevens voor Hallo cluster wordt weergegeven.

### <a name="how-do-i-access-files-from-outside-hdinsight"></a>Hoe krijg ik toegang tot bestanden uit buiten HDInsight

Er zijn een verschillende manieren tooaccess gegevens van buiten Hallo HDInsight-cluster. Hallo Hieronder volgen enkele koppelingen tooutilities en SDK's die gebruikt toowork met uw gegevens worden kunnen:

Als u __Azure Storage__, Zie Hallo koppelingen naar manieren of u toegang hebt tot uw gegevens te volgen:

* [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2): opdrachtregelinterface opdrachten voor het werken met Azure. Na het installeren, gebruiken Hallo `az storage` opdracht voor hulp bij het gebruik van opslag, of `az storage blob` voor blob-specifieke opdrachten.
* [blobxfer.PY](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage): een python-script voor het werken met blobs in Azure Storage.
* Verschillende SDK's:

    * [Java](https://github.com/Azure/azure-sdk-for-java)
    * [Node.js](https://github.com/Azure/azure-sdk-for-node)
    * [PHP](https://github.com/Azure/azure-sdk-for-php)
    * [Python](https://github.com/Azure/azure-sdk-for-python)
    * [Ruby](https://github.com/Azure/azure-sdk-for-ruby)
    * [.NET](https://github.com/Azure/azure-sdk-for-net)
    * [Opslag-REST-API](https://msdn.microsoft.com/library/azure/dd135733.aspx)

Als u __Azure Data Lake Store__, Zie Hallo koppelingen naar manieren of u toegang hebt tot uw gegevens te volgen:

* [Webbrowser](../data-lake-store/data-lake-store-get-started-portal.md)
* [PowerShell](../data-lake-store/data-lake-store-get-started-powershell.md)
* [Azure CLI 2.0](../data-lake-store/data-lake-store-get-started-cli-2.0.md)
* [WebHDFS REST-API](../data-lake-store/data-lake-store-get-started-rest-api.md)
* [Data Lake Tools voor Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)
* [.NET](../data-lake-store/data-lake-store-get-started-net-sdk.md)
* [Java](../data-lake-store/data-lake-store-get-started-java-sdk.md)
* [Python](../data-lake-store/data-lake-store-get-started-python.md)

## <a name="scaling"></a>Uw cluster schalen

Hallo-cluster schalen van functie kunt u toodynamically wijziging Hallo aantal gegevensknooppunten dat die worden gebruikt door een cluster. U kunt vergroten/verkleinen bewerkingen terwijl andere taken uitvoeren of processen worden uitgevoerd op een cluster.

Hallo verschillende clustertypen worden beïnvloed door de schaal als volgt:

* **Hadoop**: wanneer het aantal knooppunten in een cluster Hallo verkleinen, aantal Hallo-services in Hallo cluster opnieuw worden gestart. Schalen operations kan taken veroorzaken, actief of in behandeling toofail op Hallo Hallo schalen van de bewerking is voltooid. Zodra het Hallo-bewerking is voltooid, kunt u taken Hallo opnieuw indienen.
* **HBase**: regionale servers worden automatisch verdeeld binnen een paar minuten na voltooiing van Hallo bewerking schalen. toomanually saldo regionale servers, gebruikt u Hallo stappen te volgen:

    1. Toohello HDInsight-cluster via SSH verbinding. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

    2. Gebruik Hallo toostart hello HBase-shell te volgen:

            hbase shell

    3. Zodra het Hallo HBase-shell is geladen, gebruikt u Hallo toomanually saldo Hallo regionale servers te volgen:

            balancer

* **Storm**: U moet eventuele actieve Storm-topologieën opnieuw verdelen nadat een vergroten/verkleinen-bewerking is uitgevoerd. Herverdeling kunt Hallo topologie tooreadjust parallelle uitvoering instellingen op basis van nieuwe aantal knooppunten in cluster Hallo Hallo. toorebalance actieve topologieën, gebruikt u een Hallo volgende opties:

    * **SSH**: toohello server verbinden en gebruik Hallo volgende opdracht toorebalance een topologie:

            storm rebalance TOPOLOGYNAME

        U kunt ook parameters toooverride Hallo parallelle uitvoering hints oorspronkelijk is geleverd door Hallo-topologie opgeven. Bijvoorbeeld: `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` configureren Hallo topologie too5 werkprocessen, 3 Executor voor Hallo blauw spout onderdeel en 10 Executor voor Hallo geel bolt onderdeel.

    * **Storm-gebruikersinterface**: gebruik Hallo volgende stappen toorebalance een topologie met Hallo Storm-gebruikersinterface.

        1. Open **https://CLUSTERNAME.azurehdinsight.NET/stormui** in uw webbrowser, waarbij CLUSTERNAME Hallo-naam van uw Storm-cluster is. Typ desgevraagd Hallo HDInsight clusternaam beheerder (admin) en het wachtwoord die hebt opgegeven toen u Hallo-cluster.
        2. Selecteer Hallo topologie u wenst dat toorebalance en selecteer vervolgens Hallo **opnieuw verdelen** knop. Voer Hallo vertraging voordat Hallo deel opnieuw bewerking wordt uitgevoerd.

Zie voor specifieke informatie over het schalen van uw HDInsight-cluster:

* [Hadoop-clusters in HDInsight beheren met behulp van hello Azure-portal](hdinsight-administer-use-portal-linux.md#scale-clusters)
* [Hadoop-clusters in HDInsight met behulp van Azure PowerShell beheren](hdinsight-administer-use-command-line.md#scale-clusters)

## <a name="how-do-i-install-hue-or-other-hadoop-component"></a>Hoe installeer ik Hue (of andere onderdelen van Hadoop)?

HDInsight is een beheerde service. Als Azure een probleem met het Hallo-cluster detecteert, mogelijk verwijderen Hallo knooppunt mislukt en maken van een knooppunt tooreplace deze. Als u handmatig dingen op Hallo-cluster installeert, worden ze niet behouden als deze bewerking doet zich. Gebruik in plaats daarvan [HDInsight scriptacties](hdinsight-hadoop-customize-cluster.md). Een scriptactie kan gebruikte toomake Hallo volgende wijzigingen zijn:

* Installeren en configureren van een service of de website zoals Spark of Hue.
* Installeren en configureren van een onderdeel dat wijzigingen in de configuratie op meerdere knooppunten in cluster Hallo vereist. Een vereiste omgeving-variabele, maken van een map voor logboekregistratie of maken van een configuratiebestand.

Scriptacties zijn Bash-scripts. Hallo-scripts uitvoeren tijdens de clusterinrichting, en worden de gebruikte tooinstall en extra onderdelen op Hallo cluster configureren. Voorbeeldscripts zijn beschikbaar voor het installeren van Hallo volgende onderdelen:

* [HUE](hdinsight-hadoop-hue-linux.md)
* [Giraph](hdinsight-hadoop-giraph-install-linux.md)
* [Solr](hdinsight-hadoop-solr-install-linux.md)

Zie [Ontwikkeling van scriptacties met HDInsight](hdinsight-hadoop-script-actions-linux.md) voor informatie over het ontwikkelen van uw eigen scriptacties.

### <a name="jar-files"></a>JAR-bestanden

Bij sommige technologieën Hadoop vindt u in zelfstandige jar-bestanden met functies die worden gebruikt als onderdeel van een MapReduce-taak of in Pig- of Hive. Terwijl deze kunnen worden geïnstalleerd met behulp van scriptacties, kunnen ze vaak geen geen installatie vereist en geüploade toohello cluster na het inrichten en rechtstreeks worden gebruikt. Als u ervoor Hallo-onderdeel toomake blijft teruggezet van Hallo-cluster wilt, kunt u Hallo jar-bestand opslaan in Hallo standaard opslag voor uw cluster (WASB of ADL).

Bijvoorbeeld, als u wilt dat de meest recente versie van toouse Hallo van [DataFu](http://datafu.incubator.apache.org/), kunt u een jar met Hallo-project downloaden en upload het toohello HDInsight-cluster. Volg Hallo DataFu documentatie over het toouse uit Pig of Hive.

> [!IMPORTANT]
> Sommige onderdelen die zelfstandige jar-bestanden zijn worden voorzien van HDInsight, maar zijn niet in het Hallo-pad. Als u naar een specifiek onderdeel zoekt, kunt u Hallo Volg toosearch voor op het cluster:
>
> ```find / -name *componentname*.jar 2>/dev/null```
>
> Met deze opdracht retourneert Hallo pad van alle overeenkomende jar-bestanden.

toouse een andere versie van een component uploaden Hallo versie u nodig hebt en deze gebruiken in uw taken.

> [!WARNING]
> Onderdelen van Hallo HDInsight-cluster worden volledig ondersteund en Microsoft Support helpt tooisolate en oplossen van problemen toothese verwante onderdelen.
>
> Aangepaste onderdelen ontvangen binnen commercieel redelijke ondersteuning toohelp u toofurther Hallo probleem op te lossen. Dit kan leiden tot het oplossen van Hallo probleem of vragen dat u tooengage beschikbare kanalen voor Hallo openen bron technologieën waar grondige kennis van deze technologie kan worden gevonden. Bijvoorbeeld: Er zijn veel community-sites die kunnen worden gebruikt, zoals: [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Ook hebben Apache projecten project-sites op [http://apache.org](http://apache.org), bijvoorbeeld: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).

## <a name="next-steps"></a>Volgende stappen

* [Migreren van HDInsight op basis van Windows op basis van tooLinux](hdinsight-migrate-from-windows-to-linux.md)
* [Hive gebruiken met HDInsight](hdinsight-use-hive.md)
* [Pig gebruiken met HDInsight](hdinsight-use-pig.md)
* [MapReduce-taken gebruiken met HDInsight](hdinsight-use-mapreduce.md)

---
title: aaaAnalyze sensorgegevens met Apache Storm en HBase | Microsoft Docs
description: Meer informatie over hoe tooconnect tooApache Storm met een virtueel netwerk. Storm gebruiken met HBase tooprocess sensorgegevens van een event hub en deze te visualiseren met D3.js.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a>Analyseren van sensorgegevens met Apache Storm, Event Hub en HBase in HDInsight (Hadoop)

Meer informatie over hoe toouse Apache Storm op HDInsight tooprocess sensorgegevens uit Azure Event Hub. Hallo gegevens vervolgens naar Apache HBase in HDInsight wordt opgeslagen en weergegeven met behulp van D3.js.

Hello Azure Resource Manager-sjabloon die wordt gebruikt in dit document wordt gedemonstreerd hoe toocreate meerdere Azure-resources in een resourcegroep. Hallo-sjabloon maakt u een Azure-netwerk, twee HDInsight-clusters (Storm en HBase) en een Azure-Web-App. Een node.js-implementatie van een realtime webdashboard is automatisch geïmplementeerd toohello web-app.

> [!NOTE]
> Hallo-informatie in dit document en deze in dit document HDInsight versie 3.6 vereisen.
>
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a name="prerequisites"></a>Vereisten

* Een Azure-abonnement.
* [Node.js](http://nodejs.org/): gebruikte toopreview Hallo webdashboard lokaal op uw ontwikkelomgeving.
* [Java- en Hallo JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): toodevelop Hallo Storm-topologie wordt gebruikt.
* [Maven](http://maven.apache.org/what-is-maven.html): gebruikte toobuild en compileren Hallo-project.
* [GIT](http://git-scm.com/): gebruikte toodownload Hallo project vanuit GitHub.
* Een **SSH** client: tooconnect toohello Linux gebaseerde HDInsight-clusters gebruikt. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.


> [!IMPORTANT]
> U hoeft niet in een bestaand HDInsight-cluster. Hallo stappen in dit document maken Hallo resources te volgen:
> 
> * Een Azure-netwerk
> * Een Storm op HDInsight-cluster (op basis van Linux twee worker-knooppunten)
> * Een HBase op HDInsight-cluster (op basis van Linux twee worker-knooppunten)
> * Een Azure-Web-App die als host fungeert voor Hallo webdashboard

## <a name="architecture"></a>Architectuur

![Architectuurdiagram](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

In dit voorbeeld bestaat uit Hallo volgende onderdelen:

* **Azure Event Hubs**: bevat gegevens die worden verzameld van sensoren.
* **Storm op HDInsight**: biedt realtime verwerking van gegevens uit Event Hub.
* **HBase in HDInsight**: biedt een permanente NoSQL-gegevensopslag voor gegevens nadat deze is verwerkt door Storm.
* **Azure Virtual Network service**: beveiligde communicatie tussen Hallo Storm op HDInsight en HBase op HDInsight-clusters mogelijk maakt.
  
  > [!NOTE]
  > Een virtueel netwerk is vereist wanneer Hallo Java HBase client-API. Het is niet toegankelijk via openbare gateway Hallo voor HBase-clusters. Installeren HBase en Storm-clusters in hetzelfde virtuele netwerk kunt Hallo Hallo Storm-cluster (of elk ander systeem in het virtuele netwerk Hallo) toodirectly toegang tot HBase met client-API.

* **Dashboard website**: een voorbeeld van dashboard dat gegevens in real-time grafieken.
  
  * Hallo-website is geïmplementeerd in Node.js.
  * [Socket.IO](http://socket.io/) wordt gebruikt voor realtime-communicatie tussen Hallo Storm-topologie en Hallo-website.
    
    > [!NOTE]
    > Met Socket.io voor communicatie is een implementatiedetail. U kunt elk framework communicatie zoals onbewerkte WebSockets of SignalR gebruiken.

  * [D3.js](http://d3js.org/) gebruikte toograph Hallo gegevens dat toohello website wordt verzonden.

> [!IMPORTANT]
> Twee clusters zijn vereist, omdat er geen ondersteunde methode toocreate een HDInsight-cluster voor Storm en HBase.

Hallo topologie leest de gegevens uit Event Hub met behulp van Hallo [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) klasse en schrijft gegevens in HBase met Hallo [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) de klasse. Communicatie met de Hallo website kan worden bereikt via [socket.io client.java](https://github.com/nkzawa/socket.io-client.java).

Hallo volgende diagram wordt uitgelegd Hallo lay-out van Hallo-topologie:

![topologiediagram](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> Dit diagram is een vereenvoudigde weergave van Hallo-topologie. Een exemplaar van elk onderdeel is gemaakt voor elke partitie in uw Event Hub. Deze instanties zijn verdeeld over Hallo knooppunten in cluster Hallo en gegevens worden gerouteerd tussen deze als volgt:
> 
> * Gegevens van Hallo spout toohello parser gelijkmatig wordt verdeeld.
> * Gegevens uit het Hallo-parser toohello Dashboard en HBase worden gegroepeerd per apparaat-ID, zodat berichten van hetzelfde apparaat altijd Hallo stromen toohello hetzelfde onderdeel.

### <a name="topology-components"></a>Topologie-onderdelen

* **Event Hub Spout**: Hallo spout is opgegeven als onderdeel van Apache Storm versie 0.10.0 of hoger.
  
  > [!NOTE]
  > Hallo Event Hub spout gebruikt in dit voorbeeld is een Storm op HDInsight-cluster versie 3.5 of 3.6 vereist.

* **ParserBolt.java**: Hallo gegevens dat is verzonden door Hallo spout onbewerkte JSON en van tijd tot tijd meer dan een gebeurtenis op een tijdstip is verzonden. Deze bolt leest Hallo-gegevens die door Hallo spout en parseert JSON het Hallo-bericht. Hallo bolt verzendt vervolgens Hallo gegevens als een tuple die meerdere velden bevat.
* **DashboardBolt.java**: dit onderdeel wordt gedemonstreerd hoe toouse Hallo Socket.io-clientbibliotheek voor Java toosend gegevens in realtime toohello webdashboard.
* **Er is geen hbase.yaml**: Hallo topologie definitie wanneer in lokale modus uitgevoerd. Het wordt HBase-onderdelen gebruikt.
* **met hbase.yaml**: Hallo topologie definitie gebruikt bij het uitvoeren van Hallo topologie op Hallo-cluster. Dit maakt gebruik van HBase-onderdelen.
* **dev.Properties**: Hallo van configuratie-informatie voor Hallo Event Hub spout, HBase bolt en dashboard onderdelen.

## <a name="prepare-your-environment"></a>Uw omgeving voorbereiden

Voordat u dit voorbeeld gebruiken, moet u een Azure Event Hub, welke Hallo Storm-topologie leest uit.

### <a name="configure-event-hub"></a>Event Hub configureren

Event Hub is Hallo gegevensbron voor dit voorbeeld. Volgende stappen toocreate een Event Hub hello gebruiken.

1. Van Hallo [Azure-portal](https://portal.azure.com), selecteer **+ nieuw** -> **Internet der dingen** -> **Event Hubs**.
2. In Hallo **Namespace maken** sectie, Hallo volgende taken uitvoeren:
   
   1. Voer een **naam** voor Hallo-naamruimte.
   2. Selecteer een prijscategorie. **Basic** voldoende is voor dit voorbeeld.
   3. Selecteer hello Azure **abonnement** toouse.
   4. Selecteer een bestaande resourcegroep of maak een nieuwe.
   5. Selecteer Hallo **locatie** voor Hallo Event Hub.
   6. Selecteer **pincode toodashboard**, en klik vervolgens op **maken**.

3. Wanneer het proces voor het maken van Hallo is voltooid, wordt Hallo Event Hubs-informatie voor uw naamruimte weergegeven. Hier kunt u selecteren **+ Event Hub toevoegen**. In Hallo **Event Hub maken** sectie, voer een naam in van **sensordata**, en selecteer vervolgens **maken**. Laat Hallo andere velden op Hallo standaardwaarden.
4. Hallo Event Hubs bekijken voor de naamruimte, selecteer **Event Hubs**. Selecteer Hallo **sensordata** vermelding.
5. Selecteer in de Hallo sensordata Event Hub, **gedeeld toegangsbeleid**. Gebruik Hallo **+ toevoegen** koppeling tooadd Hallo beleidsregels te volgen:

    | De naam van beleid | Claims |
    | ----- | ----- |
    | apparaten | Verzenden |
    | storm | Luisteren |

1. Selecteer beide beleidsregels en noteer Hallo **primaire sleutel** waarde. Hallo-waarde vereist voor beide beleidsregels in toekomstige stappen.

## <a name="download-and-configure-hello-project"></a>Downloaden en configureren van Hallo-project

Gebruik hello toodownload Hallo project vanuit GitHub te volgen.

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

Nadat het Hallo-opdracht is voltooid, hebt u Hallo directory-structuur te volgen:

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> Dit document verder niet in toofull details van Hallo code is opgenomen in dit voorbeeld. Hallo-code is echter volledig toegelicht.

tooconfigure hello project tooread van Event Hub, open Hallo `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` bestands- en uw Event Hub informatie toohello volgende regels toevoegen:

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a>Compileren en lokaal te testen

> [!IMPORTANT]
> Hallo-topologie lokaal, moet een werkende Storm-ontwikkelomgeving. Zie voor meer informatie [een Storm-ontwikkelomgeving instellen](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) op Apache.org.

> [!WARNING]
> Als u van een Windows-ontwikkelomgeving gebruikmaakt, ontvangt u mogelijk een `java.io.IOException` wanneer Hallo-topologie die lokaal wordt uitgevoerd. Zo ja, verder toorunning Hallo-topologie op HDInsight.

Voordat u test, moet u Hallo dashboard tooview Hallo uitvoer van de topologie Hallo starten en genereren van gegevens toostore in de Event Hub.

> [!IMPORTANT]
> Hallo HBase-onderdeel van deze topologie is niet actief bij lokaal te testen. Hallo Java API voor Hallo HBase-cluster niet toegankelijk vanuit externe hello Azure Virtual Network die Hallo-clusters bevat.

### <a name="start-hello-web-application"></a>Hallo-webtoepassing starten

1. Open een opdrachtprompt en wijzig de mappen te`hdinsight-eventhub-example/dashboard`. Hallo opdracht tooinstall Hallo afhankelijkheden die nodig is voor de webtoepassing Hallo volgende gebruiken:
   
    ```bash
    npm install
    ```

2. Gebruik Hallo opdracht toostart Hallo-webtoepassing te volgen:
   
    ```bash
    node server.js
    ```
   
    U ziet een bericht vergelijkbaar toohello volgende tekst:
   
        Server listening at port 3000

3. Open een webbrowser en voer `http://localhost:3000/` als Hallo-adres. Een pagina vergelijkbaar toohello volgende afbeelding wordt weergegeven:
   
    ![webdashboard](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    Laat deze opdrachtprompt geopend. Nadat u hebt getest, Ctrl-C toostop Hallo webserver te gebruiken.

### <a name="generate-data"></a>Gegevens moeten genereren

> [!NOTE]
> Hallo stappen in deze sectie gebruiken Node.js zodat ze kunnen worden gebruikt op elk platform. Zie voor andere voorbeelden taal Hallo `SendEvents` directory.

1. Open een nieuw opdrachtprompt, shell of terminal en wijzig de mappen te`hdinsight-eventhub-example/SendEvents/nodejs`. tooinstall hello afhankelijkheden die nodig is voor de toepassing hello, Hallo volgende opdracht gebruiken:

    ```bash
    npm install
    ```

2. Open Hallo `app.js` bestand in een teksteditor en voeg Hallo Event Hub-informatie die u eerder hebt verkregen:
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > In dit voorbeeld wordt ervan uitgegaan dat u hebt gebruikt `sensordata` als Hallo-naam van uw Event Hub. En dat `devices` als Hallo-naam van het Hallo-beleid dat is een `Send` claim.

3. Gebruik Hallo opdracht tooinsert nieuwe vermeldingen in de Event Hub te volgen:
   
    ```bash
    node app.js
    ```
   
    Ziet u meerdere regels van uitvoer met Hallo gegevens verzonden tooEvent Hub:
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-hello-topology"></a>Bouwen en starten Hallo-topologie

1. Open een nieuw opdrachtpromptvenster en wijzig de mappen te`hdinsight-eventhub-example/TemperatureMonitor`. toobuild en pakket Hallo topologie, Hallo volgende opdracht gebruiken: 

    ```bash
    mvn clean package
    ```

2. toostart Hallo topologie in lokale modus, Hallo volgende opdracht gebruiken:

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * `--local`Hallo-topologie start in de lokale modus.
    * `--filter`maakt gebruik van Hallo `dev.properties` toopopulate parameters in de definitie van de topologie Hallo bestand.
    * `resources/no-hbase.yaml`maakt gebruik van Hallo `no-hbase.yaml` topologie definitie.
 
   Eenmaal gestart, Hallo topologie vermeldingen van Event Hub leest en verzendt deze toohello dashboard op uw lokale computer uitgevoerd. Hier ziet u regels worden weergegeven in Hallo webdashboard vergelijkbare toohello installatiekopie te volgen:
   
    ![dashboard met gegevens](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. Terwijl Hallo dashboard wordt uitgevoerd, gebruikt u Hallo `node app.js` opdracht van een vorige Hallo stappen toosend nieuwe gegevens tooEvent Hubs. Omdat Hallo temperatuur waarden worden willekeurig gegenereerd, moet Hallo grafiek tooshow grote veranderingen in de temperatuur bijwerken.
   
   > [!NOTE]
   > U moet zich in Hallo **hdinsight-eventhub-voorbeeld/SendEvents/Nodejs** directory wanneer u Hallo `node app.js` opdracht.

3. Nadat u hebt gecontroleerd dat dashboard Hallo-updates, stop Hallo-topologie met Ctrl + C. U kunt ook Hallo lokale webserver met Ctrl + C toostop gebruiken.

## <a name="create-a-storm-and-hbase-cluster"></a>Een Storm en HBase-cluster maken

Hallo stappen in dit gedeelte een [Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md) toocreate een virtueel Azure-netwerk en een Storm en HBase-cluster op Hallo virtueel netwerk. Hallo sjabloon wordt ook een Azure-Web-App maakt en implementeert een kopie van het Hallo-dashboard in de App.

> [!NOTE]
> Een virtueel netwerk wordt gebruikt zodat Hallo topologie uitgevoerd op Hallo Storm-cluster kan rechtstreeks communiceren met de Hallo Hallo HBase Java API met HBase-cluster.

Hallo Resource Manager-sjabloon die wordt gebruikt in dit document bevindt zich in een openbare blob-container op **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.

1. Klik op Hallo na de knop toosign in tooAzure en open Hallo Resource Manager-sjabloon in hello Azure-portal.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Van Hallo **aangepaste implementatie** sectie, voert u Hallo volgende waarden:
   
    ![HDInsight-parameters](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * **Clusternaam baseren**: deze waarde wordt gebruikt als basisnaam van Hallo voor Hallo Storm en HBase-clusters. Bijvoorbeeld, voeren **abc** maakt een Storm-cluster met de naam **storm abc** en een HBase-cluster met de naam **hbase abc**.
   * **Aanmeldingsnaam van gebruiker cluster**: Hallo-beheerdersgebruikersnaam voor Hallo Storm en HBase-clusters.
   * **Aanmeldingswachtwoord cluster**: Hallo beheerder gebruikerswachtwoord voor Hallo Storm en HBase-clusters.
   * **SSH-gebruikersnaam**: Hallo SSH gebruiker toocreate voor Hallo Storm en HBase-clusters.
   * **SSH-wachtwoord**: Hallo-wachtwoord voor Hallo SSH-gebruiker voor Hallo Storm en HBase-clusters.
   * **Locatie**: Hallo regio die in Hallo clusters worden gemaakt.
     
     Klik op **OK** toosave Hallo parameters.

3. Gebruik Hallo **basisbeginselen** sectie toocreate een resourcegroep of een bestaande set selecteren.
4. In Hallo **locatie voor resourcegroep** Selecteer vervolgkeuzemenu Hallo dezelfde locatie als u hebt geselecteerd voor Hallo **locatie** parameter in Hallo **instellingen** sectie.
5. Hallo voorwaarden lezen en selecteer vervolgens **ik ga akkoord toohello voorwaarden bovengenoemde**.
6. Controleer ten slotte **pincode toodashboard** en selecteer vervolgens **aankoop**. Het duurt ongeveer 20 minuten toocreate Hallo-clusters.

Zodra het Hallo-resources zijn gemaakt, wordt informatie over de resourcegroep Hallo weergegeven.

![De resourcegroep voor Hallo vnet en clusters](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> Merk op dat de namen van HDInsight-clusters Hallo Hallo zijn **storm BASENAME** en **hbase BASENAME**, waarbij BASENAME Hallo-naam die u hebt opgegeven toohello sjabloon. U gebruikt deze namen in een latere stap bij het verbinden van toohello clusters. Let op: naam van dashboard-site Hallo Hallo is ook **basename dashboard**. Deze waarde wordt verderop in dit document gebruikt.

## <a name="configure-hello-dashboard-bolt"></a>Hallo Dashboard bolt configureren

toosend gegevens toohello dashboard geïmplementeerd als een web-app, moet u volgt regel in Hallo Hallo wijzigen `dev.properties`bestand:

```yaml
dashboard.uri: http://localhost:3000
```

Wijziging `http://localhost:3000` te`http://BASENAME-dashboard.azurewebsites.net` en Hallo-bestand op te slaan. Vervang **BASENAME** met Hallo basisnaam u hebt opgegeven in de vorige stap Hallo. U kunt ook Hallo resourcegroep tooselect Hallo dashboard en de weergave Hallo URL eerder hebt gemaakt.

## <a name="create-hello-hbase-table"></a>Hallo HBase-tabel maken

toostore gegevens in HBase, moeten we eerst een tabel maken. Vooraf resources die Storm toowrite te moet maken, zoals het toocreate resources uit binnen een Storm-topologie kunnen leiden tot meerdere exemplaren probeert toocreate Hallo dezelfde resource. Hallo bronnen buiten Hallo topologie maken en gebruiken van Storm voor lezen/schrijven en analyses.

1. Gebruik SSH tooconnect toohello HBase-cluster met Hallo SSH-gebruiker en het wachtwoord u toohello sjabloon tijdens het maken van het cluster hebt opgegeven. Bijvoorbeeld, als u verbinding maakt met behulp van Hallo `ssh` opdracht, zou u Hallo syntaxis gebruikt:
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    Vervang `sshuser` met Hallo SSH-gebruikersnaam die u hebt opgegeven bij het maken van Hallo-cluster. Vervang `clustername` met de naam van een Hallo HBase-cluster.

2. Start op Hallo SSH-sessie, Hallo HBase-shell.
   
    ```bash
    hbase shell
    ```
   
    Nadat het Hallo-shell is geladen, ziet u een `hbase(main):001:0>` prompt.

3. Voer van Hallo HBase-shell, Hallo opdracht toocreate een sensorgegevens tabel toostore hello te volgen:
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. Controleer of dat deze Hallo-tabel is gemaakt met behulp van de volgende opdracht Hallo:
   
    ```hbase
    scan 'SensorData'
    ```
   
    Hiermee wordt informatie vergelijkbare toohello voorbeeld te volgen, wat betekent dat er 0 rijen in de tabel Hallo geretourneerd.
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. Voer `exit` tooexit hello HBase-shell:

## <a name="configure-hello-hbase-bolt"></a>Hallo HBase bolt configureren

toowrite tooHBase van Hallo Storm-cluster, moet u Hallo HBase bolt opgeven met de Hallo-configuratiegegevens van uw HBase-cluster.

1. Gebruik een van de Hallo volgen voorbeelden tooretrieve hello Zookeeper quorum voor uw HBase-cluster:

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > Vervang `your_HDInsight_cluster_name` met Hallo-naam van uw HDInsight-cluster. Voor meer informatie over het installeren van Hallo `jq` hulpprogramma, Zie [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).
    >
    > Wanneer u wordt gevraagd, moet u Hallo wachtwoord opgeven voor Hallo HDInsight admin aanmelden.

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > Vervang ' your_HDInsight_cluster_name met Hallo-naam van uw HDInsight-cluster. Wanneer u wordt gevraagd, moet u Hallo wachtwoord opgeven voor Hallo HDInsight admin aanmelden.
    >
    > Dit voorbeeld vereist Azure PowerShell. Zie voor meer informatie over het gebruik van Azure PowerShell [aan de slag met Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)

    Hallo-informatie die wordt geretourneerd door deze voorbeelden is vergelijkbaar toohello volgende tekst:

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    Deze informatie wordt gebruikt door Storm toocommunicate met Hallo HBase-cluster.

2. Hallo wijzigen `dev.properties` bestands- en Hallo Zookeeper quorum informatie toohello volgt regel toevoegen:

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a>Bouwen, pakket, en Hallo oplossing tooHDInsight implementeren

Gebruik in uw ontwikkelomgeving Hallo stappen toodeploy Hallo Storm-topologie toohello storm-cluster te volgen.

1. Van Hallo `TemperatureMonitor` map gebruik Hallo volgende opdracht tooperform een nieuwe build en een JAR-pakket maken van uw project:
   
        mvn clean package
   
    Deze opdracht maakt u een bestand met de naam `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `doel ' map van uw project.

2. Gebruik scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` en `dev.properties` bestanden tooyour Storm-cluster. Hallo volgt, Vervang in `sshuser` met Hallo SSH gebruiker die u hebt opgegeven bij het maken van Hallo-cluster, en `clustername` met Hallo-naam van uw Storm-cluster. Wanneer u wordt gevraagd, moet u Hallo wachtwoord opgeven voor Hallo SSH-gebruiker.
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > Het kan enkele minuten duren tooupload Hallo-bestanden.

    Voor meer informatie over het gebruik van Hallo `scp` en `ssh` opdrachten met HDInsight, Zie [SSH gebruiken met HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)

3. Zodra het Hallo-bestand zijn geüpload, verbinding maken met toohello Storm-cluster via SSH.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Vervang `sshuser` met Hallo SSH-gebruikersnaam. Vervang `clustername` met de naam van een Hallo Storm-cluster.

4. toostart Hallo topologie, na de opdracht van de SSH-sessie Hallo hello gebruiken:
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * `--remote`Hallo-topologie toohello Nimbus-service, die u het toohello supervisor knooppunten in cluster Hallo distribueert verzendt.
    * `--filter`maakt gebruik van Hallo `dev.properties` toopopulate parameters in de definitie van de topologie Hallo bestand.
    * `-R /with-hbase.yaml`maakt gebruik van Hallo `with-hbase.yaml` topologie in Hallo pakket opgenomen.

5. Nadat het Hallo-topologie is gestart, opent u een browser toohello-website die u hebt gepubliceerd in Azure, vervolgens gebruik Hallo `node app.js` opdracht toosend gegevens tooEvent Hub. U ziet Hallo web dashboard toodisplay Hallo updategegevens.
   
    ![dashboard](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a>HBase-gegevens weergeven

Volgende stappen tooconnect tooHBase hello gebruiken en controleer of dat Hallo gegevens toohello tabel is geschreven:

1. SSH tooconnect toohello HBase-cluster gebruiken.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Vervang `sshuser` met Hallo SSH-gebruikersnaam. Vervang `clustername` met de naam van een Hallo HBase-cluster.

2. Start op Hallo SSH-sessie, Hallo HBase-shell.
   
    ```bash
    hbase shell
    ```
   
    Nadat het Hallo-shell is geladen, ziet u een `hbase(main):001:0>` prompt.

3. Weergave rijen uit de tabel Hallo:
   
    ```hbase
    scan 'SensorData'
    ```
   
    Deze opdracht retourneert informatie vergelijkbare toohello tekst te volgen, die aangeeft dat er gegevens in de tabel Hallo.
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > Deze scanbewerking retourneert maximaal 10 rijen uit Hallo tabel.

## <a name="delete-your-clusters"></a>Uw clusters verwijderen

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toodelete hello clusters-, opslag- en web-app in één keer Hallo resourcegroep waarin ze te verwijderen.

## <a name="next-steps"></a>Volgende stappen

Zie voor meer voorbeelden van Storm-topologieën met HDInsight [voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md)

Zie voor meer informatie over de Apache Storm Hallo [Apache Storm](https://storm.incubator.apache.org/) site.

Zie voor meer informatie over HBase in HDInsight hello [HBase met HDInsight Overview](hdinsight-hbase-overview.md).

Zie voor meer informatie over Socket.io hello [socket.io](http://socket.io/) site.

Zie voor meer informatie over D3.js [D3.js - documenten met aangestuurd](http://d3js.org/).

Zie voor meer informatie over het maken van topologieën in Java [ontwikkelen van Java-topologieën voor Apache Storm op HDInsight](hdinsight-storm-develop-java-topology.md).

Zie voor meer informatie over het maken van topologieën in .NET [C#-topologieën ontwikkelen voor Apache Storm op HDInsight met behulp van Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

[azure-portal]: https://portal.azure.com

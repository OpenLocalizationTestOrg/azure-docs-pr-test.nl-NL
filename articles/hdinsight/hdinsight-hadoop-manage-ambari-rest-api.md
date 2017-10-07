---
title: aaaMonitor en beheren van Hadoop met Ambari REST-API - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Ambari toomonitor en beheren in Azure HDInsight Hadoop-clusters. In dit document leert u hoe toouse hello Ambari REST-API die deel uitmaakt van een HDInsight-clusters.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2400530f-92b3-47b7-aa48-875f028765ff
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 1866a77c8e402231bccbcfba7174253aca41339b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a>HDInsight-clusters beheren met behulp van Hallo Ambari REST-API

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Ontdek hoe toouse Hallo toomanage Ambari REST-API en bewaken in Azure HDInsight Hadoop-clusters.

Apache Ambari vereenvoudigt het Hallo-beheer en bewaking van een Hadoop-cluster met een eenvoudig toouse web UI en REST-API. Ambari is opgenomen op HDInsight-clusters die gebruikmaken van Hallo Linux-besturingssysteem. U kunt Ambari toomonitor Hallo cluster gebruiken en configuratiewijzigingen aanbrengen.

## <a id="whatis"></a>Wat is Ambari

[Apache Ambari](http://ambari.apache.org) biedt webgebruikersinterface die kunnen worden gebruikt tooprovision, beheren en bewaken van Hadoop-clusters. Ontwikkelaars kunnen deze mogelijkheden integreren in hun toepassingen met behulp van Hallo [Ambari REST-API's](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

Ambari is opgegeven met HDInsight op basis van Linux-clusters standaard.

## <a name="how-toouse-hello-ambari-rest-api"></a>Hoe toouse Hallo Ambari REST-API

> [!IMPORTANT]
> Hallo informatie en voorbeelden in dit document moeten een HDInsight-cluster dat gebruik maakt van Linux-besturingssysteem. Zie voor meer informatie [aan de slag met HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

Hallo-voorbeelden in dit document zijn bedoeld voor zowel Hallo Willemsen shell (bash) en PowerShell. Hallo bash voorbeelden zijn getest met GNU 4.3.11 bash, maar moet samen met andere houders Unix. Hallo PowerShell-voorbeelden zijn getest met PowerShell 5.0, maar moeten samenwerken met PowerShell 3.0 of hoger.

Als u Hallo __Bourne shell__ (Bash), hebt u volgende Hallo zijn geïnstalleerd:

* [cURL](http://curl.haxx.se/): cURL is een hulpprogramma dat gebruikt toowork met REST-API's vanaf de opdrachtregel Hallo worden kan. In dit document is het gebruikte toocommunicate Hello Ambari REST-API.

Of Bash of PowerShell gebruikt, moet u ook hebt [jq](https://stedolan.github.io/jq/) geïnstalleerd. Jq is een hulpprogramma voor het werken met JSON-documenten. Het wordt gebruikt in **alle** Hallo Bash-voorbeelden en **één** van Hallo PowerShell-voorbeelden.

### <a name="base-uri-for-ambari-rest-api"></a>Basis-URI voor de Ambari Rest API

Hallo basis-URI voor Hallo Ambari REST-API op HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, waarbij **CLUSTERNAME** Hallo-naam van uw cluster.

> [!IMPORTANT]
> Hoewel de clusternaam Hallo in Hallo FQDN domain name (FQDN) deel van Hallo URI (CLUSTERNAME.azurehdinsight.net) is niet hoofdlettergevoelig, andere voorvallen in Hallo URI zijn hoofdlettergevoelig. Bijvoorbeeld, als de naam van uw cluster `MyCluster`, Hallo volgen geldige URI's:
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> Hallo volgende URI's retourneren een foutmelding omdat Hallo tweede exemplaar van het Hallo-naam is geen Hallo corrigeren geval.
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a>Authentication

Verbinding maken met tooAmbari op HDInsight HTTPS is vereist. Gebruik Hallo beheerder accountnaam (Hallo standaardwaarde is **admin**) en het wachtwoord die u hebt opgegeven tijdens het maken van het cluster.

## <a name="examples-authentication-and-parsing-json"></a>Voorbeelden: Verificatie en bij het parseren van JSON

Hallo volgen voorbeelden laten zien hoe een GET-aanvraag tegen Hallo toomake baseren Ambari REST-API:

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> Hallo Bash voorbeelden in dit document zorg Hallo veronderstellingen te volgen:
>
> * Hallo aanmeldingsnaam voor Hallo-cluster is de standaardwaarde Hallo van `admin`.
> * `$PASSWORD`Hallo-wachtwoord voor Hallo HDInsight aanmelding opdracht bevat. U kunt deze waarde instellen met behulp van `PASSWORD='mypassword'`.
> * `$CLUSTERNAME`Hallo-naam van Hallo cluster bevat. U kunt deze waarde instellen door gebruik te maken`set CLUSTERNAME='clustername'`

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> Hallo PowerShell-voorbeelden in dit document zorg Hallo veronderstellingen te volgen:
>
> * `$creds`is een referentieobject dat Hallo beheerder aanmeldingsnaam en het wachtwoord voor Hallo cluster bevat. U kunt deze waarde instellen met behulp van `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` en Hallo referenties opgeeft wanneer u wordt gevraagd.
> * `$clusterName`is een tekenreeks die Hallo-naam van het Hallo-cluster bevat. U kunt deze waarde instellen met behulp van `$clusterName="clustername"`.

Beide voorbeelden retourneren een JSON-document dat begint met informatie vergelijkbare toohello voorbeeld te volgen:

```json
{
"href" : "http://10.0.0.10:8080/api/v1/clusters/CLUSTERNAME",
"Clusters" : {
    "cluster_id" : 2,
    "cluster_name" : "CLUSTERNAME",
    "health_report" : {
    "Host/stale_config" : 0,
    "Host/maintenance_state" : 0,
    "Host/host_state/HEALTHY" : 7,
    "Host/host_state/UNHEALTHY" : 0,
    "Host/host_state/HEARTBEAT_LOST" : 0,
    "Host/host_state/INIT" : 0,
    "Host/host_status/HEALTHY" : 7,
    "Host/host_status/UNHEALTHY" : 0,
    "Host/host_status/UNKNOWN" : 0,
    "Host/host_status/ALERT" : 0
    ...
```

### <a name="parsing-json-data"></a>Bij het parseren van JSON-gegevens

Hallo volgende voorbeeld wordt `jq` tooparse Hallo JSON-document van antwoord en weer te geven alleen Hallo `health_report` informatie uit Hallo resultaten.

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

PowerShell 3.0 en hoger biedt Hallo `ConvertFrom-Json` cmdlet, waarmee de JSON-document Hallo converteert naar een object dat is eenvoudiger toowork met vanuit PowerShell. Hallo volgende voorbeeld wordt `ConvertFrom-Json` toodisplay alleen Hallo `health_report` informatie uit Hallo resultaten.

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> Tijdens het meeste voorbeelden in dit document `ConvertFrom-Json` toodisplay elementen uit Hallo antwoorddocument Hallo [Update Ambari configuratie](#example-update-ambari-configuration) voorbeeld jq wordt gebruikt. Jq wordt gebruikt in dit voorbeeld tooconstruct een nieuwe sjabloon uit Hallo JSON-antwoord-document.

Zie voor een volledig overzicht van Hallo REST-API [Ambari-API-verwijzing V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a>Voorbeeld: Hallo FQDN-naam van de clusterknooppunten ophalen

Als u werkt met HDInsight, moet u mogelijk tooknow Hallo volledig gekwalificeerde domeinnaam (FQDN) van een clusterknooppunt. U kunt eenvoudig ophalen Hallo FQDN voor Hallo verschillende knooppunten in het Hallo-cluster met behulp van Hallo volgen voorbeelden:

* **Alle knooppunten**

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* **HEAD-knooppunten**

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* **Worker-knooppunten**

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* **Zookeeper-knooppunten**

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a>Voorbeeld: Hallo interne IP-adres van de clusterknooppunten ophalen

> [!IMPORTANT]
> Hallo IP-adressen die wordt geretourneerd door Hallo voorbeelden in deze sectie zijn niet rechtstreeks toegankelijk via internet Hallo. Ze zijn alleen toegankelijk vanuit hello Azure Virtual Network die Hallo HDInsight-cluster bevat.
>
> Zie voor meer informatie over het werken met HDInsight en virtuele netwerken [mogelijkheden uitbreiden HDInsight met behulp van een aangepaste Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).

toofind hello IP-adres, moet u weten Hallo interne volledig gekwalificeerde domeinnaam (FQDN) van Hallo clusterknooppunten. Zodra u Hallo FQDN hebt, kunt u vervolgens Hallo IP-adres van de host Hallo ophalen. Hallo volgende voorbeelden eerst Hallo FQDN-naam van de knooppunten van de host alle Hallo Ambari zoeken en vervolgens Ambari zoeken naar Hallo IP-adres van elke host.

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

```powershell
$uri = "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts"
$resp = Invoke-WebRequest -Uri $uri -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
foreach($item in $respObj.items) {
    $hostName = [string]$item.Hosts.host_name
    $hostInfoResp = Invoke-WebRequest -Uri "$uri/$hostName" `
        -Credential $creds
    $hostInfoObj = ConvertFrom-Json $hostInfoResp 
    $hostIp = $hostInfoObj.Hosts.ip
    "$hostName <--> $hostIp"
}
```

## <a name="example-get-hello-default-storage"></a>Voorbeeld: Hallo standaard opslag ophalen

Wanneer u een HDInsight-cluster maakt, moet u een Azure Storage-Account of een Data Lake Store als Hallo standaard opslag voor Hallo-cluster. U kunt de Ambari tooretrieve deze gegevens nadat Hallo-cluster is gemaakt. Bijvoorbeeld als u wilt dat tooread schrijftijd gegevenscontainer toohello buiten HDInsight.

Hallo ophalen volgende voorbeelden Hallo standaard opslagconfiguratie uit Hallo-cluster:

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> Deze voorbeelden retourneren Hallo eerste toegepast toohello configuratieserver (`service_config_version=1`) die deze informatie bevat. Als u een waarde die is gewijzigd na het maken van het cluster ophaalt, mag u toolist hello configuratieversies moet en ophalen van de meest recente Hallo.

Hallo-retourwaarde is vergelijkbaar tooone Hallo volgen voorbeelden:

* `wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Deze waarde geeft aan dat cluster hello Azure Storage-account voor de opslag van de standaard. Hallo `ACCOUNTNAME` waarde is de naam Hallo van Hallo storage-account. Hallo `CONTAINER` gedeelte Hallo-naam van Hallo blob-container in Hallo storage-account is. Hallo-container bevat Hallo Hallo HDFS compatibel opslagruimte voor Hallo-cluster.

* `adl://home`-Deze waarde geeft aan dat Hallo-cluster gebruikmaakt van een Azure Data Lake Store voor standaard-opslag.

    toofind hello Data Lake Store-accountnaam, gebruik Hallo volgen voorbeelden:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    Hallo retourwaarde lijkt te`ACCOUNTNAME.azuredatalakestore.net`, waarbij `ACCOUNTNAME` heet Hallo Hallo Data Lake Store-account.

    toofind hello map in Data Lake Store met Hallo opslagruimte voor Hallo-cluster, gebruik Hallo volgen voorbeelden:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    Hallo retourwaarde lijkt te`/clusters/CLUSTERNAME/`. Deze waarde is een pad binnen Hallo Data Lake Store-account. Dit pad bevat Hallo Hallo HDFS-compatibele bestandssysteem voor Hallo-cluster. 

> [!NOTE]
> Hallo `Get-AzureRmHDInsightCluster` cmdlet geleverd door [Azure PowerShell](/powershell/azure/overview) ook retourneert Hallo storage-gegevens voor Hallo-cluster.


## <a name="example-get-configuration"></a>Voorbeeld: Get-configuratie

1. Hallo-configuraties die beschikbaar voor uw cluster zijn ophalen.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    Het volgende voorbeeld wordt een JSON-document met de huidige configuratie Hallo (aangeduid met Hallo *tag* waarde) voor Hallo-onderdelen geïnstalleerd op Hallo-cluster. Hallo is volgende voorbeeld een fragment uit het Hallo-gegevens geretourneerd van een type Spark-cluster.
   
   ```json
   "spark-metrics-properties" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-fairscheduler" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-sparkconf" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   }
   ```

2. Hallo-configuratie voor Hallo-onderdeel dat u geïnteresseerd bent in ophalen. Hallo volgt, Vervang in `INITIAL` met Hallo tag geretourneerde waarde van de vorige aanvraag Hallo.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    Het volgende voorbeeld wordt een JSON-document met de huidige configuratie Hallo voor Hallo `core-site` onderdeel.

## <a name="example-update-configuration"></a>Voorbeeld: Update-configuratie

1. De huidige configuratie hello, waardoor de Ambari worden opgeslagen als Hallo 'gewenste configuratie' ophalen:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    Het volgende voorbeeld wordt een JSON-document met de huidige configuratie Hallo (aangeduid met Hallo *tag* waarde) voor Hallo-onderdelen geïnstalleerd op Hallo-cluster. Hallo is volgende voorbeeld een fragment uit het Hallo-gegevens geretourneerd van een type Spark-cluster.
   
    ```json
    "spark-metrics-properties" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-fairscheduler" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-sparkconf" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    }
    ```
   
    In deze lijst, moet u toocopy Hallo-naam van het Hallo-onderdeel (bijvoorbeeld **spark\_thrift\_sparkconf** en Hallo **tag** waarde.

2. Hallo-configuratie voor het Hallo-onderdeel en de tag ophalen met behulp van de volgende opdrachten Hallo:
   
    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
    | jq --arg newtag $(echo version$(date +%s%N)) '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    ```powershell
    $epoch = Get-Date -Year 1970 -Month 1 -Day 1 -Hour 0 -Minute 0 -Second 0
    $now = Get-Date
    $unixTimeStamp = [math]::truncate($now.ToUniversalTime().Subtract($epoch).TotalMilliSeconds)
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=spark-thrift-sparkconf&tag=INITIAL" `
        -Credential $creds
    $resp.Content | jq --arg newtag "version$unixTimeStamp" '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    > [!NOTE]
    > Vervang **spark-thrift-sparkconf** en **INITIËLE** met Hallo-onderdeel en code die u wilt dat tooretrieve Hallo configuratie voor.
   
    Jq is gebruikte tooturn Hallo gegevens opgehaald uit HDInsight naar een nieuwe configuratiesjabloon. Deze voorbeelden uitvoeren in het bijzonder Hallo van de volgende activiteiten:
   
    * Hiermee maakt u een unieke waarde met de Hallo tekenreeks '-versie en datum hello, dat is opgeslagen in `newtag`.

    * Maakt een document hoofdmap voor de nieuwe gewenste configuratie Hallo.

    * Haalt inhoud Hallo Hallo `.items[]` matrix en voegt deze toe onder Hallo **desired_config** element.

    * Hiermee verwijdert u Hallo `href`, `version`, en `Config` elementen, als deze elementen zijn niet nodig toosubmit een nieuwe configuratie.

    * Voegt een `tag` element met een waarde van `version#################`. het numerieke gedeelte Hallo is gebaseerd op Hallo huidige datum. Elke configuratie moet een unieke code hebben.
     
    Ten slotte Hallo gegevens opgeslagen toohello `newconfig.json` document. de documentstructuur Hallo moet worden weergegeven vergelijkbaar toohello voorbeeld te volgen:
     
     ```json
    {
        "Clusters": {
            "desired_config": {
            "tag": "version1459260185774265400",
            "type": "spark-thrift-sparkconf",
            "properties": {
                ....
            },
            "properties_attributes": {
                ....
            }
        }
    }
    ```

3. Open Hallo `newconfig.json` waarden document en wijzigen/toevoegen in Hallo `properties` object. Hallo volgende voorbeeld wijzigingen Hallo waarde van `"spark.yarn.am.memory"` van `"1g"` te`"3g"`. Voegt ook `"spark.kryoserializer.buffer.max"` met een waarde van `"256m"`.
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    Hallo-bestand opslaan als u klaar bent wijzigingen aanbrengen.

4. Gebruik Hallo opdrachten toosubmit Hallo bijgewerkt configuratie tooAmbari te volgen.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
    ```

    ```powershell
    $newConfig = Get-Content .\newconfig.json
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body $newConfig
    $resp.Content
    ```
   
    Deze opdrachten verzenden Hallo inhoud Hallo **newconfig.json** toohello cluster bestand zoals Hallo nieuwe configuratie gewenst. Hallo aanvraag retourneert een JSON-document. Hallo **versionTag** element in dit document moet overeenkomen met de Hallo versie hebt verzonden Hallo **configs** object bevat Hallo-configuratiewijzigingen die u hebt aangevraagd.

### <a name="example-restart-a-service-component"></a>Voorbeeld: Start opnieuw op een serviceonderdeel

Op dit punt als u Hallo Ambari-webgebruikersinterface bekijkt, Hallo Spark-service geeft aan dat deze opnieuw worden opgestart moet voordat de nieuwe configuratie Hallo van kracht toobe. Volgende stappen toorestart Hallo service Hallo gebruiken.

1. Gebruik Hallo tooenable onderhoudsmodus voor Hallo Spark-service te volgen:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}'
    $resp.Content
    ```
   
    Deze opdrachten verzenden een JSON-document toohello server Hiermee schakelt u onderhoudsmodus. U kunt controleren Hallo-service is nu in de onderhoudsmodus met Hallo aanvraag te volgen:
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    Hallo retourwaarde is `ON`.

2. Gebruik vervolgens Hallo tooturn Hallo-service uit te volgen:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}'
    $resp.Content
    ```
    
    Hallo-antwoord is vergelijkbaar toohello voorbeeld te volgen:
   
    ```json
    {
        "href" : "http://10.0.0.18:8080/api/v1/clusters/CLUSTERNAME/requests/29",
        "Requests" : {
            "id" : 29,
            "status" : "Accepted"
        }
    }
    ```
    
    > [!IMPORTANT]
    > Hallo `href` waarde die door deze URI geretourneerd met behulp van interne IP-adres van het clusterknooppunt Hallo Hallo. toouse via externe Hallo-cluster, '10.0.0.18:8080' hello gedeelte vervangen door Hallo FQDN-naam van het Hallo-cluster. 
    
    Hallo opdrachten na Hallo status van aanvraag Hallo niet ophalen:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    Een antwoord van `COMPLETED` geeft aan dat Hallo-aanvraag is voltooid.

3. Zodra de vorige aanvraag Hallo is voltooid, gebruik Hallo toostart Hallo service te volgen.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```
   
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}'
    ```
    Hallo-service maakt nu gebruik van de nieuwe configuratie Hallo.

4. Gebruik tot slot Hallo tooturn uit de onderhoudsmodus te volgen.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}'
    ```

## <a name="next-steps"></a>Volgende stappen

Zie voor een volledig overzicht van Hallo REST-API [Ambari-API-verwijzing V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).


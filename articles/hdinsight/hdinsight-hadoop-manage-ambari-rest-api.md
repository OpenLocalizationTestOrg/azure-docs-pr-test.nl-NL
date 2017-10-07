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
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a><span data-ttu-id="68fee-104">HDInsight-clusters beheren met behulp van Hallo Ambari REST-API</span><span class="sxs-lookup"><span data-stu-id="68fee-104">Manage HDInsight clusters by using hello Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="68fee-105">Ontdek hoe toouse Hallo toomanage Ambari REST-API en bewaken in Azure HDInsight Hadoop-clusters.</span><span class="sxs-lookup"><span data-stu-id="68fee-105">Learn how toouse hello Ambari REST API toomanage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="68fee-106">Apache Ambari vereenvoudigt het Hallo-beheer en bewaking van een Hadoop-cluster met een eenvoudig toouse web UI en REST-API.</span><span class="sxs-lookup"><span data-stu-id="68fee-106">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="68fee-107">Ambari is opgenomen op HDInsight-clusters die gebruikmaken van Hallo Linux-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="68fee-107">Ambari is included on HDInsight clusters that use hello Linux operating system.</span></span> <span data-ttu-id="68fee-108">U kunt Ambari toomonitor Hallo cluster gebruiken en configuratiewijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="68fee-108">You can use Ambari toomonitor hello cluster and make configuration changes.</span></span>

## <span data-ttu-id="68fee-109"><a id="whatis"></a>Wat is Ambari</span><span class="sxs-lookup"><span data-stu-id="68fee-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="68fee-110">[Apache Ambari](http://ambari.apache.org) biedt webgebruikersinterface die kunnen worden gebruikt tooprovision, beheren en bewaken van Hadoop-clusters.</span><span class="sxs-lookup"><span data-stu-id="68fee-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used tooprovision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="68fee-111">Ontwikkelaars kunnen deze mogelijkheden integreren in hun toepassingen met behulp van Hallo [Ambari REST-API's](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="68fee-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="68fee-112">Ambari is opgegeven met HDInsight op basis van Linux-clusters standaard.</span><span class="sxs-lookup"><span data-stu-id="68fee-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-toouse-hello-ambari-rest-api"></a><span data-ttu-id="68fee-113">Hoe toouse Hallo Ambari REST-API</span><span class="sxs-lookup"><span data-stu-id="68fee-113">How toouse hello Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68fee-114">Hallo informatie en voorbeelden in dit document moeten een HDInsight-cluster dat gebruik maakt van Linux-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="68fee-114">hello information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="68fee-115">Zie voor meer informatie [aan de slag met HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="68fee-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="68fee-116">Hallo-voorbeelden in dit document zijn bedoeld voor zowel Hallo Willemsen shell (bash) en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68fee-116">hello examples in this document are provided for both hello Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="68fee-117">Hallo bash voorbeelden zijn getest met GNU 4.3.11 bash, maar moet samen met andere houders Unix.</span><span class="sxs-lookup"><span data-stu-id="68fee-117">hello bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="68fee-118">Hallo PowerShell-voorbeelden zijn getest met PowerShell 5.0, maar moeten samenwerken met PowerShell 3.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="68fee-118">hello PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="68fee-119">Als u Hallo __Bourne shell__ (Bash), hebt u volgende Hallo zijn geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="68fee-119">If using hello __Bourne shell__ (Bash), you must have hello following installed:</span></span>

* <span data-ttu-id="68fee-120">[cURL](http://curl.haxx.se/): cURL is een hulpprogramma dat gebruikt toowork met REST-API's vanaf de opdrachtregel Hallo worden kan.</span><span class="sxs-lookup"><span data-stu-id="68fee-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used toowork with REST APIs from hello command line.</span></span> <span data-ttu-id="68fee-121">In dit document is het gebruikte toocommunicate Hello Ambari REST-API.</span><span class="sxs-lookup"><span data-stu-id="68fee-121">In this document, it is used toocommunicate with hello Ambari REST API.</span></span>

<span data-ttu-id="68fee-122">Of Bash of PowerShell gebruikt, moet u ook hebt [jq](https://stedolan.github.io/jq/) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="68fee-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="68fee-123">Jq is een hulpprogramma voor het werken met JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="68fee-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="68fee-124">Het wordt gebruikt in **alle** Hallo Bash-voorbeelden en **één** van Hallo PowerShell-voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="68fee-124">It is used in **all** hello Bash examples, and **one** of hello PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="68fee-125">Basis-URI voor de Ambari Rest API</span><span class="sxs-lookup"><span data-stu-id="68fee-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="68fee-126">Hallo basis-URI voor Hallo Ambari REST-API op HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, waarbij **CLUSTERNAME** Hallo-naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="68fee-126">hello base URI for hello Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68fee-127">Hoewel de clusternaam Hallo in Hallo FQDN domain name (FQDN) deel van Hallo URI (CLUSTERNAME.azurehdinsight.net) is niet hoofdlettergevoelig, andere voorvallen in Hallo URI zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="68fee-127">While hello cluster name in hello fully qualified domain name (FQDN) part of hello URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in hello URI are case-sensitive.</span></span> <span data-ttu-id="68fee-128">Bijvoorbeeld, als de naam van uw cluster `MyCluster`, Hallo volgen geldige URI's:</span><span class="sxs-lookup"><span data-stu-id="68fee-128">For example, if your cluster is named `MyCluster`, hello following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="68fee-129">Hallo volgende URI's retourneren een foutmelding omdat Hallo tweede exemplaar van het Hallo-naam is geen Hallo corrigeren geval.</span><span class="sxs-lookup"><span data-stu-id="68fee-129">hello following URIs return an error because hello second occurrence of hello name is not hello correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="68fee-130">Authentication</span><span class="sxs-lookup"><span data-stu-id="68fee-130">Authentication</span></span>

<span data-ttu-id="68fee-131">Verbinding maken met tooAmbari op HDInsight HTTPS is vereist.</span><span class="sxs-lookup"><span data-stu-id="68fee-131">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="68fee-132">Gebruik Hallo beheerder accountnaam (Hallo standaardwaarde is **admin**) en het wachtwoord die u hebt opgegeven tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="68fee-132">Use hello admin account name (hello default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="68fee-133">Voorbeelden: Verificatie en bij het parseren van JSON</span><span class="sxs-lookup"><span data-stu-id="68fee-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="68fee-134">Hallo volgen voorbeelden laten zien hoe een GET-aanvraag tegen Hallo toomake baseren Ambari REST-API:</span><span class="sxs-lookup"><span data-stu-id="68fee-134">hello following examples demonstrate how toomake a GET request against hello base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="68fee-135">Hallo Bash voorbeelden in dit document zorg Hallo veronderstellingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="68fee-135">hello Bash examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="68fee-136">Hallo aanmeldingsnaam voor Hallo-cluster is de standaardwaarde Hallo van `admin`.</span><span class="sxs-lookup"><span data-stu-id="68fee-136">hello login name for hello cluster is hello default value of `admin`.</span></span>
> * <span data-ttu-id="68fee-137">`$PASSWORD`Hallo-wachtwoord voor Hallo HDInsight aanmelding opdracht bevat.</span><span class="sxs-lookup"><span data-stu-id="68fee-137">`$PASSWORD` contains hello password for hello HDInsight login command.</span></span> <span data-ttu-id="68fee-138">U kunt deze waarde instellen met behulp van `PASSWORD='mypassword'`.</span><span class="sxs-lookup"><span data-stu-id="68fee-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="68fee-139">`$CLUSTERNAME`Hallo-naam van Hallo cluster bevat.</span><span class="sxs-lookup"><span data-stu-id="68fee-139">`$CLUSTERNAME` contains hello name of hello cluster.</span></span> <span data-ttu-id="68fee-140">U kunt deze waarde instellen door gebruik te maken`set CLUSTERNAME='clustername'`</span><span class="sxs-lookup"><span data-stu-id="68fee-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="68fee-141">Hallo PowerShell-voorbeelden in dit document zorg Hallo veronderstellingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="68fee-141">hello PowerShell examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="68fee-142">`$creds`is een referentieobject dat Hallo beheerder aanmeldingsnaam en het wachtwoord voor Hallo cluster bevat.</span><span class="sxs-lookup"><span data-stu-id="68fee-142">`$creds` is a credential object that contains hello admin login and password for hello cluster.</span></span> <span data-ttu-id="68fee-143">U kunt deze waarde instellen met behulp van `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` en Hallo referenties opgeeft wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="68fee-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` and providing hello credentials when prompted.</span></span>
> * <span data-ttu-id="68fee-144">`$clusterName`is een tekenreeks die Hallo-naam van het Hallo-cluster bevat.</span><span class="sxs-lookup"><span data-stu-id="68fee-144">`$clusterName` is a string that contains hello name of hello cluster.</span></span> <span data-ttu-id="68fee-145">U kunt deze waarde instellen met behulp van `$clusterName="clustername"`.</span><span class="sxs-lookup"><span data-stu-id="68fee-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="68fee-146">Beide voorbeelden retourneren een JSON-document dat begint met informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="68fee-146">Both examples return a JSON document that begins with information similar toohello following example:</span></span>

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

### <a name="parsing-json-data"></a><span data-ttu-id="68fee-147">Bij het parseren van JSON-gegevens</span><span class="sxs-lookup"><span data-stu-id="68fee-147">Parsing JSON data</span></span>

<span data-ttu-id="68fee-148">Hallo volgende voorbeeld wordt `jq` tooparse Hallo JSON-document van antwoord en weer te geven alleen Hallo `health_report` informatie uit Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="68fee-148">hello following example uses `jq` tooparse hello JSON response document and display only hello `health_report` information from hello results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="68fee-149">PowerShell 3.0 en hoger biedt Hallo `ConvertFrom-Json` cmdlet, waarmee de JSON-document Hallo converteert naar een object dat is eenvoudiger toowork met vanuit PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68fee-149">PowerShell 3.0 and higher provides hello `ConvertFrom-Json` cmdlet, which converts hello JSON document into an object that is easier toowork with from PowerShell.</span></span> <span data-ttu-id="68fee-150">Hallo volgende voorbeeld wordt `ConvertFrom-Json` toodisplay alleen Hallo `health_report` informatie uit Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="68fee-150">hello following example uses `ConvertFrom-Json` toodisplay only hello `health_report` information from hello results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="68fee-151">Tijdens het meeste voorbeelden in dit document `ConvertFrom-Json` toodisplay elementen uit Hallo antwoorddocument Hallo [Update Ambari configuratie](#example-update-ambari-configuration) voorbeeld jq wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="68fee-151">While most examples in this document use `ConvertFrom-Json` toodisplay elements from hello response document, hello [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="68fee-152">Jq wordt gebruikt in dit voorbeeld tooconstruct een nieuwe sjabloon uit Hallo JSON-antwoord-document.</span><span class="sxs-lookup"><span data-stu-id="68fee-152">Jq is used in this example tooconstruct a new template from hello JSON response document.</span></span>

<span data-ttu-id="68fee-153">Zie voor een volledig overzicht van Hallo REST-API [Ambari-API-verwijzing V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="68fee-153">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a><span data-ttu-id="68fee-154">Voorbeeld: Hallo FQDN-naam van de clusterknooppunten ophalen</span><span class="sxs-lookup"><span data-stu-id="68fee-154">Example: Get hello FQDN of cluster nodes</span></span>

<span data-ttu-id="68fee-155">Als u werkt met HDInsight, moet u mogelijk tooknow Hallo volledig gekwalificeerde domeinnaam (FQDN) van een clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="68fee-155">When working with HDInsight, you may need tooknow hello fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="68fee-156">U kunt eenvoudig ophalen Hallo FQDN voor Hallo verschillende knooppunten in het Hallo-cluster met behulp van Hallo volgen voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="68fee-156">You can easily retrieve hello FQDN for hello various nodes in hello cluster using hello following examples:</span></span>

* <span data-ttu-id="68fee-157">**Alle knooppunten**</span><span class="sxs-lookup"><span data-stu-id="68fee-157">**All nodes**</span></span>

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

* <span data-ttu-id="68fee-158">**HEAD-knooppunten**</span><span class="sxs-lookup"><span data-stu-id="68fee-158">**Head nodes**</span></span>

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

* <span data-ttu-id="68fee-159">**Worker-knooppunten**</span><span class="sxs-lookup"><span data-stu-id="68fee-159">**Worker nodes**</span></span>

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

* <span data-ttu-id="68fee-160">**Zookeeper-knooppunten**</span><span class="sxs-lookup"><span data-stu-id="68fee-160">**Zookeeper nodes**</span></span>

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

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="68fee-161">Voorbeeld: Hallo interne IP-adres van de clusterknooppunten ophalen</span><span class="sxs-lookup"><span data-stu-id="68fee-161">Example: Get hello internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68fee-162">Hallo IP-adressen die wordt geretourneerd door Hallo voorbeelden in deze sectie zijn niet rechtstreeks toegankelijk via internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="68fee-162">hello IP addresses returned by hello examples in this section are not directly accessible over hello internet.</span></span> <span data-ttu-id="68fee-163">Ze zijn alleen toegankelijk vanuit hello Azure Virtual Network die Hallo HDInsight-cluster bevat.</span><span class="sxs-lookup"><span data-stu-id="68fee-163">They are only accessible within hello Azure Virtual Network that contains hello HDInsight cluster.</span></span>
>
> <span data-ttu-id="68fee-164">Zie voor meer informatie over het werken met HDInsight en virtuele netwerken [mogelijkheden uitbreiden HDInsight met behulp van een aangepaste Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="68fee-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="68fee-165">toofind hello IP-adres, moet u weten Hallo interne volledig gekwalificeerde domeinnaam (FQDN) van Hallo clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="68fee-165">toofind hello IP address, you must know hello internal fully qualified domain name (FQDN) of hello cluster nodes.</span></span> <span data-ttu-id="68fee-166">Zodra u Hallo FQDN hebt, kunt u vervolgens Hallo IP-adres van de host Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="68fee-166">Once you have hello FQDN, you can then get hello IP address of hello host.</span></span> <span data-ttu-id="68fee-167">Hallo volgende voorbeelden eerst Hallo FQDN-naam van de knooppunten van de host alle Hallo Ambari zoeken en vervolgens Ambari zoeken naar Hallo IP-adres van elke host.</span><span class="sxs-lookup"><span data-stu-id="68fee-167">hello following examples first query Ambari for hello FQDN of all hello host nodes, then query Ambari for hello IP address of each host.</span></span>

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

## <a name="example-get-hello-default-storage"></a><span data-ttu-id="68fee-168">Voorbeeld: Hallo standaard opslag ophalen</span><span class="sxs-lookup"><span data-stu-id="68fee-168">Example: Get hello default storage</span></span>

<span data-ttu-id="68fee-169">Wanneer u een HDInsight-cluster maakt, moet u een Azure Storage-Account of een Data Lake Store als Hallo standaard opslag voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="68fee-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as hello default storage for hello cluster.</span></span> <span data-ttu-id="68fee-170">U kunt de Ambari tooretrieve deze gegevens nadat Hallo-cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="68fee-170">You can use Ambari tooretrieve this information after hello cluster has been created.</span></span> <span data-ttu-id="68fee-171">Bijvoorbeeld als u wilt dat tooread schrijftijd gegevenscontainer toohello buiten HDInsight.</span><span class="sxs-lookup"><span data-stu-id="68fee-171">For example, if you want tooread/write data toohello container outside HDInsight.</span></span>

<span data-ttu-id="68fee-172">Hallo ophalen volgende voorbeelden Hallo standaard opslagconfiguratie uit Hallo-cluster:</span><span class="sxs-lookup"><span data-stu-id="68fee-172">hello following examples retrieve hello default storage configuration from hello cluster:</span></span>

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
> <span data-ttu-id="68fee-173">Deze voorbeelden retourneren Hallo eerste toegepast toohello configuratieserver (`service_config_version=1`) die deze informatie bevat.</span><span class="sxs-lookup"><span data-stu-id="68fee-173">These examples return hello first configuration applied toohello server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="68fee-174">Als u een waarde die is gewijzigd na het maken van het cluster ophaalt, mag u toolist hello configuratieversies moet en ophalen van de meest recente Hallo.</span><span class="sxs-lookup"><span data-stu-id="68fee-174">If you retrieve a value that has been modified after cluster creation, you may need toolist hello configuration versions and retrieve hello latest one.</span></span>

<span data-ttu-id="68fee-175">Hallo-retourwaarde is vergelijkbaar tooone Hallo volgen voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="68fee-175">hello return value is similar tooone of hello following examples:</span></span>

* <span data-ttu-id="68fee-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Deze waarde geeft aan dat cluster hello Azure Storage-account voor de opslag van de standaard.</span><span class="sxs-lookup"><span data-stu-id="68fee-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that hello cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="68fee-177">Hallo `ACCOUNTNAME` waarde is de naam Hallo van Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="68fee-177">hello `ACCOUNTNAME` value is hello name of hello storage account.</span></span> <span data-ttu-id="68fee-178">Hallo `CONTAINER` gedeelte Hallo-naam van Hallo blob-container in Hallo storage-account is.</span><span class="sxs-lookup"><span data-stu-id="68fee-178">hello `CONTAINER` portion is hello name of hello blob container in hello storage account.</span></span> <span data-ttu-id="68fee-179">Hallo-container bevat Hallo Hallo HDFS compatibel opslagruimte voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="68fee-179">hello container is hello root of hello HDFS compatible storage for hello cluster.</span></span>

* <span data-ttu-id="68fee-180">`adl://home`-Deze waarde geeft aan dat Hallo-cluster gebruikmaakt van een Azure Data Lake Store voor standaard-opslag.</span><span class="sxs-lookup"><span data-stu-id="68fee-180">`adl://home` - This value indicates that hello cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="68fee-181">toofind hello Data Lake Store-accountnaam, gebruik Hallo volgen voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="68fee-181">toofind hello Data Lake Store account name, use hello following examples:</span></span>

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

    <span data-ttu-id="68fee-182">Hallo retourwaarde lijkt te`ACCOUNTNAME.azuredatalakestore.net`, waarbij `ACCOUNTNAME` heet Hallo Hallo Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="68fee-182">hello return value is similar too`ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is hello name of hello Data Lake Store account.</span></span>

    <span data-ttu-id="68fee-183">toofind hello map in Data Lake Store met Hallo opslagruimte voor Hallo-cluster, gebruik Hallo volgen voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="68fee-183">toofind hello directory within Data Lake Store that contains hello storage for hello cluster, use hello following examples:</span></span>

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

    <span data-ttu-id="68fee-184">Hallo retourwaarde lijkt te`/clusters/CLUSTERNAME/`.</span><span class="sxs-lookup"><span data-stu-id="68fee-184">hello return value is similar too`/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="68fee-185">Deze waarde is een pad binnen Hallo Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="68fee-185">This value is a path within hello Data Lake Store account.</span></span> <span data-ttu-id="68fee-186">Dit pad bevat Hallo Hallo HDFS-compatibele bestandssysteem voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="68fee-186">This path is hello root of hello HDFS compatible file system for hello cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="68fee-187">Hallo `Get-AzureRmHDInsightCluster` cmdlet geleverd door [Azure PowerShell](/powershell/azure/overview) ook retourneert Hallo storage-gegevens voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="68fee-187">hello `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns hello storage information for hello cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="68fee-188">Voorbeeld: Get-configuratie</span><span class="sxs-lookup"><span data-stu-id="68fee-188">Example: Get configuration</span></span>

1. <span data-ttu-id="68fee-189">Hallo-configuraties die beschikbaar voor uw cluster zijn ophalen.</span><span class="sxs-lookup"><span data-stu-id="68fee-189">Get hello configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="68fee-190">Het volgende voorbeeld wordt een JSON-document met de huidige configuratie Hallo (aangeduid met Hallo *tag* waarde) voor Hallo-onderdelen geïnstalleerd op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="68fee-190">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="68fee-191">Hallo is volgende voorbeeld een fragment uit het Hallo-gegevens geretourneerd van een type Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="68fee-191">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
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

2. <span data-ttu-id="68fee-192">Hallo-configuratie voor Hallo-onderdeel dat u geïnteresseerd bent in ophalen.</span><span class="sxs-lookup"><span data-stu-id="68fee-192">Get hello configuration for hello component that you are interested in.</span></span> <span data-ttu-id="68fee-193">Hallo volgt, Vervang in `INITIAL` met Hallo tag geretourneerde waarde van de vorige aanvraag Hallo.</span><span class="sxs-lookup"><span data-stu-id="68fee-193">In hello following example, replace `INITIAL` with hello tag value returned from hello previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="68fee-194">Het volgende voorbeeld wordt een JSON-document met de huidige configuratie Hallo voor Hallo `core-site` onderdeel.</span><span class="sxs-lookup"><span data-stu-id="68fee-194">This example returns a JSON document containing hello current configuration for hello `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="68fee-195">Voorbeeld: Update-configuratie</span><span class="sxs-lookup"><span data-stu-id="68fee-195">Example: Update configuration</span></span>

1. <span data-ttu-id="68fee-196">De huidige configuratie hello, waardoor de Ambari worden opgeslagen als Hallo 'gewenste configuratie' ophalen:</span><span class="sxs-lookup"><span data-stu-id="68fee-196">Get hello current configuration, which Ambari stores as hello "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="68fee-197">Het volgende voorbeeld wordt een JSON-document met de huidige configuratie Hallo (aangeduid met Hallo *tag* waarde) voor Hallo-onderdelen geïnstalleerd op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="68fee-197">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="68fee-198">Hallo is volgende voorbeeld een fragment uit het Hallo-gegevens geretourneerd van een type Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="68fee-198">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
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
   
    <span data-ttu-id="68fee-199">In deze lijst, moet u toocopy Hallo-naam van het Hallo-onderdeel (bijvoorbeeld **spark\_thrift\_sparkconf** en Hallo **tag** waarde.</span><span class="sxs-lookup"><span data-stu-id="68fee-199">From this list, you need toocopy hello name of hello component (for example, **spark\_thrift\_sparkconf** and hello **tag** value.</span></span>

2. <span data-ttu-id="68fee-200">Hallo-configuratie voor het Hallo-onderdeel en de tag ophalen met behulp van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="68fee-200">Retrieve hello configuration for hello component and tag by using hello following commands:</span></span>
   
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
    > <span data-ttu-id="68fee-201">Vervang **spark-thrift-sparkconf** en **INITIËLE** met Hallo-onderdeel en code die u wilt dat tooretrieve Hallo configuratie voor.</span><span class="sxs-lookup"><span data-stu-id="68fee-201">Replace **spark-thrift-sparkconf** and **INITIAL** with hello component and tag that you want tooretrieve hello configuration for.</span></span>
   
    <span data-ttu-id="68fee-202">Jq is gebruikte tooturn Hallo gegevens opgehaald uit HDInsight naar een nieuwe configuratiesjabloon.</span><span class="sxs-lookup"><span data-stu-id="68fee-202">Jq is used tooturn hello data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="68fee-203">Deze voorbeelden uitvoeren in het bijzonder Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="68fee-203">Specifically, these examples perform hello following actions:</span></span>
   
    * <span data-ttu-id="68fee-204">Hiermee maakt u een unieke waarde met de Hallo tekenreeks '-versie en datum hello, dat is opgeslagen in `newtag`.</span><span class="sxs-lookup"><span data-stu-id="68fee-204">Creates a unique value containing hello string "version" and hello date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="68fee-205">Maakt een document hoofdmap voor de nieuwe gewenste configuratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="68fee-205">Creates a root document for hello new desired configuration.</span></span>

    * <span data-ttu-id="68fee-206">Haalt inhoud Hallo Hallo `.items[]` matrix en voegt deze toe onder Hallo **desired_config** element.</span><span class="sxs-lookup"><span data-stu-id="68fee-206">Gets hello contents of hello `.items[]` array and adds it under hello **desired_config** element.</span></span>

    * <span data-ttu-id="68fee-207">Hiermee verwijdert u Hallo `href`, `version`, en `Config` elementen, als deze elementen zijn niet nodig toosubmit een nieuwe configuratie.</span><span class="sxs-lookup"><span data-stu-id="68fee-207">Deletes hello `href`, `version`, and `Config` elements, as these elements aren't needed toosubmit a new configuration.</span></span>

    * <span data-ttu-id="68fee-208">Voegt een `tag` element met een waarde van `version#################`.</span><span class="sxs-lookup"><span data-stu-id="68fee-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="68fee-209">het numerieke gedeelte Hallo is gebaseerd op Hallo huidige datum.</span><span class="sxs-lookup"><span data-stu-id="68fee-209">hello numeric portion is based on hello current date.</span></span> <span data-ttu-id="68fee-210">Elke configuratie moet een unieke code hebben.</span><span class="sxs-lookup"><span data-stu-id="68fee-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="68fee-211">Ten slotte Hallo gegevens opgeslagen toohello `newconfig.json` document.</span><span class="sxs-lookup"><span data-stu-id="68fee-211">Finally, hello data is saved toohello `newconfig.json` document.</span></span> <span data-ttu-id="68fee-212">de documentstructuur Hallo moet worden weergegeven vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="68fee-212">hello document structure should appear similar toohello following example:</span></span>
     
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

3. <span data-ttu-id="68fee-213">Open Hallo `newconfig.json` waarden document en wijzigen/toevoegen in Hallo `properties` object.</span><span class="sxs-lookup"><span data-stu-id="68fee-213">Open hello `newconfig.json` document and modify/add values in hello `properties` object.</span></span> <span data-ttu-id="68fee-214">Hallo volgende voorbeeld wijzigingen Hallo waarde van `"spark.yarn.am.memory"` van `"1g"` te`"3g"`.</span><span class="sxs-lookup"><span data-stu-id="68fee-214">hello following example changes hello value of `"spark.yarn.am.memory"` from `"1g"` too`"3g"`.</span></span> <span data-ttu-id="68fee-215">Voegt ook `"spark.kryoserializer.buffer.max"` met een waarde van `"256m"`.</span><span class="sxs-lookup"><span data-stu-id="68fee-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="68fee-216">Hallo-bestand opslaan als u klaar bent wijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="68fee-216">Save hello file once you are done making modifications.</span></span>

4. <span data-ttu-id="68fee-217">Gebruik Hallo opdrachten toosubmit Hallo bijgewerkt configuratie tooAmbari te volgen.</span><span class="sxs-lookup"><span data-stu-id="68fee-217">Use hello following commands toosubmit hello updated configuration tooAmbari.</span></span>
   
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
   
    <span data-ttu-id="68fee-218">Deze opdrachten verzenden Hallo inhoud Hallo **newconfig.json** toohello cluster bestand zoals Hallo nieuwe configuratie gewenst.</span><span class="sxs-lookup"><span data-stu-id="68fee-218">These commands submit hello contents of hello **newconfig.json** file toohello cluster as hello new desired configuration.</span></span> <span data-ttu-id="68fee-219">Hallo aanvraag retourneert een JSON-document.</span><span class="sxs-lookup"><span data-stu-id="68fee-219">hello request returns a JSON document.</span></span> <span data-ttu-id="68fee-220">Hallo **versionTag** element in dit document moet overeenkomen met de Hallo versie hebt verzonden Hallo **configs** object bevat Hallo-configuratiewijzigingen die u hebt aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="68fee-220">hello **versionTag** element in this document should match hello version you submitted, and hello **configs** object contains hello configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="68fee-221">Voorbeeld: Start opnieuw op een serviceonderdeel</span><span class="sxs-lookup"><span data-stu-id="68fee-221">Example: Restart a service component</span></span>

<span data-ttu-id="68fee-222">Op dit punt als u Hallo Ambari-webgebruikersinterface bekijkt, Hallo Spark-service geeft aan dat deze opnieuw worden opgestart moet voordat de nieuwe configuratie Hallo van kracht toobe.</span><span class="sxs-lookup"><span data-stu-id="68fee-222">At this point, if you look at hello Ambari web UI, hello Spark service indicates that it needs toobe restarted before hello new configuration can take effect.</span></span> <span data-ttu-id="68fee-223">Volgende stappen toorestart Hallo service Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="68fee-223">Use hello following steps toorestart hello service.</span></span>

1. <span data-ttu-id="68fee-224">Gebruik Hallo tooenable onderhoudsmodus voor Hallo Spark-service te volgen:</span><span class="sxs-lookup"><span data-stu-id="68fee-224">Use hello following tooenable maintenance mode for hello Spark service:</span></span>

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
   
    <span data-ttu-id="68fee-225">Deze opdrachten verzenden een JSON-document toohello server Hiermee schakelt u onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="68fee-225">These commands send a JSON document toohello server that turns on maintenance mode.</span></span> <span data-ttu-id="68fee-226">U kunt controleren Hallo-service is nu in de onderhoudsmodus met Hallo aanvraag te volgen:</span><span class="sxs-lookup"><span data-stu-id="68fee-226">You can verify that hello service is now in maintenance mode using hello following request:</span></span>
   
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
   
    <span data-ttu-id="68fee-227">Hallo retourwaarde is `ON`.</span><span class="sxs-lookup"><span data-stu-id="68fee-227">hello return value is `ON`.</span></span>

2. <span data-ttu-id="68fee-228">Gebruik vervolgens Hallo tooturn Hallo-service uit te volgen:</span><span class="sxs-lookup"><span data-stu-id="68fee-228">Next, use hello following tooturn off hello service:</span></span>

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
    
    <span data-ttu-id="68fee-229">Hallo-antwoord is vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="68fee-229">hello response is similar toohello following example:</span></span>
   
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
    > <span data-ttu-id="68fee-230">Hallo `href` waarde die door deze URI geretourneerd met behulp van interne IP-adres van het clusterknooppunt Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="68fee-230">hello `href` value returned by this URI is using hello internal IP address of hello cluster node.</span></span> <span data-ttu-id="68fee-231">toouse via externe Hallo-cluster, '10.0.0.18:8080' hello gedeelte vervangen door Hallo FQDN-naam van het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="68fee-231">toouse it from outside hello cluster, replace hello \`10.0.0.18:8080' portion with hello FQDN of hello cluster.</span></span> 
    
    <span data-ttu-id="68fee-232">Hallo opdrachten na Hallo status van aanvraag Hallo niet ophalen:</span><span class="sxs-lookup"><span data-stu-id="68fee-232">hello following commands retrieve hello status of hello request:</span></span>

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

    <span data-ttu-id="68fee-233">Een antwoord van `COMPLETED` geeft aan dat Hallo-aanvraag is voltooid.</span><span class="sxs-lookup"><span data-stu-id="68fee-233">A response of `COMPLETED` indicates that hello request has finished.</span></span>

3. <span data-ttu-id="68fee-234">Zodra de vorige aanvraag Hallo is voltooid, gebruik Hallo toostart Hallo service te volgen.</span><span class="sxs-lookup"><span data-stu-id="68fee-234">Once hello previous request completes, use hello following toostart hello service.</span></span>
   
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
    <span data-ttu-id="68fee-235">Hallo-service maakt nu gebruik van de nieuwe configuratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="68fee-235">hello service is now using hello new configuration.</span></span>

4. <span data-ttu-id="68fee-236">Gebruik tot slot Hallo tooturn uit de onderhoudsmodus te volgen.</span><span class="sxs-lookup"><span data-stu-id="68fee-236">Finally, use hello following tooturn off maintenance mode.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="68fee-237">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="68fee-237">Next steps</span></span>

<span data-ttu-id="68fee-238">Zie voor een volledig overzicht van Hallo REST-API [Ambari-API-verwijzing V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="68fee-238">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>


---
title: Bewaken en beheren van Hadoop met Ambari REST-API - Azure HDInsight | Microsoft Docs
description: Informatie over het Ambari gebruiken om te controleren en beheren in Azure HDInsight Hadoop-clusters. In dit document leert u hoe u de Ambari REST-API die deel uitmaakt van een HDInsight-clusters.
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
ms.openlocfilehash: 7960d83bce22d4f671d61e9aaf55561bc24308f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-rest-api"></a><span data-ttu-id="ed4ed-104">HDInsight-clusters beheren met behulp van de Ambari REST-API</span><span class="sxs-lookup"><span data-stu-id="ed4ed-104">Manage HDInsight clusters by using the Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="ed4ed-105">Informatie over het gebruik van de Ambari REST-API te beheren en bewaken in Azure HDInsight Hadoop-clusters.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-105">Learn how to use the Ambari REST API to manage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="ed4ed-106">Apache Ambari vereenvoudigt het beheer en bewaking van een Hadoop-cluster met een eenvoudige web-UI en REST-API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-106">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="ed4ed-107">Ambari is opgenomen op HDInsight-clusters die gebruikmaken van de Linux-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-107">Ambari is included on HDInsight clusters that use the Linux operating system.</span></span> <span data-ttu-id="ed4ed-108">U kunt Ambari gebruiken om te controleren van het cluster en configuratiewijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-108">You can use Ambari to monitor the cluster and make configuration changes.</span></span>

## <span data-ttu-id="ed4ed-109"><a id="whatis"></a>Wat is Ambari</span><span class="sxs-lookup"><span data-stu-id="ed4ed-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="ed4ed-110">[Apache Ambari](http://ambari.apache.org) biedt webgebruikersinterface die kunnen worden gebruikt voor het inrichten, beheren en controleren van Hadoop-clusters.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used to provision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="ed4ed-111">Ontwikkelaars kunnen deze mogelijkheden integreren in hun toepassingen met behulp van de [Ambari REST-API's](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="ed4ed-112">Ambari is opgegeven met HDInsight op basis van Linux-clusters standaard.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-to-use-the-ambari-rest-api"></a><span data-ttu-id="ed4ed-113">Het gebruik van de Ambari REST-API</span><span class="sxs-lookup"><span data-stu-id="ed4ed-113">How to use the Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed4ed-114">De informatie en voorbeelden in dit document vereisen een HDInsight-cluster dat gebruik maakt van Linux-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-114">The information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="ed4ed-115">Zie voor meer informatie [aan de slag met HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="ed4ed-116">De voorbeelden in dit document zijn beschikbaar voor zowel de Willemsen shell (bash) en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-116">The examples in this document are provided for both the Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="ed4ed-117">De voorbeelden zijn getest met GNU bash 4.3.11 bash, maar moet samen met andere houders Unix.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-117">The bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="ed4ed-118">De PowerShell-voorbeelden zijn getest met PowerShell 5.0, maar moeten samenwerken met PowerShell 3.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-118">The PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="ed4ed-119">Als de __Bourne shell__ (Bash), hebt u het volgende zijn geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-119">If using the __Bourne shell__ (Bash), you must have the following installed:</span></span>

* <span data-ttu-id="ed4ed-120">[cURL](http://curl.haxx.se/): cURL is een hulpprogramma waarmee kan worden gebruikt voor het werken met de REST-API's vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used to work with REST APIs from the command line.</span></span> <span data-ttu-id="ed4ed-121">In dit document, wordt deze gebruikt om te communiceren met de Ambari REST-API.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-121">In this document, it is used to communicate with the Ambari REST API.</span></span>

<span data-ttu-id="ed4ed-122">Of Bash of PowerShell gebruikt, moet u ook hebt [jq](https://stedolan.github.io/jq/) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="ed4ed-123">Jq is een hulpprogramma voor het werken met JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="ed4ed-124">Het wordt gebruikt in **alle** de voorbeelden Bash en **één** van de PowerShell-voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-124">It is used in **all** the Bash examples, and **one** of the PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="ed4ed-125">Basis-URI voor de Ambari Rest API</span><span class="sxs-lookup"><span data-stu-id="ed4ed-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="ed4ed-126">De basis-URI voor de Ambari REST-API op HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, waarbij **CLUSTERNAME** is de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-126">The base URI for the Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed4ed-127">De naam van het cluster in het gedeelte van de FQDN-naam (Fully Qualified Domain Name) van de URI (CLUSTERNAME.azurehdinsight.net) is niet hoofdlettergevoelig, zijn andere exemplaren in de URI zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-127">While the cluster name in the fully qualified domain name (FQDN) part of the URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in the URI are case-sensitive.</span></span> <span data-ttu-id="ed4ed-128">Bijvoorbeeld, als de naam van uw cluster `MyCluster`, de volgende geldige URI's zijn:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-128">For example, if your cluster is named `MyCluster`, the following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="ed4ed-129">De volgende URI's retourneren een foutmelding omdat het tweede exemplaar van de naam is niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-129">The following URIs return an error because the second occurrence of the name is not the correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="ed4ed-130">Authentication</span><span class="sxs-lookup"><span data-stu-id="ed4ed-130">Authentication</span></span>

<span data-ttu-id="ed4ed-131">Verbinding maken met Ambari op HDInsight HTTPS is vereist.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-131">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="ed4ed-132">De naam van de Administrator-account gebruiken (de standaardwaarde is **admin**) en het wachtwoord die u hebt opgegeven tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-132">Use the admin account name (the default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="ed4ed-133">Voorbeelden: Verificatie en bij het parseren van JSON</span><span class="sxs-lookup"><span data-stu-id="ed4ed-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="ed4ed-134">De volgende voorbeelden laten zien hoe u een GET-aanvraag met de base Ambari REST-API:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-134">The following examples demonstrate how to make a GET request against the base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="ed4ed-135">De Bash-voorbeelden in dit document moeten de volgende veronderstellingen:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-135">The Bash examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="ed4ed-136">De aanmeldingsnaam voor het cluster is de standaardwaarde van `admin`.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-136">The login name for the cluster is the default value of `admin`.</span></span>
> * <span data-ttu-id="ed4ed-137">`$PASSWORD`het wachtwoord voor de opdracht van de aanmelding HDInsight bevat.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-137">`$PASSWORD` contains the password for the HDInsight login command.</span></span> <span data-ttu-id="ed4ed-138">U kunt deze waarde instellen met behulp van `PASSWORD='mypassword'`.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="ed4ed-139">`$CLUSTERNAME`bevat de naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-139">`$CLUSTERNAME` contains the name of the cluster.</span></span> <span data-ttu-id="ed4ed-140">U kunt deze waarde instellen door gebruik te maken`set CLUSTERNAME='clustername'`</span><span class="sxs-lookup"><span data-stu-id="ed4ed-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="ed4ed-141">De PowerShell-voorbeelden in dit document moeten de volgende veronderstellingen:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-141">The PowerShell examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="ed4ed-142">`$creds`is een referentieobject dat de beheerderaanmelding en het wachtwoord voor het cluster bevat.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-142">`$creds` is a credential object that contains the admin login and password for the cluster.</span></span> <span data-ttu-id="ed4ed-143">U kunt deze waarde instellen met behulp van `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` en de referenties opgeeft wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` and providing the credentials when prompted.</span></span>
> * <span data-ttu-id="ed4ed-144">`$clusterName`is een tekenreeks met de naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-144">`$clusterName` is a string that contains the name of the cluster.</span></span> <span data-ttu-id="ed4ed-145">U kunt deze waarde instellen met behulp van `$clusterName="clustername"`.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="ed4ed-146">Beide voorbeelden retourneren een JSON-document dat met de informatie is vergelijkbaar met het volgende voorbeeld begint:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-146">Both examples return a JSON document that begins with information similar to the following example:</span></span>

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

### <a name="parsing-json-data"></a><span data-ttu-id="ed4ed-147">Bij het parseren van JSON-gegevens</span><span class="sxs-lookup"><span data-stu-id="ed4ed-147">Parsing JSON data</span></span>

<span data-ttu-id="ed4ed-148">Het volgende voorbeeld wordt `jq` parseren van het JSON-antwoorddocument en alleen wordt weergegeven de `health_report` informatie uit de resultaten.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-148">The following example uses `jq` to parse the JSON response document and display only the `health_report` information from the results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="ed4ed-149">PowerShell 3.0 en hoger biedt de `ConvertFrom-Json` cmdlet, waarmee het JSON-document converteert naar een object dat is eenvoudiger om te werken in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-149">PowerShell 3.0 and higher provides the `ConvertFrom-Json` cmdlet, which converts the JSON document into an object that is easier to work with from PowerShell.</span></span> <span data-ttu-id="ed4ed-150">Het volgende voorbeeld wordt `ConvertFrom-Json` om weer te geven alleen de `health_report` informatie uit de resultaten.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-150">The following example uses `ConvertFrom-Json` to display only the `health_report` information from the results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="ed4ed-151">Tijdens het meeste voorbeelden in dit document `ConvertFrom-Json` om elementen van het antwoorddocument te geven de [Update Ambari configuratie](#example-update-ambari-configuration) voorbeeld jq wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-151">While most examples in this document use `ConvertFrom-Json` to display elements from the response document, the [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="ed4ed-152">Jq wordt in dit voorbeeld gebruikt om een nieuwe sjabloon uit de JSON-antwoorddocument samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-152">Jq is used in this example to construct a new template from the JSON response document.</span></span>

<span data-ttu-id="ed4ed-153">Zie voor een volledig overzicht van de REST API [Ambari-API-verwijzing V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-153">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-the-fqdn-of-cluster-nodes"></a><span data-ttu-id="ed4ed-154">Voorbeeld: De FQDN van de clusterknooppunten ophalen</span><span class="sxs-lookup"><span data-stu-id="ed4ed-154">Example: Get the FQDN of cluster nodes</span></span>

<span data-ttu-id="ed4ed-155">Als u werkt met HDInsight, moet u wellicht weten de volledig gekwalificeerde domeinnaam (FQDN) van een clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-155">When working with HDInsight, you may need to know the fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="ed4ed-156">De FQDN-naam voor de verschillende knooppunten in het cluster met behulp van de volgende voorbeelden kunt u eenvoudig ophalen:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-156">You can easily retrieve the FQDN for the various nodes in the cluster using the following examples:</span></span>

* <span data-ttu-id="ed4ed-157">**Alle knooppunten**</span><span class="sxs-lookup"><span data-stu-id="ed4ed-157">**All nodes**</span></span>

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

* <span data-ttu-id="ed4ed-158">**HEAD-knooppunten**</span><span class="sxs-lookup"><span data-stu-id="ed4ed-158">**Head nodes**</span></span>

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

* <span data-ttu-id="ed4ed-159">**Worker-knooppunten**</span><span class="sxs-lookup"><span data-stu-id="ed4ed-159">**Worker nodes**</span></span>

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

* <span data-ttu-id="ed4ed-160">**Zookeeper-knooppunten**</span><span class="sxs-lookup"><span data-stu-id="ed4ed-160">**Zookeeper nodes**</span></span>

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

## <a name="example-get-the-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="ed4ed-161">Voorbeeld: De interne IP-adres van de clusterknooppunten ophalen</span><span class="sxs-lookup"><span data-stu-id="ed4ed-161">Example: Get the internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed4ed-162">De IP-adressen die wordt geretourneerd door de voorbeelden in deze sectie zijn niet rechtstreeks toegankelijk via het internet.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-162">The IP addresses returned by the examples in this section are not directly accessible over the internet.</span></span> <span data-ttu-id="ed4ed-163">Ze zijn alleen toegankelijk vanuit het Azure-netwerk met het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-163">They are only accessible within the Azure Virtual Network that contains the HDInsight cluster.</span></span>
>
> <span data-ttu-id="ed4ed-164">Zie voor meer informatie over het werken met HDInsight en virtuele netwerken [mogelijkheden uitbreiden HDInsight met behulp van een aangepaste Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="ed4ed-165">Als u het IP-adres zoekt, moet u weten de interne volledig gekwalificeerde domeinnaam (FQDN) van de clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-165">To find the IP address, you must know the internal fully qualified domain name (FQDN) of the cluster nodes.</span></span> <span data-ttu-id="ed4ed-166">Zodra u de FQDN-naam hebt, krijgt u het IP-adres van de host.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-166">Once you have the FQDN, you can then get the IP address of the host.</span></span> <span data-ttu-id="ed4ed-167">De volgende voorbeelden eerst Ambari zoeken naar de FQDN van alle knooppunten van de host vervolgens Ambari zoeken naar het IP-adres van elke host.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-167">The following examples first query Ambari for the FQDN of all the host nodes, then query Ambari for the IP address of each host.</span></span>

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

## <a name="example-get-the-default-storage"></a><span data-ttu-id="ed4ed-168">Voorbeeld: De opslag standaard ophalen</span><span class="sxs-lookup"><span data-stu-id="ed4ed-168">Example: Get the default storage</span></span>

<span data-ttu-id="ed4ed-169">Wanneer u een HDInsight-cluster maakt, moet u een Azure Storage-Account of een Data Lake Store als de standaard-opslag gebruiken voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as the default storage for the cluster.</span></span> <span data-ttu-id="ed4ed-170">Ambari kunt u deze informatie ophalen nadat het cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-170">You can use Ambari to retrieve this information after the cluster has been created.</span></span> <span data-ttu-id="ed4ed-171">Bijvoorbeeld als u wilt lezen/schrijven gegevens naar de container buiten HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-171">For example, if you want to read/write data to the container outside HDInsight.</span></span>

<span data-ttu-id="ed4ed-172">De standaardconfiguratie voor opslag ophalen in de volgende voorbeelden uit het cluster:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-172">The following examples retrieve the default storage configuration from the cluster:</span></span>

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
> <span data-ttu-id="ed4ed-173">Deze voorbeelden retourneert de eerste configuratie is toegepast op de server (`service_config_version=1`) die deze informatie bevat.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-173">These examples return the first configuration applied to the server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="ed4ed-174">Als u een waarde die is gewijzigd na het maken van het cluster ophaalt, moet u wellicht de configuratieversies lijst en de meest recente versie op te halen.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-174">If you retrieve a value that has been modified after cluster creation, you may need to list the configuration versions and retrieve the latest one.</span></span>

<span data-ttu-id="ed4ed-175">De geretourneerde waarde is vergelijkbaar met een van de volgende voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-175">The return value is similar to one of the following examples:</span></span>

* <span data-ttu-id="ed4ed-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Deze waarde geeft aan dat het cluster een Azure Storage-account wordt gebruikt voor standaard-opslag.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that the cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="ed4ed-177">De `ACCOUNTNAME` waarde is de naam van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-177">The `ACCOUNTNAME` value is the name of the storage account.</span></span> <span data-ttu-id="ed4ed-178">De `CONTAINER` gedeelte is de naam van de blob-container in het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-178">The `CONTAINER` portion is the name of the blob container in the storage account.</span></span> <span data-ttu-id="ed4ed-179">De container is de hoofdmap van de HDFS-compatibele opslagruimte voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-179">The container is the root of the HDFS compatible storage for the cluster.</span></span>

* <span data-ttu-id="ed4ed-180">`adl://home`-Deze waarde geeft aan dat het cluster een Azure Data Lake Store wordt gebruikt voor standaard-opslag.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-180">`adl://home` - This value indicates that the cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="ed4ed-181">De naam te zoeken Data Lake Store-account, gebruik de volgende voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-181">To find the Data Lake Store account name, use the following examples:</span></span>

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

    <span data-ttu-id="ed4ed-182">De geretourneerde waarde is vergelijkbaar met `ACCOUNTNAME.azuredatalakestore.net`, waarbij `ACCOUNTNAME` is de naam van het Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-182">The return value is similar to `ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is the name of the Data Lake Store account.</span></span>

    <span data-ttu-id="ed4ed-183">Als u wilt zoeken naar de map in Data Lake Store met de opslagruimte voor het cluster, gebruik de volgende voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-183">To find the directory within Data Lake Store that contains the storage for the cluster, use the following examples:</span></span>

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

    <span data-ttu-id="ed4ed-184">De geretourneerde waarde is vergelijkbaar met `/clusters/CLUSTERNAME/`.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-184">The return value is similar to `/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="ed4ed-185">Deze waarde is een pad in het Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-185">This value is a path within the Data Lake Store account.</span></span> <span data-ttu-id="ed4ed-186">Dit pad is de hoofdmap van het systeem HDFS compatibel bestand voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-186">This path is the root of the HDFS compatible file system for the cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="ed4ed-187">De `Get-AzureRmHDInsightCluster` cmdlet geleverd door [Azure PowerShell](/powershell/azure/overview) geeft ook de storage-gegevens voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-187">The `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns the storage information for the cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="ed4ed-188">Voorbeeld: Get-configuratie</span><span class="sxs-lookup"><span data-stu-id="ed4ed-188">Example: Get configuration</span></span>

1. <span data-ttu-id="ed4ed-189">Haal de configuraties die beschikbaar voor uw cluster zijn.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-189">Get the configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="ed4ed-190">Het volgende voorbeeld wordt een JSON-document met de huidige configuratie (geïdentificeerd door de *tag* waarde) voor de onderdelen die zijn geïnstalleerd op het cluster.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-190">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="ed4ed-191">Het volgende voorbeeld is een fragment van de gegevens van een Spark-clustertype geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-191">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
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

2. <span data-ttu-id="ed4ed-192">De configuratie voor het onderdeel dat u geïnteresseerd bent in ophalen.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-192">Get the configuration for the component that you are interested in.</span></span> <span data-ttu-id="ed4ed-193">Vervang in het volgende voorbeeld wordt `INITIAL` geretourneerd met de waarde van het label van de vorige aanvraag.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-193">In the following example, replace `INITIAL` with the tag value returned from the previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="ed4ed-194">Het volgende voorbeeld wordt een JSON-document met de huidige configuratie voor de `core-site` onderdeel.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-194">This example returns a JSON document containing the current configuration for the `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="ed4ed-195">Voorbeeld: Update-configuratie</span><span class="sxs-lookup"><span data-stu-id="ed4ed-195">Example: Update configuration</span></span>

1. <span data-ttu-id="ed4ed-196">De huidige configuratie Ambari worden opgeslagen als 'gewenste configuratie' ophalen:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-196">Get the current configuration, which Ambari stores as the "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="ed4ed-197">Het volgende voorbeeld wordt een JSON-document met de huidige configuratie (geïdentificeerd door de *tag* waarde) voor de onderdelen die zijn geïnstalleerd op het cluster.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-197">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="ed4ed-198">Het volgende voorbeeld is een fragment van de gegevens van een Spark-clustertype geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-198">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
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
   
    <span data-ttu-id="ed4ed-199">In deze lijst, moet u de naam van het onderdeel kopiëren (bijvoorbeeld **spark\_thrift\_sparkconf** en de **tag** waarde.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-199">From this list, you need to copy the name of the component (for example, **spark\_thrift\_sparkconf** and the **tag** value.</span></span>

2. <span data-ttu-id="ed4ed-200">De configuratie voor het onderdeel en de tag ophalen met behulp van de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-200">Retrieve the configuration for the component and tag by using the following commands:</span></span>
   
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
    > <span data-ttu-id="ed4ed-201">Vervang **spark-thrift-sparkconf** en **INITIËLE** met het onderdeel en code die u wilt ophalen van de configuratie voor.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-201">Replace **spark-thrift-sparkconf** and **INITIAL** with the component and tag that you want to retrieve the configuration for.</span></span>
   
    <span data-ttu-id="ed4ed-202">Jq wordt gebruikt voor het inschakelen van de gegevens opgehaald uit HDInsight naar een nieuwe configuratiesjabloon.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-202">Jq is used to turn the data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="ed4ed-203">Deze voorbeelden wordt met name de volgende acties uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-203">Specifically, these examples perform the following actions:</span></span>
   
    * <span data-ttu-id="ed4ed-204">Hiermee maakt u een unieke waarde met de tekenreeks 'versie' en de datum die wordt opgeslagen in `newtag`.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-204">Creates a unique value containing the string "version" and the date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="ed4ed-205">Maakt een document hoofdmap voor de nieuwe gewenste configuratie.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-205">Creates a root document for the new desired configuration.</span></span>

    * <span data-ttu-id="ed4ed-206">Met deze eigenschap wordt de inhoud van de `.items[]` matrix en toegevoegd onder de **desired_config** element.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-206">Gets the contents of the `.items[]` array and adds it under the **desired_config** element.</span></span>

    * <span data-ttu-id="ed4ed-207">Hiermee verwijdert u de `href`, `version`, en `Config` elementen, als deze elementen niet nodig zijn voor het verzenden van een nieuwe configuratie.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-207">Deletes the `href`, `version`, and `Config` elements, as these elements aren't needed to submit a new configuration.</span></span>

    * <span data-ttu-id="ed4ed-208">Voegt een `tag` element met een waarde van `version#################`.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="ed4ed-209">Het numerieke gedeelte is gebaseerd op de huidige datum.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-209">The numeric portion is based on the current date.</span></span> <span data-ttu-id="ed4ed-210">Elke configuratie moet een unieke code hebben.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="ed4ed-211">Ten slotte de gegevens wordt opgeslagen in de `newconfig.json` document.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-211">Finally, the data is saved to the `newconfig.json` document.</span></span> <span data-ttu-id="ed4ed-212">De documentstructuur ziet er ongeveer als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-212">The document structure should appear similar to the following example:</span></span>
     
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

3. <span data-ttu-id="ed4ed-213">Open de `newconfig.json` wijzigen/toevoegen en documenten waarden in de `properties` object.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-213">Open the `newconfig.json` document and modify/add values in the `properties` object.</span></span> <span data-ttu-id="ed4ed-214">Het volgende voorbeeld wordt de waarde van `"spark.yarn.am.memory"` van `"1g"` naar `"3g"`.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-214">The following example changes the value of `"spark.yarn.am.memory"` from `"1g"` to `"3g"`.</span></span> <span data-ttu-id="ed4ed-215">Voegt ook `"spark.kryoserializer.buffer.max"` met een waarde van `"256m"`.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="ed4ed-216">Sla het bestand als u klaar bent wijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-216">Save the file once you are done making modifications.</span></span>

4. <span data-ttu-id="ed4ed-217">Gebruik de volgende opdrachten in de bijgewerkte configuratie om Ambari te verzenden.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-217">Use the following commands to submit the updated configuration to Ambari.</span></span>
   
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
   
    <span data-ttu-id="ed4ed-218">Deze opdrachten verzenden van de inhoud van de **newconfig.json** bestand aan het cluster als de nieuwe gewenste configuratie.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-218">These commands submit the contents of the **newconfig.json** file to the cluster as the new desired configuration.</span></span> <span data-ttu-id="ed4ed-219">De aanvraag retourneert een JSON-document.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-219">The request returns a JSON document.</span></span> <span data-ttu-id="ed4ed-220">De **versionTag** element in dit document moet overeenkomen met de versie die u hebt ingediend, en de **configs** object bevat de configuratiewijzigingen die u hebt aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-220">The **versionTag** element in this document should match the version you submitted, and the **configs** object contains the configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="ed4ed-221">Voorbeeld: Start opnieuw op een serviceonderdeel</span><span class="sxs-lookup"><span data-stu-id="ed4ed-221">Example: Restart a service component</span></span>

<span data-ttu-id="ed4ed-222">Op dit punt als u de Ambari-webgebruikersinterface bekijkt, de Spark-service geeft aan dat deze opnieuw worden opgestart moet voordat de nieuwe configuratie van kracht.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-222">At this point, if you look at the Ambari web UI, the Spark service indicates that it needs to be restarted before the new configuration can take effect.</span></span> <span data-ttu-id="ed4ed-223">Gebruik de volgende stappen uit de service te starten.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-223">Use the following steps to restart the service.</span></span>

1. <span data-ttu-id="ed4ed-224">Gebruik de volgende onderhoudsmodus voor de Spark-service inschakelen:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-224">Use the following to enable maintenance mode for the Spark service:</span></span>

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
   
    <span data-ttu-id="ed4ed-225">Deze opdrachten wordt een JSON-document verzenden naar de server die Hiermee schakelt u onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-225">These commands send a JSON document to the server that turns on maintenance mode.</span></span> <span data-ttu-id="ed4ed-226">U kunt controleren of de service nu in de onderhoudsmodus met de volgende aanvraag:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-226">You can verify that the service is now in maintenance mode using the following request:</span></span>
   
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
   
    <span data-ttu-id="ed4ed-227">De geretourneerde waarde is `ON`.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-227">The return value is `ON`.</span></span>

2. <span data-ttu-id="ed4ed-228">Gebruik de volgende vervolgens de service uitschakelen:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-228">Next, use the following to turn off the service:</span></span>

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
    
    <span data-ttu-id="ed4ed-229">Het antwoord is vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-229">The response is similar to the following example:</span></span>
   
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
    > <span data-ttu-id="ed4ed-230">De `href` waarde die door deze URI geretourneerd met behulp van het interne IP-adres van het clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-230">The `href` value returned by this URI is using the internal IP address of the cluster node.</span></span> <span data-ttu-id="ed4ed-231">Als u wilt gebruiken van buiten het cluster, kunt u het gedeelte '10.0.0.18:8080' vervangen door de FQDN-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-231">To use it from outside the cluster, replace the \`10.0.0.18:8080' portion with the FQDN of the cluster.</span></span> 
    
    <span data-ttu-id="ed4ed-232">De volgende opdrachten de status van de aanvraag niet ophalen:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-232">The following commands retrieve the status of the request:</span></span>

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

    <span data-ttu-id="ed4ed-233">Een antwoord van `COMPLETED` geeft aan dat de aanvraag is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-233">A response of `COMPLETED` indicates that the request has finished.</span></span>

3. <span data-ttu-id="ed4ed-234">Zodra de vorige aanvraag is voltooid, moet u het volgende gebruiken om de service te starten.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-234">Once the previous request completes, use the following to start the service.</span></span>
   
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
    <span data-ttu-id="ed4ed-235">De service maakt nu gebruik van de nieuwe configuratie.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-235">The service is now using the new configuration.</span></span>

4. <span data-ttu-id="ed4ed-236">Gebruik tot slot de volgende onderhoudsmodus uit te schakelen.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-236">Finally, use the following to turn off maintenance mode.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="ed4ed-237">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ed4ed-237">Next steps</span></span>

<span data-ttu-id="ed4ed-238">Zie voor een volledig overzicht van de REST API [Ambari-API-verwijzing V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-238">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>


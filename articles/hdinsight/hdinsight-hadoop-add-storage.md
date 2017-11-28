---
title: Extra Azure storage-accounts toevoegen aan HDInsight | Microsoft Docs
description: Informatie over het toevoegen van extra Azure storage-accounts aan een bestaand HDInsight-cluster.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 0853e8605e07c28867676e9c13b89263ade67c88
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="add-additional-storage-accounts-to-hdinsight"></a><span data-ttu-id="e3b26-103">Extra opslagaccounts toevoegen aan HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3b26-103">Add additional storage accounts to HDInsight</span></span>

<span data-ttu-id="e3b26-104">Informatie over het gebruik van scriptacties extra Azure storage-accounts toevoegen aan HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e3b26-104">Learn how to use script actions to add additional Azure storage accounts to HDInsight.</span></span> <span data-ttu-id="e3b26-105">De stappen in dit document wordt een opslagaccount toevoegen aan een bestaand Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e3b26-105">The steps in this document add a storage account to an existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3b26-106">De informatie in dit document is over het toevoegen van extra opslagruimte aan een cluster nadat deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e3b26-106">The information in this document is about adding additional storage to a cluster after it has been created.</span></span> <span data-ttu-id="e3b26-107">Zie voor meer informatie over het storage-accounts toevoegen tijdens het maken van het cluster [clusters in HDInsight met Hadoop, Spark en Kafka instellen](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="e3b26-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="e3b26-108">Hoe werkt het</span><span class="sxs-lookup"><span data-stu-id="e3b26-108">How it works</span></span>

<span data-ttu-id="e3b26-109">Dit script bevat de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="e3b26-109">This script takes the following parameters:</span></span>

* <span data-ttu-id="e3b26-110">__Naam van het Azure-opslagaccount__: de naam van het storage-account toevoegen aan het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e3b26-110">__Azure storage account name__: The name of the storage account to add to the HDInsight cluster.</span></span> <span data-ttu-id="e3b26-111">HDInsight kan na het uitvoeren van het script, lezen en schrijven gegevens opgeslagen in dit opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e3b26-111">After running the script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="e3b26-112">__Azure-toegangssleutel__: een sleutel die toegang tot het opslagaccount verleent.</span><span class="sxs-lookup"><span data-stu-id="e3b26-112">__Azure storage account key__: A key that grants access to the storage account.</span></span>

* <span data-ttu-id="e3b26-113">__-p__ (optioneel): als u opgeeft, wordt de sleutel is niet versleuteld en wordt opgeslagen in het bestand core site.xml als tekst zonder opmaak.</span><span class="sxs-lookup"><span data-stu-id="e3b26-113">__-p__ (optional): If specified, the key is not encrypted and is stored in the core-site.xml file as plain text.</span></span>

<span data-ttu-id="e3b26-114">Tijdens de verwerking van het script worden de volgende acties uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="e3b26-114">During processing, the script performs the following actions:</span></span>

* <span data-ttu-id="e3b26-115">Als het opslagaccount al in de configuratie van de core site.xml voor het cluster bestaat, het script wordt afgesloten en er is geen verdere acties worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e3b26-115">If the storage account already exists in the core-site.xml configuration for the cluster, the script exits and no further actions are performed.</span></span>

* <span data-ttu-id="e3b26-116">Hiermee wordt gecontroleerd of het opslagaccount bestaat en toegankelijk is met de sleutel.</span><span class="sxs-lookup"><span data-stu-id="e3b26-116">Verifies that the storage account exists and can be accessed using the key.</span></span>

* <span data-ttu-id="e3b26-117">Versleutelt de sleutel met de referenties van het cluster.</span><span class="sxs-lookup"><span data-stu-id="e3b26-117">Encrypts the key using the cluster credential.</span></span>

* <span data-ttu-id="e3b26-118">Het storage-account aan het bestand core site.xml toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e3b26-118">Adds the storage account to the core-site.xml file.</span></span>

* <span data-ttu-id="e3b26-119">Stopt en de Oozie, YARN MapReduce2 en HDFS-services opnieuw gestart.</span><span class="sxs-lookup"><span data-stu-id="e3b26-119">Stops and restarts the Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="e3b26-120">Deze services starten en stoppen, kunnen ze het nieuwe opslagaccount gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e3b26-120">Stopping and starting these services allows them to use the new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="e3b26-121">Met behulp van een opslagaccount in een andere locatie dan het HDInsight-cluster wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e3b26-121">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="the-script"></a><span data-ttu-id="e3b26-122">Het script</span><span class="sxs-lookup"><span data-stu-id="e3b26-122">The script</span></span>

<span data-ttu-id="e3b26-123">__Locatie script__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="e3b26-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="e3b26-124">__Vereisten__:</span><span class="sxs-lookup"><span data-stu-id="e3b26-124">__Requirements__:</span></span>

* <span data-ttu-id="e3b26-125">Het script moet worden toegepast op de __hoofdknooppunten__.</span><span class="sxs-lookup"><span data-stu-id="e3b26-125">The script must be applied on the __Head nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="e3b26-126">Het script gebruiken</span><span class="sxs-lookup"><span data-stu-id="e3b26-126">To use the script</span></span>

<span data-ttu-id="e3b26-127">Dit script kan worden gebruikt vanuit de Azure-portal, Azure PowerShell of de Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="e3b26-127">This script can be used from the Azure portal, Azure PowerShell, or the Azure CLI 1.0.</span></span> <span data-ttu-id="e3b26-128">Zie voor meer informatie de [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span><span class="sxs-lookup"><span data-stu-id="e3b26-128">For more information, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3b26-129">Wanneer u de stappen in het document aanpassing, gebruik de volgende informatie om dit script te passen:</span><span class="sxs-lookup"><span data-stu-id="e3b26-129">When using the steps provided in the customization document, use the following information to apply this script:</span></span>
>
> * <span data-ttu-id="e3b26-130">Een voorbeeld-scriptactie URI vervangen door de URI voor dit script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="e3b26-130">Replace any example script action URI with the URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="e3b26-131">Van de voorbeeldparameters vervangen door de naam van het Azure-opslagaccount en de sleutel van het opslagaccount moet worden toegevoegd aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="e3b26-131">Replace any example parameters with the Azure storage account name and key of the storage account to be added to the cluster.</span></span> <span data-ttu-id="e3b26-132">Als u de Azure portal gebruikt, moeten deze parameters worden gescheiden door een spatie.</span><span class="sxs-lookup"><span data-stu-id="e3b26-132">If using the Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="e3b26-133">U hoeft niet te markeren met dit script als __persistente__, zoals de Ambari-configuratie voor het cluster rechtstreeks worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e3b26-133">You do not need to mark this script as __Persisted__, as it directly updates the Ambari configuration for the cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="e3b26-134">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="e3b26-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="e3b26-135">Storage-accounts niet weergegeven in de Azure portal of hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="e3b26-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="e3b26-136">Wanneer het HDInsight-cluster bekijkt in de Azure-portal, selecteert de __Opslagaccounts__ item onder __eigenschappen__ storage-accounts die zijn toegevoegd met deze scriptactie niet wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e3b26-136">When viewing the HDInsight cluster in the Azure portal, selecting the __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="e3b26-137">Azure PowerShell en Azure CLI weergeven niet het extra opslagaccount ofwel.</span><span class="sxs-lookup"><span data-stu-id="e3b26-137">Azure PowerShell and Azure CLI do not display the additional storage account either.</span></span>

<span data-ttu-id="e3b26-138">De storage-gegevens wordt niet weergegeven omdat het script wijzigt u alleen de core site.xml-configuratie voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="e3b26-138">The storage information isn't displayed because the script only modifies the core-site.xml configuration for the cluster.</span></span> <span data-ttu-id="e3b26-139">Deze informatie wordt niet gebruikt bij het ophalen van de clustergegevens met behulp van Azure management API's.</span><span class="sxs-lookup"><span data-stu-id="e3b26-139">This information is not used when retrieving the cluster information using Azure management APIs.</span></span>

<span data-ttu-id="e3b26-140">Om weer te geven gegevens van de storage-account is toegevoegd aan het cluster met dit script, moet u de Ambari REST-API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e3b26-140">To view storage account information added to the cluster using this script, use the Ambari REST API.</span></span> <span data-ttu-id="e3b26-141">Gebruik de volgende opdrachten in deze informatie voor uw cluster op te halen:</span><span class="sxs-lookup"><span data-stu-id="e3b26-141">Use the following commands to retrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter the cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="e3b26-142">Stel `$clusterName` op de naam van het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e3b26-142">Set `$clusterName` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="e3b26-143">Stel `$storageAccountName` op de naam van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e3b26-143">Set `$storageAccountName` to the name of the storage account.</span></span> <span data-ttu-id="e3b26-144">Wanneer u wordt gevraagd, typt u de cluster-aanmelding (admin) en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="e3b26-144">When prompted, enter the cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="e3b26-145">Stel `$PASSWORD` op het accountwachtwoord van de cluster-aanmelding (admin).</span><span class="sxs-lookup"><span data-stu-id="e3b26-145">Set `$PASSWORD` to the cluster login (admin) account password.</span></span> <span data-ttu-id="e3b26-146">Stel `$CLUSTERNAME` op de naam van het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e3b26-146">Set `$CLUSTERNAME` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="e3b26-147">Stel `$STORAGEACCOUNTNAME` op de naam van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e3b26-147">Set `$STORAGEACCOUNTNAME` to the name of the storage account.</span></span>
>
> <span data-ttu-id="e3b26-148">In dit voorbeeld wordt [curl (http://curl.haxx.se/)](http://curl.haxx.se/) en [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) op te halen en JSON-gegevens parseren.</span><span class="sxs-lookup"><span data-stu-id="e3b26-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) to retrieve and parse JSON data.</span></span>

<span data-ttu-id="e3b26-149">Wanneer u deze opdracht gebruikt, vervangen __CLUSTERNAME__ met de naam van het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e3b26-149">When using this command, replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="e3b26-150">Vervang __wachtwoord__ met het aanmeldingswachtwoord HTTP voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="e3b26-150">Replace __PASSWORD__ with the HTTP login password for the cluster.</span></span> <span data-ttu-id="e3b26-151">Vervang __STORAGEACCOUNT__ met de naam van het opslagaccount met behulp van de scriptactie toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e3b26-151">Replace __STORAGEACCOUNT__ with the name of the storage account added using script action.</span></span> <span data-ttu-id="e3b26-152">Met deze opdracht geretourneerde informatie lijkt op de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="e3b26-152">Information returned from this command appears similar to the following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="e3b26-153">Deze tekst is een voorbeeld van een versleutelde sleutel die wordt gebruikt voor toegang tot het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e3b26-153">This text is an example of an encrypted key, which is used to access the storage account.</span></span>

### <a name="unable-to-access-storage-after-changing-key"></a><span data-ttu-id="e3b26-154">Kan geen toegang hebben tot opslag na het wijzigen van de sleutel</span><span class="sxs-lookup"><span data-stu-id="e3b26-154">Unable to access storage after changing key</span></span>

<span data-ttu-id="e3b26-155">Als u de sleutel voor een opslagaccount wijzigt, HDInsight kan geen toegang meer tot het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e3b26-155">If you change the key for a storage account, HDInsight can no longer access the storage account.</span></span> <span data-ttu-id="e3b26-156">HDInsight gebruikt een cachekopie van de sleutel in het core site.xml voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="e3b26-156">HDInsight uses a cached copy of key in the core-site.xml for the cluster.</span></span> <span data-ttu-id="e3b26-157">Dit exemplaar in de cache moet worden bijgewerkt zodat deze overeenkomen met de nieuwe sleutel.</span><span class="sxs-lookup"><span data-stu-id="e3b26-157">This cached copy must be updated to match the new key.</span></span>

<span data-ttu-id="e3b26-158">Het script opnieuw uitgevoerd biedt __niet__ de sleutel wordt bijgewerkt als het script wordt gecontroleerd of er al een vermelding voor het opslagaccount bestaat.</span><span class="sxs-lookup"><span data-stu-id="e3b26-158">Running the script action again does __not__ update the key, as the script checks to see if an entry for the storage account already exists.</span></span> <span data-ttu-id="e3b26-159">Als er al een item bestaat, biedt het geen wijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="e3b26-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="e3b26-160">U kunt dit probleem omzeilen, moet u de bestaande vermelding voor de storage-account verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e3b26-160">To work around this problem, you must remove the existing entry for the storage account.</span></span> <span data-ttu-id="e3b26-161">Gebruik de volgende stappen uit om te verwijderen van het bestaande item:</span><span class="sxs-lookup"><span data-stu-id="e3b26-161">Use the following steps to remove the existing entry:</span></span>

1. <span data-ttu-id="e3b26-162">Open de Ambari-Webgebruikersinterface voor uw HDInsight-cluster in een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="e3b26-162">In a web browser, open the Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="e3b26-163">De URI is https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="e3b26-163">The URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="e3b26-164">Vervang __CLUSTERNAME__ door de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="e3b26-164">Replace __CLUSTERNAME__ with the name of your cluster.</span></span>

    <span data-ttu-id="e3b26-165">Wanneer u wordt gevraagd, typt u de HTTP-aanmeldingsgebruiker en het wachtwoord voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="e3b26-165">When prompted, enter the HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="e3b26-166">Selecteer in de lijst van services aan de linkerkant van de pagina __HDFS__.</span><span class="sxs-lookup"><span data-stu-id="e3b26-166">From the list of services on the left of the page, select __HDFS__.</span></span> <span data-ttu-id="e3b26-167">Selecteer vervolgens de __Configs__ tabblad in het midden van de pagina.</span><span class="sxs-lookup"><span data-stu-id="e3b26-167">Then select the __Configs__ tab in the center of the page.</span></span>

3. <span data-ttu-id="e3b26-168">In de __Filter...__  en voer een waarde van __fs.azure.account__.</span><span class="sxs-lookup"><span data-stu-id="e3b26-168">In the __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="e3b26-169">Hiermee wordt de vermeldingen voor elke extra opslagaccounts die zijn toegevoegd aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="e3b26-169">This returns entries for any additional storage accounts that have been added to the cluster.</span></span> <span data-ttu-id="e3b26-170">Er zijn twee soorten posten; __keyprovider__ en __sleutel__.</span><span class="sxs-lookup"><span data-stu-id="e3b26-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="e3b26-171">Zowel bevatten de naam van het opslagaccount als onderdeel van de naam van de sleutel.</span><span class="sxs-lookup"><span data-stu-id="e3b26-171">Both contain the name of the storage account as part of the key name.</span></span>

    <span data-ttu-id="e3b26-172">Hieronder vindt u voorbeelden van vermeldingen voor een opslagaccount met de naam __mystorage__:</span><span class="sxs-lookup"><span data-stu-id="e3b26-172">The following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="e3b26-173">Nadat u hebt vastgesteld dat de sleutels voor het opslagaccount dat u wilt verwijderen, gebruikt u de rode '-' pictogram aan de rechterkant van de vermelding te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e3b26-173">After you have identified the keys for the storage account you need to remove, use the red '-' icon to the right of the entry to delete it.</span></span> <span data-ttu-id="e3b26-174">Gebruik vervolgens de __opslaan__ knop uw wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="e3b26-174">Then use the __Save__ button to save your changes.</span></span>

5. <span data-ttu-id="e3b26-175">Nadat wijzigingen zijn opgeslagen, gebruikt u de scriptactie de storage-account en de nieuwe sleutelwaarde toevoegen aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="e3b26-175">After changes have been saved, use the script action to add the storage account and new key value to the cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="e3b26-176">Slechte prestaties</span><span class="sxs-lookup"><span data-stu-id="e3b26-176">Poor performance</span></span>

<span data-ttu-id="e3b26-177">Als het opslagaccount zich in een andere regio dan het HDInsight-cluster, kan u verminderde prestaties ervaren.</span><span class="sxs-lookup"><span data-stu-id="e3b26-177">If the storage account is in a different region than the HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="e3b26-178">Toegang tot gegevens in een andere regio verzendt netwerkverkeer buiten het regionale Azure datacenter en via het openbare internet; dit leiden latentie tot kan.</span><span class="sxs-lookup"><span data-stu-id="e3b26-178">Accessing data in a different region sends network traffic outside the regional Azure data center and across the public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="e3b26-179">Met behulp van een opslagaccount in een andere regio dan het HDInsight-cluster wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e3b26-179">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="e3b26-180">Extra kosten</span><span class="sxs-lookup"><span data-stu-id="e3b26-180">Additional charges</span></span>

<span data-ttu-id="e3b26-181">Als het opslagaccount zich in een andere regio dan het HDInsight-cluster, merkt u wellicht aanvullende uitgaande kosten op uw Azure-facturering.</span><span class="sxs-lookup"><span data-stu-id="e3b26-181">If the storage account is in a different region than the HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="e3b26-182">Een uitgaande kosten wordt toegepast wanneer de gegevens blijft een regionaal datacenter.</span><span class="sxs-lookup"><span data-stu-id="e3b26-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="e3b26-183">Deze kosten is toegepast, zelfs als het verkeer is bestemd voor een andere Azure-datacenter in een andere regio.</span><span class="sxs-lookup"><span data-stu-id="e3b26-183">This charge is applied even if the traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="e3b26-184">Met behulp van een opslagaccount in een andere regio dan het HDInsight-cluster wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e3b26-184">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3b26-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e3b26-185">Next steps</span></span>

<span data-ttu-id="e3b26-186">U hebt geleerd hoe extra opslagaccounts toevoegen aan een bestaand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e3b26-186">You have learned how to add additional storage accounts to an existing HDInsight cluster.</span></span> <span data-ttu-id="e3b26-187">Zie voor meer informatie over scriptacties [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="e3b26-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>

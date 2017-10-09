---
title: aaaAdd extra Azure storage-accounts tooHDInsight | Microsoft Docs
description: Meer informatie over hoe tooadd extra Azure storage-accounts tooan bestaand HDInsight-cluster.
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
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a><span data-ttu-id="721bb-103">Extra storage accounts tooHDInsight toevoegen</span><span class="sxs-lookup"><span data-stu-id="721bb-103">Add additional storage accounts tooHDInsight</span></span>

<span data-ttu-id="721bb-104">Meer informatie over hoe toouse script acties tooadd extra Azure storage-accounts tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="721bb-104">Learn how toouse script actions tooadd additional Azure storage accounts tooHDInsight.</span></span> <span data-ttu-id="721bb-105">Hallo toevoegen stappen in dit document een storage account tooan bestaand Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="721bb-105">hello steps in this document add a storage account tooan existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="721bb-106">Hallo-informatie in dit document is over het toevoegen van extra opslagruimte tooa cluster nadat deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="721bb-106">hello information in this document is about adding additional storage tooa cluster after it has been created.</span></span> <span data-ttu-id="721bb-107">Zie voor meer informatie over het storage-accounts toevoegen tijdens het maken van het cluster [clusters in HDInsight met Hadoop, Spark en Kafka instellen](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="721bb-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="721bb-108">Hoe werkt het?</span><span class="sxs-lookup"><span data-stu-id="721bb-108">How it works</span></span>

<span data-ttu-id="721bb-109">Dit script neemt Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="721bb-109">This script takes hello following parameters:</span></span>

* <span data-ttu-id="721bb-110">__Naam van het Azure-opslagaccount__: Hallo-naam van Hallo storage account tooadd toohello HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="721bb-110">__Azure storage account name__: hello name of hello storage account tooadd toohello HDInsight cluster.</span></span> <span data-ttu-id="721bb-111">HDInsight kan na het uitvoeren van script Hallo lezen en schrijven gegevens opgeslagen in dit opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="721bb-111">After running hello script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="721bb-112">__Azure-toegangssleutel__: een sleutel die toohello storage-toegangsaccount verleent.</span><span class="sxs-lookup"><span data-stu-id="721bb-112">__Azure storage account key__: A key that grants access toohello storage account.</span></span>

* <span data-ttu-id="721bb-113">__-p__ (optioneel): als u opgeeft, Hallo-sleutel is niet versleuteld en wordt opgeslagen in bestand van de core-site.xml Hallo als tekst zonder opmaak.</span><span class="sxs-lookup"><span data-stu-id="721bb-113">__-p__ (optional): If specified, hello key is not encrypted and is stored in hello core-site.xml file as plain text.</span></span>

<span data-ttu-id="721bb-114">Tijdens de verwerking voert Hallo script Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="721bb-114">During processing, hello script performs hello following actions:</span></span>

* <span data-ttu-id="721bb-115">Als hello storage-account al in de configuratie van de Hallo core site.xml voor Hallo cluster bestaat, Hallo script wordt afgesloten en er is geen verdere acties worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="721bb-115">If hello storage account already exists in hello core-site.xml configuration for hello cluster, hello script exits and no further actions are performed.</span></span>

* <span data-ttu-id="721bb-116">Verifieert of Hallo storage-account bestaat en toegankelijk is met Hallo-sleutel.</span><span class="sxs-lookup"><span data-stu-id="721bb-116">Verifies that hello storage account exists and can be accessed using hello key.</span></span>

* <span data-ttu-id="721bb-117">Hallo-sleutel met behulp van Hallo cluster referentie worden versleuteld.</span><span class="sxs-lookup"><span data-stu-id="721bb-117">Encrypts hello key using hello cluster credential.</span></span>

* <span data-ttu-id="721bb-118">Voegt Hallo account toohello core site.xml opslagbestand.</span><span class="sxs-lookup"><span data-stu-id="721bb-118">Adds hello storage account toohello core-site.xml file.</span></span>

* <span data-ttu-id="721bb-119">Stopt en Hallo Oozie, YARN MapReduce2 en HDFS-services opnieuw start.</span><span class="sxs-lookup"><span data-stu-id="721bb-119">Stops and restarts hello Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="721bb-120">Deze services starten en stoppen kan ze toouse Hallo nieuw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="721bb-120">Stopping and starting these services allows them toouse hello new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="721bb-121">Met behulp van een opslagaccount in een andere locatie dan Hallo HDInsight-cluster wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="721bb-121">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="hello-script"></a><span data-ttu-id="721bb-122">Hallo-script</span><span class="sxs-lookup"><span data-stu-id="721bb-122">hello script</span></span>

<span data-ttu-id="721bb-123">__Locatie script__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="721bb-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="721bb-124">__Vereisten__:</span><span class="sxs-lookup"><span data-stu-id="721bb-124">__Requirements__:</span></span>

* <span data-ttu-id="721bb-125">Hallo script moet worden toegepast op Hallo __hoofdknooppunten__.</span><span class="sxs-lookup"><span data-stu-id="721bb-125">hello script must be applied on hello __Head nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="721bb-126">toouse hello script</span><span class="sxs-lookup"><span data-stu-id="721bb-126">toouse hello script</span></span>

<span data-ttu-id="721bb-127">Dit script kan worden gebruikt vanuit hello Azure-portal, Azure PowerShell of Azure CLI 1.0 Hallo.</span><span class="sxs-lookup"><span data-stu-id="721bb-127">This script can be used from hello Azure portal, Azure PowerShell, or hello Azure CLI 1.0.</span></span> <span data-ttu-id="721bb-128">Zie voor meer informatie, Hallo [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span><span class="sxs-lookup"><span data-stu-id="721bb-128">For more information, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="721bb-129">Wanneer u stappen Hallo in Hallo aanpassing document, gebruikt u Hallo informatie tooapply na dit script:</span><span class="sxs-lookup"><span data-stu-id="721bb-129">When using hello steps provided in hello customization document, use hello following information tooapply this script:</span></span>
>
> * <span data-ttu-id="721bb-130">Een voorbeeld-scriptactie URI vervangen door Hallo URI voor dit script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="721bb-130">Replace any example script action URI with hello URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="721bb-131">Van de voorbeeldparameters vervangen door hello Azure storage-accountnaam en de sleutel van Hallo account toobe toegevoegde toohello opslagcluster.</span><span class="sxs-lookup"><span data-stu-id="721bb-131">Replace any example parameters with hello Azure storage account name and key of hello storage account toobe added toohello cluster.</span></span> <span data-ttu-id="721bb-132">Als u met behulp van hello Azure-portal, moeten deze parameters worden gescheiden door een spatie.</span><span class="sxs-lookup"><span data-stu-id="721bb-132">If using hello Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="721bb-133">U hoeft geen toomark dit script als __persistente__, zoals Hallo Ambari-configuratie voor Hallo cluster rechtstreeks worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="721bb-133">You do not need toomark this script as __Persisted__, as it directly updates hello Ambari configuration for hello cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="721bb-134">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="721bb-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="721bb-135">Storage-accounts niet weergegeven in de Azure portal of hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="721bb-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="721bb-136">Wanneer de weergave Hallo HDInsight-cluster in hello Azure-portal, selecteert u Hallo __Opslagaccounts__ item onder __eigenschappen__ storage-accounts die zijn toegevoegd met deze scriptactie niet wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="721bb-136">When viewing hello HDInsight cluster in hello Azure portal, selecting hello __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="721bb-137">Azure PowerShell en Azure CLI weergeven geen Hallo extra opslagruimte account ofwel.</span><span class="sxs-lookup"><span data-stu-id="721bb-137">Azure PowerShell and Azure CLI do not display hello additional storage account either.</span></span>

<span data-ttu-id="721bb-138">Hallo storage-gegevens wordt niet weergegeven omdat Hallo script alleen Hallo core site.xml-configuratie voor Hallo-cluster wijzigen.</span><span class="sxs-lookup"><span data-stu-id="721bb-138">hello storage information isn't displayed because hello script only modifies hello core-site.xml configuration for hello cluster.</span></span> <span data-ttu-id="721bb-139">Deze informatie wordt niet gebruikt bij het ophalen van clustergegevens Hallo met behulp van Azure management API's.</span><span class="sxs-lookup"><span data-stu-id="721bb-139">This information is not used when retrieving hello cluster information using Azure management APIs.</span></span>

<span data-ttu-id="721bb-140">gegevens van tooview storage-account toegevoegd toohello cluster met dit script, gebruik Hallo Ambari REST-API.</span><span class="sxs-lookup"><span data-stu-id="721bb-140">tooview storage account information added toohello cluster using this script, use hello Ambari REST API.</span></span> <span data-ttu-id="721bb-141">Hallo opdrachten tooretrieve na deze informatie voor uw cluster gebruiken:</span><span class="sxs-lookup"><span data-stu-id="721bb-141">Use hello following commands tooretrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="721bb-142">Stel `$clusterName` toohello-naam van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="721bb-142">Set `$clusterName` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="721bb-143">Stel `$storageAccountName` toohello-naam van Hallo-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="721bb-143">Set `$storageAccountName` toohello name of hello storage account.</span></span> <span data-ttu-id="721bb-144">Voer desgevraagd Hallo cluster aanmeldingsnaam (admin) en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="721bb-144">When prompted, enter hello cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="721bb-145">Stel `$PASSWORD` toohello cluster (admin) account aanmeldingswachtwoord.</span><span class="sxs-lookup"><span data-stu-id="721bb-145">Set `$PASSWORD` toohello cluster login (admin) account password.</span></span> <span data-ttu-id="721bb-146">Stel `$CLUSTERNAME` toohello-naam van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="721bb-146">Set `$CLUSTERNAME` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="721bb-147">Stel `$STORAGEACCOUNTNAME` toohello-naam van Hallo-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="721bb-147">Set `$STORAGEACCOUNTNAME` toohello name of hello storage account.</span></span>
>
> <span data-ttu-id="721bb-148">In dit voorbeeld wordt [curl (http://curl.haxx.se/)](http://curl.haxx.se/) en [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve en parse JSON-gegevens.</span><span class="sxs-lookup"><span data-stu-id="721bb-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve and parse JSON data.</span></span>

<span data-ttu-id="721bb-149">Wanneer u deze opdracht gebruikt, vervangen __CLUSTERNAME__ met de naam van de HDInsight-cluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="721bb-149">When using this command, replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="721bb-150">Vervang __wachtwoord__ met Hallo HTTP aanmeldingswachtwoord voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="721bb-150">Replace __PASSWORD__ with hello HTTP login password for hello cluster.</span></span> <span data-ttu-id="721bb-151">Vervang __STORAGEACCOUNT__ met de naam van Hallo storage-account is toegevoegd met behulp van de scriptactie Hallo.</span><span class="sxs-lookup"><span data-stu-id="721bb-151">Replace __STORAGEACCOUNT__ with hello name of hello storage account added using script action.</span></span> <span data-ttu-id="721bb-152">Informatie die wordt geretourneerd met deze opdracht wordt weergegeven vergelijkbaar toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="721bb-152">Information returned from this command appears similar toohello following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="721bb-153">Deze tekst is een voorbeeld van een versleutelde sleutel die wordt gebruikt tooaccess Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="721bb-153">This text is an example of an encrypted key, which is used tooaccess hello storage account.</span></span>

### <a name="unable-tooaccess-storage-after-changing-key"></a><span data-ttu-id="721bb-154">Kan geen tooaccess opslag na het wijzigen van de sleutel</span><span class="sxs-lookup"><span data-stu-id="721bb-154">Unable tooaccess storage after changing key</span></span>

<span data-ttu-id="721bb-155">Als u Hallo-sleutel voor een opslagaccount wijzigt, HDInsight kan geen toegang meer tot Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="721bb-155">If you change hello key for a storage account, HDInsight can no longer access hello storage account.</span></span> <span data-ttu-id="721bb-156">HDInsight maakt gebruik van een cachekopie van sleutel Hallo core site.xml voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="721bb-156">HDInsight uses a cached copy of key in hello core-site.xml for hello cluster.</span></span> <span data-ttu-id="721bb-157">Deze in de cache opgeslagen kopie moet bijgewerkte toomatch Hallo nieuwe sleutel.</span><span class="sxs-lookup"><span data-stu-id="721bb-157">This cached copy must be updated toomatch hello new key.</span></span>

<span data-ttu-id="721bb-158">Hallo script opnieuw uitgevoerd biedt __niet__ Hallo-sleutel, bijwerken zoals Hallo script toosee controleert u of er al een ingang voor Hallo storage-account bestaat.</span><span class="sxs-lookup"><span data-stu-id="721bb-158">Running hello script action again does __not__ update hello key, as hello script checks toosee if an entry for hello storage account already exists.</span></span> <span data-ttu-id="721bb-159">Als er al een item bestaat, biedt het geen wijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="721bb-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="721bb-160">toowork om dit probleem, moet u bestaande vermelding Hallo voor Hallo storage-account verwijderen.</span><span class="sxs-lookup"><span data-stu-id="721bb-160">toowork around this problem, you must remove hello existing entry for hello storage account.</span></span> <span data-ttu-id="721bb-161">Volgende stappen tooremove Hallo bestaande vermelding hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="721bb-161">Use hello following steps tooremove hello existing entry:</span></span>

1. <span data-ttu-id="721bb-162">Open in een webbrowser, Hallo Ambari-Webgebruikersinterface voor uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="721bb-162">In a web browser, open hello Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="721bb-163">Hallo-URI is https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="721bb-163">hello URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="721bb-164">Vervang __CLUSTERNAME__ met Hallo-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="721bb-164">Replace __CLUSTERNAME__ with hello name of your cluster.</span></span>

    <span data-ttu-id="721bb-165">Voer desgevraagd Hallo HTTP-aanmelding en het wachtwoord voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="721bb-165">When prompted, enter hello HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="721bb-166">Selecteer in de lijst met services op Hallo links van de pagina Hallo Hallo __HDFS__.</span><span class="sxs-lookup"><span data-stu-id="721bb-166">From hello list of services on hello left of hello page, select __HDFS__.</span></span> <span data-ttu-id="721bb-167">Selecteer vervolgens Hallo __Configs__ tabblad in Hallo midden van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="721bb-167">Then select hello __Configs__ tab in hello center of hello page.</span></span>

3. <span data-ttu-id="721bb-168">In Hallo __Filter...__  en voer een waarde van __fs.azure.account__.</span><span class="sxs-lookup"><span data-stu-id="721bb-168">In hello __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="721bb-169">Hiermee wordt de vermeldingen voor elke extra opslagaccounts die zijn toegevoegd aan de toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="721bb-169">This returns entries for any additional storage accounts that have been added toohello cluster.</span></span> <span data-ttu-id="721bb-170">Er zijn twee soorten posten; __keyprovider__ en __sleutel__.</span><span class="sxs-lookup"><span data-stu-id="721bb-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="721bb-171">Beide bevatten Hallo-naam van de opslagaccount Hallo als onderdeel van de sleutelnaam Hallo.</span><span class="sxs-lookup"><span data-stu-id="721bb-171">Both contain hello name of hello storage account as part of hello key name.</span></span>

    <span data-ttu-id="721bb-172">Hallo hieronder vindt u voorbeelden van vermeldingen voor een opslagaccount met de naam __mystorage__:</span><span class="sxs-lookup"><span data-stu-id="721bb-172">hello following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="721bb-173">Nadat u Hallo sleutels voor opslagaccount Hallo moet u tooremove hebt geïdentificeerd, gebruikt u rode Hallo '-' pictogram toohello rechts van Hallo vermelding toodelete deze.</span><span class="sxs-lookup"><span data-stu-id="721bb-173">After you have identified hello keys for hello storage account you need tooremove, use hello red '-' icon toohello right of hello entry toodelete it.</span></span> <span data-ttu-id="721bb-174">Gebruik vervolgens Hallo __opslaan__ knop toosave uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="721bb-174">Then use hello __Save__ button toosave your changes.</span></span>

5. <span data-ttu-id="721bb-175">Nadat wijzigingen zijn opgeslagen, Hallo script actie tooadd Hallo storage-account en nieuwe sleutelwaarde toohello cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="721bb-175">After changes have been saved, use hello script action tooadd hello storage account and new key value toohello cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="721bb-176">Slechte prestaties</span><span class="sxs-lookup"><span data-stu-id="721bb-176">Poor performance</span></span>

<span data-ttu-id="721bb-177">Als Hallo storage-account zich in een andere regio dan Hallo HDInsight-cluster, treden slechte prestaties.</span><span class="sxs-lookup"><span data-stu-id="721bb-177">If hello storage account is in a different region than hello HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="721bb-178">Toegang tot gegevens in een andere regio verzendt netwerkverkeer buiten Hallo regionale Azure-datacenter en meerdere Hallo openbare internet; dit leiden latentie tot kan.</span><span class="sxs-lookup"><span data-stu-id="721bb-178">Accessing data in a different region sends network traffic outside hello regional Azure data center and across hello public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="721bb-179">Met behulp van een opslagaccount in een andere regio dan Hallo HDInsight-cluster wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="721bb-179">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="721bb-180">Extra kosten</span><span class="sxs-lookup"><span data-stu-id="721bb-180">Additional charges</span></span>

<span data-ttu-id="721bb-181">Als Hallo storage-account zich in een andere regio dan Hallo HDInsight-cluster, merkt u wellicht aanvullende uitgaande kosten op uw Azure-facturering.</span><span class="sxs-lookup"><span data-stu-id="721bb-181">If hello storage account is in a different region than hello HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="721bb-182">Een uitgaande kosten wordt toegepast wanneer de gegevens blijft een regionaal datacenter.</span><span class="sxs-lookup"><span data-stu-id="721bb-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="721bb-183">Deze kosten is toegepast, zelfs als het Hallo-verkeer is bestemd voor een andere Azure-datacenter in een andere regio.</span><span class="sxs-lookup"><span data-stu-id="721bb-183">This charge is applied even if hello traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="721bb-184">Met behulp van een opslagaccount in een andere regio dan Hallo HDInsight-cluster wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="721bb-184">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="721bb-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="721bb-185">Next steps</span></span>

<span data-ttu-id="721bb-186">U hebt geleerd hoe tooadd extra opslagaccounts tooan bestaand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="721bb-186">You have learned how tooadd additional storage accounts tooan existing HDInsight cluster.</span></span> <span data-ttu-id="721bb-187">Zie voor meer informatie over scriptacties [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="721bb-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>

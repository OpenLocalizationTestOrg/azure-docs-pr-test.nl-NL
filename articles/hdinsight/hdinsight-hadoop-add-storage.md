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
# <a name="add-additional-storage-accounts-toohdinsight"></a>Extra storage accounts tooHDInsight toevoegen

Meer informatie over hoe toouse script acties tooadd extra Azure storage-accounts tooHDInsight. Hallo toevoegen stappen in dit document een storage account tooan bestaand Linux gebaseerde HDInsight-cluster.

> [!IMPORTANT]
> Hallo-informatie in dit document is over het toevoegen van extra opslagruimte tooa cluster nadat deze is gemaakt. Zie voor meer informatie over het storage-accounts toevoegen tijdens het maken van het cluster [clusters in HDInsight met Hadoop, Spark en Kafka instellen](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="how-it-works"></a>Hoe werkt het?

Dit script neemt Hallo volgende parameters:

* __Naam van het Azure-opslagaccount__: Hallo-naam van Hallo storage account tooadd toohello HDInsight-cluster. HDInsight kan na het uitvoeren van script Hallo lezen en schrijven gegevens opgeslagen in dit opslagaccount.

* __Azure-toegangssleutel__: een sleutel die toohello storage-toegangsaccount verleent.

* __-p__ (optioneel): als u opgeeft, Hallo-sleutel is niet versleuteld en wordt opgeslagen in bestand van de core-site.xml Hallo als tekst zonder opmaak.

Tijdens de verwerking voert Hallo script Hallo van de volgende activiteiten:

* Als hello storage-account al in de configuratie van de Hallo core site.xml voor Hallo cluster bestaat, Hallo script wordt afgesloten en er is geen verdere acties worden uitgevoerd.

* Verifieert of Hallo storage-account bestaat en toegankelijk is met Hallo-sleutel.

* Hallo-sleutel met behulp van Hallo cluster referentie worden versleuteld.

* Voegt Hallo account toohello core site.xml opslagbestand.

* Stopt en Hallo Oozie, YARN MapReduce2 en HDFS-services opnieuw start. Deze services starten en stoppen kan ze toouse Hallo nieuw opslagaccount.

> [!WARNING]
> Met behulp van een opslagaccount in een andere locatie dan Hallo HDInsight-cluster wordt niet ondersteund.

## <a name="hello-script"></a>Hallo-script

__Locatie script__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)

__Vereisten__:

* Hallo script moet worden toegepast op Hallo __hoofdknooppunten__.

## <a name="toouse-hello-script"></a>toouse hello script

Dit script kan worden gebruikt vanuit hello Azure-portal, Azure PowerShell of Azure CLI 1.0 Hallo. Zie voor meer informatie, Hallo [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.

> [!IMPORTANT]
> Wanneer u stappen Hallo in Hallo aanpassing document, gebruikt u Hallo informatie tooapply na dit script:
>
> * Een voorbeeld-scriptactie URI vervangen door Hallo URI voor dit script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).
> * Van de voorbeeldparameters vervangen door hello Azure storage-accountnaam en de sleutel van Hallo account toobe toegevoegde toohello opslagcluster. Als u met behulp van hello Azure-portal, moeten deze parameters worden gescheiden door een spatie.
> * U hoeft geen toomark dit script als __persistente__, zoals Hallo Ambari-configuratie voor Hallo cluster rechtstreeks worden bijgewerkt.

## <a name="known-issues"></a>Bekende problemen

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a>Storage-accounts niet weergegeven in de Azure portal of hulpprogramma 's

Wanneer de weergave Hallo HDInsight-cluster in hello Azure-portal, selecteert u Hallo __Opslagaccounts__ item onder __eigenschappen__ storage-accounts die zijn toegevoegd met deze scriptactie niet wordt weergegeven. Azure PowerShell en Azure CLI weergeven geen Hallo extra opslagruimte account ofwel.

Hallo storage-gegevens wordt niet weergegeven omdat Hallo script alleen Hallo core site.xml-configuratie voor Hallo-cluster wijzigen. Deze informatie wordt niet gebruikt bij het ophalen van clustergegevens Hallo met behulp van Azure management API's.

gegevens van tooview storage-account toegevoegd toohello cluster met dit script, gebruik Hallo Ambari REST-API. Hallo opdrachten tooretrieve na deze informatie voor uw cluster gebruiken:

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> Stel `$clusterName` toohello-naam van Hallo HDInsight-cluster. Stel `$storageAccountName` toohello-naam van Hallo-opslagaccount. Voer desgevraagd Hallo cluster aanmeldingsnaam (admin) en het wachtwoord.

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> Stel `$PASSWORD` toohello cluster (admin) account aanmeldingswachtwoord. Stel `$CLUSTERNAME` toohello-naam van Hallo HDInsight-cluster. Stel `$STORAGEACCOUNTNAME` toohello-naam van Hallo-opslagaccount.
>
> In dit voorbeeld wordt [curl (http://curl.haxx.se/)](http://curl.haxx.se/) en [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve en parse JSON-gegevens.

Wanneer u deze opdracht gebruikt, vervangen __CLUSTERNAME__ met de naam van de HDInsight-cluster Hallo Hallo. Vervang __wachtwoord__ met Hallo HTTP aanmeldingswachtwoord voor Hallo-cluster. Vervang __STORAGEACCOUNT__ met de naam van Hallo storage-account is toegevoegd met behulp van de scriptactie Hallo. Informatie die wordt geretourneerd met deze opdracht wordt weergegeven vergelijkbaar toohello volgende tekst:

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

Deze tekst is een voorbeeld van een versleutelde sleutel die wordt gebruikt tooaccess Hallo storage-account.

### <a name="unable-tooaccess-storage-after-changing-key"></a>Kan geen tooaccess opslag na het wijzigen van de sleutel

Als u Hallo-sleutel voor een opslagaccount wijzigt, HDInsight kan geen toegang meer tot Hallo storage-account. HDInsight maakt gebruik van een cachekopie van sleutel Hallo core site.xml voor Hallo-cluster. Deze in de cache opgeslagen kopie moet bijgewerkte toomatch Hallo nieuwe sleutel.

Hallo script opnieuw uitgevoerd biedt __niet__ Hallo-sleutel, bijwerken zoals Hallo script toosee controleert u of er al een ingang voor Hallo storage-account bestaat. Als er al een item bestaat, biedt het geen wijzigingen aanbrengen.

toowork om dit probleem, moet u bestaande vermelding Hallo voor Hallo storage-account verwijderen. Volgende stappen tooremove Hallo bestaande vermelding hello gebruiken:

1. Open in een webbrowser, Hallo Ambari-Webgebruikersinterface voor uw HDInsight-cluster. Hallo-URI is https://CLUSTERNAME.azurehdinsight.net. Vervang __CLUSTERNAME__ met Hallo-naam van het cluster.

    Voer desgevraagd Hallo HTTP-aanmelding en het wachtwoord voor uw cluster.

2. Selecteer in de lijst met services op Hallo links van de pagina Hallo Hallo __HDFS__. Selecteer vervolgens Hallo __Configs__ tabblad in Hallo midden van Hallo pagina.

3. In Hallo __Filter...__  en voer een waarde van __fs.azure.account__. Hiermee wordt de vermeldingen voor elke extra opslagaccounts die zijn toegevoegd aan de toohello cluster. Er zijn twee soorten posten; __keyprovider__ en __sleutel__. Beide bevatten Hallo-naam van de opslagaccount Hallo als onderdeel van de sleutelnaam Hallo.

    Hallo hieronder vindt u voorbeelden van vermeldingen voor een opslagaccount met de naam __mystorage__:

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. Nadat u Hallo sleutels voor opslagaccount Hallo moet u tooremove hebt geïdentificeerd, gebruikt u rode Hallo '-' pictogram toohello rechts van Hallo vermelding toodelete deze. Gebruik vervolgens Hallo __opslaan__ knop toosave uw wijzigingen.

5. Nadat wijzigingen zijn opgeslagen, Hallo script actie tooadd Hallo storage-account en nieuwe sleutelwaarde toohello cluster gebruiken.

### <a name="poor-performance"></a>Slechte prestaties

Als Hallo storage-account zich in een andere regio dan Hallo HDInsight-cluster, treden slechte prestaties. Toegang tot gegevens in een andere regio verzendt netwerkverkeer buiten Hallo regionale Azure-datacenter en meerdere Hallo openbare internet; dit leiden latentie tot kan.

> [!WARNING]
> Met behulp van een opslagaccount in een andere regio dan Hallo HDInsight-cluster wordt niet ondersteund.

### <a name="additional-charges"></a>Extra kosten

Als Hallo storage-account zich in een andere regio dan Hallo HDInsight-cluster, merkt u wellicht aanvullende uitgaande kosten op uw Azure-facturering. Een uitgaande kosten wordt toegepast wanneer de gegevens blijft een regionaal datacenter. Deze kosten is toegepast, zelfs als het Hallo-verkeer is bestemd voor een andere Azure-datacenter in een andere regio.

> [!WARNING]
> Met behulp van een opslagaccount in een andere regio dan Hallo HDInsight-cluster wordt niet ondersteund.

## <a name="next-steps"></a>Volgende stappen

U hebt geleerd hoe tooadd extra opslagaccounts tooan bestaand HDInsight-cluster. Zie voor meer informatie over scriptacties [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md)

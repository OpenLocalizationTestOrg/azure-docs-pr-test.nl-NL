---
title: aaa "Azure Batch-pool maken gebeurtenis | Microsoft Docs'
description: Naslaginformatie voor Batch-pool gebeurtenis maken.
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: ad31251969af553baa21e8c533d8ea95d3eeaf91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="pool-create-event"></a>Groep gebeurtenis maken

 Deze gebeurtenis wordt verzonden wanneer een groep is gemaakt. Hallo-inhoud van het logboek Hallo zal algemene informatie over het Hallo-groep worden blootgesteld. Houd er rekening mee dat als de doelgrootte Hallo van Hallo van toepassingen groter is dan 0 rekenknooppunten, een gebeurtenis van toepassingen starten direct na deze gebeurtenis wordt volgen.

 Hallo volgende voorbeeld ziet Hallo hoofdtekst van een groep gebeurtenis gemaakt voor een groep gemaakt met behulp van Hallo CloudServiceConfiguration eigenschap.

```
{
    "id": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "3",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicated": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoScale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

|Element|Type|Opmerkingen|
|-------------|----------|-----------|
|id|Tekenreeks|Hallo-id van Hallo pool.|
|Weergavenaam|Tekenreeks|Hallo weergavenaam van Hallo van toepassingen.|
|vmSize|Tekenreeks|Hallo-grootte van Hallo virtuele machines in Hallo van toepassingen. Alle virtuele machines in een pool zijn Hallo dezelfde grootte hebben. <br/><br/> Zie voor informatie over beschikbare grootten van virtuele machines voor Cloud Services pools (groepen gemaakt met cloudServiceConfiguration), [grootten voor Cloudservices](http://azure.microsoft.com/documentation/articles/cloud-services-sizes-specs/). Batch ondersteunt alle Cloud-Services VM-grootten, behalve `ExtraSmall`.<br/><br/> Zie voor informatie over beschikbare virtuele machine grootten voor groepen met behulp van installatiekopieën van virtuele Machines Marketplace (groepen die zijn gemaakt met virtualMachineConfiguration) Hallo [grootten voor virtuele Machines](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-sizes/) (Linux) of [groottes voor Virtuele Machines](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) (Windows). Batch ondersteunt alle Azure VM-groottes met uitzondering van `STANDARD_A0` en die met Premium Storage (de serie `STANDARD_GS`, `STANDARD_DS` en `STANDARD_DSV2`).|
|[cloudServiceConfiguration](#bk_csconf)|Complex Type|Hallo cloud-serviceconfiguratie voor Hallo van toepassingen.|
|[virtualMachineConfiguration](#bk_vmconf)|Complex Type|Hallo configuratie van de virtuele machine voor Hallo-groep.|
|[networkConfiguration](#bk_netconf)|Complex Type|Hallo netwerkconfiguratie voor Hallo van toepassingen.|
|resizeTimeout|Time|Hallo-out voor de toewijzing van compute knooppunten toohello adresgroep opgegeven voor het laatste formaat bewerking Hallo op Hallo van toepassingen.  (hello initiële formaat als Hallo pool een formaat aantallen is gemaakt.)|
|targetDedicated|Int32|Hallo aantal rekenknooppunten die zijn aangevraagd voor Hallo van toepassingen.|
|enableAutoScale|BOOL|Hiermee geeft u op of Hallo groepsgrootte automatisch wordt aangepast gedurende een bepaalde periode.|
|enableInterNodeCommunication|BOOL|Hiermee geeft u op of Hallo van toepassingen is ingesteld voor directe communicatie tussen knooppunten.|
|isAutoPool|BOOL|Speficies of Hallo van toepassingen via een taak AutoPool mechanisme is gemaakt.|
|maxTasksPerNode|Int32|Hallo maximum aantal taken dat gelijktijdig kan worden uitgevoerd op één rekenknooppunt in Hallo van toepassingen.|
|vmFillType|Tekenreeks|Hiermee definieert u hoe Hallo Batch-service taken tussen rekenknooppunten in de pool Hallo distribueert. Geldige waarden worden verdeeld of Pack.|

###  <a name="bk_csconf"></a>cloudServiceConfiguration

|Elementnaam|Type|Opmerkingen|
|------------------|----------|-----------|
|besturingssysteemtype|Tekenreeks|Hello Azure Gast OS-familie toobe op Hallo virtuele machines in de groep Hallo geïnstalleerd.<br /><br /> Mogelijke waarden zijn:<br /><br /> **2** – OS-familie 2, gelijkwaardige tooWindows Server 2008 R2 SP1.<br /><br /> **3** – OS-familie 3, gelijkwaardige tooWindows Server 2012.<br /><br /> **4** – OS-familie 4, gelijkwaardige tooWindows Server 2012 R2.<br /><br /> Zie voor meer informatie [Azure Gast OS Releases](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases).|
|targetOSVersion|Tekenreeks|Hello Azure-Gastbesturingssysteemreleases versie toobe is geïnstalleerd op virtuele machines Hallo in Hallo van toepassingen.<br /><br /> de standaardwaarde Hallo is  **\***  familie waarmee Hallo meest recente versie van besturingssysteem voor Hallo opgegeven.<br /><br /> Zie voor andere toegestane waarden [Azure Gast OS Releases](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases).|

###  <a name="bk_vmconf"></a>virtualMachineConfiguration

|Elementnaam|Type|Opmerkingen|
|------------------|----------|-----------|
|[imageReference](#bk_imgref)|Complex Type|Hiermee geeft u informatie over het Hallo-platform of toouse voor Marketplace-installatiekopie.|
|nodeAgentSKUId|Tekenreeks|Hallo SKU van Hallo Batch knooppunt agent ingericht op Hallo rekenknooppunt.|
|[windowsConfiguration](#bk_winconf)|Complex Type|Hiermee geeft u de instellingen voor Windows-besturingssysteem op Hallo virtuele machine. Deze eigenschap mag niet zijn opgegeven als Hallo imageReference verwijst naar een installatiekopie van het Linux-besturingssysteem.|

###  <a name="bk_imgref"></a>imageReference

|Elementnaam|Type|Opmerkingen|
|------------------|----------|-----------|
|Uitgever|Tekenreeks|Hallo-uitgever van de installatiekopie van het Hallo.|
|Aanbieding|Tekenreeks|Hallo aanbieding van Hallo-afbeelding.|
|SKU|Tekenreeks|Hallo SKU van Hallo-afbeelding.|
|Versie|Tekenreeks|Hallo-versie van de installatiekopie van het Hallo.|

###  <a name="bk_winconf"></a>windowsConfiguration

|Elementnaam|Type|Opmerkingen|
|------------------|----------|-----------|
|enableAutomaticUpdates|Booleaanse waarde|Hiermee wordt aangegeven of Hallo virtuele machine is ingeschakeld voor automatische updates. Als deze eigenschap niet is opgegeven, wordt de standaardwaarde Hallo geldt.|

###  <a name="bk_netconf"></a>networkConfiguration

|Elementnaam|Type|Opmerkingen|
|------------------|--------------|----------|
|subnetId|Tekenreeks|Hiermee geeft u Hallo resource-id van Hallo-subnet op van welke groep Hallo compute knooppunten worden gemaakt.|

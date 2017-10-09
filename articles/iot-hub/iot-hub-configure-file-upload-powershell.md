---
title: uploaden van aaaUse hello Azure PowerShell tooconfigure bestand | Microsoft Docs
description: Hoe toouse hello Azure PowerShell-cmdlets tooconfigure uw IoT hub tooenable bestand uploadt van verbonden apparaten. Bevat informatie over het configureren van Hallo bestemming Azure storage-account.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 9dcdc41693c09cece411921b30c91d7b3db47395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a>Uploaden van bestanden met PowerShell IoT-Hub configureren

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

Hallo toouse [bestand uploaden functionaliteit in IoT-Hub][lnk-upload], moet u eerst een Azure storage-account koppelen met uw IoT-hub. U kunt een bestaand opslagaccount gebruiken of een nieuwe maken.

toocomplete in deze zelfstudie, moet u hello te volgen:

* Een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.
* [Azure PowerShell-cmdlets][lnk-powershell-install].
* Een Azure-IoT-hub. Als u een IoT-hub hebt, kunt u Hallo [cmdlet New-AzureRmIoTHub] [ lnk-powershell-iothub] toocreate one of gebruik Hallo u portal te[een iothub maken] [ lnk-portal-hub].
* Een Azure Storage-account. Als u geen Azure storage-account hebt, kunt u Hallo [Azure PowerShell-cmdlets Storage] [ lnk-powershell-storage] toocreate one of gebruik Hallo u portal te[een opslagaccount maken] [ lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Aanmelden en uw Azure-account instellen

Meld u aan tooyour Azure-account en uw abonnement te selecteren.

1. Uitvoeren bij de PowerShell-prompt Hallo Hallo **Login-AzureRmAccount** cmdlet:

    ```powershell
    Login-AzureRmAccount
    ```

1. Aanmelden tooAzure verleent u tooall toegang tot Azure-abonnementen die zijn gekoppeld aan uw referenties in Media Player Hallo als u meerdere Azure-abonnementen hebt. Hallo opdracht toolist hello Azure-abonnementen beschikbaar voor u toouse volgende gebruiken:

    ```powershell
    Get-AzureRMSubscription
    ```

    Gebruik Hallo opdracht tooselect abonnement dat u wilt dat uw IoT-hub-opdrachten toomanage toouse toorun hello te volgen. U kunt Hallo abonnementsnaam of ID van uitvoer van de vorige opdracht Hallo Hallo gebruiken:

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a>De gegevens van uw storage-account ophalen

Hallo volgende stappen wordt ervan uitgegaan dat u uw storage-account met behulp van Hallo gemaakt **Resource Manager** implementatiemodel en niet Hallo **klassieke** implementatiemodel.

tooconfigure bestand uploadt van uw apparaten, moet u Hallo-verbindingsreeks voor Azure storage-account. Hallo storage-account moet zich in Hallo hetzelfde abonnement als uw IoT-hub. U moet ook Hallo-naam van een blob-container in Hallo storage-account. Hallo opdracht tooretrieve na uw toegangscodes voor opslag gebruiken:

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

Maak een notitie van Hallo **key1** sleutelwaarde storage-account. U moet het Hallo stappen te volgen.

U kunt een bestaande blobcontainer voor uw bestandsuploads gebruiken of nieuwe maken:

* toolist hello bestaande blob-containers in uw opslagaccount gebruiken Hallo volgende opdrachten:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* toocreate een blob-container in uw opslagaccount, gebruik Hallo volgende opdrachten:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a>Configureren van uw IoT-hub

U kunt nu uw IoT hub tooenable configureren [bestand uploaden functionaliteit] [ lnk-upload] met behulp van de gegevens van uw opslag.

Hallo configuratie vereist Hallo volgende waarden:

**Storage-container**: een blobcontainer in Azure storage-account in uw huidige Azure-abonnement tooassociate met uw IoT-hub. Hallo benodigde opslag accountgegevens in de voorgaande sectie Hallo dat u hebt opgehaald. IoT Hub genereert automatisch SAS URI's met schrijven machtigingen toothis blob-container voor apparaten toouse wanneer het uploaden van bestanden.

**Meldingen ontvangen voor de geüploade bestanden**: bestand uploaden meldingen- of uitschakelen.

**SAS TTL**: deze instelling is Hallo time-to-live Hallo SAS URI's toohello apparaat geretourneerd door de IoT Hub. Standaard tooone uur.

**Bestand notification instellingen standaard TTL**: Hallo time-to-live van een bestand uploaden melding voordat het is verlopen. Tooone dag standaard ingesteld.

**Melding levering van het maximum aantal bestanden**: Hallo aantal keren dat Hallo IoT Hub pogingen toodeliver een melding van bestand uploaden. Too10 standaard ingesteld.

Gebruik Hallo PowerShell cmdlet tooconfigure Hallo-bestand uploaden instellingen op uw IoT-hub te volgen:

```powershell
Set-AzureRmIotHub `
    -ResourceGroupName "{your iot hub resource group}" `
    -Name "{your iot hub name}" `
    -FileUploadNotificationTtl "01:00:00" `
    -FileUploadSasUriTtl "01:00:00" `
    -EnableFileUploadNotifications $true `
    -FileUploadStorageConnectionString "DefaultEndpointsProtocol=https;AccountName={your storage account name};AccountKey={your storage account key};EndpointSuffix=core.windows.net" `
    -FileUploadContainerName "{your blob container name}" `
    -FileUploadNotificationMaxDeliveryCount 10
```

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over functies voor het uploaden van bestanden Hallo van IoT Hub [uploaden van bestanden van een apparaat][lnk-upload].

Volg deze koppelingen toolearn meer over het beheren van Azure IoT Hub:

* [Bulksgewijs IoT-apparaten beheren][lnk-bulk]
* [IoT Hub metrische gegevens][lnk-metrics]
* [Bewerkingen controleren][lnk-monitor]

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]
* [Een apparaat simuleren met IoT rand][lnk-iotedge]
* [Uw IoT-oplossing van Hallo gemalen beveiligen][lnk-securing]

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-powershell-storage]: https://docs.microsoft.com/powershell/module/azurerm.storage/
[lnk-powershell-iothub]: https://docs.microsoft.com/powershell/module/azurerm.iothub/new-azurermiothub
[lnk-portal-hub]: iot-hub-create-through-portal.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md
---
title: aaaConfigure-bestand uploaden tooIoT Hub met Azure CLI (az.py) | Microsoft Docs
description: Hoe tooconfigure uploads tooAzure Iothub met behulp van Hallo platformoverschrijdende Azure CLI 2.0 (az.py).
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
ms.openlocfilehash: 390113df2d96df9833b6aa383ed66805528614a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a>Uploaden van bestanden met Azure CLI IoT-Hub configureren

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

Hallo toouse [bestand uploaden functionaliteit in IoT-Hub][lnk-upload], moet u eerst een Azure Storage-account koppelen met uw IoT-hub. U kunt een bestaand opslagaccount gebruiken of een nieuwe maken.

toocomplete in deze zelfstudie, moet u hello te volgen:

* Een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.
* [Azure CLI 2.0][lnk-CLI-install].
* Een Azure-IoT-hub. Als u een IoT-hub hebt, kunt u Hallo `az iot hub create` [opdracht] [ lnk-cli-create-iothub] toocreate one of gebruik Hallo u portal te [maken van een IoT-hub] [lnk-portal-hub].
* Een Azure Storage-account. Als u geen Azure Storage-account hebt, kunt u Hallo [Azure CLI 2.0 - storage-accounts beheren] [ lnk-manage-storage] toocreate één of gebruik Hallo u portal te[een opslagaccount maken] [lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Aanmelden en uw Azure-account instellen

Meld u aan tooyour Azure-account en uw abonnement te selecteren.

1. Uitvoeren bij de opdrachtprompt Hallo Hallo [aanmelding opdracht][lnk-login-command]:

    ```azurecli
    az login
    ```

    Volg Hallo instructies tooauthenticate met Hallo code en meld u aan tooyour Azure-account via een webbrowser.

1. Aanmelden tooAzure verleent u tooall toegang tot Azure-accounts die zijn gekoppeld aan uw referenties in Media Player Hallo als u meerdere Azure-abonnementen hebt. Gebruik de volgende Hallo [opdracht toolist hello Azure-accounts] [ lnk-az-account-command] beschikbaar voor u toouse:

    ```azurecli
    az account list
    ```

    Gebruik Hallo opdracht tooselect abonnement dat u wilt dat uw IoT-hub-opdrachten toocreate toouse toorun hello te volgen. U kunt Hallo abonnementsnaam of ID van uitvoer van de vorige opdracht Hallo Hallo gebruiken:

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a>De gegevens van uw storage-account ophalen

Hallo volgende stappen wordt ervan uitgegaan dat u uw storage-account met behulp van Hallo gemaakt **Resource Manager** implementatiemodel en niet Hallo **klassieke** implementatiemodel.

tooconfigure bestand uploadt van uw apparaten, moet u Hallo-verbindingsreeks voor Azure storage-account. Hallo storage-account moet zich in Hallo hetzelfde abonnement als uw IoT-hub. U moet ook Hallo-naam van een blob-container in Hallo storage-account. Hallo opdracht tooretrieve na uw toegangscodes voor opslag gebruiken:

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

Maak een notitie van Hallo **connectionString** waarde. U moet het Hallo stappen te volgen.

U kunt een bestaande blobcontainer voor uw bestandsuploads gebruiken of nieuwe maken:

* toolist hello bestaande blob-containers in uw opslagaccount Hallo volgende opdracht gebruiken:

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* toocreate een blob-container in uw opslagaccount, gebruik Hallo volgende opdracht:

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a>Bestand uploaden

U kunt nu uw IoT hub tooenable configureren [bestand uploaden functionaliteit] [ lnk-upload] met behulp van de gegevens van uw opslag.

Hallo configuratie vereist Hallo volgende waarden:

**Storage-container**: een blobcontainer in Azure storage-account in uw huidige Azure-abonnement tooassociate met uw IoT-hub. Hallo benodigde opslag accountgegevens in de voorgaande sectie Hallo dat u hebt opgehaald. IoT Hub genereert automatisch SAS URI's met schrijven machtigingen toothis blob-container voor apparaten toouse wanneer het uploaden van bestanden.

**Meldingen ontvangen voor de geüploade bestanden**: bestand uploaden meldingen- of uitschakelen.

**SAS TTL**: deze instelling is Hallo time-to-live Hallo SAS URI's toohello apparaat geretourneerd door de IoT Hub. Standaard tooone uur.

**Bestand notification instellingen standaard TTL**: Hallo time-to-live van een bestand uploaden melding voordat het is verlopen. Tooone dag standaard ingesteld.

**Melding levering van het maximum aantal bestanden**: Hallo aantal keren dat Hallo IoT Hub pogingen toodeliver een melding van bestand uploaden. Too10 standaard ingesteld.

Gebruik hello Azure CLI-opdrachten tooconfigure Hallo-bestand uploaden instellingen op uw IoT-hub te volgen:

Bij een bash-shell-toepassing:

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

Op de gebruik van een Windows-opdrachtprompt:

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

U kunt Hallo-bestand uploadconfiguratie op uw IoT-hub met behulp van de volgende opdracht Hallo bekijken:

```azurecli
az iot hub show --name {your iot hub name}
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

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md


[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-manage-storage]:../storage/common/storage-azure-cli.md#manage-storage-accounts
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md
[lnk-cli-create-iothub]: https://docs.microsoft.com/cli/azure/iot/hub#create
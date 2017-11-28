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
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="30fe3-103">Uploaden van bestanden met Azure CLI IoT-Hub configureren</span><span class="sxs-lookup"><span data-stu-id="30fe3-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="30fe3-104">Hallo toouse [bestand uploaden functionaliteit in IoT-Hub][lnk-upload], moet u eerst een Azure Storage-account koppelen met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="30fe3-104">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="30fe3-105">U kunt een bestaand opslagaccount gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="30fe3-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="30fe3-106">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="30fe3-106">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="30fe3-107">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="30fe3-107">An active Azure account.</span></span> <span data-ttu-id="30fe3-108">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="30fe3-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="30fe3-109">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="30fe3-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="30fe3-110">Een Azure-IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="30fe3-110">An Azure IoT hub.</span></span> <span data-ttu-id="30fe3-111">Als u een IoT-hub hebt, kunt u Hallo `az iot hub create` [opdracht] [ lnk-cli-create-iothub] toocreate one of gebruik Hallo u portal te [maken van een IoT-hub] [lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="30fe3-111">If you don't have an IoT hub, you can use hello `az iot hub create` [command][lnk-cli-create-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="30fe3-112">Een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="30fe3-112">An Azure Storage account.</span></span> <span data-ttu-id="30fe3-113">Als u geen Azure Storage-account hebt, kunt u Hallo [Azure CLI 2.0 - storage-accounts beheren] [ lnk-manage-storage] toocreate één of gebruik Hallo u portal te[een opslagaccount maken] [lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="30fe3-113">If you don't have an Azure Storage account, you can use hello [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="30fe3-114">Aanmelden en uw Azure-account instellen</span><span class="sxs-lookup"><span data-stu-id="30fe3-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="30fe3-115">Meld u aan tooyour Azure-account en uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="30fe3-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="30fe3-116">Uitvoeren bij de opdrachtprompt Hallo Hallo [aanmelding opdracht][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="30fe3-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="30fe3-117">Volg Hallo instructies tooauthenticate met Hallo code en meld u aan tooyour Azure-account via een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="30fe3-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

1. <span data-ttu-id="30fe3-118">Aanmelden tooAzure verleent u tooall toegang tot Azure-accounts die zijn gekoppeld aan uw referenties in Media Player Hallo als u meerdere Azure-abonnementen hebt.</span><span class="sxs-lookup"><span data-stu-id="30fe3-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="30fe3-119">Gebruik de volgende Hallo [opdracht toolist hello Azure-accounts] [ lnk-az-account-command] beschikbaar voor u toouse:</span><span class="sxs-lookup"><span data-stu-id="30fe3-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="30fe3-120">Gebruik Hallo opdracht tooselect abonnement dat u wilt dat uw IoT-hub-opdrachten toocreate toouse toorun hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="30fe3-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="30fe3-121">U kunt Hallo abonnementsnaam of ID van uitvoer van de vorige opdracht Hallo Hallo gebruiken:</span><span class="sxs-lookup"><span data-stu-id="30fe3-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="30fe3-122">De gegevens van uw storage-account ophalen</span><span class="sxs-lookup"><span data-stu-id="30fe3-122">Retrieve your storage account details</span></span>

<span data-ttu-id="30fe3-123">Hallo volgende stappen wordt ervan uitgegaan dat u uw storage-account met behulp van Hallo gemaakt **Resource Manager** implementatiemodel en niet Hallo **klassieke** implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="30fe3-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="30fe3-124">tooconfigure bestand uploadt van uw apparaten, moet u Hallo-verbindingsreeks voor Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="30fe3-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="30fe3-125">Hallo storage-account moet zich in Hallo hetzelfde abonnement als uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="30fe3-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="30fe3-126">U moet ook Hallo-naam van een blob-container in Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="30fe3-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="30fe3-127">Hallo opdracht tooretrieve na uw toegangscodes voor opslag gebruiken:</span><span class="sxs-lookup"><span data-stu-id="30fe3-127">Use hello following command tooretrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="30fe3-128">Maak een notitie van Hallo **connectionString** waarde.</span><span class="sxs-lookup"><span data-stu-id="30fe3-128">Make a note of hello **connectionString** value.</span></span> <span data-ttu-id="30fe3-129">U moet het Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="30fe3-129">You need it in hello following steps.</span></span>

<span data-ttu-id="30fe3-130">U kunt een bestaande blobcontainer voor uw bestandsuploads gebruiken of nieuwe maken:</span><span class="sxs-lookup"><span data-stu-id="30fe3-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="30fe3-131">toolist hello bestaande blob-containers in uw opslagaccount Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="30fe3-131">toolist hello existing blob containers in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="30fe3-132">toocreate een blob-container in uw opslagaccount, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="30fe3-132">toocreate a blob container in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="30fe3-133">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="30fe3-133">File upload</span></span>

<span data-ttu-id="30fe3-134">U kunt nu uw IoT hub tooenable configureren [bestand uploaden functionaliteit] [ lnk-upload] met behulp van de gegevens van uw opslag.</span><span class="sxs-lookup"><span data-stu-id="30fe3-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="30fe3-135">Hallo configuratie vereist Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="30fe3-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="30fe3-136">**Storage-container**: een blobcontainer in Azure storage-account in uw huidige Azure-abonnement tooassociate met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="30fe3-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="30fe3-137">Hallo benodigde opslag accountgegevens in de voorgaande sectie Hallo dat u hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="30fe3-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="30fe3-138">IoT Hub genereert automatisch SAS URI's met schrijven machtigingen toothis blob-container voor apparaten toouse wanneer het uploaden van bestanden.</span><span class="sxs-lookup"><span data-stu-id="30fe3-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="30fe3-139">**Meldingen ontvangen voor de geüploade bestanden**: bestand uploaden meldingen- of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="30fe3-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="30fe3-140">**SAS TTL**: deze instelling is Hallo time-to-live Hallo SAS URI's toohello apparaat geretourneerd door de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="30fe3-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="30fe3-141">Standaard tooone uur.</span><span class="sxs-lookup"><span data-stu-id="30fe3-141">Set tooone hour by default.</span></span>

<span data-ttu-id="30fe3-142">**Bestand notification instellingen standaard TTL**: Hallo time-to-live van een bestand uploaden melding voordat het is verlopen.</span><span class="sxs-lookup"><span data-stu-id="30fe3-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="30fe3-143">Tooone dag standaard ingesteld.</span><span class="sxs-lookup"><span data-stu-id="30fe3-143">Set tooone day by default.</span></span>

<span data-ttu-id="30fe3-144">**Melding levering van het maximum aantal bestanden**: Hallo aantal keren dat Hallo IoT Hub pogingen toodeliver een melding van bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="30fe3-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="30fe3-145">Too10 standaard ingesteld.</span><span class="sxs-lookup"><span data-stu-id="30fe3-145">Set too10 by default.</span></span>

<span data-ttu-id="30fe3-146">Gebruik hello Azure CLI-opdrachten tooconfigure Hallo-bestand uploaden instellingen op uw IoT-hub te volgen:</span><span class="sxs-lookup"><span data-stu-id="30fe3-146">Use hello following Azure CLI commands tooconfigure hello file upload settings on your IoT hub:</span></span>

<span data-ttu-id="30fe3-147">Bij een bash-shell-toepassing:</span><span class="sxs-lookup"><span data-stu-id="30fe3-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="30fe3-148">Op de gebruik van een Windows-opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="30fe3-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="30fe3-149">U kunt Hallo-bestand uploadconfiguratie op uw IoT-hub met behulp van de volgende opdracht Hallo bekijken:</span><span class="sxs-lookup"><span data-stu-id="30fe3-149">You can review hello file upload configuration on your IoT hub using hello following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="30fe3-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="30fe3-150">Next steps</span></span>

<span data-ttu-id="30fe3-151">Zie voor meer informatie over functies voor het uploaden van bestanden Hallo van IoT Hub [uploaden van bestanden van een apparaat][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="30fe3-151">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="30fe3-152">Volg deze koppelingen toolearn meer over het beheren van Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="30fe3-152">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="30fe3-153">[Bulksgewijs IoT-apparaten beheren][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="30fe3-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="30fe3-154">[IoT Hub metrische gegevens][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="30fe3-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="30fe3-155">[Bewerkingen controleren][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="30fe3-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="30fe3-156">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="30fe3-156">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="30fe3-157">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="30fe3-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="30fe3-158">[Een apparaat simuleren met IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="30fe3-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="30fe3-159">[Uw IoT-oplossing van Hallo gemalen beveiligen][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="30fe3-159">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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
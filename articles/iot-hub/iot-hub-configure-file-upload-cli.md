---
title: Bestand uploaden naar IoT Hub met Azure CLI (az.py) configureren | Microsoft Docs
description: Het configureren van uploads met Azure IoT Hub met behulp van de platformoverschrijdende Azure CLI 2.0 (az.py).
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
ms.openlocfilehash: a9af26d7ebacf5513952786621aaa92f64be263b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="323a3-103">Uploaden van bestanden met Azure CLI IoT-Hub configureren</span><span class="sxs-lookup"><span data-stu-id="323a3-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="323a3-104">Gebruik de [bestand uploaden functionaliteit in IoT-Hub][lnk-upload], moet u eerst een Azure Storage-account koppelen met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="323a3-104">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="323a3-105">U kunt een bestaand opslagaccount gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="323a3-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="323a3-106">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="323a3-106">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="323a3-107">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="323a3-107">An active Azure account.</span></span> <span data-ttu-id="323a3-108">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="323a3-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="323a3-109">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="323a3-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="323a3-110">Een Azure-IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="323a3-110">An Azure IoT hub.</span></span> <span data-ttu-id="323a3-111">Als u een IoT-hub hebt, kunt u de `az iot hub create` [opdracht] [ lnk-cli-create-iothub] een maken of gebruiken van de portal [maken van een IoT-hub] [lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="323a3-111">If you don't have an IoT hub, you can use the `az iot hub create` [command][lnk-cli-create-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="323a3-112">Een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="323a3-112">An Azure Storage account.</span></span> <span data-ttu-id="323a3-113">Als u geen Azure Storage-account hebt, kunt u de [Azure CLI 2.0 - storage-accounts beheren] [ lnk-manage-storage] te maken of de portal gebruiken om [een opslagaccount maken] [ lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="323a3-113">If you don't have an Azure Storage account, you can use the [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="323a3-114">Aanmelden en uw Azure-account instellen</span><span class="sxs-lookup"><span data-stu-id="323a3-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="323a3-115">Aanmelden bij uw Azure-account en uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="323a3-115">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="323a3-116">Voer bij de opdrachtprompt de [aanmelding opdracht][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="323a3-116">At the command prompt, run the [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="323a3-117">Volg de instructies om te verifiëren met de code en meld u aan bij uw Azure-account via een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="323a3-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

1. <span data-ttu-id="323a3-118">Als u meerdere Azure-abonnementen hebt, aanmelden bij Azure u toegang verleent tot de Azure accounts die zijn gekoppeld aan uw referenties.</span><span class="sxs-lookup"><span data-stu-id="323a3-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span></span> <span data-ttu-id="323a3-119">Gebruik de volgende [opdracht om een lijst van de Azure-accounts] [ lnk-az-account-command] beschikbaar moet worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="323a3-119">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="323a3-120">Gebruik de volgende opdracht om abonnement die u gebruiken wilt voor het uitvoeren van de opdrachten voor het maken van uw IoT-hub te selecteren.</span><span class="sxs-lookup"><span data-stu-id="323a3-120">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="323a3-121">U kunt de naam van abonnement of de ID van de uitvoer van de vorige opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="323a3-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="323a3-122">De gegevens van uw storage-account ophalen</span><span class="sxs-lookup"><span data-stu-id="323a3-122">Retrieve your storage account details</span></span>

<span data-ttu-id="323a3-123">De volgende stappen wordt ervan uitgegaan dat u hebt gemaakt dat uw storage-account met de **Resource Manager** -implementatiemodel, en niet de **klassieke** implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="323a3-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="323a3-124">Als u wilt configureren bestandsuploads van uw apparaten, moet u de verbindingsreeks voor Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="323a3-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="323a3-125">Het opslagaccount moet zich in hetzelfde abonnement als uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="323a3-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="323a3-126">U moet ook de naam van een blob-container in het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="323a3-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="323a3-127">Gebruik de volgende opdracht voor het ophalen van uw toegangscodes voor opslag:</span><span class="sxs-lookup"><span data-stu-id="323a3-127">Use the following command to retrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="323a3-128">Noteer de **connectionString** waarde.</span><span class="sxs-lookup"><span data-stu-id="323a3-128">Make a note of the **connectionString** value.</span></span> <span data-ttu-id="323a3-129">U moet deze in de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="323a3-129">You need it in the following steps.</span></span>

<span data-ttu-id="323a3-130">U kunt een bestaande blobcontainer voor uw bestandsuploads gebruiken of nieuwe maken:</span><span class="sxs-lookup"><span data-stu-id="323a3-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="323a3-131">Als de bestaande blobcontainers in uw opslagaccount wilt weergeven, moet u de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="323a3-131">To list the existing blob containers in your storage account, use the following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="323a3-132">Voor het maken van een blob-container in uw opslagaccount, moet u de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="323a3-132">To create a blob container in your storage account, use the following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="323a3-133">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="323a3-133">File upload</span></span>

<span data-ttu-id="323a3-134">U kunt nu uw IoT-hub om in te schakelen configureren [bestand uploaden functionaliteit] [ lnk-upload] met behulp van de gegevens van uw opslag.</span><span class="sxs-lookup"><span data-stu-id="323a3-134">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="323a3-135">De configuratie is vereist voor de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="323a3-135">The configuration requires the following values:</span></span>

<span data-ttu-id="323a3-136">**Storage-container**: een blobcontainer in Azure storage-account in uw huidige Azure-abonnement wilt koppelen aan uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="323a3-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="323a3-137">U hebt de accountgegevens voor de benodigde opslag in de vorige sectie hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="323a3-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="323a3-138">IoT Hub genereert automatisch SAS URI's met schrijfmachtigingen in voor deze blob-container voor apparaten voor gebruik bij het uploaden van bestanden.</span><span class="sxs-lookup"><span data-stu-id="323a3-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="323a3-139">**Meldingen ontvangen voor de geüploade bestanden**: bestand uploaden meldingen- of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="323a3-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="323a3-140">**SAS TTL**: deze instelling wordt de time-to-live van de SAS-URI's die aan het apparaat wordt geretourneerd door de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="323a3-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="323a3-141">Standaard ingesteld op één uur.</span><span class="sxs-lookup"><span data-stu-id="323a3-141">Set to one hour by default.</span></span>

<span data-ttu-id="323a3-142">**Bestand notification instellingen standaard TTL**: de time-to-live van een bestand uploaden melding voordat het is verlopen.</span><span class="sxs-lookup"><span data-stu-id="323a3-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="323a3-143">Standaard ingesteld op één dag.</span><span class="sxs-lookup"><span data-stu-id="323a3-143">Set to one day by default.</span></span>

<span data-ttu-id="323a3-144">**Melding levering van het maximum aantal bestanden**: het aantal keren dat de IoT-Hub probeert een bestand uploaden een melding.</span><span class="sxs-lookup"><span data-stu-id="323a3-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="323a3-145">Standaard ingesteld op 10.</span><span class="sxs-lookup"><span data-stu-id="323a3-145">Set to 10 by default.</span></span>

<span data-ttu-id="323a3-146">Gebruik de volgende Azure CLI-opdrachten in het bestand uploaden om instellingen te configureren op uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="323a3-146">Use the following Azure CLI commands to configure the file upload settings on your IoT hub:</span></span>

<span data-ttu-id="323a3-147">Bij een bash-shell-toepassing:</span><span class="sxs-lookup"><span data-stu-id="323a3-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="323a3-148">Op de gebruik van een Windows-opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="323a3-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="323a3-149">U kunt de configuratie van de uploaden bestand bekijken op uw IoT-hub met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="323a3-149">You can review the file upload configuration on your IoT hub using the following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="323a3-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="323a3-150">Next steps</span></span>

<span data-ttu-id="323a3-151">Zie voor meer informatie over de functies voor het uploaden van bestanden van IoT Hub [uploaden van bestanden van een apparaat][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="323a3-151">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="323a3-152">Volg deze koppelingen voor meer informatie over het beheren van Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="323a3-152">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="323a3-153">[Bulksgewijs IoT-apparaten beheren][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="323a3-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="323a3-154">[IoT Hub metrische gegevens][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="323a3-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="323a3-155">[Bewerkingen controleren][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="323a3-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="323a3-156">Als u wilt de mogelijkheden van IoT Hub verder verkennen, Zie:</span><span class="sxs-lookup"><span data-stu-id="323a3-156">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="323a3-157">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="323a3-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="323a3-158">[Een apparaat simuleren met IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="323a3-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="323a3-159">[Beveiligen van uw IoT-oplossing bouwen up][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="323a3-159">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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
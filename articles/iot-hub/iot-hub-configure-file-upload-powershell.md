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
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="0eef2-104">Uploaden van bestanden met PowerShell IoT-Hub configureren</span><span class="sxs-lookup"><span data-stu-id="0eef2-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="0eef2-105">Hallo toouse [bestand uploaden functionaliteit in IoT-Hub][lnk-upload], moet u eerst een Azure storage-account koppelen met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="0eef2-105">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="0eef2-106">U kunt een bestaand opslagaccount gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="0eef2-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="0eef2-107">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="0eef2-107">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="0eef2-108">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="0eef2-108">An active Azure account.</span></span> <span data-ttu-id="0eef2-109">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="0eef2-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="0eef2-110">[Azure PowerShell-cmdlets][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="0eef2-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="0eef2-111">Een Azure-IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="0eef2-111">An Azure IoT hub.</span></span> <span data-ttu-id="0eef2-112">Als u een IoT-hub hebt, kunt u Hallo [cmdlet New-AzureRmIoTHub] [ lnk-powershell-iothub] toocreate one of gebruik Hallo u portal te[een iothub maken] [ lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="0eef2-112">If you don't have an IoT hub, you can use hello [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="0eef2-113">Een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="0eef2-113">An Azure storage account.</span></span> <span data-ttu-id="0eef2-114">Als u geen Azure storage-account hebt, kunt u Hallo [Azure PowerShell-cmdlets Storage] [ lnk-powershell-storage] toocreate one of gebruik Hallo u portal te[een opslagaccount maken] [ lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="0eef2-114">If you don't have an Azure storage account, you can use hello [Azure Storage PowerShell cmdlets][lnk-powershell-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="0eef2-115">Aanmelden en uw Azure-account instellen</span><span class="sxs-lookup"><span data-stu-id="0eef2-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="0eef2-116">Meld u aan tooyour Azure-account en uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="0eef2-116">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="0eef2-117">Uitvoeren bij de PowerShell-prompt Hallo Hallo **Login-AzureRmAccount** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0eef2-117">At hello PowerShell prompt, run hello **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="0eef2-118">Aanmelden tooAzure verleent u tooall toegang tot Azure-abonnementen die zijn gekoppeld aan uw referenties in Media Player Hallo als u meerdere Azure-abonnementen hebt.</span><span class="sxs-lookup"><span data-stu-id="0eef2-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="0eef2-119">Hallo opdracht toolist hello Azure-abonnementen beschikbaar voor u toouse volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="0eef2-119">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="0eef2-120">Gebruik Hallo opdracht tooselect abonnement dat u wilt dat uw IoT-hub-opdrachten toomanage toouse toorun hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="0eef2-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="0eef2-121">U kunt Hallo abonnementsnaam of ID van uitvoer van de vorige opdracht Hallo Hallo gebruiken:</span><span class="sxs-lookup"><span data-stu-id="0eef2-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="0eef2-122">De gegevens van uw storage-account ophalen</span><span class="sxs-lookup"><span data-stu-id="0eef2-122">Retrieve your storage account details</span></span>

<span data-ttu-id="0eef2-123">Hallo volgende stappen wordt ervan uitgegaan dat u uw storage-account met behulp van Hallo gemaakt **Resource Manager** implementatiemodel en niet Hallo **klassieke** implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="0eef2-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="0eef2-124">tooconfigure bestand uploadt van uw apparaten, moet u Hallo-verbindingsreeks voor Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="0eef2-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="0eef2-125">Hallo storage-account moet zich in Hallo hetzelfde abonnement als uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="0eef2-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="0eef2-126">U moet ook Hallo-naam van een blob-container in Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="0eef2-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="0eef2-127">Hallo opdracht tooretrieve na uw toegangscodes voor opslag gebruiken:</span><span class="sxs-lookup"><span data-stu-id="0eef2-127">Use hello following command tooretrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="0eef2-128">Maak een notitie van Hallo **key1** sleutelwaarde storage-account.</span><span class="sxs-lookup"><span data-stu-id="0eef2-128">Make a note of hello **key1** storage account key value.</span></span> <span data-ttu-id="0eef2-129">U moet het Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="0eef2-129">You need it in hello following steps.</span></span>

<span data-ttu-id="0eef2-130">U kunt een bestaande blobcontainer voor uw bestandsuploads gebruiken of nieuwe maken:</span><span class="sxs-lookup"><span data-stu-id="0eef2-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="0eef2-131">toolist hello bestaande blob-containers in uw opslagaccount gebruiken Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="0eef2-131">toolist hello existing blob containers in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="0eef2-132">toocreate een blob-container in uw opslagaccount, gebruik Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="0eef2-132">toocreate a blob container in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="0eef2-133">Configureren van uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="0eef2-133">Configure your IoT hub</span></span>

<span data-ttu-id="0eef2-134">U kunt nu uw IoT hub tooenable configureren [bestand uploaden functionaliteit] [ lnk-upload] met behulp van de gegevens van uw opslag.</span><span class="sxs-lookup"><span data-stu-id="0eef2-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="0eef2-135">Hallo configuratie vereist Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="0eef2-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="0eef2-136">**Storage-container**: een blobcontainer in Azure storage-account in uw huidige Azure-abonnement tooassociate met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="0eef2-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="0eef2-137">Hallo benodigde opslag accountgegevens in de voorgaande sectie Hallo dat u hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="0eef2-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="0eef2-138">IoT Hub genereert automatisch SAS URI's met schrijven machtigingen toothis blob-container voor apparaten toouse wanneer het uploaden van bestanden.</span><span class="sxs-lookup"><span data-stu-id="0eef2-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="0eef2-139">**Meldingen ontvangen voor de geüploade bestanden**: bestand uploaden meldingen- of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="0eef2-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="0eef2-140">**SAS TTL**: deze instelling is Hallo time-to-live Hallo SAS URI's toohello apparaat geretourneerd door de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0eef2-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="0eef2-141">Standaard tooone uur.</span><span class="sxs-lookup"><span data-stu-id="0eef2-141">Set tooone hour by default.</span></span>

<span data-ttu-id="0eef2-142">**Bestand notification instellingen standaard TTL**: Hallo time-to-live van een bestand uploaden melding voordat het is verlopen.</span><span class="sxs-lookup"><span data-stu-id="0eef2-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="0eef2-143">Tooone dag standaard ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0eef2-143">Set tooone day by default.</span></span>

<span data-ttu-id="0eef2-144">**Melding levering van het maximum aantal bestanden**: Hallo aantal keren dat Hallo IoT Hub pogingen toodeliver een melding van bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="0eef2-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="0eef2-145">Too10 standaard ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0eef2-145">Set too10 by default.</span></span>

<span data-ttu-id="0eef2-146">Gebruik Hallo PowerShell cmdlet tooconfigure Hallo-bestand uploaden instellingen op uw IoT-hub te volgen:</span><span class="sxs-lookup"><span data-stu-id="0eef2-146">Use hello following PowerShell cmdlet tooconfigure hello file upload settings on your IoT hub:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0eef2-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0eef2-147">Next steps</span></span>

<span data-ttu-id="0eef2-148">Zie voor meer informatie over functies voor het uploaden van bestanden Hallo van IoT Hub [uploaden van bestanden van een apparaat][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="0eef2-148">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="0eef2-149">Volg deze koppelingen toolearn meer over het beheren van Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="0eef2-149">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="0eef2-150">[Bulksgewijs IoT-apparaten beheren][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="0eef2-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="0eef2-151">[IoT Hub metrische gegevens][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="0eef2-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="0eef2-152">[Bewerkingen controleren][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="0eef2-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="0eef2-153">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="0eef2-153">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="0eef2-154">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="0eef2-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="0eef2-155">[Een apparaat simuleren met IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="0eef2-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="0eef2-156">[Uw IoT-oplossing van Hallo gemalen beveiligen][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="0eef2-156">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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
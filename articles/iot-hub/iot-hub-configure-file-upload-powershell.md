---
title: Azure PowerShell gebruiken om te uploaden bestand configureren | Microsoft Docs
description: Het gebruik van de Azure PowerShell-cmdlets voor het configureren van uw IoT-hub zodat bestand uploadt van verbonden apparaten. Bevat informatie over het configureren van de doel-Azure storage-account.
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
ms.openlocfilehash: a72bda794b2da3e044c46249559610d06b1f1843
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="57d3f-104">Uploaden van bestanden met PowerShell IoT-Hub configureren</span><span class="sxs-lookup"><span data-stu-id="57d3f-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="57d3f-105">Gebruik de [bestand uploaden functionaliteit in IoT-Hub][lnk-upload], moet u eerst een Azure storage-account koppelen met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="57d3f-105">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="57d3f-106">U kunt een bestaand opslagaccount gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="57d3f-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="57d3f-107">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="57d3f-107">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="57d3f-108">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="57d3f-108">An active Azure account.</span></span> <span data-ttu-id="57d3f-109">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="57d3f-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="57d3f-110">[Azure PowerShell-cmdlets][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="57d3f-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="57d3f-111">Een Azure-IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="57d3f-111">An Azure IoT hub.</span></span> <span data-ttu-id="57d3f-112">Als u een IoT-hub hebt, kunt u de [cmdlet New-AzureRmIoTHub] [ lnk-powershell-iothub] te maken of de portal gebruiken om [een iothub maken][lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="57d3f-112">If you don't have an IoT hub, you can use the [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="57d3f-113">Een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="57d3f-113">An Azure storage account.</span></span> <span data-ttu-id="57d3f-114">Als u geen Azure storage-account hebt, kunt u de [Azure PowerShell-cmdlets Storage] [ lnk-powershell-storage] te maken of de portal gebruiken om [een opslagaccount maken] [lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="57d3f-114">If you don't have an Azure storage account, you can use the [Azure Storage PowerShell cmdlets][lnk-powershell-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="57d3f-115">Aanmelden en uw Azure-account instellen</span><span class="sxs-lookup"><span data-stu-id="57d3f-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="57d3f-116">Aanmelden bij uw Azure-account en uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="57d3f-116">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="57d3f-117">Uitvoeren op de PowerShell-prompt de **Login-AzureRmAccount** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="57d3f-117">At the PowerShell prompt, run the **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="57d3f-118">Als u meerdere Azure-abonnementen hebt, verleent aanmelden bij Azure u toegang tot alle de Azure-abonnementen die zijn gekoppeld aan uw referenties.</span><span class="sxs-lookup"><span data-stu-id="57d3f-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="57d3f-119">Gebruik de volgende opdracht voor een lijst met de Azure-abonnementen beschikbaar moet worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="57d3f-119">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="57d3f-120">Gebruik de volgende opdracht om abonnement die u gebruiken wilt voor het uitvoeren van de opdrachten voor het beheren van uw IoT-hub te selecteren.</span><span class="sxs-lookup"><span data-stu-id="57d3f-120">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="57d3f-121">U kunt de naam van abonnement of de ID van de uitvoer van de vorige opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="57d3f-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="57d3f-122">De gegevens van uw storage-account ophalen</span><span class="sxs-lookup"><span data-stu-id="57d3f-122">Retrieve your storage account details</span></span>

<span data-ttu-id="57d3f-123">De volgende stappen wordt ervan uitgegaan dat u hebt gemaakt dat uw storage-account met de **Resource Manager** -implementatiemodel, en niet de **klassieke** implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="57d3f-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="57d3f-124">Als u wilt configureren bestandsuploads van uw apparaten, moet u de verbindingsreeks voor Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="57d3f-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="57d3f-125">Het opslagaccount moet zich in hetzelfde abonnement als uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="57d3f-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="57d3f-126">U moet ook de naam van een blob-container in het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="57d3f-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="57d3f-127">Gebruik de volgende opdracht voor het ophalen van uw toegangscodes voor opslag:</span><span class="sxs-lookup"><span data-stu-id="57d3f-127">Use the following command to retrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="57d3f-128">Noteer de **key1** sleutelwaarde storage-account.</span><span class="sxs-lookup"><span data-stu-id="57d3f-128">Make a note of the **key1** storage account key value.</span></span> <span data-ttu-id="57d3f-129">U moet deze in de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="57d3f-129">You need it in the following steps.</span></span>

<span data-ttu-id="57d3f-130">U kunt een bestaande blobcontainer voor uw bestandsuploads gebruiken of nieuwe maken:</span><span class="sxs-lookup"><span data-stu-id="57d3f-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="57d3f-131">Als de bestaande blobcontainers in uw opslagaccount wilt weergeven, gebruikt u de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="57d3f-131">To list the existing blob containers in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="57d3f-132">Voor het maken van een blob-container in uw opslagaccount, gebruik de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="57d3f-132">To create a blob container in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="57d3f-133">Configureren van uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="57d3f-133">Configure your IoT hub</span></span>

<span data-ttu-id="57d3f-134">U kunt nu uw IoT-hub om in te schakelen configureren [bestand uploaden functionaliteit] [ lnk-upload] met behulp van de gegevens van uw opslag.</span><span class="sxs-lookup"><span data-stu-id="57d3f-134">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="57d3f-135">De configuratie is vereist voor de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="57d3f-135">The configuration requires the following values:</span></span>

<span data-ttu-id="57d3f-136">**Storage-container**: een blobcontainer in Azure storage-account in uw huidige Azure-abonnement wilt koppelen aan uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="57d3f-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="57d3f-137">U hebt de accountgegevens voor de benodigde opslag in de vorige sectie hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="57d3f-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="57d3f-138">IoT Hub genereert automatisch SAS URI's met schrijfmachtigingen in voor deze blob-container voor apparaten voor gebruik bij het uploaden van bestanden.</span><span class="sxs-lookup"><span data-stu-id="57d3f-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="57d3f-139">**Meldingen ontvangen voor de geüploade bestanden**: bestand uploaden meldingen- of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="57d3f-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="57d3f-140">**SAS TTL**: deze instelling wordt de time-to-live van de SAS-URI's die aan het apparaat wordt geretourneerd door de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="57d3f-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="57d3f-141">Standaard ingesteld op één uur.</span><span class="sxs-lookup"><span data-stu-id="57d3f-141">Set to one hour by default.</span></span>

<span data-ttu-id="57d3f-142">**Bestand notification instellingen standaard TTL**: de time-to-live van een bestand uploaden melding voordat het is verlopen.</span><span class="sxs-lookup"><span data-stu-id="57d3f-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="57d3f-143">Standaard ingesteld op één dag.</span><span class="sxs-lookup"><span data-stu-id="57d3f-143">Set to one day by default.</span></span>

<span data-ttu-id="57d3f-144">**Melding levering van het maximum aantal bestanden**: het aantal keren dat de IoT-Hub probeert een bestand uploaden een melding.</span><span class="sxs-lookup"><span data-stu-id="57d3f-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="57d3f-145">Standaard ingesteld op 10.</span><span class="sxs-lookup"><span data-stu-id="57d3f-145">Set to 10 by default.</span></span>

<span data-ttu-id="57d3f-146">Gebruik de volgende PowerShell-cmdlet voor het configureren van het bestand uploaden instellingen op uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="57d3f-146">Use the following PowerShell cmdlet to configure the file upload settings on your IoT hub:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="57d3f-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="57d3f-147">Next steps</span></span>

<span data-ttu-id="57d3f-148">Zie voor meer informatie over de functies voor het uploaden van bestanden van IoT Hub [uploaden van bestanden van een apparaat][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="57d3f-148">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="57d3f-149">Volg deze koppelingen voor meer informatie over het beheren van Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="57d3f-149">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="57d3f-150">[Bulksgewijs IoT-apparaten beheren][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="57d3f-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="57d3f-151">[IoT Hub metrische gegevens][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="57d3f-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="57d3f-152">[Bewerkingen controleren][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="57d3f-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="57d3f-153">Als u wilt de mogelijkheden van IoT Hub verder verkennen, Zie:</span><span class="sxs-lookup"><span data-stu-id="57d3f-153">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="57d3f-154">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="57d3f-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="57d3f-155">[Een apparaat simuleren met IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="57d3f-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="57d3f-156">[Beveiligen van uw IoT-oplossing bouwen up][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="57d3f-156">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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
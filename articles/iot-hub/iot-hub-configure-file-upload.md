---
title: De Azure portal gebruiken om te uploaden bestand configureren | Microsoft Docs
description: Het gebruik van de Azure-portal voor het configureren van uw IoT-hub zodat bestandsuploads van verbonden apparaten. Bevat informatie over het configureren van de doel-Azure storage-account.
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
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: 149dd84d7d8f4ff9cd30f9fc649ced3cb364cfb7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-iot-hub-file-uploads-using-the-azure-portal"></a><span data-ttu-id="a4302-104">IoT Hub uploaden van bestanden met de Azure portal configureren</span><span class="sxs-lookup"><span data-stu-id="a4302-104">Configure IoT Hub file uploads using the Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="a4302-105">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="a4302-105">File upload</span></span>

<span data-ttu-id="a4302-106">Gebruik de [bestand uploaden functionaliteit in IoT-Hub][lnk-upload], moet u eerst een Azure Storage-account koppelen met de hub.</span><span class="sxs-lookup"><span data-stu-id="a4302-106">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="a4302-107">Selecteer **uploaden bestand** om weer te geven een lijst met eigenschappen van bestand laden voor de IoT-hub die wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="a4302-107">Select **File upload** to display a list of file upload properties for the IoT hub that is being modified.</span></span>

![IoT Hub-bestand voor de weergave instellingen in de portal uploaden][13]

<span data-ttu-id="a4302-109">**Storage-container**: de Azure portal gebruiken om te selecteren van een blob-container in een Azure Storage-account in uw huidige Azure-abonnement wilt koppelen aan uw IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="a4302-109">**Storage container**: Use the Azure portal to select a blob container in an Azure Storage account in your current Azure subscription to associate with your IoT Hub.</span></span> <span data-ttu-id="a4302-110">Indien nodig, kunt u een Azure Storage-account op de **opslagaccounts** blade en blob-container op de **Containers** blade.</span><span class="sxs-lookup"><span data-stu-id="a4302-110">If necessary, you can create an Azure Storage account on the **Storage accounts** blade and blob container on the **Containers** blade.</span></span> <span data-ttu-id="a4302-111">IoT Hub genereert automatisch SAS URI's met schrijfmachtigingen in voor deze blob-container voor apparaten voor gebruik bij het uploaden van bestanden.</span><span class="sxs-lookup"><span data-stu-id="a4302-111">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

![Storage-containers voor uploaden van het bestand weergeven in de portal][14]

<span data-ttu-id="a4302-113">**Meldingen ontvangen voor de geüploade bestanden**: bestand uploaden meldingen via de wisselknop- of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="a4302-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via the toggle.</span></span>

<span data-ttu-id="a4302-114">**SAS TTL**: deze instelling wordt de time-to-live van de SAS-URI's die aan het apparaat wordt geretourneerd door de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a4302-114">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="a4302-115">Standaard ingesteld op één uur, maar kan worden aangepast aan andere waarden met behulp van de schuifregelaar.</span><span class="sxs-lookup"><span data-stu-id="a4302-115">Set to one hour by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="a4302-116">**Bestand notification instellingen standaard TTL**: de time-to-live van een bestand uploaden melding voordat het is verlopen.</span><span class="sxs-lookup"><span data-stu-id="a4302-116">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="a4302-117">Standaard ingesteld op één dag, maar kan worden aangepast aan andere waarden met behulp van de schuifregelaar.</span><span class="sxs-lookup"><span data-stu-id="a4302-117">Set to one day by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="a4302-118">**Melding levering van het maximum aantal bestanden**: het aantal keren dat de IoT-Hub probeert een bestand uploaden een melding.</span><span class="sxs-lookup"><span data-stu-id="a4302-118">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="a4302-119">Standaard ingesteld op 10, maar kan worden aangepast aan andere waarden met behulp van de schuifregelaar.</span><span class="sxs-lookup"><span data-stu-id="a4302-119">Set to 10 by default but can be customized to other values using the slider.</span></span>

![Het uploaden van het IoT-Hub in de portal configureren][15]

## <a name="next-steps"></a><span data-ttu-id="a4302-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a4302-121">Next steps</span></span>

<span data-ttu-id="a4302-122">Zie voor meer informatie over de functies voor het uploaden van bestanden van IoT Hub [uploaden van bestanden van een apparaat] [ lnk-upload] in de IoT Hub developer guide.</span><span class="sxs-lookup"><span data-stu-id="a4302-122">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in the IoT Hub developer guide.</span></span>

<span data-ttu-id="a4302-123">Volg deze koppelingen voor meer informatie over het beheren van Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="a4302-123">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="a4302-124">[Bulksgewijs IoT-apparaten beheren][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="a4302-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="a4302-125">[IoT Hub metrische gegevens][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="a4302-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="a4302-126">[Bewerkingen controleren][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="a4302-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="a4302-127">Als u wilt de mogelijkheden van IoT Hub verder verkennen, Zie:</span><span class="sxs-lookup"><span data-stu-id="a4302-127">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="a4302-128">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="a4302-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="a4302-129">[Een apparaat simuleren met IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="a4302-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="a4302-130">[Beveiligen van uw IoT-oplossing bouwen up][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="a4302-130">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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

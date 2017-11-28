---
title: uploaden van aaaUse hello Azure portal tooconfigure bestand | Microsoft Docs
description: Hoe toouse hello Azure portal tooconfigure bestandsuploads uw IoT hub tooenable-bestand van verbonden apparaten. Bevat informatie over het configureren van Hallo bestemming Azure storage-account.
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
ms.openlocfilehash: b90c3fbed47b4eb144d3cb7480068b7cfc776ba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a><span data-ttu-id="2f990-104">IoT Hub bestandsuploads met hello Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="2f990-104">Configure IoT Hub file uploads using hello Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="2f990-105">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="2f990-105">File upload</span></span>

<span data-ttu-id="2f990-106">Hallo toouse [bestand uploaden functionaliteit in IoT-Hub][lnk-upload], moet u eerst een Azure Storage-account koppelen met de hub.</span><span class="sxs-lookup"><span data-stu-id="2f990-106">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="2f990-107">Selecteer **uploaden bestand** toodisplay een lijst met eigenschappen van bestand laden voor Hallo IoT-hub die wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="2f990-107">Select **File upload** toodisplay a list of file upload properties for hello IoT hub that is being modified.</span></span>

![IoT Hub-bestand voor de weergave-instellingen in de portal Hallo uploaden][13]

<span data-ttu-id="2f990-109">**Storage-container**: gebruik hello Azure portal tooselect een blobcontainer in een Azure Storage-account in uw huidige Azure-abonnement tooassociate met uw IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="2f990-109">**Storage container**: Use hello Azure portal tooselect a blob container in an Azure Storage account in your current Azure subscription tooassociate with your IoT Hub.</span></span> <span data-ttu-id="2f990-110">Indien nodig, kunt u een Azure Storage-account op Hallo **opslagaccounts** blade en blob-container op Hallo **Containers** blade.</span><span class="sxs-lookup"><span data-stu-id="2f990-110">If necessary, you can create an Azure Storage account on hello **Storage accounts** blade and blob container on hello **Containers** blade.</span></span> <span data-ttu-id="2f990-111">IoT Hub genereert automatisch SAS URI's met schrijven machtigingen toothis blob-container voor apparaten toouse wanneer het uploaden van bestanden.</span><span class="sxs-lookup"><span data-stu-id="2f990-111">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

![Storage-containers voor uploaden van het bestand in Hallo portal weergeven][14]

<span data-ttu-id="2f990-113">**Meldingen ontvangen voor de geüploade bestanden**: bestand uploaden meldingen via Hallo aan/uit- of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="2f990-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via hello toggle.</span></span>

<span data-ttu-id="2f990-114">**SAS TTL**: deze instelling is Hallo time-to-live Hallo SAS URI's toohello apparaat geretourneerd door de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2f990-114">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="2f990-115">Tooone uur standaard ingesteld, maar kunnen worden aangepast tooother waarden met behulp van Hallo schuifregelaar.</span><span class="sxs-lookup"><span data-stu-id="2f990-115">Set tooone hour by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="2f990-116">**Bestand notification instellingen standaard TTL**: Hallo time-to-live van een bestand uploaden melding voordat het is verlopen.</span><span class="sxs-lookup"><span data-stu-id="2f990-116">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="2f990-117">Tooone dag standaard ingesteld, maar kunnen worden aangepast tooother waarden met behulp van Hallo schuifregelaar.</span><span class="sxs-lookup"><span data-stu-id="2f990-117">Set tooone day by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="2f990-118">**Melding levering van het maximum aantal bestanden**: Hallo aantal keren dat Hallo IoT Hub pogingen toodeliver een melding van bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="2f990-118">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="2f990-119">Too10 standaard ingesteld, maar kunnen worden aangepast tooother waarden met behulp van Hallo schuifregelaar.</span><span class="sxs-lookup"><span data-stu-id="2f990-119">Set too10 by default but can be customized tooother values using hello slider.</span></span>

![Het uploaden van het IoT-Hub in Hallo portal configureren][15]

## <a name="next-steps"></a><span data-ttu-id="2f990-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f990-121">Next steps</span></span>

<span data-ttu-id="2f990-122">Zie voor meer informatie over functies voor het uploaden van bestanden Hallo van IoT Hub [uploaden van bestanden van een apparaat] [ lnk-upload] in Hallo Ontwikkelaarshandleiding voor IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2f990-122">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in hello IoT Hub developer guide.</span></span>

<span data-ttu-id="2f990-123">Volg deze koppelingen toolearn meer over het beheren van Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="2f990-123">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="2f990-124">[Bulksgewijs IoT-apparaten beheren][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="2f990-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="2f990-125">[IoT Hub metrische gegevens][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="2f990-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="2f990-126">[Bewerkingen controleren][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="2f990-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="2f990-127">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="2f990-127">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="2f990-128">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="2f990-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="2f990-129">[Een apparaat simuleren met IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="2f990-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="2f990-130">[Uw IoT-oplossing van Hallo gemalen beveiligen][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="2f990-130">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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

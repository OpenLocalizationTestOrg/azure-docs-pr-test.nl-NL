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
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a>IoT Hub bestandsuploads met hello Azure-portal configureren

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a>Bestand uploaden

Hallo toouse [bestand uploaden functionaliteit in IoT-Hub][lnk-upload], moet u eerst een Azure Storage-account koppelen met de hub. Selecteer **uploaden bestand** toodisplay een lijst met eigenschappen van bestand laden voor Hallo IoT-hub die wordt gewijzigd.

![IoT Hub-bestand voor de weergave-instellingen in de portal Hallo uploaden][13]

**Storage-container**: gebruik hello Azure portal tooselect een blobcontainer in een Azure Storage-account in uw huidige Azure-abonnement tooassociate met uw IoT-Hub. Indien nodig, kunt u een Azure Storage-account op Hallo **opslagaccounts** blade en blob-container op Hallo **Containers** blade. IoT Hub genereert automatisch SAS URI's met schrijven machtigingen toothis blob-container voor apparaten toouse wanneer het uploaden van bestanden.

![Storage-containers voor uploaden van het bestand in Hallo portal weergeven][14]

**Meldingen ontvangen voor de geüploade bestanden**: bestand uploaden meldingen via Hallo aan/uit- of uitschakelen.

**SAS TTL**: deze instelling is Hallo time-to-live Hallo SAS URI's toohello apparaat geretourneerd door de IoT Hub. Tooone uur standaard ingesteld, maar kunnen worden aangepast tooother waarden met behulp van Hallo schuifregelaar.

**Bestand notification instellingen standaard TTL**: Hallo time-to-live van een bestand uploaden melding voordat het is verlopen. Tooone dag standaard ingesteld, maar kunnen worden aangepast tooother waarden met behulp van Hallo schuifregelaar.

**Melding levering van het maximum aantal bestanden**: Hallo aantal keren dat Hallo IoT Hub pogingen toodeliver een melding van bestand uploaden. Too10 standaard ingesteld, maar kunnen worden aangepast tooother waarden met behulp van Hallo schuifregelaar.

![Het uploaden van het IoT-Hub in Hallo portal configureren][15]

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over functies voor het uploaden van bestanden Hallo van IoT Hub [uploaden van bestanden van een apparaat] [ lnk-upload] in Hallo Ontwikkelaarshandleiding voor IoT Hub.

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

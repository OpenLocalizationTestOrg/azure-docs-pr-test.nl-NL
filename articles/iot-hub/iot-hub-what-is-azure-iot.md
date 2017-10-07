---
title: aaaAzure oplossingen voor Internet der dingen (IoT Suite) | Microsoft Docs
description: Overzicht van de architectuur van een steekproef IoT-oplossing en hoe deze zich verhoudt toodevices, Hallo service Azure IoT Hub, Azure IoT-apparaat-SDK's, Azure IoT service SDK's en andere Azure-services.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a859e379-dca7-42fa-bdf6-1125c86ad140
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 2d934e3f988c530de6a242869c021712d2aa1576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a>Volgende stappen

Azure IoT Hub is een Azure-service voor beveiligde en betrouwbare bidirectionele communicatie tussen de back-end van uw oplossing en miljoenen apparaten. Hiermee kunt Hallo back-end oplossing voor:

* telemetrie op schaal van uw apparaten te ontvangen;
* Gegevens van uw apparaten tooa stream-gebeurtenisverwerking routeren.
* uploads van bestanden vanaf apparaten te ontvangen;
* Cloud-naar-apparaat-berichten toospecific apparaten verzenden.

U kunt uw eigen back-end oplossing IoT Hub-tooimplement gebruiken. IoT-Hub bevat bovendien een identiteit register gebruikt tooprovision apparaten, hun beveiligingsreferenties en hun rechten tooconnect toohello IoT-hub. Zie toolearn meer informatie over IoT Hub [wat is IoT Hub?] [lnk-iot-hub].

toolearn hoe Azure IoT Hub kunt standaarden gebaseerd Apparaatbeheer voor u tooremotely beheren, configureren en bijwerken van uw apparaten, Zie [overzicht van Apparaatbeheer met IoT Hub][lnk-device-management].

tooimplement clienttoepassingen op een groot aantal hardwareplatforms en besturingssystemen, kunt u apparaat-hello Azure IoT SDK's. Hallo apparaat-SDK's bevatten bibliotheken die vergemakkelijken verzenden telemetrie tooan IoT hub en ontvangst cloud-naar-apparaat-berichten. Wanneer u Hallo apparaat-SDK's gebruikt, kunt u kiezen uit diverse netwerk protocollen toocommunicate met IoT Hub. meer, Zie Hallo toolearn [informatie over apparaat-SKD's][lnk-device-sdks].

schrijven van code en enkele voorbeelden uitvoeren gestart tooget Zie Hallo [aan de slag met IoT Hub] [ lnk-getstarted] zelfstudie.

Wellicht bent u ook geïnteresseerd in [Azure IoT Suite][lnk-iot-suite]. Dit is een verzameling van vooraf geconfigureerde oplossingen. IoT Suite kunt u tooget snel aan de slag en IoT-projecten tooaddress algemene IoT-scenario's--zoals externe controle, beheer van bedrijfsmiddelen en voorspeld onderhoud worden geschaald.

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md

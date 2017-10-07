---
title: aaaAzure IoT Hub IP-verbindingsfilters | Microsoft Docs
description: Hoe toouse IP filteren tooblock verbindingen van specifieke IP-adressen voor tooyour Azure IoT hub. U kunt de verbindingen van afzonderlijke of bereiken van IP-adressen blokkeren.
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a>IP-filters gebruiken

Beveiliging is een belangrijk aspect van een IoT-oplossing op basis van Azure IoT Hub. Soms moet u tooexplicitly Hallo IP-adressen waaruit apparaten verbinding maken als onderdeel van de beveiligingsconfiguratie opgeven. Hallo _IP-filter_ functie kunt u tooconfigure regels voor weigeren of verkeer van specifieke IPv4-adressen accepteren.

## <a name="when-toouse"></a>Wanneer toouse

Er zijn twee specifieke gebruiksvoorbeelden wanneer het is nuttig tooblock Hallo Iothub eindpunten voor bepaalde IP-adressen:

- Uw IoT-hub moet ontvangen verkeer alleen via een opgegeven IP-adressen en alle andere afwijzen. Bijvoorbeeld, het gebruik van uw IoT-hub met [Azure Express Route] toocreate particuliere verbindingen tussen een IoT-hub en uw on-premises infrastructuur.
- U moet tooreject verkeer van IP-adressen die zijn geïdentificeerd als verdacht door Hallo IoT hub-beheerder.

## <a name="how-filter-rules-are-applied"></a>Hoe filterregels worden toegepast

Hallo IP-filterregels worden toegepast op Hallo serviceniveau IoT Hub. Daarom toepassing hello IP-filterregels tooall verbindingen van apparaten en back-end-apps met behulp van een ondersteund protocol.

Elke verbindingspoging van een IP-adres dat overeenkomt met een rejecting IP-regel in uw IoT-hub ontvangt een niet-geautoriseerde 401-statuscode en de beschrijving. Hallo IP-regel niet wordt vermeld in het antwoord Hallo-bericht.

## <a name="default-setting"></a>Standaardinstelling

Standaard Hallo **IP-Filter** raster in Hallo-portal voor een IoT-hub is leeg. Deze instelling betekent dat uw hub verbindingen elk IP-adres aanvaardt. Deze instelling is gelijkwaardig tooa regel die Hallo 0.0.0.0/0 IP-adresbereik accepteert.

![IoT Hub standaard IP-filter-instellingen][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a>De regel van een IP-filter toevoegen of bewerken

Wanneer u een IP-filterregel toevoegt, wordt u gevraagd Hallo volgende waarden op te geven:

- Een **IP-filter regelnaam** die moet een unieke, niet-hoofdlettergevoelige, alfanumerieke tekenreeks van too128 tekens lang zijn. Alleen ASCII-7-bits Hallo alfanumerieke tekens plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` worden geaccepteerd.
- Selecteer een **afwijzen** of **accepteren** als Hallo **actie** voor Hallo IP-filterregel.
- Geef één IPv4-adres of een blok IP-adressen in CIDR-notatie. Bijvoorbeeld, in CIDR notatie 192.168.100.0/22 vertegenwoordigt Hallo 1024 IPv4-adressen van 192.168.100.0 too192.168.103.255.

![Toevoegen van een IP-filter regel tooan IoT-hub][img-ip-filter-add-rule]

Nadat u de regel Hallo opslaat, ziet u een waarschuwing meegedeeld dat Hallo-update wordt uitgevoerd.

![Meldingen over het opslaan van een regel voor IP-filter][img-ip-filter-save-new-rule]

Hallo **toevoegen** optie wordt uitgeschakeld wanneer u Hallo maximaal 10 filterregels voor de IP-bereiken.

U kunt een bestaande regel bewerken door te dubbelklikken op Hallo rij die Hallo regel bevat.

> [!NOTE]
> Weigeren IP adressen kunnen voorkomen dat andere Azure-Services (zoals Azure Stream Analytics, Azure Virtual Machines of Hallo apparaat Explorer in de portal Hallo) interactie met Hallo IoT-hub.

> [!WARNING]
> Als u Azure Stream Analytics (ASA) tooread berichten van een iothub met IP-filtering is ingeschakeld, gebruikt u Hallo Event Hub-compatibele naam en het eindpunt van uw IoT-Hub in Hallo ASA-verbindingsreeks.

## <a name="delete-an-ip-filter-rule"></a>Een IP-filter-regel verwijderen

toodelete een filterregel IP-Selecteer een of meer regels in Hallo raster en klik op **verwijderen**.

![Een IoT Hub IP-filter-regel verwijderen][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a>IP-filter Regeltoepassing

IP-filterregels in volgorde worden toegepast en Hallo van de eerste regel die overeenkomt met Hallo IP-adres Hallo bepaalt accepteren of weigeren actie.

Als u wilt dat de adressen tooaccept in Hallo bereik 192.168.100.0/22 en alle andere weigeren, moet de eerste regel Hallo in raster Hallo Hallo adresbereik 192.168.100.0/22 accepteren. de volgende regel Hallo moet alle adressen weigeren met behulp van Hallo bereik 0.0.0.0/0.

U kunt Hallo volgorde van uw IP-filterregels in Hallo raster wijzigen door Hallo drie verticale punten aan Hallo begin van een rij te klikken en slepen en neerzetten.

toosave voor uw nieuwe IP-filter regel volgorde, klikt u op **opslaan**.

![Hallo-volgorde van uw IoT Hub IP-filterregels wijzigen][img-ip-filter-rule-order]

## <a name="next-steps"></a>Volgende stappen

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

- [Bewerkingen controleren][lnk-monitor]
- [IoT Hub metrische gegevens][lnk-metrics]

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md
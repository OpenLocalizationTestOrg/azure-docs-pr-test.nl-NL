---
title: aaaUnderstand prijzen van Azure IoT Hub | Microsoft Docs
description: Handleiding voor ontwikkelaars - informatie over hoe softwarelicentiecontrole en prijzen van werkt met IoT Hub, inclusief voorbeelden gegaan.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2016
ms.author: elioda
ms.openlocfilehash: e294c0b7f483e042ca3f63e93c14e0c2d773ae7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-pricing-information"></a>Azure IoT Hub prijsgegevens

[Azure IoT Hub prijzen] [ lnk-pricing] biedt Hallo algemene informatie over de verschillende SKU's en prijzen voor IoT Hub. Dit artikel bevat aanvullende informatie over hoe verschillende functies van de IoT Hub worden gemeten als Hallo door de IoT Hub berichten.

## <a name="charges-per-operation"></a>Kosten per bewerking

| Bewerking | Factureringsgegevens | 
| --------- | ------------------- |
| Registerbewerkingen voor identiteit <br/> (maken, ophalen, weergeven, bijwerken en verwijderen) | Niet in rekening gebracht. |
| Apparaat-naar-cloud-berichten | Verzonden berichten in rekening worden gebracht in segmenten van 4 KB op inkomend in IoT Hub, bijvoorbeeld dat een 6-KB-bericht 2 berichten in rekening wordt gebracht. |
| Cloud-naar-apparaat-berichten | Verzonden berichten in segmenten van 4 KB in rekening worden gebracht, bijvoorbeeld een 6-KB-bericht 2 berichten in rekening wordt gebracht. |
| Uploaden van bestanden | Bestand overdracht tooAzure opslag is niet gemeten door de IoT-Hub. Bestand overdracht inleiding en het voltooien van berichten worden in rekening gebracht als mailberichten gemeten in intervallen van 4 KB. Bijvoorbeeld, een bestand 10 MB is in rekening gebracht twee berichten in toevoeging toohello Azure Storage kosten. |
| Directe methoden | Geslaagde methodeaanvragen in segmenten van 4 KB in rekening worden gebracht, antwoorden met niet-lege instanties in rekening worden gebracht in de 4 KB als aanvullende berichten. Aanvragen toodisconnected apparaten worden in rekening gebracht als berichten in segmenten van 4 KB. Bijvoorbeeld, een methode met een 6-KB-instantie die in een antwoord met geen hoofdcode van Hallo-apparaat resulteert, wordt in rekening gebracht als twee berichten; een methode met een 6-KB-instantie die in een antwoord 1 KB van Hallo-apparaat resulteert, wordt in rekening gebracht als twee berichten voor Hallo aanvraag plus een ander bericht Hallo-antwoorden. |
| Apparaatdubbel leest | Apparaat twin leest uit Hallo-apparaat en Hallo oplossing terug end worden in rekening gebracht als berichten in een 512-byte-segmenten. Bijvoorbeeld lezen van een apparaat 6 KB-twin wordt in rekening gebracht als 12 berichten. |
| Apparaat twin updates (tags en eigenschappen) | Apparaat twin updates van het Hallo-apparaat en Hallo-apparaat als in segmenten van 512-byte-berichten in rekening worden gebracht. Bijvoorbeeld lezen van een apparaat 6 KB-twin wordt in rekening gebracht als 12 berichten. |
| Apparaat twin query 's | Query's worden in rekening gebracht als berichten, afhankelijk van Hallo resultaat grootte in 512-byte-segmenten. |
| Taakbewerkingen <br/> (maken, bijwerken, weergeven, verwijderen) | Niet in rekening gebracht. |
| Taken per apparaat bewerkingen | Bewerkingen (zoals twin apparaatupdates en methoden) taken in rekening worden gebracht die normaal werken. Een taak waardoor 1000 methodeaanroepen met 1 KB aanvragen en antwoorden lege hoofdcode is voor het exemplaar in rekening gebracht 1000 berichten. |

> [!NOTE]
> Alle grootte wordt berekend overweegt Hallo nettolading grootte in bytes (protocol framing genegeerd). In geval van berichten (die eigenschappen en hoofdtekst) Hallo grootte wordt berekend op een manier protocol networkdirect zoals beschreven in Hallo [messaging Ontwikkelaarshandleiding voor IoT-Hub][lnk-message-size].

## <a name="example-1"></a># 1

Een apparaat verzendt één 1 KB apparaat-naar-cloud bericht per minuut tooIoT Hub, die vervolgens door Azure Stream Analytics wordt gelezen. Hallo back-end oplossing roept een methode (met 512-byte-nettolading) op Hallo apparaat elke tien minuten tootrigger een specifieke actie. Hallo apparaat reageert toohello methode met een resultaat van 200 bytes.

Hallo apparaat 1 bericht verbruikt * 60 minuten * 24 uur 1440 berichten per dag voor hello apparaat-naar-cloud-berichten, en 2 aanvraag plus antwoord = * 6 keer per uur * 24 uur = 288 berichten voor Hallo-methoden voor een totaal van 1728 berichten per dag.

## <a name="example-2"></a># 2

Een apparaat verzendt één 100 KB apparaat-naar-cloud bericht elk uur. Werkt het ook de apparaat-twin met 1 KB nettoladingen elke 4 uur. Hallo oplossing terug eenmaal per dag, leest Hallo 14 KB apparaat twin beëindigen en bijgewerkt met 512-byte-nettoladingen toochange configuraties.

Hallo apparaat verbruikt 25 (100KB / 4KB) berichten * 24 uur voor apparaat-naar-cloudberichten plus 1 bericht * 6 keer per dag voor apparaatupdates twin, voor een totaal van 156 berichten per dag.
Hallo back-end oplossing verbruikt 28 berichten (14KB/0,5 KB) tooread Hallo apparaat twin plus 1 bericht tooupdate het voor een totaal van 29 berichten.

In totaal verbruiken Hallo-apparaat en Hallo back-end oplossing 185 berichten per dag.


[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-message-size]: iot-hub-devguide-messages-construct.md

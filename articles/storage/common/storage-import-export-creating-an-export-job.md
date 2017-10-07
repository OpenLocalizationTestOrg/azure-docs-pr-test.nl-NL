---
title: exporteren van een taak voor Azure Import/Export aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate exporteren van een taak voor Hallo Microsoft Azure Import/Export-service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a>Een exporttaak voor hello Azure Import/Export-service maken
Maken van een exporttaak voor Hallo Hallo REST-API met Microsoft Azure Import/Export-service omvat Hallo stappen te volgen:

-   Hallo selecteren tooexport blobs.

-   Het verkrijgen van een back-ups van locatie.

-   Hallo exporttaak maken.

-   Verzending van uw tooMicrosoft lege stations via een ondersteunde Provider-service.

-   Hallo exporttaak met Hallo pakketgegevens bijwerken.

-   Hallo ontvangen stations terug van Microsoft.

 Zie [Hallo Windows Azure Import/Export-service tooTransfer gegevens tooBlob opslag met](storage-import-export-service.md) voor een overzicht van Hallo Import/Export-service en een zelfstudie die u laat zien hoe toouse hello [Azure-portal](https://portal.azure.com/) toocreate en beheren van importeren en exporteren van taken.

## <a name="selecting-blobs-tooexport"></a>Blobs tooexport selecteren
 een exporttaak toocreate, moet u tooprovide een lijst met blobs gewenste tooexport van uw opslagaccount. Er zijn een aantal manieren tooselect blobs toobe geëxporteerd:

-   U kunt een pad relatief blob tooselect één blob en alle bijbehorende momentopnamen.

-   U kunt een pad relatief blob tooselect één blob met uitzondering van de momentopnamen te gebruiken.

-   U kunt een blobpad relatief en een momentopname tijd tooselect één momentopname gebruiken.

-   Kunt u een blob-voorvoegsel tooselect alle blobs en momentopnamen Hello voorvoegsel opgegeven.

-   U kunt alle blobs en momentopnamen in de storage-account Hallo exporteren.

 Zie voor meer informatie over het opgeven van blobs tooexport, Hallo [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) bewerking.

## <a name="obtaining-your-shipping-location"></a>Het verkrijgen van de locatie van uw back-ups
Voordat u maakt een taak voor het exporteren, moet u tooobtain de naam van een locatie en het adres door de aanroepende Hallo [locatie ophalen](https://portal.azure.com) of [lijst locaties](/rest/api/storageimportexport/listlocations) bewerking. `List Locations`retourneert een lijst met locaties en hun e-mailadressen. U kunt een locatie selecteren van Hallo lijst geretourneerd en verzendadres uw toothat harde schijven. U kunt ook Hallo `Get Location` bewerking tooobtain Hallo verzendadres rechtstreeks voor een specifieke locatie.

Hallo stappen hieronder tooobtain Hallo back-upfunctie locatie:

-   Geef de naam Hallo Hallo-locatie van uw opslagaccount. Deze waarde kan worden gevonden in het Hallo **locatie** op Hallo van het opslagaccount **Dashboard** in Hallo-classic portal of voor de query met behulp van Hallo service management API-bewerking [ophalen Eigenschappen van het opslagaccount](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Hallo-locatie die beschikbaar tooprocess dit opslagaccount ophalen door de aanroepende Hallo `Get Location` bewerking.

-   Als hello `AlternateLocations` eigenschap Hallo locatie Hallo locatie zelf bevat, dan is dit geen probleem toouse deze locatie. Anders aanroepen Hallo `Get Location` opnieuw met een van de alternatieve locaties Hallo. de oorspronkelijke locatie Hallo mogelijk tijdelijk worden gesloten voor onderhoud.

## <a name="creating-hello-export-job"></a>Hallo exporttaak maken
 toocreate hello exporttaak, aanroep Hallo [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) bewerking. U moet tooprovide Hallo volgende informatie:

-   Een naam voor het Hallo-taak.

-   Hallo opslagaccountnaam.

-   Hallo back-upfunctie locatienaam, in de vorige stap Hallo verkregen.

-   Een taaktype (exporteren).

-   Hallo-retouradres waar Hallo schijven moeten worden verzonden nadat de exporttaak Hallo is voltooid.

-   Hallo lijst met BLOB's (of blob voorvoegsels) toobe geëxporteerd.

## <a name="shipping-your-drives"></a>Verzending van uw schijven
 Vervolgens hello Azure-hulpprogramma voor importeren/exporteren toodetermine Hallo aantal stations dat u toosend, op basis van Hallo blobs die u hebt geselecteerd geëxporteerd toobe moet gebruiken en Hallo grootte van de schijf. Zie Hallo [Azure Import/Export hulpprogramma verwijzing](storage-import-export-tool-how-to-v1.md) voor meer informatie.

 Pakket Hallo stations in een enkel pakket en moeten worden verzonden toohello adres verkregen in Hallo eerder stap. Houd er rekening mee Hallo nummer van uw pakket voor de volgende stap Hallo bijhouden.

> [!NOTE]
>  U moet uw stations via een ondersteunde Provider-service, die het pakket van een volgnummer voorzien verzenden.

## <a name="updating-hello-export-job-with-your-package-information"></a>Hallo exporttaak wordt bijgewerkt met de informatie van uw pakket
 Nadat u het volgnummer hebt, roept u Hallo [Update taakeigenschappen](/rest/api/storageimportexport/jobs#Jobs_Update) bewerkingsnaam tooupdated Hallo carrier en het volgnummer voor Hallo-taak. U kunt optioneel Hallo aantal stations, Hallo retouradres en ook Hallo back-upfunctie voor datum opgeven.

## <a name="receiving-hello-package"></a>Hallo-pakket wordt ontvangen
 Nadat de taak voor het exporteren is verwerkt, wordt uw stations tooyou met uw versleutelde gegevens worden geretourneerd. U kunt Hallo BitLocker-sleutel ophalen voor elke Hallo stations door aanroepen Hallo [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) bewerking. U kunt vervolgens Hallo-station met de sleutel Hallo ontgrendelen. Hallo station manifestbestand op elk station bevat Hallo lijst met bestanden op het Hallo-station, evenals de oorspronkelijke blobadres Hallo voor elk bestand.

## <a name="next-steps"></a>Volgende stappen

* [Met behulp van REST-API voor Hallo Import/Export-service](storage-import-export-using-the-rest-api.md)

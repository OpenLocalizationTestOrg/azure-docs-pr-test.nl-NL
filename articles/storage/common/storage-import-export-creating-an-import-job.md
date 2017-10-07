---
title: aaaCreate een Import-taak voor Azure Import/Export | Microsoft Docs
description: Meer informatie over hoe toocreate importeren voor Hallo Microsoft Azure Import/Export-service.
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a>Maken van een import-taak voor hello Azure Import/Export-service

Maken van een import-taak voor Hallo Hallo REST-API met Microsoft Azure Import/Export-service omvat Hallo stappen te volgen:

-   Schijven met hello Azure-hulpprogramma voor importeren/exporteren wordt voorbereid.

-   Het verkrijgen van Hallo locatie toowhich tooship Hallo station.

-   Hallo import-taak maken.

-   Back-upfunctie Hallo tooMicrosoft stations via een ondersteunde Provider-service.

-   Hallo import-taak met details van de back-upfunctie Hallo bijwerken.

 Zie [Hallo Microsoft Azure Import/Export-service tooTransfer gegevens tooBlob opslag met](storage-import-export-service.md) voor een overzicht van Hallo Import/Export-service en een zelfstudie die u laat zien hoe toouse hello [Azure-portal](https://portal.azure.com/) toocreate en beheren van importeren en exporteren van taken.

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a>Voorbereiden van schijven met hello Azure-hulpprogramma voor importeren/exporteren

Hallo stappen tooprepare stations voor een import-taak zijn Hallo dezelfde of hebt u Hallo jobvia Hallo portal of via Hallo REST-API.

Hieronder vindt u een kort overzicht van de voorbereiding van het station. Raadpleeg toohello [Azure Import-ExportTool verwijzing](storage-import-export-tool-how-to-v1.md) voor volledige instructies. U kunt hello Azure-hulpprogramma voor importeren/exporteren downloaden [hier](http://go.microsoft.com/fwlink/?LinkID=301900).

Voorbereiden van de schijf omvat:

-   Identificerende Hallo gegevens toobe geïmporteerd.

-   Hallo bestemming blobs in Windows Azure-opslagservice identificeren.

-   Met behulp van hello Azure-hulpprogramma voor importeren/exporteren toocopy uw gegevens tooone of meer harde schijven.

 Hello Azure-hulpprogramma voor importeren/exporteren wordt ook een manifestbestand genereren voor elk van de stations Hallo als deze wordt voorbereid. Een manifestbestand bevat:

-   Een opsomming van alle Hallo bestanden die zijn bedoeld voor het uploaden en Hallo toewijzingen van deze bestanden tooblobs.

-   Controlesommen van Hallo segmenten van elk bestand.

-   Informatie over de metagegevens en eigenschappen tooassociate Hallo met elke blob.

-   Een lijst van Hallo actie tootake als een blob die wordt geüpload Hallo heeft dezelfde naam als een bestaande blob in Hallo-container. Mogelijke opties zijn: a) blob Hallo overschrijven met Hallo-bestand, b) houden Hallo bestaande blob- en skip Hallo-bestand uploadt, c) toevoegen aan de naam van een achtervoegsel toohello dat geen met andere bestanden conflict.

## <a name="obtaining-your-shipping-location"></a>Het verkrijgen van de locatie van uw back-ups

Voordat u een import-taak maakt, moet u tooobtain de naam van een locatie en het adres door de aanroepende Hallo [lijst locaties](/rest/api/storageimportexport/listlocations) bewerking. `List Locations`retourneert een lijst met locaties en hun e-mailadressen. U kunt een locatie selecteren van Hallo lijst geretourneerd en verzendadres uw toothat harde schijven. U kunt ook Hallo `Get Location` bewerking tooobtain Hallo verzendadres rechtstreeks voor een specifieke locatie.

 Hallo stappen hieronder tooobtain Hallo back-upfunctie locatie:

-   Geef de naam Hallo Hallo-locatie van uw opslagaccount. Deze waarde kan worden gevonden in het Hallo **locatie** op Hallo van het opslagaccount **Dashboard** in Azure portal of voor de query met behulp van Hallo service management API-bewerking Hallo [opslag ophalen Eigenschappen van account](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Hallo-locatie die beschikbaar tooprocess dit opslagaccount ophalen door de aanroepende Hallo `Get Location` bewerking.

-   Als hello `AlternateLocations` eigenschap Hallo locatie Hallo locatie zelf bevat, dan is dit geen probleem toouse deze locatie. Anders aanroepen Hallo `Get Location` opnieuw met een van de alternatieve locaties Hallo. de oorspronkelijke locatie Hallo mogelijk tijdelijk worden gesloten voor onderhoud.

## <a name="creating-hello-import-job"></a>Hallo import-taak maken
toocreate hello import-taak, aanroep Hallo [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) bewerking. U moet tooprovide Hallo volgende informatie:

-   Een naam voor het Hallo-taak.

-   Hallo opslagaccountnaam.

-   Hallo locatienaam, verkregen van de vorige stap Hallo back-upfunctie.

-   Een taaktype (importeren).

-   Hallo-retouradres waar Hallo schijven moeten worden verzonden nadat Hallo import-taak is voltooid.

-   Hallo-lijst met stations in Hallo-taak. Voor elk station moet u de volgende informatie die is verkregen tijdens de stap ter voorbereiding van Hallo station Hallo opnemen:

    -   Hallo station Id

    -   Hallo BitLocker-sleutel

    -   Hallo manifestbestand relatief pad op de harde schijf Hallo

    -   Hallo Base16 gecodeerd manifestbestand MD5-hash

## <a name="shipping-your-drives"></a>Verzending van uw schijven
U moet uw stations toohello-adres dat u hebt ontvangen van de vorige stap Hallo verzenden en u Hallo Import/Export-service met het volgnummer van het pakket Hallo Hallo moet opgeven.

> [!NOTE]
>  U moet uw stations via een ondersteunde Provider-service, die het pakket van een volgnummer voorzien verzenden.

## <a name="updating-hello-import-job-with-your-shipping-information"></a>Hallo import-taak wordt bijgewerkt met uw back-ups van gegevens
Nadat u het volgnummer hebt, roept u Hallo [Update taakeigenschappen](/api/storageimportexport/jobs#Jobs_Update) bewerking tooupdate Hallo carrier naam, Hallo volgnummer voor Hallo taak en Hallo carrier nummer voor return back-ups van de back-upfunctie. U kunt optioneel Hallo aantal stations- en back-upfunctie ook datum Hallo opgeven.

## <a name="next-steps"></a>Volgende stappen

* [Met behulp van REST-API voor Hallo Import/Export-service](storage-import-export-using-the-rest-api.md)

---
title: informatie over de aaaRetrieving voor een Azure Import/Export-taak | Microsoft Docs
description: Meer informatie over hoe tooobtain statusinformatie voor de taken van Microsoft Azure Import/Export-service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 22d7e5f0-94da-49b4-a1ac-dd4c14a423c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: muralikk
ms.openlocfilehash: cbc35660519573d92f641924ac0025c9e577d69b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="retrieving-state-information-for-an-importexport-job"></a>Bij het ophalen van informatie over de status voor een taak van Import/Export
U kunt aanroepen Hallo [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) bewerking tooretrieve informatie over beide importeren en exporteren van taken. Hallo-informatie geretourneerd omvat:

-   Hallo huidige status van Hallo-taak.

-   Hallo geschatte percentage dat elke taak is voltooid.

-   Hallo huidige status van elk station.

-   URI's voor blobs bevat foutenlogboeken en uitgebreide logboekregistratie-informatie (indien ingeschakeld).

Hallo volgende secties wordt uitgelegd Hallo informatie die wordt geretourneerd door Hallo `Get Job` bewerking.

## <a name="job-states"></a>Taakstatussen
Hallo-tabel en Hallo status diagram hieronder wordt beschreven Hallo statussen van een taak via tijdens de levensduur overgangen. huidige status van taak Hallo Hallo kan worden bepaald door de aanroepende Hallo `Get Job` bewerking.

![JobStates](./media/storage-import-export-retrieving-state-info-for-a-job/JobStates.png "JobStates")

Hallo beschrijft volgende tabel elke status die een taak kan doorgeven.

|Taakstatus|Beschrijving|
|---------------|-----------------|
|`Creating`|Nadat u Hallo Job Put-bewerking aanroept, wordt een taak gemaakt en de status is ingesteld, te`Creating`. Terwijl hello Hallo wordt `Creating` staat, Hallo Import/Export-service wordt ervan uitgegaan dat Hallo stations niet verzonden toohello datacenter zijn. Een taak kan in Hallo blijven `Creating` staat zijn voor up tootwo weken, waarna deze worden automatisch verwijderd door Hallo-service.<br /><br /> Als u Hallo Update taakeigenschappen bewerking aanroepen terwijl hello Hallo wordt `Creating` staat, Hallo taak blijft in Hallo `Creating` status en time-out Hallo-interval is opnieuw ingesteld tootwo weken.|
|`Shipping`|Nadat u uw pakket verzendt, moet u Hallo taakeigenschappen bijwerken bewerking Hallo-updatestatus van Hallo taak te aanroepen`Shipping`. status van de back-upfunctie Hallo kan alleen worden ingesteld als hello `DeliveryPackage` (postcode carrier en volgnummer) en Hallo `ReturnAddress` eigenschappen zijn ingesteld voor Hallo-taak.<br /><br /> Hallo taak blijft in Hallo back-ups van de status voor up tootwo weken. Als twee weken hebt doorgegeven en Hallo stations niet zijn ontvangen, worden operators in service voor importeren/exporteren hello wordt gewaarschuwd.|
|`Received`|Nadat alle stations zijn ontvangen op Hallo Datacenter, worden taakstatus Hallo ingesteld toohello status Received hebben.|
|`Transferring`|Nadat Hallo stations zijn ontvangen op Hallo datacenter en ten minste één station verwerking is gestart, taakstatus Hallo toohello ingesteld `Transferring` status. Zie Hallo `Drive States` sectie hieronder voor meer informatie.|
|`Packaging`|Nadat alle stations verwerking is voltooid, Hallo-taak wordt geplaatst in Hallo `Packaging` status totdat Hallo stations verzonden back toohello klant zijn.|
|`Completed`|Nadat alle stations verzonden back toohello klant, zijn als Hallo taak zonder fouten is voltooid, klikt u vervolgens Hallo-taak wordt ingesteld toohello `Completed` status. Hallo taak automatisch worden verwijderd na 90 dagen in Hallo `Completed` status.|
|`Closed`|Nadat alle stations verzonden back toohello klant, zijn als er fouten tijdens de verwerking van de taak Hallo Hallo zijn, vervolgens Hallo-taak wordt ingesteld toohello `Closed` status. Hallo taak automatisch worden verwijderd na 90 dagen in Hallo `Closed` status.|

U kunt een taak alleen op bepaalde statussen annuleren. Een geannuleerde taak Hallo gegevens kopiëren stap overslaat, maar anders volgt Hallo dezelfde overgangen status als een taak die niet is geannuleerd.

Hallo bevat onderstaande tabel fouten die voor elke taakstatus, evenals de Hallo effect op Hallo taak optreden kunnen wanneer een fout optreedt.

|Taakstatus|Gebeurtenis|Resolutie / de volgende stappen|
|---------------|-----------|------------------------------|
|`Creating or Undefined`|Een of meer stations voor een taak is aangekomen, maar het Hallo-taak heeft geen Hallo `Shipping` status of er is geen record van de taak Hallo in Hallo-service.|het operationele team van Hallo Import/Export-service wordt toocontact Hallo klant toocreate proberen of Hallo taak bijwerken met de benodigde informatie toomove Hallo-taak doorsturen.<br /><br /> Als het operationele team van Hallo niet kan toocontact Hallo klant binnen twee weken, probeert Hallo operationele team tooreturn Hallo stations.<br /><br /> In de gebeurtenis Hallo die Hallo stations kunnen niet worden geretourneerd en Hallo klant kan niet worden bereikt, wordt Hallo stations veilige manier worden vernietigd 90 dagen.<br /><br /> Houd er rekening mee dat een taak kan niet worden verwerkt totdat de status is bijgewerkt, te`Shipping`.|
|`Shipping`|Hallo-pakket voor een taak niet meer dan twee weken aangekomen.|het operationele team van Hallo verwittigen Hallo klant van ontbrekende Hallo-pakket. Op basis van reactie van de klant hello, wordt Hallo operationele team ofwel Hallo interval toowait voor Hallo pakket tooarrive uitbreiden of Hallo taak annuleren.<br /><br /> In de Hallo gebeurtenis die klant Hallo kan geen verbinding worden gemaakt of niet reageert binnen 30 dagen Hallo operationele team initieert actie toomove Hallo taak in Hallo `Shipping` status rechtstreeks toohello `Closed` status.|
|`Completed/Closed`|Hallo stations nooit bereikt Hallo-mailadres van afzender of zijn beschadigd tijdens de verzending (geldt alleen tooan exporttaak).|Als stations Hallo Hallo retouradres niet bereiken, Hallo klant moet de eerste aanroep Hallo Get Job-bewerking of selectievakje Hallo taakstatus Hallo portal tooensure die Hallo stations zijn verzonden. Als Hallo stations zijn verzonden, moet Hallo klant de Neem contact op met de back-upfunctie provider tootry hello en Hallo-stations vinden.<br /><br /> Als Hallo stations zijn beschadigd tijdens de verzending, kunt Hallo klant toorequest een andere taak voor het exporteren of download Hallo ontbrekende blobs.|
|`Transferring/Packaging`|Taak is een onjuist of het adres van afzender ontbreekt.|het operationele team van Hallo wordt toohello contactpersoon voor Hallo taak tooobtain Hallo juiste adres bereiken.<br /><br /> Worden in de gebeurtenis Hallo die klant Hallo kan niet bereikt, Hallo stations worden veilig binnen 90 dagen vernietigd.|
|`Creating / Shipping/ Transferring`|Een station dat niet wordt weergegeven in de lijst van stations toobe geïmporteerd Hallo is opgenomen in de back-upfunctie pakket Hallo.|Hallo extra stations wordt niet verwerkt en wordt geretourneerd toohello klant wanneer het Hallo-taak is voltooid.|

## <a name="drive-states"></a>Station statussen
Hallo-tabel en Hallo diagram hieronder wordt beschreven Hallo levenscyclus van een afzonderlijke schijf als deze door middel van een taak worden geïmporteerd of geëxporteerd overgezet. U kunt het huidige station status Hallo ophalen door aanroepen Hallo `Get Job` bewerking en bekijken Hallo `State` element Hallo `DriveList` eigenschap.

![DriveStates](./media/storage-import-export-retrieving-state-info-for-a-job/DriveStates.png "DriveStates")

Hallo beschrijft volgende tabel elke status die een station kan doorgeven.

|Status van station|Beschrijving|
|-----------------|-----------------|
|`Specified`|Voor een import-taak als Hallo taak is gemaakt met de Hallo Job Put-bewerking, Hallo aanvankelijke status voor een station is Hallo `Specified` status. Voor een exporttaak omdat er geen station is opgegeven bij het Hallo-taak is gemaakt, Hallo initiële station status is Hallo `Received` status.|
|`Received`|Hallo station overgangen toohello `Received` status wanneer hello Import/Export-service operator Hallo stations die zijn ontvangen van het bedrijf voor een import-taak back-upfunctie Hallo is verwerkt. Voor een exporttaak Hallo initiële station status Hallo is `Received` status.|
|`NeverReceived`|Hallo-station wordt verplaatst toohello `NeverReceived` status wanneer Hallo-pakket voor een taak binnenkomt maar Hallo pakket bevat geen Hallo-station. Een station kunt ook verplaatsen naar deze status als het al twee weken geleden Hallo service Hallo back-upfunctie informatie ontvangen, maar Hallo pakket nog niet is ontvangen op Hallo Datacenter.|
|`Transferring`|Een station wordt verplaatst toohello `Transferring` status wanneer hello service begint tootransfer gegevens van Hallo station tooWindows Azure Storage.|
|`Completed`|Een station wordt verplaatst toohello `Completed` status wanneer Hallo-service heeft alle Hallo gegevens zonder fouten is overgedragen.|
|`CompletedMoreInfo`|Een station wordt verplaatst toohello `CompletedMoreInfo` status wanneer Hallo-service heeft aangetroffen enkele problemen bij het kopiëren van gegevens vanaf of toohello station. Hallo-informatie kan bestaan fouten, waarschuwingen of informatieve berichten over het overschrijven van blobs.|
|`ShippedBack`|Hallo-station wordt verplaatst toohello `ShippedBack` status wanneer van Hallo data center back toohello retouradres is verzonden.|

Hallo volgende tabel beschrijft Hallo station fout statussen en Hallo-acties die worden uitgevoerd voor elke status.

|Status van station|Gebeurtenis|Resolutie / de volgende stap|
|-----------------|-----------|-----------------------------|
|`NeverReceived`|Een station dat is gemarkeerd als `NeverReceived` (omdat deze niet is ontvangen als onderdeel van de verzending van de taak Hallo) in een andere verzending binnenkomt.|Hallo operationele team verplaatst Hallo station toohello `Received` status.|
|`N/A`|Een station dat geen deel uitmaakt van elke taak komt bij Hallo Datacenter als onderdeel van een andere taak.|Hallo-station wordt gemarkeerd als een extra schijf en wordt geretourneerd toohello klant wanneer zijn gekoppeld aan het oorspronkelijke pakket Hallo Hallo-taak is voltooid.|

## <a name="faulted-states"></a>Fout statussen
Wanneer een taak of het station tooprogress normaal via de verwachte levensduur mislukt Hallo taak of station worden verplaatst naar een `Faulted` status. Op dat moment Hallo operationele team neemt contact met Hallo klant door e-mailadres of telefoonnummer. Zodra het Hallo-probleem is opgelost, Hallo taak mislukt of station zullen worden uitgevoerd buiten het Hallo `Faulted` systeemstatus- en verplaatst naar Hallo status van de toepassing.

## <a name="next-steps"></a>Volgende stappen

* [Met behulp van REST-API voor Hallo Import/Export-service](storage-import-export-using-the-rest-api.md)

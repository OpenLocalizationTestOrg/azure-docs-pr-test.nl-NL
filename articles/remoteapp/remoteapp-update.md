---
title: aaaUpdate uw Azure RemoteApp-collectie | Microsoft Docs
description: Meer informatie over hoe tooupdate uw Azure RemoteApp-verzameling
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a>Bijwerken van een verzameling in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Er wordt een tijdje onvermijdelijk, wanneer u tooupdate Hallo apps of de afbeelding in uw Azure RemoteApp-verzameling moet worden geleverd. Als u een van Hallo installatiekopieën die zijn opgenomen in uw abonnement Azure RemoteApp in een cloud- of hybride verzameling, worden alle updates worden verwerkt door Azure RemoteApp zelf, zodat u gemakkelijk kunt plaatst.

Echter als u een aangepaste installatiekopie (dat u hebt ontwikkeld vanaf het begin of dat u hebt gemaakt door het wijzigen van een van onze installatiekopieën) gebruikt, bent u verantwoordelijk onderhouden Hallo installatiekopie en apps. Als u uw installatiekopie of Hallo Apps erin tooupdate nodig, moet u op toocreate een nieuwe, bijgewerkte versie van de installatiekopie van het Hallo en vervangen Hallo bestaande installatiekopie in de verzameling met deze nieuwe, bijgewerkte installatiekopie.

Ja, hoe moet u doen over het bijwerken van uw verzameling? Het is zeer eenvoudig:

1. Hallo-installatiekopie die u hebt gebruikt in uw verzameling bijwerken. Alle patches of de vereiste updates toepassen en sla deze op een nieuwe naam.
2. [Uploaden](remoteapp-uploadimage.md) of [importeren](remoteapp-image-on-azurevm.md) die tooRemoteApp installatiekopie.
3. Klik nu op Hallo verzameling pagina op **Update**.
4. De nieuwe installatiekopie Hallo kiezen uit Hallo **Sjablooninstallatiekopie** lijst.
5. Hier volgt de moeilijkste Hallo - moet u toodecide hoe toodeal met alle gebruikers die momenteel van een app in de verzameling Hallo gebruikmaken. Hebt u Hallo keuzes te volgen:
   
   * **Geef gebruikers 60 minuten na de update Hallo**. Zodra het Hallo-update is voltooid, wordt Azure RemoteApp een bericht tooany actieve gebruikers om door te geven toosave logboek en hun werk uit en weer aanmelden weergegeven. Na 60 minuten duurt, wordt alle actieve gebruikers dat u niet afgemeld bent automatisch afgemeld. Gebruikers kunnen direct aanmelden terug.
   * **Gebruikers direct Afmelden**. Zodra het Hallo-update is voltooid, zich afmelden bij alle gebruikers automatisch zonder waarschuwing. Als u deze optie kiest, kunnen gebruikers gegevens verliezen. Ze kunnen echter toohello app onmiddellijk opnieuw.
6. Klik op Hallo vinkje toostart Hallo bijwerken.


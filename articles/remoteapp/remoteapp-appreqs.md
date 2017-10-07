---
title: aaaApp vereisten voor Azure RemoteApp | Microsoft Docs
description: Meer informatie over de vereisten van de Hallo voor apps die u wilt dat toouse in Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fa2bcdaab457a6fbee8ac52a81d1c4154bbdce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="app-requirements"></a>App-vereisten
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Azure RemoteApp biedt ondersteuning voor streaming 32-bits of 64-bits Windows-toepassingen van een installatiekopie van Windows Server 2012 R2. De meeste bestaande 32-bits of 64-bits Windows-toepassingen uitvoeren 'als zodanig' in Azure RemoteApp (extern bureaublad-Services of voorheen bekend als Terminal Services) omgeving. Echter, er is een verschil tussen uitgevoerd en goed - sommige toepassingen goed werken en ook niet uitvoeren terwijl andere niet. Hallo volgende informatie bevat richtlijnen voor het ontwikkelen van toepassingen in een omgeving met extern bureaublad-Services en tooensure compatibiliteit testen.

Tip: Momenteel niets over het maken van voorbeelden werkt van apps voor u. Hier ziet u nieuwe onderwerpen die betrekking hebben met behulp van Microsoft Access, QuickBooks en App-V in RemoteApp.

## <a name="requirements"></a>Vereisten
Deze drie vereisten helpen als gevolgd, uw toepassing goed in RemoteApp worden uitgevoerd:

1. Toepassingen die voldoen aan alle [certificeringsvereisten voor Windows desktop-apps](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) en te voldoen[extern bureaublad-Services richtlijnen programming](https://msdn.microsoft.com/library/aa383490.aspx) heeft volledige compatibiliteit met RemoteApp.
2. Toepassingen moeten nooit gegevens lokaal opslaan op Hallo afbeeldings- of RemoteApp-exemplaren die verloren kunnen gaan.  Nadat u een RemoteApp-collectie gemaakt, Hallo exemplaren worden gekloond en staatloze zijn en mag alleen toepassingen bevatten. Gegevens opslaan in een externe bron of binnen Hallo gebruikersprofiel.
3. Aangepaste installatiekopieën mag nooit bevatten gegevens die verbroken worden kunnen.  

## <a name="testing-your-apps"></a>Uw apps testen
Gebruik deze stappen tootesting toepassingen:

1. Windows Server 2012 R2 en uw toepassing geïnstalleerd
2. Extern bureaublad inschakelen
3. Maak twee gebruikersaccounts GebruikerA en gebruiker b, beide gebruiker accounts toohello extern bureaublad-beveiligingsgroep toevoegen.
4. Meerdere sessie compatibiliteit controleren door het opstellen van twee gelijktijdige RDS sessies toohello PC tijdens het Hallo-toepassing wordt gestart.
5. App-gedrag valideren

## <a name="application-development-guidelines"></a>Richtlijnen voor het ontwikkelen van toepassing
Hallo volgen richtlijnen voor het ontwikkelen van toepassingen voor RemoteApp gebruiken.

### <a name="multiple-users"></a>Meerdere gebruikers
* Installeren van een [toepassing voor één gebruiker ](https://msdn.microsoft.com/library/aa380661.aspx)problemen kunnen veroorzaken in een omgeving.
* Toepassingen moeten [gebruikersspecifieke informatie opslaan](https://msdn.microsoft.com/library/aa383452.aspx) in gebruikersspecifieke locaties, afzonderlijk van globale gegevens die van toepassing is tooall gebruikers.
* RemoteApp maakt gebruik van meerdere [naamruimten voor objecten van de kernel](https://msdn.microsoft.com/library/aa382954.aspx); een globale naamruimte wordt hoofdzakelijk gebruikt door services in de client/server-toepassingen.
* Het is niet veilig tooassume die computernaam of het Hallo Hallo [IP-adres](https://msdn.microsoft.com/library/aa382942.aspx) toegewezen toohello computer zijn gekoppeld aan een enkele gebruiker omdat meerdere gebruikers kunnen worden geregistreerd op tegelijkertijd tooa Remote Desktop Session Host (extern bureaublad-sessie Host)-server.

### <a name="performance"></a>Prestaties
* Schakel [grafische effecten](https://msdn.microsoft.com/library/aa380822.aspx) voordat u uw app tooRemoteApp toevoegen.
* toomaximize CPU-beschikbaarheid voor alle gebruikers uitschakelen [taken op de achtergrond ](https://msdn.microsoft.com/library/aa380665.aspx) of maken van efficiënte achtergrondtaken die geen resource-intensief.
* U moet afstemmen en saldo toepassing [gebruik thread](https://msdn.microsoft.com/library/aa383520.aspx) voor een omgeving met meerdere gebruikers, met meerdere processors.
* toooptimize prestaties, het is raadzaam om voor toepassingen te[detecteren](https://msdn.microsoft.com/library/aa380798.aspx) of er in een clientsessie worden uitgevoerd.


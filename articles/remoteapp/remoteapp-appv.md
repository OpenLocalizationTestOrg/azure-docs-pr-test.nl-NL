---
title: aaaUsing App-V-apps met Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe toouse App-V-apps in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a>App-V-apps gebruiken in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

U kunt App-V-toepassingen gebruiken in een Azure RemoteApp hybride verzameling waarvoor domein is vereist.

Voordat u begint, zorg ervoor dat tooinstall Hallo App-V 5.1 client met de meest recente updates Hallo. U moet toocreate een [aangepaste installatiekopie](remoteapp-create-custom-image.md) die Hallo App-V-client bevat.  

Het is gemakkelijk toouse uw bestaande App-V-infrastructuur met Azure RemoteApp. Aangezien een hybride verzameling wordt geïmplementeerd in een Azure VNET dat toegang tooyour domeincontroller heeft en Hallo VM's verbonden met het domein zijn, kunt u gebruikmaken van uw bestaande App-v-infrastructuur en implementatie methoden tooeasyily host App-V-toepassing in Azure RemoteApp. Hier volgen enkele overwegingen die u moet rekening houden met op basis van App-V-implementatie die u momenteel hebt Hallo type:

| Configuratie-opties |  | Positief | Negatieve |
| --- | --- | --- | --- |
| Leveringsmethode |Streaming (op aanvraag) |App is altijd Hallo nieuwste en nieuwe |Eerste wachttijd |
| Gekoppeld |Snelste; App is al aanwezig op Hallo VM |Gegevensophoping - inneemt installatiekopie ruimte (maximaal 127 GB) | |
| App-locatie-opslag |Gedeelde inhoud |App wordt uitgevoerd in het geheugen van Azure RemoteApp-exemplaar |Eats geheugen en goede verbinding toostreaming (bestand) server waarop app Hallo zich bevindt |
| Schijf (in cache) |Snel kan worden uitgevoerd. De App is niet afhankelijk van beschikbaarheid van de inhoudsbron |Gegevensophoping - inneemt installatiekopie ruimte (maximaal 127 GB) | |
| Doelen |Gebruiker |Volledige zelfstandige App-V-infrastructuur vereist | |
| Global (computer) |Vooraf publiceren of de publicatie met als doel server |Moet tooupdate uw afbeelding voor Azure als u wilt dat tooupdate Hallo app (grote). Neemt enige ruimte vrij op de installatiekopie. | |

 Nadat u uw aangepaste installatiekopie en uw hybride verzameling maakt, uw toepassing publiceren, gebruikers toe te wijzen en profiteer van uw bestaande App-V-toepassingen die worden gehost in Azure RemoteApp tooany apparaat overal geleverd.


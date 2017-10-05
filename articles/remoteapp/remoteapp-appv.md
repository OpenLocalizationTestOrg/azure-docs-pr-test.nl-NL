---
title: Met behulp van App-V-apps met Azure RemoteApp | Microsoft Docs
description: Informatie over het gebruik van App-V-apps in Azure RemoteApp.
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
ms.openlocfilehash: e55bb8db83c04025c46b383a9ebbef4399178116
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a>App-V-apps gebruiken in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

U kunt App-V-toepassingen gebruiken in een Azure RemoteApp hybride verzameling waarvoor domein is vereist.

Voordat u begint, zorg ervoor dat de App-V 5.1-client installeren met de meest recente updates. U moet maken een [aangepaste installatiekopie](remoteapp-create-custom-image.md) die de App-V-client bevat.  

Het is gemakkelijk het gebruik van uw bestaande App-V-infrastructuur met Azure RemoteApp. Aangezien een hybride verzameling wordt geïmplementeerd in een Azure VNET dat toegang tot uw domeincontroller heeft en de virtuele machines verbonden met het domein worden, kunt u gebruikmaken van uw bestaande App-v-infrastructuur- en implementatiemethodes easyily host App-V-toepassing in Azure RemoteApp. Hier volgen enkele overwegingen die u moet rekening houden met op basis van het type App-V-implementatie die u momenteel hebt:

| Configuratie-opties |  | Positief | Negatieve |
| --- | --- | --- | --- |
| Leveringsmethode |Streaming (op aanvraag) |App is altijd de meest recente en nieuwe |Eerste wachttijd |
| Gekoppeld |Snelste; App is al aanwezig op de virtuele machine |Gegevensophoping - inneemt installatiekopie ruimte (maximaal 127 GB) | |
| App-locatie-opslag |Gedeelde inhoud |App wordt uitgevoerd in het geheugen van Azure RemoteApp-exemplaar |Eats geheugen en goede verbinding met streaming (bestandsserver) waarin de app zich bevindt |
| Schijf (in cache) |Snel kan worden uitgevoerd. De App is niet afhankelijk van beschikbaarheid van de inhoudsbron |Gegevensophoping - inneemt installatiekopie ruimte (maximaal 127 GB) | |
| Doelen |Gebruiker |Volledige zelfstandige App-V-infrastructuur vereist | |
| Global (computer) |Vooraf publiceren of de publicatie met als doel server |Moet uw Azure-installatiekopie bijwerken als u wilt bijwerken van de app (grote). Neemt enige ruimte vrij op de installatiekopie. | |

 Nadat u uw aangepaste installatiekopie en uw hybride verzameling maakt, uw toepassing publiceren, gebruikers toe te wijzen en profiteer van uw bestaande App-V-toepassingen die worden gehost in Azure RemoteApp geleverd aan elk apparaat een willekeurige plaats.


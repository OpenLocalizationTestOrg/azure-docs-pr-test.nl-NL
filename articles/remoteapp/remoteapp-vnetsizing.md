---
title: Informatie voor een VNET in Azure RemoteApp | Microsoft Docs
description: Meer informatie over de vereisten voor IP-adressen voor Azure RemoteApp uitgevoerd met een VNET
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9375981db64ec4a1ae523e958423b5f5787cec33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a>Informatie voor een VNET in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Wanneer u Azure RemoteApp gebruiken met een virtueel netwerk (VNET), gebruikt RemoteApp IP-adressen binnen het subnet. Op basis van de schaal van uw RemoteApp-service, moet u ervoor zorgen dat uw subnet voldoende IP-adressen beschikbaar voor RemoteApp-virtuele machines. Terwijl deze richtlijn niet perfect gezien hoe RemoteApp dynamisch draait en draait op virtuele machines binnen een verzameling, kunt u uw subnetbereik schatten. Dit is vooral belangrijk als zodra een RemoteApp-service wordt geplaatst in een VNET, u kan niet groter subnet zonder RemoteApp worden verwijderd.

U hebt voor elke RemoteApp-verzameling die u wilt uitvoeren op de maximale capaciteit, 100 IP-adressen beschikbaar. Als u een RemoteApp-verzameling in de standaard-plan hebt en u wilt dat het maximumaantal 500 gebruikers, moet u bijvoorbeeld 100 IP-adressen voor deze verzameling hebt. Daarnaast moet u 100 IP-adressen voor een RemoteApp-collectie in het basis-plan met 800 gebruikers. Als u van plan bent om minder gebruikers (kleiner dan het maximum), kunt u de IP-adressen per verzameling nodig verkleinen. De vereiste minimale subnet is 30 IP-adressen (/ 27).

Het uitchecken van de volgende informatie om te controleren of uw VNET is geconfigureerd en werkt propertly:

* [Migreren van een persoonlijke VNET naar een Azure-VNET](remoteapp-migratevnet.md)
* [Valideren van het Azure VNET gebruiken met Azure RemoteApp](remoteapp-vnet.md)


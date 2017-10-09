---
title: aaaSizing-informatie voor een VNET in Azure RemoteApp | Microsoft Docs
description: Meer informatie over vereisten voor Hallo IP-adressen voor Azure RemoteApp uitgevoerd met een VNET
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
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a>Informatie voor een VNET in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Wanneer u Azure RemoteApp gebruiken met een virtueel netwerk (VNET), gebruikt RemoteApp IP-adressen binnen het Hallo-subnet. Op basis van Hallo schaal van uw RemoteApp-service, moet u tooensure dat uw subnet voldoende IP-adressen beschikbaar voor RemoteApp-virtuele machines heeft. Terwijl deze richtlijn niet perfect gezien hoe RemoteApp dynamisch draait en draait op virtuele machines binnen een verzameling, kunt u uw subnetbereik schatten. Dit is vooral belangrijk als zodra een RemoteApp-service wordt geplaatst in een VNET, u Hallo subnetgrootte kan niet vergroten zonder RemoteApp worden verwijderd.

U hebt voor elke RemoteApp-verzameling die u toorun op de maximale capaciteit wilt, 100 IP-adressen beschikbaar. Als er een RemoteApp-verzameling in hello standaard-plan en toohave Hallo maximaal 500 gebruikers gewenste, moet u bijvoorbeeld 100 IP-adressen voor deze verzameling hebt. Op dezelfde manier moet u 100 IP-adressen voor een RemoteApp-verzameling in hello basisniveau met 800 gebruikers. Als u van plan bent toohave minder gebruikers (minder dan de maximale Hallo), kunt u de benodigde per verzameling van Hallo IP-adressen beperken. vereiste minimale subnet Hallo is 30 IP-adressen (/ 27).

Bekijk Hallo informatie toomake of dat uw VNET is geconfigureerd volgens en propertly werken:

* [Migreren van een persoonlijke VNET tooan Azure VNET](remoteapp-migratevnet.md)
* [Hello Azure VNET toouse met Azure RemoteApp valideren](remoteapp-vnet.md)


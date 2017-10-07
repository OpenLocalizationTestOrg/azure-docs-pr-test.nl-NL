---
title: aaaAzure RemoteApp-licentieverlening | Microsoft Docs
description: Informatie over licentieverlening in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: ff8ebd20-61a1-4f10-87a6-234a170534c9
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dfa808a65ea6b1a78bf74f3daddb9a84e186eebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-licensing-work-in-azure-remoteapp"></a>Hoe werkt licentieverlening in Azure RemoteApp?
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Zodat u uw Azure RemoteApp-service, sjablonen gemaakt hebt ingesteld en zijn gereed toopublish apps tooyour gebruikers. Maar er is nog steeds een laatste ding toofigure uit:-licentieverlening. Alleen hoe werkt licentieverlening voor RemoteApp en Hallo-apps die u via RemoteApp deelt?

Voor RemoteApp zijn geen Windows-licenties of Extern bureaublad-licenties vereist. Uw abonnement zorgt voor Hallo RemoteApp side zelf. (Bekijk details op Hallo van Hallo [prijsstelling](https://azure.microsoft.com/pricing/details/remoteapp).)

Als u een van Hallo installatiekopieën die is opgenomen in uw abonnement, kunt u Hallo-Apps op die installatiekopie wordt geïnstalleerd zonder een aparte licentie delen. Als u uw verzameling Hallo Windows Server 2012 R2 sjabloon installatiekopie toobuild gebruikt, kunt u System Center Endpoint Protection delen met uw gebruikers. Hallo alleen uitzonderingen toothis regel zijn Office 365 ProPlus, waarvoor een apart abonnement is vereist, en Office 2013, dat in een productieverzameling kan niet worden gedeeld.

Als u wilt dat toouse Hallo Office 365-sjablooninstallatiekopie die wordt geleverd met RemoteApp, hebt u een *bestaande* Office 365 ProPlus-abonnement. Hallo geldt ook voor elke Office 365-app te publiceren met een aangepaste sjabloon. U moet tooactivate Hallo apps met uw eigen abonnement. Dit geldt voor proefabonnementen en betaalde abonnementen. Als u wilt dat toouse Hallo Office 365-sjablooninstallatiekopie tijdens het Hallo-proefversie *en u hebt al een abonnement*, toohello Office 365-pagina te gaan[aanmelden](https://go.microsoft.com/fwlink/p/?LinkID=403802) voor een proefabonnement. Zie [How do RemoteApp and Office work together?](remoteapp-o365.md) (Hoe werken RemoteApp en Office samen?) voor meer informatie.

Als u niet tijdens de evaluatieperiode van Hallo tooget een Office 365-proefabonnement wilt, gebruikt u Hallo Office 2013 Professional Plus-sjablooninstallatiekopie die wordt geleverd met RemoteApp. Deze installatiekopie kan slechts 30 dagen worden gebruikt en kan niet worden omgezet naar een betaalde verzameling.

Voor andere apps moet u ervoor dat er Hallo licentie tooshare Hallo app toomake.

Dat klinkt logisch, toch? U kunt elke app die u hebt tooshare wettelijk recht publiceren. En moet u ervoor dat u echt toomake tooshare het gebruiksrecht heeft uw programma's.

Houd er rekening mee dat u geen CAL of volumelicentieovereenkomst kunt gebruiken in een cloudverzameling. U *kunt* een Volume License agreement tooactivate toepassingen in uw hybride verzameling (met uitzondering van Office) gebruiken. U hoeft alleen maar tooinstall ze in de sjabloon een installatiekopie van Hallo Volume License-media. Volg Hallo-informatie van Hallo toepassing leverancier tooinstall licenties in een omgeving met extern bureaublad.


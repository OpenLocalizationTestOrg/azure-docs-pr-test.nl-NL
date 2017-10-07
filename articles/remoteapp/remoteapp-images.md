---
title: "Er is een aaaWhat in hello Azure RemoteApp-sjablooninstallatiekopieën? | Microsoft Docs"
description: "Meer informatie over Hallo sjablooninstallatiekopieën opgenomen met Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a>Wat is er in hello Azure RemoteApp-sjablooninstallatiekopieën?
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Uw abonnement op Azure RemoteApp omvat drie sjablooninstallatiekopieën:

* Windows Server 2012
* Microsoft Office 365 ProPlus (abonnement op Office 365 vereist)
* Microsoft Office 2013 Professional Plus (alleen proefversie)

> [!IMPORTANT]
> Uw abonnement op Azure RemoteApp, verleent dat u toegang tot toohello software in het Hallo-installatiekopieën, met uitzondering van Office 365 ProPlus, waarvoor een apart abonnement is vereist, en Office 2013, kan niet worden gebruikt in productie Hallo. Dit betekent dat u Hallo programma's of toepassingen op Hallo sjablooninstallatiekopieën met uw gebruikers kunt delen. Als u een verzameling die gebruikmaakt van Windows Server 2012 R2-afbeelding Hallo maakt, kunt u System Center Endpoint Protection publiceren voor gebruikers tooaccess via RemoteApp.
> 
> Bekijk Hallo [RemoteApp licentiegegevens](remoteapp-licensing.md) voor meer informatie. En [Office gebruiken met Azure RemoteApp](remoteapp-o365.md) voor Hallo Office licentieverlening info.
> 
> 

Lees verder voor meer informatie over de inhoud van elke installatiekopie.

## <a name="windows-server-2012-r2--hello-vanilla-image"></a>Windows Server 2012 R2 ('hello vanilla-installatiekopie')
Deze installatiekopie is gebaseerd op het besturingssysteem Microsoft Windows Server 2012 R2 Datacenter en heeft hello volgende functies en onderdelen geïnstalleerd toomeet Hallo vereisten voor Azure RemoteApp-sjablooninstallatiekopieën:

* .NET Framework 4.5, 3.5.1, 3.5
* Bureaubladbelevenis
* Inkt- en handschriftservices
* Media Foundation
* Extern bureaublad-sessiehost
* Windows PowerShell 4.0
* Windows PowerShell ISE
* WoW64-ondersteuning

Deze installatiekopie heeft ook Hallo na toepassingen zijn geïnstalleerd:

* Adobe Flash Player
* Microsoft Silverlight
* Microsoft System Center 2012 Endpoint Protection
* Microsoft Windows Media Player

## <a name="microsoft-office-365-proplus-subscription-required"></a>Microsoft Office 365 ProPlus (abonnement vereist)
Office 365 is meest aangevraagde toepassing hello, zodat we toowork met een 'aangepaste' installatiekopie voor u gemaakt.

Deze installatiekopie is een uitbreiding van Hallo vanilla-installatiekopie en heeft hello volgende onderdelen van Microsoft Office 365 ProPlus geïnstalleerd bovendien toohello onderdelen in Windows Server 2012 R2-afbeelding Hallo beschreven:

* Toegang
* Excel
* Lync
* OneNote
* OneDrive voor bedrijven (Let erop dat Hallo sync-agent wordt niet ondersteund voor gebruik met Azure RemoteApp)
* Outlook
* PowerPoint
* Word
* Microsoft Office-taalprogramma's

Hallo installatiekopie bevat ook Visio Pro en Project Pro.

En Hallo toepassingen, evenals de volgende:

* SQL Native Client
* ODBC-stuurprogramma
* SQL Server Data Mining Client
* MasterDataServices Client
* Microsoft Publisher
* PowerQuery
* PowerMap

Volledige functionaliteit van Office 365 ProPlus-apps is alleen beschikbaar voor gebruikers met een Office 365 ProPlus-abonnement. Zie voor meer informatie over Hallo Office 365-abonnement plannen [service-abonnementen voor Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx). Nog vragen? Bekijk Hallo [Office 365 + RemoteApp](remoteapp-o365.md) informatie. Lees ook nieuwe artikel Hallo [hoe toouse uw Office 365-abonnement met Azure RemoteApp](remoteapp-officesubscription.md).

U moet toolicense Office 365 ProPlus Visio Pro en Project Pro afzonderlijk - ze elk hun eigen licentie hebben.

## <a name="microsoft-office-2013-professional-plus-trial-only"></a>Microsoft Office 2013 Professional Plus (alleen proefversie)
Tijdens het Hallo gratis proefperiode, kunt u Hallo-service met de installatiekopie van het Hallo Office 2013 testen.

Deze installatiekopie is een uitbreiding van Hallo vanilla-installatiekopie en heeft hello volgende onderdelen van Microsoft Office 2013 Professional Plus geïnstalleerd bovendien toohello onderdelen in Windows Server 2012 R2-afbeelding Hallo beschreven:

* Toegang
* Excel
* Lync
* OneNote
* OneDrive voor bedrijven (Let erop dat Hallo sync-agent wordt niet ondersteund voor gebruik met Azure RemoteApp)
* Outlook
* PowerPoint
* Project
* Visio
* Word
* Microsoft Office-taalprogramma's

> [!IMPORTANT]
> **Juridische informatie:** Deze installatiekopie bevat geen licentie voor Microsoft Office en *kan niet worden gebruikt voor productie*. Hallo Office 2013 Professional Plus-installatiekopie is bedoeld proefabonnement alleen voor gebruik. Als u wilt dat toouse Office-apps in Azure RemoteApp voor productie, moet u toouse Hallo Office 365 ProPlus-installatiekopie. Zie [Office 365 gebruiken met Azure RemoteApp](remoteapp-o365.md) voor meer informatie over licentieverlening voor Office.
> 
> 


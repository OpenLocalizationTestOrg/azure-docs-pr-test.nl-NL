---
title: aaaPublish een app in Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe toopublish toepassingen en bronnen in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a>Hoe toopublish een app in RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Nadat u uw RemoteApp-collectie maken, moet u toopublish Hallo apps of resources wilt u toomake beschikbaar voor uw gebruikers. Hallo sjablooninstallatiekopieën voorzien van uw abonnement alleen enkele apps hebben standaard - uitgegeven tooshare Hallo andere apps, moet u toopublish ze.

> [!NOTE]
> Moet u een app tooupdate? U moet te[update Hallo installatiekopie](remoteapp-update.md) eerste.
> 
> 

Op Hallo **Publishing** in Hallo-portal en klik op **publiceren**. Kunt u een app toevoegen van uw sjablooninstallatiekopie **Start** menu of geef Hallo pad toowhere Hallo app op Hallo-sjablooninstallatiekopie is geïnstalleerd. Als u tooadd uit Hallo **Start** menu Hallo app toopublish in Hallo lijst kiezen. Als u tooprovide Hallo pad toohello app kiest, voer een naam voor het Hallo-app en Hallo pad toohello app. Variabelen in Hallo pad - bijvoorbeeld '% systemdrive %' gebruiken in plaats van ' c:\".

> [!NOTE]
> Als u uw app uit Hallo tooadd wilt **Start** menu, moet u toohave *toegevoegd die app-toohello **Start** menu op uw sjablooninstallatiekopie.* Anders RemoteApp alleen zien wat *is* op Hallo **Start** menu en u wordt verwarren. 
> 
> toomake ervoor dat uw app wordt in Hallo **Start** menu, plaatst u het snelkoppelingsbestand - **lnk** - Hallo %systemdrive%\ProgramData\Microsoft\Windows\Start Start\Programma 's map.
> 
> Als u bent tooadd Hallo app toohello vergeten **Start** menu tijdens het maken van Hallo-sjabloon, kies tooadd Hallo pad toohello app. (Of maak deze opnieuw uw sjablooninstallatiekopie, maar dat is erg iets meer werk.)
> 
> 


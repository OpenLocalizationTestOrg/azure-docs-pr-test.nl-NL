---
title: Een app publiceren in Azure RemoteApp | Microsoft Docs
description: Informatie over het publiceren van toepassingen en bronnen in Azure RemoteApp.
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
ms.openlocfilehash: 4565fa498dbadd0601004c73bfee5171efe1fad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-publish-an-app-in-remoteapp"></a>Hoe u een app publiceren in RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Nadat u uw RemoteApp-collectie gemaakt, moet u de apps of de resources die u beschikbaar wilt maken voor uw gebruikers publiceren. De sjablooninstallatiekopieën met uw abonnement opgegeven slechts enkele apps die zijn gepubliceerd - standaard voor het delen van andere apps hebben, moet u ze publiceren.

> [!NOTE]
> Moet u een app bijwerken? U moet [bijwerken van de installatiekopie](remoteapp-update.md) eerste.
> 
> 

Op de **Publishing** in de portal en klik op **publiceren**. Kunt u een app toevoegen van uw sjablooninstallatiekopie **Start** menu of geef het pad naar waar de app is geïnstalleerd op de sjablooninstallatiekopie. Als u wilt toevoegen op basis van de **Start** menu, kies de app te publiceren in de lijst. Als u ervoor kiest om het pad naar de app, voert u een naam voor de app en het pad naar de app. Variabelen in het pad - bijvoorbeeld '% systemdrive %' gebruiken in plaats van ' c:\".

> [!NOTE]
> Als u wilt toevoegen van uw app uit de **Start** menu, moet u beschikken over *die app toevoegt aan de **Start** menu op uw sjablooninstallatiekopie.* Anders RemoteApp alleen zien wat *is* op de **Start** menu en u wordt verwarren. 
> 
> Om te controleren of uw app wordt de **Start** menu, plaatst u het snelkoppelingsbestand - **lnk** - binnen de Menu\Programs %systemdrive%\ProgramData\Microsoft\Windows\Start.
> 
> Als u vergeten toe te voegen van de app kan de **Start** menu tijdens het maken van de sjabloon kiest u het pad toevoegen aan de app. (Of maak deze opnieuw uw sjablooninstallatiekopie, maar dat is erg iets meer werk.)
> 
> 


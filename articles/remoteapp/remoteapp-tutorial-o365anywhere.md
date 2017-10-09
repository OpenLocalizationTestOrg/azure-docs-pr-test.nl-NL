---
title: aaaGet Hallo dezelfde Office 365-ervaring op elk apparaat met Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe tooshare elke Office 365-app met uw gebruikers met behulp van Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a>Get Hallo dezelfde Office 365-ervaring op elk apparaat met Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Dit artikel wordt uitgelegd hoe toodeploy Office 365 op elk apparaat in uw bedrijf. Uw gebruikers toegang krijgen Hallo dezelfde mogelijkheden en gebruikersinterface ervaring voor Android, Apple en Windows.

We kunnen dit met Azure RemoteApp bewerkstelligen door Office 365 te hosten op schaalbare virtuele machines in Azure, waarmee gebruikers verbinding kunnen maken. Deze set van virtuele machines noemen we een 'cloudverzameling'.

## <a name="create-a-cloud-collection"></a>Een cloudverzameling maken
Eerst nadat u een Azure-account hebt gemaakt, gaat u te**RemoteApp** door te klikken op Hallo-koppeling op Hallo linkerkant.
![Azure RemoteApp wordt weergegeven op Hallo Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)

Ga verder door te klikken op **nieuwe** op Hallo onder en 'snel maken' een verzameling. Geef een naam, Hallo regio, Hallo abonnement, Hallo-plan en Hallo installatiekopie 'Office Proffesional 2013' die wij verstrekken.
![Dialoogvenster Maken](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)

Hallo formulier Hallo verzameling maken van het proces moet worden gestart wanneer u klaar bent. Dit kan tooan uur duren.

![Wachten](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

Zodra het Hallo-proces is voltooid, er ongeveer als volgt. Als u op **Publiceren** klikt, ziet u dat de meeste Office-toepassingen al zijn gepubliceerd.
![Verzameling gemaakt](./media/remoteapp-tutorial-o365anywhere/4-done.png)

![Gepubliceerde apps](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

Op dit moment kunt u ook meer gebruikers die toegang toothis verzameling hebben door te klikken op toevoegen **gebruikerstoegang**.
![Gebruikerstoegang configureren](./media/remoteapp-tutorial-o365anywhere/6-user.png)

Nu gaan we proberen verbinding te maken tooOffice 365!

## <a name="connect-toooffice-365"></a>Verbinding maken met tooOffice 365
We je head via te[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), schuif naar beneden en klik op **clients downloaden** tooinstall hello Azure RemoteApp-client op Hallo apparaat. Hallo onderstaande schermafbeeldingen zijn voor Windows.

Zodra de toepassing hello Start wordt u gevraagd toosign met uw Microsoft-account (voorheen een 'Live-ID'), gebruik Hallo dezelfde die uw Azure-account nu. Wanneer u bent aangemeld, ziet u een melding over nieuwe uitnodigingen. Klik op de melding, waarna een lijst zoals hieronder wordt weergegeven. Hallo-uitnodiging die overeenkomt met uw e-mailadres Azure-account eigenaar accepteren.

![Nieuwe uitnodiging](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

Zo ziet het eruit wanneer er nieuwe uitnodigingen zijn.

![Een toepassing accepteren](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

U ziet alle Hallo Office-apps in Azure RemoteApp-client Hallo zodra u Hallo uitnodiging accepteren.

![Lijst met apps](./media/remoteapp-tutorial-o365anywhere/9-work.png)

Wanneer u klikt op een van deze toepassing hello moeten worden gestart op Hallo virtuele machine van Azure en u moet alle! Veel plezier!

![starten](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![PowerPoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)


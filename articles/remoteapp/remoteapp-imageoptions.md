---
title: aaaCreate een installatiekopie van een Azure RemoteApp | Microsoft Docs
description: "Meer informatie over het Hallo-opties die beschikbaar zijn voor het maken van installatiekopieën voor Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a>Create an Azure RemoteApp image (Een installatiekopie maken voor Azure RemoteApp)
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Azure RemoteApp maakt gebruik van installatiekopieën toohold Hallo apps die u met uw gebruikers deelt. (We nemen uw installatiekopie en virtuele machines toocreate - die het Hallo-gebruikers toegang wanneer ze zich aanmelden bij Azure RemoteApp.) toocreate een Azure RemoteApp-verzameling met uw keuze van toepassingen, of de cloud of hybride, begint u met een installatiekopie maken met deze toepassingen zijn geïnstalleerd. Vervolgens maakt u een verzameling die gebruikmaakt van de installatiekopie, gebruikers toohello verzameling toewijzen en publiceren van apps toothose gebruikers.

U hebt verschillende mogelijkheden voor het maken of met behulp van afbeeldingen. Hallo basic [vereiste](remoteapp-imagereqs.md) voor een installatiekopie is dat het uitvoeren van Windows Server 2012 R2 en Hallo Remote Desktop Session Host (RDSH)-rol is geïnstalleerd. Hoe u krijgt dat is waar dingen interessante krijgen.

Hebt u volgende opties wanneer deze wordt gezet tooimages Hallo:

* U kunt importeren en gebruiken een [installatiekopie op basis van een virtuele machine van Azure](remoteapp-image-on-azurevm.md). Dit is geschikt voor line-of-business-apps waarvoor u aangepaste instellingen. U kunt Hallo installatiekopie toowork voor Hallo app aanpassen.
* U kunt [maken en een aangepaste installatiekopie uploaden](remoteapp-create-custom-image.md). Dit is geschikt als er al een afbeelding die u voor uw on-premises-implementatie voor extern bureaublad-Services gebruiken.
* U kunt een van de Hallo [sjablooninstallatiekopieën](remoteapp-images.md) opgenomen in uw RemoteApp-abonnement. Deze installatiekopieën worden gemaakt en onderhouden door Hallo RemoteApp-team en sommige standaard toepassingen (zoals Hallo Office suite) dat kunt u gebruikers van de beschikbare tooyour bevatten. Houd er rekening mee dat alleen Hallo Office 365 Pro Plus-installatiekopie kan worden gebruikt in een productieomgeving.

Ongeacht waar het verkrijgen van uw installatiekopie of hoe u dit hebt gemaakt, moet u zeker dat u begrijpt Hallo toomake [appvereisten](remoteapp-appreqs.md) tooensure die uw app goed in RemoteApp werkt. Vervolgens de volgende stap Hallo toocreate is een [cloud](remoteapp-create-cloud-deployment.md) of [hybride](remoteapp-create-hybrid-deployment.md) verzameling.


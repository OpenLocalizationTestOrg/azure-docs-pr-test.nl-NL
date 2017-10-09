---
title: aanbevolen procedures voor aaaAzure RemoteApp | Microsoft Docs
description: Aanbevolen procedures voor het configureren en gebruiken van Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b851865b-bec4-4f29-82c0-7b9770c1a520
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f4d09ef30816eaebb74b69f26f3242c69ea27591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a>Aanbevolen procedures voor het configureren en gebruiken van Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) voor meer informatie.
> 
> 

Hallo volgende informatie kunt u configureren en gebruiken van Azure RemoteApp productief zijn.

## <a name="connectivity"></a>Connectiviteit
* Gebruik altijd de meest recente clientversie Hallo. Met behulp van de oudere clients, kan dit leiden tot problemen met de netwerkverbinding en andere verslechterde ervaringen. Inschakelen van automatische toepassing van updates voor uw apparaat zorgt ervoor dat de meest recente client Hallo altijd is geïnstalleerd.
* Gebruik altijd Hallo stabiel en meest betrouwbare internet verbinding beschikbaar tooyou.  
* Proxyverbinding ondersteund gebruik alleen voor optimale connectiviteit met hoge prestaties.  Hallo SOCKS-proxy wordt niet ondersteund.

## <a name="applications"></a>Toepassingen
* Opslaan en sluiten van RemoteApp-toepassingen wanneer u klaar bent met de toepassing hello. Niet sluiten Hallo toepassing kan leiden tot verlies van gegevens.
* Valideren van aangepaste toepassingen voordat u ze in Azure RemoteApp. Dit omvat zodat ze werken op een platform meerdere sessie en onnodige resources, zoals geheugen en CPU die mogelijk een andere gebruiker op Hallo stilleggen niet gebruiken dezelfde verzameling. Voor meer informatie, downloaden en bekijken Hallo [toepassing compatibiliteit met aanbevolen procedures voor extern bureaublad-Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).

## <a name="configuration-and-management"></a>Configuratie en beheer
* Houd uw sjablooninstallatiekopieën up toodate, software-updates en andere kritieke updates installeren, indien nodig. Dit zorgt ervoor dat als Azure RemoteApp auto-schalen toomeet uw capaciteit, elk exemplaar is hersteld.  
* Zorg ervoor dat uw implementatie van Active Directory Federation Services (AD FS) is veilig en betrouwbaar. Anders mislukken client verificaties, voorkomen dat gebruikers toegang tot Azure RemoteApp.
* Configureer sjablooninstallatiekopieën met geïnstalleerde toepassingen, functies of onderdelen zodanig in dat ze staatloze. Ze moeten niet afhankelijk van alle exemplaren van Hallo virtuele machines in een RemoteApp-service wordt in een permanente status.
  * Alle gebruikersgegevens opslaan in gebruikersprofielen of andere locaties externe toohello opslagservice, zoals lokale bestand shares of OneDrive.
  * Gedeelde gegevens opslaan in opslagservice locaties externe toohello, zoals lokale bestand shares of OneDrive.
  * Configureer alle systeeminstellingen in Hallo-sjablooninstallatiekopie in plaats van op afzonderlijke virtuele machines in een service.
  * Schakel automatische software-updates voor gepubliceerde toepassingen - in plaats daarvan deze handmatig toepassen toohello sjablooninstallatiekopie en te testen voordat u met Hallo-sjabloon implementeert.


---
title: Aanbevolen procedures voor Azure RemoteApp | Microsoft Docs
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
ms.openlocfilehash: ab9c2dafc622e9b6f3bcd2767218cdc03e844847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a>Aanbevolen procedures voor het configureren en gebruiken van Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) voor meer informatie.
> 
> 

De volgende informatie kunt u configureren en gebruiken van Azure RemoteApp productief zijn.

## <a name="connectivity"></a>Connectiviteit
* Gebruik altijd de meest recente clientversie. Met behulp van de oudere clients, kan dit leiden tot problemen met de netwerkverbinding en andere verslechterde ervaringen. Inschakelen van automatische toepassing van updates voor uw apparaat zorgt ervoor dat er altijd de nieuwste client is geïnstalleerd.
* Gebruik altijd de meest stabiel en betrouwbaar internetverbinding beschikbaar voor u.  
* Proxyverbinding ondersteund gebruik alleen voor optimale connectiviteit met hoge prestaties.  De SOCKS-proxy wordt niet ondersteund.

## <a name="applications"></a>Toepassingen
* Opslaan en sluiten van RemoteApp-toepassingen wanneer u klaar bent met de toepassing. De toepassing niet sluiten, kan dit leiden tot verlies van gegevens.
* Valideren van aangepaste toepassingen voordat u ze in Azure RemoteApp. Dit omvat zodat ze werken op een platform meerdere sessie en onnodige resources, zoals geheugen en CPU die mogelijk een andere gebruiker in dezelfde verzameling stilleggen niet gebruiken. Download voor informatie en bekijk de [toepassing compatibiliteit met aanbevolen procedures voor extern bureaublad-Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).

## <a name="configuration-and-management"></a>Configuratie en beheer
* Uw sjablooninstallatiekopieën up-to-date te houden, software-updates en andere kritieke updates installeren, indien nodig. Dit zorgt ervoor dat als Azure RemoteApp auto-schalen om te voldoen aan de capaciteit, elk exemplaar is een patch uitgevoerd.  
* Zorg ervoor dat uw implementatie van Active Directory Federation Services (AD FS) is veilig en betrouwbaar. Anders mislukken client verificaties, voorkomen dat gebruikers toegang tot Azure RemoteApp.
* Configureer sjablooninstallatiekopieën met geïnstalleerde toepassingen, functies of onderdelen zodanig in dat ze staatloze. Ze moeten niet afhankelijk van alle exemplaren van de virtuele machines in een RemoteApp-service wordt in een permanente status.
  * Alle gebruikersgegevens opslaan in gebruikersprofielen of andere aan de service, externe opslaglocaties, zoals lokale bestand shares of OneDrive.
  * Gedeelde gegevens opslaan in opslaglocaties buiten de service, zoals lokale bestand shares of OneDrive.
  * Alle systeeminstellingen configureren in de sjablooninstallatiekopie in plaats van op afzonderlijke virtuele machines in een service.
  * Schakel automatische software-updates voor gepubliceerde toepassingen - in plaats daarvan handmatig toepassen op de sjablooninstallatiekopie van de en te testen voordat u uit de sjabloon implementeert.


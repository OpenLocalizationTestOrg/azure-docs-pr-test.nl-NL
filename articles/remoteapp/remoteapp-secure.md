---
title: Beveiligde apps en resources in Azure RemoteApp | Microsoft Docs
description: Meer informatie over het vergrendelen van apps en resources in Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7fbade87-a453-426d-bfa5-c72227ea83cd
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 1c052906788f0f4fe4ca9fd6d3af63336245174a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a>Beveiligde apps en resources in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Azure RemoteApp biedt gebruikers de toegang tot centraal beheerde Windows-apps, kunt u bepalen wat uw gebruikers wel en niet mogelijk.  Dit is vooral handig wanneer de gebruiker verbinding vanaf een onbeheerd apparaat (zoals hun persoonlijke Macbook maakt) en u wilt de toegang van gebruikers of optreden.

Bijvoorbeeld, als u van Active Directory voor gebruikersverificatie gebruikmaakt en u wilt voorkomen dat uw gebruikers kopiëren van gegevens uit een app, kunt u een extern bureaublad-Groepsbeleid voorkomen dat gebruikers van het kopiëren van gegevens.

Een ander voorbeeld is als u wilt blokkeren van toegang tot internet voor een bepaalde app in uw verzameling. U kunt een Windows Firewall-regel waarmee de toegang wordt geblokkeerd wanneer u de installatiekopie voor uw verzameling maken kunt maken.

## <a name="implementation-options"></a>Implementatie-opties
  Hier volgen de belangrijkste implementatieopties, kunnen afzonderlijk of in combinatie naar behoefte worden gebruikt:

1. Als uw RemoteApp-collectie verbonden met het domein is kunt u een afdwingen [groepsbeleid](https://technet.microsoft.com/library/cc725828.aspx) (met uitzondering van de niet-actief en verbinding verbreken time-out beleidsregels beschreven [hier](../azure-subscription-service-limits.md)).
2. Als alternatief voor Groepsbeleid (als uw verzameling niet verbonden met het domein is of u niet de juiste bevoegdheden in AD hebt), kunt u configureren [lokaal beleid](https://technet.microsoft.com/library/cc775702.aspx) in uw sjablooninstallatiekopie.  Houd er rekening mee dat Groepsbeleid troef lokaal beleid als er een conflict optreedt.
3. Sommige OS/app-instellingen zijn niet configureerbaar ingestelde beleid, maar kan via het register sleutel met behulp van de [hulpprogramma RegEdit](remoteapp-hybridtrouble.md) tijdens het configureren van de installatiekopie van uw sjabloon.
4. U kunt [Windows Firewall](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) netwerk om toegang te controleren en naar de computer waarop de app wordt uitgevoerd. Zorg ervoor dat u de URL's en poorten die hier zijn gedefinieerd niet blokkeren.
5. U kunt [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) om te bepalen welke toepassingen en bestanden gebruikers kunnen uitvoeren. Ervaren gebruikers kunnen bijvoorbeeld nagaan wat het uitvoeren van toepassingen die u niet heeft gepubliceerd maar die beschikbaar in de installatiekopie die u gebruikt zijn voor het maken van de verzameling - AppLocker kan dit blokkeren.

## <a name="detailed-information"></a>Gedetailleerde informatie
* De volgende RDS-beleidsregels zijn waarschijnlijk het meest geschikt:
  * [Apparaten en bronnen](https://technet.microsoft.com/library/ee791794.aspx)
  * [Printeromleiding](https://technet.microsoft.com/library/ee791784.aspx)
  * [Profielen](https://technet.microsoft.com/library/ee791865.aspx).
* Houd er rekening mee dat configureren omleidingen via de RemoteApp-PowerShell-module (zoals [hier](remoteapp-redirection.md)) is afhankelijk van de client-computer aan het beleid afdwingen, zodat als beveiliging het primaire doel is moet u het beleid via de sjablooninstallatiekopie afdwingen lokaal beleid of via Groepsbeleid.
* [Beleidsregels voor Windows Server 2012 R2](https://technet.microsoft.com/library/hh831791.aspx).
* [Office 2013 beleidsregels](https://technet.microsoft.com/library/cc178969.aspx) (inclusief [het aanpassen van de Office-werkbalk](https://technet.microsoft.com/library/cc179143.aspx)).


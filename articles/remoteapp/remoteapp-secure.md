---
title: aaaSecure apps en resources in Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe toolock omlaag apps en resources in Azure RemoteApp
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
ms.openlocfilehash: 26325826e92855a12a0087f19a3e32cbe1116449
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a>Beveiligde apps en resources in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Azure RemoteApp biedt gebruikers toegang toocentrally beheerde Windows-apps, waarmee u uw gebruikers kunnen en kunnen niet worden beheerd.  Dit is vooral handig wanneer Hallo gebruiker verbinding maakt vanaf een niet-beheerde apparaten (zoals hun persoonlijke Macbook) en u wilt toocontrol Hallo gebruikerstoegang of optreden.

Als u van Active Directory voor gebruikersverificatie gebruikmaakt en u wilt dat tooprevent gebruikers van het kopiëren van gegevens uit een app, kunt u bijvoorbeeld een groepsbeleid voor extern bureaublad tooblock gebruikers van het kopiëren van gegevens configureren.

Een ander voorbeeld is als u wilt dat toegang tot internet voor een bepaalde app tooblock in uw verzameling. U kunt een Windows Firewall-regel dat blokken toegang Hallo wanneer u Hallo installatiekopie voor uw verzameling maken kunt maken.

## <a name="implementation-options"></a>Implementatie-opties
  Hier volgen Hallo sleutel implementatie-opties, die kunnen worden gebruikt afzonderlijk of in combinatie zo nodig:

1. Als uw RemoteApp-collectie verbonden met het domein is kunt u een afdwingen [groepsbeleid](https://technet.microsoft.com/library/cc725828.aspx) (met uitzondering van Hallo inactief en verbinding verbreken time-out beleidsregels die worden beschreven Hallo [hier](../azure-subscription-service-limits.md)).
2. Als een alternatieve tooGroup beleid (indien uw verzameling niet verbonden met het domein is of u niet de juiste bevoegdheden Hallo in AD hebt), kunt u configureren [lokaal beleid](https://technet.microsoft.com/library/cc775702.aspx) in uw sjablooninstallatiekopie.  Houd er rekening mee dat Groepsbeleid troef lokaal beleid als er een conflict optreedt.
3. Sommige OS/app-instellingen zijn niet configureerbaar ingestelde beleid, maar kan via de registersleutel met de Hallo [hulpprogramma RegEdit](remoteapp-hybridtrouble.md) tijdens het configureren van de installatiekopie van uw sjabloon.
4. U kunt [Windows Firewall](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) toocontrol netwerk toegang tooand van Hallo-machine waarop Hallo-app wordt uitgevoerd. Zorg ervoor dat u niet blokkeren Hallo URL's en poorten die hier zijn gedefinieerd.
5. U kunt [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) toocontrol die toepassingen en bestanden gebruikers kunnen uitvoeren. Bijvoorbeeld: ervaren gebruikers kunnen achterhalen hoe toorun toepassingen die u niet heeft gepubliceerd, maar die beschikbaar zijn in Hallo u hebt gebruikt toocreate Hallo verzameling image - AppLocker kan dit blokkeren.

## <a name="detailed-information"></a>Gedetailleerde informatie
* Hallo volgende RDS beleidsregels zijn waarschijnlijk toobe vooral handig:
  * [Apparaten en bronnen](https://technet.microsoft.com/library/ee791794.aspx)
  * [Printeromleiding](https://technet.microsoft.com/library/ee791784.aspx)
  * [Profielen](https://technet.microsoft.com/library/ee791865.aspx).
* Opmerking dat configureren omleidingen via RemoteApp-PowerShell-module Hallo (zoals [hier](remoteapp-redirection.md)) is afhankelijk van Hallo machine tooenforce Hallo clientbeleid, dus als beveiliging het hoofddoel Hallo is moet u tooenforce Hallo beleid via Hallo sjabloon installatiekopie lokaal beleid of via Groepsbeleid.
* [Beleidsregels voor Windows Server 2012 R2](https://technet.microsoft.com/library/hh831791.aspx).
* [Office 2013 beleidsregels](https://technet.microsoft.com/library/cc178969.aspx) (inclusief [hoe toocustomize Office-werkbalk Hallo](https://technet.microsoft.com/library/cc179143.aspx)).


---
title: aaaTroubleshooting hello automatische registratie van Azure AD-domein voor Windows downlevel-clients computers die lid zijn | Microsoft Docs
description: Het oplossen van problemen Hallo automatische registratie van Azure AD-domein lid zijn van computers voor Windows downlevel-clients.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a>Automatische registratie van domein het oplossen van problemen die lid zijn van computers tooAzure AD voor Windows downlevel-clients 

In dit onderwerp is van toepassing alleen toohello volgende clients: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Zie voor Windows 10 of Windows Server 2016 [automatische registratie van domein het oplossen van problemen die lid zijn van computers tooAzure AD – Windows 10 en Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).

Dit onderwerp wordt ervan uitgegaan dat u hebt geconfigureerd automatische registratie van apparaten domein vermelde in dat wordt beschreven in [hoe tooconfigure automatische registratie van Windows-domein apparaten met Azure Active Directory](active-directory-device-registration-get-started.md).
 
Dit onderwerp vindt u informatie over hoe tooresolve mogelijke problemen op te lossen.  
Een aantal dingen toonote voor geslaagde resultaten: 

- Registratie van deze clients over Azure AD is per gebruiker/apparaat. Als een voorbeeld: als jdoe en jharnett wilt toothis apparaat aanmelden, de registratie van een afzonderlijke (apparaat-id) voor elk van deze gebruikers in het tabblad info van Hallo gebruiker is gemaakt.  

- De registratie van deze clients out of box Hallo geconfigureerde tootry bij het aanmelden of vergrendelen/ontgrendelen is en kan er 5 minuten vertraging dat dit met behulp van een Task Scheduler-taak wordt geactiveerd. 

- Een opnieuw installeren van het besturingssysteem hello of een handmatige opheffen van de registratie en opnieuw te registreren, kan een nieuwe registratie maakt op Azure AD en resulteert in meerdere vermeldingen Hallo gebruiker info tabblad in hello Azure-portal. 


## <a name="step-1-retrieve-hello-registration-status"></a>Stap 1: De registratiestatus Hallo ophalen 

**tooverify hello registratiestatus:**  

1. Open Hallo opdrachtprompt als beheerder 

2. Type`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

Met deze opdracht geeft een dialoogvenster waarmee u meer informatie over de status van Hallo join.

![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a>Stap 2: De registratiestatus Hallo 

Als Hallo join niet geslaagd is, biedt Hallo dialoogvenster u meer informatie over Hallo probleem dat is opgetreden.

**Hallo meest voorkomende problemen zijn:**

- Een onjuist geconfigureerde AD FS of Azure AD

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- U bent niet aangemeld op als een domeingebruiker

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- Een quotum is bereikt

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- Hallo-service reageert niet 

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

U kunt ook Hallo statusinformatie vinden in het gebeurtenislogboek Hallo onder **toepassingen en Services Log\Microsoft-Workplace Join**.
  
**Hallo meest voorkomende oorzaken van een mislukte inschrijving zijn:** 

- Uw computer is niet op het interne netwerk van de organisatie van de hello of een VPN zonder verbinding tooan lokale AD-domeincontroller.

- U bent aangemeld op de computer tooyour met een lokaal computeraccount. 

- Problemen met de configuratie van service: 

  - Hallo federation-server is geconfigureerd toosupport **WIAORMULTIAUTHN**. 

  - Er is geen Service Connection Point-object dat tooyour geverifieerde domeinnaam op beheerpunten in Azure AD in Hallo AD-forest waar Hallo computer behoort.

  - Een gebruiker de Hallo heeft bereikt van apparaten. Zie aan de slag met Azure Active Directory-apparaatregistratie.

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie, Hallo [automatische apparaatregistratie Veelgestelde vragen](active-directory-device-registration-faq.md) 

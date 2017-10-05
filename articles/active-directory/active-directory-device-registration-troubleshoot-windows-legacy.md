---
title: Het oplossen van de automatische registratie van Azure AD-domein aangesloten computers voor downlevel-clients voor Windows | Microsoft Docs
description: Het oplossen van de automatische registratie van Azure AD-domein lid zijn van computers voor Windows downlevel-clients.
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
ms.openlocfilehash: a7c8ef4c59c53c21258f0c61963d8f994a3946ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad-for-windows-down-level-clients"></a>Het oplossen van automatische registratie van domein computers toegevoegd aan Azure AD. voor Windows downlevel-clients 

In dit onderwerp is alleen van toepassing op de volgende clients: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Zie voor Windows 10 of Windows Server 2016 [computers probleemoplossing automatische registratie van domein worden toegevoegd aan Azure AD. – Windows 10 en Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).

Dit onderwerp wordt ervan uitgegaan dat u hebt geconfigureerd automatische registratie van apparaten domein vermelde in dat wordt beschreven in [automatische registratie van Windows-domein-apparaten met Azure Active Directory configureren](active-directory-device-registration-get-started.md).
 
Dit onderwerp vindt u richtlijnen over het oplossen van problemen op te lossen.  
Een aantal zaken om aan te geven voor geslaagde resultaten: 

- Registratie van deze clients over Azure AD is per gebruiker/apparaat. Als een voorbeeld: als jdoe en jharnett moet u zich bij dit apparaat aanmelden, de registratie van een afzonderlijke (DeviceID) wordt gemaakt voor elk van deze gebruikers in het tabblad gebruiker info.  

- De registratie van deze clients buiten het vak is geconfigureerd om te proberen bij het aanmelden of vergrendelen/ontgrendelen en kan er 5 minuten vertraging dat dit met behulp van een Task Scheduler-taak wordt geactiveerd. 

- Een opnieuw installeren van het besturingssysteem of een handmatige opheffen van de registratie en opnieuw te registreren, kan een nieuwe registratie maakt op Azure AD en resulteert in meerdere vermeldingen op het tabblad gebruikers gegevens in de Azure portal. 


## <a name="step-1-retrieve-the-registration-status"></a>Stap 1: De registratiestatus ophalen 

**De registratiestatus controleren:**  

1. Open de opdrachtprompt als beheerder 

2. Type`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

Met deze opdracht geeft een dialoogvenster waarmee u meer informatie over de status van de join.

![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-the-registration-status"></a>Stap 2: De registratiestatus van de 

Als de join niet geslaagd is, biedt in het dialoogvenster u informatie over het probleem dat is opgetreden.

**De meest voorkomende problemen zijn:**

- Een onjuist geconfigureerde AD FS of Azure AD

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- U bent niet aangemeld op als een domeingebruiker

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- Een quotum is bereikt

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- De service reageert niet 

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

U kunt ook de statusinformatie vinden in het gebeurtenislogboek onder **toepassingen en Services Log\Microsoft-Workplace Join**.
  
**De meest voorkomende oorzaken voor de registratie van een mislukte zijn:** 

- Uw computer zich niet in het interne netwerk van de organisatie of een VPN zonder verbinding met een on-premises AD-domeincontroller.

- U bent aangemeld met een lokaal computeraccount op de computer. 

- Problemen met de configuratie van service: 

  - De federation-server is geconfigureerd voor ondersteuning van **WIAORMULTIAUTHN**. 

  - Er is geen Service Connection Point-object dat verwijst naar de domeinnaam van uw geverifieerde in Azure AD in het AD-forest waar de computer deel uitmaakt.

  - Een gebruiker heeft de limiet van apparaten bereikt. Zie aan de slag met Azure Active Directory-apparaatregistratie.

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie de [automatische apparaatregistratie Veelgestelde vragen](active-directory-device-registration-faq.md) 

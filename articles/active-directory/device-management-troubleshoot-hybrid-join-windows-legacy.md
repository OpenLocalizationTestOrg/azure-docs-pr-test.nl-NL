---
title: aaaTroubleshooting hybride Azure Active Directory die lid zijn van de downlevel-apparaten | Microsoft Docs
description: Het oplossen van hybride Azure Active Directory die lid zijn van downlevel-apparaten.
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a>Het oplossen van hybride Azure Active Directory die lid zijn van downlevel-apparaten 

In dit onderwerp is van toepassing alleen toohello apparaten te volgen: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Zie voor Windows 10 of Windows Server 2016 [probleemoplossing hybride Azure Active Directory die lid zijn van apparaten met Windows 10 en Windows Server 2016](device-management-troubleshoot-hybrid-join-windows-current.md).

Dit onderwerp wordt ervan uitgegaan dat u hebt [geconfigureerde hybride Azure Active Directory die lid zijn van de apparaten](device-management-hybrid-azuread-joined-devices-setup.md) toosupport Hallo volgen scenario's:

- Voorwaardelijke toegang op basis van apparaten

- [Enterprise-instellingen voor roaming](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello voor Bedrijven](active-directory-azureadjoin-passport-deployment.md) 





Dit onderwerp vindt u informatie over hoe tooresolve mogelijke problemen op te lossen.  

**Wat u moet weten:** 

- maximum aantal apparaten per gebruiker Hallo is apparaatgerichte. Bijvoorbeeld, als *jdoe* en *jharnett* tooa aanmelden apparaat, de registratie van een afzonderlijke (DeviceID) wordt gemaakt voor elk van deze in Hallo **gebruiker** tabblad info.  

- Hallo initiële registratie / join is van de apparaten geconfigureerde tooperform een poging gedaan bij het aanmelden of vergrendelen / ontgrendelen. Er zijn 5 minuten vertraging geactiveerd door een scheduler-taak. 

- Opnieuw installeren van Hallo-besturingssysteem of een handmatige unregister en opnieuw te registreren kunnen een nieuwe registratie maakt op Azure AD en resulteert in meerdere vermeldingen Hallo gebruiker info tabblad in hello Azure-portal. 


## <a name="step-1-retrieve-hello-registration-status"></a>Stap 1: De registratiestatus Hallo ophalen 

**tooverify hello registratiestatus:**  

1. Open Hallo opdrachtprompt als beheerder 

2. Type`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

Met deze opdracht geeft een dialoogvenster waarmee u meer informatie over de status van Hallo join.

![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a>Stap 2: De Hallo hybride Azure AD join-status 

Als Hallo hybride Azure AD join niet geslaagd is, biedt Hallo dialoogvenster u meer informatie over Hallo probleem dat is opgetreden.

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
  
**Hallo meest voorkomende oorzaken van een mislukte hybride Azure AD join zijn:** 

- Uw computer is niet op het interne netwerk van de organisatie van de hello of een VPN zonder verbinding tooan lokale AD-domeincontroller.

- U bent aangemeld op de computer tooyour met een lokaal computeraccount. 

- Problemen met de configuratie van service: 

  - Hallo federation-server is geconfigureerd toosupport **WIAORMULTIAUTHN**. 

  - Er is geen Service Connection Point-object dat tooyour geverifieerde domeinnaam op beheerpunten in Azure AD in Hallo AD-forest waar Hallo computer behoort.

  - Een gebruiker de Hallo heeft bereikt van apparaten. 

## <a name="next-steps"></a>Volgende stappen

Bekijk voor vragen Hallo [Apparaatbeheer Veelgestelde vragen](device-management-faq.md)  

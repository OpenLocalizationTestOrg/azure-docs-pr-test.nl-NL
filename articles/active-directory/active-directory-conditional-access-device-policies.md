---
title: apparaatbeleid voor aaaAzure Active Directory voorwaardelijke toegang voor Office 365-services | Microsoft Docs
description: Meer informatie over hoe tooprovision voorwaardelijke toegang apparaat beleid toohelp beter beveiligen van bedrijfsbronnen, terwijl de naleving en toegang tooservices gebruiker.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8664c0bb-bba1-4012-b321-e9c8363080a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 38229a8d9766efbf0e6b17875b3018011c6b4ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="active-directory-conditional-access-device-policies-for-office-365-services"></a>Active Directory voorwaardelijke toegang apparaatbeleid voor Office 365-services

Voorwaardelijke toegang is vereist toowork met meerdere onderdelen. Hierbij een multi-factor geverifieerde gebruiker, een geverifieerde apparaat en een compatibel apparaat, van andere factoren. In dit artikel wordt voornamelijk gericht op voorwaarden op basis van een apparaat dat uw organisatie toohelp beheren van toegang tot tooOffice 365 services kunt gebruiken. 

Zakelijke gebruikers willen tooaccess Office 365-services zoals Exchange en SharePoint Online op het werk of school vanaf hun persoonlijke apparaten. Wilt u Hallo toegang toobe beveiligd. U kunt voorwaardelijke toegang apparaat beleid toohelp zorg bedrijfsbronnen veiliger bij het verlenen van toegang tooservices voor gebruikers met compatibele apparaten inrichten. U kunt voorwaardelijke toegang beleid tooOffice 365 in Hallo Microsoft Intune-portal voor voorwaardelijke toegang instellen.

Azure Active Directory (Azure AD) voorwaardelijk beleid toohelp veilige toegang tooOffice 365 services worden afgedwongen. U kunt beleid voor voorwaardelijke toegang waardoor een gebruiker die gebruikmaakt van een niet-compatibele apparaten toegang krijgen tot Office 365-service maken. Hallo-gebruiker moet van het bedrijf toohello apparaatbeleid voldoen voordat de toohello-access-service wordt verleend. Ook kunt u een beleid waarvoor tooenroll gebruikers hun apparaten toogain toegang tooan Office 365-service. Beleid kunnen worden toegepast tooall gebruikers in een organisatie of tooa enkele doelgroepen beperkt. U kunt meer tooa beleid van de doel-groepen toevoegen gedurende een bepaalde periode.

Een vereiste voor het afdwingen van beleidsregels voor apparaten is dat gebruikers hun apparaten bij Azure AD Hallo device registratieservice registreren moeten. U kunt ervoor kiezen tooturn op multi-factor authentication voor apparaten die geregistreerd bij Hallo apparaatregistratieservice van Azure AD. Multi-factor authentication-server wordt aanbevolen voor hello Azure Active Directory device registration-service. Wanneer multi-factor authentication-server is ingeschakeld, worden gebruikers die hun apparaten bij Hallo apparaatregistratieservice van Azure AD registreren gecontroleerd voor tweeledige verificatie.

## <a name="how-does-a-conditional-access-policy-work"></a>Hoe werkt een beleid voor voorwaardelijke toegang?

Wanneer een gebruiker toegang tooan Office 365-service-van een platform ondersteund apparaat aanvragen, wordt Azure AD verifieert Hallo gebruiker en Hallo-apparaat. Azure AD verleent toegang toohello service alleen als de gebruiker Hallo toohello beleid instellen voor Hallo service voldoet. Krijgen gebruikers op apparaten die niet zijn ingeschreven instructies over het tooenroll en niet meer compatibel tooaccess zakelijke Office 365-services. Gebruikers op iOS en Android-apparaten vereist tooenroll van hun apparaten via de Intune-bedrijfsportal-toepassing hello zijn. Wanneer een gebruiker een apparaat inschrijft, Hallo-apparaat is geregistreerd bij Azure AD en ingeschreven voor beheer van apparaten en naleving. U moet hello Azure AD-apparaatregistratieservice met Microsoft Intune gebruiken voor mobile device management voor Office 365-services. Inschrijving van apparaten is vereist voor gebruikers tooaccess Office 365-services wanneer het apparaatbeleid wordt afgedwongen.

Wanneer een gebruiker met succes inschrijft een apparaat, het Hallo-apparaat wordt vertrouwd. Azure AD biedt Hallo geverifieerde gebruiker één aanmelding toegang toocompany toepassingen. Azure AD dwingt een voorwaardelijk beleid toogrant access tooa service niet alleen Hallo eerste tijd Hallo gebruiker toegang vraagt, maar elke keer Hallo gebruiker een aanvraag voor toegang wordt verlengd. Hallo gebruiker wanneer de aanmeldingsreferenties zijn gewijzigd, Hallo-apparaat is zoekgeraakt of gestolen of Hallo voorwaarden van het Hallo-beleid wordt niet voldaan op Hallo-tijd van aanvraag voor certificaatvernieuwing tooservices toegang geweigerd.

## <a name="deployment-considerations"></a>Overwegingen bij de implementatie

U moet hello Azure AD device registration service tooregister apparaten gebruiken.

Wanneer de on-premises gebruikers zijn over toobe geverifieerd, Active Directory Federation Services (AD FS) (versie 1.0 en hoger) is vereist. Multi-factor authentication voor Workplace Join mislukt wanneer het Hallo-id-provider is niet geschikt voor multi-factor authentication-server. U kunt multi-factor authentication-server bijvoorbeeld niet gebruiken met AD FS 2.0. Zorg ervoor dat Hallo on-premises AD FS werkt met meervoudige verificatie, en dat een geldig multi-factor authenticatiemethode aanwezig is voordat u multi-factor authentication voor hello Azure AD device registration-service inschakelt. AD FS in Windows Server 2012 R2 heeft bijvoorbeeld de mogelijkheden van multi-factor authentication-server. Ook moet u instellen een extra geldig verificatie (MFA)-methode op Hallo AD FS-server voordat u multi-factor authentication voor hello Azure AD device registration-service inschakelt. Zie voor meer informatie over ondersteunde MFA-methoden in AD FS [extra verificatiemethoden configureren voor AD FS](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs).

## <a name="next-steps"></a>Volgende stappen

*   Bekijk voor antwoorden toocommon vragen [voorwaardelijke toegang van Azure Active Directory Veelgestelde vragen over](active-directory-conditional-faqs.md).

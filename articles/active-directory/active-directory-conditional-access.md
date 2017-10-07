---
title: aaaConditional toegang in de klassieke Azure-portal Hallo | Microsoft Docs
description: "Gebruik voorwaardelijk toegangsbeheer in Azure classic portal toocheck Hallo voor specifieke condities bij het verifiëren voor toegang tot tooapplications."
services: active-directory
keywords: voorwaardelijke toegang tooapps, voorwaardelijke toegang in Azure AD, beveiligde toegang tot resources toocompany, beleidsregels voor voorwaardelijke toegang
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: da3f0a44-1399-4e0b-aefb-03a826ae4ead
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.custom: oldportal
ms.openlocfilehash: 049bd3f6ec9e35479319ee7608b007b9a1e16647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-hello-azure-classic-portal"></a>Voorwaardelijke toegang in Hallo klassieke Azure-portal

Dit onderwerp gaat over voorwaardelijke toegang in Hallo klassieke Azure-portal. Zie voor de meest recente informatie over voorwaardelijke toegang in Azure Active Directory Hallo Hallo [voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-azure-portal.md).


Hallo besturingselement mogelijkheden in voorwaardelijke toegang van Azure Active Directory (Azure AD) bieden een eenvoudige manieren toohelp beveiligde bronnen in Hallo cloud en on-premises. Beleid voor voorwaardelijke toegang zoals multi-factor authentication-server kan helpen beschermen tegen Hallo risico van gestolen en phished referenties. Andere beleidsregels voor voorwaardelijke toegang kunt gegevens van uw organisatie veilig te houden. Bijvoorbeeld, Daarnaast toorequiring referenties u wellicht een beleid dat alleen apparaten die zijn ingeschreven in een beheersysteem voor mobiele apparaten, zoals Microsoft Intune kunt krijgen tot gevoelige services van uw organisatie.

## <a name="prerequisites"></a>Vereisten
Voorwaardelijke toegang van Azure AD is een functie van [Azure Active Directory Premium](http://www.microsoft.com/identity). Elke gebruiker die toegang heeft tot een toepassing met beleid voor voorwaardelijke toegang toegepast moet een Azure AD Premium-licentie hebben. U kunt meer informatie over vereisten voor productlicenties in [rapport niet-gelicentieerde gebruikers](https://aka.ms/utc5ix).

## <a name="how-is-conditional-access-control-enforced"></a>Hoe wordt voorwaardelijk toegangsbeheer afgedwongen?
Voorwaardelijke toegang worden gecontroleerd controleert Azure AD voor specifieke condities Hallo instellen voor een gebruiker tooaccess een toepassing. Nadat de vereisten voor toegang wordt voldaan, wordt Hallo gebruiker is geverifieerd en toegang tot de toepassing hello.  

![Overzicht van voorwaardelijke toegang](./media/active-directory-conditional-access/conditionalaccess-overview.png)

## <a name="conditions"></a>Voorwaarden
Dit zijn de voorwaarden die u in een beleid voor voorwaardelijke toegang opnemen kunt:

* **Groepslidmaatschap**. Een gebruiker toegang op basis van lidmaatschap in een groep beheren.
* **Locatie**. Hallo-locatie van Hallo gebruiker tootrigger multi-factor authentication gebruiken en blok besturingselementen gebruiken als een gebruiker zich niet in een vertrouwd netwerk.
* **Apparaatplatform**. Hallo apparaatplatform, zoals iOS, Android, Windows Mobile of Windows, gebruiken als een voorwaarde voor het toepassen van beleid.
* **Apparaat is ingeschakeld**. Status van het apparaat, of ingeschakeld of uitgeschakeld, wordt al gevalideerd tijdens de evaluatie van het apparaat beleid. Als u een verloren of gestolen apparaat in de map Hallo uitschakelt, deze niet langer voldoen aan de vereisten.
* **Aanmelden en gebruiker risico**. U kunt [Azure AD Identity Protection](active-directory-identityprotection.md) voor beleid voor voorwaardelijke toegang risico. Risico beleidsregels voor voorwaardelijke toegang kunnen krijgen van uw organisatie geavanceerde beveiliging op basis van de risicogebeurtenissen en ongebruikelijke activiteiten aanmelden.

## <a name="controls"></a>Besturingselementen
Dit zijn de besturingselementen waarmee u tooenforce beleid voor voorwaardelijke toegang kunt:

* **Multi-factorauthenticatie**. U kunt sterke verificatie door middel van meervoudige verificatie vereisen. U kunt multi-factor authentication-server gebruiken met Azure multi-factor Authentication of met behulp van een lokale multi-factor authentication-provider, gecombineerd met Active Directory Federation Services (AD FS). Met multi-factor authentication helpt voorkomen dat bronnen worden geopend door onbevoegde gebruikers mogelijk hebben die toegang heeft gekregen toohello referenties van een geldige gebruiker.
* **Blok**. U kunt voorwaarden zoals locatie tooblock gebruiker gebruikerstoegang toepassen. U kunt bijvoorbeeld toegang blokkeren als een gebruiker zich niet in een vertrouwd netwerk.
* **Compatibele apparaten**. U kunt beleid voor voorwaardelijke toegang instellen op niveau Hallo-apparaten. U kunt een beleid instellen zodat alleen computers die lid zijn van een domein of mobiele apparaten die zijn ingeschreven in een management-toepassing voor mobiele apparaten, toegang krijgen bronnen van uw organisatie tot. U kunt bijvoorbeeld Intune toocheck apparaatcompatibiliteit gebruiken, en vervolgens rapporteren tooAzure AD voor afdwinging wanneer Hallo gebruiker een toepassing tooaccess probeert. Voor gedetailleerde richtlijnen over hoe toouse Intune tooprotect apps en gegevens, Zie [apps en gegevens beschermen met Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/protect-apps-and-data-with-microsoft-intune). Ook kunt u Intune tooenforce gegevensbeveiliging voor verloren of gestolen apparaten. Zie voor meer informatie [Help uw gegevens beschermen met volledig wissen of selectief wissen met Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

## <a name="applications"></a>Toepassingen
U kunt beleid voor voorwaardelijke toegang op toepassingsniveau Hallo afdwingen. Toegangsniveaus voor toepassingen en services in Hallo cloud of on-premises instellen. Hallo-beleid is toegepast rechtstreeks toohello website of service. Hallo-beleid wordt afgedwongen voor toegang tot toohello browser en tooapplications die toegang hebben tot Hallo-service.

## <a name="device-based-conditional-access"></a>Voorwaardelijke toegang op basis van apparaten
U kunt toegang tooapplications beperken van apparaten die zijn geregistreerd bij Azure AD en die voldoen aan bepaalde voorwaarden. Voorwaardelijke toegang op basis van apparaten beveiligt bronnen in een organisatie van gebruikers die proberen tooaccess Hallo resources uit:

* Onbekende of niet-beheerde apparaten.
* Apparaten die niet voldoen aan het beveiligingsbeleid Hallo uw organisatie is ingesteld.

U kunt beleid op basis van deze vereisten instellen:

* **Apparaten die lid zijn van een domein**. Stel een beleid toorestrict toegang toodevices die gekoppelde tooan lokale Active Directory-domein en die ook zijn geregistreerd bij Azure AD. Dit beleid geldt tooWindows desktops, laptops en tablets enterprise.
  Voor meer informatie over het tooset van automatische registratie van apparaten die lid zijn van een domein in Azure AD, Zie [automatische registratie van Windows-domein-apparaten met Azure Active Directory instellen](active-directory-conditional-access-automatic-device-registration-setup.md).
* **Compatibele apparaten**. Stel een beleid toorestrict toegang toodevices die zijn gemarkeerd **compatibele** in Hallo management systeemmap. Dit beleid zorgt ervoor dat alleen apparaten die voldoen aan het beveiligingsbeleid zoals het afdwingen van versleuteling op een apparaat toegang zijn toegestaan. U kunt deze beleid toorestrict toegang van apparaten na hello gebruiken:
  
  * **Windows-domein apparaten**. Beheerd door System Center Configuration Manager (in huidige vertakking Hallo) geïmplementeerd in een hybride-configuratie.
  * **Windows 10 Mobile werk- of persoonlijke apparaten**. Beheerd door Intune of door het beheersysteem ondersteunde mobiele apparaten van derden.
  * **iOS en Android-apparaten**. Beheerd door Intune.

Gebruikers die toegang tot toepassingen die worden beveiligd door een op basis van apparaten, beleid voor toegang moet hebben tot de toepassing hello van een apparaat dat voldoet aan de vereisten van dit beleid. Toegang wordt geweigerd als geprobeerd op een apparaat dat niet voldoet aan de beleidsvereisten.

Voor informatie over hoe een op basis van apparaten, tooconfigure beleid in Azure AD zien [ingesteld beleid voor voorwaardelijke toegang op basis van apparaten voor Azure Active Directory-toepassingen](active-directory-conditional-access-policy-connected-applications.md).

## <a name="resources"></a>Resources
Zie Hallo resource categorieën en artikelen toolearn meer over het instellen van voorwaardelijke toegang voor uw organisatie te volgen.

### <a name="multi-factor-authentication-and-location-policies"></a>Beleid voor meervoudige verificatie en de locatie
* [Aan de slag met voorwaardelijke toegang tooAzure AD verbonden apps op basis van de groep, de locatie en de MFA-beleid](active-directory-conditional-access-azuread-connected-apps.md)
* [Toepassingen en browsers die worden ondersteund](active-directory-conditional-access-supported-apps.md)

### <a name="device-based-conditional-access"></a>Voorwaardelijke toegang op basis van apparaten
* [Beleid voor voorwaardelijke toegang op basis van apparaten om toegang te krijgen besturingselement tooAzure Active Directory-toepassingen instellen](active-directory-conditional-access-policy-connected-applications.md)
* [Instellen van automatische registratie van Windows-apparaten met Azure Active Directory-domein](active-directory-conditional-access-automatic-device-registration-setup.md)
* [Probleemoplossing voor problemen met Azure Active Directory-toegang](active-directory-conditional-access-device-remediation.md)
* [Gegevens op verloren of gestolen apparaten beveiligen met Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)

### <a name="protect-resources-based-on-sign-in-risk"></a>Beveiligen van bronnen op basis van de aanmeldingspagina risico
* [Azure AD identity protection](active-directory-identityprotection.md)

### <a name="next-steps"></a>Volgende stappen
* [Voorwaardelijke toegang Veelgestelde vragen](active-directory-conditional-faqs.md)
* [Technische naslaginformatie](active-directory-conditional-access-technical-reference.md)


---
title: Voorwaardelijke toegang in de klassieke Azure portal | Microsoft Docs
description: "Voorwaardelijk toegangsbeheer in de klassieke Azure portal gebruiken om te controleren op bepaalde voorwaarden bij het verifiëren voor toegang tot toepassingen."
services: active-directory
keywords: voorwaardelijke toegang tot apps, voorwaardelijke toegang met Azure AD, beveiligde toegang tot bedrijfsresources, beleidsregels voor voorwaardelijke toegang
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
ms.openlocfilehash: d96eeb07c4bf3944be82d9c54aea93d52b54a37a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="conditional-access-in-the-azure-classic-portal"></a>Voorwaardelijke toegang in de klassieke Azure portal

Dit onderwerp gaat over voorwaardelijke toegang in de klassieke Azure portal. Zie voor de meest recente informatie over voorwaardelijke toegang in de Azure Active Directory [voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-azure-portal.md).


De mogelijkheden voor beheer van voorwaardelijke toegang van Azure Active Directory (Azure AD) bieden eenvoudige manieren om beveiligde bronnen in de cloud en on-premises te. Beleid voor voorwaardelijke toegang zoals multi-factor authentication-server kunt beveiligen tegen het risico van gestolen en phished referenties. Andere beleidsregels voor voorwaardelijke toegang kunt gegevens van uw organisatie veilig te houden. Bijvoorbeeld, naast het vereisen van referenties wellicht u een beleid dat alleen apparaten die zijn ingeschreven in een beheersysteem voor mobiele apparaten, zoals Microsoft Intune kunt krijgen tot gevoelige services van uw organisatie.

## <a name="prerequisites"></a>Vereisten
Voorwaardelijke toegang van Azure AD is een functie van [Azure Active Directory Premium](http://www.microsoft.com/identity). Elke gebruiker die toegang heeft tot een toepassing met beleid voor voorwaardelijke toegang toegepast moet een Azure AD Premium-licentie hebben. U kunt meer informatie over vereisten voor productlicenties in [rapport niet-gelicentieerde gebruikers](https://aka.ms/utc5ix).

## <a name="how-is-conditional-access-control-enforced"></a>Hoe wordt voorwaardelijk toegangsbeheer afgedwongen?
Met voorwaardelijk toegangsbeheer in plaats Azure AD gecontroleerd op de specifieke u voorwaarden instellen voor een gebruiker toegang tot een toepassing. Nadat de vereisten voor toegang wordt voldaan, wordt de gebruiker is geverifieerd en toegang tot de toepassing.  

![Overzicht van voorwaardelijke toegang](./media/active-directory-conditional-access/conditionalaccess-overview.png)

## <a name="conditions"></a>Voorwaarden
Dit zijn de voorwaarden die u in een beleid voor voorwaardelijke toegang opnemen kunt:

* **Groepslidmaatschap**. Een gebruiker toegang op basis van lidmaatschap in een groep beheren.
* **Locatie**. De locatie van de gebruiker trigger multi-factor authentication-server gebruiken en blok besturingselementen gebruiken als een gebruiker zich niet in een vertrouwd netwerk.
* **Apparaatplatform**. Gebruik het apparaatplatform, zoals iOS, Android, Windows Mobile of Windows, als een voorwaarde voor het toepassen van beleid.
* **Apparaat is ingeschakeld**. Status van het apparaat, of ingeschakeld of uitgeschakeld, wordt al gevalideerd tijdens de evaluatie van het apparaat beleid. Als u een verloren of gestolen apparaat in de map uitschakelt, deze niet langer voldoen aan de vereisten.
* **Aanmelden en gebruiker risico**. U kunt [Azure AD Identity Protection](active-directory-identityprotection.md) voor beleid voor voorwaardelijke toegang risico. Risico beleidsregels voor voorwaardelijke toegang kunnen krijgen van uw organisatie geavanceerde beveiliging op basis van de risicogebeurtenissen en ongebruikelijke activiteiten aanmelden.

## <a name="controls"></a>Besturingselementen
Dit zijn de besturingselementen die u gebruiken kunt voor het afdwingen van beleid voor voorwaardelijke toegang:

* **Multi-factorauthenticatie**. U kunt sterke verificatie door middel van meervoudige verificatie vereisen. U kunt multi-factor authentication-server gebruiken met Azure multi-factor Authentication of met behulp van een lokale multi-factor authentication-provider, gecombineerd met Active Directory Federation Services (AD FS). Met multi-factor authentication voorkomt bronnen worden geopend door onbevoegde gebruikers die toegang tot de referenties van een geldige gebruiker kan hebben.
* **Blok**. U kunt voorwaarden zoals de locatie van de gebruiker te blokkeren van toegang voor gebruikers toepassen. U kunt bijvoorbeeld toegang blokkeren als een gebruiker zich niet in een vertrouwd netwerk.
* **Compatibele apparaten**. U kunt beleid voor voorwaardelijke toegang instellen op het apparaatniveau van het. U kunt een beleid instellen zodat alleen computers die lid zijn van een domein of mobiele apparaten die zijn ingeschreven in een management-toepassing voor mobiele apparaten, toegang krijgen bronnen van uw organisatie tot. U kunt bijvoorbeeld Intune gebruiken om te controleren op naleving van apparaten en vervolgens naar Azure AD voor afdwinging te rapporteren wanneer de gebruiker probeert te krijgen tot een toepassing. Zie voor gedetailleerde instructies over het gebruik van Intune-apps en gegevens te beschermen [apps en gegevens beschermen met Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/protect-apps-and-data-with-microsoft-intune). U kunt Intune ook gebruiken om af te dwingen van gegevensbeveiliging voor verloren of gestolen apparaten. Zie voor meer informatie [Help uw gegevens beschermen met volledig wissen of selectief wissen met Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

## <a name="applications"></a>Toepassingen
U kunt beleid voor voorwaardelijke toegang op toepassingsniveau afdwingen. Toegangsniveaus voor toepassingen en services in de cloud of on-premises instellen. Het beleid wordt toegepast rechtstreeks naar de website of de service. Het beleid wordt afgedwongen voor toegang tot de browser en voor toepassingen die toegang tot de service.

## <a name="device-based-conditional-access"></a>Voorwaardelijke toegang op basis van apparaten
U kunt de toegang beperken tot toepassingen vanaf apparaten die zijn geregistreerd bij Azure AD en die voldoen aan bepaalde voorwaarden. Voorwaardelijke toegang op basis van apparaten beveiligt bronnen in een organisatie van gebruikers die proberen te krijgen tot de bronnen van:

* Onbekende of niet-beheerde apparaten.
* Apparaten die niet voldoen aan het beveiligingsbeleid van uw organisatie is ingesteld.

U kunt beleid op basis van deze vereisten instellen:

* **Apparaten die lid zijn van een domein**. Stel een beleid voor de toegang beperken tot apparaten die zijn gekoppeld aan een lokale Active Directory-domein en die ook zijn geregistreerd bij Azure AD. Dit beleid is van toepassing op Windows-desktops, laptops en tablets enterprise.
  Zie voor meer informatie over het instellen van automatische registratie van apparaten die lid zijn van een domein met Azure AD [automatische registratie van Windows-domein-apparaten met Azure Active Directory instellen](active-directory-conditional-access-automatic-device-registration-setup.md).
* **Compatibele apparaten**. Stel een beleid voor het beperken van toegang tot apparaten die zijn gemarkeerd **compatibele** in de map van de system management. Dit beleid zorgt ervoor dat alleen apparaten die voldoen aan het beveiligingsbeleid zoals het afdwingen van versleuteling op een apparaat toegang zijn toegestaan. U kunt dit beleid gebruiken om toegang te beperken van de volgende apparaten:
  
  * **Windows-domein apparaten**. Beheerd door System Center Configuration Manager (in de huidige vertakking) geïmplementeerd in een hybride-configuratie.
  * **Windows 10 Mobile werk- of persoonlijke apparaten**. Beheerd door Intune of door het beheersysteem ondersteunde mobiele apparaten van derden.
  * **iOS en Android-apparaten**. Beheerd door Intune.

Gebruikers die toegang tot toepassingen die worden beveiligd door een op basis van apparaten, beleid moet toegang tot de toepassing van een apparaat dat voldoet aan de vereisten van dit beleid. Toegang wordt geweigerd als geprobeerd op een apparaat dat niet voldoet aan de beleidsvereisten.

Zie voor meer informatie over het configureren van een beleid op basis van apparaten in Azure AD [ingesteld beleid voor voorwaardelijke toegang op basis van apparaten voor Azure Active Directory-toepassingen](active-directory-conditional-access-policy-connected-applications.md).

## <a name="resources"></a>Resources
Zie de volgende categorieën van de resource en de volgende artikelen voor meer informatie over het instellen van voorwaardelijke toegang voor uw organisatie.

### <a name="multi-factor-authentication-and-location-policies"></a>Beleid voor meervoudige verificatie en de locatie
* [Aan de slag met voorwaardelijke toegang tot Azure AD verbonden apps op basis van de groep, de locatie en de MFA-beleid](active-directory-conditional-access-azuread-connected-apps.md)
* [Toepassingen en browsers die worden ondersteund](active-directory-conditional-access-supported-apps.md)

### <a name="device-based-conditional-access"></a>Voorwaardelijke toegang op basis van apparaten
* [Voorwaardelijke toegang op basis van apparaten beleid voor toegangsbeheer instellen op Azure Active Directory-toepassingen](active-directory-conditional-access-policy-connected-applications.md)
* [Instellen van automatische registratie van Windows-apparaten met Azure Active Directory-domein](active-directory-conditional-access-automatic-device-registration-setup.md)
* [Probleemoplossing voor problemen met Azure Active Directory-toegang](active-directory-conditional-access-device-remediation.md)
* [Gegevens op verloren of gestolen apparaten beveiligen met Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)

### <a name="protect-resources-based-on-sign-in-risk"></a>Beveiligen van bronnen op basis van de aanmeldingspagina risico
* [Azure AD identity protection](active-directory-identityprotection.md)

### <a name="next-steps"></a>Volgende stappen
* [Voorwaardelijke toegang Veelgestelde vragen](active-directory-conditional-faqs.md)
* [Technische naslaginformatie](active-directory-conditional-access-technical-reference.md)


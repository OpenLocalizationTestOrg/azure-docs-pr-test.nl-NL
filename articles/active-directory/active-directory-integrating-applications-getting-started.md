---
title: aaaGet gestart Azure AD integreren met apps | Microsoft Docs
description: Dit artikel is een introductiehandleiding voor het integreren van Azure Active Directory (AD) met on-premises toepassingen en cloud-toepassingen.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: db6d210d-c970-49e9-bd20-36d984bcd1c3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 5a7a851e8418083fee72ab58477a9cab75d0d4bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-active-directory-with-applications-getting-started-guide"></a>Azure Active Directory integreren met toepassingen aan de slag
## <a name="overview"></a>Overzicht
Dit onderwerp is bedoeld toogive u een roadmap voor toepassingen integreren met Azure Active Directory (AD). Elk Hallo in de volgende secties bevatten een korte samenvatting van een meer gedetailleerde onderwerp zodat u kunt identificeren welke onderdelen van deze introductiehandleiding relevante tooyou zijn.  Volg Hallo koppelingen voor meer informatie over elk onderwerp.

## <a name="before-you-begin-take-inventory"></a>Voordat u begint, inventariseren
Voordat u gaan in toointegrating toepassingen met Azure AD, is het belangrijk tooknow waar u bent en waar u wilt dat toogo.  Hallo zijn volgende vragen beoogde toohelp u over uw Azure AD-integratie toepassingsproject nadenken.

### <a name="application-inventory"></a>Toepassingsinventaris
* Waar worden al uw toepassingen? Eigenaar van deze?
* Wat voor soort verificatie vereisen uw toepassingen?
* Wie toegang toowhich toepassingen nodig?
* Wilt u een nieuwe toepassing toodeploy?
  * U bouwt het intern en deze implementeren op een exemplaar van Azure compute?
  * U gebruikt een die beschikbaar is in de galerie van Azure-toepassing hello?

### <a name="user-and-group-inventory"></a>Inventarisatie van gebruikers en groepen
* Waar de gebruikersaccounts zich bevinden?
  * On-premises Active Directory
  * Azure AD
  * In de database van een afzonderlijke toepassing waarvan u eigenaar
  * In niet-toegestane toepassingen
  * Alle bovenstaande Hallo
* Welke machtigingen en roltoewijzingen individuele gebruikers hebt? U hoeft tooreview hun toegang of weet u zeker dat de toewijzingen van uw gebruikers toegang en de rol geschikt nu zijn?
* Groepen reeds bestaan in uw lokale Active Directory?
  * Hoe kan ik de groepen ingedeeld?
  * Wie zijn de groepsleden Hallo?
  * Welke machtigingen/roltoewijzingen Hallo groepen momenteel hebt?
* Wilt u tooclean van de gebruiker of groep databases voordat de integratie van?  (Dit is een vraag heel belangrijk. Garbagecollection in garbagecollection uit.)

### <a name="access-management-inventory"></a>Access management-inventarisatie
* Hoe beheert u momenteel gebruiker toegang tooapplications? Heeft die toochange nodig?  Hebt u beschouwd als andere manieren toomanage toegang, zoals met [RBAC](role-based-access-control-configure.md) bijvoorbeeld?
* Wie toegang toowhat nodig?

Misschien u vooraf Hallo-antwoorden tooall van deze vragen hebt, maar dat is geen probleem.  Deze handleiding kunt u enkele van deze vragen te beantwoorden en sommige gefundeerde beslissingen te nemen.

## <a name="prerequisites"></a>Vereisten
* Een Azure-abonnement en een Azure Active Directory-directory.  Als u nog geen Azure-abonnement hebt, kunt u Azure voor 30 dagen gratis uitproberen. [Probeer het nu!](https://azure.microsoft.com/trial/get-started-active-directory/)

## <a name="application-integration-with-azure-ad"></a>Integratie van toepassingen met Azure AD
### <a name="finding-unsanctioned-cloud-applications-with-cloud-app-discovery"></a>Zoeken naar niet-toegestane cloud-toepassingen met Cloud App Discovery
Zoals eerder vermeld, worden toepassingen die nog niet is beheerd door uw organisatie tot op heden.  Als onderdeel van de procedure inventarisatie hello is het mogelijk niet-toegestane toofind cloud-toepassingen. Zie [zoeken naar niet-toegestane cloud-toepassingen met Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).

### <a name="authentication-types"></a>Verificatietypen
Elk van uw toepassingen mogelijk andere verificatievereisten. Met Azure AD kan ondertekenen van certificaten worden gebruikt met toepassingen die gebruikmaken van SAML 2.0, WS-Federation, of OpenID Connect protocollen, evenals wachtwoord eenmalige aanmelding. Zie voor meer informatie over toepassing verificatietypen voor gebruik met Azure AD [certificaten beheren voor federatieve eenmalige aanmelding bij Azure Active Directory](active-directory-sso-certs.md) en [eenmalige aanmelding op op basis van wachtwoorden](active-directory-appssoaccess-whatis.md).

### <a name="enabling-sso-with-azure-ad-app-proxy"></a>Eenmalige aanmelding met Azure AD-toepassingsproxy inschakelen
U kunt met Microsoft Azure AD-toepassingsproxy toegang tooapplications zich binnen uw particuliere netwerk veilig, overal en op elk apparaat opgeven. Nadat u een connector voor toepassingsproxy hebt geïnstalleerd in uw omgeving, kan het eenvoudig met Azure AD geconfigureerd.

### <a name="integrating-applications-with-azure-ad"></a>Toepassingen integreren met Azure AD
Hallo bespreken volgende artikelen Hallo verschillende manieren toepassingen integreren met Azure AD en sommige advies.

* [Bepalen welke toouse Active Directory](active-directory-administer.md)
* [Toepassingen gebruiken in Azure Hallo-toepassingsgalerie](active-directory-appssoaccess-whatis.md)
* [Integratie van zelfstudies lijst met SaaS-toepassingen](active-directory-saas-tutorial-list.md)

## <a name="managing-access-tooapplications"></a>Het beheren van toegang tooapplications
Hallo volgende artikelen worden manieren beschreven kunt u access tooapplications zodra ze zijn geïntegreerd met Azure AD dat gebruikmaakt van Azure AD-Connectors en Azure AD beheren.

* [Het beheren van toegang tooapps gebruikmaken van Azure AD](active-directory-managing-access-to-apps.md)
* [Automatiseren met Azure AD-Connectors](active-directory-saas-app-provisioning.md)
* [Toewijzen van gebruikers tooan toepassing](active-directory-applications-guiding-developers-assigning-users.md)
* [Toewijzen van groepen tooan toepassing](active-directory-applications-guiding-developers-assigning-groups.md)
* [Accounts delen](active-directory-sharing-accounts.md)

## <a name="integrating-custom-applications"></a>Integratie van aangepaste toepassingen
Als u een nieuwe toepassing ontwikkelt en ontwikkelaars tooassist in het gebruik van power hello Azure AD, Zie [Guiding ontwikkelaars](active-directory-applications-guiding-developers-for-lob-applications.md).

Als u uw aangepaste toepassing toohello galerie van Azure-toepassing tooadd wilt, Zie ['Bring your own app' met Azure AD Self-Service SAML-configuratie](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

## <a name="see-also"></a>Zie ook
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)


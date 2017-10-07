---
title: aaaIntegrate eenmalige aanmelding Azure Active Directory met SaaS-apps | Microsoft Docs
description: Eenmalige aanmelding, verificatie en gebruikers inrichten gecentraliseerd beheer van SaaS-apps in Azure Active Directory inschakelen. Een overzicht van hoe u apps in Azure Active Directory tooSaaS toointegrate.
services: active-directory
keywords: Azure AD integreren met SaaS-apps
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 53b9d341-d1fc-4bbb-ac7c-3f4c68fcf00a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: aaronsm
ms.openlocfilehash: fe621a30429c81c32470635d105ae3e95184efa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-single-sign-on-with-saas-apps"></a>Eenmalige aanmelding Azure Active Directory integreren met SaaS-apps
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-enterprise-apps-manage-sso.md)
> * [Klassieke Azure Portal](active-directory-sso-integrate-saas-apps.md)
>
>

[!INCLUDE [active-directory-sso-use-case-intro](../../includes/active-directory-sso-use-case-intro.md)]

tooget gestart met het instellen van eenmalige aanmelding voor een app die u in uw organisatie bent gebracht, wordt u een bestaande map in Azure Active Directory (Azure AD). U kunt een Azure AD-directory die u via Microsoft Azure, Office 365 of Windows Intune aanschaft gebruiken. Als u twee of meer van deze hebt, raadpleegt u [uw Azure AD-directory beheren](active-directory-administer.md) toodetermine welke één toouse.

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel. Zie voor hoe tooassign beheerdersrollen in Azure AD Hallo beheerder centreren, [beheerdersrollen toewijzen in Azure Active Directory](active-directory-enterprise-apps-manage-sso.md).

## <a name="authentication"></a>Authentication
Voor toepassingen die ondersteuning bieden voor Hallo SAML 2.0, WS-Federation, of OpenID Connect protocollen, Azure Active Directory gebruikt voor het ondertekenen van certificaten tooestablish vertrouwensrelaties. Zie voor meer informatie over deze [beheren van certificaten voor federatieve eenmalige aanmelding](active-directory-sso-certs.md).

Voor toepassingen die ondersteuning bieden voor alleen HTML op basis van formulieren aanmelden, Azure Active Directory maakt gebruik van 'wachtwoordkluizen' tooestablish vertrouwensrelaties. Deze Hallo kunnen gebruikers in uw organisatie toobe automatisch aangemeld tooa SaaS-toepassing met behulp van Azure AD dat gebruikmaakt van Hallo-gebruikersaccountgegevens vanuit Hallo SaaS-toepassing. Azure AD verzamelt en Hallo gebruikersaccountgegevens en gerelateerde wachtwoord Hallo veilig worden opgeslagen. Zie voor meer informatie [op basis van wachtwoorden eenmalige aanmelding](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).

## <a name="authorization"></a>Autorisatie
Een ingerichte account kan een gebruiker is gemachtigd toobe toouse een toepassing nadat ze zijn geverifieerd via eenmalige aanmelding. Gebruikers inrichten kan worden gedaan handmatig of in sommige gevallen kunt u toevoegen en verwijderen van gebruikersgegevens uit Hallo SaaS-Apps op basis van wijzigingen in Azure Active Directory. Zie voor meer informatie over het gebruik van de bestaande Azure AD-connectors voor het automatisch inrichten [automatisch gebruikers inrichten en de inrichting voor SaaS-toepassingen](active-directory-saas-app-provisioning.md).

Anders, u kunt handmatig gebruiker informatie tooan app toevoegen of andere inrichting oplossingen die beschikbaar in de marketplace hello zijn gebruiken.

## <a name="access"></a>Toegang
Azure AD levert aanpasbare op verschillende manieren toodeploy toepassingen tooend gebruikers in uw organisatie. U bent niet vergrendeld in een bepaalde implementatie of een oplossing voor toegang. U kunt [oplossing die het beste past bij uw behoeften Hallo](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

## <a name="additional-considerations-for-applications-already-in-use"></a>Aanvullende overwegingen voor toepassingen al gebruik in
Instellen van eenmalige aanmelding op voor een toepassing die gebruikmaakt van uw organisatie al is een ander proces van het Hallo-proces voor het maken van nieuwe accounts voor een nieuwe toepassing. Er zijn een aantal voorbereidende stappen, met inbegrip van: toewijzing van gebruikersidentiteiten Hallo toepassing tooAzure AD identiteiten en kennis van hoe gebruikers krijgen met logboekregistratie in tooan toepassing nadat deze is geïntegreerd.

> [!NOTE]
> tooset van eenmalige aanmelding van een bestaande toepassing u toohave globale beheerdersrechten moet in beide Azure AD en Hallo SaaS-toepassing.
>
>

### <a name="mapping-user-accounts"></a>Toewijzing van gebruikersaccounts
De identiteit van een gebruiker heeft doorgaans een unieke id die een e-mailadres of de UPN (user Principal name worden kan). U moet toolink (map) toepassing identiteit tootheir respectieve Azure AD de identiteit van elke gebruiker. Er zijn een aantal manieren tooaccomplish dit afhankelijk van hoe Hallo vereisten van de verificatie van uw toepassing.

Zie voor meer informatie over het toewijzen van de toepassing identiteiten met Azure AD-identiteiten [uitgegeven claims in Hallo SAML-token aanpassen](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx) en [aanpassen kenmerktoewijzingen voor het inrichten van](active-directory-saas-customizing-attribute-mappings.md).

### <a name="understanding-hello-users-log-in-experience"></a>Understanding Hallo gebruiker aanmelden
Wanneer u eenmalige aanmelding voor een toepassing die al in gebruik integreert, is het belangrijk toorealize die Hallo gebruikerservaring worden beïnvloed. Voor alle toepassingen starten gebruikers met behulp van hun toosign Azure AD-referenties in. Ook kan zijn dat ze een andere portal tooaccess Hallo-toepassingen moeten gebruiken.

Eenmalige aanmelding voor sommige toepassingen kan worden uitgevoerd op een van de toepassing hello aanmelden interface, maar voor andere toepassingen Hallo gebruiker heeft toogo via een centrale portal zoals ([mijn Apps](http://myapps.microsoft.com) of [Office365](http://portal.office.com/myapps)) toosign in. Meer informatie over de verschillende typen Hallo van eenmalige aanmelding en hun gebruikerservaringen in [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

Een andere waardevolle resource is *toestemming van de gebruiker het onderdrukken van* in Hallo [Guiding ontwikkelaars](active-directory-applications-guiding-developers-for-lob-applications.md) artikel.

## <a name="next-steps"></a>Volgende stappen
Voor SaaS-apps die u in Hallo App-galerie van vinden Azure AD levert een aantal [zelfstudies over het SaaS-apps toointegrate](active-directory-saas-tutorial-list.md).

Als de app is niet in App-galerie, kunt u [toohello galerie van Azure AD-App toevoegen als een aangepaste toepassing](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

Er is veel meer details op al deze problemen in Hallo Azure.com-bibliotheek beginnen met [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).

Bovendien niet gemist Hallo [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md).

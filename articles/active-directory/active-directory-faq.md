---
title: Veelgestelde vragen over Active Directory aaaAzure | Microsoft Docs
description: Azure Active Directory-Veelgestelde vragen antwoorden op vragen over hoe tooaccess Azure en Azure Active Directory, wachtwoordbeheer en toepassing toegang krijgen tot.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2017
ms.author: markvi
ms.openlocfilehash: 63c30c4aeda4551bf02c6b968f98cded5a3b2c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-faq"></a>Veelgestelde vragen over Azure Active Directory
Azure Active Directory (Azure AD) is een uitgebreide IDaaS-oplossing (Identity as a Service) waarin alle aspecten van identiteit, toegangsbeheer en beveiliging zijn opgenomen.

Zie [Wat is Azure Active Directory?](active-directory-whatis.md) voor meer informatie.


## <a name="access-azure-and-azure-active-directory"></a>Toegang tot Azure en Azure Active Directory
**V: Waarom krijg ik 'geen abonnementen gevonden' wanneer ik probeer tooaccess Azure AD in Hallo klassieke Azure-portal?**

**A:** tooaccess Hallo klassieke Azure-portal, moet elke gebruiker machtigingen met een Azure-abonnement. Als u een betaald Office 365 of Azure AD-abonnement hebt, gaat u verder te[http://aka.ms/accessAAD](http://aka.ms/accessAAD) voor een eenmalige activeringsstap. Anders moet u een gratis tooactivate [Azure-account](https://azure.microsoft.com/pricing/free-trial/) of een betaald abonnement.

Zie voor meer informatie:

* [Hoe Azure-abonnementen worden gekoppeld aan Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* [Hallo-directory voor uw Office 365-abonnement in Azure beheren](active-directory-manage-o365-subscription.md)

- - -
**V: Wat is de relatie Hallo tussen Azure AD, Office 365 en Azure?**

**A:** Azure AD biedt u algemene identiteit en toegang tot tooall webservices. Ongeacht of u Office 365, Microsoft Azure, Intune, of anderen, u bent al gebruikmaakt van Azure AD toohelp schakelt u eenmalige aanmelding en toegang tot beheer van al deze services.

Alle gebruikers die zijn ingesteld met toouse web-services worden gedefinieerd als gebruikersaccounts in een of meer exemplaren van Azure AD. U kunt deze accounts instellen voor gratis Azure AD-functies, zoals toegang tot cloudtoepassingen.

Betaalde Azure AD-services zoals Enterprise Mobility + Security vormen een aanvulling op andere webservices, zoals Office 365 en Microsoft Azure, met uitgebreide oplossingen voor beheer en beveiliging die ook geschikt zijn voor grote organisaties.
- - -
**V: Waarom kan ik toohello Azure-portal aanmelden, maar niet Hallo klassieke Azure-portal?**

**A:** hello Azure-portal geen vereist een geldig abonnement en de klassieke portal Hallo vereist een geldig abonnement.  Als u niet een abonnement hebt, kunt u de klassieke portal toohello kan niet aanmelden.
- - -
**V: wat zijn Hallo verschillen tussen Abonnementsbeheerder en Directory-beheerder?**

**A:** standaard u Hallo abonnement beheerdersrol toegewezen wanneer u zich aanmeldt voor Azure. Een abonnementsbeheerder kunt gebruiken een Microsoft-account of een werk of schoolaccount van Hallo-map die hello Azure-abonnement is gekoppeld aan.  Deze rol is geautoriseerde toomanage services in hello Azure-portal.

Als anderen moeten toosign in en toegang tot services door met behulp van Hallo hetzelfde abonnement, kunt u deze toevoegen als medebeheerders. Deze rol Hallo heeft dezelfde toegangsrechten als de servicebeheerder hello, maar Hallo koppeling met abonnementen tooAzure mappen niet wijzigen.  Zie voor meer informatie over abonnementsbeheerders [hoe tooadd of wijzig Azure-beheerdersrollen](../billing-add-change-azure-subscription-administrator.md) en [hoe Azure-abonnementen worden gekoppeld aan Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).


Azure AD heeft een andere set admin rollen toomanage Hallo directory en identiteitsgerelateerde functies.  Deze beheerders zijn toovarious toegangsfuncties in hello Azure-portal of Hallo klassieke Azure-portal. Hallo beheerdersrol bepaalt wat ze kunnen doen, zoals het maken of bewerken van gebruikers, tooothers beheerdersrollen toewijzen, gebruikerswachtwoorden, Gebruikerslicenties beheren of domeinen beheren.  Zie [Beheerdersrollen toewijzen in Azure Active Directory](active-directory-assign-admin-roles.md) voor meer informatie over Directorybeheerders en hun rollen in Azure AD.

Daarnaast vormen betaalde Azure AD-services zoals Enterprise Mobility + Security een aanvulling op andere webservices, zoals Office 365 en Microsoft Azure, met uitgebreide oplossingen voor beheer en beveiliging die ook geschikt zijn voor grote organisaties.

- - -
**V: Is er een rapport waarin staat wanneer mijn Azure AD-gebruikerslicenties verlopen?**

**A:** Nee.  Dit is momenteel niet beschikbaar.

- - -

## <a name="get-started-with-hybrid-azure-ad"></a>Aan de slag met hybride Azure AD


**V: Hoe verlaat ik een tenant wanneer ik ben toegevoegd als samenwerker?**

**A:** wanneer u tenant van de organisatie van de tooanother worden toegevoegd als een samenwerker, kunt u Hallo 'tenant schakelbaar' in de bovenste rechts tooswitch Hallo tussen de tenants.  Op dit moment is er geen manier tooleave Hallo organisatie uitnodigen en Microsoft werkt op het bieden van deze functionaliteit.  Totdat deze functie beschikbaar is, vraagt u Hallo organisatie tooremove nodigen u uit de tenant.
- - -
**V: hoe kan ik mijn lokale directory tooAzure AD verbinden?**

**A:** uw lokale directory tooAzure AD verbinding kunnen maken met behulp van Azure AD Connect.

Zie [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md) (Uw on-premises identiteiten integreren met Azure Active Directory) voor meer informatie.

- - -
**V: Hoe stel ik eenmalige aanmelding in tussen mijn on-premises directory en mijn cloudtoepassingen?**

**A:** hoeft u alleen tooset van eenmalige aanmelding (SSO) tussen uw on-premises adreslijst en Azure AD. Als u uw cloudtoepassingen via Azure AD opent, Hallo service automatisch voor gezorgd dat uw gebruikers toocorrectly verifiëren met hun on-premises referenties.

U kunt eenmalige aanmelding eenvoudig on-premises implementeren met federatieoplossingen, zoals Active Directory Federation Services (AD FS), of door wachtwoordhashsynchronisatie te configureren. U kunt beide opties eenvoudig implementeren met behulp van de wizard hello Azure AD Connect-configuratie.

Zie [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md) (Uw on-premises identiteiten integreren met Azure Active Directory) voor meer informatie.

- - -
**V: Bevat Azure AD een selfserviceportal voor gebruikers in mijn organisatie?**

**A:** Ja, Azure AD levert u Hello [Azure AD-Toegangsvenster](http://myapps.microsoft.com) voor selfservice van gebruiker en toegang tot toepassingen. Als u een Office 365-klant bent, kunt u veel van Hallo dezelfde mogelijkheden vinden in Hallo Office 365-portal.

Zie voor meer informatie [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

- - -
**V: Helpt Azure AD mij bij het beheren van mijn on-premises infrastructuur?**

**A:** Ja. Hello Azure AD Premium-editie biedt u Azure AD Connect Health. Azure AD Connect Health kunt u controleren en meer inzicht krijgen in uw on-premises identiteits-infrastructuur en Hallo Synchronisatieservices.  

Zie voor meer informatie [uw lokale identiteit infrastructuur en de synchronisatie-services bewaken in de cloud Hallo](active-directory-aadconnect-health.md).  

- - -
## <a name="password-management"></a>Wachtwoordbeheer
**V: Kan ik Terugschrijven van wachtwoord van Azure AD gebruiken zonder wachtwoordsynchronisatie? (In dit scenario is het mogelijk toouse Azure AD selfservice voor wachtwoordherstel (SSPR) met wachtwoord terugschrijven en niet store wachtwoorden in de cloud Hallo?)**

**A:** hoeft u geen toosynchronize uw Active Directory-wachtwoorden tooAzure AD tooenable terugschrijven. In een federatieve omgeving Azure AD eenmalige aanmelding (SSO) is afhankelijk van Hallo on-premises directory tooauthenticate Hallo gebruiker. Dit scenario vereist geen Hallo lokale wachtwoord toobe bijgehouden in Azure AD.

- - -
**V: hoe lang duurt het voor een wachtwoord toobe tooActive Directory lokaal teruggeschreven?**

**A:** Het terugschrijven van het wachtwoord wordt in realtime uitgevoerd.

Zie voor meer informatie [Getting started with password management](active-directory-passwords-getting-started.md).

- - -
**V: Kan ik de functie Terugschrijven van wachtwoord gebruiken met wachtwoorden die worden beheerd door een beheerder?**

**A:** Ja, als u wachtwoord terugschrijven ingeschakeld hebt, Hallo wachtwoordbewerkingen van een beheerder teruggeschreven tooyour on-premises omgeving.  

Zie voor meer antwoorden toopassword-gerelateerde vragen [Veelgestelde vragen over wachtwoordbeheer](active-directory-passwords-faq.md).
- - -
**V: wat moet ik doen als ik mijn bestaande Office 365/Azure AD-wachtwoord tijdens een poging toochange mijn wachtwoord vergeten?**

**A:** In een dergelijke situatie zijn er meerdere oplossingen.  Gebruik selfservice voor wachtwoordherstel (SSPR) als deze optie beschikbaar is.  Of SSPR werkt, is afhankelijk van de configuratie.  Zie voor meer informatie [hoe Hallo wachtwoordherstel portal werk](active-directory-passwords-best-practices.md).

Voor Office 365-gebruikers, uw beheerder kan wachtwoord opnieuw instellen Hallo met behulp van Hallo stappen die worden beschreven in [gebruikerswachtwoorden](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).

Voor Azure AD-accounts, kunnen beheerders opnieuw instellen van wachtwoorden met behulp van een van de volgende Hallo:

- [Opnieuw instellen van accounts in hello Azure-portal](active-directory-users-reset-password-azure-portal.md)
- [Opnieuw instellen van accounts in de klassieke portal Hallo](active-directory-create-users-reset-password.md)
- [PowerShell gebruiken](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a>Beveiliging
**V: Worden accounts na een bepaald aantal mislukte pogingen vergrendeld of wordt een meer geavanceerde strategie gebruikt?**</br>
We gebruiken een meer geavanceerde strategie toolock accounts.  Dit is gebaseerd op Hallo IP-adres van Hallo-aanvraag en Hallo-wachtwoorden hebt ingevoerd. Hallo-duur van Hallo accountvergrendeling verhoogt ook op basis van Hallo kans dat het is een aanval.  

**V: bepaalde (algemene) wachtwoorden afgewezen Hello berichten 'dit wachtwoord is gebruikt toomany maal', verwijst dit toopasswords gebruikt in de huidige active directory Hallo?**</br>
Dit verwijst toopasswords die globaal gemeen hebben, zoals varianten van 'Password' en '123456'.

**V: Worden aanmeldingsaanvragen van twijfelachtige bronnen (botnets, tor-eindpunten) in een B2C-tenant geblokkeerd of is hiervoor een Basic- of Premium-tenant vereist?**</br>
We hebben wel een gateway waarmee aanvragen worden gefilterd en die enige bescherming biedt tegen botnets. Deze wordt toegepast op alle B2C-tenants.

## <a name="application-access"></a>Toegang tot toepassingen
**V: Waar vind ik een lijst met toepassingen die vooraf zijn geïntegreerd met Azure AD en de bijbehorende mogelijkheden?**

**A:** Azure AD bevat meer dan 2.600 vooraf geïntegreerde toepassingen van Microsoft, toepassingsserviceproviders en partners. Alle vooraf geïntegreerde toepassingen bieden ondersteuning voor eenmalige aanmelding (SSO). Eenmalige aanmelding kunt u uw apps voor uw organisatie referenties tooaccess gebruiken. Sommige Hallo toepassingen ondersteunen ook geautomatiseerde inrichting en de inrichting ongedaan.

Zie voor een volledige lijst met vooraf geïntegreerde toepassingen Hallo Hallo [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).

- - -
**V: Wat gebeurt er als hello App die ik nodig heeft geen hello Azure AD marketplace?**

**A:** Met Azure AD Premium kunt u elke gewenste toepassing toevoegen en configureren. U kunt eenmalige aanmelding en geautomatiseerde inrichting configureren, afhankelijk van de mogelijkheden van uw toepassing en uw voorkeuren.  

Zie voor meer informatie:

* [Eenmalige aanmelding tooapplications die zich niet in de Azure Active Directory-toepassingsgalerie Hallo configureren](active-directory-saas-custom-apps.md)
* [Met behulp van SCIM tooenable automatische inrichting van gebruikers en groepen van Azure Active Directory-tooapplications](active-directory-scim-provisioning.md)

- - -
**V: hoe gebruikers Meld tooapplications met Azure AD?**

**A:** Azure AD biedt verschillende manieren voor gebruikers tooview en toegang krijgen tot hun toepassingen, zoals:

* Hello Azure AD-Toegangsvenster
* toepassingsstartprogramma Hello Office 365
* Direct aanmelden toofederated apps
* Dieptekoppelingen toofederated, op basis van wachtwoorden of bestaande apps

Zie voor meer informatie [Deploying Azure AD integrated applications toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

- - -
**V: wat zijn Hallo verschillende manieren waarop Azure AD kunnen u de verificatie en eenmalige aanmelding tooapplications?**

**A:** Azure AD biedt ondersteuning voor een groot aantal gestandaardiseerde protocollen voor verificatie en autorisatie, zoals SAML 2.0, OpenID Connect, OAuth 2.0 en WS-Federation. Daarnaast ondersteunt Azure AD het gebruik van wachtwoordkluizen en mogelijkheden voor automatische aanmelding voor apps die alleen ondersteuning bieden voor verificatie op basis van formulieren.  

Zie voor meer informatie:

* [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md) (Verificatiescenario's voor Azure AD)
* [Verificatie- en autorisatieprotocollen](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [How does single sign-on with Azure Active Directory work?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work) (Hoe werkt eenmalige aanmelding met Azure Active Directory?)

- - -
**V: Kan ik toepassingen toevoegen die ik on-premises uitvoer?**

**A:** Azure AD-toepassingsproxy biedt eenvoudig en veilig toegang tooon-premises webtoepassingen die u kiest. U kunt toegang tot deze toepassingen in Hallo dezelfde manier als u toegang hebt tot de software als een service (SaaS)-apps in Azure AD. Er is niet nodig voor een VPN- of toochange uw netwerkinfrastructuur.  

Zie voor meer informatie [hoe tooprovide veilige externe toegang tot het tooon-premises toepassingen](active-directory-application-proxy-get-started.md).

- - -
**V: Hoe maak ik Multi-Factor Authentication verplicht voor gebruikers die toegang hebben tot een bepaalde toepassing?**

**A:** Met voorwaardelijke toegang van Azure AD kunt u een uniek toegangsbeleid toewijzen aan elke toepassing. U kunt altijd meervoudige verificatie vereisen of wanneer gebruikers niet zijn verbonden toohello lokale netwerk in uw beleid.  

Zie voor meer informatie [toegang beveiligen tooOffice 365 en andere apps tooAzure Active Directory verbonden](active-directory-conditional-access.md).

- - -
**V: Wat is geautomatiseerde gebruikersinrichting voor SaaS-apps?**

**A:** tooautomate Hallo maken, onderhoud en verwijderen van de gebruikers-id's in veel populaire cloudtoepassingen SaaS-apps met Azure AD.

Zie voor meer informatie [gebruikers inrichten en opheffen van inrichting tooSaaS toepassingen met Azure Active Directory automatiseren](active-directory-saas-app-provisioning.md).

- - -
**V: Kan ik een veilige LDAP-verbinding instellen met Azure AD?**

**A:** Nee. Azure AD biedt geen ondersteuning voor Hallo LDAP-protocol.

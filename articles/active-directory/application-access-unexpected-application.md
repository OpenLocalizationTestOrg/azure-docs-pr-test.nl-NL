---
title: aaaUnexpected toepassing in de lijst met mijn toepassingen | Microsoft Docs
description: Hoe toosee alle toepassingen in uw tenant en u begrijpt hoe toepassingen worden weergegeven in de lijst met alle toepassingen onder bedrijfstoepassingen
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a>Onverwachte toepassing in de lijst met mijn toepassingen

In dit artikel kunt u toounderstand hoe toepassingen worden weergegeven in uw **alle toepassingen** lijst onder **bedrijfstoepassingen**. 

## <a name="how-toosee-all-applications-in-your-tenant"></a>Hoe toosee alle toepassingen in uw tenant

toosee alle toepassingen in uw tenant hello, moet u toouse hello **Filter** beheren tooshow **alle toepassingen** onder Hallo **alle toepassingen** lijst. toodo deze, Hallo stappen hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

6.  Klik op Hallo gebruik Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen**.

7.  Op Hallo **Filter** blade, set Hallo **weergeven** optie te**alle toepassingen.**

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a>Waarom wordt er een specifieke toepassing weergegeven in de lijst met alle toepassingen?

Wanneer te gefilterd**alle toepassingen**, Hallo **alle toepassingen** **lijst** toont elk Service-Principal-object in uw tenant. Service-Principal-objecten kunnen worden weergegeven in deze lijst op een verschillende manieren:

1.  Wanneer u een toepassing van Hallo-toepassingsgalerie toevoegt, waaronder:

   1. **Azure AD-galerie toepassingen** : een toepassing die vooraf geïntegreerde voor eenmalige aanmelding met Azure AD is.

   2. **Application Proxy toepassingen** : een toepassing die wordt uitgevoerd in uw on-premises omgeving dat u wilt dat tooprovide beveiligde eenmalige aanmelding tooexternally.

   3. **Aangepaste ontwikkelde toepassingen** : een toepassing die uw organisatie wil toodevelop op Azure AD-ontwikkelplatform voor toepassing hello, maar die mogelijk niet bestaat.

   4. **Niet-galerie toepassingen** : Breng uw eigen toepassingen! Een webkoppeling die u wilt dat alle toepassingen die een veld de gebruikersnaam en wachtwoord SAML of OpenID Connect-protocollen ondersteunt of ondersteunt SCIM die u wenst dat toointegrate voor eenmalige aanmelding met Azure AD.

2.  Wanneer zich aanmelden voor of aanmelden bij een 3<sup>rd</sup> of een toepassing die is geïntegreerd met Azure Active Directory. Een voorbeeld hiervan is [Smartsheet](https://app.smartsheet.com/b/home) of [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).

3.  Wanneer u zich aanmelden voor of een licentie tooa gebruiker of groep tooa eerste toepassing van een leverancier toe te voegen, zoals [Microsoft Office 365](http://products.office.com/).

4.  Wanneer u de registratie van een nieuwe toepassing toevoegt door het maken van een toepassing die aangepaste zijn ontwikkeld met behulp van Hallo [toepassingsregister](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).

5.  Wanneer u de registratie van een nieuwe toepassing toevoegt door het maken van een toepassing die aangepaste zijn ontwikkeld met behulp van Hallo [V2.0-Portal voor registratie van toepassing](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).

6.  Wanneer u een toepassing toevoegen u ontwikkelt met Visual Studio [ASP.net verificatiemethoden](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) of [verbonden Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).

7.  Wanneer u een service principal-object met behulp van Hallo maakt [Azure AD PowerShell-Module](/powershell/azure/install-adv2?view=azureadps-2.0).

8.  Wanneer u [tooan toepassing toestemming](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) als een beheerder toouse gegevens in uw tenant.

9.  Wanneer een [gebruiker hiermee akkoord gaat tooan toepassing](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse gegevens in uw tenant.

10. Wanneer u bepaalde services waarmee gegevens worden opgeslagen in uw tenant inschakelen. Een voorbeeld hiervan is het wachtwoord opnieuw instellen, die is gemodelleerd als een service-principal toostore uw wachtwoord opnieuw instellen van beleid veilig.

tooget meer informatie over hoe tooyour-directory worden toegevoegd in apps Lees [hoe en waarom toepassingen tooAzure AD zijn toegevoegd](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>Ik wil tooremove dat een specifieke gebruiker of groep van toewijzing tooan toepassing

een gebruiker of groep toewijzing tooan toepassing tooremove Hallo stappen in Hallo volgen [de toewijzing van een gebruiker of groep verwijderen uit een enterprise-app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) artikel.

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a>Ik wil toodisable alle access tooan-toepassing voor elke gebruiker

toodisable alle aanmeldingen tooan Gebruikerstoepassing, volg Hallo de stappen die worden vermeld in Hallo [gebruikersaanmeldingen een enterprise-App in Azure Active Directory uitschakelen](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) artikel.

## <a name="i-want-toodelete-an-application-entirely"></a>Ik wil dat een toepassing toodelete volledig

te**verwijderen van een toepassing**, volgt u onderstaande instructies voor Hallo:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer de gewenste toodelete Hallo-toepassing.

7.  Nadat de toepassing hello wordt geladen, klikt u op **verwijderen** pictogram van Hallo bovenste toepassing **overzicht** blade.

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>Ik wil toodisable alle toekomstige toestemming operations tooany-Gebruikerstoepassing

Toestemming van de gebruiker uitschakelt voor uw hele directory voorkomen dat eindgebruikers van ermee akkoord dat tooany toepassing. Beheerders kunnen nog steeds op behalves van de gebruiker toestemming. toolearn meer informatie over de toepassing toestemming geven en waarom u kunt of wilt niet toodo, Lees [wat gebruikers- en toestemming van de beheerder](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).

te**uitschakelen alle toekomstige gebruikers toestemming bewerkingen in uw hele directory**, volgt u onderstaande instructies voor Hallo:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **gebruikersinstellingen**.

6.  Alle toekomstige gebruikers toestemming bewerkingen uitschakelen door Hallo instelling **gebruikers apps tooaccess kunnen toestaan hun gegevens** te schakelen**Nee** en klik op Hallo **opslaan** knop.

## <a name="next-steps"></a>Volgende stappen
[Toepassingen beheren met Azure Active Directory](active-directory-enable-sso-scenario.md)

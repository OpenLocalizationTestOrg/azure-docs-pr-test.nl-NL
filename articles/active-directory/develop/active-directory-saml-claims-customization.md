---
title: "aaaCustomizing uitgegeven claims in Hallo SAML-token voor vooraf geïntegreerde apps in Azure Active Directory | Microsoft Docs"
description: "Meer informatie over hoe toocustomize Hallo claims uitgegeven in Hallo SAML-token voor vooraf geïntegreerde apps in Azure Active Directory"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f1daad62-ac8a-44cd-ac76-e97455e47803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.custom: aaddev
ms.openlocfilehash: a376318929472403e799f02fdd3fbddc91d0a70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-claims-issued-in-hello-saml-token-for-pre-integrated-apps-in-azure-active-directory"></a>Uitgegeven claims aanpassen in Hallo SAML-token voor vooraf geïntegreerde apps in Azure Active Directory
Vandaag de dag duizenden vooraf geïntegreerde toepassingen in Azure Active Directory biedt ondersteuning in hello Azure AD-Toepassingsgalerie, met inbegrip van meer dan 360 die ondersteuning bieden voor eenmalige aanmelding met Hallo SAML 2.0-protocol. Wanneer een gebruiker zich tooan toepassing via Azure AD via SAML verifieert, stuurt Azure AD een token toohello-toepassing (via een HTTP POST). En vervolgens de toepassing hello valideert en Hallo token toolog Hallo gebruiker in gebruikt in plaats van naar een gebruikersnaam en wachtwoord wordt gevraagd. Deze tokens SAML bevatten stukjes informatie over Hallo gebruiker bekend als 'claims'.

In de identity-uitspreken, een "claim" is de gegevens over een id-provider over een gebruiker binnen Hallo token ze voor die gebruiker uitgeven. In [SAML-token](http://en.wikipedia.org/wiki/SAML_2.0), deze gegevens meestal is opgeslagen in Hallo SAML Attribute-instructie. Hallo wordt unieke ID van de gebruiker gewoonlijk weergegeven in Hallo die SAML-onderwerp wordt ook wel als naam-id.

Azure Active Directory geeft standaard een SAML-token tooyour-toepassing waarin een claim NameIdentifier met een waarde van Hallo de gebruikersnaam van gebruiker (UPN AKA) in Azure AD. Deze waarde kan een unieke identificatie Hallo-gebruiker. Hallo SAML-token bevat ook extra claims met e-mailadres van de gebruiker hello, voornaam en achternaam op.

tooview of bewerken Hallo claims uitgegeven in Hallo SAML-token toohello toepassing, open Hallo-toepassing in Azure-portal. Selecteer Hallo **weergeven en bewerken van alle andere gebruikerskenmerken** checkbox in Hallo **gebruikerskenmerken** sectie van de toepassing hello.

![Sectie van de kenmerken gebruiker][1]

Er zijn twee mogelijke redenen waarom u tooedit Hallo uitgegeven claims in Hallo SAML-token wellicht:
* de toepassing Hello is toorequire een andere set claim URI's of claimwaarden geschreven.
* Hallo-toepassing is geïmplementeerd op een manier die Hallo NameIdentifier claim toobe iets anders dan van Hallo gebruikersnaam (AKA UPN-naam) opgeslagen in Azure Active Directory vereist.

U kunt een van de claim standaardwaarden Hallo bewerken. Selecteer Hallo claim rij in de tabel Hallo SAML-token kenmerken. Hiermee opent u Hallo **kenmerk bewerken** sectie en u vervolgens naam van claim, de waarde en de naamruimte die is gekoppeld aan Hallo claim kunt bewerken.

![Gebruikerskenmerk bewerken][2]

U kunt ook claims (met uitzondering van NameIdentifier) met behulp van de contextmenu hello, wat wordt geopend door te klikken op Hallo verwijderen **...**  pictogram.  U kunt ook nieuwe claims op basis van Hallo toevoegen **toevoegen kenmerk** knop.

![Gebruikerskenmerk bewerken][3]

## <a name="editing-hello-nameidentifier-claim"></a>Hallo NameIdentifier claim bewerken
toosolve hello probleem waarbij de toepassing hello geïmplementeerd met behulp van een andere gebruikersnaam, klikt u op Hallo **gebruikers-id** in Hallo vervolgkeuzelijst **gebruikerskenmerken** sectie. Deze actie geeft een dialoogvenster met verschillende opties:

![Gebruikerskenmerk bewerken][4]

Selecteer in de vervolgkeuzelijst hello, **user.mail** tooset hello NameIdentifier claim toobe Hallo gebruiker e-mailadres in Hallo-directory. Of selecteer **user.onpremisessamaccountname** tooset toohello gebruiker SAM-accountnaam die zijn gesynchroniseerd vanaf lokale Azure AD.

U kunt ook speciale Hallo **ExtractMailPrefix()** functie tooremove Hallo domeinachtervoegsel van e-mailadres hello, SAM-accountnaam of Hallo UPN-naam. Dit pakt alleen het eerste deel van de gebruiker Hallo Hallo naam worden doorgegeven (bijvoorbeeld 'joe_smith' in plaats van joe_smith@contoso.com).

![Gebruikerskenmerk bewerken][5]

We hebben nu Hallo toegevoegd **join()** functie toojoin Hallo geverifieerd domein met Hallo gebruiker-id-waarde. Wanneer u Hallo join() functie selecteert in Hallo **gebruikers-id** eerst op Hallo van gebruikers-id zoals zoals e-mailadres of de gebruiker principal-naam en selecteer vervolgens in Hallo tweede vervolgkeuzelijst uw geverifieerd domein. Als u e-mailadres Hallo met Hallo geverifieerde domein selecteert, wordt Azure AD Hallo gebruikersnaam geëxtraheerd uit de eerste waarde joe_smith Hallo van joe_smith@contoso.com en voegt deze toe met contoso.onmicrosoft.com. Zie Hallo voorbeeld te volgen:

![Gebruikerskenmerk bewerken][6]

## <a name="adding-claims"></a>Claims toevoegen
Wanneer een claim toevoegen, kunt u Hallo kenmerknaam (die strikt hoeft niet toofollow een URI-patroon volgens Hallo SAML-specificatie) opgeven. Hallo tooany gebruiker kenmerkwaarde die is opgeslagen in de map Hallo ingesteld.

![Gebruikerskenmerk toevoegen][7]

U moet bijvoorbeeld toosend Hallo afdeling Hallo gebruiker behoort tooin hun organisatie als een claim (zoals Sales). Voer Hallo claimnaam zoals werd verwacht door de toepassing hello en selecteer vervolgens **user.department** Hallo-waarde.

> [!NOTE]
> Als voor een bepaalde gebruiker er geen waarde voor een geselecteerd kenmerk opgeslagen, is er geen die claim in Hallo-token wordt uitgegeven.

> [!TIP]
> Hallo **user.onpremisesecurityidentifier** en **user.onpremisesamaccountname** worden alleen ondersteund bij het synchroniseren van gebruikersgegevens van lokale Active Directory met Hallo [Azure AD Connect-hulpprogramma](../active-directory-aadconnect.md).

## <a name="restricted-claims"></a>Beperkte claims

Er zijn enkele beperkte claims in SAML. Als u deze claims toevoegt, klikt u vervolgens in Azure AD niet deze claims verzenden. Hieronder vindt u Hallo SAML claimset beperkt:

    | Claimtype (URI) |
    | ------------------- |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/Expiration |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/EXPIRED |
    | http://schemas.Microsoft.com/Identity/claims/accesstoken |
    | http://schemas.Microsoft.com/Identity/claims/openid2_id |
    | http://schemas.Microsoft.com/Identity/claims/identityprovider |
    | http://schemas.Microsoft.com/Identity/claims/objectidentifier |
    | http://schemas.Microsoft.com/Identity/claims/PUID |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/NameIdentifier [MR1] |
    | http://schemas.Microsoft.com/Identity/claims/tenantid |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/AuthenticationInstant |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/AuthenticationMethod |
    | http://schemas.Microsoft.com/AccessControlService/2010/07/claims/identityprovider |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/Groups |
    | http://schemas.Microsoft.com/claims/groups.Link |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/Role |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/wids |
    | http://schemas.Microsoft.com/2014/09/devicecontext/claims/iscompliant |
    | http://schemas.Microsoft.com/2014/02/devicecontext/claims/isknown |
    | http://schemas.Microsoft.com/2012/01/devicecontext/claims/ismanaged |
    | http://schemas.Microsoft.com/2014/03/psso |
    | http://schemas.Microsoft.com/claims/authnmethodsreferences |
    | http://schemas.xmlsoap.org/ws/2009/09/Identity/claims/actor |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/samlissuername |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/confirmationkey |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/windowsaccountname |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/primarygroupsid |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/primarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/authorizationdecision |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/Authentication |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/SID |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/denyonlyprimarygroupsid |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/denyonlyprimarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/denyonlysid |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/denyonlywindowsdevicegroup |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/windowsdeviceclaim |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/windowsdevicegroup |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/windowsfqbnversion |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/windowssubauthority |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/windowsuserclaim |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/x500distinguishedname |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/UPN |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/GroupSID |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/SPN |
    | http://schemas.Microsoft.com/ws/2008/06/Identity/claims/ispersistent |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/privatepersonalidentifier |
    | http://schemas.Microsoft.com/Identity/claims/scope |

## <a name="next-steps"></a>Volgende stappen
* [Article Index for Application Management in Azure Active Directory](../active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Eenmalige aanmelding tooapplications die zich niet in de Azure Active Directory-toepassingsgalerie Hallo configureren](../active-directory-saas-custom-apps.md)
* [Het oplossen van problemen op basis van SAML eenmalige aanmelding](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saml-claims-customization/user-attribute-section.png
[2]: ./media/active-directory-saml-claims-customization/edit-claim-name-value.png
[3]: ./media/active-directory-saml-claims-customization/delete-claim.png
[4]: ./media/active-directory-saml-claims-customization/user-identifier.png
[5]: ./media/active-directory-saml-claims-customization/extractemailprefix-function.png
[6]: ./media/active-directory-saml-claims-customization/join-function.png
[7]: ./media/active-directory-saml-claims-customization/add-attribute.png
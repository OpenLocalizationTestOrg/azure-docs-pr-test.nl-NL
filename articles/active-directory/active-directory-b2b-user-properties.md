---
title: aaaProperties van een gebruiker met Azure Active Directory B2B-samenwerking | Microsoft Docs
description: Azure Active Directory B2B-samenwerking gebruikerseigenschappen kunnen worden geconfigureerd
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 78709f64430ed4c14eadf4dc257f175c24698c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="properties-of-an-azure-active-directory-b2b-collaboration-user"></a>Eigenschappen van een gebruiker met Azure Active Directory B2B-samenwerking

Een gebruiker met samenwerking business-to-business (B2B) voor Azure Active Directory (Azure AD) is een gebruiker met UserType = Gast. Deze gastgebruiker meestal afkomstig is van een partnerorganisatie en heeft beperkte rechten in de directory, wordt standaard uitgenodigd Hallo.

Afhankelijk van Hallo die behoeften van organisatie uitnodigen, kan een gebruiker met Azure AD B2B-samenwerking in een van de volgende account statussen Hallo zijn:

- Status 1: Homed in een extern exemplaar van Azure AD en weergegeven als gastgebruiker in Hallo organisatie uitnodigen. In dit geval zich Hallo B2B gebruiker aanmeldt met een Azure AD-account die deel uitmaakt van de tenant toohello uitgenodigd. Als de partnerorganisatie Hallo geen Azure AD gebruikt, wordt nog steeds Hallo gastgebruiker in Azure AD gemaakt. Hallo-vereisten zijn dat ze gebruikmaken van hun uitnodiging en Azure AD het e-mailadres verifieert. Deze benadering wordt ook wel een just-in-time-tenancymodus (Just in time) of 'een'-tenancymodus.

- Status van 2: Homed in een Microsoft-account en weergegeven als een gastgebruiker in Hallo host organisatie. In dit geval Hallo gastgebruiker meldt zich aan met een Microsoft-account. Hallo uitgenodigd sociale identiteit van de gebruiker (google.com of vergelijkbaar), die niet is een Microsoft-account is gemaakt als een Microsoft-account tijdens inwisseling aanbieding.

- Status van 3: Homed in Hallo host organisatie lokale Active Directory en gesynchroniseerd met de Hallo host organisatie Azure AD. Bij deze release moet u PowerShell toomanually wijziging Hallo UserType van deze gebruikers in de cloud Hallo gebruiken.

- Status 4: Homed in van de organisatie van de host Azure AD met UserType = Gast en de referenties die Hallo host organisatie beheert.

  ![Hallo uitnodiging antwoorden van initialen weergeven](media/active-directory-b2b-user-properties/redemption-diagram.png)


Nu gaan we kijken hoe een gebruiker met de Azure AD B2B-samenwerking in status 1 eruit in Azure AD.

### <a name="before-invitation-redemption"></a>Voordat u een uitnodiging voor inwisseling

![Voordat de aanbieding inwisseling](media/active-directory-b2b-user-properties/before-redemption.png)

### <a name="after-invitation-redemption"></a>Na een uitnodiging voor inwisseling

![Na de aanbieding inwisseling](media/active-directory-b2b-user-properties/after-redemption.png)

## <a name="key-properties-of-hello-azure-ad-b2b-collaboration-user"></a>De sleuteleigenschappen van hello Azure AD B2B-samenwerking gebruiker
### <a name="usertype"></a>UserType
Deze eigenschap geeft Hallo relatie van Hallo gebruiker toohello host-tenancymodus. Deze eigenschap kan twee waarden hebben:
- Lid: Deze waarde geeft een werknemer van Hallo host organisatie en een gebruiker in van de organisatie Hallo salarissen. Deze gebruiker verwacht bijvoorbeeld toohave toegang krijgen tot toointernal alleen-lezen-sites. Deze gebruiker kan niet worden gezien als een externe medewerker.

- Gast: Deze waarde geeft aan dat een gebruiker die wordt niet beschouwd als interne toohello bedrijf, zoals een externe medewerker, partner, klant of dezelfde gebruiker. Een gebruiker wouldn't verwachte tooreceive worden van een Directeur interne factuur of ontvangen van de voordelen van het bedrijf, bijvoorbeeld.

  > [!NOTE]
  > Hallo UserType heeft geen relatie toohow Hallo gebruiker zich aanmeldt, een functie van de directory Hallo Hallo gebruiker, enzovoort. Deze eigenschap geeft aan van de organisatie van de gebruiker van de Hallo relatie toohello host gewoon en kan Hallo organisatie tooenforce beleidsregels die afhankelijk van deze eigenschap zijn.

### <a name="source"></a>Bron
Deze eigenschap geeft aan hoe Hallo gebruiker zich aanmeldt.

- Gebruiker uitgenodigd: Deze gebruiker heeft uitgenodigd maar een uitnodiging nog niet is gebruikt.

- Externe Active Directory: Deze gebruiker in een externe organisatie is toegewezen en verifieert met behulp van een Azure AD-account die deel uitmaakt van toohello andere organisatie. Dit type aanmelden komt overeen tooState 1.

- Microsoft-account: deze gebruiker in een Microsoft-account is homed en verifieert met behulp van een Microsoft-account. Dit type aanmelden komt overeen tooState 2.

- Windows Server Active Directory: Deze gebruiker is aangemeld vanaf de lokale Active Directory die deel uitmaakt van de organisatie toothis. Dit type aanmelden komt overeen tooState 3.

- Azure Active Directory: Deze gebruiker wordt geverifieerd met behulp van een Azure AD-account die deel uitmaakt van de organisatie toothis. Dit type aanmelden komt overeen tooState 4.
  > [!NOTE]
  > Bron- en UserType zijn onafhankelijk eigenschappen. Een waarde van de bron betekent niet dat voor een bepaalde waarde voor UserType.

## <a name="can-azure-ad-b2b-users-be-added-as-members-instead-of-guests"></a>Kunnen Azure AD B2B-gebruikers worden toegevoegd als leden in plaats van gasten?
Een Azure AD B2B-gebruiker en de gastgebruiker zijn meestal synoniem. Daarom wordt de gebruiker van een Azure AD B2B-samenwerking toegevoegd als een gebruiker met UserType Gast = standaard. In sommige gevallen is Hallo partnerorganisatie echter dat ook deel uitmaakt van een lid van een grotere organisatie toowhich Hallo host organisatie. Als dit het geval is, is het Hallo host organisatie eventueel tootreat gebruikers in de partnerorganisatie Hallo als leden in plaats van gasten. Hello Azure AD B2B uitnodiging Manager-API's tooadd gebruiken of een gebruiker vanuit Hallo organisatie toohello host partnerorganisatie als een lid uit te nodigen.

## <a name="filter-for-guest-users-in-hello-directory"></a>Filter voor gastgebruikers in Hallo directory

![Gastgebruikers filteren](media/active-directory-b2b-user-properties/filter-guest-users.png)

## <a name="convert-usertype"></a>UserType converteren
Op dit moment is is het mogelijk voor gebruikers tooconvert UserType van lid tooGuest en vice versa met behulp van PowerShell. Hallo UserType-eigenschap moet echter toorepresent Hallo gebruiker relatie toohello organisatie. Daarom moet Hallo-waarde van deze eigenschap alleen wijzigen als Hallo relatie van de organisatie Hallo gebruiker toohello wordt gewijzigd. Als de relatie van de gebruiker Hallo Hallo wijzigt, moeten problemen, zoals of Hallo UPN (user Principal name) wijzigen moet, worden opgelost? Hallo-gebruiker moet doorgaan toohave toegang toohello dezelfde bronnen? Een postvak toegewezen? Daarom niet aangeraden Hallo UserType wijzigen met behulp van PowerShell als een atomic-activiteit. Bovendien, als deze eigenschap niet-wijzigbaar wordt met behulp van PowerShell, raadzaam niet duurt een afhankelijkheid op deze waarde.

## <a name="remove-guest-user-limitations"></a>Beperkingen van Gast-gebruiker verwijderen
Mogelijk zijn er gevallen waar u toogive uw gast gebruikers hogere bevoegdheden. U kunt een gast tooany gebruikersrol toevoegen en zelfs verwijderen Hallo standaard Gast gebruikersbeperkingen in Hallo directory toogive een gebruiker Hallo dezelfde als leden toegangsrechten.

Het is mogelijk tooturn uitschakelen Gast Hallo-gebruiker standaardbeperkingen zodat gastgebruiker in de directory van het bedrijf Hallo krijgt Hallo dezelfde machtigingen als een gebruiker lid is.

![Beperkingen van Gast-gebruiker verwijderen](media/active-directory-b2b-user-properties/remove-guest-limitations.png)

## <a name="next-steps"></a>Volgende stappen

Lees ook onze andere artikelen over Azure AD B2B-samenwerking:

* [Wat is Azure AD B2B-samenwerking?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B-samenwerking tooa gebruikersrol toevoegen](active-directory-b2b-add-guest-to-role.md)
* [B2B-samenwerking uitnodigingen delegeren](active-directory-b2b-delegate-invitations.md)
* [B2B-samenwerking gebruiker controle en rapportage](active-directory-b2b-auditing-and-reporting.md)
* [Dynamische groepen en B2B-samenwerking](active-directory-b2b-dynamic-groups.md)
* [B2B-samenwerking code en PowerShell-voorbeelden](active-directory-b2b-code-samples.md)
* [SaaS-apps voor B2B-samenwerking configureren](active-directory-b2b-configure-saas-apps.md)
* [B2B-samenwerking gebruikerstokens](active-directory-b2b-user-token.md)
* [Gebruikersclaims voor B2B-samenwerking toewijzing](active-directory-b2b-claims-mapping.md)
* [Office 365 extern delen](active-directory-b2b-o365-external-user.md)
* [Huidige beperkingen voor B2B-samenwerking](active-directory-b2b-current-limitations.md)

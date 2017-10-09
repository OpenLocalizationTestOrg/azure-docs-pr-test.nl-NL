---
title: apps voor Azure AD aaaDevelop | Microsoft-Docs
description: In dit artikel bevat voor IT-professionals Hallo geschreven, richtlijnen voor het Azure-toepassingen integreren met Active Directory.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a>Line-of-business-apps ontwikkelen voor Azure Active Directory
Deze handleiding biedt een overzicht van de line-of-business (LoB) toepassingen ontwikkelt voor Azure Active Directory (AD) .hello bedoeld doelgroep is globale beheerders Active Directory/Office 365.

## <a name="overview"></a>Overzicht
Maken van toepassingen die zijn geïntegreerd met Azure AD geeft gebruikers in uw organisatie eenmalige aanmelding met Office 365. Hallo-toepassing hebben in Azure AD-hebt die u meer controle over Hallo verificatiebeleid voor de toepassing hello. meer informatie over voorwaardelijke toegang en hoe tooprotect apps met multi-factor authentication (MFA) zien toolearn [toegangsregels configureren](active-directory-conditional-access-azuread-connected-apps.md).

Uw toepassing toouse Azure Active Directory registreren. Registreren van de toepassing hello betekent dat de ontwikkelaars kunnen gebruikers van Azure AD-tooauthenticate gebruiken en toegang toouser resources zoals e-mail, agenda en documenten aanvragen.

Elk lid van uw directory (niet gasten) kunt u registreert een toepassing, ook bekend als *maken van een toepassingsobject*.

Registreren van een toepassing, kunt een gebruiker toodo Hallo aanleiding:

* Een identiteit voor de toepassing die Azure AD herkent ophalen
* Een of meer geheimen/sleutels die toepassing hello tooauthenticate zelf kunt gebruiken tooAD
* Merk Hallo toepassing in hello Azure-portal met een aangepaste naam, het logo, enzovoort.
* Toepassen van Azure AD autorisatie functies tootheir-app, met inbegrip van:

  * RBAC (op rollen gebaseerd toegangsbeheer)
  * Azure Active Directory als oAuth-autorisatie-server (een API die worden weergegeven door de toepassing hello beveiligen)
* Declareren vereiste machtigingen nodig zijn voor Hallo toepassing toofunction zoals verwacht, waaronder:

      - App-machtigingen (alleen globale beheerders). Bijvoorbeeld: lidmaatschap van een andere Azure AD-toepassing of rol lidmaatschap relatieve tooan Azure Resource, resourcegroep, de rol- of -abonnement
      - Gedelegeerde machtigingen (een willekeurige gebruiker). Bijvoorbeeld: Azure AD, aanmelden en profiel lezen

> [!NOTE]
> Standaard kan een lid registreert een toepassing. hoe toorestrict machtigingen voor het registreren van toepassingen toospecific leden, Zie toolearn [hoe toepassingen tooAzure AD zijn toegevoegd](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).
>
>

Dit is wat u, de globale beheerder hello, moeten toodo toohelp ontwikkelaars ervoor dat de toepassing gereed voor productie:

* Toegangsregels (toegang beleid/MFA) configureren
* Hallo app toorequire Gebruikerstoewijzing configureren en toewijzen van gebruikers
* Hallo standaard gebruikerservaring toestemming onderdrukken

## <a name="configure-access-rules"></a>Toegangsregels configureren
Configureer regels tooyour SaaS-apps toegang per toepassing. U kunt bijvoorbeeld MFA vereisen of dat alleen toegang toousers in vertrouwde netwerken. Hallo-details voor deze zijn beschikbaar in Hallo document [toegangsregels configureren](active-directory-conditional-access-azuread-connected-apps.md).

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a>Hallo app toorequire Gebruikerstoewijzing configureren en toewijzen van gebruikers
Standaard kunnen gebruikers toepassingen openen zonder dat wordt toegewezen. Als de toepassing hello beschrijft de functies of als u Hallo toepassing tooappear op toegangspaneel voor een gebruiker wilt, moet u de Gebruikerstoewijzing van de instellen.

[Gebruikerstoewijzing vereisen](active-directory-applications-guiding-developers-requiring-user-assignment.md)

Als u een Azure AD Premium of Enterprise Mobility Suite (EMS)-abonnee bent, wordt aangeraden met behulp van groepen. Toewijzen van groepen toohello toepassing kunt u toodelegate lopende access management toohello eigenaar van Hallo-groep. U kunt Hallo groep maken of vraag Hallo verantwoordelijke partij in uw organisatie toocreate Hallo groep met behulp van de groep management-functie.

[Toewijzen van gebruikers tooan toepassing](active-directory-applications-guiding-developers-assigning-users.md)  
[Toewijzen van groepen tooan toepassing](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a>Onderdrukken van toestemming van de gebruiker
Elke gebruiker doorloopt een toosign toestemming ervaring in standaard. Hallo zijn toestemming, waarin gebruikers toogrant machtigingen tooan toepassing, toegevoegd voor gebruikers die niet bekend bent met dergelijke beslissingen.

Voor toepassingen die u vertrouwt, kunt u Hallo gebruikerservaring vereenvoudigen door ermee akkoord dat toohello toepassing namens uw organisatie.

Voor meer informatie over de toestemming van de gebruiker en Hallo toestemming ervaring in Azure, Zie [toepassingen integreren met Azure Active Directory](active-directory-integrating-applications.md).

## <a name="related-articles"></a>Verwante artikelen
* [Veilige externe toegang tooon-premises toepassingen met Azure AD-toepassingsproxy inschakelen](active-directory-application-proxy-get-started.md)
* [Voorwaardelijke toegang tot Azure Preview voor SaaS-Apps](active-directory-conditional-access-azuread-connected-apps.md)
* [Het beheren van toegang tooapps met Azure AD](active-directory-managing-access-to-apps.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)

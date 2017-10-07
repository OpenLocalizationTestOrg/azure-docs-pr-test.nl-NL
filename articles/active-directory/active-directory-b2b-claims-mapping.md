---
title: aaaB2B samenwerking gebruikersclaims toewijzen in Azure Active Directory | Microsoft Docs
description: claims toewijzing verwijzing voor Azure Active Directory B2B-samenwerking
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a>B2B-samenwerking gebruikersclaims toewijzen in Azure Active Directory

Azure Active Directory (Azure AD) ondersteunt Hallo uitgegeven claims in Hallo SAML-token voor B2B-samenwerking gebruikers aanpassen. Als een gebruiker zich toohello toepassing verifieert, geeft Azure AD een SAML-token toohello-app met informatie (of claims) over Hallo-gebruiker die uniek wordt geïdentificeerd. Dit omvat standaard gebruikersnaam, e-mailadres, voornaam en achternaam op Hallo van de gebruiker. U kunt weergeven of bewerken Hallo claims in Hallo SAML-token toohello toepassing hello kenmerken tabblad verzonden.

Er zijn twee mogelijke redenen waarom u tooedit Hallo uitgegeven claims in Hallo SAML-token wellicht.

1. Hallo-toepassing is geschreven toorequire een andere set claim URI's of claimwaarden

2. Uw toepassing vereist Hallo NameIdentifier claim toobe iets anders dan Hallo UPN opgeslagen in Azure Active Directory.

  ![weergave claims in SAML-token](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

Raadpleeg voor informatie over hoe claims van tooadd en bewerken, in dit artikel op claims aanpassing, [uitgegeven claims in Hallo SAML-token voor vooraf geïntegreerde apps in Azure Active Directory aanpassen](develop/active-directory-saml-claims-customization.md). Voor B2B-samenwerking, gebruikers, toewijzing NameID en UPN cross-tenant worden uit veiligheidsoverwegingen voorkomen.


## <a name="next-steps"></a>Volgende stappen

Lees ook onze andere artikelen over Azure AD B2B-samenwerking:

* [Wat is Azure AD B2B-samenwerking?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Gebruikerseigenschappen B2B-samenwerking](active-directory-b2b-user-properties.md)
* [B2B-samenwerking tooa gebruikersrol toevoegen](active-directory-b2b-add-guest-to-role.md)
* [B2bB samenwerking uitnodigingen delegeren](active-directory-b2b-delegate-invitations.md)
* [Dynamische groepen en B2B-samenwerking](active-directory-b2b-dynamic-groups.md)
* [B2B-samenwerking code en PowerShell-voorbeelden](active-directory-b2b-code-samples.md)
* [SaaS-apps voor B2B-samenwerking configureren](active-directory-b2b-configure-saas-apps.md)
* [Office 365 extern delen](active-directory-b2b-o365-external-user.md)
* [B2B-samenwerking gebruikerstokens](active-directory-b2b-user-token.md)
* [Huidige beperkingen voor B2B-samenwerking](active-directory-b2b-current-limitations.md)

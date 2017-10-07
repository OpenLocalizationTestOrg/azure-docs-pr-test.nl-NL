---
title: aaaLimitations van Azure Active Directory B2B-samenwerking | Microsoft Docs
description: Huidige beperkingen voor Azure Active Directory B2B-samenwerking
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a>Beperkingen van Azure AD B2B-samenwerking
Azure Active Directory (Azure AD) B2B-samenwerking is momenteel onderwerp toohello beperkingen die in dit artikel worden beschreven.

## <a name="possible-double-multi-factor-authentication"></a>Mogelijke dubbele multi-factor authentication-server
Met Azure AD B2B, kunt u multi-factor authentication op Hallo bronorganisatie (hello organisatie uitnodigen) afdwingen. Hallo redenen voor deze benadering zijn aangegeven in [voorwaardelijke toegang voor gebruikers voor B2B-samenwerking](active-directory-b2b-mfa-instructions.md). Als een partner heeft al een multi-factorauthenticatie ingesteld en afgedwongen, hun gebruikers wellicht tooperform Hallo verificatie eenmaal binnen hun organisatie thuis en vervolgens opnieuw in jouw e-mailadres.

## <a name="instant-on"></a>Instant op
In Hallo B2B-samenwerking flows we gebruikers toohello map toevoegen en ze dynamisch bijwerken tijdens uitnodiging inwisseling en app-toewijzing. Hallo-updates- en schrijfbewerkingen normaal gebeuren in een directory-exemplaar en in alle exemplaren moeten worden gerepliceerd. Replicatie is voltooid zodra alle exemplaren worden bijgewerkt. Soms wanneer Hallo-object wordt geschreven of bijgewerkt in één exemplaar en Hallo aanroepen tooretrieve dit object is tooanother exemplaar, replicatielatentie kunnen zich voordoen. Als dat gebeurt, vernieuw of probeer toohelp. Als u een app met onze API en klik vervolgens op nieuwe pogingen met enkele schrijft back-off is een goede, defensive practice tooalleviate dit probleem.

## <a name="next-steps"></a>Volgende stappen

Lees ook onze andere artikelen over Azure AD B2B-samenwerking:

* [Wat is Azure AD B2B-samenwerking?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Gebruikerseigenschappen B2B-samenwerking](active-directory-b2b-user-properties.md)
* [B2B-samenwerking tooa gebruikersrol toevoegen](active-directory-b2b-add-guest-to-role.md)
* [B2bB samenwerking uitnodigingen delegeren](active-directory-b2b-delegate-invitations.md)
* [Dynamische groepen en B2B-samenwerking](active-directory-b2b-dynamic-groups.md)
* [B2B-samenwerking code en PowerShell-voorbeelden](active-directory-b2b-code-samples.md)
* [SaaS-apps voor B2B-samenwerking configureren](active-directory-b2b-configure-saas-apps.md)
* [B2B-samenwerking gebruikerstokens](active-directory-b2b-user-token.md)
* [Gebruikersclaims voor B2B-samenwerking toewijzing](active-directory-b2b-claims-mapping.md)
* [Office 365 extern delen](active-directory-b2b-o365-external-user.md)

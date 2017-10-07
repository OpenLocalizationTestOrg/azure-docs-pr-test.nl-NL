---
title: aaaDynamic groepen en Azure Active Directory B2B-samenwerking | Microsoft Docs
description: Azure Active Directory B2B-samenwerking kan met Azure AD-dynamische groepen worden gebruikt
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
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a>Dynamische groepen en Azure Active Directory B2B-samenwerking

## <a name="what-are-dynamic-groups"></a>Wat zijn dynamische groepen?
Dynamische configuratie van de beveiligingsgroep voor Azure Active Directory (Azure AD) is beschikbaar in [hello Azure-portal](https://portal.azure.com). Beheerders kunnen regels toopopulate groepen die zijn gemaakt in Azure Active Directory op basis van gebruikerskenmerken (zoals userType, afdeling of land) instellen. Leden kunnen automatisch worden toegevoegd tooor verwijderd uit een beveiligingsgroep op basis van hun kenmerken. Deze groepen kunnen toegang bieden tooapplications of -cloud-bronnen (SharePoint-sites, documenten) en tooassign toomembers licenties. Meer informatie over dynamische groepen in [groepen in Azure Active Directory-specifieke](active-directory-accessmanagement-dedicated-groups.md).

Hallo juiste [Azure AD Premium-P1 of P2 licentieverlening](https://azure.microsoft.com/pricing/details/active-directory/) is vereist toocreate en gebruik dynamische groepen. Meer informatie artikel Hallo [op kenmerken gebaseerde regels maken voor dynamisch lidmaatschap in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).

## <a name="what-are-hello-built-in-dynamic-groups"></a>Wat zijn de ingebouwde dynamische groepen Hallo?
Hallo **alle gebruikers** kunnen dynamische groep tenant admins toocreate een groep met alle gebruikers in het Hallo-tenant met één klik. Standaard Hallo **alle gebruikers** groep bevat alle gebruikers in Hallo directory, inclusief leden en gastbesturingssystemen.
Binnen Hallo nieuwe Azure Active Directory-beheerportal, kunt u tooenable hello **alle gebruikers** groep in Hallo groepsinstellingen weergeven.

![ingebouwde groepen](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a>Hardening Hallo dynamische groep voor alle gebruikers
Standaard Hallo **alle gebruikers** groep bevat uw B2B-samenwerking (Gast) gebruikers ook. U kunt verder te beveiligen, uw **alle gebruikers** groeperen met behulp van een regel tooremove-gastgebruikers. Hallo volgende afbeelding ziet u Hallo **alle gebruikers** groep Gasten tooexclude is gewijzigd.

![groep alle gebruikers inschakelen](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

Ook het wellicht handig toocreate een nieuwe dynamische groep waarin alleen gastgebruikers, zodat u beleid (zoals Azure AD voorwaardelijk toegangsbeleid) toothem kunt toepassen.
Wat zo'n groep als volgt uitzien:

![gastgebruikers uitsluiten](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a>Volgende stappen

Lees ook onze andere artikelen over Azure AD B2B-samenwerking:

* [Wat is Azure AD B2B-samenwerking?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Gebruikerseigenschappen B2B-samenwerking](active-directory-b2b-user-properties.md)
* [B2B-samenwerking tooa gebruikersrol toevoegen](active-directory-b2b-add-guest-to-role.md)
* [B2B-samenwerking uitnodigingen delegeren](active-directory-b2b-delegate-invitations.md)
* [B2B-samenwerking code en PowerShell-voorbeelden](active-directory-b2b-code-samples.md)
* [SaaS-apps voor B2B-samenwerking configureren](active-directory-b2b-configure-saas-apps.md)
* [B2B-samenwerking gebruikerstokens](active-directory-b2b-user-token.md)
* [Gebruikersclaims voor B2B-samenwerking toewijzing](active-directory-b2b-claims-mapping.md)
* [Office 365 extern delen](active-directory-b2b-o365-external-user.md)
* [Huidige beperkingen voor B2B-samenwerking](active-directory-b2b-current-limitations.md)

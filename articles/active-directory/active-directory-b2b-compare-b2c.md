---
title: aaaCompare B2B-samenwerking en B2C in Azure Active Directory | Microsoft Docs
description: Wat is Hallo verschil tussen Azure Active Directory B2B-samenwerking en Azure AD B2C?
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
ms.openlocfilehash: 34d88b9a7d023e077568e8df3d5e1610ae05b361
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="compare-b2b-collaboration-and-b2c-in-azure-active-directory"></a>Vergelijk B2B-samenwerking en B2C in Azure Active Directory

Zowel Azure Active Directory (Azure AD) B2B-samenwerking en Azure AD B2C kunt u toowork met externe gebruikers in Azure AD. Maar hoe vergelijk ze?


Mogelijkheden voor B2B-samenwerking |     Azure AD B2C zelfstandige aanbieding
-------- | --------
Bedoeld voor: organisaties die toobe tooauthenticate kunnen gebruikers van een andere organisatie, ongeacht de id-provider willen. | Bedoeld voor: uitnodigen klanten van uw mobiele apparaat en web-apps, of personen, institutionele of zakelijke klanten in uw Azure AD.
Identiteiten die worden ondersteund: werknemers met een werk- of schoolaccounts, samen met een werk-of schoolaccounts of elk e-mailadres. Snel toosupport direct federation.  | Identiteiten die worden ondersteund: Consumer gebruikers met lokale toepassing accounts (een e-adres of groepsnaam) of een ondersteund sociale identiteit met directe Federatie.
Die een directory Hallo partner-gebruikers hebben: Partner gebruikers van Hallo externe organisatie worden beheerd in dezelfde map als werknemers, maar aantekeningen speciaal Hallo. Deze kunnen worden beheerd hello dezelfde manier als werknemers, kunnen worden toegevoegd toohello dezelfde groepen, enzovoort  | Die directory Hallo klant gebruiker entiteiten: In de toepassingsmap Hallo. Afzonderlijk beheerd vanaf Hallo directory van de organisatie werknemer en partner (indien aanwezig.
Eenmalige aanmelding (SSO) tooall Azure AD verbonden apps wordt ondersteund. U kunt bijvoorbeeld toegang tooOffice 365 of lokale apps en tooother SaaS-apps zoals Salesforce of Workday opgeven.  |  Eenmalige aanmelding toocustomer eigendom apps in Azure AD B2C Hallo tenants wordt ondersteund. Eenmalige aanmelding tooOffice 365 of tooother Microsoft en Microsoft SaaS-apps wordt niet ondersteund.
De levenscyclus van de partner: beheerd door Hallo organisatie host/uitgenodigd.  | De levenscyclus van de klant: eigen beheer of beheerd door de toepassing hello.
Beveiligingsbeleid en naleving: beheerd door Hallo organisatie host/uitgenodigd.  | Beveiligingsbeleid en naleving: beheerd door de toepassing hello.
De huisstijl: Merk van Host/uitgenodigd organisatie wordt gebruikt.  |    De huisstijl: Beheerd door de toepassing. Doorgaans doorgaans toobe product huisstijl met Hallo organisatie geleidelijk in Hallo achtergrond.
Meer informatie: [blogbericht](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/), [documentatie](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)  | Meer informatie: [productpagina](https://azure.microsoft.com/en-us/services/active-directory-b2c/), [documentatie](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)


### <a name="next-steps"></a>Volgende stappen

Lees ook onze andere artikelen over Azure AD B2B-samenwerking:

* [Wat is Azure AD B2B-samenwerking?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Gebruikerseigenschappen B2B-samenwerking](active-directory-b2b-user-properties.md)
* [B2B-samenwerking tooa gebruikersrol toevoegen](active-directory-b2b-add-guest-to-role.md)
* [B2B-samenwerking uitnodigingen delegeren](active-directory-b2b-delegate-invitations.md)
* [Dynamische groepen en B2B-samenwerking](active-directory-b2b-dynamic-groups.md)
* [SaaS-apps voor B2B-samenwerking configureren](active-directory-b2b-configure-saas-apps.md)
* [B2B-samenwerking gebruikerstokens](active-directory-b2b-user-token.md)
* [Gebruikersclaims voor B2B-samenwerking toewijzing](active-directory-b2b-claims-mapping.md)
* [Office 365 extern delen](active-directory-b2b-o365-external-user.md)
* [Huidige beperkingen voor B2B-samenwerking](active-directory-b2b-current-limitations.md)
* [Ondersteuning krijgen voor B2B-samenwerking](active-directory-b2b-support.md)

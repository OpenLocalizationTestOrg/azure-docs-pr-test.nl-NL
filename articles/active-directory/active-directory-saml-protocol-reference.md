---
title: naslaginformatie over AD SAML-Protocol aaaAzure | Microsoft Docs
description: "Dit artikel bevat een overzicht van Hallo eenmalige aanmelding en één Sign-Out SAML-profielen in Azure Active Directory."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 88125cfc-45c1-448b-9903-a629d8f31b01
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.openlocfilehash: d540b8cd9352e3196a0f4a40f0070d0e61127bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# Hoe Hallo SAML-protocol maakt gebruik van Azure Active Directory
Azure Active Directory (Azure AD) gebruikt Hallo SAML 2.0-protocol tooenable toepassingen tooprovide een eenmalige aanmelding ervaring tootheir-gebruikers. Hallo [Single Sign-On](active-directory-single-sign-on-protocol-reference.md) en [één Afmelden](active-directory-single-sign-out-protocol-reference.md) SAML-profielen van Azure AD wordt uitgelegd hoe SAML asserties, protocollen en bindingen worden gebruikt in het Hallo-id-provider-service.

SAML-Protocol moet Hallo-identiteitsprovider (Azure AD) en Hallo serviceprovider (toepassing hello) tooexchange informatie over zichzelf.

Wanneer een toepassing wordt geregistreerd bij Azure AD, registreert app-ontwikkelaar Hallo federation-gerelateerde informatie met Azure AD. Dit omvat Hallo **omleidings-URI** van Hallo-toepassing.

Azure Active Directory wordt tenantspecifieke en algemene (tenant-onafhankelijk) eenmalige aanmelding en één afmelden eindpunten. Deze URL's vertegenwoordigen adresseerbare locaties--ze zijn niet alleen een id's--zodat u toohello eindpunt tooread Hallo metagegevens kunt gaan.

* Hallo tenantspecifieke eindpunt bevindt zich op `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.  Hallo <TenantDomainName> tijdelijke aanduiding voor een geregistreerde domeinnaam of TenantID GUID van een Azure AD-tenant vertegenwoordigt. Hallo federatiemetagegevens van de tenant van Hallo contoso.com is bijvoorbeeld op: https://login.microsoftonline.com/contoso.com/FederationMetadata/2007-06/FederationMetadata.xml

* Hallo Tenant-onafhankelijke eindpunt bevindt zich op `https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml`. In dit eindpuntadres **algemene** wordt weergegeven, in plaats van een tenant domeinnaam of -ID.

Zie voor meer informatie over Hallo Federatiemetagegevens documenten die Azure AD worden gepubliceerd [Federatiemetagegevens](active-directory-federation-metadata.md).

---
title: aaaSelf-registratie serviceportal voor Azure Active Directory B2B-samenwerking | Microsoft Docs
description: Azure Active Directory B2B-samenwerking ondersteunt uw externe bedrijfsrelaties door zakelijke partners tooselectively toegang tot uw zakelijke toepassingen inschakelen
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a>Self-service portal voor Azure AD B2B-samenwerking aanmelding

Klanten kunnen veel doen met Hallo ingebouwde functies die beschikbaar worden gesteld via onze IT-beheerder [Azure-portal](https://portal.azure.com) en onze [toepassing Toegangsvenster](https://myapps.microsoft.com) voor eindgebruikers. Maar er zijn ook op de hoogte dat bedrijven toocustomize Hallo onboarding werkstroom voor B2B gebruikers toofit de behoeften van hun organisatie moeten. Ze kunnen doen dat met [onze API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).

In als u discussies met onze klanten zien we een gemeenschappelijke nodig toename up boven alle andere gebruikers. Hallo organisatie uitnodigen kan niet van tevoren weet die Hallo afzonderlijke externe deelnemers zijn die bronnen tootheir moet gebruiken. Ze wilden een manier voor gebruikers van partnerbedrijven te registreren zichzelf met een reeks beleidsregels die Hallo besturingselementen organisatie uitnodigen. Dit scenario is mogelijk via onze API's, zodat we een project op Github die u zojuist hebt die is gepubliceerd: [Github-voorbeeldproject](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).

Onze Github-project wordt gedemonstreerd hoe organisaties kunnen onze API's gebruiken en bieden een aanmelding op basis van beleid, selfservice-functie voor hun vertrouwde partners, met regels die bepalen Hallo apps die toegang te krijgen tot. Partner gebruikers tooresources toegang kunnen krijgen als ze nodig hebben, veilig, zonder Hallo vrijgeven toomanually organisatie uitnodigen ze. U kunt eenvoudig hello project implementeren in een Azure-abonnement van uw keuze.

## <a name="as-is-code"></a>Als-code

Houd er rekening mee dat deze code als een toodemonstrate voorbeeldgebruik van hello Azure Active Directory B2B uitnodiging API beschikbaar wordt gemaakt. Deze moet worden aangepast door uw team dev of een partner en moet worden gecontroleerd voordat ze worden geïmplementeerd in een productiescenario.

## <a name="next-steps"></a>Volgende stappen

Lees ook onze andere artikelen over Azure AD B2B-samenwerking:
* [Wat is Azure AD B2B-samenwerking?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Hoe voeg beheerders van Azure Active Directory B2B-samenwerking gebruikers?](active-directory-b2b-admin-add-users.md)
* [Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen](active-directory-b2b-iw-add-users.md)
* [Hallo-elementen van Hallo uitnodigingsmail voor B2B-samenwerking](active-directory-b2b-invitation-email.md)
* [B2B-samenwerking uitnodiging inwisseling](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B-samenwerking licentieverlening](active-directory-b2b-licensing.md)
* [Het oplossen van Azure Active Directory B2B-samenwerking](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B-samenwerking Veelgestelde vragen (FAQ)](active-directory-b2b-faq.md)
* [Multi-Factor Authentication voor gebruikers van B2B-samenwerking](active-directory-b2b-mfa-instructions.md)
* [B2B-samenwerking gebruikers zonder een uitnodiging toevoegen](active-directory-b2b-add-user-without-invite.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
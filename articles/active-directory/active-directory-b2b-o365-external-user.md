---
title: aaaOffice 365 extern delen en Azure Active Directory B2B-samenwerking | Microsoft Docs
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a>Extern delen van Office 365 en Azure Active Directory B2B-samenwerking

Extern delen in Office 365 (OneDrive, SharePoint Online, uniforme, groepen, enz.) en Azure Active Directory (Azure AD) B2B collaboration zijn technisch Hallo dezelfde ding. Alle extern delen (met uitzondering van OneDrive/SharePoint Online), inclusief gasten in Office 365-groepen, al hello Azure AD B2B-samenwerking uitnodiging API's gebruikt voor het delen.

OneDrive/SharePoint Online heeft een uitnodiging voor een afzonderlijke-manager. Ondersteuning voor extern delen in OneDrive/SharePoint Online gestart voordat de ondersteuning die Azure AD zijn ontwikkeld. Na verloop van tijd OneDrive/SharePoint Online extern delen, is enkele functies samengevoegd en veel miljoenen gebruikers die werken met Hallo product van de ingebouwde patroon delen. Er zijn echter enkele subtiele verschillen tussen hoe extern delen OneDrive/SharePoint Online werkt en de werking van Azure AD B2B-samenwerking:

- OneDrive/SharePoint Online voegt gebruikers toohello directory nadat gebruikers hebben hun uitnodigingen ingewisseld. Dus voordat inwisseling er geen Hallo-gebruiker in Azure AD-portal. Als een andere site tussentijd een gebruiker in hello nodigt, wordt een uitnodiging voor een nieuwe gegenereerd. Wanneer u Azure AD B2B-samenwerking, worden gebruikers echter toegevoegd onmiddellijk op uitnodiging zodat ze overal worden weergegeven.

- Hallo inwisseling ervaring in OneDrive/SharePoint Online er anders uit Hallo ervaring in Azure AD B2B-samenwerking. Nadat een gebruiker een uitnodiging wordt ingewisseld, lijken Hallo ervaringen.

- Azure AD B2B-samenwerking uitgenodigd gebruikers kunnen worden verzameld van OneDrive/SharePoint Online-dialoogvensters voor delen. OneDrive/SharePoint Online uitgenodigd gebruikers ook weergegeven in Azure AD wanneer ze hun uitnodigingen inwisselen.

- externe toomanage delen in OneDrive/SharePoint Online met Azure AD B2B-samenwerking ingesteld Hallo OneDrive/SharePoint Online extern delen te stellen**dat alleen delen met externe gebruikers al in de map Hallo**. Gebruikers kunnen gaan tooexternally gedeelde sites en kiezen uit externe deelnemers die Hallo beheerder is toegevoegd. Hallo beheerder kan Hallo externe deelnemers via Hallo B2B-samenwerking uitnodiging API's kunt toevoegen.

![Hallo extern delen instelling OneDrive/SharePoint Online](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a>Volgende stappen

Lees ook onze andere artikelen over Azure AD B2B-samenwerking:

* [Wat is Azure AD B2B-samenwerking?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Gebruikerseigenschappen B2B-samenwerking](active-directory-b2b-user-properties.md)
* [B2B-samenwerking tooa gebruikersrol toevoegen](active-directory-b2b-add-guest-to-role.md)
* [B2B-samenwerking uitnodigingen delegeren](active-directory-b2b-delegate-invitations.md)
* [Dynamische groepen en B2B-samenwerking](active-directory-b2b-dynamic-groups.md)
* [B2B-samenwerking code en PowerShell-voorbeelden](active-directory-b2b-code-samples.md)
* [SaaS-apps voor B2B-samenwerking configureren](active-directory-b2b-configure-saas-apps.md)
* [B2B-samenwerking gebruikerstokens](active-directory-b2b-user-token.md)
* [Gebruikersclaims voor B2B-samenwerking toewijzing](active-directory-b2b-claims-mapping.md)
* [Huidige beperkingen voor B2B-samenwerking](active-directory-b2b-current-limitations.md)

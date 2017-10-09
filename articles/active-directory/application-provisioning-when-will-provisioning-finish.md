---
title: aaaUser tooan Azure AD-galerie toepassing inrichting is nemen uur of langer | Microsoft Docs
description: Hoe toofind uit waarom inrichting tooyour toepassing langer dan u duurt verwacht
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a>Gebruikers inrichten tooan Azure AD-galerie toepassing is nemen uur of meer

Tijdens het inschakelen van automatische inrichting voor een toepassing, kan de initiële synchronisatie Hallo duren van 20 minuten tooseveral uren, afhankelijk van de grootte Hallo van hello Azure AD-directory en Hallo aantal gebruikers in het bereik voor het inrichten. 

Volgende synchronisaties na de initiële synchronisatie Hallo niet sneller als Hallo-service inricht watermerken waarbij Hallo status van beide systemen na de initiële synchronisatie hello, verbeterde prestaties van de volgende synchronisatie worden opgeslagen.

## <a name="how-tooimprove-provisioning-performance"></a>Hoe tooimprove prestaties inrichten

Als de initiële synchronisatie Hallo meer dan een paar uur duurt is, is er één dat u tooimprove prestaties kunt doen:

-   **Gebruiker het bereik van de filters.** Bereik filters kunt u toofine afstemmen Hallo gegevens die Hallo inrichting service uitgepakt vanuit Azure AD door het filteren van gebruikers op basis van specifieke kenmerkwaarden. Zie voor meer informatie over het bereikfilters [inrichten van toepassing op basis van kenmerken met bereikfilters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).

## <a name="next-steps"></a>Volgende stappen
[Automatisch gebruikers inrichten en Deprovisioning tooSaaS toepassingen met Azure Active Directory](active-directory-saas-app-provisioning.md)


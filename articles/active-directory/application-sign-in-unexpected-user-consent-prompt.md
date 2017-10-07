---
title: instemmingsprompt aaaUnexpected tijdens het aanmelden tooan toepassing | Microsoft Docs
description: "Hoe tootroubleshoot wanneer een gebruiker een toestemming wordt gevraagd een toepassing ziet hebt geïntegreerd met Azure AD die u niet verwacht"
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
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a>Als u zich aanmeldt tooan toepassing onverwachte instemmingsprompt

Veel toepassingen die zijn geïntegreerd met Azure Active Directory vereisen machtigingen toovarious bronnen in de volgorde toorun. Wanneer u deze resources zijn ook worden geïntegreerd met Azure Active Directory, toestemming machtigingen tooaccess deze wordt aangevraagd met behulp van Azure AD Hallo framework. 

Dit resulteert in een instemmingsprompt wordt weergegeven Hallo eerst die een toepassing wordt gebruikt, die vaak is een eenmalige bewerking. 

## <a name="scenarios-in-which-users-see-consent-prompts"></a>Scenario's waarin gebruikers zien toestemming vragen

Aanvullende prompts kunnen worden verwacht in verschillende scenario's:

* Hallo reeks machtigingen die vereist zijn door de toepassing hello zijn gewijzigd.

* Hallo-gebruiker die oorspronkelijk ingestemd toohello toepassing is niet een beheerder en het nu een andere (niet-beheerders) gebruiker gebruikt Hallo-toepassing voor Hallo eerst.

* Hallo-gebruiker die oorspronkelijk ingestemd toohello toepassing is een beheerder, maar ze niet namens de hele organisatie Hallo toestemming.

* wordt gebruikt door de toepassing Hello [incrementele en dynamische toestemming](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest aanvullende machtigingen nadat toestemming in eerste instantie is verleend. Dit wordt vaak gebruikt als optionele functies van een toepassing extra machtigingen die vereist is voor basisfunctionaliteit niet vereist.

* Toestemming is ingetrokken na in eerste instantie wordt verleend.

* Hallo developer Hallo toepassing toorequire een prompt toestemming heeft geconfigureerd telkens wanneer deze wordt gebruikt (Opmerking: dit is niet aanbevolen).

## <a name="next-steps"></a>Volgende stappen

-   [Apps, machtigingen en toestemming in Azure Active Directory (v1.0 eindpunt)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [Scopes, machtigingen en toestemming in hello Azure Active Directory (v2.0-eindpunt)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)



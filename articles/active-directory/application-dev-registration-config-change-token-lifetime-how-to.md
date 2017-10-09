---
title: aaaHow toochange Hallo token levensduur standaardwaarden voor een toepassing ontwikkelde aangepaste | Microsoft Docs
description: Hoe tooupdate levensduur van Token beleidsregels voor uw toepassing die u voor Azure AD ontwikkelt
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
ms.openlocfilehash: 6e1aa1f2a7c33c1f55c5fb619c618ad43cd96273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a>Hoe toochange Hallo levensduur van token voor een toepassing ontwikkelde aangepaste standaardinstellingen

Azure AD Premium kunt app-ontwikkelaars en tenant admins tooconfigure Hallo levensduur van tokens die zijn uitgegeven voor niet-vertrouwelijke clients. Levensduur van token beleidsregels zijn ingesteld op basis van de tenant wide of Hallo bronnen die worden geopend.

 * tooset een levensduur van token-beleid, moet u toodownload hello [Azure AD PowerShell-Module](https://www.powershellgallery.com/packages/AzureADPreview).

 * Voer Hallo **Connect-AzureAD-bevestigen** opdracht.

 * Hier volgt een voorbeeldbeleid dat Hallo maximale leeftijd één factor vernieuwingstoken ingesteld. Hallo-beleid maken:```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```

 * Afhandeling Hallo [configureren levensduur van token](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) toolearn hoe document toocreate andere aangepaste.

## <a name="next-steps"></a>Volgende stappen
[Levensduur van Token configureren](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[Verwijzing naar Azure AD-Token](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)


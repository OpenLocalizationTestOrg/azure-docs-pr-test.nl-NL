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
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="24b8a-103">Hoe toochange Hallo levensduur van token voor een toepassing ontwikkelde aangepaste standaardinstellingen</span><span class="sxs-lookup"><span data-stu-id="24b8a-103">How toochange hello token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="24b8a-104">Azure AD Premium kunt app-ontwikkelaars en tenant admins tooconfigure Hallo levensduur van tokens die zijn uitgegeven voor niet-vertrouwelijke clients.</span><span class="sxs-lookup"><span data-stu-id="24b8a-104">Azure AD Premium allows app developers and tenant admins tooconfigure hello lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="24b8a-105">Levensduur van token beleidsregels zijn ingesteld op basis van de tenant wide of Hallo bronnen die worden geopend.</span><span class="sxs-lookup"><span data-stu-id="24b8a-105">Token lifetime policies are set on a tenant-wide basis or hello resources being accessed.</span></span>

 * <span data-ttu-id="24b8a-106">tooset een levensduur van token-beleid, moet u toodownload hello [Azure AD PowerShell-Module](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="24b8a-106">tooset a token lifetime policy, you need toodownload hello [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="24b8a-107">Voer Hallo **Connect-AzureAD-bevestigen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="24b8a-107">Run hello **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="24b8a-108">Hier volgt een voorbeeldbeleid dat Hallo maximale leeftijd één factor vernieuwingstoken ingesteld.</span><span class="sxs-lookup"><span data-stu-id="24b8a-108">Here’s an example policy that sets hello max age single factor refresh token.</span></span> <span data-ttu-id="24b8a-109">Hallo-beleid maken:```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="24b8a-109">Create hello policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="24b8a-110">Afhandeling Hallo [configureren levensduur van token](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) toolearn hoe document toocreate andere aangepaste.</span><span class="sxs-lookup"><span data-stu-id="24b8a-110">Checkout hello [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document toolearn how toocreate other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24b8a-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="24b8a-111">Next steps</span></span>
[<span data-ttu-id="24b8a-112">Levensduur van Token configureren</span><span class="sxs-lookup"><span data-stu-id="24b8a-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="24b8a-113">Verwijzing naar Azure AD-Token</span><span class="sxs-lookup"><span data-stu-id="24b8a-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)


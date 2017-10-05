---
title: Het wijzigen van de levensduur van token standaardinstellingen voor een toepassing ontwikkelde aangepaste | Microsoft Docs
description: Het bijwerken van de levensduur van Token beleidsregels voor uw toepassing die u voor Azure AD ontwikkelt
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
ms.openlocfilehash: a28eacd820ed28a6470992ce86b060e886c00bcb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-change-the-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="f267b-103">Het wijzigen van de standaardinstellingen van de levensduur van token voor een toepassing ontwikkelde aangepaste</span><span class="sxs-lookup"><span data-stu-id="f267b-103">How to change the token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="f267b-104">Azure AD Premium kunt app-ontwikkelaars en tenantbeheerders voor het configureren van de levensduur van tokens die zijn uitgegeven voor niet-vertrouwelijke clients.</span><span class="sxs-lookup"><span data-stu-id="f267b-104">Azure AD Premium allows app developers and tenant admins to configure the lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="f267b-105">Levensduur van token beleidsregels zijn ingesteld op basis van de tenant wide of de bronnen die worden geopend.</span><span class="sxs-lookup"><span data-stu-id="f267b-105">Token lifetime policies are set on a tenant-wide basis or the resources being accessed.</span></span>

 * <span data-ttu-id="f267b-106">Als u wilt een levensduur van token instellen, moet u voor het downloaden van de [Azure AD PowerShell-Module](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="f267b-106">To set a token lifetime policy, you need to download the [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="f267b-107">Voer de **Connect-AzureAD-bevestigen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="f267b-107">Run the **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="f267b-108">Hier volgt een voorbeeldbeleid dat het vernieuwingstoken dat maximale leeftijd één factor ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f267b-108">Here’s an example policy that sets the max age single factor refresh token.</span></span> <span data-ttu-id="f267b-109">Het beleid maken:```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="f267b-109">Create the policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="f267b-110">Bekijk de [configureren levensduur van token](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) document voor meer informatie over het maken van andere aangepaste.</span><span class="sxs-lookup"><span data-stu-id="f267b-110">Checkout the [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document to learn how to create other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f267b-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f267b-111">Next steps</span></span>
[<span data-ttu-id="f267b-112">Levensduur van Token configureren</span><span class="sxs-lookup"><span data-stu-id="f267b-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="f267b-113">Verwijzing naar Azure AD-Token</span><span class="sxs-lookup"><span data-stu-id="f267b-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)


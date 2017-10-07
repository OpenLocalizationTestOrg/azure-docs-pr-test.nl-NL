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
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a><span data-ttu-id="27da5-103">Als u zich aanmeldt tooan toepassing onverwachte instemmingsprompt</span><span class="sxs-lookup"><span data-stu-id="27da5-103">Unexpected consent prompt when signing in tooan application</span></span>

<span data-ttu-id="27da5-104">Veel toepassingen die zijn geïntegreerd met Azure Active Directory vereisen machtigingen toovarious bronnen in de volgorde toorun.</span><span class="sxs-lookup"><span data-stu-id="27da5-104">Many applications that integrate with Azure Active Directory require permissions toovarious resources in order toorun.</span></span> <span data-ttu-id="27da5-105">Wanneer u deze resources zijn ook worden geïntegreerd met Azure Active Directory, toestemming machtigingen tooaccess deze wordt aangevraagd met behulp van Azure AD Hallo framework.</span><span class="sxs-lookup"><span data-stu-id="27da5-105">When these resources are also integrated with Azure Active Directory, permissions tooaccess them is requested using hello Azure AD consent framework.</span></span> 

<span data-ttu-id="27da5-106">Dit resulteert in een instemmingsprompt wordt weergegeven Hallo eerst die een toepassing wordt gebruikt, die vaak is een eenmalige bewerking.</span><span class="sxs-lookup"><span data-stu-id="27da5-106">This results in a consent prompt being shown hello first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="27da5-107">Scenario's waarin gebruikers zien toestemming vragen</span><span class="sxs-lookup"><span data-stu-id="27da5-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="27da5-108">Aanvullende prompts kunnen worden verwacht in verschillende scenario's:</span><span class="sxs-lookup"><span data-stu-id="27da5-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="27da5-109">Hallo reeks machtigingen die vereist zijn door de toepassing hello zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="27da5-109">hello set of permissions required by hello application have changed.</span></span>

* <span data-ttu-id="27da5-110">Hallo-gebruiker die oorspronkelijk ingestemd toohello toepassing is niet een beheerder en het nu een andere (niet-beheerders) gebruiker gebruikt Hallo-toepassing voor Hallo eerst.</span><span class="sxs-lookup"><span data-stu-id="27da5-110">hello user who originally consented toohello application was not an administrator, and now a different (non-admin) User is using hello application for hello first time.</span></span>

* <span data-ttu-id="27da5-111">Hallo-gebruiker die oorspronkelijk ingestemd toohello toepassing is een beheerder, maar ze niet namens de hele organisatie Hallo toestemming.</span><span class="sxs-lookup"><span data-stu-id="27da5-111">hello user who originally consented toohello application was an administrator, but they did not consent on-behalf of hello entire organization.</span></span>

* <span data-ttu-id="27da5-112">wordt gebruikt door de toepassing Hello [incrementele en dynamische toestemming](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest aanvullende machtigingen nadat toestemming in eerste instantie is verleend.</span><span class="sxs-lookup"><span data-stu-id="27da5-112">hello application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest additional permissions after consent was initially granted.</span></span> <span data-ttu-id="27da5-113">Dit wordt vaak gebruikt als optionele functies van een toepassing extra machtigingen die vereist is voor basisfunctionaliteit niet vereist.</span><span class="sxs-lookup"><span data-stu-id="27da5-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="27da5-114">Toestemming is ingetrokken na in eerste instantie wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="27da5-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="27da5-115">Hallo developer Hallo toepassing toorequire een prompt toestemming heeft geconfigureerd telkens wanneer deze wordt gebruikt (Opmerking: dit is niet aanbevolen).</span><span class="sxs-lookup"><span data-stu-id="27da5-115">hello developer has configured hello application toorequire a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="27da5-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="27da5-116">Next steps</span></span>

-   [<span data-ttu-id="27da5-117">Apps, machtigingen en toestemming in Azure Active Directory (v1.0 eindpunt)</span><span class="sxs-lookup"><span data-stu-id="27da5-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="27da5-118">Scopes, machtigingen en toestemming in hello Azure Active Directory (v2.0-eindpunt)</span><span class="sxs-lookup"><span data-stu-id="27da5-118">Scopes, permissions, and consent in hello Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)



---
title: 'Azure Active Directory B2C: Dreiging management | Microsoft Docs'
description: Meer informatie over detectie en risicobeperking technieken voor denial of service-aanvallen en wachtwoord aanvallen in Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: vigunase
manager: Ajith Alexander
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2016
ms.author: 
ms.openlocfilehash: 9472cb01eb713e297053727b1a314293574bb657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="979fb-103">Azure Active Directory B2C: Threat management</span><span class="sxs-lookup"><span data-stu-id="979fb-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="979fb-104">Threat management omvat het plannen voor bescherming tegen aanvallen op uw systeem en netwerken.</span><span class="sxs-lookup"><span data-stu-id="979fb-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="979fb-105">Denial of service-aanvallen kunnen maken resources niet beschikbaar voor beoogde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="979fb-105">Denial-of-service attacks might make resources unavailable to intended users.</span></span> <span data-ttu-id="979fb-106">Wachtwoord aanvallen leiden tot onbevoegde toegang tot bronnen.</span><span class="sxs-lookup"><span data-stu-id="979fb-106">Password attacks lead to unauthorized access to resources.</span></span> <span data-ttu-id="979fb-107">Azure Active Directory B2C (Azure AD B2C) beschikt over ingebouwde functies waarmee u uw gegevens beschermen tegen deze bedreigingen op verschillende manieren kunnen.</span><span class="sxs-lookup"><span data-stu-id="979fb-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="979fb-108">Denial of service-aanvallen</span><span class="sxs-lookup"><span data-stu-id="979fb-108">Denial-of-service attacks</span></span>

<span data-ttu-id="979fb-109">Azure AD B2C maakt gebruik van detectie en risicobeperking technieken zoals SYN cookies en snelheid en verbinding beperkingen voor de onderliggende resources tegen denial of service-aanvallen te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="979fb-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits to protect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="979fb-110">Wachtwoord aanvallen</span><span class="sxs-lookup"><span data-stu-id="979fb-110">Password attacks</span></span>

<span data-ttu-id="979fb-111">Azure AD B2C heeft ook risicobeperking technieken voor wachtwoord aanvallen.</span><span class="sxs-lookup"><span data-stu-id="979fb-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="979fb-112">Risicobeperking omvat aanvallen met brute kracht wachtwoord en woordenboekaanvallen wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="979fb-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="979fb-113">Wachtwoorden die zijn ingesteld door gebruikers zijn te redelijkerwijs ingewikkeld vereist.</span><span class="sxs-lookup"><span data-stu-id="979fb-113">Passwords that are set by users are required to be reasonably complex.</span></span> <span data-ttu-id="979fb-114">Azure AD B2C analyseert met behulp van verschillende signalen, de integriteit van aanvragen.</span><span class="sxs-lookup"><span data-stu-id="979fb-114">By using various signals, Azure AD B2C analyzes the integrity of requests.</span></span> <span data-ttu-id="979fb-115">Azure AD B2C is ontworpen om te onderscheiden op intelligente wijze beoogde gebruikers tegen hackers en botnets.</span><span class="sxs-lookup"><span data-stu-id="979fb-115">Azure AD B2C is designed to intelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="979fb-116">Azure AD B2C biedt een strategie voor een geavanceerde aan accounts van vergrendeling op basis van de wachtwoorden die zijn ingevoerd, in de kans op een aanval.</span><span class="sxs-lookup"><span data-stu-id="979fb-116">Azure AD B2C provides a sophisticated strategy to lock accounts based on the passwords entered, in the likelihood of an attack.</span></span>

<span data-ttu-id="979fb-117">Voor meer informatie gaat u naar de [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span><span class="sxs-lookup"><span data-stu-id="979fb-117">For more information, visit the [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>

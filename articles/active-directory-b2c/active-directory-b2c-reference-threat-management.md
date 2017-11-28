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
ms.openlocfilehash: 60bc0cc392b332cc4e9741ddb97dfa58e68ed420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="92ccb-103">Azure Active Directory B2C: Threat management</span><span class="sxs-lookup"><span data-stu-id="92ccb-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="92ccb-104">Threat management omvat het plannen voor bescherming tegen aanvallen op uw systeem en netwerken.</span><span class="sxs-lookup"><span data-stu-id="92ccb-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="92ccb-105">Denial of service-aanvallen kunnen resources niet beschikbaar toointended gebruikers maken.</span><span class="sxs-lookup"><span data-stu-id="92ccb-105">Denial-of-service attacks might make resources unavailable toointended users.</span></span> <span data-ttu-id="92ccb-106">Wachtwoord aanvallen lead toounauthorized toegang tooresources.</span><span class="sxs-lookup"><span data-stu-id="92ccb-106">Password attacks lead toounauthorized access tooresources.</span></span> <span data-ttu-id="92ccb-107">Azure Active Directory B2C (Azure AD B2C) beschikt over ingebouwde functies waarmee u uw gegevens beschermen tegen deze bedreigingen op verschillende manieren kunnen.</span><span class="sxs-lookup"><span data-stu-id="92ccb-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="92ccb-108">Denial of service-aanvallen</span><span class="sxs-lookup"><span data-stu-id="92ccb-108">Denial-of-service attacks</span></span>

<span data-ttu-id="92ccb-109">Azure AD B2C wordt gebruikt voor detectie en risicobeperking technieken zoals SYN cookies en snelheid en verbinding limieten tooprotect onderliggende bronnen tegen denial of service-aanvallen.</span><span class="sxs-lookup"><span data-stu-id="92ccb-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits tooprotect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="92ccb-110">Wachtwoord aanvallen</span><span class="sxs-lookup"><span data-stu-id="92ccb-110">Password attacks</span></span>

<span data-ttu-id="92ccb-111">Azure AD B2C heeft ook risicobeperking technieken voor wachtwoord aanvallen.</span><span class="sxs-lookup"><span data-stu-id="92ccb-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="92ccb-112">Risicobeperking omvat aanvallen met brute kracht wachtwoord en woordenboekaanvallen wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="92ccb-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="92ccb-113">Wachtwoorden die zijn ingesteld door gebruikers zijn vereiste toobe redelijkerwijs complexe.</span><span class="sxs-lookup"><span data-stu-id="92ccb-113">Passwords that are set by users are required toobe reasonably complex.</span></span> <span data-ttu-id="92ccb-114">Azure AD B2C analyseert met behulp van verschillende signalen Hallo integriteit van aanvragen.</span><span class="sxs-lookup"><span data-stu-id="92ccb-114">By using various signals, Azure AD B2C analyzes hello integrity of requests.</span></span> <span data-ttu-id="92ccb-115">Azure AD B2C is ontworpen toointelligently beoogde gebruikers tegen hackers en botnets onderscheiden.</span><span class="sxs-lookup"><span data-stu-id="92ccb-115">Azure AD B2C is designed toointelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="92ccb-116">Azure AD B2C biedt een strategie voor geavanceerde toolock accounts op basis van wachtwoorden van Hallo ingevoerd in de kans op Hallo van een aanval.</span><span class="sxs-lookup"><span data-stu-id="92ccb-116">Azure AD B2C provides a sophisticated strategy toolock accounts based on hello passwords entered, in hello likelihood of an attack.</span></span>

<span data-ttu-id="92ccb-117">Voor meer informatie gaat u naar Hallo [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span><span class="sxs-lookup"><span data-stu-id="92ccb-117">For more information, visit hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>

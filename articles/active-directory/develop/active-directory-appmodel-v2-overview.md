---
title: Azure Active Directory v2.0-eindpunt | Microsoft Docs
description: Een inleiding tot het bouwen van apps met zowel Microsoft-Account en Azure Active Directory aanmelden.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 1e286044fb1a1b367fcac2dc14c47f68d5ed120d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="2c1f9-103">Meld u aan Microsoft-Account en Azure AD-gebruikers in een enkele app</span><span class="sxs-lookup"><span data-stu-id="2c1f9-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="2c1f9-104">In het verleden is een app-ontwikkelaar die ondersteuning bieden voor beide persoonlijke Microsoft-accounts en -werkaccounts van Azure Active Directory wilt integreren met twee afzonderlijke systemen vereist.</span><span class="sxs-lookup"><span data-stu-id="2c1f9-104">In the past, an app developer who wanted to support both personal Microsoft accounts and work accounts from Azure Active Directory was required to integrate with two separate systems.</span></span>  <span data-ttu-id="2c1f9-105">De **Azure AD v2.0-eindpunt** introduceert een nieuwe authenticatie-API-versie waarmee u zich kunt aanmelden beide typen accounts met een eenvoudige integratie.</span><span class="sxs-lookup"><span data-stu-id="2c1f9-105">The **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you to sign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="2c1f9-106">Apps die gebruikmaken van het v2.0-eindpunt kunnen ook gebruiken voor REST-API's van de [Microsoft Graph](https://graph.microsoft.io) met behulp van een type account.</span><span class="sxs-lookup"><span data-stu-id="2c1f9-106">Apps that use the v2.0 endpoint can also consume REST APIs from the [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2c1f9-107">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="2c1f9-107">Getting Started</span></span>
<span data-ttu-id="2c1f9-108">Kies uw favoriete platform in de volgende lijst om een app met behulp van onze open-source bibliotheken en frameworks te bouwen.</span><span class="sxs-lookup"><span data-stu-id="2c1f9-108">Choose your favorite platform from the following list to build an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="2c1f9-109">U kunt ook kunt u onze documentatie OAuth 2.0 & OpenID Connect protocol verzend en ontvang protocolberichten rechtstreeks zonder met behulp van een auth-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="2c1f9-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation to send & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="2c1f9-110">Wat is er nieuw</span><span class="sxs-lookup"><span data-stu-id="2c1f9-110">What's New</span></span>
<span data-ttu-id="2c1f9-111">De informatie hier erg nuttig zijn bij het begrijpen van wat is & Wat is niet mogelijk met het v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="2c1f9-111">The information here will be useful in understanding what is & what isn't possible with the v2.0 endpoint.</span></span>

* <span data-ttu-id="2c1f9-112">Meer informatie over de [typen apps kunt u met het v2.0-eindpunt](active-directory-v2-flows.md).</span><span class="sxs-lookup"><span data-stu-id="2c1f9-112">Learn about the [types of apps you can build with the v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="2c1f9-113">Inzicht in de [beperkingen, beperkingen en beperkingen](active-directory-v2-limitations.md) met het v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="2c1f9-113">Understand the [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with the v2.0 endpoint.</span></span>
* <span data-ttu-id="2c1f9-114">Bekijk deze video voor het v2.0-eindpunt overzicht:</span><span class="sxs-lookup"><span data-stu-id="2c1f9-114">Check out this overview video for the v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="2c1f9-115">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="2c1f9-115">Reference</span></span>
<span data-ttu-id="2c1f9-116">Deze koppelingen zijn handig voor het platform in de diepte verkennen:</span><span class="sxs-lookup"><span data-stu-id="2c1f9-116">These links will be useful for exploring the platform in depth:</span></span>

* [<span data-ttu-id="2c1f9-117">naslaginformatie over v2.0-Protocol</span><span class="sxs-lookup"><span data-stu-id="2c1f9-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="2c1f9-118">v2.0 tokenverwijzing</span><span class="sxs-lookup"><span data-stu-id="2c1f9-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="2c1f9-119">naslaginformatie over v2.0-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="2c1f9-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="2c1f9-120">Scopes en toestemming in het v2.0-eindpunt</span><span class="sxs-lookup"><span data-stu-id="2c1f9-120">Scopes and Consent in the v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="2c1f9-121">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="2c1f9-121">The Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="2c1f9-122">Help en ondersteuning</span><span class="sxs-lookup"><span data-stu-id="2c1f9-122">Help & Support</span></span>
<span data-ttu-id="2c1f9-123">Dit zijn de aanbevolen plaatsen voor hulp bij het ontwikkelen met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2c1f9-123">These are the best places to get help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="2c1f9-124">Stack Overflow's tags voor `azure-active-directory` en `adal`</span><span class="sxs-lookup"><span data-stu-id="2c1f9-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="2c1f9-125">Feedback op Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2c1f9-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="2c1f9-126">Als u alleen hoeft aan te melden werk- en schoolaccounts accounts van Azure Active Directory, moet u beginnen met onze [ontwikkelaarshandleiding Azure AD](active-directory-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="2c1f9-126">If you only need to sign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="2c1f9-127">Het v2.0-eindpunt is bedoeld voor gebruik door ontwikkelaars die expliciet hoeft aan te melden in persoonlijke Microsoft-accounts.</span><span class="sxs-lookup"><span data-stu-id="2c1f9-127">The v2.0 endpoint is intended for use by developers who explicitly need to sign in Microsoft personal accounts.</span></span>


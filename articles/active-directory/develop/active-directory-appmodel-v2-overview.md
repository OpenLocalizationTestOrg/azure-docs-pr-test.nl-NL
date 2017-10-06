---
title: Active Directory v2.0-eindpunt aaaAzure | Microsoft Docs
description: Een inleiding toobuilding apps met zowel Microsoft-Account en Azure Active Directory aanmelden.
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
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="725e7-103">Meld u aan Microsoft-Account en Azure AD-gebruikers in een enkele app</span><span class="sxs-lookup"><span data-stu-id="725e7-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="725e7-104">In Hallo voorbij toepassingsontwikkelaar wie toosupport beide persoonlijke Microsoft-accounts wilde en werkaccounts van Azure Active Directory is vereist toointegrate met twee afzonderlijke systemen.</span><span class="sxs-lookup"><span data-stu-id="725e7-104">In hello past, an app developer who wanted toosupport both personal Microsoft accounts and work accounts from Azure Active Directory was required toointegrate with two separate systems.</span></span>  <span data-ttu-id="725e7-105">Hallo **Azure AD v2.0-eindpunt** introduceert een nieuwe authenticatie-API-versie waarmee u toosign in beide typen accounts met een eenvoudige integratie.</span><span class="sxs-lookup"><span data-stu-id="725e7-105">hello **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you toosign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="725e7-106">Apps die gebruikmaken van Hallo v2.0-eindpunt kunnen ook verbruiken, REST-API's Hallo [Microsoft Graph](https://graph.microsoft.io) met behulp van een type account.</span><span class="sxs-lookup"><span data-stu-id="725e7-106">Apps that use hello v2.0 endpoint can also consume REST APIs from hello [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="725e7-107">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="725e7-107">Getting Started</span></span>
<span data-ttu-id="725e7-108">Kies uw favoriete platform van Hallo lijst toobuild na een app met behulp van onze open-source bibliotheken en frameworks.</span><span class="sxs-lookup"><span data-stu-id="725e7-108">Choose your favorite platform from hello following list toobuild an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="725e7-109">U kunt ook gebruik van onze OAuth 2.0 & OpenID Connect protocol documentatie toosend & protocolberichten rechtstreeks zonder met behulp van een bibliotheek auth ontvangen.</span><span class="sxs-lookup"><span data-stu-id="725e7-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation toosend & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="725e7-110">Wat is er nieuw</span><span class="sxs-lookup"><span data-stu-id="725e7-110">What's New</span></span>
<span data-ttu-id="725e7-111">Hallo informatie hier erg nuttig zijn bij het begrijpen van wat is & Wat is niet mogelijk met Hallo v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="725e7-111">hello information here will be useful in understanding what is & what isn't possible with hello v2.0 endpoint.</span></span>

* <span data-ttu-id="725e7-112">Meer informatie over Hallo [typen apps die u met Hallo v2.0-eindpunt bouwen kunt](active-directory-v2-flows.md).</span><span class="sxs-lookup"><span data-stu-id="725e7-112">Learn about hello [types of apps you can build with hello v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="725e7-113">Hallo begrijpen [beperkingen, beperkingen en beperkingen](active-directory-v2-limitations.md) met Hallo v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="725e7-113">Understand hello [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with hello v2.0 endpoint.</span></span>
* <span data-ttu-id="725e7-114">Bekijk deze video voor Hallo v2.0-eindpunt overzicht:</span><span class="sxs-lookup"><span data-stu-id="725e7-114">Check out this overview video for hello v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="725e7-115">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="725e7-115">Reference</span></span>
<span data-ttu-id="725e7-116">Deze koppelingen zijn handig voor het Hallo-platform in de diepte verkennen:</span><span class="sxs-lookup"><span data-stu-id="725e7-116">These links will be useful for exploring hello platform in depth:</span></span>

* [<span data-ttu-id="725e7-117">naslaginformatie over v2.0-Protocol</span><span class="sxs-lookup"><span data-stu-id="725e7-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="725e7-118">v2.0 tokenverwijzing</span><span class="sxs-lookup"><span data-stu-id="725e7-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="725e7-119">naslaginformatie over v2.0-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="725e7-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="725e7-120">Scopes en toestemming in Hallo v2.0-eindpunt</span><span class="sxs-lookup"><span data-stu-id="725e7-120">Scopes and Consent in hello v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="725e7-121">Hallo Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="725e7-121">hello Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="725e7-122">Help en ondersteuning</span><span class="sxs-lookup"><span data-stu-id="725e7-122">Help & Support</span></span>
<span data-ttu-id="725e7-123">Dit zijn Hallo beste locaties tooget helpen met het ontwikkelen op Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="725e7-123">These are hello best places tooget help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="725e7-124">Stack Overflow's tags voor `azure-active-directory` en `adal`</span><span class="sxs-lookup"><span data-stu-id="725e7-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="725e7-125">Feedback op Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="725e7-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="725e7-126">Als u alleen toosign in werk- en schoolaccounts accounts van Azure Active Directory moet, moet u beginnen met onze [ontwikkelaarshandleiding Azure AD](active-directory-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="725e7-126">If you only need toosign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="725e7-127">Hallo v2.0-eindpunt is bedoeld voor gebruik door ontwikkelaars die expliciet toosign in persoonlijke Microsoft-accounts moeten.</span><span class="sxs-lookup"><span data-stu-id="725e7-127">hello v2.0 endpoint is intended for use by developers who explicitly need toosign in Microsoft personal accounts.</span></span>


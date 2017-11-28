---
title: 'Azure AD Connect: Pass through-verificatie - huidige beperkingen | Microsoft Docs'
description: Dit artikel worden de huidige beperkingen Hallo van Azure Active Directory (Azure AD) Pass through-verificatie.
services: active-directory
keywords: Azure AD Connect Pass through-verificatie, install Active Directory onderdelen vereist voor Azure AD, SSO, Single Sign-on
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 2933745d071aae205c44659e6ea92697f390effb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="13e53-104">Azure Active Directory Pass-through-verificatie: Huidige beperkingen</span><span class="sxs-lookup"><span data-stu-id="13e53-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="13e53-105">Azure AD Pass-through-verificatie is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="13e53-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="13e53-106">Dit is een gratis functie en hoeft u niet alle betaald edities van Azure AD-toouse deze.</span><span class="sxs-lookup"><span data-stu-id="13e53-106">It is a free feature, and you don't need any paid editions of Azure AD toouse it.</span></span> <span data-ttu-id="13e53-107">Pass through-verificatie is alleen beschikbaar in hello world wide exemplaar van Azure AD en niet op [Microsoft Cloud Duitsland](http://www.microsoft.de/cloud-deutschland) en [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span><span class="sxs-lookup"><span data-stu-id="13e53-107">Pass-through Authentication is only available in hello world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="13e53-108">Ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="13e53-108">Supported scenarios</span></span>

<span data-ttu-id="13e53-109">Hallo volgen scenario's worden volledig ondersteund tijdens de preview:</span><span class="sxs-lookup"><span data-stu-id="13e53-109">hello following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="13e53-110">Gebruikersaanmeldingen in alle web browser gebaseerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="13e53-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="13e53-111">Gebruikersaanmeldingen in Office 365-clienttoepassingen die ondersteuning bieden voor [moderne verificatie](https://aka.ms/modernauthga).</span><span class="sxs-lookup"><span data-stu-id="13e53-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="13e53-112">Azure AD Join voor Windows 10-apparaten.</span><span class="sxs-lookup"><span data-stu-id="13e53-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="13e53-113">Ondersteuning voor Exchange ActiveSync.</span><span class="sxs-lookup"><span data-stu-id="13e53-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="13e53-114">Niet-ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="13e53-114">Unsupported scenarios</span></span>

<span data-ttu-id="13e53-115">Hallo volgende scenario's zijn _niet_ ondersteund tijdens de preview:</span><span class="sxs-lookup"><span data-stu-id="13e53-115">hello following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="13e53-116">Gebruikersaanmeldingen in clienttoepassingen verouderde Office (Office 2013 of lager).</span><span class="sxs-lookup"><span data-stu-id="13e53-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="13e53-117">Organisaties zijn aangemoedigd tooswitch toomodern verificatie, indien mogelijk.</span><span class="sxs-lookup"><span data-stu-id="13e53-117">Organizations are encouraged tooswitch toomodern authentication, if possible.</span></span> <span data-ttu-id="13e53-118">Moderne verificatie kunt u ondersteuning voor Pass-through-verificatie, maar ook helpt bij het beveiligen van uw gebruikers gebruikersaccounts via [voorwaardelijke toegang](../active-directory-conditional-access.md) functies zoals multi-factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="13e53-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="13e53-119">Gebruikersaanmeldingen in Skype voor bedrijven-clienttoepassingen, met inbegrip van Skype voor bedrijven 2016.</span><span class="sxs-lookup"><span data-stu-id="13e53-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="13e53-120">Gebruikersaanmeldingen in PowerShell v1.0.</span><span class="sxs-lookup"><span data-stu-id="13e53-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="13e53-121">Het wordt aanbevolen v2.0 PowerShell te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="13e53-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="13e53-122">Als tijdelijke oplossing voor niet-ondersteunde scenario's, schakel u synchronisatie van wachtwoordhash op Hallo [optionele functies](active-directory-aadconnect-get-started-custom.md#optional-features) pagina in hello Azure AD Connect-wizard.</span><span class="sxs-lookup"><span data-stu-id="13e53-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on hello [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in hello Azure AD Connect wizard.</span></span> <span data-ttu-id="13e53-123">Synchronisatie van wachtwoordhash fungeert als een opvang voor Hallo voorafgaand aan scenario's _alleen_ (en _niet_ als algemene tooPass via Terugvalverificatie).</span><span class="sxs-lookup"><span data-stu-id="13e53-123">Password Hash Synchronization acts as a fallback for hello preceding scenarios _only_ (and _not_ as a generic fallback tooPass-through Authentication).</span></span> <span data-ttu-id="13e53-124">Als u deze scenario's hoeft, gebruikt u de uitschakelen van synchronisatie van wachtwoordhash.</span><span class="sxs-lookup"><span data-stu-id="13e53-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13e53-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="13e53-125">Next steps</span></span>
- <span data-ttu-id="13e53-126">[**Snel starten** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) - laten en Azure AD Pass-through-verificatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="13e53-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="13e53-127">[**Technische diepgaand** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md) -begrijpen hoe deze functie werkt.</span><span class="sxs-lookup"><span data-stu-id="13e53-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="13e53-128">[**Veelgestelde vragen** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently vragen worden beantwoord.</span><span class="sxs-lookup"><span data-stu-id="13e53-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="13e53-129">[**Problemen met** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informatie over hoe tooresolve algemene problemen met een Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="13e53-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="13e53-130">[**Azure AD naadloze eenmalige aanmelding** ](active-directory-aadconnect-sso.md) -meer informatie over deze aanvullende functie.</span><span class="sxs-lookup"><span data-stu-id="13e53-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="13e53-131">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.</span><span class="sxs-lookup"><span data-stu-id="13e53-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>

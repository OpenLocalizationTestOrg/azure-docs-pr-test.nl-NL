---
title: 'Azure AD Connect: Pass through-verificatie - huidige beperkingen | Microsoft Docs'
description: Dit artikel worden de huidige beperkingen van Azure Active Directory (Azure AD) Pass through-verificatie.
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
ms.openlocfilehash: 37c0ea094d02208f2516a4a040f75894e046c670
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="ba37b-104">Azure Active Directory Pass-through-verificatie: Huidige beperkingen</span><span class="sxs-lookup"><span data-stu-id="ba37b-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="ba37b-105">Azure AD Pass-through-verificatie is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="ba37b-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="ba37b-106">Er is een gratis functie en u hoeft niet elke betaald edities van Azure AD om deze te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ba37b-106">It is a free feature, and you don't need any paid editions of Azure AD to use it.</span></span> <span data-ttu-id="ba37b-107">Pass through-verificatie is alleen beschikbaar in het wereldwijde exemplaar van Azure AD en niet op [Microsoft Cloud Duitsland](http://www.microsoft.de/cloud-deutschland) en [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span><span class="sxs-lookup"><span data-stu-id="ba37b-107">Pass-through Authentication is only available in the world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="ba37b-108">Ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="ba37b-108">Supported scenarios</span></span>

<span data-ttu-id="ba37b-109">De volgende scenario's worden volledig ondersteund tijdens de preview:</span><span class="sxs-lookup"><span data-stu-id="ba37b-109">The following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="ba37b-110">Gebruikersaanmeldingen in alle web browser gebaseerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ba37b-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="ba37b-111">Gebruikersaanmeldingen in Office 365-clienttoepassingen die ondersteuning bieden voor [moderne verificatie](https://aka.ms/modernauthga).</span><span class="sxs-lookup"><span data-stu-id="ba37b-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="ba37b-112">Azure AD Join voor Windows 10-apparaten.</span><span class="sxs-lookup"><span data-stu-id="ba37b-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="ba37b-113">Ondersteuning voor Exchange ActiveSync.</span><span class="sxs-lookup"><span data-stu-id="ba37b-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="ba37b-114">Niet-ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="ba37b-114">Unsupported scenarios</span></span>

<span data-ttu-id="ba37b-115">De volgende scenario's zijn _niet_ ondersteund tijdens de preview:</span><span class="sxs-lookup"><span data-stu-id="ba37b-115">The following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="ba37b-116">Gebruikersaanmeldingen in clienttoepassingen verouderde Office (Office 2013 of lager).</span><span class="sxs-lookup"><span data-stu-id="ba37b-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="ba37b-117">Organisaties aangemoedigd overschakelen naar moderne verificatie, indien mogelijk.</span><span class="sxs-lookup"><span data-stu-id="ba37b-117">Organizations are encouraged to switch to modern authentication, if possible.</span></span> <span data-ttu-id="ba37b-118">Moderne verificatie kunt u ondersteuning voor Pass-through-verificatie, maar ook helpt bij het beveiligen van uw gebruikers gebruikersaccounts via [voorwaardelijke toegang](../active-directory-conditional-access.md) functies zoals multi-factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="ba37b-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="ba37b-119">Gebruikersaanmeldingen in Skype voor bedrijven-clienttoepassingen, met inbegrip van Skype voor bedrijven 2016.</span><span class="sxs-lookup"><span data-stu-id="ba37b-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="ba37b-120">Gebruikersaanmeldingen in PowerShell v1.0.</span><span class="sxs-lookup"><span data-stu-id="ba37b-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="ba37b-121">Het wordt aanbevolen v2.0 PowerShell te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ba37b-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="ba37b-122">Inschakelen als tijdelijke oplossing voor niet-ondersteunde scenario's, synchronisatie van wachtwoordhash op de [optionele functies](active-directory-aadconnect-get-started-custom.md#optional-features) pagina in de Azure AD Connect-wizard.</span><span class="sxs-lookup"><span data-stu-id="ba37b-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on the [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in the Azure AD Connect wizard.</span></span> <span data-ttu-id="ba37b-123">Synchronisatie van wachtwoordhash fungeert als een opvang voor de bovenstaande scenario's _alleen_ (en _niet_ als een algemene terugvallen op Pass through-verificatie).</span><span class="sxs-lookup"><span data-stu-id="ba37b-123">Password Hash Synchronization acts as a fallback for the preceding scenarios _only_ (and _not_ as a generic fallback to Pass-through Authentication).</span></span> <span data-ttu-id="ba37b-124">Als u deze scenario's hoeft, gebruikt u de uitschakelen van synchronisatie van wachtwoordhash.</span><span class="sxs-lookup"><span data-stu-id="ba37b-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba37b-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ba37b-125">Next steps</span></span>
- <span data-ttu-id="ba37b-126">[**Snel starten** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) - laten en Azure AD Pass-through-verificatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ba37b-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="ba37b-127">[**Technische diepgaand** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md) -begrijpen hoe deze functie werkt.</span><span class="sxs-lookup"><span data-stu-id="ba37b-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="ba37b-128">[**Veelgestelde vragen** ](active-directory-aadconnect-pass-through-authentication-faq.md) -antwoorden op veelgestelde vragen.</span><span class="sxs-lookup"><span data-stu-id="ba37b-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="ba37b-129">[**Problemen met** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informatie over het oplossen van veelvoorkomende problemen met de functie.</span><span class="sxs-lookup"><span data-stu-id="ba37b-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="ba37b-130">[**Azure AD naadloze eenmalige aanmelding** ](active-directory-aadconnect-sso.md) -meer informatie over deze aanvullende functie.</span><span class="sxs-lookup"><span data-stu-id="ba37b-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="ba37b-131">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.</span><span class="sxs-lookup"><span data-stu-id="ba37b-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>

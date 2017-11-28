---
title: 'Licentieverlening: Azure AD SSPR | Microsoft Docs'
description: Azure AD selfservice voor wachtwoordherstel licentievereisten
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="65bde-103">Licentievereisten voor selfservicegebruikers Azure AD-wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="65bde-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="65bde-104">Toofunction Azure AD-wachtwoord opnieuw instellen zodat u **moet ten minste één licentie is toegewezen in uw organisatie hebben**.</span><span class="sxs-lookup"><span data-stu-id="65bde-104">In order for Azure AD Password Reset toofunction, you **must have at least one license assigned in your organization**.</span></span> <span data-ttu-id="65bde-105">We afdwingen per gebruiker licentieverlening op Hallo wachtwoord opnieuw instellen van ervaring niet.</span><span class="sxs-lookup"><span data-stu-id="65bde-105">We do not enforce per-user licensing on hello password reset experience.</span></span> <span data-ttu-id="65bde-106">toomaintain compatibiliteit met uw Microsoft-licentieovereenkomst, moet u tooassign licenties tooany gebruikers die gebruikmaken van premium-functies.</span><span class="sxs-lookup"><span data-stu-id="65bde-106">toomaintain compliance with your Microsoft licensing agreement, you need tooassign licenses tooany users that use premium features.</span></span>

* <span data-ttu-id="65bde-107">**Alleen gebruikers cloud** -Office 365 (O365) een betaald SKU of Azure AD Basic</span><span class="sxs-lookup"><span data-stu-id="65bde-107">**Cloud only users** - Office 365 (O365) any paid SKU, or Azure AD Basic</span></span>
* <span data-ttu-id="65bde-108">**Cloud** en/of **on-premises gebruikers** -Azure AD Premium-P1 of P2, Enterprise Mobility + Security (EMS) of Secure productief Enterprise (Gebeurtenisspe)</span><span class="sxs-lookup"><span data-stu-id="65bde-108">**Cloud** and/or **on-premises users** - Azure AD Premium P1 or P2, Enterprise Mobility + Security (EMS), or Secure Productive Enterprise (SPE)</span></span>

## <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="65bde-109">Licenties die vereist zijn voor write-back van wachtwoord</span><span class="sxs-lookup"><span data-stu-id="65bde-109">Licenses required for password writeback</span></span>

<span data-ttu-id="65bde-110">toouse wachtwoord terugschrijven, kunt u een van de licenties die zijn toegewezen in uw tenant te volgen Hallo moet hebben.</span><span class="sxs-lookup"><span data-stu-id="65bde-110">toouse password writeback, you must have one of hello following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="65bde-111">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="65bde-111">Azure AD Premium P1</span></span>
* <span data-ttu-id="65bde-112">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="65bde-112">Azure AD Premium P2</span></span>
* <span data-ttu-id="65bde-113">Enterprise Mobility + Security E3</span><span class="sxs-lookup"><span data-stu-id="65bde-113">Enterprise Mobility + Security E3</span></span>
* <span data-ttu-id="65bde-114">Enterprise Mobility + Security E5</span><span class="sxs-lookup"><span data-stu-id="65bde-114">Enterprise Mobility + Security E5</span></span>
* <span data-ttu-id="65bde-115">Secure Productive Enterprise E3</span><span class="sxs-lookup"><span data-stu-id="65bde-115">Secure Productive Enterprise E3</span></span>
* <span data-ttu-id="65bde-116">Secure Productive Enterprise E5</span><span class="sxs-lookup"><span data-stu-id="65bde-116">Secure Productive Enterprise E5</span></span>

> [!NOTE]
> <span data-ttu-id="65bde-117">Zelfstandige Office 365-abonnementen licentieverlening **bieden geen ondersteuning voor write-back van wachtwoord** en een van de voorgaande plannen voor deze functionaliteit toowork Hallo vereisen.</span><span class="sxs-lookup"><span data-stu-id="65bde-117">Standalone Office 365 licensing plans **do not support password writeback** and require one of hello preceding plans for this functionality toowork.</span></span>

<span data-ttu-id="65bde-118">Aanvullende licenties informatie, inclusief kosten vindt u op Hallo volgende pagina 's</span><span class="sxs-lookup"><span data-stu-id="65bde-118">Additional licensing info including costs can be found on hello following pages</span></span>

* [<span data-ttu-id="65bde-119">Azure Active Directory-prijzen site</span><span class="sxs-lookup"><span data-stu-id="65bde-119">Azure Active Directory Pricing site</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="65bde-120">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="65bde-120">Enterprise Mobility + Security</span></span>](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [<span data-ttu-id="65bde-121">Beveiligde productief Enterprise</span><span class="sxs-lookup"><span data-stu-id="65bde-121">Secure Productive Enterprise</span></span>](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="65bde-122">Groep of gebruiker gebaseerde licentieverlening inschakelen</span><span class="sxs-lookup"><span data-stu-id="65bde-122">Enable group or user-based licensing</span></span>

<span data-ttu-id="65bde-123">Azure AD nu ondersteunt op basis van een groep licentieverlening zodat beheerders tooassign licenties in bulk tooa groep gebruikers in plaats van één voor één toewijzen.</span><span class="sxs-lookup"><span data-stu-id="65bde-123">Azure AD now supports group-based licensing allowing administrators tooassign licenses in bulk tooa group of users, rather than assigning them one at a time.</span></span> [<span data-ttu-id="65bde-124">Toewijzen, controleren en oplossen van problemen met licenties</span><span class="sxs-lookup"><span data-stu-id="65bde-124">Assign, verify, and resolve problems with licenses</span></span>](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

<span data-ttu-id="65bde-125">Sommige Microsoft-services zijn niet beschikbaar op alle locaties.</span><span class="sxs-lookup"><span data-stu-id="65bde-125">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="65bde-126">Voordat u een licentie kan tooa gebruiker worden toegewezen, moet de Hallo beheerder Hallo 'Gebruikslocatie'-eigenschap op Hallo gebruiker opgeven.</span><span class="sxs-lookup"><span data-stu-id="65bde-126">Before a license can be assigned tooa user, hello administrator must specify hello “Usage location” property on hello user.</span></span> <span data-ttu-id="65bde-127">Toewijzing van licenties kan worden uitgevoerd onder User > profiel > sectie Settings in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="65bde-127">Assignment of licenses can be done under User > Profile > Settings section in hello Azure portal.</span></span> <span data-ttu-id="65bde-128">**Wanneer u de licentietoewijzing van de groep, neemt alle gebruikers zonder een gebruikslocatie opgegeven Hallo-locatie van Hallo-map.**</span><span class="sxs-lookup"><span data-stu-id="65bde-128">**When using group license assignment, any users without a usage location specified inherit hello location of hello directory.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="65bde-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="65bde-129">Next steps</span></span>

<span data-ttu-id="65bde-130">Hallo volgende koppelingen vindt u aanvullende informatie met betrekking tot het wachtwoord opnieuw instellen met behulp van Azure AD</span><span class="sxs-lookup"><span data-stu-id="65bde-130">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="65bde-131">[**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD</span><span class="sxs-lookup"><span data-stu-id="65bde-131">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="65bde-132">[**Gegevens** ](active-directory-passwords-data.md) - begrijpen Hallo-gegevens die nodig is en hoe deze wordt gebruikt voor wachtwoordbeheer</span><span class="sxs-lookup"><span data-stu-id="65bde-132">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="65bde-133">[**Implementatie** ](active-directory-passwords-best-practices.md) -plannen en implementeren van SSPR tooyour gebruikers via Hallo richtlijnen hier gevonden</span><span class="sxs-lookup"><span data-stu-id="65bde-133">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="65bde-134">[**Aanpassen** ](active-directory-passwords-customize.md) -Hallo uiterlijk Hallo SSPR ervaring voor uw bedrijf aanpassen.</span><span class="sxs-lookup"><span data-stu-id="65bde-134">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="65bde-135">[**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken</span><span class="sxs-lookup"><span data-stu-id="65bde-135">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="65bde-136">[**Technische diepgaand** ](active-directory-passwords-how-it-works.md) -Ga achter Hallo gordijn toounderstand hoe het werkt</span><span class="sxs-lookup"><span data-stu-id="65bde-136">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="65bde-137">[**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe?</span><span class="sxs-lookup"><span data-stu-id="65bde-137">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="65bde-138">Hoe komt dat?</span><span class="sxs-lookup"><span data-stu-id="65bde-138">Why?</span></span> <span data-ttu-id="65bde-139">Wat?</span><span class="sxs-lookup"><span data-stu-id="65bde-139">What?</span></span> <span data-ttu-id="65bde-140">Waar?</span><span class="sxs-lookup"><span data-stu-id="65bde-140">Where?</span></span> <span data-ttu-id="65bde-141">Wie?</span><span class="sxs-lookup"><span data-stu-id="65bde-141">Who?</span></span> <span data-ttu-id="65bde-142">Wanneer?</span><span class="sxs-lookup"><span data-stu-id="65bde-142">When?</span></span> <span data-ttu-id="65bde-143">-Beantwoordt tooquestions gewenste altijd tooask</span><span class="sxs-lookup"><span data-stu-id="65bde-143">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="65bde-144">[**Problemen met** ](active-directory-passwords-troubleshoot.md) -informatie over hoe tooresolve algemene problemen zien we met SSPR</span><span class="sxs-lookup"><span data-stu-id="65bde-144">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>


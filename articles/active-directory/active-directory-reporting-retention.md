---
title: bewaarbeleid voor Active Directory-rapport aaaAzure | Microsoft Docs
description: Bewaarbeleid voor gegevens in uw Azure Active Directory
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="93a72-103">Bewaarbeleid voor Azure Active Directory rapport</span><span class="sxs-lookup"><span data-stu-id="93a72-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="93a72-104">Dit onderwerp vindt u antwoorden toohello Veelgestelde vragen in combinatie met Hallo Gegevensretentie voor Hallo andere activiteitsrapporten in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="93a72-104">This topic provides you with answers toohello most common questions in conjunction with hello data retention for hello different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="93a72-105">**V: hoe vind u Hallo-verzameling van gegevens over de activiteit is gestart?**</span><span class="sxs-lookup"><span data-stu-id="93a72-105">**Q: How can you get hello collection of activity data started?**</span></span>

<span data-ttu-id="93a72-106">**A:**</span><span class="sxs-lookup"><span data-stu-id="93a72-106">**A:**</span></span>

| <span data-ttu-id="93a72-107">Azure AD-editie</span><span class="sxs-lookup"><span data-stu-id="93a72-107">Azure AD Edition</span></span> | <span data-ttu-id="93a72-108">Verzameling starten</span><span class="sxs-lookup"><span data-stu-id="93a72-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="93a72-109">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="93a72-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="93a72-110">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="93a72-110">Azure AD Premium P2</span></span> | <span data-ttu-id="93a72-111">Wanneer u registreert voor een abonnement</span><span class="sxs-lookup"><span data-stu-id="93a72-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="93a72-112">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="93a72-112">Azure AD Free</span></span> | <span data-ttu-id="93a72-113">eerste keer openen van Hallo Hallo [Azure Active Directory-blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) of gebruik Hallo [rapportage-API's](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="93a72-113">hello first time you open hello [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use hello [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="93a72-114">**V: waarop uw activiteitsgegevens beschikbaar is in hello Azure-portal?**</span><span class="sxs-lookup"><span data-stu-id="93a72-114">**Q: When is your activity data available in hello Azure portal?**</span></span>

<span data-ttu-id="93a72-115">**A:**</span><span class="sxs-lookup"><span data-stu-id="93a72-115">**A:**</span></span>

- <span data-ttu-id="93a72-116">**Onmiddellijk** : als u al met rapporten in de klassieke Azure-portal Hallo werkt</span><span class="sxs-lookup"><span data-stu-id="93a72-116">**Immediately** - If you have already been working with reports in hello Azure classic portal</span></span>
- <span data-ttu-id="93a72-117">**Binnen 2 uur** : als u dit nog niet hebt ingeschakeld reporting in Hallo klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="93a72-117">**Within 2 hours** - If you haven’t turned reporting on  in hello Azure classic portal</span></span>

---
<span data-ttu-id="93a72-118">**V: hoe vind u Hallo-verzameling van beveiliging signalen gestart?**</span><span class="sxs-lookup"><span data-stu-id="93a72-118">**Q: How can you get hello collection of security signals started?**</span></span>  

<span data-ttu-id="93a72-119">**A:** voor beveiliging, signalen Hallo verzamelingsproces wordt gestart wanneer u meedoen toouse Hallo Identity Protection Center.</span><span class="sxs-lookup"><span data-stu-id="93a72-119">**A:** For security signals, hello collection process starts when you opt-in toouse hello Identity Protection Center.</span></span> 


---
<span data-ttu-id="93a72-120">**V: hoe lang hello verzamelde gegevens opgeslagen?**</span><span class="sxs-lookup"><span data-stu-id="93a72-120">**Q: For how long is hello collected data stored?**</span></span>

<span data-ttu-id="93a72-121">**A:**</span><span class="sxs-lookup"><span data-stu-id="93a72-121">**A:**</span></span>

<span data-ttu-id="93a72-122">**Activiteitsrapporten**</span><span class="sxs-lookup"><span data-stu-id="93a72-122">**Activity reports**</span></span>    

| <span data-ttu-id="93a72-123">Rapport</span><span class="sxs-lookup"><span data-stu-id="93a72-123">Report</span></span>                 | <span data-ttu-id="93a72-124">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="93a72-124">Azure AD Free</span></span> | <span data-ttu-id="93a72-125">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="93a72-125">Azure AD Premium P1</span></span> | <span data-ttu-id="93a72-126">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="93a72-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="93a72-127">Directorycontrole</span><span class="sxs-lookup"><span data-stu-id="93a72-127">Directory Audit</span></span>        | <span data-ttu-id="93a72-128">7 dagen</span><span class="sxs-lookup"><span data-stu-id="93a72-128">7 days</span></span>        | <span data-ttu-id="93a72-129">30 dagen</span><span class="sxs-lookup"><span data-stu-id="93a72-129">30 days</span></span>             | <span data-ttu-id="93a72-130">30 dagen</span><span class="sxs-lookup"><span data-stu-id="93a72-130">30 days</span></span>             |
| <span data-ttu-id="93a72-131">Aanmeldingsactiviteit</span><span class="sxs-lookup"><span data-stu-id="93a72-131">Sign-in Activity</span></span>       | <span data-ttu-id="93a72-132">7 dagen</span><span class="sxs-lookup"><span data-stu-id="93a72-132">7 days</span></span>        | <span data-ttu-id="93a72-133">30 dagen</span><span class="sxs-lookup"><span data-stu-id="93a72-133">30 days</span></span>             | <span data-ttu-id="93a72-134">30 dagen</span><span class="sxs-lookup"><span data-stu-id="93a72-134">30 days</span></span>             |

<span data-ttu-id="93a72-135">**Beveiliging signalen**</span><span class="sxs-lookup"><span data-stu-id="93a72-135">**Security Signals**</span></span>

| <span data-ttu-id="93a72-136">Rapport</span><span class="sxs-lookup"><span data-stu-id="93a72-136">Report</span></span>         | <span data-ttu-id="93a72-137">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="93a72-137">Azure AD Free</span></span> | <span data-ttu-id="93a72-138">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="93a72-138">Azure AD Premium P1</span></span> | <span data-ttu-id="93a72-139">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="93a72-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="93a72-140">Gebruikers die risico lopen</span><span class="sxs-lookup"><span data-stu-id="93a72-140">Users at risk</span></span>  | <span data-ttu-id="93a72-141">7 dagen</span><span class="sxs-lookup"><span data-stu-id="93a72-141">7 days</span></span>        | <span data-ttu-id="93a72-142">30 dagen</span><span class="sxs-lookup"><span data-stu-id="93a72-142">30 days</span></span>             | <span data-ttu-id="93a72-143">90 dagen</span><span class="sxs-lookup"><span data-stu-id="93a72-143">90 days</span></span>             |
| <span data-ttu-id="93a72-144">Riskant aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="93a72-144">Risky sign-ins</span></span> | <span data-ttu-id="93a72-145">7 dagen</span><span class="sxs-lookup"><span data-stu-id="93a72-145">7 days</span></span>        | <span data-ttu-id="93a72-146">30 dagen</span><span class="sxs-lookup"><span data-stu-id="93a72-146">30 days</span></span>             | <span data-ttu-id="93a72-147">90 dagen</span><span class="sxs-lookup"><span data-stu-id="93a72-147">90 days</span></span>             |

---
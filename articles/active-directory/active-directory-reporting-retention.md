---
title: Bewaarbeleid voor Azure Active Directory rapport | Microsoft Docs
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
ms.openlocfilehash: ffeba8a6c32a21c75af21f948bbd6ea88dd9278c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="31029-103">Bewaarbeleid voor Azure Active Directory rapport</span><span class="sxs-lookup"><span data-stu-id="31029-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="31029-104">Dit onderwerp vindt u antwoorden op veelgestelde vragen in combinatie met het bewaren van gegevens voor de verschillende activiteitsrapporten in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="31029-104">This topic provides you with answers to the most common questions in conjunction with the data retention for the different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="31029-105">**V: hoe vind u de verzameling van gegevens over de activiteit is gestart?**</span><span class="sxs-lookup"><span data-stu-id="31029-105">**Q: How can you get the collection of activity data started?**</span></span>

<span data-ttu-id="31029-106">**A:**</span><span class="sxs-lookup"><span data-stu-id="31029-106">**A:**</span></span>

| <span data-ttu-id="31029-107">Azure AD-editie</span><span class="sxs-lookup"><span data-stu-id="31029-107">Azure AD Edition</span></span> | <span data-ttu-id="31029-108">Verzameling starten</span><span class="sxs-lookup"><span data-stu-id="31029-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="31029-109">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="31029-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="31029-110">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="31029-110">Azure AD Premium P2</span></span> | <span data-ttu-id="31029-111">Wanneer u registreert voor een abonnement</span><span class="sxs-lookup"><span data-stu-id="31029-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="31029-112">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="31029-112">Azure AD Free</span></span> | <span data-ttu-id="31029-113">De eerste keer dat u opent de [Azure Active Directory-blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) of gebruik de [rapportage-API's](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="31029-113">The first time you open the [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use the [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="31029-114">**V: waarop uw activiteitsgegevens beschikbaar is in de Azure-portal?**</span><span class="sxs-lookup"><span data-stu-id="31029-114">**Q: When is your activity data available in the Azure portal?**</span></span>

<span data-ttu-id="31029-115">**A:**</span><span class="sxs-lookup"><span data-stu-id="31029-115">**A:**</span></span>

- <span data-ttu-id="31029-116">**Onmiddellijk** : als u al met rapporten in de klassieke Azure portal werkt</span><span class="sxs-lookup"><span data-stu-id="31029-116">**Immediately** - If you have already been working with reports in the Azure classic portal</span></span>
- <span data-ttu-id="31029-117">**Binnen 2 uur** : als u dit nog niet hebt ingeschakeld rapportage in de klassieke Azure portal</span><span class="sxs-lookup"><span data-stu-id="31029-117">**Within 2 hours** - If you haven’t turned reporting on  in the Azure classic portal</span></span>

---
<span data-ttu-id="31029-118">**V: hoe kunt u de verzameling van beveiliging signalen gestart ophalen?**</span><span class="sxs-lookup"><span data-stu-id="31029-118">**Q: How can you get the collection of security signals started?**</span></span>  

<span data-ttu-id="31029-119">**A:** voor beveiliging opgeven, een verzamelingsproces wordt gestart wanneer u zich aanmelden bij gebruik van het Identity Protection Center.</span><span class="sxs-lookup"><span data-stu-id="31029-119">**A:** For security signals, the collection process starts when you opt-in to use the Identity Protection Center.</span></span> 


---
<span data-ttu-id="31029-120">**V: hoe lang de verzamelde gegevens opgeslagen?**</span><span class="sxs-lookup"><span data-stu-id="31029-120">**Q: For how long is the collected data stored?**</span></span>

<span data-ttu-id="31029-121">**A:**</span><span class="sxs-lookup"><span data-stu-id="31029-121">**A:**</span></span>

<span data-ttu-id="31029-122">**Activiteitsrapporten**</span><span class="sxs-lookup"><span data-stu-id="31029-122">**Activity reports**</span></span>    

| <span data-ttu-id="31029-123">Rapport</span><span class="sxs-lookup"><span data-stu-id="31029-123">Report</span></span>                 | <span data-ttu-id="31029-124">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="31029-124">Azure AD Free</span></span> | <span data-ttu-id="31029-125">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="31029-125">Azure AD Premium P1</span></span> | <span data-ttu-id="31029-126">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="31029-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="31029-127">Directorycontrole</span><span class="sxs-lookup"><span data-stu-id="31029-127">Directory Audit</span></span>        | <span data-ttu-id="31029-128">7 dagen</span><span class="sxs-lookup"><span data-stu-id="31029-128">7 days</span></span>        | <span data-ttu-id="31029-129">30 dagen</span><span class="sxs-lookup"><span data-stu-id="31029-129">30 days</span></span>             | <span data-ttu-id="31029-130">30 dagen</span><span class="sxs-lookup"><span data-stu-id="31029-130">30 days</span></span>             |
| <span data-ttu-id="31029-131">Aanmeldingsactiviteit</span><span class="sxs-lookup"><span data-stu-id="31029-131">Sign-in Activity</span></span>       | <span data-ttu-id="31029-132">7 dagen</span><span class="sxs-lookup"><span data-stu-id="31029-132">7 days</span></span>        | <span data-ttu-id="31029-133">30 dagen</span><span class="sxs-lookup"><span data-stu-id="31029-133">30 days</span></span>             | <span data-ttu-id="31029-134">30 dagen</span><span class="sxs-lookup"><span data-stu-id="31029-134">30 days</span></span>             |

<span data-ttu-id="31029-135">**Beveiliging signalen**</span><span class="sxs-lookup"><span data-stu-id="31029-135">**Security Signals**</span></span>

| <span data-ttu-id="31029-136">Rapport</span><span class="sxs-lookup"><span data-stu-id="31029-136">Report</span></span>         | <span data-ttu-id="31029-137">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="31029-137">Azure AD Free</span></span> | <span data-ttu-id="31029-138">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="31029-138">Azure AD Premium P1</span></span> | <span data-ttu-id="31029-139">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="31029-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="31029-140">Gebruikers die risico lopen</span><span class="sxs-lookup"><span data-stu-id="31029-140">Users at risk</span></span>  | <span data-ttu-id="31029-141">7 dagen</span><span class="sxs-lookup"><span data-stu-id="31029-141">7 days</span></span>        | <span data-ttu-id="31029-142">30 dagen</span><span class="sxs-lookup"><span data-stu-id="31029-142">30 days</span></span>             | <span data-ttu-id="31029-143">90 dagen</span><span class="sxs-lookup"><span data-stu-id="31029-143">90 days</span></span>             |
| <span data-ttu-id="31029-144">Riskant aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="31029-144">Risky sign-ins</span></span> | <span data-ttu-id="31029-145">7 dagen</span><span class="sxs-lookup"><span data-stu-id="31029-145">7 days</span></span>        | <span data-ttu-id="31029-146">30 dagen</span><span class="sxs-lookup"><span data-stu-id="31029-146">30 days</span></span>             | <span data-ttu-id="31029-147">90 dagen</span><span class="sxs-lookup"><span data-stu-id="31029-147">90 days</span></span>             |

---
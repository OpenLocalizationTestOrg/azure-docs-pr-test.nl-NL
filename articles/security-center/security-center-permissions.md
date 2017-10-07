---
title: aaaPermissions in Azure Security Center | Microsoft Docs
description: In dit artikel wordt uitgelegd hoe Azure Security Center gebruikt voor toegang op basis van rollen besturingselement tooassign machtigingen toousers en identificeert Hallo toegestane acties voor elke rol.
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="a45f6-103">Machtigingen in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="a45f6-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="a45f6-104">Maakt gebruik van Azure Security Center [op rollen gebaseerde toegangsbeheer (RBAC)](../active-directory/role-based-access-control-configure.md), waarmee u [ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md) die kunnen worden toegewezen toousers, groepen en services in Azure.</span><span class="sxs-lookup"><span data-stu-id="a45f6-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned toousers, groups, and services in Azure.</span></span>

<span data-ttu-id="a45f6-105">Security Center beoordeelt Hallo-configuratie van uw resources tooidentify beveiligingsproblemen en beveiligingsproblemen.</span><span class="sxs-lookup"><span data-stu-id="a45f6-105">Security Center assesses hello configuration of your resources tooidentify security issues and vulnerabilities.</span></span> <span data-ttu-id="a45f6-106">In Security Center, ziet u alleen informatie gerelateerd tooa resource wanneer u Hallo rol van eigenaar, bijdrager of lezer Hallo abonnement of resourcegroep beheergroep die deel uitmaakt van een resource te worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a45f6-106">In Security Center, you only see information related tooa resource when you are assigned hello role of Owner, Contributor, or Reader for hello subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="a45f6-107">In aanvulling toothese rollen zijn er twee specifieke Security Center-rollen:</span><span class="sxs-lookup"><span data-stu-id="a45f6-107">In addition toothese roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="a45f6-108">**Beveiliging lezer**: een gebruiker die deel uitmaakt van de rol toothis heeft rechten tooSecurity Center weer te geven.</span><span class="sxs-lookup"><span data-stu-id="a45f6-108">**Security Reader**: A user that belongs toothis role has viewing rights tooSecurity Center.</span></span> <span data-ttu-id="a45f6-109">Hallo-gebruiker kunt bekijken aanbevelingen, waarschuwingen, een beveiligingsbeleid en beveiliging, maar geen wijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="a45f6-109">hello user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="a45f6-110">**Beveiligingsbeheerder**: een gebruiker die deel uitmaakt van de rol toothis Hallo dezelfde als Hallo beveiliging lezer rechten heeft en kan ook bijwerken Hallo-beveiligingsbeleid en negeren van waarschuwingen en aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="a45f6-110">**Security Administrator**: A user that belongs toothis role has hello same rights as hello Security Reader and can also update hello security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="a45f6-111">Hallo beveiligingsrollen, beveiliging lezer en Beveiligingsbeheerder, hebben toegang alleen in Security Center.</span><span class="sxs-lookup"><span data-stu-id="a45f6-111">hello security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="a45f6-112">Hallo beveiligingsrollen hebt geen toegang tooother servicegebieden van Azure zoals opslag, Web & mobiele of Internet der dingen.</span><span class="sxs-lookup"><span data-stu-id="a45f6-112">hello security roles do not have access tooother service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="a45f6-113">Functies en de toegestane acties</span><span class="sxs-lookup"><span data-stu-id="a45f6-113">Roles and allowed actions</span></span>

<span data-ttu-id="a45f6-114">Hallo volgende tabel geeft de rollen en toegestane acties in Security Center.</span><span class="sxs-lookup"><span data-stu-id="a45f6-114">hello following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="a45f6-115">Een X geeft aan dat het Hallo-actie is toegestaan voor die rol.</span><span class="sxs-lookup"><span data-stu-id="a45f6-115">An X indicates that hello action is allowed for that role.</span></span>

| <span data-ttu-id="a45f6-116">Rol</span><span class="sxs-lookup"><span data-stu-id="a45f6-116">Role</span></span> | <span data-ttu-id="a45f6-117">Beveiligingsbeleid bewerken</span><span class="sxs-lookup"><span data-stu-id="a45f6-117">Edit security policy</span></span> | <span data-ttu-id="a45f6-118">Aanbevelingen voor beveiliging voor een resource toepassen</span><span class="sxs-lookup"><span data-stu-id="a45f6-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="a45f6-119">Negeren van waarschuwingen en aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="a45f6-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="a45f6-120">Waarschuwingen weergeven en aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="a45f6-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="a45f6-121">De eigenaar van abonnement</span><span class="sxs-lookup"><span data-stu-id="a45f6-121">Subscription Owner</span></span> | <span data-ttu-id="a45f6-122">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-122">X</span></span> | <span data-ttu-id="a45f6-123">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-123">X</span></span> | <span data-ttu-id="a45f6-124">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-124">X</span></span> | <span data-ttu-id="a45f6-125">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-125">X</span></span> |
| <span data-ttu-id="a45f6-126">Abonnement Inzender</span><span class="sxs-lookup"><span data-stu-id="a45f6-126">Subscription Contributor</span></span> | <span data-ttu-id="a45f6-127">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-127">X</span></span> | <span data-ttu-id="a45f6-128">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-128">X</span></span> | <span data-ttu-id="a45f6-129">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-129">X</span></span> | <span data-ttu-id="a45f6-130">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-130">X</span></span> |
| <span data-ttu-id="a45f6-131">De eigenaar van de resourcegroep</span><span class="sxs-lookup"><span data-stu-id="a45f6-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="a45f6-132">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-132">X</span></span> | -- | <span data-ttu-id="a45f6-133">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-133">X</span></span> |
| <span data-ttu-id="a45f6-134">Resourcegroep Inzender</span><span class="sxs-lookup"><span data-stu-id="a45f6-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="a45f6-135">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-135">X</span></span> | -- | <span data-ttu-id="a45f6-136">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-136">X</span></span> |
| <span data-ttu-id="a45f6-137">Lezer</span><span class="sxs-lookup"><span data-stu-id="a45f6-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="a45f6-138">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-138">X</span></span> |
| <span data-ttu-id="a45f6-139">Beveiligingsbeheerder</span><span class="sxs-lookup"><span data-stu-id="a45f6-139">Security Administrator</span></span> | <span data-ttu-id="a45f6-140">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-140">X</span></span> | -- | <span data-ttu-id="a45f6-141">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-141">X</span></span> | <span data-ttu-id="a45f6-142">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-142">X</span></span> |
| <span data-ttu-id="a45f6-143">Beveiliging lezer</span><span class="sxs-lookup"><span data-stu-id="a45f6-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="a45f6-144">X</span><span class="sxs-lookup"><span data-stu-id="a45f6-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="a45f6-145">Het is raadzaam dat u Hallo toewijst minimaal rol die nodig zijn voor gebruikers toocomplete hun taken.</span><span class="sxs-lookup"><span data-stu-id="a45f6-145">We recommend that you assign hello least permissive role needed for users toocomplete their tasks.</span></span> <span data-ttu-id="a45f6-146">Bijvoorbeeld toewijzen Hallo lezer rol toousers die alleen tooview informatie over de beveiligingsstatus Hallo van een resource nodig hebt, maar geen actie uitvoert, zoals het toepassen van aanbevelingen of het bewerken van beleid.</span><span class="sxs-lookup"><span data-stu-id="a45f6-146">For example, assign hello Reader role toousers who only need tooview information about hello security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="a45f6-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a45f6-147">Next steps</span></span>
<span data-ttu-id="a45f6-148">Dit artikel uitgelegd hoe Security Center RBAC tooassign machtigingen toousers gebruikt en geïdentificeerd Hallo toegestane acties voor elke rol.</span><span class="sxs-lookup"><span data-stu-id="a45f6-148">This article explained how Security Center uses RBAC tooassign permissions toousers and identified hello allowed actions for each role.</span></span> <span data-ttu-id="a45f6-149">Nu u bekend met de roltoewijzingen Hallo nodig toomonitor Hallo beveiligingsstatus van uw abonnement bent, beveiligingsbeleid, bewerken en toepassen van aanbevelingen, informatie over hoe:</span><span class="sxs-lookup"><span data-stu-id="a45f6-149">Now that you're familiar with hello role assignments needed toomonitor hello security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="a45f6-150">Instellen van beveiligingsbeleid in Security Center</span><span class="sxs-lookup"><span data-stu-id="a45f6-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="a45f6-151">Aanbevelingen voor beveiliging in Security Center beheren</span><span class="sxs-lookup"><span data-stu-id="a45f6-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="a45f6-152">Hallo beveiligingsstatus van uw Azure-resources bewaken</span><span class="sxs-lookup"><span data-stu-id="a45f6-152">Monitor hello security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="a45f6-153">Beheren en hierop reageren toosecurity waarschuwingen in Security Center</span><span class="sxs-lookup"><span data-stu-id="a45f6-153">Manage and respond toosecurity alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="a45f6-154">Bewaken van beveiligingsoplossingen van partners</span><span class="sxs-lookup"><span data-stu-id="a45f6-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)

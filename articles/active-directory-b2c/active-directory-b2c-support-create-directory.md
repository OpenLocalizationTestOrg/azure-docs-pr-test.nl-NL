---
title: 'Azure Active Directory B2C: Oplossen maken tenants | Microsoft Docs'
description: Problemen en oplossingen voor het maken van een Azure Active Directory of Azure Active Directory B2C-tenant.
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 7ba4c6b2-161b-45b5-b3bd-ccb662f5d7a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 81af4536fc223319369aff262d42149cfbf1a1e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="afd6b-103">Problemen met een Azure Active Directory of Azure Active Directory B2C-tenant maken</span><span class="sxs-lookup"><span data-stu-id="afd6b-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="afd6b-104">Een Azure AD-tenant maken</span><span class="sxs-lookup"><span data-stu-id="afd6b-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="afd6b-105">Als u een tenant van Azure Active Directory (Azure AD) op de eerste poging maken kunt, probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="afd6b-105">If you can't create an Azure Active Directory (Azure AD) tenant on the first attempt, try again.</span></span> <span data-ttu-id="afd6b-106">Als het probleem zich blijft voordoen, neem dan contact op met ondersteuning van Azure.</span><span class="sxs-lookup"><span data-stu-id="afd6b-106">If the problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="afd6b-107">Een Azure AD B2C-tenant maken</span><span class="sxs-lookup"><span data-stu-id="afd6b-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="afd6b-108">Als u problemen ondervindt wanneer u [maken van een Azure Active Directory B2C-tenant (Azure AD B2C)](active-directory-b2c-get-started.md), probeert u de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="afd6b-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try the following options:</span></span>

* <span data-ttu-id="afd6b-109">Als de Azure AD B2C-tenant niet in de lijst met tenants weergegeven, probeer het opnieuw maken van de tenant.</span><span class="sxs-lookup"><span data-stu-id="afd6b-109">If the Azure AD B2C tenant doesn't show up in your list of tenants, try again to create the tenant.</span></span>
* <span data-ttu-id="afd6b-110">Als de Azure AD B2C-tenant wordt weergegeven in de lijst met tenants en u het volgende foutbericht weergegeven ziet, de tenant verwijderen en opnieuw maken:</span><span class="sxs-lookup"><span data-stu-id="afd6b-110">If the Azure AD B2C tenant does show up in your list of tenants and you see the following  error message, delete the tenant and create it again:</span></span>

    <span data-ttu-id="afd6b-111">"Kan het maken van de B2C-tenant 'contosob2c' niet voltooien.</span><span class="sxs-lookup"><span data-stu-id="afd6b-111">"Could not complete the creation of the B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="afd6b-112">Ga naar dit [koppeling](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) voor meer informatie. "</span><span class="sxs-lookup"><span data-stu-id="afd6b-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="afd6b-113">Er zijn bekende problemen wanneer u een bestaande Azure AD B2C-tenant verwijderen en opnieuw maken met behulp van dezelfde domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="afd6b-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using the same domain name.</span></span> <span data-ttu-id="afd6b-114">Wanneer u een nieuwe Azure AD B2C-tenant maakt, moet u een andere domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="afd6b-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="afd6b-115">Als deze oplossingen niet werken, moet u contact op met ondersteuning van Azure.</span><span class="sxs-lookup"><span data-stu-id="afd6b-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="afd6b-116">Zie voor meer informatie [bestand ondersteuningsaanvragen voor Azure AD B2C](active-directory-b2c-support.md).</span><span class="sxs-lookup"><span data-stu-id="afd6b-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>


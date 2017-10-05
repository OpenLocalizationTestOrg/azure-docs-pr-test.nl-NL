---
title: Azure API Management Developer Portal sjablonen | Microsoft Docs
description: Informatie over het aanpassen van de inhoud van developer portal-pagina's met behulp van een set van sjablonen in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 5189f3d8-2a4c-4dc8-ab19-11c7df0114d4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: dc3f32a3cff2e66a798bd8f6c19c6b56a47643ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-developer-portal-templates"></a><span data-ttu-id="9a917-103">Azure API Management Developer Portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="9a917-103">Azure API Management Developer Portal Templates</span></span>
<span data-ttu-id="9a917-104">Azure API Management biedt de mogelijkheid voor het aanpassen van de inhoud van developer portal-pagina's met behulp van een set van sjablonen die hun inhoud configureren.</span><span class="sxs-lookup"><span data-stu-id="9a917-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="9a917-105">Met behulp van [DotLiquid](http://dotliquidmarkup.org/) syntaxis en de editor van uw keuze, zoals [DotLiquid voor ontwerpers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), en een opgegeven set gelokaliseerde [resources String](api-management-template-resources.md#strings), [Glyph-resources](api-management-template-resources.md#glyphs), en [pagina besturingselementen](api-management-page-controls.md), hebt u aanzienlijke flexibiliteit voor het configureren van de inhoud van de pagina's naar wens met behulp van deze sjablonen.</span><span class="sxs-lookup"><span data-stu-id="9a917-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="9a917-106">Zie voor meer informatie over het werken met sjablonen [het aanpassen van de API Management portal voor ontwikkelaars met behulp van sjablonen](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9a917-106">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  



  
##  <span data-ttu-id="9a917-107"><a name="DeveloperPortalTemplates"></a>Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="9a917-107"><a name="DeveloperPortalTemplates"></a> Developer portal templates</span></span>  
  
-   [<span data-ttu-id="9a917-108">API's</span><span class="sxs-lookup"><span data-stu-id="9a917-108">APIs</span></span>](api-management-api-templates.md)  
    -   [<span data-ttu-id="9a917-109">API-lijst</span><span class="sxs-lookup"><span data-stu-id="9a917-109">API list</span></span>](api-management-api-templates.md#APIList)  
    -   [<span data-ttu-id="9a917-110">Bewerking</span><span class="sxs-lookup"><span data-stu-id="9a917-110">Operation</span></span>](api-management-api-templates.md#Product)  
    -   [<span data-ttu-id="9a917-111">Codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="9a917-111">Code samples</span></span>](api-management-api-templates.md#CodeSamples)  
        -   [<span data-ttu-id="9a917-112">CURL</span><span class="sxs-lookup"><span data-stu-id="9a917-112">Curl</span></span>](api-management-api-templates.md#Curl)  
        -   [<span data-ttu-id="9a917-113">C#</span><span class="sxs-lookup"><span data-stu-id="9a917-113">C#</span></span>](api-management-api-templates.md#CSharp)  
        -   [<span data-ttu-id="9a917-114">Java</span><span class="sxs-lookup"><span data-stu-id="9a917-114">Java</span></span>](api-management-api-templates.md#Stub)  
        -   [<span data-ttu-id="9a917-115">JavaScript</span><span class="sxs-lookup"><span data-stu-id="9a917-115">JavaScript</span></span>](api-management-api-templates.md#JavaScript)  
        -   [<span data-ttu-id="9a917-116">Objective-C</span><span class="sxs-lookup"><span data-stu-id="9a917-116">Objective C</span></span>](api-management-api-templates.md#ObjectiveC)  
        -   [<span data-ttu-id="9a917-117">PHP</span><span class="sxs-lookup"><span data-stu-id="9a917-117">PHP</span></span>](api-management-api-templates.md#PHP)  
        -   [<span data-ttu-id="9a917-118">Python</span><span class="sxs-lookup"><span data-stu-id="9a917-118">Python</span></span>](api-management-api-templates.md#Python)  
        -   [<span data-ttu-id="9a917-119">Ruby</span><span class="sxs-lookup"><span data-stu-id="9a917-119">Ruby</span></span>](api-management-api-templates.md#Ruby)  
-   [<span data-ttu-id="9a917-120">Producten</span><span class="sxs-lookup"><span data-stu-id="9a917-120">Products</span></span>](api-management-product-templates.md)  
    -   [<span data-ttu-id="9a917-121">Lijst met producten</span><span class="sxs-lookup"><span data-stu-id="9a917-121">Product list</span></span>](api-management-product-templates.md#ProductList)  
    -   [<span data-ttu-id="9a917-122">Product</span><span class="sxs-lookup"><span data-stu-id="9a917-122">Product</span></span>](api-management-product-templates.md#Product)  
-   [<span data-ttu-id="9a917-123">Toepassingen</span><span class="sxs-lookup"><span data-stu-id="9a917-123">Applications</span></span>](api-management-application-templates.md)  
    -   [<span data-ttu-id="9a917-124">Lijst met toepassingen</span><span class="sxs-lookup"><span data-stu-id="9a917-124">Application list</span></span>](api-management-application-templates.md#ProductList)  
    -   [<span data-ttu-id="9a917-125">Toepassing</span><span class="sxs-lookup"><span data-stu-id="9a917-125">Application</span></span>](api-management-application-templates.md#Application)  
-   [<span data-ttu-id="9a917-126">Problemen</span><span class="sxs-lookup"><span data-stu-id="9a917-126">Issues</span></span>](api-management-issue-templates.md)  
    -   [<span data-ttu-id="9a917-127">Lijst met kwesties</span><span class="sxs-lookup"><span data-stu-id="9a917-127">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
-   [<span data-ttu-id="9a917-128">Gebruikersprofiel</span><span class="sxs-lookup"><span data-stu-id="9a917-128">User Profile</span></span>](api-management-user-profile-templates.md)  
    -   [<span data-ttu-id="9a917-129">Profiel</span><span class="sxs-lookup"><span data-stu-id="9a917-129">Profile</span></span>](api-management-user-profile-templates.md#Profile)  
    -   [<span data-ttu-id="9a917-130">Abonnementen</span><span class="sxs-lookup"><span data-stu-id="9a917-130">Subscriptions</span></span>](api-management-user-profile-templates.md#Subscriptions)  
    -   [<span data-ttu-id="9a917-131">Toepassingen</span><span class="sxs-lookup"><span data-stu-id="9a917-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
    -   [<span data-ttu-id="9a917-132">Update-accountgegevens</span><span class="sxs-lookup"><span data-stu-id="9a917-132">Update account info</span></span>](api-management-user-profile-templates.md#UpdateAccountInfo)  
-   [<span data-ttu-id="9a917-133">Pagina's</span><span class="sxs-lookup"><span data-stu-id="9a917-133">Pages</span></span>](api-management-page-templates.md)  
    -   [<span data-ttu-id="9a917-134">Aanmelden</span><span class="sxs-lookup"><span data-stu-id="9a917-134">Sign in</span></span>](api-management-page-templates.md#SignIn)  
    -   [<span data-ttu-id="9a917-135">Aanmelden</span><span class="sxs-lookup"><span data-stu-id="9a917-135">Sign up</span></span>](api-management-page-templates.md#SignUp)  
    -   [<span data-ttu-id="9a917-136">Pagina is niet gevonden</span><span class="sxs-lookup"><span data-stu-id="9a917-136">Page not found</span></span>](api-management-page-templates.md#PageNotFound)


## <a name="next-steps"></a><span data-ttu-id="9a917-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9a917-137">Next steps</span></span>  
-   [<span data-ttu-id="9a917-138">Verwijzing naar de sjabloon</span><span class="sxs-lookup"><span data-stu-id="9a917-138">Template reference</span></span>](api-management-developer-portal-templates-reference.md)  
-   [<span data-ttu-id="9a917-139">Naslaginformatie over gegevensmodellen</span><span class="sxs-lookup"><span data-stu-id="9a917-139">Data model reference</span></span>](api-management-template-data-model-reference.md)  
-   [<span data-ttu-id="9a917-140">Paginabesturingselementen</span><span class="sxs-lookup"><span data-stu-id="9a917-140">Page controls</span></span>](api-management-page-controls.md)  
-   [<span data-ttu-id="9a917-141">Sjabloonresources</span><span class="sxs-lookup"><span data-stu-id="9a917-141">Template resources</span></span>](api-management-template-resources.md)